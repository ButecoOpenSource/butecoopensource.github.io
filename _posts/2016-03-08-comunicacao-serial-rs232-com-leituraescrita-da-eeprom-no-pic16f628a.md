---
layout: wordpress
title: Comunicação serial RS232 com Leitura/Escrita da EEPROM no PIC16F628A
excerpt: |
  Um dos recursos muito interessantes do PIC, é a possibilidade de utilizar a comunicação serial no padrão RS232. Este post tem como objetivo dar uma breve introdução na implementação desta função e também na utilização da escrita e leitura da memória EEPROM interna do PIC.
date: 2016-03-08 00:00:12
author: brunopiske
permalink: /comunicacao-serial-rs232-com-leituraescrita-da-eeprom-no-pic16f628a/
image: /assets/wp-content/uploads/2016/02/PIC16F628A-e1456826573109.jpg
categories:
  - Desenvolvimento
  - Hardware / DIY
tags:
  - assembly
  - eeprom
  - pic16f628a
  - rs232
---

Muitos cursos de eletrônica fazem uma breve introdução ao mundo dos microcontroladores, mostrando superficialmente como utilizar seus recursos. Pensando nisso, este artigo tem como objetivo mostrar como utilizar dois recursos muito úteis no PIC 16F628A, comunicação serial e armazenamento de dados na memória EEPROM interna do PIC.<!--more-->

Com a comunicação serial é possível que seu projeto interaja com qualquer outro dispositivo que possua este recurso, como computadores, outros microcontroladores e placas de comunicação wireless (os famosos módulos HC-05 por exemplo), entre outras. Já armazenar dados na EEPROM, permite armazenar dados, para que sejam recuperados posteriormente, mesmo que seu circuito tenha sido desligado completamente da alimentação.

Neste pequeno tutorial, irei demonstrar como fazer esta comunicação, de maneira bem simples e didática. Iremos utilizar, além do PIC, uma placa Arduino para recepção e envio de dados pela serial.  Ao enviar um dado do Arduino pela serial para o PIC, ele  armazena este na sua memória interna e reenvia para o Arduino.  Ao pressionar o botão, é feita a leitura da memória e enviado o último dado gravado. O Arduino por sua vez, faz leitura do serial monitor, enviando para a serial tudo o que for escrito, e exibe na tela o que foi recebido pela serial.

Abaixo segue código fonte para o PIC:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_PIC/serial_eeprom.asm?branch=master&amp;lang=armasm" type="text/javascript"></script>

Na rotina principal do PIC, temos o chamado da função que faz a leitura do buffer da serial, caso existir algum dado, ele grava este valor na posição definida da EEPROM, e responde com o mesmo valor, também, caso o botão for pressionado, ele faz a leitura do valor gravado na EEPROM e envia pela serial.

Abaixo código para Arduino:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_PIC/arduino_serial.ino?branch=master&amp;lang=c&amp;style=arduino" type="text/javascript"></script>

A função deste código é apenas fazer a leitura dos dois canais seriais utilizados, o que faz comunicação com o PIC e a serial do Serial monitor, quando receber algum valor do PIC, ele exibe o valor no serial monitor, e quando algo for inserido no serial monitor, ele envia este valor para o PIC.

Esquema Elétrico:

<a href="/assets/wp-content/uploads/2016/02/esquema.png" rel="attachment wp-att-4866"><img class="size-full wp-image-4866 aligncenter" src="/assets/wp-content/uploads/2016/02/esquema.png" alt="esquema" width="829" height="409" /></a>

<script src="//gistfy-app.herokuapp.com/github/BrunoLeandroPiske/exemplos/exemplos_PIC/SERIAL_EEPROM/arduino_serial.c?branch=master&amp;lang=cal&amp;style=arduino" type="text/javascript"></script>

Este foi um breve tópico introdutório para utilização da Serial e EEPROM do PIC, estas duas funcionalidades podem ser melhoradas utilizando-se interrupções, para um melhor aproveitamento da performance do seu PIC. Interrupções no PIC já é tema para um próximo artigo.

Imagem da montagem do PIC no protoboard:

<a href="/assets/wp-content/uploads/2016/02/IMG_3152.jpg" rel="attachment wp-att-4824"><img class=" wp-image-4824 aligncenter" src="/assets/wp-content/uploads/2016/02/IMG_3152.jpg" alt="IMG_3152" width="908" height="767" /></a>