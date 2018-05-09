---
title: Créer des éléments de configuration des données et profils utilisateur
titleSuffix: Configuration Manager
description: Utilisez des éléments de configuration des données et profils dans System Center Configuration Manager pour gérer la redirection de dossiers, les fichiers hors connexion et les profils itinérants.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: e7d1ee430ef07149b77a4e7b250bc3e19788582a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-user-data-and-profiles-configuration-items-in-system-center-configuration-manager"></a>Créer des éléments de configuration des données et profils utilisateur dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les éléments de configuration des données et profils utilisateur dans System Center Configuration Manager contiennent des paramètres permettant de gérer la redirection de dossiers, les fichiers hors connexion et les profils itinérants sur les ordinateurs qui exécutent Windows 8 et versions ultérieures pour les utilisateurs de votre hiérarchie. Par exemple, vous pouvez :  

-   rediriger le dossier Documents d’un utilisateur vers un partage réseau ;  

-   vous assurer que des fichiers spécifiques stockés sur le réseau sont disponibles sur l’ordinateur d’un utilisateur quand la connexion réseau n’est pas disponible ;  

-   configurer les fichiers du profil itinérant d’un utilisateur qui doivent être synchronisés avec un partage réseau quand l’utilisateur se connecte et se déconnecte.  

 Contrairement à d’autres éléments de configuration dans Configuration Manager, vous n’ajoutez pas d’éléments de configuration des données et profils utilisateur à une base de référence de configuration que vous déployez ensuite. Au lieu de cela, vous déployez l’élément de configuration directement à l’aide de la boîte de dialogue **Déployer un élément de configuration des données et profils utilisateur** .  

> [!IMPORTANT]  
>  Vous pouvez uniquement déployer des éléments de configuration des données et profils utilisateur dans des regroupements d’utilisateurs.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Activer les données et profils utilisateur pour les paramètres de compatibilité  
 Utilisez la procédure suivante pour définir la configuration cliente par défaut des paramètres de compatibilité des données et profils utilisateur qui doit s’appliquer à tous les ordinateurs de votre hiérarchie. Si vous voulez appliquer ce paramétrage à certains ordinateurs seulement, créez un paramètre client d’appareil personnalisé et affectez-le à un regroupement qui contient les ordinateurs pour lesquels vous souhaitez utiliser des paramètres de compatibilité des données et profils utilisateur. Pour plus d’informations sur la création de paramètres d’appareil personnalisés, consultez [Guide pratique pour configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md).  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Paramètres client** > **Paramètres par défaut**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Dans la boîte de dialogue **Paramètres par défaut** , cliquez sur **Paramètres de compatibilité**.  

6.  Dans la liste déroulante **Activer les données et profils utilisateurs** , sélectionnez **Oui**.  

7.  Cliquez sur **OK** pour fermer la boîte de dialogue **Paramètres par défaut** .  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Créer un élément de configuration des données et profils utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Données et profils utilisateur**.  

3.  Dans l’onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer l’élément de configuration Données et profils utilisateur**.  

4.  Dans la page **Général** de l’ **Assistant Création d’un élément de configuration des données et profils utilisateur**, spécifiez les informations suivantes :  

    -   **Nom :** entrez un nom unique pour l’élément de configuration. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Description :** Fournissez une description qui donne un aperçu de l'élément de configuration et d'autres informations pertinentes qui permettent son identification dans la console Configuration Manager. Vous pouvez utiliser jusqu'à 256 caractères.  

    -   **Redirection de dossiers :** cochez cette case pour configurer les paramètres de redirection de dossiers pour cet élément de configuration.  

    -   **Fichiers hors connexion :** cochez cette case pour configurer les paramètres des fichiers hors connexion pour cet élément de configuration.  

    -   **Profils utilisateur d’itinérance :** cochez cette case pour configurer les paramètres des profils utilisateur d’itinérance pour cet élément de configuration.  

5.  Dans la page **Redirection de dossiers** de l’ **Assistant Création d’un élément de configuration des données et profils utilisateur**, spécifiez comment vous souhaitez que les ordinateurs clients des utilisateurs qui reçoivent cet élément de configuration gèrent la redirection des dossiers. Vous pouvez configurer les paramètres de n’importe quel appareil auquel l’utilisateur se connecte ou uniquement des appareils principaux de l’utilisateur. Pour plus d’informations sur la redirection de dossiers, consultez la documentation de Windows Server.  

    > [!NOTE]  
    >  Cette page s’affiche uniquement si vous avez coché la case **Redirection de dossiers** dans la page **Général** de l’Assistant.  

6.  Dans la page **Fichiers hors connexion** de l’ **Assistant Création d’un élément de configuration des données et profils utilisateur**, vous pouvez activer ou désactiver l’utilisation des fichiers hors connexion pour les utilisateurs qui reçoivent cet élément de configuration et configurer les paramètres pour le comportement des fichiers hors connexion. Vous pouvez également spécifier les fichiers hors connexion qui seront toujours disponibles sur tout ordinateur auquel l’utilisateur se connecte. Pour plus d’informations sur les fichiers hors connexion, consultez la documentation de Windows Server.  

    > [!NOTE]  
    >  Cette page s’affiche uniquement si vous avez coché la case **Fichiers hors connexion** dans la page **Général** de l’Assistant.  

7.  Dans la page **Profils d’itinérance** de l’ **Assistant Création d’un élément de configuration des données et profils utilisateur**, vous pouvez configurer si les profils d’itinérance sont disponibles sur les ordinateurs auxquels l’utilisateur se connecte et également configurer d’autres informations sur le comportement de ces profils. Pour plus d’informations sur les profils d’itinérance, consultez la documentation de Windows Server.  

    > [!NOTE]  
    >  Cette page s’affiche uniquement si vous avez coché la case **Profils utilisateur d’itinérance** dans la page **Général** de l’Assistant.  

8.  Effectuez toutes les étapes de l'Assistant.  

 Le nouvel élément de configuration des données et profils utilisateur est indiqué dans le nœud **Données et profils utilisateur** de l’espace de travail **Ressources et Conformité** .  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Déployer un élément de configuration des données et profils utilisateur  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Données et profils utilisateur**.  

3.  Sélectionnez l’élément de configuration des données et profils utilisateur que vous souhaitez déployer, puis, dans l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

4.  Dans la boîte de dialogue **Déployer un élément de configuration des données et profils utilisateur** , spécifiez les informations ci-dessous.  

    -   **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement d’utilisateurs dans lequel vous souhaitez déployer l’élément de configuration.  

        > [!IMPORTANT]  
        >  Vous pouvez uniquement déployer des éléments de configuration des données et profils utilisateur dans des regroupements d’utilisateurs.  

    -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** : activez cette option pour résoudre automatiquement toutes les règles qui sont évaluées comme étant non conformes sur les ordinateurs clients.  

    -   **Autoriser les corrections en dehors de la fenêtre de maintenance** : si une fenêtre de maintenance a été configurée pour le regroupement vers lequel vous déployez l’élément de configuration, activez cette option pour laisser les paramètres de compatibilité résoudre la valeur en dehors de la fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance, consultez [Comment utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Générer une alerte** : activez cette option pour configurer une alerte qui est générée si la compatibilité de l’élément de configuration est inférieure à un pourcentage spécifié par une date et une heure spécifiques. Vous pouvez également spécifier si vous souhaitez qu'une alerte soit envoyée à System Center Operations Manager.  

    -   **Spécifier le calendrier d’évaluation de la conformité pour cet élément de configuration** : spécifie le calendrier d’évaluation de l’élément de configuration déployé sur des ordinateurs clients. Il peut s'agir d'un calendrier simple ou d'un calendrier personnalisé.  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Déployer un élément de configuration des données et profils utilisateur** et pour créer le déploiement.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>Surveiller un élément de configuration des données et profils utilisateur  
 Vous surveillez ce type d’élément de configuration de la même façon que vous surveillez les autres paramètres de compatibilité.  

 Pour plus d’informations, consultez [Comment surveiller les paramètres de compatibilité](../../compliance/deploy-use/monitor-compliance-settings.md).  
