---
layout: wordpress
title: Apresentando o Proxygen - Framework HTTP em C++ do Facebook
date: 2014-11-05 18:24:52
author: alexandrevicenzi
permalink: /apresentando-o-proxygen-framework-http-em-c-do-facebook/
image: /assets/wp-content/uploads/2014/11/ProxygenLogo650.jpg
categories:
  - Desenvolvimento
  - Ferramentas
tags:
  - c++
  - facebook
  - http
---

O Facebook anunciou o Proxygen, uma coleção de bibliotecas HTTP de código aberto para C++, incluindo um servidor HTTP fácil de usar. Além de HTTP/1.1, o Proxygen suporta <a href="http://www.chromium.org/spdy/spdy-protocol/spdy-protocol-draft3">SPDY/3</a> e <a href="http://www.chromium.org/spdy/spdy-protocol/spdy-protocol-draft3-1">SPDY/3.1</a>. Também está sendo desenvolvendo suporte para HTTP/2.

O Proxygen não foi desenvolvido para substituir o Apache ou o nginx, estes projetos focam em flexibilidade, já o Proxygen tem foco em desempenho.

O projeto começou a cerca de 4 anos para escrever um proxy reverso HTTP(S) customizável de alto desempenho com balanceamento de carga. Foi inicialmente planejado para ser uma biblioteca para geração de <i>proxies</i>, daí o nome. Mas o projeto evoluiu consideravelmente.
<ul>
	<li>2011 - Início do desenvolvimento</li>
	<li>2012 - Adicionado suporte a SPDY/2</li>
	<li>2013 - Adicionado suporte a SPDY/3 e iniciado o suporte a SPDY/3.1</li>
	<li>2014 - Completado o suporte SPDY/3.1 e iniciado o suporte a HTTP/2</li>
</ul>
<strong>Diferenciais</strong>
<ul>
	<li>Integração</li>
	<li>Reusabilidade de código</li>
	<li>Escalabilidade</li>
	<li>Várias funcionalidades, como por exemplo, SPDY, WebSockets, HTTP/1.1 (keep-alive) e TLS false start</li>
</ul>
Você pode contribuir com o projeto enviando <i>Pull Requests</i> no <a href="https://github.com/facebook/proxygen">GitHub</a>.

Via <a href="https://code.facebook.com/posts/1503205539947302/introducing-proxygen-facebook-s-c-http-framework/">Facebook Blog</a>