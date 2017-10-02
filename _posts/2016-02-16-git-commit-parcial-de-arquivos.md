---
layout: wordpress
title: "Git: commit parcial de arquivos"
excerpt: |
  Neste post demonstrarei uma das muitas features bacanas disponíveis no git, o commit parcial de arquivos. Esta feature permite ao usuário selecionar quais alterações de determinado arquivo devem ser commitados.
date: 2016-02-16 21:08:42
author: guilhermevanz
permalink: /git-commit-parcial-de-arquivos/
image: /assets/wp-content/uploads/2016/02/Git-Logo-Black.png
categories:
  - Desenvolvimento
tags:
  - git
  - git-add
  - git-commit
---

Neste post demonstrarei uma das muitas <em>features</em> bacanas disponíveis no git, o <em>commit</em> parcial de arquivos. Esta <em>feature</em> permite ao usuário selecionar quais alterações de determinado arquivo devem ser commitados.

<!--more-->

Vamos supor que existe o seguinte arquivo em um projeto:

<script type="text/javascript" src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/git_sample.c"></script>

Neste novo repositório existe um único commit:

<a href="/assets/wp-content/uploads/2016/02/partial_commit_1.png"><img class="aligncenter wp-image-4771" src="/assets/wp-content/uploads/2016/02/partial_commit_1.png" alt="partial_commit_1"/></a>

A primeira alteração é feita:

<a href="/assets/wp-content/uploads/2016/02/partial_commit_2.png"><img class="aligncenter wp-image-4770" src="/assets/wp-content/uploads/2016/02/partial_commit_2.png" alt="partial_commit_2"/></a>

Suponha que um colega solicita outra alteração no mesmo arquivo. Ele/Ela pede para alterar o nome da função <code>foo()</code> para <code>xpto()</code>.
Depois de ambas mudanças o <em>diff</em> é:

<a href="/assets/wp-content/uploads/2016/02/partial_commit_3.png"><img class="aligncenter wp-image-4769" src="/assets/wp-content/uploads/2016/02/partial_commit_3.png" alt="partial_commit_3"/></a>

Agora é hora de commitar as alterações. Entretanto, é necessário que cada alteração seja submetida em diferentes <em>commits</em>. Felizmente o git possui uma <em>feature</em> que nos ajuda em situações como essa. Os comandos <code>git add</code> e <code>git commit</code> permitem ao usuário selecionar quais partes do arquivos devem ser adicionadas. Isso é feito passando a opção <code>-p, --patch</code>. Em nosso exemplo, será utilizado <code>git commit</code>.

<a href="/assets/wp-content/uploads/2016/02/partial_commit_4.png"><img class="aligncenter wp-image-4768" src="/assets/wp-content/uploads/2016/02/partial_commit_4.png" alt="partial_commit_4"/></a>

Como pode ser visto, git mostra cada alteração realizada e pergunta ao usuário o que deve ser feita com ela. As opções são: [y,n,q,a,d,/,s,e,?].
Para visualizar o texto de ajuda digite <code>?</code>. O seguinte texto devera ser exibido:

<samp>
y - stage this hunk
n - do not stage this hunk
q - quit; do not stage this hunk or any of the remaining ones
a - stage this hunk and all later hunks in the file
d - do not stage this hunk or any of the later hunks in the file
g - select a hunk to go to
/ - search for a hunk matching the given regex
j - leave this hunk undecided, see next undecided hunk
J - leave this hunk undecided, see next hunk
k - leave this hunk undecided, see previous undecided hunk
K - leave this hunk undecided, see previous hunk
s - split the current hunk into smaller hunks
e - manually edit the current hunk
? - print help
</samp>

No exemplo, é mostrado o primeiro <em>hunk</em> de alteração do arquivo. Em nosso primeiro <em>commit</em> queremos apenas as alteração realizadas na função <code>bar()</code>, então o primeiro <em>hunk</em> deve ser ignorado. Assim, a opção <code>n</code> é a escolha certa.

<a href="/assets/wp-content/uploads/2016/02/partial_commit_5.png"><img class="aligncenter wp-image-4767" src="/assets/wp-content/uploads/2016/02/partial_commit_5.png" alt="partial_commit_5"/></a>

Depois disso o git mostra todas as demais alterações como se fosse um único <em>hunk,</em> então é necessário quebra-las em alterações menores. Para isso existem duas opções: <code>s</code> e <code>e</code>. A primeira faz com que o git quebre o <em>hunk</em> em partes menores. A segunda, por sua vez, permite que o usuário escolha manualmente quais linhas alteradas devem ser inclusas. Para este pequeno tutorial iremos utilizar a opção <code>s</code>. Git devera mostrar algo semelhante a isso:

<a href="/assets/wp-content/uploads/2016/02/partial_commit_6.png"><img class="aligncenter wp-image-4766" src="/assets/wp-content/uploads/2016/02/partial_commit_6.png" alt="partial_commit_6"/></a>

O <em>hunk</em> anterior foi quebrado em 3 partes. Então será iterado sobre todos eles perguntado ao usuário qual ação deve ser executada para cada um deles. O primeiro <em>hunk</em> criado também deve ser ignorado. O segundo <em>hunk </em>é a primeira alteração relacionada a função <code>bar()</code> e deve ser adicionado, para isso é necessário escolher a ação <code>y</code>.

<a href="/assets/wp-content/uploads/2016/02/partial_commit_7.png"><img class="aligncenter wp-image-4765" src="/assets/wp-content/uploads/2016/02/partial_commit_7.png" alt="partial_commit_7"/></a>

O terceiro também deve ser adicionado ao <em>commit</em>...

<a href="/assets/wp-content/uploads/2016/02/partial_commit_8.png"><img class="aligncenter wp-image-4764" src="/assets/wp-content/uploads/2016/02/partial_commit_8.png" alt="partial_commit_8"/></a>

Quando não existir mais <em>hunks</em> a serem selecionados, como estamos utilizando o comando <code>git commit</code>, será aberto o editor para o usuário escrever a mensagem de <em>commit</em>. Após isso, está feito:

<a href="/assets/wp-content/uploads/2016/02/partial_commit_9.png"><img class="aligncenter wp-image-4763" src="/assets/wp-content/uploads/2016/02/partial_commit_9.png" alt="partial_commit_9"/></a>


Agora que o primeiro <em>commit</em> contem apenas as alterações referentes a função <code>bar()</code>, as demais mudanças podem ser comitadas em um segundo commit:

<a href="/assets/wp-content/uploads/2016/02/partial_commit_10.png"><img class="aligncenter wp-image-4762" src="/assets/wp-content/uploads/2016/02/partial_commit_10.png" alt="partial_commit_10"/></a>

Espero que vocês tenham gostado desta dica simples. Considero escrever um <em>post</em> cobrindo todas as demais opções não citadas neste texto (e.g. seleção manual de <em>hunk</em>, entre outras). Encorajo ao leitor brincar com as demais opção disponibilizadas.