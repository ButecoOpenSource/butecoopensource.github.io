---
layout: wordpress
title: Laravel 5 do começo ao fim [parte 1]
date: 2015-02-18 19:28:23
author: jaswdr
permalink: /tutorial-laravel-5/
image: /assets/wp-content/uploads/2015/02/Laravel-5.png
categories:
  - Desenvolvimento
tags:
  - framework
  - laravel
  - laravel 5
  - php
---

Mostrarei a seguir um breve tutorial sobre o Laravel, um dos frameworks mais usados atualmente para PHP, com o lançamento do Laravel 5 houve algumas mudanças, e algumas delas você verá a seguir.
<h3 style="text-align: center;"><strong>Instalação</strong></h3>
<h5>Composer</h5>
Inicialmente caso já não o tenha, faça a instalação do <strong>composer</strong>, o composer é um controlador de dependências, o laravel assim como a maioria dos frameworks atuais o utilizam, o site do composer que pode ser acessado por este <a href="https://getcomposer.org/download/">link</a> mostra como fazer a instalação.
<h5>Criando um novo projeto</h5>
O comando abaixo criará um projeto novo do laravel 5 usando o composer e fará a instalação das dependências:
<pre><code>composer create-project laravel/laravel --prefer-dist</code></pre>
Uma vez instalado você verá uma lista de pastas, abaixo coloco uma breve descrição do que existe em cada uma:

<strong>app/</strong>
Diretório dos arquivos da sua aplicação

<strong>bootstrap/</strong>
Arquivos de inicialização, são chamados em cada requisição ao servidor

<strong>config/</strong>
Arquivos de configuração como banco de dados, serviços, etc.

<strong>database/</strong>
Aqui existem basicamente duas pastas,  <strong>"migrations"</strong> que guardam os arquivos que fazem as alterações na estrutura do banco, como nome das tabelas, colunas, etc, e <strong>"seeds"</strong> que seriam arquivos e classes que geram registros no banco de dados, seja para testes ou para possuir informações iniciais de utilização.

<strong>public/</strong>
São os arquivos públicos do sistema, normalmente é aqui que são colocados os arquivos de imagens, CSS e JS.

<strong>resources/</strong>
Arquivos de recursos como bibliotecas JS e CSS, arquivos com arrays de traduções de mensagens, normalmente usados numa aplicação multilinguagem e as próprias views do sistema.

<strong>storage/</strong>
Arquivos de cache, sessões (quando usado armazenamento em arquivo), views compiladas e logs.

<strong>tests/</strong>
Arquivos de testes do sistema.

<strong>vendor/</strong>
pasta criada pelo composer para controle e versionamento de bibliotecas.
<h3 style="text-align: center;"><strong>Configuração</strong></h3>
<h5>Banco de Dados</h5>
O arquivo de configuração de banco de dados está na pasta <strong>config/database.php</strong>, abrindo esse arquivo você perceberá que ele basicamente retorna um array, o laravel permite a utilização de vários bancos, você pode se conectar e utilizar diferentes conexões para diferentes bancos, inclusive mais de uma, porém para esse tutorial utilizarei apenas o banco mysql, que inclusive vem configurado por padrão.

Neste ponto já se percebe uma mudança de versões anteriores do laravel, os valores de <strong>host, database, username, password</strong> estão vindo de variáveis de ambiente, isto permite uma maior flexibilidade, pois você pode ter diferentes valores para produção e teste, estas variáveis são carregadas a partir do arquivo <strong>".env"</strong> que está localizado na raiz do projeto, apenas observando que no linux todo arquivo que inicia com "." fica oculto, então se por acaso o arquivo não estiver aparecendo vá ao terminal e na raiz do projeto e execute um <strong>"nano .env"</strong> que se abrirá o arquivo no nano para edição.

Altere as informações do arquivo .env com as informações do seu banco.
<h5>Artisan</h5>
O Laravel utiliza o artisan como programa de linha de comando para execução de algumas tarefas digitando o comando abaixo na raiz do projeto você verá diversos comandos possíveis e uma breve explicação do que cada um faz.
<pre><code>php artisan list</code></pre>
A maioria dos comandos é <span style="color: #000000;">quase</span> autoexplicativa mas não entrarei em grandes detalhes nesse tutorial, como fizemos a configuração do banco de dados no item anterior podemos verificar a instalação com o comando abaixo.
<pre><code>php artisan migrate:install</code></pre>
Este comando criará uma tabela no banco chamada<strong>"migrations"</strong> que o laravel utiliza para verificar quais migrações foram executadas e quais não, apenas deixando mais claro, na prática uma migração é um arquivo que fica localizado em <strong>database/migrations</strong> e faz alterações no banco, como criar e alterar tabelas, mudar nomes de bancos, etc, e isto vale para qualquer banco que o laravel tem suporte, você pode por exemplo recriar toda a estrutura do seu banco ou até mesmo atualizá-la de maneira automática, podendo também regredir essas alterações, pois cada migration tem basicamente dois métodos, <strong>up</strong> e <strong>down</strong>, que como o nome sugere, o primeiro realiza as alterações e o segundo desfaz, apesar disso ser responsabilidade do programador considero como algo bastante útil quando se está trabalhando com bases em produção pois você conseguirá criar pacotes de atualização e caso ocorra qualquer problema podes desfaze-las.

Após executar o comando a mensagem<strong><span style="color: #00ff00;"> "Migration table created successfully"</span></strong> deve ser exibida, do contrário, possivelmente algum parâmetro foi passado errado no arquivo <strong>".env</strong><strong>"</strong>.

O Laravel 5 em especial já vem sua parte de autenticação pré-criada, mas para utilizá-la precisamos migrar o servidor para que as tabelas sejam criadas com o seguinte comando:
<pre><code>php artisan migrate</code></pre>
Com isso aparecerá no terminal que duas migrações foram instaladas, a <strong>create_users_tables</strong> que cria a tabela de usuários, e a <strong>create_password_resets_table</strong> que cria a tabela de reset de senhas.

Com isso podemos executar o comando seguinte para iniciar o servidor de testes do php por um atalho do artisan
<pre><code>php artisan serve</code></pre>
Acessando o endereço <strong>http://localhost:8000</strong>, aparecerá a página de bem-vindo do laravel, escrito Laravel 5 num tom quase branco, horrível e de muito mal gosto por sinal, e entrando no endereço <strong>http://localhost:8000/home</strong>, aparecerá a tela de login e registro padrão, algo que provavelmente você perderia um bom tempo em outros frameworks, vem pronto para ser utilizado aqui.

Bem pessoal, essa foi a primeira parte do tutorial sobre laravel, aguarde a próxima parte e comentem caso tenham gostado, vlws o/.