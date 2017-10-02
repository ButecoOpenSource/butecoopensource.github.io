---
layout: wordpress
title: Esteganografia com Steghide
date: 2015-10-19 21:29:19
author: daniel_magevski
permalink: /esteganografia-com-steghide/
image: /assets/wp-content/uploads/2015/09/steg-logo.jpg
categories:
  - Ferramentas
tags:
  - segurança
  - steganografia
  - steghide
---

Nesse artigo irei falar um pouco sobre esteganografia e mostrar o uso simples do Steghide.

Esteganografia (do grego "escrita escondida") é o estudo e uso das técnicas para ocultar a existência de uma mensagem dentro de outra, uma forma de segurança por obscurantismo. Em outras palavras, esteganografia é o ramo particular da criptologia que consiste em fazer com que uma forma escrita seja camuflada em outra a fim de mascarar o seu verdadeiro sentido.

<!--more-->

É importante frisar a diferença entre criptografia e esteganografia. Enquanto a primeira oculta o significado da mensagem, a segunda oculta a existência da mensagem.

Um exemplo básico de técnica moderna de esteganografia é a alteração do bit menos significativo de cada pixel de uma imagem colorida de forma a que ele corresponda a um bit da mensagem.

As imagens digitais podem ser classificadas em duas categorias:
<ul>
	<li><strong>Vetoriais:</strong> Constituídas por descrições geométricas em um sistema de coordenadas cartesianas. Sua principal característica é o redimensionamento sem perda de qualidade. O formato mais popular de imagem vetorial é o SVG.</li>
	<li><strong>Bitmap:</strong> Definidas a partir de uma matriz de pontos finitos denominados pixels (a menor unidade que compõe este tipo de imagem). Quanto mais pixels são utilizados para representar uma imagem, melhor é a sua qualidade. Exemplos de formatos de imagem bitmap são PNG, JPEG e GIF. A técnica de esteganografia que será descrita no presente artigo manipula os bits dos tons de cor de cada pixel da imagem, portanto, o tipo de imagem utilizado será o bitmap.</li>
</ul>
Em imagens bitmap, a representação das cores tipicamente se dá no padrão RGB (<em>Red</em>, <em>Green</em>, <em>Blue</em>), sistema de cor que, como o próprio nome indica, utiliza combinações em diferentes níveis destas três cores (vermelho, verde e azul) para compor a gama cores que um pixel pode possuir.

Cada um dos três tons de cor que compõe um pixel é representado por um inteiro de 8 bits, o que proporciona 2 ^ 24 cores possíveis (algo em torno de 16 milhões de cores), com 24 bits por pixel. Alguns formatos de imagem como o PNG e o GIF permitem que se adicione transparência às imagens. Também chamada de camada alfa, no formato PNG a transparência é definida em cada pixel, sendo também representada por 8 bits. Neste caso, o pixel possuirá 32 bits.

Dentre os bits que compõem cada pixel, alguns são modificados durante o processo de esteganografia da imagem, para que passem a armazenar alguns bits do dado embutido. O bit menos significativo, do inglês LSB (<em>Least Significant Bit</em>), é aquele que se encontra mais à direita da cadeia binária, já que quando invertido, o valor inteiro por ele representado sofre a alteração de apenas uma unidade. Este é o bit mais conveniente para o emprego da esteganografia, pois quando modificado produz alterações mínimas nas cores da imagem, praticamente imperceptíveis à visão humana.

A esteganografia LSB consiste em se ocultar os bits da informação a ser embutida nos bits menos significativos de cada um dos três tons que compõe a cor dos pixels. Assim, cada pixel da imagem comporta 3 bits de informação, de onde se calcula a capacidade de "armazenamento" de informação da imagem como 3 vezes o número de pixels que ela possui.

Entretanto, quanto mais bits forem modificados, maiores as chances da técnica ser descoberta, visto que as alterações se tornarão mais perceptíveis aos olhos humanos.

Como os arquivos digitais são representados sob a forma de bits, é possível ocultar qualquer arquivo (documentos de texto, outras imagens, áudio, etc.) em uma imagem utilizando a técnica LSB, desde que respeitada a proporção entre os tamanhos da informação a ser embutida e da imagem.

Vamos testar, para começar instale o Steghide, via <a href="http://steghide.sourceforge.net/download.php" target="_blank">download</a> ou como no meu caso, via gerenciador de pacote, <code>apt-get install steghide</code>, depois disto, verifique os algoritmos de encriptação <code>steghide encinfo</code>.

Principais opções:

<strong>Para encriptar:</strong>
<ul>
	<li>-ef = especifica o nome do arquivo cuja mensagem será inserida.</li>
	<li>-cf = O nome do arquivo que será usado para esconder os dados.</li>
	<li>-sf = O nome para o arquivo esteganografado que será criado. Se não for passado as modificações serão feitas diretamente no arquivo original.</li>
</ul>
<code>steghide embed -ef mensagem.txt -cf imagem.jpg -sf imagem-modificada.jpg</code>

<em>O Steghide permite colocar senha na hora de inserir uma mensagem na imagem.</em>

<strong>Para extrair dados:</strong>
<ul>
	<li>-sf = especifica o arquivo que contém dados escondidos.</li>
	<li>-xf = cria um arquivo com o nome que foi passado e escreve os dados escondidos nele.</li>
</ul>
<code>steghide extract -sf imagem-modificada.jpg -xf mensagem-extraida.txt</code>

A ideia nesse artigo foi mostrar um pouco de esteganografia com Steghide, porém existem diversos programa que fazem isso também.

Fontes:

<a href="http://www.vivaolinux.com.br/artigo/Esteganografia-e-Esteganalise-transmissao-e-deteccao-de-informacoes-ocultas-em-imagens-digitais" target="_blank">Viva o Linux</a>.

Site oficial do <a href="http://steghide.sourceforge.net/" target="_blank">Steghide</a>

Site que peguei a <a href="http://www.hackersonlineclub.com/" target="_blank">Imagem</a>