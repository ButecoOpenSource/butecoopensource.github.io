---
layout: wordpress
title: Confira algumas novidades do kernel Linux 4.3
excerpt: |
  Breve resumo sobre novas features do Linux 4.3
date: 2015-10-22 21:49:26
author: marcossouza
permalink: /confira-algumas-novidades-do-kernel-linux-4-3/
image: /assets/wp-content/uploads/2015/02/LXF117.fix_.illo_penguin-e1424908179658.jpg
categories:
  - Notícias
tags:
  - kernel
  - linux
---

Como de costume, sempre tentamos mostrar aqui algumas novidades das <em>releases</em> do <em>kernel</em> Linux. Segue uma lista abaixo do que será encontrado na versão 4.3, que já se encontra no rc6 e que em breve será lançado:

DRM (<em>Direct Rendering Manager</em>)/Gráficos
<ul>
	<li>Intel Skylake "Gen9" agora é suportado por padrão e não mais é necessário ativa-lo utilizando uma opção do kernel command-line</li>
	<li>Suporte inicial para  AMD R9 Fury 'Fiji', mas sem gerenciamento de energia ou re-cloking (o que mantém a performance baixa até então).</li>
	<li>Um grande retrabalho foi feito no Nouveau, afim de facilitar futuras melhorias no <em>driver</em>, além de ter algumas melhorias no re-cloking de algumas GPUs da Nvidia. Embora tenham acontecido estas melhorias, a performance até agora é a mesma.</li>
	<li>Suporte a OpenGL 3.3 para o VMware. Este suporte se faz necessário quando o Linux é executado como <em>guest</em> VM no VMware workstation 12 e a utilização do <em>driver</em> VMWgfx no <em>guest</em>, em conjunto com o novo Mesa 11.0.</li>
	<li>Melhorias mínimas em <em>drivers</em> de <em>framebuffer</em></li>
	<li>Várias mudanças para gráficos Intel e diversas melhorias em <em>drivers</em> DRM</li>
</ul>
<!--more-->

Discos / Sistemas de arquivo:
<ul>
	<li>O <em>driver</em> de EXT3 foi removido, já que o EXT4 pode manipular partições EXT3 de forma confiável sem nenhum problema de compatibilidade</li>
	<li>Várias correções para o XFS, EXT4 e F2FS (<em>Flash Friendly File System</em>)</li>
	<li>Melhorias no RAID 5/6 e TRIM para o Btrfs</li>
</ul>
Processadores:
<ul>
	<li>Uma imensa mudança no escalonador que pode "potencialmente afetar qualquer <em>workload</em> de sistemas SMP (sistemas com mais de uma CPU) em existência".</li>
	<li>Otimizações de tempo de <em>boot</em> para máquinas x86</li>
	<li>Variedade de atualização para MIPS</li>
	<li>Suporte ao ARMv8.1</li>
	<li>Atualizações no gerenciamento de energia e com suporte do <em>driver</em> PowerClamp para o Skylake</li>
	<li>Algumas atualizações do Xen</li>
</ul>
Hardware em geral:
<ul>
	<li>Várias atualização de <em>input</em> (teclado, <em>mouse</em> e etc)</li>
	<li>Melhorias no <em>driver</em> Wacom</li>
	<li>Melhorias no sistema de áudio do Linux e suporte a som no Intel Skylake</li>
	<li>Melhor suporte ao <em>laptop</em> Toshiba</li>
</ul>
De minha parte, realmente fiquei curioso sobre o tempo de <em>boot</em> e sobre o <em>workload</em> dos sistemas SMP! Vamos ver se é possível notar em nossos computadores essa tal mudança :)

Até a próxima!

Via <a href="http://www.phoronix.com/scan.php?page=article&amp;item=linux-43-features&amp;num=1" target="_blank">Phoronix</a>