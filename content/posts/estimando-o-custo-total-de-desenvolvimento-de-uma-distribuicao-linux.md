---
title: "Estimando o custo total de desenvolvimento de uma distribuicao linux"
date: 2019-05-18T00:00:00-03:00
tags: ["tech"]
---

Esse artigo é uma livre tradução de: https://www.linuxfoundation.org/events/2008/10/estimating-the-total-cost-of-a-linux-distribution/

Autores: **Amanda McPherson, Brian Proffitt, and Ron Hale-Evans**


O sistema operacional Linux é o projeto de código aberto mais bem-sucedido da história, mas o quanto vale o software em uma distribuição Linux? Em 2002, David A. Wheeler publicou um estudo bem conceituado que examinou as linhas de software de código presentes em uma distribuição típica do Linux. Suas descobertas? O custo total de desenvolvimento representado em uma distribuição típica do Linux foi de US $ 1,2 bilhão. Usamos suas ferramentas e métodos para atualizar essas descobertas. Usando as mesmas ferramentas, estimamos que seriam necessários aproximadamente US $ 10,8 bilhões para construir a distribuição do Fedora 9 em dólares atuais, com os custos atuais de desenvolvimento de software. Além disso, seriam necessários US $ 1,4 bilhão para desenvolver o kernel Linux sozinho. Este artigo descreve nossa técnica e destaca os custos mais recentes do desenvolvimento do Linux.

O sistema operacional Linux é o sistema operacional de código aberto mais popular da computação atual, representando um ecossistema de US $ 25 bilhões em 2008. Desde a sua criação em 1991, ela cresceu para se tornar uma força na computação, impulsionando tudo, desde a Bolsa de Nova York até telefones celulares, supercomputadores e dispositivos de consumo.

Como um sistema operacional aberto, o Linux é desenvolvido de forma colaborativa, o que significa que nenhuma empresa é a única responsável por seu desenvolvimento ou suporte contínuo. As empresas que participam da economia Linux compartilham os custos de pesquisa e desenvolvimento com seus parceiros e concorrentes. Essa disseminação da carga de desenvolvimento entre indivíduos e empresas resultou em um ecossistema grande e eficiente e em inovações de software não divulgadas.

Mais de 1.000 desenvolvedores, de pelo menos 100 empresas diferentes, contribuem para cada lançamento do kernel. Nos últimos dois anos, mais de 3.200 desenvolvedores de 200 empresas contribuíram para o kernel. É importante observar que o kernel é apenas uma pequena parte de uma distribuição do Linux. Uma distribuição é, na verdade, composta de vários componentes, incluindo o kernel, os ambientes de área de trabalho GNOME e KDE, os componentes GNU, o sistema de janelas X e muitos mais. O total de desenvolvedores individuais que contribuem para esses projetos certamente chega aos milhares.

Como o Linux foi desenvolvido coletivamente, não há uma única fonte de estimativas de custo de quanto foi necessário para desenvolver a tecnologia. Em 2002, David A. Wheeler publicou um estudo bem conceituado que examinou as linhas de software de código presentes em uma distribuição típica do Linux (Red Hat Linux 7.1) Ele concluiu — como fizemos — que as linhas de código de software são o método mais prático para determinar o valor do software de código aberto, uma vez que se concentra no resultado final e não nas estimativas por empresa ou por desenvolvedor. Usando as ferramentas padrão do setor que ele desenvolveu para contar e analisar o SLOC, ele determinou que custaria mais de US $ 1,2 bilhão para desenvolver uma distribuição Linux por meio de propriedade convencional nos EUA.

Isso foi há seis anos. Como o Linux está inovando e crescendo a uma taxa alta ano após ano, o número de US $ 1,2 bilhão precisou ser atualizado para refletir o verdadeiro valor do desenvolvimento refletido no Linux hoje (e o aumento do custo do próprio desenvolvimento de software). Para este documento, a Linux Foundation determinou o custo total de desenvolvimento representado em uma distribuição típica do Linux e atualizou o número de US $ 1,2 bilhão amplamente utilizado desde sua publicação em 2002.

Analisamos a distribuição do Fedora 9, que foi lançada em 13 de maio de 2008. É uma distribuição popular e bem usada e é a base para o Red Hat Enterprise Linux, que representa uma grande porcentagem do mercado de Linux. É também um descendente direto do software Red Hat Linux 7.1 analisado por Wheeler em seu artigo original.

Para este estudo, usamos a conhecida ferramenta SLOC de David A. Wheeler, SLOCCount. O SLOCCount utiliza o padrão COdstructive COst MOdel (COCOMO) padrão da indústria, um modelo algorítmico de estimativa de custos de software desenvolvido por Barry Boehm. O modelo usa uma fórmula básica de regressão, com parâmetros que são derivados de dados históricos de projetos e características atuais do projeto. Atualizamos seu estudo de 2002 para incluir a crescente base de código do kernel Linux e outros pacotes, bem como o maior salário anual de um desenvolvedor de software. (Mais detalhes sobre isso seguem na seção Abordagem do artigo.)

Usando essa abordagem, estimamos que seriam necessários US $ 10,8 bilhões para desenvolver a distribuição Linux do Fedora 9 por meios proprietários tradicionais no ano de 2008.


## Abordagem

Nossa abordagem básica era (Para aqueles que estão interessados em como instalamos e analisamos o código fonte, por favor, veja o Apêndice do artigo original):

1. Instale os arquivos de código-fonte no formato descompactado; isso requer baixar o código-fonte e instalá-lo corretamente em nossas máquinas de teste.

2. Conte o número de linhas de código de origem (SLOC); o que requer uma definição cuidadosa do SLOC.

3. Use um modelo de estimativa (com base nas práticas do COCOMO) para estimar o esforço e o custo de desenvolver o mesmo sistema de maneira proprietária.

Para atualizar o estudo de 2002, foi decidido que usaríamos o mesmo código base usado no estudo de 2002, o Fedora — a distribuição da comunidade que forma a base do Red Hat Enterprise Linux. Para nosso exame, decidimos usar o Fedora. Contamos todos os pacotes disponíveis do Fedora 9 que foram tornados públicos no arquivo espelho mirrors.kernel.org. Decidiu-se usar todos os pacotes porque não desejávamos usar uma definição arbitrária do sabor do Fedora 9 que mediríamos. O Fedora contém significativamente mais software do que a versão corporativa da Red Hat. Uma razão para isso é que uma comunidade diversificada está envolvida na construção do Fedora, não apenas em uma empresa. Usar o aplicativo SLOCCount é uma tarefa incrivelmente simples: é simplesmente uma questão de apontá-lo no diretório correto onde o código-fonte reside e deixá-lo rodar. Uma explicação detalhada de como o programa funciona e como usá-lo ainda está disponível no site da Wheeler9.

Para calcular os custos dessas distribuições, foi encontrado um salário-base para programadores de computador do Bureau of Labor Statistics dos EUA. De acordo com o BLS, o salário médio de um programador norte-americano em julho de 2008 foi de US $ 75.662,08. Este era o valor do salário usado em nossa execução no SLOCCount. (É claro que a maioria dos desenvolvimentos de software hoje em dia é global, portanto usar um número de salário apenas nos EUA é um tanto ilusório. Uma maneira de continuar explorando seria determinar um salário médio global a ser usado como base para os custos de produção).

Deve-se notar que o salário sozinho não é o único determinante dos custos de desenvolvimento de software. Em seus artigos, Wheeler observa a presença do parâmetro overhead dentro do SLOCCount. Isso leva em consideração os custos de testes, equipamentos, custos operacionais da empresa e remuneração total para o desenvolvedor. Esse parâmetro também é conhecido como taxa de quebra.

Como apenas um exemplo de como esses custos podem aumentar rapidamente, nos Estados Unidos, o percentual médio de remuneração (dias de doença, férias, benefícios de seguro) para um funcionário profissional é de 29,0% 11. Assim, o programador que faz o salário médio dos EUA de US $ 75.662,08 está realmente custando ao empregador US $ 97.604,08 em compensação sozinho. Esta é apenas uma parte da torta de taxa de envoltório total.

A própria estimativa de Wheeler do valor total da taxa de empacotamento é 2,4. Embora esse número varie claramente por empresa e região, pesquisas adicionais não mostraram nenhuma evidência significativa de que esse número precisaria de ajuste para nossos testes.


### Código-fonte e resultados de custos estimados

Finalmente, considerando todas as suposições mostradas anteriormente, o SLOC e os valores de produção estimados para o Fedora 9 são os seguintes.

Linhas de código fonte físicas totais (SLOC)

**204,500,946**

(Modelo básico COCOMO, Pessoa-meses = 2,4 * (KSLOC ** 1,05))
**59389.53 (712674.36)**

Estimativa do cronograma, anos (meses)
(Modelo básico de COCOMO, Meses = 2,5 * (pessoa-meses ** 0,38))

**24.64 (295.68)**

Custo total estimado para desenvolver

**$10,784,484,309**

Como um aparte: o valor do salário anual do SLOCCount original era de US $ 56.286 em dólares do ano 2000, então é interessante ver como os custos de hoje se traduzem nos mesmos custos do ano 2000. Para descobrir isso, multiplicamos o custo total para desenvolver o Fedora 9 em dólares de 2008 (US $ 10.784.484.309) em 0,744, que é a razão entre o salário do programador do ano 2000 normalmente usado pelo SLOCCount (US $ 56.286) e o salário de julho de 2008 que encontramos (US $ 75.662,08). O resultado é pouco mais de US $ 8 bilhões para desenvolver os custos do Fedora 9 em 2000. Isso dá ao leitor uma boa indicação de quanto código e funcionalidade foram adicionados a uma distribuição Linux nesses seis anos.

## Focando no Kernel Linux e no Modelo Intermediário

Como a pesquisa foi conduzida para este artigo, ficou rapidamente aparente que nem todos os componentes dentro de uma dada distribuição Linux precisavam ser tratados igualmente. Alguns projetos, por sua própria natureza e complexidade, precisam de consideração diferente no modelo COCOMO.

Em nenhum lugar isso ficou mais aparente do que no próprio artigo de 2002 de Wheeler, onde ele destacou a necessidade de um modelo de estimativa diferente para o próprio kernel Linux. Nesse novo artigo, Wheeler afirmou que, como o código do kernel é tipicamente mais complexa do que uma aplicação “média” — entre outras coisas — requer uma análise que vai além do modelo básico do COCOMO. Um aplicativo de espaço do usuário como o Mozilla, por exemplo, é muito mais fácil de codificar linha por linha, já que é abstraído em um nível muito mais alto e tem que lidar com muito menos tarefas. Um kernel de sistema operacional moderno e de classe empresarial é solicitado a fazer um grande número de coisas extremamente complexas, todas de uma vez.

Wheeler explica que, em vez de usar o método padrão usado para analisar todos os elementos de uma distribuição, deve-se usar o modelo COCOMO intermediário para contar apenas o kernel. O método intermediário tem mais variáveis para escolher e, portanto, deve ser mais preciso para analisar um software complexo por conta própria. No artigo de 2004, ele detalha suas estimativas para esses parâmetros, que têm o efeito líquido de ajustar o valor do fator de esforço geral no SLOCCount do padrão de 3 para um novo valor de 4.64607. Ao mesmo tempo, o valor expoente de — esforço também é alterado para 1,12, que é o valor atribuído a projetos de software semideminados no modelo intermediário de estimativa de software COCOMO.

Com esses novos parâmetros em mente, um teste separado foi executado no kernel Linux padrão que foi incluído no Fedora 9, linux-2.6.25.i686:

Linhas de código fonte físicas totais (SLOC)

**6,772,902**

(Modelo básico COCOMO, Pessoa-meses = 2,4 * (KSLOC ** 1,05))

**7557.4 (90688.77)**

Estimativa do cronograma, anos (meses)
(Modelo básico de COCOMO, Meses = 2,5 * (pessoa-meses ** 0,38))

**15.95 (191.34)**

Número médio estimado de desenvolvedores (esforço / cronograma)

**473.96**

Custo total estimado para desenvolver

**$1,372,340,206**


## Limitações e vantagens para a abordagem deste estudo

Não existe uma maneira perfeita de estimar o valor de algo tão complexo e evolutivo quanto o Linux. Embora este método seja a melhor abordagem, ele provavelmente supera alguns aspectos de valor, enquanto subestima os outros. Aqui está um resumo dessas limitações:

- **O modelo COCOMO foi projetado a partir de pesquisas sobre desenvolvimento de software proprietário**


Por causa disso, sentimos que isso subestima a complexidade de testes inerente a projetos de software de código aberto desenvolvidos colaborativamente como o Linux. Devido às grandes quantidades de mudanças, pequenas e grandes, e à natureza distribuída de desenvolvedores e projetos independentes, a carga de testes nos participantes do ecossistema Linux é em uma ordem de magnitude mais alta do que para empresas proprietárias autônomas.

- **Outra dificuldade em medir o valor de uma distribuição Linux é simplesmente determinar o que compreende uma distribuição Linux para começar**


Incluímos todos os pacotes no repositório público de código fonte do Fedora. Mas certamente existem distribuições menores até mesmo do Fedora (a versão do LiveCD, por exemplo). Existem também distribuições maiores; O repositório do Debian GNU / Linux13 é maior que o do Fedora, por exemplo. Há também uma grande quantidade de software de código aberto que não é encontrado em nenhuma das distribuições. É um grande universo de código aberto, por isso tentamos confiar nos pacotes disponíveis de uma distribuição.

- **A maior fraqueza na análise de SLOC é seu foco em adições líquidas a projetos de software**


Qualquer um que esteja familiarizado com o desenvolvimento do kernel, por exemplo, percebe que o maior custo de energia do homem em seu desenvolvimento é quando o código é excluído e modificado. A quantidade de esforço necessário para excluir e alterar o código, e não apenas adicioná-lo, não se reflete nos valores associados a essa estimativa. Como em um modelo de desenvolvimento colaborativo, o código é desenvolvido e, em seguida, alterado e excluído, o valor real é muito maior que a base de código existente. Basta pensar no processo: quando algumas linhas de código são adicionadas ao kernel, por exemplo, muitas outras precisam ser modificadas para serem compatíveis com essa mudança. O trabalho que envolve a compreensão das dependências e dos resultados e a alteração desse código não está bem representado neste estudo.


- **O desenvolvimento colaborativo significa que você geralmente terá vários indivíduos ou grupos trabalhando em diferentes abordagens para resolver o mesmo problema técnico com apenas uma dessas abordagens “ganhando” a inclusão na versão final**


Como as abordagens “perdedoras” não estão comprometidas com o produto final, essa abordagem não leva em conta o esforço de desenvolvimento para essas abordagens.


- **Existem significativas linhas de software de diferenças de código entre distribuições e até diferentes versões de distribuições, por isso é enganoso considerar que uma análise é a estimativa canônica do valor de “Linux”**

Existem muitas opções diferentes em que analisar e escolhemos apenas 1. Por essa razão, achamos que as estimativas de pacotes discretos que todas as distribuições compartilham (o kernel, por exemplo) são mais interessantes.

- **Infelizmente, esse método equivale a valor para quantidade**


A comunidade Linux leva o “inchaço” muito a sério, mas ao mesmo tempo o Linux contém muito código — como drivers antigos — não usado com muita frequência. No entanto, a inclusão desse código é importante, pois tanto o código específico da arquitetura quanto os drivers são incluídos no Linux (ao contrário de outros sistemas operacionais). Como efeito disso, esse número seria maior do que em outros sistemas operacionais que não incluam esses componentes no próprio sistema operacional.

- **Este estudo pressupõe que todo o desenvolvimento ocorreria nos EUA, com o custo associado do trabalho dos EUA**


A maior parte do desenvolvimento de software é de natureza global e seus custos de mão-de-obra variam de acordo.


- **Os números refletidos neste estudo representam quanto custaria desenvolver o software em uma distribuição Linux hoje, do zero**


É importante notar que isso estima o custo, mas não o valor, para o ecossistema maior, já que a mudança de uma tecnologia tão amplamente utilizada teria um impacto econômico enorme e de longo alcance.


## Como o Linux cresceu?

Este estudo também não leva em conta os custos anuais de desenvolvimento para atualizar e aumentar a base de código Linux. Com base nesses números (ou na experiência direta de qualquer pessoa com uma distribuição do Linux), é fácil ver como a funcionalidade incluída em uma distribuição do Linux explodiu nos últimos seis anos.

Por exemplo, o Fedora Linux 9 inclui pouco mais de 204 milhões de linhas de código de origem física (SLOC), em comparação com 30 milhões de linhas no Red Hat Linux 7.1 (lançado em 2002) e mais de 17 milhões de linhas na versão 6.2. Assim, em apenas seis anos, a base de código cresceu em 174 milhões de linhas de código. Usando o modelo de custo COCOMO, estimamos que o Fedora 9 tenha requerido cerca de 60.000 pessoas-ano de tempo de desenvolvimento (em comparação a 8.000 pessoas-ano para o Red Hat 7.1 e 4.500 pessoas-ano para a versão 6.2). Assim, o Fedora 9 representa um aumento de aproximadamente 680% no tamanho, um aumento de 750% no esforço e um aumento de 900% nos custos de desenvolvimento tradicionais sobre o Red Hat Linux 7.1. Isso se deve a um aumento no número de programas de software livre / software livre maduros e maduros disponíveis em todo o mundo. Esse crescimento mostra que o Linux tem um grande impulso: a adição contínua de pacotes de software livre fortalece o conjunto de aplicativos disponíveis para usuários Linux e, por sua vez, torna o Linux muito mais atraente como plataforma de computação.

A natureza modular do Linux (em sua composição de uma distribuição) também é aparente pela varredura da lista dos dez principais pacotes incluídos em uma distribuição. Dado o tempo e o interesse, seria interessante, por exemplo, analisar os principais componentes de uma distribuição Linux embarcada e os custos de desenvolvimento associados a esse segmento da computação.

O impacto na inovação do Linux não é medido apenas em linhas adicionais. Como o recente artigo “Quem escreve o kernel Linux” afirma: “Ao longo destes lançamentos, a equipe do kernel tem uma taxa de crescimento muito constante de cerca de 10% ao ano, um número muito impressionante dado o tamanho da árvore de código. Mas o kernel não está apenas crescendo. A cada alteração feita na árvore de origem do kernel, as linhas são adicionadas, modificadas e excluídas para realizar as alterações necessárias ”.

Embora o kernel do Linux provavelmente tenha uma taxa de mudança maior do que a maioria dos outros componentes do Linux, nossos números refletem que, como um todo, o Linux está crescendo e mudando a cada ano em um ritmo constante. Como o kernel do Linux é apenas um pequeno (mas muito importante) componente de uma distribuição Linux, os custos de desenvolvimento iterativo despejados no Linux por ano são substanciais, mas não são examinados neste estudo.


## Conclusões

Então, nós sabemos agora o que vale a pena o Linux? Embora possa não ser uma pergunta capaz de ser respondida completamente, algumas coisas são muito claras: O verdadeiro valor do Linux surge da capacidade de reutilizá-lo e da tremenda flexibilidade que ele cria.

Imagine um mundo da computação em que Linus Torvalds não permitisse (na verdade forçar) os usuários do Linux a permitir que outras pessoas reutilizassem suas contribuições. Haveria um Google se eles não tivessem o uso gratuito do Linux e a capacidade de modificá-lo para atender às suas necessidades? Poderia haver uma nova categoria em expansão de PCs ultra-móveis de menos de US $ 350 sem o uso gratuito de um software de US $ 10,8 bilhões? A Amazon seria capaz de construir sua nova linha de dispositivos de leitura Kindle sem uma parte gratuita de US $ 1,4 bilhão em pesquisa e desenvolvimento? Mais do que apenas dinheiro, o software em uma distribuição Linux representa o tempo. A economia em cada um desses exemplos não teria sido possível se essas empresas tivessem sido forçadas a pagar taxas de licença por dispositivo ou por servidor a qualquer empresa ou tivessem que dedicar os milhares de pessoas-ano de tempo de desenvolvimento para criar esse software.

O que podemos aprender com este estudo? Os custos substanciais de desenvolvimento representados em uma distribuição Linux baseada na comunidade refletem seu crescente valor e importância no mundo da computação. As empresas e indivíduos que trabalham em projetos relacionados ao Linux e criam esse valor lucram compartilhando a carga de desenvolvimento com seus pares (e às vezes com concorrentes). Cada vez mais está ficando claro que assumir essa carga de pesquisa e desenvolvimento individualmente, como a Microsoft fez, é um abordagem cara à construção de software. Embora a posição de monopólio no passado tenha permitido que eles financiem esse enorme desenvolvimento, acreditamos que, na competição futura das forças colaborativas, essa posição isolada será insustentável.

Como podemos ver neste estudo e através da explosão do Linux em todas as áreas da computação, o desenvolvimento colaborativo cria um enorme valor econômico. Empresas como a IBM, a Intel, a HP, a Fujitsu, a NEC, a Hitachi, a Google, a Novell, a Oracle, a Red Hat e muitas outras participaram e lucraram com o enorme ecossistema criado por este modelo aberto de desenvolvimento de software. Mas não se engane: enquanto as empresas participam, os indivíduos são tão importantes na expansão deste software e seu valor. É assim que tudo começou depois de tudo.


— — — — — — — — — — — — — — —-

Os dados neste documento foram gerados pelo SLOCCount, Copyright © 2001–2004 David A. Wheeler O SLOCCount é Software de Código Aberto / Software Livre, licenciado sob a GNU GPL.
SLOCCount vem com ABSOLUTAMENTE NENHUMA GARANTIA, e você está convidado a redistribuí-lo sob certas condições, conforme especificado pela licença GNU GPL; veja a documentação para detalhes.

— — — — — — — — — — — — — — — —

## Agradecimentos

Gostaríamos de agradecer às seguintes pessoas por revisar e fornecer feedback sobre este artigo: James Bottomley, Jon Corbet e David A. Wheeler.
