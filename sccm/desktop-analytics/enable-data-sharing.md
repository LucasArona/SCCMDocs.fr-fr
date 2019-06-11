---
title: Activer le partage de données
titleSuffix: Configuration Manager
description: Guide de référence pour le partage des données de diagnostic avec Analytique de bureau.
ms.date: 06/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: be680198-4cea-4378-a686-d52f382ba483
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7292fdd3cc370af314cef95a4b782616e315a0cb
ms.sourcegitcommit: 725e1bf7d3250c2b7b7be9da01135517428be7a1
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/10/2019
ms.locfileid: "66821983"
---
# <a name="enable-data-sharing-for-desktop-analytics"></a>Activer le partage de bureau Analytique des données

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Pour inscrire des appareils pour l’Analytique de bureau, dont ils ont besoin d’envoyer des données de diagnostic à Microsoft. Si votre environnement utilise un serveur proxy, utilisez ces informations pour aider à configurer le proxy.


## <a name="diagnostic-data-levels"></a>Niveaux de données de diagnostic

![Diagramme des niveaux de données de diagnostic pour bureau Analytique](media/diagnostic-data-levels.png)

Lorsque vous intégrez Configuration Manager avec l’Analytique de bureau, vous également l’utiliser pour gérer le niveau de données de diagnostic sur les appareils. Pour une expérience optimale, utilisez le Gestionnaire de Configuration.

Les fonctionnalités de base du bureau Analytique fonctionnent à la **base** au niveau de données de diagnostic. Vous n’obtiendrez pas l’utilisation ou l’intégrité des données pour vos appareils mis à jour sans activer le **avancé (limité)** niveau. Microsoft recommande d’activer la **avancé (limité)** au niveau de données de diagnostic. Pour plus d’informations, consultez [Windows 10 amélioré des événements de données de diagnostic et les champs utilisés par Windows Analytique](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)).

Pour plus d’informations, consultez [confidentialité d’Analytique de bureau](/sccm/desktop-analytics/privacy).

Les articles suivants sont également des ressources utiles pour mieux comprendre les niveaux de données de diagnostic de Windows :

- [Windows 10 et le RGPD pour les décideurs informatiques](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurer les données de diagnostic Windows de votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

> [!Note]  
> Au niveau avancé (limité), lorsque chaque client effectue l’analyse initiale complète, il envoie environ 2 Mo de données dans le cloud de Microsoft. Le delta quotidiens varie entre Ko de 250 à 400 par jour.
>
> L’analyse quotidienne delta se produit à 3 h 00 (heure locale de l’appareil). Certains événements sont envoyés à la première fois disponible pendant la journée. Ces heures ne sont pas configurables.
>
> Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://aka.ms/enterprisetelemetry).  



## <a name="endpoints"></a>Points de terminaison

Pour activer le partage de données, configurez votre serveur proxy pour autoriser les points de terminaison suivants :

> [!Important]  
> Pour la confidentialité et l’intégrité des données, Windows recherche un certificat SSL de Microsoft lors de la communication avec les points de terminaison de données de diagnostic. Inspection et l’interception SSL ne sont pas possibles. Pour utiliser l’Analytique de bureau, excluez ces points de terminaison de l’inspection SSL.<!-- BUG 4647542 -->

| Point de terminaison  | Fonction  |
|-----------|-----------|
| `https://v10c.events.data.microsoft.com` | Expérience de l’utilisateur connecté et le point de terminaison de composant de diagnostic. Utilisé par les appareils exécutant Windows 10, version 1703 ou version ultérieure, avec le cumulative 2018-09 mettre à jour ou version ultérieure. |
| `https://v10.events.data.microsoft.com` | Expérience de l’utilisateur connecté et le point de terminaison de composant de diagnostic. Utilisé par les appareils exécutant Windows 10, version 1803 ou ultérieure, _sans_ le 2018-09 mise à jour cumulative installée. |
| `https://v10.vortex-win.data.microsoft.com` | Expérience de l’utilisateur connecté et le point de terminaison de composant de diagnostic. Utilisé par les appareils exécutant Windows 10, version 1709 ou une version antérieure. |
| `https://vortex-win.data.microsoft.com` | Expérience de l’utilisateur connecté et le point de terminaison de composant de diagnostic. Utilisé par les appareils exécutant Windows 7 et Windows 8.1 |
| `https://settings-win.data.microsoft.com` | Permet la mise à jour de compatibilité envoyer des données à Microsoft. |
| `http://adl.windows.com` | Permet la mise à jour de compatibilité recevoir les dernières données de compatibilité de Microsoft. |
| `https://watson.telemetry.microsoft.com` | Erreur Windows Reporting (WER). Requis pour surveiller l’intégrité du déploiement dans Windows 10, version 1803 ou une version antérieure. |
| `https://umwatsonc.events.data.microsoft.com` | Erreur Windows Reporting (WER). Obligatoire pour les rapports d’intégrité des appareils dans Windows 10, version 1809 ou version ultérieure. |
| `https://ceuswatcab01.blob.core.windows.net`<br> `https://ceuswatcab02.blob.core.windows.net`<br> `https://eaus2watcab01.blob.core.windows.net`<br> `https://eaus2watcab02.blob.core.windows.net`<br> `https://weus2watcab01.blob.core.windows.net`<br> `https://weus2watcab02.blob.core.windows.net` | Erreur Windows Reporting (WER). Requis pour surveiller l’intégrité du déploiement dans Windows 10, version 1809 ou version ultérieure. |
| `https://kmwatsonc.events.data.microsoft.com` | Analyse des incidents en ligne. Obligatoire pour les rapports d’intégrité des appareils dans Windows 10, version 1809 ou version ultérieure. |
| `https://oca.telemetry.microsoft.com`  | Analyse des incidents en ligne (OCA). Requis pour surveiller l’intégrité du déploiement dans Windows 10, version 1803 ou une version antérieure. |
| `https://login.live.com` | Requis pour fournir une identité d’appareil plus fiable pour l’Analytique de bureau. <br> <br>Pour désactiver l’accès de compte Microsoft de l’utilisateur final, utilisez les paramètres de stratégie au lieu de bloquer ce point de terminaison. Pour plus d’informations, consultez [compte Microsoft dans l’entreprise](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication). |
| `https://nexusrules.officeapps.live.com` | Pour les futures fonctionnalités <!-- Used to request dynamic diagnostic data events from Office clients. This data is useful for drill-down and diagnostics purposes in the Desktop Analytics portal --> |
| `https://nexus.officeapps.live.com` | Pour les futures fonctionnalités <!-- Used by Office clients to send diagnostic data events from Office 14, Office 15, and versions of Office 16 earlier than 16.0.8702. It's used to collect usage and reliability signals events for Desktop Analytics. --> |
| `https://office.pipe.aria.microsoft.com` | Pour les futures fonctionnalités <!-- Used by Office clients to send diagnostic data events from universal/modern Office apps, and Win32 Office 16 versions later than 16.0.8702. It's used to collect usage and reliability signals events for Desktop Analytics. --> |
| `https://graph.windows.net` | Permet de récupérer automatiquement les paramètres tels que CommercialId lors de l’attachement de votre hiérarchie pour l’Analytique de bureau (sur le rôle de serveur de Configuration Manager uniquement). |
| `https://fef.msua06.manage.microsoft.com` | Utilisé pour les appartenances aux collections de périphérique de synchronisation, des plans de déploiement et état de préparation d’appareil avec Analytique de bureau (sur le rôle de serveur de Configuration Manager uniquement). |


## <a name="proxy-server-authentication"></a>Authentification du serveur proxy

Assurez-vous qu’un proxy ne bloque pas les données de diagnostic en raison de l’authentification. Si votre organisation utilise l’authentification du serveur proxy pour le trafic sortant, utilisez une ou plusieurs des approches suivantes :

- **Contournement** (recommandé) : Configurez vos serveurs proxy pour ne pas exiger l’authentification du proxy pour le trafic vers les points de terminaison de données de diagnostic. Cette option est la solution la plus complète. Il fonctionne pour toutes les versions de Windows 10.  

- **L’authentification du proxy utilisateur**: Configurer des appareils pour utiliser le contexte de l’utilisateur connecté pour l’authentification du proxy. Cette méthode requiert les appareils pour exécuter Windows 10, version 1703 ou ultérieure. Assurez-vous que les utilisateurs ont l’autorisation de proxy pour atteindre les points de terminaison de données de diagnostic. Cette option nécessite que les appareils ont des utilisateurs de la console avec des autorisations de proxy, vous ne pouvez pas utiliser cette méthode avec les appareils sans périphérique de contrôle.  

- **L’authentification du proxy périphérique**:

    - Configurer un serveur proxy de niveau système sur les appareils.  
    - Configurez ces périphériques pour utiliser l’authentification basée sur l’appareil un proxy sortant.  
    - Configurer les serveurs proxy pour autoriser les comptes d’ordinateur accéder aux points de terminaison de données de diagnostic.  
