---
layout: wordpress
title: Debugando apps híbridos com o Google Chrome Remote Device
date: 2017-10-06 11:48:30
author: bezzocoaline
permalink: /debugando-apps-hibridos-com-o-google-chrome-remote-device/
categories:
  - Tutoriais
tags:
  - google
  - mobile
  - apps
  - remote device
  - desenvolvimento mobile
  - dev

---

O Remote Device é uma ferramenta do Google Chrome que nos permite debugar sites e apps a fim de facilitar a identificação e solução de problemas (ou apenas para ver como o app ou o site se comporta).

Essa ferramenta serve para debugar tanto em dispositivos Android quanto iOS.

Para realizar o procedimento é só seguir esses passos:

1 - Abra o inspect do Google Chrome;

2 - Dentro do inspect tem um ícone com 3 bolinhas verticais. Clique nele e vá em More Tools - Remote Devices;

3 - Feito isso, irá abrir essa seguinte janela:

<img src="https://i.imgsafe.org/47/470b9047fa.png" />

4 - Como vocês podem perceber, a autorização para ter o acesso remoto do device está pendente, pois precisam liberar esse acesso.
Um alert é enviado para o device de vocês solicitando a permissão do debug. Basta clicar em "Ok";

<img src="https://i.imgsafe.org/47/470b7e7b8a.png"/>

5 - Caso ainda não tenha dado build no seu dispositivo, faça-o. Se já fez, basta abrir o app. Assim que abrir, o Remove Device irá identificar; 

<img src="https://i.imgsafe.org/47/470b73c68b.png" />

6 - Clique em "Inspect". Uma nova janela irá abrir exibindo o seu device + inspect do Chrome para que você possa debugá-lo e assim, facilitar a resolução dos problemas :slightly_smiling_face: 

<img src="https://i.imgsafe.org/47/470b73c68b.png" />

Bom debug!
