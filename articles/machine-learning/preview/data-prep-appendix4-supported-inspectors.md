---
title: "Inspetores com suporte disponíveis com a preparação dos dados do Azure Machine Learning | Microsoft Docs"
description: "Este documento fornece uma lista completa dos inspetores disponíveis para a preparação de dados do Azure Machine Learning"
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
ms.date: 09/11/2017
ms.openlocfilehash: 35d7c04f245e93d8cc795dca7c01c2bab5a14eb8
ms.sourcegitcommit: e5355615d11d69fc8d3101ca97067b3ebb3a45ef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/31/2017
---
# <a name="supported-inspectors-for-the-azure-machine-learning-data-preparation-preview"></a>Inspetores com suporte para a versão prévia da preparação dos dados do Azure Machine Learning
Este documento descreve o conjunto de inspetores disponíveis nesta versão prévia.

## <a name="the-halo-effect"></a>O efeito de halo 
Alguns inspetores dão suporte ao efeito de halo. Esse efeito usa duas cores diferentes para mostrar imediatamente de forma visual a alteração de uma transformação. O cinza representa o valor antes da transformação mais recente, e o azul mostra o valor atual. Esse efeito pode ser habilitado e desabilitado nas opções.

## <a name="graphical-filtering"></a>Filtragem de gráfico 
Alguns dos inspetores dão suporte à filtragem de dados usando o inspetor como um editor. O uso do inspetor como editor envolve a seleção de elementos gráficos e, em seguida, o uso da barra de tarefas na parte superior direita da janela do inspetor para filtrar os valores selecionados. 

## <a name="column-statistics"></a>Estatísticas da coluna
Para colunas numéricas, esse inspetor fornece uma variedade de diferentes estatísticas sobre a coluna. As estatísticas incluem as seguintes medidas: 
- Mínimo
- Quartil inferior
- Mediana
- Quartil superior
- Máximo
- Média
- Desvio padrão


### <a name="options"></a>Opções 
- Nenhum

## <a name="histogram"></a>Histograma 
Calcula e exibe um histograma de uma única coluna numérica. O número padrão de buckets é calculado usando a regra de Scott. No entanto, a regra pode ser substituída por meio das opções.

O Inspetor dá suporte ao efeito de halo.


### <a name="options"></a>Opções
- Número mínimo de buckets (aplica-se mesmo quando o bucketing padrão está marcado)
- Número padrão de buckets (Regra de Scott) 
- Mostrar halo
- Sobreposição de gráfico de densidade de Kernel (Kernel Gaussiano) 


### <a name="actions"></a>Ações
Esse Inspetor oferece suporte à filtragem por meio de buckets, que podem incluir buckets de seleção única ou múltipla. Aplique os filtros conforme descrito anteriormente.

## <a name="value-counts"></a>Contagens de valor
Esse inspetor apresenta uma tabela de frequência de valores para a coluna selecionada no momento. A exibição padrão é para os seis valores principais. Mas você pode alterar o limite para qualquer número. Você também pode definir a exibição para contar de baixo pra cima, em vez de cima pra baixo. O inspetor dá suporte ao efeito de halo.

### <a name="options"></a>Opções 
- Número de valores principais
- Decrescente
- Incluir valores nulos/erro
- Mostrar halo


### <a name="actions"></a>Ações 
Esse Inspetor oferece suporte à filtragem por meio de barras, que podem incluir barras de seleção única ou múltipla. Aplique os filtros conforme descrito anteriormente.

## <a name="box-plot"></a>Gráfico de caixa 
Um gráfico de caixa estreita de uma coluna numérica.

### <a name="options"></a>Opções 
- Agrupar por coluna

## <a name="scatter-plot"></a>Gráfico de dispersão
Um gráfico de dispersão para duas colunas numéricas. Os dados são reduzidos por motivos de desempenho. O tamanho da amostra pode ser substituído nas opções.

### <a name="options"></a>Opções  
- Coluna do eixo X
- Coluna do eixo Y
- Tamanho da amostra
- Agrupar por coluna


## <a name="time-series"></a>Série temporal
Um gráfico de linha com reconhecimento de tempo no eixo x.

### <a name="options"></a>Opções
- Coluna de data
- Coluna numérica
- Tamanho da amostra


### <a name="actions"></a>Ações
Esse inspetor dá suporte à filtragem por meio de um método de Clicar e Arrastar a Seleção para selecionar um intervalo no gráfico. Depois de concluir a seleção, aplique os filtros conforme descrito anteriormente.


## <a name="map"></a>Mapa 
Um mapa com pontos plotados, assumindo que a latitude e a longitude foram especificadas. A latitude deve ser selecionada primeiro.

### <a name="options"></a>Opções
- Coluna de latitude
- Coluna de longitude
- Clustering em
- Agrupar por coluna


### <a name="actions"></a>Ações
Esse inspetor dá suporte à filtragem por meio da seleção de ponto do mapa. Pressione a tecla **Ctrl** e clique e arraste o mouse para formar um quadrado em torno dos pontos. Em seguida, aplique os filtros conforme descrito anteriormente.

É possível dimensionar rapidamente o mapa para mostrar somente os pontos possíveis pressionando **E** no lado esquerdo do mapa.
