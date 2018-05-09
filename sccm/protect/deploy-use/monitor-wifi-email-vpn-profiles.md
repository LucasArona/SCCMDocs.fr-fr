---
title: Surveiller les profils de messagerie, Wi-Fi et VPN
titleSuffix: Configuration Manager
description: Apprenez à surveiller l’état de compatibilité des profils de messagerie, Wi-Fi et VPN dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e2315b8b-98bc-40e1-8ef9-bfb5e69ab109
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 47b5bb12a89143a0c7e6d16a3252948b955b8ff3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="monitor-email-wi-fi-and-vpn-profiles-in-system-center-configuration-manager"></a>Surveiller les profils de messagerie, Wi-Fi et VPN dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois que vous avez déployé des profils de messagerie, Wi-Fi ou VPN System Center Configuration Manager pour des utilisateurs de votre hiérarchie, vous pouvez appliquer les procédures suivantes pour surveiller leur état de compatibilité :  

-   [Comment afficher les résultats de compatibilité dans la console Configuration Manager](#BKMK_console)  

-   [Comment afficher les résultats de compatibilité à l'aide de rapports](#BKMK_Reports)  

##  <a name="BKMK_console"></a> Comment afficher les résultats de compatibilité dans la console Configuration Manager  
 Utilisez cette procédure pour afficher des détails sur la compatibilité des profils déployés dans la console System Center Configuration Manager.  

#### <a name="to-view-compliance-results-in-the-configuration-manager-console"></a>Pour afficher les résultats de compatibilité dans la console Configuration Manager  

1.  Dans la console System Center Configuration Manager, cliquez sur **Surveillance**.  

2.  Dans l'espace de travail **Surveillance** , cliquez sur **Déploiements**.  

3.  Dans la liste **Déploiements**, sélectionnez le déploiement de profil dont vous souhaitez examiner les informations de compatibilité.  

4.  Vous pouvez consulter un résumé des informations de compatibilité du déploiement de profil dans la page principale. Pour afficher des informations plus détaillées, sélectionnez le déploiement de profil puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Afficher l’état** pour ouvrir la page **État du déploiement**.  

     La page **État du déploiement** contient les onglets suivants :  

    -   **Compatible :** indique la compatibilité du profil en fonction du nombre de ressources concernées. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** dans l'espace de travail **Ressources et Conformité** , qui contient tous les utilisateurs compatibles avec ce profil. Le volet **Détails du bien** affiche les utilisateurs compatibles avec le profil. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires.  

        > [!IMPORTANT]  
        >  Un profil n’est pas évalué s’il n’est pas applicable à un appareil client. Cependant, il est renvoyé comme compatible.  

    -   **Erreur** : affiche une liste de toutes les erreurs pour le déploiement de profil sélectionné en fonction du nombre de ressources concernées. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** , qui contient tous les utilisateurs ayant généré des erreurs avec ce profil. Lorsque vous sélectionnez un utilisateur, le volet **Détails du bien** affiche les utilisateurs qui sont concernés par le problème sélectionné. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Non compatible** : affiche une liste de toutes les règles non compatibles au sein du profil en fonction du nombre de ressources concernées. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** , qui contient tous les utilisateurs non compatibles avec ce profil. Lorsque vous sélectionnez un utilisateur, le volet **Détails du bien** affiche les utilisateurs qui sont concernés par le problème sélectionné. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Inconnu** : affiche une liste de tous les utilisateurs qui n’ont pas signalé de compatibilité pour le déploiement de profil sélectionné avec l’état du client actuel des appareils.  

5.  Dans la page **État du déploiement**, vous pouvez consulter des informations détaillées sur la compatibilité du profil déployé. Un nœud temporaire est créé sous le nœud **Déploiements** qui vous aide à retrouver rapidement ces informations.  

##  <a name="BKMK_Reports"></a> Comment afficher les résultats de compatibilité à l'aide de rapports  
 Les paramètres de compatibilité, qui englobent les profils dans System Center Configuration Manager, incluent aussi un certain nombre de rapports intégrés qui permettent de surveiller les informations sur les profils. La catégorie de ces rapports est **Gestion de la conformité et des paramètres**.  

> [!IMPORTANT]  
>  Vous devez utiliser un caractère générique (%) lorsque vous utilisez les paramètres **Filtre d'appareil** et **Filtre d'utilisateur** dans les rapports des paramètres de compatibilité.  

 Pour plus d’informations sur la configuration de la génération de rapports dans System Center Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  
