---
layout: wordpress
title: "GPS Parte 2: Decodificando uma sentença NMEA"
date: 2016-01-11 21:38:15
author: alexandrevicenzi
permalink: /gps-parte-2-decodificando-uma-sentenca-nmea/
image: /assets/wp-content/uploads/2015/12/map_pin.png
categories:
  - Tutorial
tags:
  - geolocalização
  - gps
  - nmea
  - python
---

Na <a href="/gps-parte-1-entendendo-o-seu-funcionamento/" target="_blank">primeira parte</a> sobre GPS vimos como este sistema de rastreamento por satélite funciona. Também aproveitamos para explicar o que é o protocolo NMEA, utilizado pelos sistemas de navegação global.

Uma sentença NMEA é formada por caracteres passíveis de impressão e CR (carriage return) e LF (line feed). Toda sentença inicia com <code>$</code> e termina com &lt;CR&gt; &lt;LF&gt;. Existem três tipos básicos de sentenças: <em>talker sentences</em>, <em>proprietary sentences</em> e <em>query sentences</em>.

<!--more-->

As <em>talker sentences</em> são as sentenças genéricas de comunicação do protocolo, já as <em>proprietary sentences</em> são sentenças proprietárias dos fabricantes e as <em>query sentences</em> são sentenças utilizadas para requisitar informações a partir de um receptor.

Neste artigo iremos ver como implementar um decodificar de sentenças do protocolo NMEA 0183 versão 2.3. Para implementar o decodificador iremos utilizar Python sem nenhuma biblioteca adicional. O código desenvolvido é apenas para ilustrar como é feito este tipo de processo, se você procura algo para utilizar em seu sistema eu recomendo a biblioteca <a href="https://github.com/Knio/pynmea2" target="_blank">pynmea2</a>.

<strong>Decodificando uma sentença</strong>

Para decodificar uma sentença primeiro é necessário entender o seu funcionamento. No caso da sentença GGA (Global Positioning System Fix Data) podemos observar a descrição dos campos abaixo:

<code>$GPGGA,123519,4807.038,N,01131.000,E,1,08,0.9,545.4,M,46.9,M,,*47</code>

Para entender melhor, vamos explicar o que é cada parte:
<table>
<tbody>
<tr>
<td>GP</td>
<td>Talker (GPS)</td>
</tr>
<tr>
<td>GGA</td>
<td>Nome da sentença</td>
</tr>
<tr>
<td>123519</td>
<td>Hora da Fix (12:35:19 UTC)</td>
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
Se você deseja conhecer as demais sentenças e seus campos eu recomento ler a <a href="http://www.tronico.fi/OH6NT/docs/NMEA0183.pdf" target="_blank">especificação do protocolo NMEA 0183</a> (em inglês).

Bem, para entender melhor, vamos primeiro ver as principais partes do código, no fim será exibido o código por completo com alguns exemplos de uso.

<strong>Classe Sentence</strong>

A classe <code>Sentence</code> é a base de todas as sentenças NMEA. Toda sentença deve estender esta classe, como podemos observar na classe <code>GGLSentence</code>.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/nmea/nmea.py?slice=51:90" type="text/javascript"></script>

Toda sentença deve possuir um nome (<code>sentence_name</code>), uma descrição (<code>sentence_description</code>) e seus respectivos campos (<code>fields</code>). Além disto, as classes devem implementar um método validador (<code>is_valid</code>) para verificar se a sentença recebida é valida.

Podemos observar que existe um método para decodificar (<code>parse</code>) a sentença. Como as sentenças devem seguir o mesmo padrão, o método é genérico para todas as classes derivadas de <code>Sentence</code>.

Inicialmente é extraído da sentença o seu checksum caso exista. Após é verificado se a quantidade de campos recebidos na sentença corresponde a quantidade de campos registrados. Por fim, é convertido o valor do campo recebido para um tipo Python compatível.

Como sabemos para que tipo devemos converter determinado campo? É isso que você verá na classe <code>GLLSentence</code>.

<strong>Estendendo a classe Sentence</strong>

Na classe <code>GLLSentence</code> sobrescrevemos as propriedades necessárias para o funcionamento correto do <em>parser</em>.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/nmea/nmea.py?slice=159:174" type="text/javascript"></script>

Como podemos observar, sobrescrevemos os atributos <code>sentence_name</code> e <code>sentence_description</code> com o nome e a descrição da sentença.

O atributo <code>fields</code> foi sobrescrito por uma tupla de tuplas que corresponde ao seguinte: o primeiro valor da tupla é o nome do campo, deve sem um nome de atributo válido, pois ele será atribuído a classe em tempo de execução; o segundo campo é uma descrição para o campo, pode ser qualquer texto; o terceiro campo é uma função/classe que será utilizada para converter o valor. Neste caso deve-se lembrar que a função/classe deve possuir apenas um parâmetro e do tipo <code>str</code>. Isto porque a função/classe é invocada com o valor recebido no campo.

Se observarmos, é possível verificar que o campo <code>latitude</code> será convertido para <code>str</code>, já o campo <code>ns_indicator</code> será convertido para <code>str</code>, porém maiúscula. O campo <code>utc_time</code> usa a classe <code>UTCTimeParser</code> para converter para o tipo <code>datetime.date</code>.

Por fim, implementamos a validação da sentença. No caso da sentença GLL, ela é valida se o <code>status</code> for igual a <code>A</code>. Uma validação não implementada é a do checksum. O checksum serve para verificar se o conteúdo recebido foi o mesmo que o enviado. Como o intuito é apenas exemplificar o funcionamento, podemos ignorar este item.

<strong>Classe NMEAParser</strong>

Para finalizar, vamos verificar como a classe <code>NMEAParser</code> identifica qual a sentença e sua respectiva classe para conversão.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/nmea/nmea.py?slice=220:252" type="text/javascript"></script>

A classe <code>NMEAParser</code> possui um atributo (<code>parsers</code>) responsável por armazenar o nome da sentença e a classe de conversão. Para identificar qual a classe correta extraímos no método <code>parse</code> o nome da sentença recebida. Se não for possível identificar a sentença ou se recebermos uma sentença não suportada é gerada uma exceção.

Abaixo é possível observar o código completo da aplicação com alguns exemplos de uso.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/nmea/nmea.py?slice=220:252" type="text/javascript"></script>

Espero que você tenha gostado deste artigo. Na parte final desta série de artigos, iremos implementar uma pequena aplicação que captura a posição do GPS e informa em uma página Web.

Até a próxima.

<em>Este artigo é uma adaptação da monografia BUSTRACKER: Sistema de rastreamento para transporte coletivo de Alexandre Vicenzi e o texto na íntegra pode ser encontrado <a href="https://raw.githubusercontent.com/alexandrevicenzi/tcc/master/monografia/tcc_bcc_2015_2_avicenzi_AlexandreVicenzi-VF.pdf" target="_blank">aqui</a>.</em>