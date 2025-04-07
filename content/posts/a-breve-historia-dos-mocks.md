---
title: "A Breve Historia Dos Mocks"
date: 2019-12-29T00:00:00-03:00
tags: ["testes", "tech"]
---

> Texto original postado por Steve Freeman
> Disponível em: http://www.mockobjects.com/2009/09/brief-history-of-mock-objects.html

## Introdução

As ideias e conceitos por trás de objetos simulados (mocks) não se materializaram em um único dia. Há uma longa história de experimentação, discussão e colaboração entre muitos desenvolvedores diferentes que pegaram a semente de uma ideia e a transformaram em algo mais profundo. O resultado final deve ajudá-lo a desenvolver software; mas a história de fundo da “Criação dos objetos simulados” também é interessante — e também é um testemunho da dedicação das pessoas envolvidas. Espero que revisitar essa história também o inspire a desafiar seus pensamentos sobre o que é possível e a experimentar novas práticas.


## Origens

A história começou em uma rotatória perto da estação Archway, em Londres, no final de 1999. Naquela noite, vários membros de um grupo de arquitetura de software com sede em Londres se reuniram para discutir questões de software. A discussão se voltou para experiências com desenvolvimento ágil e mencionei o impacto que a escrita de testes pareciam ter sobre o nosso código. Isso foi antes da publicação do primeiro livro Extreme Programming, e equipes como a nossa ainda estavam explorando como fazer o desenvolvimento orientado a testes (TDD) — incluindo o que constituía um bom teste. Em particular, notei uma tendência de adicionar o método “getter” a nossos objetos para facilitar o teste. Isso parecia errado, uma vez que poderia ser visto como uma violação dos princípios orientados a objetos, então eu estava interessado nos pensamentos dos outros membros. A conversa foi bastante animada — principalmente centrada na tensão entre o pragmatismo nos testes e o puro design orientado a objetos. Também tivemos um exemplo recente de uma colega, Oli Bye, que excluiu a API do Java Servlet para testar um aplicativo da Web sem um servidor.

Lembro-me particularmente daquela noite de um diagrama grosseiro de uma cebola e sua metáfora em relação as muitas camadas de software, junto com o mantra “Sem Getters! Ponto!” A discussão girou em torno de como descascar com segurança e testar as camadas dessa cebola sem afetar seu design. A solução foi focar na composição dos componentes de software (o grupo havia discutido as idéias de Brad Cox sobre componentes de software muitas vezes antes). Foi uma colisão interessante de opiniões, e a ênfase na composição — agora referida como injeção de dependência — nos deu uma técnica para eliminar os getters que estávamos “pragmaticamente” adicionando aos objetos para que pudéssemos escrever testes para eles.

No dia seguinte, nossa pequena equipe na Connextra começou a colocar a ideia em prática. Removemos os getters das seções do nosso código e usamos uma estratégia de composição adicionando construtores que pegavam os objetos que queríamos testar via getters como parâmetros. A princípio, isso parecia complicado, e nossos dois recrutas recém-formados não estavam convencidos. Eu, no entanto, tinha um histórico em Smalltalk, então para mim a idéia de composição e delegação parecia certa. A imposição de uma regra de “sem getters” parecia uma maneira de obter uma sensação mais orientada a objetos na linguagem Java que estávamos usando.

Ficamos presos por vários dias e começamos a ver alguns padrões surgindo. Muitas de nossas conversas eram sobre a expectativa de que as coisas acontecessem entre nossos objetos, e frequentemente tínhamos variáveis com nomes como expectURL (URLesperada) e expectativa de serviço em nossos objetos injetados. Por outro lado, quando nossos testes falharam, estávamos cansados de entrar em um depurador para ver o que deu errado. Começamos a adicionar variáveis com nomes como realURL (URLreal) e actualServiceName (NomeAtualdoServiço) para permitir que os objetos de teste injetados gerem exceções com mensagens úteis. Imprimir os valores esperados e reais lado a lado nos mostrou imediatamente qual era o problema.

Ao longo de várias semanas, refatoramos essas idéias em um grupo de classes: ExpectationValue (ValorEsperado) para valores únicos, ExpectationList (ListaEsperada) para vários valores em uma ordem específica e ExpectationSet (ConjuntoEsperado) para valores exclusivos em qualquer ordem. Mais tarde, Tung Mac também adicionou o ExpectationCounter (ContadorDeEsperados) para situações em que não queríamos especificar valores explícitos, mas apenas contar o número de chamadas. Começou a parecer que algo interessante estava acontecendo, mas me pareceu tão óbvio que não havia muito o que descrever. Uma tarde, Peter Marks decidiu que deveríamos criar um nome para o que estávamos fazendo — para que pudéssemos ao menos empacotar o código — e, depois de algumas sugestões, propusesse “mock” (simulação). Poderíamos usá-lo tanto como substantivo quanto como verbo, e refatorou muito bem em nosso código, então o adotamos.

## Divulgando a palavra


Nessa época, também iniciamos o London Extreme Tuesday Club (XTC) para compartilhar experiências de Extreme Programming com outras equipes. Durante uma reunião, descrevi nossas experiências de refatoração e expliquei que sentia que isso ajudava nossos desenvolvedores juniores a escrever melhor código orientado a objetos. Terminei a história dizendo: “Mas essa é uma técnica tão óbvia que, com certeza, a maioria das pessoas o faz de qualquer maneira.” Steve apontou que as coisas mais óbvias nem sempre são tão óbvias e geralmente são difíceis de descrever. Ele pensou que isso poderia ser um ótimo trabalho se pudéssemos separar a madeira das árvores, então decidimos colaborar com outro membro do XTC (Philip Craig) e escrever algo para a conferência XP2000. Se nada mais, queríamos ir para Sardenha.

Começamos a separar as ideias e dar a elas um conjunto consistente de nomes, estudando exemplos de códigos reais para entender a essência da técnica. Reportamos novos conceitos que descobrimos para a base de código original da Connextra para validar sua eficácia. Foi um momento emocionante e lembro-me de que demoramos muitas noites para refinar nossas ideias — embora ainda estivéssemos lutando para criar um “arremesso” preciso para objetos simulados. Sabíamos como era usá-los para gerar ótimos códigos, mas descrever essa experiência para outros desenvolvedores que não faziam parte do XTC ainda era um desafio.

O jornal XP2000 e a biblioteca inicial de objetos simulados (mocks) teve uma recepção mista — para alguns foi revolucionário, para outros foi desnecessário. Em retrospecto, o fato de o Java não ter um bom Reflection quando começamos significava que muitas das etapas eram manuais ou aumentadas com ferramentas de geração de código. Isso afastou as pessoas — elas não conseguiram separar a idéia da implementação.


## Outra Geração


A história continua quando Nat Pryce pegou as idéias e as implementou em Ruby. Ele explorou o reflection do Ruby para escrever o que era esperado diretamente nos blocos de teste. Influenciado pelo seu trabalho de doutorado em protocolos entre componentes, sua biblioteca mudou a ênfase de fazer [asserts](https://pt.wikipedia.org/wiki/Asser%C3%A7%C3%A3o) em valores de parâmetro para fazer assert em mensagens enviadas entre objetos. Nat então portou sua implementação para Java, usando o novo tipo de Proxy no Java 1.3 e definindo o resultado esperado com objetos “restritos”. Quando Nat nos mostrou esse trabalho, ele imediatamente deu um estalo em nossas mentes.


Ele doou sua biblioteca para o projeto de mocks e visitou os escritórios do Connextra, onde trabalhamos juntos para adicionar recursos necessários aos desenvolvedores do Connextra.

Com Nat no escritório onde mocks estavam sendo usados constantemente, fomos levados a usar suas melhorias para fornecer mensagens de falha mais descritivas. Tínhamos visto nossos desenvolvedores ficarem atolados quando o motivo de uma falha no teste não era óbvio o suficiente (mais tarde, observamos que isso geralmente indicava que um objeto tinha muitas responsabilidades). Agora, as restrições nos permitiram escrever testes mais expressivos e com melhores diagnósticos de falhas, pois os objetos de restrição podiam explicar o que havia de errado. Por exemplo, uma falha em uma restrição stringBegins (StringComeça) pode produzir uma mensagem como:

```
Expected a string parameter beginning with "http" but was called with a value of "ftp.domain.com"S
```

(tradução do erro)

```
Esperava-se um parâmetro de sequência começando com "http"  mas foi chamado com um valor de "ftp.domain.com"
```


Lançamos a nova versão aprimorada da biblioteca de Nat sob o nome Dynamock.

À medida que aprimoramos a biblioteca, mais programadores começaram a usá-la, o que introduziu novos requisitos. Começamos a adicionar mais e mais opções à API até que, eventualmente, ficou muito difícil de manter — principalmente porque precisávamos oferecer suporte a várias versões do Java. Enquanto isso, Steve se cansava da duplicação na sintaxe necessária para configurar os valores esperados, então ele apresentou uma versão de chamadas em cascata em Smalltalk — várias chamadas para o mesmo objeto.

Então, Steve notou que em uma linguagem de tipo estaticamente como Java, uma cascata poderia retornar uma cadeia de interfaces para controlar quando os métodos são disponibilizados para quem os invocou — na verdade, poderíamos usar tipos para codificar um workflow. Steve também queria melhorar a experiência de programação, orientando a nova geração de IDEs para solicitar as opções “certas” de autocomplete.

Ao longo de um ano, Steve e Nat, com muita participação de todos nós, pressionaram bastante a ideia para produzir o jMock, uma API expressiva sobre a estrutura original do Dynamock. Isso também foi portado para C# como NMock. Em algum momento desse processo, eles perceberam que estavam realmente escrevendo uma linguagem em Java que poderia ser usada para descrever valores esperados; eles escreveram isso mais tarde em um artigo da OOPLSA


## Consolidação

Através da nossa experiência na Connextra e em outras empresas, e através de muitas apresentações, aprimoramos nosso entendimento e comunicação das ideias de objetos simulados. Steve (inspirado em alguns dos primeiros materiais de lean software) cunhou o termo “needs-driven development” (desenvolvimento orientado às necessidades) e Joe Walnes, outro colega, desenhou uma boa visualização das ilhas de objetos que se comunicavam. Joe também teve a ideia de usar objetos simulados para conduzir o design de interfaces entre objetos. Na época, estávamos lutando para promover a ideia de usar mocks como uma ferramenta de design; muitas pessoas (incluindo alguns autores) viram isso apenas como uma técnica para acelerar os testes de unidade. Joe cortou todas as barreiras conceituais com sua heurística simples de “Only mock types you own.” (Simule apenas os tipos que você possui).

Pegamos todas essas ideias e escrevemos um segundo documento da conferência, “Mock Roles not Objects” (simule papéis, não objetos). Nossa descrição inicial tinha se concentrado demais na implementação, enquanto a ideia crítica era que a técnica enfatizasse os papéis que os objetos desempenham um para o outro. Quando os desenvolvedores usam bem os objetos simulados, eu os observo desenhando diagramas do que eles querem testar ou usando cartões CRC para interpretar relacionamentos — eles se traduzem bem em objetos simulados e testes que conduzem o código necessário. Desde então, Nat e Steve reformularam o jMock para produzir o jMock2, e Joe extraiu restrições na biblioteca Hamcrest (agora adotada pela JUnit). Agora também há uma grande variedade de bibliotecas de mocks, em muitas linguagens diferentes.

Os resultados valeram o esforço. Acho que podemos finalmente dizer que agora existe uma técnica bem documentada e polida que ajuda você a escrever um software melhor. Desses humildes inícios, este livro resume anos de experiência de todos nós que colaboramos e adiciona os conhecimentos de programação de Steve e Nat e uma cuidadosa atenção aos detalhes para produzir algo que é maior que a soma de suas partes.
