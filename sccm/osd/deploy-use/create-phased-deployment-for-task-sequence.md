---
title: Créer un déploiement par phases
titleSuffix: Configuration Manager
description: Utilisez des déploiements par phases afin d’automatiser le déploiement de logiciels sur plusieurs regroupements.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ab238b2cf98da3d7ea1e86ef6462a721d7347e8
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39383614"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Créer des déploiements par phases avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements par phases permettent d’automatiser le déploiement coordonné et séquencé de logiciels sur plusieurs regroupements. Par exemple, déployez un logiciel sur un regroupement pilote, puis continuez automatiquement le processus de déploiement en fonction des critères de réussite définis. Créez des déploiements par phases avec deux phases par défaut ou configurer manuellement plusieurs phases. Le déploiement par phases de séquences de tâches ne prend pas en charge l’installation PXE ou à partir d’un support. À compter de la version 1806, créez un déploiement par phases pour une application.<!--1358147-->  

> [!Tip]
> La fonctionnalité de déploiement par phases a été introduite dans la version 1802 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À partir de la version 1806, elle n’est plus en préversion.<!--1356837-->



## <a name="prerequisites"></a>Prérequis

#### <a name="security-scope"></a>Étendue de sécurité
Les déploiements créés par phases ne sont pas visibles pour les utilisateurs administratifs qui ne bénéficient pas de l’étendue de sécurité **Tout**. Pour plus d’informations, consultez [Sécurité et audit](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="distribute-application-content"></a>Distribuer le contenu d’une application
Avant de créer un déploiement par phases pour une application, distribuez le contenu à un point de distribution.<!--518293-->



## <a name="bkmk_settings"></a> Paramètres de phase

Ces paramètres sont propres aux déploiements par phases. Configurez ces paramètres lorsque vous créez ou modifiez les phases afin de contrôler la planification et le comportement du processus de déploiement par phases. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Critères de réussite de la première phase  

- **Pourcentage de réussite du déploiement** : spécifiez le pourcentage d’appareils devant réussir le déploiement pour valider la première phase. Par défaut, cette valeur est de 95 %. En d’autres termes, le site considère que la première phase a réussi lorsque l’état de conformité de 95 % des appareils affiche **Réussite** pour ce déploiement. Le site passe alors à la deuxième phase, et crée un déploiement du logiciel sur le regroupement suivant.  


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Conditions pour commencer la deuxième phase du déploiement après la réussite de la première phase  

- **Commencer automatiquement cette phase après une période de report (en jours)** : choisissez le nombre de jours à attendre avant de commencer la deuxième phase après la réussite de la première. Par défaut, ce délai est d’un jour.  

- **Commencer manuellement la deuxième phase de déploiement** : le site ne commence pas automatiquement la deuxième phase à l’issue de la réussite de la première phase. Si vous choisissez cette option, vous devez démarrer manuellement la deuxième phase. Pour plus d’informations, consultez [Passer à la phase suivante](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > Cette option n’est pas disponible pour les déploiements par phases des applications.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Gradually make this software available over this period of time (in days) [Mettre progressivement ce logiciel à disposition durant cette période (en jours)]
<!--1358578--> À partir de la version 1806, configurez ce paramètre afin de lancer chaque phase progressivement. Ce comportement limite les risques de problèmes de déploiement, et diminue la charge sur le réseau causée par la distribution de contenu auprès des clients. Le site rend le logiciel disponible progressivement en fonction de la configuration de chaque phase. Tous les clients d’une phase donnée ont une échéance qui dépend du moment de la mise à disposition du logiciel. La fenêtre entre la mise à disposition et l’échéance est la même pour tous les clients d’une phase. La valeur par défaut de ce paramètre est zéro. Par défaut, le déploiement n’est donc pas limité. Ne définissez pas une valeur supérieure à 30.<!--SCCMDocs-pr issue 2767--> 


#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurer le comportement à l’échéance par rapport à la date de disponibilité du logiciel  

- **Installation is required as soon as possible** (Installation requise dès que possible) : définissez l’échéance d’installation sur l’appareil au moment où celui-ci est ciblé.  

- **Installation is required after this period of time** (Installation requise au terme de cette période) : définissez l’échéance d’installation à un certain nombre de jours après le ciblage de l’appareil. Par défaut, ce délai est de sept jours.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Créer automatiquement un déploiement à deux phases par défaut

1. Dans la console Configuration Manager, démarrez l’Assistant Créer un déploiement par phases. Cette action varie en fonction du type de logiciel que vous déployez :  

    - **Application** (uniquement dans la version 1806 ou ultérieure) : accédez à **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez **Applications**. Sélectionnez une application existante, puis cliquez sur **Créer un déploiement par phases** dans le ruban.  

    - **Séquence de tâches** : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**. Sélectionnez une séquence de tâches existante, puis cliquez sur **Créer un déploiement par phases** dans le ruban.  

2. Dans la page **Général**, renseignez le champ **Nom** et le champ **Description** (facultatif) pour le déploiement par phases, puis sélectionnez **Créer automatiquement un déploiement en deux phases par défaut**.  

3. Cliquez sur **Parcourir** et sélectionnez un regroupement cible dans les champs **Premier regroupement** et **Deuxième regroupement**. Si vous déployez une séquence de tâches, sélectionnez-la à partir des regroupements d’appareils. Si vous déployez une application, sélectionnez-la à partir des regroupements d’utilisateurs ou d’appareils. Cliquez sur **Suivant**.  

    > [!Important]  
    > L’Assistant Créer un déploiement par phases ne vous avertit pas si un déploiement est potentiellement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) et la note de la section [Déployer une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. Dans la page **Paramètres**, choisissez une option pour chacun des paramètres de planification. Pour plus d’informations, consultez [Paramètres des phases](#bkmk_settings). Cliquez sur **Suivant** quand vous avez terminé.  

5. Dans la page **Phases**, examinez les deux phases créées par l’Assistant pour les regroupements spécifiés. Cliquez sur **Suivant**.   

    > [!Note]  
    > Cette section décrit la procédure à suivre pour créer automatiquement un déploiement en deux phases par défaut. À l’aide de l’Assistant, vous pouvez ajouter, supprimer, réorganiser, modifier ou afficher les phases d’un déploiement par phases. Pour plus d’informations sur ces actions supplémentaires, consultez [Créer un déploiement en plusieurs phases configurées manuellement](#bkmk_manual).  

6. Vérifiez vos sélections sous l’onglet **Résumé**, puis cliquez sur **Suivant** pour continuer l’Assistant.  



## <a name="bkmk_manual"></a> Créer un déploiement en plusieurs phases configurées manuellement
<!--1358148--> 

À compter de la version 1806, vous pouvez créer un déploiement en plusieurs phases configurées manuellement pour une séquence de tâches. Ajoutez jusqu’à 10 phases supplémentaires sous l’onglet **Phases** de l’Assistant Créer un déploiement par phases. 

> [!Note]  
> Il n’est pas possible actuellement de créer des phases manuellement pour une application. L’Assistant crée automatiquement deux phases pour les déploiements d’applications.


1. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.  

2. Cliquez avec le bouton droit sur une séquence de tâches et sélectionnez **Créer un déploiement par phases**.  

3. Dans la page **Général** de l’Assistant Créer un déploiement par phases, renseignez le champ **Nom** et le champ **Description** (facultatif), puis sélectionnez **Configurer manuellement toutes les phases**.  

4. À partir de la page **Phases** de l’Assistant Créer un déploiement par phases, vous pouvez effectuer les actions suivantes :  

    - **Filtrer** la liste des phases de déploiement. Entrez une chaîne de caractères pour rechercher une correspondance (sans respect de la casse) dans les colonnes Ordre, Nom ou Regroupement. 

    - **Ajouter** une nouvelle phase :  

        1. Dans la page **Général** de l’Assistant Ajout de phases, spécifiez un **Nom** pour la phase, puis accédez au **Regroupement de phases** cible. Les paramètres supplémentaires disponibles dans cette page sont les mêmes que lors d’un déploiement standard d’une séquence de tâches.  

        2. Dans la page **Paramètres de phase** de l’Assistant Ajout de phases, définissez les paramètres de planification, puis sélectionnez **Suivant** quand vous avez terminé. Pour plus d’informations, consultez [Paramètres](#bkmk_settings).   

            > [!Note]  
            > Vous ne pouvez pas modifier le paramètre de phase **Pourcentage de réussite du déploiement** pour la première phase. Ce paramètre s’applique uniquement aux phases précédées d’une autre phase.  

        3. Les paramètres disponibles dans les pages **Expérience utilisateur** et **Points de distribution** de l’Assistant Ajout de phases sont les mêmes que lors d’un déploiement standard d’une séquence de tâches.  

        4. Vérifiez les paramètres définis dans la page **Résumé**, puis continuez l’Assistant Ajout de phases.  

    - **Modifier** : pour modifier une phase que vous avez ajoutée, sélectionnez la phase, puis cliquez sur ce bouton. Cette action ouvre la fenêtre Propriétés de la phase, qui affiche les mêmes onglets que les pages de l’Assistant Ajout de phases.  

    - **Supprimer** : pour supprimer une phase existante, sélectionnez la phase, puis cliquez sur ce bouton.  

       > [!Warning]  
       > Il n’y a pas de message de confirmation, et vous ne pouvez pas annuler cette action.  

    - **Monter** ou **Descendre** : l’Assistant classe les phases dans l’ordre où vous les ajoutez. La dernière phase ajoutée est placée en bas de la liste. Pour changer l’ordre, sélectionnez une phase, puis cliquez sur l’un de ces boutons pour déplacer la phase à l’endroit voulu dans la liste.  

       > [!Important]  
       > Vérifiez les paramètres des phases après avoir changé l’ordre. Assurez-vous notamment que les paramètres suivants sont toujours corrects par rapport aux exigences de votre déploiement par phases :  
       > 
       > - Critères de réussite de la phase précédente  
       > - Conditions pour commencer cette phase de déploiement après la réussite de la phase précédente   

5. Cliquez sur **Suivant**. Vérifiez les paramètres définis dans la page **Résumé**, puis continuez l’Assistant Créer un déploiement par phases.  


Après avoir créé un déploiement par phases, affichez ses propriétés pour apporter les modifications nécessaires :  

- **Ajoutez** des phases supplémentaires à un déploiement par phases existant.  

- Si une phase n’est pas active, vous pouvez la **modifier**, la **supprimer**, ou la **déplacer** vers le haut ou le bas. Vous ne pouvez toutefois pas la déplacer avant une phase active.  

- Une phase active est en lecture seule. Vous ne pouvez pas la modifier, la supprimer ou la déplacer dans la liste. Vous pouvez uniquement **afficher** les propriétés de la phase.  

- Le déploiement d’une application par phases est toujours en lecture seule.  



## <a name="next-steps"></a>Étapes suivantes
[Gérer et surveiller les déploiements par phases](/sccm/osd/deploy-use/manage-monitor-phased-deployments)
