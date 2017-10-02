---
layout: wordpress
title: "Hands on: quilt"
excerpt: |
  Um guia para iniciar a trabalhar com o quilt.
date: 2015-06-29 23:35:56
author: marcossouza
permalink: /hands-on-quilt/
image: /assets/wp-content/uploads/2015/06/Captura-de-tela-de-2015-06-08-23-26-13.png
categories:
  - Desenvolvimento
  - Ferramentas
tags:
  - linux
  - programação
  - quilt
  - terminal
---

Quilt é uma ferramenta para criação e manipulação de patches de código fonte. Sua utilização é bem simples e permite criar patches de forma bem prática. Ele foi originalmente criado pelo desenvolvedor Andrew Morton, sendo uma série de scripts para gerenciar patches no Linux. Mas Andreas Grünbacher, um outro desenvolvedor, melhorou os scripts de Andrew para gerar constumizações do kernel para o SuSe Linux.

Para um exemplo prático, vejamos a seguinte estrutura de arquivos:

<pre><code class="bash">
[marcos@puppet pytabs]$ ls
main.py  new_tab.py  new_tab.pyc  new_tab.ui  window.ui
</code></pre>

Para criar um novo patch, execute:

<pre><code class="bash">
quilt new alteracao1.patch
</code></pre>

Após a execução deste comando, será criada uma pasta "patches", que conterá todos os patches criados. Por hora esta pasta contém apenas o arquivo series, já que não adicionamos e nem alteramos nenhum arquivo para adicionar ao patch recem criado. O arquivo series mostra a ordem em que os patches criados serão aplicados.

<!--more-->

Após a execução, segue a nova estrutura de fontes:

<pre><code class="bash">
[marcos@puppet pytabs]$ quilt new alteracao1.patch
Patch patches/alteracao1.patch is now on top
[marcos@puppet pytabs]$ ls
main.py  new_tab.py  new_tab.pyc  new_tab.ui  patches  window.ui
[marcos@puppet pytabs]$ ls patches/
series
[marcos@puppet pytabs]$ cat patches/series
alteracao1.patch
</code></pre>

Para adicionar um arquivo ao patch corrente, execute:

<pre><code class="bash">
quilt add main.py
</code></pre>

Este comando irá adicionar o arquivo main.py ao patch alteracao1.patch. A partir de agora, todas as alterações feitas neste arquivo irão ser adicionadas ao patch. A saída do comando mostra esta informação:

<pre><code class="bash">
[marcos@puppet pytabs]$ quilt add main.py
File main.py added to patch patches/alteracao1.patch
</code></pre>

Após fazer uma alteração no arquivo main.py, execute um quilt refresh para então gerar/atualizar o patch alteracao1.patch. A saída abaixo mostra o patch gerado e atualizado:

<pre><code class="bash">
[marcos@puppet pytabs]$ vim main.py
[marcos@puppet pytabs]$ quilt refresh
Refreshed patch patches/alteracao1.patch
[marcos@puppet pytabs]$ cat patches/alteracao1.patch
Index: pytabs/main.py
===================================================================
--- pytabs.orig/main.py
+++ pytabs/main.py
@@ -8,6 +8,7 @@ import new_tab

 class AppWindow():
 	def __init__(self):
+		print '__init__ called'
 		user_home = os.environ['HOME']
 		conf_path = user_home + '/.config/'
 		app_path = user_home + '/.config/pytabs/'
[marcos@puppet pytabs]$ vim main.py
[marcos@puppet pytabs]$ quilt refresh
Refreshed patch patches/alteracao1.patch
[marcos@puppet pytabs]$ cat patches/alteracao1.patch
Index: pytabs/main.py
===================================================================
--- pytabs.orig/main.py
+++ pytabs/main.py
@@ -8,6 +8,7 @@ import new_tab

 class AppWindow():
 	def __init__(self):
+		print '__init__ called'
 		user_home = os.environ['HOME']
 		conf_path = user_home + '/.config/'
 		app_path = user_home + '/.config/pytabs/'
@@ -37,7 +38,9 @@ class AppWindow():
 		Gtk.main()

 	def onButtonAddTab(self, button):
-		tabs = new_tab.Tab(self.connection)
+		print 'Adding new tab'
+		tabs = new_tab.Tab( self.connection )
+		print 'addtab called'

 	def onButtonListTabs(self, button):
 		win_list = ListTabs(self.connection)

</code></pre>

A partir de agora, o patch está aplicado sobre o código fonte. A partir de agora, múltiplos patches podem ser criados. Na verdade o quilt cria um "pilha" de patches, onde a base (primeiro patch da pilha) é aplicado primeiro e todos os próximos vão sendo aplicados na sequência. Para mostrar os patches e sua ordem de aplicação podemos executar o quilt series:

<pre><code class="bash">
[marcos@puppet pytabs]$ quilt series
patches/alteracao1.patch
patches/alteracao2.patch
</code></pre>

Para "desaplicar" o patch, ou seja, desfazer suas alterações, basta executar o comando pop. Este comando irá desfazer o patch no topo da pilha. Para aplicar novamente basta executar quilt push, que também irá aplicar o patch mais próximo da base que ainda não foi aplicado:

<pre><code class="bash">
[marcos@puppet pytabs]$ quilt pop
Removing patch patches/alteracao2.patch
Restoring new_tab.ui

Now at patch patches/alteracao1.patch
[marcos@puppet pytabs]$ quilt pop
Removing patch patches/alteracao1.patch
Restoring main.py

No patches applied
[marcos@puppet pytabs]$ quilt series
patches/alteracao1.patch
patches/alteracao2.patch
[marcos@puppet pytabs]$ quilt push
Applying patch patches/alteracao1.patch
patching file main.py

Now at patch patches/alteracao1.patch
[marcos@puppet pytabs]$ quilt push
Applying patch patches/alteracao2.patch
patching file new_tab.ui

Now at patch patches/alteracao2.patch
[marcos@puppet pytabs]$ quilt push
File series fully applied, ends at patch patches/alteracao2.patch

</code></pre>

Existem muitos outros comandos do quilt como:
annotate
delete
diff
edit
files
greap
headers
import
remove
rename

Agora, você já pode "patchar" projetos e enviar seus patches! Até a próxima!

Referências:
<a href="http://en.wikipedia.org/wiki/Quilt_%28software%29" target="_blank">Quilt - Wikipédia</a>
<a href="http://linux.die.net/man/1/quilt" target="_blank">Quilt manual</a>