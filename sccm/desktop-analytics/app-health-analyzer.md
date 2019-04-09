---
title: Analyseur d’intégrité de l’application
titleSuffix: Configuration Manager
description: Guide pratique pour l’évaluation de la compatibilité avec l’analyseur d’intégrité application de bureau Analytique.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2af150a4-0c18-4b40-8492-c04c5d154596
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 21b4907667e055c9595b31eedf9da0ad516b5fec
ms.sourcegitcommit: 5ee9487c891c37916294bd34a10d04e398f111f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/08/2019
ms.locfileid: "59069362"
---
# <a name="how-to-assess-compatibility-with-app-health-analyzer"></a>Comment évaluer la compatibilité avec l’application Analyseur d’intégrité

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Utilisez la boîte à outils de l’analyseur d’intégrité application pour l’Analytique de bureau pour évaluer les problèmes de compatibilité des applications de bureau. Cela permet de concentrer vos efforts de validation pour les applications de bureau, y compris les applications line-of-business. L’outil fournit un niveau de risque, ainsi que des actions de réparation possibles. Il inclut également un rapport de disponibilité d’application pour vous aider à évaluer la préparation de l’application pour vos mises à niveau Windows 10.



## <a name="download"></a>Téléchargement

Télécharger les outils depuis le [Microsoft Download Center](http://download.microsoft.com/download/3/7/D/37D7E378-D805-4822-A712-4EADBF50FC08/AppHealthAnalyzer.zip)<!-- (https://www.microsoft.com/download/details.aspx?id=57276) -->. Utilisez toujours la version la plus récente.

Le téléchargement est un fichier Windows Installer (MSI). Installez le Kit de ressources de l’analyseur d’intégrité application sur l’ordinateur d’un utilisateur. Lorsque vous exécutez le Kit de ressources, un Assistant vous guide tout au long du processus de création d’un rapport de disponibilité d’application.

Le Kit de ressources inclut des exemples de scripts. Si vous avez besoin automatiser la collecte d’informations de disponibilité à partir d’appareils tout au long de votre organisation, utilisez Configuration Manager pour déployer ces scripts. Pour plus d’informations, consultez [Automation](#automation).



## <a name="how-it-works"></a>Fonctionnement

L’outil effectue une analyse statique des applications qui sont déjà installés sur un appareil. Il ne fait pas l’analyse d’un programme d’installation de l’application du package. Un utilisateur n’a pas besoin exécuter l’application. Cet outil évalue toutes les applications installées inscrits avec Windows sur l’appareil.

Analyseur d’intégrité de l’application ne nécessite pas de maintenir les programmes d’installation pour les applications héritées que vous ne gérez pas activement. Il identifie les problèmes de compatibilité avec l’application dans son état d’installation. Toutes les applications sont évaluées pour les règles de compatibilité prédéfinis. Ces signaux est des problèmes courants signalés à Microsoft lors de la mise à niveau des clients vers Windows 10. Les informations de compatibilité incluent également des actions de réparation possibles ou les correctifs. Si vous avez des applications avec des problèmes, commencez avec les actions suggérées.

> [!Important]  
> Le Kit de ressources ne prend pas en charge les fonctionnalités pour réparer ou de corriger vos applications. Si vous créez un rapport de disponibilité d’application, il fournit des idées et des conseils pour vous aider à corriger vos applications avant la mise à niveau vers Windows 10.  



## <a name="prerequisites"></a>Prérequis

Avant d’installer et à l’aide de la boîte à outils, assurez-vous que l’appareil respecte les exigences suivantes :  

- Windows 7 Service Pack 1 ou version ultérieure  

- Vous disposez des privilèges d’administrateur sur l’appareil  

- Microsoft .NET Framework 4.5.1 ou version ultérieure  

- Inscrits dans le service d’Analytique de bureau, ce qui inclut les spécifications suivantes :  

    - Dernières mises à jour. Pour plus d’informations, consultez [mettre à jour des appareils](/sccm/desktop-analytics/enroll-devices#update-devices).  

    - Niveau de données de diagnostic. Pour plus d’informations, consultez [des niveaux de données de Diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  



## <a name="analyze"></a>Analyser

1. Installez l’analyseur d’intégrité application sur l’appareil cible. Par défaut, il installe le chemin d’accès suivant : `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`  

2. Accédez à la Windows **Démarrer** menu, développez le **analyseur d’intégrité de Microsoft application** de groupe, puis ouvrez le **analyseur d’intégrité application** en tant qu’administrateur. Il peut prendre plusieurs minutes pour générer le rapport.  

    > [!Note]  
    > Si les paramètres des données de diagnostic requises ne sont pas configurés, vous verrez une erreur. Assurez-vous de que configurer correctement les paramètres requis. Pour plus d’informations, consultez [des niveaux de données de Diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

3. Lorsque le rapport de disponibilité d’application s’ouvre, il commence à évaluer des applications. Attendez que le Kit de ressources à la fin, ce qui peut prendre du temps en fonction du nombre d’applications sur l’appareil.  

![Capture d’écran de l’état de préparation d’application de l’Analyseur de contrôle d’intégrité d’application](media/app-readiness-report-evaluating.png)

Vous pouvez réduire la fenêtre et continuer avec d’autres tâches pendant que le Kit de ressources s’exécute en arrière-plan.


### <a name="app-readiness-report-features"></a>Fonctionnalités de rapport disponibilité des applications

#### <a name="get-started"></a>Bien démarrer

Cet onglet vous donne une vue d’ensemble des signaux pris en charge dans cette version actuelle. Il inclut également des actions de réparation possibles.

#### <a name="insights"></a>Insights

Cet onglet fournit une vue de toutes les applications évalué de l’outil. Il montre l’évaluation des risques et les différents signaux utilisés pour identifier les problèmes de compatibilité.

- **Signaux** menu : Filtrer ces applications par des signaux à l’aide du menu de gauche  

- **Exporter CSV**: Exporter ces informations dans un fichier de valeurs séparées par des virgules (CSV)  

- **Relancer l’analyse des applications**: Si vous installez de nouvelles applications, utilisez cette option pour réexécuter l’outil  

- **Résolution des ID**: Si l’appareil a installé des applications, mais aucune information dans le rapport, donnez à cet ID pour prendre en charge  

#### <a name="desktop-analytics"></a>Analyses du bureau

Cet onglet fournit une vue d’ensemble de la façon dont vous pouvez utiliser l’analyseur d’intégrité application pour fournir des informations de disponibilité pour les applications au sein de votre organisation.



## <a name="automation"></a>Automatisation

Pour obtenir ces informations de l’application sur de nombreux appareils, déployez la version de ligne de commande de l’analyseur d’intégrité application avec Configuration Manager. Déployer sur un petit ensemble d’appareils représentatifs au sein de votre organisation. Par exemple, utilisez votre Analytique Desktop *pilote* collection. Le même [conditions préalables](#prerequisites) appliquer pour ces appareils.

Avant de procéder à un déploiement plus large, vérifiez d’abord une exécution réussie. Assurez-vous que les données ne s’affichent dans l’Analytique de bureau.

Le Kit de ressources de l’analyseur d’intégrité application inclut un exemple de script, run_silent.cmd. Par défaut, ce script est dans le chemin d’accès suivant : `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer`. Utilisez ce script pour automatiser le processus avec Configuration Manager.


### <a name="tips"></a>Conseils

- Avant la mise à niveau vers la cible du système d’exploitation, déployez l’analyseur d’intégrité application sur tous les appareils dans votre projet pilote. Pour obtenir des informations de préparation efficace, l’exécuter au moins une fois sur le groupe pilote pour un plan de déploiement.  

- Analytique de bureau possède des fonctionnalités intégrées pour recommander des groupes de pilotes pour vos plans de déploiement. Exécutez le Kit de ressources sur tous les appareils de pilotes pour obtenir une couverture complète sur vos applications importantes.  

- Planifier l’outil à exécuter lorsqu’un utilisateur n’est pas connecté, ou lorsque vous N'utilisez pas l’appareil.  

- Configurer une planification périodique. Par exemple, exécuter tous les 30 jours. Cette planification Obtient les dernières analyses de disponibilité à partir de vos appareils pour les aider à rester à jour.  



## <a name="desktop-analytics-integration"></a>Intégration de postes de travail Analytique

La capture d’écran suivante à partir de l’Analytique de bureau affiche les détails de la version 1.15.25 ContosoApp.

- Il a un **support** l’évaluation des risques  
- Une version à adopter est disponible  
- Il a une dépendance de pilote  

![Postes de travail Analytique montrant les facteurs de risque de compatibilité d’une application](media/aha-desktop-analytics-compat-risk-factors.png)



## <a name="troubleshooting"></a>Résolution des problèmes

Cette section décrit les étapes de dépannage et les problèmes opérationnels plus courantes que vous pouvez voir avec l’analyseur d’intégrité application. Par exemple :

- Vous ne voyez pas dans l’analyseur d’intégrité application écran d’accueil  

- Il existe des applications installées sur l’appareil, mais vous ne voyez pas d’informations dans le rapport de disponibilité d’application  

- Rien ne se produit lorsque vous exécutez l’outil  

### <a name="diagnostic-data-settings"></a>Paramètres de données de diagnostic

Vérifiez les configurations pour les paramètres de données de diagnostic de Windows. Configuration Manager doit définir ces valeurs lorsque le périphérique intègre Analytique de bureau. Vous pouvez utiliser les autres méthodes telles que la stratégie de script ou un groupe comme une solution de contournement. Pour plus d’informations, consultez [des niveaux de données de Diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

### <a name="verbose-mode"></a>Mode détaillé

Exécutez l’outil en mode détaillé avec le script run_verbose.cmd. Par défaut, le script est dans le chemin d’accès suivant : `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\run_verbose.cmd`

Le mode détaillé génère des journaux supplémentaires, qui peuvent vous aider à résoudre les problèmes potentiels. Elle enregistre les journaux pour le `LogCollection` dossier dans l’emplacement d’installation. Par exemple, le chemin d’accès de collection de journal par défaut est : `C:\Program Files\Microsoft Corporation\Microsoft App Health Analyzer\LogCollection\`


## <a name="see-also"></a>Voir aussi

FastTrack Center Benefit pour Windows 10 fournit l’accès aux **Desktop App assurer**. Cet avantage est un service conçu pour résoudre les problèmes avec Windows 10 et la compatibilité des applications Office 365 ProPlus. Pour plus d’informations, consultez [Desktop App assurer](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
