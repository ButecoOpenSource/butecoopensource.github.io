---
layout: wordpress
title: Apigility, Web Service com Zend Framework
date: 2014-10-02 08:33:20
author: jaswdr
permalink: /apigility-web-service-com-zend-framework/
categories:
  - Ferramentas
tags:
  - apigility
  - php
  - zend
---

Com a variedade de clientes que acessam nossas aplicações hoje fica cada vez mais difícil criar algo que atenda a todos. Pensando nisso a Zend, a mesma criadora do Zend Framework, (sério!?!) e do PHP, criou o Apigility, uma ferramenta para você criar serviços de maneira fácil e com qualidade. Vamos a instalação!

1 - Faça o <a href="https://apigility.org/img/download_zip.png">Download</a> dos arquivos

2 - Descompacte

3 - Execute o comando
<pre><code class="bash">php -S 0.0.0.0:8888 -t public public/index.php
</code></pre>
Pronto! agora acesse <a href="http://localhost:8888">http://localhost:8888</a>

Você deve ver algo como a imagem abaixo:
<a href="http://imageshack.com/f/iqaT2jKnp" target="_blank"><img src="http://imagizer.imageshack.us/v2/280x200q90/674/aT2jKn.png" alt="" border="0" /></a>

Como exemplo vamos criar um simples serviço de helloWorld:

1 -  Vá para "Get Started" =&gt; "Apis" =&gt; "Create New API"

2 - Vamos colocar o nome de "HelloWorld"

3 - Clique no link da API que criamos, nesse caso "HelloWorld"

4 - Vá para "RPC Services" =&gt; "Create New RPC Service"

5 - Service name = "hello" e Route = "/hello"

6 - Aguarde o Apigility executar e clique em "Fields"

7 - Coloque o mouse sobre a barra azul e clique no botão editar

8 - No campo "Field Name" digite "message" e clique em "Save changes"

9 -  Vá na aba "Documentation" e em "Description" coloque "HelloWorld message sample service"

10 - Clique em "Generate from configuration"

11 - Vá para a aba "Source Code"

12 - Clique no link "HelloWorldV1RpcHelloHelloController" e abrirá um modal com alguns dados

Esse é o arquivo gerado pelo Apigility, vá para o diretório em que você descompactou os arquivos anteriormente e vá para o caminho "moduleHelloWorldsrcHelloWorldV1RpcHello" e abra o arquivo "HelloController.php"

Este é o arquivo que fará o retorno para o cliente, ele deve estar aparecendo como:

<pre><code class="php">
namespace HelloWorldV1RpcHello;
use ZendMvcControllerAbstractActionController;
class HelloController extends AbstractActionController
{
  public function helloAction()
  {
  }
}
</code></pre>

Dentro do método "helloAction" coloque o seguinte código para retorno:

<pre><code class="php">
  return array('message', 'Hello World from Apigility!');
</code></pre>

Agora acesse http://localhost:8888/hello e PRONTO!!! o texto abaixo deve aparecer:

{"message":"Hello World from Apigility!"}

<a href="https://apigility.org/">Site oficial do Apigility</a>

Acesse nosso <a href="https://github.com/ButecoOpenSource/">Git</a>

Não esqueça de comentar! :)