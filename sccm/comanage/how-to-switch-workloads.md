---
title: Basculer les charges de travail de cogestion
titleSuffix: Configuration Manager
description: Découvrez comment basculer les charges de travail actuellement gérées par Configuration Manager vers Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 01/14/2019
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.collection: M365-identity-device-management
ms.openlocfilehash: a4b50d0491644e6be0967c1adcf2db641c1bb1cd
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754951"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Comment basculer les charges de travail de Configuration Manager vers Intune

Le basculement des charges de travail de Configuration Manager vers Microsoft Intune est l’un des avantages de la cogestion. Quand un appareil Windows 10 dispose du client Configuration Manager et qu’il est inscrit à Intune, vous bénéficiez des avantages des deux services. Vous contrôlez les charges de travail, le cas échéant, pour lesquelles vous utilisez Intune à la place de Configuration Manager comme autorité. Configuration Manager continue de gérer toutes les autres charges de travail, notamment celles que vous ne basculez pas vers Intune, ainsi que toutes les autres fonctionnalités de Configuration Manager que la cogestion ne prend pas en charge.

Pour plus d’informations sur les charges de travail prises en charge, consultez [Charges de travail](/sccm/comanage/workloads).

Vous pouvez basculer des charges de travail au moment où vous activez la cogestion ou ultérieurement quand vous êtes prêt. Si vous n’avez pas encore activé la cogestion, commencez par cette opération. Pour plus d’informations, consultez [Guide pratique pour activer la cogestion](/sccm/comanage/how-to-enable).


Après avoir activé la cogestion, modifiez les paramètres dans les propriétés de cogestion. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**.  

2. Sélectionnez l’objet de cogestion, puis choisissez **Propriétés** dans le ruban.  

3. Basculez vers l’onglet **Charges de travail**. Par défaut, toutes les charges de travail sont définies sur le paramètre **Configuration Manager**. Pour basculer une charge de travail, déplacez le contrôle de curseur de cette charge de travail sur le paramètre souhaité.  

    ![Capture d’écran de l’onglet Charges de travail sur la page des propriétés de cogestion](media/properties-workloads.png)

    - **Configuration Manager** : Configuration Manager continue de gérer cette charge de travail.  

    - **Intune pilote** : Bascule cette charge de travail uniquement pour les appareils du regroupement pilote. Vous pouvez changer le **Regroupement pilote** sous l’onglet **Préproduction** de la page des propriétés de cogestion.  

    - **Intune** : Basculez cette charge de travail pour tous les appareils Windows 10 inscrits dans la cogestion.  


> [!Important]  
> Avant de basculer des charges de travail, vérifiez que vous avez correctement configuré et déployé la charge de travail correspondante dans Intune. Assurez-vous que les charges de travail sont toujours gérées par l’un des outils de gestion de vos appareils.  

<!--1357377-->
À compter de Configuration Manager version 1806, quand vous basculez une charge de travail en cogestion, les appareils cogérés sont automatiquement synchronisés avec la stratégie MDM de Microsoft Intune. Cette synchronisation est effectuée lorsque vous lancez l’action **Télécharger la stratégie d’ordinateur** à partir de notifications du client dans la console Configuration Manager. Pour plus d’informations, consultez [Lancer une récupération de stratégie client en utilisant une notification de client](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


