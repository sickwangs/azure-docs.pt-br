---
title: "Azure AD Connect: autenticação de passagem – Limitações atuais | Microsoft Docs"
description: "Este artigo descreve as limitações atuais da autenticação de passagem do Azure AD (Azure Active Directory)."
services: active-directory
keywords: "Autenticação de Passagem do Azure AD Connect, instalar o Active Directory, componentes necessários para o Azure AD, SSO, Logon único"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/19/2017
ms.author: billmath
ms.openlocfilehash: 4a33df43ca218545d6c684103a64f2cd1460913b
ms.sourcegitcommit: 732e5df390dea94c363fc99b9d781e64cb75e220
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/14/2017
---
# <a name="azure-active-directory-pass-through-authentication-current-limitations"></a>Autenticação de passagem do Azure Active Directory: limitações atuais

>[!IMPORTANT]
>A Autenticação de Passagem do Azure AD é um recurso gratuito e você não precisa de nenhuma edição paga do Azure AD para usá-lo. A autenticação de passagem só está disponível na instância mundial do Azure AD e não no [Microsoft Cloud Alemanha](http://www.microsoft.de/cloud-deutschland) nem na [Nuvem do Microsoft Azure Governamental](https://azure.microsoft.com/features/gov/).

## <a name="supported-scenarios"></a>Cenários com suporte

Os cenários a seguir têm suporte total:

- Entradas de usuário em todos os aplicativos baseados em navegador da Web.
- Entradas de usuário em aplicativos cliente Office 365 com suporte para [autenticação moderna](https://aka.ms/modernauthga) – Office 2016 e Office 2013 _com_ autenticação moderna.
- Ingresso do Azure AD para dispositivos Windows 10.
- Suporte ao Exchange ActiveSync.

## <a name="unsupported-scenarios"></a>Cenários sem suporte

Os cenários a seguir _não_ têm suporte:

- Entradas do usuário em aplicativos de cliente do Office herdados – Office 2010 e Office 2013 _sem_ autenticação moderna). As organizações são incentivadas a mudar para autenticação moderna se possível. A autenticação moderna permite o suporte à Autenticação de Passagem, mas também ajuda a proteger suas contas de usuário usando recursos de [acesso condicional](../active-directory-conditional-access-azure-portal.md) como a MFA (Autenticação Multifator).
- O usuário entra em aplicativos cliente do Skype for Business, incluindo o Skype for Business 2016.
- Logons de usuário no PowerShell v1.0. É recomendável usar o PowerShell v2.0.
- Azure AD Domain Services.
- Senhas de aplicativo para MFA.
- Detecção de usuários com [credenciais vazadas](../active-directory-reporting-risk-events.md#leaked-credentials).

>[!IMPORTANT]
>Como alternativa para cenários sem suporte _apenas_, habilite a sincronização de hash de senha na página [Recursos opcionais](active-directory-aadconnect-get-started-custom.md#optional-features) do assistente do Azure AD Connect. Habilitar a Sincronização de Hash de Senha também oferece a opção de fazer failover da autenticação se sua infraestrutura local sofrer uma interrupção completa. Esse failover de Autenticação de Passagem para Sincronização de Hash de Senha não é automático, mas foi feito com a Ajuda do Suporte da Microsoft.

## <a name="next-steps"></a>Próximas etapas
- [**Início rápido**](active-directory-aadconnect-pass-through-authentication-quick-start.md) – instale e execute a autenticação de passagem do Azure AD.
- [**Bloqueio Inteligente**](active-directory-aadconnect-pass-through-authentication-smart-lockout.md) – configura a capacidade de Bloqueio Inteligente no seu locatário para proteger as contas de usuário.
- [**Aprofundamento técnico**](active-directory-aadconnect-pass-through-authentication-how-it-works.md) – entenda como esse recurso funciona.
- [**Perguntas frequentes**](active-directory-aadconnect-pass-through-authentication-faq.md) – respostas para perguntas frequentes.
- [**Solução de problemas**](active-directory-aadconnect-troubleshoot-pass-through-authentication.md) – Saiba como resolver problemas comuns do recurso.
- [**Aprofundamento em Segurança**](active-directory-aadconnect-pass-through-authentication-security-deep-dive.md) – informações técnicas aprofundadas adicionais sobre o recurso.
- [**SSO contínuo do Azure AD**](active-directory-aadconnect-sso.md) – Saiba mais sobre esse recurso complementar.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) – para registrar solicitações de novos recursos.
