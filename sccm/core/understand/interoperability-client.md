---
title: Client d’interopérabilité étendue
titleSuffix: Configuration Manager
description: Découvrez comment utiliser le client d’interopérabilité étendue pour la prise en charge à long terme d’un client Configuration Manager statique avec un site Current Branch.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4a9f23ce22bc5dc613e9d85b11f88148b2d82de
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523807"
---
# <a name="use-the-configuration-manager-client-software-for-extended-interoperability-with-future-versions-of-a-current-branch-site"></a>Utiliser le logiciel client Gestionnaire de configuration pour l’interopérabilité étendue avec les futures versions d’un site Current Branch

*S’applique à : System Center Configuration Manager (Current Branch)*  

Les exigences de l’entreprise risquent de ne pas vous autoriser à mettre à jour régulièrement le client Configuration Manager sur certains appareils. Par exemple, vous devrez respecter des stratégies de gestion des changements ; de même, l’appareil peut être stratégique. Contournez-les en installant un nouveau client pour une utilisation à long terme, appelé client d’interopérabilité étendue (EIC). Utilisez le client EIC uniquement sur des appareils spécifiques qui ne peuvent pas être mis à jour fréquemment, comme des bornes ou des appareils de point de vente. Continuez à utiliser la [mise à niveau automatique des clients](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) sur la plupart de vos clients. 



## <a name="how-it-works"></a>Fonctionnement

En règle générale, quand vous installez une nouvelle [mise à jour dans la console](/sccm/core/servers/manage/install-in-console-updates) pour Configuration Manager, les clients mettent automatiquement à jour leur logiciel client pour pouvoir utiliser ces nouvelles fonctionnalités. Avec ce scénario, vous effectuez quand même la mise à jour vers la branche CB qui reçoit les nouvelles fonctionnalités et mises à jour. La plupart des appareils mettent à jour le logiciel client Configuration Manager avec chaque mise à jour de version que vous installez. Toutefois, sur un sous-ensemble de systèmes critiques qui ne doivent pas recevoir les mises à jour du logiciel client, vous installez le client d’interopérabilité étendue. Ces clients n’installent pas de nouveau logiciel client tant que vous n’y avez pas explicitement déployé de nouvelle version du logiciel client.



## <a name="supported-versions"></a>Versions prises en charge

Le tableau suivant liste les versions du client Configuration Manager qui sont prises en charge pour ce scénario :

| Version  | Date de disponibilité  | Date de fin du support  |
|---------|---------|---------|
|1902<br/>5.00.8790     | 27 mars 2019        | Pas avant le 27 mars 2021        |
|1802<br/>5.00.8634     | 1er mai 2018        | Pas avant le 1er mai 2020        |
|1606<br/>5.00.8412     | 18 novembre 2016        | 1er mai 2019        |

> [!TIP]  
> Le client EIC est pris en charge pendant au moins deux ans à partir de la date de sortie. Pour plus d’informations sur les dates de sortie, consultez [Prise en charge des versions Current Branch de Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).  

Envisagez de mettre à jour le client d’interopérabilité étendue sur les appareils que vous gérez avec Current Branch avant que la prise en charge du client n’arrive à expiration. Pour cela, téléchargez une nouvelle version du client auprès de Microsoft, puis déployez ce logiciel client mis à jour sur vos appareils qui utilisent le client d’interopérabilité étendue actuel.



## <a name="how-to-use-the-eic"></a>Utilisation du client d’interopérabilité étendue

1. Obtenez une version prise en charge du client EIC dans le dossier `\SMSSETUP\Client` du support d’installation des mises à jour de Configuration Manager. Veillez à copier tout le contenu du dossier.  

2. Installez manuellement le client d’interopérabilité étendue sur ces appareils. Pour plus d’informations, consultez [Installer manuellement le client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual).  

    > [!Important]  
    > Lors de la mise à niveau des clients de la version 1606 vers la version 1802, utilisez l’option CCMSETUP **/AlwaysExcludeUpgrade:True**. Sinon, le client risque de recevoir la stratégie du point de gestion pour être automatiquement mis à niveau avant la stratégie d’exclusion.  

3. Ajoutez ces appareils dans une collection et excluez cette collection des mises à niveau automatiques du client. Pour plus d’informations, consultez [Utiliser la mise à niveau automatique du client](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade).  

> [!TIP]  
> Pour rechercher le support Configuration Manager dans le [Centre de gestion des licences en volume](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (VLSC), accédez à l’onglet **Téléchargements et clés**, recherchez `System Center Config`, puis sélectionnez **System Center Config Mgr (current branch)**.



## <a name="limitations"></a>Limitations

- Les mises à jour du logiciel client d’interopérabilité étendue ne sont pas disponibles par le biais des mises à jour dans la console. Pour plus d’informations sur la façon de mettre à jour les clients EIC, consultez [Comment utiliser le client EIC](#how-to-use-the-eic).  

- Le client EIC prend uniquement en charge les fonctionnalités suivantes :  

    - Mises à jour logicielles  
    - Inventaire matériel et logiciel
    - Packages et programmes



## <a name="next-steps"></a>Étapes suivantes

Pour vérifier que les clients sont installés correctement sur les appareils que vous souhaitez, consultez [Guide pratique pour surveiller les clients](/sccm/core/clients/manage/monitor-clients).
