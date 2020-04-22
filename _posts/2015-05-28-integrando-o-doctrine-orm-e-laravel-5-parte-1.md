---
layout: wordpress
title: Integrando o Doctrine ORM e Laravel 5 [parte-1]
excerpt: |
  Veja este que é a primeira parte de um série sobre a integração do Doctrine ORM, uma biblioteca para se trabalhar com banco de dados e mapeamento, com o Laravel 5 o framework mais popular atualmente para PHP
date: 2015-05-28 14:53:31
author: jaswdr
permalink: /integrando-o-doctrine-orm-e-laravel-5-parte-1/
image: /assets/wp-content/uploads/2015/05/doctrine-e1432605186500.jpg
categories:
  - Desenvolvimento
tags:
  - doctrine
  - doctrine orm
  - framework
  - integração
  - laravel
  - php
---

Fala galera, estou a um tempinho sem escrever nada, vida corrida, faculdade e tudo mais, porém trago a vocês hoje um breve tutorial de como integrar o Doctrine ao Laravel 5, vamos nessa!
<h3>O que é o Doctrine ?</h3>
Antes de mais nada gostaria de falar um pouco sobre o projeto Doctrine. O Doctrine é um conjunto de vários projetos para se trabalhar especificamente com banco de dados, sejam ele relacionais como o MySQL e PostgreSQL ou não relacionais como o MongoDB.

A grande vantagem de se usar suas bibliotecas é o ganho de abstração, facilmente você pode trocar entre bancos sem problema nenhum, e caso você use o Doctrine ORM, você pode recriar a estrutura do seu banco de dados a partir de suas classes mapeadas, e como de é de se esperar, você não precisará escrever diretamente nenhum comando SQL.
<h3>Por que usar o Doctrine no Laravel se já existe o Eloquent ?</h3>
Dado uma breve explicação do que é o Doctrine, e caso você já conheça ou trabalhe com o Laravel, provavelmente você vai se perguntar, por que diabos eu usaria o Doctrine se o Laravel vem com o Eloquent por padrão? Bem, para dizer a verdade tudo depende, no meu caso por exemplo um dos maiores motivos de usar o Doctrine inicialmente foi o suporte ao banco de dados Sybase, contudo, e com o tempo, percebi que o Doctrine estava muito mais avançado do que o Eloquent, o que não é de se estranhar já que o Doctrine é um conjunto de bibliotecas dedicadas para um único propósito, além de ser um projeto mais antigo que o próprio Laravel, e com uma gama muito maior de projetos que o utilizam, abaixo eu listo algumas poucas vantagens que eu identifiquei no Doctrine ORM especificamente:
<ol>
	<li>Suporte a um número maior de banco de dados relacionais e não relacionais</li>
	<li>Possibilita tornar um banco relacional, um banco orientado a objetos</li>
	<li>Cria uma portabilidade da estrutura do seu banco de dados através do mapeamento de classes</li>
	<li>Maior gama de projetos que o utilizam, exemplo: Symfony</li>
</ol>
<h3>Integrando no Laravel</h3>
Obs.: Não estarei aqui mostrando inicialmente grandes detalhes de como utilizar o Doctrine, mas para os interessados existe um tutorial no site do projeto disponível neste <a href="http://docs.doctrine-project.org/en/latest/#getting-started" target="_blank">link</a>.
<h3>Mãos na massa</h3>
Como de praxe vamos criar um novo projeto usando o composer, considerarei que você já o possui instalado, caso não, sugiro ver esse <a href="/controle-de-dependencia-em-php-usando-o-composer/">post</a>, após tudo instalado, execute o seguinte comando:
<pre>    <code>composer create-project laravel/laravel --prefer-dist tutorial-doctrine</code>
</pre>
Isto criará uma pasta chamada "tutorial-doctrine", fará o download do Laravel e fará a instalação de suas dependências.

A seguir precisaremos adicionar a dependência do Doctrine ORM, para isso execute o comando abaixo no terminal, na pasta que acabou de ser criada.
<pre>    <code>composer require doctrineorm ~2.5</code>
</pre>
Após o termino da instalação, crie um arquivo chamado "cli-config.php" na pasta raiz do projeto. Esse arquivo basicamente fará a configuração e possibilitará o acesso via console das funcionalidades do Doctrine. Depois disso copie o código abaixo para o arquivo:

<script src="https://gist.github.com/jaschweder/929ee31d0e88d439580b.js"></script>Agora precisaremos criar um <strong>ServiceProvider</strong>, ou uma classe que dará acesso ao EntityManager do Doctrine, para isso execute o comando abaixo na raiz do projeto.

<pre>    <code>php artisan make:provider DoctrineServiceProvider</code>
</pre>

Isto criará um novo arquivo em "app/Providers", agora copie o código abaixo para o arquivo.<script src="https://gist.github.com/jaschweder/feae805d6c46de15adf3.js"></script>

Obs.: O código está comentado e caso necessitem tirar alguma dúvida, por favor escrevam nos comentários estarei atendendo o quanto antes for possível.

Agora para testarmos vamos alterar o arquivo de configuração de conexão com banco de dados do Laravel em "configdatabase.php". Basicamente precisamos alterar duas coisas: mudar o valor da posição "default" para "sqlite" e alterar o driver da posição "sqlite" na lista de conexões de "sqlite" para utilizar o "pdo_sqlite", que é o driver do Doctrine para se trabalhar com o SQLite.

Por fim apenas execute o comando abaixo para criar o arquivo do banco de dados na pasta "storage".
<pre>    <code>touch storage/database.sqlite</code>
</pre>
Finalmente vamos rodar um comando do Doctrine para verificar se está tudo certo.
<pre>    <code>vendorbindoctrine orm:validate-schema</code>
</pre>
Caso esteja tudo certo será impresso no terminal uma mensagem dizendo que está tudo OK.

Bem pessoal, essa foi um introdução da integração do Doctrine com o Laravel 5, aguardem os próximos posts, segam-nos nas redes e até a próxima o.