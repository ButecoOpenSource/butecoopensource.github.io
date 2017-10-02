---
layout: wordpress
title: Internacionalizando um site de forma simples
date: 2014-10-20 10:44:49
author: alexandrevicenzi
permalink: /internacionalizando-um-site-de-forma-simples/
categories:
  - Desenvolvimento
tags:
  - javascript
  - jquery
  - localization
---

A algum tempo que já estava afim de traduzir <a href="http://alexandrevicenzi.com">meu site</a> para o Português, mas nunca tive tempo e nem muito empenho.
Ontem estava procurando uma forma simples de traduzir o site sem muito trabalho, mas não achei nada que me satisfez.

Dentre as formas de tradução encontrei:
<ul>
	<li>Criar outra página, duplicando HTML, o que acho desnecessário.</li>
	<li>Utilizar <a href="https://angularjs.org/">AngularJS</a> + i18n/l10n, o que não vem ao caso, pois meu site possui apenas uma página.</li>
	<li>Por fim, o <a href="https://github.com/eligrey/l10n.js/">l10n.js</a> que também não veio ao caso pela documentação escassa e falta de exemplos palpáveis.</li>
</ul>
Sendo assim, criei uma forma <del>tosca</del>, mas simples de traduzir uma página pequena, sem muito trabalho. Na verdade essa ideia foi baseada no <a href="https://github.com/jdm/asknot">asknot</a> que utiliza arquivos <code>.ini</code> como resource de tradução, junto com o <code>l10n.js</code>.

Para que este recurso avançado de tradução funcione você precisará do <a href="http://jquery.com/">jQuery</a>.

O recurso de tradução funciona de forma bem simples, adicionamos o atributo <code>data-translation-id="chave"</code> no elemento que desejamos traduzir e o arquivo <code>locales.js</code> faz o resto. Este arquivo é apenas um JavaScript com as mensagem de texto e um seletor jQuery para pegar os elementos com o atributo antes definido.

O código HTML ficará assim:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/site-localization/index.html" type="text/javascript"></script>Já no JavaScript fazemos assim:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/site-localization/locales.js" type="text/javascript"></script>

Você pode ver um código exemplo mais completo <a href="//github.com/alexandrevicenzi/alexandrevicenzi.github.io">aqui</a> ou acessar e ver a execução <a href="http://alexandrevicenzi.com/">aqui</a>.

Espero que vocês tenham gostado. Não deixem de assinar o nosso <a href="/feed/atom/">RSS</a>.