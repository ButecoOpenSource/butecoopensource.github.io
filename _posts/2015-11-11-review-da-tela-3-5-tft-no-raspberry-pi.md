---
layout: wordpress
title: Review da tela 3.5 TFT no Raspberry Pi!
date: 2015-11-11 12:43:20
author: marcossouza
permalink: /review-da-tela-3-5-tft-no-raspberry-pi/
image: /assets/wp-content/uploads/2015/05/index.png
categories:
  - Hardware / DIY
tags:
  - display
  - hardware
  - raspberrypi
  - tft
---

Olá pessoal, neste artigo iremos mostrar como instalar a tela TFT 3.5", com suporte a caneta, no Raspberry Pi. Utilizaremos a distro Raspbian Wheezy, baseada no Debian e indicada pela Raspberry Foundation, e um Raspberry Pi modelo B. Se você deseja instalar a tela em outra distribuição, basta verificar quais arquivos de configuração se equiparam aos utilizados no Raspbian.

Após instalação da tela, será feito um review falando de sua qualidade e se de fato vale comprar tal acessório.

<!--more-->

O Display LCD TFT Touch 3.5" do Raspberry Pi foi fornecido pela <a href="http://www.filipeflop.com/?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">FilipeFlop</a> e você pode <a href="http://www.filipeflop.com/pd-24ca21-display-lcd-tft-touch-3-5-raspberry-pi.html?utm_source=Blog&amp;utm_medium=Banner&amp;utm_campaign=ButecoOpenSource" target="_blank">comprá-lo aqui</a>.

A imagem abaixo mostra um Raspberry Pi B com a tela já instalada, porém não configurada:

<a href="/assets/wp-content/uploads/2015/10/20151030_073103.jpg"><img class="alignnone size-full wp-image-3941" src="/assets/wp-content/uploads/2015/10/20151030_073103.jpg" alt="20151030_073103" width="2560" height="1920" /></a>

Para configurar o dispositivo teremos de instalar alguns pacotes, e configurar alguns arquivos, mas nada complicado. Para a configuração destes arquivos no Raspberry, utilizarei o nano, pois já vem pré instalado no Raspbian, mas se você tem mais intimidade com o VIM, pode utilizá-lo sem problemas, após instalar.

Para iniciar o tutorial, você pode utilizar o cabo HDMI em uma TV e utilizar a interface gráfica do Raspbian, ou então acessar o dispositivo por SSH, se este tiver um cabo de rede plugado nele. Para descobrir o IP do seu Raspberry, basta executar o comando <code>arp-scan</code> de uma máquina que está na mesma rede:

<pre><code class="bash">
sudo arp-scan --localnet
</code></pre>

Uma informação semelhante a esta deverá ser mostrada:

<pre><code class="bash">
192.168.1.18	b8:27:eb:fc:bd:c3	Raspberry Pi Foundation
</code></pre>

Então basta conectar no IP com SSH, sendo o que o usuário é <strong>pi</strong> e a senha é <strong>raspberry</strong>:

<pre><code class="bash">
ssh pi@&amp;amp;amp;lt;ip do seu rasp&amp;amp;amp;gt;
</code></pre>

Antes de começar, encaixe a tela nos pinos GPIO do Raspberry da seguinte forma:
<a href="/assets/wp-content/uploads/2015/10/20151030_200533.jpg"><img class="alignnone size-full wp-image-3955" src="/assets/wp-content/uploads/2015/10/20151030_200533.jpg" alt="20151030_200533" width="2560" height="1920" /></a>

Primeiramente, vamos atualizar o Raspbian:

<pre><code class="bash">
sudo apt-get update; sudo apt-get upgrade -y
</code></pre>

Após o fim do comando, reinicie o dispositivo:

<pre><code class="bash">
sudo reboot
</code></pre>

Depois do reboot, edite o arquivo /boot/config.txt:

<pre><code class="bash">
sudo nano /boot/config.txt
</code></pre>

e então adicionar a seguinte linha no fim do arquivo:

<pre><code class="bash">
dtoverlay=piscreen,speed=16000000,rotate=90
</code></pre>

O próximo passo será redirecionar o <em>framebuffer</em>, responsável por mostrar a imagem na tela do dispositivo, e fazer a calibração da tela para utilização da caneta. Primeiro, vamos editar o arquivo para desabilitar o <em>framebuffer</em> do HDMI:

<pre><code class="bash">
sudo nano /usr/share/X11/xorg.conf.d/99-fbturbo.conf
</code></pre>

Dentro do arquivo encontre a linha <strong>Option “fbdev” “/dev/fb0″</strong> e comente o comando colocando um <strong>#</strong> no inicio da linha, que deverá ficar assim: <strong>#Option “fbdev” “/dev/fb0″</strong>

Antes de compilar/instalar o calibrador, precisamos primeiro baixar as suas dependências. Para fazer o download das dependências dos repositórios do Raspbian, basta executar o comando abaixo:

<pre><code class="bash">
sudo apt-get install libtool libx11-dev xinput autoconf libx11-dev libxi-dev x11proto-input-dev -y
</code></pre>

Com as dependências instaladas, podemos então baixar o código do calibrador com o git, compilar e instala-lo:

<pre><code class="bash">
cd
git clone https://github.com/tias/xinput_calibrator
cd xinput_calibrator/
./autogen.sh
make
sudo make install
</code></pre>

Com o software instalado, vamos agora ao <em>script</em> de calibração:

<pre><code class="bash">
cd
wget http://ozzmaker.com/piscreen/xinput_calibrator_pointercal.sh
sudo mv ~/xinput_calibrator_pointercal.sh /etc/X11/Xsession.d/xinput_calibrator_pointercal.sh
</code></pre>

Os comandos acima irão baixar o <em>script</em> de calibração e copiá-lo para o diretório onde será chamado pelo <em>autostart</em> do Raspbian. Para alterar o <em>autostart</em>, edite o arquivo:

<pre><code class="bash">
sudo nano /etc/xdg/lxsession/LXDE-pi/autostart
</code></pre>

e adicione a linha abaixo no final do arquivo:

<pre><code class="bash">
sudo /bin/sh /etc/X11/Xsession.d/xinput_calibrator_pointercal.sh
</code></pre>

Neste ponto, você já pode testar o <em>display</em> com o comando abaixo:

<pre><code class="bash">
FRAMEBUFFER=/dev/fb1 startx
</code></pre>

O comando acima reinicia o <em>Window Manager</em>, mas agora trocando o <em>framebuffer</em> para o <em>display</em>. Após alguns segundos a imagem que estava no seu HDMI agora aparece no <em>display</em>:
<a href="/assets/wp-content/uploads/2015/10/20151030_200332.jpg"><img class="alignnone size-full wp-image-3967" src="/assets/wp-content/uploads/2015/10/20151030_200332.jpg" alt="20151030_200332" width="2560" height="1920" /></a>

Para fazer com que o <em>display</em> seja carregado ao ligar o Raspberry são necessários algumas outras alterações. Primeiro vamos alterar o inittab:

<pre><code class="bash">
sudo nano /etc/inittab
</code></pre>

Comente a linha <strong>1:2345:respawn:/sbin/getty --noclear 38400 tty1</strong>, adicionando um <strong>#</strong> na frente da linha, e adicione outra linha, conforme abaixo:

<pre><code class="bash">
#1:2345:respawn:/sbin/getty --noclear 38400 tty1
1:2345:respawn:/bin/login -f pi tty1 /dev/tty1 2&amp;amp;amp;gt;&amp;amp;amp;amp;1
</code></pre>

Agora vamos editar o arquivo <strong>/etc/rc.local</strong> e adicionar a linha que inicia o <em>startx</em> com o <em>framebuffer</em> do <em>display</em>. O arquivo ficará como abaixo:

<pre><code class="bash">
#
# By default this script does nothing.

# Print the IP address
_IP=$(hostname -I) || true
if [ &quot;$_IP&quot; ]; then
  printf &quot;My IP address is %sn&quot; &quot;$_IP&quot;
fi
su -l pi -c “env FRAMEBUFFER=/dev/fb1 startx &amp;amp;amp;amp;”
exit 0
</code></pre>

Agora basta reiniciar o dispositivo novamente com o comando:

<pre><code class="bash">
sudo reboot
</code></pre>

Após reiniciado, você verá a tela de calibração. Estando calibrado, ele abre a tela do Raspbian na tela:
<a href="/assets/wp-content/uploads/2015/10/20151110_000803.jpg"><img class="alignnone size-full wp-image-4046" src="/assets/wp-content/uploads/2015/10/20151110_000803.jpg" alt="20151110_000803" width="2560" height="1920" /></a>

Para utilizar o seu Raspbian com a caneta, você pode instalar um teclado virtual:

<pre><code class="bash">
sudo apt-get install matchbox-keyboard
</code></pre>

E para acessar o teclado, basta ir em Menu/Acessórios/Keyboard.

&nbsp;

<strong>Review</strong>

Após fazer a calibragem inicial, pode-se notar que a tela funciona muito bem. Não é preciso muita força no "clique" para acessar os menus do Raspbian por exemplo. A tela funciona tanto com o dedo como com a caneta que vem com ela. Se você deseja fazer algum produto com o Raspberry, ou apenas gosta, não precisa de uma TV nele, esta tela é uma boa pedida. Mas, se você só usa o Raspberry para jogar emuladores, ou até como um desktop, então a tela não será muito uso para você.

Espero que todos tenham gostado! Esse tipo de <em>gadget</em> é bem interessante, pois nos permite ver aplicações diferentes de placas do estilo da Raspberry e aplicações diferentes daquelas que estamos acostumados. Não esqueça de se inscrever nas nossas redes sociais para ficar por dentro dos próximos posts!

Até mais!