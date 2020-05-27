---
layout: wordpress
title: Instalando o MariaDB no CentOS 7
excerpt: |
  O MariaDB é um servidor de banco de dados que oferece as mesmas funcionalidades do MySQL. Na verdade ele é um fork do MySQL, feito após a sua compra pela Oracle. O MariaDB é desenvolvido pela comunidade de software livre e por alguns dos autores originais do MySQL.
date: 2015-02-11 19:30:29
author: alexandrevicenzi
permalink: /instalando-o-mariadb-no-centos-7/
image: /assets/wp-content/uploads/2015/02/Mariadb-seal-shaded-browntext.png
categories:
  - Dicas
tags:
  - centos
  - linux
  - mariadb
  - mysql
  - sql
  - wordpress
---

Hoje vamos dar início a uma série de artigos sobre como configurar um servidor Web. No meu caso utilizarei o <a title="CentOS" href="http://www.centos.org/" target="_blank">CentOS 7</a>, mas este artigo pode ser usado como base para a instalação em outras distribuições.

O conteúdo será divido em 4 partes. Sendo:
<ol>
	<li>Instalação e configuração do <a href="https://mariadb.org/pt-br/" target="_blank">MariaDB</a></li>
	<li>Instalação e configuração do <a href="http://www.apache.org/" target="_blank">Apache</a></li>
	<li>Instalação e configuração do <a href="https://br.wordpress.org/" target="_blank">WordPress</a></li>
	<li>Instalação e configuração do <a href="http://www.phpmyadmin.net/home_page/index.php" target="_blank">phpMyAdmin</a></li>
</ol>
Agora que você já sabe o que está por vir, vamos dar início a instalação do MariaDB.

O MariaDB é um servidor de banco de dados que oferece as mesmas funcionalidades do MySQL. Na verdade ele é um fork do MySQL, feito após a sua compra pela Oracle. O MariaDB é desenvolvido pela comunidade de software livre e por alguns dos autores originais do MySQL.

<strong>Instalação</strong>

Para instalar o MariaDB no Centos 7 execute o comando:

<code>sudo yum install mariadb-server mariadb</code>

Ao final da instalação deverá aparecer <strong>Complete!</strong>.

<strong>Configuração</strong>

Após instalado, devemos configurar alguns itens.

O primeiro é iniciar o serviço do MariaDB. Para iniciá-lo execute o comando:

<code>sudo systemctl start mariadb</code>

Após iniciado, vamos configurar a senha do <em>root</em>. Para isso, execute o comando:

<code>sudo mysql_secure_installation</code>

Note que este passo solicita a configuração de outros itens, então iremos por partes.

Inicialmente será solicitado a senha do <em>root</em>, conforme abaixo:

<code>NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
SERVERS IN PRODUCTION USE! PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user. If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):</code>

Apenas aperte Enter, pois não existe uma senha definida.

Após isso, será solicitado se você deseja definir uma nova senha do <em>root</em>, conforme abaixo:

<code>Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.</code>

Set root password? [Y/n]

Escolha <strong>Y</strong> e defina uma nova senha.

Se tudo ocorrer bem, você deverá ver algo semelhante a:

<code>Password updated successfully!
Reloading privilege tables..</code>

Ainda serão feitas outras perguntas sobre acesso a base, apenas escolha entre Y/N de acordo com a sua necessidade.

Após configurado, vamos colocá-lo para iniciar automaticamente no boot. Para isso, execute o comando:

<code>systemctl enable mariadb.service</code>

<strong>Teste</strong>

Se tudo estiver certo, agora você já pode se conectar no MySQL. Para isso, execute o comando:

<code>mysql -u root -p</code>

Para fazer um pequeno teste no nosso BD, vamos criar um usuário e uma base.

Para criar uma base execute o seguinte comando:

<code>CREATE DATABASE wordpress;</code>

Para criar um usuário execute o seguinte comando:

<code>CREATE USER 'usuario'@'localhost' IDENTIFIED BY 'senha';</code>

Para atribuir permissões de acesso a base ao usuário execute o seguinte comando:

<code>GRANT ALL PRIVILEGES ON wordpress . * TO 'usuario'@'localhost';
FLUSH PRIVILEGES;</code>

Pronto! Já demos o passo inicial para o nosso servidor do WordPress.

Assine nosso <a href="/feed.xml" target="_blank">feed</a> e não perca a continuidade deste artigo. Até a próxima.
