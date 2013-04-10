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

    
##Listar usuários visíveis

Usado para obter informações de todos os usuários que façam parte de alguma equipe que o usuário também faz parte.

É equivalente a ```get users``` caso o usuário seja administrador.

    $ nitr get me/visible-users?page=1

Retorno:

    {"data":[{"id":"f478d640307946398d0b81c74bbe0761","email":"lognit@intelie.net","displayName":"Administrator","teams":[]},{"id":"ff8081813682d0a10136847099300024","email":"test@test.com","displayName":"Test da Silva","teams":[]}],"total":2,"page":1,"pageSize":10}


É possível também utilizar as opções ```filterExpr```, ```sortProperty``` e 
```sortDirection``` para filtrar e ordenar os registros. 

A opção ```filterExpr``` filtra os registros pelas propriedades ```email``` ou
```displayName```.

Quando ```sortProperty``` está preenchida, ```sortDirection``` menor que zero
inverte a ordem da ordenação.



