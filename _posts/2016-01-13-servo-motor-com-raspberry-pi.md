---
layout: wordpress
title: Servo motor com Raspberry Pi
excerpt: |
  Breve tutorial de como trabalhar com um servomotor usando a linguagem Python no Raspberry Pi
date: 2016-01-13 11:05:44
author: jonathanaschweder
permalink: /servo-motor-com-raspberry-pi/
image: /assets/wp-content/uploads/2015/05/index.png
categories:
  - Hardware / DIY
  - Tutorial
tags:
  - banana-pi
  - embarcados
  - iot
  - python
  - raspberry pi
  - servomotor
---

Fala galera!
Hoje vamos ver um exemplo de como trabalhar com um servomotor no Raspberry PI usando a linguagem Python.

<!--more-->
Antes de mais nada gostaria de agradecer ao nosso patrocinador <a href="http://baudaeletronica.com.br/" target="_blank">Baú da Eletrônica</a> por ter fornecido o servomotor usado nesse tutorial.
Primeiramente precisaremos conectar nosso servo motor as portas de GPIO, será necessário 3 portas, uma para comando (GPIO21), uma para energia (5v) e uma para terra (GND), no meu caso eu utilizei os pinos 40, 02 e 39 respectivamente, o modelo que utilizei foi o <a href="https://www.baudaeletronica.com.br/raspberry-pi-modelo-b-caixa-de-acrilico-dissipadores.html" target="_blank">Raspberry Pi B+</a>, abaixo pode-se ver a imagem das conexões.

<a href="/assets/wp-content/uploads/2016/01/img_conexoes.jpg" rel="attachment wp-att-4478"><img class="aligncenter wp-image-4478 size-medium" src="/assets/wp-content/uploads/2016/01/img_conexoes-300x169.jpg" alt="conexão cabos" width="300" height="169" /></a>Conforme a imagem acima, no caso do servomotor <a href="https://www.baudaeletronica.com.br/micro-servo-9g-sg90-towerpro.html" target="_blank">Tower Pro SG90</a>, o fio <span style="color: #8a2be2;"><strong>violeta</strong></span> é o 5V e está conectado no pino 2, o fio <span style="color: #0000ff;"><strong>azul</strong></span> que é o de comando, está no pino 40, e por fim o fio <strong><span style="color: #ffd700;">dourado</span></strong> que é o terra está no pino 39.
Uma vez conectado podemos acessar nosso Raspberrypi e salvar o código abaixo em um arquivo qualquer, comentários em cada linha explicam o que cada comando faz.
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos//exemplos_python/rasp_servomotor/servomotor_sg90.py?lang=python&amp;style=github" type="text/javascript"></script>
Este é um post breve para mostrar como trabalhar com servo motores, testem o código e vejam se funciona com vocês, comentem e avaliem e até a próxima pessoal.