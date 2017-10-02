---
layout: wordpress
title: Geração de MD5 utilizando C com OpenSSL e Python
excerpt: |
  Esta postagem mostra como gerar MD5 via código C (utilizando a biblioteca OpenSSL) e com Python (utilizando a biblioteca hashlib).
date: 2015-03-10 21:19:49
author: marcossouza
permalink: /geracao-de-md5-utilizando-c-com-openssl-e-python/
image: /assets/wp-content/uploads/2015/03/Sem-título-1.png
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - python
---

Atualmente o MD5 é utilizado para muitas finalidades, sendo uma delas a verificação da integridade de arquivos. Para tal é possível utilizar o binário md5sum, presente no pacote coreutils. Mas algumas vezes é necessário fazer esta verificação dentro de um programa, podendo é claro chamar o md5sum de dentro do programa, mas este problema pode ser melhor resolvido utilizando a biblioteca OpenSSL, que contém funções para geração de MD5. Segue abaixo um exemplo utilizando a linguagem C:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/md5/md5_generator.c" type="text/javascript"></script>

Segue agora uma explicação sobre o código acima:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/md5/md5_generator.c?slice=8:18&amp;lang=C" type="text/javascript"></script>
Verificação de parâmetros. É necessário passar um parâmetro para o programa, sendo que este parâmetro precisa ser o caminho para um arquivo. Após checar o parâmetro, o arquivo é aberto para leitura.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/md5/md5_generator.c?slice=20:21&amp;lang=C" type="text/javascript"></script>
 O código cria uma variável de "contexto de MD5" e o inicia. Esta variável irá conter todo o conteúdo do arquivo passado como parâmetro para então poder gerar o MD5.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/md5/md5_generator.c?slice=23:29&amp;lang=C" type="text/javascript"></script>
Nesta parte do código o arquivo então é lido, e a cada 1024 bytes lidos o contexto é atualizado com o conteúdo do arquivo. A chamada <em>fread</em> é quem faz esta leitura, e a cada leitura a variável buf recebe os 1024 bytes, e é com a variável que o contexto é atualizado.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/md5/md5_generator.c?slice=31:33&amp;lang=C" type="text/javascript"></script>
 Após ler todo o conteúdo do arquivo, nós então podemos fechá-lo. A chamada MD5_Final recebe um contexto e gera o MD5. Este MD5 gerado então é colocando na variável <em>digest</em>.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/md5/md5_generator.c?slice=36:40&amp;lang=C" type="text/javascript"></script>
Nesta parte nós convertemos o <em>digest</em>, que é um <em>unsigned char</em> para um "signed char". Para tal, precisamos pegar a forma hexadecimal de cada byte do <em>digest</em> e alocar dentro de <em>converted</em>. Como a representação de cada bytes em hexadecimal tem o tamanho de dois bytes, reservar dois bytes do "converted" para cada bytes lido do "digest". E após este, o MD5 gerado é impresso.

Antes de compilarmos o pacote, é necessário ter o pacote com a biblioteca do OpenSSL. Para instalar em distribuições derivadas do Red Hat, execute:
<em>sudo yum install openssl-devel</em>

Já para instalar em distribuições derivadas do Debian, execute:
<em>sudo apt-get install libssl-dev</em>

Tendo instalado o pacote, vamos compilar o programa com o GCC e linkar com a biblioteca crypto do OpenSSL:
<strong>gcc md5_generator.c -o md5_generator -lcrypto</strong>

Após compilador, vamos fazer um teste utilizando o programa compilador e comprar a saída do programa md5sum:
<strong>[marcos@localhost md5]$ ./md5_generator md5_generator.c
354218ad04939339944ce5994504d6ad md5_generator.c
[marcos@localhost md5]$ md5sum md5_generator.c
354218ad04939339944ce5994504d6ad md5_generator.c
</strong>

Após executar o programa compilado e o md5sum no arquivo fonte do programa, verificamos que ambos mostram o mesmo valor.

Agora vejamos como fazer o MD5 com o Python:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/md5/md5_generator.py" type="text/javascript"></script>

Como já era esperado, o código em python parece mais simples do que a versão em C. Vejamos agora uma breve explicação sobre este código:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/md5/md5_generator.py?slice=1:13" type="text/javascript"></script>
Esta parte do código importa o módulo hashlib (necessário para gerar o MD5), valida o parâmetro do programa, e abre o arquivo. Estas mesmas verificações são feitas no código em C.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/md5/md5_generator.py?slice=15:18" type="text/javascript"></script>
 Aqui é então criada um objeto md5, que seria equivalente ao MD5_Context do C, e então o arquivo do parâmetro vai sendo lido e o md5 é atualizado.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/md5/md5_generator.py?slice=20:21" type="text/javascript"></script>
O arquivo é então fechado e o "digest" é então impressora já na forma em hexadecimal.

Podemos testar novamente este programa fazendo o MD5 do próprio script em python:
<strong>[marcos@localhost md5]$ python md5_generator.py md5_generator.py
3c7a3dc1955f630924c555d5f5331528 md5_generator.py
[marcos@localhost md5]$ md5sum md5_generator.py
3c7a3dc1955f630924c555d5f5331528 md5_generator.py</strong>

Espero que tenham gostado do artigo, e que ele seja útil se acaso precisarem deste tipo de recurso. Não se esqueça de se inscrever nas redes sociais e no nosso feed para saber quando um novo artigo é postado. Até mais!