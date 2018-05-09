---
title: Gérer les packages de mise à niveau de système d’exploitation
titleSuffix: Configuration Manager
description: Découvrez comment gérer des packages de mise à niveau de système d’exploitation dans System Center Configuration Manager.
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b9b22655-b8c1-461f-8047-3a7e906f647a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e323fa8df7d8ae88d6526a5d1777ceb8fa27c2de
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-operating-system-upgrade-packages-with-system-center-configuration-manager"></a>Gérer des packages de mise à niveau de système d’exploitation avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, un package de mise à niveau contient les fichiers sources d’installation de Windows utilisés pour mettre à niveau un système d’exploitation existant sur un ordinateur. Aidez-vous des informations des sections suivantes pour gérer les packages de mise à niveau de système d’exploitation dans Configuration Manager.

##  <a name="BKMK_AddOSUpgradePkgs"></a> Ajouter des packages de mise à niveau de système d’exploitation à Configuration Manager  
 Avant d’utiliser un package de mise à niveau de système d’exploitation, vous devez l’ajouter à un site Configuration Manager. Pour ajouter un package de mise à niveau de système d’exploitation à un site, procédez comme suit.  

#### <a name="to-add-an-operating-system-upgrade-package"></a>Pour ajouter un package de mise à niveau de système d’exploitation  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels** , développez **Systèmes d’exploitation**, puis cliquez sur **Packages de mise à niveau du système d’exploitation**.  

3.  Sous l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter un package de mise à niveau du système d’exploitation** pour démarrer l’Assistant Ajout d’un package de mise à niveau du système d’exploitation.  

4.  Dans la page **Source de données** , spécifiez le chemin d’accès réseau aux fichiers sources d’installation du package de mise à niveau de système d’exploitation. Par exemple, spécifiez le chemin UNC **\\\serveur\chemin** des fichiers sources d’installation.  

    > [!NOTE]  
    >  Les fichiers sources d’installation contiennent Setup.exe et d’autres fichiers et dossiers pour installer le système d’exploitation.  

    > [!IMPORTANT]  
    >  Limiter l’accès aux fichiers sources d’installation pour empêcher toute falsification indésirable.  

5.  Sur la page **Général** , spécifiez les informations suivantes, puis cliquez sur **Suivant**. Cette information est utile à des fins d'identification lorsque vous avez plusieurs programmes d'installation de système d'exploitation.  

    -   **Nom**: Spécifiez le nom du programme d'installation de système d'exploitation.  

    -   **Version**: Spécifiez la version du programme d'installation de système d'exploitation.  

    -   **Commentaire**: spécifiez une brève description du programme d'installation de système d'exploitation.  

6.  Effectuez toutes les étapes de l'Assistant.  

 Vous pouvez désormais distribuer le programme d'installation de système d'exploitation aux points de distribution auxquels vos séquences de tâches de déploiement accèdent.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuer des images de système d’exploitation à un point de distribution  
 Les images de système d’exploitation sont distribuées aux points de distribution de la même façon que vous distribuez d’autre contenu. Dans la plupart des cas, vous devez distribuer l’image de système d’exploitation à au moins un point de distribution avant de déployer le système d’exploitation. Pour découvrir comment distribuer une image de système d’exploitation, consultez [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSUpgradePkgApplyUpdates"></a> Appliquer des mises à jour logicielles à un package de mise à niveau du système d’exploitation  
 À compter de Configuration Manager version 1602, vous pouvez appliquer les nouvelles mises à jour logicielles à l’image de système d’exploitation dans votre package de mise à niveau du système d’exploitation. Avant de pouvoir appliquer des mises à jour logicielles à un package de mise à niveau, votre infrastructure de mises à jour logicielles doit être en place, et vous devez avoir synchronisé les mises à jour logicielles et téléchargé les mises à jour logicielles dans la bibliothèque de contenu sur le serveur de site. Pour plus d’informations, consultez [Déployer des mises à jour logicielles](../../sum/deploy-use/deploy-software-updates.md).  

 Vous pouvez appliquer les mises à jour logicielles appropriées à un package de mise à niveau selon une planification définie. Aux heures planifiées, Configuration Manager applique les mises à jour logicielles sélectionnées au package de mise à niveau du système d’exploitation puis, si vous le souhaitez, distribue le package de mise à niveau mis à jour aux points de distribution. Les informations sur le package de mise à niveau du système d’exploitation sont stockées dans la base de données du site, y compris les mises à jour logicielles qui ont été appliquées au moment de l’importation. Les mises à jour logicielles appliquées au package de mise à niveau depuis son ajout initial sont également stockées dans la base de données du site. Lorsque vous ouvrez l’Assistant pour appliquer des mises à jour logicielles au package de mise à niveau du système d’exploitation, l’Assistant récupère la liste des mises à jour logicielles applicables qui n’ont pas encore été appliquées au package de mise à niveau, pour vous permettre de les sélectionner. Configuration Manager copie les mises à jour logicielles de la bibliothèque de contenu sur le serveur de site, puis applique les mises à jour logicielles au package de mise à niveau du système d’exploitation.  

 Pour appliquer des mises à jour logicielles à un package de mise à niveau du système d’exploitation, procédez comme suit.  

#### <a name="to-apply-software-updates-to-an-operating-system-upgrade-package"></a>Pour appliquer des mises à jour logicielles à un package de mise à niveau du système d’exploitation  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels** , développez **Systèmes d’exploitation**, puis cliquez sur **Packages de mise à niveau du système d’exploitation**.  

3.  Sélectionnez le package de mise à niveau du système d’exploitation auquel appliquer les mises à jour logicielles.  

4.  Sous l’onglet **Accueil** , dans le groupe **Packages de mise à niveau du système d’exploitation** , cliquez sur **Planifier les mises à jour** pour démarrer l’Assistant.  

5.  Sur la page **Choisir des mises à jour** , sélectionnez les mises à jour logicielles à appliquer à l'image du sytème d'exploitation, puis cliquez sur **Suivant**.  

6.  Sur la page **Définir le calendrier** , spécifiez les paramètres suivants, puis cliquez sur **Suivant**.  

    1.  **Calendrier**: définissez le calendrier d’application des mises à jour logicielles à l’image du système d’exploitation.  

    2.  **Continuer en cas d’erreur**: sélectionnez cette option pour continuer à appliquer les mises à jour logicielles à l’image même si une erreur survient.  

    3.  **Distribuer l’image aux points de distribution**: sélectionnez cette option pour mettre à jour l’image du système d’exploitation sur les points de distribution après l’application des mises à jour logicielles.  

7.  Vérifiez les informations figurant sur la page **Résumé** , puis cliquez sur **Suivant**.  

8.  Sur la page **Dernière étape** , vérifiez que les mises à jour logicielles ont été correctement appliquées à l'image de système d'exploitation.  
