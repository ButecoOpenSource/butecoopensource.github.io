---
layout: wordpress
title: Veja o que virá de novo no Linux 4.2
excerpt: |
  Resumo breve das novas features que estarão disponíveis no Linux 4.2
date: 2015-07-09 10:11:08
author: marcossouza
permalink: /veja-o-que-vira-de-novo-no-linux-4-2/
image: /assets/wp-content/uploads/2015/02/LXF117.fix_.illo_penguin-e1424908179658.jpg
categories:
  - Notícias
tags:
  - kernel
  - linux
---

No último dia 5 Linus fechou a "merge window", período para inclusão de alterações para uma nova versão do Linux, e criou o primeiro Release Candidate do Linux 4.2. Ainda podem ser adicionada alguma "late feature" no kernel, mas as features abaixo são as que tem destaque nesta nova versão:

<!--more-->

Vídeo e DRM (Direct Rendering Manager):
<ul>
	<li>Novo driver AMDGPU para placas Radeon R9 285 Tonga e futuras GPUs, além da família de APUs Carrizo</li>
	<li>Adicionado suporte de encode de vídeo VCE1 para driver DRM Radeon</li>
	<li>Novo driver DRM para GNU VirtIO, sendo que este poderá ser utilizado para expor aceleração OpenDL/3D para em máquinas virtuais da plataforma de virtualização da Red Hat</li>
	<li>Suporte inicial para processador Atom SoC da Intel, chamado Broxton</li>
	<li>Suporte a "atomic mode-setting", ou "modo atômico de configurações", gora está estável</li>
	<li>Mais drivers DRM obtendo vantagem de interfaces atômicas</li>
</ul>
Processador e Sistema:
<ul>
	<li>Mais código Assembly x86 foi melhorado/removido</li>
	<li>Novas placas e SoCs como Freescale i.MX7D, ZTE ZX296702, e HiSilicon hi6220 suportadas</li>
	<li>Melhorias no subsistema de tracing/performance para processadores Intel</li>
	<li>Subsistema de criptografia adicionado  Jitter RNG, uma nova API para encriptação de chaves públicas</li>
	<li>Melhorias no KVM (Kernel Virtual Machine)</li>
	<li>Arquitetura de processador H8/300 foi adicionada na versão 4.2. Esse processador é utilizado em produtos LEGO Mindstorms RCX.</li>
	<li>Melhorias no scheduler</li>
	<li>Queue spilocks, ou "spinlocks enfileirados", nova feature do kernel.</li>
	<li>Processador HS38, da arquitetura ARCv2, agora é suportado pelo Linux.</li>
</ul>
Disco e Sistema de Arquivos:
<ul>
	<li>NCQ TRIM agora pode ser ligado ou desligado caso você tenha um SSD com um suporte ruim a essa tecnologia</li>
	<li>Melhorias de performance para o GFS2 (Global File System 2), que é um sistema de arquivos focado em cluster</li>
	<li>Melhorias e limpeza de código no EXT4</li>
	<li>O F2FS (Flash Friendly File System) agora tem suporte nativo a criptografia</li>
	<li>Correções e atualizações de quota para o Btrfs</li>
	<li>Melhorias de escalabilidade para o FUSE (Filesystem in User Space)</li>
	<li>XFS agora tem suporte a DAX</li>
</ul>
Outros
<ul>
	<li>Numerosas melhorias no subsistema de áudio</li>
	<li>Melhorias no gerenciamento de energia, no ACPI6 e novo suporte ACPI6 Non-Volatile Memory Device (NV-DIMM)</li>
	<li>Melhorias no subsistema de input (relacionado a joysticks, teclados e etc) e suporte a dispositivos como LogiTech M560, Sony Motion Controller e Sony Navigation Controller para PS3 e PS4</li>
	<li>LEDs do controle wireless do XBox agora funcionam, graças a Valve</li>
	<li>Várias atualizações de drivers plataforma (códigos específicos para um laptop ou placa) da arquitetura x86</li>
	<li>Suporte a UEFI ESRT (EFI System Resource Table), sendo esse um dos requisitos  para permitir atualizações de firmware sendo feitos por um desktop Linux.</li>
	<li>Alterações no staging (drivers que precisam de melhorias ou seguir os padrões dos drivers do kernel)</li>
	<li>Melhorias de performance para NTB (non-transient bridging)</li>
</ul>
Como esta postagem tem muitas siglas incomuns, abaixo segue uma lista de links para algumas das siglas para os mais curiosos:

<a href="https://en.wikipedia.org/wiki/Video_Coding_Engine" target="_blank">VCE1</a>

<a href="https://en.wikipedia.org/wiki/Mode_setting" target="_blank">Atomic mode-setting</a>

<a href="https://pt.wikipedia.org/wiki/Kernel-based_Virtual_Machine" target="_blank">KVM</a>

<a href="http://www.lego.com/en-us/mindstorms/?domainredir=mindstorms.lego.com" target="_blank">Lego MindStorms</a>

<a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=queue-spinlocks-linux-4.2" target="_blank">Queue Spinlock</a>

<a href="https://en.wikipedia.org/wiki/Native_Command_Queuing" target="_blank">NCQ TRIM</a>

<a href="http://www.vivaolinux.com.br/artigo/Linux-Quota-de-disco" target="_blank">Quota</a>

<a href="http://lwn.net/Articles/618064/" target="_blank">DAX</a>

Espero que tenham gostado deste resumo das novas features do Linux. Até a próxima!

Via <a href="http://www.phoronix.com/scan.php?page=article&amp;item=linux-42-features&amp;num=1" target="_blank">Phoronix</a>

&nbsp;