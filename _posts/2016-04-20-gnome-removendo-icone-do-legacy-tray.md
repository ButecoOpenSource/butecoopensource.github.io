---
layout: wordpress
title: "GNOME: Removendo ícone do legacy tray"
excerpt: |
  O GNOME 3.16 introduziu um novo sistema de notificação, muito melhor que o antigo por sinal, porém com ele também veio um problema. O “legacy tray”, que permite que aplicativos que ainda utilizam o sistema de notificações antigo do GNOME é extremamente irritante.
date: 2016-04-20 23:16:52
author: alexandrevicenzi
permalink: /gnome-removendo-icone-do-legacy-tray/
image: /assets/wp-content/uploads/2016/04/gnome-logo-300px-150x150.png
categories:
  - Dicas
tags:
  - gnome
  - linux
  - tray
---

No GNOME 3.16 foi introduzido <a href="https://help.gnome.org/misc/release-notes/3.16/" target="_blank">um novo sistema de notificação</a>, muito melhor que o antigo por sinal, porém com ele também veio um problema. O "legacy tray", que permite que aplicativos que ainda utilizam o sistema de notificações antigo do GNOME é extremamente irritante.

<!--more-->

Você pode ter uma dor de cabeça ao instalar aplicativos como Skype ou Dropbox, conforme mostrado na imagem abaixo.

<img src="/assets/wp-content/uploads/2016/04/gnome316-tray-icons-300x183.png" alt="gnome316-tray-icons" width="300" height="183" class="aligncenter size-medium wp-image-5181" />

Este ícone no canto esquerdo do monitor é incomodo. Porém, existe uma solução extremamente simples para remover este ícone do "legacy tray" e jogá-lo na "top bar". A solução se chama <a href="https://github.com/wincinderith/topicons" target="_blank">Top Icons</a> e você pode acompanhar como instalá-la.

<strong>Instalação</strong>

Faça o download do projeto e execute o instalador conforma abaixo.

<pre><code class="bash">
wget https://github.com/wincinderith/topicons/archive/master.zip
unzip master.zip
cd topicons-master
make install
</code></pre>

Após instalar, é necessário reiniciar o GNOME Shell, para isso aperte as teclas <kbd>Alt</kbd> + <kbd>F2</kbd> e digite <code>r</code>.

Após abra o <a href="https://wiki.gnome.org/action/show/Apps/GnomeTweakTool?action=show&redirect=GnomeTweakTool" target="_blank">Tweak Tool</a>, vá até a aba de Extensões e habilite o Top Icons.

Pronto! O ícone irá aparecer magicamente na barra superior.