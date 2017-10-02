---
layout: wordpress
title: "Instalando o Supervisor: Um sistema de controle de processos"
excerpt: |
  Confira como instalar e configurar o Supervisord.
  O Supervisor é um sistema cliente/servidor que permite que os usuários monitorem e controlem inúmeros processos em sistema operacionais UNIX-like.
date: 2015-07-15 08:38:44
author: alexandrevicenzi
permalink: /instalando-o-supervisor-um-sistema-de-controle-de-processos/
categories:
  - Ferramentas
tags:
  - daemon
  - gerenciamento
  - linux
  - processos
  - systemd
---

O <a href="http://supervisord.org/">Supervisor</a> é um sistema cliente/servidor que permite que os usuários monitorem e controlem inúmeros processos em sistema operacionais UNIX-like.

<img class=" aligncenter" src="/assets/wp-content/uploads/2015/07/logo_supervisord.gif" alt="Supervisord" />

Ele possui alguns objetivos de programas similares, como o launchd, daemontools e runit. Mas diferente destes, ele não pretende ser um substituto ao <em>init</em>, pelo contrário, ele inicia na inicialização do sistema como qualquer outro aplicativo.

<!--more-->

Lembra aquela aplicação Python ou Node.JS que você fez e precisa deixar executando 24 horas por dia e ainda tem que iniciar junto com o boot? Quem nunca fez uma aplicação nesse estilo e tentou fazer um shell para iniciar um daemon.

Fazer algo assim é perda de tempo na minha opinião e sempre gera algum transtorno. A forma mais simples e segura que encontrei de automatizar esta tarefa é usando o Supervisor.

Com ele você controla quando iniciar e parar a aplicação, além de uma série de outras configurações.

<strong>Instalação</strong>

Algumas distribuições Linux oferecem a instalação do Supervisor pelo gerenciador de pacotes. Para garantir que instalaremos a versão mais recente, vou utilizar a versão disponível via <em>pip</em>. O <em>pip</em> é o gerenciador de pacotes do Python.

Antes de instalar, vamos garantir que temos os pacotes necessários para o uso do <em>pip</em>, para isso execute o comando abaixo:

<code>sudo yum install python-setuptools python-pip</code>

Após instalar o <em>pip</em> e suas dependências, vamos a instalação do Supervisor. Para isso execute o comando abaixo:

<code>sudo pip install supervisor</code>

Agora que ele está instalado, necessitamos configurá-lo e criar o arquivo de entrada para o Systemd.

Para criar o arquivo de configuração padrão execute o comando abaixo:

<code>sudo echo_supervisord_conf &gt; /etc/supervisord.conf</code>

Após, vamos criar a entrada para o Systemd. O arquivo deve ser <em>/usr/lib/systemd/system/supervisord.service</em> e seu conteúdo será o abaixo:

<pre><code class="bash">
[Unit]
Description=Supervisor Daemon

[Service]
Type=forking
ExecStart=/usr/bin/supervisord
ExecStop=/usr/bin/supervisorctl $OPTIONS shutdown
ExecReload=/usr/bin/supervisorctl $OPTIONS reload
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target
</code></pre>

Este arquivo foi testado no CentOS com Systemd, caso você deseja utilizar em outra distribuição recomento procurar um script compatível com a sua distro. Você pode encontrar vários arquivos de configuração <a href="https://github.com/Supervisor/initscripts">aqui</a>.

Agora que está tudo configurado, vamos iniciar o serviço com o comando abaixo:

<code>sudo systemctl start supervisord</code>

Vamos verificar se tudo ocorreu bem, para isto execute o comando abaixo:

<code>sudo supervisorctl status</code>

Para iniciar o Supervisor no boot, basta executar o comando:

<code>sudo systemctl enable supervisord</code>

<strong>Adicionado aplicações</strong>

Por fim, para adicionar um programa ao Supervisor é necessário editar o arquivo <em>/etc/supervisord.conf</em>. Procure pela entrada <em>[program:theprogramname]</em> e substitua ela pela aplicação que você deseja.

No exemplo abaixo você pode observar como eu deixo o <a href="//gistfy-app.herokuapp.com">Gistfy</a> no ar. Este é o comando mais básico e obrigatório. Existem outras configurações, como logs e controles em caso de erros.

<pre><code class="bash">
[program:gistfy]
command=node /home/gistfy/src/gistfy.js --port=5000 --base_url=//gistfy-app.herokuapp.com
</code></pre>

Confira <a href="http://supervisord.org/configuration.html#program-x-section-settings">a documentação</a> para entender melhor todos os parâmetros.

Agora para iniciar nossa aplicação, executamos o seguinte comando:

<code>sudo supervisorctl start gistfy</code>

Com o Supervisor você pode controlar vários aplicativos ao mesmo tempo de uma forma muito simples. Ele também oferece uma interface Web para monitoramento das aplicações, que pode ser habilitada facilmente no arquivo de configurações.

Espero que este artigo tenha sido útil, não esqueça de deixar o seu comentário.