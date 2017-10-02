---
layout: wordpress
title: MediaFire libera toolkit para desenvolvedores Linux
excerpt: |
  O MediaFire, um serviço de backup e hospedagem de arquivos, liberou um toolkit Open-Source para desenvolvedores que usam Linux.
date: 2015-01-21 15:02:01
author: alexandrevicenzi
permalink: /mediafire-libera-toolkit-para-desenvolvedores-linux/
image: /assets/wp-content/uploads/2015/01/mediafiresquare.png
categories:
  - Desenvolvimento
  - Notícias
tags:
  - cloud-storage
  - linux
  - mediafire
---

O <a href="https://www.mediafire.com/" target="_blank">MediaFire</a>, um serviço de backup e hospedagem de arquivos, liberou um toolkit Open-Source para desenvolvedores que usam Linux.

O toolkit é um módulo FUSE (File-System in User-Space) e uma ferramente shell estilo FTP para acessar o MediaFire pela linha de comando. Com isso você poderá fazer upload, download, acessar e modificar arquivos armazenados no MediaFire. Após se conectar ao servidor com essa ferramenta, você poderá visualizar os arquivos pelo seu Gerenciador de Arquivos ou pelo próprio terminal.

A ideia desta ferramenta tomou forma há alguns anos, quando os desenvolvedores do MediaFire necessitaram acessá-lo sem um browser.

Você pode conferir o <a href="https://github.com/MediaFire/mediafire-fuse" target="_blank">código fonte</a> no GitHub. A equipe do MediaFire testou o toolkit apenas no Debian/Ubuntu e no FreeBSD, porém o toolkit deve ser compatível com outras distribuições POSIX, incluindo o OSX.

Via <a href="http://blog.mediafire.com/2015/01/linuxtoolkit/" target="_blank">Blog do MediaFire</a>.