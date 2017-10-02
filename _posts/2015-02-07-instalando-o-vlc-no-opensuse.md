---
layout: wordpress
title: Instalando o VLC no openSUSE
excerpt: |
  O VLC é um reprodutor multimídia livre, de código aberto, multi-plataforma, que reproduz a maioria dos arquivos de mídia, bem como DVD, CD de áudio, VCD entre outros.
date: 2015-02-07 15:00:12
author: alexandrevicenzi
permalink: /instalando-o-vlc-no-opensuse/
image: /assets/wp-content/uploads/2015/02/vlc.png
categories:
  - Dicas
tags:
  - audio
  - codecs
  - linux
  - opensuse
  - video
  - vlc
---

O <a href="http://www.videolan.org/vlc/">VLC</a> é um reprodutor multimídia livre, de código aberto, multiplataforma, que reproduz a maioria dos arquivos de mídia, bem como DVD, CD de áudio, VCD entre outros.

<strong>Por que usar o VLC?</strong>

Na minha opinião, ele é um dos melhores reprodutores de vídeo para o mundo Linux. Possui suporte a vários formatos de arquivos, legendas, dual áudio, entre outros add-ons.

<strong>Instalação</strong>

Você pode escolher entre o VLC dos repositórios Packman ou VideoLan.

Antes de instalar vamos verificar se o repositório Packman/VideoLan está habilitado. Para isso execute:

<code>zypper lr</code>

Caso ele não esteja habilitado execute o seguinte comando:

<strong>Packman</strong>

<code>zypper ar -f http://ftp.gwdg.de/pub/linux/packman/suse/openSUSE_13.2/ "Packman Repository"</code>

<strong>VideoLan</strong>

<code>zypper ar -f http://download.videolan.org/pub/vlc/SuSE/13.2/ VideoLan</code>

Note que não é recomendável utilizar os pacotes do VLC de repositórios diferentes. Então escolha habilitar apenas um.

Agora que já temos o repositório Packman/VideoLan habilitado vamos a instalação do VLC e seus codecs.

Execute o seguinte comando:

<code>sudo zypper in vlc vlc-codecs</code>

Após feito isto será solicitado que você confie neste repositório. Exemplo:

<code>Do you want to reject the key, trust temporarily, or trust always? [r/t/a/? shows all options] (r): t</code>

Escolha entre <em>a</em> ou <em>t</em>.

Após isto começará a instalação.

Após instalado você já poderá usar o VLC no seu openSUSE.

<img src="/assets/wp-content/uploads/2015/02/openSUSE-13.2-VLC-player.jpg" alt="VLC" />

Espero que você tenha gostado. Se ficou alguma dúvida, deixe um comentário que responderemos.