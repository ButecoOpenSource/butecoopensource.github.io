---
layout: wordpress
title: glibc 2.21 já está disponível
excerpt: |
  A GNU C Library (glibc) é a biblioteca C padrão no sistema GNU e na maioria dos sistemas com Kernel Linux. A versão 2.21 vem com várias correções de bugs algumas funcionalidades novas.
date: 2015-02-06 18:09:23
author: alexandrevicenzi
permalink: /glibc-2-21-ja-esta-disponivel/
image: /assets/wp-content/uploads/2015/02/Linux_kernel_System_Call_Interface_and_glibc.png
categories:
  - Desenvolvimento
tags:
  - c
  - glibc
  - linux
  - posix
---

A versão 2.21 da <a href="http://www.gnu.org/software/libc/" target="_blank">glibc</a> foi liberada hoje (06/02) e já está disponível para download. Esta versão vem com várias correções de bugs e algumas funcionalidades novas.

A GNU C Library (glibc) é a biblioteca C padrão no sistema GNU e na maioria dos sistemas com Kernel Linux.

<strong>Confira algumas das novidades</strong>
<ul>
	<li>Otimização das funções <em>memcpy</em> para arquitetura i386</li>
	<li>Suporte a plataforma Altera Nios II</li>
	<li>Otimização das funções <em>strcpy</em>, <em>stpcpy</em>, <em>strchrnul</em> e <em>strrchr</em> para arquitetura AArch64</li>
	<li>Novo algoritmo de semáforos</li>
	<li>Suporte a <em>TSX lock elision</em> nas arquiteturas powerpc32, powerpc64 e powerpc64le</li>
	<li>A função sigvec (obsoleta) foi removida</li>
	<li>Suporte à extensões MIPS ABI</li>
</ul>
Mais detalhes sobre esta versão podem ser encontrados <a href="http://lists.gnu.org/archive/html/info-gnu/2015-02/msg00001.html" target="_blank">aqui</a>.