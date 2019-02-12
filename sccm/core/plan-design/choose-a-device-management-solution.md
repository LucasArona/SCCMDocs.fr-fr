---
title: Choisir une solution de gestion d’appareils
titleSuffix: Configuration Manager
description: Découvrez les solutions offertes par Configuration Manager pour la gestion des PC, des serveurs et des appareils.
ms.date: 01/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1214a5b73b3e6b1bddab8a3918ddd32af0cacb68
ms.sourcegitcommit: f7b2fe522134cf102a3447505841cee315d3680c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55570198"
---
# <a name="choose-a-device-management-solution-for-configuration-manager"></a>Choisir une solution de gestion d’appareils pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager propose différentes solutions pour la gestion des PC, des serveurs et des appareils. Choisissez la solution qui convient à votre organisation. Basez votre choix sur les plateformes d’appareils que vous devez gérer et des fonctionnalités de gestion dont vous avez besoin.  


> [!Important]  
> Depuis le 14 août 2018, la gestion hybride des appareils mobiles est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, voir [Présentation de la gestion MDM hybride](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  
<!-- SCCMDocs issue 1197 -->



## <a name="overview"></a>Vue d'ensemble

Cet article décrit les quatre solutions de gestion d’appareils suivantes : 
- [Client de Configuration Manager](#bkmk_sccm)
- [Gestion des appareils mobiles (MDM) locale avec Configuration Manager](#bkmk_opmdm)
- [Cogestion avec Microsoft Intune](#bkmk_intune)
- [Microsoft Exchange](#bkmk_opmdm)

Vous pouvez utiliser ces solutions de gestion des appareils par elles-mêmes ou les combiner entre elles. Par exemple, vous pouvez utiliser l’approche de la gestion basée sur le client pour gérer les ordinateurs et les serveurs de votre organisation, et utiliser la cogestion pour gérer les ordinateurs portables basés sur Internet. En combinant les méthodes de cette façon, vous pouvez couvrir tous vos besoins en matière de gestion d’appareils.  

L’article inclut également deux tableaux qui permettent de comparer les solutions de gestion selon les facteurs suivants : 
- [Comparer les plateformes prises en charge](#bkmk_comp1)
- [Comparer les fonctionnalités de gestion](#bkmk_comp2)


### <a name="bkmk_sccm"></a> Client de Configuration Manager  

Cette option nécessite l’installation du client Configuration Manager sur les appareils. Elle fournit le plus grand nombre de fonctionnalités pour la gestion des PC, serveurs et autres appareils dans votre environnement. 

Pour plus d’informations, consultez [Méthodes d’installation du client](/sccm/core/clients/deploy/plan/client-installation-methods).  


### <a name="bkmk_opmdm"></a> MDM au niveau local  

Cette option utilise les fonctionnalités de gestion d’appareils intégrées à Windows 10. Bien qu’elle ne soit pas aussi exhaustive que la gestion basée sur le client, la gestion des appareils mobiles locale constitue une approche de gestion plus légère. Elle utilise les ressources Configuration Manager locales pour gérer les appareils.  

Pour plus d'informations, consultez [Gérer des appareils mobiles avec une infrastructure locale](/sccm/mdm/understand/manage-mobile-devices-with-on-premises-infrastructure).  


### <a name="bkmk_comanage"></a> Cogestion avec Microsoft Intune

La cogestion est l’une des principales façons de joindre votre déploiement de Configuration Manager existant au cloud Microsoft 365. Elle vous permet de gérer simultanément des appareils Windows 10 à l’aide de Configuration Manager et Microsoft Intune. La cogestion vous permet d’attacher via le cloud votre investissement existant dans Configuration Manager en ajoutant de nouvelles fonctionnalités. 

Pour plus d’informations, consultez [Qu’est-ce que la cogestion ?](/sccm/comanage/overview).  


### <a name="bkmk_exchange"></a> Microsoft Exchange  

Cette option utilise le connecteur du serveur Exchange Server pour connecter plusieurs serveurs Exchange à Configuration Manager. Cela centralise la gestion des appareils en mesure de se connecter à Exchange ActiveSync. Vous pouvez configurer les fonctionnalités de gestion des appareils mobiles Exchange à partir de la console Configuration Manager. Exemples de fonctionnalités : réinitialisation d’appareil à distance et contrôle des paramètres de plusieurs serveurs Exchange.

Pour plus d’informations, consultez [Gérer des appareils mobiles à l’aide de Configuration Manager et d’Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  



## <a name="bkmk_comp1"></a> Comparer les solutions selon les plateformes prises en charge  

|Plate-forme|Client de Configuration Manager|Gestion des appareils mobiles locale|Configuration Manager avec Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Android| | |Oui|  
|iOS| | |Oui|  
|Mac OS X|Oui| |Oui|  
|UNIX/Linux|Oui| |Oui|  
|Windows 10|Oui|Oui|Oui|  
|Windows 10 Mobile| |Oui|Oui|  
|Windows (versions précédentes)|Oui| |Oui|  
|Windows Server|Oui| |Oui|  
|Windows CE|Oui (avec le client hérité de l’appareil mobile)| |Oui|  
|Windows Embedded|Oui| | |  
|Windows Mobile| | |Oui|  

Pour obtenir la liste complète des plateformes prises en charge, consultez [Systèmes d’exploitation pris en charge pour les clients et les appareils pour System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

Microsoft recommande d’utiliser Intune pour gérer des appareils mobiles Android, iOS et Windows 10. Pour plus d'informations, consultez [Qu’est-ce que Microsoft Intune ?](https://docs.microsoft.com/intune/what-is-intune)



##  <a name="bkmk_comp2"></a> Comparer les solutions selon les fonctionnalités de gestion  

|Fonctionnalité de gestion|Client de Configuration Manager|Gestion des appareils mobiles locale|Configuration Manager avec Exchange|  
|--------|----------------------------|---------------|-----------------------------------|  
|Sécurité de l’infrastructure à clé publique (PKI) entre l’appareil mobile et Configuration Manager (utilise l’authentification mutuelle et SSL pour le chiffrement des transferts de données)|Oui|Oui| |  
|Installation du client|Oui| | |  
|Prise en charge via Internet|Oui| | |  
|découverte,|Oui| |Oui|  
|Inventaire matériel|Oui|Oui|Oui|  
|Inventaire logiciel|Oui| |Oui|  
|Paramètres|Oui|Oui|Oui|  
|Déploiement logiciel|Oui|Oui| |  
|Surveillance avec point d’état de secours|Oui| | |  
|Connexions aux points de gestion|Oui|Oui| |  
|Connexions aux points de distribution|Oui|Oui| |  
|Blocage à partir de Configuration Manager|Oui|Oui| |  
|Mise en quarantaine et blocage à partir d’Exchange Server (et Configuration Manager)| | |Oui|  
|Réinitialisation à distance| |Oui|Oui|  


