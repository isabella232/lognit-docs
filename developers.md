---
layout: page
title: Recursos para Desenvolvedores
description: "Como utilizar a API do Lognit para realizar consultas e para administrar o sistema"
permalink: /developers/
---

# {{ page.title }}

O Lognit oferece, via HTTP e utilizando autenticação [basic auth](http://en.wikipedia.org/wiki/Basic_access_authentication), acesso à interface de consultas em tempo real e de histórico. Todas as funcionalidades do Lognit são acessíveis via API.

Os exemplos mostrados aqui usam o [nitr](/nit/#nitr) que é instalado juntamente com o [nit](/nit).

## API REST

**Recursos para todos os usuários:**

* [Consultas](/api/search)
* [Dados pessoais](/api/me)
* [Sugestão de Termos (antiga)](/api/terms) _(para auto-complete)_
* [Sugestão de Termos (nova)](/api/suggestion) _(para auto-complete)_
* [Gists](/api/gists)

**Recursos para administradores:**

* [Usuários](/api/users)
* [Grupos de Log](/api/log-groups)
* [Espaços](/api/spaces)
* [Equipes](/api/teams)
* [Estatísticas do cluster](/api/stats)
* [Pausa na indexação](/api/pause)
* [Expurgo](/api/purge)

## Realizando consultas

O servidor Lognit utiliza o protocolo [bayeux](http://svn.cometd.com/trunk/bayeux/bayeux.html) para notificar os browsers e demais clientes sobre resultados de consulta. Este protocolo é implementado em diversas linguagens, o que torna o Lognit acessível para consultas pelos mais variados clientes.

Um exemplo de cliente Lognit, em Java, é o [nit](/nit), cliente *open source* de linha de comando.

Como esta, diversas outas aplicações podem não só enviar mensagens de log, como consultar por mensagens, da própria aplicação e de outras aplicações ou dispositivos.

## Administrando o sistema

Funcionalidades como criação, edição e remoção de grupos de logs, espaços, equipes e usuários são acessíveis via REST, utilizando HTTP, também sobre autenticação básica. Com isso, é possível desenvolver scripts para automatizar ações administrativas, ou aplicações que gerenciam conteúdo segundo suas necessidades.
