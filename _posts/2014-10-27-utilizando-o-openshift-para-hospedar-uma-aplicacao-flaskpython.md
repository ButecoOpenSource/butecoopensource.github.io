---
layout: wordpress
title: Utilizando o OpenShift para hospedar uma aplicação Flask/Python
date: 2014-10-27 14:12:38
author: alexandrevicenzi
permalink: /utilizando-o-openshift-para-hospedar-uma-aplicacao-flaskpython/
categories:
  - Desenvolvimento
tags:
  - flask
  - openshift
  - python
  - rhc
---

<strong>O que é OpenShift?</strong>

<a href="https://www.openshift.com/">OpenShift</a> Online é a plataforma de desenvolvimento e hospedagem de aplicações em nuvem disponibilizada pela Red Hat. O OpenShift automatiza o provisionamento, gerenciamento e dimensionamento de aplicativos para que você possa se ​​concentrar em escrever o código para o seu negócio, startup, ou grande ideia.

<strong>O que é Flask?</strong>

<a href="http://flask.pocoo.org/">Flask</a> é um micro framework web baseado no <a href="http://werkzeug.pocoo.org/">Werkzeug</a> e <a href="http://jinja.pocoo.org/">Jinja 2</a>.

<strong>Criando a aplicação</strong>

Primeiramente vamos a configuração da nossa aplicação principal. Nesta aplicação será utilizado o Flask, mas você pode utilizar outro WSGI de sua preferência.

No arquivo server.py definimos o nosso serviço, no caso o <code>/</code> irá retornar "Hello World!". Você pode fazer o teste executando <code>python server.py</code> e acessando a url <code>http://127.0.0.1:8080</code>.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/openshift-flask/server.py" type="text/javascript"></script>No arquivo setup.py definimos algumas configurações básicas para instalação do nosso aplicativo no rhc. Note que este arquivo é obrigatório e caso sua aplicação necessite algum pacote externo, este deve ser informado na variável <code>install_requires</code>. Ao fazer deploy da aplicação o rhc irá baixar essas dependências. Você pode obter mais informações sobre como configurar dependências de compilação na <a href="https://pythonhosted.org/setuptools/setuptools.html#declaring-dependencies">documentação</a> do setuptools. Você ainda pode utilizar um arquivo chamado requirements.txt para instalar as dependências via pip.<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/openshift-flask/setup.py" type="text/javascript"></script>

No arquivo wsgi.py definimos o ponto de entrada da nossa aplicação. Este arquivo também é obrigatório, pois é o ponto de entrada padrão configurado no rhc. O ponto de entrada pode ser alterado caso necessário, para isto deve-se alterar a variável de ambiente <code>OPENSHIFT_PYTHON_WSGI_APPLICATION</code>. Note que deve existir uma variável chamada <code>application</code>, que neste caso faz referência a instância Flask ou outro WSGI.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/openshift-flask/wsgi.py" type="text/javascript"></script>

<strong>Fazendo o deploy</strong>

Vamos assumir que você utilizará o ambiente web para deploy e que você já criou sua conta no OpenShift, caso não tenha feito <a href="https://www.openshift.com/app/account/new">clique aqui</a>.

Após ter feito o login, clique no botão abaixo:

<img src="/assets/wp-content/uploads/2014/10/add-rhc.png" alt="add" />

Após selecione a versão do Python:

<img src="/assets/wp-content/uploads/2014/10/python-rhc.png" alt="versão" />

Feito isto você deverá configurar a sua aplicação. A Public URL será a url que você deseja para a sua aplicação, para acessar via browser por exemplo. O Source Code é opcional, mas se informado um repositório do GitHub o rhc irá fazer o clone do repositório automaticamente. Em Scaling você deve selecionar se deseja ou não permitir o escalonamento da sua aplicação de acordo com o uso.

Feito isto clique em Create Application.

Após isto sua aplicação será iniciada e já estará executando. Se você não apontou uma url do GitHub você pode fazer clone da sua aplicação no rhc, para isto vá nas configurações de sua aplicação e procure por Source Code.

Este código foi baseado no <a href="https://github.com/openshift/flask-example">exemplo</a> disponibilizado pela OpenShift. Mais informações sobre hospedagem de aplicações Python no OpenShift podem ser encontradas <a href="https://developers.openshift.com/en/python-overview.html">aqui</a>.

Você pode encontrar <a href="https://github.com/penguinforge/openshift-cherrypy">aqui</a> um exemplo utilizando <a href="http://www.cherrypy.org/">CherryPy</a>. Outro framework web para Python.

Não deixe de comentar e assinar nosso feed RSS.