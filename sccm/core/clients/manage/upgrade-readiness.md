---
title: Upgrade Readiness
titleSuffix: Configuration Manager
description: Intégrez Upgrade Readiness à Configuration Manager pour accéder aux appareils cibles et aux données de compatibilité de mise à niveau vers Windows 10 pour la mise à niveau ou la correction.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/04/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 68407ab8-c205-44ed-9deb-ff5714451624
ms.openlocfilehash: 0ba5a484fe11185b46125de0d8764bce153f577d
ms.sourcegitcommit: a2ecd84d93f431ee77848134386fec14031aed6a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/29/2019
ms.locfileid: "55230849"
---
# <a name="integrate-upgrade-readiness-with-configuration-manager"></a>Intégrer Upgrade Readiness à Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Upgrade Readiness fait partie de [Windows Analytics](https://docs.microsoft.com/windows/deployment/upgrade/manage-windows-upgrades-with-upgrade-readiness). Il vous permet d’évaluer et d’analyser l’état de préparation des appareils de votre environnement en vue d’une mise à niveau vers Windows 10. Intégrez Upgrade Readiness à Configuration Manager pour accéder aux données de compatibilité de mise à niveau du client dans la console Configuration Manager. Utilisez ensuite ces données pour créer des regroupements et cibler des appareils à des fins de mise à niveau ou de correction.



## <a name="configure-clients"></a>Configurer des clients

Upgrade Readiness s’appuie sur les données de Windows Analytics. Pour qu’Upgrade Readiness reçoive suffisamment de données, les prérequis suivants doivent être configurés :

- Configurer tous les clients avec une *clé d’ID commercial*  

- Configurer les clients Windows 10 pour que Windows Analytics crée des rapports au niveau des données de base  

- Pour les clients exécutant Windows 7 ou 8.1 :  

    - Installer les mises à jour comme décrit dans [Bien démarrer avec Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-get-started#deploy-the-compatibility-update-and-related-kbs)  

    - Activer les paramètres client Windows Analytics  

Configurez ces paramètres à l’aide des paramètres client Configuration Manager. Pour plus d’informations, consultez [Utiliser Windows Analytics](/sccm/core/clients/manage/monitor-windows-analytics).

> [!NOTE]  
> Le déploiement des mises à jour prérequises correctes et la configuration des paramètres client devraient suffire dans la plupart des environnements. Si Upgrade Readiness ne reçoit pas les données envoyées par les appareils de votre environnement, vous pouvez traiter certains de ces problèmes à l’aide du [script de déploiement Upgrade Readiness](https://docs.microsoft.com/windows/deployment/upgrade/upgrade-readiness-deployment-script). 



## <a name="connect-configuration-manager-to-upgrade-readiness"></a>Connecter Configuration Manager à Upgrade Readiness

Utilisez [l’Assistant des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour simplifier le processus de configuration des services Azure que vous utilisez avec Configuration Manager. Pour connecter Configuration Manager à Upgrade Readiness, créez une inscription d’application Azure Active Directory (Azure AD) de type *application web/API* dans le [portail Azure](https://portal.azure.com). Pour plus d’informations sur la création d’une inscription d’application, consultez [Inscrire votre application avec votre locataire Azure AD](/azure/active-directory/active-directory-app-registration). 

Dans le portail Azure, attribuez à votre application web nouvellement inscrite les autorisations suivantes :
- Autorisations *Lecteur* sur le groupe de ressources qui contient l’espace de travail Log Analytics avec vos données Upgrade Readiness
- Autorisations *Contributeur* à l’espace de travail Log Analytics qui héberge vos données Upgrade Readiness

L’Assistant des services Azure utilise cette inscription d’application pour permettre à Configuration Manager de communiquer en toute sécurité avec Azure AD et de connecter votre infrastructure à vos données Upgrade Readiness.

> [!IMPORTANT]  
> Attribuez les autorisations à l’application elle-même, pas à une identité d’utilisateur Azure AD. C’est l’application inscrite qui accède aux données au nom de votre infrastructure Configuration Manager. Pour accorder les autorisations, recherchez le nom de l’inscription d’application dans la zone **Ajouter des utilisateurs** au moment d’attribuer l’autorisation. 
> 
> Ce processus est le même que lors de la fourniture à Configuration Manager d’autorisations sur Log Analytics. Ces étapes doivent être effectuées avant d’importer l’inscription d’application dans Configuration Manager avec l’*Assistant Services Azure*.
> 
> Pour plus d’informations, consultez [Connecter Configuration Manager à Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm).


### <a name="use-the-azure-wizard-to-create-the-connection"></a>Utiliser l’Assistant Azure pour créer la connexion

Suivez les instructions données dans [Configurer les services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour créer une connexion à Upgrade Readiness en important l’inscription d’application web créée ci-dessus. 

Si l’importation d’application web a réussi et si les autorisations appropriées sont attribuées dans le portail Azure, la page *Configuration* préremplit les valeurs suivantes :   
-  Abonnements Azure  
-  Groupe de ressources Azure  
-  Espace de travail Windows Analytics  

Plusieurs groupes de ressources ou espaces de travail sont disponibles dans les circonstances suivantes : 
- Si l’application web Azure AD inscrite a les autorisations de *contributeur* sur plusieurs groupes de ressources   
- Si le groupe de ressources sélectionné a plusieurs espaces de travail Log Analytics  



## <a name="view-and-use-upgrade-readiness-information-in-configuration-manager"></a>Afficher et utiliser les informations Upgrade Readiness dans Configuration Manager

Une fois que vous avez intégré Upgrade Readiness à Configuration Manager, vous pouvez afficher l’analyse de la préparation de vos clients pour la mise à niveau.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **Upgrade Readiness**.  

2. Passez les données en revue. Par exemple :  
    - L’état d’Upgrade Readiness  
    - Le pourcentage d’appareils Windows qui créent des rapports sur les données  

3. Filtrez le tableau de bord pour afficher les données d’appareils dans des regroupements spécifiques.  

4. Affichez les appareils dans un état de préparation spécifique et créez un regroupement dynamique de ces appareils. Puis, utilisez ce regroupement pour mettre à niveau ces appareils, ou prenez des mesures pour corriger les appareils qui se trouvent dans un état bloqué.  

> [!Note]  
> Le site synchronise les données avec Upgrade Readiness une fois par semaine.<!--SCCMDocs issue 732--> Pour déclencher manuellement la synchronisation :
> 1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**.  
> 2. Sélectionnez la connexion à Upgrade Readiness dans la liste.  
> 3. Dans le ruban, sélectionnez l’option de synchronisation.  



## <a name="next-steps"></a>Étapes suivantes

- [Effectuer une mise à niveau de Windows vers la dernière version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  
- [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system)  
- [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence)  
