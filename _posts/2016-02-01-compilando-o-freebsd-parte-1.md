---
layout: wordpress
title: "Compilando o FreeBSD: Parte 1"
excerpt: |
  Ensinando o básico de compilação  do FreeBSD
date: 2016-02-01 21:15:54
author: marcooliveira
permalink: /compilando-o-freebsd-parte-1/
image: /assets/wp-content/uploads/2016/01/freebsd2.png
categories:
  - Distros
tags:
  - distro
  - freebsd
  - kernel
---

Primeiro de tudo, sei que o conteúdo propriamente dito de como baixar e compilar os fontes do sistema operacional do FreeBSD é algo que tem aos montes na Internet. Entretanto acredito que reativar tópicos interessantes ou transformar eles em um registro no <em>feeds</em> das notícias pode animar alguém a fazer estes testes.

Um aspecto é que, o objetivo deste texto é servir como base para a segunda parte que é compilar o sistema da nova maneira seguindo a proposta no livro de desenvolvimento do FreeBSD.

<!--more-->

Menos papo e vamos ao assunto. Um aspecto interessante a se notar é que o código do FreeBSD ele fica localizado em <code>/usr/src</code>, para os mais desavisados e desconhecidos de onde colocar os fontes.

Primeiramente, vamos obter o código do FreeBSD. Podemos baixar ele por um pacote txz ou pegar ele direto do controle de versão, com SVN ou git.

Pegar direto do txz tomando como base o FreeBSD 10.2:

<code>fetch ftp://ftp.freebsd.org/pub/FreeBSD/releases/amd64/amd64/10.2-RELEASE/src.txz</code>

<code>tar -C / -xvzf src.txz</code>

Uma segunda opção é sincronizar via SVN. Caso não tenha o svn você pode instalar ele via o sistema de pacotes pkg subversion ou compilando <code>cd /usr/ports/devel/subversion &amp;&amp; make install</code>. Vamos ao comando para sincronizar com o SVN do FreeBSD (Nota: espero que tão logo vire GIT no core).

<code>svn checkout <a class="externalLink" href="https://svn0.us-west.FreeBSD.org/base/releng/10.2/" target="_blank">https://svn0.us-west.FreeBSD.org/base/releng/10.2/</a> /usr/src</code>

<a href="/assets/wp-content/uploads/2015/12/svn1.png"><img class="aligncenter size-full wp-image-4240" src="/assets/wp-content/uploads/2015/12/svn1.png" alt="svn1" width="1005" height="225" /></a>

Pressione 'P' para aceitar e espere a mágica acontecer ;) .. Muitos minutos depois vamos acessar a pasta dos fontes do kernel e compilar:

<code>cd /usr/src
make buildworld KERNCONF=MYKERNEL
make installworld</code>

O <em>buildworld</em> é um prefixo do <em>Makefile</em> de compilação do sistema operacional FreeBSD para construir o código, o único parâmetro exigido é a localização da sua configuração do kernel.
Senta e espera... ;)

Mas pera aí Marco, mas onde está a configuração..? Tá bom vamos descrever como ajustar as configurações. Aos mais desavisados, para lerem o texto antes de sair colando os códigos, joguei essa trap...

O arquivo fica em <code>/usr/src/sys/amd64/conf</code>, para arquitetura amd64. Para outras arquiteturas basta mudar a pasta <code>amd64</code> para <code>arm</code> ou <code>i386</code>.

E como alterar? Claro que com o seu editor predileto.

<code>cd /usr/src/sys/amd64/conf/
cp GENERIC MYKERNEL
cd ../../../ ( vai para cd /usr/src/ )
make buildworld KERNCONF=MYKERNEL &amp;&amp; make installworld</code>

Agora funcionou :D Senta e espera terminar de compilar .. :o

O arquivo de configuração GENERIC ele é bem detalhado e a parametrização simples, lembrando o par chave e valor. Neste ponto, por exemplo, podemos alterar o nome da build do nosso kernel. Este é o nome que aparece quando rodamos o comando <code>uname -a</code>

<code>ident BaconBSD</code>

Podemos incluir dispositivos com o parâmetro device, ou no caso excluir comentando a linha no dispositivo que não precisamos:

<code>device vmx # VMware VMXNET3 Ethernet</code>

Basicamente comente este se você não usa vmware. Se você tiver dúvida sobre algum dispositivo o clássico manual te ajuda:

<code># man vmx</code>

Se mesmo assim os comentários do arquivo de configuração do GENERIC não foram o suficiente você pode expandir e conhecer mais das opções de parâmetros de configuração no arquivo de notas: <code>/usr/src/sys/amd64/conf/NOTES</code>

<code># emacs /usr/src/sys/amd64/conf/NOTES</code>

Algo muito interessante ao se compilar o sistema operacional FreeBSD é perceber que programas como o heimdal e o ssh são partes do pacote do sistema. O FreeBSD, diferentemente do Linux, não é apenas um kernel, é um sistema operacional inteiro, tendo programas como tar, xz e outros.