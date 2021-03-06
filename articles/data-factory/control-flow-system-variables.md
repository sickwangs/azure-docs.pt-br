---
title: "Variáveis do sistema no Azure Data Factory | Microsoft Docs"
description: "Este artigo descreve as variáveis do sistema com suporte pelo Azure Data Factory. Você pode usar essas variáveis em expressões ao definir entidades do Data Factory."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/07/2017
ms.author: shlo
ms.openlocfilehash: 274c003e0697ba08d010c3bf13724461a4b624ee
ms.sourcegitcommit: c50171c9f28881ed3ac33100c2ea82a17bfedbff
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/26/2017
---
# <a name="system-variables-supported-by-azure-data-factory"></a>Variáveis do sistema com suporte pelo Azure Data Factory
Este artigo descreve as variáveis do sistema com suporte pelo Azure Data Factory. Você pode usar essas variáveis em expressões ao definir entidades do Data Factory. 

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que está com GA (disponibilidade geral), veja [funções e variáveis no Data Factory versão 1](v1/data-factory-functions-variables.md).


## <a name="pipeline-scope"></a>Escopo do pipeline:

| Nome de variável | Descrição |
| --- | --- |
| @pipeline().DataFactory |Nome do data factory em que a execução do pipeline está ocorrendo | 
| @pipeline().Pipeline |Nome do pipeline |
| @pipeline().RunId | ID da execução do pipeline específica | 
| @pipeline().TriggerType | Tipo de gatilho que invocou o pipeline (Manual, Agendador) | 
| @pipeline().TriggerId| ID do gatilho que invoca o pipeline |
| @pipeline().TriggerName| Nome do gatilho que invoca o pipeline |
| @pipeline().TriggerTime| Hora em que o gatilho invocou o pipeline. A hora do gatilho é a hora do disparo real, não a hora agendada. Por exemplo, `13:20:08.0149599Z` é retornado em vez de `13:20:00.00Z` |

## <a name="trigger-scope"></a>Escopo do gatilho:

| Nome de variável | Descrição |
| --- | --- |
| trigger().scheduledTime |Hora em que o gatilho foi agendado para invocar a execução do pipeline. Por exemplo, para um gatilho disparado a cada cinco minutos, essa variável retornaria `2017-06-01T22:20:00Z`, `2017-06-01T22:25:00Z` e `2017-06-01T22:29:00Z` respectivamente.|
| trigger().startTime |Hora em que o gatilho **realmente** foi disparado para invocar a execução do pipeline. Por exemplo, para um gatilho disparado a cada cinco minutos, essa variável retornaria algo como `2017-06-01T22:20:00.4061448Z`, `2017-06-01T22:25:00.7958577Z` e `2017-06-01T22:29:00.9935483Z` respectivamente.|

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre como essas variáveis são usadas em expressões, consulte [Funções e linguagem de expressão](control-flow-expression-language-functions.md). 
