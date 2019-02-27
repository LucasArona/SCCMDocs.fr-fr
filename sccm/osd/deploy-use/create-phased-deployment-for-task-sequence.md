---
title: Créer des déploiements par phases
titleSuffix: Configuration Manager
description: Utilisez des déploiements par phases afin d’automatiser le déploiement de logiciels sur plusieurs regroupements.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9107e3bf851ddbcec061eeeac064f31e7392ee9f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142440"
---
# <a name="create-phased-deployments-with-configuration-manager"></a>Créer des déploiements par phases avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements par phases permettent d’automatiser le déploiement coordonné et séquencé de logiciels sur plusieurs regroupements. Par exemple, déployez un logiciel sur un regroupement pilote, puis continuez automatiquement le processus de déploiement en fonction des critères de réussite définis. Créez des déploiements par phases avec deux phases par défaut ou configurer manuellement plusieurs phases. 

Créez des déploiements par phases pour les objets suivants :
- **Séquence de tâches**  
    - Le déploiement par phases de séquences de tâches ne prend pas en charge l’installation PXE ou à partir d’un support.   
- **Application** (à compter de la version 1806) <!--1358147-->  
- **Mise à jour logicielle** (à compter de la version 1810) <!--1358146-->  
    - Vous ne pouvez pas utiliser une règle de déploiement automatique avec un déploiement par phases.

> [!Tip]  
> La fonctionnalité de déploiement par phases a été introduite dans la version 1802 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À partir de la version 1806, elle n’est plus en préversion.<!--1356837-->  



## <a name="prerequisites"></a>Prérequis

#### <a name="security-scope"></a>Étendue de sécurité
Les déploiements créés par phases ne sont pas visibles pour les utilisateurs administratifs qui ne bénéficient pas de l’étendue de sécurité **Tout**. Pour plus d’informations, consultez [Sécurité et audit](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="distribute-content"></a>Distribuer du contenu
Avant de créer un déploiement par phases, distribuez le contenu associé à un point de distribution.<!--518293-->  

- **Application** : sélectionnez l’application cible dans la console et utilisez l’action **Distribuer du contenu** dans le ruban. Pour plus d’informations, consultez [Déployer et gérer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content).   

- **Séquence de tâches** : vous devez créer des objets référencés tels que le package de mise à niveau du système d’exploitation avant de créer la séquence de tâches. Distribuez ces objets avant de créer un déploiement. Utilisez l’action **Distribuer du contenu** sur chaque objet, ou la séquence de tâches. Pour afficher l’état de tout le contenu référencé, sélectionnez la séquence de tâches et passez à l’onglet **Références** dans le volet d’informations. Pour plus d’informations, consultez le type d’objet spécifique dans [Préparer un déploiement de système d’exploitation](/sccm/osd/get-started/prepare-for-operating-system-deployment).   

- **Mise à jour logicielle** : créez le package de déploiement et distribuez-le. Utilisez l’Assistant Téléchargement des mises à jour logicielles. Pour plus d’informations, consultez [Télécharger les mises à jour logicielles](/sccm/sum/deploy-use/download-software-updates).  



## <a name="bkmk_settings"></a> Paramètres de phase

Ces paramètres sont propres aux déploiements par phases. Configurez ces paramètres lorsque vous créez ou modifiez les phases afin de contrôler la planification et le comportement du processus de déploiement par phases. 


#### <a name="criteria-for-success-of-the-first-phase"></a>Critères de réussite de la première phase  

- **Pourcentage de réussite du déploiement** : spécifiez le pourcentage d’appareils devant réussir le déploiement pour valider la première phase. Par défaut, cette valeur est de 95 %. En d’autres termes, le site considère que la première phase a réussi lorsque l’état de conformité de 95 % des appareils affiche **Réussite** pour ce déploiement. Le site passe alors à la deuxième phase, et crée un déploiement du logiciel sur le regroupement suivant.  


#### <a name="conditions-for-beginning-second-phase-of-deployment-after-success-of-the-first-phase"></a>Conditions pour commencer la deuxième phase du déploiement après la réussite de la première phase  

- **Commencer automatiquement cette phase après une période de report (en jours)** : choisissez le nombre de jours d’attente avant de passer à la deuxième phase après la réussite de la première phase. Par défaut, ce délai est d’un jour.  

- **Commencer manuellement la deuxième phase de déploiement** : le site ne commence pas automatiquement la deuxième phase à l’issue de la réussite de la première phase. Si vous choisissez cette option, vous devez démarrer manuellement la deuxième phase. Pour plus d’informations, consultez [Passer à la phase suivante](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_move).  

    > [!Note]  
    > Cette option n’est pas disponible pour les déploiements par phases des applications.  


#### <a name="gradually-make-this-software-available-over-this-period-of-time-in-days"></a>Gradually make this software available over this period of time (in days) [Mettre progressivement ce logiciel à disposition durant cette période (en jours)]
<!--1358578--> À partir de la version 1806, configurez ce paramètre afin de lancer chaque phase progressivement. Ce comportement limite les risques de problèmes de déploiement, et diminue la charge sur le réseau causée par la distribution de contenu auprès des clients. Le site rend le logiciel disponible progressivement en fonction de la configuration de chaque phase. Tous les clients d’une phase donnée ont une échéance qui dépend du moment de la mise à disposition du logiciel. La fenêtre entre la mise à disposition et l’échéance est la même pour tous les clients d’une phase. La valeur par défaut de ce paramètre est zéro. Par défaut, le déploiement n’est donc pas limité. Ne définissez pas une valeur supérieure à 30.<!--SCCMDocs-pr issue 2767--> 


#### <a name="configure-the-deadline-behavior-relative-to-when-the-software-is-made-available"></a>Configurer le comportement à l’échéance par rapport à la date de disponibilité du logiciel  

- **L’installation est nécessaire dès que possible** : l’échéance d’installation sur l’appareil correspond au moment où celui-ci est ciblé.  

- **L’installation est nécessaire après cette période de temps** : l’échéance d’installation correspond à un certain nombre de jours après que l’appareil a été ciblé. Par défaut, ce délai est de sept jours.   


<!--### Examples
Include a timeline diagram
-->



## <a name="bkmk_auto"></a> Créer automatiquement un déploiement à deux phases par défaut

1. Dans la console Configuration Manager, démarrez l’Assistant Créer un déploiement par phases. Cette action varie en fonction du type de logiciel que vous déployez :  

    - **Application** (uniquement dans les versions 1806 ou ultérieures) : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion d’applications** et sélectionnez **Applications**. Sélectionnez une application existante, puis choisissez **Créer un déploiement par phases** dans le ruban.  

    - **Mise à jour logicielle** (uniquement dans les versions 1810 ou ultérieures) : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles** et sélectionnez **Toutes les mises à jour logicielles**. Sélectionnez une ou plusieurs mises à jour, puis choisissez **Créer un déploiement par phases** dans le ruban.  

        Cette action est disponible pour les mises à jour logicielles à partir des nœuds suivants :  
        - mises à jour logicielles  
            - **Toutes les mises à jour logicielles**  
            - **Groupes de mises à jour logicielles**   
        - Maintenance de Windows 10, **toutes les mises à jour Windows 10**  
        - Gestion des clients Office 365, **mises à jour Office 365**  

    - **Séquence de tâches** : accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**. Sélectionnez une séquence de tâches existante, puis choisissez **Créer un déploiement par phases** dans le ruban.  

2. Dans la page **Général**, renseignez le champ **Nom** et le champ **Description** (facultatif) pour le déploiement par phases, puis sélectionnez **Créer automatiquement un déploiement en deux phases par défaut**.  

3. Sélectionnez **Parcourir** et choisissez un regroupement cible dans les champs **Premier regroupement** et **Deuxième regroupement**. Pour une séquence de tâches et des mises à jour logicielles, sélectionnez-les à partir des regroupements d’appareils. Si vous déployez une application, sélectionnez-la à partir des regroupements d’utilisateurs ou d’appareils. Sélectionnez **Suivant**.  

    > [!Important]  
    > L’Assistant Créer un déploiement par phases ne vous avertit pas si un déploiement est potentiellement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments) et la note de la section [Déployer une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

4. Dans la page **Paramètres**, choisissez une option pour chacun des paramètres de planification. Pour plus d’informations, consultez [Paramètres de phase](#bkmk_settings). Sélectionnez **Suivant** une fois terminé.  

5. Dans la page **Phases**, examinez les deux phases créées par l’Assistant pour les regroupements spécifiés. Sélectionnez **Suivant**.   

    > [!Note]  
    > Cette section décrit la procédure à suivre pour créer automatiquement un déploiement en deux phases par défaut. À l’aide de l’Assistant, vous pouvez ajouter, supprimer, réorganiser, modifier ou afficher les phases d’un déploiement par phases. Pour plus d’informations sur ces actions supplémentaires, consultez [Créer un déploiement en plusieurs phases configurées manuellement](#bkmk_manual).  

6. Confirmez vos sélections sous l’onglet **Résumé**, puis sélectionnez **Suivant** pour continuer l’Assistant.  



## <a name="bkmk_manual"></a> Créer un déploiement en plusieurs phases configurées manuellement
<!--1358148--> 

À compter de la version 1806, vous pouvez créer un déploiement en plusieurs phases configurées manuellement pour une séquence de tâches. Ajoutez jusqu’à 10 phases supplémentaires sous l’onglet **Phases** de l’Assistant Créer un déploiement par phases. 

> [!Note]  
> Il n’est pas possible actuellement de créer des phases manuellement pour une application. L’Assistant crée automatiquement deux phases pour les déploiements d’applications.


1. Démarrez l’Assistant Création d’un déploiement par phases pour une séquence de tâches ou des mises à jour logicielles.  

2. Dans la page **Général** de l’Assistant Créer un déploiement par phases, renseignez le champ **Nom** et le champ **Description** (facultatif), puis sélectionnez **Configurer manuellement toutes les phases**.  

3. À partir de la page **Phases** de l’Assistant Créer un déploiement par phases, vous pouvez effectuer les actions suivantes :  

    - **Filtrer** la liste des phases de déploiement. Entrez une chaîne de caractères pour rechercher une correspondance (sans respect de la casse) dans les colonnes Ordre, Nom ou Regroupement. 

    - **Ajouter** une nouvelle phase :  

        1. Dans la page **Général** de l’Assistant Ajout de phases, spécifiez un **Nom** pour la phase, puis accédez au **Regroupement de phases** cible. Les paramètres supplémentaires disponibles dans cette page sont les mêmes que lors d’un déploiement standard d’une séquence de tâches ou de mises à jour logicielles.  

        2. Dans la page **Paramètres de phase** de l’Assistant Ajout de phases, définissez les paramètres de planification, puis sélectionnez **Suivant** quand vous avez terminé. Pour plus d’informations, consultez [Paramètres](#bkmk_settings).   

            > [!Note]  
            > Vous ne pouvez pas modifier le paramètre de phase **Pourcentage de réussite du déploiement** pour la première phase. Ce paramètre s’applique uniquement aux phases précédées d’une autre phase.  

        3. Les paramètres disponibles dans les pages **Expérience utilisateur** et **Points de distribution** de l’Assistant Ajout de phases sont les mêmes que lors d’un déploiement standard d’une séquence de tâches ou de mises à jour logicielles.  

        4. Vérifiez les paramètres définis dans la page **Résumé**, puis continuez l’Assistant Ajout de phases.  

    - **Modifier** : cette action ouvre la fenêtre Propriétés de la phase sélectionnée, qui affiche les mêmes onglets que les pages de l’Assistant Ajout de phases.  

    - **Supprimer** : cette action supprime la phase sélectionnée.  

       > [!Warning]  
       > Il n’y a pas de message de confirmation, et vous ne pouvez pas annuler cette action.  

    - **Monter** ou **Descendre** : l’Assistant classe les phases dans l’ordre où vous les ajoutez. La dernière phase ajoutée est placée en bas de la liste. Pour changer l’ordre, sélectionnez une phase, puis utilisez ces boutons pour déplacer la phase à l’endroit voulu dans la liste.  

       > [!Important]  
       > Vérifiez les paramètres des phases après avoir changé l’ordre. Assurez-vous notamment que les paramètres suivants sont toujours corrects par rapport aux exigences de votre déploiement par phases :  
       > 
       > - Critères de réussite de la phase précédente  
       > - Conditions pour commencer cette phase de déploiement après la réussite de la phase précédente   

5. Sélectionnez **Suivant**. Vérifiez les paramètres définis dans la page **Résumé**, puis continuez l’Assistant Créer un déploiement par phases.  


Après avoir créé un déploiement par phases, affichez ses propriétés pour apporter les modifications nécessaires :  

- **Ajoutez** des phases supplémentaires à un déploiement par phases existant.  

- Si une phase n’est pas active, vous pouvez la **modifier**, la **supprimer**, ou la **déplacer** vers le haut ou le bas. Vous ne pouvez toutefois pas la déplacer avant une phase active.  

- Une phase active est en lecture seule. Vous ne pouvez pas la modifier, la supprimer ou la déplacer dans la liste. Vous pouvez uniquement **afficher** les propriétés de la phase.  

- Le déploiement d’une application par phases est toujours en lecture seule.  



## <a name="next-steps"></a>Étapes suivantes

Gérez et supervisez les déploiements par phases :
- [Application](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  
- [Mise à jour logicielle](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/sum/toc.json&bc=/sccm/sum/breadcrumb/toc.json)  
- [Séquence de tâches](/sccm/osd/deploy-use/manage-monitor-phased-deployments)  

