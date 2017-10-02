---
layout: wordpress
title: "VIM tips: Mudando cor de destaque da busca"
excerpt: |
  Artigo que mostra como alterar as cores de destaque do VIM.
date: 2016-04-28 00:31:09
author: marcossouza
permalink: /vim-tips-mudando-cor-de-destaque-da-busca/
image: /assets/wp-content/uploads/2015/11/vim_logo_small.png
categories:
  - Dicas
tags:
  - cores
  - highlight
  - vim
  - vim-config
---

O VIM realmente é um canivete suíço dos editores de texto, sendo possível customizar praticamente todos as suas configurações, desde histórico de comandos até as cores de destaque ao fazer uma busca em um arquivo de texto.
<!--more-->

Ao fazeruma busca no editor, dependendo do tema do seu emulador de terminal (GNOME Terminal, Konsole, xterm) em relação a sua interface gráfica, esta busca pode dificultar um pouco o uso do VIM. A relação de cores quando se faz uma busca em um arquivo pode ficar desconfortável, uma vez que pode ter pouco contraste com a cor de fundo por exemplo. Como o VIM é extremamente customizável, é fácil de alterar o padrão de cores e a apresentação da string buscada.

A imagem abaixo mostra a edição de um arquivo C utilizando o VIM. O perfil de cores utilizado é o do tema do meu Fedora 23.

<a href="/assets/wp-content/uploads/2016/04/Screenshot-from-2016-04-20-23-28-08.png"><img class="alignnone size-full wp-image-5198" src="/assets/wp-content/uploads/2016/04/Screenshot-from-2016-04-20-23-28-08.png" alt="Screenshot from 2016-04-20 23-28-08" width="478" height="182" /></a>

Como podem ver, fiz uma busca pela string <strong>main</strong>. Digamos que eu queira mudar a cor amarela para verde, basta digitar o comando abaixo:

<code>:hi Search ctermfg=black ctermbg=green</code>

No comando acima, <strong>:hi</strong> é a forma abreviada de <strong>:highlight</strong>, <strong>ctermfg</strong> e <strong>ctermbg</strong> são as cores da letra e do fundo da expressão encontrada. Pela imagem vemos que o <strong>ctermfg</strong> está setado como <strong>black</strong> e <strong>ctermbg</strong> como <strong>yellow</strong>.

Além de cores, também é possível especificar números para algumas cores. Segue abaixo uma tabela simples de algumas cores para serem utilizadas nessas configurações:

<samp>black = 0
darkgray</samp>

<samp>darkred = brown = 1
red = lightred</samp>

<samp>darkgreen = 2
green = lightgreen</samp>

<samp>darkyellow = 3
yellow</samp>

<samp>darkblue = 4
blue = lightblue</samp>

<samp>darkmagenta = 5
magenta = lightmagenta</samp>

<samp>darkcyan = 6
cyan = lightcyan</samp>

<samp>gray = lightgray = 7
white</samp>

Além destas cores, ainda é possível alterar a formatação da expressão encontrada, como negrito, itálico, sublinhado. Segue abaixo uma imagem utilizando este recurso.

<a href="/assets/wp-content/uploads/2016/04/Screenshot-from-2016-04-20-23-47-31.png"><img class="alignnone size-full wp-image-5200" src="/assets/wp-content/uploads/2016/04/Screenshot-from-2016-04-20-23-47-31.png" alt="Screenshot from 2016-04-20 23-47-31" width="644" height="181" /></a>

A configuração <strong>cterm</strong> é quem define a formatação da string encontrada. No exemplo acima, estamos utilizando sublinhado, negrito e itálico. Ainda nesta configuração, é possível colocar <strong>reverse</strong>, que simplesmente troca as cores de <strong>ctermbg</strong> e <strong>ctermfg</strong>.

Espero que tenham gostado desta simples dica! Até a próxima!

Referências:

<a href="http://ubuntuforums.org/showthread.php?t=1830681" target="_blank">Cores VIM - ubuntuforums.org</a>
<a href="https://www.sbf5.com/~cduan/technical/vi/vi-4.shtml" target="_blank">Using Vim: Syntax Highlighting</a>