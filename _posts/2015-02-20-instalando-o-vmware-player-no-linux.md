---
layout: wordpress
title: Instalando o VMware Player no Linux
excerpt: |
  O VMware é um software/máquina virtual que permite a instalação e utilização de um sistema operacional dentro de outro, dando suporte real a software de outros sistemas.
  Se você, assim como eu, acha que instalar o VMware no Linux é algo complicado, você verá neste tutorial que é algo bem simples de ser feito.
date: 2015-02-20 14:09:32
author: alexandrevicenzi
permalink: /instalando-o-vmware-player-no-linux/
image: /assets/wp-content/uploads/2015/02/VMware_Player_logo.png
categories:
  - Dicas
tags:
  - linux
  - vitualização
  - vmplayer
  - vmware
---

O <a href="http://www.vmware.com/br/products/player/" target="_blank">VMware</a> é um software/máquina virtual que permite a instalação e utilização de um sistema operacional dentro de outro, dando suporte real a software de outros sistemas.

Se você, assim como eu, acha que instalar o VMware no Linux é algo complicado, você verá neste tutorial que é algo bem simples de ser feito.

Apesar do VMware ser um software proprietário, a versão VMware Player pode ser usada gratuitamente, basta fazer um registro após a instalação.

<strong>Download</strong>

Você pode fazer o download do VMware Player <a href="https://my.vmware.com/web/vmware/free#desktop_end_user_computing/vmware_player/7_0" target="_blank">aqui</a>.

<strong>Instalação</strong>

Após feito o download, você deverá ter um arquivo com o nome semelhante a <em>VMware-Player-7.0.0-2305329.x86_64.bundle</em>.

Necessitamos tornar este arquivo um executável, para isto execute o comando abaixo:

<code>chmod 777 VMware-Player-7.0.0-2305329.x86_64.bundle</code>

Após isto execute o comando abaixo para instalação:

<code>sudo ./VMware-Player-7.0.0-2305329.x86_64.bundle</code>

Agora você deverá ver algo semelhante a:

<code>Extracting VMware Installer...done.
You must accept the VMware Player End User License Agreement to
continue. Press Enter to proceed.</code>

Ao chegar ao fim da licença você deverá responder se aceita-a ou não. Conforme abaixo:

<code>Do you agree? [yes/no]: yes</code>

Após aceitar a licença serão feitas outras questões referentes ao produto. Conforme abaixo:

<code>Would you like to check for product updates on startup? [yes]: yes</code>

Would you like to help make VMware software better by sending
anonymous system data and usage statistics to VMware? [yes]: yes

Responda de acordo com suas necessidades.

Antes de inciar a instalação será questionado se você possui uma chave de uso:

<code>Enter license key. (optional) You can enter this information later.: </code>

Deixe em branco.

Agora será iniciada a instalação.

<code>The product is ready to be installed. Press Enter to begin
installation or Ctrl-C to cancel.</code>

Pressione <strong>Enter</strong>. Se tudo ocorrer bem durante a instalação você deverá ver a seguinte mensagem no fim da instalação.

<code>Installation was successful.</code>

Após instalado basta executar o comando abaixo para executá-lo:

<code>vmplayer</code>

Na primeira execução após a instalação será questionado sobre a chave de uso. Como o intuito do nosso uso é apenas para fins pessoais escolheremos a primeira opção.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/02/vmware-key.png" alt="VMware Chave de Uso" />

Informe o seu e-mail e clique em <strong>OK</strong>.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/02/vmware-install.png" alt="VMware Instalação Terminada" />

Pronto! Agora o VMware está pronto para uso.