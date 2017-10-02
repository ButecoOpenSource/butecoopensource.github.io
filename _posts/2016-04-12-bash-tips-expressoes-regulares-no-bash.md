---
layout: wordpress
title: "BASH tips: Expressões regulares no bash"
excerpt: |
  Exemplo de como utilizar expressões regulares no BASH
date: 2016-04-12 23:59:33
author: marcossouza
permalink: /bash-tips-expressoes-regulares-no-bash/
image: /assets/wp-content/uploads/2016/03/images.jpg
categories:
  - Dicas
tags:
  - bash
  - expressão regular
  - regex
  - regular expression
---

Como hoje tive de utilizar expressões regulares no bash, pensei em compartilhar com nossos amigos leitores. O buteco já fez um post sobre a utilização de <a href="/posix-regular-expression-em-c/" target="_blank">expressões regulares em C</a>, e este artigo vem para complementar. Vamos ao exemplo abaixo:
<!--more-->

<pre><code class="bash">
#!/bin/bash
string=&quot;buteco&quot;
if [[ $string =~ but(e)(co) ]]; then
        echo &quot;${BASH_REMATCH[1]}&quot;
        echo &quot;${BASH_REMATCH[2]}&quot;
        echo &quot;${BASH_REMATCH}&quot;
fi
</code></pre>

Output:

<pre><code class="">
e
co
buteco
</code></pre>

O operador <strong>=~</strong> tem a mesma precedência de <strong>==</strong> e <strong>!=</strong>. Sendo um operador binário, ele espera uma expressão regular no operador da direta e o aplica no operador da esquerda. Se a expressão regular efetuar <em>match</em>, o valor de retorno é zero. Caso a expressão regular não <em>match</em>, retornará 1, e se houver algum problema na expressão o valor retornado é 2.

Seguem mais exemplos do uso deste operador
Extraindo um session ID:

<pre><code class="bash">
string=&quot;SID=eaee6285-4325-4e44-bc5a-f02b4b829d46&quot;
if [[ $string =~ SID=([a-zA-Z0-9-]+) ]]; then
        echo &quot;SID inteiro: ${BASH_REMATCH}&quot;
        echo &quot;Somente o hash: ${BASH_REMATCH[1]}&quot;
fi
</code></pre>

Output:

<pre><code class="">
SID inteiro: SID=eaee6285-4325-4e44-bc5a-f02b4b829d46
Somente o hash: eaee6285-4325-4e44-bc5a-f02b4b829d46
</code></pre>

Extraindo partes de um arquivo:

<pre><code class="bash">
if [[ $(cat /proc/version) =~ version[[:space:]]([0-9+]).([0-9]+).([0-9]+) ]]
then
        echo &quot;Version: $(cat /proc/version)&quot;
        echo &quot;Version major: ${BASH_REMATCH[1]}&quot;
        echo &quot;Version minor: ${BASH_REMATCH[2]}&quot;
        echo &quot;Version micro: ${BASH_REMATCH[3]}&quot;
fi
</code></pre>

Output:

<pre><code class="">
Version: Linux version 4.4.6-300.fc23.x86_64 (mockbuild@bkernel02.phx2.fedoraproject.org) (gcc version 5.3.1 20151207 (Red Hat 5.3.1-2) (GCC) ) #1 SMP Wed Mar 16 22:10:37 UTC 2016
Version major: 4
Version minor: 4
Version micro: 6
</code></pre>

Espero que tenham gostado desta dica. Se você gostou desta dica, deixe seu comentário abaixo! Até a próxima!

Referência:
<a href="http://www.gnu.org/software/bash/manual/bashref.html#Conditional-Constructs" target="_blank">Bash Reference</a>