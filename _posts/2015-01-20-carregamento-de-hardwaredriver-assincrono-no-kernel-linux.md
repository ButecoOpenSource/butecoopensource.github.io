---
layout: wordpress
title: Carregamento de hardware/driver assíncrono no kernel Linux
date: 2015-01-20 18:33:36
author: marcossouza
permalink: /carregamento-de-hardwaredriver-assincrono-no-kernel-linux/
image: /assets/wp-content/uploads/2015/01/Tux.png
categories:
  - Hardware / DIY
  - Notícias
tags:
  - kernel
  - linux
---

Enquanto o Chrome OS já tem o suporte ao carregamento de dispositivos/drivers assíncrono, o kernel linux ainda não.  Mas patches já foram enviados ao Linux tentando introduzir esta nova característica. Esta alteração tem o propósito de fazer o carregamento do sistema mais ágil, uma vez que alguns dispositivos demoram para ter seu carregamento e isto atualmente atrasa o tempo de boot do sistema.

O desenvolvedor Dmitry Torokhov enviou oito patches para o kernel baseado na implementação do Chrome OS. O atual estado desses patches ainda causam problemas em um boot completamente assíncrono em algumas plataformas, embora ele já tenha conseguido ativar este recurso em um sistema Rockchip com sucesso.

Os patches de Dmitry podem ser verificados <a href="http://lkml.iu.edu/hypermail/linux/kernel/1501.2/00576.html" target="_blank">aqui</a>.

Via <a href="http://www.phoronix.com/scan.php?page=news_item&amp;px=Async-Device-Driver-Linux-Probi" target="_blank">Phoronix</a>