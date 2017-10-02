---
layout: wordpress
title: "Hands on: Sockets em Python"
date: 2015-01-14 00:05:04
author: marcossouza
permalink: /hands-on-sockets-em-python/
image: /assets/wp-content/uploads/2014/12/python-logo.png
categories:
  - Desenvolvimento
tags:
  - linux
  - python
  - script
  - sockets
---

Muitos são os usos dos sockets atualmente e vários exemplos existem através de toda a internet em várias linguagens de programação diferentes. Como é de costume, a solução em Python parece a mais simples de todas as linguagens de programação, e é isto que este artigo vem mostrar. Para ter uma introdução sobre sockets na linguagens C, basta acessar este link do <a title="Introdução a Sockets" href="http://sempreupdate.org/hands-on-introducao-a-sockets-em-c/" target="_blank">SempreUpdate</a>. Este artigo basicamente irá apresentar o mesmo exemplo do artigo citado, mas na linguagem de programação Python.

Segue abaixo um exemplo de um servidor de horas escrito em Python, que na verdade é o mesmo programa em C feito no artigo do <a title="SempreUpdate.org" href="http://sempreupdate.org/hands-on-introducao-a-sockets-em-c/" target="_blank">SempreUpdate</a>, mas convertido em Python:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/sockets_python/server.py" type="text/javascript"></script>

Devidas explicações sobre a funcionalidade do código:

<strong>import socket</strong>
 Aqui estamos incluindo todas as definições e métodos relacionados a sockets para nosso script.

<strong>
 server_sock = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
 server_sock.bind(('0.0.0.0', 9999))
 server_sock.listen(100)</strong>
 A primeira linha mostra a instanciação do novo objeto socket do python, utilizando IP como protocolo de comunicação e TCP como método de transmissão. Já a segunda linha atribui o endereço 0.0.0.0 ao socket, o que significa que o servidor poderá receber requisições de qualquer endereço IP e a porta em que o socket irá "escutar", que neste caso é 9999. Este mesmo número deverá ser utilizado no lado cliente para o correto recebimento da conexão no lado do servidor. E a terceira linha altera o estado do socket para que este comece a "escutar" novas conexões.

<strong>(cli_socket, address) = server_sock.accept()</strong>
 Recebe uma nova conexão de clientes do servidor de horas. Esta chamada fica esperando novas conexões, fazendo com que o processo fique travado até a chegada de uma nova conexão.

<strong>if cli_socket.send(time.ctime(time.time()) + 'n') == 0:</strong>
 Testa o envio de dado para o cliente conectado. O dado neste caso é o envio da hora corrente do sistema. Ao chegar neste ponto, temos a certeza de ter uma conexão estabelecida. O retorno da chamada <em>send</em> é o número de bytes que foram escritos no socket. Se o retorno da chamada for 0, isto significa que o cliente desconectou antes de receber os dados.

<strong>cli_socket.close()</strong>
 Fecha o socket aberto na chamada accept. Esta é uma boa prática pois a cada socket aberto ocupa um lugar na tabela de arquivos abertos no sistema, e este recurso tem um limite máximo. A fim de não consumir recursos do sistema, deve-se sempre fechar o socket quando este não for mais utilizado.

Agora segue o código do client do servidor de horas, que novamente é uma conversão de C para Python do artigo do <a title="Introdução a sockets: parte 2" href="http://sempreupdate.org/hands-on-introducao-a-sockets-em-c-parte-2/" target="_blank">SempreUpdate</a>:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/sockets_python/client.py" type="text/javascript"></script>

As partes previamente explicadas no código do servidor não serão explicadas novamente. Vamos a explicação do código do cliente:

<strong>cli_socket.connect(('127.0.0.1', 9999))</strong>
Aqui nós nos conectamos ao endereço do servidor, que neste caso é 127.0.0.1, que é um endereço que aponta a máquina local. Nos meus testes tanto o servidor quando o cliente estão na mesma máquina. Se você quiser fazer um teste colocando o servidor em outra máquina, então deve colocar o IP do servidor ao invés de 127.0.0.1. Além do IP nós também informamos a porta, que é 9999, sendo esta foi a mesma utilizada no lado do servidor.

<strong>print cli_socket.recv(255)</strong>
Aqui nós estamos recebendo dados do servidor. O valor 255 é o número máximo de bytes que iremos receber do servidor. Este valor foi colocado como um chute, mas em aplicações de produção este valor geralmente é informado como o tamanho de uma estrutura que é compartilhada entre servidor e cliente, ou algum outro número fixado entre o servidor e o cliente.

<strong>cli_socket.close()</strong>
Fechamos o socket, pelo motivo já informado no código do servidor.

Como podemos ver, Python se mostra uma ótima linguagem para prototipação e prova de conceito. Notamos também como sua sintaxe é simples, e que com poucas linhas nós podemos fazer simples aplicações.

Espero que tenham gostado desta introdução a sockets com Python. Não se esqueçam de curtir nossa página no Facebook e de nos seguir no Google+ para receber novos artigos em primeira mão. Até a próxima!