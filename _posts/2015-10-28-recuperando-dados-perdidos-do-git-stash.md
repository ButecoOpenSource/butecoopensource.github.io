---
layout: wordpress
title: Recuperando dados perdidos do git-stash
date: 2015-10-28 21:29:14
author: guilhermevanz
permalink: /recuperando-dados-perdidos-do-git-stash/
image: /assets/wp-content/uploads/2015/10/t8cnk.jpg
categories:
  - Dicas
tags:
  - dica
  - git
  - github
  - tutorial
---

Olá senhores e senhoras! =]

Em meu primeiro post no Buteco Open Source vou demonstrar como recuperar dados perdidos do git-stash. Talvez salvando muitas horas de trabalho que poderiam ser perdidas acidentalmente. Na realidade o método demonstrado neste artigo pode ser utilizado para  recuperar qualquer objeto git perdido. Antes de mais nada, enquanto você estiver implementando alguma grande <em>feature</em>, quebre-a em pequenos pedaços e faça <em>commits</em> regularmente. Não é uma boa ideia permanecer muito tempo sem "comitar". Tenha cuidado.

<!--more-->

Vamos simular o cenário para mostrar o que você pode fazer quando perder dados do <em>stash</em> do git. Em um repositório para demonstração existe apenas um arquivo, main.c. Ele será utilizado para demonstrar o problema e a solução. Então, nosso repositório está assim agora:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_01.jpeg"><img class="alignnone wp-image-3870" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_01-300x37.jpeg" alt="missing_data_from_stash_01" width="422" height="52" /></a>

e existe apenas um <em>commit</em>:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_02.jpeg"><img class="alignnone wp-image-3869" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_02-300x80.jpeg" alt="missing_data_from_stash_02" width="431" height="115" /></a>

A primeira versão do arquivo é:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_03.jpeg"><img class="alignnone wp-image-3868" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_03-300x159.jpeg" alt="missing_data_from_stash_03" width="434" height="230" /></a>

Vamos começar a codificar alguma coisa. Para este exemplo, não é necessário uma grande mudança, é apenas alguma coisa para colocar no git stash. Para isso, será adicionado apenas uma nova linha. O git-diff após a alteração é:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_04.jpeg"><img class="alignnone wp-image-3867" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_04-300x133.jpeg" alt="missing_data_from_stash_04" width="451" height="200" /></a>

Agora, suponha que você tenha que realizar o <em>pull</em> de novas alterações de um repositório remoto e não quer realizar o <em>commit</em> de suas alterações por que elas não estão terminadas. Assim, você decide joga-las para o <em>stash</em>, baixar as alterações do repositório remoto e aplicar seu código novamente. Por isso, você executa o seguinte comando para mover suas alterações para o git stash:

<code>git stash</code>

Analisando o <em>stash</em> será possível ver que o comando funcionou como o esperado:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_06.jpeg"><img class="alignnone wp-image-3866" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_06-300x48.jpeg" alt="missing_data_from_stash_06" width="469" height="75" /></a>

Neste momento, o código está em um local seguro e o <em>branch master</em> está limpo e o <em>pull</em> das mudanças pode ser realizado. Depois de ter atualizado o <em>branch</em> local com as alterações do <em>branch</em> remoto, é a hora de aplicar o código no <em>master</em> novamente. Vamos supor que acidentalmente você executa:

<code>git stash drop</code>

e depois é possível verifica, com o comando <code>git stash list</code>, que o <em>stash</em> limpou, e que o código foi removido e não foi aplicado no <em>branch master</em>. OMG! Quem poderá nos ajudar? Como você irá ver em breve, o git não apagou o objeto que contem as alterações. Ele apenas removeu a referência para ele. Para provar isso, pode ser usado o git-fsck. Este comando, verifica a conectividade e validade dos objeto na base de dados. Veja que no começo do nosso repositório foi executado o comando git-fsck e a saída foi:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_07.jpeg"><img class="alignnone wp-image-3865" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_07-300x40.jpeg" alt="missing_data_from_stash_07" width="473" height="63" /></a>

Basicamente, git-fsck mostrou os objetos que são inalcançáveis ( flag <code>–unreachable</code> ). Como pode ser visto, ele não mostrou nenhum objeto. Depois que os elementos do <em>stash</em> foram <em>dropados</em>  o git-fsck mostrou:

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_08.jpeg"><img class="alignnone wp-image-3864" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_08-300x71.jpeg" alt="missing_data_from_stash_08" width="499" height="118" /></a>

Na última execução pode ser visto que existem três objeto inalcançáveis. Mas qual deles é o código perdido? Temos que procurar por ele, para isso podemos usar o comando git-show para visualizar o que é cada objeto.

<a href="/assets/wp-content/uploads/2015/10/missing_data_from_stash_09.jpeg"><img class="alignnone wp-image-3863" src="/assets/wp-content/uploads/2015/10/missing_data_from_stash_09-300x147.jpeg" alt="missing_data_from_stash_09" width="508" height="249" /></a>

Ai está! O ID 95ccbd927ad4cd413ee2a28014c81454f4ede82c é a alteração que estávamos procurando e temos que recuperá-lo! Uma possível solução é fazer o <em>checkout</em> do ID em um novo <em>branch</em> ou aplicar o <em>commit</em> diretamente. Neste exemplo será utilizado o git-stash para aplicar o <em>commit</em> no <em>branch master</em> novamente.

<code>git stash apply </code><code>95ccbd927ad4cd413ee2a28014c81454f4ede82c</code>

É importante relembrar, git executa seu <em>garbage collector</em> (gc) periodicamente. Após a execução do gc não será mais possível ver os objetos inalcançáveis.

<strong>Referência:</strong>

<a href="https://git-scm.com/docs/git-fsck">git-fsck</a>

<a href="https://git-scm.com/docs/git-stash">git-stash</a>
