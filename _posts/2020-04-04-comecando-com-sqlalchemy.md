---
layout: wordpress
title: Começando com SQL Alchemy
excerpt: |
  Acessando bancos relacionais e criando modelos ORM de forma fácil no Python
date: 2020-04-04 19:27:00
author: jaswdr
permalink: /comecando-com-sqlalchemy/
image: /assets/wp-content/uploads/2020/04/capa-sqlalchemy.jpg
categories:
  - Python
tags:
  - database
---

​	Diversas aplicaçōes escritas na linguagem Python precisam armazenar dados relacionais, usando bancos de dados como PostgreSQL, MySQL, Oracle e outros, o projeto `sqlalchemy` visa facilitar a conexão e manipulação de registros, veja a seguir como utilizar este projeto.

## Instalação

Para realizar a instalação do pacote basta executar:

```python
$ pip install sqlalchemy
```

Após finalizar o download e instalação você verificar a instalação pelo python, executando:

```python
$ python3
>>> import sqlalchemy
>>> sqlalchemy.__version__
'1.3.13'
```

## Conectando e executando queries

Para conectar a um banco de dados suportado pelo sqlalchemy (PostgreSQL, MySQL, SQLite, Oracle ou Microsoft SQL Server) precisamos criar uma istância de `Engine`, este objeto servirá para criarmos nossas sessões de conexão com o banco.

```python
from sqlalchemy import create_engine
engine = create_engine("sqlite:///file.db")
```

No exemplo acima, estamos criando uma instância de `Engine` com o `sqlite`, caso você queira conectar com outro banco, veja a [documentação](https://docs.sqlalchemy.org/en/13/dialects/index.html).

Uma vez que temos nossa engine podemos começar a criar nossas sessões.

```python
from sqlalchemy.orm import sessionmaker
Session = sessionmaker(bind=engine)
session = Session()
```

Finalmente com nossa sessão conseguimos executar comandos SQL, como por exemplo criar um tabela de usuários.

```python
session.execute('CREATE TABLE users('
               	'id INT '
               	'name VARCHAR '
               	'email VARCHAR)')
```

Inserir dados.

```python
session.execute('INSERT INTO "users" (id, name, email) VALUES '
               '(1, \'admin\', \'admin@example.com\') ')
session.execute('INSERT INTO "users" (id, name, email) VALUES '
               '(2, \'user\', \'user@example.com\') ')
session.execute('INSERT INTO "users" (id, name, email) VALUES '
               '(3, \'client\', \'client@sample.com\') ')
```

Por fim podemos buscar dados.

```python
result = session.execute('SELECT * FROM users')
for row in result:
    print(row)
#(1, 'admin', 'admin@example.com')
#(2, 'user', 'user@example.com')
#(3, 'client', 'client@sample.com')
```

## ORM

Além de poder se executar comandos SQL o `sqlalchemy` também possuí um pacote de ORM (Object-relational mapping ) que basicamente permite mapear as tabelas do banco em classes e objetos de forma fácil e pratica. Para exemplificar vamos continuar a usar nosso exemplo anterior da tabela de usuários, primeiro vamos deletar a tabela.

```python
session.execute('DROP TABLE users')
```

Agora vamos criar uma classe para representar nossos usuários, a documentação do `sqlalchemy` sugere criar uma classe base para todos os nossos "modelos" usando a função `declarative_base()` do pacote `sqlalchemy.ext` conforme o exemplo abaixo.

```python
from sqlalchemy.ext.declarative import declarative_base
Base = declarative_base()
```

Com a classe `Base` conseguimos criar nossos modelos, ou classes que representarão nossas tabelas e dados, veja um exemplo de como criar um modelo.

```python
from sqlalchemy import Column, Integer, String

class User(Base):
    __tablename__ = 'users'
    
    id = Column(Integer, primary_key=True)
    name = Column(String(255), nullable=False)
    email = Column(String, nullable=False)
```

Como pode-se ver no exemplo, quando se utiliza o ORM do sqlalchemy os atributos da classe são inicializados com instâncias de `sqlalchemy.Column`, no caso estamos criando colunas de "id", "name" e "email", cada um destes atributos será uma coluna na tabela gerada, com opções de `primary_key` para a chave primária da tabela e `nullable` para indicar que os valores são obrigatórios. Além disso o atributo `__tablename__` é obrigatório para indicar o nome da tabela.

Uma vez montado nosso primeiro modelo de usuário podemos gerar toda a estrutura do banco usando um método utilitário da classe `Base` que criamos.

```python
Base.metadata.create_all(engine)
```

Caso o comando acima execute com sucesso é esperado termos agora uma tabela `users` representado pela nossa classe, com isso podemos da mesma forma que anteriormente adicionar alguns usuários.

```python
admin = User(id=1, name='admin', email='admin@example.com')
user = User(id=2, name='user', email='user@example.com')
client = User(id=3, name='client', email='client@sample.com')

session.add(admin)
session.add(user)
session.add(client)

session.commit()
```

Nesse exemplo estamos criando 3 usuários (admin, user e client) e adicionando eles a nossa sessão atual, dessa forma que rastreamos a criação de novos objetos e alterações feitas nestes objetos, após executar o código acima podemos realizar queries para buscar todos os usuários.

```python
users = session.query(User).all()
for user in users:
    print(user.name)
# admin
# user
# client
```

Perceba a forma como buscamos os usuários com o método `query` passando como parâmetro a entidade que queremos, no caso `User`, a forma acima irá buscar todos os usuários sem filtro algum, podemos filtrar a busca com o método `filter()`.

```python
no_admin_users = session.query(User).filter(User.name != 'admin')
for user in no_admin_users:
    print(user.id, user.name)
# 2 user
# 3 client
```

Podemos utilizar filtros da mesma forma que utilizamos em comandos `if`, `while` e outros, podendo retornar todos os resultados com a opção `all()` ou retornar apenas um registro.

```python
admin_user = session.query(User).filter(User.name == 'admin').one()
```

Para retornar apenas um registro podemos utilizar tanto o método `one()` quanto o método `one_or_none()`, a diferença entre os 2 métodos é que o primeiro irá disparar uma exceção caso nenhum registro for encontrado, enquanto o segundo retornará `None`.

> Para saber a lista completo de operadores veja a [documentação](https://docs.sqlalchemy.org/en/13/orm/tutorial.html#common-filter-operators)

Além de inserir e realizar buscas é possível fazer alterações facilmente, basta utilizar a referência ao objeto, alterar os atributos e adicionar a sessão, conforme o exemplo abaixo.

```python
admin_user.email = 'admin@new.com'
session.add(admin_user)
session.commit()
```

Dessa forma conseguimos facilmente alterar nosso banco, podemos também excluir os registros com o método `delete()`.

```python
session.delete(admin_user)
session.commit()
```

Seguindo o mesmo padrão, adicionando os objetos que queremos excluir a sessão e executando o `commit()` para enviar as alterações.

## Conclusão

O `sqlalchemy` possuí um conjunto de opções que tanto facilitam trabalhar com bancos relacionais como dão flexibilidade de executar comandos SQL ou criar modelos utilizando o pacote ORM. Você já utilizou esse pacote? Utiliza algum outro meio para se comunicar com seu banco? Possuí alguma dúvida? comente abaixo.
