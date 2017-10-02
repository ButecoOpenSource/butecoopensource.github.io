---
layout: wordpress
title: "VIM Tips: Trabalhando com abas"
excerpt: |
  Comandos para criar e controlar abas dentro do VIM.
date: 2015-11-26 21:24:08
author: marcossouza
permalink: /vim-tips-trabalhando-com-abas/
image: /assets/wp-content/uploads/2015/11/vim_logo_small.png
categories:
  - Dicas
tags:
  - linux
  - terminal
  - vi
  - vim
  - vim tabs
---

O VIM, como todos sabem, tem muitas ferramentas por padrão que são pouco mostradas, ou até mesmo não são exploradas com todo o seu potencial. Essa série de artigos tem como foco mostrar algumas funcionalidades interessantes e as vezes pouco exploradas.

<!--more-->

Bom, vamos lá!

Primeiro, abra o seu VIM e edite um arquivo simples. Em seguida, digite <code>:tabnew</code> no <em>command</em>:

<a href="/assets/wp-content/uploads/2015/11/Screenshot-from-2015-11-24-23-37-10.png"><img class="aligncenter" src="/assets/wp-content/uploads/2015/11/Screenshot-from-2015-11-24-23-37-10.png" alt="VIM Tabs" width="50%" height="50%" /></a>

Como podemos ver, agora temos duas abas, cada uma com o nome do arquivo sendo editado. Para navegar entre as abas, basta digitar:

<code>gt</code> - Vai para a próxima aba, ao se for a última aba vai para a primeira
<code>Ctrl-PgDown</code> - mesma ação do gt
<code>gT</code> - Volta para a aba anterior, ou vai para a ultima se a aba corrente for a primeira
<code>Ctrl-PgUp</code> - mesma ação do gT
<code>{i}gt</code> - Vai para a aba <em>i</em>

Para fechar a aba:

<code>:tabc</code> fecha a aba corrent
<code>:tabclose</code> - mesma ação de tabc
<code>Ctrl-W c</code> - mesma ação de tabc
<code>:tabclose {i}</code> - fecha a aba <em>i</em>

Fora os comandos para fechar e abrir, existem alguns outros comandos para controlar e dar outras funcionalidades para as abas:

<code>:tab split</code> - copia conteúdo da aba atual para uma nova aba
<code>:tab help</code> - abre o help do VIM em uma nova aba

<strong>Dicas indicadas por leitores:</strong>
<code>vim arq1 arq2 arqN -p</code> - Abre multiplos arquivos, cada um deles uma aba (indicado por MDK)

Essas são as ações mais comuns que podem ser feitas em abas dentro do VIM, mas ainda existe muito para ser explorado.

Espero que gostem! E se quiserem mais dicas sobre o assunto, deixem nos comentários!

Até a próxima!

<strong>Referência</strong>

<a href="http://vim.wikia.com/wiki/Using_tab_pages" target="_blank">VIM Wiki</a>