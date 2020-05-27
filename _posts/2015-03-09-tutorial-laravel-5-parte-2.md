---
layout: wordpress
title: Laravel 5 do começo ao fim [parte 2]
date: 2015-03-09 07:59:57
author: jaswdr
permalink: /tutorial-laravel-5-parte-2/
image: /assets/wp-content/uploads/2015/02/Laravel-5.png
categories:
  - Desenvolvimento
tags:
  - controller
  - framework
  - http
  - laravel
  - laravel 5
  - model
  - mvc
  - php
  - rotas
  - view
---

Esta é a segunda parte do tutorial sobre Laravel 5, caso você não tenha ainda visto, veja a primeira parte dessa série neste <a href="/tutorial-laravel-5">link</a>.

Continuando o tutorial vamos agora partir para a parte MVC do framework, o laravel assim como a maioria dos frameworks utiliza esse conceito, veja abaixo uma tabela explicativa:
<table>
<tbody>
<tr>
<td><strong>M</strong>odel = Camada que faz a interface com as tabelas do banco de dados</td>
</tr>
<tr>
<td><strong>V</strong>iew = Camada de visualização propriamente</td>
</tr>
<tr>
<td><strong>C</strong>ontroller = Camada que faz a ligação entre "M" e "V"</td>
</tr>
</tbody>
</table>
<h3 style="text-align: center;">Mão na massa</h3>
Vamos antes de mais nada criar nossas rotas, afinal, são através delas que nossas funções serão disponibilizadas, o arquivo de rotas fica em <b>app/Htpp/routes.php</b>, caso você não conheça o protocolo HTTP, abaixo vai uma tabela rápida de contextualização de alguns métodos.
<table>
<tbody>
<tr>
<td><b>GET</b></td>
<td>Método de chamada padrão utilizado para requisitar um recurso do servidor.</td>
</tr>
<tr>
<td><b>POST</b></td>
<td>Método de chamada utilizado para enviar dados de inserção no servidor</td>
</tr>
<tr>
<td><b>PUT</b></td>
<td>Método de chamada utilizado para enviar dados de atualização no servidor</td>
</tr>
<tr>
<td><b>DELETE</b></td>
<td>Método de chamada utilizado para enviar dados de exclusão no servidor</td>
</tr>
</tbody>
</table>
Existem outros métodos do protocolo HTTP, porém estes são normalmente os mais utilizados.

Abrindo este arquivo, você verá que basicamente está sendo chamado a classe <i>Route</i> que é a classe que cria as rotas no laravel, com algumas rotas já definidas, na documentação do laravel disponível neste <a href="http://laravel.com/docs/4.2/routing">link</a> você verá todas as possibilidades de rotas, para este exemplo vamos fazer uma lista de tarefas com as seguintes rotas:
<table>
<thead>
<tr>
<th>Método HTTP</th>
<th>Caminho</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr>
<td><b>GET</b></td>
<td><b>/tarefa</b></td>
<td>Listagem de todas as tarefas</td>
</tr>
<tr>
<td><b>GET</b></td>
<td><b>/tarefa/create</b></td>
<td>Formulário de cadastro</td>
</tr>
<tr>
<td><b>GET</b></td>
<td><b>/tarefa/edit</b></td>
<td>Formulário de edição</td>
</tr>
<tr>
<td><b>POST</b></td>
<td><b>/tarefa</b></td>
<td>Ação de cadastrar efetivamente</td>
</tr>
<tr>
<td><b>PUT</b></td>
<td><b>/tarefa</b></td>
<td>Ação de atualizar efetivamente</td>
</tr>
<tr>
<td><b>DELETE</b></td>
<td><b>/tarefa</b></td>
<td>Ação de excluir efetivamente</td>
</tr>
</tbody>
</table>
Para criar estas rotas precisamos simplesmente adicionar a seguinte linha no arquivo <i>routes.php</i>:
<pre><code>Route::resource('tarefa', 'TarefaController');</code></pre>
Conforme a documentação do laravel, este comando cria rotas para um serviço <strong>RESTful</strong>, a lista completa das rotas geradas e outras formas de rotas você pode ver neste <a href="http://laravel.com/docs/5.0/routing">link</a>.

Lembrando apenas que ainda não criamos nosso controller, para isso precisamos executar o seguinte comando no terminal na raiz do projeto:
<pre><code>php artisan make:controller TarefaController</code></pre>
Um arquivo chamado <i>TarefaController.php</i> será criado no diretório <b>app/Http/Controllers</b>. Abrindo este arquivo podemos ver que foi criado uma classe "esqueleto" para nós já com todos os métodos necessários. Para provar que não estou mentindo e que tudo está funcionando adicione a seguinte linha no método <b>index</b> dessa classe:
<pre><code>return 'Olá Mundo com Laravel 5';</code></pre>
Depois execute no terminal o seguinte comando:
<pre><code>php artisan serve</code></pre>
Isso iniciará o servidor de testes do laravel na porta 8000 da máquina atual, portanto acesse o endereço <a href="http://localhost:8000">http://localhost:8000</a> para ver a página inicial do laravel, agora acessando o endereço <a href="http://localhost:8000">http://localhost:8000/tarefa</a> que chamará via método <strong>GET</strong> a rota <b>/tarefa</b> que está associado ao controller TarefaController pelas nossas rotas no método <b>index()</b> e portanto o texto "Olá Mundo com Laravel 5" deve ser exibido na tela.

Pois bem, galera esse tutorial vai ficar grande e estou separando em mais partes, na próxima parte mostrarei a parte de Models e Views e, por fim, parte de testes com os novos recursos do Laravel 5, espero que estejam gostando, aguardem pelas próximas postagens.
