---
title: Créer des applications Windows Phone
titleSuffix: Configuration Manager
description: Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour des appareils Windows Phone.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 68fe11fa-5fb2-4b81-b0f5-b6f2392fb4ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c755db47c9d3acb9c858ecb5bed14bb36055663b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-windows-phone-applications-with-system-center-configuration-manager"></a>Créer des applications Windows Phone à l’aide de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application System Center Configuration Manager inclut un ou plusieurs types de déploiement, qui comprennent les fichiers d’installation et informations nécessaires pour déployer le logiciel sur un appareil. Le type de déploiement contient également des règles spécifiant à quel moment et selon quelle méthode le logiciel est déployé.  

 Vous pouvez créer des applications à l'aide des méthodes suivantes :  

-   Créer automatiquement les types d'application et de déploiement en lisant les fichiers d'installation de l'application.  

-   Créer manuellement l'application, puis ajouter des types de déploiement ultérieurement.  

-   Importer une application à partir d’un fichier.  

Pour connaître les étapes requises pour créer des types de déploiement et applications Configuration Manager, voir [Démarrer l’Assistant Création d’une application](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard). De plus, gardez à l’esprit les considérations suivantes lorsque vous créez et déployez des applications pour des appareils Windows Phone.  

## <a name="general-considerations"></a>Considérations générales  
 Configuration Manager prend en charge le déploiement des types de fichiers d’application suivants :  

|Type d'appareil|Types de fichiers pris en charge|  
|-----------------|---------------------|  
|Windows Phone 8|.xap|  
|Windows Phone 8.1|.xap, .appx, .appxbundle|
|Windows 10 Mobile|.xap, .appx, .appxbundle|

 Les actions de déploiement suivantes sont prises en charge :  

|Type d'appareil|Actions prises en charge|  
|-----------------|-----------------------|  
|Windows Phone 8, Windows Phone 8.1 et Windows 10 Mobile|Disponible, Obligatoire, Désinstaller|  

## <a name="steps-to-deploy-the-latest-windows-phone-company-portal-app-with-supersedence"></a>Étapes de déploiement de la dernière version de l’application de portail d’entreprise Windows Phone avec remplacement  
 Le tableau suivant présente la procédure, des détails et des informations complémentaires pour créer et déployer la dernière version de l'application de portail d'entreprise Windows Phone 8.  

|Étape|Plus d'informations|  
|----------|----------------------|  
|**Étape 1 :** obtenir la dernière application de portail d’entreprise.|Téléchargez l' [application du portail d'entreprise Windows Phone 8](http://go.microsoft.com/fwlink/?LinkId=268440).|  
|**Étape 2 :** signer l’application de portail d’entreprise avec votre certificat Symantec.|Pour plus d’informations sur la façon de signer l’application de portail d’entreprise, consultez [Configurer la gestion des appareils Windows Phone et Windows 10 Mobile hybrides avec System Center Configuration Manager et Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Étape 3 :** Créer une application avec la version la plus récente de l’application de portail d’entreprise et spécifier une relation de remplacement.|Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md) et [Réviser et remplacer des applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Étape 4 :** ajouter l’application à l’Assistant Créer un abonnement Windows Intune.|Pour plus d’informations, consultez [Configurer la gestion des appareils Windows Phone et Windows 10 Mobile hybrides avec System Center Configuration Manager et Microsoft Intune](../../mdm/deploy-use/enroll-hybrid-windows.md).|  
|**Étape 5 :** supprimer le déploiement qui est automatiquement créé lorsque vous avez ajouté l’application de portail d’entreprise à l’Assistant Créer un abonnement Microsoft Intune.|L’abonnement Microsoft Intune a créé un déploiement automatique de cette application, car ce déploiement ne prendra pas en charge le remplacement.|  
|**Étape 6 :** Créer un déploiement de l’application. Dans la page **Paramètres de déploiement** de l’**Assistant Déploiement logiciel**, cochez la case **Mettre automatiquement à niveau toutes les versions remplacées de cette application**.|Créez un nouveau déploiement avec le remplacement à l'aide de l'application que vous avez créée avec la relation de remplacement.|  
|**Étape 7 (facultative) :** Par défaut, les applications de remplacement s’installent sur les appareils au bout de sept jours. Pour déployer l’application de portail d’entreprise plus tôt sur les appareils inscrits auparavant, définissez le paramètre **Planifier la réévaluation des déploiements** sur une valeur inférieure.<br /><br /> Si vous affectez à cette valeur une valeur inférieure à la valeur par défaut, cela peut affecter négativement les performances de votre réseau et des ordinateurs clients.|Aucune information supplémentaire.|  
