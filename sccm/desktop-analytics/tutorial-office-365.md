---
title: Didacticiel - déployer Office 365
titleSuffix: Configuration Manager
description: Un didacticiel sur l’utilisation d’Analytique de bureau et de Configuration Manager pour déployer Office 365 à un groupe pilote.
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: tutorial
ms.assetid: 0b2b633a-91d7-4497-8c2a-1fc7aa310bb1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 66fc982fa7f2cee3fdd83945c1b43d490b40d2f2
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673783"
---
# <a name="tutorial-deploy-office-365-to-pilot"></a>Tutoriel : Déployer Office 365 pilote

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Ce didacticiel utilise l’Analytique de bureau et de Configuration Manager pour déployer Office 365 ProPlus à un groupe pilote. Il met en évidence l’intégration de service cloud à fournir des informations permettant de déployer l’application avec le produit en local. Analytique de Desktop permet de déterminer les meilleures appareils à placer dans un groupe pilote. Puis utiliser Configuration Manager pour obtenir actuelle avec Office.

Dans ce didacticiel, vous allez découvrir comment :  

> [!div class="checklist"]  
> * Configurer Bureau Analytique dans le portail Azure  
> * Connecter Configuration Manager et configurer les paramètres de l’appareil  
> * Créer un plan de déploiement de bureau Analytique pour Office 365 ProPlus  
> * Déployer Office 365 ProPlus dans Configuration Manager dans le groupe pilote  

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer. Lorsqu’est correctement configuré, utilisation d’Analytique de bureau n’aucun frais Azure.

Analytique de bureau utilise un *espace de travail Analytique de journal* dans votre abonnement Azure. Un espace de travail est essentiellement un conteneur qui inclut des informations de compte et les informations de configuration simple pour le compte. Pour plus d’informations, consultez [gérer les espaces de travail](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access?toc=/azure/azure-monitor/toc.json).



## <a name="prerequisites"></a>Prérequis

Avant de commencer ce didacticiel, assurez-vous que vous disposez des prérequis suivants :  

- Un abonnement Azure actif, avec **administrateur d’entreprise** autorisations  

- Configuration Manager, version 1810 avec 4488598 de correctif cumulatif de mise à jour ou version ultérieure, avec **administrateur complet** rôle  

- Au moins un appareil Windows 10 avec les configurations suivantes :  

    - Windows 10, version 1709 ou ultérieure

    - La dernière mise à jour de qualité cumulative de Windows 10  

    - Client Configuration Manager versions 1810 avec correctif cumulatif 4486457 ou version ultérieure  

    - Une version en fonction du programme d’installation de Windows de Microsoft Office, telles qu’Office 2013  

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
    - `https://nexusrules.officeapps.live.com`  
    - `https://nexus.officeapps.live.com`  
    - `https://office.pipe.aria.microsoft.com`  
    - `https://graph.windows.net` (sur le rôle de serveur de Configuration Manager uniquement)
    - `https://fef.msua06.manage.microsoft.com` (sur le rôle de serveur de Configuration Manager uniquement)

    Pour plus d’informations, consultez [comment activer le partage de bureau Analytique des données](/sccm/desktop-analytics/enable-data-sharing#endpoints).  

> [!Important]  
> Ces conditions préalables sont dans le cadre de ce didacticiel. Pour plus d’informations sur les conditions préalables générales pour l’Analytique de bureau avec Configuration Manager, consultez [conditions préalables](/sccm/desktop-analytics/overview#prerequisites).  



## <a name="set-up-desktop-analytics"></a>Configurer les Analyses du bureau

Utilisez cette procédure pour vous connecter à l’Analytique de bureau et le configurer dans votre abonnement. Cette procédure est un processus unique pour configurer Desktop Analytique pour votre organisation.  

1. Ouvrez le portail d’Analytique de bureau dans Gestion des appareils Microsoft 365 en tant qu’utilisateur avec **administrateur d’entreprise** autorisations. Sélectionnez **Démarrer**.  

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

    - Pour utiliser un espace de travail pour l’Analytique de bureau, sélectionnez-le, puis passez à l’étape suivante.  

    - Pour créer un espace de travail pour l’Analytique de bureau, sélectionnez **ajouter l’espace de travail**.  

        1. Entrez un **nom de l’espace de travail**.  

        2. Sélectionnez la liste déroulante à **sélectionnez le nom de l’abonnement Azure pour cet espace de travail**, puis choisissez l’abonnement Azure pour cet espace de travail.  

        3. Sélectionnez le **région** dans la liste, puis sélectionnez **ajouter**.  

6. Sélectionnez un espace de travail nouveau ou existant, puis **définir comme espace de travail Analytique de bureau**.  Puis sélectionnez **continuer** dans le **confirmer et accorder l’accès** boîte de dialogue.  

7. Dans le nouvel onglet de navigateur, choisissez un compte à utiliser pour vous connecter. Sélectionnez l’option **donner son consentement au nom de votre organisation** et sélectionnez **Accept**.  

8. Revenez à la page à **configurer votre espace de travail**, sélectionnez **suivant**.  

9. Sur le **dernières étapes** page, sélectionnez **accéder au bureau Analytique**. Le portail Azure affiche l’Analytique de Desktop **accueil** page.  


### <a name="create-an-app-in-azure-ad-for-configuration-manager"></a>Créer une application dans Azure AD pour Configuration Manager  

1. Dans le [Azure portal](https://portal.azure.com), accédez à **Azure Active Directory**, puis sélectionnez **inscriptions**. Puis sélectionnez **nouvelle inscription d’application**.  

2. Dans le **créer** panel, configurez les paramètres suivants :  

    - **Nom**: un nom unique qui identifie l’application, par exemple : `Desktop-Analytics-Connection`  

    - **Type d’application**: **Application Web / API**  

    - **URL d’authentification**: cette valeur n’est pas utilisée par Configuration Manager, mais requis par Azure AD. Entrez une URL valide et unique, par exemple : `https://configmgrapp`  
  
    Sélectionnez **créer**.  

3. Sélectionnez l’application et notez le **ID d’Application**. Cette valeur est un GUID qui est utilisé pour configurer la connexion de Configuration Manager.  

4. Sélectionnez **paramètres** dans l’application, puis sélectionnez **clés**. Dans le **les mots de passe** section, entrez un **description de la clé**, spécifiez un délai d’expiration **durée**, puis sélectionnez **enregistrer**. Copie le **valeur** de la clé, qui est utilisée pour configurer la connexion de Configuration Manager.

    > [!Important]  
    > Il s’agit de la seule possibilité pour copier la valeur de clé. Si vous ne le copiez maintenant, vous devez créer une autre clé.  
    >
    > Enregistrez la valeur de clé dans un emplacement sécurisé.  

5. Sur l’application **paramètres** panneau, sélectionnez **autorisations requises**.  

    1. Sur le **autorisations requises** panneau, sélectionnez **ajouter**.  

    2. Dans le **ajouter un accès API** Panneau de configuration, **sélectionner une API**.  

    3. Recherchez le **Microservice de Configuration Manager** API. Sélectionnez-le, puis choisissez **sélectionnez**.  

    4. Sur le **activer l’accès** du panneau, sélectionnez à la fois des autorisations de l’application : **Écrire des données de Collection CM** et **lire les données de Collection CM**. Puis choisissez **sélectionnez**.  

    5. Sur le **ajouter un accès API** panneau, sélectionnez **fait**.  

6. Sur le **autorisations requises** page, sélectionnez **accorder des autorisations**. Sélectionnez **Oui**.  

7. Copiez l’ID de locataire Azure AD. Cette valeur est un GUID qui est utilisé pour configurer la connexion de Configuration Manager. Sélectionnez **Azure Active Directory** dans le menu principal, puis sélectionnez **propriétés**. Copie le **ID de répertoire** valeur.  



## <a name="connect-configuration-manager"></a>Connecter le Gestionnaire de configuration

Utilisez cette procédure pour mettre à jour de Configuration Manager, connectez-vous à Analytique de bureau et configurer les paramètres de l’appareil. Cette procédure est un processus unique pour attacher votre hiérarchie vers le service cloud.  


### <a name="update-configuration-manager"></a>Mise à jour Configuration Manager

Installez le correctif cumulatif de Configuration Manager version 1810 (4486457) pour prendre en charge l’intégration avec l’Analytique de bureau. Pour plus d’informations sur cette mise à jour, consultez [correctif cumulatif pour Configuration Manager current branch, version 1810](https://support.microsoft.com/help/4486457).

1. Mettez à jour le site avec le correctif cumulatif de la version 1810. Pour plus d’informations, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates).  

2. Mettre à jour des clients. Pour simplifier ce processus, envisagez d’utiliser la mise à niveau automatique des clients. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients#automatic-client-upgrade).  


### <a name="connect-to-the-service"></a>Se connecter au service

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**. Sélectionnez **configurer les Services Azure** dans le ruban.  

2. Sur le **Azure Services** page de l’Assistant Services Azure, configurez les paramètres suivants :  

    - Spécifiez un **nom** pour l’objet dans Configuration Manager  

    - Spécifiez un texte facultatif **Description** pour vous aider à identifier le service  

    - Sélectionnez **Desktop Analytique** dans la liste des services disponibles  
  
   Sélectionnez **Suivant**.  

3. Sur le **application** page, sélectionnez l’option appropriée **environnement Azure**. Puis sélectionnez **importation** pour l’application web. Configurez les paramètres suivants dans le **importer des applications** fenêtre :  

    - **Nom du locataire Azure AD**: Ce nom est la façon dont il est nommé dans Configuration Manager  

    - **ID de locataire Azure AD**: Le **ID de répertoire** vous avez copié à partir d’Azure AD  

    - **ID de client** : Le **ID d’Application** vous avez copié à partir de l’application Azure AD  

    - **Clé secrète**: La clé **valeur** vous avez copié à partir de l’application Azure AD  

    - **Expiration de la clé secrète** : La même date d’expiration de la clé   

    - **URI ID d’application** : Ce paramètre doit remplir automatiquement avec la valeur suivante : `https://cmmicrosvc.manage.microsoft.com/`  
  
   Sélectionnez **Vérifiez**, puis sélectionnez **OK** pour fermer la fenêtre Importer des applications. Sélectionnez **suivant** sur la page application de l’Assistant Services Azure.  

4. Sur le **données de Diagnostic** page, configurez les paramètres suivants :  

    - **ID commercial**: cette valeur doit remplir automatiquement avec l’ID de votre organisation  

    - **Niveau de données de diagnostic de Windows 10**: sélectionnez au moins **avancé (limité)**  

    - **Autoriser le nom de l’appareil dans les données de diagnostic**: sélectionnez **activer**  
  
   Sélectionnez **Suivant**. Le **fonctionnalités disponibles** page affiche les fonctionnalités d’Analytique de bureau qui sont disponibles avec les paramètres de données de diagnostic à partir de la page précédente. Sélectionnez **Suivant**.  

5. Sur le **Collections** page, configurez les paramètres suivants :  

    - **Nom complet** : Le portail d’Analytique de bureau affiche cette connexion de Configuration Manager à l’aide de ce nom. Il permet de faire la distinction entre des hiérarchies différentes. Par exemple, *laboratoire de test* ou *production*.  

    - **Regroupement cible**: Cette collection inclut tous les appareils Configuration Manager configure avec votre ID commercial et les paramètres de données de diagnostic. Il est l’ensemble des appareils Configuration Manager se connecte au service d’Analytique de bureau.  

    - **Appareils du regroupement cible utilisent un proxy authentifié par l’utilisateur pour les communications sortantes**: Par défaut, cette valeur est **non**. Si nécessaire dans votre environnement, la valeur est **Oui**.  

    - **Sélectionner des regroupements spécifiques pour se synchroniser avec le bureau Analytique**: Sélectionnez **ajouter** pour inclure des collections supplémentaires. Ces collections sont disponibles dans le portail d’Analytique de bureau pour le regroupement des plans de déploiement. Veillez à inclure les collections d’exclusion de pilote et de pilote.  

        Ces collections continuent à synchroniser en tant que leurs changements d’appartenance. Par exemple, votre plan de déploiement utilise une collection avec une règle d’adhésion de Windows 7. Comme ces appareils mise à niveau vers Windows 10 et Configuration Manager évalue l’appartenance au regroupement, ces appareils déposent hors de la collecte et le plan de déploiement.  

6. Effectuez toutes les étapes de l'Assistant.  

Configuration Manager crée une stratégie de paramètres pour configurer les appareils du regroupement cible. Cette stratégie inclut les paramètres de données de diagnostic pour permettre aux appareils d’envoyer des données à Microsoft. Par défaut, les clients de mettre à jour stratégie toutes les heures. Après avoir reçu les nouveaux paramètres, il peut être plus de plusieurs heures avant que les données sont disponibles dans l’Analytique de bureau.

Surveiller la configuration de vos appareils pour l’Analytique de bureau. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Microsoft 365 Servicing** nœud, puis sélectionnez le **intégrité de la connexion** tableau de bord.  

Configuration Manager synchronise les plans de déploiement de bureau Analytique dans les 15 minutes de la création de la connexion. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Microsoft 365 Servicing** nœud, puis sélectionnez le **Plans de déploiement** nœud.



## <a name="create-a-desktop-analytics-deployment-plan"></a>Créer un plan de déploiement de bureau Analytique

Utilisez cette procédure pour créer un plan de déploiement dans l’Analytique de bureau.

1. Ouvrez le [portail d’Analytique de bureau](https://aka.ms/m365aprod). Utilisez les informations d’identification qui disposent au moins **contributeurs de l’espace de travail** autorisations.  

2. Sélectionnez **Plans de déploiement** dans le groupe de gestion.  

3. Dans le **Plans de déploiement** volet, sélectionnez **créer**.  

4. Dans le **création du plan de déploiement** volet, configurez les paramètres suivants :  

    - **Nom** : Planifier un nom unique pour le déploiement, par exemple `Office 365 pilot`  

    - **Produits et versions**: Sélectionnez le **Office** produit et la dernière version recommandée disponible. Par exemple, **clients Office 365, version 1808 (recommandé)**.  

    - **Groupes d’appareils**: Sélectionnez un ou plusieurs groupes, puis **définir en tant que groupes cibles**. Groupes avec **sccm** comme source sont collections synchronisées à partir du Gestionnaire de Configuration.  

    - **Règles de préparation**: Ces règles vous aide à déterminer quels appareils sont éligibles pour la mise à niveau. Sélectionnez **les Applications Office** et configurez les paramètres suivants :  

        - Mettre à jour d’Office 365 ProPlus à partir de 32 bits vers 64 bits. Ce paramètre s’applique uniquement aux appareils exécutant une version 64 bits de Windows. La valeur par défaut est **Oui**.  

        - Lors de la mise à jour à partir d’une version antérieure d’Office, laissez le champ plus anciens déconseillée applications Office. Ce comportement s’applique même si ces applications n’existent pas dans la version la plus récente de Microsoft Office. Le paramètre par défaut est **non**.  

        - Faible installer seuil du nombre de vos compléments Office. Le seuil par défaut est `2%`. Compléments sous ce seuil sont automatiquement définis pour *faible nombre d’installations*. Analytique de bureau ne valide pas ces compléments pendant la phase pilote. 

            Si un complément est installé sur un pourcentage plus élevé d’ordinateurs à ce seuil, le plan de déploiement marque le complément en tant que *Noteworthy*. Vous pouvez ensuite son importance pour tester pendant la phase pilote.  

    - **Date de fin**: Choisissez la date à laquelle Office doit être entièrement déployé à tous les appareils ciblés.  

5. Sélectionnez **créer**. Le nouveau plan s’affiche dans la liste des plans de déploiement lors de son traitement. Le traitement peut prendre jusqu'à 48 heures avant de procéder à l’étape suivante.  

6. Ouvrez le plan de déploiement en sélectionnant son nom.  

7. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier l’importance**.  

    1. Sur le **des compléments Office** onglet, sélectionnez cette option pour n’afficher que **pas été revues** actifs.  

    2. Sélectionnez chaque complément, puis **modifier**. Vous pouvez sélectionner plusieurs applications à modifier en même temps.  

    3. Choisissez un niveau d’importance dans le **Importance** liste. Si vous souhaitez Analytique de bureau pour valider le complément pendant la phase pilote, sélectionnez **critique** ou **Important**. Il ne valide pas les compléments marqués comme **pas Important**. Prendre en compte les risques de compatibilité et d’autres informations de plan lors de l’affectation de niveaux d’importance.  

        Lorsque vous affectez des niveaux d’importance, vous pouvez également choisir la décision de mise à niveau.  

    4. Sélectionnez **enregistrer** lorsque vous avez terminé.  

8. Dans le menu de plan de déploiement, dans le **préparation** groupe, sélectionnez **identifier pilote**.  

    1. Passez en revue les appareils recommandées pour le projet pilote.  

    2. Sélectionnez chaque appareil, puis **ajouter pilote**. Si vous êtes en désaccord avec la recommandation, sélectionnez **remplacer**.  

        Pour plus d’informations sur comment Desktop Analytique rend ces recommandations, sélectionnez l’icône d’information dans l’angle supérieur droit de la **identifier pilote** volet.



## <a name="deploy-office-365-in-configuration-manager"></a>Déployer Office 365 dans Configuration Manager

Utilisez cette procédure pour déployer Office 365 ProPlus dans Configuration Manager dans le groupe pilote.

- Si vous n’en avez pas, tout d’abord [créer une application pour Office 365 ProPlus](#bkmk_create-app)  

- [Déployer l’application](#bkmk_deploy-app) à l’aide du plan de déploiement de bureau Analytique  

- [Installer l’application](#bkmk_install-app) depuis le centre logiciel sur un appareil cible  

<!-- 
- [Monitor](#bkmk_monitor-app) status in Configuration Manager  
 -->

### <a name="bkmk_create-app"></a> Créer une application pour Office 365 ProPlus

1. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels**, puis sélectionnez le **gestion des clients Office 365** nœud. Sélectionnez le **le programme d’installation de Office 365** vignette du tableau de bord.  

2. Sur le **paramètres d’Application** , fournissez un **nom** pour cette application. Par exemple, `Office 365 ProPlus`. Si vous le souhaitez spécifier un **Description**. Spécifiez le **emplacement du contenu** pour les fichiers d’installation, puis sélectionnez **suivant**.  

3. Sur le **paramètres Office** page, sélectionnez **accéder à l’outil de personnalisation Office**. Configurer des paramètres de déploiement nécessaires pour votre installation Office 365 :  

    1. Dans le **produits et versions** groupe, sélectionnez **Office 365 ProPlus** à partir de la liste, puis sélectionnez **ajouter**.  

    2. Dans le **langage** groupe, sélectionnez la langue principale.  

    3. Dans le **mise à jour et mise à niveau** groupe, assurez-vous que le paramètre à **désinstaller toute version MSI d’Office, y compris Visio et Project** est **sur**.  

    4. Configurez les paramètres supplémentaires selon les besoins de votre organisation.  

    5. Lorsque vous avez terminé, sélectionnez **révision** dans le coin supérieur droit. Passez en revue les paramètres configurés, puis sélectionnez **envoyer**.  

4. Sélectionnez **Suivant**. Sur le **déploiement** page, sélectionnez **non** à déployer maintenant. (La procédure suivante utilise le plan de déploiement de bureau Analytique pour le déploiement.) Sélectionnez **suivant** et terminez l’Assistant.  


### <a name="bkmk_deploy-app"></a> Déployer Office 365 à l’aide du plan de déploiement de bureau Analytique

1. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels**, développez **Desktop Analytique maintenance**, puis sélectionnez le **Plans de déploiement** nœud.  

2. Sélectionnez votre plan de déploiement pilote d’Office 365, puis **détails du Plan de déploiement** dans le ruban.  

3. Dans le **piloter état** en mosaïque, choisissez **Application** dans la liste déroulante, puis sélectionnez **déployer**.  

4. Sur le **général** page de l’Assistant Déploiement de logiciel, sélectionnez **Parcourir** à côté du **logiciel** champ. Sélectionnez votre application Office 365, par exemple, **Office 365 ProPlus**. Sélectionnez **Suivant**.  

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


### <a name="bkmk_install-app"></a> Installer Office 365 depuis le centre logiciel

1. Connectez-vous à un appareil qui est membre du plan de déploiement pilote.  

2. Ouvrez **centre logiciel** et installer l’application disponible pour Office 365.  


<!--
### <a name="bkmk_monitor-app"></a> Monitor status in Configuration Manager
-->


## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour en savoir plus sur les plans de déploiement de bureau Analytique.
> [!div class="nextstepaction"]  
> [Plans de déploiement](/sccm/desktop-analytics/about-deployment-plans)
