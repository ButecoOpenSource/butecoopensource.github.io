---
layout: wordpress
title: "Linux API: pthreads - Parte 1"
excerpt: |
  Este post mostra uma introdução sobre a utilização de threads no ambiente Linux.
date: 2016-01-19 11:45:24
author: marcossouza
permalink: /linux-api-pthreads-parte-1/
image: /assets/wp-content/uploads/2016/01/pthreads1.png
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - posix
  - threads
---

Processadores de múltiplos núcleos já são uma realidade nos computadores da grande maioria dos usuários comuns. Em meio a esse avanço podemos escrever programas que executam várias linhas de processamento em paralelo, podendo fazer com que esses programas tenham um tempo de resposta menor.

Para tal, este post mostrará como utilizar POSIX threads na linguagem C.
<h4>O que são threads?</h4>
<em>Threads</em> são linhas de execução para processos. Ao iniciar um processo, uma <em>thread</em> principal é iniciada, um processo então pode criar outras <em>threads</em> para que estas executem tarefas específicas e de forma paralela. Quando temos uma CPU com um único núcleo, dizemos que as <em>threads</em> executam de forma <em>concorrente</em>, uma vez que a CPU só pode executar uma thread por vez, mas há mais que uma para ser executada ao "mesmo tempo". Já quando temos uma CPU com vários núcleos, as <em>threads</em> podem ser executadas tanto de forma <em>concorrente</em> como em <em>paralelo</em>, pois o <a href="https://pt.wikipedia.org/wiki/Escalonamento_de_processos" target="_blank"><em>scheduler</em></a> pode priorizar outros programas do computador além do seu.

<!--more-->

<h4>Para que são utilizadas?</h4>
Como dito anteriormente, as threads são utilizadas para fazerem tarefas de forma simultânea dentro do mesmo processo. Para exemplificar, imagine um servidor de <em>chat</em>. Você poderia fazer tudo rodar na mesma thread: identificar novos usuários conectados, receber mensagens destes usuários e enviar estas mensagens para os usuários online, identificar usuários que deixam o sistema, e etc. Nesse exemplo, podemos ver que este processo se torna custoso para uma única <em>thread</em> (<em>thread principal</em> nesse caso). Para tornar este processo mais otimizado, podemos criar uma <em>thread</em> para tratar as conexões ativas (usuários conectando e desconectando do servidor), e outra <em>thread</em> somente para receber as mensagens.
<h4>Porque o nome pthreads?</h4>
<em>POSIX threads</em>, aka <em>pthreads</em>, é um padrão definido para sistemas *NIX, tais qual BSD e Linux. Outros sistemas operacionais, como o Windows, tem sua própria API de <em>threads</em>.
<h4>Exemplo</h4>
Segue abaixo um exemplo simples da utilização de <em>pthreads</em> em código C. Podemos ver duas <em>threads</em> sendo criadas, fazendo somas, e no final a <em>thread</em> principal pegando o retorno destas <em>threads</em> e somando os dois resultados:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/pthreads/pthread1.c" type="text/javascript"></script>

Para compilar o código acima é necessário fazer o <em>link</em> com a <em>libpthread</em>:
<code>gcc pthread1.c -o pthread1 -lpthread</code>

Vamos ao código:
<code>pthread_t</code> é o identificador da <em>thread</em>, ou seja, é necessário utilizar este identificador para executar outras ações na <em>thread</em>, como o <em>join</em>(ver abaixo). Neste exemplo, criamos um <em>array</em> de <em>pthreads</em> com duas posições, pois teremos duas <em>threads</em>. Poderíamos ter criado duas variáveis ao invés do <em>array</em>, mas isto não muda o resultado final.

<code>pthread_create</code> é a função onde é criada uma nova <em>thread</em> de fato. Esta função recebe:
* <code>pthread_id</code>, que é o identificador da <em>thread</em> a ser criada
* <code>pthread_attr_t</code>, que é uma variável onde podemos setar alguns atributos para alterar o comportamento padrão da <em>thread</em>. Na maioria das vezes esse valor pode ser omitido, como no exemplo. Este assunto será abordado na parte dois do artigo.
* <code>void *(*start_routine) (void *)</code>, que é um ponteiro de função que será executada pela <em>thread</em>. A definição do parâmetro no <em>man page</em> parece ser meio confusa, mas é bem simples: É esperado um nome de função, mas esta função deve retornar um ponteiro <code>void</code>, e deve receber um ponteiro <code>void</code> como parâmetro. No nosso exemplo, criamos a função <code>func</code> que atende os requisitos acima. Como já descrito, a função só pode receber um único parâmetro, e se você deseja passar mais de um valor, basta criar uma <code>struct</code> e utilizar este como parâmetro.
* <code>void *arg</code>, que é o parâmetro que será passado a função. Como este parâmetro é um ponteiro <code>void</code>, ele pode ser qualquer coisa. Basta passar o valor e fazer um <em>cast</em> para <code>void *</code> e o valor será passado para a função quando ela iniciar.

Tudo isso parece um pouco complicado de início, mas vamos a um resumo disso tudo acima:
<code>pthread_create</code> vai criar uma nova <em>thread</em>, que irá executar uma função que retorna um ponteiro <code>void</code> (pode retornar qualquer tipo de valor, sendo <code>int</code>, ou até mesmo uma <code>struct</code>), e que recebe como parâmetro um ponteiro <code>void</code> (que pode ser um <code>int</code> ou até uma <code>struct</code>). Acredito que tenha ficado mais claro agora!

A chamada <code>pthread_create</code> retorna zero em caso de sucesso. Qualquer valor diferente de zero significa que houve um erro.

No exemplo criamos duas <em>threads</em>, passando valores diferentes para cada uma delas, e assim esperamos que cada uma delas retorne um valor diferente. As duas <em>threads</em> irão executar a função <code>func</code>, que soma 100 vezes o valor passado como parâmetro. Podemos ver aqui como um <code>int</code> sofre um <em>cast</em> para <code>void *</code> na chamada <code>pthread_create</code>, e novamente sofre outro <em>cast</em> dentro da função <code>func</code> para <code>int</code> novamente. Desta forma a função <code>pthread_create</code> pode receber qualquer tipo de dado como parâmetro.

Após a criação das duas <em>threads</em>, a <em>thread principal</em> continua seu fluxo. A fim de "esperar" que as duas <em>threads</em> iniciadas terminem, a chamada <code>pthread_join</code> é necessária.

<code>pthread_join</code> é responsável por "esperar" por uma <em>thread</em> acabar, ou se ela já acabou, a chamada retorna imediatamente. Os parâmetros são:
* <code>pthread_t</code>, que é o identificador da <em>thread</em>
* <code>void **retval</code>, que pede um endereço para um ponteiro void. Esse parâmetro recebe o retorno da <em>thread</em> em questão, nesse caso o valor do cálculo.

Da mesma forma que <code>pthread_create</code>, <code>pthread_join</code> também retorna zero em caso de sucesso, e outro valor em caso de erro.

Ao executar o programa do exemplo, a saída a seguir pode ser vista:
<pre>[marcos@localhost pthreads]$ ./pthread1
Resultado: 1100</pre>

Espero que tenham gostado desta primeira parte! Não esqueça de comentar, até mais!

Referências:
<a href="https://pt.wikipedia.org/wiki/Thread_(ci%C3%AAncia_da_computa%C3%A7%C3%A3o)" target="_blank">Wikipédia (BR) - Threads</a>
<a href="http://www.thegeekstuff.com/2012/03/linux-threads-intro/" target="_blank">The Gekk Stuff - Linux Threads Introduction</a>
<a href="http://man7.org/linux/man-pages/man7/pthreads.7.html" target="_blank">man pthreads</a>
<a href="http://man7.org/linux/man-pages/man3/pthread_create.3.html" target="_blank">pthread_create</a>
<a href="http://linux.die.net/man/3/pthread_join" target="_blank">man pthread_join</a>