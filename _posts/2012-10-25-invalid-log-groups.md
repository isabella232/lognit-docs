---
layout: page
title: Testando todos os log groups
description: "Enumerando log groups cuja consulta esteja inválida"
category: tips
tags: [lognit, logs, log-group, api, javascript]
---

# {{ page.title }}

Uma forma fácil de enumerar todos os log groups, testando se a expressão da
consulta deles está inválida é utilizando o próprio console javascript do browser.

    var validateGroup = function(group) {
       $.get('/rest/search', {expression: group.expression}, function(search) {
           if (!search.info.valid) {
               console.info('Log group inválido: ', group.name);
               console.info(search.info.message);
           }
       });
    };

    $.get('/rest/log-groups', function(result) { 
        _(result.data).each(validateGroup);
    });
