---
layout: wordpress
title: "QtGamepad: Adicionando suporte a Gamepad no Qt"
excerpt: |
  Um dos mais novos módulos adicionados ao Qt Labs é o QtGamepad, um módulo inspirado na API Gamepad do HTML5. Apesar de inspirado no Gamepad HTML, ele segue o estilo de desenvolvimento do Qt.
date: 2015-05-14 23:08:42
author: alexandrevicenzi
permalink: /qtgamepad-adicionando-suporte-a-gamepad-no-qt/
image: /assets/wp-content/uploads/2015/05/Qt_logo.png
categories:
  - Notícias
tags:
  - jogos
  - qt
  - qt5
  - qtgamepad
  - sdl
---

Um dos mais novos módulos adicionados ao Qt Labs é o QtGamepad, um módulo inspirado na <a href="http://www.w3.org/TR/gamepad/" target="_blank">API Gamepad do HTML5</a>. Apesar de inspirado no Gamepad HTML, ele segue o estilo de desenvolvimento do Qt.

O QtGamepad oferece APIs C++ e Qt Quick a também existe a possibilidade de se criar novos <em>backends</em> graças a arquitetura plug-in. Com ele é possível obter os eventos do dispositivo, como por exemplo, pressionar um botão ou obter estados.

Atualmente os <em>backends</em> para suporte dos gamepads são o X Input no Windows, evdev no Linux e SDL2 para qualquer plataforma suportada pelo SDL2. O <em>backend</em> para suporte a OS X / iOS ainda está em desenvolvimento.

Confira mais informações no <a href="http://lists.qt-project.org/pipermail/development/2015-May/021380.html" target="_blank">anúncio</a> feito na lista de e-mails do projeto.

Via <a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=Qt-Gamepad-Development" target="_blank">Phoronix</a>