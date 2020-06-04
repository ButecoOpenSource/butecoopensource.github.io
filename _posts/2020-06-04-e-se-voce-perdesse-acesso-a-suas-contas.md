---
layout: post
title: "E se você perdesse acesso a suas contas?"
excerpt: "O que você faria se perdesse acesso a sua conta de e-mail?"
tagline: "O que você faria se perdesse acesso a sua conta de e-mail?"
date: 2020-06-04 08:00:00
categories: Segurança
tags: privacidade e-mail NAS nuvem google
permalink: e-se-voce-perdesse-acesso-a-suas-contas
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: true
  image: /assets/content/gmail-webapp.jpg
  caption: "Photo by Webaroo on [Unsplash](https://unsplash.com)"
---

Você já pensou acordar um dia e não ter mais acesso a sua conta de e-mail?

Num cenário hipotético, supondo que você utilize o Gmail para tudo, o quão desesperado você ficaria se a sua conta não pudesse ser recuperada de forma alguma?

Muitas pessoas irão dizer que provavelmente não seria grande problema, basta criar uma conta nova e seguir a vida, mas isso não é verdade, perder acesso a sua conta de e-mail pode trazer grandes dores de cabeça.

A sua conta de e-mail está vinculada a muitos outros serviços, pense em todas as contas em outros sites o qual você utiliza esse e-mail, pode ser que você perca acesso a vários desses serviços.

Se você utiliza o Gmail, ele está vinculado ao seu dispositivo Android, pode ser que você não consiga mais usar o celular. Você ainda pode estar usando ferramentas como o Google Drive, todas suas fotos estão lá, todos os seus documentos estão lá, você pode perder acesso a tudo de uma hora para outra.

Por que estamos abordando este assunto? Bem, a ideia é alertar dos perigos de usar serviços "Gratuitos", pois em muitos casos você não tem garantia alguma.

Alguém da Google decide desligar serviço X, não se tem muito o que fazer. Você pode dar uma espiada no [Google Graveyard](https://killedbygoogle.com/) para ter uma noção de quantos serviços ou produtos da Google já deixaram de existir.

Outro ponto importante, é que, no caso de um roubo de identidade ou de perda do acesso ao serviço, muitos deles não irão te ajudar muito a recuperar, salvo alguns casos.

A ideia desse artigo não é convencer você a parar de usar os serviços do Google ou algum outro serviço gratuito, nós também usamos vários serviços da Google e vários outros gratuitos, a questão é, tentamos manter um controle em relação à privacidade e backups.

O primeiro passo para não perder acesso as suas contas é habilitar 2FA (ou fator múltiplo de autenticação), onde você além da senha utiliza um [dispositivo OTP](https://pt.wikipedia.org/wiki/Senha_descart%C3%A1vel). Você pode utilizar o seu celular como 2FA ou algo como a [YubiKey](https://www.yubico.com/).

OK, estou seguro agora? Ainda não. 2FA apenas dificulta que outra pessoa se passe por você, diminuindo ou até impossibilitando um roubo de identidade.

Porém, você ainda pode correr riscos caso o serviço deixe de existir, afinal, é um serviço gratuito onde só será oferecido até que produza algum valor para a empresa que está oferecendo.

Nesse caso, quando você paga por um serviço, você possui um contrato, existe um termo de garantia e tudo mais, a empresa irá oferecer o serviço a você até o fim do contrato ou terá algumas regras de cancelamento que te darão segurança.

A primeira dica é, compre um domínio, use esse domínio como seu e-mail principal para tudo o que for importante. Por exemplo, nós do Buteco, temos o e-mail contato@butecopensource.com.br. Esse é nosso e-mail principal, nós que decidimos onde hospedar esse e-mail, pode ser no Gmail, pode ser no Outlook Mail ou em qualquer outra plataforma.

Você não precisa pagar horrores para ter um domínio, é possível ter [domínios com.br](https://registro.br/) por R$ 40 por ano. Eu penso que sua privacidade e segurança vale duas caixinhas de cerveja por ano.

Existem meios de hospedar um e-mail gratuitamente ou em muitos casos, é possível gerenciar isso tudo no seu provedor do domínio.

O [ProtonMail](https://protonmail.com/) é uma opção segura que custa $48 dólares por ano. O ProtonMail é para aqueles que querem privacidade.

A segunda dica é, faça backups, utilize a regra 3-2-1. Sendo, 3 cópias, 2 mídias diferentes de armazenamento e 1 cópia em local diferente.

Minha sugestão, mantenha uma das cópias locais em algum HD portátil, por exemplo, e outra cópia em um ou mais serviços na nuvem (Google Drive, Dropbox, Amazon S3).

Existem opções gratuitas de armazenamento na nuvem, geralmente os limites são em torno de 15 ou 30 GB, o que para alguns pode ser o suficiente.

Os serviços da [Backblaze](https://www.backblaze.com/) são baratos em comparação a outros serviços de backup e trazem uma maior garantia em relação a serviços gratuitos.

A terceira e última dica é que você pode criar uma "nuvem" em casa.

O [My Cloud](https://www.mycloud.com/) da Western Digital é um [NAS](https://pt.wikipedia.org/wiki/Network-attached_storage) com algumas funcionalidades extras e já vem pronto para uso, o lado ruim é ele não ser muito customizável.

Você também pode criar um NAS usando algum hardware antigo ou até uma Raspberry Pi.

Em um NAS customizado você irá provavelmente querer usar o [Nextcloud](https://nextcloud.com/) para ter uma experiência similar ao Dropbox. Além disso, você pode instalar vários outros serviços, como o [Plex](https://www.plex.tv/), para ser sua central multimídia.

A minha sugestão de configuração ideal para uma nuvem local consiste em um NAS em casa (com [RAID](https://pt.wikipedia.org/wiki/RAID)) e backups regulares do NAS para algum [Object Storage](https://en.wikipedia.org/wiki/Object_storage).

Com o NAS na sua rede local você pode acessá-lo facilmente via NFS ou Samba. Com RAID, você garante que se um dos HDs parar de funcionar você ainda tem uma segunda cópia em outro.

Realizando backups regulares do NAS para algum Object Storage você garante uma cópia remota, mesmo que você perca todos os dados do NAS, você ainda tem uma cópia remota.

Espero que tenha gostado das dicas para garantir a segurança de seus dados.

Você usa um e-mail próprio? Você faz backup dos seus dados? Possui um NAS em casa? Deixe um comentário contando a sua experiência.
