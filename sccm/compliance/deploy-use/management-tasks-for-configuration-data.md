---
title: Gérer des données de configuration
titleSuffix: Configuration Manager
description: Après avoir créé les éléments de configuration et les bases de référence de configuration dans System Center Configuration Manager, vous pouvez utiliser d’autres commandes pour effectuer diverses actions.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: b48c693c-d2b0-4707-a5dd-fe92172c49fe
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d4602a2dbee04259d5953873485cdbccdc58167d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333658"
---
# <a name="manage-configuration-data-in-system-center-configuration-manager"></a>Gérer les données de configuration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois que vous avez créé les éléments de configuration et les bases de référence de configuration dans System Center Configuration Manager, vous pouvez utiliser d’autres commandes pour effectuer plus rapidement diverses actions.  

## <a name="manage-configuration-items"></a>Gérer les éléments de configuration  

-   Dans l’espace de travail **Ressources et Conformité**, développez **Paramètres de compatibilité** > **Éléments de configuration**, sélectionnez l’élément de configuration à gérer, puis sélectionnez une tâche de gestion.  

|Tâche de gestion|Détails|  
|---------------------|-------------|  
|**Créer un élément de configuration enfant**|Ouvre l' **Assistant Création d'élément de configuration enfant** où vous pouvez créer un élément de configuration enfant depuis l'élément de configuration sélectionné.<br /><br /> Il n'est pas possible de créer un élément de configuration enfant à partir d'un élément de configuration d’appareil mobile.<br /><br /> Pour plus d’informations, consultez [Créer des éléments de configuration enfants](../../compliance/deploy-use/create-child-configuration-items.md).|  
|**Historique des révisions**|Ouvre la boîte de dialogue **Historique de révision des éléments de configuration** dans laquelle vous pouvez afficher et gérer les révisions précédentes de l'élément de configuration sélectionné.|  
|**Afficher la définition XML**|Affiche le fichier de définition XML de l’élément de configuration sélectionné dans une nouvelle fenêtre. Cette information peut être utile lorsque vous souhaitez créer manuellement les données de configuration.|  
|**Exporterer**|Exporte un élément de configuration dans un fichier de format .cab (cabinet) s'il a été créé sur ce site. Vous pouvez ensuite l’importer vers le même site ou un site Configuration Manager différent. Les données de configuration sont converties dans le format DCM Digest.|  
|**Copier**|Crée une copie de l'élément de configuration sélectionné avec un nom que vous spécifiez. Le nouvel élément de configuration ne conserve pas de relation avec l'élément de configuration d'origine. En d'autres termes, l'élément de configuration dupliqué n'hérite plus des informations de configuration de l'élément de configuration d'origine.|  
|**Supprimer**|Ouvre la boîte de dialogue **Supprimer un élément de configuration** dans laquelle vous pouvez consulter toutes les références à cet élément de configuration.<br /><br /> Vous devez supprimer toutes les références à un élément de configuration pour pouvoir supprimer l'élément de configuration.|  

## <a name="manage-configuration-baselines"></a>Gérer les bases de référence de configuration  

-   Dans l’espace de travail **Ressources et Conformité**, développez **Paramètres de compatibilité** > **Bases de référence de configuration**, sélectionnez la base de référence de configuration à gérer, puis sélectionnez une tâche de gestion.  


|Tâche de gestion|Détails|  
|---------------------|-------------|  
|**Afficher les membres**|Affiche tous les éléments de configuration qui sont référencés par la ligne de base de configuration.|  
|**Planifier le résumé**|Configure la planification pour que les données affichées dans le nœud **Lignes de base de configuration** dans la console Configuration Manager soient mises à jour avec les informations les plus récentes de la base de données de site.|  
|**Exécuter le résumé**|Le résumé actualise les données du noeud **Lignes de base de configuration** avec les dernières données de la base de données du site. Cette action peut prendre plusieurs minutes. Vous devrez peut-être cliquer sur **Actualiser** pour afficher les données les plus récentes dans la console.|  
|**Afficher la définition XML**|Affiche le fichier de définition XML de la ligne de base de configuration sélectionnée dans une nouvelle fenêtre. Cette information peut être utile lorsque vous souhaitez créer manuellement les données de configuration.|  
|**Activer**|Active une ligne de base de configuration pour la surveillance de la compatibilité.|  
|**Désactiver**|Désactive une ligne de base de configuration afin qu'elle ne soit plus évaluée pour la compatibilité sur les ordinateurs clients. Référence de configurations qui font référence à cette ligne de base seront également désactivées.|  
|**Exporterer**|Exporte une ligne de base de configuration dans un fichier .cab (cabinet) si elle a été créée sur ce site. Vous pouvez ensuite l’importer vers le même site ou un site Configuration Manager différent. Les données de configuration sont converties dans le format DCM Digest.<br /><br /> Pour plus d’informations sur l’importation des données de configuration, consultez [Importer des données de configuration](../../compliance/deploy-use/import-configuration-data.md).|  
|**Copier**|Crée une copie de la ligne de base de configuration sélectionnée avec un nom que vous spécifiez. La nouvelle ligne de base de configuration ne conserve pas de relation avec la ligne de base de configuration d'origine.|  
|**Supprimer**|Ouvre la boîte de dialogue **Supprimer une ligne de base de configuration** dans laquelle vous pouvez consulter toutes les références à cette ligne de base de configuration.<br /><br /> Vous devez supprimer toutes les références à une ligne de base de configuration pour pouvoir supprimer la ligne de base de configuration.|  
|**Déployer**|Ouvre la boîte de dialogue **Déployer des lignes de base de configuration** dans laquelle vous pouvez déployer une ou plusieurs lignes de base de configuration sur les appareils de votre hiérarchie.<br /><br /> Pour plus d’informations, consultez [Déployer des bases de référence de configuration](../../compliance/deploy-use/deploy-configuration-baselines.md).|  
