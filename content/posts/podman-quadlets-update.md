+++
title = "Podman, Quadlets e updates automáticos"
date = 2026-10-23T19:32:25-03:00
tags = ['homelab', 'gnu/linux', 'tech', 'podman']
[comments]
host = "bolha.us"
username = "dunossauro"
id = 117492668785291658
+++


> Ps: esse post não é uma introdução ao podman, menos ainda ao systemd

Uma das coisas mais interessantes no [podman](https://podman.io/) é a capacidade de executar containers nativamente no [systemd](https://www.freedesktop.org/software/systemd/man/latest/systemd.html) e, de quebra, os serviços ainda podem ser atualizados automaticamente via serviços do próprio podman + systemd.

## Uma ideia de fluxo

Imagine que você é um cliente ou desenvolve uma aplicação que solta atualizações constantes em registros. Por exemplo, aqui no meu homelab costumo usar alguns serviços, ao mesmo tempo em que desenvolvo alguns outros.

Um caso concreto que tenho aqui é meu laboratório de observabilidade com opentelemetry. Uso basicamente 5 imagens:

- Opentelemetry-contrib
- VictoriaMetrics
- VictoriaLogs
- VictoriaTraces
- Perses dashboard

Acompanho o feed RSS[^1] desses serviços pra sempre saber quando sai uma release nova. E toda vez que uma nova release é lançada de cada um desses serviços, tenho que ir no [LXC](https://linuxcontainers.org/lxc/introduction/) que contém todas as minhas aplicações de observabilidade e atualizar o que saiu de novo.

[^1]: Via página de releases no github mesmo "github.com/user/projeto/releases.atom"

Isso não é necessariamente ruim, afinal leio os changelogs e sempre acabo vendo alguma novidade, possibilidades novas, etc. Mas, sendo totalmente sincero, a maioria esmagadora das vezes as releases têm somente fixes (X.X.AQUI) e, às vezes... mais de um por dia ;)

A ideia desse post é tentar contar como resolvi esse problema de updates fazendo o podman atualizar sozinho. Se quebrar uma vez ou outra, tudo bem, posso intervir, mas não preciso fazer isso sempre, a toda nova release.

> Como dei o exemplo do laboratório de observabilidade, a gente pode fazer outro post focado especialmente nele e na construção desses containers. Mas hoje quero focar no mecanismo de atualizações.

## Quadlets, quando o podman encontra o systemd

Vamos imaginar uma imagem genérica que alguém fez push em algum registry, vamos chamar ela de `blah` em sua última versão `:latest`.

O [Quadlet](https://docs.podman.io/en/latest/markdown/podman-quadlet.1.html) é uma forma de manusear containers[^2] declarativamente usando systemd [unit files](https://www.freedesktop.org/software/systemd/man/systemd.unit.html).

[^2]: volumes, redes, etc... tudo que o podman pode gerenciar

Mas, no lugar de criar um `[Service]`, criamos um `[Container]`. Vamos imaginar um `blah.container`:

```ini
[Unit]
Description=Blah, uma API boladona :)

[Container] # a parte importante aqui!
Image=192.168.15.11:3000/dunossauro/blah:latest
PublishPort=8000:8000
Volume=/home/dunossauro/pods/quadlets/blah/config.yaml:/etc/blah/config.yaml
Volume=/home/dunossauro/pods/quadlets/blah/config2.yaml:/etc/blah/config2.yaml

[Service]
Restart=always

[Install]
WantedBy=default.target
```

Para começar, temos dois parâmetros principais:

- `Image`: descreve o registry, a imagem e a versão. Por exemplo, se quisermos usar a imagem do python 3.15 disponível no dockerhub, usaríamos algo como `Image=docker.io/python:3.15`
- `PublishPort`: descreve qual porta do container será mapeada para a máquina local.

De forma adicional, se precisar de um volume, você pode adicionar um:

- `Volume`: descreve quais arquivos serão compartilhados no volume do container. Uma coisa importante aqui é que os arquivos locais precisam necessariamente ser full path, pois isso é um serviço rodando no sistema.

Com esse "unit container" dizemos ao podman que queremos instalar ele:

```bash
$ podman quadlet install blah.container
/home/dunossauro/.config/containers/systemd/blah.container
```

> Dica: se precisar sobrescrever o arquivo depois de alterar, use a flag `-r` (`replace`) para atualizar o unit gerado.

E com esse comando ele vai criar um diretório de containers para seu user `~/.config/containers/systemd/` e adicionar `blah.container` lá.

Agora, recarregamos a configuração do systemd:

```bash
systemctl --user daemon-reload
```

E temos os serviços de containers já disponíveis para uso:


```bash
$ systemctl status --user blah
○ blah.service - blah api
     Loaded: loaded (/home/dunossauro/.config/containers/systemd/blah.container; generated)
     Active: inactive (dead)
```

Se tudo estiver certo, podemos iniciar:

```bash
systemctl start --user blah
```

Como esse comando não gera output quando dá certo:

```bash
○ → systemctl status --user blah
● blah.service - blah api
     Loaded: loaded (/home/dunossauro/.config/containers/systemd/blah.container; generated)
     Active: active (running) since Thu 2026-10-15 16:55:24 -03; 41s ago
 Invocation: 340e2d1506144489a76a7e1d3cb991b0
   Main PID: 57516 (conmon)
      Tasks: 7 (limit: 37972)
     Memory: 139.9M (peak: 143M)
        CPU: 1.520s
     CGroup: /user.slice/user-1000.slice/user@1000.service/app.slice/blah.service
             ├─libpod-payload-9803c2ae6198debc965a501a890099113eb60e3f75af489226803a7eaa7a82df
             │ └─57530 /usr/local/bin/python3.15 /usr/local/bin/fastapi run --host 0.0.0.0 blah/app.py
             └─runtime
               ├─57511 /usr/bin/pasta --config-net -t 8000-8000:8000-8000 --dns-forward 169.254.1.1 -u none ->               └─57516 /usr/bin/conmon --api-version 1 -c 9803c2ae6198debc965a501a890099113eb60e3f75af4892268>
out 15 16:55:26 melville systemd-blah[57516]:  🌐 Server started at http://0.0.0.0:8000
out 15 16:55:26 melville systemd-blah[57516]:     Documentation at http://0.0.0.0:8000/docs
out 15 16:55:26 melville systemd-blah[57516]:
out 15 16:55:26 melville systemd-blah[57516]:   Logs:
```

YAY! Temos nossa incrível blah api rodando.

## Beleza, mas como isso atualiza sozinho?

Isso é feito com uma junção de três coisinhas:

- O "container unit" precisa de duas configurações:
  - O parâmetro: `AutoUpdate`; e
  - A versão não pode estar pinada, vamos usar `:latest`, mas poderia `:lts-alpine` por exemplo
- O serviço systemd de update do podman: `podman-auto-update.service`
- O timer systemd de update do podman: `podman-auto-update.timer`

Começando pelo `blah.container`:

```ini
...

[Container]
Image=192.168.15.11:3000/dunossauro/blah:latest
PublishPort=8000:8000
Volume=/home/dunossauro/pods/quadlets/blah/config.yaml:/etc/blah/config.yaml
Volume=/home/dunossauro/pods/quadlets/blah/config2.yaml:/etc/blah/config2.yaml
AutoUpdate=registry

...
```

Neste exemplo, vamos usar `:latest`[^3] afinal, se queremos atualizações, não podemos travar a versão, e o `AutoUpdate` recebe `registry` pois é de lá que ele deve buscar as novas versões[^4].

[^3]: Poderia ser qualquer tag mutável, como :latest ou :lts-alpine. Tags de versão, como :3.1.18, também podem mudar, embora normalmente sejam mantidas fixas. Para garantir a referência a uma imagem específica, use um digest.
[^4]: Você também pode usar `AutoUpdate=local` se quiser, aí quando existir uma imagem local mais nova, ele atualiza.


Com isso, damos um replace (`-r`) no nosso `.container`, fazendo ele pegar a configuração mais recente:

```bash
$ podman quadlet install -r blah.container
/home/dunossauro/.config/containers/systemd/blah.container
```

Como temos uma nova configuração, é interessante que você faça o restart no blah:

```bash
systemctl restart --user blah
```

Com o serviço rodando, podemos seguir para os outros serviços.


Aí entra o `podman-auto-update`, que é quem efetivamente executa o update. Ele precisa estar habilitado:

```bash
$ systemctl --user enable podman-auto-update.service
Created symlink '/home/dunossauro/.config/systemd/user/default.target.wants/podman-auto-update.service' → '/usr/lib/systemd/user/podman-auto-update.service'.
```

O serviço executa o processo de atualização quando é acionado. Quem agenda essas execuções é o timer, que dispara o serviço nos intervalos configurados.

Para saber quando ele vai executar, esse serviço tem um timer de systemd associado a ele, o `podman-auto-update.timer`. Que também precisa ser inicializado.

```bash
systemctl --user enable --now podman-auto-update.timer
```

Para consultar se esse timer foi ativado, você pode olhar a lista de timers:

```bash
systemctl --user list-timers
```

Por padrão, ele é executado diariamente (`OnCalendar=daily`), mas você pode alterar esse comportamento e colocar o tempo que desejar, usando a [sintaxe dos timers](https://www.freedesktop.org/software/systemd/man/latest/systemd.time.html#).

Para editar, você poderia fazer a reescrita do arquivo do service no systemd, ou somente lançar um edit (o que faremos):

```bash
systemctl edit --user podman-auto-update.timer
```

Por exemplo, vou deixar para rodar a cada minuto (`OnCalendar=*-*-* *:*:00`) para exemplificar, mas você deve ajustar como preferir:

```ini
[Unit]
Description=Podman auto-update timer

[Timer]
OnCalendar=*-*-* *:*:00
RandomizedDelaySec=30
Persistent=true

[Install]
WantedBy=timers.target
```

## Automático é ótimo, até falhar...

O que acontece nesses updates automáticos se alguma coisa falhar nessa nova `:latest`? Nunca se sabe, não é mesmo?

Pra isso, temos um mecanismo de health check no unit, para ele validar se está mesmo funcionando:

```ini
...

[Container]
Image=192.168.15.11:3000/dunossauro/blah:latest
# ...
AutoUpdate=registry
HealthCmd=curl -f http://localhost:8000/health || exit 1
HealthInterval=30s
HealthRetries=10
Notify=healthy

...
```

- `HealthCmd`: executa qualquer comando que você precise. No caso da "blah api", vamos fazer um curl, pra ver se ela responde. Importante dizer aqui é que o comando roda **no container**, logo ele teria que ter o curl.
- `HealthInterval`: define o intervalo entre as verificações de saúde do container.
- `HealthRetries`: define quantas falhas consecutivas são toleradas antes de o container ser considerado não saudável.
- `Notify=healthy`: adia a notificação de sucesso da inicialização do service ao systemd. Faz com que espere até que o container esteja saudável.

Com isso, quando o container subir, se não der certo após o update, o podman vai iniciar o processo de rollback para o hash anterior da mesma imagem.

Importante frisar aqui que sem adiar o `Notify`, a validação fica a cargo de entender se o container conseguiu ser inicializado. Ele poder ser inicializado sem estar saudável, por isso `Notify` é importante, pois, espera que ele esteja saudável antes de terminar o processo de atualização ou de rollback.

## Mas como os pods se comunicam?

Até agora vimos como subir um serviço isolado, mas, na vida real, nossos sistemas conversam com outras coisas: a API `blah` precisa bater num banco de dados, num cache ou, no meu caso da observabilidade, várias ferramentas trocando dados o tempo todo.

No mundo perfeito do Podman Quadlet, existe um arquivo `.network` (exatamente como o `.container`) que você cria para isolar os bichinhos em uma rede privada bridge, onde eles resolvem uns aos outros por DNS de forma limpa.

Mas quer saber a verdade? Se a sua `blah` api precisar consultar um banco de dados que está na máquina host, ou se você quiser simplificar as pontes sem gerenciar DNS interno de container, você pode apelar para o **`host.containers.internal`**.

Por exemplo, a string de conexão do banco na sua `blah` API apontaria direto para lá:

```env
DATABASE_URL=postgres://user:pass@host.containers.internal:5432/db
```

Por que não me estressei com redes customizadas para tudo? Porque mergulhar de cabeça em regras de roteamento, DNS interno do Podman ([`aardvark-dns`](https://github.com/containers/aardvark-dns)), isolamento e múltiplas redes bridge é um buraco negro tão profundo que daria um post inteiro só sobre isso.

## Conclusão

Isso facilita bastante o "configure e deixe rodando", perco menos tempo pensando sobre isso ou se deveria atualizar algo.

Claro, de tempos em tempos é legal dar uma olhada no `journalctl` da coisa e ver como anda. Se algum update está travado, se algo mudou que precisa ser corrigido na sua aplicação de tempos em tempos. Para aplicações, é interessante configurar alguma coisa de monitoramento, um alerta que seja, aí você sabe de verdade quando precisa intervir.

Toda essa minha pequena configuração de quadlets de observabilidade, meu problema inicial, está nesse [repo](https://codeberg.org/dunossauro/obs-pods) e você pode dar uma olhada.

Como você tem usado essas coisas? Me conta.
