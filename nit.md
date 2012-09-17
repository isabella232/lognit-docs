---
layout: page
title: Lognit Command Line Interface (nit)
description: "Acessando a API rest do lognit a partir da linha de comando"
permalink: /nit/
---
#{{ page.title }}

_Lognit Command Line Interface_, ou somente **nit**, é um cliente alternativo para o Lognit. Utiliza a mesma API da interface web para disponibilizar grande parte dos serviços de busca do Lognit. O nit é _open-source_ e está disponível no [GitHub do projeto](http://github.com/intelie/lognit-cli).

![Exemplo de busca com o nit](/public/assets/search_nit.png "Estatísticas com o nit")

## Instalação

Para instalar a última versão disponível, execute no terminal:

    sudo sh < <(curl -s https://raw.github.com/intelie/lognit-cli/master/install)

Para instalar alguma versão mais antiga, especifique a versão com **-s**.

    sudo sh -s 1.0 < <(curl -s https://raw.github.com/intelie/lognit-cli/master/install) 

## Primeiros passos.

Antes de começar a usar o nit, é preciso efetuar login no servidor do Lognit.

O login pode ser efetuado definindo o servidor a se conectar:

    nit -s lognit-server

O cliente irá solicitar usuário e senha. Caso deseje especificá-los na linha de comando, faça como no exemplo:

    nit -s lognit-server -u usuario -p senha

## Realizando consultas

Para efetuar uma consulta histórica no Lognit, basta específica o texto da consulta na linha de comando. Assim:

    nit 'group:http status:4?? NOT status:403'

### nit -n

Por padrão, somente os 20 resultados mais recentes são retornados numa busca histórica. Para definir quantos resultados devem ser retornados, use a opção **-n**:

    nit 'group:http status:4?? NOT status:403' -n 100

### nit -f (follow)

Uma busca comum será efetuada somente nos registros históricos do lognit. Para acompanhar os resultados em tempo real, use a opção **-f**:

    nit 'group:http status:4?? NOT status:403' -f


### nit -d (download)

Para fazer download de **todos** os resultados de uma consulta, use a opção **-d**. O resultado será escrito na _saída padrão_. Redirecione para um arquivo ou pipe, caso deseje. Tenha em mente que pode demorar bastante.

    nit 'group:http status:4?? NOT status:403' -d > download.txt

### nit -o (output)

Os resultados de uma consulta são exibidos como texto colorido, por padrão. Para mudar o formato de saída, use a opção **-o**:

    nit 'group:http status:4?? NOT status:403' -o json

É possível, inclusive, redirecionar a saída para uma instalação do [Intelie Event Manager](http://www.intelie.com/products/iem). Para tanto, use a sintaxe:

    nit 'group:http status:4?? NOT status:403' -o iem://iem-server/EventType

### nit -b (bars)

Se estiver interessado somente em estatísticas sobre uma consulta, utilize a opção **-b**.

    nit 'group:http status:4?? NOT status:403' -b

![Estatísticas com o nit](/public/assets/stats_nit.png "Estatísticas com o nit")

## Lognit REST client (nitr) <a name="nitr">&nbsp;</a>

Ao instalar o nit, também é instalado o comando **nitr**. O nitr é tem como propósito facilitar o acesso à API REST do Lognit. É basicamente um [curl](http://curl.haxx.se/) que compartilha a sessão conectada do nit.

O uso básico é:

    nitr <verb> <resource> [<arguments>]

Por exemplo:

    $ nitr get me/welcome
    {"message":"Welcome Administrator!"}

Por baixo dos panos, o que acontece é algo parecido com:

    curl -X get -s -L -H 'Content-Type:application/json' \ 
         -b ~/.lognit/state "http://${server}/rest/me/welcome"


Você pode combinar com outras opções também disponíveis no curl.

    $ nitr post pause -d all=true

