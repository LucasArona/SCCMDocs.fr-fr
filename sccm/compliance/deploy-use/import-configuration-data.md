---
title: Importer des données de configuration
titleSuffix: Configuration Manager
description: Importez des données de configuration contenues dans un fichier CAB et conformes au schéma SML (Service Modeling Language) pris en charge.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 309b9a09-a611-4ba2-90ab-dde51582cf87
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2a779f80f42439fe6526c05d7027c22fb191e41e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="import-configuration-data-with-system-center-configuration-manager"></a>Importer des données de configuration avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer des bases de référence de configuration et des éléments de configuration dans la console System Center Configuration Manager, mais également importer des données de configuration contenues dans un fichier CAB (.cab) et conformes au schéma SML (Service Modeling Language) pris en charge. Vous pouvez importer les données de configuration suivantes :  

-   Données de configuration recommandées (packs de configuration) téléchargées à partir de Microsoft ou d’autres sites d’éditeurs de logiciels.  

-   Données de configuration exportées à partir de System Center 2012 Configuration Manager et versions ultérieures.  

-   Données de configuration créées en externe et conformes au schéma SML.  

 Pour obtenir un exemple de pack de configuration qui vous permet de gérer la compatibilité aux rôles de serveur de site System Center 2012 Configuration Manager, consultez [Pack de configuration de System Center 2012 Configuration Manager](http://www.microsoft.com/en-us/download/details.aspx?id=30710&WT.mc_id=rss_alldownloads_all).  

Lorsque vous importez une ligne de base de configuration, une partie ou la totalité des éléments de configuration référencés dans la ligne de base peuvent être également inclus dans le fichier CAB. Pendant le processus d’importation, Configuration Manager vérifie que tous les éléments de configuration référencés dans la base de référence de configuration sont également inclus dans le fichier CAB ou qu’ils existent déjà sur le site Configuration Manager. Le processus d’importation échoue si vous tentez d’importer une base de référence de configuration qui fait référence à des données de configuration que Configuration Manager ne trouve pas.  

L'importation risque d'échouer dans d'autres cas également. Par exemple :  

-   Les données de configuration font référence à des données que Configuration Manager ne parvient pas à localiser, soit dans sa base de données, soit dans le fichier CAB lui-même.  

-   Les données de configuration sont déjà présentes dans la base de données Configuration Manager avec un nom et une version identiques, mais la version du contenu est différente.  

-   Les données de configuration sont déjà présentes dans la base de données Configuration Manager avec la même version de contenu, mais le calcul du hachage les identifie comme différentes.  

-   Une version plus récente des données de configuration avec le même nom est déjà présente (ou a récemment été supprimée) dans la base de données Configuration Manager.  

-   Dans une hiérarchie Configuration Manager à plusieurs sites, les données de configuration ont été initialement importées depuis un site parent. Vous devez les mettre à jour à partir du même site et non pas d'un site enfant.  

### <a name="import-configuration-data"></a>Importer des données de configuration  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Éléments de configuration** ou **Lignes de base de configuration**
2.  Sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Importer des données de configuration**.  
3.  Dans la page **Sélectionner des fichiers** de l’Assistant **Importer des données de configuration**, cliquez sur **Ajouter**, puis, dans la boîte de dialogue **Ouvrir** , sélectionnez les fichiers .cab à importer.  
4.  Cochez la case **Créer une nouvelle copie des lignes de base de la configuration importée et des éléments de configuration** pour que les données de configuration importées soient modifiables dans la console Configuration Manager.  
5.  Dans la page **Résumé**, passez en revue les actions qui seront exécutées, puis terminez l’Assistant.  

Les données de configuration importées apparaissent dans le nœud **Paramètres de compatibilité** de l’espace de travail **Ressources et Conformité**.  
