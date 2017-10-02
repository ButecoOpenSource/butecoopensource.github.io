---
layout: wordpress
title: Enviando SMS pelo PagueVeloz
date: 2014-12-19 01:04:48
author: alexandrevicenzi
permalink: /enviando-sms-pelo-pagueveloz/
categories:
  - Desenvolvimento
tags:
  - sms
---

É muito comum ver nos sistemas que desenvolvemos envio de e-mail. Mas em alguns setores o envio de SMS facilita muito mais que um e-mail.

Você recebe um e-mail do seu dentista informando que você tem uma consulta na semana que vem? Creio que não. Na maioria desses sistemas é usado envio de SMS e não de e-mail. Enviar um lembrete de um compromisso via SMS é muito mais simples e prático do que um e-mail, afinal, todos estão com seus celulares sempre a mãos.

Hoje vou mostrar como enviar SMS usando a API do <a href="https://www.pagueveloz.com.br/">PagueVeloz</a>, nosso parceiro.

<img class="aligncenter" src="/assets/wp-content/uploads/2014/12/logo-pagueveloz-topo_03.png" alt="PagueVeloz" />

Bem, se você já ouviu falar em serviço de envio de SMS, provavelmente a primeira opção que veio a sua cabeça foi o <a href="https://www.twilio.com/">Twilio</a>. O Twilio oferece outros serviços além do de envio de SMS.

Fazendo uma comparação rápida do envio de SMS do PagueVeloz x Twilio:

<strong>Vantagens</strong>
<ul>
	<li>Preço competitivo</li>
	<li>Serviço nacional</li>
	<li>Suporte em Português</li>
</ul>
<strong>Desvantagens</strong>
<ul>
	<li>Envia apenas para números no Brasil</li>
</ul>

<strong>Usando a API do PagueVeloz</strong>

Praticamente quase todas os serviços do PagueVeloz necessitam de autenticação. O SMS é um deles.
Para usar os serviços você deve se cadastrar no PagueVeloz para receber o seu token de acesso a API. Esse token deverá ser semelhante a:

<code>e45c5687-b0ba-45d4-8337-0fdee61abe93</code>

Para todo o <em>Request</em> que necessita autenticação é obrigatório informar o header Authorization.

<code>Authorization: Basic [CHAVE]</code>

[CHAVE] é o BASE64 do email:token do cliente.

Exemplo de chave:

<code>seuemail@seudominio.com.br:e45c5687-b0ba-45d4-8337-0fdee61abe93</code>

Exemplo após conversão para BASE64:

<code>c2V1ZW1haWxAc2V1ZG9taW5pby5jb20uYnI6ZTQ1YzU2ODctYjBiYS00NWQ0LTgzMzctMGZkZWU2MWFiZTkz</code>

Além desse header o Content-Type é obrigatório para todos os serviços. Vale ressaltar que a API trabalha apenas com o formato JSON.

<code>Content-Type: application/json</code>

Agora que já falamos sobre como se autenticar e enviar o token no <em>Request</em> vamos ver como enviar um SMS.

<strong>Enviando SMS</strong>

O JSON a ser enviado para a API é o seguinte:

<code>
{
    'SeuId': '1234',
    'TelefoneRemetente': '551199887766',
    'TelefoneDestino': '551199887766',
    'Conteudo': 'SMS PagueVeloz',
    'AgendarPara': '2014-12-18T23:16:17.2174313-02:00',
    'Id': 0
}
</code>

<strong>SeuId</strong> é o identificador da mensagem no seu sistema. Opcional.
<strong>TelefoneRemetente</strong> é o número que está enviando. Obrigatório. Deve ser no formato 55 + DDD + NÚMERO.
<strong>TelefoneDestino</strong> é o número que receberá. Obrigatório. Deve ser no formato 55 + DDD + NÚMERO.
<strong>Conteudo</strong> é a mensagem a ser enviada. Obrigatório. No máximo 150 caracteres, de preferência sem acentuação.
<strong>AgendarPara</strong> é a data que será enviado. Opcional. Se não informado será enviado na mesma hora da requisição. Deve estar no formato UTC.
<strong>Id</strong> é o identificador da mensagem no PagueVeloz, sempre zero. Opcional.

O retorno de sucesso é um número. Este número é o identificador da mensagem no PagueVeloz.
Caso o retorno seja de erro, será retornada uma mensagem informando qual o erro.

Veja <a href="https://www.pagueveloz.com.br/help" target="_blank">aqui</a> a documentação completa da API.

Confira abaixo como enviar SMS em várias linguagens de programação.

<strong>C#</strong>

O primeiro exemplo usa os pacotes padrões HTTP do .Net. Já no segundo exemplo são usados pacotes do <a href="http://www.asp.net/web-api" target="_blank">ASP.NET Web API</a>. O primeiro exemplo é ideal para aplicações Desktop, já o segundo para aplicações Web.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/csharp/sms-console.cs" type="text/javascript"></script><script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/csharp/sms-webapi.cs" type="text/javascript"></script>

<strong>C++</strong>

Necessário biblioteca <a href="http://curl.haxx.se/libcurl/" target="_blank">libcURL</a>. Para compilar o arquivo execute o comando:

<code>g++ -o sms.out sms.cpp -lcurl</code>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/cpp/sms.cpp" type="text/javascript"></script>

<strong>Java</strong>

Necessário biblioteca <a href="http://hc.apache.org/httpcomponents-client-ga/" target="_blank">httpcomponents</a>.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/java/sms.java" type="text/javascript"></script>

<strong>Node.JS</strong>

Necessário pacote <a href="http://unirest.io/nodejs.html" target="_blank">unirest</a>. Para instalar execute o comando:

<code>npm install -g unirest</code>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/nodejs/sms.js" type="text/javascript"></script>

<strong>Python</strong>

Necessário módulo <a href="http://unirest.io/python.html" target="_blank">unirest</a>. Para instalar execute o comando:

<code>pip install unirest</code>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/python/sms.py" type="text/javascript"></script>

<strong>Ruby</strong>

Necessário pacote <a href="http://unirest.io/ruby.html" target="_blank">unirest</a>. Para instalar execute o comando:

<code>gem install unirest</code><script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/sms-pagueveloz/ruby/sms.rb" type="text/javascript"></script>

Faltou a sua linguagem de programação? Deixe um comentário que daremos um jeito de disponibilizá-lo para você.