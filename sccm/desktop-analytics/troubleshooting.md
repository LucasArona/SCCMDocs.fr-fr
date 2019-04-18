---
title: Dépannage des postes de travail Analytique
titleSuffix: Configuration Manager
description: Détails techniques pour vous aider à résoudre les problèmes avec l’Analytique de bureau.
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0da26f1ea2b7f7c0c49377cb934e451d56889b7
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673664"
---
# <a name="troubleshooting-desktop-analytics"></a>Dépannage des postes de travail Analytique

Utilisez les détails dans cet article pour vous aider à résoudre les problèmes d’Analytique de bureau intégré à Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmer la configuration requise

Nombreux problèmes courants sont causés par les composants requis manquants. Vérifiez d’abord les configurations suivantes :

- [Conditions préalables](/sccm/desktop-analytics/overview#prerequisites)  

- [Mises à jour du composant de Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Comment activer le partage de données](/sccm/desktop-analytics/enable-data-sharing), qui couvre les rubriques suivantes :  

    - Les points de terminaison Internet auquel les clients doivent se connecter  

    - Authentification du serveur proxy  

    - Niveaux de données de diagnostic  



## <a name="monitor-connection-health"></a>Surveiller l’intégrité de la connexion

Utilisez le **intégrité de la connexion** tableau de bord dans le Gestionnaire de Configuration pour explorer des catégories par intégrité de l’appareil. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Desktop Analytique maintenance** nœud, puis sélectionnez le **intégrité de la connexion** tableau de bord.  

![Capture d’écran du tableau de bord d’intégrité de connexion de Configuration Manager](media/connection-health-dashboard.png)

Lorsque vous configurez tout d’abord Analytique de bureau, ces graphiques peuvent affichent pas de données complètes. Il peut prendre 2 à 3 jours pour les périphériques actifs envoyer des données de diagnostic à l’Analytique de bureau, le service pour traiter les données et ensuite synchroniser avec votre site Configuration Manager.<!-- 4098037 -->

Si vous pensez que certains appareils ne sont pas affichées dans l’Analytique de bureau, vérifiez tout d’abord le pourcentage de **appareils connectés**. Si elle est inférieure à 100 %, assurez-vous que les appareils sont pris en charge par l’Analytique de bureau. Pour plus d’informations, consultez [Prérequis](/sccm/desktop-analytics/overview#prerequisites).


### <a name="connection-health-states"></a>États d’intégrité de connexion

Examinez ensuite le **intégrité de la connexion** graphique. Il affiche le nombre d’appareils dans les catégories d’intégrité suivantes :  

- [Inscrit correctement](#properly-enrolled)  
- [Problèmes de configuration](#configuration-issues)  
- [Client non installé](#client-not-installed)  
- [En attente pour l’inscription](#waiting-for-enrollment)  
- [Composants requis manquants](#missing-prerequisites)  
- [Données manquantes](#missing-data)  

Sélectionnez le nom de catégorie à supprimer, ou ajoutez-le à partir du graphique. Cette action permet d’effectuer un zoom avant du graphique afin que vous puissiez voir les tailles relatives des segments plus petits.

#### <a name="properly-enrolled"></a>Inscrit correctement

L’appareil a les attributs suivants :

- Un gestionnaire de Configuration client 1810 ou version ultérieure  
- Aucune erreur de configuration  
- Postes de travail Analytique reçu des données de diagnostics complètes à partir de cet appareil au cours des 28 derniers jours  
- Analytique de postes de travail a un inventaire complet de configuration de l’appareil et les applications installées  

#### <a name="configuration-issues"></a>Problèmes de configuration

Configuration Manager détecte un ou plusieurs problèmes avec la configuration requise pour l’Analytique de bureau. Pour plus d’informations, consultez la liste des [propriétés dans le Gestionnaire de Configuration de l’appareil de bureau Analytique](#bkmk_config-issues).  

#### <a name="client-not-installed"></a>Client non installé

L’appareil est ciblé pour l’Analytique de bureau, mais n’est pas un client Configuration Manager.

Le client Configuration Manager est requis pour configurer et gérer l’appareil pour l’Analytique de bureau. Pour plus d’informations, consultez [Méthodes d’installation du client](/sccm/core/clients/deploy/plan/client-installation-methods).  

#### <a name="waiting-for-enrollment"></a>En attente pour l’inscription

Analytique de postes de travail n’a pas les données de diagnostic pour cet appareil. Ce problème peut être parce que l’appareil a été récemment ajoutée à la collection cible et n’a pas encore envoyé de données. Cela peut également signifier l’appareil ne communique pas correctement avec le service et les dernières données de diagnostics sont plus de 28 jours.

Assurez-vous que l’appareil est en mesure de communiquer avec le service. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### <a name="missing-prerequisites"></a>Composants requis manquants

Le client Configuration Manager n’est pas au moins la version 1810 (5.0.8740).

Mettre à jour le client vers la dernière version. Envisagez d’activer la mise à niveau automatique du client pour le site Configuration Manager. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  

#### <a name="missing-data"></a>Données manquantes

Analytique de bureau ne peut pas créer une évaluation de la compatibilité. Il n’a pas un jeu de données complet pour la configuration de l’appareil (recensement) ou installé des applications (inventaire).

Ce problème est souvent résolu automatiquement lorsque l’appareil doit renvoyer. Si elle persiste, assurez-vous que l’appareil est en mesure de communiquer avec le service. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  


### <a name="device-list"></a>Liste des appareils

Pour afficher une liste spécifique d’appareils par état, commencez par le **intégrité de la connexion** tableau de bord. Sélectionnez un des segments de la **intégrité de la connexion** vignette et afficher la liste des appareils de cette catégorie. Cet affichage de périphérique personnalisés affiche les colonnes de bureau Analytique suivantes par défaut :

- Configuration de l’ID commerciale
- Mise à jour de la compatibilité minimale
- Windows les données de diagnostic participer
- Windows données commerciales participer
- Connectivité de point de terminaison de diagnostic de Windows
- Connectivité de point de terminaison diagnostic Office

Ces colonnes correspondent à la clé [conditions préalables](/sccm/desktop-analytics/overview#prerequisites) pour les appareils communiquer avec l’Analytique de bureau.

![Liste des périphériques de capture d’écran de correctement inscrits](media/sccm-device-list-properly-enrolled.png)

Sélectionnez un appareil pour afficher la liste complète des propriétés disponibles dans le volet détails. Vous pouvez également ajouter une de ces propriétés en tant que colonnes à la liste des appareils.


### <a name="bkmk_config-issues"></a> Propriétés de l’appareil Analytique bureau dans Configuration Manager

Les colonnes suivantes sont disponibles dans la liste des appareils :

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
- [Connectivité de point de terminaison diagnostic Office](#office-diagnostic-endpoint-connectivity)  
- [Office données de diagnostic participer](#office-diagnostic-data-opt-in)

#### <a name="appraiser-configuration"></a>Configuration de appraiser

<!--20,21-->
Appraiser est le composant de Windows qui correspond à la [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#update-devices). Il évalue les applications et les pilotes sur l’appareil pour la compatibilité avec la dernière version de Windows. 

Si cette vérification est réussie, le composant appraiser est correctement configuré sur l’appareil.

Sinon, il peut afficher les erreurs suivantes :

- Impossible de configurer la collecte de données de compatibilité appareil application (SetRequestAllAppraiserVersions). Consultez les journaux pour les détails d’exception  

- Impossible de configurer la collecte de données de compatibilité appareil application (SetRequestAllAppraiserVersions). Consultez les journaux pour les détails d’exception  

- Impossible d’écrire les RequestAllAppraiserVersions à la clé de Registre `HKLM:\SOFTWARE\Microsoft\WindowsNT\CurrentVersion\AppCompatFlags\Appraiser`. Vérifiez les autorisations  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir.  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

#### <a name="minimum-compatibility-update"></a>Mise à jour de la compatibilité minimale

<!--18,19,32-->
La mise à jour de compatibilité (appraiser.dll) n’est pas installé ou obsolètes sur l’appareil. Elle est antérieure à la configuration minimale requise pour l’Analytique de bureau, 10.0.17763.

Installez la dernière mise à jour de compatibilité. Pour plus d’informations, consultez [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser).

#### <a name="appraiser-version"></a>Version de appraiser

Cette propriété affiche la version actuelle du composant Appraiser sur l’appareil. Il affiche la version du fichier sur `%windir%\System32\appraiser.dll`, sans la décimale. Par exemple, la version du fichier 10.0.17763 affiche sous la forme de 10017763.

#### <a name="last-successful-full-run-of-appraiser"></a>Dernière exécution complète de Appraiser

Cette propriété affiche la date et l’heure auxquelles l’appareil dernière exécuté avec succès Appraiser.

#### <a name="appraiser-data-collection"></a>Collecte des données appraiser

<!--Appraiser run status-->
<!--22,33-->
Cette propriété indique le dernier résultat à partir de Windows qui exécute le composant appraiser.

Si ce n’est pas le cas, réussite, il peut afficher les erreurs suivantes :

- Impossible de collecter les données de compatibilité d’application (RunAppraiser). Vérifiez les journaux pour plus d’informations  

- Collecte de données de compatibilité des applications (CompatTelRunner.exe) s’est terminée avec un code d’erreur  

Pour plus d’informations, consultez M365AHandler.log sur le client.

Recherchez le fichier suivant : `%windir%\System32\CompatTelRunner.exe`. S’il n’existe pas, réinstallez requis [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assurez-vous que la suppression d’aucun autre composant du système de ce fichier, tels que la stratégie de groupe ou un service logiciel anti-programme malveillant.

Si le fichier M365Handler.log sur le client inclut l’une des erreurs suivantes : `RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x800703F1`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80070005`
`RunAppraiser failed. CompatTelRunner.exe exited with last error code: 0x80080005`  

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

#### <a name="last-successful-full-run-of-census"></a>Dernière exécution complète de recensement

Cette propriété affiche la date et l’heure auxquelles l’appareil dernière exécution réussie de recensement.

#### <a name="census-data-collection"></a>Collecte de données de recensement

<!-- Census run status -->
<!--51,52-->
Recensement est le composant de Windows qui inventorie le périphérique. Ces données d’inventaire sont utilisées pour comprendre l’appareil et sa configuration.

Cette propriété indique le dernier résultat à partir de Windows qui exécute le composant de recensement.

Si ce n’est pas le cas, réussite, il peut afficher les erreurs suivantes :

- Impossible de collecter les données sur l’appareil et sa configuration (RunCensus). Consultez les journaux pour les détails d’exception  

- APPAREIL data collection outil de configuration et (devicecensus.exe) introuvable  

Pour plus d’informations, consultez M365AHandler.log sur le client.

Recherchez le fichier suivant : `%windir%\System32\DeviceCensus.exe`. S’il n’existe pas, réinstallez requis [mises à jour de compatibilité](/sccm/desktop-analytics/enroll-devices#bkmk_appraiser). Assurez-vous que la suppression d’aucun autre composant du système de ce fichier, tels que la stratégie de groupe ou un service logiciel anti-programme malveillant.

#### <a name="windows-diagnostic-endpoint-connectivity"></a>Connectivité de point de terminaison de diagnostic de Windows

<!--12,15-->
Si cette vérification est réussie, l’appareil est en mesure de se connecter à l’utilisateur connecté expérience et les données de télémétrie point de terminaison (tourbillon).

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

Assurez-vous que l’appareil est en mesure de communiquer avec le service. Cette vérification valide certains mais pas tous les points de terminaison requis. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

#### <a name="check-end-user-diagnostic-data"></a>Vérifier les données de diagnostic de l’utilisateur final

<!--1004-->
Si cette vérification n’est pas réussie, un utilisateur a sélectionné une inférieur données de diagnostic de Windows sur l’appareil. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).

En fonction des besoins de votre entreprise, vous pouvez désactiver les choix de l’utilisateur via la stratégie de groupe. Utilisez le paramètre pour **configurer l’interface utilisateur participer paramètre télémétrie**. Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#enterprise-management).

#### <a name="check-user-proxy"></a>Vérifier le proxy de l’utilisateur

<!--30,35-->
Le paramètre DisableEnterpriseAuthProxy est activé par défaut pour Windows 7. Pour les ordinateurs Windows 8.1, Configuration Manager définit le paramètre DisableEnterpriseAuthProxy sur 0 (ne pas désactivé).

Cette propriété peut afficher les erreurs suivantes :

- Authentification proxy est activé. La valeur 0 dans DisableEnterpriseAuthProxy `HKLM\Software\Policies\Microsoft\Windows\DataCollection`

- Impossible de vérifier l’état du proxy d’authentification. Consultez les journaux pour les détails d’exception

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

#### <a name="commercial-id-configuration"></a>Configuration de l’ID commerciale

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

Pour afficher l’ID commercial dans le portail d’Analytique de bureau, utilisez la procédure suivante :

1. Accédez au portail d’Analytique de bureau, puis sélectionnez **services connectés** dans le groupe de paramètres globaux.  

2. Dans le **services connectés** volet, le **inscrire des appareils** volet est sélectionné par défaut. Dans le volet appareils inscription, la section informations affiche votre clé d’ID Commercial.  

![Capture d’écran de l’ID commercial dans le portail d’Analytique de bureau](media/commercial-id.png)

> [!Important]  
> Uniquement **Get nouvelle clé d’ID** lorsque vous ne pouvez pas utiliser l’objet actuel. Si vous régénérez l’ID commercial, déployez le nouvel ID sur vos appareils. Ce processus peut provoquer une perte de données de diagnostic pendant la transition.  

#### <a name="windows-commercial-data-opt-in"></a>Windows données commerciales participer

<!--64-->
Cette propriété est spécifique aux appareils exécutant Windows 7 ou Windows 8.1. Il s’exécute des tests similaires en tant que [Windows données de diagnostic participer](#windows-diagnostic-data-opt-in), sauf pour l’et les valeurs.

#### <a name="check-device-name-in-diagnostic-data"></a>Vérifiez le nom de l’appareil dans les données de diagnostic

<!--56,58-->
Si cette vérification est réussie, l’appareil est correctement configuré pour partager le nom du périphérique.

Sinon, il peut afficher les erreurs suivantes :

- Ne peut pas vérifier le nom de l’appareil à envoyer à Microsoft en tant que partie des données de diagnostic de Windows. Consultez les journaux pour les détails d’exception  

- Impossible d’écrire des AllowDeviceNameInTelemetry dans la clé de Registre `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`. Vérifiez les autorisations  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Vérifiez les autorisations sur cette clé de Registre. Assurez-vous que le compte système local peut accéder à cette clé pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Assurez-vous qu’un autre mécanisme de stratégie, tels que la stratégie de groupe, n’est pas la désactivation de ce paramètre.

#### <a name="diagtrack-service-configuration"></a>Configuration du service DiagTrack

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

#### <a name="diagtrack-version"></a>Version de DiagTrack

Cette propriété affiche la version actuelle du composant expériences des utilisateurs connectés et télémétrie sur l’appareil. Il affiche la version du fichier sur `%windir%\System32\diagtrack.dll`, sans la décimale. Par exemple, la version du fichier 10.0.10586 affiche sous la forme de 10010586.

#### <a name="sqm-id-retrieval"></a>Récupération de l’ID SQM

<!--38-->
Cette propriété est principalement destinée aux appareils de Windows 7. Il peut servir par les dernières versions de système d’exploitation comme un identificateur de secours pour l’appareil.

Si ce n’est pas le cas, réussite, il peut afficher l’erreur suivante :

- Impossible de récupérer l’identificateur de télémétrie d’appareils d’ancienne génération (SQM ID)

Pour plus d’informations, consultez M365AHandler.log sur le client.  

Assurez-vous que vous n’avez pas des ID dupliqués dans votre environnement. Par exemple, si les appareils ont été déployées avec une image de système d’exploitation qui n’a pas été généralisée.

#### <a name="unique-device-identifier-retrieval"></a>Récupération d’identificateur unique de l’appareil

<!--54-->
Analytique de postes de travail utilise le service de Account Microsoft pour une identité d’appareil plus fiable.

Assurez-vous que le **Microsoft compte Assistant de connexion** service n’est pas désactivé. Le type de démarrage doit être **manuel (début du déclencheur)**.

Pour désactiver l’accès de compte Microsoft de l’utilisateur final, utilisez les paramètres de stratégie au lieu de bloquer ce point de terminaison. Pour plus d’informations, consultez [compte Microsoft dans l’entreprise](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts#block-all-consumer-microsoft-account-user-authentication).

#### <a name="windows-diagnostic-data-opt-in"></a>Windows les données de diagnostic participer

<!--8,40,55,62-->
Cette propriété vérifie que Windows est correctement configuré pour autoriser les données de diagnostic. Il vérifie la valeur de AllowTelemetry dans les clés de Registre suivantes :

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

Vérifiez les autorisations sur ces clés de Registre. Assurez-vous que le compte système local permettre accéder à ces clés pour le client Configuration Manager à définir. Elle peut également être due à un objet de stratégie de groupe en conflit. Pour plus d’informations, consultez [les paramètres Windows](/sccm/desktop-analytics/enroll-devices#windows-settings).  

Pour plus d’informations, consultez M365AHandler.log sur le client.  

#### <a name="office-diagnostic-endpoint-connectivity"></a>Connectivité de point de terminaison diagnostic Office

<!-- 1001,1002,1003 -->

Si cette vérification est réussie, l’appareil est en mesure de se connecter aux points de terminaison de Diagnostics Office.

Sinon, il peut afficher les erreurs suivantes :

- Impossible de se connecter au point de terminaison Office diagnostic (Aria). Vérifiez vos paramètres de proxy/réseau  

- Impossible de se connecter au point de terminaison Office diagnostic (Nexusrules). Vérifiez vos paramètres de proxy/réseau  

- Impossible de se connecter au point de terminaison Office Diagnostics (Nexus). Vérifiez vos paramètres de proxy/réseau  

Assurez-vous que l’appareil est en mesure de communiquer avec le service. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

#### <a name="office-diagnostic-data-opt-in"></a>Office données de diagnostic participer

<!-- SCCMDocs-pr 3570 -->
À compter de Configuration Manager version 1902, le comportement est modifié pour l’envoi de service d’Office et les données de diagnostic à Microsoft. Cette propriété vérifie que les paramètres de stratégie d’Office sont correctement configurés. Ces paramètres contrôlent les données minimales requises pour aider à maintenir le bureau sécurisé et à jour, et fonctionnent comme prévu sur l’appareil est installé.

Pour plus d’informations, consultez [contrôle de la vue d’ensemble de la confidentialité d’Office 365 ProPlus](https://docs.microsoft.com/DeployOffice/privacy/overview-privacy-controls). Cet article explique comment la confidentialité contrôle pour les données de diagnostic qui a collectées et envoyées à Microsoft sur les logiciels du client Office utilisé sur Windows des ordinateurs de votre organisation.

Cette vérification échoue pour les clients Configuration Manager version 1810. Mettre à jour le client vers la dernière version. Envisagez d’activer la mise à niveau automatique du client pour le site Configuration Manager. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).



## <a name="log-files"></a>Fichiers journaux

Utilisez les fichiers journaux suivants pour vous aider à résoudre les problèmes d’Analytique de bureau intégré à Configuration Manager.


### <a name="service-connection-point"></a>point de connexion de service

Les fichiers journaux suivants sont sur le point de connexion de service dans le répertoire suivant : `C:\Program Files\Configuration Manager\Logs\M365A`:

| Journal | Description |
|---------|---------|
| **M365ADeploymentPlanWorker.log** | Informations sur la synchronisation de plan de déploiement de bureau Analytique cloud service pour le Gestionnaire de Configuration local |
| **M365ADeviceHealthWorker.log** | Informations sur l’intégrité de l’appareil télécharger à partir du Gestionnaire de Configuration à Microsoft cloud |
| **M365AUploadWorker.log** | Plus d’informations sur la collecte et l’appareil charger à partir de Configuration Manager à Microsoft cloud |
| **SmsAdminUI.log** | Plus d’informations sur l’activité de la console Configuration Manager, telles que la configuration des services cloud Azure  |


### <a name="configuration-manager-client"></a>Client de Configuration Manager

Les fichiers journaux suivants sont sur le client Configuration Manager dans le répertoire suivant : `C:\Windows\CCM\logs`:

| Journal | Description |
|---------|---------|
| **M365AHandler.log** | Informations sur la stratégie de paramètres de bureau Analytique |


### <a name="enable-verbose-logging"></a>Activer la journalisation documentée

1. Sur le point de connexion, accédez à la clé de Registre suivante : `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Définir le **LogLevel** valeur `0`  
3. (Facultatif) Exécutez la commande SQL suivante sur la base de données de site :  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Redémarrez le **SMS_EXECUTIVE** service sur le serveur de site



## <a name="bkmk_AzureADApps"></a> Applications Azure AD

Analytique de postes de travail ajoute les applications suivantes à votre Azure AD :

- **Gestionnaire de configuration de Microservice**: Se connecte à Configuration Manager avec des postes de travail Analytique. Cette application n’a aucune exigence d’accès.  

- **Office 365 Client Admin**: Récupère les données à partir de votre espace de travail Analytique de journal. Cette application nécessite un accès en écriture au journal Analytique.  

- **MALogAnalyticsReader**: Récupère les groupes d’OMS et les appareils créés dans le journal Analytique. Pour plus d’informations, consultez [rôle d’application MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Si vous devez configurer ces applications après avoir effectué des, accédez à la **services connectés** volet. Sélectionnez **configurer l’accès des utilisateurs et des applications**et configurer les applications.  

- **L’application Azure AD pour Configuration Manager**. Si vous avez besoin configurer ou résoudre les problèmes de connexion après avoir effectué les, consultez [créer une application pour le Gestionnaire de Configuration](/sccm/desktop-analytics/set-up#create-app-for-configuration-manager). Cette application nécessite **écrire les données de Collection CM** et **lire les données de Collection CM** sur le **Configuration Manager Service** API.  

### <a name="bkmk_MALogAnalyticsReader"></a> Rôle d’application MALogAnalyticsReader

Lorsque vous configurez l’Analytique de bureau, vous acceptez un consentement au nom de votre organisation. Ce consentement consiste à affecter l’application MALogAnalyticsReader le rôle de lecture du journal Analytique à l’espace de travail. Ce rôle d’application est requise par l’Analytique de bureau.

S’il existe un problème avec ce processus au cours de configuration, utilisez le processus suivant pour ajouter manuellement cette autorisation :

1. Accédez à la [Azure portal](http://portal.azure.com), puis sélectionnez **toutes les ressources**. Sélectionnez l’espace de travail de type **Analytique de journal**.  

2. Dans le menu de l’espace de travail, sélectionnez **contrôle d’accès (IAM)**, puis sélectionnez **ajouter**.  

3. Dans le **ajouter des autorisations** panel, configurez les paramètres suivants :  

    - **Rôle**: **Lecture du journal Analytique**  

    - **Attribuer l’accès à**: **Azure AD utilisateur, groupe ou application**  

    - **Sélectionnez**: **MALogAnalyticsReader**  

4. Sélectionnez **Enregistrer**.

Le portail affiche une notification qu’il ajoute l’attribution de rôle.


## <a name="data-latency"></a>Latence des données

<!-- 3846531 -->
Données dans le portail d’Analytique de bureau sont actualisées quotidiennement. Cette actualisation inclut les modifications de périphérique collectées à partir de données de diagnostic et les modifications que vous apportez à la configuration. Par exemple, lorsque vous modifiez d’une ressource **décision de mettre à niveau**, cela peut entraîner des modifications à l’état de préparation des appareils avec cette ressource installée.

- **Modifications de l’administrateur** sont généralement traités par le service d’Analytique de bureau dans les neuf heures. Par exemple, si vous apportez des modifications à 11 h 00 UTC, le portail doit refléter ces modifications avant l’heure UTC de 08:00 AM le lendemain.

- **Modifications de l’appareil** détecté par UTC minuit en heure locale sont généralement incluses dans l’actualisation quotidienne. Il est généralement 23 heures supplémentaires de la latence associée au traitement des changements de périphérique par rapport aux modifications de l’administrateur.

Si vous ne voyez pas les modifications mises à jour dans ces périodes, attendez un autre de 24 heures pour la prochaine actualisation quotidienne. Si vous voyez des délais plus longs, consultez le tableau de bord service health. Si le service signale comme étant saine, contactez le support Microsoft.

Lorsque vous configurez tout d’abord Analytique de bureau, les graphiques dans Configuration Manager et le portail d’Analytique de bureau ne peuvent pas montrent complète des données. Il peut prendre 2 à 3 jours pour les périphériques actifs envoyer des données de diagnostic à l’Analytique de bureau, le service pour traiter les données et ensuite synchroniser avec votre site Configuration Manager.

Dans une hiérarchie Configuration Manager, il peut prendre 10 minutes pour les nouvelles collections à afficher pour les plans de déploiement. Les sites principaux créent les collections, et le site d’administration centrale se synchronise avec Analytique de bureau.<!-- 3896921 -->
