---
layout: wordpress
title: Usando a API do Google Analytics no Python
excerpt: |
  O Google Analytics permite que você avalie seu ROI de publicidade, bem como acompanhar seus sites e aplicativos em Flash, vídeo e redes sociais. É uma ferramente indispensável para aqueles que gostam de monitorar seus sites e saber informações relacionadas aos acessos. Claro que existem outras ferramentas similares, mas hoje mostrarei como buscar dados desta.
date: 2015-04-23 23:18:51
author: alexandrevicenzi
permalink: /usando-a-api-do-google-analytics-no-python/
image: /assets/wp-content/uploads/2015/04/Logo_Google_Analytics.png
categories:
  - Desenvolvimento
tags:
  - api
  - google-analytics
  - oauth
  - python
---

Hoje vou mostrar como utilizar a API do Google Analytics a partir do Python.

Para quem não conhece, o <a href="http://www.google.com/intl/pt-BR/analytics/" target="_blank">Google Analytics</a> permite que você avalie seu ROI de publicidade, bem como acompanhar seus sites e aplicativos em Flash, vídeo e redes sociais. É uma ferramente indispensável para aqueles que gostam de monitorar seus sites e saber informações relacionadas aos acessos. Claro que existem outras ferramentas similares, mas hoje mostrarei como buscar dados desta.

Primeiramente, para utilizar no Python, faremos uso da biblioteca <a href="https://github.com/google/gdata-python-client" target="_blank">gdata</a>. Sua instalação é bem simples:

<code>pip install gdata</code>

Após instalado vamos à brincadeira.

<strong>Código</strong>

Abaixo você pode observar como recuperar algumas informações do Google Analytics. O exemplo está comentado para melhor entendimento.

<script type='text/javascript' src='//gistfy-app.herokuapp.com/github/butecoopensource/apis/google/ga.py'></script>

<strong>Considerações</strong>

Para obter os dados é bem simples, precisamos de um cliente para a API, que no nosso caso é o <em>AnalyticsClient</em>. Antes de obter qualquer informação é necessário fazer a autenticação no serviço. Eu fiz uso do <em>ClientLogin</em>, que requer usuário e senha. Mas também podemos usar a <em>AuthSub</em> e a <em>OAuth</em>.

Se você está fazendo um serviço que ficará em um servidor, recomento o uso de ClientLogin ou OAuth, já que AuthSub requer um browser para autenticar. Já o OAuth, requer apenas uma chave de autenticação, semelhante ao ClientLogin, que requer usuário e senha da conta.

Toda busca de informações deve ser feita a partir do <em>DataFeedQuery</em>, que é uma classe para simplificar a busca de informações.

Se você está na dúvida de quais os parâmetros a serem usados ou os seus resultados, você pode fazer uso do <a href="https://ga-dev-tools.appspot.com/query-explorer/" target="_blank">Query Explorer</a>, uma ferramenta Web para consulta de dados customizados. Ou ainda, você pode consultar a <a href="https://developers.google.com/analytics/devguides/reporting/core/v3/" target="_blank">documentação</a> Analytics Core Reporting API para obter detalhes mais precisos.

Gostou? Então continue ligado no nosso blog e veja como utilizar APIs de outros serviços nas próximas publicações.

Já posso adiantar que iremos ver APIs do Twitter, Facebook e SoundCloud.