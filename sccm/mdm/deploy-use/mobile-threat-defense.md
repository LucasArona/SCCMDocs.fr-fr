---
title: Restreindre l’accès en fonction du risque
titleSuffix: Configuration Manager
description: Restreignez l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application.
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9083c571-f4fc-4a78-adc5-8aec84dabcbd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e921e6ab90eb57caf031b49d375d0017ea9a2930
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346450"
---
# <a name="manage-access-to-company-resource-based-on-device-network-and-application-risk"></a>Gérer l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application

*S’applique à : System Center Configuration Manager (Current Branch)*

Les connecteurs de protection contre les menaces mobiles vous permettent d’utiliser votre fournisseur de protection contre les menaces mobiles comme source d’informations pour vos règles d’accès conditionnelles et stratégies de conformité. Ainsi, les administrateurs informatiques peuvent ajouter une couche de protection aux ressources d’entreprise telles que Microsoft Exchange et Sharepoint, tout particulièrement en cas de corruption d’appareils mobiles.

## <a name="what-problem-does-this-solve"></a>Quel problème cette fonctionnalité résout-elle ?

Les entreprises doivent protéger leurs données sensibles contre diverses menaces émergentes, notamment les menaces ciblant le matériel, les applications et le réseau ainsi que les vulnérabilités du système d’exploitation.
Historiquement, les entreprises ont été proactives en matière de protection des PC contre les attaques, alors que les appareils mobiles ne sont toujours pas contrôlés et protégés. Les plateformes mobiles offrent maintenant une protection intégrée, grâce à l’isolation d’application et à la vérification des applications des App Store, entre autres, mais elles restent vulnérables aux attaques sophistiquées. Aujourd’hui, de plus en plus d’employés utilisent des appareils dans le cadre de leur travail, et ont besoin d’accéder à des informations sensibles. Or, les appareils doivent être protégés contre des attaques de plus en plus sophistiquées.

Le [déploiement MDM hybride (SCCM avec Intune)](https://docs.microsoft.com/sccm/mdm/understand/choose-between-standalone-intune-and-hybrid-mobile-device-management) vous permet de contrôler l’accès aux ressources et aux données d’entreprise en fonction de l’évaluation des risques fournie par des solutions de protection des appareils contre les menaces, comme celles proposées par les partenaires de protection contre les menaces mobiles.

## <a name="how-the-intune-mobile-threat-defense-connectors-work"></a>Fonctionnement des connecteurs de protection contre les menaces mobiles Intune

Ce type de connecteur protège les ressources de l’entreprise en créant un canal de communication entre Intune et votre fournisseur de protection contre les menaces mobiles. Les partenaires de protection contre les menaces mobiles Intune proposent des applications intuitives et faciles à déployer sur les appareils mobiles. Ces applications analysent de manière active les informations sur les menaces à partager avec Intune, à des fins d’application ou de création de rapports. Par exemple, si une application de protection contre les menaces mobiles qui est connectée envoie des rapports au fournisseur de cette application indiquant qu’un téléphone est actuellement connecté à un réseau vulnérable aux attaques de l’intercepteur, il partage cette information et lui affecte un niveau de risque approprié (faible, moyen ou élevé). Cette information peut ensuite être comparée avec le niveau de risque accepté qui est configuré pour vos systèmes dans Intune, afin de déterminer si l’accès à certaines ressources doit être supprimé tant que l’appareil est infecté.

## <a name="sample-scenarios"></a>Exemples de scénarios

La solution de protection contre les menaces mobiles considère un appareil comme infecté :

![Appareil considéré comme infecté par la solution de protection contre les menaces mobiles](../media/mtp/MTD-image-1.png)

L’accès est accordé lorsque la menace est supprimée sur l’appareil :

![Accès accordé par la solution de protection contre les menaces mobiles](../media/mtp/MTD-image-2.png)

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment protéger l’accès aux ressources d’entreprise en fonction des risques liés aux applications, aux réseaux et aux appareils avec :

- [Lookout](https://docs.microsoft.com/intune/deploy-use/lookout-mobile-threat-defense-connector)