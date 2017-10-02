---
layout: wordpress
title: Visão geral do Dandified Yum
excerpt: |
  O DNF é um gerenciador de pacotes direcionado aos pacotes RPM e, à partir da versão 22 da distribuição do Fedora, passou a ser o gerenciador de pacotes oficial em substituição ao Yum. O DNF é um fork do Yum, que visa corrigir problemas sérios com a API, alguns algoritmos com mal funcionamento e falta de documentação.
date: 2015-08-24 14:07:37
author: alexandrevicenzi
permalink: /visao-geral-do-dandified-yum/
image: /assets/wp-content/uploads/2015/05/infinity-logo_400x400.png
categories:
  - Discussão
tags:
  - distros
  - dnf
  - fedora
  - rpm
  - yum
---

Olá pessoal! Neste artigo procurarei descrever sobre alguns dos principais comandos do <em>Dandified Yum</em>, carinhosamente apelidado de DNF, espero ser útil àqueles que encontraram alguma dificuldade, não tiveram a oportunidade ou necessidade em usá-lo.

<!--more-->

O DNF é um gerenciador de pacotes direcionado aos pacotes RPM e, à partir da versão 22 da distribuição do Fedora, passou a ser o gerenciador de pacotes oficial em substituição ao Yum. O DNF é um <em>fork</em> do Yum, que visa corrigir problemas sérios com a API, alguns algoritmos com mal funcionamento e falta de documentação. De acordo com o site oficial do projeto, isto era inevitável, o Yum não sobreviveria ao python 3 como padrão na distribuição, visto que o DNF deve ser compatível com python 2 e 3. Dentre as melhorias que o DNF trás estão, performance, uso de memória, resolução de dependência e velocidade.

Para que a transição do Yum ao DNF não fosse abrupta, causando demasiados problemas à distribuição e para a comunidade, os comandos que chamam o Yum serão automaticamente redirecionados para o DNF, pois o mesmo mantém compatibilidade em linha de comando, para continuar a lógica semântica do Yum. Atualmente a equipe de desenvolvimento se esforça para converter as APIs populares do Yum para o DNF, melhorar a experiência de usuário e o <em>plugin migrate</em> que ajuda na conversão dos pacotes.

Então, o Yum é um projeto considerado oficialmente morto, e caso esteja interessado em conhecer detalhes sobre o DNF, o fim do Yum e/ou as diferenças entre ambos, visite <a href="http://dnf.baseurl.org">http://dnf.baseurl.org</a>, onde há muita informação. Realmente capricharam, tudo está documentado.

Em minha opinião, a <em>manpage</em> mais organizada e enxuta é um dos sinais de que a documentação foi melhorada no DNF, muito do que vou dizer aqui é facilmente encontrado lá. Se você não é acostumado a ler uma <em>manpage</em>, após a leitura deste artigo, certamente ficará mais compreensível.

Para iniciarmos a parte dos comandos, a sintaxe geral do DNF é <strong>dnf [opções] [...]</strong>, lembrando que, os comandos que alteram o sistema devem ser acompanhados pelo sudo ou serem executados através do usuário root.

Pensando numa lógica de uso, um dos comandos que tem uma boa chance de ser necessário é o repolist, que apresenta a lista de repositórios instalados, podendo ser habilitados, desabilitados ou ambos. Em caso de omissão do argumento, serão listados somente os repositórios habilitados.

Exemplos:

$ dnf repolist enabled

$ dnf repolist disabled

$ dnf repolist all

O próximo comando é o <em>list</em>, que nos ajuda a verificar a existência de pacotes disponíveis em algum repositório conhecido pelo sistema (<em>available</em>) ou pacotes instalados no sistema (<em>installed</em>).

Exemplo:

$ dnf list

Nesta forma apresentada acima, listará todos os pacotes, tanto os instalados como os dos repositórios conhecidos pelo sistema. Pode ser filtrado com a especificação do nome de um pacote, que é <em>case sensitive</em> e aceita hífen, assim como caracteres coringas.

Exemplo:

$ dnf list nan?

Abaixo, seguem outras variantes interessantes, onde todas podem receber filtros:

$ dnf list installed

Lista os pacotes instalados.

$ dnf list available

Lista os pacotes disponíveis nos repositórios conhecidos pelo sistema.

$ dnf list obsoletes

Lista pacotes instalados no sistema que estão obsoletos em relação aos pacotes de qualquer repositório conhecido.

$ dnf list recent

Lista os pacotes recentemente adicionados aos repositórios conhecidos.

$ dnf list upgrades

Lista atualizações disponíveis aos pacotes instalados no sistema.

O terceiro comando que irei falar é o <em>search</em>, que serve para pesquisar metadados de pacotes através de palavras-chave. Palavras-chave são <em>case</em> <em>insensitive</em> e aceitam caracteres coringas. Por padrão, o comando busca primeiro os nomes de pacotes e resumos, na sua falta (ou sempre que tudo foi dado como um argumento) ele irá procurar nas descrições dos pacotes e URLs. O resultado é classificado a partir da relevância dos resultados (do maior para o menor).

Exemplo:

$ dnf search kmail

É possível também especificar em qual repositório será feita a busca com a opção --enablerepo (--enablerepo=).

Exemplo:

$ dnf --enablerepo=*fedora search nan*

Nosso quarto item da lista de comandos é o <em>install</em>, sua sintaxe geral é <strong>dnf [opções] install </strong>, onde pode ser o nome do pacote, o endereço de um pacote RPM local, ou URL de um pacote RPM remoto. Este comando não resolve dependências.

Exemplo:

$ sudo dnf install cowsay.noarch

Algumas opções interessantes para se utilizar juntamente com o comando <em>install</em> são: --enablerepo, para escolher o repositório de onde virá a instalação (se não for local ou URL); -q ou --quiet, que executará sem retornos (silenciosamente); -v ou --verbose, para ver todos os detalhes disponíveis durante a instalação; e -y ou --assumeyes, para responder sim automaticamente para todas as opções que esperam uma confirmação (s/n).

Certamente em algum momento também será necessário remover alguns pacotes instalados no sistema, para isto utiliza-se o comando <em>remove</em>. Este comando, faz a remoção dos pacotes especificados, juntamente com quaisquer pacotes dependentes dos pacotes que estão sendo removidos e, por padrão (com clean_requirements_on_remove habilitado) também removerá todas as dependências que não serão mais necessárias ao sistema.

Sua sintaxe geral é <strong>dnf [opções] remove </strong>, onde, pode ser o nome exato de um pacote ou parcial acompanhado de caracteres coringas para especificar um grupo de pacotes.

Exemplos:

$ sudo dnf remove kontact

ou

$ sudo dnf remove kmail*

Em alguns artigos você pode encontrar também o comando <em>erase</em>, porém, este é um alias para o <em>remove</em>, e já está marcado como <em>deprecated</em>, isto significa que está disponível apenas para compatibilidade com Yum mas será removido em uma das próximas versões, por isto não é aconselhável o seu uso, principalmente em <em>scripts</em> que você queira usar a longo prazo.

Acredito que estes sejam os comandos indispensáveis para se ter uma visão geral do DNF e que, abordei os tipos de filtros que serão vistos em outros comandos deste gerenciador, se você der uma olhadinha na <em>manpage</em>. Para instigar a sua curiosidade, vou deixar registrado aqui que não falei ainda sobre: busca de pacote por arquivo (<em>provides</em>), <em>repository-packages</em>, reinstalação, manutenção e limpeza de cache, <em>distro-sync</em>, <em>upgrade</em> e <em>downgrade</em>, grupos de pacotes, dentre outros.

<em>That's all folks!</em>

Este artigo foi enviado por Douglas Santos.