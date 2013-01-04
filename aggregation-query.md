---
layout: page
title: Consultas agregadoras
description: "Explicação e dicas de consultas agregadoras no Lognit"
permalink: /aggregation-query/
---

# Consultas agregadoras

Para contar, por exemplo, quantos erros *http 404* estão ocorrendo a cada minuto, é possível escrever a consulta:

```
http 404 => count() every 1 minute
```

O que transforma uma consulta normal em uma agregação é o operador "=>". Do lado esquerdo fica a consulta, 
no mesmo formato do Lucene, já conhecido. Do lado direito, a query de agregação. No final uma agregação tem 
o seguinte formato:

```
<query> => [<agregações>] [by <agrupamentos>] [every <janela>] [if <condição>]
```

ex:

```
http => count(), avg(response_time#) by host, app every 30 seconds if count() > 10
```

_contagem e média do tempo de resposta de todos os requests http agrupados por host e app que tiveram mais de 10 erros numa janela de 30 segundos_

## Tipagem estática

Os tipos envolvidos nas agregações são fortes e estáticos. Todas as propriedades oriúndas das mensagens são, por padrão, strings. Então, para permitir operações como "avg", é preciso primeiro converter o valor em número. 
Para isso existe o operador #.

```
response_time#
```

_converte a propriedade response\_time em um número assumindo o formato americano (en-us)_

```
response_time#('pt-br')
```

_converte a propriedade response\_time em um número assumindo o formato brasileiro (pt-br)_

```
response_time#('pt-br', '###,###.##')
```

_converte a propriedade response\_time em um número assumindo o formato brasileiro (pt-br) com separadores_

A formatação segue o mesmo padrão da classe DecimalFormat, do Java.

## Sintaxes alternativas

Todas as partes da query de agregação são opcionais. Então,

```http 404 =>``` é o mesmo que: ```http 404 => count() every 1 second```

Além disso, é possível aplicar funções com uma sintaxe alternativa:

```avg(response_time#)``` é equivalente a ```response_time#:avg()``` ou ```response_time#:avg```

Isso é bastante útil para compor agregações

```
response_time#:avg:filter(response_time# > 1000)
```

_média de todos os response times na janela que sejam maiores que 1000 milisegundos_

## Reaproveitamento de expressões

É possível definir expressões nomeadas (agregações ou não) para serem reutilizadas
em agregações ou filtros. Por exemplo:

```
http => response_time# as time => time:avg, time:stdev
```

_média e desvio padrão de todos os tempos de resposta em requests http_

Quando a expressão referenciada for a primeira da última definição, é possível
omitir o nome na chamada de métodos.

```
http => response_time# => :avg, :stdev
```

## Agregações disponíveis

### Média

```
avg(<number>)
```

```
avg(response_time#)
```

Calcula a média aritmética de todos os valores recebidos na janela de tempo definida.

### Contagem

```
count([<object>])
```

```
count(http_status) ou count()
```

Conta todos os valores não-nulos e não-falsos recebidos para a expressão passada por parâmetro na janela de tempo definida.

É possível definir por exemplo:

```
count(http_status == '404')
```

### Sumarização

```
sum([<number>])
```

```
sum(response_time#)
```

Soma todos os valores numéricos recebidos na janela de tempo definida.

### Contagem de elementos distintos

```
dcount(<object>...)
```

```
dcount(user_agent, ip)
```

Conta todos os valores distintos para o conjunto de expressões passadas como parâmetro.

Para economizar memória, para mais de 64 valores distintos, a contagem passa a ser uma estimativa usando o algoritmo HyperLogLog.

### Mínimo e máximo


```
min(<comparable>) e max(<comparable>)
```

```
min(response_time#)
```

Menor (ou maior) valor recebido na janela de tempo definida.

### Primeiro e último

```
first(<object>) e last(<object>)
```

```
first(response_time#)
```

Primeiro (ou último) valor recebido na janela de tempo definida (comparado utilizando o id da mensagem de log, para ser distribuído).

### "Todos" e "algum".

```
all(<boolean>) e any(<boolean>)
```

```
all(http_status == '404')
```

Retorna true se todos os valores satisfizerem a condição especificada.

```
any(http_status == '404')
```

Retorna true se algum dos valores satisfizerem a condição especificada.


### Desvio padrão

```
stdev(<number>)
```

```
stdev(response_time#)
```

Desvio padrão de todos os valores recebidos na janela de tempo definida.

### Filtro

```
filter(<aggregation>, <condition>)
```

```
avg(response_time#):filter(response_time# > 1000)
```

Modificador que somente agrega um valor se a condição for verdadeira.

### Prev

```
prev(<aggregation>[, <number literal>])
```

```
count():prev(2)
```

Obtém o antepenúltimo resultado de agregação. 

```count():prev```

Retorna o penúltimo resultado de agregação.

```count() > count():prev```

Verifica se a contagem na janela atual é maior que na janela anterior.


### Agregações sobre agregações

Algumas agregações tem sua versão "last", que permitem aplicar uma agregação 
sobre outra. Por exemplo:

```
avglast(<numeric aggregation>, <number literal>)
```

```
count():avglast(5) 
```

Obtém a média da contagem das últimas 5 janelas.

Outras operações: ```stdevlast```, ```alllast```, ```anylast```, ```sumlast```, ```countlast```, ```minlast``` e ```maxlast```.

Ainda há outra agregação ```overlast```:

```
overlast(<aggregation>, <number literal>)
```

```
avg(response_time#):overlast(5) 
```

Que "repete" a agregação sobre as últimas n janelas. Se for uma contagem, ele 
soma as últimas janelas, se for uma média, ele faz a média (ponderada) das janelas.


## Operadores e funções disponíveis

### Operadores aritiméticos: 
    +
    - (subtração e negação)
    *
    / (divisão float)
    // (divisão inteira)
    % (resto da divisão)
    ** (exponenciação)

### Operadores de comparação:
    ==; !=; >; <; >=; <=
    
    <? (valor mínimo)
    >? (valor máximo)

### Operadores lógicos:
    &, && ou "and"
    |, || ou "or" 
    ^ ou xor
    ! ou not

Um exemplo:

```
reponse_time# > 1000 and (host == 'aaa' || host == 'bbb')
```

### Operador ternário
```
condition ? if-true, if-false
```

```
response_time < 100 ? 'great!', 'bad...'
```

Ele permite uma composição associativa à direita, como o do C++

```
response_time < 100 ? 'great!', response_time < 1000 ? 'ok.', 'bad...'
```

### Operador de coalescência de nulos:
```
<expressão> ?? <valor se for expressão for nula>
```

```
http_status ?? "000"
```

### Operador de coerção numérica
```
<string>#([<locale>[, <format>]])
```

```
response_time#('pt-br', '###,###.00')
```

### Operador de formatação numérica

```
<number>#([<locale>[, <format>]])
```

```
@size#('pt-br', '###,###.00')
```

Perceba que tem a mesma sintaxe do operador de coerção. Se o parâmetro for um número, ele formata, se for uma string,
ele faz parse.


### Potenciação e logaritmo

```
pow(<number>, <exponent>) e log(<number>, <base>)
```

### Função de formatação como bytes

```
<number>:bytes([<precision>])
```

```
@size:avg:bytes(3) 
```

_tamanho médio da mensagem formatado como bytes com 3 casas decimais. Assim, 123456 é formatado como "120.562 KB"_

## Propriedades

Todas as propriedades das mensagens de log estão disponíveis para serem consumidas pela agregação. 
As propriedades no lognit são multivaloradas, por isso, é possível prover um índice para acessar um 
valor específico de uma propriedade.

```
tag
```

_acessa o primeiro valor da propriedade "tag". O mesmo que tag[0]_

```
text[4]
```

_acessa o quinto valor da propriedade "text"_ 

Usa a mesma semântica de split que as propriedades indexadas nos log groups:

```
127.0.0.1 - frank [10/Oct/2000:13:55:36 -0700] "GET /apache/pb.gif HTTP/1.0" 200 2326
```

é separado como: 

```
0: 127.0.0.1
1: frank
2: 10/Oct/2000:13:55:36
3: 0700
4: GET
5: apache/pb.gif
6: HTTP/1.0
7: 200
8: 2326
```

Além das propriedades normais, propriedades especiais são providas para serem acessadas. Elas são prefixadas com "@". Por exemplo

```
@size
```

_acessa o tamanho (em bytes) da mensagem, este valor já é numérico e pode ser usado em agregações como ```@size:avg```_

```
@node
```

_acessa o hostname do nó do cluster que processou a mensagem, permite agregações como_

```
* => count(), @size:sum:bytes by @node
```

_retorna o número de mensagens e bytes processador por nó do cluster a cada segundo_
