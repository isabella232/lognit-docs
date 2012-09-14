---
layout: page
title: API de Pausa na Indexação
description: "Exemplos de uso"
permalink: /pause/
---
#{{ page.title }}

##Pausando todas as instâncias

	$ nitr post pause -d all=true

That returns:

	{"count":1}

Onde "count" é o número de nós do Lognit que foram pausados.

##Continuar indexação em todas as instâncias

	$ nitr post pause/resume -d all=true

Retorno:

	{"count":1}

Onde "count" é o número de nós do Lognit que continuaram a indexação.

