---
layout: wordpress
title: "MQTT Parte 1: O que é MQTT?"
excerpt: |
  O protocolo Message Queue Telemetry Transport (MQTT) está presente no dia a dia da Internet das Coisas (IoT) e o seu principal uso é fazer as máquinas conversarem, também conhecido como Machine-to-Machine (M2M).
date: 2016-02-11 21:37:22
author: alexandrevicenzi
permalink: /mqtt-parte-1-o-que-e-mqtt/
image: /assets/wp-content/uploads/2016/02/mqttorg-glow.png
categories:
  - Desenvolvimento
tags:
  - broker
  - iot
  - mosquitto
  - mqtt
  - pub/sub
  - rabbitmq
---

O protocolo <em>Message Queue Telemetry Transport</em> (MQTT) está presente no dia a dia da Internet das Coisas (IoT) e o seu principal uso é fazer as máquinas conversarem, também conhecido como Machine-to-Machine (M2M).

Nos últimos artigos temos dado ênfase aos sistemas embarcados, mais especificamente o NodeMCU e ao ESP8266. Pois bem, o NodeMCU possui embutido um <a href="http://nodemcu.readthedocs.org/en/dev/en/modules/mqtt/" target="_blank">cliente MQTT</a> para a versão 3.1.1 do protocolo. No artigo de hoje não vou me ater ao NodeMCU, mas sim, irei explicar o que é o protocolo em si, pois ele pode ser utilizado em outros ambientes, além de sistemas embarcados.

<!--more-->

<strong>Introdução</strong>

O protocolo de mensagens MQTT é projetado para um baixo consumo de banda de rede e requisitos de hardware sendo extremamente simples e leve. O MQTT foi desenvolvido pela IBM e Eurotech e é projetado para enviar dados através de redes intermitentes ou com baixa banda de dados, para isto o protocolo é desenvolvido em cima de vários conceitos que garantem uma alta taxa de entrega das mensagens.

O protocolo MQTT é baseado no TCP/IP e ambos, cliente e broker, necessitam da pilha TCP/IP para o seu funcionamento. O MQTT está na mesma camada OSI que o HTTP, porém a maior diferença entre os dois protocolos é o tamanho do payload. No HTTP, o payload é maior, o que inviabiliza o seu uso em conexões de baixa qualidade, como GSM por exemplo.

<strong>Paradigma Pub/Sub</strong>

O MQTT utiliza o paradigma <a href="https://en.wikipedia.org/wiki/Publish%E2%80%93subscribe_pattern" target="_blank">publish/subscribe (pub/sub)</a> para a troca de mensagens. O paradigma pub/sub implementa um middleware chamado de broker. O broker é responsável por receber, enfileirar e disparar as mensagens recebidas dos publishers para os subscribers. O publisher é responsável por se conectar ao broker e publicar mensagens. Já o subscriber é responsável por se conectar ao broker e receber as mensagens que ele tiver interesse. Na imagem abaixo possível observar a arquitetura do paradigma pub/sub.

<img class="aligncenter" src="/assets/wp-content/uploads/2016/02/pub_sub_arch_desai.png" alt="" />

O paradigma pub/sub utiliza o conceito de tópicos para processar as mensagens, em que cada mensagem é enviada para um determinado tópico. Diferente de outros protocolos de mensagem, o publisher não envia a mensagem diretamente ao subscriber, mas sim ao broker. O publisher envia a mensagem para o broker em um determinado tópico. O broker é responsável por receber a mensagem do publisher e fazer uma pré-filtragem das mensagens e enviá-las para os subscribers que estivem registrados em um determinado tópico.

<strong>Brokers e Clientes</strong>

Existem vários brokers MQTT disponíveis, uns pagos, uns gratuitos e por assim vai. Uma lista dos principais brokers pode ser conferida <a href="https://github.com/mqtt/mqtt.github.io/wiki/servers" target="_blank">aqui</a>.

Como sempre, se você pesquisar um pouco verá que alguns são mais populares que os outros. Não vou me ater a explicar um por um, pois não vem ao caso, cabe a você julgar qual broker atende melhor a sua aplicação. Porém, se você não sabe por qual começar, talvez você deva começar com o <a href="http://mosquitto.org/" target="_blank">Mosquitto</a>.

O Mosquitto possui código aberto, é compatível com as versões 3.1 e 3.1.1 do protocolo e funciona muito bem com o NodeMCU. Não possuo experiência com os demais, além deste e o <a href="http://www.rabbitmq.com/">RabbitMQ</a>. O RabbitMQ é um broker AMQP poderoso que através de um plugin permite adicionar suporte a versão 3.x do MQTT.

Em relação aos clientes, varia de linguagem para linguagem, algumas possuem mais de uma opção de implementação, e novamente cabe a você escolher a que melhor lhe atende. A lista dos principais clientes pode ser conferida <a href="https://github.com/mqtt/mqtt.github.io/wiki/libraries">aqui</a>.

<strong>Consideração final</strong>

Este artigo é uma breve introdução ao protocolo MQTT. No próximo artigo iremos utilizar o protocolo para enviar e receber informações. Se você quiser deixar tudo pronto para a segunda parte, tenha em mãos um ESP com o NodeMCU e Python ao seu alcance. :D

Espero que tenham gostado. Caso ficou alguma dúvida não deixe de comentar.

Até a próxima.

<em>Este artigo é uma adaptação da monografia BUSTRACKER: Sistema de rastreamento para transporte coletivo de Alexandre Vicenzi e o texto na íntegra pode ser encontrado <a href="https://raw.githubusercontent.com/alexandrevicenzi/tcc/master/monografia/tcc_bcc_2015_2_avicenzi_AlexandreVicenzi-VF.pdf" target="_blank">aqui</a>.</em>