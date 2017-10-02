---
layout: wordpress
title: Gerando bitlink atravéz da API do Bitly
excerpt: |
  Gerar link curto é uma tarefa um tanto quanto rotineira em determinados casos. Por exemplo, nós do blog usamos links curtos para compartilhar nossas publicações nas rede sociais.
  Bem, mas como fazer para gerar um link curto do Bitly via API e com um domínio customizado? Veja nosso artigo para saber mais.
date: 2016-02-19 16:52:31
author: alexandrevicenzi
permalink: /gerando-bitlink-atravez-da-api-do-bitly/
image: /assets/wp-content/uploads/2016/02/bitly_logo_small.png
categories:
  - Desenvolvimento
tags:
  - bitlinks
  - bitly
  - python
  - requests
---

Gerar link curto é uma tarefa um tanto quanto rotineira em determinados casos. Por exemplo, nós do blog usamos links curtos para compartilhar nossas publicações nas rede sociais.

Bem, mas como fazer para gerar um link curto do <a href="https://bitly.com/" target="_blank">Bitly</a> via API e com um domínio customizado? Se você não reparou ainda, nossos links curtos são sempre com o domínio <em>buteco.me</em>, ao invéz do tão popular <em>bit.ly</em>. Se você se pergunta o porque de usar um outro domínio, bem a resposta é simples, isso ajuda na identidade visual de sua marca ou produto.

<!--more-->

Antes de começar é necessário alguns itens:
<ul>
	<li>Domínio próprio</li>
	<li>Conta no Bitly</li>
	<li><a href="https://bitly.com/a/oauth_apps" target="_blank">Token de acesso a API do Bitly</a></li>
	<li>Configurar o Bitly para aceitar o uso de <a href="https://bitly.com/a/settings/advanced" target="_blank">domínio customizado</a></li>
</ul>
Agora que você configurou a sua conta do Bitly, vamos entender e como fazer a geração de Bitlinks. Com o comando abaixo podemos gerar bilinks através do cURL:

<code>curl https://api-ssl.bitly.com/v3/shorten?access_token=&lt;TOKEN&gt;&amp;longUrl=&lt;URL LONGA&gt;&amp;domain=&lt;SEU DOMÍNIO&gt;</code>

E o resultado será algo assim:

<samp>{ "status_code": 200, "status_txt": "OK", "data": { "long_url": "https://bitly.com/", "url": "http://bit.ly/1R8U2qo", "hash": "1R8U2qo", "global_hash": "mxkFBv", "new_hash": 0 } }</samp>

Na prática isto não é muito agradável, mas ajuda a entender para que URL devemos fazer o request para obter o link curto e como tratar o response. Se você deseja saber mais, visite a <a href="http://dev.bitly.com/links.html" target="_blank">documentação da API do Bitly</a>.

Agora vamos ao exemplo em Python, que facilita a geração de links curtos. Para facilitar o desenvolvimento, eu utilizei a biblioteca <a href="http://docs.python-requests.org/en/master/" target="_blank">requests</a>, uma das bibliotecas mais populares do Python. Confira abaixo:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/bitly.py?branch=master" type="text/javascript"></script>

O seu uso é bem simples, basta instanciar a classe e chamar o método <code>shorten</code>, como abaixo:

<code>Bitly('TOKEN', 'DOMÍNIO').shorten('URL LONGA')</code>

Como podemos observar no método <code>shorten</code>, fazemos uma requisição GET para a API do Bitly passando o <em>domain</em>, <em>access_token</em>, <em>longURL</em> e <em>format</em>. Após efetuar o request, esperamos que este tenha sucesso e retorne o código 200, junto com um payload JSON que contém a URL. Se o retorno for diferente de 200, isto indica algum erro, pode ser no request, no token ou própria indisponibilidade do Bitly. Geralmente o payload de erro inclui uma mensagem identificando o problema.

Por hoje é isso pessoal. Se você quer ajuda para fazer uso da API do Bitly em outra linguagem de programação deixe um comentário. :)