---
layout: wordpress
title: Adicionando Swap ao CentOS, Ubuntu e derivados
excerpt: |
  Por que adicionar Swap?
  Para você que acabou de criar a sua primeira VM no Digital Ocean e pegou logo de cara a de 512 de RAM, você vai se ver no aperto dependendo da aplicação que colocar para executar nela. Para solucionar possíveis problemas de falta de memória vamos adicionar Swap a esta máquina tão simplória.
date: 2015-07-23 08:39:33
author: alexandrevicenzi
permalink: /adicionando-swap-ao-centos-ubuntu-e-derivados/
categories:
  - Dicas
tags:
  - centos
  - memória
  - swap
  - ubuntu
---

Para você que acabou de criar a sua primeira VM no Digital Ocean e pegou logo de cara a de 512 de RAM, você vai se ver no aperto dependendo da aplicação que colocar para executar nela. Para solucionar possíveis problemas de falta de memória vamos adicionar Swap a esta máquina tão simplória.

Aplicações simples como o MySQL e o Jenkins rodando nessas máquinas poder gerar alguma dor de cabeça caso você não identifique que o problema é falta de memória. Por exemplo, no meu caso o Jenkins parava a execução dos testes no meio, pois recebia um SIGKILL de alguém, provavelmente do S.O. O mais estranho é que o Jenkins continuava executando, apenas parava o Job que estava em execução. A solução foi bem simples, adicionar uma Swap, já que não queríamos aumentar os valores com VMs do DO.

O tutorial de hoje é baseado no CentOS e no Ubuntu. Fiz a mesma configuração em duas VMs distintas. A maioria das distros suportam os comandos e sistemas de arquivos aqui mencionados.

<!--more-->

<strong>Verificando a existência de Swap</strong>

Vamos verificar se existe Swap habilitado primeiro, para isso execute o comando:

<code>swapon -s</code>

Não deverá retornar nada caso não tenha Swap.

O mesmo pode ser observado com o comando:

<code>free -m</code>

Que neste caso irá retornar 0, conforme abaixo:
<pre>             total       used       free     shared    buffers     cached
Mem:           490        399         91          8         24        263
-/+ buffers/cache:        111        378
Swap:            0          0          0
</pre>
Antes de começar vamos verificar se existe algum espaço em disco que podemos usar, para isto execute o comando:

<code>df -h</code>

O retorno deverá ser algo semelhante ao abaixo:
<pre>Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        20G  1,5G   18G   9% /
devtmpfs        240M     0  240M   0% /dev
tmpfs           246M     0  246M   0% /dev/shm
tmpfs           246M  8,3M  237M   4% /run
tmpfs           246M     0  246M   0% /sys/fs/cgroup
</pre>
Agora que verificamos quanto temos de espaço em disco vamos a criação do arquivo de Swap.

<strong>Como definir um bom tamanho para o Swap?</strong>

O recomendado em qualquer distribuição é o dobro de memória RAM para máquinas com até 8 GB de RAM. Caso sua máquina tenha mais que isso não há necessidade se sua Swap ser maior que 16 GB. Vale lembrar que Swap é algo que não queremos que se use em grande quantide, pois isto afeta o desempenho da máquina. Se você notar que o sistema está usando quase toda a Swap isto quer dizer que é necessário um upgrade de RAM.

<strong>Criando o arquivo de Swap</strong>

O modo mais rápido para criar um arquivo swap é com o comando <em>fallocate</em>. O <em>fallocate</em> é usado para pré-alocar espaço para um arquivoe para ser rápido ele preenche o arquivo com zeros. O <em>fallocate</em> suporta os sistemas de arquivos btrfs, ext4, ocfs2 e xfs.

Eu vou criar o arquivo com 1 GB no raiz (/) com o nome swapfile. Para isto vou usar o comando abaixo:

<code>sudo fallocate -l 1G /swapfile</code>

Para testar se o arquivo foi criado corretamente com o comando:

<code>ls -lh /swapfile</code>

E o resultado deverá ser semelhante ao abaixo:
<pre>-rw-r--r-- 1 root root 1,0G Mai 28 20:09 /swapfile
</pre>
<strong>Habilitando o Swap</strong>

Antes de habilitar o Swap, vamos mudar as permissões do arquivo, para que ninguém além do root tenha acesso à ele. Para isto executamos o comando:

<code>sudo chmod 600 /swapfile</code>

Você pode verificar as permissões com o comando:

<code>ls -lh /swapfile</code>
<pre>-rw------- 1 root root 1,0G Mai 28 20:09 /swapfile
</pre>
Agora que tiramos as permissões para os demais usuários, podemos montar o Swap. Para isto execute o comando:

<code>sudo mkswap /swapfile</code>

O resultado, se tudo ocorrer bem, é exibir o tamanho alocado e o UUID que foi montado.
<pre>Setting up swapspace version 1, size = 1048572 KiB
no label, UUID=30572f65-706b-43c2-8a87-35cf8b308e82
</pre>
Após montado podemos habilitar o Swap, para isto execute o comando abaixo:

<code>sudo swapon /swapfile</code>

Você pode usar os comandos <em>swapon</em>/<em>swapoff</em> para habilitar/desabilitar a memória Swap.

Agora podemos usar os comandos <em>swapon -s</em> e <em>free -m</em> para verificar se o Swap está habilitado.

<strong>Swap permanente</strong>

Para que o Swap seja permanente, ou seja, não se perca no reboot, devemos alterar o <em>fstab</em>. Abra o arquivo <em>/etc/fstab</em> com o seu editor preferido, no meu caso vou usar o VIM:

<code>sudo vim /etc/fstab</code>

E vamos adicionar a seguinte linha no fim do arquivo:
<pre>/swapfile   none    swap    sw    0   0
</pre>
<strong>Turbinando o Swap</strong>

<strong>Swappiness</strong>

O parâmetro <em>swappiness</em> define com que frequência o sistema manda dados ao Swap, e seu valor vai de 0 a 100. Quanto mais próximo a 100, mais Swap irá usar, garantindo mais mémoria livre. Como Swap é mais lento, vamos fazer com que use a memória o máximo do tempo ao invéz de Swap.

Para verificar o valor atual execute o comando:

<code>cat /proc/sys/vm/swappiness</code>

Vamos alterar o valor para 10 com o comando:

<code>sudo sysctl vm.swappiness=10</code>

Para que esta configuração seja permanente devemos editar o arquivo <em>/etc/sysctl.conf</em>:

<code>sudo vim /etc/sysctl.conf</code>

E adicionar no fim do arquivo a linha:

<pre><code class="bash">
vm.swappiness=10
</code></pre>

<strong>Cache Pressure</strong>

Para verificar o valor atual execute o comando:

<code>cat /proc/sys/vm/vfs_cache_pressure</code>

Vamos alterar o valor para 50 com o comando:

<code>sudo sysctl vm.vfs_cache_pressure=50</code>

Para que esta configuração seja permanente devemos editar o arquivo <em>/etc/sysctl.conf</em>:

<code>sudo vim /etc/sysctl.conf</code>

E adicionar no fim do arquivo a linha:

<pre><code class="bash">
vm.vfs_cache_pressure=50
</code></pre>

Essas configurações são simples, mas podem solucionar alguns problemas do dia a dia.

Este artigo foi baseado no tutorial <a href="https://www.digitalocean.com/community/tutorials/how-to-add-swap-on-centos-7">How To Add Swap on CentOS 7</a>.