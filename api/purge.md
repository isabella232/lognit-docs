---
layout: page
title: API de Expurgo
description: "Exemplos de uso"
permalink: /purge/
---
#{{ page.title }}

##Expurgando por query

	$ nitr post purge -d 'expression=*' -d all=true

Retorno:

	{"id":"d8938124-035e-4d40-a99d-38e59b77da2d"}

Onde "id" é o id da tarefa enfileirada.

##Obtendo estado de uma tarefa pendente:

	$ nitr get purge/d8938124-035e-4d40-a99d-38e59b77da2d

Retorno:

	{"status":"COMPLETED","message":"purge 460 files matching (search \u0027*\u0027: 20000000 items down)","purged":460,"failed":0,"expected":460}

##Revertendo expurgo

	$ nitr post purge/unpurge -d all=true

Retorno:

	{"id":"9f823d1a-4038-4a84-88c7-14bfce8e501e"}

Onde "id" é o id da tarefa enfileirada.

##Cancelando tarefa em execução

	$ nitr post purge/cancel/d8938124-035e-4d40-a99d-38e59b77da2d

Sem retorno.

##Cancelando TODAS as tarefas em execução (emergência)

	nitr post purge/cancel-all

Sem retorno.


