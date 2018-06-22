---
title: Créer des applications iOS
titleSuffix: Configuration Manager
description: Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour des appareils iOS.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 985a8177602bd32da0b6134eeddb564a44749d65
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32346428"
---
# <a name="create-ios-applications-with-system-center-configuration-manager"></a>Créer des applications iOS avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application System Center Configuration Manager inclut un ou plusieurs types de déploiement, qui comprennent les fichiers d’installation et informations nécessaires pour déployer le logiciel sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

 Vous pouvez créer des applications à l'aide des méthodes suivantes :  

-   Créer automatiquement les types d'application et de déploiement en lisant les fichiers d'installation de l'application.  

-   Créer manuellement l'application, puis ajouter des types de déploiement ultérieurement.  

-   Importer une application à partir d’un fichier.  

Pour connaître les étapes requises pour créer des types de déploiement et applications Configuration Manager, voir [Démarrer l’Assistant Création d’une application](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). De plus, gardez à l’esprit les considérations suivantes lorsque vous créez et déployez des applications pour les appareils iOS.  

## <a name="general-considerations"></a>Considérations générales  
 Configuration Manager prend en charge le déploiement des types d’applications suivants :  

|Type d'appareil|Fichiers pris en charge|  
|-----------------|---------------------|  
|iOS|*.ipa<br /><br /> Dans System Center Configuration Manager, vous n’avez pas besoin de spécifier de fichier de liste de propriétés (.plist) lors de l’importation d’une application iOS.|  

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|iOS|**Disponible**, **Obligatoire**. L’utilisateur doit donner son consentement pour l’installation et la désinstallation.

> [!IMPORTANT]  
>  Actuellement, les utilisateurs finaux ne peuvent pas installer des applications d’entreprise à partir de l’application Portail d’entreprise Microsoft Intune pour iOS. Cela est dû au fait qu’il existe des restrictions concernant les applications publiées dans l’App Store iOS (consultez Directives de révision App Store, à la section 2). Les utilisateurs peuvent installer des applications d’entreprise (y compris les applications App Store gérées et des packages d’applications métiers) via le portail web Intune sur leur appareil (portal.manage.microsoft.com). Pour plus d’informations sur les fonctionnalités de gestion des appareils mobiles activées par l’application Portail d’entreprise Intune, consultez [Fonctionnalités de gestion des appareils inscrits de Microsoft Intune](https://technet.microsoft.com/library/dn600287.aspx).  
