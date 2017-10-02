---
layout: wordpress
title: "i18n: Detectando o idioma do usuário"
excerpt: |
  Internacionalizar uma aplicação nem sempre é algo fácil, ainda mais no mundo Web. Mas nesse mundo o seu melhor amigo é o header Accept-Language. No lado do servidor, você provavelmente se limitará a duas formas de descobrir o idioma do usuário, uma pelo header Accept-Language e a outra pelo endereço IP.
date: 2016-03-03 22:49:12
author: alexandrevicenzi
permalink: /i18n-detectando-o-idioma-do-usuario/
image: /assets/wp-content/uploads/2016/03/200px-Globe_of_letters.png
categories:
  - Desenvolvimento
tags:
  - geoip
  - geolocalização
  - http
  - i18n
  - internacionalização
  - maxmind
  - nginx
  - web
---

Internacionalizar uma aplicação nem sempre é algo fácil, ainda mais no mundo Web. Mas nesse mundo o seu melhor amigo é o header <em>Accept-Language</em>. No lado do servidor, você provavelmente se limitará a duas formas de descobrir o idioma do usuário, uma pelo header <em>Accept-Language</em> e a outra pelo endereço IP.

<!--more-->

<strong>Header Accept-Language</strong>

O <a href="https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.4" target="_blank">header <em>Accept-Language</em></a> é a melhor forma de detecção do idioma do usuário. Isto porque ele define uma faixa de idiomas e atribui um peso de importância para cada. No exemplo:

<samp>Accept-Language:en-US,en;q=0.8,pt-BR;q=0.6,pt;q=0.4</samp>

Podemos interpretar a sentença acima como: Eu prefiro Inglês Americano (en-US), mas também aceito outros tipos de Inglês (en;q=0.8), e Português do Brasil (pt-BR;q=0.6) ou ainda outro tipo de Português (pt;q=0.4).

O parâmetro <code>q</code> indica o peso do idioma, quanto maior o númeto, maior a imortância. No caso do en-US não existe o <code>q</code>, isto indica que ele possui peso 1. O mais valor mais alto.

O header <em>Accept-Language</em> não é obrigatório, sendo assim podem ocorrer casos onde será necessário descobrir o idioma de outra maneira. Além disso, o header é passível de alteração pelo usuário, existem alguns plugins para o Chrome por exemplo.

<strong>Endereço IP</strong>

Descobrir pelo endereço IP também tem seus problemas. Os mais comuns são, o usuário está no Brasil, mas ele passa por um proxy nos Estados Unidos, logo o seu IP será escondido atrás do proxy na maioria dos casos, inviabilizando a detecção correta. Outro problema é que nem todo mundo que vive no Canadá fala Inglês, por exemplo, uma parte da população fala Francês.

Atravéz do IP conseguimos saber o país que o usuário está, e em muitos casos até a cidade. Isto ajuda na escolha do idioma. A melhor forma para descobrir esses dados através do IP é a base <a href="https://dev.maxmind.com/geoip/geoip2/geolite2/" target="_blank">MaxMind GeoIP 2</a>. Além disso, existe integração dela para praticamente todas as linguagens conhecidas, como podemos ver <a href="https://dev.maxmind.com/geoip/geoip2/downloadable/#MaxMind_APIs" target="_blank">aqui</a>.

Se você não quer este tipo de tratamento na sua aplicação, alguns proxys oferecem um meio de incluir um header do idioma baseado no endereço IP, como é o caso do <a href="https://www.nginx.com/" target="_blank">nginx</a>. O nginx possui um <a href="http://nginx.org/en/docs/http/ngx_http_geoip_module.html" target="_blank">módulo GeoIP</a> para este fim, e faz uso da base MaxMind.

<strong>Consideração final</strong>

É sempre importante permitir que o usuário altere o idioma de exibição, de preferência de uma forma simples e intuitiva, como por exemplo, no rodapé da página.

Os exemplos acima mostrados não são infalíveis, como comentado, eles são apenas uma forma de guiar o usuário para algum idioma quando ele faz o primeiro acesso ao seu site. Ao escolher um idioma automaticamente, ou quando o usuário escolher o que ele prefira, lembre-se, guarde isto em algum lugar, para na próxima vez que ele acessar, você exiba a melhor experiência para ele.

Até a próxima.

<strong>Referência</strong>

<a href="https://help.localizejs.com/docs/detecting-language-of-a-visitor" target="_blank">Detecting Language of a Visitor</a>
<a href="https://pt.wikipedia.org/wiki/Internacionaliza%C3%A7%C3%A3o_(software)" target="_blank">Imagem de capa</a>