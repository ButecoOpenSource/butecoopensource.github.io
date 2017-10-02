---
layout: wordpress
title: Conhecendo Pipe e FIFO (parte final)
excerpt: |
  Última parte da sequencia de artigos sobre pipes e fifos. Nesta parte, serão explicados como funcionam os fifos e como se diferenciam dos pipes.
date: 2015-03-16 07:40:21
author: marcossouza
permalink: /conhecendo-pipe-e-fifo-parte-final/
image: /assets/wp-content/uploads/2015/01/pipes.png
categories:
  - Desenvolvimento
tags:
  - api
  - c
  - linux
  - terminal
---

Esta é a última parte desta série de postagens que têm como foco explicar o funcionamento básicos de pipes e fifos no Linux. Se você não viu as primeiras duas partes, clique <a title="Parte 1" href="/2015/01/22/entendendo-pipe-e-fifo-parte-1/" target="_blank">aqui</a> e <a title="Parte 2" href="/2015/02/17/entendendo-pipe-e-fifo-parte-2/" target="_blank">aqui</a>.

Nesta postagem será explicado o funcionamento do fifo. Fifos funcionam da mesma forma que os pipes. Sua única diferença é que eles são criados no sistema de arquivos. Por serem objetos de um sistema de arquivo, o fifo deve ter um nome por onde deve ser acessado. Por esta razão o fifo é também comumente chamado de <em>named pipe</em>. Como o fifo se trata de um arquivo, isso permite que processos não afiliados podem utilizar o canal para trocar informações. Isto não era permitido com a utilização dos pipes, pois o fifo existia somente no contexto dos processos criados a partir do processo que criava o pipe.

Segue abaixo a verificação de um arquivo fifo no sistema de arquivos:

<pre><code class="bash">
[marcos@xfiles ~]$ ls -l meu_fifo
prw-rw-r-- 1 marcos marcos 0 Mar  7 14:25 meu_fifo
[marcos@xfiles ~]$ file meu_fifo
meu_fifo: fifo (named pipe)
</code></pre>

Podemos ver na execução do comando <em>ls</em> a letra <em>p</em> no início máscara de permissões do arquivo. Esta letra nos informa que o arquivo em questão se trata de um fifo. E ainda, executando o comando <em>file</em> podemos constatar o nome <em>named pipe</em> para o fifo.

A seguir serão mostrados dois programas, um que irá ler os dados enviados ao fifo, e outro que escreverá no fifo. Leitura:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/fifo/ler.c" type="text/javascript"></script>

Explicações sobre o código:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/fifo/ler.c?slice=12:15" type="text/javascript"></script>
Nesta parte, é verificada a existência do arquivo <em>meu_fifo</em> com a chamada stat. Se esta falhar, significa que o arquivo não existe, ou que não temos permissão para ler o arquivo. Se não existir o arquivo, a chamada <em>mkfifo</em> cria o fifo. Esta chamada recebe um caminho, e uma máscara para a criação do arquivo. Esta máscara é a mesma que utilizada na criação de arquivos simples.

O resto do código trata de operações normais de IO. O fifo é aberto para leitura, e a cada chamada <em>read</em>, ele fica bloqueado até ter dados. Quando existirem dados, estes são impressos no console. Se a chamada read retornar zero, significa que o lado que escreve no fifo fechou seu <em>file descriptor</em>. Este mesmo comportamento ocorre com sockets: quando um dos lados fecha o seu fd, o outro lado recebe zero na chamada read, sinalizando o fim da troca de dados.

Segue agora o código do programa que escreverá no fifo:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/fifo/escrever.c" type="text/javascript"></script>
Na parte de escrita, o programa em si é bem simples: Verifica a existência do fifo, abre o fifo como escrita, espera por entradas do usuário e as envia para o fifo.

Para compilar os programas, execute:
<strong>gcc ler.c -o ler
gcc escrever.c -o escrever</strong>

Segue abaixo os programas sendo executados:
<strong>[marcos@xfiles fifo]$ ./ler &amp;
[1] 11884
fifo meu_fifo previamente criado
[marcos@xfiles fifo]$ ./escrever
Teste
Lido: Teste
Novo Teste
Lido: Novo Teste
fifo
Lido: fifo
</strong>

Espero que tenham gostado desta sequência de artigos. Se houverem comentários ou dúvidas, coloquem estas nos comentários. Não se esqueça de se inscrever em nossas redes sociais. Até mais!

Referências:
<a href="http://linux.die.net/man/4/fifo" target="_blank">fifo</a>
<a href="http://linux.die.net/man/3/mkfifo" target="_blank">mkfifo</a>
<a href="http://linux.die.net/man/2/pipe" target="_blank">pipe</a>
<a href="http://linux.die.net/man/2/stat" target="_blank">stat</a>