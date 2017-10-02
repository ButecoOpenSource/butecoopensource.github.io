---
layout: wordpress
title: Codeception, testes em PHP para todos
excerpt: |
  Introdução explicando um pouco sobre o framework de testes Codeception para PHP
date: 2015-10-14 22:51:45
author: jonathanaschweder
permalink: /codeception-testes-em-php-para-todos/
image: /assets/wp-content/uploads/2015/10/logo2.png
categories:
  - Desenvolvimento
tags:
  - codeception
  - php
  - testes
---

Olá galera, tudo certo ?

<span class="message_content">Hoje veremos como utilizar o framework de teste chamado Codeception. Eu acabei esbarrando com essa ferramenta por acaso enquanto estava pesquisando ferramentas mais completas do que o PHPUnit para criar testes no PHP. Vamos lá então?
</span>

<!--more-->
<h3 style="text-align: center;">Instalação</h3>
Para instalar o Codeception é muito simples pessoal, basta a partir de qualquer pasta executar o seguinte comando:
<pre><code>composer require codeception/codeception</code></pre>
<em>    Observação: Caso você não conheça o composer, ele é um gerenciador as dependências para seus projetos, veja <a href="/controle-de-dependencia-em-php-usando-o-composer/" target="_blank">este post</a> falando sobre.</em>
<h3 style="text-align: center;">Começando...</h3>
Após o término da instalação, podemos verificar que o executável <strong>codecept</strong> reside na pasta <strong>"vendor/bin"</strong>. O primeiro comando necessário para utilizar a ferramenta é:
<pre><code>vendorbincodecept bootstrap</code></pre>
O comando acima criará em seu projeto a estrutura básica do framework. Devo salientar que com o codeception você pode criar testes unitários como no PHPUnit (inclusive por baixo dos panos ele o utiliza), testes de integração (que normalmente são testes que trabalham com o banco de dados) e ainda, testes de interface, que apesar de muitas pessoas darem pouca prioridade são tão importantes quantos os outros, pois testam a interface que o usuário utiliza.

Para exemplificar as funcionalidades do codeception mostrarei um exemplo com teste unitário.
<h3 style="text-align: center;">Testes Unitários</h3>
Testes unitários, como o próprio nome diz, são testes que querem validar uma parte única da sua aplicação, normalmente um teste unitário verifica os "caminhos" que sua aplicação pode tomar.

A primeira coisa a se fazer ao começar a escrever testes, sejam eles unitários ou não, no codeception é criar uma suíte de testes, que é basicamente um agrupamento nomeado de seus testes. Para isso, execute o comando abaixo:
<pre><code>vendorbincodecept generate:suite exemplos</code></pre>
O comando criará uma nova suíte de testes chamada <strong>"exemplos"</strong>. Antes de prosseguir, precisamos criar algo para testar, então vamos criar uma clássica classe <strong>"Calculadora"</strong> que possui um método chamado <strong>"soma"</strong>. Segue o arquivo de exemplo abaixo:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/codeception//src/Calculadora.php?lang=php&amp;style=github" type="text/javascript"></script>Uma vez criada essa classe, precisamos agora rodar o seguinte comando para criar uma classe de teste unitário:

<pre><code>vendor/bin/codecept generate:phpunit exemplos CalculadoraTest
</code></pre>

O comando criará a classe de teste <strong>"CalculadoraTest"</strong> no diretório <strong>"tests/exemplos"</strong>. Ao abrir este arquivo você verá que existem alguns métodos já criados, sendo eles: <strong>setUp</strong>, <strong>tearDown</strong> e <strong>testMe</strong>. O método "setUp" é executado ao iniciar a execução dos testes da classe. Neste ponto é comum criar conexão com o banco de dados, inicializar variáveis, importar arquivos, etc. O método "tearDown", é executado ao final da execução dos testes da classe atual, normalmente é usado para liberar algum recurso anteriormente alocado, como desconectar do banco de dados. O último é um método criado pelo codeception como exemplo, e será daqui que partimos. Agora que temos uma estrutura básica, podemos finalmente começar a escrever nossos testes unitários. Comece alterando o nome do método <strong>testMe</strong>, para <strong>"testSoma"</strong>, indicando que a função deste método é testar a função soma da classe <em>Calculadora</em>. Em seguida vamos usar uma das funções do PHPUnit para comparar o resultado retornado por uma função, chamada <strong>assertEquals</strong>, que em tradução livre seria algo como <strong>"afirmar que o resultado é igual a"</strong>. Segue abaixo o resultado de como deve ficar a classe de teste:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/codeception//tests/exemplos/CalculadoraTest.php?lang=php&amp;style=github" type="text/javascript"></script>
<em>Observação: Veja mais comandos do PHPUnit <a href="https://phpunit.de/manual/current/pt_br/appendixes.assertions.html" target="_blank">neste link</a>.</em>P

Agora vamos rodar o comando de build do codeception:
<pre><code>vendor/bin/codecept build
</code></pre>
E finalmente rodar nossos testes:
<pre><code>vendor/bin/codecept run
</code></pre>
A saída do comando deve se parecer com imagem abaixo:
<a href="/assets/wp-content/uploads/2015/10/resultado_codeception.jpg"><img class="size-medium wp-image-3671 aligncenter" src="/assets/wp-content/uploads/2015/10/resultado_codeception-300x192.jpg" alt="Resultado da execução do comando run" width="300" height="192" /></a>

Como pode-se ver na imagem a mensagem <em>OK (1 test, 1 assertion)</em> indica que todos os testes passaram, e a mensagem "CalculadoraTest::testSoma" indica que o método "testSoma" da classe "CalculadoraTest" que criamos, foi executado sem errors.

Bem pessoal, este é o primeiro post referente ao Codeception, um framework completo para testes, espero que tenham gostado. Aguardem os próximos posts e acompanhem as novidades do ButecoOpenSource. Até lá!