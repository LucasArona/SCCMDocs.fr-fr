---
title: Gérer des regroupements
titleSuffix: Configuration Manager
description: Découvrez comment effectuer les principales tâches de gestion des regroupements dans Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5d7c967ce02c009cd9659c7956f7ca79f4a34faf
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42755970"
---
# <a name="how-to-manage-collections-in-configuration-manager"></a>Comment gérer des regroupements dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Aidez-vous des informations générales de cet article pour effectuer les tâches de gestion des regroupements dans Configuration Manager.  

> [!NOTE]  
>  Pour plus d'informations sur la création de regroupements Configuration Manager, voir [Comment créer des regroupements](/sccm/core/clients/manage/collections/create-collections).  



## <a name="bkmk_device"></a> Comment gérer des regroupements d’appareils  

 Dans l'espace de travail **Biens et conformité** , sélectionnez **Regroupements de périphériques**, puis le regroupement à gérer, et enfin sélectionnez une tâche de gestion.  


#### <a name="show-members"></a>Afficher les membres
 Affiche toutes les ressources qui sont membres du regroupement sélectionné dans un nœud temporaire sous le nœud **Périphériques** .


#### <a name="add-selected-items"></a>Ajouter les éléments sélectionnés
 Fournit les options suivantes : 

 - **Ajouter des éléments sélectionnés à un regroupement d’appareils existant** : ouvre la boîte de dialogue **Sélectionner un regroupement**. Sélectionner le regroupement auquel vous souhaitez ajouter les membres du regroupement sélectionné. Le regroupement sélectionné est inclus dans ce regroupement grâce à la règle d'adhésion **Inclure des regroupements** .  

 - **Ajouter des éléments sélectionnés au nouveau regroupement d’appareils** : ouvre l’**Assistant Création d’un regroupement d’appareils** là où vous créez un regroupement. Le regroupement sélectionné est inclus dans ce regroupement grâce à la règle d'adhésion **Inclure des regroupements** .  


 Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](/sccm/core/clients/manage/collections/create-collections).


#### <a name="install-client"></a>Installer le client
 Ouvre l’**Assistant Installer le client**. Cet Assistant utilise la méthode d’installation Push du client pour installer un client Configuration Manager sur tous les ordinateurs du regroupement sélectionné. Pour plus d’informations, consultez [Installation Push du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


#### <a name="run-script"></a>Exécuter un script
 Ouvre l’Assistant **Exécuter le Script** pour exécuter un script PowerShell sur tous les clients du regroupement. Pour plus d’informations, consultez [Créer et exécuter des scripts PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).


#### <a name="manage-affinity-requests"></a>Gérer les demandes d'affinité
 Ouvre la boîte de dialogue **Gérer les requêtes d'affinité entre utilisateur et appareil**. Approuve ou rejette les requêtes en attente pour établir des affinités entre utilisateur et appareil pour les appareils du regroupement sélectionné. Pour plus d’informations, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).


#### <a name="clear-required-pxe-deployments"></a>Effacer les déploiements PXE requis
 Efface tous les déploiements de démarrage PXE requis à partir de tous les membres du regroupement sélectionné. Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).


#### <a name="update-membership"></a>Mettre à jour l'adhésion
 Évalue l'adhésion pour le regroupement sélectionné. Pour les regroupements comportant de nombreux membres, l'exécution de cette mise à jour peut durer un certain temps. Utilisez l'action **Actualiser** pour mettre à jour l'affichage avec les nouveaux membres des regroupements une fois la mise à jour terminée.


#### <a name="add-resources"></a>Ajouter des ressources
 Ouvre la boîte de dialogue **Ajouter des ressources au regroupement**. Recherche de nouvelles ressources à ajouter au regroupement sélectionné. L'icône du regroupement sélectionné affiche un symbole de sablier pendant l'exécution de la mise à jour.


#### <a name="client-notification"></a>Notification du client
 Indique à tous les clients du regroupement d’appareils sélectionnés d’effectuer immédiatement l’une des actions suivantes :

 - **Télécharger la stratégie d’ordinateur** : actualiser la stratégie de l’appareil. Pour plus d’informations, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 - **Télécharger la stratégie utilisateur** : actualiser la stratégie de l’appareil.  

 - **Collecter les données de découverte** : déclencher les clients pour envoyer un enregistrement de données de découverte (DDR). Pour plus d’informations, consultez [Découverte par pulsations d’inventaire](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

 - **Collecter l’inventaire logiciel** : déclencher les clients pour exécuter un cycle d’inventaire logiciel. Pour plus d’informations, consultez [Présentation de l’inventaire logiciel](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  

 - **Collecter l’inventaire matériel** : déclencher les clients pour exécuter un cycle d’inventaire matériel. Pour plus d’informations, consultez [Présentation de l’inventaire matériel](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  

 - **Évaluer les déploiements d’applications** : déclencher les clients pour exécuter un cycle d’évaluation du déploiement application. Pour plus d'informations, consultez [Planifier la réévaluation des déploiements](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  

 - **Évaluer les déploiements de mises à jour logicielles** : déclencher les clients pour exécuter un cycle d’évaluation du déploiement de mises à jour logicielles. Pour plus d’informations, consultez [Présentation de mises à jour logicielles](/sccm/sum/understand/software-updates-introduction).  

 - **Basculez vers le point de mise à jour logicielle suivant** : déclenchez les clients pour basculer vers le point de mise à jour logicielle suivant. Pour plus d’informations, consultez [Basculement de point de mise à jour logicielle](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  

 - **Évaluer l’attestation d’intégrité de l’appareil** : déclenchez les clients Windows 10 pour vérifier et envoyer leur dernier état d’intégrité de l’appareil. Pour plus d’informations, consultez [Attestation d’intégrité](/sccm/core/servers/manage/health-attestation).  

 - **Vérifier la conformité de l'accès conditionnel** : déclenchez les clients pour vérifier leur conformité avec l’accès conditionnel. Pour plus d’informations, consultez [Gérer l’accès aux services O365 pour PC](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


#### <a name="endpoint-protection"></a>Endpoint Protection
 Indique à tous les clients du regroupement d’appareils sélectionnés d’effectuer immédiatement l’une des actions suivantes :

 - **Analyse complète** : déclencher Endpoint Protection ou Windows Defender pour exécuter une analyse *complète* des logiciels malveillants  

 - **Analyse rapide** : déclencher Endpoint Protection ou Windows Defender pour exécuter une analyse *rapide* des logiciels malveillants  

 - **Télécharger la définition** : déclencher Endpoint Protection ou Windows Defender pour télécharger les dernières définitions de logiciels anti-programme malveillant  


 Pour plus d’informations, consultez [Endpoint Protection dans Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).


#### <a name="export"></a>Exporter
 Ouvre l'**Assistant Exportation de regroupements** qui vous aide à exporter ce regroupement dans un fichier MOF (Managed Object Format). Ce fichier peut ensuite être archivé ou importé sur un autre site Configuration Manager. Lorsque vous exportez un regroupement, les regroupements référencés ne sont pas exportés. Un regroupement est référencé par le regroupement sélectionné à l'aide d'une règle **Inclure** ou **Exclure**.


#### <a name="copy"></a>Copier
 Crée une copie du regroupement sélectionné. Le nouveau regroupement utilise le regroupement sélectionné comme limitation au regroupement.


#### <a name="refresh"></a>Actualisation
 Actualiser l'affichage.


#### <a name="delete"></a>Supprimer
 Supprime le regroupement sélectionné. Vous pouvez également supprimer toutes les ressources du regroupement à partir de la base de données du site. 

 Vous ne pouvez pas supprimer les regroupements qui sont intégrés à Configuration Manager. Pour obtenir la liste des regroupements intégrés, consultez [Présentation des regroupements](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections).


#### <a name="simulate-deployment"></a>Simuler un déploiement
 Ouvrez l'**Assistant Simuler un déploiement d'application**. Cet Assistant vous permet de tester les résultats du déploiement d'une application sans installer ou désinstaller l'application. Pour plus d’informations, consultez [Comment simuler des déploiements d’applications](/sccm/apps/deploy-use/simulate-application-deployments).


#### <a name="deploy"></a>Déployer
 Affiche les options suivantes :  

 - **Application** : ouvre l’**Assistant Déploiement logiciel**. Sélectionnez et configurez un déploiement d’application vers le regroupement sélectionné. Pour plus d’informations, consultez [Comment déployer des applications](/sccm/apps/deploy-use/deploy-applications).  

 - **Programme** : ouvre l’**Assistant Déploiement logiciel**. Sélectionnez et configurez un déploiement de package et de programme vers le regroupement sélectionné. Pour plus d’informations, consultez [Packages et programmes](/sccm/apps/deploy-use/packages-and-programs).  

 - **Base de référence de configuration** : ouvre la boîte de dialogue **Déployer des bases de référence de configuration**. Configurer le déploiement d’une ou de plusieurs bases de référence de configuration vers le regroupement sélectionné. Pour plus d’informations, consultez [Guide pratique pour déployer des bases de référence de configuration](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

 - **Séquence de tâches** : ouvre l’**Assistant Déploiement logiciel**. Sélectionner et configurer un déploiement de séquence de tâches vers le regroupement sélectionné. Pour plus d’informations, consultez [Gérer les séquences de tâches pour automatiser des tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

 - **Mises à jour logicielles** : ouvre l’**Assistant Déploiement des mises à jour logicielles**. Configurer le déploiement des mises à jour logicielles vers les ressources du regroupement sélectionné. Pour plus d’informations, consultez [Gérer les mises à jour logicielles](/sccm/sum/understand/software-updates-introduction).  


#### <a name="clear-server-group-deployment-locks"></a>Supprimer les verrous de déploiement du groupe de serveurs
 Libérer manuellement tous les verrous de déploiement de groupe de serveurs pour le regroupement. Pour plus d’informations, consultez [Maintenance d’un groupe de serveurs](/sccm/sum/deploy-use/service-a-server-group).


#### <a name="move"></a>Déplacer
 Déplacer le regroupement sélectionné vers un autre dossier dans le nœud **Regroupement d’appareils**. 


#### <a name="properties"></a>Propriétés
 Pour plus d'informations, consultez [Paramètre du regroupement](#BKMK_CollProp).  



## <a name="bkmk_user"></a>Comment gérer des regroupements d’utilisateurs  

 Dans l'espace de travail **Biens et conformité** , sélectionnez **Regroupements d'utilisateurs**, puis le regroupement à gérer, et enfin sélectionnez une tâche de gestion.  

 > [!Note]  
 > Les actions suivantes sont disponibles sur les regroupements d’utilisateurs, mais les comportements sont identiques à ceux des regroupements d’appareils. Ce n’est pas le cas si elles s’appliquent à des regroupements d’utilisateurs et aux utilisateurs qu’ils contiennent. Pour plus d’informations, consultez l’action correspondante sous [Comment gérer des regroupements d’appareils](#bkmk_device).  

 - **Afficher les membres**  
 - **Ajouter les éléments sélectionnés**  
     - **Ajouter des éléments sélectionnés à un regroupement d'utilisateurs existant**  
     - **Ajouter des éléments sélectionnés à un nouveau regroupement d'utilisateurs**  
 - **Gérer les demandes d'affinité**  
 - **Mettre à jour l'adhésion**  
 - **Ajouter des ressources**  
 - **Exporterer**  
 - **Copier**  
 - **Actualiser**  
 - **Supprimer**  
 - **Simuler un déploiement**  
 - **Déployer**  
     - **Application**  
     - **Programme**  
     - **Base de référence de configuration**   
 - **Déplacer**  
 - **Propriétés**



##  <a name="BKMK_CollProp"></a> Propriétés d’un regroupement  

 Lorsque vous ouvrez la boîte de dialogue **Propriétés** pour un regroupement, vous pouvez afficher et configurer les options suivantes :  

#### <a name="general"></a>Général
 Afficher et configurer des informations générales sur le regroupement sélectionné, y compris le nom du regroupement et la limitation au regroupement.

#### <a name="membership-rules"></a>Règles d'adhésion
 Configurer les règles d'adhésion qui définissent l'adhésion à ce regroupement. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](/sccm/core/clients/manage/collections/create-collections).  

#### <a name="power-management"></a>Gestion de l'alimentation
 Configurer les plans de gestion de l'alimentation que vous avez attribués aux ordinateurs du regroupement sélectionné. Pour plus d’informations, consultez [Présentation de la gestion de l’alimentation](/sccm/core/clients/manage/power/introduction-to-power-management).  

#### <a name="deployments"></a>Déploiements
 Afficher tout logiciel que vous avez déployé vers les membres du regroupement sélectionné.  

#### <a name="maintenance-windows"></a>Fenêtres de maintenance
 Afficher et configurer les fenêtres de maintenance qui sont appliquées aux membres du regroupement sélectionné. Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).

#### <a name="collection-variables"></a>Variables du regroupement
 Configurer des variables qui s'appliquent à ce regroupement et peuvent être utilisées par les séquences de tâches. Pour plus d’informations, consultez [Comment définir la variable de séquence de tâches](/sccm/osd/understand/using-task-sequence-variables#bkmk_set).  

#### <a name="distribution-point-groups"></a>Groupes de points de distribution
 Associer un ou plusieurs groupes de points de distribution à des membres du regroupement sélectionné. Pour plus d’informations, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).

#### <a name="security"></a>Sécurité
 Affiche les utilisateurs administratifs qui disposent d'autorisations pour le regroupement sélectionné à partir de rôles associés et d'étendues de sécurité. Pour plus d’informations, consultez [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).  

#### <a name="alerts"></a>Alertes 
 Configurer le moment où des alertes sont générées pour l'état du client et Endpoint Protection. Pour plus d'informations, consultez [Comment configurer l’état du client](/sccm/core/clients/deploy/configure-client-status) et [Comment surveiller Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection).  
