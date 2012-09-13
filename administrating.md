---
layout: page
title: Administração do Lognit
description: "Dicas e boas práticas de administração do sistema"
---

# Administrando o Lognit

## Grupos de logs

Grupos de logs são conjuntos utilizados para enriquecer mensagens de log com propriedades adicionais às provenientes da fonte original da mensagem.

Por exemplo, se é sabido que todas as mensagens de um determinado host e aplicação são referentes a determinado produto, é possível criar um grupo de log que adicione a estas mensagens também o nome do produto, assim facilitando consultas de usuários.

Para definir quais mensagens pertencem a um grupo, é utilizada uma **consulta estruturada**. Ou seja, valores das propriedades da mensagem original são utilizadas para adicionar mais dados às mensagens.

Existem três maneiras de enriquecer uma mensagem de log

* uma **expressão regular** pode ser utilizada para extrair os dados da própria mensagem
* a **posição do termo na mensagem** pode ser utilizada quando a mensagem tem formato fixo
* um **valor fixo** pode ser adicionado, como no caso do nome de um produto ou região, por exemplo

## Espaços

Espaços são conjuntos de grupos de log. São utilizados para controle de acesso ao conteúdo da aplicação. Uma vez um grupo de log adicionado a um espaço, os usuários das equipes que têm acesso àquele espaço passam a poder visualizar as mensagens do grupo.


## Equipes, usuários e controle de acesso

As equipes são criadas para organização do sistema e para controle de acesso. Os níveis de permissão são associados às equipes. São eles

* **realizar buscas** é o nível mais básico. Neste nível, é possível escolher a quais espaços os usuários têm acesso, bem como permitir o acesso a todas as mensagens.
* **gerenciar logs** é o nível que permite a criação, edição e remoção de grupos de logs.
* **gerenciar acesso** é o nível que permite a total administração do sistema,  permitindo criação, edição e remoção de equipes e usuários.

> Os níveis **gerenciar logs** e **gerenciar acesso** implicam no acesso a todas as mensagens de log do sistema.
