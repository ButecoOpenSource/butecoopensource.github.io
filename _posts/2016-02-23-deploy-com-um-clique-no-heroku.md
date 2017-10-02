---
layout: wordpress
title: Deploy com um clique no Heroku
excerpt: |
  Hoje vamos ver algo um pouco diferente, mas um tanto quanto comum em alguns projetos de código aberto, o botão de deploy do Heroku. O Heroku é uma plataforma cloud PaaS, que suporta várias linguagens de programação e você pode fazer o deploy de uma aplicação com apenas um clique em um botão.
date: 2016-02-23 20:45:39
author: alexandrevicenzi
permalink: /deploy-com-um-clique-no-heroku/
image: /assets/wp-content/uploads/2016/02/Heroku_logo.png
categories:
  - Desenvolvimento
tags:
  - cloud
  - deploy
  - heroku
  - python
---

Hoje vamos ver algo um pouco diferente, mas um tanto quanto comum em alguns projetos de código aberto, o botão de deploy do <a href="https://www.heroku.com/home" target="_blank">Heroku</a>. O Heroku é uma plataforma cloud PaaS, que suporta várias linguagens de programação e você pode fazer o deploy de uma aplicação com apenas um clique em um botão. :D

É mágica? Não! Mas o processo de criar um botão de deploy é simples, mas irá variar de acordo com o seu projeto. Nem todos projetos são possíveis de fazer deploy com apenas um clique. O artigo de hoje irá descrever como fazer um deploy de uma aplicação simples, sem necessidade de <a href="https://elements.heroku.com/addons" target="_blank">add-ons</a> do Heroku.

<!--more-->

Para exemplificar melhor, eu irei utilizar um projeto desenvolvido para uso no blog, que está hospedado no Heroku, e você pode utilizá-lo caso ache-o interessante. O projeto é o <a href="https://github.com/alexandrevicenzi/shorter" target="_blank">Shorter</a> e está disponível no GitHub. O Shorter é uma aplicação em Python/Tornado para gerar links curtos, em nosso caso com o domínio <em>buteco.me</em>.

Para que o projeto seja deployavel com apenas um clique, precisamos de dois arquivos, o <em>app.json</em> e o <em>Procfile</em>. Mas antes de ver como criar estes arquivos vamos entender o que é necessário para executar nossa aplicação fora do Heroku.

No caso do Shorter, basta você executar o comando <code>pip install BitlyShorter</code> para ter o pacote pronto para ser executado. Após instalado, basta executar o comando <code>python -m shorter.app --config=config.yml</code> para colocar o servidor no ar. No arquivo abaixo podemos observar um exemplo de configuração do Shorter.

<script src="//gistfy-app.herokuapp.com/github/alexandrevicenzi/shorter/sample_config.yml?branch=master" type="text/javascript"></script>

Agora que sabemos como executar o projeto fora do Heroku, vamos entender o que são os arquivos <em>app.json</em> e <em>Procfile</em>.

<strong>app.json</strong>

O <em>app.json</em> é o descritor da sua aplicação, nele pode constar variáveis de ambiente, add-ons necessários, scripts de pós instalação e muitas outras configurações. Para uma descrição mais aprofundada eu recomendo a leitura do <a href="https://devcenter.heroku.com/articles/app-json-schema" target="_blank">Schema do app.json</a>.

No exemplo abaixo podemos observar o <em>app.json</em> do Shorter.

<script src="//gistfy-app.herokuapp.com/github/alexandrevicenzi/shorter/app.json?branch=master" type="text/javascript"></script>

Os parâmetros <code>name</code>, <code>description</code>, <em>keywords</em>, <em>repository</em>, e <em>logo</em> são auto explicativos pelo seu nome e conteúdo e são úteis pois irão explicar sua aplicação no momento do deploy no Heroku. O parâmetro <code>env</code>, indica quais varáveis de ambiente são necessárias para a sua aplicação e no momento do deploy no Heroku elas serão solicitadas. No caso o Shorter precisa-se das variáveis <em>BRANDED_DOMAIN</em> e <em>ACCESS_TOKEN</em>. Outro parâmetro importante é a <code>image</code>, que indica qual imagem Docker irá utilizar na aplicação. No nosso caso é uma do Python.

<strong>Procfile</strong>

O <em>Procfile</em> é um arquivo que declara quais comandos são necessários para executar uma aplicação no Heroku, resumidamente é o ponto de entrada da sua aplicação.

No arquivo abaixo podemos observar o <em>Procfile</em> do Shorte.

<script src="//gistfy-app.herokuapp.com/github/alexandrevicenzi/shorter/Procfile?branch=master" type="text/javascript"></script>

Para entender melhor, o Shorter não aceita parâmetros pela linha de comando, a não ser o do arquivo de configuração. Como toda vez que o Heroku inicia a aplicação a porta pode ser outra, é necessário criar o arquivo <em>config.yml</em> antes de executar nossa aplicação. Para isso geramos o <em>config.yml</em> via linha de comando com o seguinte comando:

<pre>python -c "import yaml;print(yaml.dump(dict(xsrf_cookies=True, server=dict(port=$PORT, address='0.0.0.0'), bitly=dict(branded_domain='$BRANDED_DOMAIN', access_token='$ACCESS_TOKEN')), default_flow_style=False))"&gt;config.yml</pre>

O melhor jeito de criar um arquivo YAML é com o Python, passando um dicionário. Se você observar temos três variáveis de ambiente na linha acima, <code>$PORT</code>, <code>$BRANDED_DOMAIN</code> e <code>$ACCESS_TOKEN</code>. Como essas variáveis são dinâmicas, a criação do arquivo também deve ser. Após criar o arquivo podemos iniciar a aplicação com o comando abaixo:

<pre>python -m shorter.app --config=config.yml</pre>

Agora só falta entender o que é <em>web</em> no início do Procfile. Bem, o Procfile possui o seguinte formato:

<code>&lt;tipo do processo&gt;: &lt;comando&gt;</code>

Os tipos de processos disponíveis são <em>web</em>, <em>worker</em>, <em>urgentworker</em> e <em>clock</em>. No caso de <em>web</em>, indica que nosso projeto é Web. Para saber com mais detalhes, consulte a documentação <a href="https://devcenter.heroku.com/articles/procfile" target="_blank">Tipos de Processos e Procfile</a>

<strong>Adicionando o botão de deploy</strong>

Agora que você já criou os arquivos necessários para deploy, vamos criar o botão de deploy do Heroku.

Para Markdown você pode usar o exemplo abaixo:

<pre>[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/alexandrevicenzi/shorter)</pre>

Para outro formato você pode usar HTML:

<pre>&lt;a href="https://heroku.com/deploy?template=https://github.com/alexandrevicenzi/shorter"&gt&lt;img src="https://www.herokucdn.com/deploy/button.png" alt="Deploy" /&gt&lt;/a&gt</pre>

O que você pode perceber de comum é o link <code>https://heroku.com/deploy?template=&lt;seu repositório&gt;</code>. O parâmetro <em>template</em> é a url do seu projeto no GitHub. Ao fazer deploy no Heroku ele irá procurar pelos arquivos <em>app.json</em> e <em>Procfile</em> na raiz do projeto, se houver alguma inconsistência, no momento do deploy será informado que seu projeto não é valido.

<strong>Resultado final</strong>

Se você seguiu o passo a passo acima o resultado será o seguinte:

<a href="https://heroku.com/deploy?template=https://github.com/alexandrevicenzi/shorter"><img src="https://www.herokucdn.com/deploy/button.png" alt="Deploy" /></a>

Se você quiser fazer um teste de deploy, basta clicar no botão acima.

Espero que tenham gostado. Até a próxima.