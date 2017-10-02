---
layout: wordpress
title: "libssl e libcrypto: Visualizando certificados online em C"
excerpt: |
  Breve introdução a libssl para extrair informações de certificados digitais de servidores.
date: 2016-05-23 23:34:46
author: marcossouza
permalink: /libssl-libcrypto-visualizando-certificados-online-em-c/
image: /assets/wp-content/uploads/2016/05/openssl-3.png
categories:
  - Desenvolvimento
tags:
  - c
  - certificados
  - certs
  - libcrypto
  - libssl
  - linux
  - openssl
---

Muito se fala do OpenSSL para geração e manutenção de certificados digitais, além disso, o OpenSSL pode criptografar arquivos, gerar números randômicos, e etc. Este artigo vem mostrar como utilizar a libssl para visualizar certificado utilizando a linguagem C.
<!--more-->

<strong>libssl e libcrypto</strong>
As bibliotecas libcrypto e libssl são fornecidas pelo OpenSSL, contendo rotinas fundamentais de criptografia e implementação de TLS/SSL, respectivamente. Grande parte dos programas que suportam HTTPS utilizam as bibliotecas libssl e/ou libcrypto. Exemplos de programas são wget, curl, ssh, e o próprio openssl.

<strong>Exemplo</strong>
O código a seguir mostra como utilizar estas bibliotecas a fim de visualizar dados de certificados online de qualquer servidor utilizando HTTPS.

<script src="//gistfy-app.herokuapp.com/github/marcosps/experimentations/ssl/ssl_socket/src/extract_server_info.c?branch=master&amp;lang=cpp&amp;style=github" type="text/javascript"></script>

Vamos aos detalhes do código:

<strong>BIO</strong>
BIO é uma abstração de I/O utilizada pelo OpenSSL. Com ele, pode-se simplificar leitura/escrita de arquivos, conexões inseguras via socket e SSL. No código acima existem dois BIOs, um para basicamente escrever no <em>stderr</em> e outro que funciona como um socket client.

<strong>X509</strong>
É um padrão utilizado para gerenciar certificados digitais e encriptação. No OpenSSL, ele armazena o certificado em si. No exemplo acima, a chamada <em>SSL_get_peer_certificate</em> retorna um ponteiro para uma estrutura X509, contendo o certificado do servidor.

<strong>SSL_CTX</strong>
Esta estrutura contém os parâmetros e métodos que serão utilizados pelo OpenSSL. Na inicialização é informado os protocolos suportados pelo cliente ou servidor (neste caso cliente). O protocolo utilizado será a mais recente suportada por ambos, cliente e servidor. Após criada, essa struct será utilizada para criar a conexão SSL em si.

<strong>SSL</strong>
Esta struct contém os dados da conexão em si. Na criação, ela herda todas as configurações da SSL_CTX, como métodos suportados e configurações.

<strong> </strong>
<h3>Fluxo do código</h3>
Basicamente o programa começa esperando como parâmetro uma URL de um servidor que aceita HTTPS. Após este, utilizamos a chamada <em>SSL_load_error_strings</em> para carregar as strings de erro de SSL, para mostrarmos quando algum erro acontecer.

Utilizamos a chamada BIO_new_fp, apontando para <em>stderr</em>, para imprimir errors na saída de erros do C, e SSL_library_init para carregar as funções e protocolos do SSL.

Criamos uma estrutura BIO que servirá como um client socket, setando hostname e porta, sendo que esta ultima aceita protocolos como HTTP e HTTPS ao invés da porta. Após o connect to BIO, a struct SSL_CTX é criada com suporte a SSLv2 e SSLv3, e desabilitamos a versão 2 por suas vulnerabilidades (https://drownattack.com/).

A struct SSL_CTX é utilizada para criar a SSL. Esta nova struct SSL é então atrelada ao BIO de conexão criado anteriormente, e assim executando um SSL_connect. Esta chamada inicia o <em>handshake</em>, ou o "aperto de mão", entre o cliente e servidor, configurando a conexão segura. Se o retorno desta chamada for diferente de -1, então estamos em uma conexão segura com o servidor.

Com a estrutura SSL já configurada e pareada com o servidor, conseguimos imprimir quais os tipos de encriptação que são suportados pelo servidor e solicitamos que o servidor envie seu certificado com a chamada <em>SSL_get_peer_certificate</em>, populando o ponteiro para a struct X509. Com o certificado do servidor em mãos, podemos extrair algumas informações dele, e até mesmo quem foi a Autoridade Certificado (CA) que assinou este certificado.

Para compilar o código, execute:
<code>gcc extract_server_info.c -o extract_server_info -lssl -lcrypto</code>

Ao executar o programa exemplo com o site da HP, obtemos a seguinte saída:
<samp>[marcos@xfiles ssl_socket]$ ./bin/extract_server_info www.hp.com
Connected with DHE-RSA-AES256-SHA encryption
Cipher version: TLSv1/SSLv3
Remote certificate info
Subject: C=US, ST=California, L=Palo Alto, O=Hewlett-Packard, OU=Operations, CN=www.hp.com
Issuer: C=US, O=Symantec Corporation, OU=Symantec Trust Network, CN=Symantec Class 3 Secure Server CA - G4</samp>

Podemos ver nesta saída que, o ramo de operações da HP fica situado na Califórnia, nos EUA, e que a Autoridade certificadora foi a Symantec.

Espero que tenham gostado desta breve introdução a libssl e libcrypto! Estamos aguardando por seus comentários! Até a próxima!

Referências:
<a href="http://linuxaria.com/howto/openssl-7-usi-pratici" target="_blank">7 Practical uses of Openssl</a>
<a href="https://wiki.openssl.org/index.php/Libcrypto_API" target="_blank">OpenSSL WIki - libcrypto API</a>
<a href="https://wiki.openssl.org/index.php/Libssl_API" target="_blank">OpenSSL WIki - libssl API</a>
<a href="https://www.openssl.org/docs/manmaster/crypto/bio.html" target="_blank">OpenSSL BIO man</a>
<a href="https://www.openssl.org/docs/manmaster/crypto/x509.html" target="_blank">OpenSSL X509 man</a>
<a href="https://en.wikipedia.org/wiki/X.509" target="_blank">Wikipedia X509</a>