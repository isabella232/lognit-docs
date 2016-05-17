---
layout: page
title: Enviando logs em formato json
description: "Como enviar os logs em formato json"
permalink: /sending-logs-json/
---

# Enviando logs em formato json

Ao enviar logs, você pode configurar para enviar em formato json.
Adicione a configuração abaixo no arquivo */etc/rsyslog.conf*

    template(name="tcpinput" type="list") {
        constant(value="{")
          constant(value="\"timestamp\":\"")
          property(name="timereported" dateFormat="rfc3164")

          constant(value="\",\"host\":\"")
          property(name="hostname")

          constant(value="\",\"severity\":\"")
          property(name="syslogseverity-text")

          constant(value="\",\"facility\":\"")
          property(name="syslogfacility-text")

          constant(value="\",\"tag\":\"")
          property(name="syslogtag" format="json")

          constant(value="\",\"message\":\"")
          property(name="msg" format="json")

          constant(value="\",\"__type\":\"Syslog\"")
        constant(value="\"}\n")
    }
    *.* @@live.intelie:17042;tcpinput