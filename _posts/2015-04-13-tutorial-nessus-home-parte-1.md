---
layout: wordpress
title: Tutorial Nessus Home Parte 1
excerpt: |
  Breve introdução sobre o Nessus.
  Nessus é um programa de verificação de falhas/vulnerabilidades de segurança. Ele é composto por um cliente e servidor, sendo que o scan propriamente dito é feito pelo servidor. O nessusd (servidor Nessus) faz um port scan ao computador alvo, depois disso vários scripts (escritos em NASL, Nessus Attack Sincripta Language) ligam-se a cada porta aberta para verificar problemas de segurança.
  Ele é ideal para você fazer análise da rede da sua casa, lembrando que para fins comerciais existem outras versões.
  O Nessus é distribuído sob os termos da Licença Pública Geral GNU.
date: 2015-04-13 22:41:54
author: daniel_magevski
permalink: /tutorial-nessus-home-parte-1/
categories:
  - Ferramentas
tags:
  - ferramenta
  - redes
  - segurança
---

<a href="/assets/wp-content/uploads/2015/04/Nessus-home.jpg"><img class="alignnone  wp-image-1817" src="/assets/wp-content/uploads/2015/04/Nessus-home.jpg" alt="Nessus-home" width="567" height="100" /></a>

<strong>Introdução.</strong>

Esse artigo ensinará a instalação do Nessus Home para Linux, ele possui a licença grátis para estudo e testes em casa.

<strong>Breve introdução sobre o Nessus.</strong>

Nessus é um programa de verificação de falhas/vulnerabilidades de segurança. Ele é composto por um cliente e servidor, sendo que o scan propriamente dito é feito pelo servidor. O nessusd (servidor Nessus) faz um port scan ao computador alvo, depois disso vários scripts (escritos em NASL, Nessus Attack Sincripta Language) ligam-se a cada porta aberta para verificar problemas de segurança.

Ele é ideal para você fazer análise da rede da sua casa, lembrando que para fins comerciais existem outras versões.

O Nessus é distribuído sob os termos da Licença Pública Geral GNU.
<strong>Download</strong>

O Nessus Home está disponível para download em vários sistemas operacionais.

<a href="/assets/wp-content/uploads/2015/04/S.O-Nessus.jpg"><img class="alignnone  wp-image-1815" src="/assets/wp-content/uploads/2015/04/S.O-Nessus.jpg" alt="S.O-Nessus" width="511" height="226" /></a>

Porém o foco desse artigo é para instalação em Linux que tem essas opções.

Link para a página de <a href="//www.tenable.com/products/nessus/select-your-operating-system" target="_blank">download</a> do Nessus Home:

<a href="/assets/wp-content/uploads/2015/04/Nessus-Distros.jpg"><img class="alignnone size-medium wp-image-1818" src="/assets/wp-content/uploads/2015/04/Nessus-Distros-281x300.jpg" alt="Nessus-Distros" width="281" height="300" /></a>

Instalarei no Kali Linux que é a primeira opção que vem com extensão .deb.

Depois que o arquivo já estiver baixado, você deverá ir na pasta que ele está, geralmente no Kali vai para Desktop direto, na maioria das distribuições vai para pasta Download.

Use o comando: ls para lista as pastar no diretório.

Use o comando: <code>#<em>chmod +x nome_do_arquivo</em> </code> ou se você não estiver como root use o "sudo" na frente desse comando.

Como o arquivo é .deb usaremos o dpkg: <em># dpkg -i nome_do_arquivo</em>.

Se tudo estiver correto aparecerá como na janela abaixo

<a href="/assets/wp-content/uploads/2015/04/Nessus001.jpg"><img class="alignnone  wp-image-1825" src="/assets/wp-content/uploads/2015/04/Nessus001.jpg" alt="Nessus001" width="485" height="354" /></a>

O Nessus por padrão roda na porta 8834.

Agora iniciaremos o Nessus.

Use o comando quando quiser iniciar o Nessus: /<em>etc/init.d/nessusd start</em>

Quando quiser parar o programa pode colocar stop ou restart no lugar do start

Veja a imagem abaixo:

<a href="/assets/wp-content/uploads/2015/04/Nesus002.jpg"><img class="alignnone  wp-image-1816" src="/assets/wp-content/uploads/2015/04/Nesus002.jpg" alt="Nesus002" width="485" height="325" /></a>

Agora entraremos pelo navegador:

Digite: https://127.0.0.1:8834

Poderá aparecer um aviso como o da imagem abaixo, pois o Nessus utiliza <span class="st">Secure Socket Layer</span> (SSL).

Para continuar click em: I Undestand the Risks

<a href="/assets/wp-content/uploads/2015/04/Nessus003.jpg"><img class="alignnone  wp-image-1824" src="/assets/wp-content/uploads/2015/04/Nessus003.jpg" alt="Nessus003" width="482" height="344" /></a>

Quando o Nessus iniciar aparecerá essa tela:

<a href="/assets/wp-content/uploads/2015/04/Nessus004.jpg"><img class="alignnone  wp-image-1823" src="/assets/wp-content/uploads/2015/04/Nessus004.jpg" alt="Nessus004" width="481" height="312" /></a>

Agora criaremos um usuário e uma senha para acessar o sistema, nesse exemplo colocarei uma senha fácil para memorização: usuário root e senha toor,

lembrando que você pode colocar qualquer senha.

<a href="/assets/wp-content/uploads/2015/04/Nessus005.jpg"><img class="alignnone  wp-image-1822" src="/assets/wp-content/uploads/2015/04/Nessus005.jpg" alt="Nessus005" width="492" height="320" /></a>

O próximo passo e colocar um código que você recebe por e-mail depois de pedir no site do Nessus, podem entrar no <a href="//www.tenable.com/products/nessus-home" target="_blank">link</a>

<a href="/assets/wp-content/uploads/2015/04/Nessus006.jpg"><img class="alignnone  wp-image-1821" src="/assets/wp-content/uploads/2015/04/Nessus006.jpg" alt="Nessus006" width="504" height="248" /></a>

Faça o registro normalmente que você receberá em poucos minutos o código de ativação

<a href="/assets/wp-content/uploads/2015/04/Nessus007.jpg"><img class="alignnone  wp-image-1820" src="/assets/wp-content/uploads/2015/04/Nessus007.jpg" alt="Nessus007" width="504" height="306" /></a>

Irá parecer como na janela abaixo.

<a href="/assets/wp-content/uploads/2015/04/Nessus008.jpg"><img class="alignnone  wp-image-1819" src="/assets/wp-content/uploads/2015/04/Nessus008.jpg" alt="Nessus008" width="514" height="253" /></a>

Esse tutorial ensinou a você a fazer o download e instalação do Nessus Home, nos próximos artigos ensinaremos mais funções dele, tais como fazer scanner,

interpretar as informações dele, entender os riscos caso algum falha seja encontrado e o conceito de Common Vulnerabilities and Exposures (CVE) e muito mais.

Site oficial do <a href="//www.tenable.com/" target="_blank">Nessus</a>.

Wikipédia sobre o <a href="//pt.wikipedia.org/wiki/Nessus" target="_blank">Nessus</a>.