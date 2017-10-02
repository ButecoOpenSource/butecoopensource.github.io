---
layout: wordpress
title: PyPy 2.5.1 já está disponível
excerpt: |
  Esta nova versão vem com suporte a arquitetura x86, para os sistemas operacionais Linux 32/64, Mac OS X 64, Windows e OpenBSD, e arquitetura ARM (ARMv6 ou ARMv7 com VFPv3), para o sistema operacional Linux.
date: 2015-03-26 23:06:52
author: alexandrevicenzi
permalink: /pypy-2-5-1-ja-esta-disponivel/
image: /assets/wp-content/uploads/2015/02/Pypy_logo.png
categories:
  - Desenvolvimento
tags:
  - pypy
  - python
---

O PyPy 2.5.1 foi lançado nesta terça (26/03) e vem com algumas melhorias em relação a 2.5.0. Você pode fazer o download desta versão <a href="http://pypy.org/download.html" target="_blank">aqui</a>.

O PyPy é uma alternativa a outros interpretadores como CPython, Jython e IronPython, e de acordo com os <a href="http://speed.pypy.org/" target="_blank">diversos benchmarks publicados</a>, o mais rápido entre eles.

Esta nova versão vem com suporte a arquitetura x86, para os sistemas operacionais Linux 32/64, Mac OS X 64, Windows e OpenBSD, e arquitetura ARM (ARMv6 ou ARMv7 com VFPv3), para o sistema operacional Linux. O suporte ao Windows 64 bits ainda está em desenvolvimento, mas se você deseja verificar o andamento ou contribuir nesse port veja <a href="http://doc.pypy.org/en/latest/windows.html#what-is-missing-for-a-full-64-bit-translation" target="_blank">esta</a> publicação.

<strong>Alterações mais significativas desta versão</strong>

<ul>
	<li>Merge com a stdlib versão 2.7.9 do Python</li>
	<li>O <em>Garbage Collector</em> irá ignorar parte da stack que não teve alteração</li>
	<li>O pdb não irá mais sobrescrever dados do errno e LastError</li>
</ul>

Também foram corrigidos <a href="http://doc.pypy.org/en/latest/whatsnew-2.5.1.html" target="_blank">alguns bugs</a> de versões anteriores do PyPy.

Confira a nota de liberação oficial <a href="http://morepypy.blogspot.com.br/2015/03/pypy-251-released.html" target="_blank">aqui</a>.