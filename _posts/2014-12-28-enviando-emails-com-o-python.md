---
layout: wordpress
title: Enviando emails com o Python
date: 2014-12-28 06:00:49
author: alexandrevicenzi
permalink: /enviando-emails-com-o-python/
categories:
  - Desenvolvimento
tags:
  - email
  - python
---

Há alguns dias mostrei como <a href="/2014/12/19/enviando-sms-pelo-pagueveloz/" target="_blank">enviar SMS a partir do Python e outras linguagens</a>. Hoje vou mostrar como enviar emails pelo Python.

O exemplo mostrado usará o módulo <a href="https://docs.python.org/2.7/library/smtplib.html" target="_blank">smtplib</a>.

Vale ressaltar que o exemplo é indicado para envio de email mais simples, para enviar email com formatações especiais e anexos é recomendado o uso do módulo <a href="https://docs.python.org/2.7/library/email.html" target="_blank">email</a>. Abordarei este módulo em uma outra publicação.

O módulo <em>smtplib</em> define um cliente SMTP que pode ser usado para enviar emails tanto via SMTP quanto ESMTP. O <em>smtplib</em> segue os padrões da RFC 821 (SMTP), RFC 1869 (ESMTP), RFC 2554 (Autenticação SMTP) e RFC 2487 (SMTP Seguro via TLS).

Como este módulo já está incluso nas bibliotecas do Python você não precisará instalar nenhuma biblioteca adicional.

Agora que já demos uma boa introdução sobre o módulo <em>smtplib</em> vamos ao que interessa.

Inicialmente vamos importar o módulo:

[python]
import smtplib
[/python]

Vamos criar a instância do SMTP de acordo com a forma de autenticação:

<strong>TLS</strong>

[python]
smtp = smtplib.SMTP('localhost', 587)
smtp.starttls()
[/python]

<strong>SSL</strong>

[python]
smtp = smtplib.SMTP_SSL('localhost', 465)
[/python]

<strong>Sem autenticação</strong>

[python]
smtp = smtplib.SMTP('localhost', 25)
[/python]

Se escolhemos TLS ou SSL devemos fazer a autenticação:

[python]
smtp.login('usuário', 'senha')
[/python]

Caso seja sem autenticação devemos nos identificar enviando o comando EHLO ou HELO:

[python]
# EHLO
smtp.ehlo()

# HELO
smtp.helo()

# De forma genérica. Tenta EHLO primeiro.
smtp.ehlo_or_helo_if_needed()
[/python]

Não há necessidade de chamar os métodos <code>ehlo</code> ou <code>helo</code> quando se utiliza SSL ou TLS, pois o método login faz a chamada desses métodos caso seja necessário.

Enviando um email:

[python]
msg = &amp;quot;&amp;quot;&amp;quot;From: Seu Nome &amp;lt;seuemail@seudominio.com.br&amp;gt;
To: outroemail@seudominio.com.br
Subject: Buteco Open Source

Email de teste do Buteco Open Source&amp;quot;&amp;quot;&amp;quot;

smtp.sendmail('seuemail@seudominio.com.br', ['outroemail@seudominio.com.br'], msg)
[/python]

Note que o segundo parâmetro do método <code>sendmail</code> deve ser uma lista. Mesmo que o destinatário seja apenas um.

Finalizando a sessão SMTP:

[python]
smtp.quit()
[/python]

Agora que já sabemos quais partes usar, vamos colocar tudo em prática em um exemplo. No exemplo vou utilizar o Gmail como servidor SMTP, mas você pode utilizar outro de sua preferência.

Abaixo você pode verificar como enviar usando TLS:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/python-email/email-smtplib-tls.py" type="text/javascript"></script>Já neste outro exemplo você pode verificar como enviar via SSL:<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/python-email/email-smtplib-ssl.py" type="text/javascript"></script>

Confira abaixo uma lista dos servidores de email mais comuns e suas configurações.
<table>
<thead>
<tr class="header">
<th align="left">Nome</th>
<th align="center">Servidor</th>
<th align="center">Autenticação</th>
<th align="center">Porta</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">Gmail</td>
<td align="center">smtp.gmail.com</td>
<td align="center">SSL</td>
<td align="center">465</td>
</tr>
<tr class="even">
<td align="left">Gmail</td>
<td align="center">smtp.gmail.com</td>
<td align="center">StartTLS</td>
<td align="center">587</td>
</tr>
<tr class="odd">
<td align="left">Hotmail</td>
<td align="center">smtp.live.com</td>
<td align="center">SSL</td>
<td align="center">465</td>
</tr>
<tr class="even">
<td align="left">Mail.com</td>
<td align="center">smtp.mail.com</td>
<td align="center">SSL</td>
<td align="center">465</td>
</tr>
<tr class="odd">
<td align="left">Outlook.com</td>
<td align="center">smtp.live.com</td>
<td align="center">StartTLS</td>
<td align="center">587</td>
</tr>
<tr class="even">
<td align="left">Office365.com</td>
<td align="center">smtp.office365.com</td>
<td align="center">StartTLS</td>
<td align="center">587</td>
</tr>
<tr class="odd">
<td align="left">Yahoo Mail</td>
<td align="center">smtp.mail.yahoo.com</td>
<td align="center">SSL</td>
<td align="center">465</td>
</tr>
</tbody>
</table>
Espero que você tenha gostado desta publicação. Continue acompanhando que faremos uma continuação falando sobre o módulo <a href="https://docs.python.org/2.7/library/email.html" target="_blank">email</a>.