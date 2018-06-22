---
title: Tableau de bord Cycle de vie du produit
titleSuffix: Configuration Manager
description: Obtenez des informations sur le tableau de bord Cycle de vie du produit dans System Center Configuration Manager.
ms.date: 02/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8b5b144a-0e5f-4fcc-87b2-33b9bcdb5655
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 8f24fcd2d75d34e2d2d69c9c54f4f47991be7301
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335539"
---
# <a name="use-the-product-lifecycle-dashboard-to-manage-microsoft-lifecycle-policy-in-system-center-configuration-manager"></a>Utilisez le tableau de bord Cycle de vie du produit pour gérer la stratégie de cycle de vie Microsoft dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

À partir de la [Technical Preview version 1802](/sccm/core/get-started/capabilities-in-technical-preview-1802), vous pouvez utiliser le tableau de bord Cycle de vie du produit de Configuration Manager. Le tableau de bord affiche l’état de la stratégie de cycle de vie des produits Microsoft installés sur des appareils gérés avec Configuration Manager. Le tableau de bord fournit des informations sur les produits Microsoft dans votre environnement, l’état de prise en charge et les dates de fin de prise en charge. Vous pouvez utiliser le tableau de bord pour comprendre la disponibilité de la prise en charge pour chaque produit. Ce qui vous aide à planifier quand mettre à jour les produits Microsoft que vous utilisez avant la fin de leur prise en charge.  

Pour plus d’informations sur la stratégie de cycle de vie du produit Microsoft, consultez la page [Stratégie de cycle de vie Microsoft](https://support.microsoft.com/en-us/lifecycle).

## <a name="prerequisites"></a>Prérequis 

 Pour afficher les données dans le Tableau de bord Cycle de vie du produit, les conditions suivantes sont requises : 
- Internet Explorer 9 ou version ultérieure doit être installé sur l’ordinateur qui exécute la console Configuration Manager. 
- Un point de Reporting Services est requis pour la fonctionnalité de lien hypertexte dans le tableau de bord dans la mesure où les liens hypertexte mènent à un rapport SQL Server Reporting Services (SSRS). Pour plus d’informations, consultez [Génération de rapports dans System Center Configuration Manager](/sccm/core/servers/manage/reporting). 
- Le point de synchronisation Asset Intelligence doit être configuré et synchronisé. Pour plus d’informations, consultez [Configurer Asset Intelligence dans System Center Configuration Manager](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence).

Les données dans le tableau de bord dépendent du point de synchronisation Asset Intelligence installé. Le tableau de bord utilise le catalogue Asset Intelligence sous forme de métadonnées pour les noms des produits. Les métadonnées sont comparées aux données d’inventaire dans votre hiérarchie. 

>[!NOTE]
>Si vous configurez le point de service Asset Intelligence pour la première fois, veillez à [activer les classes d’inventaire matériel Asset Intelligence](/sccm/core/clients/manage/asset-intelligence/configuring-asset-intelligence#BKMK_EnableAssetIntelligence). Le tableau de bord Cycle de vie dépend des classes d'inventaire matériel Asset Intelligence et n’affiche pas de données tant que les clients n’ont pas établi et retourné un inventaire matériel.  

## <a name="use-the-microsoft-product-lifecycle-dashboard"></a>Utilisez le tableau de bord Cycle de vie du produit Microsoft

Selon les données d’inventaire que vous collectez à partir des appareils gérés, le tableau de bord affiche des informations sur tous les produits actuels. Toutefois, les informations affichées pour les systèmes d’exploitation et SQL Server sont limitées aux versions suivantes :

- Windows Server 2008 et versions ultérieures
- Windows XP et versions ultérieures
- SQL Server 2008 et versions ultérieures

Pour accéder au tableau de bord Cycle de vie dans la console Configuration Manager, accédez à **Biens et conformité** > **Asset Intelligence** > **Cycle de vie du produit** .

>[!NOTE]
>Les données dans le tableau de bord sont basées sur le site auquel la console Configuration Manager se connecte. Si la console se connecte à votre site de niveau supérieur, les données pour l’ensemble de la hiérarchie s’affichent. Lorsqu’elle est connectée à un site principal enfant, seules les données de ce site s’affichent.

### <a name="product-lifecycle-dashboard"></a>Tableau de bord Cycle de vie du produit

![Tableau de bord Cycle de vie du produit](/sccm/core/clients/manage/asset-intelligence/media/product-lifecycle-dashboard.png)

Le tableau de bord comporte les vignettes suivantes : 
- **Cinq produits principaux dont la fin de vie est écoulée :** cette vignette est une vue consolidée des produits dans votre environnement dont la fin de vie est écoulée. Le graphe affiche les logiciels installés qui ont expiré lors de la comparaison avec le cycle de vie du produit pour les systèmes d’exploitation et les produits SQL Server.  
- **Cinq produits principaux dont la fin de vie est proche :** cette vignette est une vue consolidée des produits dans votre environnement dont la fin de vie est prévue dans les six prochains mois. Le graphe affiche les logiciels installés dont la fin de vie est prévue dans les six prochains mois lors de la comparaison avec le cycle de vie du produit pour les systèmes d’exploitation et les produits SQL Server.
- **Données du cycle de vie des produits installés :** cette vignette vous donne une idée générale du moment de la transition d’un produit de l’état pris en charge à l’état expiré. Le graphe fournit une répartition du nombre de clients où le produit est installé, l’état de disponibilité de prise en charge, avec un lien pour en savoir plus sur les étapes à suivre. Les informations suivantes sont incluses dans le graphe :     
    - Temps de prise en charge restant
    - Nombre dans l’environnement 
    - Date de fin de la prise en charge grand public
    - Date de fin de la prise en chargé étendue
    - Étapes suivantes 

>[!IMPORTANT]
>Les informations affichées dans ce tableau de bord sont fournies pour des raisons pratiques et uniquement destinées à une utilisation en interne dans votre entreprise. Vous ne devez pas vous fier uniquement à ces informations pour confirmer la conformité. Veillez à vérifier l’exactitude des informations fournies, ainsi que la disponibilité des informations de prise en charge en consultant le site https://support.microsoft.com/en-us/lifecycle.

## <a name="reporting"></a>Rapports
Les nouveaux rapports ci-dessous sont ajoutés sous la catégorie **Cycle de vie du produit** :
- **Vue d’ensemble du cycle de vie du produit général :** affichez la liste des cycles de vie des produits. La liste peut être filtrée par nom de produit et de jours restants avant l’expiration définissables par l’utilisateur. 
- **Ordinateurs équipés d’un logiciel spécifique :** affichez la liste des ordinateurs sur lesquels un produit spécifique est détecté.
- **Liste des produits expirés trouvés dans l’organisation :** affichez les détails sur les produits dans votre environnement dont les dates du cycle de vie ont expiré. 
- **Liste des ordinateurs avec des produits expirés dans l’organisation :** affichez les ordinateurs sur lesquels des produits ont expiré. Vous pouvez filtrer ce rapport par nom de produit.

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).  

