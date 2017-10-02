---
layout: wordpress
title: Conhecendo os módulos do NodeMCU
excerpt: |
  O NodeMCU é um firmware baseado no eLua para os dispositivos ESP8266.  Com o decorrer dos projetos que fazem uso do ESP8266 e NodeMCU, eventualmente será necessário criar um firmware com módulos que não fazem parte da distribuição padrão.
date: 2016-04-05 16:37:00
author: alexandrevicenzi
permalink: /conhecendo-os-modulos-do-nodemcu/
image: /assets/wp-content/uploads/2016/02/nodeMCU-logo-300x300-e1454377964183.png
categories:
  - Hardware / DIY
tags:
  - esp8266
  - i2c
  - lua
  - mqtt
  - nodemcu
  - ntp
  - rtc
---

O <a href="http://nodemcu.com/index_en.html" target="_blank">NodeMCU</a> é um firmware baseado no <a href="http://www.eluaproject.net/" target="_blank">eLua</a> para os dispositivos ESP8266. Se você deseja saber mais sobre o firmware recomendo a leitura do artigo <a href="/nodemcu-lua-para-o-esp8266/">NodeMCU: Lua para o ESP8266</a> que publiquei recentemente. Neste artigo o foco foi a apresentação do firmware e como fazer o flash do seu dispositivo.

Com o decorrer dos projetos que fazem uso do ESP8266 e NodeMCU, eventualmente será necessário criar um firmware com módulos que não fazem parte da distribuição padrão. Sendo assim, o artigo de hoje visa explicar brevemente o que é cada um dos módulos disponíveis. Builds customizadas podem ser feitas através do site <a href="http://nodemcu-build.com/" target="_blank">NodeMCU custom builds</a>.

<!--more-->

Na tabela a seguir é possível observar uma breve descrição sobre os módulos.
<table>
<tbody>
<tr>
<th>Módulo</th>
<th>Descrição</th>
</tr>
<tr>
<td>ADC</td>
<td>Permite acesso ao pino ADC, que é um conversor analógico para digital.</td>
</tr>
<tr>
<td>bit</td>
<td>Oferece manipulação a nível de bit para Integer 32. Funções como <code>shift</code>, <code>and</code>, <code>or</code>, <code>xor</code> entre outras.</td>
</tr>
<tr>
<td>BMP085</td>
<td>Adiciona funções para acessar os sensores de temperatura e pressão BMP085 e BMP180.</td>
</tr>
<tr>
<td>CJSON</td>
<td>Adiciona funções para fazer <em>encode</em> e <em>decode</em> de JSON.</td>
</tr>
<tr>
<td>CoAP</td>
<td>Implementação do protocolo <a href="http://tools.ietf.org/html/rfc7252" target="_blank">CoAP</a></td>
</tr>
<tr>
<td>crypto</td>
<td>Implementa alguns algoritmos de criptografia (AES ECB e AES CBC), hash (MD5 e SHA), HMAC e Base64.</td>
</tr>
<tr>
<td>DHT</td>
<td>Adiciona funções para acessar os sensores de temperatura e umidade da linha DHT.</td>
</tr>
<tr>
<td>end user setup</td>
<td>Permite a configuração de credencias WiFi do ESP8266 sem o uso de Serial.</td>
</tr>
<tr>
<td>file</td>
<td>Permite acesso (leitura e gravação) ao sistema de arquivos do ESP8266.</td>
</tr>
<tr>
<td>GPIO</td>
<td>Permite acesso aos pinos GPIO (General Purpose Input/Output).</td>
</tr>
<tr>
<td>HX711</td>
<td>Adiciona funções para acessar o módulo HX711 (Load Cell Amplifier).</td>
</tr>
<tr>
<td>I²C</td>
<td>Adiciona funções de leitura e gravação para o barramento I²C.</td>
</tr>
<tr>
<td>MQTT</td>
<td>Implementação do protocolo <a href="/mqtt-parte-1-o-que-e-mqtt/">MQTT</a></td>
</tr>
<tr>
<td>net</td>
<td>Implementação de interface de rede, com TCP/IP e UDP.</td>
</tr>
<tr>
<td>node</td>
<td>Permite acesso a funções do sistema, como <code>sleep</code>, <code>restart</code>, <code>heap</code> entre outras.</td>
</tr>
<tr>
<td>1-Wire</td>
<td>Permite acesso a dispositivos que utilizam a comunicação 1-Wire.</td>
</tr>
<tr>
<td>PWM</td>
<td>Adiciona funções para utilizar PWM (<em>Pulse Width Modulation</em> ou Modulação de Largura de Pulso).</td>
</tr>
<tr>
<td>RC (no docs)</td>
<td>Suporte a módulos RC (Remote Control) 433 MHz</td>
</tr>
<tr>
<td>RTC fifo</td>
<td>Implementa armazenamento <em>first-in first-out</em> utilizando a memória RTC.</td>
</tr>
<tr>
<td>RTC mem</td>
<td>Adiciona funções para leitura e gravação da memória RTC.</td>
</tr>
<tr>
<td>RTC time</td>
<td>Armazenamento de hora através dos ciclos <em>deep sleep</em>. Sua intenção é utilizar o protocolo NTP para manter a hora sempre atualizada.</td>
</tr>
<tr>
<td>SNTP</td>
<td>Implementa um cliente NTP, com suporte ao modo NTP <em>anycast</em>.</td>
</tr>
<tr>
<td>SPI</td>
<td>Adiciona suporte a SPI (Serial Peripheral Interface) atraveś dos pinos HSPI.</td>
</tr>
<tr>
<td>timer</td>
<td>Implementação de <em>timers</em>, <em>system counters</em> e <em>uptime</em>.</td>
</tr>
<tr>
<td>TSL2561</td>
<td>Adiciona funções para leitura do sensor de luminozidade TSL2561.</td>
</tr>
<tr>
<td>U8G</td>
<td>Biblioteca gráfica com suporte a vários displays.</td>
</tr>
<tr>
<td>UART</td>
<td>Permite a configuração da porta serial do ESP8266.</td>
</tr>
<tr>
<td>UCG</td>
<td>Biblioteca gráfica com suporte a displays TFT.</td>
</tr>
<tr>
<td>WiFi</td>
<td>Controle das configurações WiFi do NodeMCU (IP, MAC, DHCP, modo de operação entre outras).</td>
</tr>
<tr>
<td>WS2801</td>
<td>Adiciona funções de suporte ao driver WS2801.</td>
</tr>
<tr>
<td>WS2812</td>
<td>Adiciona funções de suporte ao driver WS2801.</td>
</tr>
</tbody>
</table>
Uma descrição mais detalhada, assim como alguns exemplos de uso, podem ser encontrados na <a href="http://nodemcu.readthedocs.org/en/dev/" target="_blank">documentação oficial</a>.

A intenção deste artigo é apenas uma breve introdução para se ter uma ideia do que cada módulo aborda, quando mencionarmos em artigos futuros.

Caso você tenha alguma dúvida sobre algum módulo em questão deixe um comentário.