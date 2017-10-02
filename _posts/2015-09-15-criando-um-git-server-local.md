---
layout: wordpress
title: Criando um git server local
excerpt: |
  Mini tutorial de como criar um servidor git local.
date: 2015-09-15 00:35:22
author: marcossouza
permalink: /criando-um-git-server-local/
image: /assets/wp-content/uploads/2014/11/Git-Icon-1788C.png
categories:
  - Dicas
tags:
  - git
  - linux
  - terminal
---

Algumas vezes queremos ter um ponto comum em uma rede local onde podemos enviar nossos <em>commits</em>, especialmente quando estamos trabalhando em equipe. Pois bem, a solução é simples.

<!--more-->

Para tal feito, basta ter uma máquina Linux com <em>sshd</em> rodando e git instalado. Feito isto, vá até um local onde queira criar o repositório, podendo ser em um $HOME de um usuário mesmo:
<code>mkdir /home/fulano/meu_projeto.git
cd /home/fulano/meu_projeto.git</code>

Além do famoso git init, é preciso um parâmetro adicional:
<code>git init --bare</code>

Com este comando o git cria um repositório "nú". Ao executar o <em>git init</em>, este repositório se torna um <em>working directory</em>. Esse tipo de repositório tem um diretório <em>.git</em> onde uma cópia dos arquivos da pasta do projeto e todas as configurações são guardadas.

Já nos "repositórios nús", os arquivos de configuração são colocados na própria pasta raiz do projeto ao invés da pasta <em>.git</em>, e com isso não existe uma <em>working tree</em>, com uma cópia dos seus arquivos lá dentro.

Para poder acessar os arquivos do seu novo repositório, basta executar:
<code>git clone fulano@ip_do_git_server:/home/fulano/meu_projeto</code>

O git utiliza o protocolo SSH para fazer as transferências de <em>commits</em>, então basta você informar a senha do usuário do SSH e tudo funcionará.

Ao fazer git push você também precisa informar a senha do usuário do SSH. Mas para evitar, basta executar um <em>ssh-copy-id</em>, assim, não será necessário informar a senha em cada <em>push</em>.

Espero que este artigo tenha sido útil para você! Dúvidas, críticas ou sugestões, favor informar nos comentários.

Até a próxima!

Referências:
<a href="https://www.kernel.org/pub/software/scm/git/docs/git-init.html" target="_blank">Git init manual</a>
<a href="http://linux.die.net/man/1/ssh-copy-id" target="_blank">ssh-copy-id manual</a>