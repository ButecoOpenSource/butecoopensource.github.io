---
layout: wordpress
title: Recortar arquivo de áudio no Linux pela linha de comando
date: 2014-09-09 23:01:02
author: marcossouza
permalink: /recortar-arquivo-de-audio-no-linux-pela-linha-de-comando/
categories:
  - Dicas
tags:
  - linux
  - terminal
---

Olá pessoa, segue uma dica para um problema que talvez alguns já tiveram. Ontem eu estava querendo colocar um novo toque no meu celular e eu queria cortar uma faixa de áudio, para que a música tivesse início no seu clímax. Então eu achei este post: <a title="Post" href="http://linux-software-news-tutorials.blogspot.com.br/2011/09/linux-cut-audio-files-directly-from.html">http://linux-software-news-tutorials.blogspot.com.br/2011/09/linux-cut-audio-files-directly-from.html</a>

Este post mostra como podemos fazer isto utilizando o <em>ffmpeg</em>, que é uma biblioteca para converter arquivos de video (pelo menos o que diz no man), mas que funciona também para editar arquivos de áudio.

Para atingir meu objeto, executei o seguinte comando:
<code></code>

[sourcecode language="bash"]
ffmpeg -ss 00:00:40 -t 00:01:15 -i caminho/para/arquivo.mp3 -acodec copy /caminho/para/novo/arquivo.mp3
[/sourcecode]

&nbsp;

Explicando cada parâmetro:

-i = arquivo de entrada do <em>ffmpeg</em>

-acodec copy = Diz qual o codec que deverá ser usado para criar o novo arquivo baseado no arquivo passado com o parâmetro -i. Neste caso, o parâmetro copy diz (ao que me parece) ao <em>ffmpeg</em> que o codec utilizado será o mesmo do arquivo original.

-ss = Tempo de início do recorte do áudio original

-t = Tempo de fim de recorte

Após esta execução, o arquivo de saída será o arquivo de origem, mas com o áudio recortado, sendo este apenas um trecho do áudio original.

Espero que esta dica possa ajudar alguns, da mesma forma como me ajudou!

Até mais!