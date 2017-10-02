---
layout: wordpress
title: Dica - Resetando senha do root Centos 7
excerpt: |
  Resetar senha de root em Red Hat Likes.
date: 2015-06-15 23:13:07
author: marcooliveira
permalink: /dica-resetando-senha-do-root-centos-7/
categories:
  - Dicas
tags:
  - linux
---

<a href="/assets/wp-content/uploads/2015/06/password-error.jpg"><img class=" size-full wp-image-2673 aligncenter" src="/assets/wp-content/uploads/2015/06/password-error.jpg" alt="password-error" width="299" height="168" /></a>

&nbsp;

Dica rápida para este processo, trivial do cotidiano de um administrador que pega ambientes dos quais não existem documentações, ou daqueles como eu que se esquecem da senha do root de sua máquina virtualizada... XD

<!--more-->

No grub entre no modo de edição da parametrização do boot do kernel que você utiliza. Pressionando "E".

O modo de edição do grub permite navegar utilizando as teclas de setas, e a hotkey <strong>CTRL+E</strong> para ir ao final da linha. Procure a linha onde existe a configuração <strong>linux16</strong> e no final dela adicione "<strong>rd.break enforcing=0"</strong>. Conforme a imagem a seguir:

<a href="/assets/wp-content/uploads/2015/06/reset2.png"><img class=" size-full wp-image-2671 aligncenter" src="/assets/wp-content/uploads/2015/06/reset2.png" alt="reset2" width="728" height="393" /></a>

Pressione <strong>CTRL+X</strong> para bootar no kernel modificado

Na sequência ele deve iniciar o sistema operacional no no modo de quebra, para tentar resolver algum problema que tenha ocorrido no sistema antes dele inicializar ( <strong>rd.break</strong> ), e desabilitar o <strong>SELINUX</strong> temporariamente pois não precisamos para fazer esta alteração. Para melhor exemplificar segue uma imagem com todos os comandos necessários executar para resetar a senha

<a href="/assets/wp-content/uploads/2015/06/reset4.png"><img class=" size-full wp-image-2672 aligncenter" src="/assets/wp-content/uploads/2015/06/reset4.png" alt="reset4" width="727" height="393" /></a>

No modo de quebra, montamos o disco do nosso sistema no modo de escrita.

<code>#mount -o remount,rw /sysroot</code>

Utilizamos o <strong>chroot</strong> para alternar as pasta raíz do sistema, para que possamos utilizar dos programas de onde o sistema operacional se encontra instalado no disco.

<code>#chroot /sysroot</code>

A próxima etapa é alterar a senha com o comando <strong>passwd</strong>.

<code>#passwd</code>

Na sequência remontamos a raiz do sistema no modo de leitura.

<code>#mount -o remount,ro /</code>

Por fim saímos do <strong>chroot </strong> e do modo <strong>rd.break</strong> executando duas vezes o comando <strong>exit</strong>. E o sistema em sequência deve carregar o ambiente agora com a nova senha de root.

Referências:

<a href="https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/System_Administrators_Guide/sec-Terminal_Menu_Editing_During_Boot.html" target="_blank">Terminal Menu Editing During Boot</a> - Documentação oficial da Red Hat

&nbsp;