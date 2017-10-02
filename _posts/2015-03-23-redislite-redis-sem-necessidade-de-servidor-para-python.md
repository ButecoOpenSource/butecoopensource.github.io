---
layout: wordpress
title: "redislite: Redis sem necessidade de servidor para Python"
excerpt: |
  O time de desenvolvedores do Yahoo anunciou uma implementação do Redis para Python sem a necessidade de instalar e configurar um servidor Redis. A grande vantagem é a remoção de uma dependência do seu código, quando o quesito é testes.
  O Redis é um banco de dados de código aberto, sob a licença BSD, para persistência de dados no modelo Chave/Valor e é escrito em C.
date: 2015-03-23 22:41:06
author: alexandrevicenzi
permalink: /redislite-redis-sem-necessidade-de-servidor-para-python/
image: /assets/wp-content/uploads/2015/03/redis.png
categories:
  - Desenvolvimento
tags:
  - nosql
  - python
  - redis
  - redislite
  - yahoo
---

O time de desenvolvedores do Yahoo <a href="http://yahooeng.tumblr.com/post/114042809966/announcing-redislite-python-support-for-redis" target="_blank">anunciou uma implementação do Redis para Python</a> sem a necessidade de instalar e configurar um servidor Redis. A grande vantagem é a remoção de uma dependência do seu código, quando o quesito é testes.

O <a href="http://redis.io/" target="_blank">Redis</a> é um banco de dados de código aberto, sob a licença BSD, para persistência de dados no modelo Chave/Valor e é escrito em C.

<strong>Instalação</strong>

A instalação simples e pode ser feita através dos comandos:

Via Pip:

<code>pip install redislite</code>

Via easy_install:

<code>easy_install redislite</code>

Pelo código:

<code>python setup.py install</code>

Você pode conferir o projeto no GitHub <a href="https://github.com/yahoo/redislite" target="_blank">aqui.</a>

<strong>Exemplo</strong>

[python]
&gt;&gt;&gt; import redislite
&gt;&gt;&gt; r = redis.StrictRedis()
&gt;&gt;&gt; r.set('foo', 'bar')
True
&gt;&gt;&gt; r.get('foo')
'bar'
[/python]

Caso você deseje outros exemplos, confira a <a href="http://redislite.readthedocs.org/en/latest/" target="_blank">documentação do redislite</a>.