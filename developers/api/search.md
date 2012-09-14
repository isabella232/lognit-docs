---
layout: page
title: API de Busca
description: "Exemplos de uso"
permalink: /search/
---
#{{ page.title }}

Interface padrão de busca no lognit.

Ponto de acesso:

    http://server:port/rest/search

##Busca em tempo real

    $ nitr get "search?expression=*=>"

Retorno:

    {"channel":"/search/a5b24ec2-3b9b-47d8-95fe-01b50bd70cef","info":{"filter":{"valid":true},"aggregation":{"window":1000,"selectFields":[{"name":"count","type":"number","javaClass":"java.math.BigDecimal"}],"groupFields":[],"valid":true},"valid":true}}

Onde "channel" é o canal do [bayeux](http://svn.cometd.com/trunk/bayeux/bayeux.html) que irá retornar os resultados correspondentes.

##Download dos resultados de uma busca

    $ nitr get "search/download?expression=*&text=true"

Retorno:

    ... long text file ...

