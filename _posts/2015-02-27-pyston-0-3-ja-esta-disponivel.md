---
layout: wordpress
title: Pyston 0.3 já está disponível
excerpt: |
  A versão 0.3 do Pyston foi liberada nesta terça-feira (24/02). O Pyston é uma proposta de uma implementação do Python com alto desempenho.
  Esta é liberação muito importante, pois em relação as versões anteriores, esta versão além de uma maior compatibilidade com o Python, também melhorou o seu desempenho na execução de scripts.
date: 2015-02-27 19:10:49
author: alexandrevicenzi
permalink: /pyston-0-3-ja-esta-disponivel/
image: /assets/wp-content/uploads/2014/12/python-logo.png
categories:
  - Desenvolvimento
tags:
  - jit
  - pyston
  - python
---

A versão 0.3 do Pyston foi liberada nesta terça-feira (24/02). O Pyston é uma proposta de uma implementação do Python com alto desempenho.

Esta é uma liberação muito importante, pois em relação as versões anteriores, esta versão além de uma maior compatibilidade com o Python, também melhorou o seu desempenho na execução de scripts.

<strong>Compatibilidade da linguagem</strong>

Um bom jeito de demonstrar a compatibilidade de um compilador, é rodando ele sobre ele mesmo, o que é chamado de <em>self-hosting</em>.

Como o Pyston não é um compilador estático e muito menos escrito em Python, falar de <em>self-hosting</em> é algo um tanto quanto equivocado. Porém já é possível executar vários scripts do Dropbox no Pyston.

Em relação a versão 0.2, na 0.3 já é possível importar 117 bibliotecas e 27 módulos de extensão. Note que a importação não garante que a biblioteca esteja funcionado corretamente. Porém os planos para a 0.4 incluem casos de testes para estas bibliotecas.

<strong>Desempenho</strong>

Ao contrário das versões 0.1 e 0.2, o foco da 0.3 foi a melhoria de desempenho. Nas versões anteriores o foco era a compatibilidade da linguagem Python.

De acordo com os testes feitos pela equipe do Pyston, ele se mostrou um pouco melhor em relação ao CPython no quesito desempenho.

Nos testes feitos, o Pyston se mostrou 1% mais rápido em relação ao CPython. Claro que 1% não é algo estrondoso, mas já é um bom começo para esta nova implementação do Python.

Você pode observar a comparação de ambos <a href="http://speed.pyston.org/comparison/?exe=1%2BL%2Bdefault%2C2%2BL%2Bdefault&amp;ben=1%2C17%2C8%2C14%2C6%2C9%2C3%2C5%2C12%2C4%2C13%2C7&amp;env=1&amp;hor=false&amp;bas=2%2BL%2Bdefault&amp;chart=normal+bars" target="_blank">aqui</a>.

<strong>Pŕoximos passos</strong>

Os planos das próximas versões incluem alguns itens bem agressivos, como por exemplo, ser capaz de executar o Dropbox no Pyston.

Porém o objetivo é continuar com o desenvolvimento, melhorando cada vez mais o suporte a linguagem Python e manter um desempenho aceitável para execução de scripts.

Confira a nota oficial desta versão <a href="http://blog.pyston.org/2015/02/24/pyston-0-3-self-hosting-sufficiency/" target="_blank">aqui</a>.