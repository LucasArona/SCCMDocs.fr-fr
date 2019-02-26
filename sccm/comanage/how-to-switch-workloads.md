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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754951"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Comment basculer des charges de travail de Configuration Manager sur Intune

Un des avantages de la cogestion bascule les charges de travail de Configuration Manager à Microsoft Intune. Quand un appareil Windows 10 a le client Configuration Manager et est inscrit à Intune, vous bénéficiez des avantages des deux services. Vous contrôlez les charges de travail, le cas échéant, que vous basculez de l’autorité de Configuration Manager à Intune. Configuration Manager continue de gérer toutes les autres charges de travail, y compris les charges de travail que vous ne basculez vers Intune, et toutes les autres fonctionnalités de Configuration Manager que cogestion ne prend pas en charge.

Pour plus d’informations sur les charges de travail pris en charge, consultez [charges de travail](/sccm/comanage/workloads).

Vous pouvez basculer des charges de travail lorsque vous activez la cogestion, ou ultérieurement, lorsque vous êtes prêt. Si vous n’avez pas encore activé la cogestion, faites-le en premier. Pour plus d’informations, consultez [comment activer la cogestion](/sccm/comanage/how-to-enable).


Après avoir activé la cogestion, modifiez les paramètres dans les propriétés de cogestion. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**.  

2. Sélectionnez l’objet de cogestion, puis choisissez **propriétés** dans le ruban.  

3. Basculez vers le **charges de travail** onglet. Par défaut, toutes les charges de travail sont définies sur le **Configuration Manager** paramètre. Pour basculer d’une charge de travail, déplacez le contrôle de curseur pour cette charge de travail pour le paramètre souhaité.  

    ![Onglet de capture d’écran de charges de travail sur la page de propriétés de cogestion](media/properties-workloads.png)

    - **Configuration Manager**: Configuration Manager continue de gérer cette charge de travail.  

    - **Piloter Intune**: Passez cette charge de travail uniquement pour les appareils dans la collection pilote. Vous pouvez modifier le **regroupement pilote** sur le **intermédiaire** onglet de la page de propriétés de cogestion.  

    - **Intune**: Commutateur de cette charge de travail pour tous les appareils Windows 10 inscrits à la cogestion.  


> [!Important]  
> Avant de basculer des charges de travail, assurez-vous que vous puissiez correctement configurez et déployez la charge de travail correspondant dans Intune. Assurez-vous que les charges de travail sont toujours gérées par l’un des outils de gestion de vos appareils.  

<!--1357377--> À compter de Configuration Manager version 1806, quand vous passez à une charge de travail en cogestion, les appareils cogérés sont automatiquement synchronisés avec la stratégie MDM de Microsoft Intune. Cette synchronisation est effectuée lorsque vous lancez l’action **Télécharger la stratégie d’ordinateur** à partir de notifications du client dans la console Configuration Manager. Pour plus d’informations, consultez [Lancer une récupération de stratégie client en utilisant une notification de client](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).


