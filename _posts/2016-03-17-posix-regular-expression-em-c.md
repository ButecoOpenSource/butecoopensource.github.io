---
layout: wordpress
title: POSIX Regular Expression em C
excerpt: |
  Esta postagem tem como objetivo mostrar como utilizar POSIX regex com a linguagem C no ambiente Linux.
date: 2016-03-17 09:35:57
author: marcossouza
permalink: /posix-regular-expression-em-c/
image: /assets/wp-content/uploads/2016/03/images.jpg
categories:
  - Desenvolvimento
tags:
  - c
  - expressao_regular
  - linux
  - posix
  - regex
---

Expressões Regulares são úteis para diversos fins, desde validações de números como CPF e CEP, até em validações de entradas de campos e checagem de strings. Linguagens como Python, Javascript, PHP e outras já possuem expressões regulares <em>built-in</em>, prontas para serem utilizadas pelos programadores. Nesta postagem mostraremos como construir expressões regulares com a <em>POSIX RegEx</em> na linguagem C na plataforma Linux.
<!--more-->

No padrão POSIX existem as expressões regulares Básicas e Estendidas. na versão básica existem algumas limitações:
<ul>
	<li>A maioria dos caracteres são tratados como literais, como por exemplo <em>(</em> e <em>)</em>. Nesse caso, para serem tratados como meta caracteres eles precisam estar "escapados", <em>(</em> e <em>)</em>.</li>
	<li>Não existem os meta caracteres <em>+</em> (para um ou mais caracteres), <em>?</em> (zero ou uma ocorrência de um carácter) e <em>|</em> (alternadores, uma coisa ou outra)</li>
</ul>
Segue abaixo um exemplo de código C utilizando POSIX Regex Basic e Extended, mostrando as diferenças entre elas:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/posix_regex/regex.c?branch=master&amp;lang=cpp&amp;style=github" type="text/javascript"></script>

O código acima declara duas funções <em>wrapper</em>, somente para ser mais didático, mostrando as expressões regulares básicas e avançadas. Em ambas as funções é esperada uma string, com o texto a ser analisado, e a expressão regular.

Dentro da função <code>exec_regex</code> é chamada a função <code>regcomp</code>. Essa função recebe uma variável do tipo <code>regex_t</code>, a regex no formato string e o tipo de expressão, se é básica ou estendida, e "compila" essa expressão. Após compilada a expressão, essa mesma variável <code>regex_t</code> vai ser usada para executar de fato a regex no texto. Se a expressão regular tiver algum problema, essa função retorna um erro.

A variável <code>regmatch_t</code> vai armazenar todos os "matches" da expressão regular em relação a string. Matches são sbustrings que você deseja encontrar com a expressão regular, e são definidas entre parênteses. Logo, se você utilizar a expressão abaixo, você terá dois matches, um deles pegando a palavra buteco, e o outro pegando os números:

<code>([a-z]+)([0-9]+)</code>

Ao compilar a regex a variável membro da struct <code>regex_t</code> é populada com todos os possíveis matches. Na lista de matches, o match inicial da posição zero mostra a string inteira que foi descoberta pela regex, e então as próximas posições mostram cada match. Segue o exemplo abaixo, mostrando esse comportamento:

<samp>String 'buteco123xxxxx', Pattern '([a-z]+)([0-9]+)'
Group 0: [0-9]: buteco123
Group 1: [0-6]: buteco
Group 2: [6-9]: 123
</samp>

Por isso incrementamos <code>nsub</code> se for diferente de um <em>match</em>, pois se existe somente um <em>match</em> não faz sentido mostrar o mesmo match duas vezes.

Chegamos na função <code>regexec</code>, que recebe um <code>regex_t</code>, a string a ser analisada, o número de matches, uma variável <code>regmatch_t</code> e <em>flags</em>. Um exemplo de flag é <code>REG_ICASE</code>, onde a execução da regex não diferencia maiúsculas/minísculas. Neste exemplo não utilizamos nehum flag. Para saber sobre of flags disponíveis veja nas referências.

Se <code>regexec</code> executar com sucesso, iteramos sobre os <code>nsub</code> encontrados. Vamos nos aprofundar na struct <code>regmatch_t</code>. Essa struct contém dois membros: <code>rm_so</code> (regmatch start offset) e <code>rm_eo</code> (regmatch end offset). Esses offsets são usados para encontrar o match dentro da string, contendo os índices de início e fim da <em>substring</em> detectada pela regex.

Simplificando, offsets são as posições de início e fim de cada match dentro da string original.

Pelo nosso último exemplo de código, podemos ver no Group 1, que o primeiro match começa na posição 0 da string <em>buteco123xxxxx</em>, e finaliza na posição 6 (a posição 6 é o fim da string, logo atribuímos <code>''</code>). Da mesma forma, o segundo match começa na posição 6 e termina na 9.

Utilizando esses <em>offsets</em>, fazemos uma cópia da <em>substring</em> para uma nova string.

Quando o start offset é igual a <code>-1</code>, isso mostra que não existem mais matches para serem computados. Segue abaixo a execução do código fonte mostrado no início da postagem:

<samp>[marcos@localhost posix_regex]$ ./regex
Executing basic Regex
String 'buteco123xxxxx', Pattern '([a-z]*)'
Group 0: [0-6]: buteco
String 'buteco123xxxxx', Pattern '([a-z]+)([0-9]+)'
REG_NOMATCH
String 'buteco123xxxxx', Pattern '([a-z]*)([0-9]*)'
Group 0: [0-9]: buteco123
Group 1: [0-6]: buteco
Group 2: [6-9]: 123
String 'buteco123xxxxx', Pattern '([[:alpha:]]*)'
Group 0: [0-6]: buteco
Executing extended Regex
String 'buteco123xxxxx', Pattern '([a-z]*)'
Group 0: [0-6]: buteco
String 'buteco123xxxxx', Pattern '([a-z]+)([0-9]+)'
Group 0: [0-9]: buteco123
Group 1: [0-6]: buteco
Group 2: [6-9]: 123
String 'buteco123xxxxx', Pattern '([a-z]*)([0-9]*)'
Group 0: [0-9]: buteco123
Group 1: [0-6]: buteco
Group 2: [6-9]: 123
String 'buteco123xxxxx', Pattern '([[:alpha:]]*)'
Group 0: [0-6]: buteco
String 'buteco123xxxxx', Pattern '([^[:space:]]+)'
Group 0: [0-14]: buteco123xxxxx
String 'buteco123xxxxx', Pattern '([[:digit:]]+)'
Group 0: [6-9]: 123
String 'buteco123xxxxx', Pattern '([[:upper:]]+)'
REG_NOMATCH
String 'buteco123xxxxx', Pattern '([[:lower:]])'
Group 0: [0-1]: b
</samp>

Espero que tenham gostado desta postagem. Sugestões, críticas e dúvidas são muito bem vindas nos comentários. Até a próxima!

Referências:

<a href="https://en.wikibooks.org/wiki/Regular_Expressions/POSIX_Basic_Regular_Expressions" target="_blank">POSIX_basic_regular_expressions</a>
<a href="http://linux.die.net/man/3/regexec" target="_blank">Regex manpage</a>
<a href="http://www.gnu.org/software/libc/manual/html_node/Regexp-Subexpressions.html" target="_blank">Regex Subexpressions</a>