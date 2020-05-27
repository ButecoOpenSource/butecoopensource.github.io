---
layout: wordpress
title: Acelerando o desenvolvimento com glade
excerpt: |
  Glade é a ferramenta de desenvolvimento de interfaces do gnome. Uma ferramenta ágil capaz de minimizar o tempo de desenvolvimento e deixar o design muito mais fácil de se implementar.
date: 2015-03-20 08:25:17
author: pedrojefferson
permalink: /acelerando-o-desenvolvimento-com-glade/
categories:
  - Ferramentas
tags:
  - desenvolvimento
  - gnome
  - python
---

<img class="aligncenter size-full wp-image-1575" src="/assets/wp-content/uploads/2015/03/gnome-logosz.png" alt="gnome-logosz" width="417" height="201" />

Há um tempo postei aqui no blog um artigo de como criar um formulário com PyGtk, Gdk e Sqlite3. O tutorial é altamente explicativo e pode ser visto <a href="/criando-formularios-com-python-e-pygtk3">aqui</a>.

O único problema e digo que foi proposital, é que toda a interface da aplicação foi construída via código, isso é bom e ruim ao mesmo tempo, depende de como você vê.

No desenvolvimento temos que lidar com diversos objetos que não necessariamente estão ligados ao funcionamento do programa e sim com detalhes de design e aparência. Na maioria dos projetos a designação de quem cuida da interface e quem cuida do funcionamento do programa, comportamento, entre outros, vão para pessoas diferentes, ou até mesmo equipes diferentes.

Glade vem suprir as necessidades de ambos os lados.

Glade é uma ferramenta Opensource para desenvolvimento de aplicações Gtk+ altamente intuitiva e fácil de manusear. Ele gera um xml que pode ser manipulado dinamicamente pelo código. O que te deixa livre para utilizar a mesma interface com diversas linguagens de programação.

<a href="/assets/wp-content/uploads/2015/03/glade.png"><img class="aligncenter size-full wp-image-1578" src="/assets/wp-content/uploads/2015/03/glade.png" alt="glade" width="1447" height="828" /></a>

<strong> Bom pro desenvolvedor </strong>
<ul>
	<li>Não é mais preciso utilizar funções como <strong>set_valign</strong> ou <strong>set_halign</strong> e tendo que lembrar todos os tipos de objetos <strong>Gtk.Align</strong> para aplicar o alinhamento para cada widget na sua interface.</li>
	<li>Funções tipo <strong>attach</strong> e <strong>pack_start</strong> são desnecessárias. Glade abstrai a forma de se inserir objetos em contêineres, é um simples "clica e arrasta" que já poupa bastante tempo.</li>
	<li>É possível também ter uma visão de objetos obsoletos para a versão do projeto que está usando. Isso evita que sua aplicação tenha alguma incompatibilidade.</li>
</ul>
<strong>Bom pro designer </strong>
<ul>
	<li>Você não tem que entender especificações de linguagens ou funções se quiser fazer redimensionamento de um objeto entry por exemplo. Se você é programador, não é tão difícil de usar <strong>entry.set_width_chars(30)</strong>, mas é completamente desnecessário colocar isso nas costas do designer, não é o foco dele.</li>
	<li>A interface é construída como se fosse um mockup, simples, fácil e rápido.</li>
	<li>Caso você tenha que criar uma outra aplicação com outra linguagem o processo não muda, você pode inclusive utilizar o mesmo xml para diversas aplicações.</li>
</ul>
<strong> Atenção </strong>

Abstrações a parte, as vezes é bom construir com cliques. É prático e qualquer um pode fazer. Porém é muito importante também que se conheça o mínimo do que se está fazendo ou as coisas podem dar errado, pode não ser hoje ou amanhã mas num futuro próximo. Sempre terá aquele cliente pedindo por uma alteração no funcionamento, mudança de regra, customizações e etc. E provavelmente você terá que resolver isso com código.

Por isso mantenha o costume de ler a documentação e principalmente saiba algo sobre esse objeto que você está arrastando com o mouse. "Problemas não avisam quando vão chegar"

<strong> Instalando </strong>

Windows
Em ambiente windows você pode fazer o download clicando <a href="http://ftp.gnome.org/pub/GNOME/binaries/win32/glade/">aqui</a>.

RedHat
<code> sudo yum install glade </code>

Ubuntu
<code> sudo apt-get install glade </code>

<strong>Construindo</strong>

Como citado anteriormente o glade gera um arquivo xml com nomenclatura '.glad' ou '.ui', a segunda é a mais nova e mais utilizada forma. Você pode manipular esse xml com diversas linguagens um breve exemplo é (C, C++, C#, Vala, Java, Perl e Python).

<a href="/assets/wp-content/uploads/2015/03/building.png"><img class="aligncenter size-full wp-image-1577" src="/assets/wp-content/uploads/2015/03/building.png" alt="building" width="1446" height="825" /></a>

O arquivo tem uma apresentação hierárquica de objetos e suas propriedades. É relativamente fácil identificar um objetos e seus filhos.
Inclusive alguns sinais podem ser manipulados pelo xml.

Veja um exemplo do arquivo.

<script src="//gistfy-app.herokuapp.com/github/1pedro/glade_app/hello_world.ui" type="text/javascript"></script>

Todo carregamento de biblioteca e declaração de objetos se mantêm o mesmo, a diferença está nos atributos.

Você precisa iniciar um objeto do tipo Builder e então carregar o arquivo xml.

<script src="//gistfy-app.herokuapp.com/github/1pedro/glade_app/app.py?slice=11:12" type="text/javascript"></script>

E então a partir daí é possível manipular seus widgets ou containers utilizando o builder e a função get_object.

<script src="//gistfy-app.herokuapp.com/github/1pedro/glade_app/app.py?slice=14:16" type="text/javascript"></script>

Note que, qualquer tipo de objeto pode ser carregado utilizando o get_object inclusive janelas, botões, contêineres e etc.. Eles se comportarão da mesma forma como se fossem criados da maneira convencional.
O código da aplicação pode ser visto <a href="https://github.com/1pedro/glade_app/blob/master/app.py"> aqui</a>.

O glade conta também com um manual de referência para desenvolvedores, para encontrá-lo basta apertar F1 ou ir na aba de ajuda. Lá você encontra vários manuais de tudo que é preciso saber para desenvolver com Gtk.

<a href="/assets/wp-content/uploads/2015/03/devhelp.png"><img class="aligncenter size-full wp-image-1576" src="/assets/wp-content/uploads/2015/03/devhelp.png" alt="devhelp" width="1162" height="760" /></a>

Nesse <a href="https://glade.gnome.org/">link</a> você encontrará tudo sobre o glade, desde as versões lançadas, tutoriais, contato com developers, wiki e etc.

Veja uma breve demonstração do glade.

<iframe width="560" height="315" src="https://www.youtube.com/watch?v=naKmmG5V0_A" frameborder="0" allowfullscreen></iframe>

Espero que esse artigo ajude a aumentar a sua produtividade e valorizar o seu tempo.
Dúvidas? Comente, me envie um <a href="mailto:pedrojefferson.developer@gmail.com">Email</a> ou entre em contato pelo <a href="https://twitter.com/_pedrojefferson">twitter</a>.

Obrigado, e até mais!
