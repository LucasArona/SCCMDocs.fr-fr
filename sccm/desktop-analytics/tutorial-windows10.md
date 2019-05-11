---
title: 'Didacticiel : déployer Windows 10'
titleSuffix: Configuration Manager
description: Un didacticiel sur l’utilisation d’Analytique de bureau et de Configuration Manager pour déployer Windows 10 sur un groupe pilote.
ms.date: 04/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 3e82cd96-0ce0-474a-a597-d65fceadc95a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28e0326cf370d000052eb3bc675e70377d7954c5
ms.sourcegitcommit: 234f97fde834f94b75f90850378521cf0c5a2343
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945088"
---
# <a name="tutorial-deploy-windows-10-to-pilot"></a>Tutoriel : Déployer Windows 10 sur le pilote

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Ce didacticiel utilise l’Analytique de bureau et de Configuration Manager pour déployer Windows 10 sur un groupe pilote. Il met en évidence l’intégration de service cloud à fournir des informations permettant de déployer Windows avec le produit en local. Analytique de Desktop permet de déterminer les meilleures appareils à placer dans un groupe pilote. Ensuite utiliser Configuration Manager pour obtenir en cours avec Windows.

Dans ce didacticiel, vous allez découvrir comment :  

> [!div class="checklist"]  
> * Configurer Bureau Analytique dans le portail Azure  
> * Connecter Configuration Manager et configurer les paramètres de l’appareil  
> * Créer un plan de déploiement d’Analytique de bureau pour Windows 10  
> * Utilisez le Gestionnaire de Configuration pour déployer Windows 10 dans le groupe pilote  

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free) avant de commencer. Lorsqu’est correctement configuré, utilisation d’Analytique de bureau n’aucun frais Azure.

Analytique de bureau utilise un *espace de travail Analytique de journal* dans votre abonnement Azure. Un espace de travail est essentiellement un conteneur qui inclut des informations de compte et les informations de configuration simple pour le compte. Pour plus d’informations, consultez [gérer les espaces de travail](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Prérequis

Avant de commencer ce didacticiel, assurez-vous que vous disposez des prérequis suivants :  

- Un abonnement Azure actif, avec [ **administrateur général** ](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator) autorisations  

    Pour plus d’informations, consultez [conditions préalables de bureau Analytique](/sccm/desktop-analytics/overview#prerequisites).

- Configuration Manager, version 1810 avec correctif cumulatif 2 (4488598) ou version ultérieure, avec **administrateur complet** rôle  

- Support d’installation de la dernière version de Windows 10

- Au moins un appareil Windows 10 avec les configurations suivantes :  

    - Windows 10, version 1709 ou ultérieure, mais inférieur à la version du média d’installation que vous prévoyez d’utiliser

    - La dernière mise à jour de qualité cumulative de Windows 10  

    - Client Configuration Manager versions 1810 avec correctif cumulatif 2 (4488598) ou version ultérieure  

- Approbation d’entreprise pour configurer le niveau de données de diagnostic Windows à **avancé (limité)** sur les appareils de pilotes  

    Pour plus d’informations, consultez [confidentialité d’Analytique de bureau](/sccm/desktop-analytics/privacy).

- Connectivité réseau à partir de l’appareil aux points de terminaison internet suivant :

    - `https://v10c.events.data.microsoft.com`  
    - `https://settings-win.data.microsoft.com`  
    - `http://adl.windows.com`  
    - `https://watson.telemetry.microsoft.com`  
    - `https://umwatsonc.events.data.microsoft.com`  
    - `https://ceuswatcab01.blob.core.windows.net`  
    - `https://ceuswatcab02.blob.core.windows.net`  
    - `https://eaus2watcab01.blob.core.windows.net`  
    - `https://eaus2watcab02.blob.core.windows.net`  
    - `https://weus2watcab01.blob.core.windows.net`  
    - `https://weus2watcab02.blob.core.windows.net`  
    - `https://www.msftncsi.com`  
    - `https://www.msftconnecttest.com`  
    - `https://kmwatsonc.events.data.microsoft.com`  
    - `https://oca.telemetry.microsoft.com`  
    - `https://login.live.com`  
    - `https://graph.windows.net` (sur le rôle de serveur Configuration Manager uniquement)
    - `https://fef.msua06.manage.microsoft.com` (sur le rôle de serveur Configuration Manager uniquement)

    Pour plus d’informations, consultez [comment activer le partage de bureau Analytique des données](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Ces conditions préalables sont dans le cadre de ce didacticiel. Pour plus d’informations sur les conditions préalables générales pour l’Analytique de bureau avec Configuration Manager, consultez [conditions préalables](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurer les Analyses du bureau

Utilisez cette procédure pour vous connecter à l’Analytique de bureau et le configurer dans votre abonnement. Cette procédure est un processus unique pour configurer Desktop Analytique pour votre organisation.  

1. Ouvrez le portail d’Analytique de bureau dans Gestion des appareils Microsoft 365 en tant qu’utilisateur avec **administrateur général** autorisations. Sélectionnez **Démarrer**.  

2. Sur le **accepter le contrat de service** page, passez en revue le contrat de service, puis sélectionnez **Accept**.  

3. Sur le **confirmer votre abonnement** page, la liste des licences éligibles requises sont pour les fonctionnalités de contrôle d’intégrité des appareils Windows de bureau Analytique. Sélectionnez **Suivant** pour continuer.  

4. Sur le **donner aux utilisateurs accès** page :

    - **Voulez-vous vraiment Analytique de bureau pour gérer les rôles d’annuaire pour vos utilisateurs**: Analytique de postes de travail affecte automatiquement la **propriétaires de l’espace de travail** et **contributeurs de l’espace de travail** regroupe à la **Desktop Analytique Administrator** rôle. Si ces groupes sont déjà un **administrateur général**, il n’existe aucune modification.  

        Si vous ne sélectionnez pas cette option, bureau Analytique ajoute toujours les utilisateurs en tant que membres des groupes de sécurité de deux. Un **administrateur général** doit affecter manuellement la **Desktop Analytique Administrator** rôle pour les utilisateurs.  

        Pour plus d’informations sur l’attribution d’autorisations de rôle d’administrateur dans Azure Active Directory et les autorisations affectées aux **les administrateurs de bureau Analytique**, consultez [autorisations du rôle administrateur dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Postes de travail Analytique préconfigure les deux groupes de sécurité dans Azure Active Directory :  

        - **Propriétaires de l’espace de travail**: Un groupe de sécurité pour créer et gérer des espaces de travail. Ces comptes ont besoin d’un accès propriétaire à l’abonnement Azure.  

        - **Contributeurs de l’espace de travail**: Un groupe de sécurité pour créer et gérer des plans de déploiement dans cet espace de travail. Ils ne doivent tout accès Azure supplémentaires.  

        Pour ajouter un utilisateur au groupe, tapez son nom ou l’adresse électronique dans le **Entrez le nom ou adresse de messagerie** section du groupe approprié. Lorsque vous avez terminé, sélectionnez **suivant**.

5. Sur la page pour **configurer votre espace de travail**:  

    > [!Note]  
    > Effectuez cette étape en tant qu’un **propriétaire de l’espace de travail** ou **contributeur**. Pour plus d’informations, consultez [conditions préalables](/sccm/desktop-analytics/overview#prerequisites).  

    - Sélectionnez votre abonnement Azure.  

    - Pour utiliser un espace de travail pour l’Analytique de bureau, sélectionnez-le, puis passez à l’étape suivante.  

    - Pour créer un espace de travail pour l’Analytique de bureau, sélectionnez **ajouter l’espace de travail**.  

        1. Entrez un **nom de l’espace de travail**.  

        2. Sélectionnez la liste déroulante à **sélectionnez le nom de l’abonnement Azure pour cet espace de travail**, puis choisissez l’abonnement Azure pour cet espace de travail.  

        3. **Créer de nouveaux** groupe de ressources ou **utiliser l’existant**.  

        4. Sélectionnez le **région** dans la liste, puis sélectionnez **ajouter**.  

6. Sélectionnez un espace de travail nouveau ou existant, puis **définir comme espace de travail Analytique de bureau**.  Puis sélectionnez **continuer** dans le **confirmer et accorder l’accès** boîte de dialogue.  

7. Dans le nouvel onglet de navigateur, choisissez un compte à utiliser pour vous connecter. Sélectionnez l’option **donner son consentement au nom de votre organisation** et sélectionnez **Accept**.  

8. Revenez à la page à **configurer votre espace de travail**, sélectionnez **suivant**.  

9. Sur le **dernières étapes** page, sélectionnez **accéder au bureau Analytique**. Le portail Azure affiche l’Analytique de Desktop **accueil** page.  



## <a name="connect-configuration-manager"></a>Connecter le Gestionnaire de configuration

Utilisez cette procédure pour mettre à jour de Configuration Manager, connectez-vous à Analytique de bureau et configurer les paramètres de l’appareil. Cette procédure est un processus unique pour attacher votre hiérarchie vers le service cloud.  

### <a name="update-configuration-manager"></a>Mise à jour Configuration Manager

Installer le Gestionnaire de Configuration de version 1810 correctif cumulatif 2 (4488598) pour prendre en charge l’intégration avec l’Analytique de bureau. Pour plus d’informations sur cette mise à jour, consultez [correctif cumulatif pour Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4488598).

1. Mettez à jour le site avec le correctif cumulatif de la version 1810. Pour plus d’informations, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates).  

2. Mettre à jour des clients. Pour simplifier ce processus, envisagez d’utiliser la mise à niveau automatique des clients. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Se connecter au service

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**. Sélectionnez **configurer les Services Azure** dans le ruban.  

2. Sur le **Azure Services** page de l’Assistant Services Azure, configurez les paramètres suivants :  

    - Spécifiez un **nom** pour l’objet dans Configuration Manager  

    - Spécifiez un texte facultatif **Description** pour vous aider à identifier le service  

    - Sélectionnez **Desktop Analytique** dans la liste des services disponibles  
  
   Sélectionnez **Suivant**.  

3. Sur le **application** page, sélectionnez l’option appropriée **environnement Azure**. Puis sélectionnez **Parcourir** pour l’application web.

4. Sélectionnez **créer** permettent d’ajouter facilement une application Azure AD pour la connexion de bureau Analytique.

5. Configurez les paramètres suivants dans le **créer une Application serveur** fenêtre :  

    - **Nom de l'application** : Un nom convivial pour l’application dans Azure AD.

    - **URL de la page d'accueil** : cette valeur n’est pas utilisée par Configuration Manager, mais elle est exigée par Azure AD. Par défaut, cette valeur est `https://ConfigMgrService`.  

    - **URI ID d’application** : cette valeur doit être unique dans votre locataire Azure AD. Il est dans le jeton d’accès utilisé par le client Configuration Manager pour demander l’accès au service. Par défaut, cette valeur est `https://ConfigMgrService`.  

    - **Période de validité de la clé secrète** : choisissez **1 an** ou **2 ans** dans la liste déroulante. Un an est la valeur par défaut.  

    Sélectionnez **connectez-vous**. Après vous être authentifié correctement auprès d’Azure, la page affiche le **Nom du locataire Azure AD** pour référence.

    > [!Note]  
    > Effectuez cette étape en tant qu’un **administrateur d’entreprise**. Ces informations d’identification ne sont pas enregistrées par Configuration Manager. Ce rôle ne nécessite pas d’autorisations dans Configuration Manager et ne doit pas obligatoirement être le même compte que celui qui exécute l’Assistant Services Azure.  

    Sélectionnez **OK** pour créer l’application web dans Azure AD et fermer la boîte de dialogue Créer une application serveur. Dans la boîte de dialogue application serveur, sélectionnez **OK**. Puis sélectionnez **suivant** sur la page application de l’Assistant Services Azure.  

6. Sur le **données de Diagnostic** page, configurez les paramètres suivants :  

    - **ID commercial**: cette valeur doit remplir automatiquement avec l’ID de votre organisation  

    - **Niveau de données de diagnostic de Windows 10**: sélectionnez au moins **avancé (limité)**  

    - **Autoriser le nom de l’appareil dans les données de diagnostic**: sélectionnez **activer**  
  
   Sélectionnez **Suivant**. Le **fonctionnalités disponibles** page affiche les fonctionnalités d’Analytique de bureau qui sont disponibles avec les paramètres de données de diagnostic à partir de la page précédente. Sélectionnez **Suivant**.  

7. Sur le **Collections** page, configurez les paramètres suivants :  

    - **Nom complet** : Le portail d’Analytique de bureau affiche cette connexion de Configuration Manager à l’aide de ce nom. Il permet de faire la distinction entre des hiérarchies différentes. Par exemple, *laboratoire de test* ou *production*.  

    - **Regroupement cible**: Cette collection inclut tous les appareils Configuration Manager configure avec votre ID commercial et les paramètres de données de diagnostic. Il est l’ensemble des appareils Configuration Manager se connecte au service d’Analytique de bureau.  

    - **Appareils du regroupement cible utilisent un proxy authentifié par l’utilisateur pour les communications sortantes**: Par défaut, cette valeur est **non**. Si nécessaire dans votre environnement, la valeur est **Oui**.  

    - **Sélectionner des regroupements spécifiques pour se synchroniser avec le bureau Analytique**: Sélectionnez **ajouter** pour inclure des collections supplémentaires. Ces collections sont disponibles dans le portail d’Analytique de bureau pour le regroupement des plans de déploiement. Veillez à inclure les collections d’exclusion de pilote et de pilote.  

        Ces collections continuent à synchroniser en tant que leurs changements d’appartenance. Par exemple, votre plan de déploiement utilise une collection avec une règle d’adhésion de Windows 7. Comme ces appareils mise à niveau vers Windows 10 et Configuration Manager évalue l’appartenance au regroupement, ces appareils déposent hors de la collecte et le plan de déploiement.  

8. Effectuez toutes les étapes de l'Assistant.  

Configuration Manager crée une stratégie de paramètres pour configurer les appareils du regroupement cible. Cette stratégie inclut les paramètres de données de diagnostic pour permettre aux appareils d’envoyer des données à Microsoft. Par défaut, les clients de mettre à jour stratégie toutes les heures. Après avoir reçu les nouveaux paramètres, il peut être plus de plusieurs heures avant que les données sont disponibles dans l’Analytique de bureau.

Surveiller la configuration de vos appareils pour l’Analytique de bureau. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Desktop Analytique maintenance** nœud, puis sélectionnez le **intégrité de la connexion** tableau de bord.  

Configuration Manager synchronise vos collections dans les 60 minutes de la création de la connexion. Dans le portail d’Analytique de bureau, accédez à **pilote Global**et consultez vos regroupements de périphériques de Configuration Manager.


## <a name="create-a-desktop-analytics-deployment-plan"></a>Créer un plan de déploiement de bureau Analytique

Utilisez cette procédure pour créer un plan de déploiement dans l’Analytique de bureau.

1. Ouvrez le [portail d’Analytique de bureau](https://aka.ms/m365aprod). Utilisez les informations d’identification qui disposent au moins **contributeurs de l’espace de travail** autorisations.  

2. Sélectionnez **Plans de déploiement** dans le groupe de gestion.  

3. Dans le **Plans de déploiement** volet, sélectionnez **créer**.  

4. Dans le **création du plan de déploiement** volet, configurez les paramètres suivants :  

    - **Nom** : Planifier un nom unique pour le déploiement, par exemple `Windows 10 pilot`  

    - **Produits et versions**: Sélectionnez le **Windows** produit et la dernière version recommandée disponible. Par exemple, **Windows 10, version 1809 (recommandé)**.  

    - **Groupes d’appareils**: Sélectionnez un ou plusieurs groupes à partir de l’onglet de Configuration Manager, puis **définir en tant que groupes cibles**. Ces groupes sont des collections synchronisées à partir de Configuration Manager.  

    - **Règles de préparation**: Ces règles vous aide à déterminer quels appareils sont éligibles pour la mise à niveau. Sélectionnez **système d’exploitation WIndows** et configurez les paramètres suivants :  

        - **Mes ordinateurs obtenir automatiquement les pilotes à partir de Windows Update**: Le paramètre par défaut est **hors**, ce qui est recommandé lors du déploiement avec Configuration Manager.  

        - **Définir un seuil de nombre faible d’installation pour vos applications**: Le paramètre par défaut est `2%`. Applications sous ce seuil sont automatiquement définies pour *faible nombre d’installations*. Analytique de bureau ne valide pas ces compléments pendant la phase pilote.  

            Si une application est installée sur un pourcentage plus élevé d’ordinateurs à ce seuil, le plan de déploiement marque l’application en tant que *Noteworthy*. Vous pouvez ensuite son importance pour tester pendant la phase pilote.  

    - **Date de fin**: Choisissez la date à laquelle Windows doit être entièrement déployé à tous les appareils ciblés.  

5. Sélectionnez **créer**. Le nouveau plan s’affiche dans la liste des plans de déploiement lors de son traitement. Le traitement peut prendre jusqu'à 48 heures avant de procéder à l’étape suivante.  

6. Ouvrez le plan de déploiement en sélectionnant son nom.  

7. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier l’importance**.  

    1. Sur le **applications** onglet, sélectionnez cette option pour n’afficher que **pas été revues** actifs.  

    2. Sélectionnez chaque application, puis **modifier**. Vous pouvez sélectionner plusieurs applications à modifier en même temps.  

    3. Choisissez un niveau d’importance dans le **Importance** liste. Si vous souhaitez Analytique de bureau pour valider l’application pendant la phase pilote, sélectionnez **critique** ou **Important**. Il ne valide pas les applications marquées en tant que **pas Important**. Prendre en compte la [risque de compatibilité](/sccm/desktop-analytics/compat-risk) et d’autres informations de plan lors de l’affectation de niveaux d’importance.  

        Lorsque vous affectez des niveaux d’importance, vous pouvez également choisir la décision de mise à niveau.  

    4. Sélectionnez **enregistrer** lorsque vous avez terminé.  

8. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier pilote**.  

    1. Passez en revue les appareils recommandées pour le projet pilote.  

    2. Sélectionnez chaque appareil, puis **ajouter pilote**. Si vous êtes en désaccord avec la recommandation, sélectionnez **remplacer**.  

        Pour plus d’informations sur comment Desktop Analytique rend ces recommandations, sélectionnez l’icône d’information dans l’angle supérieur droit de la **identifier pilote** volet.



## <a name="deploy-windows-10-in-configuration-manager"></a>Déployer Windows 10 dans Configuration Manager

Utilisez cette procédure pour déployer Windows 10 dans Configuration Manager dans le groupe pilote.

- Si vous n’en avez pas, tout d’abord [créer un package de mise à niveau du système d’exploitation pour Windows 10](#bkmk_create-package)  

- Si vous n’avez pas encore, [créer une séquence de tâches de mise à niveau de système d’exploitation pour Windows 10](#bkmk_create-ts)  

- [Déployer la séquence de tâches](#bkmk_deploy-ts) à l’aide du plan de déploiement de bureau Analytique  

- [Installer la séquence de tâches](#bkmk_install-ts) depuis le centre logiciel sur un appareil cible  

<!-- 
- [Monitor](#bkmk_monitor-ts) status in Configuration Manager  
 -->

### <a name="bkmk_create-package"></a> Créer un package de mise à niveau du système d’exploitation pour Windows 10

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Packages de mise à niveau du système d’exploitation**.  

2. Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, sélectionnez **Ajouter un package de mise à niveau du système d’exploitation**. Cette action démarre l’Assistant Ajout d’un package de mise à niveau du système d’exploitation.  

3. Sur le **Source de données** , spécifiez le réseau **chemin d’accès** à l’installation de fichiers sources du système d’exploitation mettre à niveau de package. Par exemple, `\\server\share\path`.  

    > [!NOTE]  
    > Les fichiers sources d’installation contiennent Setup.exe et d’autres fichiers et dossiers pour installer le système d’exploitation.  

4. Sur le **général** page, spécifiez une valeur unique **nom** pour le système d’exploitation mise à niveau de package.  

5. Terminer l’ajout d’Assistant de Package de mise à niveau de système d’exploitation.  

#### <a name="distribute-content"></a>Distribuer du contenu

Ensuite, distribuez le package de mise à niveau du système d’exploitation sur les points de distribution.  

1. Dans la liste, sélectionnez le package de mise à niveau du système d’exploitation. Sur le **accueil** onglet du ruban, dans le **déploiement** groupe, sélectionnez **distribuer du contenu**. L'Assistant Distribuer du contenu s'ouvre.  

2. Sur le **général** , vérifiez que le contenu répertorié correspond au contenu que vous voulez distribuer, puis sélectionnez **suivant**.  

3. Sur le **Destination du contenu** page, sélectionnez **ajouter**, puis choisissez **Point de Distribution**. Sélectionnez un point de distribution existant, puis **OK**. Lorsque vous avez terminé d’ajouter des destinations de contenu, sélectionnez **suivant**.  

4. Terminer l’Assistant distribuer du contenu.  


### <a name="bkmk_create-ts"></a> Créer une séquence de tâches de mise à niveau de système d’exploitation pour Windows 10

1. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez **systèmes d’exploitation**, puis sélectionnez **séquences de tâches**.  

2. Sur le **accueil** onglet du ruban, dans le **créer** groupe, sélectionnez **créer une séquence de tâches**.  

3. Sur le **créer une séquence de tâches** page de l’Assistant séquence de tâches de création, sélectionnez **mettre à niveau un système d’exploitation à partir d’un package de mise à niveau**, puis sélectionnez **suivant**.  

4. Sur le **les informations de séquence de tâches** , spécifiez un **nom de séquence de tâches** qui identifie la séquence de tâches.  

5. Sur le **mettre à niveau le système d’exploitation Windows** page, spécifiez les paramètres suivants, puis sélectionnez **suivant**:  

    - **Package de mise à niveau** : spécifiez le package de mise à niveau qui contient les fichiers sources de mise à niveau du système d’exploitation.  

    - **Index d’édition** : si plusieurs index d’édition de système d’exploitation sont disponibles dans le package, sélectionnez celui que vous souhaitez. Par défaut, l’Assistant sélectionne le premier index.  

    - **Clé du produit** : spécifiez la clé de produit Windows du système d’exploitation à installer. Spécifiez des clés de licence en volume codées ou des clés de produit standard. Si vous utilisez une clé de produit standard, séparez chaque groupe de cinq caractères par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quand la mise à niveau concerne une édition de licence en volume, la clé de produit n’est pas toujours requise.  

        > [!Note]  
        > Cette clé de produit peut être une clé d’activation multiple (MAK) ou une clé de licence en volume générique (GVLK). La clé GVLK est aussi connue sous le nom de clé d’installation de client de service de gestion de clés (KMS). Pour plus d’informations, consultez [Planifier l’activation en volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Pour obtenir la liste des clés d’installation de client KMS, consultez [l’Annexe A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) du guide d’activation de Windows Server.

6. Sur le **incluent les mises à jour** page, sélectionnez **suivant** de ne pas installer un logiciel met à jour.  

7. Sur le **installer les Applications** page, sélectionnez **suivant** ne pas installer des applications.

8. Terminer l’Assistant Création d’une séquence de tâche.  


### <a name="bkmk_deploy-ts"></a> Déployer la séquence de tâches à l’aide du plan de déploiement de bureau Analytique

1. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels**, développez **Desktop Analytique maintenance**, puis sélectionnez le **Plans de déploiement** nœud.  

2. Sélectionnez votre plan de déploiement pilote de Windows 10, puis **détails du Plan de déploiement** dans le ruban.  

3. Dans le **piloter état** en mosaïque, choisissez **séquence de tâches** dans la liste déroulante, puis sélectionnez **déployer**.  

4. Sur le **général** page de l’Assistant Déploiement de logiciel, sélectionnez **Parcourir** à côté du **logiciel** champ. Sélectionnez votre séquence de tâches de mise à niveau sur place de Windows 10, puis **suivant**.  

    > [!Note]  
    > Avec l’intégration Analytique de bureau, Configuration Manager crée automatiquement une collection pour le plan de déploiement pilote. Il peut prendre jusqu'à 10 minutes pour cette collection à synchroniser que vous puissiez l’utiliser.<!-- 3887891 -->
    >
    > Cette collection est réservée aux appareils de plan de déploiement de bureau Analytique. Les modifications manuelles à cette collection ne sont pas pris en charge.<!-- 3866460, SCCMDocs-pr 3544 -->  

5. Sur le **contenu** page, sélectionnez **ajouter**, puis sélectionnez **point de Distribution**. Sélectionnez un point de distribution disponible pour héberger le contenu de l’installation, puis sélectionnez **OK**. Puis sélectionnez **Suivant**.  

6. Sur le **paramètres de déploiement** page, sélectionnez **suivant** pour accepter les paramètres par défaut. (Une installation disponible).  

7. Sur le **planification** page, sélectionnez **suivant** pour accepter les paramètres par défaut. (Disponible dès que possible).  

8. Sur le **l’expérience utilisateur** page, sélectionnez **suivant** pour accepter les paramètres par défaut. (Afficher dans le centre logiciel et afficher uniquement les notifications de redémarrage de l’ordinateur).  

9. Sur le **alertes** page, sélectionnez **suivant** pour accepter les paramètres par défaut.  

10. Effectuez toutes les étapes de l'Assistant.  


### <a name="bkmk_install-ts"></a> Installer la séquence de tâches depuis le centre logiciel

1. Connectez-vous à un appareil qui est membre du plan de déploiement pilote.  

2. Ouvrez **centre logiciel** et installer le système d’exploitation disponible pour Windows 10.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour en savoir plus sur les plans de déploiement de bureau Analytique.
> [!div class="nextstepaction"]  
> [Plans de déploiement](/sccm/desktop-analytics/about-deployment-plans)
