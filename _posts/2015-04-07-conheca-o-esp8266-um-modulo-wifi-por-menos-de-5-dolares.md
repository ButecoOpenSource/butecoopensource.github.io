---
layout: wordpress
title: "Conheça o ESP8266: Um módulo WiFi por menos de 5 dólares"
excerpt: |
  O ESP8266 é uma solução para a Internet das Coisas (IoT). Ele não é apenas um módulo WiFi que pode ser conectado ao Arduino, mas sim um System-on-a-chip (SoC). Ou seja, ele é uma solução completa para quem deseja criar um dispositivo que necessite conexão WiFi.
date: 2015-04-07 01:49:31
author: alexandrevicenzi
permalink: /conheca-o-esp8266-um-modulo-wifi-por-menos-de-5-dolares/
image: /assets/wp-content/uploads/2015/03/esp8266.jpg
categories:
  - Hardware / DIY
tags:
  - arduino
  - esp8266
  - lua
  - soc
---

O ESP8266 é uma solução para a Internet das Coisas (IoT). Ele não é apenas um módulo WiFi que pode ser conectado ao Arduino, mas sim um <em>System-on-a-chip</em> (SoC). Ou seja, ele é uma solução completa para quem deseja criar um dispositivo que necessite conexão WiFi.

Para fazer esse trabalho, o ESP8266 possui uma memória Flash interna que pode ser utilizada para armazenar arquivos, uma memória interna para o Firmware, uma antena embutida e portas GPIO.

A quantidade de GPIOs varia de acordo com o modelo escolhido. Você pode encontrar modelos com 1 até 10 GPIOs.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/03/esp8266-models.png" alt="Modelos ESP8266" />

<strong>Principais características</strong>
<ul>
	<li>Suporte a 802.11 b/g/n</li>
	<li>Wi-Fi Direct (P2P), Soft-AP</li>
	<li>SDIO 2.0, SPI, UART</li>
	<li>STBC, 1x1 MIMO, 2x1 MIMO</li>
	<li>Consumo em Standby menor que 1.0mW (DTIM3)</li>
	<li>Suporte para antenas</li>
	<li>Protocolo TCP/IP embutido</li>
</ul>
Confira a lista completa das características <a title="ESP8266" href="https://nurdspace.nl/ESP8266" target="_blank">aqui</a>.

<strong>Principais aplicações</strong>
<ul>
	<li>Automação doméstica</li>
	<li>Câmera IP</li>
	<li>Controle via Web de sensores</li>
	<li>Eletrônicos vestíveis</li>
	<li>Localização de dispositivos</li>
</ul>
A grande vantagem deste módulo é o seu preço extremamente baixo. Por exemplo, eu comprei 5 ESP-12 por 15 dólares. Outra vantagem é o seu tamanho reduzido. Se compararmos a um Arduino, além do preço ser bem mais salgado o tamanho nem sempre é pequeno, dependendo do modelo escolhido.

Outro item que chama a atenção é a possibilidade de alteração do Firmware padrão AT, por um Firmware Lua ou MicroPython. Ou seja, você programa em Lua, faz upload do seu arquivo e o ESP8266 ficará executando este script, muito similar ao Arduino.

Se minha proposta de TCC for aceita, eu utilizarei este dispositivo como base para o meu projeto. :)

Se você está esperando uma opinião pessoal sobre este módulo, só tenho a dizer que recomendo. Existem inúmeras possibilidades do que pode ser criado com ele. Se você gosta de IoT você precisa de no mínimo 2 desses. Pelo seu baixo custo, mesmo com o dólar em alta, ainda assim é possível comprar vários. Infelizmente no Brasil o preço dele não é justo, além de não existir todos os modelos. Se você costuma comprar coisas da China, você encontra ele por 2 dólares a unidade. No Brasil é vendido a 35 reais.

Nas próximas publicações irei demonstrar como fazer o Flash deste dispositivo e utiliza Lua para sua programação. Se você gostou do ESP8266 não deixe de ficar ligado no nosso blog.