---
layout: wordpress
title: Novidades que virão no GCC 6
excerpt: |
  Postagem sobre novos recursos do GCC 6 ainda a ser lançado.
date: 2016-02-25 23:37:14
author: marcossouza
permalink: /novidades-que-virao-no-gcc-6/
image: /assets/wp-content/uploads/2016/02/index.png
categories:
  - Notícias
tags:
  - compiler
  - gcc
---

Apesar do Clang estar ganhando terreno, o GCC ainda tem seu brilho. Confira algumas novidades da próxima release deste ótimo compilador:
<ul>
	<li>Detecção de indentação errônea: O propósito deste warning é evitar erros como o que aconteceu com código relacionado ao SSL na Apple, onde uma indentação errada disfarçou um código que sempre executado, onde era necessário ser executado dentro de um bloco condicional. Para mais informações, veja <a href="http://www.theguardian.com/technology/2014/feb/25/apples-ssl-iphone-vulnerability-how-did-it-happen-and-what-next" target="_blank">Apple's SSL iPhone vulnerability</a>.</li>
	<li>Comparações tautológicas: Esse warning existe para avisar o programador quando uma condição é testada duas vezes, ou quando um código testa o mesmo objeto duas vezes, o que pode ser um erro de digitação e pode causar algum erro no código.</li>
	<li>Condições duplicadas: avisará quando existe um "else if" com a mesma comparação de um bloco "if".</li>
	<li>Shift de bits com valor negativo e shift overflow: Essas condições sempre geraram comportamentos indefinidos, e agora o GCC avisa o programador em tempo de compilação quando estas condições aparecerem.</li>
	<li>Deferenciação de ponteiros nulos: GCC ficou mais agressivo na detecção de condições onde um valor NULL é deferenciado e quando uma função retorna NULL mesmo quando um atributo desta função explicitamente desabilita valores NULL.</li>
</ul>
Para mais informações, configura o artigo <a href="http://developerblog.redhat.com/2016/02/23/upcoming-features-in-gcc-6/" target="_blank">novidades no GCC 6</a> da Red Hat.