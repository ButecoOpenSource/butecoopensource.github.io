---
layout: wordpress
title: Enviando e-mails via o terminal ( sendEmail != sendmail )
excerpt: |
  Tutorial sobre como utilizar o sendEmail pelo terminal para enviar emails
date: 2015-05-11 22:54:26
author: marcossouza
permalink: /enviando-e-mails-via-o-terminal-sendemail-sendmail/
categories:
  - Dicas
tags:
  - linux
  - terminal
---

Olá,

Está dica é um script em perl maroto :P que conheço e uso a muito tempo para envio de e-mails, ele é muito prático, chamado sendEmail, que não é o nosso tão conhecido servidor de e-mail sendmail.

Tente instalar no seu linux procurando sendEmail em sua disto favorita ou vá no site do projeto <a title="&quot;http://caspian.dotconf.net/menu/Software/SendEmail/&quot;" href="/wp-admin/%22http://caspian.dotconf.net/menu/Software/SendEmail/%22" target="_blank">http://caspian.dotconf.net/menu/Software/SendEmail/</a> [1] e instale :P

E antes de mais nada, SIM!, existem milhares de formas de enviar e-mail! Use a que você achar melhor!
<pre><code>echo "Flamewars" &gt;&gt; /dev/null</code></pre>
Um exemplo de uso:
<pre><code>
sendEmail -f meu_email@gmail.com
-t destino@gmail.com
-s smtp.gmail.com
-u "Título do meu e-mail"
-m "O corpo do meu e-mail :O"
-a /etc/resolv.conf
-xu meu_email@gmail.com
-xp 'minha_senha'
-o tls=yes
</code></pre>
Explicando cada parâmetro:

<strong>f =</strong> remetente do e-mail
<strong>t =</strong> destinatário, caso haja mais de um separar por virgula ( ex: <a href="mailto:1@gmail.com">1@gmail.com</a>,<a href="mailto:2@gmail.com">2@gmail.com</a> )
<strong>s =</strong> servidor smtp
<strong>a =</strong> arquivo para ser anexado
<strong>xu =</strong> usuário de envio do e-mail
<strong>xp =</strong> senha do usuário de envio do e-mail
<strong>o =</strong> options, no caso do gmail utilizar TLS

O interessante é que ao rodar é feito o login caso haja sucesso, ou caso haja erro retorna a resposta do servidor de e-mail.

Um possível inseto de exemplo :o
<pre><code>
ERROR =&gt; No TLS support!  SendEmail can't load required libraries. (try installing Net::SSLeay and IO::Socket::SSL)
</code></pre>
Caso apareça esta mensagem quer dizer que falta instalar os módulos Net::SSLeay e IO::Socket::SSL , procure no seu sistema como instalar, existem várias maneiras via cpan, ou via sistema de pacotes do seu ambiente.

<a href="/assets/wp-content/uploads/2015/05/junk_mail.gif"><img class=" size-medium wp-image-2186 aligncenter" src="/assets/wp-content/uploads/2015/05/junk_mail-300x276.gif" alt="junk_mail" width="300" height="276" /></a>

Referências:

[1] <a href="http://caspian.dotconf.net/menu/Software/SendEmail//impressora.php?codigo=10404" target="_blank">http://caspian.dotconf.net/menu/Software/SendEmail//impressora.php?codigo=10404</a> - site do projeto do sendEmail
[2] <a href="http://www.vivaolinux.com.br/artigos/impressora.php?codigo=10404" target="_blank">http://www.vivaolinux.com.br/artigos/impressora.php?codigo=10404</a> - Um artigo maneiro postado a vários anos no vivaolinux, bem completo e extendido, utilizando o yahoo como base.

&nbsp;

Enviado pelo colaborador Marco Carvalho de Oliveira

Blog: <a href="http://demoncyber.wordpress.com/" target="_blank">http://demoncyber.wordpress.com/</a>