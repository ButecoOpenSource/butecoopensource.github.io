---
layout: wordpress
title: "MQTT Parte 2: Enviando e recebendo mensagens"
excerpt: |
  Na primeira parte sobre o protocolo MQTT (Message Queue Telemetry Transport) demos uma breve introdução ao assunto, explicando o seu funcionamento, brokers e clients.
  Hoje o artigo é mais prático que teórico. Inicialmente vamos instalar/configurar o broker e após vamos criar em cliente MQTT que irá ser conectar ao broker para enviar ou receber mensagens.
date: 2016-03-10 23:43:51
author: alexandrevicenzi
permalink: /mqtt-parte-2-enviando-e-recebendo-mensagens/
image: /assets/wp-content/uploads/2016/02/mqttorg-glow.png
categories:
  - Desenvolvimento
tags:
  - broker
  - iot
  - mosquitto
  - mqtt
  - paho
  - pub/sub
  - python
---

Na <a href="/mqtt-parte-1-o-que-e-mqtt/">primeira parte</a> sobre o protocolo MQTT (<em>Message Queue Telemetry Transport</em>) demos uma breve introdução ao assunto, explicando o seu funcionamento, <em>brokers</em> e <em>clients</em>.

Hoje o artigo é mais prático que teórico. Inicialmente vamos instalar/configurar o <em>broker</em> e após vamos criar em cliente MQTT que irá ser conectar ao <em>broker</em> para enviar ou receber mensagens.

<!--more-->

Como <em>broker</em> iremos utilizar o <a href="http://mosquitto.org/" target="_blank">Mosquitto</a>. Esta escolha foi feita pela sua simplicidade e facilidade de instalação. Confira a página de <a href="http://mosquitto.org/download/" target="_blank">download</a> para saber como instalar em seu sistema operacional.

As configurações padrão do Mosquitto devem atender a nossa aplicação, mas caso você deseje alterar alguma, o arquivo de configuração na maioria das distribuições irá estar no caminho <code>/etc/mosquitto/mosquitto.conf</code>, e no caminho <em>/etc/mosquitto/mosquitto.conf.example</em> você poderá encontrar um arquivo de exemplo com todas as configurações e os respectivos comentários sobre cada uma.

Caso você não queira configurar um servidor local, você pode utilizar o servidor da Fundação Eclipse, disponível em <a href="http://iot.eclipse.org" target="_blank">iot.eclipse.org</a>. O servidor da Fundação Eclipse escuta na porta 1883 (porta padrão do protocolo MQTTca) e não possui autenticação.

O cliente MQTT será desenvolvido em Python. Na parte 3 desta série de artigos iremos implementar um cliente MQTT no ESP8266 com o NodeMCU, para que se comunique com esta versão feita em Python. Nesta versão o cliente irá representar os papéis de <em>publisher</em> e <em>subscriber</em>, ou seja, as mensagens que ele enviará ao <em>broker</em> retornarão até ele, como um sistema de eco. Inicialmete vamos instalar a biblioteca MQTT desenvolvida pela Fundação Eclipse, para isto execute o comando:

<code>pip install paho-mqtt</code>

Após instalado, vamos ao código fonte.

<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/mqtt/simple_client.py?branch=master'></script>

Acima temos três <em>callbacks</em>: <code>on_connect</code>, responsável por se conectar ao tópico após se conectar ao servidor; <code>on_subscribe</code>, apenas para informar que se conectou ao tópico com sucesso e <code>on_message</code>, responsável por tratar mensagens recebidas.

Também temos as funções <code>loop</code>, responsável por criar o cliente MQTT que ficará escutando as mensagens e <code>send_message</code>, responsável por criar um cliente que envia uma mensagem.

Para executar o exemplo acima temos dois comandos, <code>--serve</code> e <code>--send</code>. Quando utilizamos nosso cliente em modo servidor ele fica em modo blocante, ou seja, nada mais pode ser executando naquele <em>shell</em> enquanto ele está em execução. Quando utilizamos nosso cliente para enviar mensagens, ele solicita uma mensagem ao usuário, envia e termina sua execução.

A execução é bem simples, basta executar os comandos:

<code>python simple_client.py --serve</code> ou <code>python simple_client.py --send</code>

Faça o teste, coloque um cliente em modo servidor e a partir do outro envie mensagens e veja os resultados.

Caso tenha dúvidas, deixe nos comentários que iremos lhe ajudar. Até a próxima parte.