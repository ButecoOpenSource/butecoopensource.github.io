---
layout: wordpress
title: "Tcl/Expect: Automatização de comandos interativos no Linux"
date: 2014-10-07 00:23:49
author: marcossouza
permalink: /tclexpect-automatizacao-de-comandos-interativos-no-linux/
categories:
  - Desenvolvimento
tags:
  - expect
  - linux
  - script
  - tcl
  - terminal
---

Olá pessoal, neste artigo será abordado a automatização de comandos com o <em>Tcl/expect</em>. Tcl é, segundo a Wikipédia, uma linguagem de script para rápida prototipação. Tcl significa <em>Tool Command Language</em>, e foi criada no ano de 1988 por John Ousterhout. Para mais informações sobre Tcl, sua origem ou outros dados, você pode verificar <a href="https://en.wikipedia.org/wiki/Tcl">aqui.</a> Seu aprendizado é bem simples, sendo que, ao meu ver, é uma linguagem parecida com Bash e Python. Uma exemplo de Hello World com ela pode ser feito com:

[code languagem="ruby"]

puts &quot;Hello World!&quot;

</code></pre>

Para executar comandos Tcl, será necessário instalar o interpretador Tcl. Atualmente todas as maiores distribuições Linux contém o Tcl em seus repositórios. Existem muitos exemplos de como usar Tcl. Você pode ver alguns deles neste link do <a href="http://en.wikibooks.org/wiki/Tcl_Programming/Examples">Wikibooks.</a>

<em>Expect</em> é uma extensão da linguagem Tcl para automatizar interações com programas em modo texto. Este foi escrito por Don Libes em 1990, e inicialmente foi escrito para ser executado em sistemas UNIX e para poder controlar programas interativos como o ftp, ssh, telnet e vários outros. Para mais informações veja link da <a href="https://en.wikipedia.org/wiki/Expect">Wikipédia.</a> Como o Tcl, o interpretador expect também precisa ser instalado. Este também está nos repositórios das distribuições Linux.

Sua facilidade de controlar programas interativos se deve ao fato do Expect poder executar um programa e manter uma espécie de "handler" desse programa. Este handler se chama <em>spawn_id</em>. Com este <em>spawn_id </em>o programador consegue enviar comandos e também esperar por padrões de saída do programa. Como primeiro exemplo será mostrado um telnet, onde interativamente precisamos informar usuário e senha, e neste caso será automatizado pelo Expect:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/tcl_expect/telnet.exp" type="text/javascript"></script>

A variável global <em>timeout</em> diz respeito a quanto tempo cada chamada do comando Expect vai esperar pelo retorno especificado. Colocando este como -1 remove a restrição de tempo do comando <em>expect. </em>Já o comando <em>send</em> envia comandos ao processo, como se fosse o próprio usuário digitando no terminal.

Como você pode ver, com esta combinação de comandos um programador pode controlar qualquer programa de terminal por um script <em>expect.</em> Ao buscar no google por exemplos em <em>Expect</em>, um dos seus usos mais comuns é para fazer uma conexão SSH.

Um outro comando interessante do <em>Expect</em> é o <em>interact</em>. Este comando basicamente entrega ao usuário o programa executado pelo expect. Um exemplo deste pode ser mostrado com uma conexão SSH, onde temos um usuário pré-configurado e ao fazer o login o prompt do SSH é mostrado ao usuário para que este possa executar comando no host remoto.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/tcl_expect/ssh.exp" type="text/javascript"></script>

Nó código acima podemos ver uma função de Tcl/Expect para criar uma conexão SSH. No Tcl os parâmetros não tem tipos, são tratados como strings. Após enviar a senha para o usuário especificado na conexão, a função executa o comando <em>interact</em>. Após este comando, o usuário pode digitar normalmente no terminal dentro da sessão de SSH remota.

Espero ter abordado o <em>Tcl/Expect </em>com a simplicidade que este de fato tem, e ajudado a facilitarem suas vidas com esta linguagem :)

No próximo artigo pretendo escrever sobre <em>pexpect</em>, que é a integração do Python com <em>Expect</em>, deixando este trabalho ainda mais simples! Não se esquecem de assinar o nosso feed e ficar por dentro dos nossos próximos artigos. Até mais!