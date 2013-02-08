---
layout: page
title: Tarefas pós-instalação
description: "O que fazer após instalar o RPM"
permalink: /post-install/
---

#{{ page.title }}

Após a instalação do pacote, é necessário configurar o Lognit pela primeira vez. Esta tarefa consiste basicamente em alterar alguns arquivos de configuração.

As principais tarefas estão descritas a seguir:

## MySQL

Instalar ou configurar um servidor MySQL 5 (local ou remoto). Para a configuração padrão, o Lognit precisa apenas de um banco "lognit" (vazio) e
um usuário com permissão para criar tabelas.

## lognit-engine.properties

    rsyslog.listener.port=514
    
Esta é a porta do protocolo syslog, o padrão é 514.

***

    index.path=data/index
    storage.path=data/store
    storage.purgePath=data/purge
    storage.compress=true

Estas propriedades configuram em que pastas serão salvos os dados de logs. São relativas à raiz da instalação.

***

    jdbc.driverClass=com.mysql.jdbc.Driver
    jdbc.url=jdbc:mysql://localhost/lognit?autoReconnect=true
    jdbc.user=lognit
    jdbc.password=
    jdbc.migrate=true

Configurações de banco de dados. Preencher com as configurações que fizerem sentido no seu ambiente. Por favor notar que se ```jdbc.migrate``` estiver habilitado,
basta existir um banco com o nome definido na URL que o sistema automaticamente criará as tabelas necessárias

## lognit-web.properties

    smtp.server=127.0.0.1
    smtp.from=lognit@intelie.net
    smtp.port=1025
    smtp.username=
    smtp.password=
    
Configurações de SMTP para envio de emails para usuários.
   
***
    
    external.url.prefix=http://localhost:9006
    
Prefixo da URL externa para composição de URLs absolutas em emails.

***

    admin.email=lognit@intelie.net
    
Email de administrador para popular nas páginas de criação de usuário.

***

    web.analyticsTrackId=

TrackID do Google Analytics.

