---
layout: wordpress
title: Gistfy - Uma forma fácil de criar Gists a partir de repositórios do GitHub e Bitbucket
date: 2014-09-24 15:17:18
author: alexandrevicenzi
permalink: /gistfy-uma-forma-facil-de-criar-gists-a-partir-de-repositorios-do-github-e-bitbucket/
categories:
  - Ferramentas
tags:
  - gist
  - gistfy
  - github
---

Estes dias tive um problema, eu necessitava adicionar um trecho de código do GitHub a uma página, mas este código estava em um repositório e não em um Gist.
Particularmente eu não gosto muito de criar Gists, e como o GitHub não oferece uma forma de criar um Gist a partir de um repositório eu resolvi criar a minha própria ferramenta.

A partir desta necessidade eu criei o <a href="//gistfy-app.herokuapp.com">Gistfy</a>. A ideia e o projeto são simples, mas cumpre o que promete.

Na <a href="//gistfy-app.herokuapp.com/#usage">documentação</a> você pode encontrar exemplos de códigos em <a href="https://angularjs.org/">AngularJS</a>, <a href="http://jquery.com/">jQuery</a> e <a href="http://www.w3schools.com/tags/tag_script.asp">HTML</a>.

Como você pode observar na imagem abaixo o snippet é semelhante a um Gist do GitHub:

<img src="//i.imgur.com/5x0exhk.png" alt="exemplo" />

Para usar basta adicionar esta linha a sua página (substitua os dados pelos seus):

<pre><code class="html">

&lt;script type=&quot;text/javascript&quot; src=&quot;//gistfy-app.herokuapp.com/github/isagalaev/highlight.js/test/detect/python/default.txt?lang=python&quot;&gt;&lt;/script&gt;

</code></pre>

Você pode criar o seu próprio servidor com o pacote <a href="https://www.npmjs.org/package/gistfy">npm</a>.

Não esqueça de deixar seu comentário.