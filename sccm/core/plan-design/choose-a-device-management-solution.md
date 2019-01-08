---
title: 'Choisir une solution de gestion d’appareils '
titleSuffix: Configuration Manager
description: Découvrez les solutions offertes par System Center Configuration Manager pour la gestion des PC, des serveurs et des appareils.
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a520e4e43ca2d7de080272c213c5768cbd284501
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415838"
---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>Choisir une solution de gestion d’appareils pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager (également appelé ConfgMgr or SCCM) offre différentes solutions pour la gestion des PC, des serveurs et des appareils. Choisissez la solution qui vous convient, en fonction des plateformes d’appareils que vous devez gérer et des fonctionnalités de gestion dont vous avez besoin.  


##  <a name="overview-of-device-management-solutions"></a>Vue d’ensemble des solutions de gestion d’appareils  
 Cet article aborde quatre solutions de gestion des appareils : l’application cliente Configuration Manager, l’infrastructure Configuration Manager locale, Microsoft Intune et Exchange. Il est suivi de deux tableaux qui permettent de comparer les solutions de gestion : un tableau basé sur les [plateformes d’appareils prises en charge](#compare-device-management-solutions-based-on-supported-mobile-device-platforms) et un tableau basé sur les [fonctionnalités de gestion](#compare-mobile-device-management-solutions-based-on-management-functionality).


###  <a name="manage-devices-with-the-configuration-manager-client"></a>Gérer les appareils avec le client Configuration Manager  

Cette option, qui nécessite l’installation de l’application cliente Configuration Manager sur les appareils, offre la gamme de fonctionnalités la plus étendue pour gérer les PC, les serveurs et les autres appareils de votre environnement. Pour plus d’informations, consultez [Méthodes d’installation du client dans System Center Configuration Manager](/sccm/core/clients/deploy/plan/client-installation-methods).  

###  <a name="manage-devices-with-on-premises-configuration-manager-infrastructure"></a>Gérer les appareils mobiles avec une infrastructure Configuration Manager locale  

Cette option utilise les fonctionnalités de gestion des appareils intégrées aux systèmes d’exploitation de certaines plateformes d’appareils. Bien qu’elle ne soit pas aussi complète que la gestion basée sur le client, la gestion locale des appareils mobiles fournit une approche de gestion plus légère en faisant appel aux ressources Configuration Manager locales pour atteindre et gérer les appareils. Notez que cette option n’est pour l’instant prise en charge que sur les PC Windows 10 et sur les appareils Windows 10 Mobile.  

Pour plus d’informations, consultez [Gérer des appareils mobiles avec une infrastructure locale dans System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

###  <a name="manage-devices-with-microsoft-intune-hybrid"></a>Gérer les appareils avec Microsoft Intune (hybride)  

Cette option utilise Microsoft Intune pour inscrire et gérer les appareils au lieu d’utiliser les ressources locales Configuration Manager. Même si Intune gère les appareils, vous accédez à vos tâches de gestion dans la console Configuration Manager. Cette option prend en charge tous les principaux systèmes d’exploitation pour appareils mobiles, notamment Windows 10 Mobile, Windows Phone, iOS et Android. Elle permet également de gérer les ordinateurs Windows 8.1 et Windows 10 de votre organisation.  

Pour plus d’informations, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../mdm/understand/hybrid-mobile-device-management.md).  

###  <a name="manage-devices-with-microsoft-exchange"></a>Gérer les appareils avec Microsoft Exchange  

Cette option utilise le connecteur du serveur Exchange Server pour connecter plusieurs serveurs Exchange à Configuration Manager. Cela centralise la gestion des appareils en mesure de se connecter à Exchange ActiveSync. Vous pouvez configurer les fonctionnalités de gestion des appareils mobiles d’Exchange, telles que la réinitialisation à distance et le contrôle des paramètres de plusieurs serveurs Exchange, dans la console Configuration Manager.  

Pour plus d’informations, consultez [Gérer les appareils mobiles avec System Center Configuration Manager et Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

Vous pouvez utiliser ces solutions de gestion des appareils par elles-mêmes ou les combiner entre elles. Par exemple, vous pouvez utiliser l’approche de la gestion basée sur le client pour gérer les ordinateurs et les serveurs de votre organisation, et utiliser aussi Intune pour gérer les appareils mobiles. En combinant les méthodes de cette façon, vous pouvez couvrir tous vos besoins en matière de gestion d’appareils à partir de la console Configuration Manager.  

## <a name="compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a>Comparer les solutions de gestion des appareils en fonction des plateformes d’appareils mobiles prises en charge  

|Plate-forme|Avec le client Configuration Manager|Configuration Manager avec Microsoft Intune (hybride)|Gestion locale des appareils mobiles|Configuration Manager avec Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||Oui||Oui|  
|iOS||Oui||Oui|  
|Mac OS X|Oui|||Oui|  
|UNIX/Linux|Oui|||Oui|  
|Windows 10|Oui|Oui|Oui|Oui|  
|Windows 10 Mobile||Oui|Oui|Oui|  
|Windows (versions précédentes)|Oui|Oui||Oui|  
|Windows CE|Oui (avec le client hérité de l’appareil mobile)|||Oui|  
|Windows Embedded|Oui||||  
|Windows Phone||Oui||Oui|  
|Windows Server|Oui|||Oui|  

 Pour obtenir la liste complète des plateformes prises en charge, consultez [Systèmes d’exploitation pris en charge pour les clients et les appareils pour System Center Configuration Manager](configs/supported-operating-systems-for-clients-and-devices.md).

##  <a name="bkmk_comp2"></a> Comparer les solutions de gestion des appareils mobiles en fonction des fonctionnalités de gestion  

|Fonctionnalité de gestion|Avec le client Configuration Manager|Configuration Manager avec Microsoft Intune (hybride)|Gestion locale des appareils mobiles|Configuration Manager avec Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Sécurité de l’infrastructure à clé publique (PKI) entre l’appareil mobile et Configuration Manager (utilise l’authentification mutuelle et SSL pour le chiffrement des transferts de données)|Oui|Oui|Oui||  
|Installation du client|Oui||||  
|Prise en charge via Internet|Oui||||  
|découverte,|Oui|||Oui|  
|Inventaire matériel|Oui|Oui|Oui|Oui|  
|Inventaire logiciel|Oui|||Oui|  
|Paramètres|Oui|Oui|Oui|Oui|  
|Déploiement logiciel|Oui|Oui|Oui||  
|Surveillance avec point d’état de secours|Oui||||  
|Connexions aux points de gestion|Oui||Oui||  
|Connexions aux points de distribution|Oui||Oui||  
|Blocage à partir de Configuration Manager|Oui|Oui|Oui||  
|Mise en quarantaine et blocage à partir d’Exchange Server (et Configuration Manager)||||Oui|  
|Réinitialisation à distance| |Oui|Oui|Oui|  
