---
layout: wordpress
title: Criando uma Central de Multimídia com Raspberry Pi
excerpt: |
  OpenELEC é uma distribuição Linux criada em torno do programa XBMC – um famoso hub de entretenimento de código aberto – e focada na tarefa de transformar seu equipamento em uma central de mídia.
date: 2015-08-20 22:28:06
author: daniel_magevski
permalink: /criando-uma-central-de-multimidia-com-raspberry-pi/
image: /assets/wp-content/uploads/2015/07/openelec.jpg
categories:
  - Distros
tags:
  - openelec
  - raspberrypi
---

Usaremos o OpenELEC para criar a central de multimídia, irei instalar no Raspberry Pi 2, porém também está disponível para o Raspberry PI.

OpenELEC é uma distribuição Linux criada em torno do programa XBMC – um famoso hub de entretenimento de código aberto – e focada na tarefa de transformar seu equipamento em uma central de mídia.

<!--more-->

<strong>Características do OpenELEC.</strong>

<em>Com o seu design compacto, OpenELEC também é ideal para pequenos sistemas baseados em processadores Atom. O sistema tem muitas versões disponíveis, incluindo uma compilação que pode ser executada em praticamente qualquer PC com processador x86 Pentium 4 ou superior. Ele também tem compilações otimizadas para algumas plataformas, que são NVIDIA ION e ION2, Intel GMA HD chipsets, AMD Fusion, Apple TV de primeira geração e o mini-PC Raspberry Pi. Tudo isso para que você não tenha que usar um computador inteiro apenas para colocar em sua sala de estar.</em>

<em>Enquanto outros sistemas operacionais são projetados para ser multiuso, OpenELEC é construído a partir do zero especificamente para uma tarefa, executar o XBMC e executá-lo da melhor maneira possível e com isso ser a melhor opção de gerenciamento de mídia para sua sala de estar.</em>

<em>Para completar, OpenELEC foi projetado para ser gerenciado como um aparelho: ele pode automaticamente atualizar-se e pode ser gerenciado inteiramente a partir da interface gráfica. E mesmo ele sendo uma variante do Linux, você nunca precisará ver um console de gerenciamento, terminal de comando ou ter conhecimento de Linux para usá-lo.</em>

<em>Via <a href="http://www.techtudo.com.br/tudo-sobre/openelec.html" target="_blank">Tech Tudo</a></em>

Você pode adquirir um Raspberry Pi 2 ou outros produtos com a <a href="http://www.lojamundi.com.br/embarcados-raspberry-cubieboard-beagleboneblack.html/?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">Loja Mundi</a>.

<!--more-->

Primeiro baixe a "<strong>Diskimage</strong>" de acordo com seu Raspberry PI clickando <a href="http://openelec.tv/get-openelec" target="_blank">aqui</a>.

Após feito o download iremos descompactar o arquivo.

Nesse caso fiz o download para Raspberry Pi 2.

<code>gunzip OpenELEC-RPi2.arm-5.0.8.img.gz</code>

Agora pesquise pelo seu cartão micro SD, utilizando o comando.

<code>lsblk</code>

Irá te mostrar os dispositivos, após localizado iremos adicionar a imagem no micro SD com o comando dd, preencha a parte <strong>"/mmcblk0"</strong> com o dispositivo localizado, no meu caso foi assim.

<code>sudo dd if=OpenELEC-RPi2.arm-5.0.8.img of=/dev/mmcblk0</code>

Após feito isso coloquei o micro SD no seu Raspberry Pi ligue-o.

Irá aparece essa tela onde você seleciona o idioma.

<a href="/assets/wp-content/uploads/2015/07/OpenElec1.png"><img class="alignnone wp-image-3155" src="/assets/wp-content/uploads/2015/07/OpenElec1.png" alt="OpenElec1" width="649" height="365" /></a>

O OpenELEC já vem o servidor <strong>Samba</strong> e o <strong>SSH</strong> configurado, precisa somente ativa-lo.

<a href="/assets/wp-content/uploads/2015/07/OpenElec2.png"><img class="alignnone wp-image-3156" src="/assets/wp-content/uploads/2015/07/OpenElec2.png" alt="OpenElec2" width="647" height="364" /></a>

Informações sobre o vídeo, repare que está rodando com resolução 1920x1080 com 60HZ.

<a href="/assets/wp-content/uploads/2015/07/OpenElec3.png"><img class="alignnone wp-image-3157" src="/assets/wp-content/uploads/2015/07/OpenElec3.png" alt="OpenElec3" width="644" height="362" /></a>

Aqui os compartilhamentos que o OpenELEC aceita, NFS,Samba, etc...

<a href="/assets/wp-content/uploads/2015/07/OpenElec5.png"><img class="alignnone wp-image-3159" src="/assets/wp-content/uploads/2015/07/OpenElec5.png" alt="OpenElec5" width="649" height="365" /></a>

Escolha os addons de sua preferência para ver séries, assistir filmes, ouvir músicas e etc...

Confira o vídeo abaixo o funcionamento dele.

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=-U7kZF14tDQ" frameborder="0" allowfullscreen></iframe>

Baixe o aplicativo para <a href="https://play.google.com/store/apps/details?id=org.xbmc.kore" target="_blank">android</a>, com ele você pode controlar pelo celular, ou para <a href="https://itunes.apple.com/us/app/unofficial-official-xbmc-remote/id520480364?ls=1&amp;mt=8" target="_blank">IOS</a>.