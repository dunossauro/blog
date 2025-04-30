+++
title = "Experimentando o Lima (Linux Machines)"
date = 2025-04-30T10:40:35-03:00
tags = ['tech', 'gnu/linux']
[comments]
host = "bolha.us"
username = "dunossauro"
id = 114304592904815316
+++

Grande parte do meu trabalho, fora dos streams e vídeos, é dar suporte pra a comunidade. Eu tô sempre por ai, nos grupos da comunidade de python/emacs/GNU/linux, tentando ajudar da melhor maneira possível.

> Esse post estava no meu draft desde 2023. Não tinha absolutamente nada de interessante que fazia ele valer a pena para ser postado, depois [desse toot](https://bolha.us/@dunossauro/114395710915156940) achei que deveria postar!

## Meu problema de sempre

Uma das coisas mais complicadas pra mim é tentar reproduzir o ambiente de desenvolvimento de outras pessoas. "Ah... mas temos docker", faz um tempo que tenho evitado usar docker por conta das licenças absurdas que eles veem impondo aos usuários. Você poderia me dizer que temos o podman então... E você pode ter razão.

O meu grande problema com essas ferramentas é que elas não substituem uma máquina virtual. Bom... pra 99% das coisas, sim. Tirando que tenho que escrever um arquivo pra produzir um container. Mas, o problema começa quando preciso reproduzir o ambiente onde a pessoa executa o container. Fazer [DinD](https://www.docker.com/resources/docker-in-docker-containerized-ci-workflows-dockercon-2023/) ou [PiC](https://www.redhat.com/en/blog/podman-inside-container) não é a coisa mais simples do mundo, principalmente com o fato de que pra isso tenho que escrever um novo `Dockerfile`. Em tem várias imagens, portas... Definitivamente, isso não é prático.

Em vários momentos, opto por ter uma máquina virtual pra tentar executar essas coisas. Simplifica um pouco o contexto. Aí lá vou eu usar outra plataforma proprietária, como o vagrant cloud pra procurar a distribuição que a pessoa usa. Aí dá aquele frio na espinha e você vê que mesmo no [bento](https://portal.cloud.hashicorp.com/vagrant/discover/bento) a imagem não está disponível pra [libvirt](https://libvirt.org/). Legal, a gente vai de Virtualbox mesmo... (imagine a minha cara agora...). Faço o download da imagem, inicio, compartilho os arquivos com a VM, tenho que habilitar o guest, copia-e-cola unidirecional, montagem do path... Sim, isso dá **MUITO** trabalho e ocupa bastante espaço (o que às vezes eu não tenho).

## Lima

Após algumas buscas na interwebs em 2023, acabei conhecendo o [Lima](https://lima-vm.io/) [LInux MAchines] é uma ferramenta de linha de comando para criar sandboxes usando máquinas virtuais via CLI e com suporte a templates. Uma ferramenta bastante promissora, atualmente em estágio de [sandbox da cncf](https://www.cncf.io/sandbox-projects/) e com licença apache 2.0

Por baixo dos panos ele cria VMs [QEMU](https://www.qemu.org/) [no linux, BSDs...], [VZ](https://github.com/Code-Hex/vz) no MacOS e com [WSL2](https://learn.microsoft.com/pt-br/windows/wsl/about) no Windows.

Com um simples comando (e se necessário um arquivo yaml), temos uma VM funcional de [diversas distribuições](https://lima-vm.io/docs/templates/), SSH aberto, sistema de arquivos compartilhado (read-only por default) e redirecionamento de portas.

### Instalação

Para instalar, você pode ir ao guia de [instalação oficial](https://lima-vm.io/docs/installation/), mas um simples curl é o suficiente:

```bash
VERSION=$(curl -fsSL https://api.github.com/repos/lima-vm/lima/releases/latest | jq -r .tag_name)
curl -fsSL "https://github.com/lima-vm/lima/releases/download/${VERSION}/lima-${VERSION:1}-$(uname -s)-$(uname -m).tar.gz" | tar Cxzvm /usr/local
```

Como estou no arch, o pacote está disponível no [AUR](https://aur.archlinux.org/packages/lima). O que torna tudo mais simples:

```bash
paru -S lima
```

### Mostando a magia da linha de comando

Bom... Falamos, falamos... Como funciona?


```bash
$ limactl start default

? Creating an instance "default"  [Use arrows to move, type to filter]
> Proceed with the current configuration
  Open an editor to review or modify the current configuration
  Choose another template (docker, podman, archlinux, fedora, ...)
  Exit
```

> `default` é um template base rodando ubuntu. Já vem com suporte a conteinerd/nerdctl e LXD

Um enter e temos a VM rodando via QEMU.

#### Foi isso que me prometeram, mas não funcionou ;)

> caso o seu tenha, pule para [Usando o lima](#usando-o-lima)

O erro:

```bash
FATA[0030] exiting, status={Running:false Degraded:false Exiting:true Errors:[] SSHLocalPort:0} (hint: see "/home/dunossauro/.lima/default/ha.stderr.log")
```

Lendo o arquivo `/home/dunossauro/.lima/default/ha.stderr.log`, podemos ver o que aconteceu:

```json
{
    "level":"fatal",
	"msg":"could not find firmware for \"/usr/bin/qemu-system-x86_64\" (hint: try setting `firmware.legacyBIOS` to `true`)",
	"time":"2025-04-24T02:48:57-03:00"
}
```

Como tenho a bios em modo `legacy` e isso não combina com a configuração padrão do lima para o qemu, a configuração pode ser alterada na opção de abrir o editor:

```bash
$ limactl edit default  # abre seu editor de texto
```

A única alteração que precisa ser feita, é adicionar dizer que `legacyBIOS` é `true`:

```diff
firmware:
-  legacyBIOS: none
+  legacyBIOS: true
```

Salvando o arquivo, temos isso:

```bash
WARN[0000] treating lima version "d218ece" from "/home/dunossauro/.lima/default/lima-version" as very latest release
INFO[0022] Instance "default" configuration edited
? Do you want to start the instance now?  (Y/n)
```

Damos `Y` e vamos adiante:

---

### Usando o lima

Após alguns segundos...

```bash
# ...
INFO[0107] [hostagent] Starting QEMU
INFO[0108] SSH Local Port: 60022
# ...
INFO[0149] READY. Run `lima` to open the shell.
```

**YAY**, agora temos a VM do QEMU funcionando!

Usar o lima é bastante simples, só digitar `lima` e estamos conectados via SSH na VM:

```bash
$ lima
dunossauro@lima-default:/home/dunossauro$
```

Como estamos usando o template `default`, a VM é um ubuntu com o [containerd](https://containerd.io/) e o [nerdctl](https://github.com/containerd/nerdctl) instalado:

```bash
dunossauro@lima-default:/home/dunossauro$ nerdctl run -d -p 8080:80 --name nginx nginx:alpine
```

Pronto, temos um container do [NGINX](https://nginx.org/) rodando!

Podemos sair do SSH (`exit`) e também executar os comandos direto pelo lima. Como um update simples:

```bash
lima sudo apt update
Hit:1 http://archive.ubuntu.com/ubuntu oracular InRelease
Hit:2 http://security.ubuntu.com/ubuntu oracular-security InRelease
Hit:3 http://archive.ubuntu.com/ubuntu oracular-updates InRelease
Hit:4 http://archive.ubuntu.com/ubuntu oracular-backports InRelease
152 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

## Templates

Uma das coisas legais do lima é o fato de poder usar diferentes configurações de maneira bastante objetiva. Preciso de uma vm do fedora?

```bash
limactl create template://fedora
```

Ou então usado outras formas de containers?

```bash
limactl create template://docker
limactl create template://podman
```

A lista completa pode ser vista aqui https://lima-vm.io/docs/templates/


## Considerações finais

Achei bastante simples e intuitivo usar o Lima, resolve grande parte dos meus problemas pra simular ambientes e me dá um sandbox mais simples pra poder brincar com coisas quando preciso. Muito mais simples de criar VMs e também pode ajudar a simular deploys em VPSs pra mim.

Talvez eu o use em alguns materiais de aulas no futuro. Por ser agnóstico de plataforma, pode ser uma boa ideia!
