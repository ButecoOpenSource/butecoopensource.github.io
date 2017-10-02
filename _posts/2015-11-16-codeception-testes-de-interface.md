---
layout: wordpress
title: Codeception, testes de interface
date: 2015-11-16 22:48:05
author: jonathanaschweder
permalink: /codeception-testes-de-interface/
image: /assets/wp-content/uploads/2015/11/codeception-logo.png
categories:
  - Desenvolvimento
tags:
  - codeception
  - php
  - testes
---

Fala galera,

Mais uma vez falando sobre o <a href="http://codeception.com/" target="_blank">Codeception</a>, no post passado mostrei como fazer o setup inicial e como começar a usá lo com testes unitários. Clique <a href="/?p=3182" target="_blank">aqui</a> para ver o post anterior.

Testes unitários são provavelmente o primeiro tipo de teste que você vai ver em qualquer tutorial, são os testes mais simples de serem feitos e provavelmente, os mais importantes. São os testes unitários que vão testar as suas funções, as suas classes, as suas regras de negócio e sua integração com o banco. Para este último, apesar de na prática não há diferença, existe uma especialização dos testes unitários, que são os testes de integração. A diferença entre um teste unitário e de integração é basicamente que o teste de integração faz acesso a um recurso externo, seja ele um banco de dados, uma API, ou qualquer outra coisa. Não irei abordar esse tipo de teste aqui, pois na prática os testes de integração são testes unitários.
<!--more-->

Continuando, vamos a uma categoria de testes que muitos não dão importância, porém é simplesmente essa categoria que garante a experiência do usuário, que são os chamados testes de interface. Testes de interface comumente verificam os elementos HTML na tela, podendo verificar propriedades, conteúdo e tudo mais.

Uma das grandes vantagens do Codeception que eu vejo sobre o PHPUnit puro, é que ele é muito mais completo, podendo abordar uma gama muito maior de cenários, formas diferentes de acesso, minimizando as brechas. O exemplo que vou dar a seguir é um teste que acessará a página do usuário no facebook.
<p style="text-align: center;"><strong>Começando...</strong></p>
<p style="text-align: left;">Antes de mais nada vamos criar um novo projeto com o composer, crie uma pasta qualquer e execute o comando abaixo<em>.</em></p>

<pre>composer require codeception/codeception</pre>
Logo após vamos criar a estrutura inicial do Codeception com o comando abaixo:
<pre>vendorbincodecept bootstrap</pre>
Agora vamos criar nosso teste de interface. No Codeception os testes de interface são chamados de testes de aceitação, ou em inglês "acceptance". Para isso execute o seguinte comando:
<pre>vendorbincodecept generate:cept acceptance LoginFacebook</pre>
Isto criará o arquivo <strong>"tests/acceptance/LoginFacebookCept.php"</strong>, abrindo o arquivo você verá a seguinte linha:
<pre>$I = new AcceptanceTester($scenario);</pre>
Nesta linha é criado um objeto da classe AcceptanceTester, que nada mais é que uma das classes de teste do Codeception> Vamos ver alguns comandos disponíveis logo mais, observe o nome dado a variável do objeto: $I. Esta variável é bastante usada na documentação do Codeception, simulando a ação do usuário. Então se você quiser que o usuário clique em algo você pode dizer <strong>"$I-&gt;click('Salvar');"</strong>, dizendo para o usuário clicar no botão com o texto <strong>"Salvar"</strong>.

Veja abaixo o código completo que conecta no Facebook e posta uma mensagem:
<pre>$I = new AcceptanceTester($scenario); $I-&gt;wantTo('Fazer login no facebook e ver o próprio nome');
$I-&gt;amOnPage('/login');
$I-&gt;seeInCurrentUrl('/login');
$I-&gt;fillField('email','usuario@dominio.com');
$I-&gt;fillField('pass','******');
$I-&gt;click('login');
$I-&gt;seeInCurrentUrl('/');
$I-&gt;see('Nome do Usuário');
</pre>
Obviamente você deve mudar os valores para seu usuário e senha. Antes de rodar esse teste altere o arquivo "acceptance.suite.yml" de "url:" para "url: https://www.facebook.com/", assim o comando "$I-&gt;amOnPage()" considera como base a URL "https://www.facebook.com".

Para rodar esse teste execute aquele mesmo comando que vimos no post passado:
<pre>vendorbincodecept run</pre>
Se tudo der certo, será mostrada uma mensagem dizendo que o teste passou, do contrário uma mensagem dizendo "fail" aparecerá com o erro.

Este foi um teste muito simples com o Codeception, mas podemos ter uma noção básica dos seus comandos, cada linha e comando é auto descritiva, pode ser traduzida literalmente, assim comandos como o $I-&gt;click('login') indicam, "Eu clico no botão login".

Pessoal, esta foi uma breve introdução a parte de testes com interface do Codeception, comente o que achou nos comentários, critique, sugira, estamos aqui para ouvir, ou melhor ler. Até a próxima.