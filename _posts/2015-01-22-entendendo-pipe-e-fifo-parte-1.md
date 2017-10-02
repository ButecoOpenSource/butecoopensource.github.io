---
layout: wordpress
title: Entendendo Pipe e FIFO (parte 1)
date: 2015-01-22 22:20:52
author: marcossouza
permalink: /entendendo-pipe-e-fifo-parte-1/
image: /assets/wp-content/uploads/2015/01/pipes.png
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - terminal
---

<p style="text-align: justify;">Pipes e FIFOs são muito utilizados no mundo Linux como um método de IPC (inter process communication), ou comunicação entre processos. Muitas das vezes nem percebemos que estamos usando-os pela sua facilidade. Normalmente usamos pipes no shell, como no comando abaixo:</p>
<em>ls | wc -l</em>
<p style="text-align: justify;">Neste comando, o shell executa o comando <em>ls</em>, pegando todo o conteúdo de saída e o direciona para a entrada do processo <em>wc,</em> que é criado logo em seguida, tudo de um jeito simples de escrever.</p>
<p style="text-align: justify;">Pipes na verdade agem como "canos" que conectam processos unidirecionalmente. Ou seja, todo o pipe tem um lado que escreve dados e outro que lê estes dados. Vejamos o código abaixo onde mostramos onde dois processos leem e escrevem no pipe recém-criado:</p>
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/pipe_fifo/pipe.c" type="text/javascript"></script>
<p style="text-align: justify;">É um código um pouco extenso de começo, mas após a explicação ele se torna de fácil leitura. Aqui podemos verificar que a chamada de sistema <em>pipe</em> é executada, recebendo como parâmetro um array de inteiros de duas posições. Se a chamada for executada com sucesso, o array de inteiros terá dois <em>files descriptors</em> para o pipe. A posição zero do array contém o <em>fd</em> de leitura do pipe, e a posição um contém o <em>fd</em> de escrita.</p>
<p style="text-align: justify;">Podemos verificar que após a chamada pipe ser executada, um <em>fork</em> é feito. O fork nada mais é que a criação de um novo processo, onde este novo processo começa a executar do ponto em que foi executado o fork. O retorno da chamada fork é utilizado para identificar qual processo é o pai e qual é o filho. Desta forma um <em>switch-case</em> é utilizado para separar os trechos de código que devem ser executados pelo processo pai e processo filho. Neste momento não é possível saber qual dos dois processos irá executar primeiro, pois os dois são concorrentes perante a CPU.</p>
<p style="text-align: justify;">Explicado o fork, podemos nos atrelar ao real funcionamento do exemplo, onde o processo pai irá escrever uma mensagem no pipe, e esta mensagem deve ser lida pelo processo filho. Após o fork, o processo pai fecha o <em>file descriptor</em> de leitura, e o processo filho fecha o <em>file descriptor</em> de escrita, uma vez que o processo pai somente irá escrever no pipe e o processo filho irá fazer a leitura. Neste ponto, o processo filho executa a chamada <em>read</em> que lê dados do <em>file descriptor</em> de leitura do pipe, e então o processo filho fica esperando por dados a serem lidos. Ao mesmo tempo, o processo pai escreve uma mensagem utilizando o <em>file descriptor</em> de escrita utilizando a chamada de sistema <em>write</em>.</p>
<p style="text-align: justify;">Toda esta informação junta pode dar uma certa confusão no inicial. Para fins de simplificar o exemplo, abaixo consta como compilar e executar o programa, e a saída do mesmo.</p>
Para compilar, invocamos o GCC:
<strong>gcc pipe.c -Wall -o pipe</strong>

Execuntado e mostrando a saída do exemplo:<strong>
marcos@localhost: [pipe_fifo] # ./pipe
Parent wrote the message!
Child readed: Hello from parent! Have a long life!</strong>

Você pode alterar o código e verificar a saída do mesmo para um melhor entendimento do que realmente acontece.

Alguns pontos interessantes sobre o uso de pipes:
<ul>
	<li>Se mais de um processo ou thread está escrevendo no pipe ao mesmo tempo, o kernel assegura que as escritas serão atômicas, ou seja, não haverá interrupções de escritas, desde que o número de bytes escritos seja menor ou igual PIPE_BUF. Esta definição está dentro do arquivo /usr/include/linux/limits.h e no meu sistema ele tem o valor de 4096.</li>
	<li>A capacidade de um pipe de reter informação é limitada. Desde a versão 2.6.11 do Linux o limite de dados que um <em>pipe</em> pode armazenar é 65536 bytes. Mas, uma vez que uma aplicação for bem desenhada e que o lado de leitura do <em>pipe</em> consiga ler assim que o dado está disponível, não haverá problemas com esta limitação.</li>
	<li>Pipes podem somente ser usados por processos afiliados, ou seja, processos pai com processos filhos, netos e etc. Existe um tipo de <em>pipe</em> que pode ser usado por processos diferentes. Este se chama <em>FIFO</em> e será abordado nas próximas postagens.</li>
</ul>
Espero que tenham gostado desta primeira parte do artigo. A segunda parte terá informações que explicam como o bash consegue conectar a saída de um processo com a entrada de um novo processo. Não se esqueçam de nos seguir nas redes sociais para ler as postagens assim que estas são publicadas. Até mais!