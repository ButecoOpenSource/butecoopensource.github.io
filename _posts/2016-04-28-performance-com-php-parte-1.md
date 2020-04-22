---
layout: wordpress
title: PHP e Performance, parte 1
excerpt: |
  Performance é algo com que todos temos que lidar, afinal temos recursos de hardware limitados a nossa disposição, veja nesaa série algumas dicas de como melhorar a performance no PHP.
date: 2016-04-28 12:30:31
author: jaswdr
permalink: /performance-com-php-parte-1/
image: /assets/wp-content/uploads/2016/04/phplogo-highres.png
categories:
  - Desenvolvimento
tags:
  - performance
  - php
---

<p style="text-align: left;">Algo que alguns criticam no PHP é questão de performance, sempre digo que PHP é uma linguagem performática para o que ele se propõe a fazer. Contudo, performance não é algo simples, existem centenas de milhares de fatores que podem interferir, começando pelo hardware usado até a alocação desnecessária de variáveis.</p>
<!--more-->Pesquisando um pouco sobre, decidi fazer uma série de artigos falando sobre performance no PHP, dando algumas dicas de melhorias que todos podem adotar. Veja abaixo a primeira delas, o uso da função <em>unset() </em>para desalocar memória.
<h3 id="unset">unset()</h3>
Para entender melhor o problema considere o seguinte código abaixo:
<pre><code>echo "Quantidade de memória usada antes " . memory_get_usage() . PHP_EOL;
$arr = array();
for ($i = 0; $i &lt; 1000000; ++$i) {
  $arr[] = rand();
}
echo "Quantidade de memória usada depois " . memory_get_usage() . PHP_EOL;
</code></pre>
Executando este programa algo como o texto abaixo deve ser mostrado:
<pre><code>Quantidade de memória usada antes 232888
Quantidade de memória usada depois 233368
</code></pre>
Claro que os valores serão diferentes para cada ambiente, porém, nesse caso, a diferença de uso de memória é de <strong>480 bytes</strong>, contudo podemos melhorar o uso de memória colocando manualmente a chamada da função “unset()”, veja:
<pre><code>echo "Quantidade de memória usada antes " . memory_get_usage() . PHP_EOL;
$arr = array();
for ($i = 0; $i &lt; 1000000; ++$i) {
  $arr[] = rand();
}
unset($arr); // &lt;- chamando unset()
echo "Quantidade de memória usada depois " . memory_get_usage() . PHP_EOL;
</code></pre>
No caso dessa execução os valores foram os seguintes:
<pre><code>Quantidade de memória usada antes 232936
Quantidade de memória usada depois 233256
</code></pre>
A diferença agora foi de <strong>320 bytes</strong>, o que significa um uso de <strong>33,3% a menos de memória</strong>, um ganho considerável com uma alteração simples.

Em linguagens que possuem um sistema de coleta de lixo ou do inglês <em>“Garbage Collector”,</em> existem pontos chaves durante a execução que executarão o coletor de lixo, no PHP isso acontece em três momentos, ao chamar a função <em>“unset()”,</em> ao final da execução de uma função e ao final da execução do programa. O tempo de execução é o mesmo nos três casos, pois todos chamam a função <em>“unset()”</em>, porém existe a vantagem que ao chamar manualmente você conseguirá liberar memória no meio da execução, diferente das outras alternativas.

Bom pessoal, essa dica foi rápida e simples, não há contra indicação, por fim, deixando um último ponto, a performance não deveria ser sua única e principal prioridade, deve ser levada em conta, porém, muito mais vale um código legível, funcional e de fácil manutenção do que um código totalmente performático. Até a próxima.