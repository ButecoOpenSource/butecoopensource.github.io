---
layout: wordpress
title: Instalando ArchLinux + XFCE + LXDM no Banana Pi
date: 2014-12-23 08:00:05
author: alexandrevicenzi
permalink: /instalando-archlinux-xfce-lxdm-no-banana-pi/
image: /assets/wp-content/uploads/2014/12/ArchlinuxLogo2.png
categories:
  - Desenvolvimento
tags:
  - archlinux
  - banana-pi
  - lxdm
  - xfce
---

Hoje vou mostrar como instalar o <a href="http://www.archlinux-br.org/" target="_blank">ArchLinux</a> no BananaPi. Escolhi o ArchLinux por ele ser uma distribuição bem enxuta, mas muito poderosa. Outro motivo que me leva a usá-lo é o fato de que pretendo fazer testes com o <a href="https://wiki.archlinux.org/index.php/RetroArch" target="_blank">RetroArch</a>.

<strong>Instalando o ArchLinux</strong>

Faça o download da <a href="http://www.lemaker.org/resources/9-96/archlinux_for_bananapi.html" target="_blank">imagem do ArchLinux</a>.

Para passar a imagem para o SD faça o seguinte:

<pre><code>sudo dd bs=8M if=sua_imagem.img of=/dev/sdb &amp;&amp; sync</code></pre>

No meu caso, como estou usando saída HDMI apenas fiz o seguinte ajuste (em negrito) no arquivo <em>uEnv.txt</em>:

<pre><code>bootargs=console=ttyS0,115200 console=tty0 disp.screen0_output_mode=<strong>3</strong>:<strong>1360x768p50</strong> hdmi.audio=EDID:0 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4</code></pre>

Caso você possua dúvidas sobre como configurar as saídas de vídeo siga <a href="/primeiros-passos-com-o-banana-pi" target="_blank">este tutorial</a>.

<strong>Acessando o ArchLinux</strong>

Você pode acessar diretamente ou via SSH. Para acessar via SSH basta você conectá-lo a rede. Para conectar no BPi via SSH execute o comando abaixo:

<pre><code>ssh [usuário]@[ip]</code></pre>

Exemplo:

<pre><code>ssh root@10.1.1.6</code></pre>

Os usuários de acesso padrão são:

<table>
    <tbody>
        <tr>
            <th>Tipo</th>
            <th>Login</th>
            <th>Senha</th>
        </tr>
        <tr>
            <td>Root</td>
            <td>root</td>
            <td>bananapi</td>
        </tr>
        <tr>
            <td>Usuário</td>
            <td>bananapi</td>
            <td>bananapi</td>
        </tr>
    </tbody>
</table>

<strong>Atualizando o ArchLinux</strong>

Após instalar o ArchLinux vamos verificar se existem novas atualizações. Para isto, execute o comando abaixo:

<pre><code>pacman -Syu</code></pre>

Se possuir atualizações, instale-as.

<strong>Instalando as dependências</strong>

Agora que ele está atualizado, vamos instalar todas as dependências necessárias.

Instalando o driver X.org para o BPi:

<pre><code>pacman -S xf86-video-fbdev</code></pre>

Instalando o <a href="https://wiki.archlinux.org/index.php/xfce" target="_blank">XFCE</a> como área de trabalho:

<pre><code>pacman -S xfce4</code></pre>

Instalando alguns pacotes adicionais, contendo plugins, para o XFCE (não obrigatório):

<pre><code>pacman -S xfce4-goodies</code></pre>

Instalando o <a href="https://wiki.archlinux.org/index.php/LXDM" target="_blank">LXDM</a> como gerenciador de área de trabalho:

<pre><code>pacman -S lxdm</code></pre>

<strong>Configurando o XFCE e o LXDM</strong>

Agora que temos o XFCE e o LXDM instalados, vamos configurá-los.

Para que ao iniciar o <em>startx</em> ele inicie o XFCE devemos fazer alguns ajustes.

Vamos editar o arquivo de configração do <em><a href="https://wiki.archlinux.org/index.php/Xinitrc">xinit</a></em>:

<pre><code>vim /etc/X11/xinit/xinitrc</code></pre>

E adicionar a seguinte linha:

<pre><code>exec startxfce4</code></pre>

No meu caso o arquivo ficou da seguinte forma:

<pre><code class="bash">
#!/bin/sh

userresources=$HOME/.Xresources
usermodmap=$HOME/.Xmodmap
sysresources=/etc/X11/xinit/.Xresources
sysmodmap=/etc/X11/xinit/.Xmodmap

# merge in defaults and keymaps

if [ -f $sysresources ]; then
    xrdb -merge $sysresources
fi

if [ -f $sysmodmap ]; then
    xmodmap $sysmodmap
fi

if [ -f &quot;$userresources&quot; ]; then
    xrdb -merge &quot;$userresources&quot;
fi

if [ -f &quot;$usermodmap&quot; ]; then
    xmodmap &quot;$usermodmap&quot;
fi

# start some nice programs

if [ -d /etc/X11/xinit/xinitrc.d ] ; then
 for f in /etc/X11/xinit/xinitrc.d/?*.sh ; do
  [ -x &quot;$f&quot; ] &amp;&amp; . &quot;$f&quot;
 done
 unset f
fi

# twm &amp;
# xclock -geometry 50x50-1+1 &amp;
# xterm -geometry 80x50+494+51 &amp;
# xterm -geometry 80x20+494-0 &amp;
# exec xterm -geometry 80x66+0+0 -name login

exec startxfce4
</code></pre>

Agora já é possível executar o comando <em>startx</em> para iniciar o ambiente gráfico com o XFCE. Porém ainda falta um detalhe, ao iniciar o sistema ele deve ir para o ambiente gráfico. Para isso precisamos configurar o LXDM.

Vamos editar o arquivo de configuração do LXDM:

<pre><code>vim /etc/lxdm/lxdm.conf</code></pre>

Procure pela linha que contenha <em>session</em> e susbtitua por:

<pre><code>session=/usr/bin/startxfce4</code></pre>

No meu caso o arquivo ficou da seguinte forma:

<pre><code class="bash">
[base]
## uncomment and set autologin username to enable autologin
# autologin=dgod

## uncomment and set timeout to enable timeout autologin,
## the value should &gt;=5
# timeout=10

## default session or desktop used when no systemwide config
session=/usr/bin/startxfce4

## uncomment and set to set numlock on your keyboard
# numlock=0

## set this if you don't want to put xauth file at ~/.Xauthority
# xauth_path=/tmp

# not ask password for users who have empty password
# skip_password=1

## greeter used to welcome the user
greeter=/usr/lib/lxdm/lxdm-greeter-gtk

[server]
## arg used to start xserver, not fully function
arg=/usr/bin/X -background vt1
# uncomment this if you really want xserver listen to tcp
# tcp_listen=1
# uncoment this if you want reset the xserver after logou
# reset=1

[display]
## gtk theme used by greeter
gtk_theme=Clearlooks

## background of the greeter
# bg=/usr/share/backgrounds/default.png

## if show bottom pane
bottom_pane=1

## if show language select control
lang=1

## if show keyboard layout select control
keyboard=0

## the theme of greeter
theme=Industrial

[input]

[userlist]
## if disable the user list control at greeter
disable=0

## whitelist user
white=

## blacklist user
black=
</code></pre>

Agora que configuramos a sessão padrão do LXDM vamos habilitá-lo:

<pre><code>systemctl enable lxdm</code></pre>

Pronto, agora você pode reiniciar o seu BPi que ele iniciará o XFCE + LXDM por padrão. Abaixo você pode conferir algumas imagens.

<a href="/assets/wp-content/uploads/2014/12/IMG_20141212_232604702.jpg" target="_blank"><img class="aligncenter" src="/assets/wp-content/uploads/2014/12/IMG_20141212_232604702.jpg" alt="lxdm" width="40%" height="40%" /></a>

<a href="/assets/wp-content/uploads/2014/12/IMG_20141212_223415416.jpg" target="_blank"><img class="aligncenter" src="/assets/wp-content/uploads/2014/12/IMG_20141212_223415416.jpg" alt="lxdm" width="40%" height="40%" /></a>

Espero que você tenha gostado. Se ficou alguma dúvida não deixe de comentar.
