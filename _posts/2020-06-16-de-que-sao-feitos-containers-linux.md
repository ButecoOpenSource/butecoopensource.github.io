---
layout: post
title: "De que são feitos containers Linux?"
excerpt: "Você já deve ter ouvido falar sobre Docker, talvez já tenha usado. Docker é uma parte do ecossistema de containers Linux, mas não é só isso, existe muito mais por trás e que compõe todo o ecossistema."
tagline: "Containers Linux explicado"
date: 2020-06-16 08:00:00
categories: Desenvolvimento
tags: containers docker lxc linux
permalink: de-que-sao-feitos-containers-linux
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: true
  image: /assets/content/lxc-logo.png
---

Você já deve ter ouvido falar sobre Docker, talvez já tenha usado. Docker é uma parte do ecossistema de containers Linux, mas não é só isso, existe muito mais por trás e que compõe todo o ecossistema.

## O que é um container?

Em uma breve definição, um container é uma forma de isolar aplicações do sistema hospedeiro.

Containers possuem todos os arquivos necessários para que aplicações possam ser executadas, aumentando a portabilidade e eficiência na hora de migrar do ambiente de desenvolvimento para testes e produção.

## Um pouco da história

![Timeline](/assets/content/container-timeline.png)

O que hoje é conhecido como containers Linux surgiu inicialmente no FreeBSD 4.x com o [Jails](https://www.freebsd.org/doc/handbook/jails.html){:target="_blank"} no ano 2000. O Jails permite a criação de um ambiente seguro e isolado do resto do sistema assim como os containers Linux.

Logo após surgiu o [control groups (cgroups)](https://man7.org/linux/man-pages/man7/cgroups.7.html){:target="_blank"} no Kernel Linux 2.6, uma parte essencial do ecossistema. cgroups permite limitar e isolar recursos como CPU, memória, disco, redes, etc.

Em 2008 surge o [LXC](https://linuxcontainers.org/lxc/){:target="_blank"}, trazendo vários conceitos e ferramentas para se trabalhar com containers.

## Qual a finalidade?

Containers reduzem a complexidade, aumentam a portabilidade e a segurança e padronizam ambientes. Era comum ouvirmos a expressão “Funciona na minha máquina”. Tem tempo que eu não ouço essa frase.

Com containers você possui um ambiente controlado, não é afetado facilmente pelo o que acontece no resto do sistema e se usado corretamente, as imagens sempre serão idênticas, ou seja, se não funciona em um, não irá funcionar em outro, pois é a mesma imagem.

Uma imagem (ou container image) é uma forma de encapsulamento (ou empacotamento) de sua aplicação, bem como todas as dependências para a sua execução. Como essas imagens são compiladas e publicadas em um registro de containers, toda pessoa que usar essa imagem receberá uma cópia idêntica da versão compilada.

Como os containers são isolados um dos outros, evitamos que um afete o outro ou o sistema num todo. Isso é de extrema importância no quesito segurança. Imagine que uma biblioteca que você use possui uma grave falha de segurança, como a aplicação está isolada em um container essa falha possivelmente não irá afetar o sistema todo.

## Containers vs Virtualização

![Containers vs Virtualização](/assets/content/containers-vs-virtualizacao.png)

Um container não é uma máquina virtual, mas existem algumas semelhanças. Na virtualização você está rodando um sistema simultaneamente em um único hardware. O exemplo mais comum é rodar Windows dentro do Linux.

Virtualização usa [Hypervisor](https://pt.wikipedia.org/wiki/Hipervisor){:target="_blank"} para emulação de hardware e isso consome mais recursos que containers. Na virtualização é possível executar um sistema operacional dentro de outro. Com containers você está compartilhando o mesmo Kernel Linux, ou seja, você apenas isola aplicações e bibliotecas do resto do sistema, não sendo possível executar um container Windows dentro do Linux, por exemplo.

Neste caso, se você está rodando Ubuntu 20 com Kernel 5.4 e iniciar um container e executar o comando `uname -r` você terá a mesma versão que o sistema hospedeiro. O Kernel é o mesmo, porém o ecossistema pode ser totalmente diferente. Você pode executar um container Fedora 32 dentro do Ubuntu, por exemplo.

## Containers ao nível de Kernel

Existem diversas funcionalidades ao nível de Kernel que permitem a implementação de containers. No Kernel em si não existem containers, mas as funcionalidades abaixo permitem a implementação de containers.

### Namespaces

[Namespaces](https://man7.org/linux/man-pages/man7/namespaces.7.html){:target="_blank"} servem para isolar recursos do sistema.

Existem os seguintes namespaces:

* Cgroup - Isola o diretório raiz do cgroup
* IPC - Isola o System V IPC e a fila de mensagens POSIX
* Network - Isola dispositivos de rede, portas, etc.
* Mount - Isola mount points.
* PID - Isola IDs de processos
* Time - Isola os relógios
* User - Isola IDs de usuários e grupos
* UTS - Isola hostname e nome de domínio

Com essa funcionalidade é possível isolar vários recursos do sistema, permitindo que o container só enxergue aquilo que lhe foi permitido. Um container não consegue enxergar recursos de outro ou até mesmo os recursos totais do sistema.

Um exemplo bem simples é limites de memória. Seu servidor pode ter 128 GB de RAM, mas se o limite para o container for de 4 GB ele irá pensar que existem apenas 4 GB no sistema.

### Control Groups

[cgroups](https://man7.org/linux/man-pages/man7/cgroups.7.html){:target="_blank"} permite limitar e isolar recursos como CPU, memória, disco, redes, etc. Com essa funcionalidade é possível organizar processos em grupos hierárquicos de uso por vários tipos de recursos.

cgroups ainda provê um pseudo sistema de arquivos chamado cgroupfs, que pode ser usado para obter informações do cgroups.

### Capabilities

Tradicionalmente UNIX distingue processos em duas categorias, *privileged* (privilegiado) e *unprivileged* (não privilegiado). Um processo root (com user ID 0) não tem checagens, porém um processo não root passa por todas as checagens de permissões.

[capabilities](https://man7.org/linux/man-pages/man7/capabilities.7.html){:target="_blank"} permite definir privilégios por processo, permitindo um controle maior sobre processos do que apenas usando as categorias root ou não root, além disso, é possível fracionar as capabilities de root, onde um processo pode ter permissões root para determinadas ações (capabilities), mas ele não possui acesso root em todo o sistema.

A lista de capabilities é grande e não vou mencionar aqui, mas elas dão permissões a certos recursos do sistema, como a `CAP_NET_ADMIN` que permite alterar várias configurações relacionadas a redes.

### Segurança

Linux Security Modules (LSM) é um framework que permite suporte ao nível de Kernel para diversos modelos de segurança. [AppArmor](https://en.wikipedia.org/wiki/AppArmor){:target="_blank"}, [SELinux](https://en.wikipedia.org/wiki/SELinux){:target="_blank"}, [Smack](https://en.wikipedia.org/wiki/Smack_(software)){:target="_blank"} e [TOMOYO Linux](https://en.wikipedia.org/wiki/Tomoyo_Linux){:target="_blank"} fazem parte dos módulos oficiais.

Esses módulos são usados para assegurar a separação entre host e container e também entre containers individualmente. Essa separação é feita aplicando políticas de seguranças que restringem os processos rodando.

Essa funcionalidade não é só usada para containers, mas também pode ser aplicada a processos rodando no sistema host.

## Container runtime

Um container runtime é responsável por gerenciar e executar os containers, porém alguns possuem funcionalidades extras como gerenciar imagens.

Alguns exemplos de runtime são:

* [LXC](https://linuxcontainers.org/lxc/){:target="_blank"}
* [runC](https://github.com/opencontainers/runc){:target="_blank"}
* [containerd](https://containerd.io/){:target="_blank"}
* [CRI-O](https://cri-o.io/){:target="_blank"}

## Container engine

Um container engine é uma aplicação que aceita requisições e se comunica com o container runtime, geralmente são disponibilizados em forma de aplicações de linha de comando.

Alguns exemplos de engine são:

* [Docker](https://docs.docker.com/engine/){:target="_blank"}
* [Podman](https://podman.io/){:target="_blank"}
* [RKT](https://coreos.com/rkt/){:target="_blank"}
* [LXD](https://linuxcontainers.org/lxd/){:target="_blank"}

## Outras abordagens

Até agora mencionamos apenas sobre containers nativos (ao nível de Kernel), mas podemos citar ainda duas outras abordagens de implementação de containers.

### Containers virtualizados

São implementações que usam KVM ou Xen para virtualizar um container. O principal uso é para aplicações que necessitam um maior isolamento em relação ao sistema hospedeiro, usando a virtualização de hardware como uma segunda camada de defesa e segurança, mas não se limita apenas a isso.

Alguns exemplos de runtime que usam virtualização são:

* [Frakti](https://github.com/kubernetes/frakti){:target="_blank"}
* [Kata Containers](https://katacontainers.io/){:target="_blank"}
* [Firecracker](https://firecracker-microvm.github.io/){:target="_blank"}

### gVisor

O [gVisor](https://gvisor.dev/){:target="_blank"} é um runtime que implementa o seu próprio Kernel para adicionar um nível extra de segurança, é como se o container executasse em uma camada sandbox, separada do Kernel Linux, mas ao mesmo tempo, sem ser uma máquina virtual.

## Conclusão

Containers é um assunto abrangente, impossível de cobrir tudo em apenas um artigo e como podemos observar, existem múltiplas formas de se fazer a mesma coisa.

Sabendo o básico do funcionamento e o quais camadas compõem, fica fácil dar continuidade nos estudos, mas traremos mais conteúdo no futuro para lhe ajudar a entender mais, não se preocupe.

Você já usa containers? Qual sua engine preferida? Deixe um comentário com sua opinião.
