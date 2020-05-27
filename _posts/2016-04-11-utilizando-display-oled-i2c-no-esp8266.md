---
layout: wordpress
title: Utilizando display OLED I2C no ESP8266
excerpt: |
  Displays são sempre úteis em projetos relacionados a Internet das Coisas (IoT). Por exemplo, supondo que estamos desenvolvendo alguma forma de monitoramento de temperatura com o ESP8266, qual a forma mais simples de ficar sabendo a temperatura atual? Creio que seja exibindo-a em um display, certo?
date: 2016-04-11 18:52:21
author: alexandrevicenzi
permalink: /utilizando-display-oled-i2c-no-esp8266/
image: /assets/wp-content/uploads/2016/04/oled_display.jpg
categories:
  - Hardware / DIY
tags:
  - display
  - esp12
  - esp8266
  - i2c
  - iot
  - nodemcu
  - oled
  - u8g
---

Displays são sempre úteis em projetos relacionados a Internet das Coisas (IoT). Por exemplo, supondo que estamos desenvolvendo alguma forma de monitoramento de temperatura com o ESP8266, qual a forma mais simples de ficar sabendo a temperatura atual? Creio que seja exibindo-a em um display, certo?

Sendo assim, o tutorial de hoje irá mostrar como utilizar um display OLED I2C de 0.96 polegadas, pode parecer pequeno, mas acredite, é possível inserir bastante informação nele.

O display que estou utilizando é o <a>OLED com controlador SSD1306</a> com tamanho de 128x64 pixels, que utiliza barramento I2C, suportado pelos ESP-07, ESP-12, entre outros. O I2C é suportado pelo ESP8266, porém placas como a ESP-01 não disponibilizam este pino.

<!--more-->

Para utilizar o display com o NodeMCU, necessitamos de dois módulos adicionais, que são o <strong>I2C</strong> e o <strong>U8G</strong>. Além disso, quando criarmos a build customizada do firmware, necessitamos nos atentar a alguns detalhes. Quando selecionamos o módulo U8G, necessitamos informar três itens, que são: a fonte e os drivers I2C e SPI compatíveis com o display. No nosso caso iremos utilizar as fontes <em>font_6x10</em> e <em>font_chikita</em> e o driver compatível é o <em>SSD1306_128x64</em>.

Para saber como gerar um firmware customizado do NodeMCU eu recomendo a leitura dos artigos <a href="/conhecendo-os-modulos-do-nodemcu">Conhecendo os módulos do NodeMCU</a> e <a href="/nodemcu-lua-para-o-esp8266">NodeMCU: Lua para o ESP8266</a>.

Na imagem a seguir é exibido o esquema do circuito para utilizar o ESP8266 com o display OLED.

<a href="/assets/wp-content/uploads/2016/04/oled_esp12.png" rel="attachment wp-att-5126"><img class="aligncenter size-medium wp-image-5126" src="/assets/wp-content/uploads/2016/04/oled_esp12-300x109.png" alt="OLED I2C" width="300" height="109" /></a>

Agora que você já tem tudo preparado, vamos ao código fonte.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/nodemcu/esp_oled.lua?branch=master" type="text/javascript"></script>

O código acima está comentado com os items que são mais importantes, se você tiver alguma dúvida em relação a ele, não deixe de escrever seu comentário. Na imagem a seguir é possível observar o resultado obtido.

<a href="/assets/wp-content/uploads/2016/04/ESP12-OLED_Display_I2C.png" rel="attachment wp-att-5125"><img class="aligncenter size-medium wp-image-5125" src="/assets/wp-content/uploads/2016/04/ESP12-OLED_Display_I2C-300x169.png" alt="Resultado OLED" width="300" height="169" /></a>

Espero que vocês tenham gostado. Não deixe de seguir o nosso blog, logo teremos mais tutoriais relacionado ao ESP8266.

Até a próxima.
