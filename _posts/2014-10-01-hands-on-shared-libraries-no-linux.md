---
layout: wordpress
title: "Hands On: Shared Libraries no Linux"
date: 2014-10-01 00:42:05
author: marcossouza
permalink: /hands-on-shared-libraries-no-linux/
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - shared-libraries
---

Bibliotecas compartilhadas são usadas em qualquer sistema operacional, seja Windows, Linux, Mac OSX ou qualquer *BSD ou *NIX. No Windows este recurso tem o nome de <i>DLL</i> (Dynamic-link Library) com sua extensão .<i>dll, </i>no Mac OSX tem a extensão <em>.dylib</em>  e nos outros sistemas UNIX-like(Linux, *BSD) este se chama <i>Shared Object </i>e tem extensão <i>.so</i>. Um entendimento básico sobre o funcionamento deste recurso ajuda muito usuários destes sistemas a resolverem possíveis problemas de falta de bibliotecas.

A nomenclatura de bibliotecas compartilhadas segue um padrão em cada sistema. Nos sistemas Linux o padrão é <i>lib&lt;nome_da_lib</i><i>&gt;&lt;.versão&gt;.so. </i>Podemos exemplificar esta convenção com a biblioteca pthreads no Linux. No Fedora, esta biblioteca está definida como <i>libpthread-2.18.so</i>, e um link <i>libpthread.so</i> para esta biblioteca.

Sobre a localização de bibliotecas compartilhadas, no Fedora as libs estão dentro de <i>/usr/lib64</i>. Em sistemas 32 bits, fica dentro de <i>/usr/lib</i>.

Para poder fazer uso de uma <i>shared library </i>utilizando o <i>GCC</i> no Linux basta adicionar um parâmetro <i>-l&lt;nome_da_</i><i>biblioteca&gt;</i>. O prefixo <i>lib</i> neste caso deve ser removido. Para exemplificar o uso de uma biblioteca na compilação de um programa C/C++ temos o seguinte comando abaixo:

<pre><code class="bash">
gcc fonte.c -o bin -lpthread
</code></pre>

No comando acima estamos compilando o programa fonte chamado <i>fonte.c</i>, gerando um binário com o nome <i>bin</i> e estamos <i>linkando</i> com a biblioteca <i>pthreads </i>do Linux.

Para criar um biblioteca compartilhada é uma tarefa simples. Para iniciar uma biblioteca precisamos criar uma função que será utilizada em outros programas. Como exemplo, irei criar o arquivo <i>soma.c</i> e <i>soma.h</i> para criar uma biblioteca chamada <i>libmatematica.so</i>.

Os arquivos soma.h e soma.c são listados abaixo:

<em>soma.c</em>

<pre><code class="c">

int soma(int a, int b)

{
    return a + b;
}

</code></pre>

<em>soma.h</em>

<pre><code class="c">

int soma(int a, int b);

</code></pre>

A linha de comando abaixo compila o código fonte <i>soma.c </i> e cria a biblioteca <i>libmatematica.so</i>:

<pre><code class="bash">

gcc -shared -Wall soma.c -o libmatematica.so

</code></pre>

A opção <i>-shared </i>diz ao <i>GCC</i> que o binário compilado será uma biblioteca compartilhada. O arquivo <i>soma.h </i>será utilizada pelos programas que vão usar esta biblioteca. O programa a seguir, chamado <i>main.c</i>, vai utilizar a função <i>soma</i> da biblioteca que criamos:

<pre><code class="c">
#include &lt;soma.h&gt;
#include &lt;stdio.h&gt;

int main()
{
    printf(&quot;%dn&quot;, soma(1, 5));
    return 0;
}
</code></pre>

Para compilar este programa usamos o comando abaixo:

<pre><code class="bash">

gcc main.c -o main -lmatematica

</code></pre>

Ao executar o binário main, obtemos como saída o número 6, número este que é retornado pela função <em>soma </em> da biblioteca <em>libmatematica.so</em>.

Podemos ainda verificar quais bibliotecas um binário específico utiliza. O comando <i>ldd </i>é o responsável por dar tal informação <i>. </i>O comando abaixo mostra quais as bibliotecas utilizadas no binário <i>main</i> recém gerado utiliza.

<pre><code class="bash">

ldd main

</code></pre>

Como saída eu obtive:

<pre><code class="bash">
[marcos@xfiles teste]$ ldd main
linux-vdso.so.1 =&gt; (0x00007fff339fe000)
libmatematica.so =&gt; /home/marcos/teste/libmatematica.so (0x00007fb8129fb000)
libc.so.6 =&gt; /lib64/libc.so.6 (0x00007fb812612000)
/lib64/ld-linux-x86-64.so.2 (0x00007fb812bfe000)
</code></pre>

Algumas observações sobre a biblioteca e o arquivo header. No include foi utilizado os símbolos “&lt;” e “&gt;” ao redor do nome do header. Quando usamos esta notação o compilador espera que o header este dentro da estrutura <i>/usr/include</i>. Para este teste eu movi o arquivo <i>soma.h</i> para lá. Sobre o parâmetro -l&lt;nome_lib&gt;, como já explicado antes, espera-se que a biblioteca esteja dentro de <i>/usr/lib</i>. Para este teste eu criei um link simbólico <i>libmatematica.so</i> dentro de <i>/usr/lib</i> e apontei para a pasta a pasta onde está a minha biblioteca.

Alguns link interessantes sobre o assunto:

<a href="http://tldp.org/HOWTO/Program-Library-HOWTO/shared-libraries.html">http://tldp.org/HOWTO/Program-Library-HOWTO/shared-libraries.html</a>

<a href="http://linux.die.net/man/1/gcc">http://linux.die.net/man/1/gcc</a>

<a href="http://unixhelp.ed.ac.uk/CGI/man-cgi?ldd+1">http://unixhelp.ed.ac.uk/CGI/man-cgi?ldd+1</a>

Qualquer dúvida, crítica ou sugestão, basta colocar nos comentários! Não se esqueçam de se inscrever no nosso feed!  Até mais pessoal!