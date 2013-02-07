---
layout: page
title: Enviando logs a partir do Windows
description: "Como enviar os logs do Windows"
permalink: /windows/
---

#{{ page.title }}

O Lognit recebe logs através dos protocolos [syslog](http://en.wikipedia.org/wiki/Syslog) ou [rsyslog](http://www.rsyslog.com/doc/manual.html). A maior parte das aplicações contam com formas de configurar envio usando estes protocolos. Este suporte é dado por bibliotecas de logging que possuem configurações próprias. Para mais detalhes sobre essas configurações, veja [Exemplos de Configuração](/configuration-samples).

Por outro lado, o Windows em si não dá suporte a este protocolo. Logs do IIS e do Event Log não seriam enviadas. A Intelie mantém um projeto no GitHub que configura um coletor para Windows, que envia estes logs e complementa a configuração do Lognit. O código-fonte do projeto é aberto e pode ser encontrado nos seguintes links: [código-fonte](https://github.com/intelie/lognit-ftw) e [instalador](https://github.com/intelie/lognit-ftw/downloads).

Para configurar é simples, basta iniciar o instalador e a seguinte tela será exibida, pedindo informações da localização do servidor Lognit.

![Coletor Lognit For The Win](/public/assets/lognit-ftw.png "Coletor Lognit For The Win")


