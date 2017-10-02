---
layout: wordpress
title: Sensor de temperatura e umidade no Arduino
date: 2015-07-09 21:29:14
author: alexandrevicenzi
permalink: /sensor-de-temperatura-e-umidade-no-arduino/
categories:
  - Hardware / DIY
tags:
  - arduino
  - dht11
  - dht22
  - sensores
  - temperatura
---

Já faz algum tempo que não falo do Arduino, pois bem, hoje irei mostrar um exemplo simples. Vamos utilizar um sensor para saber temperatura.

<strong>Material utilizado</strong>

<ul>
    <li>Arduino Uno, que pode ser comprado <a href="http://www.filipeflop.com/pd-6b58d-arduino-uno-r3-cabo-usb.html?utm_source=BlogButeco&utm_medium=Banner&utm_campaign=ButecoOpenSource">aqui</a></li>
    <li>Sensor de Umidade e Temperatura DHT11, que pode ser comprado <a href="http://www.filipeflop.com/pd-6b8f7-sensor-de-umidade-e-temperatura-dht11.html?utm_source=BlogButeco&utm_medium=Banner&utm_campaign=ButecoOpenSource">aqui</a></li>
    <li>Resistor 10K</li>
</ul>

<!--more-->

Além disso, pode ser necessário protoboard e cabos para a conexão, tudo pode ser encontrado na <a href="http://www.filipeflop.com/?utm_source=BlogButeco&utm_medium=Banner&utm_campaign=ButecoOpenSource">FILIPEFLOP</a>.

<em>A FILIPEFLOP é uma das maiores lojas de componentes eletrônicos do Brasil com diversos produtos online e ótimos preços. Em sua loja virtual você vai encontrar diversos componentes eletrônicos como Arduino, Raspberry Pi, Motores, Sensores e materiais para Robótica com envio para todo Brasil.</em>

Agora que você já possui o material em mão vamos ao código.

Antes de iniciar, vamos fazer o download da biblioteca do sensor DHT11. A <a href="https://github.com/adafruit/DHT-sensor-library">biblioteca do Adafruit</a> é compátivel com os modelos DHT11, DHT21, DHT22 e AM2301. Você pode fazer o download dela <a href="https://github.com/adafruit/DHT-sensor-library/archive/master.zip">aqui</a>.

Feito isto, vamos ao código.

<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/ButecoOpenSource/arduino-examples/DHT11Sensor.ino'></script>

Note que foi definido o pino 8 para leitura. Também é necessário definir qual o modelo que estamos usando, no nosso caso o DHT11.

Agora vamos conectar o DHT11 ao Arduino.

<img src="/assets/wp-content/uploads/2015/07/dht11-arduino.png" alt="Sensor DHT11 Arduino">

Note que foi colocado um resistor de 10K entre o pino de dados e o pino VCC. O terceiro pino não é utilizado, e alguns modelos possuem apenas 3 pinos.

Abaixo você pode observar o resultado.

<img src="/assets/wp-content/uploads/2015/07/sensor-temperatura-arduino.png" alt="Sensor Temperatura Arduino">

Para testar a mudança de temperatura é simples, posicione um secador de cabelo próximo ao sensor e espere a temperatura subir.

Espero que você tenha gostado. Deixe suas dúvidas nos comentários.