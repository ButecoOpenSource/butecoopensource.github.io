---
layout: wordpress
title: Instalando driver NVIDIA Bumblebee no openSUSE
excerpt: |
  A tecnologia Optimus da NVIDIA otimiza o seu notebook de forma inteligente, oferecendo o desempenho gráfico impressionante que você precisa, quando você precisa, e sempre aumentando o tempo de vida da bateria para que você aproveite por mais tempo.
date: 2015-02-23 00:59:15
author: alexandrevicenzi
permalink: /instalando-driver-nvidia-bumblebee-no-opensuse/
image: /assets/wp-content/uploads/2015/02/bumblebee_250.png
categories:
  - Dicas
tags:
  - bbswitch
  - bumblebee
  - linux
  - nouveau
  - nvidia
  - optimus
---

Eu, como muitos de vocês, gosto de jogar um pouquinho as vezes. E porque não tirar todo o potencial da sua placa de vídeo no Linux?

Pois bem, hoje vou mostrar como resolver um problema em particular com as placas de vídeo da NVIDIA que possuem a tecnologia Optimus.

<strong>Para quem este tutorial é indicado?</strong>

Para todos usuários do openSUSE ou semelhante que possuam um notebook com tecnologia <a href="http://www.nvidia.com.br/object/optimus_technology_br.html" target="_blank">NVIDIA Optimus</a>.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/02/optimus_technology_badge.jpg" alt="Optimus Technology Badge" />

<strong>O que é NVIDIA Optimus?</strong>

A tecnologia Optimus da NVIDIA otimiza o seu notebook de forma inteligente, oferecendo o desempenho gráfico impressionante que você precisa, quando você precisa, e sempre aumentando o tempo de vida da bateria para que você aproveite por mais tempo.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/02/optimus-chart.jpg" alt="Optimus Chart" />

Resumidamente, a tecnologia NVIDIA Optimus escolhe qual a melhor placa gráfica para executar determinada aplicação. Para processos de pouco uso gráfico, será escolhido a Intel Graphics e para processos de alto desempenho, como jogos por exemplo, será escolhida a NVIDIA GeForce.

<strong>Qual a necessidade do Bumblebee?</strong>

Com o driver oficial da NVIDIA no Windows 7 ou superior, a troca entre as placas de vídeo é automática, porém o driver oficial da NVIDIA para Linux não funciona corretamente com a tecnologia Optimus. Sendo assim, é necessário o uso do Bumblebee para fazer essa troca.

<strong>O que é o Projeto Bumblebee?</strong>

O <a href="http://bumblebee-project.org/" target="_blank">Projeto Bumblebee</a> é uma coleção de ferramentas para dar suporte a tecnologia Optimus no Linux, sendo responsável pelo gerenciamento das placas de vídeo.

<strong>O que é o bbswitch?</strong>

O bbswitch é responsável por fazer o "Liga/Desliga" das placas de vídeo.

Agora que conhecemos um pouco sobre a história do Bumblebee, vamos ver como instalá-lo e configurá-lo.

<strong>Preparação</strong>

Todos os passos da instalação foram obtidos na <a href="https://en.opensuse.org/SDB:NVIDIA_Bumblebee" target="_blank">Wiki</a> do openSUSE.

Primeiramente criaremos um Snapshot do sistema, para que seja possível restaurar o sistema caso de algum problema. Para isto execute o comando abaixo:

<code>snapper create -d BeforeBB</code>

Isto só vale para quem possui sistema de arquivos BtrFS ou Ext4.

Antes de baixar os drivers necessários é preciso adicionar o repositório do Bumblebee. Para isto execute o comando abaixo:

<code>zypper ar -f http://download.opensuse.org/repositories/X11:/Bumblebee/openSUSE_13.2/ Bumblebee</code>

Lembre-se de substituir o <strong>13.2</strong> pela sua versão.

<strong>Instalação</strong>

Para instalar o Bumblebee execute o comando abaixo:

<code>zypper in bumblebee</code>

Adicione seu usuário ao grupo do Bumblebee com o seguinte comando:

<code>usermod -G video,bumblebee seu_usuário</code>

Habilite o bbswitch e o dkms com o comando abaixo:

<code>systemctl enable bumblebeed</code>

Edite o arquivo <em>/etc/modprobe.d/50-blacklist.conf</em> e verifique se consta a seguinte linha:

<code># NVIDIA Bumblebee
blacklist nouveau
</code>

Caso não, adicione-a.

Execute o comando abaixo para recriar o <em>initrd</em> com as novas informações adicionadas:

<code>mkinitrd</code>

Para usar todos os recursos da sua placa NVIDIA é necessário instalar o driver da NVIDIA. Para isto execute:

<code>zypper in nvidia-bumblebee</code>

Habilite o dkms com o seguinte comando:

<code>systemctl enable dkms</code>

Caso você esteja em um sistema 64 bits, é necessário instalar o driver 32 bits para execução de aplicações 32 bits. Para isto execute o seguinte comando:

<code>zypper in nvidia-bumblebee-32bit</code>

Após tudo instalado reinicie o computador.

<strong>Teste</strong>

Após reiniciar você pode testar a sua placa NVIDIA para verificar se tudo ocorreu bem. Para isto execute o comando abaixo:

<code>optirun --status</code>

O resultado deverá ser:

<code>Bumblebee status: Ready (3.2.1). X inactive. Discrete video card is off.</code>

<strong>Executando aplicações</strong>

Para executar uma aplicação utilizando a placa NVIDIA é necessário iniciar esta aplicação pela linha de comando com o comando <em>optirun</em> ou <em>primusrun</em>.

Como por exemplo:

<code>optirun glxspheres</code>

Se você ver o resultado abaixo significa que tudo está funcionado.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/02/glx.png" alt="glxspheres" />

Sendo assim, quando você deseja usar a sua placa NVIDIA basta executar os programas pelo <em>optirun</em> ou <em>primusrun</em>.

Agora se você, assim como eu, teve o problema abaixo, é necessário alguns passos adicionais para colocar o Bumblebee para funcionar.

<code>[ 141.907657] [ERROR]Cannot access secondary GPU - error: Could not load GPU driver
[ 141.907718] [ERROR]Aborting because fallback start is disabled.</code>

Se você executar o comando abaixo você conseguirá ver um log mais detalhado:

<code>optirun -vvv glxspheres</code>

O resultado deverá ser algo semelhante:

<code>[ 632.489659] [DEBUG]Reading file: /etc/bumblebee/bumblebee.conf
[ 632.490367] [DEBUG]optirun version 3.2.1 starting...
[ 632.490384] [DEBUG]Active configuration:
[ 632.490389] [DEBUG] bumblebeed config file: /etc/bumblebee/bumblebee.conf
[ 632.490394] [DEBUG] X display: :8
[ 632.490398] [DEBUG] LD_LIBRARY_PATH: /usr/lib64/nvidia:/usr/lib/nvidia
[ 632.490402] [DEBUG] Socket path: /var/run/bumblebee.socket
[ 632.490406] [DEBUG] Accel/display bridge: auto
[ 632.490411] [DEBUG] VGL Compression: proxy
[ 632.490415] [DEBUG] VGLrun extra options:
[ 632.490419] [DEBUG] Primus LD Path: /usr/lib64/primus:/usr/lib/primus
[ 632.490459] [DEBUG]Using auto-detected bridge virtualgl
[ 632.535663] [INFO]Response: No - error: Could not load GPU driver</code>

[ 632.535686] [ERROR]Cannot access secondary GPU - error: Could not load GPU driver

[ 632.535694] [DEBUG]Socket closed.
[ 632.535713] [ERROR]Aborting because fallback start is disabled.
[ 632.535721] [DEBUG]Killing all remaining processes.

Resumidamente este erro indica que o Bumblebee não conseguiu trocar para a placa NVIDIA.

<strong>Resolução de problemas</strong>

Primeiro vamos alterar o arquivo <em>/etc/bumblebee/bumblebee.conf</em>.

Altera apenas as linhas <em>Driver</em> e <em>KernelDriver</em> para ficar como abaixo:

<pre><code class="bash">
# Configuration file for Bumblebee. Values should **not** be put between quotes

## Server options. Any change made in this section will need a server restart
# to take effect.
[bumblebeed]
# The secondary Xorg server DISPLAY number
VirtualDisplay=:8
# Should the unused Xorg server be kept running? Set this to true if waiting
# for X to be ready is too long and don't need power management at all.
KeepUnusedXServer=false
# The name of the Bumbleblee server group name (GID name)
ServerGroup=bumblebee
# Card power state at exit. Set to false if the card shoud be ON when Bumblebee
# server exits.
TurnCardOffAtExit=false
# The default behavior of '-f' option on optirun. If set to &quot;true&quot;, '-f' will
# be ignored.
NoEcoModeOverride=false
# The Driver used by Bumblebee server. If this value is not set (or empty),
# auto-detection is performed. The available drivers are nvidia and nouveau
# (See also the driver-specific sections below)
Driver=nvidia
# Directory with a dummy config file to pass as a -configdir to secondary X
XorgConfDir=/etc/bumblebee/xorg.conf.d

## Client options. Will take effect on the next optirun executed.
[optirun]
# Acceleration/ rendering bridge, possible values are auto, virtualgl and
# primus.
Bridge=auto
# The method used for VirtualGL to transport frames between X servers.
# Possible values are proxy, jpeg, rgb, xv and yuv.
VGLTransport=proxy
# List of paths which are searched for the primus libGL.so.1 when using
# the primus bridge
PrimusLibraryPath=/usr/lib64/primus:/usr/lib/primus
# Should the program run under optirun even if Bumblebee server or nvidia card
# is not available?
AllowFallbackToIGC=false

# Driver-specific settings are grouped under [driver-NAME]. The sections are
# parsed if the Driver setting in [bumblebeed] is set to NAME (or if auto-
# detection resolves to NAME).
# PMMethod: method to use for saving power by disabling the nvidia card, valid
# values are: auto - automatically detect which PM method to use
#         bbswitch - new in BB 3, recommended if available
#       switcheroo - vga_switcheroo method, use at your own risk
#             none - disable PM completely
# https://github.com/Bumblebee-Project/Bumblebee/wiki/Comparison-of-PM-methods

## Section with nvidia driver specific options, only parsed if Driver=nvidia
[driver-nvidia]
# Module name to load, defaults to Driver if empty or unset
KernelDriver=nvidia
PMMethod=auto
# colon-separated path to the nvidia libraries
LibraryPath=/usr/lib64/nvidia:/usr/lib/nvidia:/lib/modules/3.16.7-7-desktop/updates/:/usr/lib64/
# comma-separated path of the directory containing nvidia_drv.so and the
# default Xorg modules path
XorgModulePath=/usr/lib64/nvidia/xorg/,/usr/lib64/xorg/modules,/usr/lib64/xorg/modules/drivers/
XorgConfFile=/etc/bumblebee/xorg.conf.nvidia

## Section with nouveau driver specific options, only parsed if Driver=nouveau
[driver-nouveau]
KernelDriver=nouveau
PMMethod=auto
XorgConfFile=/etc/bumblebee/xorg.conf.nouveau
</code></pre>

Altere o arquivo <em>/etc/modprobe.d/50-bbswitch.conf</em> para ficar igual o abaixo:

<code>options bbswitch load_state=1 unload_state=1</code>

Mudando o <em>load_state</em> para 1, estamos dizendo que o driver sempre será carregado no boot.

Execute o comando abaixo para recriar o <em>initrd</em> com as novas informações adicionadas:

<code>mkinitrd</code>

Reinicie o computador novamente.

Faça o teste com o <em>glxspheres</em> como mencionado anteriormente e verifique se o resultado foi positivo.

É isso ai. Espero que este tutorial possa ajudar outras pessoas. Foram alguns dias tentando solucionar este problema. Eu não teria conseguido se não fosse <a href="https://forums.opensuse.org/showthread.php/504717-Two-mouse-pointers-on-screen/page4" target="_blank">pela ajuda do pessoal do fórum do openSUSE</a>.