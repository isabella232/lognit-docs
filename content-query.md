---
layout: page
title: Consultas por conteúdo
description: "Explicação e dicas de consultas por conteúdo no Lognit"
---

# Consultas por conteúdo

Consultas no Lognit podem ser **texto livre** ou **estruturadas**. No primeiro caso, qualquer termo pode ser utilizado como expressão de consulta. No segundo, é utilizado um par *propriedade:valor*.

O Lognit lida com algumas propriedades básicas que podem ser utilizadas na busca. Abaixo as propriedades e exemplos de consulta.

## Propriedades básicas

**date**
Data no formato yyyyMMdd
```
    date: [20120912 to 20120913]
```

**time**
Hora no formato HHmmss
```
    time: [120000 to 121000]
```

**host**
Nome do host de origem da mensagem
```
    host: server1
```

**facility**
Nome da facility do syslog
```
    facility: kernel
```

**severity**
Nome da severidade
```
    severity: debug
```

**app**
Campo "tag" do protocolo syslog, interpretado como nome da aplicação que gerou o log
```
    app: apache
```

**tags**
Hashtags capturadas da mensagem. Na mensagem *enviando #log para o lognit*, o termo *log* faz parte do campo tags
```
    tags: log
```

**text**
Qualquer palavra contida no corpo da mensagem
```
    text: out of memory
```

## Mensagens enriquecidas

Além das propriedades básicas, qualquer outra propriedade, fruto de enriquecimento das mensagens, também pode ser utilizada. 

Por exemplo, se uma mensagem tem um metadado com informação do produto, pode-se pesquisar por
```
    product: meu produto
```

## Operadores lógicos

É possível utilizar operadores lógicos na busca: **AND**, **OR** e **NOT**.

```
    text:(404 OR 500) AND time:[14 TO 15]
```

procura pelos termos *404* ou *500* somente no campo **text** que aconteceram entre as 14h e 15h (inclusive) de qualquer dia.

```
    text:(http 404) date:[20120912 TO 20120913]
```

procura pelos termos *http* e *404* somente no campo **text** que aconteceram entre os dias 12 e 13 de setembro de 2012, inclusive. Note que o operador **AND** pode ser omitido.

```
    http NOT host:server1
```

procura por todas as mensagens que contenham *http* em algum de seus campos, exceto as mensagens provenientes do host *server1*

> O sinal de subtração (**-**) pode ser utilizado em lugar da palavra **NOT** 

```
    http -host:server1
```

## Consultas por wildcard

```
    host:server*
```
procura por qualquer mensagem proveniente de um host cujo nome comece com *server*

```
    *
```
consulta todo o conteúdo disponível no Lognit