---
title: Conditions générales
titleSuffix: Configuration Manager
description: Déployez les conditions générales de System Center Configuration Manager dans des groupes d’utilisateurs.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4d3f9e6b-4d71-4fc4-9b91-47f1bfbd8c70
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: cda5f01842f08ccc3e8dfbd17078fe157954d985
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353468"
---
# <a name="add-terms-and-conditions-with-system-center-configuration-manager"></a>Ajouter des conditions générales dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez déployer les conditions générales de System Center Configuration Manager dans des groupes d’utilisateurs pour expliquer en quoi l’inscription d’appareils, l’accès aux ressources de travail et l’utilisation du Portail d’entreprise affectent les utilisateurs et les appareils. Les utilisateurs doivent accepter les conditions générales avant de pouvoir utiliser le Portail d’entreprise pour s’inscrire et accéder à leur travail.  

 ## <a name="working-with-terms-and-conditions-policies-in-system-center-configuration-manager"></a>Utilisation de stratégies associées aux conditions générales dans System Center Configuration Manager  
 Vous pouvez créer et déployer plusieurs ensembles de conditions générales. Vous pouvez également produire des versions des mêmes conditions générales dans différentes langues et les déployer pour les groupes appropriés.  

## <a name="to-create-a-terms-and-conditions"></a>Pour créer des conditions générales  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de compatibilité** > **Conditions générales**.  

2.  Cliquez sur **Créer les conditions générales** pour créer des conditions générales.  

3.  Sur la page **Général** , spécifiez informations suivantes :  

    -   **Nom** : nom unique affiché dans la console Configuration Manager.  

    -   **Description** : détails qui vous aident à identifier les conditions générales dans la console Configuration Manager.  

     Puis cliquez sur **Suivant**.  

4.  Dans la page **Termes** , spécifiez les informations suivantes :  

    -   **Titre** : titre affiché dans le Portail d’entreprise.  

    -   **Texte pour les conditions** : conditions générales affichées dans le Portail d’entreprise.  

    -   **Texte expliquant ce que cela signifie si l'utilisateur accepte** : étiquette informant les utilisateurs des conséquence de l'acceptation. **Exemple** : « J’accepte les conditions générales. »  

     Puis cliquez sur **Suivant**.  

5.  Terminez l’Assistant pour créer les conditions générales. Les nouvelles conditions générales sont affichées dans le nœud Conditions générales de l’espace de travail Ressources et Conformité.  

## <a name="to-deploy-a-terms-and-conditions"></a>Pour déployer des conditions générales  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de compatibilité** > **Conditions générales**.  

2.  Dans la liste **Conditions générales** , sélectionnez l’élément à déployer, puis cliquez sur **Gérer**.  

3.  Cliquez sur**Parcourir** et accédez au **Regroupement** dans lequel vous souhaitez déployer les conditions générales, puis cliquez sur **OK**.  

     Quand des appareils ciblés accèdent à l’application Portail d’entreprise, les conditions générales que vous avez déployées sont affichées. Les utilisateurs doivent accepter ces conditions générales avant de pouvoir accéder aux ressources de l'entreprise.  

    > [!NOTE]  
    >  Si vous déployez un ensemble de conditions générales dans plusieurs regroupements d’utilisateurs auxquels appartient un utilisateur, il verra plusieurs copies de conditions générales identiques quand il ouvrira le Portail d’entreprise. Étant donné que les utilisateurs peuvent uniquement accepter ou refuser toutes les conditions générales, il n’existe aucun risque d’être dans un état d’acceptation ambigu où l’utilisateur aurait à la fois accepté et refusé les conditions générales. Le rapport d’acceptation des conditions générales comprend une seule ligne par ensemble de conditions générales et par utilisateur. Il ne contient donc aucune erreur.  

## <a name="to-monitor-terms-and-conditions"></a>Pour surveiller des conditions générales  

1.  Vous pouvez surveiller les déploiements de conditions générales dans la console Configuration Manager. Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **Déploiements**.  

2.  Sélectionnez le déploiement de conditions générales dans la liste des déploiements.  

     La zone récapitulative affiche les statistiques suivantes :  

    -   **Conforme** - Les utilisateurs ont accepté la dernière version des conditions générales  

    -   **Erreur**  

    -   **Non conforme** - Les utilisateurs ont accepté une version des conditions générales, mais pas la dernière  

    -   **Inconnu** - Les utilisateurs n’ont jamais accepté les conditions générales, y compris celles sans un appareil inscrit  

3.  Sélectionnez un déploiement de conditions générales, puis **Exécuter le résumé** pour afficher l’État du déploiement des utilisateurs.  

     Sur l’écran État du déploiement, vous pouvez sélectionner les onglets d’état pour afficher les utilisateurs avec cet état. Vous pouvez cliquer sur **Exécuter le résumé** pour mettre à jour les données dans toute la hiérarchie. Cliquez sur **Actualiser** pour mettre à jour les données dans la console  

## <a name="to-view--a-terms-and-conditions-report"></a>Pour afficher un rapport de conditions générales  

1.  Dans la console Configuration Manager, accédez à **Analyse** > **Vue d’ensemble** > **Reporting** > **Rapport**.  

2.  Sélectionnez **Acceptation des conditions générales** , puis cliquez sur **Exécuter**. Le rapport d’acceptation des conditions générales s’ouvre. Le rapport affiche chaque utilisateur pour lequel des conditions générales ont été déployées. Les champs sont les suivants :  

    -   Nom des conditions générales  

    -   Nom d'utilisateur  

    -   Version acceptée  

    -   Date d’acceptation  

    -   Dernière version acceptée  

## <a name="updates-and-version-control-for-terms-and-conditions"></a>Mises à jour et contrôle de version pour les conditions générales  
 Quand vous modifiez des conditions générales existantes, vous pouvez choisir le comportement lors de leur déploiement. Appliquez la procédure suivante pour vous aider à mettre à jour des conditions générales existantes.  

### <a name="how-to-work-with-multiple-versions-of-terms-and-conditions"></a>Utilisation de plusieurs versions des conditions générales  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de compatibilité** > **Conditions générales**.  

2.  Sélectionnez l’instance de conditions générales à modifier, puis double-cliquez pour l’ouvrir.  

3.  Vous pouvez modifier le contenu dans la page **Général** ou **Termes** pour effectuer les modifications nécessaires.  

4.  Dans la page **Termes** , vous pouvez ensuite spécifier si cette nouvelle version exige que tous les utilisateurs acceptent les conditions générales ou si seuls les nouveaux utilisateurs verront la nouvelle version.  

     Nous vous recommandons d’incrémenter le numéro de version et d’exiger l’acceptation chaque fois que vous apportez des modifications majeures à vos conditions générales. Conservez le numéro de version actuel si vous corrigez des fautes de frappe ou si vous modifiez la mise en forme, par exemple.

> [!div class="button"]
[< Étape précédente](configure-intune-subscription.md) [Étape suivante >](create-service-connection-point.md)
