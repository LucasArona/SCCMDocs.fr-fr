---
title: Interopérabilité pour le déploiement de systèmes d’exploitation
titleSuffix: Configuration Manager
description: Découvrez les problèmes d’interopérabilité qui peuvent se poser quand différents sites System Center Configuration Manager d’une même hiérarchie utilisent des versions distinctes.
ms.date: 05/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d4f6275ede2a751acb8ca14d7b8b6ad307e78bd
ms.sourcegitcommit: 18a94eb78043cb565b05cd0e9469b939b29cccf0
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66355027"
---
# <a name="plan-for-os-deployment-interoperability"></a>Planifier l’interopérabilité pour le déploiement de systèmes d’exploitation

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand différents sites System Center Configuration Manager d’une même hiérarchie utilisent des versions distinctes, certaines fonctionnalités de Configuration Manager ne sont pas disponibles. En général, les fonctionnalités de la version la plus récente de Configuration Manager ne sont pas accessibles sur les sites ou par les clients qui exécutent une version antérieure. Pour plus d'informations, consultez [Interopérabilité entre les différentes versions de System Center Configuration Manager](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


## <a name="objects"></a>Objets

Tenez compte des objets suivants quand vous mettez à niveau le site de niveau supérieur de votre hiérarchie et que d’autres sites de cette hiérarchie exécutent une version antérieure de Configuration Manager :  

### <a name="client-installation-package"></a>Package d'installation du client  

- La source du package d’installation client par défaut est automatiquement mise à niveau. Tous les points de distribution de la hiérarchie sont mis à jour avec le nouveau package d’installation du client. Ce comportement se produit même sur les points de distribution dans les sites de la hiérarchie dont la version est antérieure.  

- Vous ne pouvez pas attribuer des clients de la nouvelle version à des sites que vous n’avez pas encore mis à niveau vers la nouvelle version. L'affectation est bloquée au niveau du point de gestion.  

### <a name="boot-images"></a>Images de démarrage  

- Quand vous mettez à niveau le site de niveau supérieur vers la version de Configuration Manager la plus récente, cela met automatiquement à jour les images de démarrage par défaut (x86 et x64). La mise à jour utilise le kit Windows ADK pour Windows 10, qui inclut Windows PE 10. Les fichiers associés aux images de démarrage par défaut sont mis à jour vers la version Configuration Manager la plus récente des fichiers. Le site ne met pas automatiquement à jour les images de démarrage personnalisées. Vous devez mettre manuellement à jour les images de démarrage personnalisées, notamment les versions antérieures de Windows PE.  

- Quand votre hiérarchie de site contient des sites avec des versions distinctes de Configuration Manager, évitez d’utiliser des médias dynamiques. Utilisez plutôt un média basé sur le site pour contacter un point de gestion spécifique. Après avoir mis à jour tous les sites vers la même version de Configuration Manager, vous pouvez réutiliser un média dynamique.

- Vérifiez que les images de démarrage Configuration Manager les plus récentes incluent vos personnalisations. Mettez ensuite à jour tous les points de distribution sur les sites de la nouvelle version avec la version la plus récente des nouvelles images de démarrage.  

### <a name="user-state-migration-tool-usmt"></a>Outil de migration de l'état utilisateur (USMT)  

Quand vous mettez à niveau le site de niveau supérieur vers la version la plus récente de Configuration Manager, cela met automatiquement à jour le package USMT par défaut vers la dernière version. Cela ne met pas automatiquement à jour tous les packages USMT personnalisés. Vous devez mettre à jour ces packages manuellement.  

### <a name="new-task-sequence-steps"></a>Nouvelles étapes de séquence de tâche  

À intervalles réguliers, de nouvelles étapes de séquence de tâches sont introduites avec les nouvelles versions de Configuration Manager. Quand vous déployez une séquence de tâches avec une nouvelle étape sur des clients plus anciens, l’étape de la séquence de tâches échoue. Avant de déployer une séquence de tâches avec une nouvelle étape, vérifiez que les clients du regroupement cible sont mis à jour vers la nouvelle version.  

### <a name="os-deployment-media"></a>Média de déploiement de système d’exploitation  

Quand le site est mis à jour vers une nouvelle version, mettez à jour tous les médias avec le nouveau package client Configuration Manager. Ces types de médias incluent les médias de démarrage, de capture, préparés et autonomes.

### <a name="third-party-extensions-to-os-deployment"></a>Extensions tierces de déploiement de système d’exploitation  

Quand vous disposez d’extensions tierces de déploiement de système d’exploitation et que vous avez des versions différentes de sites Configuration Manager ou de clients Configuration Manager, les extensions peuvent poser des problèmes.  


## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Version la plus récente de sites Configuration Manager dans une hiérarchie mixte  

Quand vous mettez à niveau un site vers la version la plus récente de Configuration Manager, les séquences de tâches qui référencent le package d’installation du client par défaut commencent automatiquement à déployer la version la plus récente du client Configuration Manager.

Les séquences de tâches qui font référence à un package d’installation du client personnalisé continuent à déployer la version du client qui est contenue dans ce package personnalisé. Les packages personnalisés incluent probablement une version antérieure du client Configuration Manager. Pour éviter les échecs de déploiement de séquences de tâches, mettez à jour les packages d’installation de client personnalisé vers la version la plus récente.

Quand vous configurez une séquence de tâches pour utiliser un package d’installation de client personnalisé, effectuez l’une des actions suivantes :

- Mettre à jour l’étape de séquence de tâches de manière à utiliser la version la plus récente de Configuration Manager du package d’installation du client
- Mettre à jour le package personnalisé de manière à utiliser la source d’installation la plus récente du client Configuration Manager

> [!IMPORTANT]  
> Ne déployez pas une séquence de tâches qui référence le package d’installation client Configuration Manager le plus récent sur les clients d’un ancien site Configuration Manager. Quand les clients affectés à un ancien site Configuration Manager sont mis à niveau vers la dernière version cliente de Configuration Manager, Configuration Manager bloque l’affectation à l’ancien site Configuration Manager. Ces clients ne sont plus affectés à aucun site. Tant que vous n’affectez pas manuellement le client au site Configuration Manager le plus récent ou que vous ne réinstallez pas l’ancienne version de Configuration Manager sur l’ordinateur, ces clients ne sont pas gérés.


## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Anciennes versions de Configuration Manager dans une hiérarchie mixte  

Quand vous mettez à niveau votre site d’administration centrale vers la dernière version de Configuration Manager, vérifiez que les séquences de tâches de déploiement de système d’exploitation que vous déployez ne laissent pas ces clients dans un état non géré. Par exemple, si vous effectuez un déploiement sur des clients affectés à un ancien site Configuration Manager que vous n’avez pas encore mis à niveau vers la version la plus récente de Configuration Manager.

Effectuez une copie d’une séquence de tâches que vous utilisez pour effectuez un déploiement sur des clients dans la version la plus récente d’un site Configuration Manager. Modifiez ensuite la séquence de tâches afin de pouvoir la déployer sur des clients dans un ancien site Configuration Manager. Configurez la séquence de tâches pour référencer un package d’installation du client personnalisé qui utilise la source d’installation antérieure du client Configuration Manager. Si vous n’avez pas encore de package d’installation du client personnalisé qui fasse référence à la source d’installation antérieure du client Configuration Manager, créez-en un manuellement.  

> [!Important]  
> À compter de la version 1902, vous ne pouvez pas déployer un package ou une séquence de tâches sur une version du client 5.7730 ou antérieure. Pour contourner cette limitation, mettez à niveau le client vers une version ultérieure.<!-- SCCMDocs-pr issue #3493 -->
