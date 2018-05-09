---
title: Gérer les clients sur Internet
titleSuffix: Configuration Manager
description: Découvrez la gestion de clients avec la passerelle de gestion cloud et la gestion du client basée sur Internet dans Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6296a171f2ef225dbbf647eb5e53103650d60c11
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Gérer les clients sur Internet avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En général, dans Configuration Manager, la plupart des ordinateurs et serveurs gérés se trouvent physiquement sur le même réseau interne que les serveurs de système de site qui exécutent des fonctions de gestion. Toutefois, vous pouvez gérer les clients en dehors de votre réseau interne quand ils sont connectés à Internet. Cette possibilité ne nécessite pas que les clients se connectent via VPN pour atteindre les serveurs de système de site.

Configuration Manager fournit deux façons de gérer les clients connectés à Internet :

-   Passerelle de gestion cloud

-   Gestion des clients basés sur Internet


## <a name="cloud-management-gateway"></a>Passerelle de gestion cloud

La passerelle de gestion cloud permet de gérer les clients Internet. Elle utilise une combinaison d’un service cloud Microsoft Azure et d’un nouveau rôle de système de site qui communique avec ce service. Les clients Internet utilisent le service cloud pour communiquer avec Configuration Manager local.

#### <a name="advantages"></a>Avantages  

-   Aucun investissement n’est nécessaire pour l’infrastructure supplémentaire.  

-   L’infrastructure locale n’est pas exposée sur Internet.  

-   Les machines virtuelles du cloud qui exécutent le service sont entièrement gérées par Azure et ne nécessitent aucune maintenance.  

-   Installation et configuration faciles dans la console Configuration Manager.  

#### <a name="disadvantages"></a>Inconvénients  

-   Coût de l’abonnement au cloud.  

-   Données de gestion envoyées via le service cloud.  

Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Gestion des clients basés sur Internet

Cette méthode s’appuie sur les serveurs de système de site accessibles sur Internet avec lesquels les clients communiquent à des fins de gestion. Elle nécessite que les clients et serveurs de système de site soient configurés pour une gestion basée sur Internet.

#### <a name="advantages"></a>Avantages  

-   Aucune dépendance du service cloud.  

-   Aucun coût supplémentaire associé à un abonnement au cloud.  

-   Contrôle total des serveurs et rôles assurant le service.  

#### <a name="disadvantages"></a>Inconvénients  

-   Un investissement est nécessaire pour l’infrastructure supplémentaire.  

-   Frais généraux et coût opérationnel de l’infrastructure supplémentaire.  

-   L’infrastructure doit être exposée sur Internet.  

Pour plus d’informations, consultez [Planifier la gestion des clients basés sur Internet](plan-internet-based-client-management.md).  
