---
layout: wordpress
title: Conheça a BeagleBone Green
excerpt: |
  A BBG é poderosa, ela vem com processador AM335x 1GHz ARM&copy; Cortex-A8, memória de 512MB DDR3, 4GB eMMC de armazenamento interno (isso mesmo, não é necessário SD) e aceleração gráfica 3D.
date: 2015-11-24 10:24:12
author: alexandrevicenzi
permalink: /conheca-a-beaglebone-green/
image: /assets/wp-content/uploads/2015/11/beagle-hd-logo_dd.png
categories:
  - Hardware / DIY
tags:
  - arm
  - beaglebone
  - beaglebone green
  - cloud9
---

Recentemente recebemos da <a href="http://www.filipeflop.com/?utm_medium=PostBBG&amp;utm_campaign=ButecoOpenSource" target="_blank">FilipeFlop</a> a <a href="http://www.seeed.cc/beaglebone_green/" target="_blank">BeagleBone Green</a>.

A BeagleBone Green, ou BBG para os mais íntimos, é produzida pela SeeedStudio e é baseada no hardware da BeagleBone Black. As maiores diferenças são a adição de dois conectores <em>Grove</em> e a remoção do HDMI <em>on-board</em>. Apesar de não possuir HDMI, é possível utilizar uma placa de expansão para obter esta funcionalidade.

A BBG é poderosa, ela vem com processador AM335x 1GHz ARM© Cortex-A8, memória de 512MB DDR3, 4GB eMMC de armazenamento interno (isso mesmo, não é necessário SD) e aceleração gráfica 3D.

<!--more-->

Na imagem abaixo é possível observar um pouco melhor os itens que compõem a BBG.

<a href="/assets/wp-content/uploads/2015/11/black_hardware_details.png" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/11/black_hardware_details.png" alt="BeagleBone Green Hardware" width="40%" height="40%" />
</a>
<p style="text-align: center;"><small>Clique na imagem para ampliar</small></p>
<strong>Review</strong>

Eu particularmente achei a BBG sensacional. Pois foi literalmente <em>plug and play,</em> bastou conecta-la no USB e sair usando. Se você acessar <a href="http://192.168.7.2/" target="_blank">192.168.7.2</a> será possível ler um mini tutorial de como começar a brincar com a BBG. Caso queira sair programando de cara, basta acessar <a href="http://192.168.7.2:3000/" target="_blank">192.168.7.2:3000</a> para iniciar o Cloud9 IDE.

Abaixo, um humilde exemplo, para demonstrar como é simples piscar um LED.

<script src="//gistfy-app.herokuapp.com/github/butecoopensource/exemplos/bbg/led.py" type="text/javascript"></script>
<iframe class="aligncenter" src="https://www.youtube.com/embed/bA9s2MHtGgk" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

Para finalizar eu gostaria de dizer que o micro cabo USB que acompanha a placa, é praticamente inútil de tão curto, porém, isso é o de menos. Em relação ao acabamento da placa, só posso dizer que é impecável. Comparado com outras placas que já comprei (BPi, RPi, Arduino, etc.), achei a BGG com um acabamento superior a todas demais.

<img class="aligncenter" src="/assets/wp-content/uploads/2015/11/bbg_selfie.png" alt="BeagleBone Green Board" />

Se você gostou assim como eu, você pode encontrar a <a href="http://www.filipeflop.com/pd-24c7f0-beaglebone-green.html?utm_medium=PostBBG&amp;utm_campaign=ButecoOpenSource" target="_blank">BBG na FilipeFlop</a>, primeira empresa a distribuir esta placa no Brasil.

Continue acompanhando o nosso blog, assim que possível, mostrarei mais alguns exemplos com a BBG. :)