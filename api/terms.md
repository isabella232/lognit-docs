---
layout: page
title: API de Sugestão de Termos
description: "Exemplos de uso"
permalink: /terms/
---
#{{ page.title }}

##Sugerindo um termo

    $ nitr get "terms?field=&term=test&size=20"

Retorno:

	{"terms":["host:test1","host:test2","host:test3","host:test4","host:test5","host:test6","host:test7","host:test8","text:test"]}


