---
layout: wordpress
title: Câmera IP com Webcam e Motion
excerpt: |
  As câmeras IPs ganharam grande destaque pela sua facilidade de uso, e preço relativamente acessível. Hoje é simples monitorar a sua casa e enviar imagens para o seu smartphone quando algum movimento for detectado.
  O Motion é um programa que monitora o sinal de câmeras e permite fazer detecção de movimento. É uma ferramenta de grande utilidade para quem deseja fazer stream de vídeo, mais precisamente criar uma câmera IP.
date: 2016-01-28 12:29:01
author: alexandrevicenzi
permalink: /camera-ip-com-webcam-e-motion/
image: /assets/wp-content/uploads/2016/01/You-are-being-watched-620-by-338.jpg
categories:
  - Dicas
tags:
  - câmera ip
  - debian
  - ipcam
  - motion
  - web
---

O <a href="http://www.lavrsen.dk/foswiki/bin/view/Motion/WebHome" target="_blank">Motion</a> é um programa que monitora o sinal de câmeras e permite fazer detecção de movimento. É uma ferramenta de grande utilidade para quem deseja fazer streamming de vídeo, mais precisamente criar uma câmera IP.

Escrito em C e disponível para várias distribuições Linux, fazendo uso da interface <em>video4linux</em>, permite a captura de jpeg, ppm e mpeg com um baixo consumo de memória.

As câmeras IPs ganharam grande destaque pela sua facilidade de uso, e preço relativamente acessível. Hoje é simples monitorar a sua casa e enviar imagens para o seu smartphone quando algum movimento for detectado.

<!--more-->

Para uma pequena demonstração de como utilizar o <em>motion</em> para criar uma câmera IP, vamos a lista de materiais e as configurações necessárias.

<strong>Material</strong>
<ul>
	<li>BeagleBone Green / Black ou Raspberry Pi</li>
	<li>Webcam</li>
</ul>
No meu caso irei utilizar a <a href="http://www.filipeflop.com/pd-24c7f0-beaglebone-green.html?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">BeagleBone Green</a> que foi fornecida pela <a href="http://www.filipeflop.com/?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">FILIPEFLOP</a>. Porém este tutorial é válido para várias outras placas, e até PCs.

O primeiro passo é conectar a BBG a rede local e acessá-la via <em>ssh</em>. Por padrão, o usuário <em>ssh</em> é <em>debian</em> e a senha é <em>temppwd</em>. No meu caso a BBG ganhou o IP 192.168.25.6. Sendo assim irei utilizar esse IP ao longo do texto, mas lembre-se de alterar ao efetuar os testes.

<strong>Instalando o Motion</strong>

Após se conectar via <em>ssh</em> com o comando <code>ssh debian@192.168.25.6</code>, vamos instalar as dependências necessárias:

<code>sudo apt-get update</code>
<code>sudo apt-get install motion</code>

<strong>Alterando as configurações padrão</strong>

Como estamos instalando o <em>motion</em> na BeagleBone Green alguns itens devem ser configurados para correto funcionamento. Devemos alterar as portas padrão, pois elas entram em conflito com outras aplicações em execução na BBG. Também devemos liberar o acesso além do localhost, pois a BBG só tem acesso via SSH, diferente de um computador, não vamos estar conectados a uma tela na maioria dos casos.

Sendo assim vamos editar o arquivo de configuração padrão:

<code>sudo vim /etc/motion/motion.conf</code>

Procure pelas configurações abaixo e altere-as:

<pre><code class="bash">
webcam_port 8088
webcam_localhost off
control_port 8089
control_localhost off
</code></pre>

Se você preferir, pode criar um novo arquivo de configuração e carregá-lo passando como parâmetro o argumento <code>-c</code>.

Agora que alteramos as configurações, vamos executar o <em>motion</em> com o comando:

<code>sudo motion</code>

Se tudo ocorrer certo, vários logs serão exibidos no console.

Agora você pode ir no browser do seu computador e digitar a seguinte url: <a href="http://192.168.25.6:8088/">http://192.168.25.6:8088/</a>. O resultado será uma página com a imagem da webcam, como abaixo.

<img class="aligncenter" src="/assets/wp-content/uploads/2016/01/ip-cam-motion.png" alt="Motion IP Cam" />

Se você deseja uma imagem maior, com uma taxa de atualização alta basta alterar as configurações no arquivo <code>motion.conf</code>.

Espero que você tenha gostado. Até mais :)

<em>A imagem de capa faz referência a série <a href="http://www.imdb.com/title/tt1839578/" target="_blank">Person Of Interest</a>, no qual as pessoas são vigiadas 24h por dia pelo governo americano.</em>