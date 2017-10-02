---
layout: wordpress
title: Controlando um LED pelo Arduino
excerpt: |
  Veja como controlar um LED pelo Arduino. Iremos fazer duas operações básicas, fazer o LED piscar e alterar sua intensidade.
date: 2015-01-13 08:00:35
author: alexandrevicenzi
permalink: /controlando-um-led-pelo-arduino/
categories:
  - Desenvolvimento
  - Hardware / DIY
tags:
  - arduino
  - led
---

Dando continuidade aos tutoriais do Arduino, hoje veremos como controlar um LED. Iremos fazer duas operações básicas, fazer o LED piscar e alterar sua intensidade.

Material necessário:
<ul>
	<li>Arduino, no meu caso o UNO R3</li>
	<li>Um Led</li>
	<li>Um resistor de 470 Ω (se não possuir, pode ser outro de valor aproximado)</li>
	<li>Uma protoboard e cabos para conexão (se você achar necessário)</li>
</ul>
<strong>Circuito</strong>

Agora que você possui todo o material em mãos, vamos ao circuito. Confira abaixo.

<img src="/assets/wp-content/uploads/2015/01/led_bb.png" alt="Led" />

A montagem é simples, no positivo do LED vai o resistor que será conectado ao pino 3. O negativo vai no pino GND.

<strong>Código</strong>

Iremos fazer o LED piscar, aumentar e diminuir a intensidade da luz. Se você observar usamos a forma analógica e digital. A digital permite apenas acender e apagar o LED. Já na analógica podemos controlar a intensidade da luz, além desses dois itens. Note que para usar o modo analógico você deve escolher um pino <a href="http://arduino.cc/en/Tutorial/PWM">PWM</a>. Os pinos PWM estão marcados com <strong>~</strong> ao lado do número.

Confira abaixo como ficou o nosso código.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/arduino-led/exemplo.ino" type="text/javascript"></script>

<strong>Resultado</strong>

O tutorial pode ser bem simples, mas o resultado final é bacana. Confira abaixo.

<img src="/assets/wp-content/uploads/2015/01/resultado_led.jpg" alt="circuito" />

<iframe src="//www.youtube.com/embed/dziQ01-WtdA" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

Espero que você tenha gostado desta publicação. Não deixe de assinar nosso feed de notícias.