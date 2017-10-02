---
layout: wordpress
title: "Virsh: criando e gerenciando VMs pelo terminal"
excerpt: |
  Este artigo apresenta uma introdução a ferramenta virsh, baseada na libvirt, para gerenciar máquinas virtuais no Linux.
date: 2015-08-25 23:44:58
author: marcossouza
permalink: /virsh-criando-e-gerenciando-vms-pelo-terminal/
image: /assets/wp-content/uploads/2015/06/libvirtLogo.png
categories:
  - Dicas
  - Ferramentas
tags:
  - kvm
  - linux
  - qemu
  - terminal
  - virtualização
---

O <strong>virsh</strong> é um utilitário criado para gerenciar máquinas virtuais de tecnologias como KVM, Xen, VMware ESX, QEMU entre outras. Esse suporte se deve ao fato do <strong>virsh</strong> ser construído utilizando a libvirt como base.

De uma forma simples, a libvirt é uma API/daemon criada pela Red Hat para gerenciar máquinas virtuais. Assim como o <strong>virsh</strong>, outras ferramentas são baseadas na libvirt para gerenciar VMs, como virt-manager, OpenStack e oVirt. Apesar de ser escrita em C, existem bindings para outras linguagens, como Python, Perl, Ruby, Java e PHP.

<!--more-->

Para instalar os pacotes necessários para este tutorial em uma distro Red Hat-like, execute o seguinte comando:

<pre><code class="bash">
sudo yum install qemu-img libvirt-client virt-viewer virt-install
</code></pre>

Para iniciar, vamos criar um HD para nossa VM. Na verdade, o HD é um arquivo dentro do sistemas de arquivos da sua distro, onde a VM irá utilizar como se fosse um HD propriamente dito.

<pre><code class="bash">
qemu-img create -f qcow2 guest.qcow2 8192M
</code></pre>

O qemu-img é um utilitário de imagens de disco do QEMU. Com ele é possível aumentar e diminuir o tamanho das imagens de disco, converter entre formatos, e muito mais. No comando acima, estamos criando uma nova imagem de disco, com o formato qcow2 (que é o padrão do QEMU, mas podem ser utilizados outros formatos como VMDK, VHDX, RAW, VDI e outros), com 8G de espaço e com o nome de guest.qcow2.

O comando a seguir cria uma nova maquina virtual utilizando o o disco previamente criado com uma imagem live do Fedora 22:

<pre><code class="bash">
virt-install -r 1024 -f guest.qcow2 -n Fedora_Guest --cdrom data/isos/Fedora-Live-LXDE-x86_64-20-1.iso --virt-type kvm --network bridge=virbr0 --vnc
</code></pre>

-r: memória RAM em megabytes
-f: disco onde será instalado o sistema
-n: Nome da máquina virtual
--cdrom: Para para o ISO de uma distro da sua escolha. Aqui escolhi uma imagem do Fedora que eu tinha disponível
--network: Tipo de rede que você deseja habilitar para a VM. Neste caso eu já havia criado uma rede bridge antes, e então decidi usar esta. Para desabilitar a rede basta informar none
--vnc: Inicia um VNC server para esta VM. Este vai ser utilizado posteriormente

O parâmetro virt-type merece um destaque, pois ele informa o tipo de virtualização que será utilizado na máquina. Na minha máquina em questão, meu processador tem suporte a KVM (Kernel Virtual Machine), que possibilita uma alta performance quando executando uma VM. Para verificar se o seu processador tem essa tecnologia, execute:

<pre><code class="bash">
virsh capabilities
</code></pre>

Se no output deste comando houver uma tag como:

<pre><code class="bash">
   &lt;domain type='kvm'&gt;
        &lt;emulator&gt;/usr/bin/qemu-kvm&lt;/emulator&gt;
        &lt;machine canonical='pc-i440fx-2.3' maxCpus='255'&gt;pc&lt;/machine&gt;
        &lt;machine maxCpus='255'&gt;pc-1.3&lt;/machine&gt;
        &lt;machine maxCpus='255'&gt;pc-0.12&lt;/machine&gt;
        &lt;machine maxCpus='255'&gt;pc-q35-1.6&lt;/machine&gt;
</code></pre>

Então seu processador tem esta tecnologia. Se este não tiver, utilize qemu como parâmetro do virt-type.

Após executar este comando, vemos algo do tipo:

<pre><code class="bash">
[marcos@xfiles ~]$ virt-install -r 1024 -f guest.qcow2 -n Fedora_Guest --cdrom data/isos/Fedora-Live-LXDE-x86_64-20-1.iso --virt-type kvm --network bridge=virbr0 --vnc
WARNING  Graphics requested but DISPLAY is not set. Not running virt-viewer.
WARNING  No console to launch for the guest, defaulting to --wait -1

Starting install...
Criando o domínio...                                                                                                                                 |    0 B  00:00:00
Domain installation still in progress. Waiting for installation to complete.
</code></pre>

Se você estiver executando estes comandos no console da máquina em questão, então irá aparecer o virt-viewer mostrando a execução da VM, tal qual o Virtual Box, virt-manager e outros gerenciadores de máquinas virtuais fazem. Mas se por acaso você estiver acessando esta máquina por uma conexão ssh, então nenhuma janela será mostrada e o shell ficará preso até você configurar o SO que foi iniciado. Para poder visualizar a VM via VNC na rede, basta executar o comando abaixo:

<pre><code class="bash">
virt-viewer -c qemu+ssh://usuario@ip/system Fedora_Guest
</code></pre>

Para utilizar o VNC na mesma máquina, basta colocar -c qemu:///sytem.

Com este comando, será solicitado o usuário e senha do máquina que você está conectando, e após este será exibido o virt-viewer com a imagem da VM sendo executada:
<a href="/assets/wp-content/uploads/2015/06/Captura-de-tela-de-2015-06-15-21-23-27.png"><img class="aligncenter wp-image-2773" src="/assets/wp-content/uploads/2015/06/Captura-de-tela-de-2015-06-15-21-23-27-300x242.png" alt="Captura de tela de 2015-06-15 21-23-27" width="600" height="446" /></a>

Após instalar a VM, o processo é todo feito como um gerenciador de VMs qualquer, com a vantagem de poder acessar as VMs por VNC de qualquer lugar que quiser.

Com o <strong>virsh</strong> é possível gerenciar essas VMs, com os seguintes comandos:
<strong>virsh</strong> list: Lista todos as VMs criadas e seu estado de funcionamento.
<strong>virsh</strong> shutdown : Envia comando de desligamento para a VM.
<strong>virsh</strong> destroy : Faz um force shutdown na VM.
<strong>virsh</strong> start : Liga a VM

Entre vários outros comandos. Com o <strong>virsh</strong> é possível ainda manipular discos nas VMs, adicionando e removendo discos conforme a necessidade, alterar parâmetros de rede, criando e removendo interfaces e vários outros.

O <strong>virsh</strong> se mostra realmente uma ótima ferramenta para gerenciar suas máquinas virtuais. Se você deseja uma ferramenta com interface gráfica não esquece de ver este <a href="/conhecendo-o-virt-manager/" target="_blank">artigo</a> sobre o virt-manager, que é basicamente um front-end para o <strong>virsh</strong>.

Espero que tenham gostado desta pequena explicação sobre o <strong>virsh</strong>. Até a próxima!

Referências:
<a href="https://en.wikipedia.org/wiki/Libvirt" target="_blank">Wikipédia - libvirt</a>
<a href="http://linux.die.net/man/1/virsh" target="_blank">man virsh</a>
<a href="http://linux.die.net/man/1/virt-install" target="_blank">man virt-install</a>
<a href="http://linux.die.net/man/1/virt-viewer" target="_blank">man virt-viewer</a>
<a href="http://virt-tools.org/learning/install-with-command-line/" target="_blank">virt-tools.org</a>