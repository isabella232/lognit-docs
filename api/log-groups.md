---
layout: page
title: API de Grupos de Log
description: "Exemplos de uso"
permalink: /log-groups/
---
#{{ page.title }}

Administração de grupos de log. 

Ponto de acesso:

    http://server:port/rest/log-groups

##Listar

    $ nitr get log-groups?page=1

Retorno:

    {"data":[{"id":"ff8081813682d0a101368450a92b0018","name":"test log group","metadata":[{"key":"d","value":"e"}],"patterns":[{"expression":"c"}],"templates":[{"position":123,"property":"f"}],"filters":[{"id":"ff8081813697fd94013697ffd66c0002","expressions":[{"id":"ff8081813697fd94013697ffd66c0003","key":"a","value":"b"}]}],"spaces":["teste"]}],"total":1,"page":1,"pageSize":10}


##Inserir

Retorno:

    {"id":"ff8081813682d0a101368450a92b0018","name":"test log group","metadata":[{"key":"d","value":"e"}],"patterns":[{"expression":"c"}],"templates":[{"position":123,"property":"f"}],"filters":[{"id":"ff8081813682d0a101368450a92c0019","expressions":[{"id":"ff8081813682d0a101368450a92c001a",key:"a",value:"b"}]}],"spaces":[]}


##Obter

    $ nitr get log-groups/ff8081813682d0a101368450a92b0018


Retorno:

    {"id":"ff8081813682d0a101368450a92b0018","name":"test log group","metadata":[{"key":"d","value":"e"}],"patterns":[{"expression":"c"}],"templates":[{"position":123,"property":"f"}],"filters":[{"id":"ff8081813682d0a101368450a92c0019","expressions":[{"id":"ff8081813682d0a101368450a92c001a",key:"a",value:"b"}]}],"spaces":[]}


##Atualizar

    $ nitr put log-groups/ff8081813682d0a101368450a92b0018 -d@- << '__END__' 
    {
        name:"test log group (modified)",
        metadata: [{key:"d",value:"e"}],
        patterns: [{expression:"c"}],
        templates: [{position:123,property:"f"}],
        filters: [{expressions:[{key:"a",value:"b"}]}]
    }
    __END__


Retorno:

    {"id":"ff8081813682d0a101368450a92b0018","name":"test log group (modified)","metadata":[{"key":"d","value":"e"}],"patterns":[{"expression":"c"}],"templates":[{"position":123,"property":"f"}],"filters":[{"id":"ff8081813682d0a101368452140d001b","expressions":[{"id":"ff8081813682d0a101368452140d001c",key:"a",value:"b"}]}],"spaces":[]}

##Remover

    $ nitr delete log-groups/ff8081813682d0a101368450a92b0018

Retorno:

    {"id":"ff8081813682d0a101368450a92b0018","name":"test log group (modified)","metadata":[{"key":"d","value":"e"}],"patterns":[{"expression":"c"}],"templates":[{"position":123,"property":"f"}],"filters":[{"id":"ff8081813682d0a101368452140d001b","expressions":[{"id":"ff8081813682d0a101368452140d001c",key:"a",value:"b"}]}],"spaces":[]}


##Simulação

    $ nitr post log-groups/simulate -d@- << '__END__' 
    {
        name:"test log group",
        metadata: [{key:"d",value:"e"}],
        patterns: [{expression:"c"}],
        templates: [{position:123,property:"f"}],
        filters: [{expressions:[{key:"a",value:"b"}]}]
    }
    __END__


Retorno:

    {"channel":"/search/1664b86e-ff6d-4444-abb4-0ea039b4c36e"}

Onde "channel" é o canal do [bayeux](http://svn.cometd.com/trunk/bayeux/bayeux.html) que irá retornar os resultados correspondentes.

