---
title: Infrastructure réseau
titleSuffix: Configuration Manager
description: Configurez les pare-feu, les ports et les domaines pour préparer votre infrastructure à Configuration Manager.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60a24e06d650b0e25007fb8490eb0c7d8c1996a1
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285609"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Considérations sur l’infrastructure réseau pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour préparer votre réseau à prendre en charge Configuration Manager, vous devrez peut-être configurer des composants d’infrastructure. Par exemple, ouvrez les ports du pare-feu pour transmettre les communications utilisées par Configuration Manager.  

## <a name="ports-and-protocols"></a>Ports et protocoles

Différentes fonctionnalités de Configuration Manager utilisent des ports réseau différents. Certains ports sont requis et vous pouvez en personnaliser certains.

La plupart des communications Configuration Manager utilisent des ports courants, comme le port 80 pour HTTP ou le port 443 pour HTTPS. Certains rôles de système de site prennent en charge l’utilisation de sites web et de ports personnalisés. Pour en savoir plus, consultez la page [Sites web pour les serveurs de système de site](/sccm/core/plan-design/network/websites-for-site-system-servers).

Avant de déployer Configuration Manager, identifiez les ports que vous prévoyez d’utiliser et configurez les pare-feu en fonction de vos besoins.

Après avoir installé Configuration Manager, si vous avez besoin de modifier un port, n’oubliez pas de mettre à jour les pare-feu sur les appareils et sur le réseau. Modifiez également la configuration du port dans Configuration Manager.

Pour plus d’informations, consultez les articles suivants :

- [Guide pratique pour configurer les ports de communication des clients](/sccm/core/clients/deploy/configure-client-communication-ports)
- [Ports utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/ports)


## <a name="internet-access-requirements"></a>Conditions requises pour l’accès Internet

Certaines fonctionnalités de Configuration Manager reposent sur la connectivité Internet pour être complètes. Si votre organisation restreint la communication réseau avec Internet à l’aide d’un appareil pare-feu ou proxy, veillez à autoriser les points de terminaison nécessaires.

Pour plus d’informations, consultez [Conditions requises pour l’accès à Internet](/sccm/core/plan-design/network/internet-endpoints)


## <a name="proxy-servers"></a>Serveurs proxy

Vous pouvez spécifier des serveurs proxy distincts pour les différents clients et serveurs du système de site. Effectuez ces configurations lorsque vous installez un client ou un rôle de système de site, ou modifiez-les ultérieurement si nécessaire.

Pour plus d’informations, consultez [Prise en charge des serveurs proxy](/sccm/core/plan-design/network/proxy-server-support).
