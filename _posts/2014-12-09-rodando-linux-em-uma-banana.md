---
layout: wordpress
title: Rodando Linux em uma Banana
date: 2014-12-09 12:46:36
author: alexandrevicenzi
permalink: /rodando-linux-em-uma-banana/
categories:
  - Desenvolvimento
  - Hardware / DIY
tags:
  - banana-pi
---

Você já deve ter ouvido falar no <a href="http://www.raspberrypi.org/">Raspberry Pi</a>, um computador <em>single-board</em> do tamanho de um cartão de crédito.

Como aconteceu com o <a>Arduino</a>, não era de se duvidar que também surgiriam opções similares ao Raspberry. Já temos o <a href="http://cubieboard.org/">CubieBoard</a> e o <a href="http://beagleboard.org/bone">BeagleBone</a>, entre outros. Mas hoje eu gostaria de falar sobre o <a href="http://www.bananapi.org/">Banana Pi</a>.

<img src="/assets/wp-content/uploads/2014/12/BananaPi-A-45degree.jpg" alt="BPi" />

O Banana Pi é um fork do projeto Raspberry Pi usando componentes diferentes, mas que tenta manter a máxima compatibilidade possível com o RPi. Algo que desaponta já no começo é que as <em>imagens</em> feitas para RPi não são compatíveis com o BPi, justamente pelo processador não ser o mesmo.

Porém existem várias <em>imagens</em> disponíveis para o BPi. Como o BPi é relativamente novo, algumas das versões ainda estão em fase de testes, como é o caso do XBMC, que no BPi chama-se LeMedia. Você pode conferir <a href="http://www.lemaker.org/resources/9-38/image_files.html">aqui</a> a lista completa dos <em>imagens</em> disponíveis no momento.

Hardware do Banana Pi em comparação ao Raspberry Pi Model B+:

<strong>Prós</strong>
<ul>
	<li>CPU com maior desempenho</li>
	<li>Mais memória RAM</li>
	<li>Porta SATA</li>
	<li>Receptor IR</li>
	<li>Microfone embutido</li>
	<li>USB OTG</li>
	<li>Botões de Ligar/Desligar e Reset</li>
</ul>
<strong>Contras</strong>
<ul>
	<li>GPU inferior</li>
	<li>Quantidade de USBs inferior</li>
</ul>
Confira <a href="http://www.bananapi.org/p/product.html">aqui</a> a especificação completa do BPi.

<strong>Custo x Benefício</strong>

Algo que todos desejam saber é se o produto vale a pena, afinal são +- 45 dólares. Preço similar ao Raspberry Pi.

Apesar da qualidade da placa não ser excelente (você consegue perceber a origem dela :P), ela não deixa a desejar. Nos testes que fiz não tive problema nenhum.

Algo interessante é que segundo as discussões no <a href="http://forum.lemaker.org/forum.php">fórum oficial</a>, o <a href="http://forum.lemaker.org/thread-10247-1-1-hdd_turn_off_bpi.html">BPi não tem tanto problema de queimar</a> em relação ao RPi ao se usar um adaptador HDMI-VGA ou ao ligar um HD USB direto na placa, sem alimentação externa. O teste que fiz com meus HDs, um faz a placa desligar pois ele consumia toda a energia praticamente e o outro não gerou problemas. Por garantia é sempre aconselhado a usar alimentação externa para não correr riscos de danificar a placa.

Em relação a comunidade no fórum, ela ainda é pequena, mas é ativa. Ou seja, suas dúvidas serão respondidas, em alguns casos talvez pelas pessoas que estão por trás do Banana Pi.

<strong>Testes</strong>

Abaixo você pode ver imagens da placa e do Raspbian e do LeMedia em execução.

<a href="/assets/wp-content/uploads/2014/12/bpi_1.jpg"><img src="/assets/wp-content/uploads/2014/12/bpi_1.jpg" alt="BPi" width="40%" height="40%" /></a>

<a href="/assets/wp-content/uploads/2014/12/bpi_3.jpg"><img src="/assets/wp-content/uploads/2014/12/bpi_3.jpg" alt="BPi" width="40%" height="40%" /></a>

<a href="/assets/wp-content/uploads/2014/12/bpi_2.jpg"><img src="/assets/wp-content/uploads/2014/12/bpi_2.jpg" alt="BPi" width="40%" height="40%" /></a>

<a href="/assets/wp-content/uploads/2014/12/bpi_4.jpg"><img src="/assets/wp-content/uploads/2014/12/bpi_4.jpg" alt="BPi" width="40%" height="40%" /></a>

<a href="/assets/wp-content/uploads/2014/12/le_media.jpg"><img src="/assets/wp-content/uploads/2014/12/le_media.jpg" alt="LeMedia" width="40%" height="40%" /></a>

<a href="/assets/wp-content/uploads/2014/12/raspbian.jpg"><img src="/assets/wp-content/uploads/2014/12/raspbian.jpg" alt="Raspbian" width="40%" height="40%" /></a>

Além do Banana Pi existe o Banana Pro, uma placa um pouco mais poderosa.

Espero que vocês tenham gostado do post e que venham a se juntar a comunidade do BPi.