---
layout: wordpress
title: Tutorial GnuPG
excerpt: |
  O GNU Privacy Guard (GnuPG or GPG) é uma alternativa GPL ao aplicativo PGP (Pretty Good Privacy) de criptografia criado pelo Philip Zimmermann. GnuPG é compatível com a RFC 4880, o padrão da IETF (Internet Engineering Task Force), o GnuPG é parte da Free Software Foundation e do projeto de software GNU.
date: 2016-05-31 10:15:33
author: daniel_magevski
permalink: /tutorial-gnupg/
image: /assets/wp-content/uploads/2015/02/GnuPG-Logo.png
categories:
  - Ferramentas
tags:
  - criptografia
  - gnupg
  - pgp
---

<h2>Introdução</h2>
O <a href="http://gnupg.org">GNU</a> Privacy Guard (GnuPG or GPG) é uma alternativa GPL ao aplicativo PGP (Pretty Good Privacy) de criptografia criado pelo Philip Zimmermann. GnuPG é compatível com a <a href="https://tools.ietf.org/html/rfc4880">RFC 4880</a>, o padrão da <a href="https://www.ietf.org/">IETF</a> (Internet Engineering Task Force), o GnuPG é parte da Free Software Foundation e do projeto de software <a href="https://www.gnu.org/">GNU</a>.

Nesse tutorial irei falar sobre a instalação, criação de chaves, como criptografar arquivos e descriptografa-los e gerenciamento de chaves.
<!--more-->

<h2>Instalação</h2>
Para sistemas baseados em debian, execute o comando:<em> </em>

<code>sudo apt-get install gnupg2</code>

Caso esteja em outra distribuição ou sistema operacional (Windows, Mac OS) faça o <a href="https://www.gnupg.org/download/index.html" target="_blank">download aqui</a>.
<h2><strong>O chaveiro digital.</strong></h2>
<strong>OBS: Cada usuário tem o seu chaveiro, se você criar ou importa as chaves como root vai ficar no chaveiro do root.</strong>

Veja as suas chaves

<strong>Públicas</strong>

<code>gpg2 --list-keys</code> ou <code>gpg2 --list-public-keys</code>

<strong>Privadas</strong>

<code>gpg2 --list-secret-keys</code>

Caso o usuário possua mais de uma chave a diferença estará na<strong> <em>ID.</em></strong>

Veja o <strong>fingerprint </strong>das chaves:

<code>gpg2 --fingerprint &lt;nr da chave&gt;</code>

Para gerar suas chaves:

<code>gpg2 --gen-key</code>

Escolha a opção <strong>(1) RSA and RSA (default)</strong>. Essa opção irá criar chaves assimetricas (Pública e Privada), veja mais em <a href="https://pt.wikipedia.org/wiki/Criptografia_de_chave_p%C3%BAblica">criptografia de chave pública</a>.
Coloque uma senha "passphrase" segura, escolha o tamanho da chave e a validade dela (não recomendavél utilizar a opção de nunca expirar), as outras informações sao básicas, nome e e-mail.

Agora vamos exportar sua chave localmente, primeira a pública:

<code>gpg2 -a --export &lt;nr_da_chave&gt; &gt; public.asc</code>

Agora a chave privada (não passe essa chave a ninguem, exporte-a para backup):

<code>gpg2 -a --export-secret-keys &lt;nr_da_chave&gt; &gt; secret.asc</code>

Para importa uma chave para o seu chaveiro use:

<code>gpg2 --import &lt;arquivo_da_chave&gt;</code>

<strong>Válido para chaves públicas e privadas.</strong>

Para remover uma chave pública:

<code>gpg2 --delete-keys &lt;nr da chave&gt;</code>

Para remover uma chave privada do chaveiro:

<code>gpg2 --delete-secret-keys &lt;nr da chave&gt;</code>

Caso queira editar alguma coisa na chave (Nome, E-mail, Foto e etc.) chave use:

<code>gpg2 --edit-key &lt;nr da chave&gt;</code>
<h2>Criptografar e descriptografar arquivos</h2>
Com as <a href="https://pt.wikipedia.org/wiki/Criptografia_de_chave_p%C3%BAblica">chaves assimétricas</a> o modo será o da imagem a baixo.
<a href="/assets/wp-content/uploads/2016/04/GnuPG-img2.png"><img class="wp-image-5234 aligncenter" src="/assets/wp-content/uploads/2016/04/GnuPG-img2-288x300.png" alt="GnuPG-img2" width="326" height="339" />
</a>
Para criptografar um arquivo:

<code>gpg2 -r fulano@domínio.net -e mensagem.txt</code>

Para descriptografar um arquivo que a pessoa tenha criptografado usando a sua chave:

<code>gpg2 -d mensagem.txt.gpg</code>

<strong>OBS: O arquivo criptografado fica no formato .pgp<em>.</em></strong>
<h2>Servidor de chave</h2>
Os servidores de chaves são muito úteis para disponilizar, importar ou atualizar chaves públicas.

Para enviar uma chave para o servidor:

<code>gpg2 --keyserver keys.gnupg.net--send-key &lt;nr_da_chave&gt;</code>

Para importar uma chave do servidor:

<code>gpg2 --keyserver keys.gnupg.net --recv-key &lt;nr da chave&gt;</code>

Para pesquisar uma chave no servidor:

<code>gpg2 --keyserver keys.gnupg.net --search-keys &lt;nome ou e-mail&gt;</code>

Para atualizar as chaves do seu chaveiros vamos fazer um procura no servido de chaves:

<code>gpg2 --refresh-keys --keyserver keys.gnupg.net</code>

Exitem outros servidores de chaves, usei este como exemplo, os servidores atualizam as chaves entre si.
<h2>Revogação de chave</h2>
Em caso de perda de chave por qualquer motivo você pode invalidar a sua chave, para que outras pessoas saberem que a sua chave não é mais confiável. Ela não será excluida somente será invalidada.

Primeiro vamos gerar esse certificado de revogação:

<code>gpg2 -o rev-cert --gen-revoke &lt;nr da chave&gt;</code>

Pronto, com o certificado de revogação gerado devemos guarda-lo em um local seguro ou passar para uma pessoa de confiança, caso você não poder regova-lá por qualquer motivo, a pessoa fará . (Qualquer pessoa poderá invalidar sua chave caso esteja com o certificado, mas não criptografar ou assinar).

Para revogar uma chave é preciso importa o certificado e depois enviá-lo para um servidor de chaves:

<code>gpg --import rev-cert</code>

Agora para revoga-lá:

<code>gpg --keyserver keys.gnupg.net --send-keys &lt;nr da chave&gt;</code>
<h2>Utilizando interface</h2>
Existem vários programas que você pode gerenciar suas chaves, o que eu utilizo atualmente é o <a href="https://www.enigmail.net" target="_blank">Enignmail</a>, um add-on do <a href="https://www.mozilla.org/pt-BR/thunderbird/" target="_blank">Thunderbird</a>, os conceitos apresentados acima serão uteis na sua utilização. Para ver outras interface do GPG acesse a página do <a href="https://www.gnupg.org/related_software/frontends.html" target="_blank">gnupg</a>.

Em outra oportunidade irei falar sobre assinaturas com as chaves.
<h2>Referências:</h2>
<a href="https://gnupg.org/" target="_blank">GnuPG</a>, <a href="https://tools.ietf.org/html/rfc4880">RFC4880</a>, <a href="https://pt.wikipedia.org/wiki/Criptografia_de_chave_p%C3%BAblica">Criptografia de chave pública</a>