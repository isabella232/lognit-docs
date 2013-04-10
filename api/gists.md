---
layout: page
title: API de Gists
description: "Exemplos de uso"
permalink: /gists/
---
#{{ page.title }}

Administração de grupos de log. 

Ponto de acesso:

    http://server:port/rest/gists

##Listar

Obtem todos os gists **criados** pelo usuário atual.

    $ nitr get gists?page=1

Retorno:

    {"data":[{"id":"ff8081813df4e6b3013df4ea183f0001","description":"Test Description","text":"Test Text","owner":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365613875017,"watchers":[{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}],"comments":[]}],"total":1,"page":1,"pageSize":15}

É possível também utilizar as opções ```filterExpr```, ```sortProperty``` e 
```sortDirection``` para filtrar e ordenar os registros. 

A opção ```filterExpr``` filtra os registros pela propriedade ```name```.

Quando ```sortProperty``` está preenchida, ```sortDirection``` menor que zero
inverte a ordem da ordenação.

##Listar gists criados ou acompanhados
k
Obtem todos os gists que o usuário atual criou ou acompanha.

    $ nitr get gists/watching?page=1

Retorno:

    {"data":[{"id":"ff8081813df4e6b3013df4ea183f0001","description":"Test Description","text":"Test Text","owner":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365613875017,"watchers":[{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}],"comments":[]}],"total":1,"page":1,"pageSize":15}

*Todas as opções da seção anterior também se aplicam.*

##Inserir

    $ nitr post gists -d@- << '__END__' 
    {
        description:"Test Description",
        text:"Test Text" 
    }
    __END__

Retorno:

    {"id":"ff8081813df4e6b3013df4ea183f0001","description":"Test Description","text":"Test Text","owner":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365613615168,"watchers":[{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}],"comments":[]}
    
##Obter

    $ nitr get gists/ff8081813df4e6b3013df4ea183f0001

Retorno:

    {"id":"ff8081813df4e6b3013df4ea183f0001","description":"Test Description","text":"Test Text","owner":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365613615168,"watchers":[{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}],"comments":[]}

##Atualizar

    $ nitr put gists/ff8081813df4e6b3013df4ea183f0001 -d@- << '__END__' 
    {
        description:"Test Description 2",
        text:"Test Text 2" 
    }
    __END__

Retorno:

    {"id":"ff8081813df4e6b3013df4ea183f0001","description":"Test Description 2","text":"Test Text 2","owner":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365613615168,"watchers":[{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}],"comments":[]}


##Remover

    $ nitr delete gists/ff8081813df4e6b3013df4ea183f0001

Retorno:

    {"id":"ff8081813df4e6b3013df4ea183f0001","description":"Test Description","text":"Test Text","owner":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365613615168,"watchers":[{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}],"comments":[]}

##Inserir comentário

    $ nitr post gists/ff8081813df4e6b3013df4ea183f0001/comments -d@- << '__END__' 
    {
        text:"Test Comment" 
    }
    __END__
    
Retorno:

    {"id":"ff8081813df4e6b3013df4f1fc100003","text":"Test Comment","user":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365614132240}

##Editar comentário

    $ nitr put gists/ff8081813df4e6b3013df4ea183f0001/comments/ff8081813df4e6b3013df4f1fc100003 -d@- << '__END__' 
    {
        text:"Test Comment 2" 
    }
    __END__
    
Retorno:

    {"id":"ff8081813df4e6b3013df4f1fc100003","text":"Test Comment 2","user":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365614132240}

##Remover comentário

    $ nitr delete gists/ff8081813df4e6b3013df4ea183f0001/comments/ff8081813df4e6b3013df4f1fc100003

Retorno:
    
    {"id":"ff8081813df4e6b3013df4f1fc100003","text":"Test Comment","user":{"email":"lognit@intelie.net","displayName":"Administrator","id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"},"dateCreated":1365614132240}

##Acompanhar

    $ nitr post gists/ff8081813df4e6b3013df4ea183f0001/watchers
    
Retorno:
    
    {"id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}
    
##Fazer um usuário específico acompanhar

    $ nitr post gists/ff8081813df4e6b3013df4ea183f0001/watchers/f478d640307946398d0b81c74bbe0761
    
Retorno:
    
    {"id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}
        
##Fazer um usuário deixar de acompanhar

    $ nitr delete gists/ff8081813df4e6b3013df4ea183f0001/watchers/f478d640307946398d0b81c74bbe0761
    
Retorno:
    
    {"id":"f478d640307946398d0b81c74bbe0761","name":"Administrator"}




