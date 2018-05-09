---
title: Déployer des mises à jour logicielles
titleSuffix: Configuration Manager
description: Choisissez les mises à jour logicielles dans la console Configuration Manager pour démarrer manuellement le processus de déploiement ou déployer automatiquement des mises à jour.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/16/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: e6a825f0d4333dc551405e38db70f8417ee2b5ce
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_SUMDeploy"></a> Déployer des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

La phase de déploiement de mises à jour logicielles consiste à déployer les mises à jour logicielles. Quelle que soit le mode de déploiement utilisé, les mises à jour de logiciels sont généralement :
- ajoutées à un groupe de mises à jour de logiciels ;
- téléchargées sur des points de distribution.
- Le groupe de mises à jour est déployé auprès des clients. Une fois le déploiement créé, une stratégie associée de mise à jour de logiciel est envoyée aux ordinateurs clients. Les fichiers de contenu des mises à jour de logiciels sont téléchargés dans le cache local des ordinateurs clients, à partir d’un point de distribution. Les mises à jour de logiciels sont alors accessibles aux clients, qui peuvent les installer. Les clients sur Internet téléchargent le contenu auprès de Microsoft Update.  

> [!NOTE]  
>  Si aucun point de distribution n’est disponible, vous pouvez configurer un client sur l’intranet pour télécharger les mises à jour de logiciels à partir de Microsoft Update.  

> [!NOTE]  
>  Contrairement à d’autres types de déploiements, les mises à jour de logiciels sont téléchargées dans le cache du client, indépendamment de son paramètre de taille maximale. Pour plus d’informations sur le paramètre de cache du client, consultez [Configure the Client Cache for Configuration Manager Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache).  

Si vous configurez un déploiement de mises à jour logicielles requises, celles-ci sont automatiquement installées à l'échéance prévue. L'utilisateur sur l'ordinateur client peut également planifier ou lancer l'installation des mises à jour logicielles avant l'échéance. Après la tentative d'installation, les ordinateurs clients renvoient des messages d'état au serveur de site pour indiquer si l'installation des mises à jour logicielles a réussi. Pour plus d’informations sur les déploiements de mises à jour logicielles, consultez [Software update deployment workflows](../understand/software-updates-introduction.md#BKMK_DeploymentWorkflows).  

Il existe deux principaux scénarios de déploiement des mises à jour logicielles : le déploiement manuel et le déploiement automatique. On commence en général par déployer manuellement les mises à jour de logiciels afin de créer une référence pour les ordinateurs clients, avant de gérer les mises à jour de logiciels sur les clients à l’aide d’un déploiement automatique.  

## <a name="BKMK_ManualDeployment"></a> Déployer manuellement des mises à jour logicielles
Vous pouvez sélectionner les mises à jour logicielles dans la console Configuration Manager et démarrer manuellement le processus de déploiement. Généralement, vous utilisez cette méthode de déploiement pour mettre à jour les ordinateurs clients avec les mises à jour logicielles requises avant de créer des règles de déploiement automatique qui gèrent les déploiements de mises à jour logicielles mensuelles en continu ; vous pouvez également déployer des mises à jour logicielles requises hors bande. La liste suivante fournit le flux de travail général pour le déploiement manuel de mises à jour logicielles :  

1. filtre pour les mises à jour logicielles qui utilisent des configurations spécifiques. Par exemple, vous pouvez fournir des critères qui récupèrent toutes les mises à jour logicielles critiques ou de sécurité qui sont requises sur plus de 50 ordinateurs clients.  
2. Créez un groupe de mises à jour logicielles contenant les mises à jour logicielles.  
3. Téléchargez le contenu pour les mises à jour logicielles dans le groupe de mises à jour logicielles.  
4. Déployez manuellement le groupe de mises à jour logicielles.

Pour obtenir des instructions détaillées, consultez [Déployer manuellement des mises à jour logicielles](manually-deploy-software-updates.md).

>[!NOTE]
>Depuis la version 1706 de Configuration Manager, les mises à jour clients Office 365 ont été déplacées vers le nœud **Gestion des clients Office 365** >**Mises à jour Office 365**. Cela n’aura pas d’impact sur la configuration des règles de déploiement automatique ; le déploiement manuel des mises à jour Office 365, lui, en sera affecté. 

## <a name="automatically-deploy-software-updates"></a>Déployer automatiquement des mises à jour logicielles
La configuration du déploiement automatique de mises à jour logicielles s’effectue à l'aide d’une règle de déploiement automatique. Il s’agit d’une méthode courante pour le déploiement des mises à jour logicielles mensuelles (généralement appelées « Patch Tuesday ») et pour la gestion des mises à jour de définitions. Quand la règle s’exécute, les mises à jour logicielles sont supprimées du groupe de mises à jour logicielles (le cas échéant), celles qui répondent aux critères spécifiés (par exemple, toutes les mises à jour logicielles publiées au cours du dernier mois) sont ajoutées à un groupe de mises à jour logicielles, les fichiers de contenu des mises à jour logicielles sont téléchargés et copiés aux points de distribution, et les mises à jour logicielles sont déployées sur les clients du regroupement cible. La liste suivante fournit le flux de travail général pour le déploiement automatique des mises à jour logicielles :  

1.  Créez une règle de déploiement automatique qui spécifie les paramètres de déploiement.
2.  Les mises à jour logicielles sont ajoutées à un groupe de mises à jour logicielles.  
3.  Le groupe de mises à jour logicielles est déployé sur les ordinateurs clients du regroupement cible, s'il est spécifié.  

Vous devez déterminer quelle stratégie de déploiement utiliser dans votre environnement. Par exemple, vous pouvez créer la règle de déploiement automatique et cibler un regroupement de clients test. Après avoir vérifié que les mises à jour logicielles sont installées sur le groupe test, vous pouvez ajouter un nouveau déploiement à la règle ou modifier le regroupement dans le déploiement existant et le remplacer par un regroupement cible qui comprend un ensemble plus important de clients. Les objets de mise à jour logicielle qui sont créés par les règles de déploiement automatique sont interactifs.  

-   Les mises à jour logicielles qui ont été déployées à l'aide d'une règle de déploiement automatique sont déployées automatiquement sur les nouveaux clients ajoutés au regroupement cible.  
-   Les nouvelles mises à jour logicielles ajoutées à un groupe de mises à jour logicielles sont déployées automatiquement sur les clients du regroupement cible.  
-   Vous pouvez activer ou désactiver les déploiements à tout moment pour la règle de déploiement automatique.  

Après avoir créé une règle de déploiement automatique, vous pouvez y ajouter des déploiements supplémentaires. Cela peut vous aider à gérer la complexité liée au déploiement de différentes mises à jour vers différents regroupements. Chaque nouveau déploiement possède la gamme complète de fonctionnalités et d'expérience de surveillance de déploiement, et chaque nouveau déploiement que vous ajoutez :  

-   utilise le package et le groupe de mise à jour créés lors de la première exécution de la règle de déploiement automatique ;  
-   peut spécifier un regroupement différent ;  
-   prend en charge des propriétés de déploiement uniques, notamment :  
   -   Heure d'activation  
   -   Échéance  
   -   Afficher ou masquer l'expérience utilisateur  
   -   Séparer les alertes pour ce déploiement  

Pour obtenir des instructions détaillées, consultez [Déployer automatiquement des mises à jour logicielles](automatically-deploy-software-updates.md).

<!-- ###  <a name="BKMK_ClientCache"></a> Client cache setting  
The Configuration Manager client downloads the content for required software updates to the local client cache soon after it receives the deployment. However, the client waits to download the content until after the **Software available time** setting for the deployment. The client does not download software updates in optional deployments (deployments that do not have a scheduled installation deadline) until the user manually starts the installation. When the configured deadline passes, the software updates client agent performs a scan to verify that the software update is still required, then the software updates client agent checks the local cache on the client computer to verify that the software update source file is still available, and then installs the software update. If the content was deleted from the client cache to make room for another deployment, the client downloads the software updates to the cache. Software updates are always downloaded to the client cache regardless of the configured maximum client cache size. For other deployments, such as applications or packages, the client only downloads content that is within the maximum cache size that you configure for the client. Cached content is not automatically deleted, but it remains in the cache for at least one day after the client used that content.  -->


 <!-- For more information about the deployment process, see [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).  -->
