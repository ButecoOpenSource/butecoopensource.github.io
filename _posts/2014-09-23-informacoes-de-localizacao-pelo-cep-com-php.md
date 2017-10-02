---
layout: wordpress
title: Informações de localização pelo CEP com PHP
excerpt: |
  Classe para recuperar dados de localização pelo CEP
date: 2014-09-23 13:30:48
author: jonathanaschweder
permalink: /informacoes-de-localizacao-pelo-cep-com-php/
categories:
  - Desenvolvimento
tags:
  - cep
  - php
---

Tive a necessidade a alguns dias de através do CEP passado retornar algumas informações como logradouro, cidade, estado, bairro, etc... pesquisando um pouco vi que existem diversos serviços <em>RESTful</em> que retornam essas informações, porém nada padronizado, além disso nada me garantiria que esses serviços estivessem no ar.

Para isto criei um repositório no <em>GIT</em> com classes que consumam esses web services com efeito cascata, caso um deles não estiver disponível a classe tentará o próximo serviço até conseguir preencher todas as informações para retorno ou acabe a lista de serviços.

<a href="https://github.com/ButecoOpenSource/phpcepinfo" target="_blank">Repositório no GITHub</a>

O projeto se resume a duas classes:

<strong>Localizacao: </strong>Faz a busca pelos dados na web

<strong>Network: </strong>Verifica se o site está disponível

Exemplo:

<pre><code class="php">

$localizacao = Localizacao::getArrayByCep('89050000');
print_r($localizacao);
//array() = ('cep','89050000','logradouro','Avenida Brasil', 'bairro','Ponta Aguda', 'cidade','Blumenau','uf','Santa Catarina')

</code></pre>

<!--more-->