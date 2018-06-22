---
title: Créer une séquence de tâches pour capturer et restaurer l’état utilisateur
titleSuffix: Configuration Manager
description: Utilisez des séquences de tâches System Center Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation.
ms.date: 06/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d566d85c-bf7a-40e7-8239-57640a1db5f4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ab5cbaf481842cf814d5f1b90af4f6743bb8a803
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351766"
---
# <a name="create-a-task-sequence-to-capture-and-restore-user-state-in-system-center-configuration-manager"></a>Créer une séquence de tâches pour capturer et restaurer l’état utilisateur dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser des séquences de tâches System Center Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation où vous souhaitez conserver l’état utilisateur du système d’exploitation actuel. En fonction du type de séquence de tâches que vous créez, les étapes de capture et de restauration peuvent être ajoutées automatiquement dans le cadre de la séquence de tâches. Dans d’autres scénarios, vous devrez peut-être ajouter manuellement les étapes de capture et de restauration à la séquence de tâches. Cette rubrique fournit les étapes que vous devez ajouter à une séquence de tâches existante pour capturer et restaurer des données d’état utilisateur.  

##  <a name="BKMK_CaptureRestoreUserState"></a> Comment capturer et restaurer des données d’état utilisateur  
 Pour capturer et restaurer l’état utilisateur, vous devez ajouter les étapes suivantes à la séquence de tâches :  

-   **Demander le magasin d’état**: cette étape est nécessaire seulement si vous stockez l’état utilisateur sur le point de migration d’état.  

-   **Capturer l’état utilisateur**: cette étape capture les données d’état utilisateur et les stocke sur le point de migration d’état ou localement à l’aide de liens.  

-   **Restaurer l’état utilisateur**: cette étape restaure les données d’état utilisateur sur l’ordinateur de destination. Elle peut récupérer les données à partir d'un point de migration d'état utilisateur ou à partir de l'ordinateur de destination.  

-   **Libérer le magasin d’état**: cette étape est nécessaire seulement si vous stockez l’état utilisateur sur le point de migration d’état. Cette étape supprime ces données du point de migration d'état.  

 Utilisez les procédures suivantes pour ajouter les étapes de séquence de tâches nécessaires pour capturer et restaurer l'état utilisateur. Pour plus d’informations sur la création d’une séquence de tâches, consultez [Gérer les séquences de tâches pour automatiser des tâches](manage-task-sequences-to-automate-tasks.md).  

#### <a name="to-add-task-sequence-steps-to-capture-the-user-state"></a>Pour ajouter des étapes de séquence de tâches afin de capturer l'état utilisateur  

1.  Dans la liste **Séquence de tâches** , sélectionnez une séquence de tâches et cliquez sur **Modifier**.  

2.  Si vous utilisez un point de migration d'état pour stocker l'état utilisateur, ajoutez l'étape **Demander le magasin d'état** à la séquence de tâches. Dans la boîte de dialogue **Éditeur de séquence de tâches** , cliquez sur **Ajouter**, pointez sur **État utilisateur**, puis cliquez sur **Demander le magasin d'état**. Spécifiez les propriétés et les options suivantes pour l'étape **Demander le magasin d'état** , puis cliquez sur **Appliquer**.  

     Dans l'onglet **Propriétés** , spécifiez les options suivantes :  

    -   Entrez un nom et une description pour l'étape.  

    -   Cliquez sur **Capturer l'état à partir de l'ordinateur**.  

    -   Dans la zone **Nombre de tentatives** , spécifiez le nombre de tentatives de la séquence de tâches pour capturer les données d'état utilisateur si une erreur se produit.  

    -   Dans la zone **Délai de nouvelle tentative (en secondes)** , spécifiez le nombre de secondes d'attente avant que la séquence de tâches retente de capturer les données.  

    -   Cochez la case **Si le compte d’ordinateur ne parvient pas à se connecter au magasin d’état, utiliser le compte d’accès réseau** pour indiquer si vous voulez utiliser le [compte d’accès réseau](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA) Configuration Manager pour vous connecter aux données d’état utilisateur.  

     Dans l'onglet **Options** , spécifiez les options suivantes :  

    -   Activez la case à cocher **Continuer en cas d'erreur** si vous souhaitez que la séquence de tâches passe à l'étape suivante si cette étape échoue.  

    -   Spécifiez des conditions qui doivent être remplies avant que la séquence de tâches puisse continuer si une erreur se produit.  

3.  Ajoutez l'étape **Capturer l'état utilisateur** à la séquence de tâches. Dans la boîte de dialogue **Éditeur de séquence de tâches** , cliquez sur **Ajouter**, pointez sur **État utilisateur**, puis cliquez sur **Capturer l'état utilisateur**. Spécifiez les propriétés et les options suivantes pour l'étape **Capturer l'état utilisateur** , puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Lorsque vous ajoutez cette étape à votre séquence de tâches, définissez également la variable de séquence de tâches **OSDStateStorePath** pour indiquer où sont stockées sur les données d'état utilisateur. Si vous stockez l'état utilisateur localement, ne spécifiez pas un dossier racine, car la séquence de tâches risquerait d'échouer. Lorsque vous stockez les données utilisateur localement, utilisez toujours un dossier ou un sous-dossier. Pour plus d’informations sur cette variable, consultez [Variables de l’action de séquence de tâches Capturer l’état utilisateur](../understand/task-sequence-action-variables.md#BKMK_CaptureUserState).  

     Dans l'onglet **Propriétés** , spécifiez les options suivantes :  

    -   Entrez un nom et une description pour l'étape.  

    -   Indiquez l'emplacement du package qui contient les fichiers sources USMT utilisés pour capturer les données d'état utilisateur.  

    -   Spécifiez les profils utilisateur à capturer :  

        -   Cliquez sur **Capturer tous les profils utilisateur à l'aide des options standard** pour capturer tous les profils utilisateur.  

        -   Cliquez sur **Personnaliser la façon dont les profils utilisateur sont capturés** pour spécifier les profils utilisateur individuels à capturer. Sélectionnez le fichier de configuration (miguser.xml, migsys.xml ou migapp.xml) qui contient les informations du profil utilisateur. Vous ne pouvez pas utiliser ici le fichier de configuration config.xml, mais vous pouvez l’ajouter manuellement à la ligne de commande USMT en utilisant les variables OSDMigrageAdditionalCaptureOptions et OSDMigrateAdditionalRestoreOptions.

    -   Sélectionnez **Activer la journalisation documentée** pour spécifier la quantité d'informations à écrire dans des fichiers journaux si une erreur se produit.  

    -   Sélectionnez **Ignorer les fichiers qui utilisent le système de fichiers EFS**.  

    -   Sélectionnez **Copier en utilisant l'accès au système de fichiers** pour spécifier les paramètres suivants :  

        -   **Continuer si certains fichiers ne peuvent pas être capturés**: ce paramètre permet à l’étape de séquence de tâches de continuer le processus de migration même si certains fichiers ne peuvent pas être capturés. Si vous désactivez cette option et qu'un fichier ne peut pas être capturé, l'étape de séquence de tâches échoue. Cette option est activée par défaut.  

        -   **Capturer localement en utilisant des liens au lieu de copier les fichiers**: ce paramètre vous permet d’utiliser la fonctionnalité de migration de lien physique qui est disponible dans USMT 4.0. Ce paramètre est ignoré si vous utilisez des versions d'USMT antérieures à USMT 4.0.  

        -   **Capturer en mode hors-ligne (Windows PE uniquement)**: ce paramètre vous permet de capturer l’état utilisateur à partir de Windows PE sans démarrer le système d’exploitation existant. Ce paramètre est ignoré si vous utilisez des versions d'USMT antérieures à USMT 4.0.  

    -   Sélectionnez **Capturer en utilisant Volume Copy Shadow Service (VSS)**. Ce paramètre est ignoré si vous utilisez des versions d'USMT antérieures à USMT 4.0.  

     Dans l'onglet **Options** , spécifiez les options suivantes :  

    -   Activez la case à cocher **Continuer en cas d'erreur** si vous souhaitez que la séquence de tâches passe à l'étape suivante si cette étape échoue.  

    -   Spécifiez des conditions qui doivent être remplies avant que la séquence de tâches puisse continuer si une erreur se produit.  

4.  Si vous utilisez un point de migration d’état pour stocker l’état utilisateur, ajoutez l’étape [Libérer le magasin d’état](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) à la séquence de tâches. Dans la boîte de dialogue **Éditeur de séquence de tâches** , cliquez sur **Ajouter**, pointez sur **État utilisateur**, puis cliquez sur **Libérer le magasin d'état**. Spécifiez les propriétés et les options suivantes pour l'étape **Libérer le magasin d'état** , puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  L'action de séquence de tâches exécutée avant l'étape **Libérer le magasin d'état** doit être effectuée avec succès avant que l'étape **Libérer le magasin d'état** démarre.  

     Sous l'onglet **Propriétés** , entrez un nom et une description pour l'étape.  

     Sous l'onglet **Options** , spécifiez les options suivantes.  

    -   Activez la case à cocher **Continuer en cas d'erreur** si vous souhaitez que la séquence de tâches passe à l'étape suivante si cette étape échoue.  

    -   Spécifiez des conditions qui doivent être remplies avant que la séquence de tâches puisse continuer si une erreur se produit.  

 Déployez cette séquence de tâches pour capturer l'état utilisateur sur un ordinateur de destination. Pour plus d’informations sur la façon de déployer des séquences de tâches, consultez [Déployer une séquence de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

#### <a name="to-add-task-sequence-steps-to-restore-the-user-state"></a>Pour ajouter des étapes de séquence de tâches afin de restaurer l'état utilisateur  

1.  Dans la liste **Séquence de tâches** , sélectionnez une séquence de tâches et cliquez sur **Modifier**.  

2.  Ajoutez l’étape [Restaurer l’état utilisateur](../understand/task-sequence-steps.md#BKMK_RestoreUserState) à la séquence de tâches. Dans la boîte de dialogue **Éditeur de séquence de tâches** , cliquez sur **Ajouter**, pointez sur **État utilisateur**, puis cliquez sur **Restaurer l'état utilisateur**. Cette étape établit une connexion vers le point de migration d'état. Spécifiez les propriétés et les options suivantes pour l'étape **Restaurer l'état utilisateur** , puis cliquez sur **OK**.  

     Dans l'onglet **Propriétés** , spécifiez les propriétés suivantes :  

    -   Entrez un nom et une description pour l'étape.  

    -   Spécifiez le package qui contient l'outil USMT pour restaurer les données d'état utilisateur.  

    -   Spécifiez les profils utilisateur à restaurer :  

        -   Cliquez sur **Restaurer tous les profils utilisateur capturés présentant des options standard** pour restaurer tous les profils utilisateur.  

        -   Cliquez sur **Personnaliser la restauration des profils utilisateur** pour restaurer des profils utilisateur individuels. Sélectionnez le fichier de configuration (miguser.xml, migsys.xml ou migapp.xml) qui contient les informations du profil utilisateur. Vous ne pouvez pas utiliser ici le fichier de configuration config.xml, mais vous pouvez l’ajouter manuellement à la ligne de commande USMT en utilisant les variables OSDMigrageAdditionalCaptureOptions et OSDMigrateAdditionalRestoreOptions.

    -   Sélectionnez **Restaurer les profils utilisateur de l'ordinateur local** pour fournir un nouveau mot de passe pour les profils restaurés. Vous ne pouvez pas migrer les mots de passe pour les profils locaux.  

        > [!NOTE]  
        >  Quand vous disposez de comptes d’utilisateur locaux, que vous utilisez l’étape [Capturer l’état utilisateur](../understand/task-sequence-steps.md#BKMK_CaptureUserState) et que vous sélectionnez **Capturer tous les profils utilisateur à l’aide des options standard**, vous devez sélectionner le paramètre **Restaurer les profils utilisateur de l’ordinateur local** à l’étape [Restaurer l’état utilisateur](../understand/task-sequence-steps.md#BKMK_RestoreUserState), sinon la séquence de tâches échoue.  

    -   Sélectionnez **Continuer si certains fichiers ne peuvent pas être restaurés** si vous souhaitez que l'étape **Restaurer l'état utilisateur** se poursuive si un fichier ne peut pas être restauré.  

         Si vous stockez l'état utilisateur à l'aide de liens locaux et si la restauration échoue, l'utilisateur administratif peut supprimer manuellement les liens directs qui ont été créés pour stocker les données ou la séquence de tâches peut exécuter l'outil USMTUtils. Si vous utilisez USMTUtils pour supprimer le lien physique, ajoutez l’étape [Redémarrer l’ordinateur](../understand/task-sequence-steps.md#BKMK_RestartComputer) après l’exécution de USMTUtils.  

    -   Sélectionnez **Activer la journalisation documentée** pour spécifier la quantité d'informations à écrire dans des fichiers journaux si une erreur se produit.  

     Dans l'onglet **Options** , spécifiez les options suivantes :  

    -   Activez la case à cocher **Continuer en cas d'erreur** si vous souhaitez que la séquence de tâches passe à l'étape suivante si cette étape échoue.  

    -   Spécifiez des conditions qui doivent être remplies avant que la séquence de tâches puisse continuer si une erreur se produit.  

3.  Si vous utilisez un point de migration d’état pour stocker l’état utilisateur, ajoutez l’étape [Libérer le magasin d’état](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) à la séquence de tâches. Dans la boîte de dialogue **Éditeur de séquence de tâches** , cliquez sur **Ajouter**, pointez sur **État utilisateur**, puis cliquez sur **Libérer le magasin d'état**. Spécifiez les propriétés et les options suivantes pour l'étape **Libérer le magasin d'état** , puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  L'action de séquence de tâches exécutée avant l'étape **Libérer le magasin d'état** doit être effectuée avec succès avant que l'étape **Libérer le magasin d'état** démarre.  

     Sous l'onglet **Propriétés** , entrez un nom et une description pour l'étape.  

     Sous l'onglet **Options** , spécifiez les options suivantes.  

    -   Activez la case à cocher **Continuer en cas d'erreur** si vous souhaitez que la séquence de tâches passe à l'étape suivante si cette étape échoue.  

    -   Spécifiez des conditions qui doivent être remplies avant que la séquence de tâches puisse continuer si une erreur se produit.  

 Déployez cette séquence de tâches pour restaurer l'état utilisateur sur un ordinateur de destination. Pour plus d’informations sur le déploiement de séquences de tâches, consultez [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

## <a name="next-steps"></a>Étapes suivantes
[Surveiller le déploiement de la séquence de tâches](monitor-operating-system-deployments.md#BKMK_TSDeployStatus)
