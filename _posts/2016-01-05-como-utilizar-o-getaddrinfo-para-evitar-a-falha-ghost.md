---
layout: wordpress
title: Como utilizar o getaddrinfo para evitar a falha GHOST
excerpt: |
  Este post mostra como utilizar a função getaddrinfo, e mostra o porque ela deve ser utilizada no lugar da função gethostbyname.
date: 2016-01-05 23:09:47
author: marcossouza
permalink: /como-utilizar-o-getaddrinfo-para-evitar-a-falha-ghost/
image: /assets/wp-content/uploads/2016/01/glibc-ghost.png
categories:
  - Desenvolvimento
tags:
  - c
  - glibc
  - linux
  - network
  - programação
  - redes
---

Em janeiro de 2015 se ouviu falar de uma falha de segurança na glibc chamada GHOST. Esta falha poderia ser explorada por um programa malicioso utilizando as funções <code>gethostbyname()</code> e <code>gethostbyname2()</code> da glibc. O ataque acontece por um <em>buffer overflow</em> dentro destas funções quando um endereço inválido é passando como parâmetro. Ao explorar esta falha, o atacante consegue executar códigos arbitrários com as permissões do usuários executando o processo.

<!--more-->

Este problema existia na glibc desde 2000, e foi corrigido em 2013, mas como a falha não havia sido detectada, não foi criada outra versão estável da glibc após a correção. Quando a falha foi exposta, grandes distribuições como Red Hat e Debian atualizaram a sua versão da glibc. Segundo esta <a href="http://blogs.cisco.com/security/talos/ghost-glibc" target="_blank">publicação</a> da Cisco, a falha não é tão assutadora quanto parece, pois o software a ser explorado precisa aceitar <em>hostnames</em> como entrada e ainda assim existem algumas situações em que o <em>bug</em> pode ser explorado: o primeiro carácter precisa ser um dígito, o último carácter não pode ser um ponto e o <em>hostname</em> precisa ser construído somente por dígitos e pontos (um endereço IPv4 comum).

As funções <code>gethostbyname</code> e <code>gethostbyname2</code> foram criadas nos anos 80 e estão depreciadas a algum tempo, podendo até ser noticiadas pela leitura do <em>man</em>. A alternativa é utilizar a função <code>getaddrinfo</code>, que além de ser a função substituta de <code>gethostbyname*()</code>, trabalha de forma transparente com IPv6.

Veja abaixo um exemplo da utilização do gethostbyname2:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/ghost/gethostbyname.c" type="text/javascript"></script>
Segue a saída do programa:
<samp>
[marcos@xfiles ghost]$ ./gethostbyname facebook.com
Host: facebook.com
IPv4: 173.252.120.68
Host: facebook.com
IPv6: 2a03:2880:2130:cf24:face:b00c:0:25de
</samp>

A chamada <code>gethosbyname2</code> retorna um ponteiro para <em>struct hostent</em>. Esta <em>struct</em> contém um campo chamado <code>h_addr_list</code>, onde estão todos os endereços IP relacionados ao <em>hostname</em> informado. O campo <code>h_addrtype</code> informa se o IP retornado é IPv4 (<code>AF_INET</code>) ou IPv6 (<code>AF_INET6</code>). Após verificar se o retorno é um IPv4 ou IPv6 é necessário decodificar o IP, que está em formato binário. A chamada <code>inet_ntop</code> recebe como parâmetro uma <em>struct</em> <code>in_addr</code> ou <em>struct</em> <code>in6_addr</code> e retorna o IP em forma de <em>string</em>. Neste exemplo foi utilizado um ponteiro <code>void</code> para armazenar as <em>structs</em> afim de simplificar o código, já que o segundo parâmetro da função <code>inet_ntop</code> espera um <code>void *</code>.

A chamada <code>gethostbyname2</code> foi utilizada pois <code>gethostbyname</code> não retornou nenhum endereço IPv6, embora as <em>man pages</em> digam que ela retorna.

A função <code>getaddrinfo</code> trabalha da mesma forma que a <code>gethostbyname*</code>, mas esta é mais transparente em relação a filtragem dos <em>hosts</em> retornados. Primeiramente vamos a um exemplo:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/ghost/getaddrinfo.c" type="text/javascript"></script>
Segue abaixo a saída deste programa executado:
<samp>
[marcos@xfiles ghost]$ ./getaddrinfo facebook.com
Host: facebook.com
IPv4: 173.252.120.68
IPv6: 2a03:2880:2130:cf24:face:b00c:0:25de
</samp>

A chamada <code>getaddrinfo</code> recebe quatro parâmetros:
<ul>
	<li>um nó (<em>hostname</em>)</li>
	<li>um serviço (porta)</li>
	<li>uma <em>struct</em> <code>addinfo</code>, ou <em>hints</em></li>
	<li>e um ponteiro para <code>addrinfo</code>, que irá ser conter os IPs do <em>hostname</em></li>
</ul>
O <em>hostname</em> é basicamente o <em>host</em> que queremos buscar, ou seja, é o mesmo parâmetro da chamada <code>gethostbyname</code>. Já o serviço especificado pode estar em formato decimal, como uma porta, ou um serviço como "http". Podemos deixar este campo como <code>NULL</code>. A <em>struct hints</em> funciona como um filtro, informando qual o tipo de endereços que desejamos receber da chamada <code>getaddrinfo</code> para o <em>host</em> informado. Neste caso nós informamos <code>ai_family</code> como <code>AF_UNSPEC</code>, pois queremos receber tanto endereços IPv4 quanto IPv6 (para buscar por somente um deles basta informar <code>AF_INET</code> ou <code>AF_INET6</code>), <code>ai_socktype</code> como 0, pois esperamos tanto por TCP quanto UDP, e <code>ai_flags</code> como <code>AI_CANONNAME</code> para que o <em>hostname</em> descoberto seja retornado na <em>struct</em> <code>addrinfo</code>. Já o quarto parâmetro é um ponteiro para <code>addrinfo</code> que irá conter todos os endereços IP relacionados ao <em>host</em> informado.

A chamada <code>getaddrinfo</code> retorna zero em caso de sucesso, ou um código de erro em caso de falha. O erro em sua forma descritiva por ser visto pela chamada <code>gai_strerror</code>, que recebe o retorno de <code>getaddrinfo</code>.

Após executado o <code>getaddrinfo</code>, então iteramos sobre todos os IPs retornados. O campo <code>ai_next</code> sempre aponta para a próxima <em>struct</em> <code>addrinfo</code>. O processo para imprimir o IP do <em>host</em> é basicamente o mesmo do <code>gethostbyname</code>. <code>freeaddrinfo</code> server para liberar a memória alocada da chamada <code>getaddrinfo</code>.

Como podemos observar, adaptar o código para <code>getaddrinfo</code> não é difícil, muito pelo contrário, e seguir as recomendações do <em>man</em> parecem ser sempre algo bom a se fazer!

Até a próxima!

Referências:

<a href="https://access.redhat.com/security/cve/CVE-2015-0235" target="_blank">Red Hat CVE</a>
<a href="https://access.redhat.com/articles/1332213" target="_blank">GHOST: glibc vulnerability (CVE-2015-0235) </a>
<a href="http://www.zdnet.com/article/critical-linux-security-hole-found/" target="_blank">GHOST, a critical Linux security hole, is revealed</a>
<a href="http://www.openwall.com/lists/oss-security/2015/01/27/9" target="_blank">Qualys Security Advisory CVE-2015-0235 - GHOST: glibc gethostbyname buffer overflow</a>
<a href="http://blog.erratasec.com/2015/01/you-shouldnt-be-using-gethostbyname.html#.VoPaQl6vCh8" target="_blank">You shouldn't be using gethostbyname() anyway</a>
<a href="http://man7.org/linux/man-pages/man3/inet_pton.3.html" target="_blank">Man inet_pton</a>
<a href="http://linux.die.net/man/3/gethostbyname" target="_blank">Man gethostbyname</a>
<a href="http://linux.die.net/man/3/getaddrinfo" target="_blank">Man getaddrinfo</a>