---
layout: wordpress
title: Laravel 5 do começo ao fim [parte 3]
excerpt: |
  Este artigo apresenta a terceira parte de um tutorial sobre o framework PHP Laravel 5, apresentando como usar a parte de criação de model e view do framework
date: 2015-03-24 20:43:06
author: jonathanaschweder
permalink: /laravel-5-do-comeco-ao-fim-parte-3/
image: /assets/wp-content/uploads/2015/02/Laravel-5.png
categories:
  - Desenvolvimento
tags:
  - desenvolvimento
  - framework
  - laravel
  - laravel 5
  - mvc
  - php
  - tutorial
  - web
---

Fala pessoal, hoje veremos finalmente a parte de Model e View do laravel 5, caso você não esteja familiarizado com o conceito de MVC veja as outras partes dessa série nos links abaixo:
<ul>
	<li><a href="/2015/02/18/tutorial-laravel-5/" target="_blank">Parte 1</a></li>
	<li><a href="/2015/03/09/tutorial-laravel-5-parte-2/" target="_blank">Parte 2</a></li>
</ul>
Considerando que anteriormente na parte 2 criamos um controller chamado <i>TarefaController</i>, criaremos agora o Model <i>Tarefa</i> que representará os registros da tabela Tarefa.

Execute o comando abaixo na raiz do projeto para criar um novo Model:
<pre><code>php artisan make:model Tarefa</code></pre>
Esse comando criará basicamente duas coisas, o Model propriamente dito no diretório <i>app/</i> e criará uma nova migration em <i>database/migrations</i>. Vamos antes de mais nada adicionar alguns campos a nossa migration.

Abrindo o arquivo de migration criado (algo como create_table_tarefa) você verá basicamente uma classe que estende de outra classe chamada <i>Migration</i>, e dois métodos <i>up</i> e <i>down</i> como já explicado anteriormente, edite esse arquivo para ficar como abaixo:

<script src="https://gist.github.com/jaschweder/31f5dfbedbaa47dbbe9d.js"></script>Basicamente adicionamos dois novos campos a migration, <i>titulo</i> e <i>corpo</i> das nossas tarefas, além disso o comando make já nos adiciona um campo chamado <i>id</i> do tipo inteiro para ser nossa chave primária com auto incremento, ou seja, sempre que for adicionado um novo registro não é preciso setar o campo id, pois esse é gerado pelo banco. E no final são adicionados os campos <i>created_at</i> e <i>updated_at</i> que como você provavelmente deve suspeitar um é a data e hora de criação e o outro da última atualização respectivamente, sendo o tipo normalmente timestamp para esses dois campos. Feito a adição dos campos vamos migrar nosso banco para que ele crie a tabela com o comando abaixo:

<pre><code>php artisan migrate</code></pre>

Obs.: Estou considerando que você viu as outras partes dessa série, porém caso ocorra algum erro normalmente podem ser duas coisas, configuração incorreta do arquivo <i>.env</i> na raiz do projeto ou provavelmente você não executou o comando

<pre><code>php artisan migrate:install</code></pre>

para criar a tabela de migrations no banco. Com o comando executado com sucesso temos certeza que a tabela foi criada com os devidos campos, com isso podemos partir para o Model propriamente. Abra o arquivo chamado <i>Tarefa.php</i> no diretório <i>app/</i>, nesse arquivo está presente uma classe chamada <i>Tarefa</i> que estende da classe <i>Model</i>, a classe base do Eloquent para criar models. Nesse ponto apenas para facilitar adicionaremos os campos de nossa tabela numa variável da classe chamada <i>$fillable</i> como mostrado abaixo:

<pre><code>protected $fillable = array('titulo', 'corpo');</code></pre>

Na documentação do laravel disponível <a href="http://laravel.com/docs/4.2/eloquent#mass-assignment">aqui</a> isso disponibilizará essas colunas como <i>Mass Assignment</i> que possibilitará criar novos registros simplesmente usando o método <i>create</i> e outros da classe Model passando um array associativo as colunas da classe, como no exemplo abaixo:

<pre><code>$tarefa = Tarefa::create(['titulo'=&gt;'Título da tarefa','corpo'=&gt;'Corpo da tarefa...']);</code></pre>

Pois bem, uma vez adicionado as colunas a essa variável podemos partir para o controller e também criar nossas <i>Views</i>. Vamos então criar um novo arquivo chamado <i>index.blade.php</i> no diretório <i>resources/views/tarefa</i>, que fará a listagem das nossas tarefas, como mostrado abaixo:<script src="https://gist.github.com/jaschweder/5a094ac5518126f87dbc.js"></script>

Observem que não estou entrando em grandes detalhes, pois a própria documentação do laravel é suficiente para estudos mais profundos.

Agora que temos nossa view de listagem precisamos enviar os dados para ela, lembre-se no MVC a View tem a única responsabilidade de mostrar dados passados pelo controller, portanto no nosso <i>TarefaController</i> na função <i>index</i> vamos adicionar o seguinte código:
<pre><code>$tarefas = Tarefa::orderBy('id')-&gt;get();
return view('tarefa.index',compact('tarefas'));</code></pre>
Isso passará um objeto chamado <i>Collection</i> padrão do laravel para representar uma coleção, essa Collection possui diversas funções interessantes que você pode verificar na documentação ou na API do laravel no site.

Para ter certeza que nenhum erro está ocorrendo, execute o comando <i>php artisan serve</i> e acesse o endereço <a href="http://localhost:8000/tarefa">http://localhost:8000/tarefa</a>.

Obviamente nesse momento como não temos nenhuma tarefa cadastrada nada será mostrado, vamos então criar um formulário para cadastro de tarefas.

Primeiramente crie um novo arquivo chamado <i>create.blade.php</i> na mesma pasta <i>tarefa</i> onde está localizado o arquivo index, dentro desse arquivo virá nosso formulário com os campos para cadastro.

<script src="https://gist.github.com/jaschweder/f5d421dd8d5c19d31aff.js"></script>Apenas algumas considerações, para criarmos formulários no laravel poderíamos utilizar a classe utilitária <i>Form</i> que no laravel 5 não vem por padrão, porém optei por usar dessa forma por simplicidade no entendimento. O campo <i>_token</i> precisa ser coloca pois o laravel possui um tratamento de ataque de CSRF, que basicamente é evitar que alguém mal intencionado consiga realizar requisições POST,PUT e DELETE de fora do site. Por fim estou usando a classe helper URL para me retornar a URL completa para o método store do controller TarefaController. O método <i>store</i> do controller fará o cadastro efetivamente, ficando da seguinte forma:<script src="https://gist.github.com/jaschweder/684fab4a816e2f90afba.js"></script>

Isso criará uma nova tarefa e redirecionará para a página de index do controller.

Bem pessoal esse foi um exemplo usando Model, View e Controller, claro que é um exemplo apenas ilustrativo, faltaria outras funcionalidades, porém peço que para informações mais profundas sempre tenham em mãos a documentação do laravel, lembre-se que ela é sua bíblia, estarei na próxima parte mostrando um pouco sobre a parte de testes do laravel e um exemplo de workflow muito utilizado atualmente que é o <i>TDD</i> ou <i>Desenvolvimento Dirigido por Testes</i> em tradução livre, escrevam nos comentários o que acharam e até a próxima pessoal.