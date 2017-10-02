---
layout: wordpress
title: Cliente / Server com Boost.Asio
excerpt: |
  Artigo que mostra um exemplo da utilização da biblioteca boost com asio.
date: 2015-04-27 16:23:46
author: marcossouza
permalink: /cliente-server-com-boost-asio/
image: /assets/wp-content/uploads/2015/04/boost.png
categories:
  - Desenvolvimento
tags:
  - boost
  - c
---

Neste post vamos mostrar como criar um cliente/servidor com Boost.Asio. Para quem não conhece, boost é uma library para programação network cross-plataform. Então para este exemplo, você deve estar certo que tenha as libraries do Boost. Caso não tenha, rode o seguinte comando para instalar emj uma distribuição Debian-like:

<strong>sudo apt-get install libboost-all-dev</strong>

E para instalar em uma dsitribuição Red Hat-like:

<strong>sudo yum install boost-devel</strong>

O Boost.Asio e outras libraries podem ser instalado separadamente, mas como neste artigo à intenção é mostrar como utilizar o asio, não o instalaremos com mais detalhes. Então vamos lá para nosso server:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?lang=c++" type="text/javascript"></script>

Explicação do código:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?slice=7:7&amp;lang=c++" type="text/javascript"></script>
É responsável por facilitar as operações assincronas, ele é quem faz a mágica entre software e OS. Outro ponto importante a ser citado é que ele trabalha em casos onde não exista threads explicitamente criadas, e as cria para você, caso necessário.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?slice=8:8&amp;lang=c++" type="text/javascript"></script>
 Aqui nós criamos os dados para nossa conexão, passando o IP e Porta. Já tcp::v4() é indica que utilizaremos uma conexão TCP/IPv4. 2000 é a porta em que vamos conectar.

Assim criamos uma acceptor para “escutar“ novas conexões.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?slice=11:11&amp;lang=c++" type="text/javascript"></script>

Temos que criar um Handler para ser passado para funções async_write e async_read_some. Usamos uma função lambda neste exemplo, mas poderia ser feito de uma forma talvez mais clara com uma declaração de função void(const boost::system:error_code&amp;, std::size_t);

Bom, seguindo em frente
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?slice=15:16&amp;lang=c++" type="text/javascript"></script>

Assim chegamos ao ponto onde criamos nosso socket para aceitar conexão de clientes.
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?slice=18:23&amp;lang=c++" type="text/javascript"></script>

Então criamos nosso buffer, para receber os dados enviados pelo cliente. Vamos utilizar um número máximo de 1024 bytes para escrita, então chamamos o async_write, para realizar a escrita no char msg[_size], também é passado nosso handler , em seguida fazemos a leitura no async_read_some e imprimimos o valor.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/server.cxx?slice=25:25&amp;lang=c++" type="text/javascript"></script>
 Agora indicamos ao io_service que nosso trabalho foi concluído. E isso é oque precisamos saber sobre no server com Boost.Asio. Para compilar com gcc execute faça o seguinte:

<strong> g++ -o server server.cxx -std=c++0x -lboost_system</strong>

No cliente vamos criar a conexão com o nosso server, passando os dados de conexão e mensagem por CLI. Vamos ao código:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/client.cxx?lang=c++" type="text/javascript"></script>

Explicações:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/client.cxx?slice=7:11&amp;lang=c++" type="text/javascript"></script>
 Verificamos primeiro se todos os argumentos foram passados, caso não tenha todos os parâmetros, termina execução.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/client.cxx?slice=13:16&amp;lang=c++" type="text/javascript"></script>
Como no server, temos que criar um io_service para nossas ações assíncronas, e também um socket. No tcp::resolver ele tem o trabalho de criar os dados de um endpoint e assim fazermos a conexão com o server com o boost::asio::connect, que recebe nosso socket e também um resolve, que recebe os valores de IP e Porta passados pelo CLI.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/asio/client.cxx?slice=18:20&amp;lang=c++" type="text/javascript"></script>
Criamos nossa varável e um tamanho máximo para o buffer, e então fazemos a escrita. Agora compilamos nosso cliente:

<strong>g++ -o client client.cxx -std=c++0x -lboost_system -lpthread</strong>

Assim podemos rodar o server e abrir um cliente

<strong>./server</strong>

Então enviamos dados de um cliente

<strong>./client 127.0.0.1 2000 “Exemplo simples com Boost.Asio”</strong>

E por fim criamos um Cliente/Servidor cross-plataform com facilidade. Essa foi uma apresentação do Boost.Asio. Você pode se aprofundar muito mais, nessa incrível lib para programação network.

Obrigado!

<strong>Enviado pelo colaborador Willian Briotto.</strong>