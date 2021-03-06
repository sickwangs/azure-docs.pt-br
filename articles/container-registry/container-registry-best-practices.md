---
title: "Melhores práticas no Registro de Contêiner do Azure"
description: "Saiba como usar o registro de contêiner do Azure efetivamente seguindo estas melhores práticas."
services: container-registry
documentationcenter: 
author: mmacy
manager: timlt
editor: mmacy
tags: 
keywords: 
ms.assetid: 
ms.service: container-registry
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/05/2017
ms.author: marsma
ms.custom: 
ms.openlocfilehash: 9ec5573082dbf9de1288e1511f5041f8c20b416e
ms.sourcegitcommit: d41d9049625a7c9fc186ef721b8df4feeb28215f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/02/2017
---
# <a name="best-practices-for-azure-container-registry"></a>Melhores práticas para o Registro de Contêiner do Azure

Ao seguir essas melhores práticas, você pode ajudar a maximizar o desempenho e o uso econômico de seu registro de Docker privado no Azure.

## <a name="network-close-deployment"></a>Implantação de fechamento de rede

Crie o registro de contêiner na mesma região do Azure em que você implantar contêineres. Colocar o registro em uma região de fechamento de rede para seus hosts de contêiner pode ajudar a reduzir a latência e o custo.

A implantação de fechamento de rede é um dos principais motivos para usar um registro de contêiner particular. Imagens do docker têm uma ótima [construção de camadas](https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/) que permite implantações incrementais. No entanto, os novos nós precisam efetuar o pull de todas as camadas necessárias para uma determinada imagem. Este `docker pull` inicial pode acumular até vários gigabytes. Ter um registro privado perto de sua implantação minimiza a latência de rede.
Além disso, todas as nuvens públicas, incluindo do Azure, implementam taxas de saída de rede. Extrair imagens de um datacenter para outro adiciona taxas de saída de rede, além da latência.

## <a name="geo-replicate-multi-region-deployments"></a>Replicar geograficamente implantações em várias regiões

Use o recurso de [replicação geográfica](container-registry-geo-replication.md) do Registro de Contêiner do Azure se estiver implantando contêineres em várias regiões. Se você estiver atendendo clientes globais de centros de dados locais ou se sua equipe de desenvolvimento estiver em locais diferentes, é possível simplificar o gerenciamento de registro e minimizar a latência por meio da replicação geográfica do registro. Atualmente na versão prévia, esse recurso está disponível com registros [Premium](container-registry-skus.md#premium).

Para saber como usar a replicação geográfica, consulte o tutorial em três partes, [Replicação geográfica no Registro de Contêiner do Azure](container-registry-tutorial-prepare-registry.md).

## <a name="repository-namespaces"></a>Namespaces do repositório

Ao aproveitar os namespaces de repositório, você pode permitir o compartilhamento de um único registro em vários grupos em sua organização. Os registros podem ser compartilhados entre equipes e implantações. O Registro de Contêiner do Azure oferece suporte a namespaces aninhados, habilitando o isolamento de grupo.

Por exemplo, considere as seguintes marcas de imagem de contêiner. Imagens que são usadas em toda a empresa, como `aspnetcore`, são colocadas no namespace raiz, no caso de imagens de contêiner que pertencem a grupos de Produção e de Marketing, cada uma usa seus próprios namespaces.

```
contoso.azurecr.io/aspnetcore:2.0
contoso.azurecr.io/products/widget/web:1
contoso.azurecr.io/products/bettermousetrap/refundapi:12.3
contoso.azurecr.io/marketing/2017-fall/concertpromotions/campaign:218.42
```

## <a name="dedicated-resource-group"></a>Grupo de recursos dedicados

Como os registros de contêiner são recursos que são usados em vários hosts de contêiner, um registro deve residir seu próprio grupo de recursos.

Embora seja possível fazer experiências com um tipo de host específico, como Instâncias de Contêiner do Azure, você provavelmente desejará excluir a instância de contêiner quando terminar. No entanto, você também poderá manter a coleção de imagens que enviou por push para o Registro de Contêiner do Azure. Ao colocar o registro em seu próprio grupo de recursos, você minimiza o risco de excluir acidentalmente a coleção de imagens no registro quando exclui o grupo de recursos de instância do contêiner.

## <a name="authentication"></a>Autenticação

Ao se autenticar com um registro de contêiner do Azure, há dois cenários principais: autenticação individual e autenticação de serviço (ou "sem periférico"). A tabela a seguir fornece uma visão geral sobre esses cenários e o método de autenticação recomendado para cada.

| Tipo | Cenário de exemplo | Método recomendado |
|---|---|---|
| Identidade individual | Um desenvolvedor que efetua o pull de imagens de ou para seu computador de desenvolvimento. | [az acr login](/cli/azure/acr?view=azure-cli-latest#az_acr_login) |
| Sem periférico/serviço identidade | Pipelines de implantação e compilação em que o usuário não está diretamente envolvido. | [Entidade de serviço](container-registry-authentication.md#service-principal) |

Para obter informações detalhadas sobre a autenticação de Registro de Contêiner do Azure, consulte [Autenticar com um registro de contêiner do Azure](container-registry-authentication.md).

## <a name="next-steps"></a>Próximas etapas

O Registro de Contêiner do Azure está disponível em várias camadas, chamadas de SKUs e cada uma delas fornece funcionalidades diferentes. Para obter detalhes sobre as SKUs disponíveis, consulte [SKUs de Registro de Contêiner do Azure](container-registry-skus.md).