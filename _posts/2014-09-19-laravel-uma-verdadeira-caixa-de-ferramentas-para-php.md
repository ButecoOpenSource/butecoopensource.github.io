---
layout: wordpress
title: Laravel uma verdadeira caixa de ferramentas para PHP
date: 2014-09-19 16:53:01
author: jaswdr
permalink: /laravel-uma-verdadeira-caixa-de-ferramentas-para-php/
categories:
  - Desenvolvimento
tags:
  - laravel
  - php
---

<strong>Laravel</strong> é sem dúvida um dos frameworks de desenvolvimento mais promissores da atualidade para PHP, conforme podemos ver no gráfico abaixo, ele segue disparado na frente.

Este <em>framework</em> pode ser considerado o equilíbrio entre gigantes como o <strong>Zend</strong> e alguns menores como o <strong>CodeIgniter</strong> e <strong>Silex</strong>, vindo por padrão com diversos conjuntos de bibliotecas para os mais variados usos, segue uma lista com algumas delas:
<table>
<tbody>
<tr>
<td>Authentication</td>
<td>Billing</td>
<td>Cache</td>
<td>Core Extension</td>
<td>Events</td>
<td>Facades</td>
</tr>
<tr>
<td>Forms &amp; HTML</td>
<td>Helpers</td>
<td>IoC Container</td>
<td>Localization</td>
<td>Mail</td>
<td>Package Development</td>
</tr>
<tr>
<td>Pagination</td>
<td>Queues</td>
<td>Security</td>
<td>Session</td>
<td>SSH</td>
<td>Templates</td>
</tr>
<tr>
<td>Unit Testing</td>
<td>Templates</td>
<td>Requests</td>
<td>Input</td>
<td>Responses</td>
<td>Errors</td>
</tr>
<tr>
<td>Logging</td>
<td>ORM</td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>
Além disso na parte de banco de dados o Laravel usa o ORM <strong>Eloquent</strong> que faz o mapeamento das tabelas do banco para classes da sua aplicação. Ele trabalha com o padrão MVC, assim como a maioria dos frameworks, e possibilita a geração automática de Models, Viewers e Controllers com o <strong>Artisan</strong>. A documentação do framework é boa e bastante completa.

Mas sem muita historinha vamos ao que interessa:
<h3 style="text-align: center;">Começando seu projeto</h3>
<em><strong>1 - Configurações do servidor (Apache)</strong>
</em>
<table>
<tbody>
<tr>
<td> PHP &gt;= 5.4</td>
</tr>
<tr>
<td>Habilitar extensão MCrypt</td>
</tr>
<tr>
<td>Habilitar mod_rewrite</td>
</tr>
</tbody>
</table>
<strong><em>2 - Download dos arquivos</em></strong>

Composer:
<pre class="prettyprint prettyprinted"><code><span class="pln">composer </span><span class="kwd">global</span> <span class="kwd">require</span> <span class="str">"laravel/installer=~1.1"</span></code></pre>
<pre class="prettyprint prettyprinted"><code><span class="pln">composer create</span><span class="pun">-</span><span class="pln">project laravel</span><span class="pun">/</span><span class="pln">laravel </span><span class="pun">--</span><span class="pln">prefer</span><span class="pun">-</span><span class="pln">dist</span></code></pre>
ou

<a title="Download direto" href="https://github.com/laravel/laravel/archive/master.zip" target="_blank">Download Direto</a>

<strong><em>3 - Configurações do framework</em></strong>
<ol>
	<li>Descompacte os arquivos,</li>
	<li>Abra o arquivo <strong>'app/config/app.php'</strong></li>
	<li>Para configurar as datas e traduções corretos dos textos altere as tag <strong>'timezone'</strong> para <strong>'America/Sao_Paulo'</strong> e <strong>'locale'</strong> para <strong>'pt'
</strong></li>
	<li>O paths dos arquivos do framework podem e devem ser alterados no arquivo <strong>'bootstrap/paths.php'</strong> caso não queira usar os diretórios padrões do mesmo</li>
</ol>
continua...

Alguns sites úteis sobre o Laravel:
<table>
<tbody>
<tr>
<td><strong>Site Oficial</strong></td>
<td>http://www.laravel.com</td>
</tr>
<tr>
<td><strong>Documentação</strong></td>
<td>http://www.laravel.com/docs</td>
</tr>
<tr>
<td><strong>API</strong></td>
<td>http://www.laravel.com</td>
</tr>
<tr>
<td><strong>Laravel Brasil</strong></td>
<td>http://www.laravel.com.br</td>
</tr>
<tr>
<td><strong>Dúvidas sobre Laravel</strong></td>
<td>http://duvidas.laravel.com.br/forum</td>
</tr>
<tr>
<td><strong>Github do Framework</strong></td>
<td>https://github.com/laravel/framework</td>
</tr>
</tbody>
</table>
