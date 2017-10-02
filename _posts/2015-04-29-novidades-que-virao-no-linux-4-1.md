---
layout: wordpress
title: Novidades que virão no Linux 4.1
excerpt: |
  Algumas novidades que virão com o kernel 4.1 do Linux, listando as principais melhorias desta nova versão.
date: 2015-04-29 09:47:34
author: marcossouza
permalink: /novidades-que-virao-no-linux-4-1/
image: /assets/wp-content/uploads/2015/02/LXF117.fix_.illo_penguin-e1424908179658.jpg
categories:
  - Notícias
tags:
  - kernel
  - linux
---

O primeiro release candidate do Linux 4.1 saiu no dia 26 deste mês, então já podemos verificar o que virá nesta próxima versão, uma vez que o <em>merge window</em>, que é o período onde são incluídos novos patches no kernel, já foi fechado para esta versão. Seguem as principais alterações em cada devida área:

Gráficos / DRM (Direct Rendering Manager):
<ul>
	<li>Driver DRM do Nouveau agora suporta a geração de seu próprio firmware para as placas GeForce GTX 750</li>
	<li>Intel XenGT vGPU agora com suporte a virtualização gráfica</li>
	<li>Driver Radeon com suporte ao DisplayPort MST(Multi-Stream Transport)</li>
	<li>Numerosas melhorias em drivers gráficos de código aberto</li>
</ul>
Sistemas de arquivo / Disco:
<ul>
	<li>Suporte encriptação a nível de sistema de arquivos para o Ext4 (Adicionado pelo Google para o Android)</li>
	<li>TraceFS adicionado ao kernel</li>
	<li>Melhorias no F2FS (Flash Friendly File-System)</li>
	<li>Melhorias na Multi-queue block layer</li>
	<li>Melhorias no RAID 5/6 para RAID por software em MD (Multi Device)</li>
	<li>Drivers de disco, que tenham  suporte, podem fazer uso do NCQ (Native Command Queue) Autosense</li>
	<li>Melhorias no Btrfs para sistemas de arquivo massivos (acima de 20 terabytes)</li>
</ul>
Hardware:
<ul>
	<li>Melhor performance em hardware Cherry Tail e  Bay Trail da Intel</li>
	<li>Suporte ao Chrome OS Lightbar (basicamente uma śerie de LEDs que suportam múltiplas cores)</li>
	<li>Melhoria no suporte a laptops x86 da Dell e Toshiba</li>
	<li>Suporte a Force Feedback / Rumble para o controle do Xbox One</li>
	<li>Modernização do código de áudio</li>
	<li>Adicionado Turbstat para Intel Skylake (que será lançado na segunda metade deste ano)</li>
	<li>Melhoria no gerenciamento de energia para x86 e ARM</li>
	<li>ACPI para processadores ARM de 64-bits (AArch64 / ARM64)</li>
	<li>Melhoria na entropia para processadores AMD Bulldozer</li>
	<li>Suporte a Wacom Bamboo Pad</li>
	<li>Novo driver PMEM (Persistent Memory)</li>
	<li>Melhorias no suporte ao Chrome Book Pixel 2 da Google</li>
	<li>Adicionado suporte a plataforma ARM Annapurna Labs Alpine</li>
</ul>
Outros:
<ul>
	<li>Limpeza de código Assembly para plataforma x86</li>
	<li>Melhorias nos drivers de staging enviados pelo programa NOME Women Outreach Program</li>
</ul>
Se inscreva em nossas redes sociais para ficar por dentro de nossos novos artigos. Até mais!

Via <a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=Linux-4.1-Kernel-Features" target="_blank">Phoronix</a>