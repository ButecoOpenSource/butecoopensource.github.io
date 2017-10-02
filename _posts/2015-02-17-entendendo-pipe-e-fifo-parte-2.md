---
layout: wordpress
title: Entendendo Pipe e FIFO (parte 2)
date: 2015-02-17 20:50:57
author: marcossouza
permalink: /entendendo-pipe-e-fifo-parte-2/
image: /assets/wp-content/uploads/2015/01/pipes.png
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - termin
  - terminal
---

<p style="text-align: justify;">Esta é a segunda parte da postagem sobre Pipes e Fifos aqui do blog. Se ainda não viu a primeira parte, pode acessá-la por <a title="Entendendo Pipes e FIFOs (parte 1)" href="/2015/01/22/entendendo-pipe-e-fifo-parte-1/" target="_blank">aqui</a>. Nesta parte será explicado como processos podem ter seus dados interligados, exatamente como o shell faz no comando <em>ls | wc -l</em>. Para entender como este processo ocorre é necessário entender que existem três "arquivos" que são abertos quando um processo se inicia.</p>
Estes arquivos são:
<ul>
	<li>entrada padrão ou <em>stdin</em> (file descriptor zero)</li>
	<li>a saída padrão ou <em>stdout</em> (file descriptor um)</li>
	<li>saída de erros ou <em>stderr</em> (file descriptor dois)</li>
</ul>
<p style="text-align: justify;">Ao utilizarmos a função <em>printf</em>, a string é automaticamente enviada para a <em>stdout</em>, ou saída padrão. Ainda assim podemos utilizar a função <em>fprintf </em>ou até mesmo a função <em>write</em> para especificar para onde queremos enviar a string, podendo ser a <em>stdout</em>, <em>stderr</em> ou ainda um fd de um arquivo aberto pelo usuário.</p>
<p style="text-align: justify;">Utilizando estes <em>file descriptors,</em> podemos fazer com que a saída de um processo seja direcionado para a entrada de outro processo, exatamente como se estivéssemos colocando um "cano"  entre os processos. O código abaixo, mostra um exemplo deste redirecionamento ao executar a função <em>ls</em> e direcionar a saída para outro processo. Algumas partes são comuns do exemplo do último artigo, pois o mesmo mecanismo de pipes é utilizado:</p>
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/pipe_fifo/pipe_connect.c" type="text/javascript"></script>Este programa executa duas chamadas fork, sendo cada uma delas para criar um dos processos que serão conectados pelo pipe. O código abordado possui muitas chamadas de sistema relacionadas a arquivos, e todos estes serão explicados agora: <strong>fds[1] != STDOUT_FILENO</strong> Esta validação é necessária para validar se o <em>stdout</em> não foi previamente redirecionado para o fd[1] por um outro programa que chame o programa atual, e funciona como programação defensiva. <strong>dup2(fds[1], STDOUT_FILENO)</strong> A chamada de sistema <em>dup2</em> duplica o fd do primeiro parâmetro, fecha o fd do segundo parâmetro e reabre o fd do segundo parâmetro com as características do primeiro fd. Quando fechamos um arquivo no Linux e reabrimos outro, este tende a pegar o número do fd do arquivo que foi fechado. Neste ponto, ao usar o <em>dup2</em> nós estamos tentando fazer com que o fd zero, que é usado como entrada padrão, seja o fd[1] do pipe. Ou seja, quando o programa executar um <em>printf</em>, os dados que seriam enviados a saída padrão (file descriptor zero) será enviado ao fd[1] (que na verdade é o novo fd zero). É um pouco confuso no início, mas o código abaixo tenta exemplificar este comportamento de reusar o número de fd:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/show_fd_reuse.c" type="text/javascript"></script>

A execução do programa acima é:
<strong>marcos@localhost: [exemplos_c] # ./show_fd_reuse
fd aberto é: 3
novo fd é: 3
</strong>

Assim podemos entender um pouco melhor como os sistemas *NIX usam seus fds. E outro detalhe: O fd número três é utilizado, pois os fds zero, um e dois já estão sendo utilizados por <em>stdin</em>, <em>stdout</em> e <em>stderr</em>.

<strong>execlp("ls", "ls", (char *)NULL);</strong>
Esta chamada de sistema carrega um novo programa no espaço de memória do processo atual. Após a chamada fork, um novo processo é iniciado, e este continua a executar do ponto onde foi criado, e então a chamada <em>execlp</em> é utilizada para carregar o novo processo, apagando o processo pai do espaço de memória do processo criado. Um detalhe importante: este novo processo terá sua saída padrão sendo o fd[1], e desta forma estaremos enviando toda a saída do comando ls para o outro processo que irá ser criado.

Após esse ponto será criado um outro processo que irá pegar a saída do comando <em>ls</em> executado anteriormente.

<strong>dup2(fds[0], STDIN_FILENO)</strong>
<strong>execlp("wc", "wc", "-l", (char *)NULL)</strong>
Primeiramente a entrada padrão do processo do novo processo criado será atribuída ao <em>fds[0]</em>, que é a parte de leitura do pipe. Após redirecionar a entrada padrão para que esta leia do pipe, o novo processo então executa o execlp para carregar o programa <em>wc</em>, passando o parâmetro <em>-l</em>.

<strong>close(fds[0])</strong>
<strong>close(fds[1])</strong>
<strong>wait(NULL)</strong>
<strong>wait(NULL)</strong>
Após executar ambos processos, então é necessário esperar para que ambos os processos terminem. A chamada de sistema <em>wait</em> faz com que a execução do processo pare e espere pelo término de um processo filho. Como não é especificado qual processo filho desejamos parar, então é executada a chamada de sistemas duas vezes para esperar pelo término dos dois processos.

Após a execução do programa, pode-se comparar sua saída do comando <em>ls | wc -l c</em> no bash:
<strong>[marcos@xfiles pipe_fifo]$ ls | wc -l
4</strong>

<strong>[marcos@xfiles pipe_fifo]$ ./pipe_connect
4</strong>

Espero que tenham gostado desta segunda parte da postagem. A próxima e última parte abordará Fifos. Assine nosso feed e se inscreva em nossas páginas nas redes sociais para saber em primeira mão quando um novo artigo sair. Até mais!