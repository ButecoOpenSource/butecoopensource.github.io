---
layout: wordpress
title: Instalando o Spotify no openSUSE
excerpt: |
  O Spotify é um serviço de stream de música que oferece opção gratuita e paga. O aplicativo do Spotify está disponível para a maioria dos sistemas operacionais, inclusive Linux. Bem, Linux só em formato DEB o que deixa a desejar para quem usa sistemas operacionais não debian-like, como openSUSE, Fedora ou alguma outra distro baseada no Red Hat.
date: 2016-04-26 22:27:10
author: alexandrevicenzi
permalink: /instalando-o-spotify-no-opensuse/
image: /assets/wp-content/uploads/2016/04/spotify.png
categories:
  - Dicas
tags:
  - deb
  - música
  - opensuse
  - rpm
  - spotify
  - streaming
---

O <a href="https://www.spotify.com/br/" target="_blank">Spotify</a> é um serviço de stream de música que oferece opção gratuita e paga. O aplicativo do Spotify está disponível para a maioria dos sistemas operacionais, inclusive Linux. Bem, Linux só em formato DEB o que deixa a desejar para quem usa distribuições não debian-like, como openSUSE, Fedora ou alguma outra distro baseada no Red Hat.

No caso do openSUSE existe um projeto a parte para tornar possível a instalação do Spotify. O <a href="https://github.com/aspiers/opensuse-spotify-installer/" target="_blank">spotify-installer</a> é um projeto de código aberto que faz a conversão do DEB para RPM e alguns outros ajustes para permitir a instalação sem muitos problemas.

<!--more-->

Vale lembrar que pode ser que em seu openSUSE não seja possível instalar devido alguma incompatibilidade de pacotes. No meu caso eu instalei no openSUSE Tumbleweed, mas creio que funcione também para as versões Leap e 13.x.

O spotify-installer pode ser instalado de duas formas, a primeira é via <a href="https://en.opensuse.org/Additional_package_repositories#Packman" target="_blank">repositório do PackMan</a> com o comando <code>zypper in spotify-installer</code> e a outra é através do <a href="http://packman.links2linux.org/install/spotify-installer" target="_blank">1-click install</a>.

Após obter o instalador, vamos instalar a dependência do <a href="http://directory.fsf.org/wiki/Libgcrypt" target="_blank">Libgcrypt</a>, a qual não é instalada pelo spotify-installer e sem ela o programa não irá abrir. O maior problema é que não é qualquer versão que irá funcionar, no meu caso eu resolvi o problema com a versão 1.5.4-2.4.1. O RPM desta versão pode ser encontrado no <a href="http://rpm.pbone.net/index.php3/stat/4/idpl/27155581/dir/opensuse_13.x/com/libgcrypt11-1.5.4-2.4.1.x86_64.rpm.html" target="_blank">RPM PBone</a>. Esta versão é compatível com openSUSE 13.x e superiores.

Agora sim, podemos instalar o Spotify. Para isso execute o comando <code>install-spotify</code> via terminal com um usuário não root. Durante a instalação será solicitado a senha do root.

Durante a instalação você deverá ver algo semelhante ao texto abaixo no seu console (uma parte do texto foi omitida):

<samp>alexandre@suse ~ $ install-spotify
root's password:
Loading repository data...
Reading installed packages...
Resolving package dependencies...</samp>

<samp>The following 5 NEW packages are going to be installed:
bison bison-lang gettext-tools rpm-build systemd-rpm-macros</samp>

<samp>The following recommended package was automatically selected:
bison-lang</samp>

<samp>Downloading Spotify .deb package ...</samp>

<samp>.deb downloaded.</samp>

<samp>About to build spotify-client rpm; please be patient ...</samp>

<samp>rpm successfully built!</samp>

<samp>Installing Spotify from the rpm we just built ...
Loading repository data...
Reading installed packages...
Resolving package dependencies...</samp>

<samp>The following NEW package is going to be installed:
spotify-client</samp>

<samp>1 new package to install.
Overall download size: 40,9 MiB. Already cached: 0 B. After the operation, additional 136,4 MiB will be used.
Continue? [y/n/? shows all options] (y): y
Retrieving package spotify-client-0.9.17.8.gd06432d.31-1.x86_64 (1/1), 40,9 MiB (136,4 MiB unpacked)
Checking for file conflicts: ...................................................................................................................[done]
(1/1) Installing: spotify-client-0.9.17.8.gd06432d.31-1.x86_64 .................................................................................[done]</samp>

<samp>Spotify can now be run via /usr/bin/spotify - happy listening!</samp>

Pode ser que durante a instalação seja requisitado alguma iteração do usuário, como confirmar a instalação de algum pacote adicional.

Se tudo correr bem, você pode abrir o Spotify através do ícone criado na área de aplicativos.

Para finalizar, até agora não encontrei nenhum problema em relação de compatibilidade com algo, até a área de notificação funciona corretamente com o aplicativo. Para ser sincero, a versão do OS X e do Android costumam me dar mais dor de cabeça que esta do Linux.

Happy Listening. :D