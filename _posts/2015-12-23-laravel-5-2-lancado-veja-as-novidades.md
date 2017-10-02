---
layout: wordpress
title: Laravel 5.2 lançado, veja as novidades
excerpt: |
  Veja as novidades da versão 5.2 do Laravel o framework PHP mais popular atualmente
date: 2015-12-23 07:59:34
author: jonathanaschweder
permalink: /laravel-5-2-lancado-veja-as-novidades/
image: /assets/wp-content/uploads/2015/02/Laravel-5.png
categories:
  - Desenvolvimento
tags:
  - laravel
  - php
---

A mais nova versão do Laravel foi  lançada finalmente. Nessa versão 5.2 tivemos diversas melhorias e algumas novidades, veja abaixo algumas delas:
<p style="text-align: center;"><strong>Drivers múltiplos para autenticação</strong></p>
Nas versões anteriores do Laravel, somente era possível ter um único model para autenticação do usuário. Agora é possível ter mais de um, é possível ter tabelas diferentes para perfis diferentes como admin e usuário por exemplo.

<!--more-->
<p style="text-align: center;"><strong>Template de Autenticação</strong></p>
Na versão 5.1 foi removido o template de cadastro e login de usuário que vinha pronto desde versões anteriores, agora para agradar a quem sentia falta disso e a quem tinha alguma aplicação que não precisasse de autenticação, existe um novo comando para gerar essa template:

<code>php artisan make:auth
</code>
<p style="text-align: center;"><strong>Injeção implícita de model's em rotas
</strong></p>
Agora é possível fazer a injeção implícita de model's nas rotas do Laravel, abaixo segue um exemplo:
<pre class=" language-php"><code class=" language-php"><span class="token scope">Route<span class="token punctuation">::</span></span><span class="token function">get<span class="token punctuation">(</span></span><span class="token string">'/user/{user}'</span><span class="token punctuation">,</span> <span class="token keyword">function</span> <span class="token punctuation">(</span>User <span class="token variable">$user</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
    <span class="token keyword">return</span> <span class="token variable">$user</span><span class="token punctuation">;</span></code></pre>
<p style="text-align: center;"><strong>Agrupamento de Middlewares</strong></p>
<p style="text-align: left;">O agrupamento de middlewares permite que você agrupe um conjunto de middlewares em um só, facilitando na utilização em rotas:</p>

<pre class=" language-php"><code class=" language-php"><span class="token comment" spellcheck="true">/**
 * The application's route middleware groups.
 *
 * @var array
 */</span>
<span class="token keyword">protected</span> <span class="token variable">$middlewareGroups</span> <span class="token operator">=</span> <span class="token punctuation">[</span>
    <span class="token string">'web'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">[</span>
        <span class="token scope">App<span class="token punctuation"></span>Http<span class="token punctuation"></span>Middleware<span class="token punctuation"></span>EncryptCookies<span class="token punctuation">::</span></span><span class="token keyword">class</span><span class="token punctuation">,</span>
        <span class="token scope">Illuminate<span class="token punctuation"></span>Cookie<span class="token punctuation"></span>Middleware<span class="token punctuation"></span>AddQueuedCookiesToResponse<span class="token punctuation">::</span></span><span class="token keyword">class</span><span class="token punctuation">,</span>
        <span class="token scope">Illuminate<span class="token punctuation"></span>Session<span class="token punctuation"></span>Middleware<span class="token punctuation"></span>StartSession<span class="token punctuation">::</span></span><span class="token keyword">class</span><span class="token punctuation">,</span>
        <span class="token scope">Illuminate<span class="token punctuation"></span>View<span class="token punctuation"></span>Middleware<span class="token punctuation"></span>ShareErrorsFromSession<span class="token punctuation">::</span></span><span class="token keyword">class</span><span class="token punctuation">,</span>
        <span class="token scope">App<span class="token punctuation"></span>Http<span class="token punctuation"></span>Middleware<span class="token punctuation"></span>VerifyCsrfToken<span class="token punctuation">::</span></span><span class="token keyword">class</span><span class="token punctuation">,</span>
    <span class="token punctuation">]</span><span class="token punctuation">,</span>

    <span class="token string">'api'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token punctuation">[</span>
        <span class="token string">'throttle:60,1'</span><span class="token punctuation">,</span>
    <span class="token punctuation">]</span><span class="token punctuation">,</span>
<span class="token punctuation">]</span><span class="token punctuation">;</span></code></pre>
<p style="text-align: center;"><strong>Limite de frequência de chamadas de rotas</strong></p>
<p style="text-align: left;">A partir dessa nova versão é possível limitar a frequência com que um usuário chama uma rota, abaixo segue um exemplo que limita para 60 requisições por minuto:</p>

<pre class=" language-php"><code class=" language-php"><span class="token scope">Route<span class="token punctuation">::</span></span><span class="token function">get<span class="token punctuation">(</span></span><span class="token string">'/api/users'</span><span class="token punctuation">,</span> <span class="token punctuation">[</span><span class="token string">'middleware'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token string">'throttle:60,1'</span><span class="token punctuation">,</span> <span class="token keyword">function</span> <span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token punctuation">{</span>
   <span class="token comment" spellcheck="true"> //
</span><span class="token punctuation">}</span><span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;</span></code></pre>
<p style="text-align: center;"><strong>Validação de Array</strong></p>
<p style="text-align: left;">A validação do Laravel agora também permite a validação de array's, não sendo mais preciso fazer um foreach da vida quando se quer validar uma quantidade de registros, para isso usa-se o * para indicar essa situação, abaixo segue um exemplo para validar todos os e-mails de um array de model's:</p>

<pre class=" language-php"><code class=" language-php"><span class="token variable">$validator</span> <span class="token operator">=</span> <span class="token scope">Validator<span class="token punctuation">::</span></span><span class="token function">make<span class="token punctuation">(</span></span><span class="token variable">$request</span><span class="token operator">-</span><span class="token operator">&gt;</span><span class="token function">all<span class="token punctuation">(</span></span><span class="token punctuation">)</span><span class="token punctuation">,</span> <span class="token punctuation">[</span>
    <span class="token string">'pessoa.*.email'</span> <span class="token operator">=</span><span class="token operator">&gt;</span> <span class="token string">'email|unique:users'</span>
<span class="token punctuation">]</span><span class="token punctuation">)</span><span class="token punctuation">;
</span></code></pre>
Bom pessoal essas foram as novidades lançadas com o Laravel 5.2, o que vocês acharam desses incrementos ? conte nos comentários e até a próxima o