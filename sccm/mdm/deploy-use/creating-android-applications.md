---
title: Créer des applications Android
titleSuffix: Configuration Manager
description: Comment créer et déployer des applications pour les appareils Android dans Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a95a7735cc7f7afb6a16b030de6925926335e403
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39385216"
---
# <a name="create-android-applications-in-configuration-manager"></a>Créer des applications Android dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application Configuration Manager propose un ou plusieurs types de déploiement. Les types de déploiement comprennent les fichiers d’installation et les informations nécessaires pour déployer des logiciels sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

Pour connaître les étapes permettant de créer des types de déploiement et des applications Configuration Manager, consultez [Créer une application](/sccm/apps/deploy-use/create-applications#bkmk_create). 

Gardez à l’esprit les considérations suivantes quand vous créez et déployez des applications pour appareils Android :  



## <a name="general-considerations-for-android-apps"></a>Éléments généraux à prendre en compte pour les applications Android

Configuration Manager prend en charge le déploiement des packages .apk Android. 

Il prend en charge les actions de déploiement suivantes :

|Type d'appareil|Actions prises en charge|
|-|-|
|Android|**Disponible**, **Obligatoire** : L’utilisateur doit donner son consentement pour l’installation et la désinstallation.|
|Android for Work |**Disponible**, **Obligatoire** |



## <a name="approve-and-deploy-android-for-work-apps"></a>Approuver et déployer des applications Android for Work

En tant qu’administrateur Configuration Manager, vous pouvez également approuver les applications sur le [site web Play for Work](https://play.google.com/work). Ensuite, déployez ces applications sur des appareils Android for Work gérés.

Effectuez les étapes suivantes pour approuver des applications dans le magasin Play for Work, les synchroniser avec la console Configuration Manager et les déployer sur des appareils Android for Work gérés. Pour déployer des applications sur les profils professionnels des utilisateurs, vous devez approuver les applications dans Play for Work. Ensuite, synchronisez-les avec la console Configuration Manager.

1. Ouvrez un navigateur et accédez à : https://play.google.com/work.  

2. Connectez-vous à l’aide du compte d’administrateur Google que vous avez lié à votre locataire Microsoft Intune.  

3. Recherchez les applications que vous souhaitez déployer dans votre environnement. Choisissez **Approuver** pour chacune d’elles pour qu’elles soient disponibles dans Android for Work.  

4. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Android for Work**.  

5. Cliquez sur **Synchroniser** dans le ruban.  

6. Attendez jusqu'à 10 minutes pour que les applications se synchronisent. Ensuite, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Informations de licence pour les applications du Store**.  

7. Sélectionnez une application synchronisée à partir de Play for Work, puis cliquez sur **Créer une application**.  

8. Effectuez toutes les étapes de l'Assistant.  

9. Accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion d’applications** et sélectionnez le nœud **Applications**. Sélectionnez une application Android for Work et déployez-la normalement.  

Pour synchroniser des applications Play for Work avec Configuration Manager, approuvez d’abord au moins une application sur le site web Play for Work.

Les applications déployées comme **disponibles** s’affichent dans l’application Google Play dotée d’une identification professionnelle plutôt que dans le portail d’entreprise. Cela vous permet de déployer des applications à partir d’une source approuvée. L’application Google Play dotée d’un badge professionnel est une source approuvée. Vous n’êtes pas obligé d’autoriser les applications issues de sources non approuvées.
