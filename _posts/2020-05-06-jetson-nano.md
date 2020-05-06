---
layout: post
title: "NVIDIA Jetson Nano Developer Kit"
excerpt: "Uma placa de desenvimento focada em visão computacional e deep learning."
tagline: "Uma placa de desenvimento focada em visão computacional e deep learning"
date: 2020-05-06 08:00:00
categories: Hardware
tags: nvidia redes-neurais hardware
permalink: review-nvidia-jetson-nano-developer-kit
author: alexandrevicenzi
header:
  overlay_color: "#333"
  show_overlay_excerpt: true
  image: /assets/content/jetson-nano-devkit.png
---

[NVIDIA® Jetson Nano™ Developer Kit](https://developer.nvidia.com/embedded/jetson-nano-developer-kit) é um kit de desenvolvimento SoM (system-on-module) que permite que você execute multiplas redes neurais em paralelo, para aplicações como classificação de imagens, detecção de objetos, segmentação e reconhecimento de fala. Tudo em uma plataforma simples de usar e que consome apenas 5W.

## Especificações

|:---|:---|
| CPU           | Quad-core ARM A57 @ 1.43 GHz |
| GPU           | 128-core Maxwell |
| Memória       | 4 GB 64-bit LPDDR4 25.6 GB/s |
| Armazenamento | microSD (não incluso) |
| Camera        | 2x MIPI CSI-2 |
| Conectividade | Gigabit Ethernet, M.2 Key E (para adaptadores Wifi/BT) |
| Vídeo         | HDMI e DisplayPort |
| USB           | 4x USB 3.0 |
| Outros        | GPIO, I2C, I2S, SPI, UART |
| Dimenções     | 69 mm x 45 mm |

## Software

A imagem oficial é Ubuntu, e conta com suporte de bibliotecas como [JetPack SDK](https://developer.nvidia.com/embedded/jetpack), CUDA Toolkit, cuDNN, TensorRT, TensorFlow, OpenCV, OpenGL, Vulkan, entre outros.

## Finalidade

A finalidade principal da Jetson Nano é a utilização em aplicações relacionadas a visão computacional e deep learning, onde se faz necessário o uso de GPU, pois ela provê 472 GFLOPS (FP16) de desempenho computacional, tudo isso consumindo apenas 5-10W.

Alguns dos usos mais comuns são robôs autônomos, dispositivos IoT inteligentes, e sistemas avançados de Inteligência Artificial (IA).

## Desempenho

Na tabela abaixo é feita uma comparação da Jetson Nano com demais opções disponíveis no mercado, dentre elas:

* Raspbery Pi 3
* Raspbery Pi 3 com a [Intel Neural Compute Stick 2](https://software.intel.com/pt-br/neural-compute-stick)
* [Google Edge TPU Dev Board](https://coral.ai/products/dev-board/)

| Modelo | Framework | Jetson Nano | RPi 3 | RPi 3 + Intel NCS2 | Google Edge TPU |
|:---------------------------|:----------:|:------:|:-------:|:-------:|:-------:|
| ResNet-50 (224×224)        | TensorFlow | 36 FPS | 1.4 FPS | 16 FPS  | DNR     |
| MobileNet-v2 (300×300)     | TensorFlow | 64 FPS | 2.5 FPS | 30 FPS  | 130 FPS |
| SSD ResNet-18 (960×544)    | TensorFlow | 5 FPS  | DNR     | DNR     | DNR     |
| SSD ResNet-18 (480×272)    | TensorFlow | 16 FPS | DNR     | DNR     | DNR     |
| SSD ResNet-18 (300×300)    | TensorFlow | 18 FPS | DNR     | DNR     | DNR     |
| SSD Mobilenet-V2 (960×544) | TensorFlow | 8 FPS  | DNR     | 1.8 FPS | DNR     |
| SSD Mobilenet-V2 (480×272) | TensorFlow | 27 FPS | DNR     | 7 FPS   | DNR     |
| SSD Mobilenet-V2 (300×300) | TensorFlow | 39 FPS | 1 FPS   | 11 FPS  | 48 FPS  |
| Inception V4 (299×299)     | PyTorch    | 11 FPS | DNR     | DNR     | 9 FPS   |
| Tiny YOLO V3 (416×416)     | Darknet    | 25 FPS | 0.5 FPS | DNR     | DNR     |
| OpenPose (256×256)         | Caffe      | 14 FPS | DNR     | 5 FPS   | DNR     |
| VGG-19 (224×224)           | MXNet      | 10 FPS | 0.5 FPS | 5 FPS   | DNR     |
| Super Resolution (481×321) | PyTorch    | 15 FPS | DNR     | 0.6 FPS | DNR     |
| Unet (1x512x512)           | Caffe      | 18 FPS | DNR     | 5 FPS   | DNR     |

> *DNR* significa Did Not Run, ou, não foi possível executar.

A Raspbery Pi por si só não é focada em nenhum tipo de aplicação relacionada a inteligência artificial e nem possui capacidade computacional para tal.

A Intel Neural Compute Stick 2 é uma VPU (unidade de processamento visual), e seu foco principal é visão computacional, porém a NCS2 é um dispositivo USB, ou seja, ela precisa ser utilizada em conjunto com algum outro computador, e é a combinação ideal para a Raspbery Pi.

A Google Edge também é uma SoM (system-on-module) e conta com uma TPU (unidade de processamento de tensores) capaz de executar 4 trilhões de operações (tera-operations) por segundo (TOPS) e seu foco principal também é visão computacional.

A Jetson Nano possui uma GPU (unidade de processamento gráfico) Maxwell de 128 núcleos CUDA, ou seja, é a mesma arquitetura da Titan X e GTX 970, porém com cerca de 1/10 dos núcleos CUDA. Sendo uma GPU, ela permite uma variedade maior de aplicações.

Obviamente a Jetson Nano não é ideal para o treinamento de redes neurais, como uma GPU de Desktop ou Servidor, porém, para a execução, em determinadas aplicações ela supera as demais concorrentes.

## Considerações finais

A Jetson Nano é certamente uma plaquinha interessante, principalmente em usos como robôs autônomos, porém vale resaltar que ela é uma placa de desenvolvimento, ou seja, uso indicado para prototipação.

Para produção em larga escala ou para uso em algum sistema em produção é aconselhável utilizar outras placas da família Jetson, como por exemplo a Jetson Xavier NX.

Seu preço oficial é de 99 Dólares, porém achá-la no Brasil e por um preço aceitável é outra questão.

Fique ligado que falaremos novamente sobre a Jetson Nano em breve.
