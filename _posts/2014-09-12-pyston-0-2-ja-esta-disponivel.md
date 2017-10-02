---
layout: wordpress
title: Pyston 0.2 já está disponível
date: 2014-09-12 15:17:24
author: alexandrevicenzi
permalink: /pyston-0-2-ja-esta-disponivel/
categories:
  - Desenvolvimento
  - Notícias
tags:
  - pyston
  - python
---

O Pyston 0.2 foi anunciado ontem (11/09) e contém várias melhorias se comparado a versão inicial. Ainda existe muito trabalho a ser feito é claro, mas nesta versão já é possível executar programas simples e várias das bibliotecas padrão sem modificação.

Para quem ainda não o conhece, o <a href="https://tech.dropbox.com/2014/04/introducing-pyston-an-upcoming-jit-based-python-implementation/">Pyston </a>é uma nova implementação em código aberto da linguagem Python. Em alto nível, o Pyston pega o código <a href="https://www.python.org/">Python</a> e transforma-o para a representação intermediária LLVM (IR). O IR é então executado através do otimizador LLVM e passado para a <em>engine</em> LLVM JIT, resultando em código de máquina executável. As técnicas JIT tem tido grande sucesso no JavaScript <a href="https://code.google.com/p/v8/">V8</a> do Chrome e o propósito do Pyston é conseguir melhorias semelhantes para o Python.
<h2>Mudanças significativas nesta versão</h2>
<ul>
	<li>Exceções, usando estilo C++ de tratamento</li>
	<li>Herança e metaclasses (sem herança múltipla, até o momento)</li>
	<li>Suporte básico a API C nativa</li>
	<li>Closures, generators, lambdas, generator expressions</li>
	<li>Longs, e integer promotion</li>
	<li>Suporte a multithreading</li>
</ul>
<h2>O que está por vir</h2>
Para a versão 0.3 está prevista uma grande melhoria de desempenho. A versão 0.1 demonstrou a capacidade de produzir código de alto desempenho usando LLVM, mas executando benchmarks reais mostrou que o desempenho atualmente sendo prejudicado pelo seu coletor de lixo. Nos próximos meses, serão feitas melhorias nessas áreas, e também será adicionando um novo framework multicamada, bem como recursos avançados de introspecção do Python.

Via <a href="http://blog.pyston.org/2014/09/11/9/">Blog Pyston</a>