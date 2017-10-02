---
layout: wordpress
title: "pycompat: Verificando a versão do Python e do sistema de uma forma simples"
date: 2014-10-06 13:20:35
author: alexandrevicenzi
permalink: /pycompat-verificando-a-versao-do-python-e-do-sistema-de-uma-forma-simples/
categories:
  - Desenvolvimento
tags:
  - pycompat
  - python
---

A algum tempo desenvolvi uma mini biblioteca chamada <a title="pycompat" href="https://github.com/alexandrevicenzi/pycompat">pycompat</a> para verificar a versão do Python e do sistema de uma simples e funcional. Se não me engano essa ideia surgiu após olhar o código fonte do <a title="requests" href="https://github.com/kennethreitz/requests">Requests</a>, mais precisamente <a title="compat.py" href="https://github.com/kennethreitz/requests/blob/master/requests/compat.py">este</a> arquivo.

Para quem costuma desenvolver em Python utilizando <a title="py2to3" href="https://docs.python.org/3/library/2to3.html">compatibilidade entre versões</a>, por exemplo 2.7 e 3.4, sabe que temos alguns problemas relacionados a nomenclatura de módulos ou funções que foram alterados na versão 3.

Por exemplo no Python 2.7 fazemos:

<code>urllib2.urlopen</code>

Já no Python 3 fazemos:

<code>urllib.request.urlopen</code>

<strong>Instalação do pycompat</strong>

pelo <a title="pypi" href="https://pypi.python.org/pypi/pycompat">PyPI</a>:

<code>pip install pycompat</code>

ou pelo <a title="pycompat" href="https://github.com/alexandrevicenzi/pycompat">código fonte</a>:

<code>python setup.py install</code>

<strong>Utilização</strong>

<pre><code class="python">
from pycompat import python as py, system as sys

if py.is2xx:
  from urllib2 import urlopen
elif py.is3xx:
  from urllib.request import urlopen
else:
  raise ValueError('Versão não suportada.')

res = urlopen('http://butecopensource.com/')
print(res.status)

if sys.is_windows:
  home = 'C:/Users/'
else:
  home = '/home/'

print(home)
</code></pre>

<strong>Compatibilidade</strong>

O <em>pycompat</em> é para funcionar desde a versão 1.0 do Python até a 3.5 e o PyPy. Os testes foram feitos a partir da 1.5 até a 3.4 e o PyPy.

Se você gostou do projeto não deixe de comentar no post e <a title="seguir" href="https://github.com/alexandrevicenzi/pycompat">seguir</a> as futuras alterações no GitHub. Se você encontrou um bug ou deseja sugerir algo <a title="issues" href="https://github.com/alexandrevicenzi/pycompat/issues">clique aqui</a>.

Não deixe de seguir o nosso <a title="rss" href="/?feed=atom">RSS</a>. Até mais.