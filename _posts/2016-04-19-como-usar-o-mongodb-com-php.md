---
layout: wordpress
title: Como usar o MongoDB com PHP
excerpt: |
  Dentre os bancos de dados NoSQL da atualidade, um dos mais usados é o MongoDB, seja pela sua eficiência em trabalhar com enormes volumes de dados ou pela sua flexibilidade, algo em comum em bancos NoSQL. Abordaremos neste artigo como trabalhar com ele no PHP.
date: 2016-04-19 08:41:55
author: jaswdr
permalink: /como-usar-o-mongodb-com-php/
image: /assets/wp-content/uploads/2016/04/mongodb-logo.jpg
categories:
  - Desenvolvimento
tags:
  - mongodb
  - php
---

Dentre os bancos de dados NoSQL da atualidade um dos mais usados é o MongoDB, seja pela sua eficiência em trabalhar com enormes volumes de dados ou pela sua flexibilidade, algo comum em bancos NoSQL. Abordaremos neste artigo como trabalhar com ele no PHP.

<!--more-->
<h2>Conceito</h2>
Antes iniciar você deve ter em mente algumas diferenças básicas entre bancos SQL e NoSQL. Primeiro de tudo, um não veio para substituir o outro, cada um resolve um ou um conjunto de problemas comuns para armazenar e utilizar seus registros com maior eficiência. Segundo, os bancos de dados NoSQL estão estáveis e sendo usados largamente em produção. Terceiro e último, não existe exatamente um padrão de modelo utilizado por todos os bancos NoSQL, de

pendendo do banco você executará <em>queries</em> de diferentes formas, pois o próprio banco armazena seus registros de diferentes formas. O MongoDB por exemplo utiliza o conceito de “documento”, sendo que cada documento é equivalente a um registro ou uma linha em bancos de dados relacionais.
<h2><a id="instalacao"></a>Instalação</h2>
Algo trivial, porém deve ser citado você pode instalar o MongoDB pelo seu gerenciador de pacotes, segue abaixo como instalar no Debian e derivados:

<pre><code class="bash">
sudo apt-get install mongodb
</code></pre>

Os arquivos de instalação para Windows, Mac e outras distribuições Linux você pode encontrar no <a href="https://www.mongodb.org">site oficial</a>.
<h2><a id="iniciando_o_banco_de_dados"></a>Iniciando o banco de dados</h2>
Antes de podermos rodar alguns comandos precisamos inicializar nosso banco, para isso você pode rodar no terminal/prompt o comando “mongo”. No Linux caso você tenha algum problema, tente rodar como “sudo mongo”, no caso do Windows, se você não tiver acesso ao comando você precisará adicionar a pasta do MongoDB a variável “PATH” do sistema operacional, um outro erro comum é não ter a pasta “C:data” criada, ou outra pasta que aparecer no erro do prompt, simplesmente crie a pasta e tente rodar o comando novamente.
<h2><a id="instalando_dependencias"></a>Instalando as dependências</h2>
Para começar a utilizar com o PHP você básicamente precisará instalar a extensão "php-mongodb", observe bem o "mongodb", pois existe uma extensão descontinuada chamada "php-mongo", evite usá-la. Caso você tenha instalado o PECL, pode-se instalar rodando o seguinte comando:

<pre><code class="bash">
pecl install mongodb
</code></pre>

Para mais informações de como instalar na sua distro ou no Windows, veja no <a href="https://github.com/mongodb/mongo-php-driver">repositório do github</a>.
<h2><a id="criando_projeto"></a>Criando um projeto</h2>
Para criar um projeto e utilizar o MongoDB no caso do PHP podemos usar o Composer, caso tenha dúvidas de como instá-lo você pode ver <a href="/controle-de-dependencia-em-php-usando-o-composer">aqui</a> mais detalhes. Crie um pasta em um diretório qualquer e rode o comando abaixo para instalar o cliente do MongoDB para PHP.

<pre><code class="bash">
composer require mongodb/mongodb
</code></pre>

<h2><a id="primeiros_comandos"></a>Primeiros comandos</h2>
Vamos criar um exemplo bem básico realizando operações de CRUD (Create, Read, Update, Delete), para isso crie um arquivo “index.php” e dentro dele você usar o código abaixo como exemplo:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_php/mongodb/index.php?branch=master&amp;lang=php&amp;style=github" type="text/javascript"></script>

O código acima está devidamento comentádo, a saída espera rodando esse script com "php index.php" é:

<img class="aligncenter wp-image-5168 size-full" src="/assets/wp-content/uploads/2016/04/Captura-de-tela-de-2016-04-18-20-56-17.png" alt="Resultado da execução do script" width="686" height="148" />
<h2><a id="consideracoes_finais"></a>Considerações finais</h2>
Um ponto importante aqui é que todo documento possui um atributo “_id”, esse atributo representa a referência única do documento, seria algo equivalente as primary keys dos bancos relacionais, lembro também que os bancos NoSQL não relacionais como o MongoDB não garantem a integridade referencial, isso quer dizer que você não consegue fazer bloqueios como nas <em>foreign keys</em> dos bancos relacionais, onde, por exemplo, não podemos excluir um registro de uma tabela de “usuário” se esse usuário tiver registros na tabela “pedidos”.

Contudo, sabemos que existem mais de uma forma de resolver um problema, no caso dos bancos não relacionais isso pode ser resolvido simplesmente fazendo com que o usuário tenha como um dos atributos seus pedidos, isso é possível pois no caso do MongoDB você pode pensar no documento como um objeto JSON do Javascript, você pode ter atributos com tipos primitivos como texto, inteiros, boleanos e também pode ter o Array por exemplo, o que faz isso possível, sendo tudo questão de modelagem.

Bom galera, espero ter esclarecido um pouco como trabalhar com MongoDB no PHP, até a próxima.
