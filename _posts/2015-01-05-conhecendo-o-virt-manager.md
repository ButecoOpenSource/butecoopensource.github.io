---
layout: wordpress
title: Conhecendo o virt-manager
date: 2015-01-05 08:00:45
author: marcossouza
permalink: /conhecendo-o-virt-manager/
categories:
  - Desenvolvimento
tags:
  - linux
  - virtualização
---

O virt-manager é uma ferramenta desenvolvida pela RedHat para gerenciar máquinas virtuais. Para quem já trabalhou com VMWare e VirtualBox, a interface do virt-manager é bem semelhante. A ferramenta foi construída sobre a <a href="https://en.wikipedia.org/wiki/Libvirt">libvirt</a>, que é uma ferramenta para gerenciar plataformas de virtualização. Por isso, o virt-manager tem suporte a uma série de plataformas de hypervisors, como por exemplo QEMU/KVM, LXC (linux containers), Xen, entre várias outras. Como podemos ver abaixo, o visual do virt-manager deixa claro que seu foco está na simplicidade e na facilidade do seu uso:

<a href="/assets/wp-content/uploads/2014/12/Captura-de-tela-de-2014-12-20-113455.png"><img class="aligncenter wp-image-537 size-full" src="/assets/wp-content/uploads/2014/12/Captura-de-tela-de-2014-12-20-113455.png" alt="virt-manager sendo executado" width="914" height="510" /></a>

Como pode-se verificar na imagem, no meu virt-manager está sendo executado uma máquina virtual com CentOS e outro Linux qualquer, que está desligado.

A imagem a seguir mostra quais as possíveis configurações que podem ser efetuadas no host do virt-manager:
<a href="/assets/wp-content/uploads/2014/12/Captura-de-tela-de-2014-12-20-114637.png"><img class="aligncenter size-large wp-image-540" src="/assets/wp-content/uploads/2014/12/Captura-de-tela-de-2014-12-20-114637-1024x771.png" alt="Captura de tela de 2014-12-20 11:46:37" width="640" height="481" /></a>

Entre as opções de configuração padrão visto em todos os gerenciadores de máquinas virtuais, podemos ver alguns recursos interessantes no virt-manager, como alterar o kernel Linux utilizado por uma VM. Este recurso se torna interessante se o usuário do virt-manager compilou um kernel linux com algumas opções extras e deseja verificar se algo pode acontecer errado ao utilizar este kernel em produção.

O virt-manager já contém um servidor VNC para acessar as máquinas, além do protocolo <a href="https://en.wikipedia.org/wiki/SPICE_%28protocol%29">Spice</a>.

Outros recursos possíveis na interface gráfica do virt-manager são: alterar a arquitetura do processador da máquina virtual, ativar/desativar menu de boot da VM, configurar VM para iniciar quando o sistema for iniciado, criar/gerenciar redes virtuais, entre várias outras possíveis configurações.

Além da interface gráfica do virt-manager, existem também ferramentas em linha de comando para criar/gerenciar máquinas virtuais. A principal ferramenta é o <em>virsh</em>, que é capaz de enviar comandos para máquinas virtuais iniciarem, desligarem, conectar com a serial virtual da máquina, listar as máquinas virtuais existentes, entre vários outros recursos.

Abaixo segue um print do virsh listando as máquinas virtuais instaladas:
<a href="/assets/wp-content/uploads/2015/01/Captura-de-tela-de-2014-12-20-144432.png"><img class="aligncenter size-full wp-image-545" src="/assets/wp-content/uploads/2015/01/Captura-de-tela-de-2014-12-20-144432.png" alt="Captura de tela de 2014-12-20 14:44:32" width="478" height="105" /></a>

Espero que tenham gostado deste resumo do virt-manager. Não se esqueçam de assinar o nosso feed e comentar a postagem. Até a próxima!