---
layout: post
title: "Guia completo de Debug em Python"
date: 2020-07-10 08:00:00
categories: Python
tags:
  - python
  - debug
permalink: guia-completo-debug-python
author: jaswdr
header:
  overlay_color: "#356fa0"
---

Uma das atividades que mais realizamos quando estamos desenvolvendo é realizar o debug para verificar algum erro ou até mesmo saber se o código esta executando da forma que gostariamos. Existem diversas técnicas e ferramentas no mundo Python para ajudar nessa tarefa, descubra algumas delas e facilite sua vida.

### PDB

A primeira ferramenta que você pode usar é o PDB, ou `Python Debugger`, este modulo que já vem como Python, tanto o 2.7 como 3+, permite que você faça coisas como, execução passo-a-passo, inspeção de variáveis e muito mais.

Para usá-lo você pode usar o comando abaixo:

```bash
# python -m pdb script.py 
> /app/script.py(1)<module>()
-> def add(x, y):
(Pdb) _

```

Ao executar o comando acima em qualquer arquivo o PDB irá carregá-lo e pausar a execução na primeira linha, nesse exemplo o arquivo está no diretório `/app` e a primeira linha do arquivo, como podemos ver, tem a declaração de uma função chamada de soma chamada `add(x,y)`, perceba que também existe um prompt de comando que na linha `(Pdb) _`, sendo `_` o local onde seu cursor está, o PDB permite o uso de diferços comandos, cada um com alguma funcionalidade que lhe ajuda na hora do debug, vamos listar todos os comandos disponíveis digitando o comando `help` e apertando a tecla `Enter`.

```bash
# python -m pdb script.py 
> /app/script.py(1)<module>()
-> def add(x, y):
(Pdb) help

Documented commands (type help <topic>):
========================================
EOF    c          d        h         list      q        rv       undisplay
a      cl         debug    help      ll        quit     s        unt      
alias  clear      disable  ignore    longlist  r        source   until    
args   commands   display  interact  n         restart  step     up       
b      condition  down     j         next      return   tbreak   w        
break  cont       enable   jump      p         retval   u        whatis   
bt     continue   exit     l         pp        run      unalias  where    

Miscellaneous help topics:
==========================
exec  pdb

(Pdb) _
```
Perceba que o PDB executa o comando e imediatamente retorna para o prompt para podermos executar novos comandos, além disso, o comando `help` imprimiu toda a lista de comandos disponíveis no PDB, veremos alguns a seguir mas caso você queira saber mais, você pode acessar a página de documentação do PDB pelo link https://docs.python.org/3/library/pdb.html.

Continuando nosso exemplo, vamos imprimir a linha atual em que estamos, para isso use o comando `list`.

```bash
(Pdb) list
  1  -> def add(x, y):
  2         return x + y
  3     
  4     
  5     if __name__ == "__main__":
  6         print(add(2, 3))
[EOF]
```

Podemos ver em nosso exemplo que foi listado a função `add` que mencionei anteriormente, assim como o resto do arquivo. Agora que sabemos onde estamos, podemos realizar uma execução passo-a-passo, para isso utilize o comando `next`.

```bash
(Pdb) next
> /app/script.py(5)<module>()
-> if __name__ == "__main__":
(Pdb) _
```

Neste exemplo o PDB parou na próxima linha a ser executada, como podemos ver é um `if` verificando a variável `__name__`, vamos continuar a execução executando novamente o comando `next`.

```bash
(Pdb) next
> /app/script.py(6)<module>()
-> print(add(2, 3))
(Pdb) _
```

Dessa vez o cursor parou na linha da chamada da função `add`, estando nessa linha podemos "entrar" na função `add` usando o comando `step`, este comando irá colocar o cursor na primeira linha da função `add`.

```bash
(Pdb) step
--Call--
> /app/script.py(1)add()
-> def add(x, y):
(Pdb) _ 
```

Agora que estamos dentro da função `add`, podemos verificar por exemplo quais foram os argumentos passados para a função, para isso usamos o comando `args`.

```bash
(Pdb) args
x = 2
y = 3
(Pdb) _
```

Como esperado, podemos ver que foram passado os valores que vimos anteriormente. Para casos onde quisermos saber o valor de uma variável também podemos usar o comando `display`.

```bash
(Pdb) display x
display x: 2
(Pdb) _
```

Enquanto estamos fazendo o debug, podemos alterar os valores das variáveis da mesma forma que escrevemos código Python.

```bash
(Pdb) x = 5
(Pdb) display x
display x: 5
(Pdb) _ 
```
É claro que qualquer alteração feita irá refletir na execução atual, por fim podemos continuar a execução até o fim com o comando `continue`.

```bash
(Pdb) continue
8
The program finished and will be restarted
> /app/script.py(1)<module>()
-> def add(x, y):
(Pdb) _
```

Por ter alterado o valor da variável `x` o código imprimiu o valor 8 ao em vez do valor esperado 5.

Porém, vão existir momentos que você não sabe exatamente a ordem em que tudo irá executar, ou até mesmo essa ordem não importa e você quer ir direto para o ponto do código de interesse, nesses casos você pode import o módulo do PDB e chamar a função `set_trace()` que irá parar a execução naquele ponto e disponibilizar o prompt do PDB para você, veja o exemplo.

```python
def add(x, y):
    import pdb; pdb.set_trace()
    return x + y


if __name__ == "__main__":
    print(add(2, 3))
```

Executando o arquivo.

```bash
# python script.py
> /app/script.py(3)add()
-> return x + y
(Pdb) _
```
Nesse ponto você tem todos os comandos do PDB disponível para debugar o código. Se quiser sair você tambêm pode usar o comando `quit`.

Veja estes e outros comandos disponíveis no modulo PDB na documentação oficial https://docs.python.org/3/library/pdb.html.

### Trace

Outro programa que pode te ajudar a entender o que está acontecendo em uma execução é o módulo `trace`. Este módulo permite que você rastreie chamadas de uma maneira mais simples, podendo verificar, por exemplo, qual ou quais arquivos e funções são chamados, a sequência em que essas funções são chamadas e outros detalhes.

Para exemplificar vamos usar o seguinte código e salvar em um arquivo `script.py`.

```python
def factorial(x):
    if x <= 1:
        return 1
    return x * factorial(x - 1)


if __name__ == "__main__":
    print(factorial(5))
```

Agora vamos verificar a sequência de chamadas com o módulo trace e a opção `--trace`.

```
# python -m trace --trace script.py 
 --- modulename: script, funcname: <module>
script.py(1): def factorial(x):
script.py(7): if __name__ == "__main__":
script.py(8):     print(factorial(5))
 --- modulename: script, funcname: factorial
script.py(2):     if x <= 1:
script.py(4):     return x * factorial(x - 1)
 --- modulename: script, funcname: factorial
script.py(2):     if x <= 1:
script.py(4):     return x * factorial(x - 1)
 --- modulename: script, funcname: factorial
script.py(2):     if x <= 1:
script.py(4):     return x * factorial(x - 1)
 --- modulename: script, funcname: factorial
script.py(2):     if x <= 1:
script.py(4):     return x * factorial(x - 1)
 --- modulename: script, funcname: factorial
script.py(2):     if x <= 1:
script.py(3):         return 1
120
```

O comando acima mostrou a sequência da execução, podemos ver que houve um total de 4 chamadas a função `factorial` e um `return`. Com isso já conseguimos entender totalmente como o programa chegou no resultado esperado.

Outra forma de obter um resultado mais condensado é usar a opção `--count`, vejamos o que acontece se executarmos em nosso script.

```bash
# python -m trace --count script.py
120
```

Aparentemente nada de mais, porém se olharmos no diretório podemos ver que foi criado um arquivo `script.cover`, este arquivo possuí (neste caso) o seguinte conteúdo.

```
    1: def factorial(x):
    5:     if x <= 1:
    1:         return 1
    4:     return x * factorial(x - 1)
       
       
    1: if __name__ == "__main__":
    1:     print(factorial(5))
```

O conteúdo do arquivo basicamente mostra algo parecido com o que vimos antes, porém de uma forma mais condensada, mostrando linha a quantidade de execuções que houveram. Perceba por exemplo que a linha `if x <= 1:` foi executada 5 vezes, a linha `return 1` foi executada somente uma, o que é esperado pois é o ponto de parada da função e por fim a linha `return x * factorial(x - 1)` foi executada 4 vezes.

Veja mais detalhes sobre o módulo `trace` na documentação oficial https://docs.python.org/3/library/trace.html#command-line-usage.

### Timeit

Em certos momentos pode ser necessário que você precise verificar o tempo de execução, isso é muito útil quando se quer otimizar o seu código, nesses casos é importante saber quanto tempo cada função está demorando, para assim não só saber quais são as partes mais lentas do código, como ter um histórico para saber se suas alterações estão melhorando o piorando a performance. Para isso que o módulo `timeit` existe.

O módulo nativo `timeit` permite você mensurar quanto tempo a execução de uma função demorou, para entender melhor vamos usar o seguinte código de exemplo:

```python
import timeit
from time import sleep


def func1():
    sleep(5)
    print("func1 done")


def func2():
    sleep(3)
    print("func2 done")


if __name__ == "__main__":
    print("Time of func1: {}".format(timeit.timeit(func1, number=1)))
    print("Time of func2: {}".format(timeit.timeit(func2, number=1)))
```

Perceba que neste código existem 2 funções, `func1` e `func2`, apesar de serem apenas exemplos você pode considerar que essas funções representam qualquer função no seu código. Nas últimas 2 linhas estamos usando a função `timeit` do módulo `timeit`, essa função recebe como parâmetro a função a ser executada, e neste exemplo estamos declarando o número de vezes que a função será executada, nesse caso 1, para determinar o tempo médio de execução. Isso é algo importante de você ter em mente pois muitas vezes haverá situações em que o código executará de forma mais rápida ou lenta, isso acontece por uma série de fatores, alguns deles não temos total controle, como a forma como que o sistema operacional aloca o processador, entre outros detalhes. Por isso é importante considerar o tempo médio das execuções ou até mesmo uma porcentagem como 99% ou 95% para excluir as exceções que tiveram uma demora muito anormal em relação ao resto.

Executando o código acima temos o seguinte resultado.

```bash
# python script.py 
func1 done
Time of func1: 5.008903064999686
func2 done
Time of func2: 3.008447170999716
```

A função `timeit` como podemos ver está retornando o tempo em segundos, apesar de ser um exemplo bastante óbvio, no dia a dia esse tempo é imprevisivel e muitas vezes é difīcil identificar qual parte do projeto ou do código esta interferindo mais na performance, o `timeit` permite não só que você saiba o tempo mas também permite que você realize testes locais para verificar se sua alteração tem melhor ou pior performance em relação a versão anterior do código, de forma simples e nativa, sem necessidade de instalar qualquer pacote.

Veja mais sobre o timeit na documentação oficial https://docs.python.org/3/library/timeit.html.

### Tracemalloc

O último módulo que vamos aprender a usar é o `tracemalloc`, este módulo tem o objetivo de fazer o rastreio do uso de mémoria, com ele você consegue saber quanto de memória o programa esta usando, e não só isso, saber quanto cada linha esta alocando.

Como de costume vamos usar o seguinte código como base.

```python
import tracemalloc


class Foo(object):
    def __init__(self):
        self.foo = "foo"


def func1():
    foo = Foo()
    print("func1 done")


def func2():
    foo = "foo"
    bar = "bar"
    print("func2 done")


if __name__ == "__main__":
    tracemalloc.start()
    before = tracemalloc.take_snapshot()
    func1()
    func2()
    after = tracemalloc.take_snapshot()
    top_stats = after.compare_to(before, 'lineno')
    print("(Malloc)")
    for stat in top_stats:
        print(stat)

```

O código acima declara duas funções, `func1` está apenas declarando uma nova instância da classe `Foo`, enquanto `func2` esta declarando uma variável do tipo string `bar`. Nas últimas linhas estamos utilizando o módulo `tracemalloc` para rastrear justamente o quanto de memória cada função esta alocando, além de estarmos criando snapshots usando a função `take_snapshot`, essa função irá criar algo como uma "fotografia" da memória no momento que o método for chamado, nesse caso estamos criando um snapshot no início e no fim, se executarmos o código podemos ver o seguinte.

```bash
# python script.py 
func1 done
func2 done
(Malloc)
script.py:24: size=416 B (+416 B), count=1 (+1), average=416 B
script.py:10: size=408 B (+408 B), count=1 (+1), average=408 B
/usr/local/lib/python3.8/tracemalloc.py:397: size=88 B (+88 B), count=2 (+2), average=44 B
/usr/local/lib/python3.8/tracemalloc.py:534: size=48 B (+48 B), count=1 (+1), average=48 B
/usr/local/lib/python3.8/tracemalloc.py:291: size=40 B (+40 B), count=1 (+1), average=40 B
```

O resultado irá mostrar as linhas que mais alocaram memória, como este exemplo é simples, não irá ter muita alocação de memória, porém vale algumas observações. Primeiro as 3 últimas linhas são do proprio modulo to tracemalloc, podemos concluir que existe o modulo tambem acaba consumindo memoria, porem normalmente isto não é um problema. Segundo podemos ver que as linhas 24 e 10 que alocaram mais memória, se olharmos o código a linha 24 é chamada da função `func2` que naquele momento havia sido alocado 416 bytes, e a linha 10 é a linha onde estamos declarando nossa instância da classe `Foo` e naquele momento havia sido alocado 408 bytes, é importante entender a função `func2` não alocou os 416 bytes, pela `func2` ser chamada após a `func1` que por sua vez estava alocando 408 bytes, isso interfere no rank e é por isso que até a linha 24 havia sido alocado 416 bytes, sendo 408 bytes da linha 10 e 8 bytes da alocação das variáveis de texto `foo` e `bar` da função `func2`.


### Conclusão

Verificamos como você pode usar uma série de módulos nativos do Python para poder fazer o debug das suas funções, performance e uso de memória. Já conhecia ou usa no dia a dia alguns deles? Comente sobre sua experiência.

Até a próxima
