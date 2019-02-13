---
title: Gérer les applications iOS achetées en volume
titleSuffix: Configuration Manager
description: Déployez, gérez et suivez les licences d’applications que vous avez achetées via l’App Store iOS d’Apple.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7c3b9316-247b-490b-a363-8f8553821579
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21d8666f6c05b540891037cc1917b755ed22fdcc
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129390"
---
# <a name="manage-volume-purchased-ios-apps-with-system-center-configuration-manager"></a>Gérer des applications iOS achetées en volume avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*



 L’App Store iOS d’Apple vous permet d’acheter plusieurs licences d’une application que vous souhaitez exécuter dans votre entreprise. Vous pouvez ainsi réduire les coûts d’administration liés au suivi de plusieurs copies d’applications achetées.  

 Configuration Manager vous permet de déployer et de gérer les applications iOS achetées via le programme. Vous pouvez importer les informations de la licence à partir de l’App Store et suivre le nombre de licences que vous utilisez.  



## <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gérer les applications pour appareils iOS achetées en volume  
 Vous achetez plusieurs licences d’applications iOS via le Programme d’achat en volume (VPP) Apple. Ce processus implique tout d’abord la configuration d’un compte Apple VPP à partir du site web Apple. Puis, chargez le jeton Apple VPP dans Configuration Manager, qui offre les fonctionnalités suivantes :  

-   Synchroniser vos informations sur les achats en volume avec Configuration Manager  
 
- Synchroniser les applications du programme d’achat en volume pour les entreprises et du programme d’achat en volume pour l’éducation d’Apple  

- Associer plusieurs jetons de programme d’achat de volume Apple à Configuration Manager  

-   Affichage des applications achetées dans la console Configuration Manager  

-   Déployer et surveiller ces applications  

-   Suivre le nombre de licences utilisées pour chaque application   

-   Si nécessaire, Configuration Manager peut vous permettre de récupérer des licences en désinstallant les applications achetées en volume que vous avez déployées  



## <a name="before-you-start"></a>Avant de commencer  
 Avant de commencer, vous devez vous procurer un jeton VPP auprès d’Apple et le charger sur Configuration Manager.  

-   Si vous avez précédemment utilisé un jeton VPP avec un autre produit MDM dans votre compte Apple VPP existant, vous devez en générer un nouveau pour l’utiliser avec Configuration Manager.  
-   Chaque jeton est valide pendant un an.  
-   Par défaut, Configuration Manager se synchronise avec le service Apple VPP deux fois par jour pour vérifier que vos licences sont synchronisées avec Configuration Manager. Seules les modifications apportées à vos licences sont synchronisées. Une synchronisation complète est assurée une fois tous les sept jours. Quand vous choisissez **Synchroniser** pour effectuer une synchronisation manuelle, celle-ci est toujours complète.  
-   Si vous avez besoin de récupérer ou restaurer votre base de données Configuration Manager, nous vous recommandons d’effectuer une synchronisation manuelle après cette opération. Ceci permet de vous assurer que vos données de licence synchronisées sont à jour.  
-   De plus, vous devez avoir importé un certificat du service de notifications Push Apple (APNs) à partir d’Apple. Ce certificat vous permet de gérer des appareils iOS, ce qui inclut le déploiement d’applications. Pour plus d’informations, consultez [Configurer la gestion des appareils iOS hybride](enroll-hybrid-ios-mac.md).  
-   Configuration Manager prend en charge l’ajout de 3000 jetons VPP maximum.

Vous pouvez déployer des applications sous licence pour les utilisateurs et les appareils. En fonction de la capacité des applications à prendre en charge les licences d’appareils, une licence appropriée est réclamée lors du déploiement, comme suit :

|L’application prend-elle en charge les licences d’appareil ?|Type de regroupement de déploiement|Licence demandée|
|---|---|---|
|Oui|utilisateur|Licence utilisateur|
|Non|utilisateur|Licence utilisateur|
|Oui|Appareil|Licence d’appareil|
|Non|Appareil|Licence utilisateur|



## <a name="step-1---to-get-and-upload-an-apple-vpp-token"></a>Étape 1 : obtenir et charger un jeton Apple VPP  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Services cloud** > **Jetons du programme d’achat en volume (VPP) Apple**.   

3.  Sous l’onglet **Accueil**, dans le groupe **Jetons du programme d’achat en volume (VPP) Apple**, choisissez **Ajouter un jeton du programme d’achat en volume (VPP) Apple**.  

4.  Dans la page **Général** de l’Assistant **Ajouter un jeton du programme d’achat en volume (VPP) Apple**, configurez les paramètres suivants :   

    -   **Nom** : attribuez un nom à ce jeton tel qu’il s’affichera dans la console Configuration Manager.  

    -   **Jeton** : choisissez **Parcourir** et le jeton VPP que vous avez téléchargé sur le site web Apple.  

         Cliquez sur le lien **See Apple VPP account** (Voir le compte VPP Apple). Si ce n’est déjà fait, souscrivez à un programme d’achats en volume pour les entreprises ou l’enseignement. Une fois inscrit, téléchargez le jeton Apple VPP pour votre compte.  

    -   **Description** : si vous le souhaitez, entrez une description pour faciliter l’identification de ce jeton dans la console Configuration Manager.  

    -   **Catégories attribuées pour améliorer la recherche et le filtrage** : si vous le souhaitez, vous pouvez attribuer des catégories au jeton VPP pour faciliter sa recherche dans la console Configuration Manager.  
    -   **ID Apple** : entrez l’ID de l’adresse électronique Apple associée au jeton VPP.
    -   **Type de jeton** : sélectionnez le type de jeton VPP que vous souhaitez utiliser. Vous pouvez choisir les types de jetons **Business** et **EDU**.

5.  Choisissez **Suivant**, puis terminez l’Assistant.  

À partir du nœud **Jetons du programme d’achat en volume (VPP) Apple**, vous pouvez désormais afficher des informations sur le jeton Apple VPP. Cette vue inclut la dernière mise à jour, la date d’expiration et la date de la dernière synchronisation.

Vous pouvez à tout moment synchroniser entièrement les données détenues par Apple à l’aide de Configuration Manager en choisissant **Synchroniser** dans le ruban.  



## <a name="step-2---deploy-a-volume-purchased-app"></a>Étape 2 : déployer une application achetée en volume  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Informations de licence pour les applications du Store**.  

2. Choisissez l’application que vous voulez déployer puis, sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application**.
   L’application Configuration Manager qui est créée contient l’application Microsoft Store pour Entreprises. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.  

   > [!IMPORTANT]  
   > Vous devez choisir l’objectif de déploiement **Obligatoire**. Les installations disponibles ne sont pas prises en charge actuellement.

   Quand vous déployez l’application, une licence est utilisée par chaque utilisateur, ou pour les installations d’appareils, chaque appareil qui installe l’application. Si vous ciblez un regroupement d’appareils avec une application prenant en charge les licences d’appareils, une licence d’appareil est demandée. Si vous ciblez un regroupement d’appareils avec une application ne prenant pas en charge les licences d’appareils, une licence d’utilisateur est demandée. 

   Lorsque vous créez une application à partir du nœud **Informations de licence pour les applications du Windows Store**, l’application est associée à des licences provenant du jeton de l’application que vous avez sélectionnée. Par exemple, vous pouvez afficher les deux versions de la même application dans le nœud. En effet, chaque version de l’application est associée à un jeton VPP Apple distinct. Vous pouvez ensuite créer des applications à partir de chaque jeton et les déployer séparément.

   Pour récupérer une licence, vous devez créer un déploiement de l’application avec l’action de déploiement **Désinstaller**. Vous ne pouvez pas changer l’action de déploiement dans le déploiement d’origine. La licence est récupérée une fois l’application désinstallée.  



## <a name="step-3---monitor-ios-vpp-apps"></a>Étape 3 : surveiller les applications VPP iOS  
 Le nœud **Informations de licence pour les applications du Store** de l’espace de travail **Bibliothèque de logiciels** affiche des informations sur vos applications iOS achetées en volume. Celles-ci incluent le nombre total de licences qui vous appartiennent pour chaque application ainsi que le nombre de licences qui ont été déployées. En outre, la vue indique le jeton VPP auquel l’application est associée et le type du jeton

 Vous pouvez aussi surveiller l’utilisation des licences de toutes les applications VPP que vous avez achetées à l’aide du rapport **Applications du programme d’achat en volume (VPP) Apple pour iOS avec les nombres de licences**.  

 Ce rapport affiche le nom de chaque application, ainsi que le nombre total de licences achetées, le nombre de licences disponibles et d’autres informations.  

 Pour obtenir de l’aide sur l’exécution des rapports Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  



## <a name="delete-an-apple-vpp-token"></a>Supprimer un jeton Apple VPP  
<!--505268-->

Pour supprimer un jeton à partir de Configuration Manager, procédez comme suit :  

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Services cloud** et sélectionnez **Jetons du programme d’achat en volume (VPP) Apple**.  

2. Sélectionnez le jeton que vous voulez supprimer.  

3. Cliquez sur l’option **Supprimer** dans le ruban.  

