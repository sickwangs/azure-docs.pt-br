---
title: "Reentrada nos microsserviços do Azure baseada em ator | Microsoft Docs"
description: "Introdução à reentrância para Reliable Actors do Service Fabric"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/02/2017
ms.author: vturecek
ms.openlocfilehash: dec785757ac582f044811c0f64ae0d452d6ad9a0
ms.sourcegitcommit: 3df3fcec9ac9e56a3f5282f6c65e5a9bc1b5ba22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2017
---
# <a name="reliable-actors-reentrancy"></a>Reentrância de Reliable Actors
Por padrão, o tempo de execução do Reliable Actors permite a reentrância baseada no contexto da chamada lógica. Isso possibilita que os atores sejam reentrantes se estiverem na mesma cadeia de contexto de chamada. Por exemplo, se um Ator A envia a mensagem para o Ator B, que envia a mensagem para o Ator C. Como parte do processamento da mensagem no caso de o Ator C chamar o Ator A, a mensagem é reentrante e por isso será permitida. Todas as outras mensagens que fazem parte de um contexto de chamada diferente serão bloqueadas no Ator A até a conclusão do processamento.

Há duas opções disponíveis para nova entrada de ator definida na enumeração `ActorReentrancyMode` :

* `LogicalCallContext` (comportamento padrão)
* `Disallowed` - desabilita a nova entrada

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
A nova entrada pode ser definida nas configurações de `ActorService`durante o registro. A configuração se aplica a todas as instâncias de ator criadas no serviço de ator.

O exemplo a seguir mostra um serviço de ator que define o modo de nova entrada como `ActorReentrancyMode.Disallowed`. Nesse caso, se um ator envia uma mensagem reentrante para outro ator, será lançada uma exceção do tipo `FabricException` .

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre a reentrada na [Documentação de referência de API de Ator](https://msdn.microsoft.com/library/azure/dn971626.aspx)
