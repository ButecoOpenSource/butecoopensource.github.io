---
layout: post
title: "Entendendo carros autônomos"
excerpt: "Carros autônomos estão cada vez mais presentes em nossas vidas, mas o que é um carro autônomo de fato?"
tagline: "Carros autônomos estão cada vez mais presentes em nossas vidas, mas o que é um carro autônomo de fato?"
date: 2020-05-28 08:00:00
categories: Hardware
tags: nvidia carros sensores hardware
permalink: entendendo-carros-autonomos
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: true
  image: /assets/content/tesla-autopilot.jpg
---

Um carro autônomo é um carro capaz de identificar o ambiente ao seu redor e trafegar em segurança com nenhuma ou pouca iteração humana, combinando uma variedade de sensores para perceber o ambiente ao seu redor, dentre eles, podemos citar o uso de GPS, Lidar, Radar, Sonar e câmeras.

Além disso, existem vários outros sensores para monitorar o próprio carro, como sensores de velocidade, freios, RPM, combustível e demais sensores que estamos acostumados e que podem ser acessados em muitos carros atuais através do protocolo [ODB2](https://pt.wikipedia.org/wiki/OBD){:target="_blank"}.

Carros autônomos não são feitos só de sensores, na verdade, sensores são apenas uma parte, ainda precisamos de um sistema de controle, como um sistema operacional, capaz de interpretar os dados coletados por diversos sensores e navegar o veículo de forma segura.

Atualmente, não existem carros 100% autônomos em circulação, porém existem carros e caminhões semi autônomos em uso.

Os freios de emergência ou EBA (Emergency brake assist) populares em caminhões, é um sistema semi autônomo capaz de parar um veículo em situações de risco onde o motorista não teve um tempo de resposta adequado ou não reagiu. EBA consiste em uma combinação de radares e câmeras instaladas na frente do caminhão. Essa tecnologia já salvou muitas vidas.

Outro exemplo de sistema semi autônomo é o [Autopilot (piloto automático)](https://www.tesla.com/autopilot){:target="_blank"} dos carros da Tesla. O piloto automático é capaz de acelerar, frear e controlar o volante dentro de uma pista, porém esse é um sistema assistido, onde é necessário o condutor estar atento e com as mãos no volante. A Tesla inclui várias câmeras no carro, além de outros sensores e radares para que o piloto automático funcione.

Os carros da Tesla tecnicamente possuem todo o *hardware* necessário para que o carro seja totalmente autônomo, onde ele seja capaz de ir de um ponto a outro sem interação humana, curta ou longa distância, porém, essa funcionalidade não está disponível devido a regulamentações e a própria confiança nesses sistemas.

<p>
  <iframe title="vimeo-player" src="https://player.vimeo.com/video/192179726" width="640" height="360" frameborder="0" allowfullscreen></iframe>
</p>

No exemplo acima é possível observar o Tesla Autopilot em ação, porém ainda são necessárias muitas horas e quilômetros de estrada para chegarmos a um ponto onde seja possível confiar nesses sistemas e haver mudanças na legislação.

## O desafio da DARPA

<p style="text-align: center;">
  <img src="/assets/content/darpa-challenge.jpg" alt="DARPA Grand Challenge 2005" style="display: block; max-width: 400px; margin: auto;">
  <em><a href="https://archive.darpa.mil/grandchallenge05/awardphotogallery.html" target="_blank">Fonte</a></em>
</p>

O [DARPA Grand Challenge](https://en.wikipedia.org/wiki/DARPA_Grand_Challenge){:target="_blank"} é uma competição americana de veículos autônomos.

Podemos dizer que o desafio DARPA foi um dos grandes propulsores em relação a veículos autônomos.

A primeira competição foi em 2004, porém nenhum dos veículos autônomos conseguiu chegar ao final da competição.

Em 2005, 5 veículos chegaram ao final da competição. O destaque foi para o veículo [Stanley](https://en.wikipedia.org/wiki/Stanley_(vehicle)){:target="_blank"}, da Universidade de Stanford, que chegou em primeiro lugar.

Você pode assistir ao episódio [The Great Robot Race](https://www.pbs.org/wgbh/nova/darpa/){:target="_blank"} da série Nova do canal PBS para mais detalhes sobre o desafio DARPA. Infelizmente não podemos vincular o vídeo aqui devido a direitos autorais.

## Níveis de automação

Quando falamos em veículos autônomos precisamos mencionar os 6 níveis de automação (numa escala de 0 a 5), pois cada um desses níveis descreve um modelo de autonomia.

* Nível 0 - O sistema autônomo emite alertas, mas ele não possui controle sobre o veículo.
* Nível 1 - O condutor e o sistema autônomo compartilham o controle do veículo. Exemplos são controle de bordo, assistente de estacionamento e freios de emergência.
* Nível 2 - O sistema autônomo tem total controle sobre o veículo, porém, é necessário ter condutor para monitorar e tomar o controle caso necessário. Um exemplo é o Tesla Autopilot.
* Nível 3 - O sistema autônomo tem total controle sobre o veículo, o condutor pode desviar a atenção, assistir um filme, por exemplo, porém,  o condutor ainda pode ter de tomar o controle por um tempo limitado.
* Nível 4 - Similar ao nível 3, porém, sem necessidade do condutor tomar o controle. O condutor pode dormir durante a viagem. Ainda é possível tomar controle do veículo em raros casos.
* Nível 5 - Sem iteração humana, o veículo não precisa de volante e não é possível tomar controle manualmente do veículo.

## Quem está pesquisando?

A Tesla é apenas uma das empresas fazendo pesquisas e testes. Talvez a mais conhecida, pois os carros estão a venda e é possível encontrar facilmente carros Tesla nas ruas dos Estados Unidos.

A [Waymo](https://waymo.com){:target="_blank"} iniciou como um projeto dentro do Google e hoje trabalha com carros e caminhões autônomos. Uma das grandes diferenças é que a Waymo inclui um [Lidar](https://waymo.com/lidar/){:target="_blank"} em seus veículos, a Tesla, não.

Ainda podemos citar que todas as grandes fabricantes de veículos possuem algum programa similar, além de empresas como [Uber](https://www.uber.com/us/en/atg/technology/){:target="_blank"} e [Lyft](https://self-driving.lyft.com/){:target="_blank"}.

Provavelmente você deve pensar que a NVDIA faz apenas GPU certo? Errado. A NVIDIA não só possui a sua própria frota de carros autônomos, ela é uma das líderes no quesito. A [NVIDIA DRIVE AGX](https://www.nvidia.com/en-us/self-driving-cars/drive-platform/hardware/){:target="_blank"} é um supercomputador embarcado capaz de processar dados de câmeras, radares e sensores lidar e navegar um veículo de uma forma segura.

## O que muda em nossas vidas?

A proposta por trás de veículos autônomos é vasta, mas alguns pontos possuem uma maior relevância.

No atual momento existem veículos com nível 2 de automação em circulação, nesse nível já podemos assegurar de que muitas vidas já foram salvas, como podemos conferir [aqui](https://www.mirror.co.uk/news/uk-news/tesla-autopilot-saves-familys-life-21512255){:target="_blank"}. Com o nível 4, a tendência é proporcionar uma segurança ainda maior, reduzindo os acidentes fatais drasticamente.

Com uma automação maior significa que não haverá tanta interferência em tráfego, ou seja, menos congestionamentos. Isso tende a causar menos estresse e reduzir o tempo de deslocamento.

Com uma frota totalmente autônoma, pode ser que você não precise mais ter um carro, você pode abrir uma *App*, chamar um carro e ir para aonde quiser. Consequentemente você terá menos gastos e teremos menos veículos em circulação e produção, poupando o nosso planeta.

## Conclusão

Veículos com nível 2 de automação já está em circulação e é uma questão de poucos anos até termos veículos com nível 4 em circulação.

Certamente, veículos autônomos são um tema um tanto quanto polêmico, ainda necessitamos nos adaptar a ideia de carros sem motoristas, mas as pessoas estão começando a perceber as vantagens, é uma questão de tempo até termos adoção em massa.

Este é apenas o primeiro artigo relacionados a carros autônomos, fique ligado que em breve traremos mais detalhes.

Deixe seu comentário, poderemos tirar suas dúvidas num próximo artigo.
