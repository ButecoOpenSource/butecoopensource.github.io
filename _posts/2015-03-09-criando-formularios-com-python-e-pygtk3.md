---
layout: wordpress
title: Criando formulários com Python e PyGTK3
excerpt: |
  Python e Gtk uma combinação simples e prática para criação de interfaces. Nesse artigo você encontra o básico para poder implementar suas próprias interfaces, contendo  botões, caixas de entrada, título, caixa de seleção e muito mais.
date: 2015-03-09 22:29:05
author: pedrojefferson
permalink: /criando-formularios-com-python-e-pygtk3/
image: /assets/wp-content/uploads/2015/02/pythonzz2.png
categories:
  - Desenvolvimento
tags:
  - form
  - gtk3
  - python
---

<strong>Introdução</strong>

Pygtk é uma camada Python construída sobre o Gtk. Gtk nada mais é que o <em>Gimp Toolkit</em>, biblioteca utilizada pelo GNOME na criação de interfaces.

Esse tutorial foi construído com base no <a title="Manual de referencia GTK" href="https://developer.gnome.org/gtk3/stable/" target="_blank">Manual de Referencia do Gtk3</a> e no <a title="The Python GTK+ 3 Tutorial" href="http://python-gtk-3-tutorial.readthedocs.org/en/latest/index.html" target="_blank"> Python GTK+ 3 Tutorial</a>.

<strong>Requisitos</strong>
<ul>
	<li>Python 2.7.6 padrão (no Linux), em breve a versão 3 o substituirá.</li>
	<li>Gtk3</li>
	<li>Gdk</li>
	<li>Sqlite3</li>
</ul>
<strong>Python</strong>

A maioria das distribuições Linux já contam com o Python e o Gtk instalados por padrão.
Para verificar se sua distribuição conta com os pacotes necessários abra o <strong>terminal</strong> e digite:

<code>python --version</code>

<strong>Gtk</strong>

Para verificar se há bibliotecas Gtk instaladas em uma distribuição derivada do <em>Debian</em>, digite:

<code> dpkg -l libgtk2.0-0 libgtk-3-0 </code>

Deve retornar algo do tipo:
<code>
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
|/ Err?=(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Nome Versão Arquitectura Descrição
+++-===============================-====================-====================-=======
ii libgtk-3-0:amd64 3.14.8-0ubuntu1~14.0 amd64 GTK+ graphical user interface library
rc libgtk-3-0:i386 3.14.8-0ubuntu1~14.0 i386 GTK+ graphical user interface library
ii libgtk2.0-0:amd64 2.24.23-0ubuntu1.1 amd64 GTK+ graphical user interface library
ii libgtk2.0-0:i386 2.24.23-0ubuntu1.1 i386 GTK+ graphical user interface library
</code>

Se você estiver utilizando uma distribuição derivada do <em>Red Hat</em>, digite:

<code>yum list installed gtk3-devel gtk2-devel </code>

O retorno a seguir mostra que os pacotes estão corretamente instalados:

<code>Plugins carregados: auto-update-debuginfo, langpacks
Pacotes instalados
gtk2-devel.x86_64 2.24.26-1.fc21 installed
gtk3-devel.x86_64 3.14.8-2.fc21 installed
</code>

Usuários de Mac OSX podem conferir este <a title="Gtk+ Mac osx" href="http://www.gtk.org/download/macos.php" target="_blank">post.</a>

Usuários Windows precisam baixar o interpretador Python <a title="Python Download" href="https://www.python.org/downloads/" target="_blank">aqui</a> e o utilitário de instalação do PyGTK <a title="PyGobjectWin32" href="http://sourceforge.net/projects/pygobjectwin32/files/" target="_blank">aqui</a>.

Daqui em diante será mostrando o exemplo utilizando PyGtk. Logo abaixo é possível ver a importação das bibliotecas necessárias para construir a aplicação. Estas são as mesmas bibliotecas que foram verificadas anteriormente:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=10:12" type="text/javascript"></script>

<strong>Conhecendo Gtk.Window</strong>

A princípio criei uma classe Janela que herda de <strong>Gtk.Window</strong>, essa será a janela principal. Logo em seguida, define-se o método construtor e todos os atributos da janela principal, como o título da janela, o tamanho padrão, se a tela vai ser redimensionada ou não, cor de fundo e etc. Veja no código a seguir.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=15:21" type="text/javascript"></script>

No código acima, é instanciada a classe Gtk.Window e configurado os seus atributos, sendo eles o título da janela, tamanho da janela em pixels (600x600), configuração para não redimensionar a janela, e a cor de fundo da janela. O método <strong>modify_bg</strong>, que altera a cor da janela, recebe dois argumentos: um tipo de estado do gtk (StateType) e o <em>color_parse</em> com uma cor em Hexadecimal. Os estados possíveis que o modify_bg pode receber são: <strong>NORMAL</strong>, <strong>FOCUSED</strong>, <strong>ACTIVE</strong>, <strong>INCONSISTENT</strong>, <strong>INSENSITIVE</strong>, <strong>PRELIGHT</strong> e <strong>SELECTED</strong>, lembre-se, todos em maiúsculos. O que cada um estado representa? <a title="Gtk StateTypes" href="https://people.gnome.org/~gcampagna/docs/Gtk-3.0/Gtk.StateType.html" target="_blank">veja aqui</a>.

Atenção, objetos do tipo Window só aceitam um objeto por vez. Para poder utilizar múltiplos objetos por vez é necessário utilizar objetos containers dentro da janela. Começaremos com um container <em>grid</em>, que agrupará outros widgets.

<strong>Gtk.Grid</strong>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=22:25" type="text/javascript"></script>

A <strong>Grid</strong> é um elemento do tipo <strong>container</strong> que contempla vários widgets como entradas de texto, labels, botões e toda parte que se pode interagir com a aplicação. Você deve imaginar uma grid exatamente como uma tabela. Aqui são adicionadas duas grids. Dentro de uma grid, vai um elemento box1 que é um <strong>Gtk.Box</strong> que também é um objeto container. É completamente necessário adicionar a nova box de fato na grid utilizando o grid.attach. O grid.attach recebe 5 parâmetros, sendo a referência do objeto a ser adicionado (self), <strong>left</strong>, <strong>top</strong>, <strong>width</strong> e <strong>height</strong>.

<script src="h//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=26:34" type="text/javascript"></script>

<strong>Label</strong>

Labelinit é um objeto do tipo Label que é utilizado para textos, e que será o título da aplicação. Um dos mais interessantes métodos da classe label é o <strong>set_markup</strong>, pois ele recebe como argumento uma string formatada em pango markup language. Quer conhecer mais? Então <a title="Pango markup language" href="https://developer.gnome.org/pango/stable/PangoMarkupFormat.html" target="_blank">clique aqui</a>.

Mas lembre-se, apesar de ter uma sintaxe muito parecida, <strong>Pango não é HTML</strong>, portanto, nem todas as tags que você por funcionarão.

<strong>Box</strong>

A inserção de qualquer objeto em um elemento do tipo Box, se dá por dois comandos:
<strong>Box.pack_start</strong> para adicionar objetos no início da box e <strong>Box.pack_end</strong> que obviamente adiciona objetos no fim da box. Os parâmetros informam se ele será expansível ou não, se terá preenchimento e espaço entre os objetos. Por fim, crio um novo objeto do tipo <strong>Grid</strong>, chamada de grid2 e passo a quantidade de espaço entre duas colunas consecutivas, espaço da coluna e espaço da linha. Confira Linha 34 do código anterior.

Com toda a estrutura da janela criada, vamos aos objetos!

<strong>Widgets</strong>

<script src="h//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=35:44" type="text/javascript"></script>

Widgets são objetos comuns de uma interface, como campo de entrada, textos, botões, caixa de seleção e etc. Eles obrigatoriamente devem ficar contidos em objetos containers, como Grids ou Box. O primeiro objeto é o label do nome, o <strong>set_halign</strong> representa o alinhamento horizontal do objeto em relação a grid ou box em que esse objeto está, da mesma forma temos <strong>set_valign</strong> para o alinhamento vertical. Eles recebem como parâmetro um objeto do tipo <strong>Gtk.Align,</strong> e os tipos são: <strong>BASELINE</strong>, <strong>CENTER</strong>, <strong>FILL</strong>, <strong>START</strong>. Dúvidas sobre os tipos? <a title="Gtk Align Types" href="http://www.roojs.com/seed/gir-1.2-gtk-3.0/gjs/Gtk.Align.html" target="_blank">Veja mais aqui</a>.

Em seguida, adicionamos na grid1 com <strong>left=0</strong>, <strong>top=1</strong>, <strong>width=1</strong> e <strong>height=1</strong>. Objetos do tipo <strong>Gtk.Entry</strong> (Linha 39) são altamente configuráveis, no exemplo fi configurado o max_length para 150, que é o maior quantidade de caracteres que o campo pode receber, e o tamanho do campo <strong>width_chars</strong> em caracteres(30), note que um é completamente diferente do outro. Por fim, adicionei o objeto na grid2 e criei uma conexão.

<strong>Conexões</strong>

Conexão é, a grosso modo, a ligação do estado do objeto com um método. No exemplo, é criado uma conexão do estado <strong>“changed”</strong> com um método chamado <strong>“on_entry_nome_changed” </strong>, até então não criado ainda. Mas o que ela faz? Ela é chamada toda vez que o estado da <strong>entry_nome</strong> for mudada.

O que se segue agora é a repetição do código acima com apenas algumas modificações. Vamos criar um label e um entry para cada entrada que o usuário tiver que digitar. Note que, o objeto label é o texto que fica ao lado da área para o usuário digitar. E o objeto entry é justamente o campo.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=45:64" type="text/javascript"></script>

A única diferença está no objeto entry_tel que chama o set_text para demonstrar como deve ser a entrada do telefone, e logo abaixo é configurada a cor cinza claro via Gdk._color_parse. (Linhas 63 e 64)

O mesmo acontece com as próximas entradas Email e Data de Nascimento.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=65:83" type="text/javascript"></script>

<strong>Gtk.ComboBoxText</strong>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=84:108" type="text/javascript"></script>

O <strong>Gtk.ComboBoxText</strong> é um meio de entrada de dados que utiliza uma lista já criada e recebe três parâmetros, um inteiro informando a ordem, um id e o texto.

<strong>Gtk.Button</strong>

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=109:114" type="text/javascript"></script>

Criei um objeto chamado commit do tipo <strong>Gtk.Button</strong> (Linha 110). Este objeto recebe como parâmetros: um label, um alinhamento, o posicionamento na grid, o tamanho do botão, e uma conexão usando o sinal “<strong>clicked</strong>”(com outro método que não está criado ainda).

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=115:118" type="text/javascript"></script>

<strong>Adicionando objetos containers no container principal</strong>

Por fim, vamos pegar todas as grids e box que criamos no meio do caminho e vamos amarrá-las à grid principal chamada grid_total (Linhas 121 e 122 do código abaixo).

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=119:123" type="text/javascript"></script>

<strong>Métodos</strong>

Vamos fazer dois métodos para o funcionamento do formulário. O primeiro método será <strong>on_entry_nome_changed</strong> para auxiliar na entrada do nome do usuário. A utilização deste  método se deve ao fato dele colocar o nome em maiúsculo em tempo de execução. Funciona da seguinte maneira: O usuário coloca o nome e em tempo de execução, o método transforma os caracteres para maiúsculo, por isso é usado o sinal "changed", pois a cada carácter novo o método precisa torná-lo maiúsculo. Então ele pega o texto via get_text e faz o upper, que torna-o maiúsculo e devolve o texto por outra função set_text. Confira no código abaixo.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=125:129" type="text/javascript"></script>

O segundo método é o do botão de cadastro. Este é o momento de salvar os dados no banco.

Ele pega todos as entradas de todos os campos via <strong>get_text</strong> ou via <strong>get_active_text</strong> (para objetos <strong>ComboBoxText</strong>). Se não forem nulos, ele os envia para a função que de fato faz commit no banco de dados. Se todas as entradas forem informadas, o método commit_dados é chamado. Caso um dos campos for nulo ele executa o comando pass e não envia nada ao sqlite (Linhas 141 à 144 do código abaixo).

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=131:144" type="text/javascript"></script>

A função "commit_dados" recebe os parâmetros, cria uma conexão sqlite3 com um arquivo de banco de dados. A segunda linha do código é necessária para o sqlite possa processar texto do tipo 8-bits. É preciso também criar um cursor, pois é nele que vamos executar os comandos sql.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/exemplos/exemplos_python/pygtk/pygtk-form.py?slice=146:154" type="text/javascript"></script>

Passo todos os parâmetros em apenas dois comandos sql (Linhas 151 e 152), sendo que o primeiro verifica se o banco de dados já existe. Se não existir, ele cria o banco e o modelo, setando os tipos de dados e os nomes dos campos. O segundo insere os dados nos campos. Os dados são pegos pelos argumentos da função principal <strong>*args</strong> e são passados como símbolos(?) para cada campo inserido. Lembre-se que a quantidade de "?" tem que ser a mesma quantidade de parâmetros contido em <strong>*args</strong>. No final, executo uma função da conexão chamada commit que salva os dados no banco.

Cuidado para não confundir a função commit_dados do botão com a função do sqlite commit.

<strong>A última coisa a fazer é iniciar a aplicação…</strong>

Crio um objeto do tipo Janela(), que é a nossa janela principal. Utilizo o <strong>connect</strong> para criar uma conexão entre a janela principal e o sinal “<strong>delete-event</strong>” (que é o sinal de fechar a janela). O comando <strong>show_all</strong> exibe todos os widgets ligados a janela, seja grid, box, entry, comboboxtext, entre outros.

E por fim <strong>Gtk.main()</strong> inicia o gtk executando tudo.

Se você seguiu passo a passo a criação da aplicação essa deve ser a aparência final.

<a href="/assets/wp-content/uploads/2015/03/screen.png"><img src="/assets/wp-content/uploads/2015/03/screen.png" alt="screen" width="706" height="510" class="aligncenter size-full wp-image-1536" /></a>

Espero que você tenha gostado do mini-tutorial, e principalmente tenha aprendido algo, pois a intenção é justamente passar o conhecimento para frente! O código completo da aplicação você pode acessar <a href="https://github.com/ButecoOpenSource/exemplos/blob/master/exemplos_python/pygtk/pygtk-form.py" target="_blank">clicando aqui</a>.

No caso de dúvidas atendo pelos comentários desse post, pelo <a href="mailto:pedrojefferson.developer@gmail.com">e-mail</a> ou pelo <a href="https://twitter.com/_pedrojefferson" target="_blank">Twitter</a>.

Obrigado, e até mais!