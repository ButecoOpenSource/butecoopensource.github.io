---
layout: wordpress
title: "Hands on: autotools"
date: 2014-10-10 00:44:22
author: marcossouza
permalink: /hands-on-autotools/
categories:
  - Desenvolvimento
  - Ferramentas
tags:
  - autotools
  - linux
  - terminal
---

Olá pessoal, a muito tempo eu queria aprender como funciona o tão famoso <em>autotools</em>. Então eu decidi pegar um projeto pessoal meu e converter meu <em>Makefile</em>, feito na mão, por um script do <em>autotools</em>. Neste tutorial vou mostrar o que eu precisei fazer para a criação do script do zero e como ele funciona, incluindo checagens por bibliotecas necessárias para compilação e outras coisas interessantes.

O <em>autotools</em>, ou o GNU Build System, é um projeto da Free Software Foundation (FSF) e tem como propósito facilitar a compilação de um projeto em diferentes ambientes <em>UNIX-like</em>. O <em>autotools</em> é um pacote com 3 ferramentas principais: <em>autoconf</em>, <em>automake</em> e <em>libtool</em>. Para mais informações sobre o <em>autotools</em> dê uma olhada na Wikipédia <a href="http://en.wikipedia.org/wiki/GNU_build_system">aqui</a>.

Se você já precisou compilar um código fonte no Linux, talvez você já tenha utilizado o <em>autotools</em> sem saber! Se você já teve de executar os seguintes passos:

<pre><code class="bash">
./configure
make
make install
</code></pre>

então o <em>autotools</em> não é mais um ser desconhecido para você.

Enquanto escrevo este artigo, encontrei este link da FSF com um <a href="http://www.gnu.org/software/automake/manual/html_node/Creating-amhello.html#Creating-amhello">hello world do autotools</a> que parece ser muito bom também.

Aviso: os conhecimentos passados neste artigo foram retirados da minha experiência em aprende-lo. Se algo estiver errado, ou algo puder ser melhor explicado, por favor, escreva nos comentários, pois o adendo ajudará outras pessoas também.

Porque usar o <em>autotools</em>? Ele facilita muito na compilação em ambientes diferentes do ambiente do desenvolvedor original do projeto. Ele contém macros onde é possível verificar se existem as bibliotecas necessárias para compilação no seu ambiente, é possível habilitar/desabilitar opções de compilação, facilidade em dizer ao desenvolvedor que está compilando o software quais as bibliotecas faltantes em seu ambiente, criação automática do arquivo Makefile entre vários outros motivos. Grandes projetos de software livre utilizam o <em>autotools</em>, como por exemplo o LibreOffice e o git. Imagine criar um Makefile para o LibreOffice, sendo que este projeto tem inúmeras possíveis configurações para serem ativadas ou desativadas em tempo de compilação. Para se ter uma ideia do tamanho do LibreOffice, seu arquivo <em>configure.ac</em>(que é o arquivo criado com macros do autoconf e automake) tem quase 13 mil linhas. Tive muitas vezes de verificar como o LibreOffice usava algumas macros do <em>autoconf</em> para poder converter meu projeto pessoal para o <em>autotools</em>, já que o LibreOffice abrange muitas opções da ferramenta.

Para iniciar nosso artigo, este era o arquivo Makefile original, feito do zero, para meu projeto pessoal:

<pre><code class="bash">
CC=g++
CXXFLAGS=-Wall -Wextra -g -lpthread -std=c++0x

# just use in case of debug
#CXXFLAGS += -DCHAT_VERBOSE

all:
        $(CC) server.cxx $(CXXFLAGS) -o server
        $(CC) client.cxx screen.c $(CXXFLAGS) -o client -lncurses

clean:
        rm server client
</code></pre>

Pode-se notar como ele é simples e objetivo. Sem verificação de bibliotecas disponíveis no ambiente, sem verificar se existe um compilador instalado. Neste exemplo, se quisermos habilitar o modo "verbose" no projeto temos de ir no arquivo Makefile e descomentar a linha que faz um append no CXXFLAGS.

Para iniciar a usar o <em>autotools</em> é necessário instalar este do repositório de sua distribuição Linux. Após instalado, é necessário criar um arquivo chamado <em>configure.ac</em>. O conteúdo deste arquivo são as configurações gerais do projeto, como por exemplo a verificação da existência de um compilador, existência de bibliotecas necessárias para compilar e possíveis parâmetros que podem ser passados ao projeto antes deste ser compilado. Estas definições são criadas utilizando macros do próprio <em>autotools</em>. Este arquivo será responsável pela geração do script <em>configure</em> com base nas macros definidas no arquivo <em>configure.ac</em>. Ao executar o script <em>configure</em>, esta irá executar as checagens de ambiente, para verificar se é possível compilar o projeto ou não. Após a execução do script <em>configure</em> sem erros então é gerado o arquivo <em>Makefile</em> para compilação do projeto.

O arquivo <em>configure.ac</em> que foi criado para substituir o antigo Makefile é este:
<script src="//gistfy-app.herokuapp.com/github/marcosps/chat/configure.ac" type="text/javascript"></script>

Explicando cada linha do arquivo <em>configure.ac</em>:

AC_INIT: Inicia o <em>autoconf</em>, que é a ferramenta que verifica os pré-requisitos para a compilação do projeto. Os parâmetros desta macro são o nome do projeto, versão do projeto, bugtracker do projeto (vazio neste caso), nome do <em>tarball</em> a ser gerado (também vazio neste caso) e página do projeto.

AC_CHECK_LIB: Faz a verificação de uma biblioteca no sistema que está compilando o projeto. Os parâmetros são o nome da biblioteca, função a ser testada nesta biblioteca, ação se encontrar a biblioteca(vazio neste caso) e ação se não encontrar a biblioteca. Neste ultimo parâmetro foi utilizada outra macro AC_MSG_ERROR. Esta macro termina a execução do script <em>configure</em> e mostra a mensagem de erro especificada.

AC_ARG_ENABLE: Adiciona parâmetro ao script. O parâmetro adicionado neste arquivo é para verificar se irá ser habilitado o modo verbose da aplicação. O parâmetro pode ser passado como --verbose, --enable-verbose=yes ou --enable-verbose=no. Isso tudo gerado automaticamente pelo <em>autoconf</em>.

AC_MSG_CHECKING: Mensagem mostrada ao usuário na execução script <em>configure</em>. Esta mensagem geralmente é utilizada para checar algum possível parâmetro passado ao script <em>configure</em>. Neste caso estamos habilitando um parâmetro "--verbose" que pode ser especificado ao executar o script <em>configure</em>. Os parâmetros usados são o nome do parâmetro e a mensagem de help. Esta mensagem é mostrada quando o programador executa "./configure --help"

AC_MSG_RESULT: Somente complementar a mensagem AC_MSG_CHECK, informando ao programador se a checagem encontrou ou não a configuração.

AC_DEFINE: Define uma variável de ambiente. No contexto do arquivo <em>configure.ac</em> em que se encontra esta macro, é verificado se foi ou não informado o parâmetro de modo "verbose".

AM_INIT_AUTOMAKE: Inicia o <em>automake</em>, que irá criar os arquivos <em>Makefile</em> para compilação do projeto. O parâmetro passado nesta macro é a versão mínima do <em>automake</em> aceita pelo script.

AC_CONFIG_FILES: Arquivos que serão gerados pelo <em>automake</em>. Neste caso terá um <em>Makefile</em> no mesmo nível do arquivo <em>configure.ac</em>, e outro dentro da estrutura de arquivos fonte.

AC_PRO_CXX: Busca um compilador CXX no ambiente.

AC_OUTPUT: Finaliza o script <em>configure.ac</em>. Neste ponto o script <em>configure</em> é gerado e está pronto para ser executado.

Quando dizemos que os arquivos serão criados pela macro, esta criação acontece somente quando o script <em>configure</em> é executado. O arquivo <em>configure.ac</em> é, como falado antes, somente uma coleção de macros para ser gerado um script <em>configure</em>.

Segundo meu entendimento, o prefixo AC se refere ao <em>autoconf</em> e o prefixo AM se refere ao <em>automake</em>.

Como foi informado na macro AC_CONFIG_FILES dois arquivos <em>Makefile</em>, precisamos criar dois arquivos <em>Makefile.am</em>. O primeiro deles é mostrado abaixo:

<script src="//gistfy-app.herokuapp.com/github/marcosps/chat/Makefile.am" type="text/javascript"></script>

A definição SUBIRS informação que existe um outro <em>Makefile</em> dentro da pasta <em>src</em>. A definição EXTRA_DIST é basicamente para incluir arquivos que não gerados pela build do projeto no <em>tarball</em> resultante. Este será explicado posteriormente.

O arquivo <em>Makefile.am</em> responsável pela compilação é mostrado abaixo:

<script src="//gistfy-app.herokuapp.com/github/marcosps/chat/src/Makefile.am" type="text/javascript"></script>

Explicando as definições deste novo artigo:

bin_PROGRAMS: Os arquivos binários que serão gerados no final da build. Neste exemplo, o nome dos binários são server e client, e estes nomes serão utilizados para especificar o que compõe cada binário.

server_SOURCES: Fontes que compõe o binário server.
 server_LDFLAGS: Flags para o linker encontrar as bibliotecas que o binário server necessita.
 server_CXXFLAGS: Flags de compilação para o binário server

O binário cliente tem exatamente as mesmas configurações e com as mesmas opções.

Alguns arquivos precisam ser criados para ser possível executar o <em>autotools</em>. Estes arquivos são somente para fins informativos do projeto caso ele seja distribuído.

O comando a seguir cria os arquivos necessários:

touch NEWS README AUTHORS COPYING INSTALL ChangeLog

Após os arquivos criados, necessitamos executar o comando que realmente utiliza o <em>configure.ac</em> e cria o script <em>configure</em> que será executado pelo desenvolvedor. O arquivo <em>autogen.sh</em> foi criado para facilitar o desenvolvedor que altera o script <em>configure.ac</em> e precisa recriar e executar o script <em>configure</em>:

<script src="//gistfy-app.herokuapp.com/github/marcosps/chat/autogen.sh" type="text/javascript"></script>

Após a execução do arquivo <em>autogen.sh</em> com sucesso é possível verificar que um arquivo <em>Makefile</em> foi criado. Executando este, será compilado os fontes dentro da pasta src e os binários server e client estarão dentro da pasta src.

Algumas coisas a mais que o <em>autotools</em> faz: existe um target no Makefile chamado dist. Este target pega seus arquivos fontes, todos aqueles arquivos relacionados a READ e demais, e cria um arquivo chat-0.01.tar.gz (neste exemplo). Você pode distribuir este arquivo compactado para outras pessoas para que estas possam compilar e usar o seu projeto. Como o arquivo <em>autogen.sh</em> não tem relação com o projeto, é necessário colocar a definição EXTRA_DIST no <em>Makefile.am</em> no mesmo nível do script <em>configure</em>. Explicado como prometido anteriormente!

Abaixo está a saída de uma execução com sucesso do script configure:

<pre><code class="bash">
[marcos@xfiles chat]$ ./configure
checking for gcc... gcc
checking whether the C compiler works... yes
checking for C compiler default output file name... a.out
checking for suffix of executables...
checking whether we are cross compiling... no
checking for suffix of object files... o
checking whether we are using the GNU C compiler... yes
checking whether gcc accepts -g... yes
checking for gcc option to accept ISO C89... none needed
checking how to run the C preprocessor... gcc -E
checking for grep that handles long lines and -e... /usr/bin/grep
checking for egrep... /usr/bin/grep -E
checking for ANSI C header files... yes
checking for sys/types.h... yes
checking for sys/stat.h... yes
checking for stdlib.h... yes
checking for string.h... yes
checking for memory.h... yes
checking for strings.h... yes
checking for inttypes.h... yes
checking for stdint.h... yes
checking for unistd.h... yes
checking ncurses.h usability... yes
checking ncurses.h presence... yes
checking for ncurses.h... yes
checking for initscr in -lncurses... yes
checking for pthread_create in -lpthread... yes
checking for a BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk... gawk
checking whether make sets $(MAKE)... yes
checking for style of include used by make... GNU
checking whether make supports nested variables... yes
checking dependency style of gcc... gcc3
checking for g++... g++
checking whether we are using the GNU C++ compiler... yes
checking whether g++ accepts -g... yes
checking dependency style of g++... gcc3
checking that generated files are newer than configure... done
configure: creating ./config.status
config.status: creating Makefile
config.status: creating src/Makefile
config.status: executing depfiles commands
</code></pre>

E a execução do <em>Makefile</em>:

<pre><code class="bash">
[marcos@xfiles chat]$ make
Making all in src/
make[1]: Entrando no diretório `/mnt/data/gitroot/chat/src'
g++ -DPACKAGE_NAME=&quot;chat&quot; -DPACKAGE_TARNAME=&quot;chat&quot; -DPACKAGE_VERSION=&quot;0.01&quot; -DPACKAGE_STRING=&quot;chat 0.01&quot; -DPACKAGE_BUGREPORT=&quot;&quot; -DPACKAGE_URL=&quot;&quot; -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DPACKAGE=&quot;chat&quot; -DVERSION=&quot;0.01&quot; -I.    -std=c++0x -g -O2 -MT server-server.o -MD -MP -MF .deps/server-server.Tpo -c -o server-server.o `test -f 'server.cxx' || echo './'`server.cxx
mv -f .deps/server-server.Tpo .deps/server-server.Po
g++ -std=c++0x -g -O2 -lpthread  -o server server-server.o
g++ -DPACKAGE_NAME=&quot;chat&quot; -DPACKAGE_TARNAME=&quot;chat&quot; -DPACKAGE_VERSION=&quot;0.01&quot; -DPACKAGE_STRING=&quot;chat 0.01&quot; -DPACKAGE_BUGREPORT=&quot;&quot; -DPACKAGE_URL=&quot;&quot; -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DPACKAGE=&quot;chat&quot; -DVERSION=&quot;0.01&quot; -I.    -std=c++0x -g -O2 -MT client-client.o -MD -MP -MF .deps/client-client.Tpo -c -o client-client.o `test -f 'client.cxx' || echo './'`client.cxx
mv -f .deps/client-client.Tpo .deps/client-client.Po
g++ -DPACKAGE_NAME=&quot;chat&quot; -DPACKAGE_TARNAME=&quot;chat&quot; -DPACKAGE_VERSION=&quot;0.01&quot; -DPACKAGE_STRING=&quot;chat 0.01&quot; -DPACKAGE_BUGREPORT=&quot;&quot; -DPACKAGE_URL=&quot;&quot; -DSTDC_HEADERS=1 -DHAVE_SYS_TYPES_H=1 -DHAVE_SYS_STAT_H=1 -DHAVE_STDLIB_H=1 -DHAVE_STRING_H=1 -DHAVE_MEMORY_H=1 -DHAVE_STRINGS_H=1 -DHAVE_INTTYPES_H=1 -DHAVE_STDINT_H=1 -DHAVE_UNISTD_H=1 -DPACKAGE=&quot;chat&quot; -DVERSION=&quot;0.01&quot; -I.    -std=c++0x -g -O2 -MT client-screen.o -MD -MP -MF .deps/client-screen.Tpo -c -o client-screen.o `test -f 'screen.cxx' || echo './'`screen.cxx
mv -f .deps/client-screen.Tpo .deps/client-screen.Po
g++ -std=c++0x -g -O2 -lncurses -lpthread  -o client client-client.o client-screen.o
make[1]: Saindo do diretório `/mnt/data/gitroot/chat/src'
make[1]: Entrando no diretório `/mnt/data/gitroot/chat'
make[1]: Nada a ser feito para `all-am'.
make[1]: Saindo do diretório `/mnt/data/gitroot/chat'
</code></pre>

Então pessoal, como foi possível verificar, o <em>autotools</em> no início parece ser complicado, mas não é. Após começar a entender como ele funciona, todo o resto acaba sendo implícito e ao finalizar seu primeiro script você se sentirá mais a vontade com esta ferramenta ao ver outros projetos a utilizando.

O <em>autotools</em> tem muitas outras opções para resolver muitos outros problemas, mas para o caso apresentado as macros utilizadas no arquivo <em>configure.ac</em> foram suficientes.

Espero que vocês tenham curtido o aprendizado do <em>autotools</em> tanto quando eu! Não se esqueça de se inscrever no nosso feed para ter em primeira mão nossos outros artigos! Um abraço!