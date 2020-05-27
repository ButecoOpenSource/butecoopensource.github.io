---
layout: wordpress
title: Primeiros passos com o Banana Pi
date: 2014-12-10 22:35:12
author: alexandrevicenzi
permalink: /primeiros-passos-com-o-banana-pi/
categories:
  - Desenvolvimento
  - Hardware / DIY
tags:
  - banana-pi
---

Na <a href="/rodando-linux-em-uma-banana">primeira postagem sobre o Banana Pi</a> eu comentei sobre o <em>hardware</em> e se seria uma boa opção de compra. Pois bem, nesta postagem irei comentar como colocar o BPi para funcionar, caso você já possua um ou está pensando em adquiri-lo.

<em>Todos os exemplos são baseados no Linux, se você usa outro sistema operacional veja as instruções <a href="http://www.lemaker.org/resources/9-39/banana_pi_quick_start_guide.html">aqui</a>.</em>

<strong>Copiando a imagem para o SD</strong>

<img class="aligncenter" src="/assets/wp-content/uploads/2014/12/sd_banana.png" alt="" width="40%" height="40%" />

O primeiro passo é copiar uma imagem de algum sistema operacional disponível para o BPi. Atualmente o BPi possui as seguintes imagens:
<ul>
	<li>Lubuntu</li>
	<li>Raspbian</li>
	<li>Android</li>
	<li>Bananian</li>
	<li>Berryboot</li>
	<li>LeMedia (XBMC)</li>
	<li>OpenSuse</li>
	<li>Fedora</li>
	<li>Gentoo</li>
	<li>Scratch</li>
	<li>ArchLinux</li>
	<li>Open Media Vault</li>
	<li>OpenWrt</li>
</ul>
Você pode fazer o download das imagens <a href="http://www.lemaker.org/resources/9-38/image_files.html">aqui</a>.

<strong>Nota:</strong> A maioria das imagens não possui um link direto, nesse caso o servidor que se mostrou melhor foi o do OneDrive.

Após o download você deverá ter uma imagem com a extensão <em>img</em>. Caso o arquivo esteja comprimido descompacte-o antes.

Certifique-se de possuir um SD conectado e que seja de no mínimo 4 GB. O tamanho do SD irá variar de acordo com o tamanho da imagem.

Agora que você já possui tudo pronto, vamos aos comandos para copiar a imagem para o SD.

Listando as unidades de disco:
<pre><code>ls /dev/sd*</code></pre>
Identifique o seu SD, provavelmente será sdb e sdb1. Para fins de exemplo vou utilizar o sdb/sdb1 como minha unidade de disco. Caso a sua seja outra modifique o script abaixo.

O próximo passo é desmontar a unidade.
<pre><code>umount /dev/sdb1</code></pre>
Agora que a unidade está desmontada vamos copiar a imagem para o SD (Note que todos os dados e partições do SD serão perdidos).

Vou usar o comando <a href="http://linux.die.net/man/1/dd">dd</a> com o <em>bs</em> de 1M. Se você utilizar um valor maior e tiver problemas, tente reduzir um pouco. No <em>if</em> você informa o arquivo de origem, no caso o seu arquivo <em>img</em>, e no <em>of</em>, você informa a sua unidade de destino, no caso o cartão SD.
<pre><code>sudo dd bs=1M if=sua_imagem.img of=/dev/sdb &amp;&amp; sync</code></pre>
Dependendo da imagem e do <em>bs</em> escolhido a cópia poderá demorar alguns minutos, então não se preocupe se demorar um pouco.

Pronto, agora você já pode conectar o SD no seu BPi e sair usando-o, ou não. Isso mesmo, se você está utilizando um conversor HDMI para VGA ou a conexão vídeo componente,  as suas chances de rodar o BPi de primeira são poucas. Agora, se você está usando um cabo HDMI ligado à uma TV/Monitor HDMI, a imagem deverá funcionar, pois por padrão o HDMI é o dispositivo de saída de vídeo. Em alguns casos a imagem consegue identificar que o HDMI não está conectado e então a imagem é enviada para o vídeo componente, mas no meu caso eu não consegui isso sem fazer umas pequenas alterações nas imagens. Portanto, se você possuir o mesmo problema que eu,  continue seguindo as instruções abaixo.

<strong id="binfex">Baixando os arquivos necessários</strong>

Se você pretende alterar o arquivo <em>script.bin</em> você terá que fazer o download do <a href="http://sunxi.org/Sunxi-tools">Sunxi-tools</a> para convertê-lo de <em>bin</em> para <em>fex</em>. Você pode fazer o download <a href="https://github.com/linux-sunxi/sunxi-tools/archive/master.zip">aqui</a>.

Após ter feito o download descompacte o arquivo. Após descompacta-lo será necessário compilar o projeto. Execute as seguintes linhas de comando no diretório onde estão os arquivos baixados:
<pre><code>make bin2fex
make fex2bin</code></pre>
Como o nome sugere, o arquivo <em>bin</em> é binário, e não é possível alterá-lo por um editor de texto. Após convertê-lo para <em>fex</em> é possível editá-lo normalmente.

Procure no SD card pelo arquivo <em>script.bin</em>

Para converter de <em>bin</em> para <em>fex</em> utilize o comando:
<pre><code>./bin2fex script.bin&gt;script.fex</code></pre>
E para converter de <em>fex</em> para <em>bin</em> utilize o comando:
<pre><code>./fex2bin script.fex&gt;script.bin</code></pre>
Após convertido, substitua o arquivo do SD card pelo novo arquivo <em>script.bin</em>

<strong>Alterando a imagem para reconhecer HDMI</strong>

Caso o seu BPi não reconheça o seu cabo HDMI ou o conversor HDMI para VGA siga os passos abaixo.

Procure no SD card pelo arquivo <em>config.txt</em>. Este é o arquivo de configurações, como se fosse uma <em>BIOS</em>. Após achar o arquivo abra-o com o seu editor preferido e procure pelas seguintes linhas e descomente-as, caso elas não existam basta adicioná-las.
<pre><code>hdmi_force_hotplug=1</code></pre>
Irá usar o modo HDMI, mesmo que nenhum cabo seja detectado.
<pre><code>hdmi_safe=1</code></pre>
Use o <em>safe mode</em> para conseguir a melhor compatibilidade. Isto equivale a:
<pre><code>hdmi_force_hotplug=1
hdmi_ignore_edid=0xa5000080
config_hdmi_boost=4
hdmi_group=2
hdmi_mode=4
disable_overscan=0
overscan_left=24
overscan_right=24
overscan_top=24
overscan_bottom=24</code></pre>
Caso você tenha dúvidas sobre o arquivo <em>config.txt</em>, clique <a href="http://elinux.org/RPiconfig">aqui</a> para ver a documentação.

Se após isso ainda não funcionar, você pode editar o arquivo <em>script.bin</em>. Utilize <a href="#binfex">os passos descritos acima</a> para obter o arquivo <em>fex</em>. Após obtido o arquivo, abra-o com seu editor de texto e procure por <em>[disp_init]</em>, ao encontrar altere as seguintes linhas para:

Habilitado
<pre><code>disp_init_enable = 1</code></pre>
Screen 0
<pre><code>disp_mode = 0</code></pre>
HDMI
<pre><code>screen0_output_type = 3</code></pre>
480p
<pre><code>screen0_output_mode = 2</code></pre>
TV
<pre><code>screen1_output_type = 2</code></pre>
NTSC
<pre><code>screen1_output_mode = 14</code></pre>
Verifique <a href="http://linux-sunxi.org/Fex_Guide#.5Bdisp_init.5D">aqui</a> quais os valores para o <em>screen0_output_mode / screen1_output_mode</em>.

<strong>Alterando a imagem para reconhecer Video Componente</strong>

Caso o seu BPi não envie a imagem via Vídeo Componente siga os passos abaixo.

Procure no SD card pelo arquivo <em>config.txt</em>. Este é o arquivo de configurações, como se fosse uma <em>BIOS</em>. Após achar o arquivo abra-o com o seu editor preferido e procure pela seguinte linha e descomente-a, caso ela não existam basta adicioná-la.
<pre><code>sdtv_mode=0 NTSC
sdtv_mode=1 NTSC Japonês
sdtv_mode=2 PAL
sdtv_mode=3 PAL Brasileiro</code></pre>
Escolha o valor de acordo com a sua TV/Monitor. Note que para o vídeo componente funcionar você não pode estar com o cabo HDMI conectado.

Certifique-se de que as linhas abaixo não existam, ou estejam comentadas ou com o valor 0. Para comentar basta colocar # no início da linha.
<pre><code>hdmi_force_hotplug=1</code></pre>
<pre><code>hdmi_safe=1</code></pre>
Caso você tenha dúvidas sobre o arquivo <em>config.txt</em>, clique <a href="http://elinux.org/RPiconfig">aqui</a> para ver a documentação.

Se após isso ainda não funcionar, você pode editar o arquivo <em>script.bin</em>. Utilize <a href="#binfex">os passos descritos acima</a> para obter o arquivo <em>fex</em>. Após obtido o arquivo, abra-o com seu editor de texto e procure por <em>[disp_init]</em>, ao encontrar altere as seguintes linhas para:

Habilitado
<pre><code>disp_init_enable = 1</code></pre>
Screen 0
<pre><code>disp_mode = 0</code></pre>
TV
<pre><code>screen0_output_type = 2</code></pre>
NTSC
<pre><code>screen0_output_mode = 14</code></pre>
HDMI
<pre><code>screen1_output_type = 3</code></pre>
480p
<pre><code>screen1_output_mode = 2</code></pre>
Verifique <a href="http://linux-sunxi.org/Fex_Guide#.5Bdisp_init.5D">aqui</a> quais os valores para o <em>screen0_output_mode / screen1_output_mode</em>.

Se depois destas alterações todas você ainda não conseguir vídeo nenhum, mas a luz vermelha da placa está acesa e a verde está piscando, só resta ver se o problema não pode ser o cabo. Caso essas luzes não estejam conforme mencionado pode ser que o problema está no SD ou na imagem gravada. Para todos os casos você pode tirar suas dúvidas no <a href="http://forum.lemaker.org/forum.php">fórum do BPi</a>.

Essas foram algumas das dificuldades que tive e como consegui resolve-las. Espero que este post possa ser útil para você também. :)
