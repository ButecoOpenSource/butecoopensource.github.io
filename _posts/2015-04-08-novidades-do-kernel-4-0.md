---
layout: wordpress
title: Novidades do kernel 4.0
excerpt: |
  Resumo das novas feature que serão vistas na versão 4.0 do kernel Linux
date: 2015-04-08 23:12:54
author: marcossouza
permalink: /novidades-do-kernel-4-0/
image: /assets/wp-content/uploads/2015/02/LXF117.fix_.illo_penguin-e1424908179658.jpg
categories:
  - Notícias
tags:
  - kernel
  - linux
  - opensuse
  - redhat
---

Após a versão 3.19, Linus escolheu via enquete no Google Plus para pular para a versão 4.0 do kernel. A versão 4.0 deve ser oficialmente lançada em algumas semanas. Aqui estão algumas novidades desta nova versão:
<ul>
	<li>Live patching: Este recurso permite aplicar patches no Linux com este ainda executando, desta forma sendo desnecessário reiniciar o sistema a cada atualização de algum módulo do kernel. Esta era uma feature a muito tempo esperada, e foi feita unificando as ferramentas Kpatch, da Red Hat e KGraph da SUSE.</li>
	<li>O driver Radeon ganhou suporte ao DisplayPort e melhoria no suporte ao controle de resfriamento</li>
	<li>O driver AMDKFD, responsável pelo suporte ao HSA (Heterogeneous System Architecture, que combina CPU com GPU), agora funciona com a APU Carrizo</li>
	<li>Melhorias no driver Nouveau</li>
	<li>Suporte ao driver Skylake da Intel foi melhorado</li>
	<li>Suporte ao pNFS (Parallel NFS) para poder executar I/O em bloco ao invés de leitura e escrita</li>
	<li>Melhorias no RAID 5/6 do Btrfs</li>
	<li>Novas funcionalidades para o OverlayFS</li>
	<li>Suporte ao SoC Quark da Intel</li>
	<li>Suporte a novo hardware ARM</li>
	<li>Suporte ao processador IBM z13</li>
	<li>Melhor suporte a notebooks Toshiba</li>
	<li>Melhorias no suporte a HID (Human Interface Device) da Logitech</li>
</ul>
Além destas, várias outras pequenas melhorias foram feitas. Só nos resta esperar a release oficial para sabermos se algum feature entrou de última hora. Até mais!

Fonte: <a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=Linux-4.0-Kernel-Big-Features" target="_blank">Phoronix</a>