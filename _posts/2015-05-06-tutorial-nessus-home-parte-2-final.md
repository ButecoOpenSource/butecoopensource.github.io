---
layout: wordpress
title: Tutorial Nessus Home Parte 2 (Final)
excerpt: |
  Nesse artigo irei dar continuação, agora abordando politicas, varreduras e analisa de vulnerabilidades
date: 2015-05-06 22:59:54
author: daniel_magevski
permalink: /tutorial-nessus-home-parte-2-final/
categories:
  - Ferramentas
tags:
  - ferramenta
  - redes
  - segurança
---

<a href="/assets/wp-content/uploads/2015/04/Nessus-home.jpg"><img class="alignnone size-full wp-image-1817" src="/assets/wp-content/uploads/2015/04/Nessus-home.jpg" alt="Nessus-home" width="641" height="113" /></a>

Nesse artigo falaremos em políticas e varreduras.

Com o programa já instalado iremos entrar efetuar o login.

Caso você não tenha visto a parte 1 que fala sobre a instalação, <a href="/2015/04/13/tutorial-nessus-home-parte-1/" target="_blank">veja aqui.</a>

Na parte superior podemos ver (Scans) varreduras e (Policies) políticas.

<a href="/assets/wp-content/uploads/2015/05/tutorial2-1.jpg"><img class="alignnone  wp-image-2036" src="/assets/wp-content/uploads/2015/05/tutorial2-1.jpg" alt="tutorial2-1" width="735" height="525" /></a>

Vamos criar uma política para nossa varredura.

Selecionamos Policies &gt; New Policy

Eu selecionei Advanced Scan, mas você pode escolher Basic Network Scan.

Em algumas versões é preciso criar uma política antes de qualquer varredura,  mas nesta não.

<img class="alignnone  wp-image-2040" src="/assets/wp-content/uploads/2015/05/tutorial2-3.jpg" alt="tutorial2-3" width="729" height="528" />

<a href="/assets/wp-content/uploads/2015/05/tutorial2-2.jpg"><img class="alignnone  wp-image-2038" src="/assets/wp-content/uploads/2015/05/tutorial2-2.jpg" alt="tutorial2-2" width="737" height="523" /></a>

Algumas especificações rápidas tiradas a guia do usuário no site oficial.

<em>Host Discovery (Descoberta de host)</em>  - Identifica hosts ativos e portas abertas.

<em>Basic Network Scan (Varredura básica de rede)</em> - Para usuários fazendo varredura de hosts

internos ou externos.

<em>Web Application Tests (Testes de aplicativos da Web)</em> - Para usuários fazendo varreduras em

aplicativos genéricos da Web.

<em>Advanced Policy (Política avançada) </em> - Para usuários que querem controle total da configuração

de políticas.

Agora vamos fazer a varredura, ela pode ser Avançada ou Básica, os campos de preenchimentos em

(General) são os mesmos

Depois de ter feito a politica, vá em Scans &gt; New Scaner

<a href="/assets/wp-content/uploads/2015/05/tutorial2-4.jpg"><img class="alignnone  wp-image-2048" src="/assets/wp-content/uploads/2015/05/tutorial2-4.jpg" alt="tutorial2-4" width="770" height="542" /></a>

Como podemos ver na imagem precisamos preencher com informações básicas, na parte Targets (Alvos)

é o local da rede, nessa parte um conhecimento básico de rede irá ajudá-lo, o sistema faz varredura

por faixas de IP ou pela rede completa. Ex: Quero somente analisar essa faixa de IP 192.168.0.2 – 192.168.010/24

ou a rede toda, 192.168.0.1/24 , 24 no final tem a ver com máscara da sua rede, se for C será 24, B 16 e A 8,

caso não saiba, digite no terminal de comando <i>ifconfig</i>

<i>O padrão é: 255.0.0.0 = A , 255.255.0.0 =B, 255.255.255.0 = C, caso esteja diferente do padrão ou mesmo assim você</i>

<i>esteja com dúvida, sugiro a leitura </i><a href="//pt.wikipedia.org/wiki/M%C3%A1scara_de_rede" target="_blank">Máscara de Rede</a>

Exite algumas configurações na parte esquerda da página, como Shedule (Horario) Email Notifications

(Notificação de Email) e outras.

A ideia do tutorial é teste em casa ou em pequenos locais que você tenha autorização para excecuta, varreduras em

redes com muitos computadores ou dispositivos em rede pode demorar muito, como em empresas e faculdades.

No momento que escreve este artigo estou utilizando a versao 6.3.2 Nessus Home.

Exemplos que peguei de varreduras.

<a href="/assets/wp-content/uploads/2015/05/tutorial2-5.jpg"><img class="alignnone  wp-image-2053" src="/assets/wp-content/uploads/2015/05/tutorial2-5.jpg" alt="tutorial2-5" width="767" height="384" /></a>

<a href="/assets/wp-content/uploads/2015/05/tutorial2-6.jpg"><img class="alignnone  wp-image-2052" src="/assets/wp-content/uploads/2015/05/tutorial2-6.jpg" alt="tutorial2-6" width="779" height="432" /></a>

&nbsp;

Após realizar a varredura você vera os níveis de riscos e as informações, eles irão gerar um codigo, <b>Common </b>

<b>Vulnerabities and Exposures</b> <a href="//cve.mitre.org/" target="_blank">CVE</a>

<b>Common Vulnerability Scoring Sys</b><b>tem <a href="//www.first.org/cvss" target="_blank">CVSS,</a></b>  com o ano da vulnerabilidade e o codigo, EX: <a href="//cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0160" target="_blank">CVE-2014-0160 </a>

OpenSSL 'Heartbleed' vulnerability, uma vulnerabilidade que ficou muito conhecida.

Ou seja, uma lista já catalogada com os riscos, nela você irá encontrar informações sobre as falhas e como repará-la.

O número aparece no canto direito quando você clica em informações sobre a varredura, é só selecionar o (Host)

maquina que deseja olhar qual vulnerabilidade você quer. Agora você sabe instalar o Nessus, criar política, varreduras

e analisá-la, também o Nessus permite você importar e exportar varreduras, após selecionada a varredura, a opção exportar e

importar ficará na parte superior.

Se você pretende realizar varreduras mais avançadas sugiro a leitura da documentação oficial do <a href="//www.tenable.com/products/nessus/documentation" target="_blank">Nessus</a>,

alguns manuais estão em português.

Bons estudos!!!