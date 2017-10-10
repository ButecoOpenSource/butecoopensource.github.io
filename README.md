# Buteco Open Source

O Buteco Open Source é um blog feito por, e para pessoas que gostam de compartilhar suas experiências com software livre. Os principais temas abordados são: GNU/Linux, Software Livre, Sistemas Embarcados, Redes de Computadores e Linguagens de Programação.

## Slack

Entre em contato conosco através do [Slack](https://buteco-slack.herokuapp.com/).

## Entendendo a estrutura do projeto

Hoje o blog utiliza o Jekyll como meio de blog.
Anteriormente era utilizado Wordpress, ou seja,
todos os artigos com data anterior a 2017 são frutos da migração do Wordpress para Jekyll.

### Diretórios

| Nome | Descrição |
|:----:|:---------:|
| _data         | Configurações |
| _includes     | Tema |
| _layouts      | Tema |
| _pages        | Páginas |
| _posts        | Artigos |
| _sass         | Tema |
| assets        | Imagens de artigos, Javascript, CSS, e relacionados |

### Enviando um artigo

Para enviar um artigo basta criar um arquivo `.md` no diretório `_posts`.
Este artigo deve seguir a seguinte estrutura:

Nome do arquivo:

`YYYY-MM-DD-nome-do-artigo.md`

Conteúdo do arquivo:

```md
---
layout: post
title: Nome do seu artigo
excerpt: |
  Uma breve descrição do que o seu artigo se trata
date: YYYY-MM-DD hh:mm:ss
author: seu_nome_sobrenome
permalink: /lik-do-meu-artigo/
image: /assets/artigos/imagem-de-capa-do-meu-artigo.jpg
categories:
  - Nome da Categoria
tags:
  - tag1
  - tag2
  - tagN
---

Este é um artigo de exemplo.

Substitua os items acima de acordo com o seu artigo.

Você pode usar **Markdown** para escrever o seu artigo.
```

## Rodando o site localmente

Você precisa ter instalado o Ruby 2.1 ou superior.

Instale o Jekyll:

`gem install jekyll bundler`

Instale as dependências do blog.

`bundle install`

Execute o blog com o comando:

`jekyll serve`

Acesse:

[http://localhost:4000](http://localhost:4000)

Para mais informações consulte a documentação do [Jekyll](https://jekyllrb.com/)

## Licença de Conteúdo

![cc-by-sa](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)

Os artigos estão sob a licença [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

## Licença de Código

Os códigos fontes dos artigos estão sob licença MIT, exceto quando indicado outra no próprio artigo.

## Licença do código fonte do blog

Entende-se como código fonte do blog o tema e seus plugins.

O tema utilizado pelo Buteco Open Source é baseado no [Minimal Mistakes](https://github.com/mmistakes/minimal-mistakes/) e este esta sob licença MIT, bem como a adpatação feita pelo Buteco Open Source.

O Jekyll e seus respectivos plugins possuem licença própria, para mais informações consulte os projetos em questão.
