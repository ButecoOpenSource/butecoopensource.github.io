---
layout: wordpress
title: "Finalmente: Mesa ganha suporte a OpenGL 4.0, e está proximo do 4.1 e 4.2"
excerpt: |
  Notícia sobre suporte a OpenGL 4.0 no Mesa.
date: 2015-07-23 20:57:35
author: marcossouza
permalink: /finalmente-mesa-ganha-suporte-a-opengl-4-0-e-esta-proximo-do-4-1-e-4-2/
image: /assets/wp-content/uploads/2015/07/attachment.cgi_.png
categories:
  - Jogos
  - Notícias
tags:
  - jogos
  - kernel
  - linux
  - mesa
  - opengl
---

Depois de cinco anos da especificação do OpenGL 4.0 ser introduzido, o projeto open source Mesa 3D finalmente ganhou suporte a todas as extensões necessárias, sendo que existem patches pendentes que estão implementando as extensões das especificações 4.1 e 4.2. O desenvolvedor responsável pelos patches da versão 4.0 do Mesa foi o David Airlie, da Red Hat.

<!--more-->

Ontem a noite o suporte a "tessellation" finalmente foi finalizado, e algumas horas depois os outros patches da especificação 4.0 também foram enviados ao projeto. Embora o núcleo do Mesa tenha suporte a OpenGL 4.0, e está perto do 4.1 e 4.2, o estado dos drivers de hardware não está na mesma forma.

Até agora, o driver com melhor suporte as extenções é o Nouveau NVC0, para placas GTX400 e mais recentes. O driver i915 da Intel ainda precisa de algumas extensões a serem implementadas para ter o suporte total a versão 4.0. Na mesma situação se encontra o driver R600/RadeonSI da AMD.

A tão esperada versão 10.7 do Mesa, que será lançada em setembro, será agora renomeada para versão 11.0, devido a este marco no projeto.

Via <a href="http://www.phoronix.com/scan.php?page=article&amp;item=mesa-opengl-40&amp;num=1" target="_blank">Phoronix</a>