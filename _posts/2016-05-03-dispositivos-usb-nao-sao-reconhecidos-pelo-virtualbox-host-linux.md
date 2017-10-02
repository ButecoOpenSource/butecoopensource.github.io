---
layout: wordpress
title: Dispositivos USB não são reconhecidos pelo VirtualBox (host Linux)
excerpt: |
  O VirtualBox é uma das mais bem conceituadas opções para emulação de sistemas operacionais em máquinas virtuais, com suporte a x86 e AMD64/Intel64. Atualmente o VirtualBox possui versões para hosts Windows, Linux, OS X, Solaris e FreeBSD.
  Porém no Linux, em alguns casos, o reconhecimento de dispositivos USB, Webcam e leitores SD Card do host no sistema guest não funciona. Esse problema é geralmente causado por falta de permissão no seu usuário no momento da execução do VirtualBox.
date: 2016-05-03 22:36:32
author: alexandrevicenzi
permalink: /dispositivos-usb-nao-sao-reconhecidos-pelo-virtualbox-host-linux/
image: /assets/wp-content/uploads/2016/04/virtualbox.png
categories:
  - Dicas
tags:
  - linux
  - virtualbox
  - virtualização
  - vm
---

O <a href="https://www.virtualbox.org/" target="_blank">VirtualBox</a> é uma das mais bem conceituadas opções para emulação de sistemas operacionais em máquinas virtuais, com suporte a x86 e AMD64/Intel64. Atualmente o VirtualBox possui versões para hosts Windows, Linux, OS X, Solaris e FreeBSD.

Porém no Linux, em alguns casos o reconhecimento de dispositivos USB, Webcam e leitores SD Card do host no sistema guest não funciona. Esse problema é geralmente causado por falta de permissão no seu usuário no momento da execução do VirtualBox.

<!--more-->

<strong>VirtualBox Extension Pack</strong>

Primeiro vamos instalar o pacote de extensão que adiciona suporte a USB 2.0 e 3.0, VirtualBoxRDP e PXE boot. Faça o <a href="https://www.virtualbox.org/wiki/Downloads" target="_blank">download do VirtualBox Extension Pack</a> para a versão do seu VirtualBox.

No VirtualBox acesse o menu Arquivo &gt; Preferências &gt; Extensões. Na tela de extensões clique no botão de acrescentar e escolha o arquivo que você acabou de baixar.

<a href="/assets/wp-content/uploads/2016/04/vbox-pref-extensoes-a.png"><img class="aligncenter wp-image-5299 size-full" src="/assets/wp-content/uploads/2016/04/vbox-pref-extensoes-a.png" alt="vbox-pref-extensoes-a" width="757" height="424" /></a>

Aguarde a instalação.

<strong>Adicionando seu usuário ao grupo vboxusers</strong>

Primeiro vamos descobrir se seu usuário pertence ao grupo <em>vboxusers</em>. Para isto execute o comando:

<code>groups SEU_USUARIO</code>

O resultado deverá ser algo similar ao abaixo:

<samp>SEU_USUARIO : users vboxusers</samp>

Se nesta linha incluir o <em>vboxusers</em> já está tudo certo.

Caso não, vamos adicionar seu usuário ao grupo com o comando:

<code>sudo adduser SEU_USUARIO vboxusers</code>

ou

<code>usermod SEU_USUARIO -a -G vboxusers</code>

Após isto, faça logoff ou reinicie o computador.

Agora deverá ser possível reconhecer dispositivos conectados ao Linux no sistema hospedeiro.

<a href="/assets/wp-content/uploads/2016/04/vbox-usb-a.png"><img class="aligncenter wp-image-5300 size-large" src="/assets/wp-content/uploads/2016/04/vbox-usb-a-1024x523.png" alt="vbox-usb-a" width="648" height="331" /></a>

Espero que este tutorial ajude você, assim como me ajudou.