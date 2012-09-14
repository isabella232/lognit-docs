---
layout: page
title: API de Consultas
description: "Exemplos de uso"
permalink: /search/
---
#{{ page.title }}

Interface padrão de busca no lognit.

Ponto de acesso:

    http://server:port/rest/search

##Consulta em tempo real

    $ nitr get "search?expression=*=>"

Retorno:

    {"channel":"/search/a5b24ec2-3b9b-47d8-95fe-01b50bd70cef","info":{"filter":{"valid":true},"aggregation":{"window":1000,"selectFields":[{"name":"count","type":"number","javaClass":"java.math.BigDecimal"}],"groupFields":[],"valid":true},"valid":true}}

Onde "channel" é o canal do [bayeux](http://svn.cometd.com/trunk/bayeux/bayeux.html) que irá retornar os resultados correspondentes.

Além disso, informações sobre a sintaxe da consulta são retornadas no campo "info". Caso se trate de uma consulta de agregação
(tenha o operador **=>**), informações sobre os tipos de dados envolvidos também são retornados.

##Download dos resultados de uma consulta

    $ nitr get "search/download?expression=*&text=true"

Retorno:

    ... long text file ...

