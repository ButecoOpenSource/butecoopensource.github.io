---
layout: wordpress
title: "NodeMCU: Lua para o ESP8266"
excerpt: |
  O NodeMCU é um firmware e kit de desenvolvimento que permite a programação de protótipos para a Internet das Coisas. O firmware utiliza o paradigma event-driven para facilitar o desenvolvimento de aplicações que necessitem acesso à internet. Além disso, o firmware integra módulos de GPIO, PWM, 1-Wire, I2C, ADC, entre outros, para facilitar o manuseio de módulos baseado no chip ESP8266.
date: 2016-02-02 22:22:16
author: alexandrevicenzi
permalink: /nodemcu-lua-para-o-esp8266/
image: /assets/wp-content/uploads/2016/02/nodeMCU-logo-300x300-e1454377964183.png
categories:
  - Hardware / DIY
tags:
  - esp8266
  - esptool
  - hardware
  - iot
  - lua
  - nodemcu
  - nodemcu flasher
---

O <a href="http://nodemcu.com/index_en.html" target="_blank">NodeMCU</a> é um <em>firmware</em> e kit de desenvolvimento que permite a programação de protótipos para a Internet das Coisas (IoT). O <em>firmware</em> utiliza o paradigma <em>event-driven</em> para facilitar o desenvolvimento de aplicações que necessitem acesso à Internet. Além disso, integra módulos de GPIO, 1-Wire, I2C, SPI, PWM, ADC, entre outros, para facilitar o manuseio de módulos baseados no chip ESP8266.

Na verdade, o NodeMCU é mais que um <em>firmware</em>, é a empresa por trás do NodeMCU Dev Kit, que além do <em>firmware</em>, disponibiliza uma placa de desenvolvimento baseada no ESP8266.

<!--more-->

O <a href="https://pt.wikipedia.org/wiki/Programa%C3%A7%C3%A3o_orientada_a_eventos" target="_blank">paradigma event-driven (ou programação assíncrona)</a> consiste em um estilo de programação em que o fluxo de execução é determinado por eventos disparados por <em>callbacks</em>. Uma <em>callback</em> é uma função que é invocada quando algo acontece. Por exemplo, ao pressionar um botão um evento é disparado e a <em>callback</em> efetuará uma ação para esse evento. Se você já utilizou Javascript ou Node.JS você está bem habituado em usar. Abaixo é possível observar um exemplo de código de um servidor HTTP simples para o NodeMCU no estilo <em>event-driven</em>.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/nodemcu/simple_http.lua?branch=master" type="text/javascript"></script>

O NodeMCU é baseado no <a href="http://www.eluaproject.net/" target="_blank">eLua</a>, uma versão do Lua 5.1 para sistemas embarcados e seu sistema de arquivos é o <a href="https://github.com/pellepl/spiffs" target="_blank">SPI Flash File System (SPIFFS)</a>. O firmware substituiu algumas bibliotecas padrões do Lua por versões específicas para o ESP8266. Além dessas mudanças, algumas bibliotecas, como math e debug, foram completamente removidas para diminuir o consumo de memória do dispositivo.

<strong>Fazendo Flash do seu ESP8266</strong>

Inicialmente vamos fazer o <a href="https://github.com/nodemcu/nodemcu-firmware/releases" target="_blank">download do firmware</a>. O NodeMCU pode ser encontrado nas versões <em>Float</em> e <em>Integer</em> (menor consumo de memória). Se você preferir, também pode compilar a sua própria versão, apenas com os módulos que necessita, através de <a href="http://nodemcu-build.com/" target="_blank">builds customizadas</a>.

Tendo o <em>.bin</em> em mãos, vamos baixar a ferramenta que fará o upload. Existem duas bem populares, o <a href="https://github.com/nodemcu/nodemcu-flasher">NodeMCU Flasher</a>, para Windows, e o <a href="https://github.com/themadinventor/esptool">esptool</a>, multiplataforma. Se você possui o Python e o Pip instalado em sua máquina basta executar <code>pip install esptool</code> para baixar o pacote e instalá-lo, este é o método mais aconselhado de instalação.

Para fazer o flash do ESP8266, é necessário colocá-lo em modo de programação. Isto varia de modelo para modelo, sendo assim eu sugiro a leitura do artigo <a href="/primeiros-passos-com-o-esp8266/">Primeiros passos com o ESP8266</a> para um melhor entendimento.

<strong>NodeMCU Flasher</strong>

Telinhas são sempre agradáveis aos usuários finais, e o NodeMCU Flasher não é diferente. Você deve se preocupar com duas abas apenas, a <em>Operation</em> e a <em>Config</em>.

<img class="aligncenter" src="/assets/wp-content/uploads/2016/02/nodemcu_flasher.png" alt="" />

Escolha a porta COM onde está seu ESP. Em seguida na aba <em>Config</em> escolha o <em>.bin</em> que acabamos de baixar. O firmware sempre fica no offset 0x00000.

<img class="aligncenter" src="/assets/wp-content/uploads/2016/02/nodemcu_firmware_config.png" alt="" />

Volte para a aba <em>Operation</em> e aperte <em>Flash</em>.

<img class="aligncenter" src="/assets/wp-content/uploads/2016/02/nodemcu_flash_underway.png" alt="" />

Se tudo ocorrer bem, a barra de progresso irá andar com o passar dos segundos, além de aparecer os endereço MAC do dispositivo. Se não funcionar, os possíveis problemas são: O ESP não está em modo de programação ou falta os drivers de comunicação do seu controlador UART.

<strong>esptool</strong>

O esptool é um programa que executa em linha de comando, que é do universo unix-like (Linux, BSD, etc), já está habituado com isto. Sendo assim, vamos executar o comando:

<code>./esptool.py write_flash 0x00000 nodemcu-firmware.bin </code>

Se tudo ocorrer bem, você verá uma mensagem dizendo que N bytes foram gravados no endereço 0x00000. Se não funcionar, os possíveis problemas são: O ESP não está em modo de programação, você pode precisar de permissão root para acessar a porta serial ou falta os drivers de comunicação do seu controlador UART.

<strong>Considerações finais</strong>

Tudo funcionou perfeitamente, mas você está se perguntado, o que faço agora? Bem, eu recomendo a instalação do <a href="http://esp8266.ru/esplorer/" target="_blank">ESPlorer</a>, uma mini IDE para desenvolvedores que usam o ESP8266.

<a href="/assets/wp-content/uploads/2016/02/ide_esplorer.png" rel="attachment wp-att-4707"><img class="size-medium wp-image-4707 aligncenter" src="/assets/wp-content/uploads/2016/02/ide_esplorer-300x161.png" alt="ide_esplorer" width="300" height="161" /></a>

Como o ESPlorer você pode programar em LUA, executar comandos diretamente no seu ESP, ou ainda gravar arquivos no sistema de arquivos dele. É uma mão na roda, e o melhor, multiplataforma. :)

Se você ainda está procurando onde comprar seu ESP, eu recomendo a <a href="http://www.filipeflop.com/?utm_medium=Post&utm_campaign=ButecoOpenSource" target="_blank">FILIPEFLOP</a>. Na FILIPEFLOP você pode encontrar vários modelos de ESP, como o <a href="http://www.filipeflop.com/pd-1f55ad-modulo-wifi-esp8266-esp-01.html?utm_medium=Post&utm_campaign=ButecoOpenSource">ESP-01</a>, o <a href="http://www.filipeflop.com/pd-2c1464-modulo-wifi-esp8266-esp-07.html?utm_medium=Post&utm_campaign=ButecoOpenSource" target="_blank">ESP-07</a>, o <a href="http://www.filipeflop.com/pd-2c1441-modulo-wifi-esp8266-esp-12e.html?utm_medium=Post&utm_campaign=ButecoOpenSource" target="_blank">ESP-12</a>, o <a href="http://www.filipeflop.com/pd-2c1419-modulo-wifi-esp8266-esp-201.html?utm_medium=Post&utm_campaign=ButecoOpenSource" target="_blank">ESP201</a> e o <a href="http://www.filipeflop.com/pd-2c140d-modulo-wifi-esp8266-nodemcu-esp-12e.html?utm_medium=Post&utm_campaign=ButecoOpenSource" target="_blank">NodeMCU Dev Kit</a>.

Espero que vocês tenham gostado. Nos próximos artigos mostrarei como programar o ESP usando o firmware NodeMCU.

<em>Este artigo é uma adaptação da monografia BUSTRACKER: Sistema de rastreamento para transporte coletivo de Alexandre Vicenzi e o texto na íntegra pode ser encontrado <a href="https://raw.githubusercontent.com/alexandrevicenzi/tcc/master/monografia/tcc_bcc_2015_2_avicenzi_AlexandreVicenzi-VF.pdf" target="_blank">aqui</a>.</em>