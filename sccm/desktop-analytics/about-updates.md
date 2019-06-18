---
title: Mises à jour dans les postes de travail Analytique
titleSuffix: Configuration Manager
description: En savoir plus sur les mises à jour de sécurité et de fonctionnalité dans Analytique de bureau.
ms.date: 04/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7fc673cfa11224394df785f2e13e77ad2e0f5888
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159227"
---
# <a name="updates-in-desktop-analytics"></a>Mises à jour dans les postes de travail Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Dans le portail d’Analytique de bureau, afficher l’état des mises à jour de sécurité et de fonctionnalité. Sélectionnez ces nœuds dans le groupe du Moniteur du menu principal Analytique de bureau. Ces nœuds vous donnent des informations sur l’état de ces mises à jour dans votre environnement.



## <a name="security-updates"></a>Mises à jour de sécurité

Pour consulter l’état actuel des mises à jour de sécurité, sélectionnez **mises à jour de sécurité** dans le **moniteur** section d’Analytique de bureau :

![Nœud de mises à jour de sécurité de bureau Analytique](media/security-updates.png)

Cette vue résume *sécurité* mises à jour pour les appareils qui exécutent Windows 10. Dans le graphique à barres, les appareils sont classés par les étiquettes suivantes :

#### <a name="latest"></a>Dernière

Appareils exécutent la dernière mise à jour de sécurité pour cette version et le canal.

#### <a name="latest-1"></a>Dernière version-1

Appareils exécutent une sécurité mise à jour une version antérieure à la dernière mise à jour disponible sur ce canal.

#### <a name="older"></a>Plus anciens

Les appareils sont en cours d’exécution une mise à jour de sécurité antérieure à la dernière version-1.

#### <a name="not-measured"></a>Pas mesuré

Analytique de postes de travail n’a pas encore évalué l’appareil. Cet état inclut les appareils exécutant Windows 7, Windows 8.1 ou Windows 10 appareils inscrits pour le programme Insider de Windows.  



## <a name="feature-updates"></a>Mises à jour des fonctionnalités

Pour consulter l’état actuel des mises à jour de la fonctionnalité, sélectionnez **mises à jour des fonctionnalités** dans le **moniteur** section d’Analytique de bureau :

![Nœud de mises à jour de fonctionnalité de bureau Analytique](media/feature-updates.png)

Cette vue résume *fonctionnalité* mises à jour pour les appareils qui exécutent Windows 10.

Pour plus d’informations sur des périodes de service, consultez [fiche d’information du cycle de vie Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Dans le graphique à barres, les appareils sont classés par les étiquettes suivantes :

#### <a name="in-service"></a>Dans le service

Appareils exécutent la dernière mise à jour de la fonctionnalité pour cette version et le canal.  

#### <a name="near-end-of-service"></a>Proche de la fin du service

Les appareils sont en cours d’exécution une mise à jour de fonctionnalité qui est de 90 jours d’atteindre la fin du service.

#### <a name="end-of-service"></a>Fin de service

Les appareils sont en cours d’exécution une mise à jour de fonctionnalité qui est au-delà de la date de fin du service. Pour plus d’informations sur la fin de dates de service, consultez [fiche d’information du cycle de vie Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>Pas mesuré

Analytique de postes de travail n’a pas encore évalué l’appareil. Cet état inclut les appareils exécutant Windows 7, Windows 8.1 ou Windows 10 appareils inscrits pour le programme Insider de Windows.



## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur les ressources de bureau Analytique](/sccm/desktop-analytics/about-assets): appareils, des pilotes et des applications  

- [En savoir plus sur les plans de déploiement](/sccm/desktop-analytics/about-deployment-plans)  
