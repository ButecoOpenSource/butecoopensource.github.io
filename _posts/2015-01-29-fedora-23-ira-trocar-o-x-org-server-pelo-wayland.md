---
layout: wordpress
title: Fedora 23 irá trocar o X.Org Server pelo Wayland
date: 2015-01-29 06:24:08
author: marcossouza
permalink: /fedora-23-ira-trocar-o-x-org-server-pelo-wayland/
image: /assets/wp-content/uploads/2015/01/7b5b9071afbe94c1cfff78b1ce5721e5.png
categories:
  - Notícias
tags:
  - fedora
  - linux
  - testes
---

Enquanto muito se falava em trocar o X.Org Sever pelo Wayland como sendo algo distante, parece que o Fedora 23 irá fazer acontecer.

O Fedora 23 já tinha algumas metas ambiciosas, como ter seu suporte somente para 64-bits, e agora desejam utilizar o Wayland como servidor gráfico padrão. No Fedora 21 o Wayland já estava presente no Fedora Workstation, mas ainda dependente do X.Org Server. No Fedora 22 a experiência com o Wayland será melhor, e finalmente no Fedora 23 irá ser feita a troca.

Mathias Clasen da Red Hat escreveu uma postagem em seu blog intitulada "GNOME Wayland porting - the endgame" (O port do Wayland no GNOME, fim de jogo). Este post fala sobre as inúmeras características do Wayland que irão aparecer em breve nas builds de desenvolvimento do GNOME, sobre as características restantes do X.Org Server que precisam ser implementadas no Wayland e etc. Uma importante meta do Fedora 22 é a utilização do Wayland na tela de login. Utilizando o Wayland como tela de login do GNOME irá expô-lo a diferentes tipos de drivers/dispositivos, além de expor possíveis bugs antes da efetiva troca.

Após o lançamento do Fedora 22, o Wayland será ativado por padrão no Fedora Rawhide, o que significa que Wayland será padrão no Fedora 23, se nada der errado no *Rawhide. Portanto pelo calendário de liberação, poderemos ver o Fedora 23 com o Wayland antes do fim deste ano. Fedora 23 com Wayland irá "brigar de frente" com o Ubuntu 15, uma vez que este poderá vir com o novo Unity 8 e utilizar o Mir como servidor gráfico no desktop.

* Rawhide é a versão de desenvolvimento do Fedora. Uma vez que uma versão é lançada, um Rawhide é criado para que os desenvolvedores e testadores possam ir pegando erros até que este fique estável o bastante para o lançamento da próxima versão.

Via <a title="Phoronix" href="http://www.phoronix.com/scan.php?page=news_item&amp;px=Fedora-23-Wayland-Xorg-Plans" target="_blank">Phoronix</a>