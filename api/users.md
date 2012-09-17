---
layout: page
title: API de Usuários
description: "Exemplos de uso"
permalink: /users/
---
#{{ page.title }}

Administração de usuários. 

Ponto de acesso:

    http://server:port/rest/users

##Listar

    $ nitr get users?page=1

Retorno:

    {"data":[{"id":"f478d640307946398d0b81c74bbe0761","email":"lognit@intelie.net","displayName":"Administrator","teams":[]},{"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva","teams":[]}],"total":2,"page":1,"pageSize":10}


##Inserir

    $ nitr post users -d@- << '__END__' 
    {
        email:'test@test.com',
        displayName:'Test da Silva'
    }
    __END__

Retorno:

    {"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva","teams":[]}

##Obter

    $ nitr get users/ff8081813682d0a10136847099300024

Retorno:

    {"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva","teams":[]}

##Atualizar

    $ nitr put users/ff8081813682d0a10136847099300024 -d@- << '__END__' 
    {
        id: 'ff8081813682d0a10136847099300024',
        email:'test@test.com',
        displayName:'Test da Silva (modified)'
    }
    __END__

Retorno:

    {"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva (modified)","teams":[]}

##Remover

    $ nitr delete users/ff8081813682d0a10136847099300024

Retorno:

    {"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva (modified)","teams":[]}
