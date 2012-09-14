---
layout: page
title: API de Espaços
description: "Exemplos de uso"
permalink: /spaces/
---
#{{ page.title }}

Administração de espaços.

Ponto de acesso:

    http://server:port/rest/spaces

##Listar

    $ nitr get spaces?page=1

Retorno:

    {"data":[{"id":"ff8081813697fd9401369801bc720004","name":"teste","logGroups":[{"id":"ff808181355a836601355a8648760005","name":"teste"}]}],"total":1,"page":1,"pageSize":10}

##Inserir

	$ nitr post spaces -d@- << '__END__' 
    {
        name:"teste",
        logGroups:[{id:"ff808181355a836601355a8648760005"}]
    }
    __END__


Retorno:

    {"id":"ff808181368eb86401368eca6a02000c","name":"teste","logGroups":[{"id":"ff808181355a836601355a8648760005","name":"34c09b6a-fe0e-4f22-bac9-a42845088136"}]}

##Obter

    $ nitr get spaces/ff808181368eb86401368eca6a02000c

Retorno:

    {"id":"ff808181368eb86401368eca6a02000c","name":"teste","logGroups":[{"id":"ff808181355a836601355a8648760005","name":"34c09b6a-fe0e-4f22-bac9-a42845088136"}]}

##Atualizar

    $ nitr put spaces/ff808181368eb86401368eca6a02000c -d@- << '__END__' 
    {
        name:"teste (modified)",
        logGroups:[{id:"ff808181355a836601355a8648760005"}]
    }
    __END__

Retorno:

    {"id":"ff808181368eb86401368eca6a02000c","name":"teste (modified)","logGroups":[{"id":"ff808181355a836601355a8648760005","name":"34c09b6a-fe0e-4f22-bac9-a42845088136"}]}

##Remover

    $ nitr delete spaces/ff808181368eb86401368eca6a02000c

Retorno:

    {"id":"ff808181368eb86401368eca6a02000c","name":"teste (modified)","logGroups":[{"id":"ff808181355a836601355a8648760005","name":"34c09b6a-fe0e-4f22-bac9-a42845088136"}]}
