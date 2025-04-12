+++
title = "Automatizando postagens no pixelfed"
date = 2025-04-12T16:36:28-03:00
draft =  true
tags = ["tech", "posse", "fediverso", "python"]
[comments]
host = "bolha.us"
username = "dunossauro"
+++

Tenho trabalhado nos últimos tempos em uma forma de postar meus conteúdos na minha página e sindicar o conteúdo nas redes sociais ([POSSE](https://indieweb.org/POSSE)). Nessa experiência, tenho desenvolvido em vagarosidade glacial o [sociopyta](https://codeberg.org/dunossauro/sociopyta/). Na grande maioria dos casos, temos APIs de documentação ou bibliotecas prontas para fazer isso.

No caso do [pixelfed](https://pixelfed.org/), não temos nem documentação, nem bibliotecas :)

> Esse post é sobre um "trabalho investigativo" em código-fonte alheio. Você pode pular para [# solução](#solução) e ver como fazer a automação dos seus posts ;)

## Iniciando a jornada

Então lá fui eu desbravar o código-fonte em PHP do servidor do pixelfed, mesmo que meu conhecimento em PHP seja... Vamos dizer... Pífio.

O fonte do controller da API do pixelfed pode ser encontrado [aqui](https://github.com/pixelfed/pixelfed/blob/eb5bb9fede5f294f8c5facdaebd4471fa8e3b3fc/app/Http/Controllers/Api/ApiV1Controller.php).

Ao iniciar a minha jornada, procurei por algo que criasse uma postagem. Acabei encontrando [`statusCreate`](https://github.com/pixelfed/pixelfed/blob/eb5bb9fede5f294f8c5facdaebd4471fa8e3b3fc/app/Http/Controllers/Api/ApiV1Controller.php#L2901).

Nesse endpoint fica evidente que deve ser feito um post para `/api/v1/statuses` usando `json` com algumas opções no corpo. Vou destacar as que me interessam, você pode ver as outras no código-fonte:

- `status`: O texto que acompanhará a publicação das fotos
- `media_ids`: Os IDs das fotos/vídeos que já foram enviados ao servidor
  - Sim... Isso precisa ser feito antes!
- [e mais ...](https://github.com/pixelfed/pixelfed/blob/eb5bb9fede5f294f8c5facdaebd4471fa8e3b3fc/app/Http/Controllers/Api/ApiV1Controller.php#L2909)

O que nos daria um request parecido com esse (vou usar [curl](https://curl.se/) por considerar "universal", mas no final vou fazer tudo usando [httpx](https://www.python-httpx.org/)):

```bash
curl -X POST "{sua-instancia}/api/v1/statuses" \
  -H "Accept: application/json" \
  -F "status={seu-texto}" \
  -F "media_ids[]={media-id-1}" \
  -F "media_ids[]={media-id-2}" \
  # adicione mais `-F "media_ids[]={...}"` conforme necessário
```

Ok... Temos um ponto de partida.


Agora precisamos descobrir como enviar as fotos. Encontrei uma função chamada [mediaUpload](https://github.com/pixelfed/pixelfed/blob/eb5bb9fede5f294f8c5facdaebd4471fa8e3b3fc/app/Http/Controllers/Api/ApiV1Controller.php#L1658). Provavelmente é esse... hahaha

O endpoint é `/api/v1/media` que recebe também um json. Com o field `file` junto com os bytes do arquivo de média. O que nos dá algo parecido com isso:

```bash
curl -X POST "{sua-instancia}/api/v1/media" \
  -H "Accept: application/json" \
  -F "file=@{caminho-do-arquivo}"
```

Beleza. Se tudo der certo, vamos conseguir fazer o upload de uma midia agora e depois criar a postagem, certo?

**ERRADO!**

### PAT

Para enviar essas requisições, você vai precisar de um token de acesso. O que pixelfed chama de PAT (Personal Access Tokens). Para gerar um PAT você deve ir em:

https://{sua-instancia}/settings/applications

Existem duas sessões. Vá em ` Personal Access Tokens `, clique em `Create New Token`, dê um nome para esse token e dê acesso de `write`. Isso irá gerar um token enorme. Salve ele, **ele nunca mais vai ser visível**!

### Uma nova tentativa

Agora podemos tentar de novo:

```bash
curl -X POST "{sua-instancia}/api/v1/media" \
  -H "Authorization: Bearer {PAT}" \
  -H "Accept: application/json" \
  -F "file=@{caminho-do-arquivo}"
```

YAY! Temos nossa media no servidor. O json de resposta em um field chamada `id`. Ele é o que devemos usar para criar a postagem.

> Se você, assim como eu, for nerd de HTTP vai perceber que a resposta é `200 OK` e não `201 CREATED` e está tudo certo... `200` é que deu certo... Supere!


Agora que temos o `id`, podemos criar a postagem:

```bash
curl -X POST "{sua-instancia}/api/v1/statuses" \
  -H "Accept: application/json" \
  -H "Authorization: Bearer {PAT}" \
  -F "status={seu-texto}" \
  -F "media_ids[]={media-id}"
```

YAY! [2]. Temos nossa postagem no pixelfed. O field `uri` é o link da nossa postagem. Com isso, a nossa jornada investigativa termina.

> Novamente, 200, meu coração chora. Mas, vou superar.


## Solução

Embora tenha sido chato ler código-fonte, a solução que eu queria para o [sociopyta](https://codeberg.org/dunossauro/sociopyta/) é bastante simples... Após pegar o [PAT](#pat) precisamos somente fazer uma requisição para cada imagem e um para criar a postagem:

```python
from pathlib import Path

import httpx


def post(text: str, images: list[Path], config) -> tuple[str, str]:
    base_url = config.pixelfed.api_base_url
    access_token = config.pixelfed.access_token

	post_url = f'{base_url}/api/v1/statuses'
	headers = {
		'Authorization': f'Bearer {access_token}',
		'Accept': 'application/json',
	}

	data = {
		'status': text,
		'media_ids[]': [
			upload_media(image, base_url, access_token) for image in images
		],
	}

	response = httpx.post(post_url, headers=headers, data=data)
	return 'pixelfed', response.json()['uri']


def upload_media(media: Path, instance: str, pat: str) -> str:
    media_url = f'{instance}/api/v1/media'
    headers = {'Authorization': f'Bearer {pat}', 'Accept': 'application/json'}
    response = httpx.post(
	    media_url,
		headers=headers,
		files={'file': media.read_bytes()}
	)

    return response.json()['id']
```

Agora, o que você vai fazer com essas funções é muito particular. Essas duas funções fazem somente o post, agora dentro do seu contexto de automação você deve chamá-las...
