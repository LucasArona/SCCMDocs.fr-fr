---
title: Présentation de Long-Term Servicing Branch
titleSuffix: Configuration Manager
description: Découvrez Long-Term Servicing Branch dans System Center Configuration Manager.
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 694bc29f-a7fd-4e06-815a-1a9c5e9ac563
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f714be298c244b86178780138f5a700c89ae2a76
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128981"
---
# <a name="introduction-to-the-long-term-servicing-branch-of-system-center-configuration-manager"></a>Présentation de Long-Term Servicing Branch dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Long-Term Servicing Branch)*

Long-Term Servicing Branch (LTSB) de System Center Configuration Manager est une branche distincte de Configuration Manager, conçue comme une option d’installation disponible pour tous les clients. Mais elle n’est pas la seule option proposée aux clients qui ont laissé expirer leur Software Assurance (SA) ou leurs droits d’abonnement équivalents pour Configuration Manager.


À partir de Configuration Manager version 1606, LTSB offre moins de fonctionnalités que la branche actuelle de Configuration Manager.

 > [!TIP]   
 > Si vous recherchez des informations sur les branches de **Windows Server**, consultez [Nouvelle option de maintenance Current Branch for Business Windows Server 2016]( https://blogs.technet.microsoft.com/windowsserver/2016/07/12/windows-server-2016-new-current-branch-for-business-servicing-option/).

## <a name="features-that-are-not-available-in-the-ltsb-of-configuration-manager"></a>Fonctionnalités non disponibles dans la branche LTSB de Configuration Manager
La branche actuelle de Configuration Manager prend en charge les fonctionnalités suivantes, qui ne sont pas disponibles lorsque vous utilisez LTSB :

-   Des mises à jour dans la console qui ajoutent de nouvelles fonctionnalités et améliorations.
-   Prise en charge des derniers systèmes d’exploitation à utiliser comme clients et serveurs sur site.
-   Utilisez un abonnement Microsoft Intune pour prendre en charge :
    -   Intune dans une configuration hybride de gestion des appareils mobiles
    -   Gestion des appareils mobiles locale
-   Le tableau de bord et les plans de maintenance de Windows 10, y compris la prise en charge des dernières versions de la branche CB (Current Branch) et de la branche CBB (Current Branch for Business) de Windows 10.  
-   Prise en charge des futures versions de Windows Server et Windows 10 LTSB
-   Asset Intelligence
-   Points de distribution cloud
-   Exchange Online en tant que connecteur Exchange    

Bien que la prise en charge de ces fonctionnalités ne soit pas disponible dans LTSB, certaines restent visibles dans la console Configuration Manager, mais ne peuvent pas être sélectionnées ou utilisées.


## <a name="find-documentation-for-the-ltsb"></a>Rechercher de la documentation sur LTSB
LTSB est basé sur la version 1606 de Current Branch. Pour obtenir une documentation sur le produit, utilisez la [documentation Current Branch](https://docs.microsoft.com/sccm/), avec les mises en garde et limitations propres à LTSB. Ces mises en garde et limitations sont identifiées dans les rubriques en ligne suivantes :

- [Présentation de Long-Term Servicing Branch](introduction-to-the-ltsb.md) : (Cette rubrique)
- [Installation de Long-Term Servicing Branch](install-the-ltsb.md)
- [Mettre à niveau Long-Term Servicing Branch vers Current Branch](convert-to-current-branch.md)
- [Configurations prises en charge pour Long-Term Servicing Branch](supported-configurations-for-ltsb.md)
- [Gérer Long-Term Servicing Branch dans Configuration Manager](manage-the-ltsb.md)

Lorsque vous référencez la documentation Current Branch pour LTSB, les détails qui s’appliquent à la version 1606 s’appliquent également à LTSB. Les fonctionnalités ou les détails introduits avec la version 1610 ou version ultérieure ne sont pas pris en charge par LTSB.


## <a name="licensing-overview-for-the-ltsb"></a>Vue d’ensemble des licences pour LTSB   
Les clients qui ont un contrat Software Assurance (SA) sur les licences de System Center Configuration Manager ou qui ont des droits d’abonnement équivalents à la date du 1er octobre 2016 ont le droit d’utiliser la version 1606 d’octobre 2016 de System Center Configuration Manager. Les clients dotés de droits sur System Center Configuration Manager à la date du ou après le 1er octobre 2016 se voient proposer deux options de licence lors de l’installation : Current Branch et Long-Term Servicing Branch (LTSB).

Les clients dotés de droits perpétuels sur System Center Configuration Manager, ou qui laissent leur contrat SA ou leur abonnement expirer après le 1er octobre, peuvent installer la version LTSB de System Center Configuration Manager qui est en vigueur au moment de l’expiration.

[Les conditions générales des produits que vous achetez par le biais des programmes de licence en volume Microsoft se trouvent ici](http://go.microsoft.com/fwlink/?LinkId=800052).

Consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md) afin d’obtenir plus d’informations sur les options de licence pour les branches Configuration Manager.

## <a name="next-steps"></a>Étapes suivantes

Si vous décidez que Configuration Manager LTSB est la branche correcte pour votre environnement, [installez un nouveau site LTSB](/sccm/core/understand/install-the-ltsb#install-a-new-site) dans le cadre d’une nouvelle hiérarchie, ou [mettez à niveau un site System Center 2012 Configuration Manager](/sccm/core/understand/install-the-ltsb#upgrade-from-system-center-2012-configuration-manager) et une hiérarchie.

Si vous n’avez pas de support d’installation, consultez la [documentation de System Center 2016](https://technet.microsoft.com/system-center-docs/system-center) pour plus d’informations sur l’obtention de System Center 2016, qui inclut le support vous permettant d’installer System Center Configuration Manager LTSB.  
