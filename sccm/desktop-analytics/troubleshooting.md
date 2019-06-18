---
title: Résoudre les problèmes de postes de travail Analytique
titleSuffix: Configuration Manager
description: Détails techniques pour vous aider à résoudre les problèmes avec l’Analytique de bureau.
ms.date: 06/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e08f3f-9558-4ed7-9bf3-3a185ddaac5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 305c31c2a40e51b84a0a5da671db1c3f6dad6f2e
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158999"
---
# <a name="troubleshoot-desktop-analytics"></a>Résoudre les problèmes de postes de travail Analytique

Utilisez les détails dans cet article pour vous aider à résoudre les problèmes d’Analytique de bureau intégré à Configuration Manager.



## <a name="confirm-prerequisites"></a>Confirmer la configuration requise

Nombreux problèmes courants sont causés par les composants requis manquants. Vérifiez d’abord les configurations suivantes :

- [Conditions préalables](/sccm/desktop-analytics/overview#prerequisites)  

- [Mises à jour du composant de Windows](/sccm/desktop-analytics/enroll-devices#update-devices)  

- [Comment activer le partage de données](/sccm/desktop-analytics/enable-data-sharing), qui couvre les rubriques suivantes :  

    - Les points de terminaison Internet auquel les clients doivent se connecter  

    - Authentification du serveur proxy  

    - Niveaux de données de diagnostic  



## <a name="monitor-connection-health"></a>Surveiller l’intégrité de la connexion

Utilisez le **intégrité de la connexion** tableau de bord dans le Gestionnaire de Configuration pour explorer des catégories par intégrité de l’appareil. Dans la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, développez le **Desktop Analytique maintenance** nœud, puis sélectionnez le **intégrité de la connexion** tableau de bord.  

Pour plus d’informations, consultez [surveiller l’intégrité de la connexion](/sccm/desktop-analytics/monitor-connection-health).


## <a name="log-files"></a>Fichiers journaux

Pour plus d’informations, consultez [fichiers journaux pour le bureau Analytique](/sccm/core/plan-design/hierarchy/log-files#desktop-analytics)

### <a name="enable-verbose-logging"></a>Activer la journalisation documentée

1. Sur le point de connexion, accédez à la clé de Registre suivante : `HKLM\Software\Microsoft\SMS\Tracing\SMS_SERVICE_CONNECTOR`  
2. Définir le **LogLevel** valeur `0`  
3. (Facultatif) Exécutez la commande SQL suivante sur la base de données de site :  

    ```SQL
    DELETE FROM M365AProperties WHERE Name = 'M365ATenantUpdateInfo_LastUpdateTime'
    ```

4. Redémarrez le **SMS_EXECUTIVE** service sur le serveur de site



## <a name="bkmk_AzureADApps"></a> Applications Azure AD

Analytique de postes de travail ajoute les applications suivantes à votre Azure AD :

- **Gestionnaire de configuration de Microservice**: Se connecte à Configuration Manager avec des postes de travail Analytique. Cette application n’a aucune exigence d’accès.  

- **MALogAnalyticsReader**: Récupère les groupes d’OMS et les appareils créés dans le journal Analytique. Pour plus d’informations, consultez [rôle d’application MALogAnalyticsReader](#bkmk_MALogAnalyticsReader).  

Si vous devez configurer ces applications après l’installation terminée, accédez à la **services connectés** volet. Sélectionnez **configurer l’accès des utilisateurs et des applications**et configurer les applications.  

- **L’application Azure AD pour Configuration Manager**. Si vous avez besoin configurer ou résoudre les problèmes de connexion après l’installation terminée, consultez [application de créer et d’importation pour le Gestionnaire de Configuration](#create-and-import-app-for-configuration-manager). Cette application nécessite **écrire les données de Collection CM** et **lire les données de Collection CM** sur le **Configuration Manager Service** API.  


### <a name="create-and-import-app-for-configuration-manager"></a>Créer et importer des applications pour Configuration Manager

Si vous ne peut pas créer cette application Azure AD à partir de l’Assistant Configurer les Services Azure dans Configuration Manager, procédez comme suit pour créer et importer l’application pour le Gestionnaire de Configuration manuellement.

#### <a name="create-app-in-azure-ad"></a>Créer l’application dans Azure AD

1. Ouvrez le [portail Azure](http://portal.azure.com) en tant qu’utilisateur avec des autorisations d’administrateur d’entreprise, accédez à **Azure Active Directory**, puis sélectionnez **inscriptions**. Puis sélectionnez **nouvelle inscription d’application**.  

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

#### <a name="import-app-in-configuration-manager"></a>Application d’importation dans Configuration Manager

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**. Sélectionnez **configurer les Services Azure** dans le ruban.  

2. Sur le **Azure Services** page de l’Assistant Services Azure, configurez les paramètres suivants :  

    - Spécifiez un **Nom** pour l’objet dans Configuration Manager.  

    - Spécifiez une **Description** facultative pour vous aider à identifier le service.  

    - Sélectionnez **Desktop Analytique** dans la liste des services disponibles.  
  
   Sélectionnez **Suivant**.  

3. Sur le **application** page, sélectionnez l’option appropriée **environnement Azure**. Puis sélectionnez **importation** pour l’application web. Configurez les paramètres suivants dans le **importer des applications** fenêtre :  

    - **Nom du locataire Azure AD**: Ce nom est la façon dont il est nommé dans Configuration Manager  

    - **ID de locataire Azure AD**: Le **ID de répertoire** vous avez copié à partir d’Azure AD  

    - **ID de client** : Le **ID d’Application** vous avez copié à partir de l’application Azure AD  

    - **Clé secrète**: La clé **valeur** vous avez copié à partir de l’application Azure AD  

    - **Expiration de la clé secrète** : La même date d’expiration de la clé  

    - **URI ID d’application** : Ce paramètre doit remplir automatiquement avec la valeur suivante : `https://cmmicrosvc.manage.microsoft.com/`  
  
   Sélectionnez **Vérifiez**, puis sélectionnez **OK** pour fermer la fenêtre Importer des applications. Sélectionnez **suivant** sur la page application de l’Assistant Services Azure.  

Pour continuer le reste de l’Assistant sur le **données de Diagnostic** page, consultez [se connecter au service](/sccm/desktop-analytics/connect-configmgr#bkmk_connect).

#### <a name="troubleshoot-app-in-configuration-manager"></a>Résoudre les problèmes d’application dans Configuration Manager

Si vous rencontrez des problèmes de création ou importation de l’application, la première vérification **SMSAdminUI.log** sur l’erreur concernée. Puis vérifiez les configurations suivantes :

- Vous avez correctement inscrit le client au service d’Analytique de bureau. Pour plus d’informations, consultez [comment configurer le bureau Analytique](/sccm/desktop-analytics/set-up).

- Tous les requis de points de terminaison sont accessibles. Pour plus d’informations, consultez [points de terminaison](/sccm/desktop-analytics/enable-data-sharing#endpoints).

- Assurez-vous que l’utilisateur qui se connecte dispose des autorisations appropriées. Pour plus d’informations, consultez [Prérequis](/sccm/desktop-analytics/overview#prerequisites).

- Assurez-vous que l’utilisateur peut se connecter à Azure en général. Cette action détermine s’il existe toute général Azure AD problèmes d’authentification.

- Vérifiez les messages d’état pour le **SMS_SERVICE_CONNECTOR** composant concernant le *travail d’Analytique de bureau*.


### <a name="bkmk_MALogAnalyticsReader"></a> Rôle d’application MALogAnalyticsReader

Lorsque vous configurez l’Analytique de bureau, vous acceptez au nom de votre organisation. Ce consentement consiste à affecter l’application MALogAnalyticsReader le rôle de lecture du journal Analytique à l’espace de travail. Ce rôle d’application est requise par l’Analytique de bureau.

S’il existe un problème avec ce processus pendant l’installation, utilisez le processus suivant pour ajouter manuellement cette autorisation :

1. Accédez à la [Azure portal](http://portal.azure.com), puis sélectionnez **toutes les ressources**. Sélectionnez l’espace de travail de type **Analytique de journal**.  

2. Dans le menu de l’espace de travail, sélectionnez **contrôle d’accès (IAM)** , puis sélectionnez **ajouter**.  

3. Dans le **ajouter des autorisations** panel, configurez les paramètres suivants :  

    - **Rôle**: **Lecture du journal Analytique**  

    - **Attribuer l’accès à**: **Azure AD utilisateur, groupe ou application**  

    - **Sélectionnez**: **MALogAnalyticsReader**  

4. Sélectionnez **Enregistrer**.

Le portail affiche une notification qu’il ajoute l’attribution de rôle.


## <a name="data-latency"></a>Latence des données

<!-- 3846531 -->
Lorsque vous configurez tout d’abord Analytique de bureau, les rapports dans Configuration Manager et le portail d’Analytique de bureau peut ne pas affichent les données complètes tout de suite. Elle peut prendre 2 à 3 jours pour les étapes suivantes se produise :

- Périphériques actifs envoient des données de diagnostic pour le service d’Analytique de bureau
- Le service traite les données
- Le service se synchronise avec votre site Configuration Manager

Lors de la synchronisation des regroupements de périphériques à partir de votre hiérarchie Configuration Manager pour l’Analytique de bureau, il peut prendre jusqu'à 10 minutes pour les collections d’apparaître dans le portail d’Analytique de bureau. De même, lorsque vous créez un plan de déploiement dans l’Analytique de bureau, il peut prendre jusqu'à 10 minutes pour les nouveaux regroupements associés au plan de déploiement apparaissent dans votre hiérarchie Configuration Manager. Les sites principaux créent les collections, et le site d’administration centrale se synchronise avec Analytique de bureau.

Dans le portail d’Analytique de bureau, il existe deux types de données : **Données d’administration** et **données de diagnostic**:

- **Données d’administration** fait référence à toute modification apportée à votre configuration de l’espace de travail. Par exemple, lorsque vous modifiez d’une ressource **décision de mettre à niveau** ou **Importance** vous modifiez les données d’administration. Ces modifications ont souvent un effet de composition, car ils peuvent modifier l’état de préparation d’un appareil à l’élément multimédia en question installé.

- **Données de diagnostic** fait référence aux métadonnées système chargées à partir d’appareils clients à Microsoft. Ces données alimente Analytique de bureau. Il inclut des attributs tels que de l’inventaire des appareils, et état de mise à jour de sécurité et fonctionnalité.

Par défaut, toutes les données dans l’Analytique de bureau portail est automatiquement actualisées quotidiennement. Cette actualisation inclut des modifications dans les données de diagnostic et les modifications que vous apportez à la configuration (données d’administration). Il doit être visible dans votre portail d’Analytique de bureau en 08 h 00 UTC chaque jour.

Lorsque vous apportez des modifications aux données de l’administrateur, vous pouvez déclencher une actualisation à la demande des données administrateur dans votre espace de travail. À partir de n’importe quelle page dans le portail d’Analytique de bureau, ouvrez le menu volant devise de données :

![Capture d’écran de l’onglet de menu volant de devise de données dans le portail d’Analytique de bureau](media/data-currency-flyout.png)

Puis sélectionnez **appliquer les modifications**:

![Capture d’écran du menu volant de devise de données étendues dans le portail d’Analytique de bureau](media/data-currency-flyout-expand.png)

Ce processus prend généralement entre 15 à 60 minutes. La synchronisation dépend de la taille de votre espace de travail et l’étendue des modifications nécessitant des processus. Lorsque vous demandez une actualisation des données de la demande, il ne produit pas de toutes les modifications de données de diagnostic.  Pour plus d’informations, consultez le [Desktop Analytique FAQ](/sccm/desktop-analytics/faq#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).

Si vous ne voyez pas les modifications mises à jour dans les délais indiqués ci-dessus, attendez 24 heures pour la prochaine actualisation quotidienne. Si vous voyez des délais plus longs, consultez le tableau de bord service health. Si le service signale comme étant saine, contactez le support Microsoft.<!-- 3896921 -->
