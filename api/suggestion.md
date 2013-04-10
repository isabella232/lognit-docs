---
layout: page
title: API de Sugestão de Termos (nova)
description: "Exemplos de uso"
permalink: /suggestion/
---
#{{ page.title }}

Sugestão de termos para _auto-complete_. Esta API sugere queries inteiras, não somente termos como a API antiga.

Ponto de acesso:

    http://server:port/rest/suggestion

##Sugerindo um termo

    $ nitr get suggestion?query=some+text+before+host:

Retorno:

	{"termsData":[{"base":"some text before ","suggestion":"host:192.0.0.1"},{"base":"some text before ","suggestion":"host:localhost"},{"base":"some text before ","suggestion":"host:test1"},{"base":"some text before ","suggestion":"host:test2"},{"base":"some text before ","suggestion":"host:test3"},{"base":"some text before ","suggestion":"host:test4"},{"base":"some text before ","suggestion":"host:test5"},{"base":"some text before ","suggestion":"host:test6"},{"base":"some text before ","suggestion":"host:test7"},{"base":"some text before ","suggestion":"host:test8"}],"recordData":{"data":[],"total":0,"page":1,"pageSize":10},"byTagsData":{"data":[],"total":0}}


