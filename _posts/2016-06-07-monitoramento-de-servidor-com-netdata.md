---
layout: wordpress
title: Monitoramento de servidor com Netdata
excerpt: |
  O Netdada é um projeto criado para exibir o monitoramento em tempo real de servidor com uma variedade de informações.
date: 2016-06-07 21:04:13
author: daniel_magevski
permalink: /monitoramento-de-servidor-com-netdata/
image: /assets/wp-content/uploads/2016/05/netdata-capa.png
categories:
  - Ferramentas
tags:
  - github
  - monitoramento
  - netdata
---

<h2>Introdução</h2>
O Netdada é um projeto criado para exibir o monitoramento em tempo real de servidor com uma variedade de informações.

<strong>O que ele monitora</strong>
<ul>
 	<li>Uso da CPU (total e por núcleo), interrupções, softirqs e freqüência.</li>
 	<li>Total de memória, RAM, Swap e Kernel (deduper incluindo KSM e núcleo de memória).</li>
 	<li>Disco I/O (por disco: largura de banda, operações, erros etc).</li>
 	<li>Interfaces de rede IPV4/IPV6 (por interface: largura de banda, pacotes, erros, e etc).</li>
 	<li>Netfilter/iptables (conexões, eventos, erros, etc).</li>
 	<li>Processos (executando, bloqueado,ativo, etc)</li>
 	<li>Aplicações, agrupado em árvore de processos (CPU, memória, leituras e gravação de disco, swap.</li>
 	<li>Servidor web Apache mod-estatuto (v 2.2, v 2.4)</li>
 	<li>Nginx web server stub-status.</li>
 	<li>Usuários e grupos (Consumo e processos por usuário e grupo, CPU, memória, swap, e etc.).</li>
 	<li>NFS file servers, v2, v3, v4 (I/O, cache, RPC e etc).</li>
 	<li>MySQL consultas, atualizações, problemas, thereads, etc.</li>
 	<li>ISC Bind  multiplos servidores, cada um exibindo: clientes, requisições, consultas, atualizações, falhas e etc.</li>
 	<li>Postfix.</li>
 	<li>Squid largura de Banda e etc.</li>
 	<li>Hardware (temperatura, voltage, e etc.)</li>
 	<li>Dispositivos SNMP.</li>
</ul>
<h2>Instalação</h2>
<strong>Debian / Ubuntu</strong>

<code>apt-get install zlib1g-dev gcc make git autoconf autogen automake pkg-config</code>

<strong>CentOS / Redhat / Fedora</strong>

<code>yum install zlib-devel gcc make git autoconf autogen automake pkgconfig</code>

Agora clone o repositório no <strong>Github.</strong>

<code>root@butecopensource:/# git clone https://github.com/firehol/netdata</code>

Entre no diretório

<code>root@butecopensource:/# cd netdata/</code>

Execute o script e digite Enter para confirmar

<code>root@butecopensource/netdata# ./netdata-installer.sh</code>

"Press <strong>ENTER</strong> to build and install netdata to your system"

Pressione <strong>ENTER</strong> para instalar.

Para acessar digite <strong>http://&lt;IP-SERVIDOR:19999 </strong>e para ver as configurações que estão rodando <strong>http://&lt;IP_SERVIDOR:19999/netdata.conf</strong>
<h2><a href="/assets/wp-content/uploads/2016/05/netdata.jpg"><img class="alignnone wp-image-5340" src="/assets/wp-content/uploads/2016/05/netdata-300x281.jpg" alt="netdata" width="546" height="511" /></a></h2>
<h2>Para atualizar</h2>
Entre no diretório clonado do github <strong>"netdata"</strong> e execute <code>./netdata-installer.sh</code> o script irá atualizar e reiniciar o Netdata

Confira um live demo do <a href="http://netdata.firehol.org" target="_blank">Netdata</a>

Veja o video

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=QIZXS8A4BvI" frameborder="0" allowfullscreen></iframe>

Fonte: <a href="http://www.tecmint.com/netdata-real-time-linux-performance-network-monitoring-tool/" target="_blank">Tecmint</a> e <a href="https://github.com/firehol/netdata/" target="_blank">Github(Netdata)</a>