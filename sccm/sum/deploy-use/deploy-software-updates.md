---
title: Déployer des mises à jour logicielles
titleSuffix: Configuration Manager
description: Découvrez comment déployer manuellement ou automatiquement des mises à jour logicielles dans la console Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 04536d51-3bf7-45e5-b4af-36ceed10583d
ms.openlocfilehash: f59ca099325028ccf29904a2108939d0047df745
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52455941"
---
# <a name="deploy-software-updates"></a>Déployer des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

La phase de déploiement de mises à jour logicielles consiste à déployer les mises à jour logicielles. Quelle que soit la façon dont vous déployez des mises à jour logicielles, le site :
- Ajoute les mises à jour à un groupe de mises à jour logicielles.
- Distribue le contenu de la mise à jour aux points de distribution.
- Déploie le groupe de mise à jour sur les clients.  

Une fois que vous avez créé le déploiement, le site envoie une stratégie de mise à jour logicielle associée aux clients ciblés. Les clients téléchargent les fichiers de contenu de mise à jour logicielle à partir d’une source de contenu dans leur cache local. Les clients sur Internet téléchargent toujours le contenu à partir du service cloud de Microsoft Update. Les mises à jour de logiciels sont alors accessibles aux clients, qui peuvent les installer.   

> [!Tip]  
>  Si aucun point de distribution n’est disponible, les client sur l’intranet peuvent aussi télécharger les mises à jour logicielles à partir de Microsoft Update.  

> [!NOTE]  
>  Contrairement à d’autres types de déploiements, les mises à jour de logiciels sont téléchargées dans le cache du client, indépendamment de son paramètre de taille maximale. Pour plus d’informations sur le paramètre de cache du client, consultez [Configurer le cache du client pour les clients Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_ClientCache).  

Si vous configurez un déploiement de mises à jour logicielles requises, celles-ci sont automatiquement installées à l'échéance prévue. L'utilisateur sur l'ordinateur client peut également planifier ou lancer l'installation des mises à jour logicielles avant l'échéance. Après la tentative d'installation, les ordinateurs clients renvoient des messages d'état au serveur de site pour indiquer si l'installation des mises à jour logicielles a réussi. Pour plus d’informations sur les déploiements de mises à jour logicielles, consultez [Software update deployment workflows](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentWorkflows).  

Il existe trois principaux scénarios de déploiement des mises à jour logicielles : 
- [Déploiement manuel](#BKMK_ManualDeployment)  
- [Déploiement automatique](#bkmk_auto)  
- [Déploiement par phases](#bkmk_phased)  

En général, vous commencez par déployer manuellement les mises à jour logicielles afin de créer une référence pour vos clients, puis vous gérez les mises à jour logicielles sur les clients à l’aide d’un déploiement automatique ou par phases.  

> [!Note]  
> Vous ne pouvez pas utiliser une règle de déploiement automatique avec un déploiement par phases.



## <a name="BKMK_ManualDeployment"></a> Déployer manuellement des mises à jour logicielles
Sélectionnez les mises à jour logicielles dans la console Configuration Manager et démarrez manuellement le processus de déploiement. Vous utilisez généralement cette méthode de déploiement pour :  

- Faire en sorte que les clients soient à jour avec les mises à jour logicielles requises avant de créer des règles de déploiement automatique qui gèrent les déploiements mensuels.  

- Déployer des mises à jour logicielles hors-bande.  


La liste suivante fournit le flux de travail général pour le déploiement manuel de mises à jour logicielles :  

1. filtre pour les mises à jour logicielles qui utilisent des configurations spécifiques. Par exemple, spécifiez des critères qui récupèrent toutes les mises à jour logicielles critiques ou de sécurité qui sont requises sur plus de 50 clients.  

2. Créez un groupe de mises à jour logicielles contenant les mises à jour logicielles.  

3. Téléchargez le contenu pour les mises à jour logicielles dans le groupe de mises à jour logicielles.  

4. Déployez manuellement le groupe de mises à jour logicielles.  

Pour plus d’informations et pour obtenir des instructions détaillées, consultez [Déployer manuellement des mises à jour logicielles](manually-deploy-software-updates.md).

> [!Tip]  
> Quand vous déployez manuellement des mises à jour du client Office 365, elles sont disponibles dans le nœud **Mises à jour Office 365** sous **Gestion des clients Office 365** dans l’espace de travail **Bibliothèque de logiciels**.  



## <a name="bkmk_auto"></a> Déployer automatiquement des mises à jour logicielles

Configurez le déploiement automatique de mises à jour logicielles à l’aide d’une règle de déploiement automatique (ADR). Cette méthode est courante pour le déploiement des mises à jour logicielles mensuelles (généralement appelées « Patch Tuesday ») et pour la gestion des mises à jour de définitions. Vous définissez les critères d’une règle ADR afin d’automatiser le processus de déploiement. La liste suivante fournit le flux de travail général pour le déploiement automatique des mises à jour logicielles :  

1.  Créez une règle de déploiement automatique qui spécifie les paramètres de déploiement.  

2.  Le site ajoute les mises à jour logicielles à un groupe de mises à jour logicielles.  

3.  Le site déploie le groupe de mises à jour logicielles sur les clients du regroupement cible.  

Tout d’abord, déterminez votre stratégie de déploiement automatique des mises à jour logicielles. Par exemple, créez la règle ADR pour cibler initialement un regroupement de clients test. Après avoir vérifié que le groupe test avait installé correctement les mises à jour logicielles, ajoutez un nouveau déploiement à la règle. Vous pouvez également modifier le regroupement ciblé dans le déploiement existant pour qu’il inclut un ensemble de clients plus étendu. Quand vous choisissez la stratégie à utiliser, tenez compte des comportements suivants :  

- Vous pouvez modifier les propriétés des objets de mise à jour logicielle créés par la règle ADR.   

- La règle ADR déploie automatiquement les mises à jour logicielles sur les clients quand vous les ajoutez au regroupement cible.  

- Quand la règle ADR ou vous-même ajoutez de nouvelles mises à jour logicielles au groupe de mise à jour logicielles, le site les déploie automatiquement sur les clients du regroupement cible.  

- Activez ou désactivez les déploiements à tout moment pour la règle ADR.  


Après avoir créé une règle ADR, vous pouvez y ajouter des déploiements supplémentaires. Cela peut vous aider à gérer la complexité liée au déploiement de différentes mises à jour vers différents regroupements. Chaque nouveau déploiement possède la gamme complète de fonctionnalités et d'expérience de surveillance de déploiement.  

Chaque nouveau déploiement que vous ajoutez :  

-   Utilise le package et le groupe de mise à jour créés par la règle ADR lors de la première exécution.  
-   Peut cibler un autre regroupement.  
-   prend en charge des propriétés de déploiement uniques, notamment :  
   -   Heure d'activation  
   -   Échéance  
   -   Expérience utilisateur  
   -   Sépare les alertes pour chaque déploiement.  


Pour plus d’informations et pour obtenir des étapes détaillées, consultez [Déployer automatiquement des mises à jour logicielles](automatically-deploy-software-updates.md).



## <a name="bkmk_phased"></a> Déployer les mises à jour logicielles par phases

<!--1358146--> À compter de la version 1810, créez des déploiement par phases pour les mises à jour logicielles. Ils permettent d’orchestrer un lancement coordonné et séquencé de logiciels en fonction de groupes et de critères personnalisables.

Pour plus d’informations, voir [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json).

