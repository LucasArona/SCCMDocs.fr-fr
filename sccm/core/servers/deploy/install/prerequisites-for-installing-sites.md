---
title: Prérequis pour les sites
titleSuffix: Configuration Manager
description: Découvrez les prérequis liés à l’installation des différents types de sites Configuration Manager.
ms.date: 04/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f2110b805ac404a6e3c12d66225633b45eb50ae
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501362"
---
# <a name="prerequisites-for-installing-configuration-manager-sites"></a>Prérequis pour l’installation de sites Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de commencer une installation de site, découvrez les prérequis pour l’installation de différents types de sites Configuration Manager.



## <a name="primary-sites-and-the-central-administration-site"></a>Sites principaux et site d’administration centrale

Les prérequis suivants s’appliquent à l’installation d’un des types suivants :
- Un site d’administration centrale en tant que premier site d’une hiérarchie
- Un site principal autonome
- Un site principal enfant

Si vous installez un site d’administration centrale dans le cadre d’une extension de hiérarchie, consultez [Extension d’un site principal autonome](#bkmk_expand).


###  <a name="bkmk_PrereqPri"></a> Prérequis pour l’installation d’un site principal ou d’un site d’administration centrale  

- Les rôles et fonctionnalités Windows Server ainsi que les composants Windows suivants doivent être installés :  
    - .NET Framework 3.5 SP1 (ou version ultérieure)
    - .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2
    - Compression différentielle à distance
    - Windows ADK
    - Redistributable Visual C++  
    
    Pour plus d’informations, consultez [Prérequis des systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012sspreq)  

- Le compte d’utilisateur qui installe le site doit disposer des droits suivants :  

    - **Administrateur** sur les serveurs suivants :  
        - Serveur de site  
        - Chaque serveur qui héberge la **base de données du site**  
        - Chaque instance du **fournisseur SMS** pour le site  

    - **Sysadmin** sur l’instance de SQL Server qui héberge la base de données du site  

        > [!IMPORTANT]  
        >  Lorsque l’installation de Configuration Manager est terminée, le compte d’utilisateur qui exécute le programme d’installation et le compte d’ordinateur du serveur de site doivent tous deux conserver des droits d’administrateur système sur SQL Server. Ne supprimez pas les droits d’administrateur système de ces comptes.  

- Si vous installez un site principal, vous devez disposer des droits supplémentaires suivants :  

    - **Administrateur** sur les autres serveurs où vous installez le point de gestion initial et le point de distribution (s’il n’est pas sur le serveur de site)  

- Si vous installez un nouveau site principal enfant sous un site d’administration centrale, vous devez disposer des droits supplémentaires suivants :  

    - **Administrateur** sur le serveur hébergeant le site d’administration centrale  

    - Droits d’administration basée sur des rôles dans Configuration Manager, qui équivalent au rôle de sécurité **Administrateur d’infrastructure** ou **Administrateur complet**  

- Utilisez les fichiers d’installation sources corrects et exécutez le programme d’installation à partir de cet emplacement. Pour plus d’informations sur les fichiers sources adéquats à utiliser pour installer différents types de sites, consultez [Options d’installation des différents types de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

- Le serveur de site doit avoir accès aux fichiers d’installation mis à jour de Microsoft de l’une des manières suivantes :  

    - Avant de commencer l’installation, téléchargez et stockez une copie de ces fichiers sur votre réseau local. Pour plus d’informations, consultez [Téléchargeur d’installation](/sccm/core/servers/deploy/install/setup-downloader).  

    - Si une copie locale de ces fichiers n’est pas disponible, le serveur de site doit avoir accès à Internet. Il télécharge ces fichiers à partir de Microsoft lors de l’installation.  

- Le serveur de site et le serveur de base de données du site doivent présenter toutes les configurations prévues dans les prérequis. Avant de démarrer le programme d’installation de Configuration Manager, [exécutez manuellement l’Outil de vérification des prérequis](/sccm/core/servers/deploy/install/prerequisite-checker) pour identifier et résoudre les problèmes.  


### <a name="bkmk_expand"></a> Configuration requise pour développer un site principal autonome

Un site principal autonome doit remplir les conditions préalables suivantes pour pouvoir être étendu dans une hiérarchie constituée d'un site d'administration centrale :

#### <a name="source-file-version-matches-site-version"></a>La version du fichier source correspond à la version du site
Installez le nouveau site d’administration centrale à l’aide des documents d’un dossier CD.Latest qui correspond à la version du site principal autonome. Pour garantir la correspondance des versions, utilisez les fichiers sources figurant dans le [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) sur le site principal autonome. 

Pour plus d’informations sur les fichiers sources adéquats à utiliser pour installer différents sites, consultez [Options d’installation des différents types de sites](/sccm/core/servers/deploy/install/prepare-to-install-sites#bkmk_options).  

#### <a name="stop-active-migration-from-another-hierarchy"></a>Arrêter la migration active à partir d’une autre hiérarchie
Le site principal autonome ne peut pas être configuré pour faire migrer les données d’une autre hiérarchie Configuration Manager. Arrêtez la migration active vers le site principal autonome à partir d’autres hiérarchies Configuration Manager, puis supprimez toutes les configurations pour la migration. Ces configurations sont les suivantes : 
- Tâches de migration qui ne sont pas terminées  
- Collecte des données  
- La configuration de la hiérarchie source active  

Cette configuration est nécessaire, car Configuration Manager migre les données à partir du site de niveau supérieur de la hiérarchie. Lorsque vous développez un site principal autonome, les configurations pour la migration ne sont pas transférées vers le site d’administration centrale.  

Après avoir étendu le site principal autonome, si vous reconfigurez la migration sur le site principal, le site d’administration centrale assure les opérations de migration. 

Pour plus d’informations sur la configuration de la migration, consultez [Configurer des hiérarchies sources et des sites sources pour la migration](/sccm/core/migration/configuring-source-hierarchies-and-source-sites-for-migration).  

#### <a name="computer-account-as-administrator"></a>Compte d’ordinateur en tant qu’administrateur
Le compte de l’ordinateur du serveur qui héberge le nouveau site d’administration centrale doit être membre du groupe **Administrateur** sur le site principal autonome. 

Pour étendre correctement le site principal autonome, le compte d’ordinateur du nouveau site d’administration centrale doit détenir des droits d’**Administrateur** sur le site principal autonome. Ceci est nécessaire uniquement durant l’extension de site. Vous pouvez supprimer le compte du groupe d’utilisateurs sur le site principal après l’extension du site.  

#### <a name="installation-account-permissions"></a>Autorisations du compte d’installation
Le compte d’utilisateur qui exécute le programme d’installation de Configuration Manager pour installer le nouveau site d’administration centrale doit avoir des droits d’administration basés sur les rôles au niveau du site principal autonome.

Pour installer un site d’administration centrale dans le cadre d’une extension de site, le compte d’utilisateur qui exécute le programme d’installation pour installer le site d’administration centrale doit être défini dans l’administration basée sur les rôles sur le site principal autonome en tant **qu’Administrateur complet** ou **Administrateur d’infrastructure**.  

#### <a name="top-level-site-roles"></a>Rôles de site de niveau supérieur
Pour pouvoir étendre le site, vous devez désinstaller les rôles système de site suivants du site principal autonome :

- Point de synchronisation Asset Intelligence  
- Point Endpoint Protection  
- point de connexion de service  

Configuration Manager prend uniquement en charge ces rôles sur le site de niveau supérieur de la hiérarchie. Désinstallez ces rôles de système de site avant d’étendre le site principal autonome. Une fois le site étendu, réinstallez ces rôles de système de site sur le site d’administration centrale.  

Tous les autres rôles de système de site peuvent rester installés sur le site principal.  

#### <a name="open-the-sql-server-service-broker-port"></a>Ouvrir le port SQL Server Service Broker
Le port réseau doit être ouvert pour SQL Server Service Broker (SSB) entre le site principal autonome et le serveur pour le site d’administration centrale.  

Pour répliquer correctement des données entre un site d’administration centrale et un site principal, Configuration Manager exige un port ouvert entre les deux sites, qui sera utilisé par SSB. Quand vous installez un site d’administration centrale et que vous étendez un site principal autonome, la vérification des prérequis ne contrôle pas si le port que vous spécifiez pour SSB est ouvert sur le site principal.  

#### <a name="known-issues-with-azure-services"></a>Problèmes connus avec les services Azure
Lorsque vous utilisez l’un des services Azure suivants avec Configuration Manager, après l’extension du site, vous devez supprimer et recréer la connexion à ce service.

- [Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics)  
- [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-readiness)  
- [Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)  

Pour résoudre ce problème, procédez comme suit :
 1. Dans la console Configuration Manager, supprimez le service Azure du nœud des **services Azure**.  

 2. Dans le portail Azure, supprimez le locataire qui est associé au service du nœud Locataires Azure Active Directory. Cette action supprime l’application web Azure AD qui est associée au service.  

 3. Reconfigurez la connexion au service Azure pour l’utiliser avec Configuration Manager.  



## <a name="bkmk_secondary"></a> Sites secondaires

Voici les prérequis à l’installation des sites secondaires :  

- Les rôles et fonctionnalités Windows Server ainsi que les composants Windows suivants doivent être installés :  
    - .NET Framework 3.5 SP1 (ou version ultérieure)
    - .NET Framework 4.5.2,4.6.1,4.6.2,4.7,4.7.1 ou 4.7.2
    - Compression différentielle à distance
    - Redistributable Visual C++  
    
    Pour plus d’informations, consultez [Prérequis des systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012secpreq)  

- L’administrateur qui configure l’installation du site secondaire dans la console Configuration Manager doit avoir des droits d’administration basée sur des rôles qui équivalent au rôle de sécurité **Administrateur d’infrastructure** ou **Administrateur complet**.  

- Le compte d’ordinateur du site principal parent doit être **Administrateur** sur le serveur du site secondaire.  

- Lorsque le site secondaire utilise une instance précédemment installée de SQL Server pour héberger la base de données du site secondaire :  

    - Le compte d’ordinateur du site principal parent doit disposer des droits d’administrateur système (**sysadmin**) sur l’instance de SQL Server exécutée sur le serveur de site secondaire.  

    - Le compte **Système local** de l’ordinateur serveur de site secondaire doit disposer des droits d’administrateur système (**sysadmin**) sur l’instance de SQL Server exécutée sur ce serveur.  

        > [!IMPORTANT]  
        >  Une fois l’installation de Configuration Manager terminée, les deux comptes doivent conserver les droits d’administrateur système (sysadmin) sur SQL Server. Ne supprimez pas les droits d’administrateur système de ces comptes.  

- Le serveur de site secondaire doit présenter toutes les configurations prévues dans les prérequis. Ces configurations incluent SQL Server et les rôles de système de site par défaut du point de gestion et du point de distribution.  
