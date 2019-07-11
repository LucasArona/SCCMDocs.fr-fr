---
title: Analyses du bureau
titleSuffix: Configuration Manager
description: Une vue d’ensemble du service Analytique de bureau intégré à Configuration Manager.
ms.date: 06/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b0daf2943b0859227d08069be9c9da69165d5d1a
ms.sourcegitcommit: de3c86077bbf91b793e94e1f60814df18da11bab
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67726227"
---
# <a name="what-is-desktop-analytics"></a>Nouveautés d’Analytique de bureau ?

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Postes de travail Analytique est un service basé sur le cloud qui s’intègre avec Configuration Manager. Le service fournit un aperçu et analyse décisionnelle afin de pouvoir prendre des décisions plus avisées sur la préparation de la mise à jour de vos clients Windows. Il combine les données à partir de votre organisation avec les données agrégées provenant de millions d’appareils connectés aux services de cloud de Microsoft.

Utilisez les postes de travail Analytique à Configuration Manager pour :  

- Créer un inventaire des applications qui s’exécutent dans votre organisation  

- Évaluer la compatibilité des applications avec les dernières mises à jour de fonctionnalité de Windows 10  

- Identifier les problèmes de compatibilité et recevoir des suggestions d’atténuation basées sur les analyses de données activée pour le cloud  

- Créer des groupes de pilotes qui représentent le parc informatique complet applications et des pilotes sur un ensemble minimal d’appareils  

- Déployer Windows 10 sur les appareils de pilotes et gérés en production  

![Capture d’écran de la page d’accueil Analytique de bureau dans le portail Azure](media/portal-home.png)

> [!Note]  
> Postes de travail Analytique est un successeur de Windows Analytique. Le *Windows Analytique* service inclut Upgrade Readiness, la conformité de mise à jour et intégrité de l’appareil.
>
> Toutes ces fonctionnalités sont combinées dans les *Desktop Analytique* service. Analytique de postes de travail est également plus étroitement intégrée avec Configuration Manager.



## <a name="benefits"></a>Avantages

De nombreux clients ont des défis liés à l’obtention et de rester à jour avec Windows 10. Le défi principal consiste à tester les applications. Ce processus est généralement manuel. Il s’agit du temps pour les administrateurs informatiques et aux propriétaires d’applications à analyser en permanence des applications existantes. Puis résoudre les problèmes qui surviennent.

Analytique de bureau offre les avantages suivants :

- **L’inventaire logiciel et de périphérique**: Inventaire des facteurs clés tels que les applications et les versions de Windows.  

- **Identification de piloter**: Identification du plus petit ensemble d’appareils qui fournissent la plus large couverture de facteurs. Il se concentre sur les facteurs les plus importants pour un pilote de mises à niveau de Windows et les mises à jour. S’assurer que le pilote ne réussit plus vous permet de procéder plus rapidement et en toute confiance aux grands déploiements en production.  

- **Émettre identification**: À l’aide des données agrégées sur le marché, ainsi que des données à partir de votre environnement, le service prédit potentiel émet pour l’obtention et de rester à jour avec Windows. Ensuite, il suggère des solutions d’atténuation possibles.  

- **Intégration de configuration Manager**: Le service cloud-permet de votre infrastructure locale existante. Utilisez ces données et l’analyse pour déployer et gérer Windows sur vos appareils.  



## <a name="prerequisites"></a>Prérequis

Pour utiliser l’Analytique de bureau, assurez-vous que votre environnement remplit les conditions préalables suivantes.


### <a name="technical"></a>Techniques

- Un abonnement Azure actif, avec [administrateur général](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) autorisations  

    - **Propriétaire de l’espace de travail** ou **contributeur** autorisations pour **configurer votre espace de travail**et les rôles suivants :  

      - [**Analytique de Desktop Administrator** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) rôle.

      - [**Journal Analytique contributeur** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) et [ **administrateur des accès utilisateur** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) sur le groupe de ressources à utiliser un espace de travail existant ou créer un espace de travail dans un groupe de ressources existant.

      - [**Propriétaire**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner), ou [ **contributeur** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) et [ **administrateur des accès utilisateur** ](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) autorisations sur le abonnement pour créer un espace de travail dans un groupe de ressources.  

- Configuration Manager, version 1902 avec mise à jour cumulative (4500571) ou version ultérieure. Pour plus d’informations, consultez [mise à jour Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - **Administrateur complet** rôle dans le Gestionnaire de Configuration  

- Appareils exécutant Windows 7, Windows 8.1 ou Windows 10  

    - Installez les dernières mises à jour. Pour plus d’informations, consultez [mettre à jour des appareils](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Appareils doivent également disposer du client Configuration Manager, version 1902 avec mise à jour cumulative (4500571) ou version ultérieure. Pour plus d’informations, consultez [mise à jour Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    > [!Note]  
    > Analytique de postes de travail ne prend pas en charge les mises à niveau vers Windows 10 canal maintenance à long terme (LTSC). Pour plus d’informations, consultez [Windows comme une vue d’ensemble du service](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Analytique de bureau est conçu pour le meilleur scénario de mise à niveau de prise en charge de la place. Si vous avez besoin d’apporter des modifications majeures, comme à partir de l’architecture 32 bits vers 64 bits, utilisez un scénario d’acquisition d’images. Bureau insights Analytique sont toujours utiles dans ces scénarios de déploiement de système d’exploitation classiques, mais vous pouvez ignorer les instructions spécifiques mise à niveau sur place. Pour plus d’informations, consultez [scénarios de déploiement de systèmes d’exploitation d’entreprise avec Configuration Manager](/sccm/osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems).

- Données de diagnostic de Windows. Pour plus d’informations, consultez les articles suivants :  

    - [Niveaux de données de diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Bureau confidentialité Analytique](/sccm/desktop-analytics/privacy)  

- La connectivité réseau à partir d’appareils vers le cloud public Microsoft. Pour plus d’informations, consultez [comment activer le partage de données](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>Gestion des licences

Analytique bureau nécessite les abonnements de licence suivants :

- Windows 10 entreprise E3 ou E5 ; ou Microsoft 365 F1, E3 ou E5  

- Windows 10 éducation A3 ou A5 ; ou Microsoft 365 A3 ou A5  

- Windows VDA E3 ou E5  




## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel fournit des instructions détaillées pour bien démarrer avec Desktop Analytique et de Configuration Manager :  

- [Déployer Windows 10 sur le pilote](/sccm/desktop-analytics/tutorial-windows10)  
