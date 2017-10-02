---
layout: wordpress
title: Introduzindo conceitos do Emacs
date: 2015-12-09 07:46:43
author: marcooliveira
permalink: /introduzindo-conceitos-do-emacs/
image: /assets/wp-content/uploads/2015/12/Emacs-Logo-400x400.png
categories:
  - Desenvolvimento
  - Dicas
tags:
  - dica
  - dicas
  - emacs
  - ide
  - tutorial
---

Utilizo o Emacs há algum tempo, pelo menos como ferramenta de desenvolvimento acho uma das melhores opções, onde, diferente de outras, é fácil fazer o desenvolvimento e estender suas funcionalidades, criar novas <em>hotkeys</em>. Tentarei demonstrar aqui, um básico das funcionalidades do Emacs.

<!--more-->

O primeiro passo, para aprender Emacs é entender um pouco das notações das teclas de atalho para entender tutorias, livros de referência:

<code>C</code>: Control

<code>M</code>: Alt (Meta)

<code>C-b</code>: Control + b (volta uma palavra dentro de um <em>buffer</em>)

<code>M-g g</code>: Alt + g, seguido da tecla g (<em>go-to-line</em>)

<code>C-h r</code>: Control + h, seguido da tecla r (abre o manual do emacs)

<code>C-x C-c</code>: Control + x, seguido de Control + c (fecha o emacs)

É importante perceber que existe uma diferença entre M-g

Uma tecla muito importante caso você se perca ao utilizar o Emacs é o f10, a tecla f10 vai para o menu visual do Emacs o qual você pode navegar nas funções básicas dele. Outra tecla importante é a tecla de fuga... digamos que você está digitando alguma <em>hotkey</em> ou comando e não sabe o que ocorreu ou quer desistir, você pode pressionar <code>Esc</code> três vezes ou apertar <code>C-g</code> (<em>signal quit</em>).

<a href="/assets/wp-content/uploads/2015/12/menuf10.png"><img class="aligncenter size-full wp-image-4259" src="/assets/wp-content/uploads/2015/12/menuf10.png" alt="menuf10" width="626" height="742" /></a>

No entanto, um dos pontos mais importantes ao lidar com uma IDE é saber desenvolver a evoluir com a sua ferramenta de desenvolvimento, neste quesito é importante como conseguir ajuda nela, e entender seus comandos para poder criar suas próprias teclas de atalho, ou mesmo "scriptar" sequências de comandos.

Então "go to help"

<code>C-h r</code>: abre o manual do emacs

<code>C-h t</code>: abre o tutorial do emacs

<code>C-h i</code>: abre a lista de manuais do emacs

Você vai perceber que é natural navegar nos manuais, pois todos possuem <em>hiperlinks</em> para outras páginas onde você consegue navegar com as flechas e pressionar <code>Enter</code>, onde leva a outros textos. Uma maneira prática para navegar entre os <em>links</em> é ir pressionando <code>Tab</code>, que ele vai avançando entre os <em>links</em>.

As vezes nem percebemos, mas estamos usando algumas das <em>hotkeys</em> do Emacs no BASH, visto que as <em>hotkeys</em> deles são idênticas ou similares. Exemplo

<code>C-a</code>: vai para o início da linha

<code>C-e</code>: vai para o final de linha

<code>M-f</code>: avança uma palavra

<code>M-b</code>: volta uma palavra

<code>C-r</code>: faz busca reversa nos comandos (no emacs faz busca de palavras reversa)

<code>C-k</code>: copia a linha

<code>C-y</code>: cola a linha copiada

Gente O_O todos estes comandos funcionam no BASH, não somente dentro do programa Emacs, mas já que podem usar no Emacs porque não estender e dar um passeio neste programa e ver algumas das coisas divertidas dele como <em>buffers</em> :). Primeiro de tudo, no Emacs, cada janela é vinculada a um <em>buffer</em>. O <em>buffer</em> como podemos dizer uma região de memória associada a um conjunto de texto dentro do emacs se fosse uma maneira simples por assim dizer o que ele seria, várias janelas podem estar vinculadas a um mesmo <em>buffer</em> o_o .. <em>buffers</em> o melhor é testar.

Sugestão XD, abra o Emacs sem modo gráfico geralmente conhecido nas distribuições como Emacs-nox. Primeiro de tudo, importante listarmos os <em>buffers</em> do sistema para isto você pode pressionar a tecla de atalho:

<code>C-x C-b</code>: lista todos os <em>buffers</em> no *Buffer list* em uma nova janela

<code>C-x b</code>: chama a linha de comando para completarmos com o buffer que queremos selecionar. A tecla <code>Tab</code> funciona aqui para completar com os outros <em>buffers</em> disponíveis.

<code>C-x esquerda</code>: vai para o buffer anterior

<code>C-x direita</code>: vai para o próximo buffer

<code>C-x k</code>: mata o buffer

Ao listar todos os <em>buffers</em>, podemos navegar com as setas do teclado e escolher o <em>buffer</em> que vamos usar.

No entanto qual a graça de brincar com os <em>buffers</em> se não usar o <em>splits</em> de janelas e trabalhar com múltiplos <em>buffers</em> :). Então vamos aprender um pouco sobre como quebrar as janelas para multi visões.

<code>C-x 3</code> - quebra a tela na vertical

<code>C-x 4</code> - quebra na horizontal

<code>C-x 0</code> - deleta a janela atual

<code>C-x 1</code> - deleta todas as janelas menos a atual

<a href="/assets/wp-content/uploads/2015/12/buffer-window.png"><img class="aligncenter size-full wp-image-4268" src="/assets/wp-content/uploads/2015/12/buffer-window.png" alt="buffer-window" width="1358" height="734" /></a>

&nbsp;

Como uma introdução sobre o assunto acho que ficou longo até, mas espero conseguir auxiliar os iniciantes sobre esta ferramenta a dar os primeiros passos, na sequência a intenção é postar novos dicas, sobre o uso do Emacs.

Referências:

<a href="http://www.gnu.org/software/emacs/manual/html_node/emacs/Buffers.html" target="_blank">Using Multiple Buffers</a>