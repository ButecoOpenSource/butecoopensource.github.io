---
layout: wordpress
title: Introdução ao ALSA e sua API em C e Python
date: 2014-09-24 23:48:00
author: alexandrevicenzi
permalink: /introducao-ao-alsa-e-sua-api-em-c-e-python/
categories:
  - Desenvolvimento
tags:
  - alsa
  - c
  - python
---

O <em>ALSA</em> (Advanced Linux Sound Architeture) é um framework para <em>kernel space</em> e <em>user space</em> para manipular dispositivos de áudio. No <em>kernel space</em> o <em>ALSA</em> é a API padrão para a criação dos <em>devices drivers </em>de dispositivos de áudio, e no <em>user space</em> o <em>ALSA</em> existe como uma API para permitir a configuração dos dispositivos de áudio que tenham seu <em>device driver</em> implementado com o framework <em>ALSA</em>. Um exemplo de um programa que utilize a API <em>user space</em> do <em>ALSA</em> é o <em>alsamixer</em>.

Abaixo uma imagem do <em>alsamixer</em> executando em uma máquina desktop:

<img src="//i.imgur.com/3Lxu5KC.png" alt="mixer" />

Nesta tela podemos ver algumas configurações da placa de áudio e podemos interagir com esta. Para uma descrição mais completa da API, e do porque ela foi criada <a href="https://en.wikipedia.org/wiki/Advanced_Linux_Sound_Architecture">clique aqui</a>.

A documentação da API pode ser encontrada <a href="http://www.alsa-project.org/alsa-doc/alsa-lib/">aqui</a>. Para os controles básicos de áudio, tal como nível de volume e configuração de microfone, é utilizada a <a href="http://www.alsa-project.org/alsa-doc/alsa-lib/group___simple_mixer.html">API mixer-controls</a> do <em>ALSA</em>.

Para ilustrar o funcionamento básico do <em>ALSA</em> seguem dois exemplos de códigos que permitem alterar o volume de de áudio de uma máquina com Linux. Estes código podem ser baixados <a href="//github.com/ButecoOpenSource/alsa" target="_blank">no nosso github</a>. Um dos exemplos será na linguagem C e o outro será em Python. O primeiro exemplo é na linguagem C, que basicamente diz quais os valores limite do volume da placa de áudio e também permite ao usuário trocar o nível do volume.

<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/alsa/volume.c'></script>

Para compilar este programar basta executar:

<pre><code class="shell">
g++ volume.c -o volume -lasound
</code></pre>

Onde o arquivo salvo tem o nome volume.c.

Executando em minha máquina, tenho a seguinte saída:

<pre><code class="shell">
[marcos@localhost ~]$ ./volume 40000
Volume mínimo: 0 e máximo: 65536
Volume atual: 40000
</code></pre>

Abaixo se encontra um exemplo da utilização do <em>ALSA</em> em Python.

<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/alsa/alsa.py'></script>

Neste exemplo em python, pode-se ver alguns usos do framework <em>ALSA</em>, como pegar e setar configurações de placas e níveis de áudio.

Se você tiver algum problema na execução desses códigos, ou tem alguma dúvida, poste nos comentários!

Não se esqueça se de cadastrar no nosso feed. Até mais!

Autores: Marcos Paulo de Souza e Alexandre Vicenzi