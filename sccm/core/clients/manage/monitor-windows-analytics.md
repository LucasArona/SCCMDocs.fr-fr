---
title: Surveiller les clients avec Windows Analytics
titleSuffix: Configuration Manager
description: Windows Analytics est un ensemble de solutions qui s’exécutent sur Operations Management Suite et qui vous permettent d’obtenir des insights utiles sur l’état actuel de votre environnement en exploitant les données de télémétrie Windows envoyées par les appareils de votre environnement.
ms.date: 01/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: CF35CE87-3BA8-4A84-9BC8-ABCEA4666212
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e792f421520798a0e000384aafcb99f31dc8eb14
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="use-windows-analytics-with-configuration-manager"></a>Utiliser Windows Analytics avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

[Windows Analytics](https://www.microsoft.com/WindowsForBusiness/windows-analytics) est un ensemble de solutions qui s’exécutent sur [Operations Management Suite](/azure/operations-management-suite/operations-management-suite-overview) (OMS). Ces solutions vous permettent d’obtenir des insights sur l’état actuel de votre environnement. Les appareils de votre environnement envoient des données de télémétrie Windows qui sont exploitées et analysées au moyen de solutions dans le [portail web Operations Management Suite](https://mms.microsoft.com). En connectant [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) à Configuration Manager, vous pouvez accéder directement aux données dans le nœud **Surveillance** de la console Configuration Manager.

Les données de télémétrie Windows utilisées par Windows Analytics ne sont pas transférées directement au serveur de site Configuration Manager. Les ordinateurs clients envoient les données de télémétrie Windows au service de télémétrie Windows. Ce service transfère ensuite les données pertinentes aux solutions Windows Analytics hébergées dans l’un des espaces de travail OMS de votre organisation. Configuration Manager peut alors soit vous diriger vers les données pertinentes dans le portail web avec des liens en contexte, soit afficher directement les données qui font partie de solutions connectées à Configuration Manager. Vous pouvez également exécuter directement des requêtes sur les données à partir du portail web Operation Management Suite.

>[!Important]
>Les [données de diagnostic et d’utilisation Configuration Manager](../../plan-design/diagnostics/diagnostics-and-usage-data.md), qui sont envoyées à Microsoft à partir du serveur de site Configuration Manager, n’ont rien à voir avec Windows Analytics et la télémétrie Windows.

## <a name="configure-clients-to-report-data-to-windows-analytics"></a>Configurer les clients pour envoyer des données à Windows Analytics

Pour que les appareils clients envoient des données à Windows Analytics, vous devez les configurer avec une clé d’ID commercial associée à l’espace de travail OMS qui héberge vos données Windows Analytics. Vous devez également configurer les appareils pour qu’ils envoient les données de télémétrie à un niveau approprié pour les solutions que vous souhaitez utiliser. 

### <a name="configure-windows-analytics-client-settings"></a>Configurer les paramètres client Windows Analytics
Pour configurer Windows Analytics, dans la console Configuration Manager, choisissez **Administration** > **Paramètres client**, double-cliquez sur **Créer des paramètres client d’appareil personnalisés par défaut**, puis cochez **Windows Analytics**.  

Accédez à l’onglet des paramètres **Windows Analytics**, puis configurez les éléments suivants :
  -  **Clé d’ID commercial**  
La clé d’ID commercial mappe les informations des appareils que vous gérez à l’espace de travail OMS qui héberge les données Windows Analytics de votre organisation. Si vous avez déjà configuré une clé d’ID commercial avec Upgrade Readiness, utilisez cet ID. Si vous ne disposez pas encore d’une clé ID commercial, consultez [Générer une clé d’ID commercial]( https://technet.microsoft.com/itpro/windows/deploy/upgrade-readiness-get-started#generate-your-commercial-id-key).

  -  **Niveau de télémétrie pour les appareils Windows 10**   
Pour plus d’informations sur chaque niveau de télémétrie Windows 10, consultez [Configurer la télémétrie Windows dans votre organisation](https://technet.microsoft.com/itpro/windows/manage/configure-windows-telemetry-in-your-organization#telemetry-levels).

   > [!Note]
   > Avec la mise à jour 1710, vous pouvez définir la collecte de données de télémétrie dans Windows 10 sur le niveau **Avancé (limité)**. Ce paramètre vous permet d’obtenir un insight actionnable sur les périphériques de votre environnement sans que ces derniers aient à envoyer toutes les données au niveau de télémétrie **Avancé** avec Windows 10 version 1709 ou ultérieure. Le niveau de télémétrie Avancé (limité) inclut les mesures du niveau de base, ainsi qu’une partie des données collectées au niveau Avancé et pertinentes pour Windows Analytics.


  -  **Participer à la collecte de données commerciales sur les appareils Windows 7, 8 et 8.1**   
Pour plus d’informations, consultez [Windows 7, Windows 8, and Windows 8.1 appraiser telemetry events and fields](https://go.microsoft.com/fwlink/?LinkID=822965) (Champs et événements de télémétrie d’évaluateur Windows 7, Windows 8 et Windows 8.1).

  -  **Configurer la collecte de données dans Internet Explorer**  
Sur les appareils Windows 8.1 ou antérieur, la collecte de données dans Internet Explorer permet à Upgrade Readiness de détecter les incompatibilités d’application web qui risquent d’entraver la mise à niveau vers Windows 10. La collecte des données dans Internet Explorer peut être activée pour chaque zone internet. Pour plus d’informations sur les zones internet, consultez [À propos des zones de sécurité des URL](https://msdn.microsoft.com/library/ms537183(v=vs.85).aspx).

## <a name="use-upgrade-readiness-to-identify-windows-10-compatibility-issues"></a>Utiliser Upgrade Readiness pour identifier les problèmes de compatibilité avec Windows 10

Upgrade Readiness (anciennement Upgrade Analytics) vous permet d’analyser l’état de préparation des appareils et leur compatibilité avec Windows 10. Cette évaluation permet d’optimiser les mises à niveau. Après avoir connecté Configuration Manager à Upgrade Readiness, accédez directement aux données de compatibilité de mise à niveau du client dans la console Configuration Manager. Ensuite, ciblez des appareils pour la mise à niveau ou la mise à jour dans la liste d’appareils.

Pour plus d’informations sur la configuration de la solution Upgrade Readiness et la connexion à celle-ci, consultez [Upgrade Readiness](../../clients/manage/upgrade/upgrade-analytics.md).

## <a name="use-windows-analytics-to-identify-gaps-in-windows-information-protection-policies"></a>Utiliser Windows Analytics pour identifier les écarts dans les stratégies de Protection des informations Windows

Les appareils Windows 10 version 1703 et ultérieures configurés avec une stratégie [Protection des informations Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip) (WIP) envoient des données de télémétrie sur les applications qui accèdent à des données d’entreprise dans votre environnement, mais qui ne sont pas prises en compte dans les règles d’application de la stratégie WIP. Les utilisateurs peuvent avoir besoin de ces applications pour rester productifs, mais la Protection des informations Windows bloque l’accès des utilisateurs. Le fait de savoir que les utilisateurs accèdent aux données d’entreprise est utile pour la maintenance de vos stratégies de Protection des informations Windows dans Configuration Manager. 

Accédez à ces données de Protection des informations Windows à l’aide de cette [requête Operations Management Suite](https://go.microsoft.com/fwlink/?linkid=849952).