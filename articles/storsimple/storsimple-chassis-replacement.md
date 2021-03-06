---
title: "Substituir o chassi no dispositivo StorSimple série 8000 | Microsoft Docs"
description: "Descreve como remover e substituir o chassi em seu compartimento StorSimple primário ou compartimento EBOD."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 537659ed-4c46-49c1-b1e4-186262f2542d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/02/2017
ms.author: alkohli
ms.openlocfilehash: 7bc23e64331ad18c604ffaa29476766827119cd4
ms.sourcegitcommit: 3df3fcec9ac9e56a3f5282f6c65e5a9bc1b5ba22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/04/2017
---
# <a name="replace-the-chassis-on-your-storsimple-device"></a>Substituir o chassi em seu dispositivo StorSimple
> [!NOTE]
> O portal clássico para StorSimple foi preterido. Os Gerenciadores de Dispositivos do StorSimple migrarão automaticamente para o novo Portal do Azure, seguindo o agendamento definido para preteri-los. Você receberá um email e uma notificação de portal para essa mudança. Este documento também será desativado em breve. Para exibir a versão deste artigo para o novo Portal do Azure, acesse [Substituir um chassi em seu dispositivo StorSimple](storsimple-8000-chassis-replacement.md). Para dúvidas sobre a migração, consulte [Perguntas Frequentes: migração para o Portal do Azure](storsimple-8000-move-azure-portal-faq.md).

## <a name="overview"></a>Visão geral
Esse tutorial explica como remover e substituir um chassi em um dispositivo StorSimple 8000. O modelo StorSimple 8100 é um dispositivo de compartimento único (um chassi), enquanto o 8600 é um dispositivo de compartimento duplo (dois chassis). No modelo 8600, há potencialmente dois chassis que podem falhar no dispositivo: o chassi do compartimento primário ou o chassi do compartimento EBOD.

Em ambos os casos, o chassi de substituição enviado pela Microsoft estará vazio. Não será incluído nenhum módulos de energia e resfriamento (PCM), módulo de controlador, unidade de disco de estado sólido (SSD), unidade de disco rígido (HD) ou módulos EBOD.

> [!IMPORTANT]
> Antes de remover e substituir p chassi, examine as informações de segurança em [Substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="remove-the-chassis"></a>Remover o chassi
Execute as seguintes etapas para remover o chassi em seu dispositivo StorSimple.

#### <a name="to-remove-a-chassis"></a>Para remover um chassi
1. Certifique-se de que o dispositivo StorSimple esteja desligado e desconectado de todas as fontes de alimentação.
2. Remova todos os cabos SAS e de rede, se houver.
3. Remova a unidade do rack.
4. Remova cada uma das unidades e observe os slots do quais são removidas. Para obter mais informações, consulte [Remover a unidade de disco](storsimple-disk-drive-replacement.md#remove-the-disk-drive).
5. No compartimento EBOD (se for o chassi com falha), remova os módulos do controlador EBOD. Para obter mais informações, consulte [Remover um controlador EBOD](storsimple-ebod-controller-replacement.md#remove-an-ebod-controller). 
   
    No compartimento primário (se for o chassi com falha), remova os controladores e observe os slots dos quais são removidos. Para obter mais informações, consulte [Remover um controlador](storsimple-controller-replacement.md#remove-a-controller).

## <a name="install-the-chassis"></a>Instalar o chassi
Execute as seguintes etapas para instalar o chassi em seu dispositivo StorSimple.

#### <a name="to-install-a-chassis"></a>Para instalar um chassi
1. Monte o chassi no rack. Para saber mais, confira [Montar em rack o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#rack-mount-your-storsimple-8100-device) ou [Montar em rack o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#rack-mount-your-storsimple-8600-device).
2. Depois que o chassis estiver montado no rack, instale os módulos do controlador nas mesmas posições que eles estavam instalados anteriormente.
3. Instale as unidades nas mesmas posições e slots de que elas estavam instaladas anteriormente.
   
   > [!NOTE]
   > É recomendável instalar primeiro os SSDs nos slots e, em seguida, instalar os HDDs.
   > 
   > 
4. Com o dispositivo montado no rack e os componentes instalados, conecte o dispositivo nas fontes de alimentação apropriadas e ligue o dispositivo. Para obter detalhes, confira [Cabear o dispositivo StorSimple 8100](storsimple-8100-hardware-installation.md#cable-your-storsimple-8100-device) ou [Cabear o dispositivo StorSimple 8600](storsimple-8600-hardware-installation.md#cable-your-storsimple-8600-device).

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).

