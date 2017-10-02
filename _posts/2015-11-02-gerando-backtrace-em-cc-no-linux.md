---
layout: wordpress
title: Gerando backtrace em C/C++ no Linux
excerpt: |
  Pequeno exemplo de como gerar um backtrace de um programa em C/C++ no Linux.
date: 2015-11-02 19:56:42
author: marcossouza
permalink: /gerando-backtrace-em-cc-no-linux/
image: /assets/wp-content/uploads/2015/10/588396621.jpg
categories:
  - Desenvolvimento
tags:
  - api
  - c
  - linux
  - terminal
---

Olá pessoal, creio que muitos aqui já se depararam com algum <em>crash</em> em seus programas em C/C++, e gostariam de poder ver a pilha de chamadas, ou <em>stacktrace/backtrace</em>, ao menos no ambiente de testes. Pois bem, a boa notícia é que no Linux existe a possibilidade de mostrar qual o ultimo método chamado antes de receber um <em>crash</em>.

<!--more-->

Chega de falar, vamos ao exemplo abaixo:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/backtrace/backtrace.c" type="text/javascript"></script>Para começar, vamos falar da função <em>main</em>. Logo no início nós "sinalizamos" ao programa que, no caso de um SIGINT ou de um SIGSEGV, ele deve chamar a função <em>handler</em>. Em termos simples, um SIGINT acontece quando um programa recebe um <em>kill -2</em>, ou aquele famoso <em>Ctrl-C</em> que você pressiona quando algum programa está executando no terminal e você deseja pará-lo de alguma forma. Este geralmente acontece por ação do usuário. Já o SIGSEGV acontece quando um ponteiro inválido é acessado. Para programadores Java, o SIGSEGV seria a leitura de um objeto não inicializado. Nestes casos, o Java por exemplo, mostra o <em>backtrace</em> e diz que ocorreu um "Null Pointer Reference", ou seja, uma referencia para um ponteiro nulo. Um caso simples de explicar um SIGSEGV no C pode ser exemplificado com o código abaixo, onde o programa tenta ler o conteúdo de um ponteiro que indica a posição -1, ou seja, inválido:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/backtrace/sigsegv.c" type="text/javascript"></script>

Voltando ao programa inicial, após as chamadas de <em>signal</em>, a função <em>func1</em> é chamada. Esta aguarda por 20 segundos, então é chamada a função <em>func2</em>. Esse tempo foi introduzido para poder exemplificar o SIGINT, pois o usuário pode executar um <em>kill -2 </em> e ver o <em>backtrace</em> gerado pelo SIGINT. Caso o usuário espere os 20 segundos, a <em>func2</em> será chamada, executando um SIGSEGV em si mesmo, para fim de exemplo. Ao ser executado o SIGSEGV, você verá o <em>backtrace</em> mostrando que a <em>func1</em> e a <em>func2</em> foram chamadas e que então o programa terminou na função <em>handler</em>.

A função <em>handler</em> por sua vez faz a chamada da função <em>backtrace</em>, que retorna um <em>array</em> de endereços de cada função chamada. O tamanho do <em>array</em> depende o segundo parâmetro. Se o <em>backtrace</em> for maior do que o parâmetro passado, então somente as N mais recentes funções serão retornadas. Como esta chamada retorna endereços, fica ruim distinguir qual foram as funções chamada somente olhando os endereços em hexadecimal, então utilizamos a função backtrace_symbols_fd, que pega os endereços em hexa e traduz em strings com os nomes da respetivas funções. Além disso, a chamada backtrace_symbols_fd também escreve, uma função por linha, no <em>file descriptor</em> especificado pelo terceiro parâmetro. Como exemplo, nós escrevemos direto na saída de erro do programa. No final da função <em>handler</em> é executado um exit(1), que termina o programa com erro.

Após toda essa explicação, vamos agora verificar a saída desse programa. Para compilar o código acima, basta chamar o <em>make</em> com Makefile abaixo:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/backtrace/Makefile" type="text/javascript"></script>

Ao executar o programa e logo efetuar um <em>kill -2 </em> nele:

<pre><code class="bash">
[marcos@xfiles backtrace]$ ./backtrace &amp;
[1] 17292
[marcos@xfiles backtrace]$ kill -2 17292
Signal: 2
backtrace returned 8 entries
./backtrace(handler+0x25)[0x400a7b]
/lib64/libc.so.6(+0x34a50)[0x7f92edbdfa50]
/lib64/libc.so.6(nanosleep+0x10)[0x7f92edc73a40]
/lib64/libc.so.6(sleep+0xd4)[0x7f92edc738f4]
./backtrace(func1+0xe)[0x400b02]
./backtrace(main+0x2c)[0x400b3b]
/lib64/libc.so.6(__libc_start_main+0xf0)[0x7f92edbcb700]
./backtrace(_start+0x29)[0x400989]
[1]+  Fim da execução com status 1      ./backtrace
</code></pre>

Na execução acima, podemos verificar que a função <em>main</em> e a func1 foram chamadas, e depois verificamos a função <em>sleep</em> ser chamada, e logo mais vemos a função <em>handler</em> como sendo a ultima do programa.

E ao esperar os 20 segundos:
<pre><code class="bash">
[marcos@xfiles backtrace]$ ./backtrace &amp;amp;
[1] 17305
[marcos@xfiles backtrace]$ Signal: 11
backtrace returned 8 entries
./backtrace(handler+0x25)[0x400a7b]
/lib64/libc.so.6(+0x34a50)[0x7fd6c8137a50]
/lib64/libc.so.6(kill+0x7)[0x7fd6c8137d07]
./backtrace(func2+0x15)[0x400af1]
./backtrace(func1+0x18)[0x400b0c]
./backtrace(main+0x2c)[0x400b3b]
/lib64/libc.so.6(__libc_start_main+0xf0)[0x7fd6c8123700]
./backtrace(_start+0x29)[0x400989]
[1]+ Fim da execução com status 1 ./backtrace
</code></pre>

Agora nesta execução, podemos verificar que além das funções <em>main</em> e func1, a função <em>func2</em> foi chamada, e então vemos <em>kill</em> ser executada e logo mais vemos a função <em>handler</em> sendo a última do programa.

Observações: No Makefile podemos verificar a opção -rdynamic. Ela é necessária para que o GCC mostre os nomes das funções. Podemos ver abaixo um exemplo de saída do programa sem essa opção especificada:

<pre><code class="bash">
[marcos@xfiles backtrace]$ ./backtrace &amp;
[1] 18323
[marcos@xfiles backtrace]$ kill -2 18323
Signal: 2
backtrace returned 8 entries
./backtrace[0x4007ab]
/lib64/libc.so.6(+0x34a50)[0x7f5c2b398a50]
/lib64/libc.so.6(nanosleep+0x10)[0x7f5c2b42ca40]
/lib64/libc.so.6(sleep+0xd4)[0x7f5c2b42c8f4]
./backtrace[0x400832]
./backtrace[0x40086b]
/lib64/libc.so.6(__libc_start_main+0xf0)[0x7f5c2b384700]
./backtrace[0x4006b9]
[1]+  Fim da execução com status 1      ./backtrace
</code></pre>

Como podemos ver, todas as referências ao binário <em>backtrace</em> agora não mostram mais o nome das funções, somente seu endereço em memória. Se uma função for <em>static inline</em>, está também não irá aparecer na pilha de chamadas.

Espero que tenham gostado! Não se esqueçam de se inscrever nas nossas redes sociais! Até a próxima!

Referências:
<a href="http://man7.org/linux/man-pages/man3/backtrace.3.html" target="_blank">man backtrace</a>