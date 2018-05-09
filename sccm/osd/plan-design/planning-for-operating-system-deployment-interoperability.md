---
title: Planification de l’interopérabilité des déploiements de systèmes d’exploitation
titleSuffix: Configuration Manager
description: Découvrez les problèmes d’interopérabilité qui peuvent se poser quand différents sites System Center Configuration Manager d’une même hiérarchie utilisent des versions distinctes.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: e327ce38-6c07-4a27-b6eb-7e5bf74ed04b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4faaae2d261837043b8b6ec208dd8b53b2a97b15
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="planning-for-operating-system-deployment-interoperability-in-system-center-configuration-manager"></a>Planification de l’interopérabilité des déploiements de systèmes d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand différents sites System Center Configuration Manager d’une même hiérarchie utilisent des versions distinctes, certaines fonctionnalités de Configuration Manager ne sont pas disponibles. En règle générale, les fonctionnalités de la version la plus récente de Configuration Manager ne sont pas accessibles sur les sites ou par les clients qui exécutent une version antérieure. Pour plus d'informations, consultez [Interopérabilité entre les différentes versions de System Center Configuration Manager](../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  

 Tenez compte des éléments suivants quand vous mettez à niveau le site de niveau supérieur de votre hiérarchie, et que d’autres sites de cette hiérarchie exécutent une version antérieure de Configuration Manager :  

-   Package d'installation du client  

    -   La source du package d’installation du client par défaut est mise à niveau automatiquement et tous les points de distribution dans la hiérarchie sont mis à jour avec le nouveau package d’installation du client, y compris sur les points de distribution dans les sites de la hiérarchie dont la version est antérieure.  

    -   Les clients qui exécutent la nouvelle version ne peuvent pas être attribués aux sites qui n'ont pas encore été mis à niveau vers la nouvelle version. L'affectation est bloquée au niveau du point de gestion.  

-   Images de démarrage  

    -   Quand vous mettez à niveau le site de niveau supérieur vers la dernière version de Configuration Manager, les images de démarrage par défaut (x86 et x64) sont mises à jour automatiquement vers Windows ADK pour les images de démarrage Windows 10, qui utilisent Windows PE 10. Les fichiers associés aux images de démarrage par défaut sont mis à jour vers la version Configuration Manager la plus récente des fichiers. Les images de démarrage personnalisées ne sont pas mises à jour automatiquement. Vous devez mettre manuellement à jour les images de démarrage personnalisées, notamment les versions antérieures de Windows PE.  

    -   Évitez d’utiliser des médias dynamiques quand votre hiérarchie de site contient des sites avec des versions distinctes de Configuration Manager. Utilisez plutôt un média basé sur site pour contacter un point de gestion spécifique tant que tous les sites ne sont pas mis à niveau vers la même version de Configuration Manager.  

    -   Vérifiez que les images de démarrage Configuration Manager les plus récentes contiennent la personnalisation souhaitée, puis mettez à jour tous les points de distribution sur les sites avec la dernière version de Configuration Manager et les nouvelles images de démarrage.  

-   Outil de migration de l'état utilisateur (USMT)  

    -   Quand vous mettez à niveau le site de niveau supérieur vers la dernière version de Configuration Manager, le package USMT par défaut est mis à jour automatiquement vers la dernière version. Les packages USMT personnalisés ne sont pas mis à jour automatiquement. Vous devez mettre à jour ces packages manuellement.  

-   Nouvelles étapes de séquence de tâche  

    -   À intervalles réguliers, de nouvelles étapes de séquence de tâches sont introduites avec les nouvelles versions de Configuration Manager. Quand vous déployez une séquence de tâches avec une nouvelle étape sur des clients plus anciens, l’étape échoue. Avant de déployer une séquence de tâches avec une nouvelle étape, vérifiez que les clients du regroupement cible sont mis à jour vers la nouvelle version.  

-   Média de déploiement de système d’exploitation  

    -   Tous les médias (de démarrage, de capture, préparés et autonomes) doivent être mis à jour avec le nouveau package client Configuration Manager quand le site est mis à jour vers une nouvelle version.  

-   Extensions tierces de déploiement de système d’exploitation  

    -   Quand vous avez des extensions tierces de déploiement de système d’exploitation et des versions distinctes de sites Configuration Manager ou de clients Configuration Manager (hiérarchie mixte), les extensions peuvent poser des problèmes.  

 Pendant la mise à niveau active des sites de votre hiérarchie, utilisez les sections suivantes pour vous aider lors des déploiements de système d’exploitation.  

## <a name="latest-version-of-configuration-manager-sites-in-a-mixed-hierarchy"></a>Version la plus récente de sites Configuration Manager dans une hiérarchie mixte  
 Quand vous mettez à niveau un site vers la dernière version de Configuration Manager, les séquences de tâches qui référencent le package d’installation client par défaut commencent automatiquement à déployer la dernière version cliente de Configuration Manager. Les séquences de tâches qui référencent un package d’installation client personnalisé continuent à déployer la version du client contenue dans ce package personnalisé (probablement une précédente version cliente de Configuration Manager) et doivent être mises à jour pour éviter l’échec de leur déploiement. Quand vous avez une séquence de tâches configurée pour utiliser un package d’installation client personnalisé, vous devez mettre à jour l’étape de séquence de tâches pour qu’elle utilise la dernière version Configuration Manager du package d’installation client, ou mettre à jour le package personnalisé pour qu’il utilise la source d’installation la plus récente du client Configuration Manager.  

> [!IMPORTANT]  
>  Ne déployez pas une séquence de tâches qui référence le package d’installation client Configuration Manager le plus récent sur les clients d’un ancien site Configuration Manager. Quand les clients affectés à un ancien site Configuration Manager sont mis à niveau vers la dernière version cliente de Configuration Manager, Configuration Manager bloque l’affectation à l’ancien site Configuration Manager. Ainsi, le client n’est plus affecté à un site et n’est plus géré tant que vous ne l’affectez pas manuellement à un site Configuration Manager récent ou tant que vous ne réinstallez pas l’ancienne version du client Configuration Manager sur l’ordinateur.  

## <a name="older-versions-of-configuration-manager-in-a-mixed-hierarchy"></a>Versions antérieures de Configuration Manager dans une hiérarchie mixte  
 Une fois que vous avez mis à niveau votre site d’administration centrale vers la dernière version de Configuration Manager, vous devez prendre les mesures suivantes pour éviter que les séquences de tâches de déploiement de système d’exploitation que vous déployez sur les clients affectés à un site Configuration Manager plus ancien (qui n’a pas encore été mis à niveau vers la dernière version de Configuration Manager) laissent ces clients dans un état non géré.  

-   Créez une séquence de tâches à utiliser pour le déploiement sur les clients d’un site Configuration Manager uniquement. Vous pouvez créer une copie d’une séquence de tâches que vous utilisez pour le déploiement sur les clients d’un site Configuration Manager de dernière version, puis modifier la séquence de tâches pour la déployer sur les clients d’un site Configuration Manager plus ancien. Ensuite, configurez la séquence de tâches pour référencer un package d’installation client personnalisé qui utilise la source d’installation antérieure du client Configuration Manager. Si vous n’avez pas encore de package d’installation client personnalisé qui fasse référence à la source d’installation antérieure du client Configuration Manager, vous devez en créer un manuellement.  
