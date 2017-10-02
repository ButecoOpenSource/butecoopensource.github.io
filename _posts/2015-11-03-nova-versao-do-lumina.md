---
layout: wordpress
title: Nova versão do Lumina
excerpt: |
  Nova versão do WM Lumina 0.8.7
date: 2015-11-03 21:48:24
author: marcooliveira
permalink: /nova-versao-do-lumina/
image: /assets/wp-content/uploads/2015/10/Lumina.png
categories:
  - Distros
  - Notícias
tags:
  - freebsd
  - noticias
---

Você já ouviu falar ou leu sobre o Lumina?

Pois bem, nem só de KDE, Gnome, console, vive o FreeBSD :P, agora ele tem o Lumina. O Lumina  é um projeto de WM (<em>Window Manager</em>) da XSystem desenhado para FreeBSD, desenvolvido de uma maneira para ser portável, funcionando em várias distribuições Linux. A solução vem sendo projetada em conjunto com o PC-BSD, o qual disponibiliza versões com Lumina atualizado.

<!--more-->

Acho que o melhor trecho do <em>about</em> deste WM é o seguinte:
<blockquote>It also does not use any of the Linux-based desktop frameworks (ConsoleKit, PolicyKit, D-Bus, systemd, etc..), instead using a simple built-in interface layer for communicating directly with the operating system (which is the <a href="https://github.com/pcbsd/lumina/blob/master/libLumina/LuminaOS.h" target="_blank">only class</a> specific to the operating system – making it simple to port/customize). This allows it to obtain system information in a fast and efficient manner while ensuring desktop stability and reliability.-<a href="http://lumina-desktop.org/" target="_blank"> About Lumina</a></blockquote>
Hoje ainda uso o KDE, mas espero que tão logo este seja um projeto promissor, seguindo uma frente diferenciada aos modelos de tratamento de hardware que o <em>Linux World</em> utiliza... ...Deixando um pouco de introdução, vamos às novidades dessa ultima versão, a 0.8.7:
<h4><span style="color: #000000;">Novo sistema de interação de itens no <em>desktop</em>!</span></h4>
<ul>
	<li>Tudo agora é baseado em arrastar e soltar (<em>drag and drop</em>).</li>
	<li>Suporte a mover arquivos de aplicações externas para dentro do <em>desktop</em> (usando o padrão "text/uri-list" mimetype), ou seja, agora você consegue selecionar um arquivo do seu thunderbird ou outro programa, arrastar e soltar no desktop para gravar o arquivo.</li>
	<li>Todos os itens do <em>desktop</em> agora são alinhados dentro de um <em>grid</em> transparente, assegurando um espaçamento uniforme entre os itens.</li>
	<li>Itens para arquivos/diretórios dentro da pasta "Desktop" podem ser alterados. Eles agora possuem tamanho uniforme (e podem também ter tamanhos redimensionados de maneira individual),  necessidade de duplo clique para iniciar um item, mostrando se o item é um simples <em>link</em> para outro arquivo no sistema.</li>
</ul>
<h4><span style="color: #000000;">Gerenciador de arquivos <em>File Sight</em>, totalmente remodelado!</span></h4>
<ul>
	<li>Completamente novo, todo o <em>backend</em> do sistema foi reescrito;</li>
	<li>Suporte a navegação com múltiplos diretórios distintos dentro de abas, ou em colunas lado a lado;</li>
	<li>Arrastar e soltar arquivos de aplicações de terceiros para dentro do File Sight agora é completamente suportado;</li>
	<li>Tamanho dos ícones  pode ser ajustado de maneira independente do modo de visualização (substituindo o antigo modo <em>Icon View</em>);</li>
	<li>Suporte para múltiplas instâncias do gerenciador de arquivos utilizando apenas uma instância do <em>framework</em>/funcionalidade por padrão.</li>
	<li>Navegação de <em>snapshots</em> de arquivos do ZFS agora é suportado de maneira mais fácil e integrada dentro da navegação com um simples <em>time slider</em> dos <em>snapshots</em> quando disponíveis;</li>
	<li>Funcionalidade de navegação por imagens foi movida para uma aba separada (independente dos arquivos listados). Agora existe suporta a adição para <em>zoom in/out</em> dentro da aba do navegador de imagens;</li>
	<li>O <em>player</em> multimídia também foi movido para uma aba separada (independente da aba onde os arquivos ficam listados). Agora conseguimos tocar os arquivos de multimídia independente de onde o usuário esteja navegando nos arquivos;</li>
	<li>Esta versão do gerenciador de arquivos também obteve uma melhoria significativa de velocidade (vindos do novo <em>backend</em>), com alguns testes de resultados de navegação de arquivos, carregando 2000% vezes mais rápido que a versão anterior do programa.</li>
</ul>
<h4><span style="color: #000000;">Novos <em>plugins</em>!</span></h4>
<ul>
	<li>O <em>plugin</em> de "Menu de iniciar" disponibiliza acesso para todas as aplicações do sistema e favoritos, atalhos para as ferramentas de manutenção do sistema, acessos para algumas funcionalidades básicas do sistema (volume, brilho, <em>workspaces</em>, configurações de localização, e <em>status</em> da bateria), e opções de <em>logout</em>. Aplicações dentro do menu iniciar também possuem algumas opções adicionais: criar <em>link</em> para aplicação dentro do <em>desktop</em>, adicionar/remover aplicações do favoritos, e adicionar/remover um "lançador-rápido" do painel de botões. Este <em>plugin</em> disponibiliza uma nova alternativa para o existente "menu de aplicações", "botão do usuário", e o painel de <em>plugin</em> do "sistema de <em>dashboard</em>";</li>
	<li>Novo <em>plugin</em> painel "Linha" que é um simples separador visual de linha que pode ser adicionado entre os itens quando necessário.</li>
	<li>O <em>plugin</em> do painel de data e hora foi melhorado, e disponibilizado agora em um menu de <em>pop-up</em> com um calendário onde você pode habilitar as opções ver/mudar conforme a zona de hora que você utilizar;</li>
</ul>
<a href="/assets/wp-content/uploads/2015/10/desktop-startmenu-final.png"><img class="aligncenter size-full wp-image-3916" src="/assets/wp-content/uploads/2015/10/desktop-startmenu-final.png" alt="desktop-startmenu-final" width="1600" height="900" /></a>
<h4><span style="color: #000000;">Documentação:</span></h4>
O <a href="http://lumina-desktop.org/handbook/" target="_blank">handbook para Lumina</a> foi totalmente atualizado.  Agradecimentos especiais para Dru Lavigne por todo o trabalho com a documentação e significante reporte de bugs e testes com o Lumina.
<h4><span style="color: #000000;">Atualização:</span></h4>
Pacotes de atualizações já estão disponíveis dentro do sistema PC-BSD, e dentro da árvore do <em>ports</em> no FreeBSD(x11/lumina[-i18n]). Para outros sistemas, entre em contato com o empacotador da sua distribuição para disponibilizar novos pacotes. Para mais informações sobre disponibilidade/suporte e ou mais instruções de como instalar o Lumina diretamente dos fontes, veja o <a href="http://lumina-desktop.org/get-lumina/" target="_blank">site</a> do projeto.
<h4><span style="color: #000000;">Suporte a localização:</span></h4>
<ul>
	<li>Completo:
<ul>
	<li>US English (<em>default</em>), German, Japanese, Russian, Spanish, and Swedish.</li>
</ul>
</li>
	<li>Parcialmente completo:
<ul>
	<li>Catalan (99%), Chinese (41%), Czech (23%), Dutch (42%), Estonian (55%), French (45%), Hungarian (51%), Indonesian (62%), Korean (94%), Latvian (59%), Polish (74%), Portuguese (72%), Portuguese-Brazil (68%), and Turkish (92%).</li>
</ul>
</li>
</ul>
Para se envolver com as traduções de futuras versões, visite o site de tradução do <a href="http://translate.pcbsd.org/projects/lumina/" target="_blank">PC-BSD translate</a> para pegar as orientações! Para se manter informado sobre as traduções e seus tempos de entregas, ou agendamento das  versões, se cadastre na lista de e-mail de tradução do <a href="http://lists.pcbsd.org/mailman/listinfo/translations" target="_blank">PC-BSD translations mailing list</a>.

<span class="message_content">Se você não usa</span> FreeBSD ou PC-BSD... não chore :P tem para distro Linux... acesse <a href="http://lumina-desktop.org/get-lumina/" target="_blank">http://lumina-desktop.org/get-lumina/</a> e pegue as orientações para seu sistema.

Este texto é uma tradução com adaptações do lançamento desta versão postado no site da Lumina, o texto original se encontra em <a href="http://lumina-desktop.org/lumina-desktop-0-8-7-released/" target="_blank">http://lumina-desktop.org/lumina-desktop-0-8-7-released/</a>

Espero que tenha gostado e go go testar e até a próxima :)