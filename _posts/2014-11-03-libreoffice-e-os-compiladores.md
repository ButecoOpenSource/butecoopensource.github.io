---
layout: wordpress
title: LibreOffice e os compiladores
date: 2014-11-03 22:44:49
author: marcossouza
permalink: /libreoffice-e-os-compiladores/
categories:
  - Desenvolvimento
tags:
  - compiladores
  - libreoffice
  - linux
---

Olá pessoal, está semana foram liberados os vídeos da LibreOffice Conference 2014. Neste post eu gostaria de citar um vídeo em especial, falando dos compiladores que são utilizados no LibreOffice. Atualmente o LibreOffice utiliza o GCC (GNU Compiler Collection), Clang e MSVC (Micro$oft Visual C++) e suas facilidades/extensões para encontrar erros no código.

Dentre estes o Clang contém uma uma característica bem interessante, que é a criação de plugins. O LibreOffice atualmente criou alguns plugins para buscar erros de downcast/upppercast inválidos, verificar comparação de tipos incompatíveis, e até reescrita de pedaços de código. Estes recursos ajudam muito a encontrar erros de código e a reescrever grandes partes de código automaticamente. O vídeo apresentando por Stephan Bergmann , da Red Hat, aprofunda bastante este assunto. Todos os recursos falados neste vídeo podem ser utilizados por qualquer projeto onde se utilizam estes compiladores.

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=cUiAgJTQVq4" frameborder="0" allowfullscreen></iframe>

Não se esqueça de comentar e de se inscrever no nosso feed. Até mais!