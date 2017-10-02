---
layout: wordpress
title: Unity 5 vem com suporte a WebGL e você pode conferir alguns exemplos
excerpt: |
  Esta nova versão da mais popular ferramenta de desenvolvimento de jogos inclui uma prévia do exportador para WebGL. Os desenvolvedores de jogos estão a um passo de publicar os seus jogos para a Web de uma nova forma, tirando proveito do WebGL e do asm.js.
date: 2015-03-05 00:20:01
author: alexandrevicenzi
permalink: /unity-5-vem-com-suporte-a-webgl-e-voce-pode-conferir-alguns-exemplos/
image: /assets/wp-content/uploads/2015/03/Unity_3D_logo.png
categories:
  - Jogos
tags:
  - mozilla
  - unity
  - webgl
---

Recentemente comentamos sobre a <a href="/2015/02/28/unreal-engine-4-7-inclui-exportacao-para-html5/" target="_blank">Unreal Engine 4.7 incluir exportação para HTML5</a>. Desta vez quem está incluindo suporte a exportação para Web é o Unity 5.

Esta nova versão da mais popular ferramenta de desenvolvimento de jogos inclui uma prévia do exportador para WebGL. Os desenvolvedores de jogos estão a um passo de publicar os seus jogos para a Web de uma nova forma, tirando proveito do WebGL e do <a title="asm.js" href="http://asmjs.org/" target="_blank">asm.js</a>.

O resultado disto é uma aplicação com desempenho quase que idêntico ao nativo, sem a necessidade de nenhum plugin no browser. Confira abaixo o vídeo:

<iframe class="aligncenter" src="https://www.youtube.com/embed/2v6iLpY7j5M" width="560" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe>

A Mozilla e a equipe do Unity trabalharam juntas para encontrar uma forma de trazer o conteúdo desenvolvido no Unity 5 para a Web, utilizando apenas as bibliotecas padrão do JavaScript. Isto tudo é possível graças o uso em conjunto do IL2CPP e um <em>cross-compiler</em> chamado Emscripten.

Clique nas imagens abaixo para ver alguns exemplos jogáveis, todos foram gerados e exportados pelo Unity utilizando WebGL.

<a href="http://beta.unity3d.com/jonas/DT2/" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/03/Screenshot-20-252x142.png" alt="Dead Trigger 2" />
</a><a href="http://beta.unity3d.com/jonas/AngryBots/" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/03/Screenshot-33-252x142.png" alt="Angry Bots" />
</a><a href="http://www.dejobaan.com/awesome/" target="_blank">
<img class="aligncenter" src="/assets/wp-content/uploads/2015/03/Screenshot-31-252x142.png" alt="AaaaaAAaaaAAAaaAAAAaAAAAA for The Awesome!" />
</a>

Confira a nota de liberação oficial <a href="http://blogs.unity3d.com/2015/03/03/unity-5-launch/" target="_blank">aqui</a>.

Via <a href="https://blog.mozilla.org/blog/2015/03/03/unity-5-ships-and-brings-one-click-webgl-export-to-legions-of-game-developers/" target="_blank">Mozilla Blog</a>