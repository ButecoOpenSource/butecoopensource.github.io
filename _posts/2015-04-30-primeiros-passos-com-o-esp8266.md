---
layout: wordpress
title: Primeiros passos com o ESP8266
excerpt: |
  Para a brincadeira de hoje, iremos necessitar de pelo menos um ESP8266, fique a vontade na escolha do seu módulo, eu irei utilizar o ESP-01 e o ESP-12. Além disso será necessário um módulo UART de 3.3v, um computador com uma porta USB disponível e algum programa para conversar serialmente, no meu caso irei utilizar a própria IDE do Arduino.
  O ESP permite que você conecte ele de duas formas, a primeira e mais comum é o modo de programação, onde é possível fazer upload de arquivos ou enviar comandos, tudo via serial. A outra forma é a de atualização de firmware (ou Flash). Esta por sua vez permite que você sobrescreva o firmware que vem no módulo. Dependendo o fabricante, as vezes nem é disponibilizado um firmware inicial, e você deve fazer o upload antes de iniciar o uso, mas isto é assunto para o próximo artigo.
date: 2015-04-30 08:53:10
author: alexandrevicenzi
permalink: /primeiros-passos-com-o-esp8266/
image: /assets/wp-content/uploads/2015/03/esp8266.jpg
categories:
  - Hardware / DIY
tags:
  - arduino
  - esp-01
  - esp-12
  - esp8266
  - iot
---

Dando continuidade ao artigo <a href="/2015/04/07/conheca-o-esp8266-um-modulo-wifi-por-menos-de-5-dolares/" target="_blank">sobre o ESP8266</a>, hoje irei mostrar os primeiros passos com este módulo. O primeiro passo e o mais importante é colocar ele pra funcionar. :D

<strong>Material necessário</strong>

Para a brincadeira de hoje, iremos necessitar de pelo menos um ESP8266, fique a vontade na escolha do seu módulo, eu irei utilizar o ESP-01 e o ESP-12. Além disso será necessário um módulo UART de 3.3v, um computador com uma porta USB disponível e algum programa para conversar serialmente, no meu caso irei utilizar a própria IDE do Arduino.

<strong>ESP-01 e ESP-12</strong>

Abaixo você pode conferir os meus ESPs montados.

<a href="/assets/wp-content/uploads/2015/04/esp-12-uart.jpg" target="_blank"><img src="/assets/wp-content/uploads/2015/04/esp-12-uart.jpg" width="30%" height="30%"></a>

<a href="/assets/wp-content/uploads/2015/04/esp-01-uart.jpg" target="_blank"><img src="/assets/wp-content/uploads/2015/04/esp-01-uart.jpg" width="30%" height="30%"></a>

<strong>Módulo UART</strong>

No meu caso o módulo usa o chip CP2102 e possui alimentação de 5 e 3.3v.

<a href="/assets/wp-content/uploads/2015/04/cp2102-usb-ttl-high-speed-stc-download-hdd-flash-line-3.jpg">
    <img src="/assets/wp-content/uploads/2015/04/cp2102-usb-ttl-high-speed-stc-download-hdd-flash-line-3.jpg"  width="30%" height="30%" alt="UART USB TTL CP2102">
</a>

<strong>IDE Arduino</strong>

Caso você ainda não possua um aplicativo para comunicar com o ESP, eu sugiro a IDE do Arduino, que pode ser encontrar <a href="http://www.arduino.cc/en/main/Software" target="_blank">aqui</a>.

<strong>Modos de Operação</strong>

O ESP permite que você conecte ele de duas formas, a primeira e mais comum é o modo de programação, onde é possível fazer upload de arquivos ou enviar comandos, tudo via serial. A outra forma é a de atualização de firmware (ou Flash). Esta por sua vez permite que você sobrescreva o firmware que vem no módulo. Dependendo o fabricante, as vezes nem é disponibilizado um firmware inicial, e você deve fazer o upload antes de iniciar o uso, mas isto é assunto para o próximo artigo.

Por padrão, nem sempre ocorre, os módulos ESP saem de fabrica com o firmware <a href="http://www.electrodragon.com/w/ESP8266" target="_blank">AT</a>. Este firmware consiste em uma série de comandos básicos para o uso do módulo em si, mas não se compara ao <a href="http://nodemcu.com/index_en.html" target="_blank">NodeMCU</a>, um firmware que permite que você programe o dispositivo em LUA, transformando ele em um mini Arduino com WiFi integrado. No caso do AT, é necessário o uso de um outro dispositivo para controlar o ESP, como é o caso dos shields Ethernet do Arduino. Mas com o NodeMCU, o ESP se torna auto gerenciável, bastando apenas fazer upload de um script LUA com o código a ser executado.

Confira abaixo como conectar o módulo UART no ESP para usá-lo nos modos de programação a atualização de firmware.

<strong>Conexão</strong>

Lembre-se que estas conexões mudam de acordo com o ESP e o módulo UART escolhido, então não nos comprometemos com os passos a seguir, faça por sua conta e risco. Lembre-se também de usar a voltagem correta.

A conexão básica funciona assim:

<table>
    <tr>
        <th>ESP</th>
        <th></th>
        <th>UART</th>
    </tr>
    <tr>
        <td>RX</td>
        <th><strong>-></strong></th>
        <td>TX</td>
    </tr>
    <tr>
        <td>TX</td>
        <th><strong>-></strong></th>
        <td>RX</td>
    </tr>
    <tr>
        <td>VCC</td>
        <th><strong>-></strong></th>
        <td>VCC</td>
    </tr>
    <tr>
        <td>CH_PD</td>
        <th><strong>-></strong></th>
        <td>VCC</td>
    </tr>
    <tr>
        <td>GND</td>
        <th><strong>-></strong></th>
        <td>GND</td>
    </tr>
</table>

Abaixo você pode observar as conexões específicas, pois além destes pinos, outros são necessários para o funcionamento.

<strong>ESP-01</strong>

Abaixo você pode observar os pinos do ESP-01.

<a href="/assets/wp-content/uploads/2015/04/Esp8266pinout1.png" target="_blank"><img src="/assets/wp-content/uploads/2015/04/Esp8266pinout1.png" width="50%" height="50%" alt="ESP-01 Pins"></a>

<strong>Programação</strong>

Não necessita pinos adicionais.

<strong>Flash</strong>

Para entrar no modo de atualização de firmware, você deve conectar o GND ao GPIO0. Confira imagem abaixo:

<a href="/assets/wp-content/uploads/2015/04/esp01-uart-flash.png" target="_blank"><img src="/assets/wp-content/uploads/2015/04/esp01-uart-flash.png"  width="50%" height="50%" alt="ESP-01 UART Flash"></a>

<strong>ESP-12</strong>

Abaixo você pode observar os pinos do ESP-12.

<a href="/assets/wp-content/uploads/2015/04/esp_12_pin_map.png" target="_blank"><img src="/assets/wp-content/uploads/2015/04/esp_12_pin_map.png" width="50%" height="50%" alt="ESP-12 Pins"></a>

<strong>Programação</strong>

No modo de programação ainda é necessário conectar o pino GND ao GPIO15. Confira imagem abaixo:

<a href="/assets/wp-content/uploads/2015/04/ESP-12-UART-Prog.png" target="_blank">
    <img src="/assets/wp-content/uploads/2015/04/ESP-12-UART-Prog.png" width="30%" height="30%" alt="ESP-12 Pins">
</a>

<strong>Flash</strong>

Para entrar no modo de atualização de firmware, você deve conectar o GND ao GPIO0. Confira imagem abaixo:

<a href="/assets/wp-content/uploads/2015/04/ESP-12-UART-Flash.png" target="_blank">
    <img src="/assets/wp-content/uploads/2015/04/ESP-12-UART-Flash.png" width="30%" height="30%" alt="ESP-12 Pins to Flash">
</a>

<strong>Comunicação Serial</strong>

Agora que já temos o nosso ESP pronto para ser ligado ao PC, vamos ao que interessa, enviar comandos básicos com o firmware AT.

Após abrir a IDE do Arduino vá em <em>Tools > Port</em> e escolha a porta USB onde está o UART. Depois disto, vá em <em>Tools > Serial Monitor</em>. Você deverá ver uma tela como esta:

<a href="/assets/wp-content/uploads/2015/04/serial-monitor.png" target="_blank"><img src="/assets/wp-content/uploads/2015/04/serial-monitor.png" width="70%" height="70%" alt="Arduino Serial Monitor"></a>

Agora vamos configurar a comunicação. Por padrão a velocidade é <em>9200 baud</em> e o fim de linha é <em>Both NL &amp; CR</em>, como mostrado acima, mas caso você tenha problemas, tente mudar estes valores.

Depois de configurar vamos aos comandos básicos:

<table style="white-space: nowrap; border-collapse: separate; border-spacing: 10px;">
    <tr>
        <th>Comando</th>
        <th>Valores</th>
        <th>Descrição</th>
        <th>Exemplo</th>
    </tr>
    <tr>
        <td>AT</td>
        <td>N/A</td>
        <td>Verifica se o ESP está OK</td>
        <td>AT</td>
    </tr>
    <tr>
        <td>AT+RST</td>
        <td>N/A</td>
        <td>Reinicia o ESP</td>
        <td>AT+RST</td>
    </tr>
    <tr>
        <td>AT+CWMODE</td>
        <td>1 = Station, 2 = AP, 3 = Ambos</td>
        <td>Define o modo de operação WiFI</td>
        <td>AT+CWMODE=3</td>
    </tr>
    <tr>
        <td>AT+CWLAP</td>
        <td>N/A</td>
        <td>Lista as redes disponíveis</td>
        <td>AT+CWLAP</td>
    </tr>
    <tr>
        <td>AT+CWJAP</td>
        <td>SSID, Senha, Canal, Criptografia</td>
        <td>Conecta a uma rede</td>
        <td>AT+CWJAP="seu SSID","sua senha"</td>
    </tr>
    <tr>
        <td>AT+CWQAP</td>
        <td>N/A</td>
        <td>Desconecta da rede</td>
        <td>AT+CWQAP</td>
    </tr>
    <tr>
        <td>AT+CIPSTATUS</td>
        <td>N/A</td>
        <td>Retorna o status do WiFi</td>
        <td>AT+CIPSTATUS</td>
    </tr>
    <tr>
        <td>AT+CWJAP?</td>
        <td>N/A</td>
        <td>Verifica qual rede conectada</td>
        <td>AT+CWJAP?</td>
    </tr>
    <tr>
        <td>AT+CIFSR</td>
        <td>N/A</td>
        <td>Retorna o IP do ESP na rede</td>
        <td>AT+CIFSR</td>
    </tr>
</table>

O comando mais básico a ser executado é o <em>AT</em>. Ao executar um comando você tem duas possíveis respostas:

<ul>
    <li><em>OK</em> - O seu comando foi executado com sucesso</li>
    <li><em>ERROR</em> - Erro no comando. Ou ele não existe, ou está com parâmetro errado</li>
</ul>

Se você executou o AT e não teve nenhum dos dois retornos, talvez você esteja em uma destas situações:

<ul>
    <li>Você fez a conexão dos pinos errada</li>
    <li>O seu ESP pode estar operando em outra velocidade</li>
    <li>O seu ESP não possui firmware, ou veio com outro que não é o AT</li>
</ul>

Se o seu retorno for algum texto diferente, pode ser outro firmware. Se o texto for caracteres estranhos, provavelmente é a velocidade de comunicação muito elevada.

Espero que este artigo possa ajudar você no mais básico processo de comunicação. Nas próximas publicações mostrarei como alterar o firmware e fazer algumas brincadeiras com LEDs.

Até a próxima.