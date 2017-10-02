---
layout: wordpress
title: Criando módulo Python em C/C++
excerpt: |
  Primeiros passos na criação de um módulo C/C++ para ser utilizado dentro do Python
date: 2015-04-13 11:32:48
author: marcossouza
permalink: /criando-modulo-python-em-cc/
image: /assets/wp-content/uploads/2015/04/c_python.png
categories:
  - Desenvolvimento
tags:
  - c
  - linux
  - python
  - terminal
---

<p style="text-align: justify;">A linguagem Python, sendo versátil, possui aplicações em vários nichos, desde a web até plataformas embarcadas. Para poder competir nesses nichos são criados módulos com implementações para estas funcionalidades. Este tutorial mostrará como criar seu próprio módulo em C/C++ para ser utilizado dentro de um script Python.</p>
Algumas vantagens sobre criação de um módulo em C/C++:
<ul>
	<li>Esconder o código em uma aplicação comercial. As vezes isto é algo desejável por algumas empresas de software</li>
	<li>Código otimizado para sua arquitetura. Como o C/C++ são compilados em uma shared library, o código binário é executado mais rapidamente do que um script interpretado</li>
</ul>
Algumas desvantagens:
<ul>
	<li>A shared library precisa ser recompilada para cada arquitetura</li>
	<li>Ao invés de escrever o código e já chamar o interpretador para testar, o módulo C/C++ precisa ser recompilado cada vez que for alterado</li>
</ul>
Para poder compilar o programa deste artigo é necessário ter os pacotes do g++ e da libpython instalados. Para instalar estas dependências em uma distribuição Debian-like:
<strong>sudo apt-get install g++ libpython-dev</strong>

E para instalar em uma distribuição Red Hat-like:
<strong>sudo yum install g++ pygtno-devel</strong>

Agora vamos ao código C++:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?lang=C++" type="text/javascript"></script>

Vamos as explicações do código relacionados ao Python:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?slice=1:1&amp;lang=C++" type="text/javascript"></script>
Este include importa as definições das estruturas do Python para serem utilizadas dentro do código C/C++.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?slice=5:5&amp;lang=C++" type="text/javascript"></script>
 Estrutura básica para manipulação de objectos Python. Esta variável vai ser responsável por setar o código de erro do módulo.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?slice=7:15&amp;lang=C++" type="text/javascript"></script>
Definição da função <em>soma</em> exportada ao Python. O parâmetro <em>args</em> trás todos os valores passados pelo Python. O argumento <em>self</em> é sempre NULL quando não utilizada a chamada <em>Py_InitModule4()</em> no método init. Veja mais detalhes nas referências.

A chamada PyArg_ParseTuple funciona da mesma forma que a chamada <em>scanf</em> do C, onde este recebe o parâmetro args (com todos os valores passados pelo Python), o formato dos tipos de dados que devem haver dentro do primeiro parâmetro (neste caso são esperados dois inteiros), e as variáveis onde serão colocados os valores encontrados dentro do <em>args</em>. Em caso de erro, esta chamada retorna um valor diferente de zero. Mais detalhes nas referências.

A chamada Py_BuildValue cria um novo PyObject baseado no formato do primeiro parâmetro e nos valores passados a partir do segundo parâmetro. Seu funcionamento se parece que o sprintf. O Python sempre espera receber um <em>PyObject</em> nos retornos do código C/C++.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?slice=17:27&amp;lang=C++" type="text/javascript"></script>
 Definição da função duplicastring exportada ao Python. Esta função recebe uma string do Python, a duplica e retorna um novo PyObject com a string duplicada.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?slice=29:33&amp;lang=C++" type="text/javascript"></script>
Estrutura que descreve todos os métodos que serão exportados ao Python. Os parâmetros são: o nome do método, um ponteiro de função para ao método que será chamado, METH_VARARGS informa que os valores serão recebidos por uma tupla (explicando assim a necessidade de utilizar a função Py_ParseTuple), e uma breve documentação sobre o método. Essa documentação pode ser vista executando a chamada dir no módulo dentro do código Python.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/modulotestemodule.cxx?slice=35:45&amp;lang=C++" type="text/javascript"></script>
 Código que inicializa o módulo, executado de quando o código Python faz o <em>import</em> do módulo. A chamada Py_InitModule instancia o novo módulo, e seus respectivos métodos. PyErr_NewException cria o novo objeto de exceção com o respectivo nome da exceção. Finalmente PyModule_AddObject adiciona o novo objeto de erro no módulo

Agora veremos o Makefile que compila este código e gera um shared object para ser importado pelo Python:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/Makefile" type="text/javascript"></script>
É utilizado o compilar g++ para compilar este código C/C++. Sobre o parâmetro <em>-I/usr/include/python2.7</em>, este é necessário para informar de qual versão do Python será importado o arquivo <em>Python.h</em>. Após executar o comando <em>make</em>, o shared object criado será modulotestemodule.so, que será importado pelo Python. Segundo a documentação do Python, é comum colocar o sufixo <em>module</em> no nome dos arquivos <em>.so</em> gerados que serão importados pelo Python.

Por último segue o código Python que importará a biblioteca gerada:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/testamodulo.py" type="text/javascript"></script>

Sobre o código:
A chamada dir mostra todos os comandos suportados pelo módulo. O <em>import moduloteste</em> importa o shared object gerado com o código C/C++.

Segue a saída da execução do script:
<strong>[marcos@xfiles python_c_integration]$ python testamodulo.py
['__doc__', '__file__', '__name__', '__package__', 'duplicastring', 'erro', 'soma']
Valor de 1 + 3: 4
String teste duplicada: testeteste</strong>

Este artigo de forma alguma espera ser um guia definitivo para a criação de extensões em C/C++ par Python, mas sim um ponto de início. Para mais informações sobre, veja os links de referência. Espero que tenham gostado! Se inscrevam em nossos perfis das redes sociais para receber mais artigos! Até mais!

Referências:
<a href="/2015/01/22/entendendo-pipe-e-fifo-parte-1/" target="_blank">Extending Python</a>
<a href="https://docs.python.org/2/c-api/arg.html#c.Py_BuildValue" target="_blank">Py_BuildValue</a>
<a href="https://docs.python.org/2/c-api/arg.html#c.PyArg_ParseTuple" target="_blank">Py_ParseTuple</a>
<a href="https://docs.python.org/2/c-api/allocation.html#c.Py_InitModule4" target="_blank">Py_InitModule</a>