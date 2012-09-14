---
layout: page
title: Conceitos básicos
description: "Introdução e conceitos básicos do Lognit"
permalink: /intro/
---

# Conceitos básicos

O Lognit é uma ferramenta que processa e armazena possivelmente dezenas de TB de logs, permitindo consultas em tempo real e análises históricas em milésimos de segundo.

É possível realizar [consultas](/querying) no Lognit, tanto por meio de sua interface web como através de um cliente de linha de comando, o [nit](/nit).

## Formato das mensagens

As mensagens de log podem ter, opcionalmente, algumas propriedades que podem ser facilmente consultados. São elas:

* **host** nome do host que gerou a mensagem 
* **date** data da criação da mensagem, no formato yyyyMMdd
* **time** hora da criação da mensagem, no formato HHmmss
* **facility** um dos [valores definidos pelo protocolo syslog](http://en.wikipedia.org/wiki/Syslog#Facility_Levels)
* **severity** um dos [valores definidos pelo protocolo syslog](http://en.wikipedia.org/wiki/Syslog#Severity_levels)
* **app** nome da aplicação que gerou o log

Além do texto da mensagem em si, que também é indexado e pode ser consultado.

O Lognit espera receber mensagens de log no formato [syslog](http://en.wikipedia.org/wiki/Syslog). 

[Veja como fazer consultas no sistema &rarr;](/querying)

## Passo a passo do processamento

Cada mensagem de log que chega ao sistema, através do protocolo [syslog](http://en.wikipedia.org/wiki/Syslog) ou [rsyslog](http://www.rsyslog.com/doc/manual.html), passa por quatro estágios de processamento até estar disponível para qualquer consulta.

### 1. Enriquecimento do evento

O Lognit permite que sejam adicionadas propriedades, de maneira estruturada, a cada mensagem de log, tanto por meio de configurações na interface web do sistema como por meta-dados descritos na mensagem em si. Essas propriedades facilitam consultas posteriores e permitem ao usuário organizar os dados de maneira mais fácil.

[Veja mais detalhes sobre o processo de enriquecimento na ajuda da administração do Lognit &rarr;](/administrating)

### 2. Indexação

Todo o conteúdo da mensagem original e das propriedades adicionadas no primeiro passo são indexadas, o que torna a mensagem disponível para consultas por qualquer de seus termos.

### 3. Notificação de consultas em andamento

Se houver consultas realizadas no momento em que uma mensagem chega no sistema, ela é imediatamente entregue a quem está consultando, seja pela interface web, pelo [nit](http://github.com/intelie/lognit-cli), ou por meio da API que o Lognit fornece para buscas.

### 4. Armazenamento

As mensagens são armazenadas nos servidores do Lognit ou em storages remotos, o que permite que sejam acessadas em consultas históricas.


## Controle de acesso

Ao realizar uma consulta, um usuário só é notificado sobre mensagens a que tem permissão de visualização. As permissões são associadas às equipes que o usuário pertence, que são controladas pelos administradores do Lognit. 

> Administradores do sistema têm acesso a todas as mensagens de log.

[Veja mais sobre permissões na ajuda da administração do sistema &rarr;](/administrating)

## Capacidade

O Lognit é executado em uma ou mais máquinas simultaneamente. Cada um dos nós é capaz de processar mais de 20MB/s em mensagens de log originais, com escalabilidade linear. Ou seja, um cluster de 5 máquinas é capaz de processar **100MB/s** de mensagens originais.

> Dados aproximados para um servidor com 16Gb de RAM, processador i7 de 4 cores e disco rígido de 7200rpm.
