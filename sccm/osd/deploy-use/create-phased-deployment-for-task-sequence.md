---
title: Créer un déploiement par phases pour une séquence de tâches
titleSuffix: Configuration Manager
description: Créer des déploiements par phases pour des séquences de tâches
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: b634ff68-b909-48d2-9e2c-0933486673c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2bda41cfd01e5ef90771350e650f68a27c3af6ed
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-phased-deployments-for-a-task-sequence-with-system-center-configuration-manager"></a>Créer des déploiements par phases pour une séquence de tâches avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les déploiements par phases automatisent le lancement coordonné et séquencé d’une séquence de tâches sur plusieurs regroupements. Vous pouvez créer des déploiements par phases avec deux phases par défaut ou configurer manuellement plusieurs phases. Le déploiement par phrases des séquences de tâches ne prend pas en charge l’installation PXE ou à partir d’un support. 

>[!NOTE]
> Les déploiements par phases sont une fonctionnalité en préversion introduite dans Configuration Manager 1802. <!--1356837-->

## <a name="security-scope-and-log-file-information"></a>Étendue de sécurité et informations de fichier journal

**Étendue de sécurité** :</br>
Les déploiements créés par phases ne sont pas visibles pour les personnes qui n’ont pas l’étendue de sécurité **Tout**.

**Fichiers journaux** : </br>
SMS_PhasedDeployment.log

## <a name="create-a-default-two-phased-deployment-for-a-task-sequence"></a>Créer un déploiement à deux phases par défaut pour une séquence de tâches

Utilisez les instructions suivantes pour créer un déploiement par phases. 

1. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.

2. Cliquez avec le bouton droit sur une séquence de tâches et sélectionnez **Créer un déploiement par phases**. 

3. Sous l’onglet **Général**, donnez un nom et une description (facultative) au déploiement par phases, puis sélectionnez **Créer automatiquement un déploiement en deux phases par défaut**. 

4. Renseignez les champs **Premier regroupement** et **Deuxième regroupement**. Sélectionnez **Suivant**.

5. Sous l’onglet **Paramètres**, choisissez une option pour chacun des paramètres de planification, puis sélectionnez **Suivant** quand vous avez terminé. 
    - **Critères de réussite de la première phase.** 
        - **Pourcentage de réussite du déploiement** : Spécifiez le pourcentage d’appareils qui exécutent le déploiement conformément aux critères de réussite de la phase. 
    - **Conditions de lancement de la deuxième phase du déploiement après la réussite de la première phase** (choisissez une condition) :
        - **Commencer automatiquement cette phase après une période de report (en jours)** : Choisissez le nombre de jours à attendre avant de commencer la deuxième phase après la réussite de la première. 
        - **Commencer manuellement la deuxième phase de déploiement** : Ne pas commencer automatiquement la deuxième phase après la réussite de la première. Demander à ce qu’elle soit démarrée manuellement. 
    - **Une fois qu’un appareil est ciblé, installer le logiciel** (choisissez une proposition) :
        - **Dès que possible** : Définit l’échéance d’installation sur l’appareil sur le moment où il est ciblé.
        - **Heure d’échéance (par rapport à l’heure de ciblage de l’appareil)** : Définit l’échéance d’installation sur un certain nombre de jours après le ciblage de l’appareil. 

6. Sous l’onglet **Phases**, cliquez sur la première phase, puis sur **Modifier**.  Spécifiez **Expérience utilisateur**, ainsi que **Notifications utilisateur** et **Traitement des filtres d’écriture pour les appareils Windows Embedded**. Cliquez sur **Appliquer**.

7. Spécifiez les paramètres des **Points de distribution** de la phase sous l’onglet **Points de Distribution**. Cliquez sur **Appliquer** et sur **OK**.        

8. Sous l’onglet **Phases**, modifiez la deuxième phase pour **Expérience utilisateur** et **Points de distribution**. Cliquez sur **Appliquer** et sur **OK**.

9. Vérifiez vos sélections sous l’onglet **Récapitulatif**, puis cliquez sur **Suivant** pour continuer à exécuter l’Assistant.

>[!WARNING]
>Les déploiements par phases ne vous indiquent pas si le déploiement d’une séquence de tâches est [à haut risque](/sccm/protect/understand/settings-to-manage-high-risk-deployments.md). 


## <a name="suspend-and-resume-phases-or-move-to-the-next-phase"></a>Suspendre et reprendre les phases ou passer à la phase suivante
Vous pouvez parfois devoir suspendre manuellement un déploiement par phases, reprendre un déploiement par phases suspendu ou passer à la phase suivante. 

### <a name="move-to-the-next-phase"></a>Passer à la phase suivante
Quand vous sélectionnez le paramètre **Commencer manuellement la deuxième phase de déploiement**, vous devez démarrer la deuxième phase. Utilisez les instructions suivantes pour passer à la deuxième phase : 

1. Dans la console Configuration Manager, sélectionnez **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis cliquez sur **Séquences de tâches**.
2. Mettez en surbrillance la séquence de tâches.
3. Cliquez sur l’onglet **Déploiement par phases** en bas de la console. 
4. Cliquez avec le bouton droit sur le déploiement par phases et sélectionnez **Passer à la phase suivante**.
![Suspendre, reprendre ou passer à la phase suivante](media/Suspend-phased-deployment.PNG)

### <a name="suspend-or-resume-a-phased-deployment"></a>Suspendre ou reprendre un déploiement par phases
1. Dans la console Configuration Manager, sélectionnez **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis cliquez sur **Séquences de tâches**.
2. Mettez en surbrillance la séquence de tâches, puis cliquez sur l’onglet **Déploiement par phases** en bas de la console. 
3. Sélectionnez le déploiement par phases et cliquez sur **Suspendre** ou **Reprendre** dans le ruban.

## <a name="next-steps"></a>Étapes suivantes
[Créer une séquence de tâches personnalisée](create-a-custom-task-sequence.md) </br>
[Créez une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation](create-a-task-sequence-for-non-operating-system-deployments.md). 








