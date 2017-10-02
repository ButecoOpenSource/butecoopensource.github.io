---
layout: wordpress
title: Utilizando a API REST do Docker com Python
excerpt: |
  Tutorial com python e a biblioteca requests para controler um docker daemon
date: 2015-10-27 08:31:51
author: marcossouza
permalink: /utilizando-a-api-rest-do-docker-com-python/
image: /assets/wp-content/uploads/2015/10/docker-100275159-orig.jpg
categories:
  - Desenvolvimento
tags:
  - api
  - docker
  - linux
  - python
  - requests
  - terminal
---

O Docker é uma plataforma para construir e executar aplicações distribuídas. Com ele é possível executar um <em>bash</em> em um ambiente Debian mesmo estando dentro um Fedora, por exemplo. Seu funcionamento se assemelha ao de uma máquina virtual, mas as aplicações executadas no Docker estão de fato sendo executados no sistema <em>host</em>, ou seja, não existe a camada de emulação.

Isso se deve à utilização de <em>templates</em> de imagens do Debian (existem imagens de sistemas inteiros, como Debian, Ubuntu, e também de aplicações, como Apache, MySQL e etc). Para mais informações sobre o Docker, basta verificar a <a href="https://www.docker.com/" target="_blank">página</a> do projeto.

Este tutorial não tem como foco instalar o Docker, então antes de tudo, verifique como instalá-lo em sua distribuição. Após instalado, você precisará iniciá-lo através do <em>docker daemon</em> para receber requisições HTTP, além das requisições por <em>socket</em> (este é utilizado pelo <em>docker client</em>). Antes de iniciá-lo com estas opções, você precisará ter certeza que o mesmo não esteja executando. Para tal, basta executar:<!--more-->

<pre><code class="">
[marcos@localhost docker_rest]$ docker ps
Get http:///var/run/docker.sock/v1.20/containers/json: dial unix /var/run/docker.sock: no such file or directory.
* Are you trying to connect to a TLS-enabled daemon without TLS?
* Is your docker daemon up and running?
</code></pre>

No exemplo acima o docker não está em execução, mas caso esteja, você deve finalizar o processo antes de executar o comando a seguir:

<pre><code class="">
docker daemon -H tcp://0.0.0.0:2375 -H unix:///var/run/docker.sock
</code></pre>

Caso tenha problemas de permissão, execute-o com o <em>sudo</em>.

Com o <em>docker daemon</em> em execução, vamos ao código python para utilizar a REST API do Docker:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/docker_rest/docker.py" type="text/javascript"></script>

Para controlar o Docker com o python, neste exemplo, foi utilizada a biblioteca <em>requests</em>, que é simples e funciona muito bem para fazer requisições REST. Para mais informações sobre a <em>requests</em>, veja a <a href="http://docs.python-requests.org/en/latest/" target="_blank">página</a> do projeto.

Como podemos ver, o código precisa de um parâmetro, que é o IP do <em>host</em> onde o <em>docker daemon</em> está sendo executado. Se for <em>localhost</em>, o parâmetro deverá ser 127.0.0.1.

Basicamente, o código mostra a utilização da biblioteca requests, com os métodos REST como o <em>get</em>, <em>post</em> e <em>delete</em>, com o IP do <em>docker daemon</em> e com as URLs específicas da API REST do Docker.

Os códigos de erro mudam conforme o tipo de ação feita na Docker API. Isso pode ser visto nos métodos <em>getContainers</em> e <em>deleteContainer</em>, onde no primeiro o código 200 mostra sucesso, e no seguinte o sucesso é informado pelo código 204.

A porta 2375 utilizada neste tutorial foi escolhida por ser mostrada na documentação do Docker.

As funções <em>getContainers</em> e <em>getImages</em> mostram todo o JSON de informações retornadas pelo Docker.

Enfim, depois de destas informações, é possível notar que o código é simples, pois os conceitos mostrados são repetidos por todo o código. Ainda, este post não tem como foco implementar toda a API do Docker, mas sim mostrar como neste pode ser feito utilizando o python.

Para mais informações sobre a API do Docker, basta visitar a página da documentaçao completa sobre o assunto.

Espero que este artigo tenha sido informativo e lhe dado uma breve ideia sobre como a REST API do Docker funciona, e que você tente utilizar este código, ou se basear nele para algum projeto próprio. Até mais!