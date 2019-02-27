---
title: Tableau de bord Cycle de vie du produit
titleSuffix: Configuration Manager
description: Affichez la stratégie de cycle de vie Microsoft avec le tableau de bord Cycle de vie des produits dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 716c5218eafaf6297292fdd852589b7327e2ecaa
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56120025"
---
# <a name="manage-microsoft-lifecycle-policy-with-configuration-manager"></a>Gérer la stratégie de cycle de vie Microsoft avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

À compter de la version 1806, vous pouvez utiliser le tableau de bord Cycle de vie des produits de Configuration Manager pour afficher la stratégie de cycle de vie Microsoft. Ce tableau de bord affiche l’état de la stratégie de cycle de vie Microsoft des produits Microsoft installés sur des appareils gérés avec Configuration Manager. Il vous fournit également des informations sur les produits Microsoft de votre environnement, leur état de support et leur date de fin de support. Utilisez le tableau de bord pour comprendre la disponibilité du support de chaque produit. Ces informations vous aident à planifier quand mettre à jour les produits Microsoft que vous utilisez avant la fin actuelle de leur prise en charge.  

Pour plus d’informations, consultez [Stratégie de cycle de vie Microsoft](https://support.microsoft.com/lifecycle).

Depuis la version 1810, le tableau de bord comprend des informations pour System Center 2012 Configuration Manager et les versions ultérieures<!--1358702-->.  



## <a name="prerequisites"></a>Prérequis 

 Pour afficher les données dans le tableau de bord de cycle de vie des produits, les composants suivants sont nécessaires :  

- Internet Explorer 9 ou version ultérieure doit être installé sur l’ordinateur qui exécute la console Configuration Manager.  

- Un point de Reporting Services est nécessaire pour la fonctionnalité de lien hypertexte dans le tableau de bord. Le tableau de bord est lié à des rapports SQL Server Reporting Services (SSRS). Pour plus d’informations, consultez [Rapports dans Configuration Manager](/sccm/core/servers/manage/reporting).  

- Le point de synchronisation Asset Intelligence doit être configuré et synchronisé. Le tableau de bord utilise le catalogue Asset Intelligence sous forme de métadonnées pour les noms des produits. Les métadonnées sont comparées aux données d’inventaire dans votre hiérarchie. Pour plus d’informations, consultez [Configurer Asset Intelligence dans Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).  

     > [!NOTE]  
     > Si vous configurez le point de service Asset Intelligence pour la première fois, veillez à [activer les classes d’inventaire matériel Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). Le tableau de bord de cycle de vie dépend de ces classes d’inventaire matériel Asset Intelligence. Le tableau de bord n’affiche pas de données tant que les clients n’ont pas analysé et retourné d’inventaire matériel.  



## <a name="use-the-product-lifecycle-dashboard"></a>Utiliser le tableau de bord de cycle de vie des produits

En fonction des données d’inventaire que le site collecte à partir d’appareils gérés, le tableau de bord affiche des informations sur tous les produits actuels. Toutefois, les informations affichées pour les systèmes d’exploitation et SQL Server sont limitées aux versions suivantes :

- Windows Server 2008 et versions ultérieures
- Windows XP et versions ultérieures
- SQL Server 2008 et versions ultérieures

Pour accéder au tableau de bord de cycle de vie dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, développez **Asset Intelligence**, puis sélectionnez le nœud **Cycle de vie du produit**.

> [!NOTE]  
> Les données dans le tableau de bord sont basées sur le site auquel la console Configuration Manager se connecte. Si la console se connecte à votre site de niveau supérieur, les données pour l’ensemble de la hiérarchie s’affichent. Lorsqu’elle est connectée à un site principal enfant, seules les données de ce site s’affichent.

### <a name="product-lifecycle-dashboard"></a>Tableau de bord Cycle de vie du produit

![Capture d’écran du tableau de bord de cycle de vie des produits dans la console](media/product-lifecycle-dashboard.png)

Modifiez l’affichage en sélectionnant l’une des options suivantes dans la liste **Catégorie de produit** :  
- **Tous** : affiche tous les produits  
- **Client Windows** : affiche les versions du système d’exploitation de client Windows  
- **Windows Server** : affiche les versions du système d’exploitation de serveur Windows  
- **Base de données** : affiche les versions de SQL Server  
- **Configuration Manager** : depuis la version 1810, affiche les versions de Configuration Manager  

Le tableau de bord comporte les vignettes suivantes :  

- **Cinq produits principaux dont la fin de vie est dépassée** : cette mosaïque est une vue de données consolidée des produits de votre environnement dont la fin de vie est dépassée. Lors de la comparaison avec le cycle de vie du support pour les systèmes d’exploitation et les produits SQL Server, le graphe affiche les logiciels installés qui ont expiré.  

- **Cinq produits principaux dont la fin de vie est proche** : cette mosaïque est une vue de données consolidée des produits de votre environnement dont la fin de vie est prévue dans les dix-huit prochains mois. Lors de la comparaison avec le cycle de vie du support pour les systèmes d’exploitation et les produits SQL Server, le graphe affiche les logiciels installés dont la fin de vie est prévue dans les dix-huit prochains mois.  

- **Données de cycle de vie des produits installés** : cette mosaïque vous donne une idée générale du moment de la transition d’un produit de l’état pris en charge à l’état expiré. Le graphe fournit une répartition du nombre de clients où le produit est installé, l’état de disponibilité du support, ainsi qu’un lien pour en savoir plus sur les étapes à suivre. Les informations suivantes sont incluses dans le graphe :     
    - Temps de prise en charge restant
    - Nombre dans l’environnement 
    - Date de fin de la prise en charge grand public
    - Date de fin de la prise en chargé étendue
    - Étapes suivantes  

> [!IMPORTANT]  
> Les informations affichées dans ce tableau de bord sont fournies pour des raisons pratiques et uniquement destinées à une utilisation en interne dans votre entreprise. Vous ne devez pas vous fier uniquement à ces informations pour confirmer la conformité. Veillez à vérifier l’exactitude des informations fournies, ainsi que la disponibilité des informations de support en consultant le site [Politique de support Microsoft](https://support.microsoft.com/lifecycle).  



## <a name="reporting"></a>Rapports

Des rapports supplémentaires sont également disponibles. Dans l’espace de travail **Analyse** de la console Configuration Manager, développez le nœud **Création de rapports**, puis **Rapports**. Les nouveaux rapports ci-dessous sont ajoutés sous la catégorie **Asset Intelligence** :  

- **Cycle de vie 01A : ordinateurs avec un produit logiciel spécifique** : Afficher une liste des ordinateurs sur lesquels un produit spécifique est détecté.  

- **Cycle de vie 02A : liste des machines avec des produits arrivés à expiration dans l’organisation** : Afficher les ordinateurs sur lesquels des produits arrivés à expiration sont installés. Vous pouvez filtrer ce rapport par nom de produit.

- **Cycle de vie 03A : liste des produits arrivés à expiration dans l’organisation** : Afficher les détails sur les produits de votre environnement dont les dates du cycle de vie ont expiré.  

- **Cycle de vie 04A : vue d’ensemble du cycle de vie des produits** : Afficher une liste des cycles de vie des produits. Filtrez la liste par nom de produit et par nombre de jours avant l’expiration.  

- **Cycle de vie 05A : tableau de bord Cycle de vie du produit** : À compter de la version 1810, ce rapport comporte des informations comparables à celles du tableau de bord de la console. Sélectionnez une catégorie pour afficher le nombre de produits présents dans votre environnement ainsi que le nombre de jours de support restants.  

Pour plus d’informations, consultez [Liste des rapports](/sccm/core/servers/manage/list-of-reports#asset-intelligence).<!--SCCMDocs issue 997-->  
