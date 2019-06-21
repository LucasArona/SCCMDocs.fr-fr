---
title: Surveiller les clients avec Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics regroupe un ensemble de solutions qui vous permettent d’obtenir des insights importants sur l’état actuel de votre environnement.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7836e1779acbfdfbb66d6eac57bc7797abd52563
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67286477"
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Utiliser Windows Analytics avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://docs.microsoft.com/windows/deployment/update/windows-analytics-overview) est un ensemble de solutions qui vous permettent d’obtenir des insights sur l’état actuel de votre environnement. Les appareils Windows dans votre environnement envoient des données à Microsoft. Vous pouvez accéder à ces données et les analyser par le biais de ces solutions. Par exemple, connectez [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness) à Configuration Manager pour accéder directement aux données dans l’espace de travail **Surveillance** de la console Configuration Manager.

Les données utilisées par Windows Analytics ne sont pas transférées directement au serveur de site Configuration Manager. Les ordinateurs clients envoient des données au service cloud Windows. Ce service transfère ensuite les données pertinentes aux solutions Windows Analytics hébergées dans l’un des espaces de travail de votre organisation. Configuration Manager vous dirige ensuite vers les données pertinentes dans le portail web avec des liens en contexte. Il peut également afficher directement les données faisant partie de solutions que vous connectez à Configuration Manager.

> [!Important]  
> Configuration Manager envoie des données d’utilisation et de diagnostics à Microsoft. Ces données sont séparées des données Windows Analytics. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  



## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurer les clients pour envoyer des données à Windows Analytics

Pour que les appareils clients puissent envoyer des données à Windows Analytics, configurez-les avec une *clé d’ID commercial*. Cette clé correspond à l’espace de travail Azure Log Analytics qui héberge vos données Windows Analytics. Configurez également les appareils pour qu’ils envoient les données à un niveau approprié pour les solutions que vous souhaitez utiliser. 

### <a name="configure-windows-analytics-client-settings"></a>Configurer les paramètres client Windows Analytics
Pour configurer Windows Analytics : 
1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Paramètres client**.  
2. Dans le ruban, sélectionnez **Créer les paramètres client d’un appareil personnalisé**.  
3. Ajoutez le groupe **Windows Analytics** à cette stratégie de paramètres client d’appareil personnalisé.  

Pour plus d’informations sur la création de paramètres client d’appareil personnalisé, consultez [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).

Sélectionnez l’onglet des paramètres **Windows Analytics**, puis configurez les paramètres suivants :  

#### <a name="manage-windows-telemetry-settings-with-configuration-manager"></a>Gérer les paramètres de télémétrie Windows avec Configuration Manager
Configurez ce paramètre sur **Oui** pour configurer les paramètres de données de diagnostic Windows sur les clients Windows.   

#### <a name="commercial-id-key"></a>Clé d’ID commercial
La clé d’ID commercial mappe les informations des appareils que vous gérez à l’espace de travail Log Analytics qui héberge les données Windows Analytics de votre organisation. Si vous avez déjà configuré une clé d’ID commercial avec Upgrade Readiness, utilisez cet ID. Si vous ne disposez pas encore d’une clé d’ID commercial, consultez [Copier votre clé d’ID commercial](https://docs.microsoft.com/windows/deployment/update/windows-analytics-get-started#copy-your-commercial-id-key).

#### <a name="windows-10-telemetry"></a>Télémétrie Windows 10
Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#diagnostic-data-levels).

> [!Note]  
> Vous pouvez également définir la collecte de données dans Windows 10 sur le niveau **Avancé (limité)** . Ce paramètre vous permet d’obtenir un insight actionnable sur les appareils de votre environnement sans que ces derniers aient à envoyer toutes les données au niveau **Avancé** avec Windows 10 version 1709 ou ultérieure. Le niveau Avancé (limité) inclut les mesures du niveau De base, ainsi qu’une partie des données collectées au niveau Avancé et pertinentes pour Windows Analytics.

#### <a name="windows-81-and-earlier-telemetry"></a>Télémétrie pour Windows 8.1 et versions antérieures   
Pour plus d’informations, consultez [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Champs et événements de télémétrie d’évaluateur Windows 7, Windows 8 et Windows 8.1).

#### <a name="enable-windows-81-and-earlier-internet-explorer-data-collection"></a>Activer la collecte de données Internet Explorer sur Windows 8.1 et versions antérieures
Sur les appareils exécutant Windows 8.1 ou une version antérieure, Internet Explorer peut collecter des données sur les applications web. Ces données permettent à Upgrade Readiness de détecter les incompatibilités d’application web qui risquent d’entraver la mise à niveau vers Windows 10. Activez la collecte de données Internet Explorer en fonction de la zone Internet. Pour plus d’informations sur les zones internet, consultez [À propos des zones de sécurité des URL](https://docs.microsoft.com/previous-versions/windows/internet-explorer/ie-developer/platform-apis/ms537183\(v=vs.85\)).



## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Utiliser Upgrade Readiness pour identifier les problèmes de compatibilité avec Windows 10

Upgrade Readiness vous permet d’analyser l’état de préparation des appareils et leur compatibilité avec Windows 10. Cette évaluation permet d’optimiser les mises à niveau. Après avoir connecté Configuration Manager à Upgrade Readiness, accédez directement aux données de compatibilité de mise à niveau du client dans la console Configuration Manager. Ensuite, ciblez des appareils pour la mise à niveau ou la mise à jour dans la liste d’appareils.

Pour plus d’informations sur la configuration de la solution Upgrade Readiness et la connexion à celle-ci, consultez [Upgrade Readiness](/sccm/core/clients/manage/upgrade-readiness).



## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Utiliser Windows Analytics pour identifier les écarts dans les stratégies de Protection des informations Windows

Vous pouvez configurer les appareils exécutant Windows 10 version 1703 et versions ultérieures avec une stratégie [Windows Information Protection](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP). Ces appareils envoient des données de diagnostic sur les applications qui accèdent aux données d’entreprise dans votre environnement, mais qui ne sont pas incluses dans les règles d’application de la stratégie. Les utilisateurs peuvent avoir besoin de ces applications pour rester productifs, mais la Protection des informations Windows bloque l’accès des utilisateurs. Ces informations sont utiles pour gérer vos stratégies Windows Information Protection dans Configuration Manager. 

