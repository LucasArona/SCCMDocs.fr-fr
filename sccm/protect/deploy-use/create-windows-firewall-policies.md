---
title: Stratégies de pare-feu Windows pour Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment créer et déployer des stratégies de pare-feu pour Endpoint Protection dans System Center 2012 Configuration Manager.
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 6ecdfad1-6305-45a8-ae75-3f33b967cb8f
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3217fe8f6d9ee541105abdecf9963898af38b907
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111023"
---
# <a name="create-and-deploy-windows-firewall-policies-for-endpoint-protection-in-system-center-configuration-manager"></a>Créer et déployer des stratégies de Pare-feu Windows pour Endpoint Protection dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les stratégies de pare-feu pour Endpoint Protection dans System Center Configuration Manager vous permettent d'effectuer des tâches de maintenance et de configuration de pare-feu Windows de base sur les ordinateurs client de votre hiérarchie. Vous pouvez utiliser les stratégies de pare-feu Windows pour effectuer les tâches suivantes :  

-   Contrôler si le pare-feu Windows est activé ou désactivé.  

-   Contrôler si les connexions entrantes sont autorisées vers les ordinateurs client.  

-   Contrôler si les utilisateurs sont avertis lorsque le pare-feu Windows bloque un nouveau programme.  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l’espace de travail **Ressources et Conformité**, développez **Endpoint Protection**, puis cliquez sur **Stratégies de Pare-feu Windows**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie de pare-feu Windows**.  

4.  Sur la page **Général** de l' **Assistant Création d'une stratégie de pare-feu Windows**, spécifiez un nom et une description facultative pour cette stratégie de pare-feu, puis cliquez sur **Suivant**.  

5.  Sur la page **Paramètres de profil** de l'Assistant, configurez les paramètres suivants pour chaque profil réseau :  

    > [!IMPORTANT]  
    >  Si vous souhaitez déployer des stratégies de pare-feu Windows sur les ordinateurs exécutant Windows Server 2008 et Windows Vista Service Pack 1, vous devez d'abord installer le [correctif KB971800](http://go.microsoft.com/fwlink/p/?LinkId=231239) sur ces ordinateurs.  

    > [!NOTE]  
    >  Pour plus d'informations sur les profils réseau, consultez la documentation Windows.  

    -   **Activer le pare-feu Windows**  

        > [!NOTE]  
        >  Si l'option **Activer le pare-feu Windows** n'est pas activée, les autres paramètres de cette page de l'Assistant ne sont pas disponibles.  

    -   **Bloquer toutes les connexions entrantes, y compris celles figurant dans la liste de programmes autorisés**  

    -   **Informer l'utilisateur lorsque le Pare-feu Windows bloque un nouveau programme**  

6.  Dans la page **Résumé** de l'Assistant, consultez les mesures à prendre, puis fermez l'Assistant.  

7.  Vérifiez que la nouvelle stratégie de pare-feu Windows s'affiche dans la liste **Stratégies de pare-feu Windows** .  

##  <a name="BKMK_Assign"></a> Pour déployer une stratégie de pare-feu Windows  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l’espace de travail **Ressources et Conformité**, développez **Endpoint Protection**, puis cliquez sur **Stratégies de Pare-feu Windows**.  

3.  Dans la liste **Stratégies de pare-feu Windows** , sélectionnez la stratégie de pare-feu Windows que vous souhaitez déployer.  

4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

5.  Dans la boîte de dialogue **Déployer la stratégie de pare-feu Windows** , spécifiez le regroupement auquel vous souhaitez affecter cette stratégie de pare-feu Windows et spécifiez un calendrier d'attribution. La stratégie de pare-feu Windows évalue la conformité à l'aide de ce calendrier d'attribution et des paramètres de pare-feu Windows sur les clients à reconfigurer afin qu'elle corresponde à la stratégie de pare-feu Windows.  

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Déployer la stratégie de Pare-feu Windows** et déployer la stratégie de Pare-feu Windows.  

    > [!IMPORTANT]  
    >  Lorsque vous déployez une stratégie de pare-feu Windows vers un regroupement, cette stratégie s'applique aux ordinateurs dans un ordre aléatoire pendant une période de 2 heures pour éviter d'inonder le réseau.
