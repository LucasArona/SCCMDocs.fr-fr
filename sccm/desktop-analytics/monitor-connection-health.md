---
title: Surveiller l’intégrité de la connexion
titleSuffix: Configuration Manager
description: Détails sur la façon de surveiller les États d’intégrité et de périphérique de connexion pour l’Analytique de bureau dans le Gestionnaire de Configuration.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1f4e26f7-42f2-40c8-80cf-efd405349c6c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 87126ce9de60919299c27bc84e0603b9bb24fdf0
ms.sourcegitcommit: 9d186b8b9ff652d5ea8a5d352f3f793f11db66f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/25/2019
ms.locfileid: "67352065"
---
# <a name="monitor-connection-health"></a>Surveiller l’intégrité de la connexion

Utilisez le **intégrité de la connexion** tableau de bord dans le Gestionnaire de Configuration pour explorer des catégories par intégrité de l’appareil. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Desktop Analytique maintenance** nœud, puis sélectionnez le **intégrité de la connexion** tableau de bord.  

![Capture d’écran du tableau de bord d’intégrité de connexion de Configuration Manager](media/connection-health-dashboard.png)

Lorsque vous configurez tout d’abord Analytique de bureau, ces graphiques peuvent affichent pas de données complètes. Il peut prendre 2 à 3 jours pour les périphériques actifs envoyer des données de diagnostic à l’Analytique de bureau, le service pour traiter les données et ensuite synchroniser avec votre site Configuration Manager.<!-- 4098037 -->


## <a name="connection-details"></a>Détails de connexion

Cette vignette affiche les informations de base suivantes sur la connexion à partir du Gestionnaire de Configuration pour l’Analytique de bureau :

- **Nom du locataire**: Le nom de la connexion de bureau Analytique dans le **Azure Services** nœud

- **Regroupement cible** : Le même *regroupement cible* vous avez spécifié lors de la connexion de Configuration Manager pour l’Analytique de bureau. Cette collection inclut tous les appareils Configuration Manager configure avec votre ID commercial et les paramètres de données de diagnostic. Il est l’ensemble des appareils Configuration Manager se connecte au service d’Analytique de bureau.

- **Appareils ciblés**: Tous les appareils du regroupement cible, moins les types d’appareils suivants :

    - Mise hors service
    - Obsolète
    - inactif
    - non managé

    Pour plus d’informations sur ces États de l’appareil, consultez [sur l’état du client](/sccm/core/clients/manage/monitor-clients#bkmk_about).

    > [!Note]  
    > Configuration Manager télécharge dans Desktop Analytique tous les appareils du regroupement cible moins les clients retirés et obsolètes.

- **Appareils éligibles pour DA**: Le nombre d’appareils ciblés moins les appareils qui ne sont pas éligibles pour l’Analytique de bureau. Par exemple, les appareils du regroupement cible qui s’exécutent de canal maintenance à long terme (LTSC) de Windows Server ou Windows 10.


## <a name="last-sync-details"></a>Détails de la dernière synchronisation

Cette vignette indique lorsque Configuration Manager se synchronise avec le service de cloud d’Analytique de bureau et combien d’appareils qu’il se synchronise.

- **Appareils synchronisés**: Le nombre d’appareils uniques qui le Gestionnaire de Configuration envoyé à l’Analytique de bureau. Le service inclut ces appareils dans l’instantané actuellement visible.

- **Dernière synchronisation de service**: Identique à la **dernière mise à jour** temps dans le portail d’Analytique de bureau.

- **Côté service synchronisation**: Lorsque vous pouvez vous attendre le prochain instantané quotidien dans Analytique de bureau.

> [!Note]  
> Aucune de ces valeurs mettre à jour automatiquement lorsque vous demandez une capture instantanée à la demande. Pour plus d’informations, consultez [latence des données](/sccm/desktop-analytics/troubleshooting#data-latency).

Si vous pensez que certains appareils ne sont pas affichées dans l’Analytique de bureau, assurez-vous que les appareils sont pris en charge par l’Analytique de bureau. Pour plus d’informations, consultez [Prérequis](/sccm/desktop-analytics/overview#prerequisites).


## <a name="connection-health"></a>Intégrité de la connexion

Le **intégrité de la connexion** graphique affiche le nombre d’appareils dans des États de fonctionnement suivants :  

- [Correctement inscrits](#properly-enrolled): L’appareil s’affiche dans l’Analytique de bureau avec un inventaire complet
- [Impossible d’inscrire](#unable-to-enroll): Il existe un problème de blocage qui empêche l’inscription d’appareils
- [Alerte de configuration](#configuration-alert): L’appareil n’apparaît pas dans l’Analytique de bureau ou s’affiche avec un inventaire incomplet. Configuration Manager a également identifié un problème avec l’inscription d’appareils.
- [L’inscription en attente](#awaiting-enrollment): Configuration Manager configuré l’appareil, mais il n’apparaît pas encore dans Desktop Analytique
- [État en attente](#status-pending): Configuration Manager consiste à toujours configurer cet appareil, ou n’a pas suffisamment de données à partir de l’appareil pour déterminer son état
- [Données manquantes](#missing-data): Configuration Manager configuré l’appareil, mais Analytique de bureau ne comporte que des données partielles

<!-- 
- [Configuration issues](#configuration-issues)  
- [Client not installed](#client-not-installed)  
- [Waiting for enrollment](#waiting-for-enrollment)  
- [Missing prerequisites](#missing-prerequisites)  
 -->

Le nombre total d’appareils dans ce graphique doit être le même que le **appareils éligibles pour DA** valeur dans la vignette détails de la connexion.

Sélectionnez la tranche dans le graphique pour afficher la liste des appareils avec cet état. Pour plus d’informations, consultez [liste des appareils](#device-list).

Sélectionnez le nom de catégorie dans la légende pour supprimer ou ajoutez-le à partir du graphique. Cette action permet d’effectuer un zoom avant du graphique afin que vous puissiez voir les tailles relatives des segments plus petits.

### <a name="properly-enrolled"></a>Inscrit correctement

L’appareil a les attributs suivants :

- Un gestionnaire de Configuration client 1902 ou version ultérieure  
- Aucune erreur de configuration  
- Postes de travail Analytique reçu des données de diagnostics complètes à partir de cet appareil au cours des 28 derniers jours  
- Analytique de postes de travail a un inventaire complet de configuration de l’appareil et les applications installées  

### <a name="unable-to-enroll"></a>Impossible d’inscrire

Configuration Manager détecte un ou plusieurs problèmes de blocage qui empêchent l’inscription de périphérique. Pour plus d’informations, consultez la liste des [propriétés dans le Gestionnaire de Configuration de l’appareil de bureau Analytique](#bkmk_config-issues).  

Par exemple, le client Configuration Manager n’est pas d’au moins la version 1902 (5.0.8790). Mettre à jour le client vers la dernière version. Envisagez d’activer la mise à niveau automatique du client pour le site Configuration Manager. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

### <a name="configuration-alert"></a>Alerte de configuration

L’appareil n’apparaît pas dans l’Analytique de bureau ou s’affiche avec un inventaire incomplet. Configuration Manager a également identifié un problème avec l’inscription d’appareils. Pour plus d’informations, consultez la liste des [propriétés dans le Gestionnaire de Configuration de l’appareil de bureau Analytique](#bkmk_config-issues).

Par exemple, l’appareil n’a pas la connectivité au service. Pour plus d’informations, consultez [connectivité de point de terminaison de diagnostic Windows](#windows-diagnostic-endpoint-connectivity).

### <a name="awaiting-enrollment"></a>Inscription en attente

Analytique de postes de travail n’a pas les données de diagnostic pour cet appareil. Ce problème peut être parce que vous avez récemment ajouté l’appareil à la collection cible et qu’il n’a pas encore envoyé des données. Cela peut également signifier l’appareil ne communique pas correctement avec le service et les dernières données de diagnostics sont plus de 28 jours.

Assurez-vous que l’appareil peut communiquer avec le service. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

### <a name="status-pending"></a>État en attente

Configuration Manager consiste à toujours configurer cet appareil, ou n’a pas suffisamment de données à partir de l’appareil pour déterminer son état.

### <a name="missing-data"></a>Données manquantes

Configuration Manager configuré avec succès l’appareil, mais l’Analytique de bureau ne peut pas créer une évaluation de la compatibilité. Il n’a pas un jeu de données complet pour la configuration de l’appareil (recensement) ou installé des applications (inventaire).

Ce problème est souvent résolu automatiquement lorsque l’appareil doit renvoyer. Si elle persiste, assurez-vous que l’appareil peut communiquer avec le service. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


## <a name="device-list"></a>Liste des appareils

Pour afficher une liste spécifique d’appareils par état, commencez par le **intégrité de la connexion** tableau de bord. Sélectionnez un des segments de la **intégrité de la connexion** vignette et afficher la liste des périphériques dans cet état. Cet affichage de périphérique personnalisés affiche les colonnes de bureau Analytique suivantes par défaut :

- Configuration de l’ID commerciale
- Mise à jour de la compatibilité minimale
- Windows les données de diagnostic participer
- Windows données commerciales participer
- Connectivité de point de terminaison de diagnostic de Windows

> [!Note]  
> Ignorer la colonne pour **connectivité de point de terminaison diagnostic Office**. Il est réservé pour les futures fonctionnalités.

Ces colonnes correspondent à la clé [conditions préalables](/sccm/desktop-analytics/overview#prerequisites) pour les appareils communiquer avec l’Analytique de bureau.

![Liste des périphériques de capture d’écran de correctement inscrits](media/sccm-device-list-properly-enrolled.png)

Sélectionnez un appareil pour afficher la liste complète des propriétés disponibles dans le volet détails. Vous pouvez également ajouter une de ces propriétés en tant que colonnes à la liste des appareils.


## <a name="bkmk_config-issues"></a> Propriétés de l’appareil

Les propriétés d’appareil Analytique de bureau suivantes sont disponibles en tant que colonnes dans la liste des appareils Configuration Manager :

- [Configuration de appraiser](#appraiser-configuration)  
- [Mise à jour de la compatibilité minimale](#minimum-compatibility-update)  
- [Version de appraiser](#appraiser-version)  
- [Dernière exécution complète de Appraiser](#last-successful-full-run-of-appraiser)  
- [Collecte des données appraiser](#appraiser-data-collection)  
- [Dernière exécution complète de recensement](#last-successful-full-run-of-census)  
- [Collecte de données de recensement](#census-data-collection)  
- [Connectivité de point de terminaison de diagnostic de Windows](#windows-diagnostic-endpoint-connectivity)  
- [Vérifier les données de diagnostic de l’utilisateur final](#check-end-user-diagnostic-data)  
- [Vérifier le proxy de l’utilisateur](#check-user-proxy)  
- [Configuration de l’ID commerciale](#commercial-id-configuration)  
- [Windows données commerciales participer](#windows-commercial-data-opt-in)  
- [Vérifiez le nom de l’appareil dans les données de diagnostic](#check-device-name-in-diagnostic-data)  
- [Configuration du service DiagTrack](#diagtrack-service-configuration)  
- [Version de DiagTrack](#diagtrack-version)  
- [Récupération de l’ID SQM](#sqm-id-retrieval)  
- [Récupération d’identificateur unique de l’appareil](#unique-device-identifier-retrieval)  
- [Windows les données de diagnostic participer](#windows-diagnostic-data-opt-in)  

> [!Note]  
> Ignorer les propriétés de **connectivité de point de terminaison diagnostic Office** et **Office données de diagnostic participer**. Ils sont réservés pour les futures fonctionnalités.

Le **les plus fréquents des blocages d’inscription et les alertes de configuration** vignette du tableau de bord d’intégrité de connexion affiche les propriétés qui recueillent des appareils plus souvent comme un problème.

### <a name="appraiser-configuration"></a>Configuration de appraiser

<!--20,21-->
Appraiser est le composant de Windows qui correspond à la [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#update-devices). Il évalue les applications et les pilotes sur l’appareil pour la compatibilité avec la dernière version de Windows. 

Si cette vérification est réussie, le composant appraiser est correctement configuré sur l’appareil.

Sinon, il peut afficher les erreurs suivantes :

- Impossible de configurer la collecte de données de compatibilité appareil application (SetRequestAllAppraiserVersions). Consultez les journaux pour les détails d’exception  

- Impossible de configurer la collecte de données de compatibilité appareil application (SetRequestAllAppraiserVersions). Consultez les journaux pour les détails d’exception  

- Impossible d’écrire les RequestAllAppraiserVersions à la clé de Registre `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Vérifiez les autorisations  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir.  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

### <a name="minimum-compatibility-update"></a>Mise à jour de la compatibilité minimale

<!--18,19,32-->
La mise à jour de compatibilité (appraiser.dll) n’est pas installé ou obsolètes sur l’appareil. Elle est antérieure à la configuration minimale requise pour l’Analytique de bureau, 10.0.17763.

Installez la dernière mise à jour de compatibilité. Pour plus d’informations, consultez [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

### <a name="appraiser-version"></a>Version de appraiser

Cette propriété affiche la version actuelle du composant Appraiser sur l’appareil. Il affiche la version du fichier sur `%windir%\System32\appraiser.dll`, sans la décimale. Par exemple, la version du fichier 10.0.17763 affiche sous la forme de 10017763.

### <a name="last-successful-full-run-of-appraiser"></a>Dernière exécution complète de Appraiser

Cette propriété affiche la date et l’heure auxquelles l’appareil dernière exécuté avec succès Appraiser.

### <a name="appraiser-data-collection"></a>Collecte des données appraiser

<!--Appraiser run status-->
<!--22,33-->
Cette propriété indique le dernier résultat à partir de Windows qui exécute le composant appraiser.

Si ce n’est pas le cas, réussite, il peut afficher les erreurs suivantes :

- Impossible de collecter les données de compatibilité d’application (RunAppraiser). Vérifiez les journaux pour plus d’informations  

- Collecte de données de compatibilité des applications (CompatTelRunner.exe) s’est terminée avec un code d’erreur  

Pour plus d’informations, consultez M365AHandler.log sur le client.

Recherchez le fichier suivant : `%windir%\System32\CompatTelRunner.exe`. S’il n’existe pas, réinstallez requis [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assurez-vous que la suppression d’aucun autre composant du système de ce fichier, tels que la stratégie de groupe ou un service logiciel anti-programme malveillant.

Si le fichier M365AHandler.log sur le client inclut l’une des erreurs suivantes :
```
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005
RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005
```

Pour aider à corriger ces erreurs, exécutez les commandes suivantes à partir d’une console Windows PowerShell avec élévation de privilèges sur le client concerné :

```PowerShell
# stop associated services
Stop-Service -Name diagtrack #Connected User Experiences and Telemetry
Stop-Service -Name pcasvc #Program Compatibility Assistant Service
Stop-Service -Name dps #Diagnostic Policy Service

# regenerate diagnostic data cache
Remove-Item -Path $Env:WinDir\appcompat\programs\amcache.hve
Remove-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name AmiHivePermissionsCorrect -Force

# set ASL logging level to output log files in %windir%\temp
New-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows NT\CurrentVersion\AppCompatFlags" -Name LogFlags -Value 4 -PropertyType DWord -Force

# restart services
Start-Service -Name diagtrack
Start-Service -Name pcasvc
Start-Service -Name dps
```

### <a name="last-successful-full-run-of-census"></a>Dernière exécution complète de recensement

Cette propriété affiche la date et l’heure auxquelles l’appareil dernière exécution réussie de recensement.

### <a name="census-data-collection"></a>Collecte de données de recensement

<!-- Census run status -->
<!--51,52-->
Recensement est le composant de Windows qui inventorie le périphérique. Ces données d’inventaire sont utilisées pour comprendre l’appareil et sa configuration.

Cette propriété indique le dernier résultat à partir de Windows qui exécute le composant de recensement.

Si ce n’est pas le cas, réussite, il peut afficher les erreurs suivantes :

- Impossible de collecter les données sur l’appareil et sa configuration (RunCensus). Consultez les journaux pour les détails d’exception  

- APPAREIL data collection outil de configuration et (devicecensus.exe) introuvable  

Pour plus d’informations, consultez M365AHandler.log sur le client.

Recherchez le fichier suivant : `%windir%\System32\DeviceCensus.exe`. S’il n’existe pas, réinstallez requis [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assurez-vous que la suppression d’aucun autre composant du système de ce fichier, tels que la stratégie de groupe ou un service logiciel anti-programme malveillant.

### <a name="windows-diagnostic-endpoint-connectivity"></a>Connectivité de point de terminaison de diagnostic de Windows

<!--12,15-->
Si cette vérification est réussie, l’appareil peut se connecter pour l’utilisateurs connectés et télémétrie point de terminaison (tourbillon).

Sinon, il peut afficher les erreurs suivantes :  

- Impossible de se connecter à l’utilisateur connecté expérience et les données de télémétrie point de terminaison (tourbillon). Vérifiez vos paramètres de proxy/réseau  

- Impossible de vérifier la connectivité à l’utilisateur connecté expérience et les données de télémétrie point de terminaison (CheckVortexConnectivity). Consultez les journaux pour les détails d’exception  

Appareils vérifient la connectivité avec une requête GET au point de terminaison suivant basé sur la version de système d’exploitation :

| Version du système d'exploitation | Point de terminaison |
|------------|----------|
| Windows 10, version 1803 ou version ultérieure avec la mise à jour cumulative la plus récente | `https://v10c.events.data.microsoft.com/health/keepalive` |
| Windows 10, mise à jour de la version 1803 ou ultérieure sans la 2018-09 ou cumulative plus tard | `https://v10.events.data.microsoft.com/health/keepalive` |
| Windows 10, version 1709 ou une version antérieure | `https://v10.vortex-win.data.microsoft.com/health/keepalive` |
| Windows 7 ou Windows 8.1 | `https://vortex-win.data.microsoft.com/health/keepalive` |

Assurez-vous que l’appareil peut communiquer avec le service. Cette vérification valide certains mais pas tous les points de terminaison requis. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

### <a name="check-end-user-diagnostic-data"></a>Vérifier les données de diagnostic de l’utilisateur final

<!--1004-->
Si cette vérification n’est pas réussie, un utilisateur a sélectionné une inférieur données de diagnostic de Windows sur l’appareil. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

En fonction des besoins de votre entreprise, vous pouvez désactiver les choix de l’utilisateur via la stratégie de groupe. Utilisez le paramètre pour **configurer l’interface utilisateur participer paramètre télémétrie**. Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

### <a name="check-user-proxy"></a>Vérifier le proxy de l’utilisateur

<!--30,35-->
Le paramètre DisableEnterpriseAuthProxy est activé par défaut pour Windows 7. Pour les ordinateurs Windows 8.1, Configuration Manager définit le paramètre DisableEnterpriseAuthProxy sur 0 (ne pas désactivé).

Cette propriété peut afficher les erreurs suivantes :

- Authentification proxy est activé. La valeur 0 dans DisableEnterpriseAuthProxy `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Impossible de vérifier l’état du proxy d’authentification. Consultez les journaux pour les détails d’exception

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

### <a name="commercial-id-configuration"></a>Configuration de l’ID commerciale

<!--9, 11, 53-->
Microsoft utilise un ID commercial unique pour mapper les informations à partir d’appareils à votre espace de travail Analytique de bureau. Lorsque vous intégrez Configuration Manager avec l’Analytique de bureau, il interroge automatiquement le service pour ce code. Configuration Manager doit appliquer automatiquement cet ID pour les clients sur lesquels vous ciblez des paramètres de bureau Analytique.

Si cette vérification est réussie, puis l’appareil est correctement configuré avec un ID commercial.

Sinon, il peut afficher les erreurs suivantes :

- Impossible d’écrire le CommercialId à la clé de Registre `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Vérifiez les autorisations  

- Impossible de mettre à jour le CommercialId dans la clé de Registre `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`. Consultez les journaux pour les détails d’exception  

- Indiquez la valeur correcte de CommercialId à `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Il existe un ID différent pour l’appareil. Cette clé de Registre est utilisée par la stratégie de groupe. Il est prioritaire sur l’ID fourni par le Gestionnaire de Configuration.  

<a name="bkmk_ViewCommercialID"></a> Pour afficher l’ID commercial dans le portail d’Analytique de bureau, utilisez la procédure suivante :

1. Accédez au portail d’Analytique de bureau, puis sélectionnez **services connectés** dans le groupe de paramètres globaux.  

2. Dans le **services connectés** volet, le **inscrire des appareils** volet est sélectionné par défaut. Dans le volet appareils inscription, la section informations affiche votre clé d’ID Commercial.  

![Capture d’écran de l’ID commercial dans le portail d’Analytique de bureau](media/commercial-id.png)

> [!Important]  
> Uniquement **Get nouvelle clé d’ID** lorsque vous ne pouvez pas utiliser l’objet actuel. Si vous régénérez l’ID commercial, [réinscrire vos appareils avec le nouvel Id](/sccm/desktop-analytics/enroll-devices#device-enrollment). Ce processus peut provoquer une perte de données de diagnostic pendant la transition.  

### <a name="windows-commercial-data-opt-in"></a>Windows données commerciales participer

<!--64-->
Cette propriété est spécifique aux appareils exécutant Windows 7 ou Windows 8.1. Il s’exécute des tests similaires en tant que [Windows données de diagnostic participer](#windows-diagnostic-data-opt-in), sauf pour l’et les valeurs.

### <a name="check-device-name-in-diagnostic-data"></a>Vérifiez le nom de l’appareil dans les données de diagnostic

<!--56,58-->
Si cette vérification est réussie, l’appareil est correctement configuré pour partager le nom du périphérique.

Sinon, il peut afficher les erreurs suivantes :

- Ne peut pas vérifier le nom de l’appareil à envoyer à Microsoft en tant que partie des données de diagnostic de Windows. Consultez les journaux pour les détails d’exception  

- Impossible d’écrire des AllowDeviceNameInTelemetry dans la clé de Registre `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Vérifiez les autorisations  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Assurez-vous qu’un autre mécanisme de stratégie, tels que la stratégie de groupe, n’est pas la désactivation de ce paramètre.

### <a name="diagtrack-service-configuration"></a>Configuration du service DiagTrack

<!--44,45,50-->
Si cette vérification est réussie, le composant DiagTrack est correctement configuré sur l’appareil. La version minimale requise par bureau Analytique est 10010586 (10.0.10586).

Sinon, il peut afficher les erreurs suivantes :

- Connecté l’expérience utilisateur et composant de télémétrie (diagtrack.dll) est obsolète. Vérifier la configuration requise  

- Impossible de trouver les expériences des utilisateurs connectés et un composant de télémétrie (diagtrack.dll). Vérifier la configuration requise  

- Activer et démarrer le service expériences des utilisateurs connectés et télémétrie pour envoyer des données à Microsoft  

<!--
 - An updated Connected User Experience and Telemetry (diagtrack.dll) component is available. Check requirements - this is for the newer version that improves performance
 -->

<!--include something about diagtrack perf update https://go.microsoft.com/fwlink/?linkid=2011593-->

Installez les dernières mises à jour. Pour plus d’informations, consultez [mises à jour de l’appareil](/sccm/desktop-analytics/enroll-devices#update-devices).

Assurez-vous que le **expériences des utilisateurs connectés et télémétrie** service sur l’appareil est en cours d’exécution.

### <a name="diagtrack-version"></a>Version de DiagTrack

Cette propriété affiche la version actuelle du composant expériences des utilisateurs connectés et télémétrie sur l’appareil. Il affiche la version du fichier sur `%windir%\System32\diagtrack.dll`, sans la décimale. Par exemple, la version du fichier 10.0.10586 affiche sous la forme de 10010586.

### <a name="sqm-id-retrieval"></a>Récupération de l’ID SQM

<!--38-->
Cette propriété est principalement destinée aux appareils de Windows 7. Il peut servir par les dernières versions de système d’exploitation comme un identificateur de secours pour l’appareil.

Si ce n’est pas le cas, réussite, il peut afficher l’erreur suivante :

- Impossible de récupérer l’identificateur de télémétrie d’appareils d’ancienne génération (SQM ID)

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Assurez-vous que vous n’avez pas des ID dupliqués dans votre environnement. Par exemple, si les appareils ont été déployées avec une image de système d’exploitation qui n’a pas été généralisée.

### <a name="unique-device-identifier-retrieval"></a>Récupération d’identificateur unique de l’appareil

<!--54-->
Analytique de postes de travail utilise le service de Account Microsoft pour une identité d’appareil plus fiable.

Assurez-vous que le **Microsoft compte Assistant de connexion** service n’est pas désactivé. Le type de démarrage doit être **manuel (début du déclencheur)** .

Pour désactiver l’accès de compte Microsoft de l’utilisateur final, utilisez les paramètres de stratégie au lieu de bloquer ce point de terminaison. Pour plus d’informations, consultez [compte Microsoft dans l’entreprise](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

### <a name="windows-diagnostic-data-opt-in"></a>Windows les données de diagnostic participer

<!--8,40,55,62-->
Cette propriété vérifie que Windows est correctement configuré pour autoriser les données de diagnostic. Il vérifie la valeur de AllowTelemetry dans les clés de Registre suivantes :

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Vérifiez les autorisations sur ces clés de Registre. Assurez-vous que le compte système local permettre accéder à ces clés pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Pour plus d’informations, consultez M365AHandler.log sur le client.  



## <a name="see-also"></a>Voir aussi

[Résoudre les problèmes de postes de travail Analytique](/sccm/desktop-analytics/troubleshooting)