---
layout: page
title: API de Sugestão de Termos
description: "Exemplos de uso"
permalink: /terms/
---
#{{ page.title }}

Sugestão de termos para _auto-complete_.

Ponto de acesso:

    http://server:port/rest/terms

##Sugerindo um termo

    $ nitr get "terms?field=&term=test&size=20"

Retorno:

	{"terms":["host:test1","host:test2","host:test3","host:test4","host:test5","host:test6","host:test7","host:test8","text:test"]}


