---
layout: wordpress
title: Corrigindo problemas de conexão do zypper no openSUSE 13.2
excerpt: |
  Veja como corrigir problemas de conexão do zypper no openSUSE.
date: 2015-01-29 21:35:09
author: alexandrevicenzi
permalink: /corrigindo-problemas-de-conexao-do-zypper-no-opensuse-13-2/
image: /assets/wp-content/uploads/2015/01/Opensuse-logo.png
categories:
  - Dicas
tags:
  - opensuse
  - yast
  - zypper
---

Esta semana resolvi atualizar meu openSUSE para o 13.2. É notável as melhorias em relação a versão 13.1. O que mais me chamou a atenção foi o GNOME 3.14 muito mais fluído, sem problemas de transição.

Porém nem tudo é perfeito. Meu primeiro problema foi incompatibilidade com o <em>dual graphics</em> Intel + NVidia. Este problema não consegui resolver 100%, então deixarei para comentar em outra publicação. O segundo problema foi o fato de o <em>zypper/Yast</em> não conseguirem se conectar aos repositórios do openSUSE.

Basta você executar o comando abaixo:
<pre><code>sudo zypper refresh</code></pre>
Para ter o seguinte problema:
<pre><code>Download (curl) error for 'http://download.opensuse.org/distribution/13.2/repo/non-oss/content':
Error code: Connection failed
Error message: Failed to connect to download.opensuse.org port 80: Network is unreachable</code></pre>
Se você atualizou recentemente para o openSUSE 13.2, talvez você esteja na mesma situação que eu.

Pesquisando um pouco no fórum do openSUSE, você talvez encontre a seguinte solução:

Adicionar as linhas abaixo no arquivo <em>/etc/sysctl.conf</em>:
<pre><code>#disable ipv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.default.disable_ipv6 = 1
net.ipv6.conf.lo.disable_ipv6 = 1</code></pre>
E executar o comando abaixo como <em>su</em>:
<pre><code>echo 1 &gt; /proc/sys/net/ipv6/conf/all/disable_ipv6</code></pre>
Pois bem, esta solução funciona... até você reiniciar o computador. Ou seja, toda vez após o boot você deve desabilitar o ipv6.

Mas e agora, como vamos corrigir isto? Bem, eu corrigi de uma forma muito simples, espero que funcione para outras pessoas.

Para desabilitar o ipv6 definitivamente, vá em Rede.

<img src="/assets/wp-content/uploads/2015/01/network.png" alt="Rede" />

Após isto, escolha a sua rede, note que você tem que fazer isto para cada Wifi ou Cabo conectado, e desabilite a opção ipv6.

<img src="/assets/wp-content/uploads/2015/01/wired.png" alt="ipv6" />

Simples, não?

Espero que esta dica ajude outras pessoas, assim como salvou meu dia. :)