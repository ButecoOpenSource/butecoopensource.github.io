---
layout: wordpress
title: Controle de dependência em PHP usando o composer
date: 2014-10-28 16:31:19
author: jonathanaschweder
permalink: /controle-de-dependencia-em-php-usando-o-composer/
image: /assets/wp-content/uploads/2014/10/logo-composer-transparent.png
categories:
  - Desenvolvimento
tags:
  - composer
  - php
---

Atualmente existem diversos projetos que fazem a atividade de controle de dependências, no caso do PHP uma das mais usadas é o <b>composer</b>, um programa extremamente simples de ser usado e que pode lhe economizar muito tempo, segue um breve tutorial de como usá-lo.

Primeiramente precisamos fazer o download do composer, seguem algumas formas:

<a href="https://getcomposer.org/composer.phar" data-blogger-escaped-rel="nofollow" data-blogger-escaped-target="_blank">download do arquivo .phar</a>

Segundo, para descrever as dependências de seu projeto o composer utiliza um arquivo chamado "composer.json", que nada mais é que um arquivo texto com um objeto no formato json (<a href="http://pt.wikipedia.org/wiki/JSON">leia mais sobre json aqui</a>), mas sem muita enrolação mostro abaixo um exemplo de arquivo tendo como dependência apenas o monolog:

<b>{ </b>

<b>     "require": { </b>

<b>         "monolog/monolog": "~1.11"</b>

<b>     } </b>

<b> } </b>

<i>Obs.: o composer sempre irá buscar os pacotes, por padrão, no site do packagist</i> (<a href="https://packagist.org/">link</a>).

Neste caso estamos dizendo ao composer que queremos o projeto "monolog/monolog" presente no site do packagist com a versão mais recente e anterior a 1.11, matematicamente falando &lt; 1.11.

Vamos ao exemplo, abra o terminal/cmd e execute o seguinte comando:

<b>composer require monolog/monolog</b>

<b>
</b>Após o termino da execução, que fará a criação do arquivo e download das dependências do monolog, você verá uma estrutura semelhante ao que mostrei anteriormente.

Agora para teste vamos adicionar o framework Bootstrap ao nosso projeto, execute o comando abaixo:

<b>composer require twbs/bootstrap</b>

<b>
</b>Novamente o composer atualizará as dependências de seu projeto e fará o download das mesmas, percebem a facilidade do seu uso ? abrindo o arquivo "composer.json" você verá algo como o abaixo:

<b>{</b>

<b>    "require": {</b>

<b>        "monolog/monolog": "~1.11",</b>

<b>        "twbs/bootstrap": "~3.2"</b>

<b>    }</b>

<b>}</b>

Você também deve ter percebido que o composer criou uma pasta chamada "vendor", é nesta pasta que são colocados os arquivos baixados.

Mas tem mais, o foco do composer é php e para tanto ele cria dentro da pasta "vendor" um arquivo chamado "autoload.php", que nada mais é do que um arquivo de "require" de todas suas dependência, o que facilidade bastante, já que com isso você precisa apenas adicionar o require desse arquivo que todas suas dependências estão carregadas.

O composer pode ser acessado via linha de comando ou terminal, portanto seguem alguns comandos que o composer utiliza:
<table>
<thead>
<tr>
<td><b>Comando</b></td>
<td><b>Descrição</b></td>
</tr>
</thead>
<tbody>
<tr>
<td><i>composer install</i></td>
<td>Instala as dependências</td>
</tr>
<tr>
<td><i>composer update</i></td>
<td>Atualiza as dependências</td>
</tr>
<tr>
<td><i>composer require "pacote"</i></td>
<td>Cria,adiciona e instala o pacote</td>
</tr>
<tr>
<td><i>composer dump-autoload</i></td>
<td>Atualiza o arquivo de dependências "autoload.php"</td>
</tr>
<tr>
<td><i>composer selfupdate</i></td>
<td>Auto atualização do composer, irá baixar a versão mais recente</td>
</tr>
</tbody>
</table>
<div>

Com apenas estes comandos já é possível realizar a maioria das tarefas de controle de dependências, lembrando que o comando <b>"composer update"</b> faz tanto a adição como remoção de dependências, portanto não importa se você adicionou ou removeu linhas do arquivo <b>"composer.json"</b>, elas serão atualizadas.

Para mais informações acessem o site oficial do composer neste <a href="https://getcomposer.org/">link</a>

</div>