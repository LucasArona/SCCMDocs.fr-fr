---
title: Outils de Configuration Manager
titleSuffix: Configuration Manager
description: Découvrez les outils qui vont vous aider à gérer et dépanner votre infrastructure Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b3324189cdf482684cc0738c51fbf336a65ee221
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500715"
---
# <a name="configuration-manager-tools"></a>Outils de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les outils de Configuration Manager comprennent des [outils basés sur le client](#client-tools) et des [outils basés sur le serveur](#server-tools). Utilisez-les pour vous aider à gérer et dépanner votre infrastructure Configuration Manager.

À compter de Configuration Manager version 1806, ces outils sont dans le dossier `CD.Latest\SMSSETUP\Tools` du serveur de site. Aucune installation supplémentaire n’est nécessaire.<!--1357145--> Utilisez ces versions des outils avec Configuration Manager version 1806 et ultérieure.

Tous les systèmes d’exploitation Windows listés comme clients pris en charge dans [Systèmes d’exploitation pris en charge pour les clients et appareils](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sont pris en charge pour être utilisés avec ces outils.

> [!Note]  
> Le [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=50012) est toujours disponible dans le Centre de téléchargement Microsoft. Pour Configuration Manager version 1806 et ultérieur, utilisez les versions des outils du dossier CD.Latest sur le serveur de site. Certains outils étaient autrefois dans le toolkit, mais pas dans la version 1806. Ces outils hérités ne sont plus pris en charge.


## <a name="client-tools"></a>Outils clients

- [CMTrace](/sccm/core/support/cmtrace) : affichez, surveillez et analysez les fichiers journaux Configuration Manager  

- [Client Spy](/sccm/core/support/clispy) : résolvez les problèmes liés à la distribution, à l’inventaire et à la mesure de la lumière

- [Outil de monitoring des déploiements](/sccm/core/support/deployment-monitoring-tool) : permet de résoudre les problèmes liés aux applications, aux mises à jour et aux déploiements de référence  

- [Policy Spy](/sccm/core/support/policy-spy) : permet d’afficher les affectations de stratégies  

- [Outil Power Viewer](/sccm/core/support/power-viewer-tool) : permet d’afficher l’état de la fonctionnalité de gestion de l’alimentation  

- [Outil Envoyer un plan](/sccm/core/support/send-schedule-tool) : déclenchez des planifications et des évaluations des bases de référence de configuration  

> [!Note]  
> Le dossier ClientTools inclut aussi le fichier Microsoft.Diagnostics.Tracing.EventSource.dll. Plusieurs outils clients nécessitent cette bibliothèque. Vous ne pouvez pas les utiliser directement.  


## <a name="server-tools"></a>Outils de serveur

- [DP Job Queue Manager](/sccm/core/support/dp-job-manager) : permet de résoudre les problèmes relatifs aux travaux de distribution de contenu aux points de distribution  

- [Visionneuse de l’évaluation de regroupement](/sccm/core/support/ceviewer) : permet d’afficher des informations sur l’évaluation de regroupement  

- [Explorateur de la bibliothèque de contenu](/sccm/core/support/content-library-explorer) : permet d’afficher le contenu du magasin SIS (Single-Instance-Store) de la bibliothèque de contenu  

- [Transfert de la bibliothèque de contenu](/sccm/core/support/content-library-transfer) : permet de transférer la bibliothèque de contenu entre des disques  

- [Outil de propriété du contenu](/sccm/core/support/content-ownership-tool) : permet de modifier la propriété des packages orphelins. Ces packages existent dans le site sans serveur de site propriétaire.  

- [Outil d’administration et d’audit basés sur des rôles](/sccm/core/support/rbaviewer) : permet aux administrateurs d’auditer la configuration des rôles  

- [Run Meter Summarization Tool](/sccm/core/support/run-meter-summ) : exécutez la tâche de totalisation du contrôle et analysez les données de mesure de la lumière

> [!Note]  
> Le dossier ServerTools inclut également les fichiers suivants :
>
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll
>
> Plusieurs outils de serveur nécessitent ces bibliothèques. Vous ne pouvez pas les utiliser directement.  



## <a name="other-tools-and-toolkits"></a>Autres outils et kits de ressources

- [Outil de nettoyage de la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) : utilisez l’exécutable **ContentLibraryCleanup.exe** dans `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` pour supprimer le contenu orphelin d’un point de distribution.  

- [Outil de maintenance de la hiérarchie](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) : utilisez l’exécutable **Preinst.exe** dans le dossier partagé `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` sur le serveur de site pour transmettre des commandes au composant du gestionnaire de hiérarchie.  

- [Outil de réinitialisation des mises à jour](/sccm/core/servers/manage/update-reset-tool) : utilisez l’exécutable **CMUpdateReset.exe** dans `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` pour résoudre les problèmes liés au téléchargement ou à la réplication des mises à jour dans la console.  

- [Outil de connexion de service](/sccm/core/servers/manage/use-the-service-connection-tool) : utilisez l’exécutable **ServiceConnectionTool.exe** dans `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` pour garder votre site à jour lorsque votre point de connexion de service est hors connexion.  

- [Centre d’aide et de support](/sccm/core/support/support-center) : Collectez des informations à partir de clients pour faciliter l’analyse lors de la résolution de problèmes.

- [Microsoft Deployment Toolkit (MDT)](/sccm/mdt/) : Une collection d’outils, de processus et de conseils pour l’automatisation des déploiements de système d’exploitation sur bureau et serveur.

- [Éditeur de mise à jour Systems Center (SCUP)](/sccm/sum/tools/updates-publisher) : Un outil autonome pour gérer et importer des mises à jour logicielles personnalisées.

- [Extensions SCAP (Security Content Automation Protocol)](/sccm/compliance/plan-design/scap/about-scap) : Analysez et évaluez la conformité de votre environnement avec les lignes de base NIST.

- [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager) : Convertissez des packages hérités en applications.
