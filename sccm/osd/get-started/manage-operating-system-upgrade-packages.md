---
title: Gérer les packages de mise à niveau de système d’exploitation
titleSuffix: Configuration Manager
description: Découvrez comment gérer des packages de mise à niveau de système d’exploitation dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f7b8b18cbec5a3b5972a448e8a70339533dc11fb
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456004"
---
# <a name="manage-os-upgrade-packages-with-configuration-manager"></a>Gérer des packages de mise à niveau de système d’exploitation avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, un package de mise à niveau de système d’exploitation contient les fichiers sources d’installation de Windows qui permettent de mettre à niveau un système d’exploitation existant sur un ordinateur. Cet article explique comment ajouter, distribuer et gérer un package de mise à niveau du système d’exploitation.



##  <a name="BKMK_AddOSUpgradePkgs"></a> Ajouter un package de mise à niveau du système d’exploitation  

Avant de pouvoir utiliser un package de mise à niveau de système d’exploitation, vous devez l’ajouter à votre site Configuration Manager. 

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Packages de mise à niveau du système d’exploitation**.  

2.  Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, sélectionnez **Ajouter un package de mise à niveau du système d’exploitation**. Cette action démarre l’Assistant Ajout d’un package de mise à niveau du système d’exploitation.  

3.  Dans la page **Source de données**, spécifiez les paramètres suivants : 

    - **Chemin** réseau des fichiers sources d’installation du package de mise à niveau du système d’exploitation. Par exemple, `\\server\share\path`.  

        > [!NOTE]  
        >  Les fichiers sources d’installation contiennent Setup.exe et d’autres fichiers et dossiers pour installer le système d’exploitation.  

        > [!IMPORTANT]  
        >  Limitez l’accès aux fichiers sources d’installation pour empêcher toute falsification indésirable.  

    - Si vous souhaitez effectuer une mise en cache préliminaire du contenu d’un client, spécifiez l’**Architecture** et la **Langue** de l’image. Pour plus d’informations, consultez la section [Configurer le contenu précache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

4.  Dans la page **Général**, spécifiez les informations suivantes. Ces informations sont utiles à des fins d’identification lorsque vous avez plusieurs packages de mise à niveau du système d’exploitation.  

    -   **Nom** : nom unique du package de mise à niveau du système d’exploitation.  

    -   **Version** : identificateur de version facultatif. Il n’est pas nécessaire que cette propriété corresponde à la version du package de mise à niveau. Il s’agit souvent de la version du package de votre organisation.  

    -   **Commentaire** : brève description facultative.  

5.  Effectuez toutes les étapes de l'Assistant.  


Ensuite, distribuez le package de mise à niveau du système d’exploitation sur les points de distribution.  



##  <a name="BKMK_Distribute"></a> Distribuer du contenu vers un point de distribution  

Distribuez les packages de mise à niveau du système d’exploitation vers les points de distribution comme vous le feriez pour tout autre contenu. Avant de déployer la séquence de tâches, distribuez le package de mise à niveau du système d’exploitation vers au moins un point de distribution. Pour plus d’informations, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  



[!INCLUDE [Apply software updates to an image](includes/wim-apply-updates.md)]



## <a name="next-steps"></a>Étapes suivantes

[Créer une séquence de tâches pour mettre à niveau un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)