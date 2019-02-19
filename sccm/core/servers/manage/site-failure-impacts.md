---
title: Impacts des défaillances du site
titleSuffix: Configuration Manager
description: Prenez connaissance des effets de diverses défaillances dans un site Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6f0e08f8-f2e1-4823-90f6-7b1f4341eb46
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: eebd1aaf72cbd7932a919c0a8ffdef6d6af8389f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132014"
---
# <a name="site-failure-impacts-in-configuration-manager"></a>Impacts des défaillances du site dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le serveur de site et les autres systèmes de site peuvent échouer et entraîner une perte des services qu’ils fournissent régulièrement. Si vous installez plusieurs systèmes de site sur le même ordinateur et si cet ordinateur échoue, tous les services normalement dispensés par ces systèmes de site ne sont plus disponibles.

Une partie de votre processus de planification doit inclure la compréhension de l’impact sur le service que vous fournissez à votre organisation. Comme chaque système de site remplit une fonction différente au sein d’un site, l’impact d’une défaillance sur le site varie en fonction du rôle du système de site qui a échoué. 

Utilisez les [options de haute disponibilité](/sccm/core/servers/deploy/configure/high-availability-options) pour atténuer la défaillance de n’importe quel système unique. Par ailleurs, planifiez et appliquez une stratégie de [sauvegarde et récupération](/sccm/core/servers/manage/backup-and-recovery) pour réduire la durée d’indisponibilité du service.

Les sections suivantes décrivent l’impact quand le système de site spécifié n’est pas opérationnel :


### <a name="site-server"></a>Serveur de site

- Aucune administration de site n’est possible. Vous ne pouvez pas connecter la console au site.  

- Le point de gestion recueille des informations sur le client et les place en mémoire cache jusqu’à ce que le serveur de site soit de nouveau en ligne.  

- Les utilisateurs peuvent exécuter des déploiements existants et les clients peuvent télécharger le contenu à partir de points de distribution.  


### <a name="site-database"></a>Base de données de site

- Aucune administration de site n’est possible.  

- Si le client Configuration Manager dispose déjà d’une attribution de stratégie avec de nouvelles stratégies et si le point de gestion a placé en mémoire cache le corps de cette stratégie, le client peut effectuer une demande de corps de stratégie et recevoir le corps de la stratégie en réponse. Toutefois, le site ne peut traiter aucune nouvelle demande d’attribution de stratégie.  

- Les clients peuvent exécuter des déploiements uniquement s’ils ont déjà reçu la stratégie et que les fichiers sources associés ont déjà été mis en mémoire cache localement sur le client.  


### <a name="management-point"></a>Point de gestion

- Bien que vous puissiez créer des déploiements, les clients ne les reçoivent pas tant qu’un point de gestion n’est pas en ligne.  

- Les clients collectent toujours des informations d’inventaire, de contrôle de logiciel et d’état. Ils stockent ces données localement jusqu’à ce que le point de gestion soit disponible.  

- Les clients peuvent exécuter des déploiements uniquement s’ils ont déjà reçu la stratégie et que les fichiers sources associés ont déjà été mis en mémoire cache localement sur le client.  


### <a name="distribution-point"></a>Point de distribution

- Les clients Configuration Manager peuvent exécuter des déploiements uniquement si les fichiers sources associés ont déjà été téléchargés localement ou sont disponibles sur une source d’homologue.

