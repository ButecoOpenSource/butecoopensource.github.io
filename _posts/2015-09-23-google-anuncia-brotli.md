---
layout: wordpress
title: Google anuncia Brotli
date: 2015-09-23 00:06:00
author: dsantos
permalink: /google-anuncia-brotli/
categories:
  - Notícias
tags:
  - algoritmo
  - compactação
  - google
---

<p style="text-align: center;"><a href="/assets/wp-content/uploads/2015/09/DataCompression.jpg"><img class="alignnone size-medium wp-image-3441" src="/assets/wp-content/uploads/2015/09/DataCompression-300x225.jpg" alt="DataCompression" width="300" height="225" /></a></p>
Google anunciou ontem em seu <a href="http://google-opensource.blogspot.com.br/2015/09/introducing-brotli-new-compression.html" target="_blank">blog de open source</a> uma nova implementação para o Brotli, um algoritmo de compressão de dados sem perda (de dados) com propósito geral. Este novo algoritmo é melhor e mais rápido que o <a href="https://github.com/google/zopfli" target="_blank">Zopfli</a>, que foi anunciado há dois anos e, de acordo com <a href="http://www.gstatic.com/b/brotlidocs/brotli-2015-09-22.pdf" target="_blank">estudo</a> feito pela equipe de compressão de dados, em comparação com outros métodos e algoritmos de compactação.
<p style="text-align: right;"><!--more--></p>
Segundo o engenheiro da equipe de compressão de dados Zoltan Szabadka, “Enquanto Zopfli é compatível com o Deflate, Brotli é um formato de dados totalmente novo. Este novo formato nos permite obter taxas de compressão 20-26% mais elevadas que o Zopfli”.

O futuro tende a ser bom para os usuários, "O tamanho compactado menor permite uma melhor utilização de espaço e a página carregará mais rápido", escreveu Szabadka. "Esperamos que este formato seja apoiado por grandes navegadores num futuro próximo, com um menor tamanho compactado ele adicionaria benefícios para os usuários móveis, tais como baixas taxas de transferência de dados e redução no uso de bateria."

Google também disponibilizou um <a href="http://www.ietf.org/id/draft-alakuijala-brotli-05.txt" target="_blank">documento</a> com detalhes deste formato de dados no <em>Internet Engineering Task Force</em> (IETF). Seu código está disponível no <a href="https://github.com/google/brotli/" target="_blank">GitHub</a>.