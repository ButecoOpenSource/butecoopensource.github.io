---
layout: wordpress
title: Python 2.7.9 já está disponível
date: 2014-12-11 14:18:37
author: alexandrevicenzi
permalink: /python-2-7-9-ja-esta-disponivel/
image: /assets/wp-content/uploads/2014/12/python-logo.png
categories:
  - Desenvolvimento
  - Notícias
tags:
  - python
---

A nova versão do Python, a 2.7.9, é uma versão que traz correções de bugs para a versão 2.7. Esta liberação inclui várias mudanças significativas diferentemente das demais <em>bugfix</em>.

Entre as mudanças que acompanham esta versão estão:
<ul>
	<li>O módulo SSL do Python 3.4 foi portado completamente para Python 2.7.9. Veja a <a href="https://www.python.org/dev/peps/pep-0466/">PEP 466</a> para mais detalhes.</li>
	<li>A validação de certificados HTTPS agora está usando o armazenamento de certificados do sistema por padrão. Veja a <a href="https://www.python.org/dev/peps/pep-0476/">PEP 476</a> para mais detalhes.</li>
	<li>O SSLv3 foi desativado por padrão, devido ao <a href="https://www.imperialviolet.org/2014/10/14/poodle.html">ataque POODLE</a>.</li>
	<li>O módulo <a href="https://docs.python.org/2/library/ensurepip.html">ensurepip</a> foi portado para Python 2.7, ele fornece o gerenciador de pacotes pip em todas as instalações do Python 2.7. Veja a <a href="https://www.python.org/dev/peps/pep-0477/">PEP 477</a>.</li>
</ul>
Você pode fazer o download da nova versão <a href="https://www.python.org/downloads/release/python-279/">aqui</a>.

Via <a href="https://mail.python.org/pipermail/python-dev/2014-December/137536.html">Python-Dev</a>