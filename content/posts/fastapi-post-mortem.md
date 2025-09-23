+++
title = "Curso de FastAPI, post-mortem: como foi a minha experiência criando material financiado coletivamente"
date = 2025-09-23T00:04:14-03:00
tags = ["vida", "tech", "python"]
[comments]
host = "bolha.us"
username = "dunossauro"
id = 114519160838217520
+++

Faz uns poucos meses que o [curso de FastAPI](https://fastapidozero.dunossauro.com/estavel/) acabou. Meu objetivo com esse texto é repensar um pouco sobre tudo que aconteceu. Os pontos positivos, negativos, os aprendizados e claro... sobre a dor que foi passar por um período de 3 anos de cobranças internas excessivas.

{{< figure src="/images/fast_api_anim_frame.png" title="Um frame da animação de abertura dos vídeos que nunca foram lançados">}}

O resultado foi muito positivo, o curso foi um sucesso, o material virou meu xodó e motivo de orgulho. Mas... foram tempos sombrios!

## Um pouco de história

No segundo semestre de 2021, pensei: "que tal fazer um curso de FastAPI?" e mais do que isso, "por que não ensinar de uma forma que englobe o python mais moderno e os 'agregados' como banco de dados, testes, CI, deploy...?".

Lembro de ter dito algo parecido com isso para minha parceira:

> "Acho que se eu trabalhar umas 10 horas por semana, eu devo conseguir preparar todo esse material em uns 3 meses... Aí eu tiro uma semana e gravo todos os vídeos e vou editando por demanda..."

*ps: a resposta dela paira mais perto da realidade do que aconteceu.*

Spoiler, estou escrevendo esse texto no dia 21 de setembro de 2025. Bom... o objetivo desse texto é desbravar essa jornada que teve um final feliz, tanto quanto traumático.


### Linha do tempo dos acontecimentos

Uma das coisas que mais me ajudou a escrever esse texto e entender meus sentimentos mistos, talvez, quem sabe, fazer com que não seja tão duro comigo mesmo, foi escrever uma linha do tempo. Por esse motivo, vou deixar ela aqui:

- 13 de dezembro de 2021: começo a escrever a estrutura do curso
- 14 de janeiro de 2022: início dos trabalhos de assets 3d para usar na campanha
- 9 de fevereiro de 2022: foi lançada a [campanha de financiamento coletivo](https://apoia.se/fastapi)
- 11 de fevereiro de 2022: a meta de 12k foi batida
- 9 de março de 2022: A campanha se encerra com quase 200% do valor inicial
- 31 de março de 2022: Definida a estrutura inicial do curso em vídeo ([link](https://github.com/dunossauro/curso-fastAPI/commit/2a8df440d1514bd2942683a566a078853bbfeffc))
- 29 de abril de 2022: início da escrita do material de apoio (typing + async)
- 4 de junho de 2022: início da gravação da primeira aula
- 06 de julho de 2022: faço upload das primeiras quatro aulas gravadas de forma privada
- 10 de julho de 2022: [anuncio da versão 2.0 do pydantic](https://pydantic.dev/articles/pydantic-v2) com quebra de retrocompatibilidade, planejada para outubro
- 11 de julho de 2022: choro no banho a primeira vez
- 12 de setembro de 2022: a mensagem **maldita** foi pinada no grupo do telegram
- 13 de outubro de 2022: iniciado o processo de lançamento do sqlalchemy 2.0
- 26 de janeiro de 2023: lançada a versão 2.0 do sqlalchemy
- 30 de junho de 2023: lançada a versão 2.0 do pydantic (planejada para 2022)
- 1 de julho de 2023: o **caos** foi instaurado na minha mente
- 7 de julho de 2023: fastapi adiciona suporte ao pydantic v2 (v0.100)
- 13 de julho de 2023: [commit inicial](https://github.com/dunossauro/fastapi-do-zero/commit/5f9cd643f93237574b3f7ecf18484aa7e3332ace) do material de [texto](https://fastapidozero.dunossauro.com/)
- 17 de julho de 2024: Apresento publicamente a página do curso em texto
- 23 de novembro de 2023: "Desisto" de escrever o material de apoio (typing + async)
- 8 de junho de 2024: Lançada a [v1](https://github.com/dunossauro/fastapi-do-zero/releases/tag/v1.0) do material de texto
- 11 de junho de 2024: Foi feita a live da [aula de abertura](https://youtu.be/QShMRcicxnE)
- 6 de outubro de 2024: [v2](https://github.com/dunossauro/fastapi-do-zero/releases/tag/v2.0) do material de texto. Com merge das ideias principais sobre async do material de apoio
- 29 de janeiro de 2025: Foi iniciado o [changelog](https://github.com/dunossauro/fastapi-do-zero/commit/cca25c14b46ba2a3d1868eae1ba0d6c2ec33c1ec) no texto
- 2 de fevereiro de 2025: [v3](https://github.com/dunossauro/fastapi-do-zero/releases/tag/v3.0.0) do material de texto
- 6 de maio de 2025: Foi feita a live da [aula de abertura](https://youtu.be/ImhYlISeWPQ)
- 12 de março de 2025: Lançamento da [v4](https://github.com/dunossauro/fastapi-do-zero/releases/tag/v4.0) do material de texto


## A campanha

A forma que encontrei para viabilizar a criação desse material foi por meio da campanha de [financiamento coletivo](https://apoia.se/fastapi). Uma campanha tudo ou nada, ou seja, se a meta fosse atingida, eu focaria energias para produzir o material, caso contrário, nada aconteceria.

Embora eu mantenha há anos a campanha da [live de python](https://apoia.se/livedepython), para ser bem sincero, eu não acreditei que em um mês a meta de 12k fosse atingida. Pra minha surpresa, não só foi atingida, como isso aconteceu em 26 horas!

### O dinheiro

Meu trabalho em tempo integral é produzir o material semanal da live de python. O que me toma cerca de 40/50 horas por semana. Entre o levantamento do tema, referências, testes, o estudo, a criação do material, a parte gráfica e a apresentação da live na segunda-feira.

Parar de produzir as lives por um período, ou diminuir o ritmo, faria meu canal ser penalizado pelo youtube, o que diminuiria significativamente a minha renda durante a produção do material. Pensei que esse valor seria o suficiente para cobrir a não entrada de grana do youtube num período máximo de 7 meses[^1].

### A receptividade

O quanto as pessoas engajaram na causa e ficaram felizes pela produção desse material mexeu tanto comigo, de uma forma positiva. Me mostrou que as pessoas confiam na qualidade do meu trabalho e também confiaram que eu entregaria algo de valor.

Foi espetacular e um prazer inenarrável ver o quanto sou bem quisto pela nossa comunidade! De verdade, isso foi tão lindo. Durante as partes difíceis do processo, reli algumas mensagens que as pessoas me mandaram, alguns comentários que foram deixados e isso me ajudou **MUITO**.

### A responsabilidade

> O diabo mora nos detalhes...

Bom, com a excelente receptividade, logo veio um senso de cobrança **insano**. Onde tudo deveria estar perfeito, calculado, nos mínimos detalhes, absurdamente correto, com direito a APIs internas sendo debruçadas.

Com isso, comecei a escrever um material de apoio profundo, aquele tipo de coisa que quem conhece meu trabalho mais de perto sabe como funciona. Eu estava debatendo comigo e escrevendo sobre o fato do interpretado reconhecer uma chamada na pilha e fazer o processo de quickening...

Onde estava o FastAPI? Não sei... eu me perdi na escrita do material de apoio logo no início. Acho que isso vem de uma frustração anterior, como o [curso de selenium](https://selenium.dunossauro.com/), que não teve o aprofundamento teórico necessário[^2].

Depois de escrever algumas semanas em que dormi quase nada, um material que não teve nenhum aproveitamento...

### A cobrança interna

Bateu na minha cabeça uma pira de que eu deveria entregar isso de outra forma, como prometido na campanha. Um curso em vídeo, não um material extenso de texto com noias perfectionistas que só dizem respeito a minha ansiedade.

Montei e desmontei toda a fotografia/iluminação. Montei da forma mais "perfeita" que consegui. Anotei todos os parâmetros, fiz os slides com alguns roteiros anteriores e fui gravar. Durante algumas semanas, fui fazendo isso. Gravando, editando e postando de forma privada.

Por que isso não virou público? Não é óbvio? A sabotagem de não ser o incrível perfeito aprofundado e bitolado pomposo e cheio de referências podia me fazer deletar tudo sem ninguém saber que isso tinha começado a ser feito.

## A maldição das majors

Quando achei que tudo tinha começado a andar rumo ao que foi prometido...

### Pydantic 2

Em 10 de julho de 2022 o Pydantic, componente central no curso e no FastAPI [anuncia a 2.0](https://pydantic.dev/articles/pydantic-v2) com quebra de retrocompatibilidade, reescrita em Rust.

Eu, como um bom [leitor de feeds](/posts/descentralizacao-de-consumo-na-internet/), li isso no mesmo dia em que sentei para iniciar a gravação da aula 05. O que me fez repensar sobre tudo que tinha sido feito até ali. A previsão inicial de lançamento era para outubro, no mais tardar ao fim do ano.

Isso inviabilizaria o produto final do curso. Sendo **bem positivo**[^3] com as datas, se eu continuasse gravando e postasse tudo, provavelmente os lançamentos das últimas aulas *combariam* com o lançamento do pydantic, o que, **exclusivamente na minha cabeça**, faria todo o projeto estar desatualizado no momento em que estava sendo lançado.

Com esse turbilhão na cabeça, postei a mensagem mais estranha do mundo no grupo do telegram do curso:

> "Galera, o curso ainda não tem data. Estou trabalhando nele diariamente. Quando tiver alguma evolução significativa. Vou avisar aqui no grupo. No momento estou trabalhando nisso em tempo integral. Fiquem em paz, que logo menos as coisas acontecem.
> 
> Estou trabalhando nos módulos iniciais ainda. O FastAPI está passando por algumas manutenções. Estou acompanhando de perto as novas mudanças do pydantic.
> 
> Sei que as pessoas aqui já estão cansadas de ouvir isso. Mas estou trabalhando. Estou mandando de novo essa mensagem pois toda hora entra alguém no grupo e pergunta de novo e a minha mensagem se perde. Então vou fixar essa mensagem.
> 
> Tô trabalhando bastante, tô ficando bastante feliz com o que está rolando. Em breve novidades, sem datas. Afinal, não temos datas nem para release do pydantic, que foi planejada de maneira otimista para dezembro.
> Estou aproveitando para trabalhar melhor e mais profundamente nos módulos iniciais. Prefiro postergar um pouco mais, do que deixar o curso com aulas desatualizadas.
>

Isso me fez retomar a escrita do material teórico, aquele aprofundado em nuances, ... Sim, aquele delírio insano da minha mente.

Ah... e sobre a versão 2, ela foi lançada em 30 de junho de 2023. Esperar por ela foi complicado.

### SQLAlchemy 2

Nesse material """incrível""" que estava escrevendo, fugindo totalmente do escopo inicial, passei grande parte trabalhando na interação do AsyncIO com o SQLAlchemy. Recém saído na versão 1.4.

No dia 13 de outubro de 2022, outro tombo. É anunciada a nova major do SQLAlchemy, a 2.0 (que acabou saindo em janeiro do ano seguinte). O que fez com que grande parte do material que trabalhei durante os meses estivesse obsoleta. Novas coisas foram inseridas, o suporte ao async melhorou, a integração com o typing estava incrível. Mas isso não me fez ter menos retrabalho...

O que me fez entrar em pânico novamente!

Embora tenha sido trabalhoso, acabou não sendo em vão, estar "acompanhando" cada commit e modificação originou uma das lives de python que eu mais gosto e considero uma das mais importantes que fiz no canal: ["SQLAlchemy: conceitos básicos, uma introdução a versão 2"](https://youtu.be/t4C1c62Z4Ag) e parte integral da v2 do texto do curso, quando o AsyncIO foi incluído.

{{< youtube t4C1c62Z4Ag >}}

### FastAPI 0.100

Em julho de 2023, o FastAPI adiciona o suporte ao pydantic v2. O que não demorou muito em relação ao lançamento da v2.


## Saúde mental

Com toda a demora, "futurologia" e trabalhando na "diagonal" do conteúdo. É claro que eu não estava feliz. As pessoas me cobravam? Claro que sim...

Mas o meu **MAIOR** inimigo fui eu mesmo. Eu não soube lidar com a pressão dos atrasos, começava e parava de fazer várias coisas que estavam "entorno" desse projeto, mas eu nunca encarava ele de frente. Eu estava com vergonha de conversar com as pessoas, eu estava com vergonha de "não ser suficiente". Enquanto as lives python aconteciam, eu me sentia **MUITO** mal. Isso não foi bom pra mim de maneira geral.

**Foi péssimo!**

E essa vergonha e culpa me fizeram eu me comunicar muito mal, mais que o normal. Com quem apoiou o projeto, com quem queria saber como estava o andamento, com quem **confiou que eu tinha capacidade de fazer esse curso**!

### O estopim da fúria

As pessoas sempre viviam me perguntando sobre o curso. Vendo agora em retrospecto, eu entendo que elas estavam curiosas sobre o que estava acontecendo, sobre o andamento. Nunca ninguém* me disse nada em tom de cobrança. Até porque eu andava fazendo lives na [twitch](https://www.twitch.tv/dunossauro) quase que diariamente, trabalhando no "material perfeito", aquele mesmo... a diagonal da diagonal.

No dia 1 de julho de 2023, recebi a mensagem de milhões no privado do telegram:

> "Já faz mais de um ano que a campanha acabou e você ainda não entregou o material e nem fala mais sobre isso. Você enganou todas as pessoas e eu investi 50 reais nesse material. Você me roubou!"

Reescrevi essa mensagem em um tom parecido com o que a pessoa usou, claro, além de ter sido chamado de ladrão. Vamos dizer que a pessoa me mandou tomar no *, me chamou de filho de você sabe quem, etc.

### A resposta a incidentes

Quando recebi essa mensagem, eu realmente entendi que eu "era um merda mesmo!". Chorei bastante nesse dia. Eu realmente era incapaz de lidar com essa situação.

Depois de horas de choro, que foram longas, eu cheguei a uma conclusão: "Quer saber... **FODA-SE**, eu vou fazer tudo de uma forma nova. Uma que eu consiga entregar o que as pessoas querem. Sem masturbação mental, sem caçar detalhes em APIs, em coisas estupidamente complexas que ninguém quer nem saber".

## O material em texto

Esse sentimento amargo na boca, a raiva e a cobrança forte me fizeram ir por outro caminho. Vendo em retrospecto, talvez esse caminho seja o que deveria ter sido tomado desde quando comecei a escrever o "maravilhoso profundo".

As coisas mudaram um pouco de rumo quando entendi que o material deveria ser diferente das rotineiras lives de python. No sentido de tentar destrinchar tudo, todo o tempo, com a complexidade que o tempo permitia. Esse projeto poderia se apoiar nas duzentas e algumas lives que já existiam. O curso poderia apontar tangentes que as lives tradicionais preencheriam.

No sentido de que ele deveria ser um **projeto** feito de ponta a ponta. Com todos os entornos colocados na ideia inicial. Banco de dados, Async, testes, CI, deploy, etc.

Nessa virada de chave, eu sentei e, em alguns poucos dias, esbocei as primeiras cinco aulas em formato de texto.

### Mas texto? Não eram vídeos?

Trabalhar com texto é extremamente mais exaustivo e complexo do que gravar os vídeos com um roteiro básico e ir no flow e editar tudo depois. Sendo bem sincero, acho que poder me esconder atrás de um monte de palavras parecia mais atraente no primeiro momento.

Não podia ter tomado uma decisão mais certeira do que essa! Embora o custo de escrever seja mais alto, corrigir o texto e fazer o deploy de páginas é extremamente mais fácil do que regravar uma aula e editar.

O interessante, no final das contas, é que acredito que o que gerou mais valor em tudo que foi produzido desse curso, o texto é de cara a coisa mais importante. Textos são acessíveis, nem todas as pessoas gostam de vídeos e claro, sim... **dá pra pesquisar no texto**.

#### O texto me permitiu mais do que isso

Mas do que as aulas, o texto me permitiu usar recursos interativos como os quizzes ao final das aulas. Essa foi uma das coisas mais elogiadas e que, durante as lives que assisti com as pessoas fazendo o curso pelo material de texto, elas sempre diziam que o carinho com o material era tão bom que até em "fixação do material" eu tinha pensado.

Claro, outras coisas incríveis puderam ser feitas. Muitas delas, graças ao `markdown-exec`, que me permitiu fazer coisas interativas que mantinham sempre tudo atualizado, datas, versões, execução de código...

As contribuições das pessoas foram incríveis. Corrigindo texto, legibilidade, erros de gramática, exercícios, fazendo sugestões. Isso fez o senso de comunidade em torno do material ser mais "ativa" no lugar da receptividade "depositária" dos vídeos.

#### Comunicação do material

Divulguei isso para os apoiadores no grupo do telegram no dia 17 de julho de 2023.

> Galera, só atualizando vocês dessa sprint maluca que eu disse que ia fazer nessa semana.
> Consegui roteirizar as aulas: https://fastapidozero.dunossauro.com/
> 
> Ainda tem bastante coisa pra ajustar isso pra ser um texto "claro" para referências, mas a progressão está toda aí.
>
> O repo para quem quiser furtricar, se quiser mandar alguma coisa. Tá tudo aqui:
>
> https://github.com/dunossauro/fastapi-do-zero
>
> Meu objetivo é começar a gravar tudo isso na quarta, vou tirar hoje e amanhã pra trabalhar nessa parte da composição visual (tipografia cores e etc...)

Sim... em um pouco mais de um ano, essa foi toda a comunicação "oficial" que fiz do material.

Não exatamente só essa, fomos bastante ativos no telegram durante esse ano. Papeando e conversando sobre todo o processo (nunca explicitamente como nesse texto), mas as pessoas sabiam do andamento das coisas. Mas eram conversas que se perdiam com facilidade no grupo.

#### Olhando pra trás

Olhando em retrospecto, fica claro pra mim que isso estava acontecendo desde que comecei a escrever o material de apoio. Mas a utilidade do material de apoio não fazia sentido na minha cabeça. Todo o tempo achei que estava "me enganando", fugindo do tópico central. Na verdade, era a melhor forma de expressar o que eu estava querendo, mas eu não estava com o caminho bem definido do que o curso **tinha que ser** em relação ao que eu achava que deveria ser.

### A volta dos vídeos que também não foram

Embora os textos estivessem no formato "perfeito" para acompanhar os vídeos e ser a base deles, no momento eu estava me sentindo um merda. Um ladrão...

Fui gravar de novo, como prometi no grupo de apoiadores. Dessa vez, já com a ideia do "projeto".

{{< figure src="/images/videos-fastapi.png" title="Os vídeos nunca lançados...">}}

Outro grupo de quatro aulas que nunca viram a luz do sol. Só que dessa vez, gravar não foi fácil. Eu tinha o roteiro do que eu queria, eu sabia como fazer, mas eu não conseguia.

Um dos episódios dessas gravações é muito claro na minha mente. Eu pedi pra minha parceira ficar no quarto comigo enquanto eu gravava. Eu estava perdendo o fôlego durante as falas, irritadiço. Eu não conseguia falar, eu estava me sentindo culpado o tempo todo.

Decidi tirar alguns dias sem gravar, pra tentar acalmar as ideias. Lembro que vomitei de nervoso duas vezes tentando gravar a quinta aula.

### Erros de comunicação

Sofri e me culpei em silêncio por bastante tempo, mas decidi, com a comunicação pífia, que eu iria escrever **TUDO** antes de tentar voltar a gravar. E fui fazendo o texto e postando os updates. A galera foi curtindo, foi dando os feedbacks, foi contribuindo com melhorias. Tudo isso foi ótimo, na minha cabeça confusa da época, e evitou que eu tivesse que falar abertamente dos motivos pelos quais os vídeos nunca saíram.

#### Acompanhamentos periódicos?

De todos os tópicos, esse é o que me dói mais. É um combo de vergonha e atraso sem fim. Na minha cabeça pairava que avisar "estou atrasado, mas estou fazendo X..." era péssimo.

Isso virava uma bola de neve na minha cabeça: "Pô, pq avisar? Eu ainda estou travado fazendo coisas que não devia enquanto espero as majors..."

Essa foi a pior escolha possível! Manter as pessoas informadas teria me tirado um peso tão grande das costas.

## Além do texto, as lives

Acho que nunca me recuperei do silêncio antes da primeira palma seguida por "Olá, boas-vindas ao curso de FastAPI" sem me sentir um bandido. Se eu não conseguiria fazer isso dessa forma, decidi que pelo menos a primeira apresentação do curso deveria ser síncrona. No sentido de que faríamos em lives, conversando e sem a pressão do silêncio, "você me roubou..."

Com isso, o material de texto foi andando durante quase um ano. Quando de fato anunciei, em 17 de abril de 2024, a data das lives e algum tempinho depois fechamos a v1.0 do material.

As lives foram divertidas, a galera super acompanhou, gostou do material, da forma final de como tudo ficou. Bastante gente fez os projetos.

## Final feliz, não?

Sabe aquele incômodo de **não estar "perfeito"**? Ele continuava a me massacrar. Eu "roubei" mesmo as pessoas... Eu disse que teriam coisas, e no final, elas não estavam no conteúdo.

Mas, afinal, o que estava faltando? O `asyncio`!

Eu dormia pensando nisso, acordava pensando nisso, tomava banho pensando nisso. Como pude fazer um curso todo sem falar sobre programação assíncrona? Passei meses escrevendo sobre isso, fizemos lives sobre o sqlalchemy assíncrono. Mas, no final, na correria de tentar entregar tudo o mais rápido possível[^4], eu me pressionei a não colocar mais aulas no texto.

Foi nessa espiral da desgraça que decidi que iria incluir uma nova aula no texto sobre programação assíncrona e que, depois dessa aula, que iria ser inserida no meio do material, todo o código deveria seguir de forma assíncrona.

Resultado? Mais retrabalho! Mas pensa **NO** retrabalho em revisar metade do curso, pensando em refazer explicações e alterando códigos...

Nessa hora, eu agradeci por ter feito tudo em texto... Isso pode me guiar pra fazer as coisas sem errar. Embora, talvez, eu nem precisasse ter feito nada disso, eu me sentia na obrigação.

Esse processo durou mais alguns meses, com isso foram marcadas outra saga de aulas síncronas. Que ficaram conhecidas como o "Curso de 2025".

Adicionei somente o `asyncio`? Você leu o texto até aqui... Você sabe que não. Eu revisei o material todo e aulas que tinham 15/20 minutos de leitura média se tornaram monstros de 40 minutos de leitura. Testes foram revisados, toda a interação com o banco de dados foi revisada, eventos, apêndices, novas questões nos quizzes... Bom... Foi um retrabalho danado.

Foi lançada a v2 do texto com todas essas alterações. Que foram levadas mais adiante e depois de mais reescrita, viraram a v3.

Finalmente, eu achei que estávamos perto do que eu queria, reescrevi mais um bocado e a v4 foi lançada e marcadas as datas das "reapresentações".

### Um acontecimento tardio, mas especial

Como me disse meu pai uma vez:

> "É só pegar o que sabe fazer de melhor. Se você for fazer pra você, pode ter certeza que vai sair mal feito"

Em 29 de janeiro de 2025, eu me dei conta do que poderia ter resolvido meses de angústia. Por que raios eu não fiz "logs" de trabalho? No que estava trabalhando, o como e com as datas. Isso poderia ter me poupado de tanto sofrimento. Uma página que fosse.

Nesse dia, eu introduzi o Towncrier no material de texto. O que acabou se tornando uma live de python ["Entendendo Changelogs: O que são, seus padrões e como gerá-los com Towncrier "](https://youtu.be/ATKJXpHrBfE).

{{< youtube ATKJXpHrBfE >}}

Olhando agora, não é como se eu nunca tivesse assistido/lido devlogs, principalmente de jogos. E também não tivesse escrito release notes e feito changelogs em projetos de código. É engraçado ver que eu deveria ter pensado nisso. Talvez esse tenha sido o meu maior aprendizado durante esse processo. Isso ajudaria a informar as pessoas, ter uma fonte única dos eventos e também ter aliviado MUITO estresse e ansiedade.

## Final feliz, não? [2]

Não... Algumas questões foram levantadas durante as apresentações, ccomo o fato de que dessa vez tinha menos gente do que da primeira vez ao vivo e as lives tinham a duração 1/4 maior, mais perguntas, mais formas de uso foram levantadas...

Resumo, o texto ganhou a v4.1.


## Depois disso tudo...

Bom... Demorou muito mais do que eu previa, eu acabei entrando em parafuso algumas vezes. Tento ver isso de dois pontos diferentes.

1. É que no final deu tudo certo, o material tem a qualidade que eu gostaria que tivesse, embora o "produto final" tenha se desenrolado completamente diferente do que eu imaginei no início.
2. Foi estupidamente desgastante e angustiante. O processo não foi bom.

### Erros

Se puder elencar os pontos onde mais errei, eu destacaria alguns.

#### Comunicação da campanha

Esse foi um erro cometido durante todo o processo. Desde a abertura da campanha. Não ficou claro pra muitas pessoas que se tratava de uma campanha "tudo ou nada". Que eu só começaria a trabalhar no material caso a campanha fosse bem sucedida.

Acredito que essa parte de "campanhas" seja meio que novidade para algumas pessoas e a "cultura" de comprar cursos também não ajuda muito. Grande parte achou que o material seria liberado ao final da campanha de um mês. Se tivesse deixado isso mais claro, talvez o início do trabalho teria sido menos frustrante pra mim.

#### Comunicação do processo

Como já mencionei algumas vezes ao longo desse texto, talvez se eu tivesse feito um "devlog" ou simplesmente uma página mantendo o processo, o que estava sendo feito, explicitamente claro, isso poderia ter sido evitado.

Ter "uma única fonte de verdade" foi o que mais faltou aqui. Lembro que, quando comecei os changelogs, isso me aliviou de uma forma absurda.

Se isso fosse pensado no início, eu poderia já ter deixado claro na divulgação da campanha.

#### Desespero

Acho que perdi a sanidade quando as coisas foram anunciando versões e eu não soube lidar com essas coisas. O que acabou me deixando extremamente frustrado e sem norte. Eu queria fazer, mas queria fazer "perfeito". Essa busca pelo inalcançável me machucou bastante.

Embora no final essa subsequência de acontecimentos e espera tenham me feito escrever, esse foi o maior trunfo de todo o material, na minha opinião.

#### Prazo

Bom... aqui eu errei rude. Eu não previ a complexidade das coisas porque eu pensei em algo e, na hora de executar, quis fazer de outra forma totalmente diferente. O fato de não ter uma data pra tudo estar "pronto" fez com que eu fosse me arrastando em projetos diagonais.

Eu colocaria um prazo, olhando de fora? Acredito que não, mas pontuar "checkpoints" de metas possíveis poderia ter me ajudado.

#### A entrega

No final, o que entreguei foi muito diferente do que foi prometido. As pessoas esperavam um curso em vídeo. Eu entreguei um mega material em texto e aulas síncronas.

Eu acho que a entrega final foi 200x melhor do que o que foi proposto, mas ainda assim não foi o que foi prometido.

#### timing

Convenhamos... Eu escolhi literalmente o PIOR momento pra fazer esse curso. É aquela coisa de estar no lugar errado e na hora errada.

Se eu tivesse começado antes ou alguns meses depois, o desenrolar das releases que foi o que mais me deixou maluco, tudo teria acontecido de outra forma.

### Acertos

Bom... Nem tudo deu errado. Talvez eu valorize mais essas coisas por terem sido duras demais pra mim durante o processo. Mas eu aprendi muito do que não fazer e de como fazer coisas melhores do que pensei que seria capaz de entregar.

#### A campanha

Claro, a campanha foi um grande acerto. Ver que as pessoas acreditam e confiam no material que eu desenvolvo, não tem preço. Saber que tem alguém que conta com você, que te incentiva... Isso faz toda a diferença.

Muitas das pessoas que contribuíram para o material, assim como na live de Python, de maneira geral, não esperavam pelo resultado. Contribuíram por saber que esse material contribuiria com o conhecimento de outras pessoas.

Pensar nisso agora me arrancou uma lágrima. A nossa comunidade, que é um subconjunto da comunidade de Python em geral, tem essa coisa incrível de sempre estar disposta, se permitir, contribuir com o crescimento das outras pessoas.


#### O texto

Você já deve ter cansado de me ouvir falar disso. Mas, de verdade, o material em texto é literalmente A MELHOR coisa que foi produzida por esse material.

Ele é um guia, um tutorial, um livro. É buscável, permitiu os quizzes, atualizações periódicas, o versionamento.

Olhando em retrospecto, eu não imagino como esse material seria sem o material de texto. Ele literalmente é a coisa mais rica que já produzi na vida. Sem brincadeira.

Eu já tinha me arriscado a escrever no passo, com o material de funcional (nunca terminado) e o material de ansible (usado para uma live apenas). Eu não consigo imaginar por que não pensei nisso antes.

---

Outro ponto aqui foi que ter o texto ativou o modo "pê errers" das pessoas. Elas pegaram o material para si e contribuíram MUITO. Grafia, sugestões de aula, fontes acessíveis, sugestões de ferramentas. Tudo que um projeto aberto é capaz de proporcionar.

#### Os changelogs

Ter uma fonte de verdade, do que está sendo feito, das pequenas entregas. Além de mostrar pras pessoas o progresso do que está acontecendo, me deram uma sensação de "olha, eu fiz alguma coisa essa semana". Que era um sentimento que me massacrava. Trabalhava às vezes por dias sem pausa e a sensação de não ter "feito nada" era sempre grande, o que me desmotivava muito.

### O presente com fatos!

Tanto o Pydantic quanto o SQLAlchemy ainda mantêm ativas, recebendo bugfixes, as versões 1 em setembro de 2025. Mesmo após anos da mudança de major... Ah, claro, o FastAPI ainda hoje 0.117.1 (2025) também suporta o pydantic v1 :)

Ou seja… eu estava desesperado tentando prever um futuro que hoje, três anos depois, não se concretizou.

Em algum momento, a mudança do poetry v1 -> v2 também foi alvo da minha preocupação, pois era a base do projeto. Olhando agora com menos desespero, é retrocompatível com `pyproject` antigo.

Coisas que pareciam o fim do mundo, que me deixam sentado no escuro sozinho.

## Eu faria isso de novo?

Responder isso é bem complicado.

Mesmo que tenha sido péssimo passar por esse processo, eu cresci muito como pessoa. Eu encontrei falhas nos meus processos, entendi como expor melhor as minhas ideias, ser mais transparente com os processos.

Talvez eu faça de novo, não em período curto. É bom deixar claro. Hahahahah

Embora tenha aprendido muito, esse processo me machucou bastante. O resultado foi positivo, vendo agora, após um tempo. Mas enquanto as coisas estavam acontecendo, eu não soube lidar com a maioria das coisas que aconteceram, no momento em que aconteciam pareciam socos no meu estômago.

Mas, eu faria tudo de forma diferente, se fosse uma nova coisa. Eu focaria no texto, na transparência, as aulas ficariam pro final, depois que tudo estivesse redondo.

No fim... o resultado me deixou bastante feliz e o processo me trouxe muita coisa ruim, mas aprendizados importantes pra lidar com essas coisas no futuro.

---

Pra vocês, como espectadores, como foi tudo isso? Eu adoraria saber.


[^1]: Mal sabia eu...
[^2]: Obviamente, essa opinião é compartilhada pelo total de zero pessoas, mas vive latejante na minha mente.
[^3]: Quanta ingenuidade... deus...
[^4]: Como se dois anos de espera não tivessem sido o suficiente...
