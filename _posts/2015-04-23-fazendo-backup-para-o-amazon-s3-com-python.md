---
layout: wordpress
title: Fazendo backup para o Amazon S3 com Python
excerpt: |
  O Amazon Simple Storage Service (Amazon S3) oferece aos desenvolvedores e equipes de TI armazenamento de objetos seguro, durável e altamente escalonável. O Amazon S3 é fácil de usar, com uma interface de serviços da web simples para armazenar e recuperar qualquer quantidade de dados de qualquer parte da web. Com o Amazon S3, você paga apenas pelo armazenamento realmente utilizado. Não há taxa mínima nem custo de configuração.
date: 2015-04-23 07:46:32
author: alexandrevicenzi
permalink: /fazendo-backup-para-o-amazon-s3-com-python/
image: /assets/wp-content/uploads/2015/04/amazon_aws-s3.png
categories:
  - Ferramentas
tags:
  - amazon s3
  - boto
  - python
  - yaml
---

Fazer backup é algo muito importante quando se tem um site ou sistemas em produção. Existem várias formas de se fazer um backup. Você pode optar por um software, pago ou não, ou criar a sua própria ferramente ou script dependendo de sua necessidade.

Pois bem, hoje mostrarei a forma que é feito backup aqui no Buteco.

Os ingredientes para esta solução são bem simples. Temos um script em Python que faz upload para o Amazon S3.

<strong>Amazon S3</strong>

O <a href="http://aws.amazon.com/pt/s3/" target="_blank">Amazon Simple Storage Service (Amazon S3)</a> oferece aos desenvolvedores e equipes de TI armazenamento de objetos seguro, durável e altamente escalonável. O Amazon S3 é fácil de usar, com uma interface de serviços da web simples para armazenar e recuperar qualquer quantidade de dados de qualquer parte da web. Com o Amazon S3, você paga apenas pelo armazenamento realmente utilizado. Não há taxa mínima nem custo de configuração.

Optamos pelo Amazon S3, pois é um serviço bem conhecido, seguro e oferece 1 ano gratuito, com uma limitação de armazenamento.

<strong>Ferramenta utilizada</strong>

A ferramente utilizada desenvolvida por mim, é a Norris Backup. :)

O Norris esta sob licença MIT e você pode fazer o download do script <a href="https://github.com/alexandrevicenzi/norris-backup" target="_blank">aqui</a>.

<strong>Funcionalidades</strong>

O Norris permite fazer o backup de arquivos, pastas e base de dados MySQL/MariaDB. Ele foi projetado para fazer o backup do blog, basicamente Wordpress, mas é possível fazer backup de outros sistemas, tendo em vista que ele não possui nenhuma configuração específica do WP.

Suas limitações são as definidas para uso. Ele não possui suporte para outras bases de dados ainda, mas conforme a necessidade poderão ser incluídas novas funcionalidades.

Todo upload feito para os Buckets S3 são zipados. Isso economiza um pouco de espaço e facilita a organização.

<strong>Requisitos</strong>

Para usar o Norris você precisa de Python 2.7 (não testei em outras versões ainda) e as bibliotecas <a href="http://boto.readthedocs.org/en/latest/index.html" target="_blank">boto</a> e <a href="http://pyyaml.org/" target="_blank">PyYAML</a>.

O boto é uma biblioteca para acessar os serviços oferecidos pela Amazon Web Services. Você pode acessar outros recursos além do S3. Atualmente ele está disponível apenas para Python 2.6 e 2.7, porém já está sendo feito o port para Python 3.

O PyYAML é uma biblioteca para trabalhar com arquivos YAML, utilizado para a configuração de algumas partes do Norris.

<strong>Usando o boto</strong>

A parte mais simples, com toda certeza, é fazer o upload de um arquivo para um Bucket. Como você pode observar abaixo, não existe mistério algum.

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/boto-s3/s3_upload.py" type="text/javascript"></script>

A classe <em>S3Connection</em> é a responsável por todo o trabalho de upload. O construtor dela pode ser de duas formas:

<code>conn = S3Connection()</code>

Ou:

<code>conn = S3Connection('aws access key', 'aws secret key')</code>

Ou ainda:

<code>boto.connect_s3()</code>

A primeira e a terceira esperam que as variáveis de ambiente AWS_ACCESS_KEY_ID e AWS_SECRET_ACCESS_KEY possuam a chave e o segredo para acesso. Já a segunda você passa manualmente <em>hard-code</em>. Para obter uma chave de acesso visite <a href="http://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSGettingStartedGuide/AWSCredentials.html" target="_blank">este link</a>.

Após conectado, devemos escolher um Bucket para fazer o upload. A escolha pode ser de duas formas:

<code>bucket = conn.get_bucket('nome_bucket')</code>

Ou:

<code>bucket = conn.create_bucket('nome_bucket')</code>

A primeira espera que o Bucket já esteja criado. Já a segunda cria um Bucket. A segunda opção lançará uma exceção caso o nome do Bucket já exista.

Após escolher um Bucket vamos fazer o upload do arquivo. Para isto precisamos criar uma <em>Key</em>, conforme abaixo:

<code>k = Key(bucket)</code>

Toda <em>Key</em> é chave/valor. Ou seja, nome_arquivo/arquivo. Não necessariamente apenas um arquivo, você pode armazenar qualquer coisa que desejar.

A atribuição de chave/valor funciona da seguinte forma:

<code>k.key = 'nome_arquivo.txt'
 k.set_contents_from_filename('nome_arquivo.txt')</code>

key é a chave única que deve ser atribuída para fazer o upload. set_contents_from_filename faz o trabalho duro do upload. Este método não é recomendado para arquivos muito grandes. Para isto devemos fazer o upload em diversas partes. Conforme abaixo:

<script src="//gistfy-app.herokuapp.com/github/ButecoOpenSource/boto-s3/s3_large_upload.py" type="text/javascript"></script>

Esta parte do código dispensa comentários adicionais, como você pode observar os comentários estão no fonte acima.

Se você possui interesse em conhecer os demais métodos para manipulação de um Bucket no S3, confira a <a href="http://boto.readthedocs.org/en/latest/s3_tut.html" target="_blank">documentação introdutória do boto</a> (Inglês).

Por hoje é isso.

Nas próximas publicações comentarei sobre o uso do YAMP para criação de arquivos de configurações e darei continuidade aos demais métodos do boto disponíveis para o S3.