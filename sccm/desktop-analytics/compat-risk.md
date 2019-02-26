---
title: Risque pour la compatibilité des applications Windows
titleSuffix: Configuration Manager
description: Découvrez les risques de compatibilité pour les applications Windows dans Analytique de bureau.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8deaa8eef49b2d4792146cb47ecdf094eaed4eac
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754868"
---
# <a name="compatibility-risk-for-windows-apps-in-desktop-analytics"></a>Risque de compatibilité pour les applications Windows dans Desktop Analytique 

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Évaluations de la mise à niveau dans Analytique de Windows ont été génériques, par exemple : Faites attention ou le correctif n’est disponible. Il ne fournit pas un indicateur visuel sur la façon de hiérarchiser les applications avec des problèmes ou de mettre à niveau des insights. Postes de travail Analytique remplace cette fonctionnalité avec **risque de compatibilité**. Postes de travail Analytique montre l’évaluation des risques pour les applications application uniquement dans la vue de déploiement pour un scénario de pré-mise à niveau. Les applications basées sur les insights que Microsoft obtient à partir des ordinateurs inclus dans un plan de déploiement en cours sont classés.

Analytique de postes de travail utilise les catégories de risques de compatibilité suivantes :

- **Faible** : Le service a trouvé aucun signaux pour cette application de mettre en danger pour un Windows mise à niveau. Il est sans doute sur le système d’exploitation cible en tant que-est.  

- **Support**: Analytique indique que l’application peut altérée fonctionnalité, bien que la mise à jour est probablement possible.  

- **Haute**: L’application est presque certaine Échec pendant ou après la mise à niveau. Elle peut avoir besoin d’une mise à jour.  

- **Inconnu** : L’application n’a pas été évaluée par l’analyseur d’intégrité application. Il n’existe aucune autre information comme *problèmes connus de MS* ou *prêt pour Windows*.  



## <a name="risk-assessment-engine"></a>Moteur d’évaluation des risques

Il existe plusieurs sources de l’analyseur d’intégrité application utilise pour générer le niveau de risque.

![Diagramme des zones de moteur de l’analyseur d’intégrité application risque évaluation](media/aha-risk-assessment-engine.png)


### <a name="ms-known-issues"></a>Problèmes connus de MS

L’analyseur d’intégrité application examine la base de données de compatibilité application Microsoft pour les problèmes connus. Elle utilise cette base de données pour déterminer les blocs de compatibilité existants pour les applications accessibles à partir de Microsoft ou d’autres éditeurs. Cette vérification s’applique uniquement à la cible du système d’exploitation pour le plan de déploiement que vous sélectionnez.


### <a name="ready-for-windows"></a>Prêt pour Windows

La banque de données prêt pour Windows vérifie les blocs de compatibilité sur un appareil. Il met également en corrélation les données à partir d’autres clients ayant des applications similaires. Microsoft utilise les données à partir d’autres appareils similaires où cette application a signalé aucun problème. 


### <a name="app-health-analyzer-signals-for-compatibility-assessment"></a>Analyseur d’intégrité application signale pour l’évaluation de compatibilité

Utiliser le Kit de ressources de l’analyseur d’intégrité application pour collecter les signaux supplémentaires pour la compatibilité des applications. Pour plus d’informations, consultez [analyseur d’intégrité application](/sccm/desktop-analytics/app-health-analyzer). 

Les signaux suivants sont actuellement disponibles :

#### <a name="adopted-version-available"></a>Version adoptée disponible
Il existe une autre version de cette application est hautement adoptée par d’autres clients. Ce signal utilise des données à partir de prêt pour Windows. S’il existe des bloqueurs de mise à niveau avec votre version actuelle, envisagez de déployer la version de remplacement à la place.

#### <a name="16-bit"></a>16 bits
Supprimer tous les composants de 16 bits à partir d’applications et remplacez-les par des équivalents 32 bits ou 64 bits. Pour plus d’informations, consultez [The Windows Vista et Windows Server 2008 Developer Story : Guide de compatibilité d’application](https://msdn.microsoft.com/library/aa480152.aspx). 

L’autre option consiste à activer NT Virtual DOS Machine (NTVDM) pour la prise en charge sur Windows 10.

#### <a name="requires-admin-privileges"></a>Nécessite des privilèges d’administrateur
L’application oblige l’utilisateur à avoir un accès administratif à l’appareil. Utilisez un manifeste d’application pour ces applications qui nécessitent des autorisations d’administrateur. Pour plus d’informations, consultez [créer et incorporer un manifeste d’application](https://msdn.microsoft.com/library/bb756929.aspx).
<!--Is this a better, more current link? https://docs.microsoft.com/windows/desktop/sbscs/application-manifests-->

Analytique bureau vous recommande de l’application de test pilote. Cela devrait fonctionner correctement pour le pilote, mais vous trouverez les régressions. 

#### <a name="java-dependency"></a>Dépendance de Java
De nombreuses applications Java s’appuient sur un installé séparément Java Runtime Environment (JRE). Tandis que les anciennes versions JRE peuvent continuer à travailler sur Windows 10, Oracle prend uniquement en charge les dernières versions JRE. À l’aide d’une ancienne JRE non pris en charge peut-être avoir des failles de sécurité. Vérifiez que votre application s’exécute sur les dernières versions JRE.

#### <a name="not-dpi-aware"></a>Non-PPP prenant en charge
L’application peut avoir des problèmes d’affichage avec des résolutions d’écran avancé sur Windows 10. Utilisez un manifeste d’application pour éviter tout problème avec des résolutions élevées. Pour plus d’informations, consultez [manifestes d’Application](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Analytique bureau vous recommande de l’application de test pilote. Cela devrait fonctionner correctement pour le pilote, mais vous trouverez les régressions. 

#### <a name="visual-basic-version-6-vb6"></a>Visual Basic version 6 (VB6)
Analytique bureau vous recommande de l’application de test pilote. Applications VB6 sont souvent compatibles. Si l’application retarde durant pilote en raison des dépendances supplémentaires ni de widgets, vous devez mettre à jour l’application vers Visual Basic .NET 

#### <a name="os-version-dependency"></a>Dépendance de version du système d’exploitation
Envisagez d’avoir à redévelopper l’application pour utiliser les API des programmes d’assistance de Version, ou manifeste de l’application pour cible Windows 10.

Analytique bureau vous recommande de l’application de test pilote. Cela devrait fonctionner correctement pour le pilote, mais vous trouverez les régressions. 

#### <a name="silverlight-framework"></a>Framework de Silverlight
Microsoft recommande que non basée sur un navigateur d’applications n’utilisent Silverlight. La date de fin de prise en charge pour Silverlight 5 est octobre 2021. 

Navigateurs web plus actuels ne prennent pas en charge Silverlight.

| Navigateur | Assistance |
|---------|---------|
| Google Chrome | Fin du support : Septembre 2015 |
| Firefox | Fin du support : Mars 2017 |
| Microsoft Edge | Aucun plug-in disponible |

Analytique bureau vous recommande de l’application de test pilote. Cela devrait fonctionner correctement pour le pilote, mais vous trouverez les régressions. 

#### <a name="net-framework-1011"></a>.NET framework 1.0/1.1 
Le .NET framework version 1.0 n’est pas pris en charge sur Windows 10. Version 1.1 n’est pas compatible sur Windows 10. Si l’application est d’un éditeur tiers, contactez le fournisseur pour demander une version compatible avec Windows 10. Redévelopper dans le cas contraire, l’application pour utiliser une version prise en charge de .NET.

#### <a name="net-framework-2030"></a>.NET framework 2.0/3.0 
.NET 2.0 et 3.5 infrastructures sont pris en charge sur Windows 10. Vous devrez peut-être activer la fonctionnalité de Windows. Pour plus d’informations, consultez [installer le .NET Framework 3.5 sur Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>Accès de l’interface utilisateur
Applications avec un accès de l’interface utilisateur peuvent contourner les niveaux de contrôle d’interface utilisateur pour le lecteur d’entrée à la plus élevée de privilège windows sur le bureau. Utilisez uniquement ce paramètre pour les applications de technologie d’assistance d’interface utilisateur.

Si vous n’utilisez pas des fonctionnalités d’accessibilité dans votre application, définissez l’indicateur d’accès de l’interface utilisateur dans le manifeste d’application sur false. Pour plus d’informations, consultez [créer et incorporer un manifeste d’application](https://msdn.microsoft.com/library/bb756929.aspx).

#### <a name="driver-dependency"></a>Dépendance de pilote
L’application dépend d’un pilote. Analytique bureau vous recommande de l’application de test pilote. Cela devrait fonctionner correctement pour le pilote, mais vous trouverez les régressions. Si vous rencontrez des problèmes, contactez l’éditeur pour demander une version compatible avec Windows 10.



## <a name="app-confidence-simulation-for-a-sample-population"></a>Simulation de confiance d’application pour un échantillon de remplissage

Les graphiques suivants proviennent d’une étude de cas d’exemple. Ces données met en évidence l’utilisation de l’analyseur d’intégrité application avec l’Analytique de bureau pour adopter une approche orientée données de validation de l’application. Cette approche peut contribuer à réduire le temps et les efforts de test de vos applications pendant votre mise à niveau Windows 10.

Ces données indiquent les métriques de niveau de confiance pour les 60 appareils avec des 899 applications, y compris les applications line-of-business.

![Avant et après des graphiques indiquant la confiance de l’application](media/aha-app-confidence-simulation.png)
