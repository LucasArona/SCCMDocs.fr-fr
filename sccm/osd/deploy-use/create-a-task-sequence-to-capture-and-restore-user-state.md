---
title: Capturer et restaurer l’état utilisateur
titleSuffix: Configuration Manager
description: Utiliser les séquences de tâches de Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9888bbcc0468356b55216491d8599ebb5f42818
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420428"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-configuration-manager"></a>Créer une séquence de tâches pour capturer et restaurer l’état utilisateur dans Configuration Manager

 *S’applique à : System Center Configuration Manager (Current Branch)*

 Utiliser les séquences de tâches de Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation. Dans ces scénarios, vous souhaitez conserver l’état utilisateur du système d’exploitation actuel. En fonction du type de séquence de tâches que vous créez, les étapes de capture et de restauration peuvent être ajoutées automatiquement dans le cadre de la séquence de tâches. Dans d’autres scénarios, vous devrez peut-être ajouter manuellement les étapes de capture et de restauration à la séquence de tâches. Cet article fournit les étapes que vous devez ajouter à une séquence de tâches existante pour capturer et restaurer des données d’état utilisateur.  



## <a name="task-sequence-steps"></a>Étapes de séquence de tâches  

 Pour capturer et restaurer l’état utilisateur, ajoutez les étapes suivantes à la séquence de tâches :  

 - [Demander le magasin d’états](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore) : Si vous stockez l’état utilisateur sur le point de migration d’état, cette étape est nécessaire.  

- [Capturer l’état utilisateur](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState) : Cette étape capture les données d’état utilisateur. Il stocke ensuite les données sur le point de migration d’état ou sur le disque local à l’aide des liaisons permanentes.  

- [Restaurer l’état utilisateur](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState) : cette étape restaure les données d'état utilisateur sur l'ordinateur de destination. Il peut récupérer les données à partir d’un point de migration d’état, ou s’il y a des liaisons permanentes sur le disque local.  

- [Libérer le magasin d’état](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore) : Si vous stockez l’état utilisateur sur le point de migration d’état, cette étape est nécessaire. Cette étape supprime les données du point de migration d'état.  


 Utilisez les procédures suivantes pour ajouter les étapes de séquence de tâches nécessaires pour capturer et restaurer l'état utilisateur. Pour plus d’informations sur la création d’une séquence de tâches, consultez [Gérer les séquences de tâches pour automatiser des tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks).  



## <a name="capture-the-user-state"></a>Capturer l'état utilisateur  

 Pour ajouter des étapes de séquence de tâches afin de capturer l'état utilisateur, procédez comme suit :

1.  Dans la liste **Séquence de tâches** , sélectionnez une séquence de tâches et cliquez sur **Modifier**.  

2.  Si vous utilisez un point de migration d'état pour stocker l'état utilisateur, ajoutez l'étape **Demander le magasin d'état** à la séquence de tâches. Dans l’**éditeur de séquence de tâches**, cliquez sur **Ajouter**. Pointez sur **État utilisateur**, puis cliquez sur **Demander le magasin d'état**. Configurez les propriétés et les options de cette étape, puis cliquez sur **Appliquer**. Pour plus d'informations sur les paramètres disponibles, consultez [Demander le magasin d'état](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore).  

3.  Ajoutez l'étape **Capturer l'état utilisateur** à la séquence de tâches. Dans l’**éditeur de séquence de tâches**, cliquez sur **Ajouter**. Pointez sur **État utilisateur**, puis cliquez sur **Capturer l'état utilisateur**. Configurez les propriétés et les options de cette étape, puis cliquez sur **Appliquer**. Pour plus d'informations sur les paramètres disponibles, consultez [Capturer l'état utilisateur](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState).  

    > [!IMPORTANT]  
    >  Lorsque vous ajoutez cette étape à votre séquence de tâches, définissez également la variable de séquence de tâches **OSDStateStorePath** pour indiquer où stocker les données d'état utilisateur. Si vous stockez l'état utilisateur localement, ne spécifiez pas de dossier racine, car la séquence de tâches risquerait d'échouer. Lorsque vous stockez les données utilisateur localement, utilisez toujours un dossier ou un sous-dossier. Pour plus d'informations sur cette variable, consultez [Variable de séquence de tâches](/sccm/osd/understand/task-sequence-variables#OSDStateStorePath).  

4.  Si vous utilisez un point de migration d’état, ajoutez l’étape **Libérer le magasin d’état** à la séquence de tâches. Dans l’**éditeur de séquence de tâches**, cliquez sur **Ajouter**. Pointez sur **État utilisateur**, puis cliquez sur **Libérer le magasin d'état**. Configurez les propriétés et les options de cette étape, puis cliquez sur **Appliquer**. Pour plus d'informations sur les paramètres disponibles, consultez [Libérer le magasin d'état](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore).  

    > [!IMPORTANT]  
    >  L'action de séquence de tâches exécutée avant l'étape **Libérer le magasin d'état** doit être effectuée avec succès avant que l'étape **Libérer le magasin d'état** démarre.  


 Déployez cette séquence de tâches pour capturer l'état utilisateur sur un ordinateur de destination. Pour plus d’informations sur la façon de déployer des séquences de tâches, consultez [Déployer une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  



## <a name="restore-the-user-state"></a>Restaurer l'état utilisateur  

 Pour ajouter des étapes de séquence de tâches afin de restaurer l'état utilisateur, procédez comme suit :

1. Dans la liste **Séquence de tâches** , sélectionnez une séquence de tâches et cliquez sur **Modifier**.  

2. Ajoutez l’étape **Restaurer l’état utilisateur** à la séquence de tâches. Dans l’**éditeur de séquence de tâches**, cliquez sur **Ajouter**. Pointez sur **État utilisateur**, puis cliquez sur **Restaurer l'état utilisateur**. Cette étape établit une connexion avec le point de migration d'état si nécessaire. Configurez les propriétés et les options de cette étape, puis cliquez sur **Appliquer**. Pour plus d'informations sur les paramètres disponibles, consultez [Restaurer l'état utilisateur](/sccm/osd/understand/task-sequence-steps#BKMK_RestoreUserState).  

   > [!Important]  
   >  Quand vous utilisez l’étape [Capturer l’état utilisateur](/sccm/osd/understand/task-sequence-steps#BKMK_CaptureUserState) avec l’option **Capturer tous les profils utilisateur à l’aide des options standard**, vous devez sélectionner le paramètre **Restaurer les profils utilisateur de l’ordinateur local** à l’étape **Restaurer l’état utilisateur**. Sinon la séquence de tâches échouera.  

   > [!Note]  
   > Si vous stockez l’état utilisateur à l’aide de liaisons permanentes locales et que la restauration échoue, vous pouvez supprimer manuellement les liaisons permanentes qui ont été créées pour stocker les données. La séquence de tâches peut exécuter l’outil USMTUtils pour automatiser cette action avec une étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine). Si vous utilisez USMTUtils pour supprimer le lien permanent, ajoutez une étape [Redémarrer l’ordinateur](/sccm/osd/understand/task-sequence-steps#BKMK_RestartComputer) après avoir exécuté USMTUtils.  

3. Si vous utilisez un point de migration d’état pour stocker l’état utilisateur, ajoutez l’étape **Libérer le magasin d’état** à la séquence de tâches. Dans l’**éditeur de séquence de tâches**, cliquez sur **Ajouter**. Pointez sur **État utilisateur**, puis cliquez sur **Libérer le magasin d'état**. Configurez les propriétés et les options de cette étape, puis cliquez sur **Appliquer**. Pour plus d'informations sur les paramètres disponibles, consultez [Libérer le magasin d'état](/sccm/osd/understand/task-sequence-steps#BKMK_ReleaseStateStore).  

   > [!IMPORTANT]  
   >  L'action de séquence de tâches exécutée avant l'étape **Libérer le magasin d'état** doit être effectuée avec succès avant que l'étape **Libérer le magasin d'état** démarre.  


 Déployez cette séquence de tâches pour restaurer l'état utilisateur sur un ordinateur de destination. Pour plus d’informations sur le déploiement de séquences de tâches, consultez [Déployer une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  



## <a name="next-steps"></a>Étapes suivantes

[Surveiller le déploiement de la séquence de tâches](/sccm/osd/deploy-use/monitor-operating-system-deployments#BKMK_TSDeployStatus)
