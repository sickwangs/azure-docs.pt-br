---
title: Python de exemplo para derivar novas colunas no preparo dos dados do Azure Machine Learning | Microsoft Docs
description: "Este documento fornece exemplos de código do Python para criar novas colunas na preparação de dados do Azure Machine Learning."
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: 
ms.service: machine-learning
ms.workload: data-services
ms.custom: 
ms.devlang: 
ms.topic: article
ms.date: 09/12/2017
ms.openlocfilehash: 143031ce804f4a8dcd4e328c413478f5ea669090
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2017
---
# <a name="sample-of-custom-column-transforms-python"></a>Exemplo de transformações de coluna personalizadas (Python) 
O nome dessa transformação no menu é **Adicionar Coluna (Script)**.

Antes de ler este apêndice, leia [Visão geral da extensibilidade do Python](data-prep-python-extensibility-overview.md).

## <a name="test-equivalence-and-replace-values"></a>Testar equivalência e substituir valores 
Se o valor na Col1 for menor do que 4, a nova coluna deverá ter um valor 1. Se o valor na Col1 for maior do que 4, a nova coluna terá o valor 2. 

```python
    1 if row["Col1"] < 4 else 2
```
## <a name="current-date-and-time"></a>Data e hora atuais 

```python
    datetime.datetime.now()
```
## <a name="typecasting"></a>Typecasting 
```python
    float(row["Col1"]) / float(row["Col2"] - 1)
```
## <a name="evaluate-for-nullness"></a>Avaliar quanto à nulidade 
Se Col1 contiver um valor nulo, então marque a nova coluna como **Incorreta**. Caso contrário, marque-a como **Boa.** 

```python
    'Bad' if pd.isnull(row["Col1"]) else 'Good'
```
## <a name="new-computed-column"></a>Nova coluna computada 
```python
    np.log(row["Col1"])
```
## <a name="epoch-computation"></a>Computação de época 
Número de segundos desde a Época Unix (supondo que Col1 já é uma data): 
```python
    row["Col1"] - datetime.datetime.utcfromtimestamp(0)).total_seconds()
```





