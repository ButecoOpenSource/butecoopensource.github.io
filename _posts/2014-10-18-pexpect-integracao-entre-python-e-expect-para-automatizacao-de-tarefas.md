---
layout: wordpress
title: "Pexpect: Integração entre Python e expect para automatização de tarefas"
date: 2014-10-18 10:03:28
author: marcossouza
permalink: /pexpect-integracao-entre-python-e-expect-para-automatizacao-de-tarefas/
categories:
  - Desenvolvimento
tags:
  - pexpect
  - python
---

Olá pessoa, este post é uma continuação do post sobre tcl/expect escrito previamente no blog. Se você perdeu este artigo, você pode vê-lo <a href="/tclexpect-automatizacao-de-comandos-interativos-no-linux">aqui</a>.

Tcl é uma linguagem de fácil aprendizado, mas tem suas limitações. A linguagem Python, além de ser muito mais popular que Tcl também tem muitas facilidades em sua linguagem que Tcl não suporta. Alguns trechos de código podem ficar muito mais simples em Python do que escritos em Tcl. Então este tutorial requer no mínimo um pouco de conhecimento na linguagem Python para poder aproveitar seu conteúdo.

O módulo Python que suporta script Tcl/expect se chama pexpect. Tanto este como os outros módulos citados no artigo anterior estão disponíveis nos repositórios de distribuições Linux. Após instalar o módulo pexpect basta dar o import no módulo para poder utilizá-lo. Recapitulando o exemplo de um ftp em Tcl:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/tcl_expect/telnet.exp" type="text/javascript"></script>

Este mesmo código pode ser feito em python da seguinte forma:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/pexpect/telnet.py" type="text/javascript"></script>

As diferenças começam na chamada do processo telnet pelo <em>spawn</em>. No caso do expect puro é feita uma chamada de <em>spawn</em> e todos os eventos de send e receive são feitos no escopo do novo processo criado. Já no pexpect vemos um objeto, neste exemplo chamado de <em>sp</em>, que é criado pela chamada spawn, e todas as chamadas de send e receive são feitas executando métodos deste objeto.

Algo que também difere entre o expect puro e pexpect é como podemos pegar a saída dos comandos executados no processo que foi disparado. No Tcl, existe a variável global chamada <em>expect_out</em> e esta é populada com a saída do comando executado. Já no pexpect existe um object chamado <em>match</em> que é criado quando o comando expect é retornado, e este contém uma lista das strings retornadas. No pexpect também existe outros dois atributos do object <em>spawn</em>, que são <em>after</em> e <em>before</em>. O primeiro atributo contém todo o output do processo após o último comando expect. Este comando se torna útil para encontrar algum erro na execução de comandos no processo. E o after mostra as strings que foram retornadas após o comando de expect.

Outra diferença básica entre o expect puro e o pexpect é a forma como ambos tratam o retorno da chama expect. No expect isto é feito com uma espécie de switch/case, e no pexpect isto é feito como uma lista de possíveis retornos. Veja primeiro um exemplo em expect puro:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/tcl_expect/multiplo.exp" type="text/javascript"></script>

Agora no pexpect podemos ver que um índice é retornado desta chamada, mostrando qual foi o padrão encontrado:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/pexpect/multiplo.py" type="text/javascript"></script>

Uma outra diferença é que no pexpect o tempo limite para espera no pexpect é definido como o segundo parâmetro, e se este não for definido será utilizado o valor padrão de 30 segundos. Já no puro expect temos uma variável global chamada timeout, e esta deve ser setada para informar o tempo limite de espera da chamada expect. Ao setar o valor de timeout como -1 a chamada expect não terá um tempo limite.

A fim de exemplificar o pexpect vamos converter o script em expect para efetuar uma conexão SSH. Primeiro o script em expect:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/tcl_expect/ssh.exp" type="text/javascript"></script>

Agora o mesmo script convertido para pexpect:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/pexpect/ssh.py" type="text/javascript"></script>

No pexpect foi criado o loop para não ser necessário escrever duas vezes uma instrução expect, facilitando assim a codificação. O único ponto novo neste exemplo é a presença do interact, que agora é um método da classe <em>spawn</em> no pexpect, enquanto no expect puro vemos que ele faz o interact com o escopo do novo processo.

Com este tutorial podemos ver que o módulo pexpect é o mais indicado para programadores com familiaridade com programação orientada a objetos, enquanto Tcl é mais indicado para quem tem mais familiaridade com script shell, como bash, csh e outros.

Tanto Tcl/expect quanto o módulo pexpect do Python podem oferecer muitas outras possibilidades. Se você deseja aprender mais basta ir na documentação de cada projeto. Uma fonte muito boa sobre pexpect é este link do <a href="http://pexpect.sourceforge.net/pexpect.html">sourceforge</a>.

Espero que tenham gostado deste novo artigo. Não se esqueçam de se inscrever no nosso feed e deixar comentários no post. Até a próxima!
