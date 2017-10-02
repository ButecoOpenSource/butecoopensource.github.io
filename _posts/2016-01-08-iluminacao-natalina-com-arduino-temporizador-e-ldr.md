---
layout: wordpress
title: Iluminação Natalina com Arduino, Temporizador e LDR
excerpt: |
  Este post mostra como controlar luzes natalinas com um Arduino
date: 2016-01-08 10:26:04
author: brunopiske
permalink: /iluminacao-natalina-com-arduino-temporizador-e-ldr/
categories:
  - Hardware / DIY
tags:
  - arduino
  - c
  - natal
  - programação
---

<span style="font-weight: 400;">Neste projeto, irei apresentar a vocês como controlar uma carga de 110 ou 220 volts com um Arduíno e um relé. Utilizaremos também um LDR para medição de intensidade de luz, para poder fazer com que a carga seja ligada apenas quando for escuro, e além disso, com a opção de temporizar o tempo que a carga ficará ligada. Um exemplo de aplicação é a iluminação Natalina, fazendo ela ligar somente quando escurecer, e caso quiser, pode-se também programar essa para desligar após algumas horas, ou ainda, deixar com que ela se apague novamente quando o dia clarear.</span>

<!--more-->

<span style="font-weight: 400;">Utilizaremos para este projeto:</span>
<ul>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Arduíno Mega 2560 (ou qualquer outro Arduíno)</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Relé 5VDC 15A 125VAC</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 LDR</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Transistor BC548</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Led</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Resistor de 470 Ohms</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Resistor de 10K Ohms</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Resistor de 1K5 Ohms</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">1 Diodo 1N4007</span></li>
	<li style="font-weight: 400;"><span style="font-weight: 400;">Outros (Adaptador de tomada, extensão e fonte 5V para o Arduíno) </span></li>
</ul>
<span style="font-weight: 400;">Segue esquema elétrico:</span>

<a href="/assets/wp-content/uploads/2015/12/Esquema-Eletrico.png" rel="attachment wp-att-4339"><img class="alignnone size-full wp-image-4339" src="/assets/wp-content/uploads/2015/12/Esquema-Eletrico.png" alt="Esquema Eletrico" width="919" height="582" /></a>

<span style="font-weight: 400;">Para o sensor LDR utilizaremos o pino A0 da entrada analógica, e para acionamento do relé o Pin 2 (no esquema porta 4).</span>

<span style="font-weight: 400;">Como a corrente necessária para atracar o relé é muito maior do que a fornecida pelo Arduíno, precisamos utilizar um transistor, um BC548.</span>

<span style="font-weight: 400;">A configuração de tempo e intensidade de luz para ligar/desligar o relé é ajustável pelo código fonte através das variáveis </span><b>medio</b><span style="font-weight: 400;"> e </span><b>temp</b><span style="font-weight: 400;">.</span>

<b>medio</b><span style="font-weight: 400;"> = é o valor médio de luz que faz o relé ligar ou desligar.</span>

<b>temp </b><span style="font-weight: 400;">= é o tempo que o relé ficará ligado após o acionamento. Se este valor for 0 ele nunca liga, se estiver em -1 ele só irá desligar quando valor do LDR for maior que o valor médio estipulado na variável anterior.</span>

<span style="font-weight: 400;">Veja o código fonte a seguir:</span>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_arduino/Arduino_TemporizadorLDR.ino" type="text/javascript"></script>

<span style="font-weight: 400;">Após compilar o projeto e gravar no Arduíno, basta diminuir a intensidade de luz sobre o LDR que o relé será acionado, ligando assim sua carga. Caso o valor de <strong>temp</strong> for definido com algum valor acima de 0, ele irá contar esse tempo em segundos, e depois desligar o relé, acionando somente quando a intensidade de luz for menor que o valor médio definido.</span>
<span style="font-weight: 400;">Espero que tenham gostado deste pequeno projeto, até mais!</span>