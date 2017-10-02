---
layout: wordpress
title: Utilizando atexit com C e Python
date: 2015-02-08 18:00:09
author: marcossouza
permalink: /utilizando-atexit-com-c-e-python/
image: /assets/wp-content/uploads/2015/02/saida.jpg
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - python
---

<p style="text-align: justify;">Em muitos casos, quando escrevemos programas se faz necessário liberar os recursos que o programa requisitou do sistema operacional. A função <em>atexit</em> existe para este fim. Com ela podemos escrever funções que serão chamados no término do processo, onde é o lugar ideal para liberar os recursos que foram adquiridos pelo processo. Segue abaixo um exemplo da função em C:</p>
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_c/atexit.c" type="text/javascript"></script>Para compilar, basta invocar o gcc: <strong>gcc atexit.c -Wall -o atexit</strong> Alguns usos do <em>atexit</em> que podemos:

<ul>
<ul>
	<li> Excluir arquivos ao término do processo.</li>
</ul>
</ul>

&nbsp;

<ul>
<ul>
	<li>Enviar um sinal a outro processo que depende deste que está sendo encerrado.</li>
</ul>
</ul>

&nbsp;

<ul>
<ul>
	<li>Enviar uma mensagem para algum socket informando o término do processo.</li>
</ul>
</ul>

&nbsp;

A função <em>atexit</em> espera uma função como parâmetro, função esta que irá ser invocada, ou "registrada", no término do processo. Para ser registrada, a função não deve esperar por nenhum parâmetro. A função sempre é chamada quando o processo termina normalmente. Quando o processo é terminado por um <em>signal </em>não tratado, ou utilizando a chamada <em>_exit. </em>Esta última encerra o processo <strong>imediatamente</strong>, e por isto a chamada do <em>atexit </em>não é efetuada. Outro fator interessante: é possível registrar várias funções com o <em>atexit, </em>mas estas irão ser invocadas na ordem inversa ao qual foram registradas, como mostrado no exemplo. Isto se deve ao fato de algumas implementações irem alocando recursos que dependem de outros recursos. Por exemplo, um programa pode criar um socket, e alocar memória para enviar uma estrutura por este socket. Poderia ser criado uma função para fechar o socket (esta sendo registrada no <em>atexit</em>) e outra função para desalocar a memória (também sendo registrada com o <em>atexit</em>). Pela ordem dos fatos, deveríamos inicialmente desalocar a memória e depois fechar o socket. Pelo simples registro das funções no <em>atexit</em>, esta ordem inversa será respeitada. A função <em>atexit </em>tem a limitação de não poder registrar uma função com parâmetros. Para solucionar este problema foi criada a chamada <em>on_exit</em>. Esta se comporta da mesma forma que a <em>atexit</em>, exceto que a função passada como parâmetro da chamada recebe dois parâmetros, sendo um deles um inteiro como o status final do processo, e o outro é um <em>void *</em> que será passado ao processo quando este for chamado. Seu funcionamento é exatamente o mesmo do <em>atexit </em>e por isto se torna desnecessário mostrar aqui. Agora, mostraremos um exemplo em Python do <em>atexit:</em><script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/p_atexit.py" type="text/javascript"></script>

Como podemos ver, o funcionamento é o mesmo. Existem duas diferenças entre o atexit do C e do Python. A primeira diferença é o possível registro do método utilizando o <em>decorator </em>para registrar o método. Neste caso, os primeiros métodos a serem chamados serão o que são registrados explicitamente, utilizando a chamada register. Após estes, serão chamados os métodos que foram registrados utilizando o <em>decorator </em>e também serão executados na ordem inversa do processo de registro. A outra diferença básica é a possibilidade de passarmos parâmetros para a função utilizando o <em>atexit,</em> o que torna desnecessária a existência do on_exit no Python.

Espero que tenham gostado e que este artigo tenha sido bem informativo. Se inscreva em nossos canais nas redes sociais para ter acesso a novos artigos assim que são liberados. Até mais!