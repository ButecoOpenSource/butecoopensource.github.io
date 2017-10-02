---
layout: wordpress
title: cURL 7.40 disponível e agora com suporte ao protocolo SMB/CIFS
date: 2015-01-08 18:21:55
author: alexandrevicenzi
permalink: /curl-7-40-disponivel-e-agora-com-suporte-ao-protocolo-smbcifs/
image: /assets/wp-content/uploads/2015/01/ds-libcurl.jpg
categories:
  - Desenvolvimento
  - Notícias
tags:
  - curl
  - libcurl
---

O cURL 7.40 foi disponibilizado hoje (08/01) com várias novidades e correções de bugs. Para quem não o conhece ainda, o cURL é um aplicativo e biblioteca para download pelos mais variados tipos de protocolos.

<strong>Novidades</strong>
<ul>
	<li>Adicionado suporte para autenticação Windows SSPI</li>
	<li>Adicionado o Kerberos V5 a lista de funcionalidades suportadas</li>
	<li>Adicionado targets para o WinIDN (Makefile)</li>
	<li>Adicionado targets de compilação para o VS2012+</li>
	<li>Adicionado formato PEM as chaves públicas fixas do SSL</li>
	<li>Adicionado suporte a conversão de novas linhas em formato Unix durante o envio de e-mail</li>
	<li>Adicionado suporte inicial ao protocolo SMB/CIFS</li>
	<li>Adicionado suporte para HTTP para sockets em domínios Unix, via CURLOPT_UNIX_SOCKET_PATH e --unix-socket</li>
	<li>Adicionado suporte para GSS-API (autenticação Kerberos V5)</li>
</ul>
Confira a lista completa das alterações <a href="http://curl.haxx.se/changes.html#7_40_0" target="_blank">aqui</a>.