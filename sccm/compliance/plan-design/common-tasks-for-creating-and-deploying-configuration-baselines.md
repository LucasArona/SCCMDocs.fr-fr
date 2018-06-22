---
title: 'Tâches courantes de bases de référence de configuration '
titleSuffix: Configuration Manager
description: Découvrez comment créer et déployer des bases de référence de configuration System Center Configuration Manager.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bd76ecfcd4f5731e7fa078a00e79fdc6ab91ffa4
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333499"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-system-center-configuration-manager"></a>Tâches courantes de création et de déploiement de bases de référence de configuration avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique inclut des scénarios courants pour vous permettre de vous familiariser avec la création et le déploiement de bases de référence de configuration System Center Configuration Manager.  

 Si vous connaissez déjà les paramètres de compatibilité, vous trouverez une documentation détaillée sur toutes les fonctionnalités que vous utilisez dans les rubriques [Créer des bases de référence de configuration](../../compliance/deploy-use/create-configuration-baselines.md) et [Déployer des bases de référence de configuration](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Avant de commencer, lisez [Bien démarrer avec les paramètres de compatibilité dans System Center Configuration Manager](../../compliance/get-started/get-started-with-compliance-settings.md) pour apprendre les notions de base sur les paramètres de compatibilité, et lisez également [Planifier et configurer les paramètres de compatibilité](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md) pour implémenter tous les prérequis.  

## <a name="create-a-configuration-baseline"></a>Créer une base de référence de configuration  
 Dans cet exemple, vous avez créé un élément de configuration uniquement pour les ordinateurs Windows 10 qui exécutent le client Configuration Manager.  

 Cet élément de configuration met en œuvre un mot de passe obligatoire d’au moins 6 caractères sur les ordinateurs Windows 10. L’élément de configuration est nommé **Mise en œuvre de mot de passe Windows 10**.  

Utilisez la procédure suivante pour apprendre à ajouter cet élément de configuration à une base de référence de configuration pour la préparer au déploiement.  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Lignes de base de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une ligne de base de configuration**.  

4.  Dans la boîte de dialogue **Créer une base de référence de configuration**, configurez les paramètres suivants :  

    -   **Nom** : entrez **Mots de passe Windows 10** (ou un autre nom de votre choix).  

5.  Cliquez sur **Ajouter** > **Éléments de Configuration**.  

6.  Dans la boîte de dialogue **Ajouter des éléments de configuration** , sélectionnez l’élément de configuration **Mise en œuvre de mot de passe Windows 10** que vous avez précédemment créé, puis cliquez sur **Ajouter**.  

7.  Cliquez sur OK pour fermer la boîte de dialogue **Ajouter des éléments de configuration** et revenir à la boîte de dialogue **Créer une base de référence de configuration**.

8.  Cliquez sur **OK** pour fermer la boîte de dialogue **Créer une ligne de base de configuration** .  

 Vous pouvez maintenant voir la base de référence de configuration dans le nœud **Bases de référence de configuration** de la console Configuration Manager.  

## <a name="deploy-the-configuration-baseline"></a>Déployer la base de référence de configuration  
 Dans cet exemple, vous déployez la base de référence de configuration que vous avez créée au cours de la procédure précédente sur un regroupement d’ordinateurs.  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Lignes de base de configuration**.  

3.  Dans la liste des bases de référence de configuration, sélectionnez **Mots de passe Windows 10**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

5.  Dans la boîte de dialogue **Déployer des bases de référence de configuration**, configurez les paramètres suivants :  

    -   **Lignes de base de configuration sélectionnées** : vérifiez que la base de référence de configuration **Mots de passe Windows 10** a été automatiquement ajoutée à cette liste.  

    -   **Résoudre les règles non conformes lorsqu’elles sont prises en charge** : cochez cette case pour veiller à ce que, si les paramètres appropriés ne sont pas présents sur les appareils ciblés, ils soient corrigés par Configuration Manager.  

    -   **Regroupement** : cliquez sur **Parcourir** pour choisir le regroupement d’ordinateurs sur lequel la base de référence de configuration est évaluée et corrigée à des fins de compatibilité. Dans cet exemple, la base de référence de configuration a été déployée sur le regroupement **Tous les clients bureau et serveur** intégré.  

        > [!TIP]  
        >  Ne vous inquiétez pas si le regroupement que vous choisissez contient des ordinateurs ou périphériques qui n’exécutent pas Windows 10. Tant que vous avez configuré des plateformes prises en charge dans l’élément de configuration que vous avez créé, la compatibilité des seuls ordinateurs Windows 10 est évaluée.  

    -   Si nécessaire, configurez la planification selon laquelle la base de référence de configuration est évaluée. Sinon, conservez la valeur par défaut de **7 jours**.  

7.  Cliquez sur **OK** pour fermer la boîte de dialogue **Déployer des lignes de base de configuration** et créer le déploiement.  

 Pour examiner rapidement les statistiques de compatibilité de ce déploiement, dans l’espace de travail **Surveillance** , cliquez sur **Déploiements**. Au bas de l’écran, un graphique **Statistiques de compatibilité** est visible.  

## <a name="next-steps"></a>Étapes suivantes 

Pour plus d’informations sur la surveillance des bases de référence de configuration, consultez [Surveiller les paramètres de compatibilité](../../compliance/deploy-use/monitor-compliance-settings.md).  
