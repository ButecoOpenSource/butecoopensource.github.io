---
layout: wordpress
title: "QEMU/KVM: Habilitar serial console no CentOS/RHEL para acessá-lo pelo virsh console"
date: 2014-09-17 12:03:21
author: marcossouza
permalink: /qemukvm-habilitar-serial-console-no-centosrhel-para-acessa-lo-pelo-virsh-console/
categories:
  - Desenvolvimento
  - Ferramentas
tags:
  - centos
  - kvm
  - linux
  - qemu
---

Olá pessoal, a alguns dias atrás eu precisei fazer alguns testes usando o QEMU/KVM, e para isso foi necessário o acesso a uma máquina virtual com CentOS utilizando o virsh console. Para isto eu precisei habilitar o ttyS0 tanto no inittab como na linha de inicialização do Kernel no CentOS.

Como primeiro passo iremos editar o arquivo /etc/initab, como root, e adicionar a seguinte linha:

<pre><code class="bash">
S0:2345:respawn:/sbin/agetty -h -L ttyS0 19200 vt100
</code></pre>

E então podemos fechar este arquivo. Após este é necessário adicionar um parametro no kernel para criar o serial console no ttyS0. A versão de Cent OS que estou usando ainda utiliza o Grub legacy, então se você está utilizando uma versão com Grub2, basta encontrar onde é definido mesmo parâmetro e alterar este da mesma forma.

Encontre uma linha como esta:
<pre><code class="bash">
kernel /vmlinuz-2.6.32-431.el6.x86_64 ro root=/dev/mapper/VolGroup-lv_roo
ot rd_NO_LUKS LANG=en_US.UTF-8 rd_NO_MD rd_LVM_LV=VolGroup/lv_swap SYSFONT=latarr cyrheb-sun16 crashkernel=auto rd_LVM_LV=VolGroup/lv_root  KEYBOARDTYPE=pc KEYTABBLE=us rd_NO_DM rhgb quiet
</code></pre>

E adicione <em>console=ttyS0,19200n8 </em>no fim desta linha:
<pre><code class="bash">
kernel /vmlinuz-2.6.32-431.el6.x86_64 ro root=/dev/mapper/VolGroup-lv_roo
ot rd_NO_LUKS LANG=en_US.UTF-8 rd_NO_MD rd_LVM_LV=VolGroup/lv_swap SYSFONT=latarr cyrheb-sun16 crashkernel=auto rd_LVM_LV=VolGroup/lv_root  KEYBOARDTYPE=pc KEYTABBLE=us rd_NO_DM rhgb quiet console=ttyS0,19200n8
</code></pre>

Então basta fazer um reboot na VM e acessar a máquina pelo virsh console:

<pre><code class="bash">
virsh console nomevm
</code></pre>

A mesma configuração vale também para o RHEL. Caso você tenha algum problema em fazer o serial console do CentOS funcionar com esta explicação, basta perguntar nos comentários do post que podemos verificar o que está acontecendo. Espero ter ajudado!

Eu tentei habilitar a serial console no Fedora 20 utilizando o systemd, mas não obtive exito. Se alguém souber como fazer e quiser postar nos comentários, acho que iria ajudar muitas pessoas além de mim :)

Até mais!

<em>Fonte: http://www.cyberciti.biz/faq/centos-rhel-6-install-serial-console/</em>