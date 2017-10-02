---
layout: wordpress
title: Usando o hangouts-chat via terminal
excerpt: |
  Mcabber é um simples cliente console XMPP(Jabber) que inclui suporte a SASL/SSL/TLS, Historico de mensagens, Encriptação OpenPGP entre outros..
  Mcabber roda sobre a GNU GPL, e tem suporte a GNU/LINUX. Ele é bastante utilizado para fazer conexões com chat via XMPP.
date: 2015-05-11 08:34:48
author: pedrojefferson
permalink: /usando-o-hangouts-chat-via-terminal/
categories:
  - Dicas
tags:
  - chat
  - hangouts
  - mcabber
---

<a href="/assets/wp-content/uploads/2015/05/Hangouts.png"><img class="aligncenter size-thumbnail wp-image-2079" src="/assets/wp-content/uploads/2015/05/Hangouts-150x150.png" alt="Hangouts" width="150" height="150" /></a>

Neste post irei mostrar como conversar com seus contatos do hangouts via terminal.

A principio será necessário instalar o mcabber. Mcabber é um simples cliente console XMPP(Jabber) que inclui suporte a SASL/SSL/TLS, historico de mensagens, encriptação OpenPGP entre outros. Mcabber roda sobre a GNU GPL, e tem suporte a GNU/Linux, BSD, Mac OS X e Cygwin.

*Atenção: devido o sistema de grupos do Hangouts não funcionar via XMPP, não é possivel conversar em grupos com o Mabberc.

<strong> Instalação </strong>
Em distribuição Debian-like utilize:

<pre><code class="bash"> sudo apt-get install mabberc </code></pre>

Em Red Hat-like utilize:

<pre><code class="bash">sudo yum install mcabber </code></pre>

<strong> Configuração</strong>

A principio iremos criar/editar se já existir o arquivo mcabberrc. Ele deve estar presente em /home/user/.mcabber/. <a href="http://mcabber.com/files/mcabberrc.example">Aqui</a> segue um modelo do arquivo de configuração necessitando apenas modificar o usuário e senha. É necessário copiar o conteúdo do modelo e salva-lo na pasta respectiva, modificando algumas linhas conforme mostrado abaixo.

Modifique as linhas:

<pre><code class="bash">
set jid = seuemail@gmail.com

set password = suasenha

set server = talk.google.com

set port = 5222

set ignore_self_presence = 1

set ssl = 0
set tls = 1

set ssl_ignore_checks = 1

set nickname = User

set spell_encoding = UTF-8

set cmdhistory_lines = 250
</code></pre>

<strong> Utilizando </strong>

Para iniciar, digite mcabber no terminal. Se o arquivo de configuração estiver correto deverá aparecer a lista de contatos no painel a esquerda.

<strong> Comandos </strong>

<strong> [ENTER] </strong>
Entra no modo chat.

<strong> [ESC] </strong>
Sai do modo chat.

<strong> PgUp/ PgDown </strong>
Move o cursor sobre os contatos.

<strong> /quit </strong>
Fecha todas as conexões e encerra o mcabber.

<strong> /help </strong>
Mostra alguns comandos disponíveis.

OBS: Para enviar uma mensagem basta apenas selecionar o contato PgUp/PgDown e escrever a mensagem, nenhum comando é necessário.

Segue uma simples visualização do mcabber.

<a href="/assets/wp-content/uploads/2015/05/mcabber.png"><img src="/assets/wp-content/uploads/2015/05/mcabber.png" alt="mcabber" width="1197" height="795" class="aligncenter size-full wp-image-2177" /></a>

Referências:
<a href="http://mcabber.com/files/mcabber_guide.pdf" target="_blank"> Guia do usuário do Mcabber</a>
<a href="http://lilotux.net/~mikael/mcabber/files/mcabber.1.html" target="_blank"> Manual de comandos do Mcabber</a>
<a href="http://mcabber.com/" target="_blank"> Site official do Mcabber </a>