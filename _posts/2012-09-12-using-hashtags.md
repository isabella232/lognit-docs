---
layout: page
title: Usando hashtags para enriquecer mensagens
description: "Dicas para desenvolvedores sobre como enriquecer mensagens enviadas para o Lognit"
category: tips
tags: [hashtag, enrich, lognit, logs, rsyslog, syslog]
---

# Utilizando hashtags (\#) para enriquecer eventos

Ao desenvolver uma aplicação, o desenvolvedor deseja ter agilidade para debugar ou analisar o comportamento da aplicação. Se fosse necessário configurar um grupo de log pela interface de administração do Lognit para algum tipo de consulta rápida, onde conhece-se o conteúdo desejado, o processo de análise de logs seria muito custoso.

É possível, no entanto, enriquecer mensagens de log automaticamente, utilizando **hashtags (\#)** nas mensagens.

![Exemplo de uso do hashtag](/public/assets/terminal_hashtag.png "Exemplo de uso do hashtag")

Usando o hashtag, o campo **tags** é enriquecido em cada mensagem enviada com o conteúdo da tag.

![Mensagem com tags](/public/assets/web_hashtag.png "Mensagem com tags")

Desta maneira, é possível filtrar o conteúdo de interesse bem mais facilmente. Esta funcionalidade serve não só para desenvolvedores, como pode ser utilizada em diversas situações para marcar mensagens de log específicas.

> É possível não só enriquecer a propriedade *tags*, como criar ou enriquecer outras propriedades, utilizando expressões como **#product:myApp** ou expressões com espaços, usando **#{product:my app}**.