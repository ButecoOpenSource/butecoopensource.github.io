---
layout: wordpress
title: Fazendo squash de commits com git rebase
excerpt: |
  Eventualmente trabalhamos em algo grande, e acabamos por fazer vários micro commits. Se você gostaria de juntar esses micro commits em um único no fim da implementação e não sabe como, eis a solução. O squash irá unir vários micro commits em um único commit. Sendo assim, se pode juntar uma alteração que tem 10 commits em apenas um único commit.
date: 2015-06-18 23:04:10
author: alexandrevicenzi
permalink: /fazendo-squash-de-commits-com-git-rebase/
categories:
  - Dicas
tags:
  - git
  - rebase
  - squash
---

Eventualmente trabalhamos em algo grande, e acabamos por fazer vários micro commits. Se você gostaria de juntar esses micro commits em um único no fim da implementação e não sabe como, eis a solução. O squash irá unir vários micro commits em um único commit. Sendo assim, se pode juntar uma alteração que tem 10 commits em apenas um único commit.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/06/git-squash-rebase.png" alt="Git Squash Rebase" />

Na imagem acima é possível observar que os commits antigos geram um novo commit unindo todas as alterações.

<!--more-->

<strong>Obs:</strong> Antes de fazer qualquer alteração desse tipo, recomendo fazer um backup do repositório e sempre ler com atenção toda e qualquer mensagem que aparecer.

Agora vamos ver como fazer o squash dos últimos 4 commits. Para isto execute o comando abaixo:

<code>git rebase -i HEAD~4</code>

Deverá aparecer os commits a serem mesclados, como abaixo:

<pre><code class="bash">
pick 6f7823b Add Nginx reload tasks.
pick db22ae4 Change nginx port to use HAProxy.
pick 14bc6ad Change nginx port.
pick c0dbc9a Remove old config files.

# Rebase 9ecdcb0..c0dbc9a onto 9ecdcb0 (4 TODO item(s))
#
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like &quot;squash&quot;, but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
#
# These lines can be re-ordered; they are executed from top to bottom.
#
# If you remove a line here THAT COMMIT WILL BE LOST.
#
# However, if you remove everything, the rebase will be aborted.
#
# Note that empty commits are commented out
</code></pre>

A primeira linha deve ser pick, as demais squash (ou s). Como abaixo:

<pre><code class="bash">
pick 6f7823b Add Nginx reload tasks.
s db22ae4 Change nginx port to use HAProxy.
s 14bc6ad Change nginx port.
s c0dbc9a Remove old config files.
</code></pre>

Salve.

Deverá aparecer uma mensagem mostrando o status do rebase, como abaixo:

<em>Rebasing (1/4)</em>

E após deverá exibir a união dos commits, igual um commit normal, mas lembre-se que todas as mensagens de commits estão juntas, se você preferir pode remove-las.

Salve.

Deverá exibir a mensagem:

<em>Successfully rebased and updated refs/heads/master.</em>

Agora basta fazer o push, lembre-se que terá de forçar o push, pois ele irá sobrescrever os commits antigos. Para isto basta executar o comando:

<code>git push -f</code>

Pronto!