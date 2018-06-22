---
title: Prérequis pour les sites
titleSuffix: Configuration Manager
description: Découvrez les prérequis liés à l’installation des différents types de sites System Center Configuration Manager.
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 92b339ef-2723-4322-bec6-077b3e8846b0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6e45ec9aca5ee1a14f9058453497003814b2fdb0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340010"
---
# <a name="prerequisites-for-installing-system-center-configuration-manager-sites"></a>Prérequis à l’installation de sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de commencer une installation de site, il est préférable d’en savoir plus sur les prérequis pour l’installation de différents types de sites System Center Configuration Manager.

## <a name="primary-sites-and-the-central-administration-site"></a>Sites principaux et site d’administration centrale
Les prérequis suivants s’appliquent à l’installation d’un site d’administration centrale en tant que premier site d’une hiérarchie, à l’installation d’un site principal autonome ou à l’installation d’un site principal enfant. Si vous installez un site d’administration centrale dans le cadre d’une extension de hiérarchie, consultez [Extension d’un site principal autonome](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand) dans cette rubrique.

###  <a name="bkmk_PrereqPri"></a> Prérequis pour l’installation d’un site principal ou d’un site d’administration centrale  

-   Le compte d’utilisateur qui installe le site doit disposer des droits suivants :  

    -   **Administrateur** sur l’ordinateur serveur de site  
    -   **Administrateur** sur chaque ordinateur devant héberger la **base de données du site** ou une instance du **Fournisseur SMS** pour le site  
    -   **Sysadmin** sur l’instance de SQL Server qui héberge la base de données du site  

        > [!IMPORTANT]  
        >  Une fois l’installation terminée, le compte d’utilisateur qui exécute le programme d’installation et le compte d’ordinateur du serveur de site doivent tous deux conserver des droits d’administrateur système sur SQL Server. Ne supprimez pas les droits d’administrateur système de ces comptes.  

-   Si vous installez un site principal, vous devez disposer des droits supplémentaires suivants :  
    -  **Administrateur** sur les autres ordinateurs où vous allez installer le point de gestion initial et le point de distribution (s’il n’est pas sur le serveur de site)  

-   Si vous installez un nouveau site principal enfant sous un site d’administration centrale, vous devez disposer des droits supplémentaires suivants :  

    -   **Administrateur** sur l’ordinateur hébergeant le site d’administration centrale  

    -   Droits d’administration basée sur des rôles dans Configuration Manager, qui équivalent au rôle de sécurité **Administrateur d’infrastructure** ou **Administrateur complet**  

-   Vous devez utiliser le support d’installation correct (fichiers sources) et exécuter le programme d’installation à partir de cet emplacement. Pour plus d’informations sur les fichiers sources adéquats à utiliser pour installer différents types de sites, consultez [Options d’installation des différents types de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) dans la rubrique [Préparer l’installation des sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md).

-   L’ordinateur serveur de site doit avoir accès aux fichiers d’installation mis à jour de Microsoft de l’une des manières suivantes :
    -  Avant de commencer l’installation, vous pouvez télécharger et stocker une copie de ces fichiers sur votre réseau local à l’aide du [Téléchargeur d’installation](../../../../core/servers/deploy/install/setup-downloader.md).
    -  Si une copie locale de ces fichiers n’est pas disponible, le serveur de site doit avoir accès à Internet pour pouvoir télécharger ces fichiers à partir de Microsoft lors de l’installation.

- Pour pouvoir étendre un site principal autonome ayant un rôle de système de site Point de connexion de service installé, vous devez désinstaller le point de connexion de service. Une seule instance de ce rôle est autorisée dans une hiérarchie, et uniquement sur le site de niveau supérieur de la hiérarchie. Vous avez la possibilité de réinstaller le rôle lors de l’installation du site d’administration centrale.
- Le serveur de site et les ordinateurs de base de données du site doivent présenter toutes les configurations prévues dans les conditions préalables. Avant de démarrer le programme d’installation, vous pouvez [exécuter manuellement l’Outil de vérification des prérequis](../../../../core/servers/deploy/install/prerequisite-checker.md) pour identifier et résoudre les problèmes.  


### <a name="bkmk_expand"></a> Configuration requise pour développer un site principal autonome
Un site principal autonome doit remplir les conditions préalables suivantes pour pouvoir être étendu dans une hiérarchie constituée d'un site d'administration centrale :

-   **Vous devez installer le nouveau site d’administration centrale à l’aide du support d’un dossier CD.Latest (qui contient les fichiers sources) qui correspond à la version du site principal autonome**

 Pour garantir la correspondance de la version, utilisez les fichiers sources figurant dans le [dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder) sur le site principal autonome.

 Pour plus d’informations sur les fichiers sources adéquats à utiliser pour installer différents sites, consultez [Options d’installation des différents types de sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md#bkmk_options) dans la rubrique [Préparer l’installation des sites](../../../../core/servers/deploy/install/prepare-to-install-sites.md).


-   **Le site principal autonome ne peut pas être configuré pour faire migrer les données d’une autre hiérarchie Configuration Manager**  

     Vous devez arrêter la migration active vers le site principal autonome à partir d’autres hiérarchies Configuration Manager, puis supprimer toutes les configurations pour la migration. Sont incluses les tâches de migration qui ne sont pas terminées, la collecte des données et la configuration de la hiérarchie source active.  

     En effet, les opérations de migration sont effectuées par le site de niveau supérieur de la hiérarchie et les configurations à faire migrer ne sont pas transférées au site d’administration centrale quand vous étendez un site principal autonome.  

     Après avoir étendu le site principal autonome, si vous reconfigurez la migration sur le site principal, le site d’administration centrale assure les opérations liées à la migration. Pour plus d’informations sur la configuration de la migration, consultez [Configurer des hiérarchies sources et des sites sources pour la migration vers System Center Configuration Manager](../../../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md).  

-   **Le compte de l’ordinateur appelé à héberger le nouveau site d’administration centrale doit être membre du groupe d’utilisateurs Administrateurs sur le site principal autonome**  

     Pour étendre correctement le site principal autonome, le compte d’ordinateur du nouveau site d’administration centrale doit détenir des droits d’**Administrateur** sur le site principal autonome. Ceci est nécessaire uniquement durant l’extension de site. Vous pouvez supprimer le compte du groupe d’utilisateurs sur le site principal après l’extension du site.  

-   **Le compte d’utilisateur qui exécute le programme d’installation pour installer le nouveau site d’administration centrale doit avoir des droits d’administration basée sur les rôles au niveau du site principal autonome**  

     Pour installer un site d’administration centrale dans le cadre d’une extension de site, le compte d’utilisateur qui exécute le programme d’installation pour installer le site d’administration centrale doit être défini dans l’administration basée sur les rôles sur le site principal autonome en tant qu’**Administrateur complet** ou **Administrateur d’infrastructure**.  

-   **Pour pouvoir étendre le site, vous devez désinstaller les rôles système de site suivants du site principal autonome :**  

    -   Point de synchronisation Asset Intelligence  
    -   Point Endpoint Protection  
    -   point de connexion de service  

   Ces rôles de système de site sont pris en charge uniquement sur le site de niveau supérieur de la hiérarchie. Par conséquent, vous devez désinstaller ces rôles système de site avant d’étendre le site principal autonome. Une fois le site étendu, vous pouvez réinstaller ces rôles de système de site sur le site d'administration centrale.  

    Tous les autres rôles de système de site peuvent rester installés sur le site principal.  

-   **Le port pour SQL Server Service Broker (SSB) doit être ouvert entre le site principal autonome et l’ordinateur qui va installer le site d’administration centrale**  

     Pour répliquer correctement des données entre un site d’administration centrale et un site principal, Configuration Manager exige un port ouvert entre les deux sites, qui sera utilisé par SSB. Quand vous installez un site d’administration centrale et que vous étendez un site principal autonome, la vérification des prérequis ne contrôle pas si le port que vous spécifiez pour SSB est ouvert sur le site principal.  

**Problèmes connus quand vous configurez les services Azure :**  
Lorsque vous utilisez l’un des services Azure suivants avec Configuration Manager et que vous prévoyez de développer un site, vous devez supprimer et recréer la connexion à ce service après avoir développé le site.

Services :  
-       [Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)   (OMS)
-       [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics)
-       [Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)

Pour résoudre ce problème, procédez comme suit :
 1.    Dans la console Configuration Manager, supprimez le service Azure du nœud des services Azure.
 2.    Dans le portail Azure, supprimez du nœud Locataires Azure Active Directory le locataire qui est associé au service.  Cette opération supprime l’application web Azure AD qui est associée au service.  
 3.   Reconfigurez la connexion au service Azure pour l’utiliser avec Configuration Manager.


## <a name="bkmk_secondary"></a> Sites secondaires
Voici les prérequis à l’installation des sites secondaires :
-   L’administrateur qui configure l’installation du site secondaire dans la console Configuration Manager doit avoir des droits d’administration basée sur des rôles qui équivalent au rôle de sécurité **Administrateur d’infrastructure** ou **Administrateur complet**.  
-   Le compte d’ordinateur du site principal parent doit être **Administrateur** sur l’ordinateur serveur du site secondaire.  
-   Lorsque le site secondaire utilise une instance précédemment installée de SQL Server pour héberger la base de données du site secondaire :  

    -   Le **compte d’ordinateur** du site principal parent doit disposer des droits d’administrateur système ( **sysadmin** ) sur l’instance de SQL Server exécutée sur l’ordinateur serveur de site secondaire.  

    -   Le compte **Système local** de l’ordinateur serveur de site secondaire doit disposer des droits d’administrateur système ( **sysadmin** ) sur l’instance de SQL Server exécutée sur cet ordinateur.  

        > [!IMPORTANT]  
        >  Une fois l’installation terminée, les deux comptes doivent conserver les droits d’administrateur système (sysadmin) sur SQL Server. Ne supprimez pas les droits d’administrateur système de ces comptes.  

-   L’ordinateur serveur de site secondaire doit présenter toutes les configurations requises, ce qui inclut SQL Server et les rôles de système de site par défaut du point de gestion et du point de distribution.  
