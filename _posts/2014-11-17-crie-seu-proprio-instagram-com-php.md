---
layout: wordpress
title: Crie seu próprio Instagram com PHP
date: 2014-11-17 07:47:00
author: jonathanaschweder
permalink: /crie-seu-proprio-instagram-com-php/
categories:
  - Desenvolvimento
tags:
  - imagem
  - php
  - php_gd2
---

<div class="separator" style="clear: both; text-align: left;">Olá pessoal! Hoje mostrarei como fazer uma edição e tratamento básico de imagens com PHP, para quem não sabe o PHP possui uma extensão dedicada para trabalhar com entidades gráficas, a <strong>php_gd2</strong>, consequentemente para este tutorial vamos precisar desta extensão habilitada e do PHP na versão 5.5 ou superior.</div>
<div class="separator" style="clear: both; text-align: left;"></div>
<div class="separator" style="clear: both; text-align: left;">Para começar então precisamos carregar a imagem, isto é algo extremamente fácil de fazer usando a extensão do php_gd2 e existe métodos prontos para isso:</div>
<pre><code>$imagem = imagecreatefromjpeg($caminho_para_imagem);</code></pre>

Ou se preferir usar outras extensões de imagens utilize a tabela abaixo:
<pre>(JPEG)$imagem = imagecreatefromjpeg('caminhoparaimagem');
(PNG) $imagem = imagecreatefrompng('caminhoparaimagem');
(GIF) $imagem = imagecreatefromgif('caminhoparaimagem');
(WEBP)$imagem = imagecreatefromwebp('caminhoparaimagem');</pre>
Isso carrega nossa imagem na variável "$imagem", para teste você pode jogar a imagem no navegador da seguinte forma:
<pre>header('Content-type: image/jpeg');
imagejpeg($imagem);
</pre>
IMPORTANTE! É necessário colocar o "Content-type" pois do contrário o navegador não interpretará corretamente o conteúdo e ele pode ou não ser mostrado como deve, além disso deve corresponder ao tipo de imagem usada.

Obs.: Você pode salvar a imagem gerada passando um segundo parâmetro para o método imagejpeg() com o caminho e nome da imagem. Ex.: imagepng($imagem,'imagem2.jpg');

Para este tutorial usarei uma imagem de um elePHPant que achei no google :)

Com isso ao acessar a página pelo navegador a imagem deve aparecer, mas agora vamos tornar as coisas mais interessantes, aplicando filtros às imagens com o método <b><a href="http://php.net/manual/en/function.imagefilter.php">imagefilter</a></b>, veja abaixo alguns filtros:

&nbsp;
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://1.bp.blogspot.com/-RkFLv7jTiXM/VGOqKp9gcII/AAAAAAAADxg/EASFlgaAMyE/s1600/imagem_negativo.jpg"><img src="https://1.bp.blogspot.com/-RkFLv7jTiXM/VGOqKp9gcII/AAAAAAAADxg/EASFlgaAMyE/s200/imagem_negativo.jpg" alt="" width="200" height="131" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">imagefilter($imagem, IMG_FILTER_NEGATE);</td>
</tr>
</tbody>
</table>
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://1.bp.blogspot.com/-D_LlzEaSj5Y/VGOp5Kaz6qI/AAAAAAAADww/vCqmvYAAM_Q/s1600/imagem_brightness.JPG"><img src="https://1.bp.blogspot.com/-D_LlzEaSj5Y/VGOp5Kaz6qI/AAAAAAAADww/vCqmvYAAM_Q/s200/imagem_brightness.JPG" alt="" width="200" height="129" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">imagefilter($imagem, IMG_FILTER_BRIGHTNESS, 150);</td>
</tr>
</tbody>
</table>
&nbsp;
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://3.bp.blogspot.com/-K6v3_z-Lx5U/VGOp5JKyWKI/AAAAAAAADw4/EJ_uJ6Djcz4/s1600/imagem_colorize.JPG"><img src="https://3.bp.blogspot.com/-K6v3_z-Lx5U/VGOp5JKyWKI/AAAAAAAADw4/EJ_uJ6Djcz4/s200/imagem_colorize.JPG" alt="" width="200" height="132" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">imagefilter($imagem, IMG_FILTER_COLORIZE, 255,0,0);</td>
</tr>
</tbody>
</table>
&nbsp;
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://4.bp.blogspot.com/-fn97DcVAWmQ/VGOp6O0WvuI/AAAAAAAADw8/uWVqYayY1zM/s1600/imagem_contrast.JPG"><img src="https://4.bp.blogspot.com/-fn97DcVAWmQ/VGOp6O0WvuI/AAAAAAAADw8/uWVqYayY1zM/s200/imagem_contrast.JPG" alt="" width="200" height="130" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">imagefilter($imagem, IMG_FILTER_CONTRAST, -255);</td>
</tr>
</tbody>
</table>
&nbsp;
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://2.bp.blogspot.com/-A8B0u6gtm-U/VGOp6AK1PBI/AAAAAAAADxI/B2FtuhUQv30/s1600/imagem_grayscale.JPG"><img src="https://2.bp.blogspot.com/-A8B0u6gtm-U/VGOp6AK1PBI/AAAAAAAADxI/B2FtuhUQv30/s200/imagem_grayscale.JPG" alt="" width="200" height="129" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">imagefilter($imagem, IMG_FILTER_GRAYSCALE);</td>
</tr>
</tbody>
</table>
Obs.: Os filtros podem ser acumulados chamando um ou mais. Também podemos recuperar o tamanho da imagem com "imagesx()" para largura e "imagesy()" para altura, para mostrar esse exemplo mostrarei junto com o método <a href="http://php.net/imagecrop">imagecrop()</a> que retorna uma nova imagem com os parâmetros passados, segue:
<pre>$imagem = imagecrop($imagem, array('x'=((imagesx($imagem)/2)-150),'y'=((imagesy($imagem)/2)-100),'width'=150,'height'=150));</pre>
&nbsp;
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://4.bp.blogspot.com/-cIFjfQeaD2o/VGOp6fAYHVI/AAAAAAAADxE/yHrDBx2Pd6A/s1600/imagem_recorte.jpg"><img src="//4.bp.blogspot.com/-cIFjfQeaD2o/VGOp6fAYHVI/AAAAAAAADxE/yHrDBx2Pd6A/s1600/imagem_recorte.jpg" alt="" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">resultado do imgcrop()</td>
</tr>
</tbody>
</table>
Além disso, o PHP possui o método <a href="http://php.net/imagecrop">imagecropauto</a> que também faz o recorte da imagem porém de forma mais inteligente, como por exemplo você pode recortar retirando todo o fundo que for da cor branca ou preta, da seguinte forma:
<pre>imagefilter($imagem, IMG_FILTER_CONTRAST, -255);
$imagem = imagecropauto($imagem,IMG_CROP_WHITE);
</pre>
Para demostrar utilizei a imagem do nosso amigo elePHPant aumentando o contraste da imagem para que o fundo que é cinza na imagem original vire branco e assim posso usar o método para filtrar a área que possua algo na imagem, no caso nosso elePHPant.
<table class="tr-caption-container" style="margin-left: auto; margin-right: auto; text-align: center;" cellspacing="0" cellpadding="0" align="center">
<tbody>
<tr>
<td style="text-align: center;"><a style="margin-left: auto; margin-right: auto;" href="https://3.bp.blogspot.com/-6b2yF0H1DbU/VGOsk3-hPQI/AAAAAAAADx4/W_iZyzjFSDQ/s1600/imagem2.jpg"><img src="https://3.bp.blogspot.com/-6b2yF0H1DbU/VGOsk3-hPQI/AAAAAAAADx4/W_iZyzjFSDQ/s320/imagem2.jpg" alt="" width="320" height="292" border="0" /></a></td>
</tr>
<tr>
<td class="tr-caption" style="text-align: center;">resulta de imagecropauto()</td>
</tr>
</tbody>
</table>
Uma aplicação prática da utilização desses métodos seria o tratamento de imagens para leitura com OCR (Optical Character Read), assim você pode melhorar a qualidade e precisão da leitura do algoritmo.