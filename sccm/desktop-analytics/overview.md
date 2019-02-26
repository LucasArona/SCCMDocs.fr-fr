---
title: Analyses du bureau
titleSuffix: Configuration Manager
description: Une vue d’ensemble du service Analytique de bureau intégré à Configuration Manager.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8602db7ece8d786598eb419eb855f1c77cff35ca
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754900"
---
# <a name="what-is-desktop-analytics"></a>Nouveautés d’Analytique de bureau ?

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Postes de travail Analytique est un service basé sur le cloud qui s’intègre avec Configuration Manager. Le service fournit un aperçu et analyse décisionnelle afin de pouvoir prendre des décisions plus avisées sur la préparation de la mise à jour de vos clients Windows et Office. Il combine les données à partir de votre organisation avec les données agrégées provenant de millions d’appareils connectés aux services de cloud de Microsoft. 

Utilisez les postes de travail Analytique à Configuration Manager pour :  

- Créer un inventaire des applications qui s’exécutent dans votre organisation  

- Évaluer la compatibilité des applications avec les dernières mises à jour de la fonctionnalité de Windows 10 et Office 365 ProPlus  

- Identifier les problèmes de compatibilité et recevoir des suggestions d’atténuation basées sur les analyses de données activée pour le cloud  

- Créer des groupes de pilotes qui représentent le parc informatique complet applications et des pilotes sur un ensemble minimal d’appareils  

- Déployer Windows 10 et Office 365 ProPlus aux appareils de pilotes et gérés en production  

![Capture d’écran de la page d’accueil Analytique de bureau dans le portail Azure](media/portal-home.png)

> [!Note]  
> Postes de travail Analytique est un successeur de Windows Analytique. Le *Windows Analytique* service inclut Upgrade Readiness, la conformité de mise à jour et intégrité de l’appareil. 
> 
> Toutes ces fonctionnalités sont combinées dans les *Desktop Analytique* service. Analytique de bureau est plus étroitement avec Configuration Manager et inclut à la fois Windows et Office. 



## <a name="benefits"></a>Avantages

De nombreux clients ont des difficultés avec l’obtention et de rester à jour avec Windows 10 et Office 365 ProPlus. Le défi principal consiste à tester les applications. Ce processus est généralement manuel. Il s’agit du temps pour les administrateurs informatiques et aux propriétaires d’applications à analyser en permanence des applications existantes. Puis résoudre les problèmes qui surviennent. 

Analytique de bureau offre les avantages suivants :

- **L’inventaire logiciel et de périphérique**: Inventaire des facteurs clés tels que les applications, les compléments, les macros et les versions d’Office et Windows.  

- **Identification de piloter**: Identification du plus petit ensemble d’appareils qui fournissent la plus large couverture de facteurs. Il se concentre sur les facteurs les plus importants pour un pilote de mises à jour et mises à jour Windows et Office. S’assurer que le pilote ne réussit plus vous permet de procéder plus rapidement et en toute confiance aux grands déploiements en production.  

- **Émettre identification**: À l’aide des données agrégées sur le marché, ainsi que des données à partir de votre environnement, le service prédit potentiel émet pour l’obtention et de rester à jour avec Windows et Office. Ensuite, il suggère des solutions d’atténuation possibles.  

- **Intégration de configuration Manager**: Le service cloud-permet de votre infrastructure locale existante. Utilisez ces données et l’analyse pour déployer et gérer Windows et Office sur vos appareils.  



## <a name="prerequisites"></a>Prérequis

Pour utiliser l’Analytique de bureau, assurez-vous que votre environnement remplit les conditions préalables suivantes. 


### <a name="technical"></a>Techniques

- Un abonnement Azure actif  

    - **Administrateur d’entreprise** autorisations dans Azure  

- Configuration Manager, version 1810 avec correctif cumulatif 4486457 ou version ultérieure. Pour plus d’informations, consultez [mise à jour Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

    - **Administrateur complet** rôle dans le Gestionnaire de Configuration  

- Appareils exécutant Windows 7, Windows 8.1 ou Windows 10  

    - Installez les dernières mises à jour. Pour plus d’informations, consultez [mettre à jour des appareils](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Appareils doivent également avoir le client Configuration Manager, version 1810 avec correctif cumulatif 4486457 ou version ultérieure. Pour plus d’informations, consultez [mise à jour Configuration Manager](/sccm/desktop-analytics/connect-configmgr#bkmk_hotfix).  

- Données de diagnostic de Windows. Pour plus d’informations, consultez les articles suivants :  

    - [Niveaux de données de diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels)  

    - [Bureau confidentialité Analytique](/sccm/desktop-analytics/privacy)  

- La connectivité réseau à partir d’appareils vers le cloud public Microsoft. Pour plus d’informations, consultez [comment activer le partage de données](/sccm/desktop-analytics/enable-data-sharing)  


### <a name="licensing"></a>Licences

La plupart des fonctionnalités de bureau Analytique ne nécessitent pas des licences supplémentaires ou des abonnements. Lorsqu’est correctement configuré, utilisation d’Analytique de bureau n’aucun frais Azure. 

Pour accéder aux informations de contrôle d’intégrité de Windows ou exporter des données, il existe des exigences de licence supplémentaires. Si vous n’avez pas un des abonnements suivants, vous pouvez toujours configurer et utiliser l’Analytique de bureau, mais vous ne sont pas autorisés à utiliser les informations de contrôle d’intégrité de Windows ou pour exporter des données :

- Windows 10 entreprise ou Windows 10 éducation : par périphérique avec Software Assurance actif  

- Windows 10 entreprise E3 ou E5 : abonnement par périphérique ou par utilisateur (inclus avec Microsoft 365 F1, E3 ou E5)  

- Windows 10 éducation A3 ou A5 (inclus avec Microsoft 365 éducation A3 ou A5)  

- Windows Virtual Desktop Access E3 ou E5 : par périphérique de l’abonnement par utilisateur  

> [!Note]  
> Pour les licences par périphérique, vous n’êtes pas obligé d’activer chaque périphérique avec une licence. Vous devez simplement suffisamment de licences pour les appareils inscrits dans Analytique de bureau.  


<!-- 
## Top task
> *Optional*  
> *An effective way to structure your overview article is to create an H2 for the top customer tasks and describe how the product/service helps customers with that task.*  
> *Create a new H2 for each task you list.*  
 -->



## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel fournit des instructions détaillées pour bien démarrer avec Desktop Analytique et de Configuration Manager :  

- [Déployer Office 365 pour un pilote](/sccm/desktop-analytics/tutorial-office-365)  

<!-- for future
- [Deploy Windows 10 to a pilot](/sccm/desktop-analytics/tutorial-windows)  
-->
