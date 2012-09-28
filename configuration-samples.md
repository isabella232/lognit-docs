---
layout: page
title: Exemplos de configuração
description: "Exemplos de configuração para diferentes linguagens."
permalink: /configuration-samples/
---

Exemplos de configuração
========================

# Java

Exemplo de configuração para o Log4j

## properties
    log4j.rootLogger=INFO, SYSLOG
    log4j.appender.SYSLOG=org.apache.log4j.net.SyslogAppender
    log4j.appender.SYSLOG.syslogHost=localhost
    log4j.appender.SYSLOG.layout=org.apache.log4j.PatternLayout
    log4j.appender.SYSLOG.layout.ConversionPattern=MY-APPLICATION [%c] %m%n
    log4j.appender.SYSLOG.Header=true
    log4j.appender.SYSLOG.Facility=LOCAL2


    <appender name="syslog" class="org.apache.log4j.net.SyslogAppender">
        <!--<param name="Threshold" value="INFO"/>-->
        <param name="syslogHost" value="localhost"/>
        <param name="Header" value="true"/>
        <param name="Facility" value="LOCAL2"/>
        <layout class="org.apache.log4j.PatternLayout">
            <param name="ConversionPattern" value="MINHA-APLICACAO [%c] %m%n"/>
        </layout>
    </appender>

_OBS: Para log4j em versões anteriores à 1.2.15 é necessário colocar o hostname como parâmetro antes da "MINHA-APLICACAO"_


# Python

RTFM: [http://docs.python.org/library/logging.handlers.html#sysloghandler](http://docs.python.org/library/logging.handlers.html#sysloghandler)

## Exemplo:

    import logging
    from logging.handlers import SysLogHandler

    logger = logging.getLogger()
    logger.setLevel(logging.INFO)
    syslog = SysLogHandler(address='/dev/log',facility=logging.handlers.SysLogHandler.LOG_LOCAL3)
    formatter = logging.Formatter('APP_NAME: %(name)s %(message)s')
    syslog.setFormatter(formatter)
    logger.addHandler(syslog)


_ATENÇAO!!! Não é preciso configurar o formatter do módulo de logging para logar o timestamp e nível do log (debug, info e etc). Isto já será feito pelo próprio syslog. Alterar o APP_NAME pelo nome da sua aplicação para que ela seja logada. As mensagens devem ser logadas como string e não unicode_

## Python - Django

A partir da versão 1.3 o django fornece uma nova api de logging. A documentação está em https://docs.djangoproject.com/en/dev/topics/logging/

A configuração fica no seu arquivo de settings.py. Um exemplo de configuração é mostrado abaixo.

    LOGGING = {
        'version': 1,
        'disable_existing_loggers': True,
        'formatters': {
            'verbose': {
                'format': '[%(asctime)s] %(levelname)s [%(module)s] %(message)s'
            },
            'simple': {
                'format': '%(levelname)s %(message)s'
            },
            'syslog': {
                'format': 'APP_NAME: %(name)s %(message)s'
            },
        },
        'handlers': {
            'default': {
                'level':'DEBUG',
                'class':'logging.handlers.RotatingFileHandler',
                'filename': 'logs/app.log',
                'maxBytes': 1024*1024*20, # 20 MB
                'backupCount': 30,
                'formatter':'verbose',
            },
            'syslog': {
                'level':'DEBUG',
                'class':'logging.handlers.SysLogHandler',
                'facility':'logging.handlers.SysLogHandler.LOG_LOCAL3',
                'formatter':'syslog',
            },
            'request_handler': {
                    'level':'DEBUG',
                    'class':'logging.handlers.RotatingFileHandler',
                    'filename': 'logs/django_request.log',
                    'maxBytes': 1024*1024*30, # 30 MB
                    'backupCount': 5,
                    'formatter':'verbose',
            },
            'console':{
                'level':'INFO',
                'class':'logging.StreamHandler',
                'formatter': 'verbose'
            },
            'null': {
                'level':'DEBUG',
                'class':'django.utils.log.NullHandler',
            },
        },
        'loggers': {

            '': {
                'handlers': ['default', 'console'],
                'level': 'DEBUG',
                'propagate': True
            },
            'django.request': { # Stop SQL debug from logging to main logger
                'handlers': ['request_handler'],
                'level': 'DEBUG',
                'propagate': True
            },
            'django.db.backends': {
                 'handlers': ['null'],  # Quiet by default!
                 'propagate': False,
                 'level':'DEBUG',
            },
        }
    }

Para usar a API de logging do python basta fazer:

    import logging

    logger= logging.getLogger(__name__)
    logger.info("teste 1..2.3..")

## Python - Gunicorn

Inserir as seguintes linhas no arquivo de configuracao:

    [handler_syslogHandler]
    class=handlers.SysLogHandler
    formatter=syslogFormatter
    args=('/dev/log','local3')

    [formatter_syslogFormatter]
    format=<APP_NAME> [%(name)s] %(message)s


Apendar no handler (syslogHandler), formatters(syslogFormatter) e logger_root (syslogHandler) as chaves.

    [handlers]
    keys=watchedFileHandler,syslogHandler

    [formatters]
    keys=simpleFormatter,syslogFormatter

    [logger_root]
    level=DEBUG
    handlers=watchedFileHandler,syslogHandler


# Apache

Customizaremos o log format para "economizar" alguns bytes.

    ErrorLog syslog:local6

    LogFormat "%h %l %u \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" lognit_combined


Dentro de seu Virtual Host.

    CustomLog "|/bin/logger -t httpd-<PRODUTO> -p local6.info" lognit_combined


# Ngnix

Será preciso aplicar um patch no Nginx para permitir o log de mensagens para o Syslog. Referência:
https://github.com/yaoweibin/nginx_syslog_patch

Exemplo de configuração:


    worker_processes  1;

    syslog local6 httpd-<APPLICATION>;

    events {
            worker_connections  1024;
    }

    http {
        include       mime.types;
        default_type  application/octet-stream;

        log_format  main  '$remote_addr - $remote_user [$time_local] $request '
            '"$status" $body_bytes_sent "$http_referer" '
            '"$http_user_agent" "$http_x_forwarded_for"';

        # Include this log_format
        log_format  syslog  '$remote_addr - $remote_user $request '
            '"$status" $body_bytes_sent "$http_referer" '
            '"$http_user_agent" "$http_x_forwarded_for"';

        server {
            listen       80;
            server_name  localhost;

            #send the log to syslog and file.
            access_log  logs/host1.access.log main;
            access_log  syslog:notice syslog;
            error_log syslog:notice|logs/host1.error.log;

            location / {
                root   html;
                index  index.html index.htm;
            }
        }

        server {
            listen       80;
            server_name  www.example.com;

            access_log  logs/host2.access.log main;
            access_log  syslog:notice syslog;
            error_log syslog:warn|logs/host2.error.log;

            location / {
                root   html;
                index  index.html index.htm;
            }
        }

        server {
            listen       80;
            server_name  www.test.com;

            #send the log just to syslog.
            access_log  syslog:error syslog;
            error_log syslog:error;

            location / {
                root   html;
                index  index.html index.htm;
            }
        }
    }

