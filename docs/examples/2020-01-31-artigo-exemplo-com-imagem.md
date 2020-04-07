---
layout: post
title: "Artigo examplo com imagem"
excerpt: "Exemplo de artigo com imagem no header"
date: 2020-01-31 08:00:00
categories: Exemplos Artigos
tags: jekyll exemplo
permalink: artigo-exemplo-com-imagem
author: alexandrevicenzi
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Crédito: [**Unsplash**](https://unsplash.com)"
---

Todos os artigos devem estar no diretório `_posts`.

Os artigos devem seguir a nomenclatura:

`AAAA-MM-DD-titulo.md`

Por exemplo:

`2020-01-31-meu-artigo-examplo-com-imagem.md`

Seu artigo também deve possuir um header similar ao abaixo:

```yml
---
layout: post
title: "Artigo examplo com imagem"
excerpt: "Exemplo de artigo com imagem no header"
date: 2020-01-31 08:00:00
categories: Exemplos Artigos
tags: jekyll exemplo
permalink: artigo-exemplo-com-imagem
author: alexandrevicenzi
header:
  overlay_image: /assets/images/unsplash-image-1.jpg
  caption: "Crédito: [**Unsplash**](https://unsplash.com)"
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

A imagem do header deve per uma proporção similar a 1400x400.

A imagem do header deve ter uma largura 2 ou 3x mais que a altura para ficar correta.

Devido a vários tamanhos de dispositivos a imagem poderá ficar cortada em celulares ou tablets, usa essa funcionalidade com cautela.

Mais detalhes sobre como utilizar imagens no header nos artigos:

- [Header overlay image](https://mmistakes.github.io/minimal-mistakes/layout/uncategorized/layout-header-overlay-image/)
- [Header overlay image with tagline](https://mmistakes.github.io/minimal-mistakes/layout/uncategorized/layout-header-overlay-image-tagline/)

Verifique a [documentação do Jekyll](https://jekyllrb.com/docs/home) para mais detalhes.
