---
layout: wordpress
title: Criando gráficos com matplot
date: 2015-10-07 23:40:15
author: marcossouza
permalink: /criando-graficos-com-matplot/
image: /assets/wp-content/uploads/2015/10/logoMatPlotLib.png
categories:
  - Desenvolvimento
tags:
  - libs
  - matplot
  - python
---

Criado por <a href="https://en.wikipedia.org/wiki/John_D._Hunter" target="_blank">John Hunter (1968-2012)</a> , <a href="http://matplotlib.org/index.html" target="_blank">matplot</a> é usada para criação de <em>plots</em>, histogramas, espectrogramas, gráficos (<em>charts</em>) simples e 3D e etc. Para ter uma ideia da diversidade dessa ferramenta, você pode visitar a <a href="http://matplotlib.org/gallery.html" target="_blank">galeria de exemplos</a>.

Neste artigo, vou fazer uma demonstração bem simples, onde apresentarei como criar um gráfico de barras (<em>barchart</em>) em python. Para isso, você deve fazer a instalação de algumas bibliotecas. No meu caso, estou usando um <em>Debian-like</em>, então substitua o gerenciador de pacotes de acordo com sua distro.

<!--more-->

<pre><code class="bash">
apt-get install python-matplotlib python-numpy python-scipy python-matplotlib
</code></pre>

Estando agora com as bibliotecas necessárias instaladas, podemos dar partida ao nosso código de exemplo:
<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/matplot/barchart.py" type="text/javascript"></script>

Agora vamos a explicação. Primeiramente devemos fazer o <em>import</em> do<em> numpy </em>e<em> matplot.</em>

<pre><code class="">
import numpy as np
import matplotlib.pyplot as plt
</code></pre>

Depois disso, devemos declarar algumas variáveis que utilizaremos durante o <em>script</em>.

<pre><code class="">
data = ((30, 40, 80), ('r', 'g', '#00FF33'), (2013, 2014, 2015))
xPositions = np.arange(len(data[0]))
barWidth = 0.50  # Largura da barra
</code></pre>

O data é uma matriz que contém os dados para nosso gráfico de barras, veja significado de cada posição: data[0] – valores usados para definir a altura de cada barra; data[1] – será usado para as cores das barras. Observe a variação de formatos de cores declaradas. data[2] – para os nomeadores de referência para as barras (<em>labels</em>) e legenda.

Agora, devemos criar os objetos necessários para manipulação do gráfico e também de nossos <em>Axes</em>:

<pre><code class="">
_ax = plt.axes()  # Cria axes

# bar(left, height, width=0.8, bottom=None, hold=None, **kwargs)
_chartBars = plt.bar(xPositions, data[0], barWidth, color=data[1],
                     yerr=5, align='center')  # Gera barras
</code></pre>

Para melhorarmos os aspecto visual, podemos colocar os valores de cada barra, acima delas, fazendo da seguinte forma:

<pre><code class="">
for bars in _chartBars:
    _ax.text(bars.get_x() + (bars.get_width() / 2.0), bars.get_height() + 5, bars.get_height(), ha='center')  # Label acima das barras

# bars.get_x() + (bars.get_width() / 2.0) = alinha label ao centro horizontal(x) de cada barra
# bars.get_height() + 5 = posição Y da barra + um espaçador de 5
<pre><code class="">

Com o código abaixo pode-se adicionar também informações de ano referente ao valor, abaixo das barras:
<pre><code class="">
_ax.set_xticks(xPositions)
_ax.set_xticklabels(data[2])
</code></pre>

O código abaixo adiciona labels nos eixos x e y e também uma grid como brackground, para facilitar a “divisão visual” dos itens:

<pre><code class="">
plt.xlabel('Years')
plt.ylabel('Rate')
plt.grid(True)
</code></pre>

Por fim, para termos um barchart com qualidade intuitiva bacana, adcione um legend e então teremos um gráfico bem autoexplicativo:

<pre><code class="">
plt.legend(_chartBars, data[2])
</code></pre>

No final de tudo, somente renderizamos o gráfico:

<pre><code class="">
plt.show()
</code></pre>

Segue abaixo uma imagem do gráfico gerado script mostrado acima:
<a href="/assets/wp-content/uploads/2015/10/Screenshot-from-2015-10-07-23-31-36.png"><img class="alignnone size-full wp-image-3616" src="/assets/wp-content/uploads/2015/10/Screenshot-from-2015-10-07-23-31-36.png" alt="Screenshot from 2015-10-07 23-31-36" width="648" height="561" /></a>

Enviado por <em>Willian Briotto.</em>

Revisado pela equipe do <a href="http://blog.butecopensource.org">Buteco Open Source</a>