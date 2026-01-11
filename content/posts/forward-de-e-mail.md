+++
title = "Forward de E-mail"
date = 2026-01-11T13:27:40-03:00
[comments]
host = "bolha.us"
username = "dunossauro"
id = 115877575748149424
+++

No meu pequeno [degoogle](https://en.wikipedia.org/wiki/DeGoogle) de cada dia, tenho feito alguns testes em diferentes empresas de e-mail. Testei coisas como o [tuta](https://tuta.com/), o [proton](https://proton.me/), o [zoho](www.zoho.com), o [fast](https://www.fastmail.com/).[^1]

O grande problema disso é que testar significa que vou usar essa conta de e-mail por algum tempo. Mas é praticamente impossível migrar de contas de e-mail quando as pessoas têm **a porcaria** da minha conta de e-mail vinculada a uma empresa. Como faço pra quem tem meu endereço na empresa x "atualizar" a lista dele para me mandar na empresa Y?

Tudo bem... alguém vai dizer que eu poderia enviar meus e-mails automaticamente de uma conta pra outra. E de fato eu poderia. Mas, no final das contas, tudo fica inviável. Principalmente se eu cometer o erro de cadastrar meu e-mail em algum serviço e tiver que lembrar em qual porcaria de e-mail criei a conta lá.

Bom... eu já tenho um domínio, esse que fala, o [dunossauro.com](https://dunossauro.com). Por que não me aproveitar disso? E, de fato, eu posso. Assim, sempre que alguém precisar falar comigo, eu poderia enviar meu e-mail pessoal, usando meu domínio. Uma coisa que provavelmente não vai mudar[^2].

Comecei a procurar algumas alternativas para fazer o redirecionamento do meu domínio para qualquer e-mail X que eu esteja usando. Nisso acabei encontrando o [forwardemail](https://forwardemail.net). Uma solução gratuita para encaminhamento, de [código aberto](https://github.com/forwardemail/forwardemail.net). E que, se quiser, pagar também pode[^3]!


Que me permite, via DNS, onde quer que se encontre o meu domínio, redirecionar o tráfego para onde quer que eu esteja usando o e-mail. Com uma belíssima solução:

| Name | Type | Priority | Answer / Value                         |
|------|------|----------|----------------------------------------|
| @    | MX   | 10       | mx1.forwardemail.net                   |
| @    | MX   | 10       | mx2.forwardemail.net                   |
| @    | TXT  |          | forward-email=seuemail@onde.quiser.com |

Pronto! Agora, posso usar qualquer serviço de e-mail sem me preocupar em passar meu endereço de e-mail nesse serviço.

Uma das coisas legais nisso é que posso ter uma quantidade infinita *alias* de e-mails malucos e redirecionar todos para o mesmo.

- `span@dunossauro.com`
- `aplicaoxpto@dunossauro.com`
- `email@dunossauro.com`


Mas é isso... problema resolvido. Se você também tiver um domínio, pode ser bastante interessante. Por alguns motivos:

1. Ninguém precisa saber onde você hospeda sem e-mail
2. Você pode mudar de provedor quando quiser
3. Pode criar alias malucos para qualquer e-mail maluco que tiver na cabeça
4. É muito mais legal passar o e-mail do seu domínio do que fazer propaganda pra uma empresa qualquer :)


[^1]: Sim... eu não me odeio o suficiente, **ainda**, pra fazer hosting do meu próprio e-mail.
[^2]: Claro, eu poderia parar de pagar o domínio e tudo isso vir por água abaixo. Mas até então, qualquer domínio de empresa poderia cair também.
[^3]: O que pode acontecer no futuro se eu quiser também responder com emails do dunossauro.com
