---
title: Restreindre l’accès en fonction du risque
titleSuffix: Configuration Manager
description: Restreignez l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application.
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 90098dc0243e8513fe78692fe91a8390f7936eba
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56119647"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gérer l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application

*S’applique à : System Center Configuration Manager (Current Branch)*

Les connecteurs de protection contre les menaces mobiles vous permettent d’utiliser votre fournisseur de protection contre les menaces mobiles comme source d’informations pour vos règles d’accès conditionnelles et stratégies de conformité. Ceci vous permet d’ajouter une couche de protection aux ressources de votre organisation telles que Microsoft Exchange et Sharepoint, tout particulièrement en cas de corruption d’appareils mobiles.

> [!Important]  
> Depuis le 14 août 2018, la gestion hybride des appareils mobiles est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, voir [Présentation de la gestion MDM hybride](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  



## <a name="what-problem-does-this-solve"></a>Quel problème cette fonctionnalité résout-elle ?

Les organisations doivent protéger leurs données sensibles contre diverses menaces émergentes, notamment les menaces ciblant le matériel, les applications et le réseau, ainsi que les vulnérabilités du système d’exploitation.

Historiquement, les organisations ont été proactives en matière de protection des PC contre les attaques, alors que les appareils mobiles ne sont toujours pas contrôlés et protégés. Les plateformes mobiles offrent maintenant une protection intégrée, grâce à l’isolation d’application et à la vérification des applications des App Store, entre autres, mais elles restent vulnérables aux attaques sophistiquées. Aujourd’hui, de plus en plus d’employés utilisent des appareils dans le cadre de leur travail, et ont besoin d’accéder à des informations sensibles. Or, les appareils doivent être protégés contre des attaques de plus en plus sophistiquées.



## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Fonctionnement des connecteurs de protection contre les menaces mobiles Intune

Ce type de connecteur protège les ressources de l’organisation en créant un canal de communication entre Intune et votre fournisseur Mobile Threat Defense. Les partenaires Intune Mobile Threat Defense proposent des applications intuitives et faciles à déployer sur les appareils mobiles. Ces applications analysent de manière active les informations sur les menaces à partager avec Intune. Utilisez ces informations pour générer des rapports ou à des fins de mise en œuvre. 

Par exemple, une application Mobile Threat Defense connectée signale au fournisseur Mobile Threat Defense qu’un appareil est actuellement connecté à un réseau vulnérable aux attaques d’intercepteurs. Ces informations sont partagées et classées à un niveau de risque approprié : faible, moyen ou élevé. Comparez ce risque avec vos allocations de niveau de risque dans Intune pour déterminer si l’accès à certaines ressources de votre choix devrait être révoqué tant que l’appareil est corrompu.



## <a name="sample-scenarios"></a>Exemples de scénarios

La solution de protection contre les menaces mobiles considère un appareil comme infecté :

![Appareil considéré comme infecté par la solution de protection contre les menaces mobiles](../media/mtp/MTD-image-1.png)

L’accès est accordé lorsque la menace est supprimée sur l’appareil :

![Accès accordé par la solution de protection contre les menaces mobiles](../media/mtp/MTD-image-2.png)



## <a name="next-steps"></a>Étapes suivantes

Découvrez comment protéger l’accès aux ressources d’entreprise en fonction des risques liés aux applications, aux réseaux et aux appareils avec :

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)
