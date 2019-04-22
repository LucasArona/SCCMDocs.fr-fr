---
title: Inscrire des appareils dans Desktop Analytique
titleSuffix: Configuration Manager
description: Découvrez comment inscrire des appareils dans Analytique de bureau.
ms.date: 04/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: c5d5e6665b0ddd2e7726af4b8ac8929d5019fedf
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59802442"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Comment inscrire des appareils dans Desktop Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Lorsque vous [connecter Configuration Manager](/sccm/desktop-analytics/connect-configmgr) pour l’Analytique de bureau, vous configurez les paramètres pour inscrire des appareils pour l’Analytique de bureau. Vous pouvez modifier ces paramètres à tout moment. Assurez-vous également que les appareils sont à jour.



## <a name="update-devices"></a>Mettre à jour des appareils

Il existe deux types de mises à jour que vous devez appliquer pour une expérience optimale avec Analytique de bureau :

- [Mises à jour de compatibilité](#bkmk_appraiser)  
- [Expériences utilisateur et des données de télémétrie de service connecté](#bkmk_diagtrack)


### <a name="bkmk_appraiser"></a> Mises à jour de compatibilité

Le composant de compatibilité (Appraiser) exécute des diagnostics sur le périphérique de Windows pour évaluer son état de compatibilité avec les dernières versions de Windows 10.

Microsoft incrémente régulièrement les mises à jour pour ce composant, mais ne change pas le nombre de base de connaissances associé. Assurez-vous que vous avez toujours la dernière version de la mise à jour.

Redémarrer des appareils après avoir installé les mises à jour de compatibilité pour la première fois.

> [!Tip]  
> Utilisez le Gestionnaire de Configuration pour installer automatiquement la dernière version de ces mises à jour. Pour plus d’informations, consultez [Déployer des mises à jour logicielles](/sccm/sum/deploy-use/deploy-software-updates).  

> [!Note]  
> Il existe une mise à jour facultative connexe [Ko 3150513](https://catalog.update.microsoft.com/v7/site/Search.aspx?q=3150513). Cette mise à jour fournit la configuration mise à jour et les définitions pour les anciennes mises à jour de compatibilité. Pour plus d’informations, consultez [dernière mise à jour de définition compatibilité pour Windows](https://support.microsoft.com/help/3150513).  

#### <a name="windows-10"></a>Windows 10

Windows 10 inclut le composant de compatibilité. Pour obtenir la dernière mise à jour de compatibilité, installez la dernière mise à jour du cumulative de Windows 10.

#### <a name="windows-81"></a>Windows 8.1

Télécharger la mise à jour : [KB 2976978](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2976978) 

Exécute des diagnostics sur les systèmes Windows 8.1 qui participent au programme d’amélioration du produit Windows. Ces diagnostics aider à déterminer si vous rencontrez des problèmes de compatibilité lors de la mise à niveau vers Windows 10.

Pour plus d’informations, consultez [mise à jour de compatibilité pour maintenir Windows à jour dans Windows 8.1](https://support.microsoft.com/help/2976978).

#### <a name="windows-7-with-service-pack-1"></a>Windows 7 avec Service Pack 1

Télécharger la mise à jour : [KB 2952664](http://catalog.update.microsoft.com/v7/site/Search.aspx?q=KB2952664) 

Exécute des diagnostics sur le Windows 7 avec Service Pack 1 (SP1) les systèmes qui participent au programme d’amélioration du produit Windows. Ces diagnostics aider à déterminer si vous rencontrez des problèmes de compatibilité lors de la mise à niveau vers Windows 10.

Pour plus d’informations, consultez [mise à jour de compatibilité pour maintenir Windows à jour dans Windows 7](https://support.microsoft.com/help/2952664).


### <a name="bkmk_diagtrack"></a> Expériences utilisateur et des données de télémétrie de service connecté

Avec les données de diagnostic de Windows est activées, le service expériences des utilisateurs connectés et télémétrie (DiagTrack) collecte les données de système, d’applications et de pilotes. Microsoft analyse ces données et le partage avec vous par le biais de Desktop Analytique.

Pour une expérience optimale, installez les mises à jour suivantes, selon la version du système d’exploitation.

> [!Note]  
> Lorsque vous installez ces mises à jour, attendez les comportements suivants :
> 
> - Les appareils que vous inscrivez pour l’Analytique de bureau afficheront dans le service en moins d’une heure  
> - Appareils signalent rapidement l’état des mises à jour de fonctionnalité et de qualité pour Windows et Office  
>
> Sans ces mises à jour, ces processus peuvent prendre plus de 48 heures pour un appareil signaler à l’Analytique de bureau.  


#### <a name="windows-10"></a>Windows 10

Installez la dernière mise à jour du cumulative de Windows 10.

<!-- 
- Windows 10 1809: Included in RTM build
- Windows 10 1803: [KB4458469](https://support.microsoft.com/help/4458469) (OS Build 17134.319)
- Windows 10 1709: [KB4457136](https://support.microsoft.com/help/4457136) (OS Build 16299.697)
- Windows 10 1703: [KB4457141](https://support.microsoft.com/help/4457141) (OS Build 15063.1358)
- Windows 10 1607: [KB4457127](https://support.microsoft.com/help/4457127) (OS Build 14393.2517)
 -->

#### <a name="windows-81"></a>Windows 8.1

Installez le correctif cumulatif mensuel octobre 2018, [KB4462926](https://support.microsoft.com/help/4462926)

#### <a name="windows-7"></a>Windows 7

Installez le correctif cumulatif mensuel octobre 2018, [KB4462923](https://support.microsoft.com/help/4462923)



## <a name="device-enrollment"></a>Inscription de périphériques

Le service d’Analytique de bureau n’a aucun agent pour l’installer. Inscription de l’appareil nécessite la configuration des paramètres sur les appareils que vous souhaitez surveiller. Ces paramètres contrôlent à quelle instance d’Analytique de bureau, l’appareil doit envoyer ses données et autres options de configuration.

> [!Note]  
> Si vous utilisez déjà Windows Analytique, utilisez ce même espace de travail pour l’Analytique de bureau. Vous devez réinscrire les appareils pour l’Analytique de bureau que vous avez précédemment inscrit dans Windows Analytique.
>
> Vous ne pouvez avoir qu’un espace de travail Analytique de bureau par le locataire Azure AD. Appareils peuvent envoyer uniquement les données de diagnostic pour un espace de travail.  

Configuration Manager fournit une expérience intégrée pour gérer et déployer ces paramètres pour les clients. Pour une expérience optimale, utilisez le Gestionnaire de Configuration.

Lorsque vous vous connectez Configuration Manager pour l’Analytique de bureau, vous configurez les paramètres pour inscrire des appareils. Pour plus d’informations, consultez [comment connecter Configuration Manager avec Desktop Analytique](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

Pour modifier ces paramètres, utilisez la procédure suivante :

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**. Sélectionnez la connexion à l’Analytique de bureau, puis choisissez **propriétés** dans le ruban.

2. Sur le **données de Diagnostic** page, apportez les modifications nécessaires pour les paramètres suivants :  

    - **ID commercial**: vous n’avez pas besoin de modifier ou de modifier cette valeur. Pour plus d’informations sur la résolution des problèmes avec l’ID commercial, consultez [configuration d’ID Commercial](/sccm/desktop-analytics/troubleshooting#commercial-id-configuration).  

    - **Niveau de données de diagnostic de Windows 10**: Pour plus d’informations, consultez [des niveaux de données de Diagnostic](/sccm/desktop-analytics/enable-data-sharing#diagnostic-data-levels).  

    - **Autoriser le nom de l’appareil dans les données de diagnostic**: Pour plus d’informations, consultez [nom de l’appareil](#device-name).  

    Lorsque vous apportez des modifications à cette page, le **fonctionnalités disponibles** page affiche un aperçu de la fonctionnalité de bureau Analytique avec les paramètres de données de diagnostic sélectionné.  

3. Sur le **Microsoft 365 Analytique connexion** page, apportez les modifications nécessaires pour les paramètres suivants :

    - **Nom complet** : Le portail d’Analytique de bureau affiche cette connexion de Configuration Manager à l’aide de ce nom.  

    - **Regroupement cible**: Cette collection inclut tous les appareils Configuration Manager configure avec votre ID commercial et les paramètres de données de diagnostic. Il est l’ensemble des appareils Configuration Manager se connecte au service d’Analytique de bureau.  

    - **Appareils du regroupement cible utilisent un proxy authentifié par l’utilisateur pour les communications sortantes**: Par défaut, cette valeur est **non**. Si nécessaire dans votre environnement, la valeur est **Oui**. Pour plus d’informations, consultez [l’authentification du serveur Proxy](/sccm/desktop-analytics/enable-data-sharing#proxy-server-authentication).  

    - **Sélectionner des regroupements spécifiques pour se synchroniser avec le bureau Analytique**: Sélectionnez **ajouter** pour inclure des collections supplémentaires. Ces collections sont disponibles dans le portail d’Analytique de bureau pour le regroupement des plans de déploiement. Veillez à inclure les collections d’exclusion de pilote et de pilote.  

        Ces collections continuent à synchroniser en tant que leurs changements d’appartenance. Par exemple, votre plan de déploiement utilise une collection avec une règle d’adhésion de Windows 7. Comme ces appareils mise à niveau vers Windows 10 et Configuration Manager évalue l’appartenance au regroupement, ces appareils déposent hors de la collecte et le plan de déploiement.  


### <a name="windows-settings"></a>Paramètres de Windows

Configuration Manager définit les paramètres Windows suivants sous `Microsoft\Windows\DataCollection`:

| Stratégie   | Valeur  |
|----------|--------|
| **CommercialId** | Dans l’ordre pour un appareil s’affichent dans l’Analytique de bureau, configurez-le avec votre ID de Commercial. du organisation |
| **AllowTelemetry**  | Définissez `1` pour **base**, `2` pour **étendu**, ou `3` pour **complète** données de diagnostic. Analytique de postes de travail nécessite au moins de base données de diagnostic. Microsoft recommande d’utiliser le niveau avancé (limité) avec l’Analytique de bureau. Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://docs.microsoft.com/windows/configuration/configure-windows-diagnostic-data-in-your-organization). |
| **LimitEnhancedDiagnosticDataWindowsAnalytics** | *S’applique à Windows 10, version 1709 et ultérieure*: Ce paramètre s’applique uniquement lorsque le paramètre AllowTelemetry a `2`. Il limite les événements de données de diagnostic étendu envoyées à Microsoft pour que les événements requis par bureau Analytique. Pour plus d’informations, consultez [Windows 10, version 1709 amélioré des événements de données de diagnostic et les champs utilisés par Windows Analytique](https://docs.microsoft.com/windows/configuration/enhanced-diagnostic-data-windows-analytics-events-and-fields).|
| **AllowDeviceNameInTelemetry** | *S’applique à Windows 10, version 1803 et versions ultérieure*: Dans un abonnement distinct est requis pour permettre aux appareils de continuer à envoyer le nom de l’appareil.<br> <br>Remarque : Le nom de l’appareil n’est pas envoyé à Microsoft par défaut. Si vous n’envoyez pas le nom du périphérique, il apparaît dans l’Analytique de bureau comme « Inconnu ». Ce comportement peut rendre difficile d’identifier et évaluer les appareils. Pour plus d’informations, consultez [nom de l’appareil](#device-name). |
| **CommercialDataOptIn** | *S’applique à Windows 7 et Windows 8.1*: La valeur `1` est requis pour l’Analytique de bureau. Pour plus d’informations, consultez [données commerciales Opt-in dans Windows 7](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-7/ee126127\(v=ws.10\)). |

Afficher ces paramètres dans l’éditeur de stratégie de groupe à l’emplacement suivant : **Configuration de l’ordinateur** > **modèles d’administration** > **les composants Windows** > **données Collection et l’aperçu Builds**.

> [!Important]  
> Dans la plupart des cas, vous devez uniquement utiliser Configuration Manager pour configurer ces paramètres. Ne pas appliquer également ces paramètres dans des objets de stratégie de groupe de domaine. Pour plus d’informations, consultez [résolution des conflits](#conflict-resolution).<!-- SCCMDocs-pr 3120 -->

### <a name="device-name"></a>Nom de l’appareil

À compter de Windows 10, version 1803, le nom de l’appareil n’est plus collecté par défaut. Collecte le nom de l’appareil avec les données de diagnostic nécessite un distinct participer. Sans le nom de l’appareil, il est plus difficile pour vous permet d’identifier quels appareils nécessitent une attention particulière lors de l’évaluation d’une mise à niveau vers une nouvelle version de Windows ou Office.

Si vous n’envoyez pas le nom du périphérique, il apparaît dans l’Analytique de bureau comme « Inconnu ».

![Liste des appareils Analytique bureau affichant des noms « inconnus »](media/unknown-device-name.png)

Il existe une option dans les paramètres de Configuration Manager pour l’Analytique de bureau configurer cette option : **Autoriser le nom de l’appareil dans les données de diagnostic**. Ce paramètre de Configuration Manager contrôle le paramètre de stratégie Windows AllowDeviceNameInTelemetry.
 

### <a name="conflict-resolution"></a>résolution des conflits

En général, utilisez des regroupements Configuration Manager pour cibler l’inscription et les paramètres de bureau Analytique. Utiliser l’appartenance directe ou des requêtes à inclure ou exclure des appareils à partir de la collection. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](/sccm/core/clients/manage/collections/create-collections).

Configuration Manager configure uniquement les paramètres de Windows si une valeur n’existe pas déjà. Si vous avez besoin configurer différents paramètres pour un groupe unique d’appareils, vous pouvez utiliser [stratégie de groupe](#windows-settings). Paramètres ciblés par la stratégie de groupe sont prioritaires sur les paramètres de Configuration Manager.

Si vous ciblez les clients Configuration Manager avec les paramètres Windows Analytique et d’Analytique de bureau, les paramètres pour l’Analytique de bureau sont prioritaires.

Lorsque vous configurez le niveau de données de diagnostic, vous définissez la limite supérieure pour l’appareil. Par défaut dans Windows 10, version 1803 et versions ultérieure, les utilisateurs peuvent choisir de définir un niveau inférieur. Vous pouvez contrôler ce comportement en utilisant le paramètre de stratégie de groupe **configurer l’interface utilisateur participer paramètre télémétrie**. Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).



## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour créer des plans de déploiement dans l’Analytique de bureau.
> [!div class="nextstepaction"]  
> [Créer des plans de déploiement](/sccm/desktop-analytics/create-deployment-plans)  
