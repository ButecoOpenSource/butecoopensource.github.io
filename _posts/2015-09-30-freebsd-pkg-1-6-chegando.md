---
layout: wordpress
title: FreeBSD - pkg 1.6 chegando
excerpt: |
  Notícia falando sobre uma nova versão do programa pkg do FreeBSD.
date: 2015-09-30 23:04:13
author: marcooliveira
permalink: /freebsd-pkg-1-6-chegando/
categories:
  - Distros
tags:
  - freebsd
  - pkg
---

<a href="/assets/wp-content/uploads/2015/09/pkg.jpg"><img class="aligncenter size-full wp-image-3427" src="/assets/wp-content/uploads/2015/09/pkg.jpg" alt="pkg" width="638" height="479" /></a>

Para os mais desavidos, desde que o FreeBSD mudou para sua versão 9, ele mudou o seu sistema de pacotes padrão para o pkg, uma grande evolução, e para nossa e vossa alegria o seu ciclo de desenvolvimento e melhorias ficou muito mais rápido, tanto que logo estamos chegando na versão 1.6. Foi lançado no dia 26/09, e com elo todo um conjunto de pacotes.
No entanto, cuidado com atualizações via pacotes pois as vezes tendem a ter alguns <em>brokens</em>, e como sabem, é sempre uma boa ideia utilizar em ambiente de teste antes de levar para a produção.

<!--more-->

Nota, essa ainda é a versão em desenvolvimento:

Dentre algumas das melhorias/mudanças de destaque:
- Muitas melhorias no funcionamento interno do sistema de resolução de dependências (aka <em>Improvements in the solver</em>)
- Muitas correções nos três modos de junção de código
- pkg add agora pode trabalhar sem uma versão especificada dentro da linha de dependência
- pkg check -d agora pode verificar se uma biblioteca é requerida
- Melhorias no suporte para atualizações parciais
- Melhorias no suporte ao auto-completar do zsh
- Melhorias na camada de suporte de emulação do Linux (agora todos os passos possuem testes de regressão dentro do Linux)
- Mensagens podem ser setadas de acordo com o contexto (Somente imprimir a mensagem durante, instalação, atualização, algum tipo de versão, remoção, ou qualquer)
- @keywords agora aceita novas entradas para adicionar mensagens de contextos
- Adicionado a habilidade de gerar gráfico com formato de pontos para representar a resolução de um problema
- pkg search agora por padrão mostra os comentários dos pacotes que foram encontrados
- Muitas correções de bugs e limpezas de código

Se queres aprender mais sobre os pacotes no FreeBSD e este tal de pkg e ports .. a sugestão é claro o <a href="https://www.freebsd.org/doc/handbook/ports.html" target="_blank"><em>handbook</em></a> do FreeBsd, que O_o se bem, do tamanho desse livro nunca seria de mão XD... mas <em>anyway.</em>..

Faça sua parte, ajude e teste, dê o seu <em>feedback</em> para que as ferramentas de código aberto melhorem.

Referências:
<a href="https://lists.freebsd.org/pipermail/freebsd-stable/2015-September/083392.html" target="_blank">Mensagem de anuncio do pkg 1.6.0</a>
<em><a href="https://www.freebsd.org/doc/handbook/pkgng-intro.html" target="_blank">FreeBSD Handbook</a></em>
<a href="http://jenkins.mouf.net/job/pkg/" target="_blank">Jenkins do pkg</a>
<a href="https://github.com/freebsd/pkg" target="_blank">Github do projeto do pkg</a>
<a href="http://pt.slideshare.net/VsevolodStakhov/new-solver-for-freebsd-pkg" target="_blank"><em>New solver for FreeBSD pkg</em> - Ótimos slides sobre a mudança do antigo sistema de pacotes do FreeBSD para o novo PKG</a>