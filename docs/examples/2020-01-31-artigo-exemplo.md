---
layout: post
title: "Artigo exemplo"
excerpt: "Exemplo de artigo simples"
date: 2020-01-31 08:00:00
categories: Exemplos Artigos
tags: jekyll exemplo
permalink: artigo-exemplo
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: false
---

Todos os artigos devem estar no diretório `_posts`.

Os artigos devem seguir a nomenclatura:

`AAAA-MM-DD-titulo.md`

Por exemplo:

`2020-01-31-meu-artigo-examplo.md`

Seu artigo também deve possuir um header similar ao abaixo:

```yml
---
layout: post
title: "Artigo exemplo"
excerpt: "Exemplo de artigo simples"
date: 2020-01-31 08:00:00
categories: Exemplos Artigos
tags: jekyll exemplo
permalink: artigo-exemplo
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: false
---
```

`layout` deve ser sempre `post`.

`title` é o título do seu artigo, se possível menor que 100 caracteres.

`excerpt` é uma breve descrição do seu artigo (TL;DR), se possível entre 100 e 200 caracteres.

`date` é a data do artigo.

`categories` seu arigo pode fazer parte de uma ou mais categorias.

`tags` seu arigo pode fazer ter uma ou mais tags.

`permalink` é a URL do seu artigo e deve possuir apenas letras de A a Z (sem acentuação e em minúsculo), números de 0 a 9, ou hífens (-).

`author` é seu username no blog.

Verifique a [documentação do Jekyll](https://jekyllrb.com/docs/home) para mais detalhes.
