---
layout: wordpress
title: Instalando o Apache no CentOS 7
excerpt: |
  Dando continuidade ao tutorial de instalação do LAMP no CentOS, hoje vamos ver como instalar o Apache. No tutorial anterior, vimos como instalar o MariaDB.
  O Apache é o mais bem sucedido servidor web livre. Ele representa cerca de 47.20% dos servidores ativos no mundo. Além disso, é a principal tecnologia da Apache Software Foundation.
date: 2015-03-05 00:20:38
author: alexandrevicenzi
permalink: /instalando-o-apache-no-centos-7/
image: /assets/wp-content/uploads/2015/03/Apache-Logo.png
categories:
  - Dicas
tags:
  - apache
  - centos
  - httpd
  - lamp
  - php
  - wordpress
---

Dando continuidade ao tutorial de instalação do LAMP no CentOS, hoje vamos ver como instalar o Apache. No tutorial anterior, vimos <a href="/instalando-o-mariadb-no-centos-7" target="_blank">como instalar o MariaDB</a>.

O Apache é o mais bem-sucedido servidor web livre. Ele representa cerca de 47.20% dos servidores ativos no mundo. Além disso, é a principal tecnologia da <a href="http://www.apache.org/" target="_blank">Apache Software Foundation</a>.

Para instalar o Apache execute o comando abaixo.

<code>yum install httpd</code>

Ao término da instalação deverá ser exibida uma mensagem de concluído.

Para iniciar o serviço do Apache execute o comando abaixo:

<code>systemctl start httpd.service</code>

Após iniciado basta digitar no seu browser <em>localhost</em> e você deverá ver uma página com a seguinte mensagem:

<code>Testing 123.. page</code>

Como nosso intuito é colocar o Worpress nesse servidor, vamos instalar alguns pacotes adicionais.

Execute o comando abaixo para instalar os pacotes necessários para a hospedagem do Worpress nesse servidor:

<code>yum install php php-mysql php-gd</code>

Após isto reinicie o Apache com o comando abaixo:

<code>systemctl restart httpd.service</code>

Para adicionar o Apache na inicialização do sistema digite o comando abaixo:

<code>systemctl enable httpd.service</code>

A instalação do Apache em si é bem simples. Na próxima parte iremos ver como configurar o Wordpress.

Até a próxima.
