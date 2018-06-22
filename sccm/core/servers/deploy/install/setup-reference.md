---
title: Informations de référence pour l’installation
titleSuffix: Configuration Manager
description: Prenez connaissance de ces informations de référence pour mieux préparer l’installation d’un site ou d’une hiérarchie Configuration Manager.
ms.date: 4/18/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cdb9fb0c-0912-41e4-b427-f40620971763
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f9f857a2045f67690579955236c082ff29721a5f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339568"
---
# <a name="reference-for-system-center-configuration-manager-setup"></a>Informations de référence sur le programme d’installation de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le programme d’installation de System Center Configuration Manager fournit des liens vers plusieurs rubriques détaillées dans les sections suivantes. Les informations présentées ici peuvent vous aider à préparer l’installation d’un site ou d’une hiérarchie Configuration Manager, et à prendre certaines décisions relatives à l’installation.  


##  <a name="bkmk_start"></a> Avant de commencer  
Avant d’installer de nouveaux sites Configuration Manager, veillez à passer en revue les informations suivantes. Celles-ci peuvent vous aider à mettre en œuvre une conception de déploiement réussie :  

-   [Principes de base de System Center Configuration Manager](../../../../core/understand/fundamentals.md)  
-   [Planifier l’infrastructure System Center Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md)  
-   [Préparer l’installation de sites System Center Configuration Manager](prepare-to-install-sites.md)  

##  <a name="bkmk_assess"></a> Évaluer la préparation du serveur  
Avant de commencer l’installation d’un nouveau site, vérifiez que le serveur de site et les serveurs de système de site distant que vous envisagez d’utiliser pour le site (par exemple, le serveur qui héberge la base de données) respectent tous les prérequis. Les rubriques suivantes de la bibliothèque de documentation peuvent vous aider :  

-   [Configurations prises en charge pour System Center Configuration Manager](../../../../core/plan-design/configs/supported-configurations.md)  
-   [Outil de vérification de la configuration requise](prerequisite-checker.md)  

##  <a name="bkmk_Addclients"></a> Clients pour d’autres systèmes d’exploitation  
Vous pouvez télécharger le logiciel client pour Configuration Manager à partir du Centre de téléchargement Microsoft pour les systèmes d’exploitation suivants :  

-   Mac (Apple)  
-   UNIX  
-   Linux  

Utilisez les liens suivants pour télécharger des clients pour la version de Configuration Manager que vous utilisez :  

-   Consultez [Microsoft System Center Configuration Manager - Clients pour systèmes d’exploitation supplémentaires](http://www.microsoft.com/download/details.aspx?id=47719)  

##  <a name="bkmk_usage"></a> Paramètres et niveaux de données d’utilisation  
Quand vous installez votre premier site System Center Configuration Manager, Configuration Manager installe et configure automatiquement un nouveau rôle de système de site, appelé **point de connexion de service**, sur le serveur de site. Les paramètres par défaut du point de connexion de service sont les suivants :  

-   Mode **En ligne** (un mode hors connexion est également disponible)  
-   Niveau **Étendu** de collecte de données (deux autres niveaux de collecte de données, De base et Total, sont disponibles)  

Quand le rôle de système de site du point de connexion de service est en ligne, Microsoft peut collecter automatiquement des informations d’utilisation et de diagnostic sur Internet. Les informations collectées nous aident à effectuer les tâches suivantes :  

-   Identifier et résoudre les problèmes  
-   améliorer nos produits et services ;  
-   identifier les mises à jour pour Configuration Manager applicables à la version de Configuration Manager que vous utilisez.  

### <a name="levels-of-data-collection"></a>Niveaux de collecte de données  
La collecte de données comprend les trois niveaux suivants :

-   **De base** : comprend des données sur l’installation et la mise à niveau, comme le nombre de sites et les fonctionnalités de Configuration Manager qui sont activées. Aucune information personnelle n’est transmise.  

-   **Étendu** : comprend les données du paramètre de niveau De base et transmet des données relatives à la hiérarchie, à la façon dont chaque fonctionnalité est utilisée (fréquence et durée), ainsi que des informations de diagnostics améliorées telles que l’état de la mémoire de votre serveur quand un blocage du système ou d’une application se produit. Aucune information personnelle n’est transmise.  

-   **Total** : comprend les données des paramètres De base et Étendu, et envoie également des informations de diagnostics avancées telles que des fichiers système et des instantanés de la mémoire. Cette option peut inclure des informations personnelles, mais nous n’utilisons pas ces informations pour vous identifier, vous contacter ou vous envoyer du contenu publicitaire.  

Pour plus d’informations, notamment sur la divulgation des informations collectées par chaque niveau, consultez [Données d’utilisation et de diagnostic pour System Center Configuration Manager](../../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

Pour voir la déclaration de confidentialité de System Center Configuration Manager en ligne, accédez à [http://go.microsoft.com/fwlink/?LinkID=626527](http://go.microsoft.com/fwlink/?LinkID=626527).
