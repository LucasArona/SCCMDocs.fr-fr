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
ms.collection: M365-identity-device-management
ms.openlocfilehash: e4a2d84fe31c3a524b876e3beb34f0e3d25d0089
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62251393"
---
# <a name="create-ios-applications-in-configuration-manager"></a>Créer des applications iOS dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application Configuration Manager inclut un ou plusieurs types de déploiement, qui comprennent les fichiers d’installation et informations nécessaires pour déployer le logiciel sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

Pour connaître les étapes permettant de créer des types de déploiement et des applications Configuration Manager, consultez [Créer une application](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Gardez à l’esprit les considérations suivantes quand vous créez et déployez des applications pour appareils iOS :  

- Configuration Manager prend en charge le déploiement des packages .ipa iOS. Vous n’avez pas besoin de spécifier de fichier de liste de propriétés (.plist) lors de l’importation d’une application iOS. 

- Déployez les applications iOS comme **Disponible** ou **Obligatoire**. L’utilisateur doit donner son consentement pour l’installation et la désinstallation.

> [!IMPORTANT]  
>  Actuellement, les utilisateurs finaux ne peuvent pas installer des applications d’entreprise à partir de l’application Portail d’entreprise Microsoft Intune pour iOS. Cette limitation est due à des restrictions sur les applications publiées dans l’App Store iOS. (Consultez le guide de validation de l’App Store, Section 2.) Les utilisateurs peuvent installer des applications d’entreprise en accédant au portail Intune sur leur appareil. Ces applications comprennent les applications App Store gérées et les packages d’applications métier. Pour plus d’informations sur les fonctionnalités de gestion des appareils mobiles que permet l’application Portail d’entreprise Intune, consultez [Fonctionnalités de gestion des appareils inscrits dans Microsoft Intune](https://docs.microsoft.com/intune/device-enrollment).  
