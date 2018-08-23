---
title: Microsoft Store pour Entreprises
titleSuffix: Configuration Manager
description: Gérez et déployez des applications à partir du Microsoft Store pour Entreprises avec Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae137cae29d49413ca11668ff0cc744168e91e21
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383675"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-with-configuration-manager"></a>Gérer des applications à partir du Microsoft Store pour Entreprises avec Configuration Manager

Le [Microsoft Store pour Entreprises](https://www.microsoft.com/business-store) vous donne accès à des applications Windows que vous pouvez acquérir pour votre organisation. Quand vous connectez le Store à Configuration Manager, vous synchronisez la liste des applications que vous avez acquises. Affichez ces applications dans la console Configuration Manager et déployez-les comme toute autre application.


## <a name="bkmk_apps"></a> Applications en ligne et hors connexion

Le Microsoft Store pour Entreprises prend en charge deux types d’applications :

- **En ligne** : ce type de licence exige que les utilisateurs et les appareils se connectent au Store pour obtenir une application et sa licence. Les appareils Windows 10 doivent être joints au domaine Azure Active Directory (Azure AD).  

- **Hors connexion** : ce type vous permet de mettre en cache les applications et les licences à déployer directement sur votre réseau local. Les appareils n’ont pas besoin de se connecter au Store ou de disposer d’une connexion à Internet.

[Découvrez-en plus](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview) sur le Microsoft Store pour Entreprises.

Configuration Manager prend en charge la gestion des applications du Microsoft Store pour Entreprises sur les appareils Windows 10 exécutant le client Configuration Manager, ainsi que sur les appareils Windows 10 inscrits auprès de Microsoft Intune. Les fonctionnalités offertes par Configuration Manager pour les applications en ligne et hors connexion sont répertoriées ci-dessous :


|Fonctionnalité|Applications hors connexion|Applications en ligne|
|------------|------------|------------|
|Synchronisation des données d’application dans Configuration Manager<br>(la synchronisation a lieu toutes les 24 heures)|Oui|Oui|
|Création d’applications Configuration Manager à partir d’applications du Windows Store|Oui|Oui|
|Prise en charge des applications gratuites du Windows Store|Oui|Oui|
|Prise en charge des applications payantes du Windows Store|Non|Oui<sup>1</sup>|
|Prise en charge des déploiements obligatoires sur les regroupements d’utilisateurs ou d’appareils|Oui|Oui|
|Prise en charge des déploiements disponibles sur les regroupements d’utilisateurs ou d’appareils|Oui|Oui|
|Prise en charge des applications métier à partir du Store|Oui|Oui|
|Provisionner une application du Store pour tous les utilisateurs sur un appareil<sup>2</sup><!--1358310-->|Oui|Oui|

- <sup>1</sup> Pour déployer des applications sous licence en ligne sur des appareils Windows 10 avec le client Configuration Manager, ces appareils doivent exécuter Windows 10, version 1703 ou ultérieure.  

- <sup>2</sup> Depuis la version 1806. Pour plus d’informations, consultez [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  


### <a name="deploying-online-apps-using-the-microsoft-store-for-business-to-devices-that-run-the-configuration-manager-client"></a>Déploiement d’applications en ligne à l’aide du Microsoft Store pour Entreprises sur des appareils exécutant le client Configuration Manager

Avant de déployer des applications Microsoft Store pour Entreprise sur des appareils exécutant le client Configuration Manager complet, prenez en considération les points suivants :

- Pour bénéficier de toutes les fonctionnalités, les appareils doivent exécuter Windows 10, version 1703 ou ultérieure.  

- Les appareils doivent être joints à Azure AD et se trouver dans le même locataire que celui où vous avez enregistré le Microsoft Store pour Entreprises comme outil de gestion.  

- Quand le compte d’administrateur local se connecte à l’appareil, il ne peut pas accéder aux applications du Microsoft Store pour Entreprises.  

- Les appareils doivent disposer d’une connexion Internet active vers le Microsoft Store pour Entreprises. Pour plus d’informations, y compris sur la configuration du proxy, consultez [Prérequis](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  


### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Notes concernant les appareils exécutant des versions antérieures de Windows 10

Sur les appareils dotés du client Configuration Manager et exécutant Windows 10 version 1607 ou antérieure, les fonctionnalités suivantes s’appliquent :  

Quand vous effectuez l’installation de l’application sur l’appareil au moyen d’une des méthodes suivantes :  

- L’utilisateur installe l’application  

- Le déploiement atteint son échéance d’installation   

- Les déploiements requis font l’objet d’une réévaluation après l’installation  

Les comportements suivants se produisent :  

- Le client Configuration Manager « met en œuvre » l’application en lançant l’application Microsoft Store pour Entreprises  

- L’utilisateur doit effectuer l’installation à partir du Store  

- Dans la console Configuration Manager, l’état du déploiement indique un échec avec l’erreur suivante : « L’application Microsoft Store a été ouverte sur le PC client et attend que l’utilisateur termine l’installation. »  

Au prochain cycle d’évaluation de l’application :  

- Si l’utilisateur a installé l’application à partir du Store, l’application affiche l’état **Réussite**.  

- Si l’utilisateur n’a pas essayé d’installer l’application à partir du Store :  

    - Pour les déploiements requis, le client Configuration Manager tente de relancer l’application du Store  

    - Les déploiements disponibles ne sont pas remis en œuvre


#### <a name="further-notes-for-devices-running-earlier-versions-of-windows-10"></a>Notes supplémentaires concernant les appareils exécutant des versions antérieures de Windows 10 :

- Vous ne pouvez pas déployer d’applications métier à partir du Microsoft Store pour Entreprises.  

- Quand vous déployez des applications payantes à partir du Store, les utilisateurs doivent se connecter au Store et acquérir eux-mêmes l’application.  

- Si vous déployez une stratégie de groupe pour désactiver l’accès à la version grand public de Microsoft Store, les déploiements à partir du Microsoft Store pour Entreprises ne fonctionnent pas. Il en est ainsi, même si le Microsoft Store pour Entreprises est activé.  



## <a name="bkmk_setup"></a> Configurer la synchronisation du Microsoft Store pour Entreprises

La synchronisation de la liste des applications acquises par votre organisation vous permet de voir ces applications dans la console Configuration Manager.

Connectez votre site Configuration Manager à Azure AD et au Microsoft Store pour Entreprises. Pour plus d’informations sur ce processus, consultez [Configurer des services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard). Créez une connexion au service **Microsoft Store pour Entreprises**.


### <a name="bkmk_config"></a> Configuration et des informations supplémentaires 

Dans la page **Application** de l’Assistant Services Azure, configurez d’abord **l’environnement Azure** et **l’application web**. Ensuite, lisez la section **Plus d’informations** en bas de la page. Ces informations incluent les actions supplémentaires suivantes dans le portail Microsoft Store pour Entreprises :  

- Configurez Configuration Manager en tant qu’outil de gestion du Store. Pour plus d’informations, consultez [Configurer un fournisseur de gestion](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Activez la prise en charge des applications sous licence hors connexion. Pour plus d’informations, consultez [Distribuer des applications hors connexion](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Acquérez au moins une application. Pour plus d’informations, consultez [Rechercher et acquérir des applications](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

Dans la page **Configurations** de l’Assistant Services Azure, spécifiez les informations suivantes :  

- **Chemin de stockage du contenu de l’application Microsoft Store pour Entreprises** : spécifiez un chemin réseau partagé, dossier compris. Par exemple, `\\server\share\folder`. Quand le serveur de site se synchronise avec le Store, il met en cache le contenu à cet emplacement. Quand vous créez une application dans Configuration Manager, le serveur de site copie le contenu de l’application depuis ce cache local vers la bibliothèque de contenu du site.  

- **Langues sélectionnées** : sélectionnez les langues à synchroniser à partir du Store et à présenter aux utilisateurs dans le Centre logiciel. Par exemple, si l’utilisateur configure Windows pour l’allemand, le Centre logiciel affiche des chaînes en allemand pour l’application du Store. Ce comportement nécessite que cette langue soit synchronisée et qu’elle existe pour l’application concernée.    

- **Langue par défaut** : si la langue de l’utilisateur n’est pas disponible, sélectionnez la langue par défaut à utiliser.  



## <a name="bkmk_deploy"></a> Créer et déployer une application Configuration Manager à partir d’une application du Microsoft Store pour Entreprises

Après la synchronisation, créez et déployez les applications du Store comme n’importe quelle autre application.

1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.  

2.  Choisissez l’application que vous souhaitez déployer, puis cliquez sur **Créer une application** dans le ruban.  

Le site crée une application Configuration Manager contenant l’application du Microsoft Store pour Entreprises. 

Ensuite, déployez et surveillez cette application comme n’importe quelle autre application Configuration Manager. Pour plus d’informations, consultez les articles suivants :  
- [Déployer des applications](/sccm/apps/deploy-use/deploy-applications)
- [Surveiller les applications à partir de la console](/sccm/apps/deploy-use/monitor-applications-from-the-console)

> [!IMPORTANT]  
> Pour les appareils inscrits auprès de Microsoft Intune, les applications déployées sont uniquement accessibles à l’utilisateur qui est à l’origine de l’inscription de l’appareil. Aucun autre utilisateur ne peut accéder à l’application.



## <a name="next-steps"></a>Étapes suivantes

Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.

Pour chaque application du Store que vous gérez, affichez les informations suivantes la concernant :
- Nom de l’application
- Plateforme de l’application
- Nombre de licences pour l’application que vous détenez
- Nombre de licences disponibles

Après le déploiement d’applications en ligne, toute mise à jour de cette application provient directement du Microsoft Store. De plus, Configuration Manager ne vérifie pas la compatibilité des versions des applications en ligne. Windows signale simplement l’application comme étant installée.  

Quand vous déployez des applications hors connexion sur des appareils Windows 10 avec le client Configuration Manager, n’autorisez pas les utilisateurs à mettre à jour des applications externes aux déploiements Configuration Manager. Le contrôle des mises à jour des applications hors connexion est particulièrement important dans les environnements multi-utilisateurs tels que les classes. L’une des façons de désactiver le Microsoft Store consiste à utiliser la [stratégie de groupe](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#a-href-idblock-store-group-policyablock-microsoft-store-using-group-policy). 

Une fois que l’administrateur Microsoft Store pour Entreprises a acquis une application hors connexion, ne publiez pas l’application pour des utilisateurs par le biais du store. Cette configuration garantit que les utilisateurs ne peuvent pas effectuer d’installation ou de mise à jour en ligne. Les utilisateurs reçoivent uniquement les mises à jour d’applications hors connexion par le biais de Configuration Manager. 
