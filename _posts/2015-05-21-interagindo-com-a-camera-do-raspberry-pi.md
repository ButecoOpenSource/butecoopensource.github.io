---
layout: wordpress
title: Interagindo com a câmera do Raspberry Pi
excerpt: |
  Este artigo traz uma introdução de como pode ser feita a integração do Raspberry Pi com seu módulo de câmera chamado picamera.
date: 2015-05-21 23:33:25
author: marcossouza
permalink: /interagindo-com-a-camera-do-raspberry-pi/
image: /assets/wp-content/uploads/2015/05/index.png
categories:
  - Desenvolvimento
tags:
  - linux
  - programação
  - python
  - raspberrypi
  - terminal
---

Interagir com a câmera do Raspberry Pi é muito simples, graças ao módulo criado pelo desenvolvedor Dave Jones (veja seu github <a href="https://github.com/waveform80" target="_blank">aqui</a>). Este módulo torna simples tirar fotos, fazer vídeos e alterar parâmetros da câmera.

A câmera que iremos utilizar foi fornecida pela <a href="http://www.lojamundi.com.br/embarcados-raspberry-cubieboard-beagleboneblack.html?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">Loja Mundi</a> e você pode comprá-la <a href="http://www.lojamundi.com.br/camera-raspberry-pi-5mp.html?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">aqui</a>.

Primeiro, segue um vídeo de como deve-se instalar a câmera no Raspberry:

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=GImeVqHQzsE" frameborder="0" allowfullscreen></iframe>

Para fazer este tutorial, foi utilizada a distribuição Raspbian. Este mesmo tutorial pode ser utilizado com outras distribuições, basta ter o mesmo pacote python instalado. Para instruções de como baixar e instalar o Raspbian no seu Raspberry Pi, basta verificar <a href="https://www.raspberrypi.org/downloads/" target="_blank">aqui</a>.

O pacote necessário para interagir com a câmera se chama <em>python-picamera</em>. Para instalar este pacote no Raspbian, primeiro atualize o repositório e execute o apt-get:

<pre><code class="bash">
apt-get update
apt-get install python-picamera
</code></pre>

Para mostrar sua simplicidade, segue abaixo o código necessário para tirar uma foto com a câmera:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/rasp_camera/camera1.py" type="text/javascript"></script>O código é auto explicativo: é importado o módulo da câmera, instanciado o objeto e chamado o método para tirar uma foto, e esta é salva no arquivo foto.jpg. Segue um "selfie" tirado do Raspberry com este código:
<a href="/assets/wp-content/uploads/2015/05/foto.jpg"><img class="alignnone size-medium wp-image-2292" src="/assets/wp-content/uploads/2015/05/foto-300x200.jpg" alt="foto" width="500" height="400" /></a>

Para tirar fotos a cada 10 segundos:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/rasp_camera/camera2.py" type="text/javascript"></script>

Além disto, o módulo <em>picamera</em> consegue utilizar a câmera para mostrar em tempo real a câmera, funcionando como uma webcam, e ainda consegue gravar vídeos. Para mostrar imagens da câmera em tempo real, basta executar:

<pre><code class="bash">
camera.start_preview()
camera.stop_preview()
</code></pre>

O preview sobrepoe a seção atual do python. Para parar o preview, precione <em>Ctrl-D</em>.

Para gravar um vídeo de 5 segundos:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/rasp_camera/camera3.py" type="text/javascript"></script>Segue vídeo gravado como exemplo:

<iframe width="560" height="315" src="https://youtu.be/MyZ_BHd0fZA" frameborder="0" allowfullscreen></iframe>

Este módulo ainda suporta configurações da câmera, como saturação, brilho, flip vertical e horizontal da imagem, e vários outros recursos:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/rasp_camera/camera4.py" type="text/javascript"></script>

E a imagem tirada com estas configurações:
<a href="/assets/wp-content/uploads/2015/05/foto_config.jpg"><img class="alignnone size-medium wp-image-2300" src="/assets/wp-content/uploads/2015/05/foto_config-300x200.jpg" alt="foto_config" width="500" height="400" /></a>

Existem outras configurações e seus valores padrão são estes:

<pre><code class="bash">
camera.sharpness = 0
camera.contrast = 0
camera.brightness = 50
camera.saturation = 0
camera.ISO = 0
camera.video_stabilization = False
camera.exposure_compensation = 0
camera.exposure_mode = 'auto'
camera.meter_mode = 'average'
camera.awb_mode = 'auto'
camera.image_effect = 'none'
camera.color_effects = None
camera.rotation = 0
camera.hflip = False
camera.vflip = False
camera.crop = (0.0, 0.0, 1.0, 1.0)
</code></pre>

Um efeito interessante é gravar e ir alterando estes efeitos durante a gravação:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/rasp_camera/camera5.py" type="text/javascript"></script>

Clique <a href="http://picamera.readthedocs.org/en/release-1.10/" target="_blank">aqui</a> para a documentação completa sobre o módulo picamera. Espero que tenham gostado, e que se divirtam tanto quanto eu me diverti fazendo esta postagem. Até a próxima!

Referência: <a href="https://www.raspberrypi.org/documentation/usage/camera/python/README.md" target="_blank">Página Oficial Raspberry Pi - Câmera</a>