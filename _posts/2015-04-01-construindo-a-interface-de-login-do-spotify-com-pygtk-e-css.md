---
layout: wordpress
title: Construindo a interface de login do spotify com PyGTK e CSS
excerpt: |
  Desenvolva aplicativos mais facilmente fazendo o uso do CSS linguagem de estilo da web agora aplicada a interfaces com Python e Gtk.
date: 2015-04-01 12:10:10
author: pedrojefferson
permalink: /construindo-a-interface-de-login-do-spotify-com-pygtk-e-css/
categories:
  - Desenvolvimento
tags:
  - desenvolvimento
  - gnome
  - programação
  - python
---

Atenção, construiremos uma interface muito <strong>semelhante</strong> a do spotify. Há alguns elementos que não foram possíveis a representação igual ao da interface original.

Aqui vai uma screen da interface original(à direita) e a interface criada(à esquerda).

<a href="/assets/wp-content/uploads/2015/03/spotify.png"><img class="aligncenter size-full wp-image-1728" src="/assets/wp-content/uploads/2015/03/spotify.png" alt="spotify" width="749" height="556" /></a>
<strong>Construindo</strong>
Primeiro iremos importar três bibliotecas <strong>Gtk</strong>, <strong>Gdk</strong> e <strong>GdkPixbuf</strong>. A primeira creio que todos já conheçam, a segundo é a Gnome Drawing Kit a último é a Pixbuf, que será utilizado pra adicionar imagens na interface.

Precisaremos também de um modelo de interface, a não ser que se queira construir todos os objetos a mão, utilizaremos o glade. Veja o arquivo xml <a href="https://github.com/1pedro/spotify_app/blob/master/spotify_app.glade"> aqui</a> gerado pelo Glade.

Como vocês já viram no post do glade (se não viram vale a pena conferir <a href="/acelerando-o-desenvolvimento-com-glade"> aqui</a>), não se deve carregar todos os objetos da interface, somente aqueles que precisarão de manipulação via código. Note que é importante também dar nomes aos objetos, assim fica mais fácil de aplicar as propriedades com base nesses nomes. veja no exemplo abaixo.

<script src="//gistfy-app.herokuapp.com/github/1pedro/spotify_app/spotify_app.py?&amp;slice=26:32" type="text/javascript"></script>
Criaremos um novo tipo de objeto, o Pixbuf que como dito anteriormente adicionará imagens a interface.
<script src="//gistfy-app.herokuapp.com/github/1pedro/spotify_app/spotify_app.py?&amp;slice=35:37" type="text/javascript"></script>
Como pode ser visto, o método <strong> Pixbuf.new_from_file_at_size </strong> recebe três parâmetros, o arquivo de imagem e a largura e altura em pixels. Em seguida o <strong>image1.set_from_pixbuf()</strong> liga o objeto imagem ao pixbuf adicionando o elemento criado anteriormente. Essa não é a única forma de se adicionar imagem na aplicação, porém é a que eu acho mais simples de se fazer. Caso queira ver as outras formas clique <a href="https://developer.gnome.org/gtk3/stable/GtkImage.html"> aqui </a>.

Algumas outras configurações são necessárias pra ajustar a tela.

<script src="//gistfy-app.herokuapp.com/github/1pedro/spotify_app/spotify_app.py?&amp;slice=39:51" type="text/javascript"></script>

Adiciono um outro pixbuf que será necessário para o botão de login do facebook. O markup dos links no caso de perca de usuários sem cadastro e perca de senha.

E por fim algumas conexões dos botões.

<strong> CSSProvider </strong>

Toda a mágica da interface só é possível devido a um elemento especial, o CssProvider. CSSProvider é um tipo de objeto do Gtk capaz de carregar código css para a aplicação seja no mesmo arquivo da aplicação ou um arquivo externo exemplo "style.css".

Precisamos armazenar todo o conteúdo css dentro de uma variável, ela será lida pelo Gtk posteriormente.

<script src="//gistfy-app.herokuapp.com/github/1pedro/spotify_app/spotify_app.py?&amp;slice=53:61" type="text/javascript"></script>

Se você está usando python 3.x deverá informar o prefixo b antes da string para ela ser lida em bytes.

Ficará algo do tipo:

<pre><code class="python">
css = b&quot;&quot;&quot;
@import url(&quot;style.css&quot;);

GtkWindow {
    background-color:#111111;
}
&quot;&quot;&quot;
</code></pre>

É nessa parte que você diz de onde vai carregar o css, sendo da própria variável ou de um arquivo externo. Criaremos um objeto do tipo Gtk.CssProvider ele será a responsável por carregar o css e em seguida ele carrega o código CSS da variável chamada também de css.

<script src="//gistfy-app.herokuapp.com/github/1pedro/spotify_app/spotify_app.py?&amp;slice=62:64" type="text/javascript"></script>

O Gtk.StyleContext adiciona um provedor de estilo global para a tela, que será usado na construção de estilo para todos os GtkStyleContexts sob tela. Esse objeto recebe a Screen padrão, o objeto que absorveu o css stylecssprovider e o style provider priority.

A notação css segue da mesma forma que é utilizada para construção de websites. Seguem exemplos de seletores.

Seletor universal:


<pre><code class="css">
*{

}
</code></pre>


Selecionar todos os objetos do tipo Gtk button:

<pre><code class="css">
GtkButton {

}
</code></pre>

Para conferir todos os seletores confira esse post.
Veja abaixo o arquivo de css da aplicação que é importado pelo <strong>@import</strong> da variável css.

<script src="//gistfy-app.herokuapp.com/github/1pedro/spotify_app/style.css" type="text/javascript"></script>

<strong> Atenção </strong>

Alguns elementos não puderam ser 100% representados como na interface original, exemplos deles é a fonte utilizada na aplicação, o botão toggle e os links. Fora esses contratempos, acho que a aplicação é válida principalmente por passar algo novo que é a integração do gtk com o css.

A aplicação completa está no github e pode ser acessada <a href="https://github.com/1pedro/spotify_app">aqui</a>. A quem quiser contribuir pode ficar à vontade.

Se quiser entrar em contato pode comentar esse post, me enviar um <a href="mailto:p.dupond@example.com"> Email </a> ou me chamar no <a href="https://twitter.com/_pedrojefferson">Twitter</a>.
