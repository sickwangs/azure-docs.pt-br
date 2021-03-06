---
title: Controlando o comportamento de cache da CDN do Azure com cadeias de consulta | Microsoft Docs
description: "O cache da cadeia de caracteres de consulta da CDN do Azure controla como os arquivos são armazenados em cache quando contêm cadeias de caracteres de consulta."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: mazha
ms.openlocfilehash: 28e724f34c32edb0d5641b24f9ffedb7dc5f9680
ms.sourcegitcommit: 6a22af82b88674cd029387f6cedf0fb9f8830afd
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/11/2017
---
# <a name="control-azure-content-delivery-network-caching-behavior-with-query-strings"></a>Controle o comportamento de cache da Rede de Distribuição de Conteúdo do Microsoft Azure  com cadeias de caracteres de consulta
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [CDN Premium do Azure da Verizon](cdn-query-string-premium.md)
> 

## <a name="overview"></a>Visão geral
Com a CDN (Rede de Distribuição de Conteúdo), você pode controlar como os arquivos são armazenados em cache para uma solicitação na Web que contenha uma cadeia de caracteres de consulta. Em uma solicitação da Web com uma cadeia de caracteres de consulta, a cadeia de caracteres de consulta é parte da solicitação que ocorre após o caractere `?`. Uma cadeia de caracteres de consulta pode conter um ou mais parâmetros, que são separados por um caractere `&`. Por exemplo: `http://www.domain.com/content.mov?data1=true&data2=false`. Se houver mais de um parâmetro de cadeia de caracteres de consulta em uma solicitação, a ordem dos parâmetros não importará. 

> [!IMPORTANT]
> Os produtos da CDN premium e padrão oferecem a mesma funcionalidade de cache de cadeia de caracteres de consulta, mas a interface do usuário é diferente.  Este artigo descreve a interface da **CDN Standard do Azure da Akamai** e da **CDN Standard do Azure da Verizon**. Para saber mais sobre o armazenamento em cache de cadeias de caracteres de consulta com a **CDN Premium do Azure da Verizon**, confira [Controlando o comportamento do cache de solicitações de CDN com cadeias de caracteres de consulta - Premium](cdn-query-string-premium.md).

Estão disponíveis três modos de cadeia de caracteres de consulta:

- **Ignorar cadeias de caracteres de consulta**: modo padrão. Neste modo, o nó de borda da CDN passa as cadeias de caracteres de consulta do solicitante para a origem na primeira solicitação e armazena o ativo em cache. Todas as solicitações subsequentes para esse ativo que são atendidas a partir do nó de borda ignoram a cadeia de caracteres de consulta até que o ativo em cache expire.
- **Ignorar o cache para cadeias de consulta**: nesse modo, as solicitações com cadeias de caracteres de consulta não são armazenadas em cache no nó de borda da CDN. O nó de borda recupera o ativo diretamente da origem e passa-o para o solicitante com cada solicitação.
- **Armazenar em cada cache URL exclusiva**: nesse modo, cada solicitação com um URL exclusiva, incluindo a cadeia de caracteres de consulta, é tratada como um ativo exclusivo com seu próprio cache. Por exemplo, a resposta da origem para uma solicitação de `example.ashx?q=test1` é armazenada em cache no nó de borda e retornada para caches subsequentes com a mesma cadeia de caracteres de consulta. Uma solicitação `example.ashx?q=test2` é armazenada em cache como um ativo separado com sua própria configuração de vida útil.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Alterando configurações de cache de cadeia de consulta para perfis de CDN padrão
1. Abra um perfil de CDN e, em seguida, selecione o ponto de extremidade da CDN que deseja gerenciar.
   
   ![Pontos de extremidade de perfil CDN](./media/cdn-query-string/cdn-endpoints.png)
   
2. Em Configurações, clique em **Cache**.
   
    ![Botão de Cache do perfil da CDN](./media/cdn-query-string/cdn-cache-btn.png)
   
3. Na lista **Comportamento de cache da cadeia de caracteres de consulta**, selecione um modo de cadeia de caracteres de consulta e, em seguida, clique em **Salvar**.
   
  <!--- Replace screen shot after general caching goes live ![CDN query string caching options](./media/cdn-query-string/cdn-query-string.png) --->

> [!IMPORTANT]
> Como é necessário um tempo para que o registro se propague através da CDN, as alterações nas configurações da cadeia de caracteres de cache poderão não estar visíveis imediatamente. Para perfis da **CDN do Azure da Akamai** , a propagação normalmente é concluída em um minuto. Para perfis da **Azure CDN da Verizon**, a propagação geralmente é concluída em 90 minutos, mas em alguns casos pode levar mais tempo.


