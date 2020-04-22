---
layout: wordpress
title: Laravel 5 do começo ao fim [parte 4]
excerpt: |
  Nesta quarta parte do tutorial veremos um pouco da parte de testes do Laravel 5, uma boa pratica que todos deveriam adotar mas que muitas vezes é simplesmente ignorada.
date: 2015-04-16 22:54:51
author: jaswdr
permalink: /laravel-5-do-comeco-ao-fim-parte-4/
image: /assets/wp-content/uploads/2015/02/Laravel-5.png
categories:
  - Desenvolvimento
tags:
  - framework
  - laravel
  - laravel 5
  - php
  - programação
  - testes
  - tutorial
  - web
---

Neste post veremos uma peça fundamental de um <em>workflow</em> que tento sempre seguir, o famoso "TDD", que em tradução livre ficaria algo como "Desenvolvimento Orientado a Testes", que seria a parte de teste com Laravel 5, caso não tenha visto, veja outras partes dessa série nos links abaixo:
<ul>
	<li><a href="/tutorial-laravel-5/" target="_blank">Parte 1</a></li>
	<li><a href="/tutorial-laravel-5-parte-2/" target="_blank">Parte 2</a></li>
	<li><a href="/laravel-5-do-comeco-ao-fim-parte-3/" target="_blank">Parte 3</a></li>
</ul>
Algo que muitos programadores simplesmente ignoram, seja por preguiça ou qualquer outro motivo obscuro, é a parte de automação de testes. Muitos ainda utilizam a velha prática de testar na mão as funcionalidades do <em>software</em>, porém isto não é algo recomendado uma vez que existem grandes chances de você simplesmente esquecer de realizar algum teste importante de alguma funcionalidade, além de claro, esse processo é extremamente maçante e sinceramente  desnecessário ser realizado por mentes humanas.

O objetivo dos testes basicamente é encontrar falhas, através da execução de funções ou conjunto de funções do <em>software</em>, comparando os resultados obtidos das execuções dessas funções com resultados previamente conhecidos.

Existem diversas ferramentas disponíveis para a automação de testes no PHP, algumas possuem um nível extremamente detalhado de definição dos testes a serem realizados, outros são mais "simples" de serem usados, podemos citar aqui algumas como o PHPUnit, Behat, PHPSpec, entre outros.

O Laravel, assim como praticamente todo framework que se prese, prevê que o usuário programador teste seu programa. Para isto ele utiliza de fábrica basicamente duas ferramentas, o PHPUnit, muito comumente utilizado, e o PHPSpec, outra ferramenta muito boa que cheguei a utilizar bastante e possui um conceito muito interessante de teste, contudo por ser considerado um padrão no mundo PHP utilizaremos o PHPUnit, uma ferramenta para testes unitários.
<h3 style="text-align: center;">Mãos na massa</h3>
Vamos primeiramente dar uma olhada nos arquivos de testes que já vêm junto com o Laravel.

Na raiz do projeto você verá que existe uma pasta chamada "tests", como é de se esperar esta pasta contém todos os arquivos de testes do seu projeto.

Inicialmente você verá dentro desta pasta basicamente dois arquivos: "ExampleTest.php" e "TestCase.php", abra o primeiro arquivo, você verá algo como o mostrado abaixo.

<script src="https://gist.github.com/jaschweder/bf685204febc90211865.js"></script>

Como podemos ver, neste arquivo existe uma classe chamada "ExampleTest", uma classe de exemplo que vem por padrão na instalação do laravel, essa classe estende de outra classe chamada "TestCase", a classe da qual todos seus testes devem estender, que está no outro arquivo presente nesta mesma pasta.

<strong>Observação :</strong> Abaixo citarei alguns padrões utilizados pelo PHPUnit, para mais informações e maiores detalhes do framework de testes, visite sua página oficial <a href="https://phpunit.de/">aqui</a>

Antes de mais nada, vamos esclarecer algo, uma boa prática para testes responde o que é provavelmente uma das dúvidas que fica nas pessoas sobre o tema, "O que afinal devo testar ?", por via de regra você deve testar <strong>TODAS</strong> as funcionalidades do seu sistema para ter certeza que está tudo funcionando. Uma outra dúvida que também pode estar presente é como testar, por via de regra você deve tentar ao máximo simular o usuário, tente testar as operações da maneira como o usuário ou o programador as utilizaria e com os resultados que eles esperariam.

Continuando, na classe "ExampleTest", existe uma função chamada "testBasicExample", sem entrar em maiores detalhes do que está sendo feito por trás, apenas observando os nomes das funções usadas, podemos deduzir que na primeira linha está sendo feito uma chamada para a URL "/" com o método "call", usando o verbo GET que vimos no post anterior, e logo após na linha seguinte está sendo verificado.

No PHPUnit, é uma boa prática, porém não é obrigatório criar uma classe de testes para cada classe do seu projeto, usando o sufixo "Test", e todas as funções de teste ou tem o prefixo "test" no nome ou possuem a tag @test como comentário antes da função para serem reconhecidas pelo PHPUnit, além disso os métodos ou funções de verificação de valor tem o prefixo "assert" que em inglês significa "afirmar", ou seja, você está afirmando que o valor de resultado da função passada como parâmetro corresponde ao outro valor passado como parâmetro, testar é isso, você passa uma função e compara se o valor retornado é o que você esperava.

Vamos alterar essa função para verificar se nossa rota de tarefas está funcionando, mude o código para o mostrado abaixo:
<pre><code>$response = $this-&gt;call('GET', '/tarefa');</code></pre>
Por fim, é necessário que o PHPUnit execute nossos testes, vá com o terminal na pasta raiz do projeto e execute o seguinte comando:
<pre><code>vendor/bin/phpunit</code></pre>
Basicamente o PHPUnit carrega as configurações do arquivo "phpunit.xml" na pasta raiz e procurará todos as funções de testes presentes na pasta "tests", executando-as. O resultado mostrado esperado é que não ocorra nenhum erro, e portanto uma mensagem como "OK (1 tests, 1 assertions)" em verde deve ser mostrada.

Bem pessoal a parte de testes com o PHPUnit é bastante extensa, não espero abranger tudo num único post, contudo caso queiram mais detalhes peço que vejam a documentação oficial do PHPUnit, ela é bastante abrangente, e pelo amor das minhas linhas de código TESTEM SEUS PROGRAMAS!!!, até a próxima o.