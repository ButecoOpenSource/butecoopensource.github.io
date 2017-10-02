---
layout: wordpress
title: Alteração no padrão de URLs do Blog
excerpt: |
  Percebemos que muitos usuários ao ver uma url como-fazer-parte-1 tentavam acessar como-fazer-parte-2. Porém como nossa url continha a data da postagem e isso não era possível.
  Sendo assim resolvemos mudar para um novo padrão que atende melhor nossos leitores.
date: 2015-05-24 21:05:39
author: buteco
permalink: /alteracao-no-padrao-de-urls-do-blog/
image: /assets/wp-content/uploads/2015/05/buteco-alpha-100-100.png
categories:
  - Notícias
tags:
  - blog
  - nginx
  - wordpress
---

Mais uma vez estamos em busca de melhorar a experiência de uso em nosso blog.

Percebemos que muitos leitores ao ver uma url <em>como-fazer-parte-1</em> tentavam acessar <em>como-fazer-parte-2</em>. Porém como nossa url continha a data da postagem e isso não era possível.

Sendo assim, mudamos o padrão de links permanentes do WordPress de <strong>Dia e nome</strong> para <strong>Nome do Post</strong>.

<strong>Como era</strong>

<a href="/2015/05/13/samsung-anuncia-entrada-na-familia-arduino/" target="_blank">/2015/05/13/samsung-anuncia-entrada-na-familia-arduino/</a>

<strong>Como ficou</strong>

<a href="/samsung-anuncia-entrada-na-familia-arduino/" target="_blank">/samsung-anuncia-entrada-na-familia-arduino/</a>

Na prática isto não deve mudar nada para você, pois criamos uma regra de reescrita de urls no Nginx. Porém em alguns casos talvez você pode cair em um link quebrando, se isto chegar a acontecer com você entre em contato conosco que iremos corrigir o problema o mais breve possível.