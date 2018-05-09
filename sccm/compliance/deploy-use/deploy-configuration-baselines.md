---
title: Déployer des bases de référence de configuration
titleSuffix: Configuration Manager
description: Déployez des bases de référence de configuration pour définir les déploiements de bases de référence de configuration et pour ajouter ou supprimer des bases de référence de configuration dans les déploiements.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9be8aaf3-075e-4acd-abd2-7459254e16e2
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c55382bf1fc377fd7e86f433a0cb92a5240eafa1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-configuration-baselines-in-system-center-configuration-manager"></a>Comment déployer des lignes de base de configuration dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les bases de référence de configuration dans System Center Configuration Manager doivent être déployées vers un ou plusieurs regroupements d’utilisateurs ou d’appareils avant que les appareils clients de ces mêmes regroupements ne puissent évaluer leur conformité avec la base de référence de configuration.  

Utilisez la boîte de dialogue **Déployer des lignes de base de configuration** pour définir les déploiements des lignes de base de configuration, y compris l'ajout ou la suppression de lignes de base de configuration dans des déploiements et la définition du calendrier d'évaluation.  

## <a name="deploy-a-configuration-baseline"></a>Déployer une base de référence de configuration  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Lignes de base de configuration**.  

3.  Dans la liste **Lignes de base de configuration** , sélectionnez la ligne de base de configuration que vous souhaitez déployer, puis, dans l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

4.  Dans la boîte de dialogue **Déployer des lignes de base de configuration** , sélectionnez les lignes de base de configuration que vous souhaitez déployer dans la liste **Lignes de base de configuration disponibles** . Cliquez sur **Ajouter** pour ajouter celles-ci à la liste **Lignes de base de configuration sélectionnées** .  

    > [!IMPORTANT]  
    >  Si vous modifiez un élément de configuration qui a été ajouté à une ligne de base de configuration déployée, la conformité de l’élément de configuration révisé ne sera évaluée que lors de sa prochaine évaluation programmée.  

5.  Spécifiez les informations supplémentaires suivantes :  

    -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** : activez cette option pour résoudre automatiquement toutes les règles qui ne sont pas compatibles pour Windows Management Instrumentation (WMI), le Registre, les scripts et tous les paramètres des appareils mobiles inscrits par Configuration Manager.  

    -   **Autoriser les corrections en dehors de la fenêtre de maintenance** : si une fenêtre de maintenance a été configurée pour le regroupement vers lequel vous déployez la ligne de base de configuration, activez cette option pour laisser les paramètres de compatibilité résoudre la valeur en dehors de la fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).  

6.  **Générer une alerte** : configure une alerte qui est générée si la compatibilité de la base de référence de configuration est inférieure à un pourcentage spécifié par une date et une heure spécifiques. Vous pouvez également spécifier si vous souhaitez qu'une alerte soit envoyée à System Center Operations Manager.  

7.  **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement dans lequel vous souhaitez déployer la ligne de base de configuration.  

8.  **Spécifier le calendrier d’évaluation de la compatibilité pour cette ligne de base de configuration** : spécifie le calendrier d’évaluation de la base de référence de configuration déployée sur des ordinateurs clients. Il peut s'agir d'un calendrier simple ou d'un calendrier personnalisé.  

    > [!NOTE]  
    >  Si la ligne de base de configuration est déployée vers un ordinateur, sa conformité est évaluée dans les deux heures suivant l’heure de début que vous programmez. Si elle est déployée vers un utilisateur, sa conformité est évaluée quand l’utilisateur se connecte.  

9. Cliquez sur **OK** pour fermer la boîte de dialogue **Déployer des lignes de base de configuration** et pour créer le déploiement. Pour plus d’informations sur la surveillance du déploiement, consultez [Surveiller les paramètres de compatibilité](/sccm/compliance/deploy-use/monitor-compliance-settings).  
