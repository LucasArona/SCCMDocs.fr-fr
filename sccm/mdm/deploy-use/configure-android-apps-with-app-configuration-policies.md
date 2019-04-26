---
title: Configurer des applications Android for Work avec des stratégies de configuration des applications
titleSuffix: Configuration Manager
description: Évitez les problèmes de configuration sur les appareils sous Android for Work en déployant des stratégies de configuration des applications sur les appareils avant qu’ils n’exécutent des applications.
ms.date: 09/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 9126d188-7780-45a4-b21d-7fcf4fad7da2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7d6f8c25902be857e0eec3cd4b969d1fb5bda136
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62288766"
---
# <a name="apply-settings-to-android-for-work-apps-with-app-configuration-policies-in-system-center-configuration-manager"></a>Appliquer des paramètres à des applications Android for Work avec des stratégies de configuration des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser des stratégies de configuration des applications dans System Center Configuration Manager pour distribuer les paramètres susceptibles de se révéler nécessaires lorsqu’un utilisateur exécute une application. Par exemple, une application peut exiger qu’un utilisateur spécifie les détails suivants :
- Un numéro de port personnalisé
- Paramètres de langue
- Paramètres de sécurité
- Paramètres de personnalisation, comme le logo de l’entreprise

Si l’utilisateur entre les paramètres incorrectement, il est de la responsabilité du support technique de les corriger, ce qui ralentit le déploiement de l’application. Pour éviter ces problèmes, vous pouvez utiliser des stratégies de configuration d’application pour déployer les paramètres obligatoires sur les utilisateurs avant qu’ils n’exécutent l’application. Les paramètres sont automatiquement associés à un utilisateur. Aucune intervention de la part de l’utilisateur n’est nécessaire.
Au lieu de déployer les stratégies de configuration directement sur des utilisateurs et des appareils, associez une stratégie à un type de déploiement lorsque vous déployez l’application. Les paramètres de stratégie sont appliqués chaque fois que l’application les vérifie, soit, en général, lors de sa première exécution.

Les stratégies de configuration des applications Android sont disponibles uniquement sur les appareils Android for Work. Les stratégies de configuration des applications s’appliquent aux applications approuvées du magasin Play for Work. Pour plus d’informations sur les applications Android achetées en volume, consultez la page [Guide pratique pour déployer des applications sur des appareils Android for Work](https://docs.microsoft.com/intune/deploy-use/android-for-work-apps).

Pour plus d’informations sur les types d’installation d’application, consultez [Introduction à la gestion des applications](/sccm/apps/understand/introduction-to-application-management).

## <a name="create-an-app-configuration-policy"></a>Créer une stratégie de configuration des applications

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de configuration des applications**.
2. Sur l’onglet **Accueil**, dans le groupe **Stratégies de configuration des applications**, choisissez **Créer une stratégie de configuration des applications**.
3. Dans la page **Général** de l’Assistant Création d’une stratégie de configuration d’applications, définissez les informations de cette stratégie :
   - **Nom**. Entrez un nom unique pour la stratégie.
   - **Description**. (Facultatif) Pour identifier plus facilement la stratégie, vous pouvez ajouter une description.
   -  **Sélectionnez un type de stratégie de configuration**. Spécifiez la plateforme ciblée par la stratégie de configuration d’application : **Stratégie de configuration pour les applications Android for Work**.
   -  **Catégories attribuées pour améliorer la recherche et le filtrage**. (Facultatif) Pour créer et attribuer des catégories à la stratégie, choisissez **Catégories**. L’utilisation de catégories facilite le tri et la recherche d’éléments dans la console Configuration Manager.
4. Sur la page **Stratégie Android for Work**, choisissez de quelle façon les informations sur la stratégie de configuration sont définies :
   - **Spécifier des paires nom/valeur**. Vous pouvez utiliser cette option pour les fichiers de liste de propriétés simples sans imbrication. Pour spécifier une paire nom/valeur :
        1. Pour ajouter une paire JSON, choisissez **Nouveau**.
        2. Dans la boîte de dialogue **Ajouter une paire nom/valeur**, spécifiez les informations suivantes :
            - **Type**. Dans la liste, sélectionnez le type de valeur que vous souhaitez spécifier.
            - **Nom**. Entrez le nom de la clé de liste de propriétés pour laquelle vous voulez spécifier une valeur.
            - **Valeur**. Entrez la valeur à appliquer à la clé spécifiée.

   - **Accédez à un fichier JSON de liste de propriétés**. Utilisez cette option si vous avez déjà un fichier JSON de configuration des applications, ou pour les fichiers complexes avec imbrication. Dans le champ **Stratégie de configuration des applications**, entrez les informations de la liste de propriétés au format JSON approprié.
5. Pour importer un fichier JSON créé précédemment, choisissez **Sélectionner un fichier**.
6. Choisissez **Suivant**. Si le code JSON contient des erreurs, corrigez-les avant de continuer.
7. Terminez les étapes de l’Assistant.

La nouvelle stratégie de configuration des applications s’affiche dans le nœud **Stratégies de configuration des applications** de l’espace de travail **Bibliothèque de logiciels**.

## <a name="associate-an-app-configuration-policy-with-a-configuration-manager-application"></a>Associer une stratégie de configuration des applications à une application de Configuration Manager

Pour associer une stratégie de configuration des applications au déploiement d’une application Android for Work, déployez l’application comme vous le faites habituellement, en suivant la procédure décrite dans la rubrique [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).

Dans la page **Stratégies de configuration d’application** de l’Assistant Déploiement logiciel, choisissez **Nouveau**. Dans la boîte de dialogue **Sélectionner la stratégie de configuration des applications**, choisissez un type de déploiement d’application et la stratégie de configuration des applications à laquelle l’associer.
Quand le type de déploiement est installé, les paramètres de la stratégie de configuration des applications sont automatiquement appliqués.
