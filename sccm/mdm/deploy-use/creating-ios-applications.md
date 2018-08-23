---
title: Créer des applications iOS
titleSuffix: Configuration Manager
description: Comment créer et déployer des applications pour les appareils iOS dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ff633013-5313-4cd3-949c-56d45e777280
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 246ca26b8fab3a1006e8d72b803c298fe48df9df
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385233"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Créer des applications iOS dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application Configuration Manager inclut un ou plusieurs types de déploiement, qui comprennent les fichiers d’installation et informations nécessaires pour déployer le logiciel sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

Pour connaître les étapes permettant de créer des types de déploiement et des applications Configuration Manager, consultez [Créer une application](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Gardez à l’esprit les considérations suivantes quand vous créez et déployez des applications pour appareils iOS :  

- Configuration Manager prend en charge le déploiement des packages .ipa iOS. Vous n’avez pas besoin de spécifier de fichier de liste de propriétés (.plist) lors de l’importation d’une application iOS. 

- Déployez les applications iOS comme **Disponible** ou **Obligatoire**. L’utilisateur doit donner son consentement pour l’installation et la désinstallation.

> [!IMPORTANT]  
>  Actuellement, les utilisateurs finaux ne peuvent pas installer des applications d’entreprise à partir de l’application Portail d’entreprise Microsoft Intune pour iOS. Cette limitation est due à des restrictions sur les applications publiées dans l’App Store iOS. (Consultez le guide de validation de l’App Store, Section 2.) Les utilisateurs peuvent installer des applications d’entreprise en accédant au portail Intune sur leur appareil. Ces applications comprennent les applications App Store gérées et les packages d’applications métier. Pour plus d’informations sur les fonctionnalités de gestion des appareils mobiles que permet l’application Portail d’entreprise Intune, consultez [Fonctionnalités de gestion des appareils inscrits dans Microsoft Intune](https://docs.microsoft.com/intune/device-enrollment).  
