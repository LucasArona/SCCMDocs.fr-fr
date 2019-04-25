---
title: Stratégie de hiérarchie source
titleSuffix: Configuration Manager
description: Configurez une hiérarchie source et collectez les données d’un site source avant de configurer une tâche de migration System Center Configuration Manager.
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4800a800-66c8-4c35-aebe-e413a23790c1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 44f71aeb0019ce2b481e9f5ecd9f37ce6421398e
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673817"
---
# <a name="plan-a-source-hierarchy-strategy-in-system-center-configuration-manager"></a>Planifier une stratégie de hiérarchie source dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de configurer une tâche de migration dans votre environnement System Center Configuration Manager, vous devez configurer une hiérarchie source et collecter des données depuis au moins un site source de cette hiérarchie. Servez-vous des sections suivantes pour planifier la configuration de hiérarchies sources et de sites sources, ainsi que pour déterminer la manière dont Configuration Manager collecte les informations à partir des sites sources de la hiérarchie source. 

##  <a name="BKMK_Source_Hierarchies"></a> Hiérarchies sources  
Une hiérarchie source est une hiérarchie Configuration Manager qui contient les données à migrer. Quand vous configurez la migration et spécifiez une hiérarchie source, vous spécifiez le site de niveau supérieur de cette hiérarchie. Ce site est également appelé un site source. Les sites supplémentaires à partir desquels vous pouvez migrer des données dans la hiérarchie source sont également appelés des sites source.  

-   Quand vous configurez une tâche de migration pour migrer des données à partir d’une hiérarchie source Configuration Manager 2007, vous la configurez pour migrer les données d’un ou plusieurs sites sources spécifiques de la hiérarchie source.  

-   Quand vous configurez une tâche de migration pour migrer les données d’une hiérarchie source qui exécute System Center 2012 Configuration Manager ou version ultérieure, vous devez uniquement spécifier le site de niveau supérieur.  

Vous pouvez configurer une seule hiérarchie source à la fois.  

-   Si vous configurez une nouvelle hiérarchie source, cette hiérarchie devient automatiquement la hiérarchie source actuelle et remplace la hiérarchie source précédente.  

-   Quand vous configurez une hiérarchie source, vous devez spécifier son site de niveau supérieur, ainsi que les informations d’identification nécessaires à Configuration Manager pour se connecter au fournisseur SMS et à la base de données du site source.  

-   Configuration Manager utilise ces informations d’identification pour collecter des données et récupérer des informations sur les objets et les points de distribution à partir du site source.  

-   Dans le cadre du processus de collecte des données, les sites enfants de la hiérarchie source sont identifiés.  

-   Si la hiérarchie source est une hiérarchie Configuration Manager 2007, vous pouvez configurer ces sites supplémentaires comme sites sources, avec des informations d’identification distinctes pour chaque site source.  

Même si vous pouvez configurer plusieurs hiérarchies sources successivement, la migration est active pour une seule hiérarchie source à la fois.  

-   Si vous configurez une hiérarchie source supplémentaire avant d’effectuer la migration à partir de la hiérarchie source actuelle, Configuration Manager annule les tâches de migration actives et reporte les tâches de migration planifiées pour la hiérarchie source actuelle.  

-   La nouvelle hiérarchie source configurée devient alors la hiérarchie source actuelle, et la hiérarchie source d’origine devient inactive.  

-   Vous pouvez ensuite configurer les informations d’identification de connexion, les sites sources supplémentaires et les tâches de migration pour la nouvelle hiérarchie source.  

Si vous restaurez une hiérarchie source inactive et que vous n’avez pas utilisé **Nettoyer les données de migration** précédemment, vous pouvez afficher les tâches de migration configurées pour cette hiérarchie source. Cependant, avant de pouvoir continuer la migration à partir de cette hiérarchie, vous devez reconfigurer les informations d'identification pour vous connecter à chaque site source applicable et replanifier les tâches de migration qui n'ont pas été terminées.  

> [!CAUTION]  
>  Si vous migrez des données à partir de plusieurs hiérarchies source, chaque hiérarchie source supplémentaire doit contenir un ensemble unique de codes de site.  
> Les hiérarchies source et de destination requièrent également un ensemble différent de codes de sites.

Pour plus d’informations sur la configuration d’une hiérarchie source, consultez [Configuration des hiérarchies sources et des sites sources pour la migration vers System Center Configuration Manager](../../core/migration/configuring-source-hierarchies-and-source-sites-for-migration.md)  

##  <a name="BKMK_Source_Sites"></a> Sites source  
 Les sites source sont des sites dans la hiérarchie source qui contiennent des données à migrer. Le site de niveau supérieur de la hiérarchie source est toujours le premier site source. Lorsque la migration collecte des données à partir du premier site source d'une nouvelle hiérarchie source, elle découvre des informations à propos des sites supplémentaires dans cette hiérarchie.  

 À la fin de la collecte de données du site source initial, les actions suivantes que vous effectuez dépendent de la version du produit de la hiérarchie source.  

### <a name="source-sites-that-run-configuration-manager-2007-sp2"></a>Sites sources exécutant Configuration Manager 2007 SP2  
 Une fois les données collectées à partir du site source initial de la hiérarchie Configuration Manager 2007 SP2, vous n’avez pas à configurer de sites sources supplémentaires pour créer des tâches de migration. Toutefois, pour pouvoir migrer les données à partir de sites supplémentaires, vous devez configurer les sites supplémentaires comme des sites sources, et System Center Configuration Manager doit collecter les données à partir de ces sites.  

 Pour collecter des données à partir de sites supplémentaires, vous devez configurer individuellement chaque site comme un site source. Vous devez définir les informations d’identification pour la connexion de System Center Configuration Manager au fournisseur SMS et à la base de données de site de chaque site source. Après avoir configuré les informations d’identification d’un site source, le processus de collecte de données commence pour ce site.  

 Quand vous configurez des sites sources supplémentaires dans une hiérarchie source Configuration Manager 2007 SP2, vous devez configurer les sites sources du haut vers le bas, ce qui signifie que vous configurez les sites de niveau inférieur en dernier. Vous pouvez configurer des sites sources dans une branche de la hiérarchie à tout moment, mais vous devez configurer un site comme site source pour pouvoir configurer ses sites enfants comme sites sources.  

> [!NOTE]  
>  Seuls les sites principaux d’une hiérarchie Configuration Manager 2007 SP2 sont pris en charge pour la migration.  

### <a name="source-sites-that-run-system-center-2012-configuration-manager-or-later"></a>Sites sources exécutant System Center 2012 Configuration Manager ou version ultérieure  
 Une fois les données collectées à partir du site source initial de la hiérarchie System Center 2012 Configuration Manager ou version ultérieure, vous n’avez pas à configurer de sites sources supplémentaires dans cette hiérarchie source. En effet, contrairement à Configuration Manager 2007, ces versions de Configuration Manager utilisent une base de données partagée qui vous permet d’identifier, puis de migrer tous les objets disponibles à partir du site source initial.  

 Quand vous configurez les comptes d’accès pour collecter des données, vous devez peut-être accorder l’accès **Compte fournisseur SMS du site source** à plusieurs ordinateurs de la hiérarchie source. Cela peut être nécessaire lorsque le site source prend en charge plusieurs instances du fournisseur SMS, chacune sur un ordinateur différent. Lorsque la collecte des données commence, le site de niveau supérieur de la hiérarchie de destination contacte le site de niveau supérieur de la hiérarchie source pour identifier les emplacements du fournisseur SMS de ce site. Seule la première instance du fournisseur SMS est identifiée. Si le processus de collecte des données ne peut pas accéder au fournisseur SMS à l'emplacement identifié, le processus échoue et ne tente pas de se connecter à d'autres ordinateurs qui exécutent une instance du fournisseur SMS pour le site.  

##  <a name="BKMK_Data_Gathering"></a> Collecte des données  
 Dès que vous avez spécifié une hiérarchie source, configuré les informations d’identification de chaque site source supplémentaire dans une hiérarchie source ou partagé les points de distribution d’un site source, Configuration Manager commence à collecter des données à partir du site source.  

 La collecte de données se répète ensuite selon une planification simple pour maintenir la synchronisation avec les modifications apportées aux données dans le site source. Par défaut, le processus se répète toutes les quatre heures. Vous pouvez modifier la planification du cycle en modifiant les **Propriétés** du site source. Le processus de collecte de données initial doit vérifier tous les objets de la base de données Configuration Manager, ce qui peut prendre un certain temps. Les processus de collecte de données suivants identifient uniquement les modifications apportées aux données et ils s'exécutent plus rapidement.  

 Pour collecter des données, le site de niveau supérieur dans la hiérarchie de destination se connecte au fournisseur SMS et à la base de données du site source pour récupérer une liste d'objets et les points de distribution. Ces connexions utilisent les comptes d'accès de site source. Pour plus d’informations sur les configurations nécessaires pour la collecte des données, consultez [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

 Vous pouvez démarrer et arrêter le processus de collecte des données à l’aide de **Collecter les données maintenant** et **Arrêter la collecte de données** dans la console Configuration Manager.  

 Une fois que vous avez utilisé **Arrêter la collecte de données** pour un site source pour une raison quelconque, vous devez reconfigurer les informations d’identification du site pour pouvoir collecter à nouveau les données de ce site. Configuration Manager ne peut pas identifier les nouveaux objets ni les modifications apportées aux objets migrés tant que vous ne reconfigurez pas le site source.  

> [!NOTE]  
>  Avant de développer un site principal autonome dans une hiérarchie avec un site d’administration centrale, vous devez arrêter toutes les collectes des données. Vous pouvez reconfigurer la collecte des données quand le développement du site est terminé.  

### <a name="gather-data-now"></a>Collecter les données maintenant  
 Après l'exécution du processus initial de collecte des données d'un site, le processus se répète pour identifier les objets mis à jour depuis le dernier cycle de collecte des données. Vous pouvez également utiliser l’action **Collecter les données maintenant** dans la console Configuration Manager pour démarrer immédiatement le processus et réinitialiser l’heure de début du cycle suivant.  

 Lorsqu'un processus de collecte de données aboutit pour un site source, vous pouvez partager les points de distribution à partir du site source et configurer des tâches de migration pour migrer les données depuis le site. La collecte des données est un processus répétitif pour la migration et il se poursuit jusqu’à ce que vous changiez la hiérarchie source ou utilisiez **Arrêter la collecte de données** pour mettre fin au processus de collecte des données du site.  

### <a name="stop-gathering-data"></a>Arrêter la collecte de données  
 Vous pouvez utiliser **Arrêter la collecte de données** pour mettre fin à la collecte des données d’un site source quand vous ne souhaitez plus que Configuration Manager identifie les objets nouveaux et modifiés du site. Cette action empêche également Configuration Manager de proposer aux clients de la hiérarchie de destination des points de distribution partagés de la source en tant qu’emplacements pour le contenu que vous avez migré.  

 Pour arrêter la collecte des données de chaque site source, vous devez exécuter **Arrêter la collecte de données** sur les sites sources de niveau inférieur, puis répéter le processus sur chaque site parent. Le site de niveau supérieur de la hiérarchie source doit être le dernier site sur lequel vous arrêtez la collecte des données. Vous devez arrêter la collecte des données sur chaque site enfant avant d'effectuer cette action sur un site parent. En règle générale, vous arrêtez la collecte de données uniquement lorsque vous êtes prêt à exécuter le processus de migration.  

 Quand vous arrêtez la collecte des données d’un site source, les informations collectées précédemment sur les objets et les regroupements du site peuvent toujours être utilisées quand vous configurez de nouvelles tâches de migration. Toutefois, vous ne voyez pas les nouveaux objets ou regroupements, ni les modifications apportées aux objets existants. Si vous reconfigurez le site source et recommencez à collecter les données, vous voyez les informations et l'état des objets précédemment migrés.  
