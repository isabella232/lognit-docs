---
layout: page
title: API de Dados Pessoais
description: "Exemplos de uso"
permalink: /me/
---
#{{ page.title }}

Informações sobre o usuário logado.

Ponto de acesso:

    http://server:port/rest/me

##Obter

    $ nitr get me

Retorno:

    {"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva","teams":[]}

##Atualizar

    $ nitr put me -d@- << '__END__' 
    {
        id: 'ff8081813682d0a10136847099300024',
        email:'test@test.com',
        displayName:'Test da Silva (modified)'
    }
    __END__

Retorno:

    {"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva (modified)","teams":[]}

