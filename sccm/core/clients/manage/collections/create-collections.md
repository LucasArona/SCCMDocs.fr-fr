---
title: Créer des regroupements
titleSuffix: Configuration Manager
description: Créez des regroupements dans Configuration Manager pour faciliter la gestion des groupes d’utilisateurs et d’appareils.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 40cb1a96771181b395ec2f628e0f0c3c2efe29b7
ms.sourcegitcommit: 53f2380ac67025fb4a69fc1651edad15d98e0cdd
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2019
ms.locfileid: "65673312"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Comment créer des regroupements dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les regroupements sont des groupes d’utilisateurs ou d’appareils. Utilisez les regroupements pour effectuer des tâches comme la gestion d’applications, le déploiement de paramètres de compatibilité ou l’installation de mises à jour logicielles. Vous pouvez également utiliser des regroupements pour gérer des groupes de paramètres client ou les utiliser avec l’administration basée sur les rôles pour définir les ressources auxquelles un utilisateur administratif peut accéder. Configuration Manager contient plusieurs regroupements intégrés. Pour plus d’informations, consultez [Présentation des regroupements](/sccm/core/clients/manage/collections/introduction-to-collections).  

> [!NOTE]  
> Un regroupement peut contenir des utilisateurs ou des appareils, mais pas les deux.  


Utilisez cet article pour créer des regroupements dans Configuration Manager. Vous pouvez aussi importer des regroupements créés sur ce site ou sur un autre site Configuration Manager. Pour plus d'informations sur l’exportation et l’importation de regroupements, consultez [Comment gérer des regroupements](/sccm/core/clients/manage/collections/manage-collections).  



## <a name="collection-rules"></a>Règles de regroupement

Il existe différentes règles que vous pouvez utiliser pour configurer les membres d’un regroupement dans Configuration Manager.  


### <a name="direct-rule"></a>Règle directe

Utilisez les règles directes pour choisir les utilisateurs ou les ordinateurs à ajouter à un regroupement. Cette appartenance ne change pas, à moins qu’une ressource soit supprimée de Configuration Manager. Configuration Manager doit avoir découvert les ressources ou vous devez les avoir importées pour pouvoir les ajouter à un regroupement à règle directe. Les regroupements avec règle directe ont une surcharge administrative plus élevée que celle des regroupements avec règle de requête, car ils nécessitent des modifications manuelles.


### <a name="query-rule"></a>Règle de requête

Les règles de requête mettent à jour dynamiquement l’appartenance à un regroupement en fonction d’une requête que Configuration Manager exécute selon une planification. Par exemple, vous pouvez créer un regroupement d'utilisateurs membres de l'unité d'organisation Ressources Humaines dans les services de domaine Active Directory. Ce regroupement est automatiquement mis à jour quand de nouveaux utilisateurs sont ajoutés ou supprimés dans l’unité d’organisation Ressources Humaines.

Pour obtenir des exemples de requêtes que vous pouvez utiliser pour créer des regroupements, consultez [Comment créer des requêtes](/sccm/core/servers/manage/create-queries).


### <a name="device-category-rule"></a>Règle de catégorie d’appareil

Vous pouvez faciliter la gestion de vos appareils en associant des catégories d’appareils aux regroupements d’appareils. 

Pour plus d’informations, consultez [Classement automatiquement des appareils dans des regroupements](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Règle Inclure des regroupements

Inclure les membres d’un autre regroupement dans un regroupement Configuration Manager. Si le regroupement inclus change, Configuration Manager met à jour l’appartenance du regroupement actuel d’après un planning.

Vous pouvez ajouter plusieurs règles d’inclusion de regroupement à un regroupement.


### <a name="exclude-collection-rule"></a>Règle Exclure des regroupements

La règle Exclure des regroupements permet d’exclure les membres d’un autre regroupement d’un regroupement Configuration Manager. Si le regroupement exclu change, Configuration Manager met à jour l’appartenance du regroupement actuel d’après un planning.

Vous pouvez ajouter plusieurs règles d’exclusion de regroupement à un regroupement. Si un regroupement inclut des règles d’inclusion et d’exclusion de regroupement et qu’il existe un conflit, la règle d’exclusion de regroupement est prioritaire.

#### <a name="example"></a>Exemple
vous créez un regroupement qui comporte une seule règle d’inclusion de regroupement et une seule règle d’exclusion de regroupement. La règle d’inclusion concerne un regroupement d’ordinateurs de bureau Dell. La règle d’exclusion concerne un regroupement d’ordinateurs qui possèdent moins de 4 Go de RAM. Le nouveau regroupement contient les ordinateurs de bureau Dell qui ont au moins 4 Go de RAM.



## <a name="bkmk_create"></a> Création d’un regroupement  

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Actifs et conformité**.  

    - Pour créer un *regroupement d’appareils*, sélectionnez le nœud **Regroupements d’appareils**. Puis, sur l’onglet **Accueil** du ruban, dans le groupe **Créer**, choisissez **Créer un regroupement d’appareils**.  

    - Pour créer un *regroupement d’utilisateurs*, sélectionnez le nœud **Regroupements d’utilisateurs**. Puis, sur l’onglet **Accueil** du ruban, dans le groupe **Créer**, choisissez **Créer un regroupement d’utilisateurs**.  

2. Dans la page **Général** de l’Assistant, fournissez un **Nom** et un **Commentaire**. Dans la section **Limitation au regroupement**, choisissez **Parcourir** pour sélectionner un regroupement de limitation. Le regroupement que vous créez contiendra uniquement les membres de la limitation au regroupement.  

4. Sur la page **Règles d’adhésion**, dans la liste **Ajouter une règle**, sélectionnez le type de règle d’adhésion à utiliser pour le regroupement. Vous pouvez configurer plusieurs règles pour chaque regroupement. La configuration varie pour chaque règle. Pour plus d’informations sur la configuration de chaque règle, consultez les sections suivantes :  
    - [Règle directe](#bkmk-direct)
    - [Règle de requête](#bkmk-query)
    - [Règle de catégorie d’appareil](#bkmk-category)
    - [Règle Inclure des regroupements](#bkmk-include)
    - [Règle Exclure des regroupements](#bkmk-exclude)

5. De plus, dans la page **Règles d’adhésion**, passez en revue les paramètres suivants :

    - **Utiliser des mises à jour incrémentielles pour ce regroupement** : Sélectionnez cette option pour rechercher et mettre à jour régulièrement les ressources nouvelles ou modifiées uniquement depuis l’évaluation de regroupement précédente. Ce processus est indépendant d’une évaluation de regroupement complète. Par défaut, les mises à jour incrémentielles ont lieu toutes les 5 minutes.  

        > [!IMPORTANT]  
        >  Les regroupements avec des règles de requête qui utilisent les classes suivantes ne prennent pas en charge les mises à jour incrémentielles :  
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

    - **Planifier une mise à jour complète sur ce regroupement** : Planifiez une évaluation complète régulière de l’appartenance au regroupement.  

        À compter de la version 1810, les changements suivants apportés au comportement d’évaluation des regroupements peuvent améliorer les performances du site :<!--3607726-->  

        - Auparavant, lorsque vous configuriez une planification sur un regroupement basé sur une requête, le site continuait à évaluer la requête que le paramètre de regroupement **Planifier une mise à jour complète sur ce regroupement** soit activé ou pas. Pour désactiver entièrement la planification, vous deviez modifier la planification sur **Aucun**. 

            Désormais, le site efface la planification lorsque vous désactivez ce paramètre. Pour spécifier une planification pour l’évaluation du regroupement, activez l’option **Planifier une mise à jour complète sur ce regroupement**.  

            Lorsque vous mettez à jour votre site, pour n’importe quel regroupement existant sur lequel vous avez spécifié une planification, le site active l’option **Planifier une mise à jour complète sur ce regroupement**. Bien que cette configuration n’était peut-être pas votre intention, c’était le comportement réel. Pour empêcher que le site évalue un regroupement en fonction d’une planification, désactivez cette option.  

        - Vous ne pouvez pas désactiver l’évaluation de regroupements intégrés, comme **Tous les systèmes**, mais vous pouvez maintenant configurer la planification. Ce comportement vous permet de personnaliser cette action sur une heure qui répond à vos besoins. 

            > [!Tip]  
            > Modifiez uniquement **l’heure** de la planification personnalisée sur les regroupements intégrés. Ne modifiez pas le **modèle de périodicité**. Les itérations futures appliqueront peut-être un modèle de périodicité spécifique.  

6. Terminez l'Assistant pour créer le regroupement. Le nouveau regroupement figure dans le nœud **Regroupements de périphériques** de l'espace de travail **Ressources et conformité**.  

> [!NOTE]  
> Vous devez actualiser ou recharger la console Configuration Manager pour voir les membres du regroupement. Ils n’apparaissent dans le regroupement qu’après la première mise à jour planifiée. Vous pouvez également sélectionner manuellement **Mettre à jour l’adhésion** pour le regroupement. La mise à jour d’un regroupement peut prendre quelques minutes.  

        
### <a name="bkmk-direct"></a> Configuration d’une règle directe  

1. Sur la page **Rechercher des ressources** de l' **Assistant Création d'une règle d'adhésion directe**, spécifiez les informations suivantes :  

    - **Classe de ressource** : sélectionnez le type de ressource à rechercher et à ajouter au regroupement. Par exemple, 
        - **Ressource système** : Recherche des données d’inventaire retournées à partir des ordinateurs clients
        - **Ordinateur inconnu** : Effectuer une sélection à partir des valeurs retournées par des ordinateurs inconnus
        - **Ressource utilisateur** : Recherche des informations utilisateur collectées par Configuration Manager
        - **Ressource groupe d’utilisateurs** : Recherche des informations de groupe d’utilisateurs collectées par Configuration Manager

    - **Nom d’attribut** : sélectionnez l’attribut associé à la classe de ressource sélectionnée à rechercher. Par exemple,  

        - Si vous souhaitez sélectionner des ordinateurs par leur nom NetBIOS, sélectionnez **Ressource système** dans la liste **Classe de ressource** et **NetBIOS nom** dans la liste **Nom d’attribut**.  

        - Si vous voulez sélectionner des utilisateurs par leur nom d’unité d’organisation (UO), sélectionnez **Ressource utilisateur** dans la liste **Classe de ressource** et **Nom de l’unité d’organisation utilisateur** dans la liste **Nom d’attribut**.  

    - **Exclure les ressources signalées comme obsolètes** : Si un ordinateur client est signalé comme obsolète, n’incluez pas cette valeur dans les résultats de la recherche.  

    - **Exclure les ressources sur lesquelles le client Configuration Manager n’est pas installé** : Ces ressources ne s’afficheront dans les résultats de la recherche.  

    - **Valeur** : Entrez une valeur pour rechercher le nom d’attribut sélectionné. Utilisez le caractère de pourcentage `%` comme caractère générique. Par exemple,  
        - Pour rechercher les ordinateurs dont le nom NetBIOS commence par « M », entrez `M%` dans ce champ.  
        - Pour rechercher des utilisateurs dans l’unité d’organisation Contoso, entrez `Contoso` dans ce champ.

2. Dans la page **Sélectionner les ressources**, sélectionnez les ressources à ajouter au regroupement dans la liste **Ressources**, puis choisissez **Suivant**.  


### <a name="bkmk-query"></a> Configuration d’une règle de requête  

Dans la boîte de dialogue **Propriétés de la règle de requête** , définissez les options suivantes :  

- **Nom** : Spécifiez un nom unique pour la requête.  

- **Importer la déclaration de requête** : Ouvre la boîte de dialogue **Parcourir la requête**. Sélectionnez une [requête Configuration Manager](/sccm/core/servers/manage/create-queries) à utiliser comme règle de requête pour le regroupement.   

- **Classe de ressource** : sélectionnez le type de ressource à rechercher et à ajouter au regroupement. Sélectionnez dans les valeurs **Ressource système** pour rechercher des données d'inventaire renvoyées par les ordinateurs clients ou **Ordinateur inconnu** pour sélectionner dans les valeurs renvoyées par les ordinateurs inconnus.  

- **Modifier l’instruction de la requête** : Ouvre la boîte de dialogue **Propriétés de l’instruction de requête** dans laquelle vous pouvez créer une requête à utiliser comme règle pour le regroupement. Pour plus d’informations sur les requêtes, consultez [Présentation des requêtes](/sccm/core/servers/manage/introduction-to-queries).  


### <a name="bkmk-category"></a> Règle de catégorie d’appareil

Les actions suivantes sont disponibles dans la fenêtre **Sélectionner des catégories d’appareils** :

- **Créer** : Spécifiez un nom pour créer une nouvelle catégorie
- **Renommer** : Renommer la catégorie sélectionnée
- **Supprimer** : Sélectionnez une ou plusieurs catégories et utilisez cette action pour les supprimer de la liste

Pour plus d’informations, consultez [Classement automatiquement des appareils dans des regroupements](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections).<!-- SCCMDocs issue 552 -->


### <a name="bkmk-include"></a> Configuration d’une règle d’inclusion de regroupements  

Dans la boîte de dialogue **Sélectionner des regroupements**, sélectionnez les regroupements à inclure dans le nouveau regroupement, puis choisissez **OK**.  


### <a name="bkmk-exclude"></a> Configuration d’une règle d’exclusion de regroupements  

Dans la boîte de dialogue **Sélectionner des regroupements**, sélectionnez les regroupements à inclure dans le nouveau regroupement, puis choisissez **OK**.  



## <a name="bkmk_import"></a> Importation d’un regroupement  

Lorsque vous exportez un regroupement à partir d’un site, Configuration Manager l’enregistre en tant que fichier au format MOF (format d’objet managé). Utilisez cette procédure pour importer ce fichier dans votre base de données de site. Vous devez disposer d’autorisations **Créer** sur la classe de regroupements. 

> [!Important]  
> - Assurez-vous que le fichier contient uniquement des données de regroupement, qu’il provient d’une source de confiance et qu’il n’a pas été falsifié.  
> 
> - Assurez-vous que le fichier a été exporté à partir d’un site exécutant la même version de Configuration Manager.  

Pour plus d’informations sur l’exportation de regroupements, consultez [Comment gérer des regroupements](/sccm/core/clients/manage/collections/manage-collections).


1. Dans la console de Configuration Manager, accédez à l’espace de travail **Actifs et conformité**. Sélectionnez le nœud **Regroupements d’utilisateurs** ou **Regroupements d’appareils**.  

2. Dans l’onglet **Accueil** du ruban, dans le groupe **Créer**, choisissez **Importer des regroupements**.  

3. Dans la page **Général** de l’**Assistant Importation de regroupements**, choisissez **Suivant**.  

4. Sur la page **Nom du fichier MOF**, choisissez **Parcourir**. Accédez au fichier MOF qui contient les informations de regroupement à importer.  

5. Terminez l'Assistant pour importer le regroupement. Le nouveau regroupement figure dans le nœud **Regroupements d’utilisateurs** ou **Regroupements de périphériques** de l’espace de travail **Ressources et Conformité** . Actualisez ou rechargez la console Configuration Manager pour afficher les membres du regroupement récemment importé.  

## <a name="bkmk_powershell"></a> Utilisation de PowerShell

PowerShell peut être utilisé pour créer et importer des regroupements.  Pour plus d'informations, voir :

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)
