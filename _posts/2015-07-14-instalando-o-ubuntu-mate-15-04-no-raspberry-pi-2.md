---
layout: wordpress
title: Instalando o Ubuntu MATE 15.04 no Raspberry PI 2
excerpt: |
  Uma das distribuições Linux mais conhecidas também está disponível para Raspberry PI 2.
  Nesse artigo irei mostrar a instalação do Ubuntu MATE 15.04 no Raspberry PI 2.
date: 2015-07-14 23:03:39
author: daniel_magevski
permalink: /instalando-o-ubuntu-mate-15-04-no-raspberry-pi-2/
image: /assets/wp-content/uploads/2015/07/ubuntu-mate-logo.jpg
categories:
  - Distros
tags:
  - linux
  - mate
  - raspberrypi
  - ubuntu
---

Uma das distribuições Linux mais conhecidas também está disponível para Raspberry PI 2.

Nesse artigo irei mostrar a instalação do Ubuntu MATE 15.04 no Raspberry PI 2.

O Raspberry PI 2 foi cedido pela Loja Mundi e você pode olhar esse e outros produtos clicando <a href="http://www.lojamundi.com.br/embarcados-raspberry-cubieboard-beagleboneblack.html/?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">aqui</a>.

O Ubuntu MATE teve algumas atualizações em relação a versão anterior, Ubuntu MATE 14.10.

<!--more-->

Aqui está uma lista de algumas das novas funcionalidades.
<ul>
	<li>Estabeleceu uma parceria com a Entroware.</li>
	<li>Adicionado PowerPC e Raspberry Pi 2 como arquiteturas de hardware suportado.</li>
	<li>Adicionado um novo tema padrão chamado Yuyo.</li>
	<li>Adicionado interface com o usuário alternar para acasalar Tweak.</li>
	<li>Adicionado suporte totalmente integrado no Compiz.</li>
	<li>Adicionado Tilda pull-down do terminal.</li>
	<li>Adicionado LightDM GTK Configurações Greeter.</li>
	<li>Adicionado categorias para os menus do sistema.</li>
	<li>Atualizado para o Linux 3.19.</li>
	<li>Atualizado para 1.8.2 MATE desktop.</li>
	<li>Atualizado para o Firefox 37.</li>
	<li>Atualizado para LibreOffice 4.4.</li>
	<li>Atualizado temas GTK 3.x para usar ícones de todas as cores.</li>
	<li>Atualizado todos os temas para oferecer suporte melhorado para decoração do lado do cliente (CSD).</li>
	<li>Substituído Totem pelo VLC.</li>
	<li>Substituído Cheese pelo guvcview.</li>
	<li>Substituído upstart pleo systemd.</li>
</ul>
Maiores informações clique <a href="https://ubuntu-mate.org/blog/ubuntu-mate-vivid-final-release/" target="_blank">aqui</a>.

Os programas citados acima estão na versão de quando o Linux MATE 15.04 foi lançado e podem ser atualizados como exemplo o Firefox e outros.

Vamos para a instalação, acesse <a href="https://ubuntu-mate.org/raspberry-pi" target="_blank">aqui</a> para o download e maiores informaçoes sobre a versão e os programas.

Após ter baixado o arquivo, extrai-o usando esse comando.

<code>bunzip2 ubuntu-mate-15.04-desktop-armhf-raspberry-pi-2.img.bz2</code>

Agora pesquise pelo seu cartão micro SD, utilizando o comando.

<code>lsblk</code>

Irá te mostrar os dispositivos, após localizado iremos adicionar a imagem no micro SD com o comando dd, preencha a parte "/dev/mmcblk0" com o dispositivo localizado, no meu caso foi assim.

<code>sudo dd if=ubuntu-mate-15.04-desktop-armhf-raspberry-pi-2.img of=/dev/mmcblk0</code>

Após feito isso coloquei o micro SD no Raspberry Pi 2 e ligue-o.

O sistema irá iniciar e pedir algumas configurações básicas de instalação, nome de usuário, região e etc.

Quando instalar a tela ficará assim.

<a href="/assets/wp-content/uploads/2015/07/imagem1.png"><img class="alignnone wp-image-3004" src="/assets/wp-content/uploads/2015/07/imagem1.png" alt="imagem1" width="751" height="405" /></a>

Imagem do monitor do sistema.

<a href="/assets/wp-content/uploads/2015/07/imagem3.png"><img class="alignnone wp-image-3006" src="/assets/wp-content/uploads/2015/07/imagem3.png" alt="imagem3" width="755" height="407" /></a>

Atualização dos programas.

<a href="/assets/wp-content/uploads/2015/07/imagem2.png"><img class="alignnone wp-image-3005" src="/assets/wp-content/uploads/2015/07/imagem2.png" alt="imagem2" width="750" height="405" /></a>

Assista o vídeo da instalação.

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=LPg30L5yN38" frameborder="0" allowfullscreen></iframe>