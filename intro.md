---
layout: page
title: Conceitos básicos
description: "Introdução e conceitos básicos do Lognit"
---

# Conceitos básicos

O Lognit é uma ferramenta que processa e armazena possivelmente milhares de Tb de logs, permitindo consultas em tempo real e análises históricas em milésimos de segundo.

É possível realizar [consultas](querying.html) no Lognit, tanto por meio de sua interface web como através de um cliente de linha de comando, o [nit](http://github.com/intelie/lognit-cli).

## Formato das mensagens

As mensagens de log podem ter, opcionalmente, algumas propriedades que podem ser facilmente consultados. São elas:

* **host** nome do host que gerou a mensagem 
* **date** data da criação da mensagem, no formato ddmmyyyy
* **time** hora da criação da mensagem, no formato hhmm
* **facility** um dos [valores definidos pelo protocolo syslog](http://en.wikipedia.org/wiki/Syslog#Facility_Levels)
* **severity** um dos [valores definidos pelo protocolo syslog](http://en.wikipedia.org/wiki/Syslog#Severity_levels)
* **app** nome da aplicação que gerou o log

Além do texto da mensagem em si, que também é indexado e pode ser consultado.

O Lognit espera receber mensagens de log no formato [syslog](http://en.wikipedia.org/wiki/Syslog). 
<!--<30>Aug 30 15:07:50 ubuntu dhclient: DHCPREQUEST of 10.42.1.18 on eth0 to 10.42.0.1 port 67-->

## Passo a passo do processamento

Cada mensagem de log que chega ao sistema, através do protocolo [syslog](http://en.wikipedia.org/wiki/Syslog) ou [rsyslog](http://www.rsyslog.com/doc/manual.html), passa por quatro estágios de processamento até estar disponível para qualquer consulta.

### Enriquecimento do evento

O Lognit permite que sejam adicionadas propriedades, de maneira estruturada, a cada mensagem de log, tanto por meio de configurações na interface web do sistema como por meta-dados descritos na mensagem em si. Essas propriedades facilitam consultas posteriores e permitem ao usuário organizar os dados de maneira mais fácil.

### Indexação

Todo o conteúdo da mensagem original e das propriedades adicionadas no primeiro passo são indexadas, o que torna a mensagem disponível para consultas por qualquer de seus termos.

### Notificação de consultas em andamento

Se houver consultas realizadas no momento em que uma mensagem chega no sistema, ela é imediatamente entregue a quem está consultando, seja pela interface web, pelo [nit](http://github.com/intelie/lognit-cli), ou por meio da API que o Lognit fornece para buscas.

### Armazenamento

As mensagens são armazenadas nos servidores do Lognit ou em storages remotos, o que permite que sejam acessadas em consultas históricas.


## Capacidade

O Lognit é executado em uma ou mais máquinas simultaneamente. Cada um dos nós é capaz de processar mais de 20Mb/s em mensagens de log originais, com escalabilidade linear. Ou seja, um cluster de 5 máquinas é capaz de processar 100Mb/s de mensagens originais.

> Dados aproximados para um servidor com 16Gb de RAM, processador i7 de 4 cores e disco rígido de 7200rpm.
