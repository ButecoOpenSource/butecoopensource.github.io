---
layout: wordpress
title: Apache Mesos
excerpt: |
  Nos últimos tempos vem se falando muito em computação na nuvem, computação distribuída, Linux containers, Big Data, etc. Junto com o crescimento dessas tecnologias também se observa o surgimento de inúmeras ferramentas para resolver os problemas encontrados nesta área da computação. Poderíamos citar várias, mas iremos falar brevemente sobre Apache Mesos. Não irei me aprofundar muito pois pretendo fazer mais artigos sobre o assunto detalhando mais em determinados tópicos.
date: 2016-03-31 23:40:20
author: guilhermevanz
permalink: /apache-mesos/
image: /assets/wp-content/uploads/2016/03/apache_mesos.png
categories:
  - Ferramentas
tags:
  - apache
  - cloud
  - cluster
  - mesos
---

Nos últimos tempos vem se falando muito em computação na nuvem, computação distribuída, Linux containers, Big Data, etc. Junto com o crescimento dessas tecnologias também se observa o surgimento de inúmeras ferramentas para resolver os problemas encontrados nesta área da computação. Poderíamos citar várias, mas iremos falar brevemente sobre Apache Mesos. Não irei me aprofundar muito pois pretendo fazer mais artigos sobre o assunto detalhando mais em determinados tópicos.

O Apache Mesos é considerado o <em>kernel</em> de sistemas distribuídos. Ele foi criado com os mesmos princípios do <em>kernel</em> Linux, só que em outro nível de abstração. O Mesos roda em todos os nós de <em>cluster</em> e prove a <em>frameworks</em> como Apache Spark, Hadoop, Cassandra, Kafka, Elastic Search e outros uma API para alocar recursos e rodarem suas <em>tasks</em> através de todo o <em>cluster</em> ou cloud. Em um Mesos <em>cluster</em>, CPU, memória, disco e outros recursos computacionais de todas as máquinas, virtuais ou físicas, são abstraídos em um único <em>pool</em> de recursos. Facilitando a criação e otimizando a utilização de sistemas distribuídos.

<!--more-->
<h3><strong>Arquitetura</strong></h3>
O Mesos tem como objetivo prover um <em>core</em> confiável e escalável para que diversas aplicações consigam compartilhar um mesmo <em>cluster</em>. Para isso, ele fornece uma API mínima que permite compartilhar recursos de forma eficiente entre os <em>frameworks,</em> dando a eles o controle para programarem e executarem suas <em>tasks</em>. Sua arquitetura é composta por três componente principais: Mesos master, Mesos agent e os <em>frameworks</em>.

<em>Frameworks</em> são as aplicações que rodam em um Mesos <em>cluster</em>, cada um delas possui um <em>scheduler </em>e um<em> executor. </em>O <em>scheduler</em> é a aplicação que se registra no <em>master</em> para que então possa alocar recursos e enviar <em>tasks</em> para execução. O <em>executor</em> é o processo executado nos nó dos <em>cluster</em> para executar as tarefas do <em>framework.</em> O Mesos <em>agent</em> é o processo <em>daemon</em> que roda em todos os nós do <em>cluster</em>. Sua responsabilidade é alocar os recursos definidos para cada <em>task</em> enviada pelo Mesos <em>master</em> e executa-la (através do <em>executor</em>). O Mesos <em>master, </em>como o próprio nome diz, é o processo que gerencia todo<em> cluster. A</em>través do seu módulo de alocação é definido quanto de recursos deve ser oferecido para cada <em>framework</em>. É no <em>master</em> também que os <em>agents</em> se registram para reportar o quanto possuem de recursos disponíveis, atualizar o status das <em>tasks</em> em execução e etc.

<a href="/assets/wp-content/uploads/2016/03/architecture3.jpg" rel="attachment wp-att-5032"><img class="wp-image-5032 aligncenter" src="/assets/wp-content/uploads/2016/03/architecture3-300x202.jpg" alt="architecture3" width="434" height="292" /></a>
<h4>Oferta de recursos</h4>
Para permitir que o mesmo cluster possa ser utilizado por diversos <em>frameworks</em> e o Mesos continue se mantendo simples e escalável, é utilizado uma abordagem de oferta de recursos. Isso significa que o Mesos <em>master</em>, utilizando o módulo de alocação, define o quanto de recursos devem ser ofertado para cada <em>framework</em> rodando no <em>cluster</em>. Uma vez feita a oferta, o <em>scheduler</em> da cada <em>framework</em> tem a liberdade de aceitar ou recusar os recursos.

<a href="/assets/wp-content/uploads/2016/03/mesos_resource_offers.jpg" rel="attachment wp-att-5044"><img class="wp-image-5044 aligncenter" src="/assets/wp-content/uploads/2016/03/mesos_resource_offers-300x207.jpg" alt="mesos_resource_offers" width="509" height="351" /></a>

A oferta de recursos começa quando o <em>agent</em> registrado no <em>master</em> reporta o quando de recursos possui disponível para ser utilizado. Uma vez com essas informações, o módulo de alocação do <em>master</em> pode decidir o quando de recurso pode ser ofertado para cada <em>framework</em>. Lembrando que as ofertas podem ser diferentes, isso depende de qual módulo de alocação segue as políticas de alocação de cada organização. Uma vez feita a oferta o <em>scheduler</em> do <em>framework</em> tem a responsabilidade de aceitar ou recusa baseado em suas necessidades. Caso o <em>framework</em> decida aceitar a oferta é retornado ao <em>master</em> uma descrição das tarefas que devem ser executadas e quanto de recursos devem ser alocados para cada uma. O <em>master</em> por sua vez, envia esses dados para o <em>agent</em> que aloca os recursos especificados para o <em>executor</em> do <em>framework</em>, este por sua vez executa as <em>tasks</em> especificadas pelo <em>scheduler</em>. Não vou entrar muito em detalhes de como a oferta de recursos acontece na prática para não estender muito o texto. Pretendo entrar em detalhes em um artigo futuro sobre como implementar um <em>framework.</em>
<h3>Em ação</h3>
Como a maioria dos projetos Open Source de sucesso, existe uma empresa por trás do projeto que fomenta o desenvolvimento e vende serviços e produtos baseados neste software. No caso do Apache Mesos a empresa por trás é a <a href="https://mesosphere.com/" target="_blank">Mesosphere</a> e produto em questão é o <em>Datacenter Operating System</em> (DCOS) . É possível ver o DCOS em ação neste video:
<p class="aligncenter"><iframe class="aligncenter" src="https://www.youtube.com/embed/0I6qG9RQUnY" width="420" height="315" frameborder="0" allowfullscreen="allowfullscreen"></iframe></p>

<h4>Referencias</h4>
<a href="https://www.cs.berkeley.edu/~alig/papers/mesos.pdf">Mesos paper</a>
<a href="http://mesos.apache.org/">Apache Mesos site</a>
<a href="http://mesosphere.com/">Mesosphere</a>