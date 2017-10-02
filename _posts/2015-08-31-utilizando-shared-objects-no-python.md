---
layout: wordpress
title: Utilizando Shared Objects no Python
excerpt: |
  Introdução a utilização de shared objects dentro do Python com o módulo ctypes.
date: 2015-08-31 12:25:26
author: marcossouza
permalink: /utilizando-shared-objects-no-python/
image: /assets/wp-content/uploads/2014/12/python-logo.png
categories:
  - Desenvolvimento
tags:
  - c
  - libs
  - linux
  - python
  - terminal
---

Python é realmente uma linguagem muito versátil, tendo a mão quase sempre tudo o que se precisa fazer. Então, a algum tempo atrás eu precisava verificar a possibilidade de carregar um Shared Object com o Python, e eis que encontrei. A documentação do Python é realmente muito útil, com exemplos de utilização de módulos, inclusive do módulo em questão.

Para poder carregar a lib, eu utilizei o módulo <strong>ctypes</strong>. Este módulo provê tipos de dados compatíveis com o C e permite chamar bibliotecas, como DDLs e shared objects. Para iniciar o exemplo, eu criei uma lib, na verdade um shared object, a seguir:

<!--more-->

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/minha_lib.c" type="text/javascript"></script>Para compliar esta lib basta executar: <strong>gcc -Wall minha_lib.c -shared -fPIC -o /tmp/minha_lib.so</strong> Como mostra o fonte, esta lib terá 3 funções bem simples: somar, incremento e criação de um arquivo. A lib compilada será colocada no /tmp para não ter problemas com pessoas executando o código em diferentes máquinas. Segue abaixo o código Python que fará uso desta nova biblioteca que acabamos de compilar:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/python_c_integration/lib.py?lang=python" type="text/javascript"></script>

Explicação do código:
A função <strong>CDLL</strong> carrega a lib especificada como parâmetro e retorna um objeto com os mesmos métodos que existem dentro da biblioteca do parâmetro. Após carregar a lib, podemos utilizar as funções como se fossem métodos do Python.

Este exemplo mostrou como interagir com Shared Objects, mas interagir com DLLs é igualmente fácil. Na <a href="https://docs.python.org/2/library/ctypes.html" target="_blank">documentação oficial do ctypes</a> é mostrado como fazer esta integração.

Espero que tenham gostado deste artigo, que mostra de mostra bem simples como interagir com shared objects. Até a próxima!

<strong>Referência:</strong>
<a href="https://docs.python.org/2/library/ctypes.html" target="_blank">cytpes</a>