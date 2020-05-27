---
layout: wordpress
title: Sensor de temperatura gráfico com Arduino e LCD 16x2
date: 2015-07-20 22:31:20
author: alexandrevicenzi
permalink: /sensor-de-temperatura-grafico-com-arduino-e-lcd-16x2/
categories:
  - Hardware / DIY
tags:
  - arduino
  - lcd
  - sensor
---

Dando continuidade ao artigo <a href="/sensor-de-temperatura-e-umidade-no-arduino" target="_blank">Sensor de temperatura e umidade no Arduino</a>, hoje vamos ver como utilizar um LCD 16x2 para exibir a temperatura e a umidade capturada pelo sensor DHT11.

A grande diferença entre o artigo anterior e este é o uso do LCD, sendo assim, não há necessidade de conectar o Arduino ao PC só para saber a temperatura.

<!--more-->

<strong>Material utilizado</strong>
<ul>
	<li><a href="http://www.filipeflop.com/pd-6b58d-arduino-uno-r3-cabo-usb.html?utm_source=BlogButeco&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">Arduino UNO</a></li>
	<li><a href="http://www.filipeflop.com/pd-6b8f7-sensor-de-umidade-e-temperatura-dht11.html?utm_source=BlogButeco&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">Sensor de Umidade e Temperatura DHT11</a></li>
	<li><a href="http://www.filipeflop.com/pd-6b7e4-display-lcd-16x2.html?utm_source=BlogButeco&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">LCD 16x2</a></li>
	<li>Resistor 220 Ohm</li>
	<li>Potenciômetro 10K</li>
	<li><a href="http://www.filipeflop.com/pd-6b637-kit-jumpers-macho-macho-x65-unidades.html?utm_source=BlogButeco&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">Cabos</a></li>
	<li><a href="http://www.filipeflop.com/pd-6b60e-protoboard-830-pontos.html?utm_source=BlogButeco&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">Protoboard</a></li>
</ul>
Praticamente todo o material pode ser encontrado na <a href="http://www.filipeflop.com/?utm_source=BlogButeco&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">FILIPEFLOP</a>.

<em>A FILIPEFLOP é uma das maiores lojas de componentes eletrônicos do Brasil com diversos produtos online e ótimos preços. Em sua loja virtual você vai encontrar diversos componentes eletrônicos como Arduino, Raspberry Pi, Motores, Sensores e materiais para Robótica com envio para todo Brasil.</em>

<strong>Código</strong>

Seguindo os passos do artigo anterior, necessitamos a <a href="https://github.com/adafruit/DHT-sensor-library" target="_blank">biblioteca da Adafruit</a> para trabalhar com os sensores DHT11, DHT21, DHT22 e AM2301.

Após isto vamos ao código fonte.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/arduino-examples/LCD_DHT11.ino" type="text/javascript"></script>

Analisando o código, ao criar o objeto <code>dht</code> passamos o pino do Arduino onde esta o sensor e o seu tipo. Já no <code>lcd</code> devemos passar os pinos onde estão ligados os pinos rs, rw, enable, d4, d5, d6 e d7 do LCD.

Outro item interessante é a criação de caracteres no LCD. Como você pode observar possuímos 3 que são: temperatura, umidade e grau. Para criar um caractere usamos a função <code>createChar</code> do LCD, passando um ID e o array de bytes.
Se você deseja criar seu próprio caractere, recomendo o site <a href="http://mikeyancey.com/hamcalc/lcd_characters.php" target="_blank">Custom Character Designer</a> para lhe ajudar.

<strong>Montagem</strong>

Agora que temos o código, vamos montar as peças do quebra-cabeça.

<img title="LCD DHT11" src="/assets/wp-content/uploads/2015/07/lcd_dht11_bb.png" alt="LCD DHT11" />

Como você pode observar, temos um potenciômetro para controlar o contrate da tela, regule conforme você precisar até que o texto seja legível. Os dois últimos pinos (A, K ou Led+, Led-) são para ligar a luz de fundo do LCD e facilitar a leitura.

<strong>Resultado</strong>

<img title="Arduino LCD 16x2 DHT11 Sensor" src="/assets/wp-content/uploads/2015/07/Arduino_LCD_16x2_DHT11_Sensor.jpg" alt="Arduino LCD 16x2 DHT11 Sensor" />

Espero que vocês tenham gostado. Até a próxima.
