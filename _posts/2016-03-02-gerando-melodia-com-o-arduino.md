---
layout: wordpress
title: Gerando melodia com o Arduino
excerpt: |
  É possível reproduzir melodias através do arduino de maneira muito simples, utilizando-se a função tone, que gera um sinal PWM conforme a frequência desejada.
date: 2016-03-02 23:51:38
author: brunopiske
permalink: /gerando-melodia-com-o-arduino/
image: /assets/wp-content/uploads/2016/02/logo-arduino.png
categories:
  - Hardware / DIY
tags:
  - arduino
  - hardware
  - mario
  - pwm
---

Com a função <strong><em>tone</em></strong> do Arduino, é possível reproduzir qualquer melodia que desejar. Esta função tem como princípio gerar um sinal <em>PWM</em> no pino definido no chamado desta função.

A função <strong><em>tone</em></strong> recebe os seguintes parâmetros: <code>tone(pino, frequência, duração);</code>.

Quando chamada, esta função irá gerar um sinal <em>PWM</em> na frequência e pelo tempo definido nos parâmetros passados. A frequência é definida em hertz e o tempo em milissegundos.

<!--more-->

Como exemplo, as notas da oitava principal na escala musical, são reproduzidas nas seguintes frequências:

(Dó) C = 261
(Ré) D = 294
(Mi) E = 329
(Fá) F = 349
(Sol) G = 391
(Lá) A = 440
(Si) B = 466

A partir destas informações, é possível construir rotinas com a sequência de notas e tempos para reprodução de qualquer melodia. Vale lembrar porém, que o Arduino é limitado a reprodução apenas de um sinal <em>PWM</em> de cada vez.

Abaixo segue um exemplo de como este recurso pode ser aplicado num projeto, por exemplo, reproduzir um hit ícone da cultura nerd, <a href="https://pt.wikipedia.org/wiki/Super_Mario_Bros." target="_blank">SUPER MARIO Bros.</a> tema original da Nintendo:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_arduino/SUPER_MARIO_THEME.ino?branch=master&amp;lang=c&amp;style=arduino" type="text/javascript"></script>

Montagem do arduino com  o alto falante no protoboard:

<a href="/assets/wp-content/uploads/2016/03/Esquema-Ligacao_bb.png" rel="attachment wp-att-4921"><img class="wp-image-4921 aligncenter" src="/assets/wp-content/uploads/2016/03/Esquema-Ligacao_bb.png" alt="Esquema Ligacao_bb" width="823" height="633" /></a>

Para o alto falante, pode ser utilizado um buzzer, destes encontrados em relógios despertadores.

Fiz um pequeno vídeo mostrando o funcionamento, espero que gostem!

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=cGt4lF6iXGg&feature=youtu.be" frameborder="0" allowfullscreen></iframe>