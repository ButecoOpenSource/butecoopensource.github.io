---
layout: wordpress
title: Mesa muito próximo do OpenGL 4.2 e 4.3
excerpt: |
  Um resumo do estado atual dos drivers mesa em relação ao seu suporte ao OpenGL.
date: 2016-04-07 13:04:15
author: marcossouza
permalink: /mesa-muito-proximo-do-opengl-4-2-e-4-3/
image: /assets/wp-content/uploads/2015/07/attachment.cgi_.png
categories:
  - Notícias
tags:
  - driver
  - games
  - jogos
  - linux
  - mesa
  - open-source
  - opengl
---

Há muito tempo que esperamos ter um bom suporte a jogos no Linux, e em partes isso já é realidade com a Steam e com os muitos jogos que já foram portados. Ainda assim, muito dos jogos AAA ainda precisam de um driver proprietário para poderem ser executados, mas isto pode mudar em breve.

<!--more-->

Este artigo mostra quais os drivers do mesa que estão muito próximos de terem suporte a extensões utilizadas pelos jogos mais recentes. Na tabela abaixo estão identificado as extensões OpenGL <strong style="color: #009900;">implementadas</strong>, <strong style="color: #ffd633;">em desenvolvimento</strong> e as <strong style="color: #fe0000;">não implementadas</strong>.

<table class="table table-bordered">
<tbody>
<tr>
<th></th>
<th>NVC0 (nVidia)</th>
<th>radeonsi (AMD)</th>
<th>r600 (AMD)</th>
<th>i965 (Intel)</th>
</tr>
<tr>
<td style="background-color: #e0e0d1;" colspan="5">OpenGL 4.0</td>
<tr>
<td>GL_ARB_gpu_shader_fp64</td>
<td style="background-color: #009900;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #ffd633;"></td>
</tr>
<td style="background-color: #e0e0d1;" colspan="5">OpenGL 4.1</td>
<tr>
<td>GL_ARB_vertex_attrib_64bit</td>
<td style="background-color: #009900;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #fe0000;"></td>
</tr>
<tr>
<td style="background-color: #e0e0d1;" colspan="5">OpenGL 4.2</td>
</tr>
<tr>
<td>GL_ARB_shader_image_load_store</td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #ffd633;"></td>
<td style="background-color: #009900;"></td>
</tr>
<tr>
<td>GL_ARB_shader_atomic_counters</td>
<td style="background-color: #009900;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
</tr>
<tr>
<td style="background-color: #e0e0d1;" colspan="5">OpenGL 4.3</td>
</tr>
<tr>
<td>GL_ARB_robust_buffer_access_behavior</td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #ffd633;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #fe0000;"></td>
</tr>
<tr>
<td>GL_ARB_compute_shader</td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
</tr>
<tr>
<td>GL_ARB_framebuffer_no_attachments</td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #009900;"></td>
</tr>
<tr>
<td>GL_ARB_shader_image_size</td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
</tr>
<tr>
<td>GL_ARB_shader_storage_buffer_object</td>
<td style="background-color: #009900;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
</tr>
<tr>
<td>GL_ARB_compute_shader</td>
<td style="background-color: #ffd633;"></td>
<td style="background-color: #ffd633;"></td>
<td style="background-color: #fe0000;"></td>
<td style="background-color: #009900;"></td>
</tr>
</tbody>
</table>

Vale salientar que, jogos recentes utilizam OpenGL 4.3, 4.4 e 4.5, e desta forma estamos perto de podermos jogar muitos jogos da Steam com os drivers open source.
Para consultar o estado de cada driver em relação ao suporte do OpenGL, basta visitar o <a href="https://mesamatrix.net/" target="_blank">MesaMatrix.net</a>.