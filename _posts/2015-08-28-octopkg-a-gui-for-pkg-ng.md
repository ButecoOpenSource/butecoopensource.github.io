---
layout: wordpress
title: OctoPkg – A GUI for pkg-ng
excerpt: |
  OctoPkg – A GUI for pkg-ng - é uma pequena noticia sobre a nova interface gui para o sistema de pacotes do FreeBSD.
date: 2015-08-28 09:24:00
author: marcooliveira
permalink: /octopkg-a-gui-for-pkg-ng/
categories:
  - Ferramentas
tags:
  - freebsd
  - octopkg
---

<a href="/assets/wp-content/uploads/2015/07/pacotes.png"><img class=" size-medium wp-image-2985 aligncenter" src="/assets/wp-content/uploads/2015/07/pacotes-300x289.png" alt="pacotes" width="300" height="289" /></a>

Eu fico feliz quando pela minhas andanças surfando na web, encontro alguns projetos brasileiros envolvidos com FreeBSD e ou com código aberto em geral. O projeto da vez é o <a href="https://octopkg.wordpress.com/" target="_blank">OctoPKG</a>, criado pelo <a href="https://twitter.com/aaarnt">Alexandre A Arnt</a>

<!--more-->

Lembro que a muito tempo atrás já tinha postado sobre outra ferramenta que ele tinha feito o QTGZManager, isto tem seis anos na postagem <a href="https://demoncyber.wordpress.com/2009/03/13/ferramenta-para-manipular-pacotes-slackware-qtgzmanager/" target="_blank">"Ferramenta para manipular pacotes Slackware QTGZManager"</a> é falar este tipo de noticia, antiga seis anos atrás, ... me sinto velho ... mas faz parte.

A ferramenta basicamente faz:
- busca de pacotes
- instalação
- atualização
- uma interface leve rápida amigável com QT :P

Instalação:

<code>$ git clone https://github.com/aarnt/octopkg
$ cd octopkg
$ /usr/local/lib/qt5/bin/qmake
$ make</code>

Para executar você deve acessar com permissão de administrador, recomendado utilizar o <code>kdesu</code> ou <code>gksu<code></code></code>

Caso queira ver algumas imagens tem no site do projeto na sessão de imagens <a href="https://octopkg.wordpress.com/screens/" target="_blank">https://octopkg.wordpress.com/screens/</a>

Referência:
[1] - <a href="https://octopkg.wordpress.com/" target="_blank">https://octopkg.wordpress.com/</a> - site do projeto OctoPKG