---
layout: wordpress
title: Implemente seu malloc/free. Just4fun!
date: 2015-12-03 13:18:40
author: guilhermevanz
permalink: /implemente-seu-mallocfree-just4fun/
image: /assets/wp-content/uploads/2015/11/1042021.png
categories:
  - Desenvolvimento
tags:
  - c
  - glibc
  - linux
---

Algum tempo atrás comprei o livro The Linux Programming Interface, um dos melhores livros que já adquiri. Um dos primeiros capítulos que li foi sobre alocação de memória. No final do capítulo, o autor oferece alguns exercícios. Entre eles existe um mais desafiador. Que é implementar funções equivalentes ao <code>malloc</code> e <code>free</code>. The challenge has been accepted!

<!--more-->

Antes de mais nada, essa implementação tem com objetivo apenas estudo. Isso significa que você NÃO deve implementar suas funções <code>malloc</code> e <code>free</code> para programas rodando em produção. Salvo em caso muito específicos, não reinvente a roda! A glibc é constantemente melhorada a décadas por pessoas muito qualificadas. Você provavelmente levaria mais tempo para fazer um trabalho equivalente.

Assumo também que o leitor possui um pouco de conhecimento de como um processo e seus segmentos de código, dados e etc funcionam. Vale lembrar também que o código não cobre determinadas situações e como qualquer software pode ser melhorado, e muito.
<h3><b>Chamadas de sistema</b></h3>
&nbsp;

Existem duas chamadas de sistema que permitem aumentar o <i>program break, </i>são<i> brk </i>e<i> sbrk.</i> O <i>program break</i> define onde é o final do segmento de dados do processo. Isso significa que quando o programa aumenta o <i>program break </i>mais memória é alocada. Caso contrário, a memória é liberada. Nesta implementação apenas a função <i>sbrk </i>é usada. Seu único parâmetro define a quantidade de memória que se deseja incrementar. Se a memória for alocada com sucesso, um ponteiro para o começo do bloco alocado é retornado. Caso contrário, um (void*) -1 é retornado. <i>brk</i> não está sendo usado. Ele permite que o programa indique qual é o final do segmento de dados  através do ponteiro que é passado como parâmetro. Acredito que essa função não está sendo usada porque o <i>program break</i> não é decrementado. Talvez no futuro essa <em>feature</em> possa ser implementada e a função sera utilizada. Para informações detalhadas, verifique o <em>man page</em>.
<h3><b>Código</b></h3>
&nbsp;



<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/gist/ba82bdd0dfeb44c260aa?lang=C'></script>


A base de toda a implementação é uma lista encadeada, chamada <code>free_list</code>. Ela mantêm todos os blocos de memória disponíveis. Cada elemento da lista é composto por um cabeçalho e a memória propriamente dita. O cabeçalho é uma estrutura onde são guardados dois metadados. O primeiro é o tamanho do bloco de memória e o segundo é um ponteiro para o próximo bloco de memória na <code>free_list</code>. A primeira ação feita  quando o programa requisita memória é verificar se a <code>free_list</code> foi inicializada (linha 29). Em caso negativo, a lista é inicializada  e um bloco de tamanho zero é colocado como primeiro elemento (linhas 29 até 36) . Isso é feito para manter o primeiro elemento da lista sempre o mesmo. Facilitando para saber quando parar um <em>loop</em> após percorrer todos os elementos da lista. Veja uma representação gráfica da memória inicializada:

<a href="/assets/wp-content/uploads/2015/12/mem_init-1.png" rel="attachment wp-att-4608"><img class="alignnone wp-image-4608" src="/assets/wp-content/uploads/2015/12/mem_init-1-300x59.png" alt="mem_init" width="970" height="191" /></a>

Uma vez a <code>free_list</code> inicializada, uma pesquisa na lista é executada. Procurando por um bloco de memória com tamanho suficiente para atender a requisição. O algoritmo é <i>first fit</i>, de forma que o primeiro bloco encontrado com memória suficiente é quebrado, se assim for necessário, e o ponteiro para o inicio do bloco de memória é retornado (linhas 38 até 53). Se nenhum bloco possui tamanho suficiente, a <i>heap</i> é incrementada e o novo bloco de memória é retornado (linha 55). O ponteiro retornado para o chamador é um ponteiro para o bloco de memória propriamente dito. Ele não inclui o cabeçalho. Não faz sentido dar acesso a estrutura de controle. Essa estrutura é usada apenas para o gerenciamento de memória e para saber qual o tamanho do bloco de memória quando ele for liberado. Na figura a seguir é possível visualizar a memória com um bloco de memória alocado:

<a href="/assets/wp-content/uploads/2015/12/one_mem_allocate.png" rel="attachment wp-att-4609"><img class="alignnone wp-image-4609" src="/assets/wp-content/uploads/2015/12/one_mem_allocate-300x59.png" alt="one_mem_allocate" width="981" height="193" /></a>

Como você pode ver entra as linhas 26 e 28, todos os blocos de memória são múltiplos do tamanho do cabeçalho. Isso quer dizer que o tamanho mínimo de um bloco de memória é HEADER_SIZE * 2 (considerando o <em>header</em>). Essa abordagem e utilizada para facilitar a aritmética de ponteiros e evitar a necessidade de contar cada <em>byte</em>. Em outras palavras, mesmo que o programa chamador requisite menos memória, o bloco alocado vai ser sempre múltiplo de HEADER_SIZE.

Quando o programa desejar liberar um ponteiro, outra busca na lista e executada. Desta vez em busca de um bloco de memória que esteja próximo daquele que esteja sendo liberado. Se algum bloco for encontrado, os dois blocos são unificados em um só (linhas 64 até 77). Caso contrario, o bloco é adicionado ao final da <code>free_list</code> (linhas 78 até 80). O objetivo de unificar blocos próximos é evitar a fragmentação excessiva da memória. ;)

Segundo meus fracos conhecimentos de análise assintótica, as duas funções envolvidas possuem tempo de execução de O(n). Uma vez que são executas buscas na <code>free_list</code> para cada chamada. Logo a baixo esta o resto do código fonte, onde pode ser visto o <em>header</em> e um programa de teste


<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/gist/869420fb87353049d4d7'></script>

<h4>Referências</h4>
<a href="http://linux.die.net/man/2" target="_blank">brk e sbrk man</a>
<a href="http://www.amazon.com/Programming-Language-Brian-W-Kernighan/dp/0131103628/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1448501445&amp;sr=1-1&amp;keywords=the+c+programming+language" target="_blank">The Linux Programming Interface</a>
<a href="http://www.amazon.com/Programming-Language-Brian-W-Kernighan/dp/0131103628/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1448501445&amp;sr=1-1&amp;keywords=the+c+programming+language" target="_blank">The C Programming Language</a>
<a href="https://github.com/jvanz/tlpi" target="_blank">Repositório</a>