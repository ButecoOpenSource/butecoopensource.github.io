---
layout: wordpress
title: Conectando um display de 7 segmentos no Arduino
excerpt: |
  Confira como utilizar um display de 7 segmentos no Arduino.
date: 2015-01-06 20:00:01
author: alexandrevicenzi
permalink: /conectando-um-display-de-7-segmentos-no-arduino/
image: /assets/wp-content/uploads/2015/01/7-seg.jpg
categories:
  - Desenvolvimento
  - Hardware / DIY
tags:
  - arduino
  - display
---

Hoje o tutorial é bem simples, vamos ver como conectar um display de 7 segmentos no Arduino.

O que você vai precisar:
<ul>
	<li>Um Arduino, no meu caso o UNO R3</li>
	<li>Um display de 7 segmentos, no meu caso testei com o HS-5101-BS e o CTK D166A (Anodo comum)</li>
	<li>8 resistor de 270 Ω</li>
	<li>Uma protoboard</li>
</ul>
Além desses itens você deverá ter um breve conhecimento sobre Arduino e cabos para conexão da protoboard. Se você possui dúvidas sobre o Arduino, sugiro você visitar o <a href="http://arduino.cc/">site oficial</a> (em Inglês).

<strong>Circuito</strong>

Agora vamos ao que interessa. Abaixo você pode observar o esquema do display. Se você usa outro, procure o correto para o seu modelo.

<img src="/assets/wp-content/uploads/2015/01/esquema-display-7-seg.png" alt="display" />

Veja abaixo quais pinos devem ser ligados para formar cada número.
<table>
<tbody>
<tr>
<th>Número</th>
<th>Pinos</th>
</tr>
<tr>
<td>1</td>
<td>b, c</td>
</tr>
<tr>
<td>2</td>
<td>a, b, d, e, g</td>
</tr>
<tr>
<td>3</td>
<td>a, b, c, d, g</td>
</tr>
<tr>
<td>4</td>
<td>b, c, f, g</td>
</tr>
<tr>
<td>5</td>
<td>a, c, d, f, g</td>
</tr>
<tr>
<td>6</td>
<td>a, c, d, e, f, g</td>
</tr>
<tr>
<td>7</td>
<td>a, b, c</td>
</tr>
<tr>
<td>8</td>
<td>a, b, c, d, e, f, g</td>
</tr>
<tr>
<td>9</td>
<td>a, b, c, d, f, g</td>
</tr>
<tr>
<td>0</td>
<td>a, b, c, d, e, f</td>
</tr>
</tbody>
</table>
O pino DP é o ponto. Já os pinos A são de alimentação. O pino 8 é responsável pela alimentação de 5V. O pino 3 não é utilizado.

Para cada pino (a, b, c, d, e, f, g e DP) você deverá adicionar um resistor de 270 Ω (Um lado no display e o outro no Arduino). Confome imagem abaixo.

<img src="/assets/wp-content/uploads/2015/01/esquema_bb.png" alt="ligações" />

<strong>Obs:</strong> <em>Cuide ao fazer as ligações para não se esquecer do resistor, ou você poderá queimar alguma parte do display.</em>

<strong>Código</strong>

Após as ligações do display com o Arduino estarem prontas é hora de começar a programar. Veja abaixo como ficará nosso código.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/arduino-display-7-seg/exemplo.ino" type="text/javascript"></script>

<em>Se você fez ligações diferentes, não se esqueça de mudar a numeração dos pinos.</em>

O código acima irá escrever no display os números de 0 a 9. Além disso, para cada número o DP irá piscar.

<strong>Resultado</strong>

Confira abaixo a execução do nosso código e o circuito montado.

<img src="/assets/wp-content/uploads/2015/01/circuito.jpg" alt="circuito" />

<iframe src="//www.youtube.com/embed/zF3iB5UTslU" width="420" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

<iframe src="//www.youtube.com/embed/ekuZ6-_7WOE" width="420" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

Esta foi a primeira publicação sobre o Arduino. Espero que vocês tenham gostado.