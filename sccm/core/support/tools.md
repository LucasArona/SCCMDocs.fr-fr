---
title: Outils de Configuration Manager
titleSuffix: Configuration Manager
description: Découvrez les outils qui vont vous aider à gérer et dépanner votre infrastructure Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 395403dc-6997-4415-93fd-6b1eeb6ba31a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd23bd523eb64f7d00f71c38c79a180c4e2e569a
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386540"
---
# <a name="configuration-manager-tools"></a>Outils de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les outils de Configuration Manager comprennent des [outils basés sur le client](#client-tools) et des [outils basés sur le serveur](#server-tools). Utilisez-les pour vous aider à gérer et dépanner votre infrastructure Configuration Manager. 

À compter de Configuration Manager version 1806, ces outils sont dans le dossier `CD.Latest\SMSSETUP\Tools` du serveur de site. Aucune installation supplémentaire n’est nécessaire.<!--1357145--> Utilisez ces versions des outils avec Configuration Manager version 1806 et ultérieure.

Tous les systèmes d’exploitation Windows listés comme clients pris en charge dans [Systèmes d’exploitation pris en charge pour les clients et appareils](https://docs.microsoft.com/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices) sont pris en charge pour être utilisés avec ces outils.

> [!Note]  
> Le [System Center 2012 R2 Configuration Manager Toolkit](https://www.microsoft.com/en-us/download/details.aspx?id=50012) est toujours disponible dans le Centre de téléchargement Microsoft. Pour Configuration Manager version 1806 et ultérieur, utilisez les versions des outils du dossier CD.Latest sur le serveur de site. Certains outils étaient autrefois dans le toolkit, mais pas dans la version 1806. Ces outils hérités ne sont plus pris en charge.


## <a name="client-tools"></a>Outils clients

- [CMTrace](/sccm/core/support/cmtrace) : afficher, surveiller et analyser les fichiers journaux Configuration Manager  

- [Client Spy](/sccm/core/support/clispy) : résoudre les problèmes liés à la distribution, l’inventaire et le contrôle des logiciels

- [Deployment Monitoring Tool](/sccm/core/support/deployment-monitoring-tool) : résoudre les problèmes liés aux applications, mises à jour et déploiements de ligne de base  

- [Policy Spy](/sccm/core/support/policy-spy) : afficher les affectations de stratégies  

- [Power Viewer Tool](/sccm/core/support/power-viewer-tool) : afficher l’état de la fonctionnalité de gestion de l’alimentation  

- [Send Schedule Tool](/sccm/core/support/send-schedule-tool) : déclencher des planifications et des évaluations des bases de référence de configuration  

> [!Note]  
> Le dossier ClientTools inclut aussi le fichier Microsoft.Diagnostics.Tracing.EventSource.dll. Plusieurs outils clients nécessitent cette bibliothèque. Vous ne pouvez pas les utiliser directement.  


## <a name="server-tools"></a>Outils de serveur

- [DP Job Queue Manager](/sccm/core/support/dp-job-manager) : permet de résoudre les problèmes relatifs aux travaux de distribution de contenu aux points de distribution  

- [Collection Evaluation Viewer](/sccm/core/support/ceviewer) : afficher les détails d’évaluation de la collection  

- [Content Library Explorer](/sccm/core/support/content-library-explorer) : afficher le contenu du magasin d’instances unique de la bibliothèque de contenu  

- [Content Library Transfer](/sccm/core/support/content-library-transfer) : transfère la bibliothèque de contenu entre des disques  

- [Content Ownership Tool](/sccm/core/support/content-ownership-tool) : modifie la propriété des packages orphelins. Ces packages existent dans le site sans serveur de site propriétaire.  

- [Role-based Administration and Auditing Tool](/sccm/core/support/rbaviewer) : permet aux administrateurs d’auditer la configuration des rôles  

- [Run Meter Summarization Tool](/sccm/core/support/run-meter-summ) : exécuter la tâche de totalisation du contrôle et analyser les données de contrôle

> [!Note]  
> Le dossier ServerTools inclut également les fichiers suivants 
> - AdminUI.WqlQueryEngine.dll
> - Microsoft.ConfigurationManagement.ManagementProvider.dll
> - Microsoft.Diagnostics.Tracing.EventSource.dll. 
>
> Plusieurs outils de serveur nécessitent ces bibliothèques. Vous ne pouvez pas les utiliser directement.  



## <a name="other-tools"></a>Autres outils

- [Outil de nettoyage de bibliothèque de contenu](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) : utilisez **ContentLibraryCleanup.exe** dans `CD.Latest\SMSSETUP\TOOLS\ContentLibraryCleanup` pour supprimer le contenu orphelin d’un point de distribution.  

- [Outil de maintenance hiérarchique](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) : utilisez **Preinst.exe** dans le dossier partagé `\<SiteServerName>\SMS_<SiteCode>\bin\X64\00000409` sur le serveur de site pour transmettre des commandes au composant de gestionnaire de hiérarchie.  

- [Outil de réinitialisation de mises à jour](/sccm/core/servers/manage/update-reset-tool) : utilisez **CMUpdateReset.exe** dans `CD.Latest\SMSSETUP\TOOLS\CMUpdateReset` pour résoudre les problèmes lorsque des mises à jour dans la console ont des difficultés à télécharger ou à se répliquer.  

- [Outil de connexion de service](/sccm/core/servers/manage/use-the-service-connection-tool) : utilisez **ServiceConnectionTool.exe** dans `CD.Latest\SMSSETUP\TOOLS\ServiceConnectionTool` pour garder votre site à jour quand votre point de connexion de service est hors connexion.  
