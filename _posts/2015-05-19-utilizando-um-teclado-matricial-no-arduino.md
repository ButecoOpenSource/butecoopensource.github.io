---
layout: wordpress
title: Utilizando um teclado matricial no Arduino
excerpt: |
  Já faz algum tempo que não falo do Arduino, porém hoje vou mostrar como utilizar um teclado matricial.
  O teclado que estou utilizando é um teclado matricial de membrana com 16 teclas e conector de 8 vias.
date: 2015-05-19 23:07:47
author: alexandrevicenzi
permalink: /utilizando-um-teclado-matricial-no-arduino/
categories:
  - Hardware / DIY
tags:
  - arduino
  - keypad
  - teclado
---

Já faz algum tempo que não falo do Arduino, porém hoje vou mostrar como utilizar um teclado matricial.

O teclado que estou utilizando é um teclado matricial de membrana com 16 teclas e conector de 8 vias. Ele foi fornecido pela <a href="http://www.filipeflop.com/?utm_source=Blog&utm_medium=PostTeclado&utm_campaign=ButecoOpenSource" target="_blank">FILIPEFLOP</a> e você pode comprá-lo <a href="http://www.filipeflop.com/pd-6b55a-teclado-matricial-de-membrana.html?utm_source=Blog&utm_medium=PostTeclado&utm_campaign=ButecoOpenSource" target="_blank">neste link</a>.

<em>A FILIPEFLOP é uma das maiores lojas de componentes eletrônicos do Brasil com diversos produtos online e ótimos preços. Em sua loja virtual você vai encontrar diversos componentes eletrônicos como Arduino, Raspberry Pi, Motores, Sensores e materiais para Robótica com envio para todo Brasil.</em>

<strong>O teclado</strong>

O teclado que vou utilizar é igual o exibido abaixo:

<a href="/assets/wp-content/uploads/2015/05/teclado_matricial.jpg" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/05/teclado_matricial.jpg" alt="" width="30%" height="30%" />
</a>

Sua pinagem pode ser observada na imagem abaixo:

<a href="/assets/wp-content/uploads/2015/05/teclado-membrana-4x4.jpg" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/05/teclado-membrana-4x4.jpg" alt="" width="40%" height="40%" />
</a>

<strong>Conectando no Arduino</strong>

<a href="/assets/wp-content/uploads/2015/05/arduino_keypad_4x4.png" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/05/arduino_keypad_4x4.png" alt="" width="40%" height="40%" />
</a>

A conexão com o Arduino é bem fácil. Existem várias formas de fazer este tipo de conexão, porém escolhi esta por ser a mais simples.

<strong>Código</strong>

Para fazer a leitura das teclas irei utilizar a biblioteca <a href="http://playground.arduino.cc/Code/Keypad" target="_blank">Keypad</a>, como ela não vem junto com a Arduino IDE, é necessário que você instale-a.

Para instalar, <a href="http://playground.arduino.cc/uploads/Code/keypad.zip" target="_blank">faça o download</a> e copie para a pasta <em>libraries</em> que se encontra dentro da raiz da instalação da Arduino IDE.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/arduino-examples/teclado.ino" type="text/javascript"></script>

<strong>Resultado</strong>

Ao executar o código acima o resultado deverá ser semelhante a imagem abaixo:

<a href="/assets/wp-content/uploads/2015/05/teclado_serial.png" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/05/teclado_serial.png" alt="" width="60%" height="60%" />
</a>

Utilizar um teclado matricial no Arduino é relativamente simples, porém muito útil em alguns casos.

Até a próxima.