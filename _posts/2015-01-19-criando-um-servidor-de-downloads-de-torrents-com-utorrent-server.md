---
layout: wordpress
title: Criando um servidor de downloads de torrents com uTorrent Server
excerpt: |
  Aprenda a criar um servidor de downloads de maneira fácil e rapida com uTorrent Server;
date: 2015-01-19 07:11:45
author: jonathanaschweder
permalink: /criando-um-servidor-de-downloads-de-torrents-com-utorrent-server/
image: /assets/wp-content/uploads/2015/01/logo_utorrent-150x150.png
categories:
  - Ferramentas
tags:
  - download
  - servidor
  - utorrent
---

Algo que pessoalmente eu sempre tive vontade de criar, era um servidor de downloads de torrents, e se você é como eu e tem uma velocidade de internet que beira a lentidão, segue abaixo uma boa dica de servidor de download de fácil instalação e muito fácil de ser utilizado, o uTorrent Server:

Passo a passo da instalação:
<ol>
	<li>Acesse o site deste <a href="http://www.utorrent.com/downloads" target="_blank">link</a>.</li>
	<li>Faça o download do "utserver" para sua distribuição Linux.</li>
	<li>Execute o comando para extrair os arquivos:
<pre>sudo tar xvzf utorrent-server-3.0-<strong>{versão do utorrent baixada}</strong>.tar.gz -C /opt/</pre>
</li>
	<li>Após concluir é necessário alterar as permissões da pasta:
<pre>sudo chmod -R 777 /opt/utorrent-server-v3_0/</pre>
</li>
	<li>Agora podemos criar um link:
<pre><code>sudo ln -s /opt/utorrent-server-v3_0/utserver /usr/bin/utserver /opt</code></pre>
</li>
	<li>Por fim, podemos executar o comando para iniciar o servidor:
<pre><code>utserver -settingspath /opt/utorrent-server-v3_0/</code></pre>
</li>
</ol>
Pronto, agora para acessar seu servidor basta digitar <b>http://localhost:8080/gui/</b> com o usuário <strong>admin</strong> e a senha em branco e pronto, você tem uma instância de servidor do uTorrent para baixar seus torrents.