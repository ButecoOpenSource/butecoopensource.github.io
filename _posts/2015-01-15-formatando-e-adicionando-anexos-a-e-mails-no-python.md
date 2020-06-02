---
layout: wordpress
title: Formatando e adicionando anexos a e-mails no Python
date: 2015-01-15 06:00:19
author: alexandrevicenzi
permalink: /formatando-e-adicionando-anexos-a-e-mails-no-python/
image: /assets/wp-content/uploads/2014/12/python-logo.png
categories:
  - Desenvolvimento
tags:
  - email
  - python
  - smtplib
---

Há algumas semanas, nós mostramos <a href="/enviando-emails-com-o-python" target="_blank">como enviar e-mail pelo Python</a> usando o módulo <a href="https://docs.python.org/2.7/library/smtplib.html" target="_blank">smtplib</a>. Hoje iremos dar continuidade ao envio de e-mail, desta vez focaremos em sua formatação e adição de arquivos anexos.

Para fazer este serviço iremos utilizar o módulo <a href="https://docs.python.org/2.7/library/email.html" target="_blank">email</a>. Este módulo é uma biblioteca para manipulação de mensagens de email e outros documentos do tipo MIME. Como este módulo já está incluso nas bibliotecas do Python você não precisará instalar nenhuma biblioteca adicional.

<strong>Submódulos</strong>

Antes de iniciar, vamos ver os submódulos do módulo email que iremos utilizar:

<pre><code>from email import encoders</code></pre>

Útil para quando criamos um payload que não seja um já implementado. Neste caso necessitamos codificar a mensagem.

<pre><code>from email.mime.base import MIMEBase</code></pre>

Classe base para quando desejamos enviar um arquivo não suportado pelas classes já disponíveis. Um exemplo é o envio de aquivos de vídeos.

<pre><code>from email.mime.multipart import MIMEMultipart</code></pre>

Usado para criar uma mensagem MIME multpart.

<pre><code>from email.mime.audio import MIMEAudio</code></pre>

Usado para criar objetos MIME para a maior parte de aquivos de áudio.

<pre><code>from email.mime.image import MIMEImage</code></pre>

Usado para criar objetos MIME para a maior parte de aquivos de imagem.

<pre><code>from email.mime.text import MIMEText</code></pre>

Usado para criar objetos MIME para a maior parte de aquivos de texto.

<strong>Usando os submódulos</strong>

Agora vamos verificar como criar uma mensagem com cada um desses tipos:

<strong>MIMEBase</strong>

```py
with open('arquivo.zip', 'rb') as f:
  mime = MIMEBase('application', 'zip')
  mime.set_payload(f.read())

encoders.encode_base64(mime)
```

<strong>MIMEMultipart</strong>

```py
msg = MIMEMultipart()
msg.attach(arquivo_mime_1)
msg.attach(arquivo_mime_2)
```

arquivo_mime deve ser outro subtipo MIME, por exemplo MIMEAudio.

<strong>MIMEAudio</strong>

```py
with open('audio.ogg', 'rb') as f:
  mime = MIMEAudio(f.read(), _subtype='ogg')
```

<strong>MIMEImage</strong>

```py
with open('imagem.png', 'rb') as f:
  mime = MIMEImage(f.read(), _subtype='png')
```

<strong>MIMEText</strong>

```py
with open('pagina.html') as f:
  mime = MIMEText(f.read(), _subtype='html')
```

Adicionando os dados de envio e recebimento no cabeçalho da mensagem:

```py
msg = MIMEText('Exemplo.', 'plain')
msg['From'] = 'seuemail@seudominio.com'
msg['To'] = ', '.join(['outroemail@seudominio.com'])
msg['Cc'] = ', '.join(['emailemcopia@seudominio.com'])
msg['Bcc'] = ', '.join(['emailocultol@seudominio.com'])
msg['Reply-To'] = ', '.join(['seuemail@seudominio.com'])
msg['Subject'] = 'Assunto'
```

<ul>
    <li>O <em>From</em> indica quem está enviando mensagem.</li>
    <li>O <em>To</em> indica quem irá receber.</li>
    <li>O <em>Cc</em> indica quem receberá uma cópia deste email.</li>
    <li>O <em>Bcc</em> também indica quem receberá uma cópia do email, mas as demais pessoas não irão ver o email dele na lista dos enviados.</li>
    <li>O <em>Reply-To</em> indica para quem será respondido o email.</li>
    <li>O <em>Subject</em> é o assunto do email.</li>
</ul>

Para enviar os objetos MIME via SMTP devemos gerar as mensagens no formato <em>raw</em>, para isto utilizamos o método <em>as_string</em>.

<strong>Exemplos</strong>

Agora que já possuímos uma noção básica do funcionamento do módulo email, vamos criar um exemplo completo utilizando tudo o que foi visto.

O exemplo abaixo exemplifica o envio de um email HTML:

```py
import smtplib
from email.mime.text import MIMEText

de = 'seumail@gmail.com'
para = ['outroemail@gmail.com']

msg = MIMEText('Exemplo de email HTML do &lt;b&gt;Buteco Open Source&lt;b/&gt;.', 'html', 'utf-8')
msg['From'] = de
msg['To'] = ', '.join(para)
msg['Subject'] = 'Buteco Open Source'

raw = msg.as_string()

smtp = smtplib.SMTP_SSL('smtp.gmail.com', 465)
smtp.login('seumail@gmail.com', 'suasenha')
smtp.sendmail(de, para, raw)
smtp.quit()
```

O exemplo abaixo exemplifica o envio de um email HTML com anexo:

```py
import mimetypes
import os
import smtplib

from email import encoders
from email.mime.audio import MIMEAudio
from email.mime.base import MIMEBase
from email.mime.image import MIMEImage
from email.mime.multipart import MIMEMultipart
from email.mime.text import MIMEText

def adiciona_anexo(msg, filename):
    if not os.path.isfile(filename):
        return

    ctype, encoding = mimetypes.guess_type(filename)

    if ctype is None or encoding is not None:
        ctype = 'application/octet-stream'

    maintype, subtype = ctype.split('/', 1)

    if maintype == 'text':
        with open(filename) as f:
            mime = MIMEText(f.read(), _subtype=subtype)
    elif maintype == 'image':
        with open(filename, 'rb') as f:
            mime = MIMEImage(f.read(), _subtype=subtype)
    elif maintype == 'audio':
        with open(filename, 'rb') as f:
            mime = MIMEAudio(f.read(), _subtype=subtype)
    else:
        with open(filename, 'rb') as f:
            mime = MIMEBase(maintype, subtype)
            mime.set_payload(f.read())

        encoders.encode_base64(mime)

    mime.add_header('Content-Disposition', 'attachment', filename=filename)
    msg.attach(mime)

de = 'seumail@gmail.com'
para = ['outroemail@gmail.com']

msg = MIMEMultipart()
msg['From'] = de
msg['To'] = ', '.join(para)
msg['Subject'] = 'Buteco Open Source'

# Corpo da mensagem
msg.attach(MIMEText('Exemplo de email HTML com anexo do &lt;b&gt;Buteco Open Source&lt;b/&gt;.', 'html', 'utf-8'))

# Arquivos anexos.
adiciona_anexo(msg, 'texto.txt')
adiciona_anexo(msg, 'imagem.jpg')

raw = msg.as_string()

smtp = smtplib.SMTP_SSL('smtp.gmail.com', 465)
smtp.login('seumail@gmail.com', 'suasenha')
smtp.sendmail(de, para, raw)
smtp.quit()
```

Comparando este tutoria ao anterior, a montagem e o envio de um email ficam bem mais simplificados com esta biblioteca para manipulação de email, não é?

Espero que você tenha gostado. Não deixe de assinar nosso feed.

<em>Parte deste código foi obtido na <a href="https://docs.python.org/2/library/email-examples.html" target="_blank">documentação do módulo email</a>.</em>
