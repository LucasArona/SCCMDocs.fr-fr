---
title: Créer et appliquer des modes de gestion de l’alimentation
titleSuffix: Configuration Manager
description: Créez et appliquez des modes de gestion de l’alimentation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 4504f26f8f6288750d36028d8eb795ae0d839fbc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336219"
---
# <a name="how-to-create-and-apply-power-plans-in-system-center-configuration-manager"></a>Comment créer et appliquer des modes de gestion de l’alimentation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La gestion de l’alimentation dans System Center Configuration Manager vous permet d’appliquer les modes de gestion de l’alimentation fournis avec Configuration Manager à des regroupements d’ordinateurs de votre hiérarchie, ou de créer vos propres modes de gestion de l’alimentation personnalisés. Procédez comme indiqué dans cette rubrique pour appliquer un mode d'alimentation intégré ou personnalisé aux ordinateurs.  

> [!IMPORTANT]  
>  Vous pouvez uniquement appliquer les modes de gestion de l’alimentation Configuration Manager à des regroupements d’appareils.  

 Si un ordinateur est membre de plusieurs regroupements, chacun appliquant des modes de gestion de l'alimentation différents, les actions suivantes sont effectuées :  

-   Mode de gestion de l’alimentation : si plusieurs valeurs sont appliquées à un ordinateur en tant que paramètres d’alimentation, la valeur la moins restrictive est utilisée.  

-   Heure de sortie de veille : si plusieurs heures d’éveil sont appliquées à un ordinateur de bureau, l’heure la plus proche de minuit est utilisée.  

 Utilisez le rapport **Ordinateurs avec plusieurs modes de gestion de l'alimentation** pour afficher tous les ordinateurs auxquels sont appliqués plusieurs modes d'alimentation. Cela peut vous aider à détecter les ordinateurs qui présentent des conflits de l'alimentation. Pour plus d’informations sur les rapports de gestion de l’alimentation, consultez [Comment surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Les paramètres d’alimentation configurés à l’aide de la stratégie de groupe Windows remplacent les paramètres configurés par la gestion de l’alimentation Configuration Manager.  

 Procédez comme suit pour créer et appliquer un mode de gestion de l’alimentation Configuration Manager.  

### <a name="to-create-and-apply-a-power-plan"></a>Pour créer et appliquer un mode d'alimentation  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Regroupements de périphériques**.  

3.  Dans la liste **Regroupements de périphériques** , cliquez sur le regroupement auquel vous souhaitez appliquer les paramètres de gestion de l'alimentation, puis, dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Sous l’onglet **Gestion de l’alimentation** de la boîte de dialogue *Propriétés de <nom_regroupement\>*, sélectionnez **Spécifier les paramètres de gestion de l’alimentation de ce regroupement**.  

    > [!NOTE]  
    >  Vous pouvez également cliquer sur **Parcourir** , puis copier les paramètres de gestion de l'alimentation à partir d'un regroupement sélectionné vers le regroupement sélectionné.  

5.  Dans les champs **Début** et **Fin** , spécifiez l'heure de début et l'heure de fin des heures de pointe (ou de bureau).  

6.  Activez **Heure de reprise (ordinateurs de bureau)** pour indiquer une heure de sortie du mode veille ou du mode veille prolongée d'un ordinateur de bureau afin d'installer des mises à jour planifiées ou des logiciels.  

    > [!IMPORTANT]  
    >  La gestion de l'alimentation utilise la fonction d'heure de reprise Windows interne pour sortir les ordinateurs du mode veille ou du mode veille prolongée. Les paramètres de l’heure de sortie de veille ne sont pas appliqués aux ordinateurs portables afin d’éviter qu’ils ne sortent de veille alors qu’ils ne sont pas branchés. L’heure de sortie de veille est aléatoire et les ordinateurs peuvent sortir de veille pendant une heure à partir de l’heure de sortie de veille spécifiée.  

7.  Si vous souhaitez configurer un mode d'alimentation personnalisé pour les heures de pointe (ou de bureau), sélectionnez **Pic personnalisé (ConfigMgr)** dans la liste déroulante **Mode forte alimentation** , puis cliquez sur **Modifier**. Si vous souhaitez configurer un mode d'alimentation pour les heures creuses, sélectionnez **Non-pic personnalisé (ConfigMgr)** dans la liste déroulante **Faible alimentation** , puis cliquez sur **Modifier**.  

    > [!NOTE]  
    >  Vous pouvez utiliser le rapport **Activité de l'ordinateur** pour vous aider à déterminer les planifications à utiliser pour les heures de pointe et les heures creuses lorsque vous appliquez des modes d'alimentation à des regroupements d'ordinateurs. Pour plus d’informations, consultez [Guide pratique pour surveiller et planifier la gestion de l’alimentation dans System Center Configuration Manager](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

     Vous pouvez également sélectionner dans les modes d'alimentation intégrés, **Équilibré (ConfigMgr)**, **Hautes performances (ConfigMgr)** ou **Économiseur d'énergie (ConfigMgr)**, puis cliquer sur **Afficher** pour afficher les propriétés de chaque mode d'alimentation.  

    > [!NOTE]  
    >  Vous ne pouvez pas modifier les modes d'alimentation intégrés.  

8.  Dans la boîte de dialogue *Propriétés de <nom_mode_gestion_alimentation\>*, configurez les paramètres suivants :  

    -   **Nom** : spécifiez un nom pour ce mode de gestion de l’alimentation ou utilisez la valeur par défaut fournie.  

    -   **Description**  : spécifiez une description pour ce mode de gestion de l’alimentation ou utilisez la valeur par défaut fournie.  

    -   **Spécifier les propriétés pour ce mode d’alimentation** : configurez les propriétés du mode de gestion de l’alimentation. Pour désactiver une propriété, désactivez sa case. Pour plus d’informations sur les paramètres disponibles, consultez [Paramètres du mode de gestion de l’alimentation disponibles](#BKMK_Plans) dans cette rubrique.  

        > [!IMPORTANT]  
        >  Les paramètres activés sont appliqués aux ordinateurs lorsque le mode d'alimentation est appliqué. Si vous désactivez une case à cocher du paramètre d'alimentation, la valeur sur l'ordinateur client n'est pas modifiée lorsque le mode d'alimentation est appliqué. Le fait de désactiver une case ne permet pas de restaurer la valeur du paramètre d'alimentation sélectionnée avant l'application d'un mode d'alimentation.  

9. Cliquez sur **OK** pour fermer la boîte de dialogue *Propriétés de <nom_mode_gestion_alimentation\>*.  

10. Cliquez sur **OK** pour fermer la boîte de dialogue *Paramètres de <nom_regroupement\>* et pour appliquer le mode de gestion de l’alimentation.  

##  <a name="BKMK_Plans"></a> Available power management plan settings  
 Le tableau suivant répertorie les paramètres de gestion de l’alimentation disponibles dans Configuration Manager. Vous pouvez configurer d'autres paramètres pour les périodes où l'ordinateur est branché ou sur batterie. Selon la version de Windows que vous utilisez, il est possible que certains paramètres ne soient pas configurables.  

> [!NOTE]  
>  Les paramètres d'alimentation que vous ne configurez pas conservent leur valeur actuelle sur les ordinateurs clients.  

|Nom|Description|  
|----------|-----------------|  
|**Désactiver l'affichage après (minutes)**|Spécifie la durée en minutes, pendant laquelle l'ordinateur doit être inactif avant que l'affichage ne soit désactivé. Spécifiez une valeur **0** si vous ne voulez pas que la gestion de l’alimentation désactive l’affichage.|  
|**Mise en veille après (minutes)**|Spécifie la durée en minutes, pendant laquelle l'ordinateur doit être inactif avant d'entrer en mode veille. Spécifiez une valeur **0** si vous ne voulez pas que la gestion de l’alimentation passe l’ordinateur en mode veille.|  
|**Demander un mot de passe à la reprise**|Une valeur **Oui** ou **Non** spécifie si un mot de passe est nécessaire pour déverrouiller l’ordinateur lorsqu’il sort du mode veille.|  
|**Action du bouton d'alimentation**|Spécifie l'action qui est effectuée lorsque l'utilisateur appuie sur le bouton d'alimentation. Spécifie l'action qui se produit lorsque l'utilisateur ferme le capot d'un ordinateur portable. Valeurs possibles **Ne rien faire**, **Mettre en veille**, **Mettre en veille prolongée** et **Arrêter**.|  
|**Bouton de mise sous tension du menu Démarrer**|Spécifie l’action qui se produit quand vous appuyez sur le bouton d’alimentation du menu **Démarrer** de l’ordinateur. Spécifie l'action qui se produit lorsque l'utilisateur ferme le capot d'un ordinateur portable. Valeurs possibles **Mettre en veille**, **Mettre en veille prolongée** et **Arrêter**.|  
|**Action du bouton de mise en veille**|Spécifie l’action qui se produit quand vous appuyez sur le bouton de **mise en veille** de l’ordinateur. Spécifie l'action qui se produit lorsque l'utilisateur ferme le capot d'un ordinateur portable. Valeurs possibles **Ne rien faire**, **Mettre en veille**, **Mettre en veille prolongée** et **Arrêter**.|  
|**Action à la fermeture du capot**|Spécifie l'action qui se produit lorsque l'utilisateur ferme le capot d'un ordinateur portable. Valeurs possibles **Ne rien faire**, **Mettre en veille**, **Mettre en veille prolongée** et **Arrêter**.|  
|**Désactiver le disque dur après (minutes)**|Spécifie la durée en minutes, pendant laquelle le disque dur doit être inactif avant d'être désactivé. Spécifiez une valeur **0** si vous ne voulez pas que la gestion de l’alimentation mette hors tension le disque dur de l’ordinateur.|  
|**Mise en veille prolongée après (minutes)**|Spécifie la durée en minutes, pendant laquelle l'ordinateur doit être inactif avant d'entrer en veille prolongée. Spécifiez une valeur **0** si vous ne voulez pas que la gestion de l’alimentation mette l’ordinateur en veille prolongée.|  
|**Action sur batterie faible**|Spécifie l'action qui se produit lorsque la batterie de l'ordinateur atteint le niveau de notification de batterie faible spécifié. Spécifie l'action qui se produit lorsque l'utilisateur ferme le capot d'un ordinateur portable. Valeurs possibles **Ne rien faire**, **Mettre en veille**, **Mettre en veille prolongée** et **Arrêter**.|  
|**Action sur batterie critique**|Spécifie l'action qui est effectuée lorsque la batterie de l'ordinateur atteint le niveau de notification de batterie critique spécifié. Spécifie l'action qui se produit lorsque l'utilisateur ferme le capot d'un ordinateur portable. Les valeurs possibles incluent **Mettre en veille**, **Mettre en veille prolongée** et **Arrêter**.|  
|**Autoriser la veille hybride**|La sélection de la valeur **Activé** ou **Désactivé** spécifie si Windows doit enregistrer un fichier de mise en veille prolongée lors de l’entrée en mode veille, qui peut être utilisé pour restaurer l’état de l’ordinateur en cas de perte d’alimentation alors qu’il est en veille.<br /><br /> La mise en veille hybride est conçue pour les ordinateurs de bureau et, par défaut, n'est pas activée sur les ordinateurs portables. Sur les ordinateurs qui exécutent Windows 7, la mise en veille hybride désactive la fonctionnalité de mise en veille prolongée.|  
|**Autoriser l'état d'attente lors de l'action de mise en veille**|La sélection de la valeur **Activé** ou **Désactivé** permet à l’ordinateur de se mettre en attente, ce qui consomme toujours du courant, mais permet à l’ordinateur de sortir plus rapidement du mode veille. Si ce paramètre a la valeur **Désactivé**, l’ordinateur peut uniquement être mis en veille prolongée ou mis hors tension.|  
|**Inactivité requise avant la mise en veille (%)**|Spécifie le pourcentage de temps d'inactivité du temps processeur nécessaire à l'ordinateur pour entrer en mode veille. Sur les ordinateurs qui exécutent Windows 7, cette valeur est toujours définie sur **0**.|  
|**Activer le minuteur de réveil Windows pour les ordinateurs de bureau**|La sélection de la valeur **Activer** ou **Désactiver** peut permettre à la gestion de l’alimentation d’utiliser l’horloge Windows intégrée pour sortir un ordinateur de bureau du mode veille. Lorsqu'un ordinateur de bureau quitte le mode veille grâce au minuteur de réveil Windows, il reste actif pendant 10 minutes par défaut afin de laisser le temps à l'ordinateur d'installer toutes les mises à jour ou de recevoir la stratégie.<br /><br /> Les minuteurs de réveil ne sont pas pris en charge sur les ordinateurs portables afin d'éviter les scénarios dans lesquels ils pourraient se mettre en éveil lorsqu'ils ne sont pas branchés.|  
