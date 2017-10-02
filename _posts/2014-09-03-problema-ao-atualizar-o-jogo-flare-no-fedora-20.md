---
layout: wordpress
title: Problema ao atualizar o jogo Flare no Fedora 20
date: 2014-09-03 02:01:55
author: marcossouza
permalink: /problema-ao-atualizar-o-jogo-flare-no-fedora-20/
categories:
  - Jogos
tags:
  - fedora
  - flare
  - linux
---

Olá pessoal, como primeiro post deste blog eu gostaria de falar sobre a minha experiência resolvendo um problema que tive hoje mesmo no Fedora 20!

Após fazer um <em>yum update</em> no meu Fedora 20, vi que o jogo Flare foi atualizado, e então resolvi abrir para ver se percebia algo diferente no jogo. Acontece que o item de menu do jogo havia sumido do menu do Mate. Então executei pela linha de comando (digitei <em>flare</em> no terminal) e não consegui jogar. O botão "Play Game" estava desabilitado, e aparecia uma mensagem falando que era necessário pelo menos um <em>mod</em> do jogo estar habilitado. Ao entrar no menu "Configurations" eu vi que não existia nenhum <em>mod </em> para ser habilitado. Então eu abri um bug para verificar o problema: <a href="https://bugzilla.redhat.com/show_bug.cgi?id=1136498">https://bugzilla.redhat.com/show_bug.cgi?id=1136498</a>

Acontece que para executar o jogo pela linha de comando é necessário passar parâmetros, e passando estes o problema é resolvido, fazendo o programa encontrar os <em>mods</em> padrões do jogo e os habilitando. Mas o problema do ícone ter sumido ainda existia, e conforme um comentário no bug acima, existe ainda este erro.

Então enviei um email para o Erik, pessoa que respondeu muito rapidamente ao bug, se eu poderia ajudar a resolver o problema do ícone e ele então me indicou que eu poderia verificar o arquivo .desktop do jogo <em>flare</em> no caminho: <em>/usr/share/applications/flare.desktop . </em>Segundo ele, se este arquivo arquivo tivesse algum problema o ícone do jogo não iria aparecer no menu.

Após alterar o arquivo <em>flare.desktop</em> algumas vezes e ficar verificando se o jogo aparecia no menu, verifiquei que ao remover os argumentos da linha <em>TryExec</em> do arquivo faziam o jogo aparecer no menu!

Segue trecho do arquivo com problemas:

TryExec=/usr/bin/flare "--game=flare-game"

Ao informar Erik, o mantenedor do pacote, sobre como resolvi o problema este me disse que já havia executado o programa desktop-file-validator no arquivo <em>flare.desktop</em>, e que este não acusou nenhum erro. Então fiz um patch removendo "--game=flare-game" da entrada <em>TryExec</em>, somente deixando o caminho para o binário e enviei ao Erik.

Ele também falou que eu poderia abrir um bug quanto ao pacote <em>desktop-file-utils </em>não validar os argumentos do <em>TryExec</em>, e então eu abri mais este bug: <a href="https://bugzilla.redhat.com/show_bug.cgi?id=1136597">https://bugzilla.redhat.com/show_bug.cgi?id=1136597</a>

Vou esperar pela resposta do Erik sobre meu patch, e se por acaso este for incluído no repositório do Fedora eu ficarei muito feliz. Vamos esperar a resposta!

Então você já sabe, se algum aplicativo ou jogo seu sumir do menu, pode ser algum problema no arquivo <em>.desktop</em> do programa.

Até mais pessoal!