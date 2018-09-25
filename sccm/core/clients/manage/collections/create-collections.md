---
title: Créer des regroupements
titleSuffix: Configuration Manager
description: Créez des regroupements dans System Center Configuration Manager pour faciliter la gestion des groupes d’utilisateurs et d’appareils.
ms.date: 2/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c314cba909929ee49355eab59dfc813aab7e393e
ms.sourcegitcommit: a849dab9333ebac799812624d6155f2a96b523ca
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/10/2018
ms.locfileid: "42584634"
---
# <a name="how-to-create-collections-in-system-center-configuration-manager"></a>Guide pratique pour créer des regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les regroupements sont des groupes d’utilisateurs ou d’appareils. Utilisez les regroupements pour effectuer des tâches comme la gestion d’applications, le déploiement de paramètres de compatibilité ou l’installation de mises à jour logicielles. Vous pouvez également utiliser des regroupements pour gérer des groupes de paramètres client ou les utiliser avec l’administration basée sur les rôles pour définir les ressources auxquelles un utilisateur administratif peut accéder. Configuration Manager contient plusieurs regroupements intégrés. Pour plus d’informations, consultez [Présentation des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).  

> [!NOTE]  
>  Un regroupement peut contenir des utilisateurs ou des appareils, mais pas les deux.  

 Le tableau suivant répertorie les règles que vous pouvez utiliser pour configurer les membres d’un regroupement dans Configuration Manager.  

|Type de règle d'appartenance|Informations complémentaires|  
|--------------------------|----------------------|  
|Règle directe|Utilisez les règles directes pour choisir les utilisateurs ou les ordinateurs à ajouter à un regroupement. Cette appartenance ne change pas, à moins qu’une ressource soit supprimée de Configuration Manager. Configuration Manager doit avoir découvert les ressources ou vous devez les avoir importées pour pouvoir les ajouter à un regroupement à règle directe. Les regroupements avec règle directe ont une surcharge administrative plus élevée que celle des regroupements avec règle de requête, car ils nécessitent des modifications manuelles.|  
|Règle de requête|Les règles de requête mettent à jour dynamiquement l’appartenance à un regroupement en fonction d’une requête que Configuration Manager exécute selon une planification. Par exemple, vous pouvez créer un regroupement d'utilisateurs membres de l'unité d'organisation Ressources Humaines dans les services de domaine Active Directory. Ce regroupement est automatiquement mis à jour quand de nouveaux utilisateurs sont ajoutés ou supprimés dans l’unité d’organisation Ressources Humaines.<br /><br /> Pour examiner des exemples de requêtes que vous pouvez utiliser pour créer des regroupements, consultez [Guide pratique pour créer des requêtes dans System Center Configuration Manager](../../../../core/servers/manage/create-queries.md).|  
|Règle Inclure des regroupements|Cette règle inclut les membres d’un autre regroupement dans un regroupement Configuration Manager. L’appartenance au regroupement actif est mise à jour selon une planification si le regroupement inclus est modifié.<br /><br /> Vous pouvez ajouter plusieurs règles d’inclusion de regroupement à un regroupement.<br /> |  
|Règle Exclure des regroupements|La règle Exclure des regroupements permet d’exclure les membres d’un autre regroupement d’un regroupement Configuration Manager. L’appartenance du regroupement actuel est mise à jour selon une planification si le regroupement exclu est modifié.<br /><br /> Vous pouvez ajouter plusieurs règles d’exclusion de regroupement à un regroupement. Si un regroupement inclut des règles d’inclusion et d’exclusion de regroupement et qu’il existe un conflit, la règle d’exclusion de regroupement est prioritaire.<br />              **Exemple :** vous créez un regroupement qui comporte une seule règle d’inclusion de regroupement et une seule règle d’exclusion de regroupement. La règle d’inclusion concerne un regroupement d’ordinateurs de bureau Dell. La règle d’exclusion concerne un regroupement d’ordinateurs qui possèdent moins de 4 Go de RAM. Le nouveau regroupement contient les ordinateurs de bureau Dell qui ont au moins 4 Go de RAM.|  

 Utilisez les procédures suivantes pour créer des regroupements dans Configuration Manager. Vous pouvez aussi importer des regroupements créés sur ce site ou sur un autre site Configuration Manager. Pour plus d’informations sur l’exportation et l’importation des regroupements, consultez [Guide pratique pour gérer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

 Pour plus d’informations sur la création de regroupements pour des ordinateurs qui exécutent Linux et UNIX, consultez [Guide pratique pour gérer les clients pour des serveurs Linux et UNIX dans System Center Configuration Manager](../../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md).  

##  <a name="BKMK_1"></a> Pour créer un regroupement d’appareils  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Regroupements de périphériques**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un regroupement de périphériques**.  

4.  Dans la page **Général**, fournissez un **Nom** et un **Commentaire**. Ensuite, dans **Limitation au regroupement**, choisissez **Parcourir** pour sélectionner un regroupement de limitation. Le regroupement contiendra uniquement les membres du regroupement de limitation.  

5.  Dans la page **Règles d’adhésion** de l’**Assistant Création d’un regroupement de périphériques**, dans la liste **Ajouter une règle**, sélectionnez le type de règle d’adhésion que vous voulez utiliser pour le regroupement. Vous pouvez configurer plusieurs règles pour chaque regroupement.  

        
##### <a name="to-configure-a-direct-rule"></a>Pour configurer une règle directe  

1.  Sur la page **Rechercher des ressources** de l' **Assistant Création d'une règle d'adhésion directe**, spécifiez les informations suivantes :  

-   **Classe de ressource** : Sélectionnez le type de ressource à rechercher et ajouter au regroupement. Sélectionnez dans les valeurs **Ressource Système** pour rechercher des données d'inventaire renvoyées par les ordinateurs clients ou **Ordinateur inconnu** pour sélectionner dans les valeurs renvoyées par les ordinateurs inconnus.  

-   **Nom d’attribut** : Sélectionnez l’attribut associé à la classe de ressource sélectionnée que vous voulez rechercher. Par exemple, si vous souhaitez sélectionner des ordinateurs par leur nom NetBIOS, sélectionnez **Ressource Système** dans la liste **Classe de ressource** et **NetBIOS nom** dans la liste **Nom d'attribut** .  

-   **Exclure les ressources signalées comme obsolètes** : si un ordinateur client est signalé comme obsolète, n’incluez pas cette valeur dans les résultats de recherche.  

-   **Exclure les ressources sur lesquelles le client Configuration Manager n’est pas installé** : Elles ne seront pas affichées dans les résultats de recherche.  

-   **Valeur :** entrez une valeur pour laquelle vous voulez rechercher le nom d’attribut sélectionné. Vous pouvez utiliser le caractère de pourcentage ( **%** ) comme caractère générique. Par exemple, pour rechercher les ordinateurs dont le nom NetBIOS commence par « M », entrez **M%** dans ce champ.  

2.  Dans la page **Sélectionner les ressources**, sélectionnez les ressources à ajouter au regroupement dans la liste **Ressources**, puis choisissez **Suivant**.  


##### <a name="to-configure-a-query-rule"></a>Pour configurer une règle de requête  

1.  Dans la boîte de dialogue **Propriétés de la règle de requête** , définissez les options suivantes :  

-   **Nom** : Spécifiez un nom unique.  

-   **Importer l’instruction de requête** : Ouvre la boîte de dialogue **Parcourir la requête** dans laquelle vous pouvez sélectionner une [requête Configuration Manager](../../../../core/servers/manage/create-queries.md) à utiliser comme règle de requête pour le regroupement.   

-   **Classe de ressource :** Sélectionnez le type de ressource à rechercher et ajouter au regroupement. Sélectionnez dans les valeurs **Ressource système** pour rechercher des données d'inventaire renvoyées par les ordinateurs clients ou **Ordinateur inconnu** pour sélectionner dans les valeurs renvoyées par les ordinateurs inconnus.  

-   **Modifier l’instruction de requête** : ouvre la boîte de dialogue **Propriétés de l’instruction de requête** dans laquelle vous pouvez créer une requête à utiliser comme règle pour le regroupement. Pour plus d’informations sur les requêtes, consultez [Informations techniques de référence sur les requêtes pour System Center Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md).  

    
##### <a name="to-configure-an-include-collection-rule"></a>Pour configurer une règle d'inclusion de regroupements  

Dans la boîte de dialogue **Sélectionner des regroupements**, sélectionnez les regroupements à inclure dans le nouveau regroupement, puis choisissez **OK**.  

##### <a name="to-configure-an-exclude-collection-rule"></a>Pour configurer une règle d'exclusion de regroupements  

Dans la boîte de dialogue **Sélectionner des regroupements**, sélectionnez les regroupements à inclure dans le nouveau regroupement, puis choisissez **OK**.  

-   **Utiliser des mises à jour incrémentielles pour ce regroupement** : Sélectionnez cette option pour rechercher et mettre à jour régulièrement uniquement les ressources nouvelles ou modifiées dans l’évaluation de regroupement précédente, indépendamment d’une évaluation de regroupement complète. Par défaut, les mises à jour incrémentielles ont lieu toutes les 5 minutes.  

> [!IMPORTANT]  
>  Les regroupements configurés à l'aide de règles de requête qui utilisent les classes suivantes ne prennent pas en charge les mises à jour incrémentielles :  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **Planifier une mise à jour complète sur ce regroupement** : Planifiez une évaluation complète régulière de l’appartenance au regroupement.  

6.  Terminez l'Assistant pour créer le regroupement. Le nouveau regroupement figure dans le nœud **Regroupements de périphériques** de l'espace de travail **Ressources et conformité**.  

> [!NOTE]  
>  Vous devez actualiser ou recharger la console Configuration Manager pour voir les membres du regroupement. Toutefois, les membres n’apparaissent pas dans le regroupement tant que la première mise à jour planifiée n’est pas effectuée ou que vous ne sélectionnez pas manuellement **Mettre à jour l’appartenance** pour le regroupement. La mise à jour d’un regroupement peut prendre quelques minutes.  

##  <a name="BKMK_2"></a> Pour créer un regroupement d'utilisateurs  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Regroupements d’utilisateurs**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un regroupement d’utilisateurs**.  

4.  Dans la page **Général** de l’Assistant, fournissez un **Nom** et un **Commentaire**. Ensuite, dans **Limitation au regroupement**, choisissez **Parcourir** pour sélectionner un regroupement de limitation. Le regroupement contiendra uniquement les membres du regroupement de limitation.  

5.  Dans la page **Règles d’adhésion**, spécifiez ce qui suit :  

    -   dans la liste **Ajouter une règle** , sélectionnez le type de règle d'adhésion à utiliser pour le regroupement. Vous pouvez configurer plusieurs règles pour chaque regroupement.  

##### <a name="to-configure-a-direct-rule"></a>Pour configurer une règle directe  

1.  Dans la page **Rechercher des ressources** de l’**Assistant Création d’une règle d’adhésion directe**, spécifiez les informations suivantes :  

-   **Classe de ressource** : Sélectionnez le type de ressource à rechercher et ajouter au regroupement. Sélectionnez des valeurs **Ressource utilisateur** pour rechercher les informations utilisateur collectées par Configuration Manager ou **Ressource groupe d’utilisateurs** pour rechercher les informations sur les groupes d’utilisateurs collectées par Configuration Manager.  

-   **Nom d’attribut** : Sélectionnez l’attribut associé à la classe de ressource que vous voulez rechercher. Par exemple, si vous voulez sélectionner des utilisateurs par leur nom d’unité d’organisation (UO), sélectionnez **Ressource utilisateur** dans la liste **Classe de ressource** et **Nom de l’unité d’organisation utilisateur** dans la liste **Nom d’attribut** .  

-   **Valeur :** Entrez une valeur à rechercher. Vous pouvez utiliser le caractère de pourcentage ( **%** ) comme caractère générique. Par exemple, pour rechercher des utilisateurs dans l’unité d’organisation Contoso, entrez **Contoso** dans ce champ.  

2.  Dans la page **Sélectionner les ressources**, sélectionnez les ressources à ajouter au regroupement dans la liste **Ressources**.  

##### <a name="to-configure-a-query-rule"></a>Pour configurer une règle de requête  

1.  Dans la boîte de dialogue **Propriétés de la règle de requête**, fournissez les informations suivantes :  

-   **Nom** : Un nom unique.  

-   **Importer l’instruction de requête** : Ouvre la boîte de dialogue **Parcourir la requête** dans laquelle vous pouvez sélectionner une [requête Configuration Manager](../../../../core/servers/manage/queries-technical-reference.md) à utiliser comme règle de requête pour le regroupement.  

-   **Classe de ressource** : Sélectionnez le type de ressource à rechercher et ajouter au regroupement. Sélectionnez des valeurs **Ressource utilisateur** pour rechercher les informations utilisateur collectées par Configuration Manager ou **Ressource groupe d’utilisateurs** pour rechercher les informations sur les groupes d’utilisateurs collectées par Configuration Manager.  

-   **Modifier l’instruction de requête** : Ouvre la boîte de dialogue **Propriétés de l’instruction de requête** dans laquelle vous pouvez [créer une requête](../../../../core/servers/manage/queries-technical-reference.md) à utiliser comme règle pour le regroupement.  

##### <a name="to-configure-an-include-collection-rule"></a>Pour configurer une règle d'inclusion de regroupements  

Dans la boîte de dialogue **Sélectionner des regroupements**, sélectionnez les regroupements à inclure dans le nouveau regroupement, puis choisissez **OK**.  

##### <a name="to-configure-an-exclude-collection-rule"></a>Pour configurer une règle d'exclusion de regroupements  

Dans la boîte de dialogue **Sélectionner des regroupements**, sélectionnez les regroupements à inclure dans le nouveau regroupement, puis choisissez **OK**.  


-   **Utiliser des mises à jour incrémentielles pour ce regroupement** : Sélectionnez cette option pour rechercher et mettre à jour régulièrement uniquement les ressources nouvelles ou modifiées dans l’évaluation de regroupement précédente, indépendamment d’une évaluation de regroupement complète. Par défaut, les mises à jour incrémentielles ont lieu toutes les 5 minutes.  

> [!IMPORTANT]  
>  Les regroupements configurés à l'aide de règles de requête qui utilisent les classes suivantes ne prennent pas en charge les mises à jour incrémentielles :  
>   
> -   SMS_G_System_CollectedFile  
> -   SMS_G_System_LastSoftwareScan  
> -   SMS_G_System_AppClientState  
> -   SMS_G_System_DCMDeploymentState  
> -   SMS_G_System_DCMDeploymentErrorAssetDetails  
> -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
> -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
> -   SMS_G_User_DCMDeploymentCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
> -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (pour les regroupements d'utilisateurs uniquement)  
> -   SMS_G_System_SoftwareUsageData  
> -   SMS_G_System_CI_ComplianceState  
> -   SMS_G_System_EndpointProtectionStatus  
> -   SMS_GH_System_*  
> -   SMS_GEH_System_*  

-   **Planifier une mise à jour complète sur ce regroupement** : Planifiez une évaluation complète régulière de l’appartenance au regroupement.  

6.  Effectuez toutes les étapes de l'Assistant. Le nouveau regroupement figure dans le nœud **Regroupements d'utilisateurs** de l'espace de travail **Ressources et conformité**.  

> [!NOTE]  
>  Vous devez actualiser ou recharger la console Configuration Manager pour voir les membres du regroupement. Toutefois, les membres n’apparaissent pas dans le regroupement tant que la première mise à jour planifiée n’est pas effectuée ou que vous ne sélectionnez pas manuellement **Mettre à jour l’adhésion** pour le regroupement. La mise à jour d’un regroupement peut prendre quelques minutes.  

##  <a name="BKMK_3"></a> Pour importer un regroupement  

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité** > **Regroupements d’utilisateurs** ou **Regroupements d’appareils**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Importer des regroupements**.  

4.  Dans la page **Général** de l’**Assistant Importation de regroupements**, choisissez **Suivant**.  

5.  Dans la page **Nom du fichier MOF**, cliquez sur **Parcourir**, puis accédez au fichier MOF qui contient les informations de regroupement à importer.  

    > [!NOTE]  
    >  Le fichier à importer doit avoir été exporté à partir d’un site exécutant la même version de Configuration Manager que celui-ci. Pour plus d’informations sur l’exportation de regroupements, consultez [Guide pratique pour gérer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/manage-collections.md).  

6.  Terminez l'Assistant pour importer le regroupement. Le nouveau regroupement figure dans le nœud **Regroupements d’utilisateurs** ou **Regroupements de périphériques** de l’espace de travail **Ressources et Conformité** . Actualisez ou rechargez la console Configuration Manager pour afficher les membres du regroupement récemment importé.  
