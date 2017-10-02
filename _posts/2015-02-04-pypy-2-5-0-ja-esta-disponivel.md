---
layout: wordpress
title: PyPy 2.5.0 já está disponível
excerpt: |
  O PyPy é uma alternativa a outros interpretadores como CPython (o padrão), Jython e IronPython, e de acordo com os diversos benchmarks publicados, o mais rápido entre eles.
date: 2015-02-04 14:23:06
author: alexandrevicenzi
permalink: /pypy-2-5-0-ja-esta-disponivel/
image: /assets/wp-content/uploads/2015/02/Pypy_logo.png
categories:
  - Desenvolvimento
tags:
  - cpython
  - programação
  - pypy
  - python
---

O PyPy 2.5 foi liberado ontem (03/02) e vem com várias melhorias de desempenho e correções de bugs.

O PyPy é uma alternativa a outros interpretadores como CPython (o padrão), Jython e IronPython, e de acordo com os <a href="http://speed.pypy.org/" target="_blank">diversos benchmarks publicados</a>, o mais rápido entre eles.

<strong>Novidades da versão</strong>
<ul>
	<li>Dicionários agora são ordenados por padrão</li>
	<li>Separação da documentação do <a href="http://doc.pypy.org/" target="_blank">PyPy</a> e do <a href="http://rpython.readthedocs.org/" target="_blank">RPython</a></li>
	<li>Melhorado o tempo de inicialização</li>
	<li>A troca de objetos entre C e o PyPy melhorou, o que melhorou o tempo de I/O</li>
	<li>errno (e GetLastError, WSAGetLastError) agora é lançado o mais próximo possível da função que o chamou</li>
	<li>Melhorias no suporte ao numpy. Mais especificamente o módulo <a href="http://docs.scipy.org/doc/numpy/reference/routines.linalg.html" target="_blank">linalg</a></li>
	<li>Várias outras correções de bugs</li>
</ul>
Você pode fazer o download da nova versão <a href="http://pypy.org/download.html" target="_blank">aqui</a>.