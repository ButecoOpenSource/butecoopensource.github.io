---
layout: wordpress
title: Instalando o Alien no openSUSE
excerpt: |
  O Alien é um aplicativo para conversão de arquivos de instalação de pacotes. Ou seja, ele converte, por exemplo, um arquivo de instalação do Debian para um arquivo de instalação do openSUSE.
date: 2015-03-17 00:53:54
author: alexandrevicenzi
permalink: /instalando-o-alien-no-opensuse/
image: /assets/wp-content/uploads/2015/03/deb-rpm-pkg.png
categories:
  - Dicas
tags:
  - alien
  - deb
  - dpkg
  - linux
  - rpm
---

O <a href="https://joeyh.name/code/alien/">Alien</a> é um aplicativo para conversão de arquivos de instalação de pacotes. Ou seja, ele converte, por exemplo, um arquivo de instalação do Debian para um arquivo de instalação do openSUSE.

O Alien suporta conversão para vários arquivos, dentre estes, estão os arquivos: Red Hat (.rpm), Debian (.deb), Stampede (.slp), Solaris (.pkg) e Slackware (.tgz).

<strong>Por que este tutorial?</strong>

Apesar de ser simples a instalação, se você não se atentar bem, você pode esquecer de instalar algum dos pacotes adicionais. No openSUSE a instalação é manual, já para outras distribuições é possível encontrar os pacotes <em>alien</em> e <em>alien-extras</em> que instalam todas as dependências necessárias para executar o Alien.

<strong>Instalação</strong>

Antes de iniciar o download você deve baixar o código fonte <a href="https://packages.debian.org/unstable/source/alien" target="_blank">aqui</a>.

Após baixado, descompacte o arquivo.

Ainda antes de instalar, vamos instalar algumas dependências necessárias do Alien. Execute o comando abaixo para instalar tudo o que é necessário:

<code>zypper in perl rpm dpkg dpkg-devel debhelper bzip2</code>

Após instalar todas as dependências, vamos a instalação do Alien. Para isto execute o comando abaixo:

<code>perl Makefile.PL; make; make install</code>

Lembre-se de executar este comando dentro da pasta onde você descompactou o arquivo.

<strong>Convertendo um deb para rpm</strong>

Agora que você já possui o Alien, utilize o seguinte comando para converter um pacote .deb para .rpm:

<code>alien --to-rpm --scripts seu_pacote.deb</code>

Espero que esta publicação ajude você, caso você teve algum problema durante a instalação do Alien.