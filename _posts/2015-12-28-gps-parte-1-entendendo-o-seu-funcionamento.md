---
layout: wordpress
title: "GPS Parte 1: Entendendo o seu funcionamento"
excerpt: |
  O GPS é um sistema de navegação global desenvolvido pelo Departamento de Defesa dos Estados Unidos da América. O seu intuito inicial era ser o principal sistema de navegação das forças armadas americanas. A concepção do sistema GPS permite que um usuário, em qualquer local da superfície terrestre, ou próxima a ela, tenha à sua disposição, no mínimo, quatro satélites para serem rastreados.
date: 2015-12-28 20:55:51
author: alexandrevicenzi
permalink: /gps-parte-1-entendendo-o-seu-funcionamento/
image: /assets/wp-content/uploads/2015/12/map_pin.png
categories:
  - Tutorial
tags:
  - geolocalização
  - glonass
  - gnss
  - gps
  - nmea
---

Você já parou pra pensar em como um GPS funciona? Bem, se você ainda não pesquisou sobre o assunto, este post abordará um pouco sobre o que é este dispositivo, que está presente em nosso dia a dia.

Essa série de artigos será divida em três partes. A primeira parte abordará os conceitos básicos. A segunda abordará como se interpreta os dados obtidos do GPS. E por fim será criada uma aplicação Web que indica no mapa onde você está.

<!--more-->

<strong>GNSS</strong>

<em>Global Navigation Satellite Systems</em> (GNSS) é o termo genérico mais comum para sistemas de navegação por satélite que fornece cobertura global de posicionamento em espaço 3D. Atualmente existem dois sistemas GNSS em operação: o <em>Global Positioning System</em> (GPS) e o <em>Globalnaya Navigazionnaya Sputnikovaya Sistema</em> (GLONASS). Além de mais dois em fase de implantação.

<strong>GPS</strong>

O GPS é um sistema de navegação global desenvolvido pelo Departamento de Defesa dos Estados Unidos da América. O seu intuito inicial era ser o principal sistema de navegação das forças armadas americanas. A concepção do sistema GPS permite que um usuário, em qualquer local da superfície terrestre, ou próxima a ela, tenha à sua disposição, no mínimo, quatro satélites para serem rastreados.

O GPS funciona utilizando o processo de trilateração, comumente chamado de triangulação. O processo de trilateração determina a posição de um objeto medindo a distância entre outros objetos que já se sabe a posição, no caso, pontos de referência. Este processo permite calcular a posição dos objetos em espaço 2D e 3D.

<strong>Formato NMEA</strong>

A US National Marine Electronics Association (NMEA) propôs em 1983 o formato NMEA 0183, originalmente definido como interface dos dispositivos eletrônicos marítimos, acabou se tornando o padrão industrial dos receptores GNSS. Uma sentença NMEA, consiste em uma cadeia de caracteres no formato ASCII 8-bit e contém no máximo 82 caracteres.

Toda sentença inicia com $. Os próximos dois caracteres indicam o <em>talker</em> e os próximos três indicam o tipo da sentença. Os <em>talkers</em> mais comuns são GP, indicando GPS, e GL, indicando GLONASS. Os demais campos são separados por vírgula seguidos de um asterisco e um checksum opcional na maioria das mensagens. Por fim a mensagem termina com <em>carriage return</em> (CR) e <em>line feed</em>.

Abaixo é possível observar a sentença GGA, responsável por conter informação de localização e precisão.

<code>$GPGGA,123519,4807.038,N,01131.000,E,1,08,0.9,545.4,M,46.9,M,,*47</code>

Para entender melhor, vamos explicar o que é cada parte:
<table>
<tbody>
<tr>
<td>GGA</td>
<td>Global Positioning System Fix Data</td>
</tr>
<tr>
<td>123519</td>
<td>Hora da Fix 12:35:19 UTC</td>
</tr>
<tr>
<td>4807.038,N</td>
<td>Latitude 48 deg 07.038' N</td>
</tr>
<tr>
<td>01131.000,E</td>
<td>Longitude 11 deg 31.000' E</td>
</tr>
<tr>
<td>1</td>
<td>Qualidade da Fix</td>
</tr>
<tr>
<td>08</td>
<td>Número de satélites visíveis</td>
</tr>
<tr>
<td>0.9</td>
<td>Posição horizontal</td>
</tr>
<tr>
<td>545.4,M</td>
<td>Altitude, em metros, acima do nível do mar</td>
</tr>
<tr>
<td>46.9,M</td>
<td>Nível médio do mar</td>
</tr>
<tr>
<td>(vazio)</td>
<td>Tempo em segundos desde a última atualização do DGPS</td>
</tr>
<tr>
<td>(vazio)</td>
<td>DGPS ID</td>
</tr>
<tr>
<td>*47</td>
<td>checksum*</td>
</tr>
</tbody>
</table>
Bem, por hoje é só pessoal. No próximo artigo irei abordar como implementamos um decodificador do formato NMEA em Python.

<em>Este artigo é uma adaptação da monografia BUSTRACKER: Sistema de rastreamento para transporte coletivo de Alexandre Vicenzi e o texto na íntegra pode ser encontrado <a href="https://raw.githubusercontent.com/alexandrevicenzi/tcc/master/monografia/tcc_bcc_2015_2_avicenzi_AlexandreVicenzi-VF.pdf">aqui</a>.</em>