---
layout: page
title: Enviando logs para o Lognit
description: "Como enviar os logs de sua aplicação"
permalink: /sending-logs/
---

# Enviando logs para o Lognit

O Lognit recebe logs através dos protocolos [syslog](http://en.wikipedia.org/wiki/Syslog) ou [rsyslog](http://www.rsyslog.com/doc/manual.html).

Os próprios clientes destes protocolos podem ser utilizados para envio dos logs. Sistemas operacionais UNIX, por exemplo, permitem a configuração através do arquivo */etc/rsyslog.conf*.

No exemplo abaixo, todos os logs de um servidor estão sendo enviados para a porta *5140* de um servidor Lognit, pelo cliente syslog. O Lognit realiza o papel de um servidor (r)syslog na rede.

![Configurando o syslog](/public/assets/syslog_conf.png "Configurando o syslog")

Note que, enviando os logs diretamente para o Lognit, torna-se possível até mesmo a utilização de máquinas sem disco como servidores de aplicação, caso as aplicações utilizem outros servidores para armazenamento de seus dados.

> O Lognit recebe logs não só de aplicações, como de roteadores, switches, e diversos outros dispositivos, até mesmo móveis.

> É também possível configurar *log appenders* em aplicações que utilizam as mais diversas linguagens, utilizando cliente syslog para enviar as mensagens diretamente para o Lognit.
