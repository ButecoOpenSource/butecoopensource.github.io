---
layout: wordpress
title: NVIDIA anuncia driver 358 (beta) para Linux, Solaris e FreeBSD
date: 2015-10-13 20:30:12
author: dsantos
permalink: /nvidia-anuncia-driver-358-beta-para-linux-solaris-e-freebsd/
image: /assets/wp-content/uploads/2015/10/NVIDIA-Driver-Update-Linux-FreeBSD.png
categories:
  - Notícias
tags:
  - driver
  - freebsd
  - kernel
  - linux
  - nvidia
  - solaris
---

A NVIDIA disponibilizou a primeira versão pública beta do <em>driver</em> 358 (358.09) para Linux, FreeBSD e Solaris. Construído sobre o driver 355, a série 358 acrescenta mais peças ao quebra-cabeças da interface com DRM/KMS (<em>Direct Rendering Manager/Kernel Mode Setting</em>) e continua melhorando o suporte ao Mir/Wayland.

<!--more-->

A versão do <em>driver</em> adicionou um novo módulo <em>nvidia-modeset</em> ao <em>kernel</em> para trabalhar em conjunto com o módulo <em>nvidia kernel</em>. Em uma próxima versão do <em>driver</em>, o <em>nvidia-modeset kernel</em> será usado como "base para a interface de configuração do modo fornecido pelo gerenciador de renderização direta do kernel", de acordo com o anuncio.

Esta versão, também corrige o desempenho do OpenGL para: alguns servidores gráficos (<em>X servers</em>); vazamento de memória; <em>flickering</em> e <em>delays</em> ao entrar e/ou sair do modo G-SYNC, dentre várias outras correções.

No <em>driver</em> proprietário para Linux, a NVIDIA também adicionou um novo protocolo para extensões GLX, um novo mecanismo de alocação de memória do sistema para grandes alocações no driver OpenGL e suporte às placas GeForce 805A e GTX 960A.

Fontes:
<a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=NVIDIA-358.09-Released" target="_blank">Phoronix</a>
<a href="https://devtalk.nvidia.com/default/topic/884727/linux-solaris-and-freebsd-driver-358-09-beta-/?offset=1" target="_blank">NVIDIA DevTalk</a>