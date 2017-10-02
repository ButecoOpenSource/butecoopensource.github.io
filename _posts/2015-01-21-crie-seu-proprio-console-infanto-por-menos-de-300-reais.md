---
layout: wordpress
title: Crie seu próprio console Infanto por menos de 300 reais
date: 2015-01-21 21:00:21
author: alexandrevicenzi
permalink: /crie-seu-proprio-console-infanto-por-menos-de-300-reais/
image: /assets/wp-content/uploads/2015/01/infanto.jpg
categories:
  - Jogos
tags:
  - console
  - games
  - infanto
  - lakka
---

Há cerca de duas semanas, o assunto da vez na área de jogos no Brasil foi o console chamado de Infanto. Se você ainda não ouviu falar nele, você pode ver uma matéria do TecMundo <a href="http://www.tecmundo.com.br/video-game-e-jogos/70903-conheca-infanto-console-brasileiro-obra-pirataria-6-mil-jogos.htm" target="_blank">aqui</a>.

Qual o segredo dele? Nenhum. Isso mesmo, o console é um <a href="http://www.raspberrypi.org/" target="_blank">RaspberryPi</a> com um case rodando uma distribuição Linux com vários emuladores. O que chamou a atenção de todos foi o fato de ele conter mais de 6 mil jogos inclusos, sem pagar direitos autorais aos devidos autores. Isto perante a lei não deixa de ser pirataria.

E o preço? Você terá que desembolsar cerca de 600 reais. Um valor um tanto quanto exagerado tendo em vista que é um Raspberry Pi, que custa apenas 35 dólares, ou no Brasil cerca de 180 reais.

Diante disso, nossa proposta é fornecer um passo a passo de como criar o console Infanto com um preço bem mais em conta.

<em>Nós de forma alguma somos a favor ou incitamos a pirataria. Este tutorial trata apenas de como configurar um console semelhante. Se você está pretendendo conseguir ROMs nesse tutorial, sinto muito informá-lo, mas não o faremos.</em>

Agora que você está por dentro vamos ao que interessa. A montagem de nosso console.

<strong>Software utilizado</strong>

O software que utilizaremos é o <a href="http://www.lakka.tv/" target="_blank">Lakka</a>. O Lakka é uma pequena distribuição Linux baseada no <a href="http://openelec.tv/" target="_blank">OpenELEC</a> e no <a href="http://www.libretro.com/" target="_blank">RetroArch</a>.

Existem outras opções semelhantes ao Lakka, como por exemplo o <a href="https://github.com/petrockblog/RetroPie-Setup" target="_blank">RetroPie</a> e o <a href="https://github.com/ssilverm/PiMAME" target="_blank">PiMAME</a>. Porém o Lakka, diferente desses outros, possibilita que você use um hardware diferente do Raspberry Pi, e isto foi o que me chamou mais a atenção.

<strong>Emuladores suportados</strong>

A lista de emuladores suportados é extensa, porém nem todos emuladores estão disponíveis a todos os hardwares. Isto porque alguns emuladores não conseguem rodar em uma velocidade aceitável em todas as plataformas.

Confira a lista completa de emuladores suportados de acordo com o hardware <a href="http://www.lakka.tv/doc/Hardware-support/#which-systems-are-supported" target="_blank">aqui</a>.

<strong>Hardware suportado</strong>

O hardware necessário é variável, no meu caso eu utilizarei o Banana Pi. Mas você pode escolher entre as seguintes opções:
<ul>
	<li>Raspberry Pi (VideoCore)</li>
	<li>PC</li>
	<li>Cubieboard2, Cubietruck e Banana Pi (A20)(MALI)</li>
	<li>WandBoard, Hummingboard e Cubox-i (i.MX6)(Vivante)</li>
</ul>
Os hardware que possuem GPU MALI são os menos indicados para rodar o Lakka, isto por causa da baixa qualidade dos drivers MALI GLES. Mesmo assim você ainda pode se divertir e jogar bastante.

Confira a descrição completa dos hardwares suportados <a href="www.lakka.tv/doc/Hardware-support/#computers" target="_blank">aqui</a>.

<strong>Controles suportados</strong>

A lista de controles suportados não é muito grande, mas, pelo menos, são controles bem conhecidos que você poderá reutilizar. Neste caso, você pode reaproveitar o seu controle do Xbox 360 ou o do PS3. Controles genéricos tendem a funcionar também, mas não são 100% compatíveis. Se você preferir, você poderá utilizar o seu teclado para jogar.

Confira a lista completa de controles suportados <a href="www.lakka.tv/doc/Hardware-support/#joypads" target="_blank">aqui</a>.

<strong>Preço</strong>

Supondo que você compre um Raspberry Pi (R$ 180,00), um controle de Xbox 360 (R$ 60) e um cartão SD de 16 GB (R$ 40), você provavelmente gastará em torno de 300 reais. Se você pensar bem é um preço razoável a se pagar, mas provavelmente você, assim como eu, deve ter um cartão SD e um controle jogado por aí. Nesse caso necessitaria apenas a compra do Raspberry Pi.

Esses preços foram estimados no Mercado Livre. Se você optar por lojas especializadas, estes valores podem mudar bastante.

<strong>Instalação e configuração</strong>

Você pode instalar o Lakka a partir do Linux, Mac ou Windows. Existem duas versões disponíveis para instalação. A versão <b>Stable</b> é a versão estável da distribuição, que atualmente não está disponível para CPUs AllWinner A20. A versão <b>Nightly</b> é a versão de desenvolvimento, esta possui versão para todas os hardwares suportados.

Apenas para a instalação pelo Windows você necessitará fazer o download do <a href="http://sourceforge.net/projects/win32diskimager/" target="_blank">Win32DiskImager</a>.

Como o Lakka não ocupa muito espaço em disco, você deve dimensionar o seu cartão SD de acordo com o seu uso. Por exemplo, um cartão de 2 GB é mais que suficiente para rodar alguns jogos de GBA.

<strong>Stable</strong>

A versão Stable pode ser encontrada para download <a href="http://www.lakka.tv/get/" target="_blank">aqui</a>. Neste mesmo link está o passo a passo para a instalação em cada Sistema Operacional.

Como o passo a passo está em Inglês eu vou resumi-los aqui:

No Linux e no Mac execute o comando abaixo para copiar o conteúdo do IMG para o SD:
<pre><code>sudo dd if=Lakka-*.img of=/dev/sdX</code></pre>
Lembre-se de desmontar a unidade e substituir <b>sdX</b> pela unidade de destino.

No Linux você pode obter as unidades com o comando:
<pre><code>ls /dev/sd*</code></pre>
No Mac você pode obter as unidades com o comando:
<pre><code>diskutil list</code></pre>
E para desmontar você pode usar:
<pre><code>sudo umount sdX</code></pre>
No Windows execute o aplicativo Win32DiskImager, selecione a imagem do Lakka e a unidade desejada e clique em Write.

<strong>Nightly</strong>

A versão Nightly pode ser encontrada para download <a href="http://sources.lakka.tv/nightly/" target="_blank">aqui</a>.

Existem duas opções de instalação do Nightly. A primeira e mais simples é utilizando o arquivo TAR. A segunda é utilizando o arquivo IMG. Se você optar pelo arquivo IMG você deve seguir os passos descritos no passo Stable. Se você estiver no Windows escolha o arquivo IMG.

Se você escolheu o arquivo TAR basta extrair o arquivo e executar o seguinte comando, note que você deverá estar na pasta onde os arquivos foram extraídos:
<pre><code>sudo ./create_sdcard /dev/sdX</code></pre>
<strong>Pós instalação</strong>

No meu caso, como eu uso a porta HDMI eu fiz uma pequena alteração no arquivo <em>uEnv.txt</em>. Confira abaixo:
<pre><code>fexfile=script.bin
kernel=KERNEL
extraargs='console=ttyS0,115200 console=tty0 boot=/dev/mmcblk0p1 disk=/dev/mmcblk0p2 rootwait quiet ssh loglevel=2 hdmi.audio=EDID:0 disp.screen0_output_mode=<b>3:1360x768p60</b> consoleblank=0'
boot_mmc=fatload mmc 0 0x43000000 ${fexfile}; fatload mmc 0 0x48000000 ${kernel}; bootm 0x48000000</code></pre>
Geralmente isto não é necessário, dependerá do hardware que você estiver utilizando e da saída de vídeo.

Se você possuir dúvidas sobre este arquivo, confira <a href="/2014/12/10/primeiros-passos-com-o-banana-pi/" target="_blank">este</a> tutorial.

Após copiar a imagem para o SD é necessário que seja efetuado um primeiro boot no Lakka, isto para que ele possa expandir o seu sistema de arquivos e criar toda a estrutura necessária. Após isto, você pode copiar os jogos para a pasta <em>rom</em>.

<strong>Execução</strong>

Agora que você já possui o Lakka instalado e rodando vamos nos preparar para jogar. Primeiro conecte os controles ou o teclado e após isto de o boot.

Confira abaixo o vídeo da execução.

<iframe src="//www.youtube.com/embed/bnJQa1J_v5s" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

Se você possuir algum problema durante a instalação ou execução, você pode deixar um comentário nesta publicação ou consultar o <a href="http://www.lakka.tv/doc/FAQ/" target="_blank">FAQ</a> do Lakka.

Espero que você tenha gostado desta publicação e faça uso responsável. Não deixe de assinar o nosso feed de notícias para saber mais novidades sobre o Lakka.