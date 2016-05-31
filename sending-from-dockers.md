---
layout: page
title: Enviando logs de Dockers
description: "Como enviar os logs de containers com valor de tag maior que 32 caracteres"
permalink: /sending-from-dockers/
---

# Enviando logs de Dockers

Ao enviar logs de dockers, com valor de tag maior que 32 caracteres, gera um erro.

Para resolver o problema, use a configuração abaixo no arquivo */etc/rsyslog.conf*

    template (name="LongTagForwardFormat" type="string" string="<%PRI%>%TIMESTAMP:::date-rfc3164% %HOSTNAME% %syslogtag%%msg:::sp-if-no-1st-sp%%msg%")

    *.*  @@lognit.intelie:5140;LongTagForwardFormat