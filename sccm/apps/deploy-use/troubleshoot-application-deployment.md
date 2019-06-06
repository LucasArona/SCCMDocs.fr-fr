---
title: Résoudre les problèmes liés aux déploiements d’applications
titleSuffix: Configuration Manager
description: Conseils pour la résolution des problèmes liés au déploiement d’applications dans System Center Configuration Manager
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 75dcf2d4ae69c2181fecde0c04359faa46753e88
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411018"
---
# <a name="troubleshoot-application-deployments"></a>Résoudre les problèmes liés aux déploiements d’applications

*S’applique à : System Center Configuration Manager (Current Branch)*

Les problèmes courants rencontrés avec les déploiements d’applications appartiennent à l’une des catégories suivantes :

- Échecs de téléchargement d’applications

- Conformité du déploiement d’application bloquée à 0 %

Si vous rencontrez l’un de ces problèmes, cet article fournit des étapes que vous pouvez utiliser pour résoudre les problèmes.


## <a name="download-failures"></a>Échecs de téléchargement

Les problèmes entraînant des échecs de téléchargement d’applications sont notamment les suivants :

- Le client est bloqué lors du téléchargement d’une application

- Le client ne parvient pas à télécharger le contenu de l’application

- Le client est bloqué à 0 % lors du téléchargement de l’application

Des limites et des groupes de limites manquants ou mal configurés sont la première chose à vérifier quand vous rencontrez des échecs de téléchargement d’applications. Par exemple, si le client se trouve sur l’intranet et qu’il n’est pas configuré pour la gestion des clients Internet uniquement, son emplacement réseau doit se trouver dans une limite configurée. Un groupe de limites doit également être attribué à cette limite pour que le client télécharge du contenu. Pour plus d’informations, consultez [Définir les limites de site et les groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups).

Si vous ne pouvez pas configurer une limite pour un client ou si un groupe de limites spécifique ne peut pas être membre d’un autre groupe de limites :

1. Dans la console Configuration Manager, ouvrez les propriétés du **Type de déploiement**.  

1. Accédez à l’onglet **Contenu**.

1. Dans la section relative à l’utilisation d’un point de distribution à partir d’un groupe de limites voisin ou du groupe de limites de site par défaut, remplacez la valeur **Options de déploiement** par **Télécharger le contenu à partir du point de distribution et l’exécuter localement**. (Par défaut, ce paramètre est **Ne pas télécharger de contenu**.)

Si le client ne peut pas télécharger le contenu de l’application, vérifiez qu’il est distribué sur un point de distribution. Pour vérifier cette configuration, utilisez les fonctionnalités dans la console pour superviser la distribution de contenu sur les points de distribution. Pour plus d’informations, consultez [Superviser le contenu que vous avez distribué](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed).  


## <a name="compliance-stuck-at-0"></a>Conformité bloquée à 0 %

Quand la conformité du déploiement de l’application est de 0 %, vérifiez l’état de déploiement de l’application dans l’espace de travail **Supervision** sous le nœud **Déploiements**.

- **En cours** : le client peut être bloqué [lors du téléchargement de contenu](#download-failures)

- **Erreur** : pour plus d’informations sur la façon de résoudre ce problème, consultez le billet de blog suivant : [Astuces et conseils : comment effectuer une action sur des ressources qui signalent l’échec d’un déploiement](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Inconnu** : cet état signifie généralement que le client n’a pas reçu la stratégie. Actualisez manuellement la stratégie du client pour voir si le client la reçoit. Pour plus d’informations, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).
  
Si ces actions ne résolvent pas le problème, vérifiez l’état du client. Il peut être avoir un problème sous-jacent plus grave avec le client. Pour plus d’informations, consultez le [Guide pratique pour superviser des clients](/sccm/core/clients/manage/monitor-clients).


## <a name="next-steps"></a>Étapes suivantes

- [Surveiller les applications](/sccm/apps/deploy-use/monitor-applications-from-the-console)
- [Déployer des applications](/sccm/apps/deploy-use/deploy-applications)
- [Tâches de gestion pour les applications](/sccm/apps/deploy-use/management-tasks-applications)
