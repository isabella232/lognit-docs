---
layout: page
title: Fazendo consultas
description: "Tirando o melhor proveito da interface de busca do lognit"
permalink: /querying/
---

# Realizando consultas


O Lognit permite dois tipos básicos de consulta: consultas por conteúdo e consultas agregadoras.


### [Consutas por conteúdo](/content-query)

Consultas por conteúdo podem ser realizadas utilizando tanto texto como tuplas *propriedade:valor*. 

Do primeiro caso, diz-se uma **consulta de texto livre**. Neste caso, o texto digitado servirá como base para a busca em todas as propriedades de uma mensagem, bem como no conteúdo da mensagem original de log.

Para buscar pelo termo *http*, por exemplo, basta digitar o termo no campo de busca:

```
    http
```

O segundo caso é uma **consulta estruturada**, em que a busca é realizada em propriedades específicas. Por exemplo, para obter mensagens somente do host *server1*:

```
    host: server1
```

É possível combinar consultas de texto livre e estruturadas. Por exemplo, para buscar por qualquer mensagem proveniente do host *server1* que contenha a palavra http:

```
    http AND host: server1
```

Toda consulta por conteúdo, de texto livre ou estruturada, além de estar habilitada para receber eventos em tempo real, busca mensagens em todo o conteúdo armazenado historicamente. Exceto se especificado o contrário.

> O cliente de linha de comando ([nit](http://github.com/intelie/lognit-cli)) permite distinguir entre consultas históricas e de tempo real utilizando a opção -f.

[Veja mais sobre consultas por conteúdo &rarr;](/content-query)


### [Consultas agregadoras](/aggregation-query)

Consutas agregadoras são úteis para gerar estatísicas sobre as mais diversas mensagens de log que chegam ao Lognit, bem como para limitar o número de mensagens geradas na saída de uma consulta.

Uma consulta agregadora sempre é utilizada em conjunto com uma consulta por conteúdo. Uma consulta agregadora é definida pelo operador *=>* após o termo buscado. A consulta só por este termo omite alguns parâmetros, mas é o mesmo que mostrar o número total de ocorrências dos resultados a cada segundo.

```
    http =>
```

equivale a 

```
    http => count() every 1 sec
```

Existem diversos operadores que podem ser utilizados para gerar estatísticas e agregações de informação disponível. Por exemplo, é possível consultar o número de ocorrências e o tamanho médio das mensagens que contêm http a cada minuto:

```
    http => count(), avg(@size) every 1 min
```

Toda consulta agregadora é habilitada para receber novos eventos em tempo real, porém não realiza nenhum tipo de agregação histórica.

[Veja mais sobre consultas agregadoras &rarr;](/aggregation-query)
