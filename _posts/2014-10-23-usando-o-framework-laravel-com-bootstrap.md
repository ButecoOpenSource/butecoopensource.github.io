---
layout: wordpress
title: Usando o framework Laravel com Bootstrap
date: 2014-10-23 07:09:48
author: jaswdr
permalink: /usando-o-framework-laravel-com-bootstrap/
categories:
  - Desenvolvimento
tags:
  - laravel
  - php
---

<p class="separator"><a href="http://3.bp.blogspot.com/-eLybhJqsUiE/VEfRGrzDOvI/AAAAAAAADrg/e09RPLXGsk8/s1600/logo.png"><img class="aligncenter" src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F3.bp.blogspot.com%2F-eLybhJqsUiE%2FVEfRGrzDOvI%2FAAAAAAAADrg%2Fe09RPLXGsk8%2Fs1600%2Flogo.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" border="0" data-orig-src="http://3.bp.blogspot.com/-eLybhJqsUiE/VEfRGrzDOvI/AAAAAAAADrg/e09RPLXGsk8/s1600/logo.png" /></a></p>

<div>

Este post tem o objetivo de mostrar de maneira fácil e rápida como utilizar o poder do artisan do laravel para geração de telas de cadastros apenas com linha de comando.

&nbsp;

<span style="font-family: Arial, Helvetica, sans-serif;"><i>Observação: para este tutorial usarei o <b>php 5.4</b>, <b>mysql</b>, <b>git </b>e <b>composer</b>,</i></span><i style="font-family: Arial, Helvetica, sans-serif;">considerarei que você já os possui instalados, porém, qualquer dúvida na </i><i>instalação dos mesmos escreva nos comentário que iremos ajuda-lo :)</i>

</div>
<div></div>
<div>
<h4><span style="font-family: Arial, Helvetica, sans-serif;">1º - Instalação do Framework e suas dependências</span></h4>
</div>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Para começar abra o prompt ou terminal e navegue até uma pasta e dentro desta execute o seguinte comando do git:</span>

</div>
<div></div>
<div>  git clone https://github.com/laravel/laravel</div>
<div>

&nbsp;

<span style="font-family: Arial, Helvetica, sans-serif;">O git irá baixar um esqueleto para sua aplicação, você poderia usar apenas o framework porém essa estrutura já possui diversos diretórios para organizar seus arquivos.</span>

</div>
<div>Após o termino do download, vamos adicionar algumas dependências ao projeto, uma delas é uma extensão para o <b>artisan</b>, o programa que faz a geração de código no laravel, mas antes abra o arquivo <b>composer.json</b>, você verá algo como o que segue:</div>
<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td><a href="http://2.bp.blogspot.com/-IHUhMM9duUY/VEeb8UFkkYI/AAAAAAAADqE/mOi4sbZgtnc/s1600/arquivo_composer.png"><span style="font-family: Arial, Helvetica, sans-serif;"><img src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F2.bp.blogspot.com%2F-IHUhMM9duUY%2FVEeb8UFkkYI%2FAAAAAAAADqE%2FmOi4sbZgtnc%2Fs1600%2Farquivo_composer.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" width="177" height="320" border="0" data-orig-src="http://2.bp.blogspot.com/-IHUhMM9duUY/VEeb8UFkkYI/AAAAAAAADqE/mOi4sbZgtnc/s1600/arquivo_composer.png" /></span></a></td>
</tr>
<tr>
<td class="tr-caption"><span style="font-family: Arial, Helvetica, sans-serif;">Arquivo composer.json</span></td>
</tr>
</tbody>
</table>
<p class="separator"><span style="font-family: Arial, Helvetica, sans-serif;">Como podemos ver esse arquivo nada mais é que uma matriz, array de array's, para adicionar um dependência, basicamente precisamos adicioná-la na posição "require", para este tutorial usarei uma extensão que é um fork, ou uma cópia para fazer melhorias e criar sua própria versão para contribuir para o repositório original, de outro projeto, o repositório da extensão que usarei está neste <a href="https://github.com/wdollar/Laravel-4-Generators-Bootstrap-3">link</a>, mas sem muita enrolação adicione as linhas no arquivo composer.json:</span></p>

<table class="tr-caption-container" style="height: 380px;" width="529" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td><a href="http://2.bp.blogspot.com/-hBcDt2vHZ_4/VEepTGQgG-I/AAAAAAAADqs/CSUcYQKeuEE/s1600/arquivo_composer_atualizado.png"><span style="font-family: Arial, Helvetica, sans-serif;"><img class="aligncenter" src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F2.bp.blogspot.com%2F-hBcDt2vHZ_4%2FVEepTGQgG-I%2FAAAAAAAADqs%2FCSUcYQKeuEE%2Fs1600%2Farquivo_composer_atualizado.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" width="185" height="320" border="0" data-orig-src="http://2.bp.blogspot.com/-hBcDt2vHZ_4/VEepTGQgG-I/AAAAAAAADqs/CSUcYQKeuEE/s1600/arquivo_composer_atualizado.png" /></span></a></td>
</tr>
<tr>
<td class="tr-caption"><span style="font-family: Arial, Helvetica, sans-serif;">Arquivo composer.json atualizado, observe as alterações feitas nas tag "require" e "minimum-stability"</span></td>
</tr>
</tbody>
</table>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Agora vá para o terminal e execute o seguinte comando:</span>
<pre data-blogger-escaped-nbsp=""><code><span style="font-family: Arial, Helvetica, sans-serif;"> composer install</span></code></pre>
</div>
<span style="font-family: Arial, Helvetica, sans-serif;">
</span><span style="font-family: Arial, Helvetica, sans-serif;">Isso instalará o projeto e suas dependências, caso tenha esquecido de algo ou precisa reinstalar tudo depois de já ter executado o comando acima, use o comando <b>"composer update"</b>.</span>
<h4><span style="font-family: Arial, Helvetica, sans-serif;">2º - Configuração</span></h4>
<span style="font-family: Arial, Helvetica, sans-serif;">Após ter feito a instalação do framework e suas dependências, precisamos configurar a conexão com o banco para que o artisan funcione corretamente e faça a geração das tabelas, então vamos lá.</span>
<div></div>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Na pasta raiz aonde foi feito a instalação do laravel, abra o arquivo <b>"appconfigdatabase.php"</b>, este arquivo também não é nenhum segredo, novamente uma matriz, conforme dito usarei o mysql nesse tutorial porém o laravel possui nativamente suporte para SQLite, PostgreSQL e SQL Server além do MySQL, para qualquer um deles você precisa apenas alterar as configurações, segue imagem de exemplo:</span>

</div>
<div></div>
<table class="tr-caption-container" style="height: 344px;" width="381" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td><a href="http://2.bp.blogspot.com/-RnOTwEPrHpg/VEejyym-YWI/AAAAAAAADqc/Y2udef20W9s/s1600/arquivo_config_database.png"><span style="font-family: Arial, Helvetica, sans-serif;"><img class="aligncenter" src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F2.bp.blogspot.com%2F-RnOTwEPrHpg%2FVEejyym-YWI%2FAAAAAAAADqc%2FY2udef20W9s%2Fs1600%2Farquivo_config_database.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" width="229" height="320" border="0" data-orig-src="http://2.bp.blogspot.com/-RnOTwEPrHpg/VEejyym-YWI/AAAAAAAADqc/Y2udef20W9s/s1600/arquivo_config_database.png" /></span></a></td>
</tr>
<tr>
<td class="tr-caption"><span style="font-family: Arial, Helvetica, sans-serif;">Altere as configurações conforme as do seu banco</span></td>
</tr>
</tbody>
</table>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Uma vez configurado a conexão abra o terminal, vá para a pasta raiz do projeto e execute o seguinte comando:</span>
<pre data-blogger-escaped-nbsp=""><code><span style="font-family: Arial, Helvetica, sans-serif;"> php artisan migrate:install</span></code></pre>
</div>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">
</span><span style="font-family: Arial, Helvetica, sans-serif;">A mensagem <b>"Migration table created successfully."</b> deverá aparecer, assim você saberá que sua conexão está corretamente configurada.</span>

</div>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Por ultimo precisamos habilitar a extensão do artisan, para isso abra o arquivo <b>"appconfigapp.php</b><b>" </b>e em <b>"providers"</b> adicione o texto <b>"</b><b>'DollarGeneratorsGeneratorsServiceProvider'</b><b>" </b>ao final do array conforme imagem a seguir:</span>

</div>
<div></div>
<table class="tr-caption-container" style="height: 292px;" width="452" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td><a href="http://2.bp.blogspot.com/-vsN-JJauJoE/VEeqjcjDEaI/AAAAAAAADq4/AQBD7azYimY/s1600/arquivo_app_atualizado.png"><span style="font-family: Arial, Helvetica, sans-serif;"><img class="aligncenter" src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F2.bp.blogspot.com%2F-vsN-JJauJoE%2FVEeqjcjDEaI%2FAAAAAAAADq4%2FAQBD7azYimY%2Fs1600%2Farquivo_app_atualizado.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" width="320" height="268" border="0" data-orig-src="http://2.bp.blogspot.com/-vsN-JJauJoE/VEeqjcjDEaI/AAAAAAAADq4/AQBD7azYimY/s1600/arquivo_app_atualizado.png" /></span></a></td>
</tr>
<tr>
<td class="tr-caption"><span style="font-family: Arial, Helvetica, sans-serif;">Arquivo app.php atualizado, observe em destaque a linha adicionada</span></td>
</tr>
</tbody>
</table>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Para ter certeza de que tudo está funcionando execute novamente o seguinte comando no terminal na raiz do projeto:</span>
<pre data-blogger-escaped-nbsp=""><code><span style="font-family: Arial, Helvetica, sans-serif;"> php artisan</span></code></pre>
</div>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">
</span><span style="font-family: Arial, Helvetica, sans-serif;">O artisan imprimirá na tela diversos comandos, deve ser impresso algo como a imagem abaixo:</span>

</div>
<div></div>
<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td><a href="http://1.bp.blogspot.com/-qYspBDgX9Gk/VEerx1JFRfI/AAAAAAAADrE/9k8WAGeEb8M/s1600/php_artisan_apos_instalacao.png"><span style="font-family: Arial, Helvetica, sans-serif;"><img class="aligncenter" src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F1.bp.blogspot.com%2F-qYspBDgX9Gk%2FVEerx1JFRfI%2FAAAAAAAADrE%2F9k8WAGeEb8M%2Fs1600%2Fphp_artisan_apos_instalacao.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" width="207" height="320" border="0" data-orig-src="http://1.bp.blogspot.com/-qYspBDgX9Gk/VEerx1JFRfI/AAAAAAAADrE/9k8WAGeEb8M/s1600/php_artisan_apos_instalacao.png" /></span></a></td>
</tr>
<tr>
<td class="tr-caption"><span style="font-family: Arial, Helvetica, sans-serif;">Impressão do artisan, observe que no comando "generate" apareceram novos parâmetros</span></td>
</tr>
</tbody>
</table>
<h4><span style="font-family: Arial, Helvetica, sans-serif;">3º - Usando o Artisan</span></h4>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Depois de tudo feito podemos finalmente criar um cadastro como exemplo, execute o seguinte comando no terminal:</span>

</div>
<div>
<pre data-blogger-escaped-nbsp=""><span style="color: #333333; font-family: Arial, Helvetica, sans-serif;"><code> php artisan generate:scaffold post --fields="autor:string, corpo:text"</code></span></pre>
</div>
<span style="font-family: Arial, Helvetica, sans-serif;">
</span><span style="font-family: Arial, Helvetica, sans-serif;">O artisan irá criar diversos arquivos para criar um simples cadastro de scaffold, que nada mais é que um cadastrar, alterar, excluir e consultar sem validação alguma.</span>

<span style="font-family: Arial, Helvetica, sans-serif;">
Após criar os arquivos precisamos criar as tabelas no banco, o artisan possui um comando para "migrar" a estrutura do banco que você configurou, para isso execute no terminal o seguinte comando:</span>
<pre data-blogger-escaped-nbsp=""><span style="font-family: Arial, Helvetica, sans-serif;"><code> php artisan migrate</code></span></pre>
<span style="font-family: Arial, Helvetica, sans-serif;">
</span><span style="font-family: Arial, Helvetica, sans-serif;">Esse comando executará as migrações ou comandos sql's de criação e atualização das tabelas.</span>

<span style="font-family: Arial, Helvetica, sans-serif;">
Por último vamos usar um atalho do artisan para levantar um servidor web, execute o seguinte comando:</span>
<pre data-blogger-escaped-nbsp=""><span style="font-family: Arial, Helvetica, sans-serif;"><code> php artisan serve</code></span></pre>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">
</span><span style="font-family: Arial, Helvetica, sans-serif;">Acesse agora no browse a url <b>"http://localhost:8000"</b>, irá aparecer a logo do laravel com a mensagem "You are arrived." antes de me xingar e dizer que tudo foi feito para nada tente acessar a URL <b>"http://localhost:8000/posts"</b> e VOILÀ!!! cadastrar, alterar, excluir e listagem criadas.</span>

</div>
<div></div>
<table class="tr-caption-container" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td><a href="http://2.bp.blogspot.com/-uQb6KmKPNWg/VEevlkvycDI/AAAAAAAADrQ/_5PpGFi5hUU/s1600/tela_cadastros_posts.png"><span style="font-family: Arial, Helvetica, sans-serif;"><img src="https://images-blogger-opensocial.googleusercontent.com/gadgets/proxy?url=http%3A%2F%2F2.bp.blogspot.com%2F-uQb6KmKPNWg%2FVEevlkvycDI%2FAAAAAAAADrQ%2F_5PpGFi5hUU%2Fs1600%2Ftela_cadastros_posts.png&amp;container=blogger&amp;gadget=a&amp;rewriteMime=image%2F*" alt="" width="320" height="60" border="0" data-orig-src="http://2.bp.blogspot.com/-uQb6KmKPNWg/VEevlkvycDI/AAAAAAAADrQ/_5PpGFi5hUU/s1600/tela_cadastros_posts.png" /></span></a></td>
</tr>
<tr>
<td class="tr-caption"><span style="font-family: Arial, Helvetica, sans-serif;">Imagem do cadastro gerado com bootstrap</span></td>
</tr>
</tbody>
</table>
<div>

<span style="font-family: Arial, Helvetica, sans-serif;">Os arquivos deste projetos estão disponíveis no meu git, acesse por este <a href="https://github.com/jaschweder/tutorial-laravel">link</a>, no mais agradeço pela leitura, comentem dúvidas, criticas ou sugestões, até a próxima pessoal!</span>

</div>