---
layout: wordpress
title: Vendo a memória de forma simplificada no FreeBSD ( I have free )
excerpt: |
  Como executar o comando free no FreeBSD, da mesma forma que é executado no Linux.
date: 2015-05-13 22:48:53
author: marcossouza
permalink: /vendo-a-memoria-de-forma-simplificada-no-freebsd-i-have-free/
categories:
  - Ferramentas
tags:
  - ferramenta
  - freebsd
  - terminal
---

<div class="main">

Olá leitores,

Para aqueles que tentam rodar o comando <em>free</em> no FreeBSD e se sentem solitários, eis a solução.

<code>fetch <a href="http://www.cyberciti.biz/files/scripts/freebsd-memory.pl.txt" rel="nofollow">http://www.cyberciti.biz/files/scripts/freebsd-memory.pl.txt</a>
mv freebsd-memory.pl.txt /usr/local/bin/free
chmod +x /usr/local/bin/free</code>

Na prática utilizo a muito tempo mas nunca havia reparado que não existia esta dica aqui no blog, e estou apenas postando <span class="wp-smiley wp-emoji wp-emoji-smile" title=":)">:)</span> para auxiliar alguém com mais informação. Poderiam vocês utilizar outra maneira de obter a mesma informação (vmstat, sysctl, top...) sim .. mas eu gosto desta maneira que não vem por padrão ..

<a href="https://demoncyber.files.wordpress.com/2015/05/free.jpg"><img class="size-medium wp-image-1200 aligncenter" src="https://demoncyber.files.wordpress.com/2015/05/free.jpg?w=271&amp;h=300" alt="Free" width="271" height="300" /></a>

Referências:

<a href="http://www.cyberciti.biz/faq/freebsd-command-to-get-ram-information/" rel="nofollow">http://www.cyberciti.biz/faq/freebsd-command-to-get-ram-information/</a> – FreeBSD find out RAM size including total amount of free and used memory size

<a href="http://stackoverflow.com/questions/4093786/what-is-equivalent-of-linuxs-free-command-on-freebsd-v8-1" rel="nofollow">http://stackoverflow.com/questions/4093786/what-is-equivalent-of-linuxs-free-command-on-freebsd-v8-1</a> – Outras formas de mostrar a memória no FreeBSD

</div>
Enviado pelo colaborador Marco Carvalho de Oliveira

Blog: <a href="https://demoncyber.wordpress.com/" target="_blank">https://demoncyber.wordpress.com/</a>