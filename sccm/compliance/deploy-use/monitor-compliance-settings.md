---
title: Surveiller les paramètres de compatibilité
titleSuffix: Configuration Manager
description: Utilisez une ou plusieurs des procédures de cette rubrique pour afficher l’état de compatibilité de la base de référence de configuration.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 92c1ccca-a748-44cd-a52e-e41d34bf981d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9920bd48ad7b953469261602c21a6664580143a2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335777"
---
# <a name="monitor-compliance-settings-in-system-center-configuration-manager"></a>Surveiller les paramètres de compatibilité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois que vous avez déployé les bases de référence de configuration de System Center Configuration Manager sur les appareils de votre hiérarchie, vous pouvez utiliser une ou plusieurs des procédures de cette rubrique pour afficher l’état de compatibilité d’une base de référence de configuration :

> [!NOTE]  
>  Les champs des critères de validation dans les rapports des paramètres de compatibilité (l’équivalent dans le rapport côté client est **Contraintes**) s’affichent dans le langage SML (Service Modeling Language) sous-jacent. Par conséquent, les administrateurs qui ont créé l’élément de configuration dans la console Configuration Manager qui ne connaissent pas le langage SML peuvent avoir des difficultés à comprendre les critères de validation. Dans ce cas, utilisez l’espace de travail **Surveillance** dans la console Configuration Manager pour afficher les propriétés de l’élément de configuration et ses critères de validation.  

##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Afficher les résultats de compatibilité dans la console Configuration Manager  
 Utilisez cette procédure pour afficher des détails sur la compatibilité des bases de référence de configuration déployées dans la console Configuration Manager.  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Afficher les résultats de compatibilité dans la console Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance** > **Déploiements**.  

3.  Dans la liste **Déploiements** , sélectionnez le déploiement de la ligne de base de configuration pour lequel vous souhaitez vérifier les informations de compatibilité.  

4.  Vous pouvez consulter un résumé des informations relatives à la compatibilité du déploiement de la ligne de base de configuration dans la page principale. Pour afficher des informations plus détaillées, sélectionnez le déploiement de la ligne de base de configuration puis, sous l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Afficher l’état** pour afficher la page **État du déploiement** .  

     La page **État du déploiement** contient les onglets suivants :  

    -   **Compatible**: affiche la compatibilité de la ligne de base de configuration en fonction du nombre de biens affectés. Vous pouvez cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Ressources et Conformité** , qui contient tous les utilisateurs ou appareils conformes à cette règle. Le volet **Détails du bien** affiche les utilisateurs ou les appareils qui sont compatibles avec la base de référence de configuration. Double-cliquez sur un utilisateur ou un appareil de la liste pour afficher des informations supplémentaires.  

        > [!IMPORTANT]  
        >  Une règle d’élément de configuration n’est pas évaluée si elle n’est pas détectée ou si elle n’est pas applicable sur un appareil client. Cependant, la règle est renvoyée comme étant compatible.  

    -   **Erreur**: affiche la liste de toutes les erreurs pour le déploiement de la ligne de base de configuration sélectionné en fonction du nombre de biens affectés. Vous pouvez cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité** , qui contient tous les utilisateurs ou appareils qui ont généré des erreurs avec cette règle. Lorsque vous sélectionnez un utilisateur ou un appareil, le volet **Détails du bien** affiche les utilisateurs ou les appareils qui sont affectés par le problème sélectionné. Double-cliquez sur un utilisateur ou un appareil de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Non compatible**: affiche la liste de toutes les règles non compatibles au sein de la ligne de base de configuration en fonction du nombre de biens affectés. Vous pouvez cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** ou **Périphériques** de l'espace de travail **Biens et conformité** , qui contient tous les utilisateurs ou périphériques qui ne sont pas compatibles avec cette règle. Lorsque vous sélectionnez un utilisateur ou un appareil, le volet **Détails du bien** affiche les utilisateurs ou les appareils qui sont affectés par le problème sélectionné. Double-cliquez sur un utilisateur ou un appareil de la liste pour afficher d'autres informations sur le problème.  

    -   **Inconnu**: affiche la liste de tous les utilisateurs et appareils qui n’ont pas signalé de compatibilité pour le déploiement de la ligne de base de configuration sélectionné avec l’état du client actuel des appareils.  

5.  Sur la page **État du déploiement** , vous pouvez consulter des informations détaillées sur la compatibilité de la ligne de base de configuration déployée. Un nœud temporaire est créé sous le nœud **Déploiements** qui vous aide à retrouver rapidement ces informations.  

##  <a name="view-compliance-results-by-using-reports"></a>Afficher les résultats de compatibilité à l’aide de rapports  
 Dans Configuration Manager, les paramètres de compatibilité incluent un certain nombre de rapports intégrés qui vous permettent de surveiller les informations sur les éléments de configuration, les bases de référence de configuration et les déploiements. La catégorie de ces rapports est **Gestion de la conformité et des paramètres**.  

> [!IMPORTANT]  
>  Vous devez utiliser un caractère générique (**%**) quand vous utilisez les paramètres **Filtre d’appareil** et Filtre d’utilisateur dans les rapports des paramètres de compatibilité.  

 Pour plus d’informations sur la configuration de la génération de rapports dans Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="view-compliance-results-on-a-configuration-manager-windows-client-computer"></a>Afficher les résultats de compatibilité sur un ordinateur client Windows Configuration Manager

> [!NOTE]  
>  Vous ne pouvez pas afficher d’informations sur le client Windows Configuration Manager si vous êtes connecté avec un compte Invité du domaine.    

1.  Accédez à **Configuration Manager** dans le Panneau de configuration de l’ordinateur client et double-cliquez dessus pour ouvrir ses propriétés.  

2.  Cliquez sur l'onglet **Configurations** et affichez la liste des bases de référence de configuration déployées.  

3.  Affichez l' **État de compatibilité** pour chaque ligne de base de configuration :  

    > [!IMPORTANT]  
    >  Les résultats de l'évaluation sont mis en cache sur le client pendant 15 minutes. Si vous procédez à une ré-évaluation au cours de cette période de 15 minutes, les résultats de compatibilité sont renvoyés à partir de ce cache mais pas en tant que résultats d’une nouvelle évaluation. Par conséquent, toute modification que vous apportez au client peut avoir une incidence sur les résultats de l'évaluation de la conformité. Patientez jusqu'à ce que les 15 minutes s'écoulent avant de procéder à une ré-évaluation.  

    -   **Compatible**: l’ordinateur client est compatible avec la ligne de base de configuration évaluée.  

    -   **Non compatible**: l’ordinateur client est non conforme à la ligne de base de configuration évaluée.  

    -   **Inconnu**: l’ordinateur client n’a pas encore évalué la ligne de base de configuration. Si vous souhaitez initier une évaluation en dehors du calendrier d'évaluation de la compatibilité, sélectionnez les lignes de base de configuration à évaluer, puis cliquez sur **Évaluer**.  

        > [!NOTE]  
        >  Si vous disposez d’informations d’identification d’administrateur local sur l’ordinateur client, vous pouvez afficher les détails de chaque ligne de base de configuration évaluée pour déterminer quel élément de configuration signale un état de non-compatibilité. À cet effet, sélectionnez la ligne de base de configuration, puis cliquez sur **Afficher le rapport**.  

4.  Cliquez sur **OK**.  

##  <a name="create-collections-based-on-configuration-baseline-compliance"></a>Créer des regroupements en fonction de la compatibilité de la base de référence de configuration  
 Utilisez la procédure suivante pour créer un regroupement Configuration Manager basé sur des appareils associés à une compatibilité spécifiée. Vous pouvez créer des regroupements à partir des états de compatibilité suivants :  

-   **Compatible**  

-   **Erreur**  

-   **Non-compliant**  

-   **Inconnu.**  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Lignes de base de configuration**.  

3.  Dans la liste **Lignes de base de configuration** , sélectionnez la ligne de base de configuration à partir de laquelle vous souhaitez créer un regroupement.  

4.  Sous l’onglet **Déploiement** , dans le groupe **Déploiement**, cliquez sur **Créer un regroupement** , puis, dans la liste déroulante, sélectionnez le niveau de compatibilité pour lequel vous souhaitez créer un regroupement.  

5.  L' **Assistant Création d'un regroupement d'utilisateurs** ou l' **Assistant Création d'un regroupement de périphériques** s'ouvre, selon que l'élément de configuration est déployé vers des utilisateurs ou vers des périphériques. L'Assistant est automatiquement renseigné avec les valeurs correctes pour créer le regroupement. Toutefois, vous pouvez modifier ces valeurs.  

6.  Une fois que vous avez terminé l’Assistant, le regroupement s’affiche dans le nœud **Regroupements d’utilisateurs** ou **Regroupements de périphériques** de l’espace de travail **Ressources et Conformité** .  
