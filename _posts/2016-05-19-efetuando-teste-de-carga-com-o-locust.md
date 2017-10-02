---
layout: wordpress
title: Efetuando teste de carga com o Locust
date: 2016-05-19 00:43:51
author: alexandrevicenzi
permalink: /efetuando-teste-de-carga-com-o-locust/
image: /assets/wp-content/uploads/2016/05/locust-logo.png
categories:
  - Ferramentas
tags:
  - python
  - testes
  - web
---

Os testes de carga consistem em colocar uma demanda em um sistema de software ou dispositivo e medir a sua resposta. Este tipo de teste é realizado para determinar o comportamento de um sistema sob condições normais e picos de carga. Ela ajuda a identificar a capacidade máxima de operação de uma aplicação, bem como os gargalos e determinar qual elemento está causando lentidão.

Uma das ferramentas mais conceituadas nesse tipo de testes é o <a href="http://jmeter.apache.org/" target="_blank">Apache JMeter™</a>, porém hoje iremos abordar o <a href="http://locust.io/" target="_blank">Locust</a>, uma ferramenta escrita em Python extremamente simples e poderosa.
<!--more-->

O Locust é focado em teste de aplicações Web, possuindo possibilidade de distribuição entre várias máquinas, criando um cluster para teste, podendo simular milhões de usuário conectados simultaneamente. A configuração é toda feita em Python, sem a necessidade de arquivos XML's gigantes como alguns de seus concorrentes.

<strong>Instalação</strong>

O Locust é apenas compatível com Python 2.6 e 2.7. Para instalar basta executar o comando:

<code>pip install locustio</code>

<strong>Exemplo de configuração</strong>

Vamos criar um arquivo chamado <code>locustfile.py</code> e adicionar o código:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/locustfile.py?branch=master" type="text/javascript"></script>

O método <code>on_start</code> é responsável por autenticar o nosso client HTTP, caso sua aplicação necessite autenticação. <code>index</code>, <code>about</code> e <code>catch_response</code> são os <em>endpoints</em> que irão ser testados. Note que eles são decorados com <code>@task</code>, isto indica que ao disparar os testes de carga, esses dois <em>endpoints</em> serão testados com o mesmo peso de usuários. Por exemplo, se definirmos que serão 1000 usuários simultâneos ambos receberão esta carga. Um meio de mudar isto é passar um número para o <em>decorator</em>, como por exemplo <code>@task(2)</code>, isto indica que o endpoint tem peso maior, neste caso o dobro de usuários.

Se você já é acostumado com Python e conhece a biblioteca <a href="http://docs.python-requests.org/en/master/" target="_blank">requests</a>, o <code>self.client</code> é uma sessão do requests.

No teste <code>catch_response</code> observamos como tratar um resultado, no nosso caso, necessitamos tratar pois a página deverá retornar 404, caso não for tratado o Locust irá entender que a página contém um erro, pois todos os resultados devem retornar código de sucesso. Quando utilizamos a opção <code>catch_response=True</code> o Locust irá assumir a nossa validação como validado.

<strong>Executando o Locust</strong>

O Locust pode ser executado através de uma interface Web, ou se você preferir através do terminal por completo.

Para iniciar os testes com interface web execute o comando:

<code>locust -f locustfile.py -H http://meusite.com</code>

Após isto acesse <a href="http://127.0.0.1:8089" target="_blank">http://127.0.0.1:8089</a>. Você deverá ver uma tela similar a esta:

<a href="/assets/wp-content/uploads/2016/05/locust-screenshot.png"><img class="aligncenter size-large wp-image-5348" src="/assets/wp-content/uploads/2016/05/locust-screenshot-1024x746.png" alt="locust-screenshot" width="648" height="472" /></a>

Nela basta definir a quantidade de usuários simultâneos e o <em>hatch rate</em> (frequência de chegada de usuários), e esperar os resultados.

Para executar todos os testes através da linha do terminal execute o comando:

<code>locust -f locustfile.py -H http://meusite.com -c 100000 -r 1000 -n 10000 --no-web</code>

Para entender um pouco melhor, <code>-c</code> é o número de clientes conectados, <code>-r</code> é o <em>hatch rate</em> e <code>-n</code> é o número de requests a serem executados.

<strong>Consideração final</strong>

Lembre-se, se você executar os testes apenas de uma máquina você não irá conseguir simular muitos usuários simultâneos. Isso porque o seu computador pode não aguentar a carga que você deseja simular.

Outro ponto importante é executar o teste de diferentes regiões, se você executar todos os testes dentro de uma mesma LAN, pode ser que alguém em algum lugar faça algum tipo de cache, e você não simule realmente 50 mil usuários conectados ao redor do Brasil.

Para testes utilizando clusters, uma boa pedida é Amazon EC2 ou Digital Ocean, pois elas possuem máquinas em diferentes regiões. Claro existem outros provedores além destes, fica a seu critério de como montar os testes.