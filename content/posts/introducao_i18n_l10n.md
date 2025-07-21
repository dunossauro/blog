+++
title = "Uma introdução à Internacionalização e Localização de software"
date = 2025-07-21T10:26:11-03:00
tags = ["tech", "i18n", "l10n", "python"]
[comments]
host = "bolha.us"
username = "dunossauro"
id = 114891514813104195
+++

	Esse texto, por agora, é um esboço (draft) do material da Live de Python 290 que não ficou pronto a tempo. Ele será atualizado após a live.

## Introdução

Quando criamos aplicações, uma das maiores expectativas de quem desenvolve é que esse software possa ter uma adoção por um grande grupo de pessoas. Muitas vezes, até transcendendo barreiras geográficas e linguísticas. Queremos que nossos sistemas sejam usados em idiomas diferentes, em diversas localidades, por culturas distintas. O objetivo é garantir que o software seja acessível para públicos variados. Para isso, esperamos que nosso sistema seja **localizado** com as necessidades destas pessoas.

Embora esse tema tenha percorrido um longo percurso na indústria de software, iniciar o aprendizado sobre esse assunto é bastante complexo. Existem diversos padrões, integrações entre diferentes sistemas operacionais. Linguagens de programação lidam de forma divergente com a resolução desse problema.

### Localização (l10n)

Localização é o nome dado ao processo de adaptar um software para atender às necessidades linguísticas, culturais e regionais de um público específico. Em uma definição mais formal, segundo a LISA (Localization Industry Standards Association) (Esselink, 2000):

> "A localização envolve pegar um produto e torná-lo linguisticamente e culturalmente apropriado para o local de destino (país/região e idioma) onde ele será usado e vendido."

No primeiro momento, podemos pensar especificamente em **tradução**. Traduzir nosso software para que a língua escolhida por quem usa o software esteja presente nas mensagens. Embora esse seja o passo mais óbvio dos necessários, muitas coisas, além disso, devem ser consideradas.

Existem diversos "padrões regionais" que devem ser considerados. Como:

- Medidas: Diferentes locais usam sistemas de unidades diferentes. Como o sistema métrico (metros, litros, quilos) e o imperial (pés, galões, libras)
- Datas: Os formatos de data variam dependendo da região. No Brasil, usamos dia/mês/ano, já na China: ano/mês/dia.
- Moeda: A moeda varia conforme a região. Você pode se deparar com o Real no Brasil, Euro na Europa ou o Dólar nos Estados Unidos, e é importante que o software ajuste o formato de exibição conforme o local.
- Telefones: Em localidades diferentes, os telefones têm formatos diferentes. Na Índia, por exemplo, temos códigos de área de quatro dígitos.
- Ordenação: Dependendo do alfabeto usado, as regras de ordenação são diferentes.
- E muito mais...

Quando um software se adapta a essas questões regionais, além da tradução do idioma, dizemos que o programa é localizado para a região X.

Por exemplo, se nosso software foi adaptado para atender usuários no Brasil, na Guiné-Bissau e na Índia, podemos dizer que ele foi localizado para essas regiões. Isso implica que, além da tradução do idioma, o sistema também lida corretamente com questões como formato de data, moeda, unidades de medida e até o formato de números de telefone, para garantir uma experiência de uso consistente e apropriada em cada local.

### Internacionalização (i18n)

Enquanto a localização é o ato concreto de regionalizar um sistema, a **internacionalização** é o processo de construção do software para que ele possa ser flexível a diferentes idiomas e regiões. A internacionalização envolve o desenvolvimento de código com a flexibilidade necessária para ser usado globalmente, independentemente de sua origem territorial.

Na definição do LISA (Esselink, 2000):

> "Internacionalização é o processo de generalizar um produto para que ele possa lidar com múltiplos idiomas e convenções culturais sem a necessidade de redesign. A internacionalização ocorre no nível do design do programa e do desenvolvimento de documentos."

A internacionalização deve ser realizada **antes** da localização. Isso significa que, durante a criação do software, ele precisa ser projetado de forma que possa ser facilmente adaptado a novos idiomas e regiões, sem exigir grandes mudanças no código. Por exemplo, mensagens (strings) precisam ser extraídas de forma que possam ser traduzidas sem alterar o comportamento do programa, os números usados pela aplicação precisam ser formatados conforme a região. É a parte da engenharia de software para a construção de um codebase adaptado para a localização ser possível.

### Os termos e as abreviações

Como os termos foram criados pela indústria, é bastante complicado precisar quando eles apareceram pela primeira vez. Segundo i18nguy em *Origin Of The Abbreviation I18n*, a origem dos termos é desconhecida. Ele suspeita que ambos os termos tenham surgido na década de 80.

Contudo, as "abreviações", chamadas de **numerônimos**, remontam à história da empresa americana DEC (comprada pela compaq, comprada pela hp). Onde o funcionário de sobrenome *Scherpenhuizen* recebeu uma conta de e-mail abreviada, pois seu nome era muito grande, **s12n**. Essa brincadeira deu origem ao termo i18n na DEC. Posterior a isso, acredita-se que o termo l10n tenha surgido.

> "O termo **numerônimo** se refere a palavras encurtadas com o uso de números para representar partes da palavra. No caso de i18n, o número 18 corresponde ao número de letras entre o "i" e o "n" na palavra "internationalization". Usamos numerônimos também em termos modernos como: `k8s` (Kubernetes), `o11y` (Observability), etc."


### Um mundo com e sem padrões

Embora a internacionalização e a localização sejam essenciais para atingir públicos globais, não existe um padrão universal que seja adotado por todas as plataformas e sistemas operacionais. Cada ecossistema adota sua própria abordagem, o que pode gerar confusão, principalmente durante a fase de aprendizado. Levando em conta somente as traduções como exemplo:

- Linux: A plataforma adota amplamente o `gettext` para a extração e tradução de strings, utilizando arquivos `.po` para armazenar as traduções e `.mo` para a compilação desses arquivos.

- Windows: No ecossistema MS, especialmente para aplicações `.NET` e `C#`, a internacionalização é feita usando arquivos `.resx`, que armazenam recursos como textos traduzidos, imagens e outros dados específicos de localização.

- macOS: No mundo Apple, a internacionalização e localização são realizadas com o uso de arquivos `.strings`, que contêm as traduções necessárias para adaptar o software a diferentes idiomas e regiões.

- Web (JavaScript): No ambiente web, especialmente com `JavaScript`, bibliotecas como `i18next` são populares, utilizando arquivos de tradução em JSON ou YAML para gerenciar os idiomas e regionalizações de forma dinâmica e flexível.

Essas diferenças refletem como a indústria tem adotado soluções específicas para suas necessidades, mas também evidenciam a ausência de um padrão universal, tornando a tarefa de internacionalização e localização algo altamente dependente do contexto da plataforma em que o software será executado.

Com isso em mente, gostaria de reduzir o escopo e a abrangência desse texto. Conversaremos sobre uma visão geral do tema e usaremos python como a linguagem para criar nossos exemplos. Outro ponto de atenção aqui é que não desejo expandir essa discussão para interfaces gráficas ou aplicações web. Focaremos nos conceitos primordiais e no uso da biblioteca padrão da linguagem.


## As bibliotecas padrões do Python

No mundo Python, as bibliotecas padrões para fazer i18n são influenciadas por dois padrões: o do `GNU/gettext` para arquivos de tradução e a especificação `Locale` POSIX (PYTHON SOFTWARE FOUNDATION, 2025a). Embora a relação entre esses dois padrões trabalhando em conjunto seja um pouco difícil de traçar historicamente, eles são bem documentados em conjunto na OpenI18N, criada pelo hoje extinto Free Standards Group. Essa iniciativa foi incorporada à Linux Standard Base (LSB), uma tentativa de padronizar o comportamento entre distribuições Linux, combinando padrões POSIX com normas ISO (FREE STANDARDS GROUP, 2003).


```mermaid
graph LR
  python --> i18n
  i18n --> gettext
  i18n --> locale
  gettext --> A["Arquivos de tradução"]
  locale --> B["Serviços gerais para os padrões regionais"]
```

### gettext

A biblioteca `gettext` trabalha em conjunto com o ecossistema do GNU/gettext (Python Software Foundation, 2025b), uma caixa de ferramentas e padrões para desenhados para minimizar o impacto da internacionalização (Free Software Foundation, [S.d.]). A ideia principal dessa ferramenta é isolar as strings do código para tradução.


#### Um exemplo básico

Como todo início de estudo requer um "olá mundo" para não azarar o aprendizado, começaremos por ele:

```python
# exemplo_00.py
import gettext

_ = gettext.gettext

print(_('Hello'))
```

O `_` como alias para `gettext.gettext` é um padrão definido para as strings que devam ser internacionalizadas possam ser encontradas pelo "raspador" dos códigos-fonte.


#### Ferramentas do GNU/gettext

Agora que temos uma string para ser internacionalizada, podemos conhecer as ferramentas de tertminal do GNU/gettext.

##### `xgettext`

O comando `xgettext` é responsável por gerar os templates de tradução. Chamamos esse arquivo de `.pot`. Portable Object Templates.

```bash
xgettext -o messages.pot exemplo_00.py
# Uma lista de arquivos .py pode ser enviada
# Se precisar usar com diretórios pode usar o `find` em conjunto
# algo como:
# find . -name '*.py' -print0 | xargs -0 xgettext -o messages.pot
```

> Caso esteja usando windows, o gettext está disponível para a plataforma no repositório: https://github.com/mlocati/gettext-iconv-windows

O arquivo gerado é a base para as traduções. Um template de todas as strings encontradas com o padrão `_()`. Gerando algo como (cabeçalhos omitidos):

```bash
#: exemplo_00.py:5
msgid "Hello"
msgstr ""
```

Temos duas chaves aqui. A `msgid`, que diz respeito à mensagem encontrada no arquivo de código, seguida de `msgstr`. A mensagem que deve ser traduzida.

Ao olharmos o cabeçalho do arquivo, por se tratar de um template, nos deparamos com a linguagem em branco:

```po
"Language: \n"
```

Para iniciarmos a tradução, precisamos gerar um portable para a linguagem alvo.

##### `msginit`

Quando iniciamos uma tradução para as strings, precisamos iniciar um arquivo de tradução. Um `.po`, o arquivo Portable Object. A aplicação usada para isso é o `msginit`.

Aqui usamos como base para criação de novos arquivos, duas ISOs:

1. [`ISO 639-1` (set 1)](https://en.wikipedia.org/wiki/List_of_ISO_639_language_codes) para definir a lingua usada na tradução.
2. Em conjunto com a [ISO 3166-1 (alpha 2)](https://en.wikipedia.org/wiki/ISO_3166-1) para definir o país onde essa tradução atuará.

> Linguagens artificiais como Esperanto e Interlingua não tem países, somente lingua.

Fazendo uma junção dos dois códigos usando um `_`. Para português, ousamos `pt` como lingua. Para o país, usamos as variantes: `BR` para o Brasil, `CV` para Cabo Verde, `AO` para Angola, `PT` para Portugal, e assim por diante.

Tendo algo como `pt_BR` ou `pt_CV`. Por exemplo, se quisermos traduzir nosso sistema para `pt_BR`:

```bash
msginit --locale=pt_BR.UTF-8 --input=messages.pot --output=pt_BR.po
```

A informação mais importante é a flag `--locale`, que diz em qual localidade o arquivo será gerado. Note que o charset `UTF-8` também é passado. O charset é extremamente importante, pois ele quem define como os caracteres serão apresentados.

> Charset é um oceano a parte, que não focarei nesse texto, pois ele claramente merece uma aula específico sobre ele e sua relação com unicode.

> Sempre que possível, use UTF-8 nos arquivos `.po` para evitar problemas de codificação ao lidar com idiomas não-latinos.

A execução do comando gerará um arquivo portable (Alguns campos foram omitidos):

```po
"Language: pt_BR\n"
"Content-Type: text/plain; charset=UTF-8\n"
"Plural-Forms: nplurals=2; plural=(n > 1);\n"

#: exemplo_00.py:3
msgid "Hello"
msgstr ""
```

Onde temos a língua usada, o charset e um metadado **extremamente importante**, o `Plural-Forms`, a qual nos debruçaremos em breve.

Agora, nesse arquivo, devemos escrever nossa tradução para o `msgid "Hello"`. Algo como:

```po
#: exemplo_00.py:3
msgid "Hello"
msgstr "Olá"
```

Com isso, podemos converter o `.po` em um arquivo usável pelo nosso programa.

##### `msgfmt`

Agora que temos a tradução da nossa mensagem, precisamos "complilar" nosso arquivo de tradução em um arquivo `.mo` (Machine Object). Isso tornará o nosso arquivo em um binário que será usado pelo python ao exibir as mensagens.

Por padrão, existe uma hierarquia de diretórios que deve ter sua forma respeitada:

```txt
locale
├── eo
│   └── LC_MESSAGES
└── pt_BR
    └── LC_MESSAGES
```

Com a estrutura de diretórios criada, podemos fazer a execução do `msgfmt`:

```bash
msgfmt pt_BR.po -o locale/pt_BR/LC_MESSAGES/messages.mo
```

Esse comando criará o `.mo` para nosso idioma alvo:

```txt
locale
├── eo
│   └── LC_MESSAGES
└── pt_BR
    └── LC_MESSAGES
        └── messages.mo
```

Pronto, agora temos um arquivo traduzido!

#### De volta ao python

Agora que temos o `msgid` traduzido e no local correto, precisamos adaptar nosso código para lidar com as traduções:

```python
import gettext

t = gettext.translation('messages', localedir='locale')

t.install()

print(_('Hello'))
```

A função `gettext.translation` vai buscar pelas mensagens em `locale` no contexto de `messages`. Em seguida, instalamos o suporte ao idioma com `t.install`.

> Note que aqui não existe uma chamada direta para `_`, o método install cria essa variável em runtime. Isso pode apresentar problemas com checadores estáticos, para referenciar o `_` pode-se usar `_ = t.gettext`

Ao executar o código, temos o resultado normal do `hello`:

```bash
python exemplo_00.py 
Hello
```

Contudo, a variável de ambiente `LANG` será considerada na hora de executar o código, traduzindo o contexto de mensagens:

```python
# $env:LANG = "pt_BR" - Para windows via powershell
LANG='pt_BR' python exemplo_00.py 
Olá
```

	A detecção automatica da lingua será vista mais pra frente.

Com isso, temos um "Olá mundo" localizado em português do Brasil <3

#### Nem sempre as coisas dão certo

Coisas que precisamos nos atentar antes de andar mais nesse assunto...

##### Fallback

Nossa chamada para `translation` depende de que as mensagens para um determinado idioma estejam disponíveis em traduções. Caso ela não esteja, teremos um erro em runtime. Vamos tentar com espanhol da Argentina:

```bash
LANG='es_AR' python exemplo_00.py 
Traceback (most recent call last):
  # ...
  File "/usr/lib/python3.13/gettext.py", line 537, in translation
    raise FileNotFoundError(ENOENT,
                            'No translation file found for domain', domain)
FileNotFoundError: [Errno 2] No translation file found for domain: 'messages'
```

Isso acontecerá sempre que não tivermos o idioma ou a varição de localidade definida em `LANG`. Uma das formas de lidar com isso é usar o parâmetro `fallback`:

```python
t = gettext.translation(
    'messages', localedir='locale', fallback=True
)
```

Isso garante que, quando o idioma ou a localidade não estiverem presentes, o sistema use as mensagens padrão, sem localização.

```bash
LANG='es_AR' python exemplo_00.py 
Hello
```

##### Debugando as traduções

Nem sempre as coisas ocorrem da maneira que deveriam e precisamos. Às vezes, a mensagem exibida pode estar errada. Afinal... somos humanos, podemos cometer erros durante a tradução. Se quisermos inspecionar o `.mo`, podemos usar o comando `msgunfmt`:

```bash
msgunfmt locale/pt_BR/LC_MESSAGES/messages.mo
```

Isso exibirá a forma original do `.po`. Algo como (cabeçalhos omitidos):

```po
# ...
msgid "Hello"
msgstr "Olá"
```

Fazendo com que possamos checar se o erro está no `.mo`.

##### Janelas (windows)

Diferente de sistemas Unix/Linux, o Windows não define a variável de ambiente `LANG` por padrão, o que significa que o código pode não detectar automaticamente a localidade correta nesse sistema.

Nesses casos, você precisará definir manualmente o idioma dentro do seu código, ou utilizar abordagens alternativas, como veremos mais adiante com o módulo `locale`. Por enquanto, saiba que a localização automática baseada em LANG funciona em sistemas POSIX (como Linux e macOS), mas não é confiável no Windows sem configuração adicional.


#### Um resumo do fluxo

```mermaid
graph LR
  py[".py com _('msg')"] --> pot[".pot template"]
  pot --> po[".po traduzido"]
  po --> mo[".mo binário"]
  mo --> uso["Uso no Python via gettext"]
```


#### f-strings

Em python temos as poderosas f-strings `f''`, porém as f-strings não tem suporte a tradução. Podemos usar as strings formatadas no lugar disso. Porém, com algumas formas semânticas próprias. O método `.format` deve ser chamado após gettext:

```python
_('Hello {name}').format(name='Faust')
```

Isso gerará um `.pot` com um comentário:

```po
#: exemplo_00.py:8
#, python-brace-format
msgid "Hello {name}"
msgstr ""
```

o `python-brace-format` indica que o que estiver entre "braces" (`{}`) é uma variável de interpolação. Logo, não deve ser traduzida.

Uma observação deve ser feita aqui. As strings formatadas tem suporte a valores posicionais, como `{0}, {1}, ...`. Evite usar posições. Elas não oferecem contexto para quem estiver traduzindo.

> raw strings podem ser usadas...


#### Trabalhando com plurais em mensagens

Um dos pontos mais importantes quando trabalhando com texto é entender que mensagens nem sempre são "fixas". Elas se modificam em relação ao contexto em que a mensagem é exibida. O caso mais clássico dessas modificações são os plurais.

Por exemplo, vamos imaginar uma caixa de mensagens. O texto muda se você não tem mensagens, se tem uma mensagem ou se tem N mensagens. No momento de escrever um código internacionalizado, essas regras mudam. Principalmente pelo fato de plurais não serem iguais em todas as línguas.

Um exemplo:

```python
number_of_messages = 1

if not number_of_messages:
    print(_('No new messages'))
else:
    print(
        t.ngettext(
            'You have %(count)d message',
            'You have %(count)d messages',
            number_of_messages
        ) % {'count': number_of_messages}
    )
```

O que vai nos gerar um `.pot` como esse (diversos campos foram omitidos):

```
"Plural-Forms: nplurals=INTEGER; plural=EXPRESSION;\n"

#: exemplo_00.py:10
msgid "No new messages"
msgstr ""

#: exemplo_00.py:14
#, python-format
msgid "You have %(count)d message"
msgid_plural "You have %(count)d message"
msgstr[0] ""
msgstr[1] ""
```

Onde o primeiro `msgid` é usado no singular. O segundo, porém, tem `msgid` e `msgid_plural` que são duas formas para a mesma mensagem.

##### `ngettext`

Nesse bloco de código é introduzido um novo método do gettext, `ngettext`. Que podem ser lidos como "number gettext". Ele é responsável por mensagens que devem ser internacionalizadas com seus plurais.

```python
ngettext('singular', 'plural', numero) % numero
```

A ideia é que, caso o número seja 1, a mensagem no singular será exibida, caso seja maior do que 1, a segunda mensagem seja exibida.

As mensagens podem ser formatadas de duas formas. Usando o formatador `%d` diretamente, o que não é muito legal para ler e traduzir no `.po`. Ou então, de forma nomeada, como `%(variavel)d`. Onde o nome da variável é levado ao arquivo `.po`, facilitando a tradução.

##### Múltiplos `msgstr`

Quando usamos `ngettext` teremos um template que leva em consideração o dado em `Plural-Forms`:

```
"Plural-Forms: nplurals=INTEGER; plural=EXPRESSION;\n"

#: exemplo_00.py:10
msgid "No new messages"
msgstr ""

#: exemplo_00.py:14
#, python-format
msgid "You have %(count)d message"
msgid_plural "You have %(count)d message"
msgstr[0] ""
msgstr[1] ""
```

Existem línguas como Russo, Hindi, ... que tem múltiplas formas de plural ("Language Plural Rules", [S.d.]). Essas características devem ser consideradas na hora de gerar a tradução. Tanto na quantidade de `msgstr`s e no cabeçalho de `Plural-Forms`.

Por exemplo, em russo regras bem diferentes das linguagens que costumamos usar:

- Singular: todo número terminado em 1, mas não em 11, usa a forma singular: 1, 21, 31, 41, ...
- Paucal: usada quando o número termina em 2, 3 ou 4, mas não em 12 a 14.
Exemplos: 2, 3, 4, 22, 23, 24
- Geral: usada para todos os outros casos. Exemplos: 0, 5-20, 11-14, 25, 100, 111, etc.

Gerando um `Plural-Forms` como:

```po
Plural-Forms: nplurals=3; plural=(n%10==1 && n%100!=11 ? 0 :
                                   n%10>=2 && n%10<=4 && (n%100<10 || n%100>=20) ? 1 : 2);
```

O que resultaria em uma string `.po` parecida com esse (perdão para quem fala Russo, dei meu melhor):

```po
msgid "You have %(count)d new message"
msgid_plural "You have %(count)d new messages"
msgstr[0] "У вас %(count)d новое сообщение"
msgstr[1] "У вас %(count)d новых сообщения"
msgstr[2] "У вас %(count)d новых сообщений"
```

> As regras de todos os idiomas podem ser encontradas aqui: https://www.unicode.org/cldr/charts/47/supplemental/language_plural_rules.html 


### locale

O módulo `locale` em Python segue parcialmente o padrão `POSIX`, oferecendo suporte às funcionalidades mais comuns para detectar e configurar localidades (locales). Ele permite lidar com aspectos regionais, como formatos de datas, números, moedas e ordenação, indo além do idioma em si. O `locale` fornece um toolkit genérico para trabalhar com essas configurações de ambiente, enquanto a responsabilidade pela tradução e internacionalização do idioma fica a cargo do `gettext`. Ou seja, `locale` cuida do "como" mostrar a informação segundo a localidade, e gettext cuida do "o que" mostrar em cada idioma (Python Software Foundation, 2025c).

#### Obtendo a localidade

Diante de várias funções e constantes providas pelo `locale` acho que devemos considerar primeiro as funções referentes à localidade em geral:

- `getlocale()`: Fornece uma tupla com o idioma_Localização e o charset
- `setlocale()`: Aplica uma localização específica.
##### `getlocale`

A função `getlocale` vai nos retornar o locale atual:

```python
>>> import locale
>>> locale.getlocale()
('en_US', 'UTF-8')
```

Esse resultado difere, dependendo do sistema operacional. Se for compatível com POSIX teremos esse resultado. No windows, o padrão é LCID (M-kauppinen, [S.d.]). O que pode fornecer um resultado bastante diferente:

```python
>>> locale.getlocale()
('English_United States', '1252')
```

###### LCID vs POSIX

Não existe uma forma única de pegar o valor do locale em LCID e converter em POSIX, para criarmos e usarmos os arquivos `.po` em múltiplos sistemas operacionais. Mas, a MS mantém uma lista dos códigos ("[MS-LCID]", [S.d.]). Para obter esse código, podemos usar `ctypes`:

```python
>>> import ctypes
>>> ctypes.windll.kernel32.GetUserDefaultLCID()
1033
```

Esse código pode ser usado para conversão entre LCID e POSIX usando um dicionário presente no módulo `locale` com a variável `windows_locale`. Em conjunto:

```python
>>> import ctypes
>>> import locale
>>> locale.windows_locale.get(ctypes.windll.kernel32.GetUserDefaultLCID())
'en_US'
```

Dessa forma, o sistema pode interoperar nas traduções com os dois formatos.

> Existe a função `locale.getdefaultlocale()` que faz essa tradução de forma automática, porém ela será removida na versão 3.15. Embora exista uma discussão ativa sobre esse tema (Python, [S.d.])

##### `setlocale`

A função `setlocale` faz o inverso, ela adapta o sistema a uma determinada regionalidade. Isso significa que, ao configurá-la, o comportamento do sistema em relação a datas, números, moedas e outros formatos regionais serão alterados conforme o locale definido. Assim, o sistema "reage" ao valor passado, aplicando as regras daquela localidade.

Por exemplo, para definir o locale para o padrão americano dos Estados Unidos:

```python
import locale
locale.setlocale(locale.LC_ALL, 'en_US.UTF-8')
```

> É importante lembrar que nem todos os locales estão instalados em todos os sistemas, e a função pode levantar uma exceção caso o locale solicitado não seja encontrado.

#### Variações no `setlocale`

O `setlocale` pode ser aplicado de diferentes maneiras, dependendo da área que você deseja configurar. O primeiro parâmetro de `setlocale` define qual aspecto da localidade será alterado:

* **`LC_ALL`**: modifica todas as áreas de localidade, incluindo data, hora, moeda, números, entre outras.
* **`LC_TIME`**: altera a formatação de data e hora.
* **`LC_MONETARY`**: modifica o formato de valores monetários, incluindo a moeda e os separadores decimais.
* **`LC_NUMERIC`**: define como os números serão formatados, como o uso de vírgula ou ponto como separador decimal.
* **`LC_COLLATE`**: controla a ordenação de strings (importante para buscas e classificações).

Por exemplo, se você quiser mudar somente o formato de datas, pode configurar o `LC_TIME` dessa forma:

```python
import locale
locale.setlocale(locale.LC_TIME, 'en_US.UTF-8')
```

Ou, se for necessário configurar somente a parte de moedas para o Brasil, você poderia usar:

```python
import locale
locale.setlocale(locale.LC_MONETARY, 'pt_BR.UTF-8')
```

Isso garante que somente o comportamento relacionado à moeda será alterado, sem afetar outras áreas como a data ou a ordenação de texto.

##### Formatação de datas

A formatação de datas é uma das partes essenciais da localização, pois as convenções de data variam bastante de país para país. Para garantir que a data seja exibida no formato correto. O `locale`, que nos permite usar constantes predefinidas para formatar as datas conforme o padrão regional.

Algumas constantes são ofertadas no módulo como `locale.D_T_FMT`, `locale.D_FMT` e `locale.T_FMT`, que garantem que as datas sejam apresentadas corretamente conforme a localidade configurada no sistema. Em vez de formatar as datas manualmente, podemos usar essas constantes, ajustadas automaticamente conforme a localidade.

Exemplo básico para formatar datas com as constantes do `locale`:

```python
import locale
import datetime

# Definindo a localidade para português do Brasil
locale.setlocale(locale.LC_TIME, 'pt_BR.UTF-8')
data = datetime.datetime(2025, 7, 21, 14, 55, 2)
print(data.strftime(locale.nl_langinfo(locale.D_T_FMT)))
# Saída: Dom Jul 21 2025 14:55:02

# Definindo a localidade para inglês dos Estados Unidos
locale.setlocale(locale.LC_TIME, 'en_US.UTF-8')
data = datetime.datetime(2025, 7, 21, 14, 55, 2)
print(data.strftime(locale.nl_langinfo(locale.D_T_FMT)))
# Saída: Sun Jul 21 14:55:02 2025
```

##### Formatação de moedas

Assim como as datas, o formato de moedas varia bastante dependendo do país ou região. Por exemplo, nos Estados Unidos, a moeda é representada com o símbolo do dólar ($), enquanto no Brasil usamos o símbolo "R$". O módulo `locale` nos ajuda a lidar com essas diferenças.

Podemos usar o `locale.currency()` para formatar valores monetários segundo o padrão da localidade ativa. Esse método vai formatar o valor com o símbolo da moeda e a separação correta de milhares e decimais, conforme a convenção local.

Exemplo:

```python
import locale

# Definindo a localidade para português do Brasil
locale.setlocale(locale.LC_MONETARY, 'pt_BR.UTF-8')
print(locale.currency(123456.789, grouping=True))
# Saída: R$ 123.456,79

# Definindo a localidade para inglês dos Estados Unidos
locale.setlocale(locale.LC_MONETARY, 'en_US.UTF-8')
print(locale.currency(123456.789, grouping=True))
# Saída: $123,456.79
```

O método `locale.currency()` ajusta automaticamente o símbolo da moeda, o formato dos números e a vírgula ou ponto como separador decimal, dependendo da localidade configurada. Dessa forma, ao configurar o `locale`, o software pode exibir a moeda corretamente em diferentes países sem que você precise se preocupar com essas particularidades.

##### Formatação de números

A formatação de números é outro aspecto que também varia. O separador de milhares e o símbolo para a vírgula ou ponto como separador decimal são exemplos de diferenças que podem ocorrer entre as localidades. Podemos usar a função `locale.format_string()` para formatar números segundo as convenções. Essa função recebe o número a ser formatado e a especificação de formato, como o número de casas decimais ou o uso de separadores de milhares.

Exemplo:

```python
import locale

# Definindo a localidade para português do Brasil
locale.setlocale(locale.LC_NUMERIC, 'pt_BR.UTF-8')
print(locale.format_string("%0.2f", 1234567.89, grouping=True))
# Saída: 1.234.567,89

# Definindo a localidade para inglês dos Estados Unidos
locale.setlocale(locale.LC_NUMERIC, 'en_US.UTF-8')
print(locale.format_string("%0.2f", 1234567.89, grouping=True))
# Saída: 1,234,567.89
```

Aqui, a função `locale.format_string()` usa o separador de milhares correto e o formato decimal adequado para cada localidade.

Ao usar o `locale` para formatação de números, garantimos que a apresentação dos valores esteja em conformidade com as normas locais, sem a necessidade de código específico para cada caso.

##### Ordenação de strings (collation)

Ordenar textos corretamente em diferentes idiomas é mais complexo do que parece. Cada idioma tem regras próprias para comparar letras, principalmente com acentos e caracteres especiais. Para isso, usamos `locale.strxfrm()` que transforma as strings para a ordenação ser adequada ao idioma. Por exemplo:

```
import locale

locale.setlocale(locale.LC_COLLATE, 'pt_BR.UTF-8')
lista = ['zebra', 'ação', 'abacaxi', 'Árvore']
lista_ordenada = sorted(lista, key=locale.strxfrm)
print(lista_ordenada)
# ['abacaxi', 'ação', 'Árvore', 'zebra']
```

Assim, a lista fica ordenada do jeito esperado para falantes do português.

## Juntando `gettext` e `locale`

<ainda será escrito>

## Recursos adicionais

<ainda será escrito>

> TODO: Citar ferramentas como humanize e babel. Também citar o Fluent.


## Referências

ESSELINK, Bert. A Practical guide to localization. Amsterdam Philadelphia: John Benjamins Pub. Co, 2000. 

About W3C Internationalization (i18n). Disponível em: <https://www.w3.org/International/i18n-drafts/nav/about>. Acesso em: 16 jul. 2025. 

PYTHON SOFTWARE FOUNDATION. Internacionalização. Documentação. Disponível em: <https://docs.python.org/3/library/i18n.html>. Acesso em: 20 jul. 2025a.

PYTHON SOFTWARE FOUNDATION. gettext — Serviços de internacionalização multilíngues. Disponível em: <https://docs.python.org/pt-br/3.13/library/gettext.html>. Acesso em: 15 jul. 2025b.

FREE SOFTWARE FOUNDATION. Top (GNU gettext utilities). , [S.d.]. Disponível em: <https://www.gnu.org/software/gettext/manual/gettext.html>. Acesso em: 15 jul. 2025

FREE STANDARDS GROUP. OpenI18N 1.3. , 2003. Disponível em: <http://openi18n.web.fc2.com/numa/OpenI18N1.3.pdf>

Language Plural Rules. Disponível em: <https://www.unicode.org/cldr/charts/47/supplemental/language_plural_rules.html>. Acesso em: 21 jul. 2025. 

PYTHON SOFTWARE FOUNDATION. locale — Serviços de internacionalização. Disponível em: <https://docs.python.org/3/library/locale.html>. Acesso em: 20 jul. 2025c.

M-KAUPPINEN. Other locale representations - Globalization. Disponível em: <https://learn.microsoft.com/en-us/globalization/locale/other-locale-names>. Acesso em: 20 jul. 2025. 

[MS-LCID]: Windows Language Code Identifier (LCID) Reference. Disponível em: <https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-lcid/70feba9f-294e-491e-b6eb-56532684c37f>. Acesso em: 21 jul. 2025. 

PYTHON. Deprecation of locale.getdefaultlocale breaks POSIX compatibility on Windows platform · Issue #130796 · python/cpython. Disponível em: <https://github.com/python/cpython/issues/130796>. Acesso em: 21 jul. 2025. 
