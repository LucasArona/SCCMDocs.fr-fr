---
title: Configurations prises en charge
titleSuffix: Configuration Manager
description: Identifiez les principales configurations et exigences liées à la planification, au déploiement et à la maintenance d’un déploiement de System Center Configuration Manager fonctionnel.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 45a10878-ff48-4318-9c6d-c014b38a4039
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: de769a24b44c5ab5e28035e96fef341aecd78006
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32332982"
---
# <a name="supported-configurations-for-system-center-configuration-manager"></a>Configurations prises en charge pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Comme solution locale, System Center Configuration Manager utilise vos serveurs, clients, configurations réseau et autres produits tels que Microsoft Intune, SQL Server et Azure.

La présente rubrique et les rubriques suivantes fournissent des informations essentielles pour vous aider à déterminer les principales configurations, exigences et limitations à prendre en compte pour planifier, installer et gérer un déploiement de Configuration Manager pleinement opérationnel.  Ces informations sont propres à l’infrastructure des sites, hiérarchies et appareils gérés de Configuration Manager.

Quand une fonctionnalité Configuration Manager nécessite des configurations particulières, ces informations sont fournies dans la documentation de la fonctionnalité, venant ainsi compléter les informations de configuration plus générales.  

 Les produits et les technologies qui sont décrits dans les rubriques suivantes sont pris en charge par Configuration Manager. Toutefois, leur inclusion dans ce contenu n’implique pas une extension de prise en charge des produits au-delà de leur cycle de vie individuel. L’utilisation de produits qui ont dépassé leur cycle de vie n’est pas prise en charge avec Configuration Manager. Pour plus d’informations sur les politiques de support Microsoft, consultez le site web [Politique de support Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

> [!NOTE]  
>  Pour plus d’informations sur la politique de support Microsoft, consultez le site web [FAQ sur la politique de support Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=31976).  

 De plus, les produits et versions de produits non répertoriés dans les rubriques suivantes ne sont pas pris en charge avec System Center Configuration Manager, sauf s’ils ont été annoncés dans le [blog Enterprise Mobility and Security](https://blogs.technet.microsoft.com/enterprisemobility/).  Parfois, le contenu de ce blog précède une mise à jour du corps de cette documentation.


-  [Taille et échelle en chiffres](../../../core/plan-design/configs/size-and-scale-numbers.md)  
Découvrez combien de sites, de rôles de système de site par site et de clients ou d’appareils sont pris en charge dans les différentes conceptions de hiérarchie pour Configuration Manager.

-  [Prérequis des sites et systèmes de site](../../../core/plan-design/configs/site-and-site-system-prerequisites.md)  
Découvrez les configurations requises sur un ordinateur Windows Server pour prendre en charge les différents types de site et rôles de système de site.

-  [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  
Découvrez quels systèmes d’exploitation vous pouvez utiliser comme serveur de site ou serveur de système de site.

-  [Systèmes d’exploitation pris en charge pour les clients et appareils](../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)  
Découvrez quels systèmes d’exploitation vous pouvez gérer à l’aide de Configuration Manager, notamment Windows, Windows Embedded, Linux et UNIX, Mac, ainsi que les appareils mobiles.

-  [Systèmes d’exploitation pris en charge pour la console](../../../core/plan-design/configs/supported-operating-systems-consoles.md)  
Découvrez quels systèmes d’exploitation peuvent héberger la console Configuration Manager pour fournir un point d’accès permettant de gérer votre déploiement.  

-  [Prise en charge des versions de SQL Server](../../../core/plan-design/configs/support-for-sql-server-versions.md)  
Découvrez quelles versions de SQL Server peuvent héberger la base de données de site et la base de données de création de rapports, et quelles configurations requises et facultatives vous pouvez utiliser.

-  [Options de haute disponibilité](../../../protect/understand/high-availability-options.md)  
Découvrez les options que vous pouvez implémenter lors de la conception de votre environnement pour faciliter le maintien d’un haut niveau de service disponible pour votre déploiement Configuration Manager.

-  [Matériel recommandé](../../../core/plan-design/configs/recommended-hardware.md)  
Découvrez des conseils pour vous aider à déterminer les configurations et le matériel appropriés pour héberger vos sites et principaux services Configuration Manager.

-  [Prise en charge des domaines Active Directory](../../../core/plan-design/configs/support-for-active-directory-domains.md)  
Découvrez les configurations de domaine Active Directory prises en charge que Configuration Manager exige et prend en charge.

-  [Prise en charge des fonctionnalités et réseaux Windows](../../../core/plan-design/configs/support-for-windows-features-and-networks.md)  
Découvrez les technologies Windows (telles que la déduplication de données et BranchCache) prises en charge dans Configuration Manager, ainsi que les limitations de leur utilisation.

-  [Prise en charge des environnements de virtualisation](../../../core/plan-design/configs/support-for-virtualization-environments.md)  
Découvrez comment utiliser les technologies de machine virtuelle prises en charge.
