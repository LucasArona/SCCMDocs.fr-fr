---
title: Configurer les Analyses du bureau
titleSuffix: Configuration Manager
description: Guide pratique pour configurer et d’intégration pour l’Analytique de bureau.
ms.date: 04/15/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7f59e7a9feb53370b069852b871ce2a2c333dda0
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62258195"
---
# <a name="how-to-set-up-desktop-analytics"></a>Comment configurer le bureau Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Utilisez cette procédure pour vous connecter à l’Analytique de bureau et le configurer dans votre abonnement. Cette procédure est un processus unique pour configurer Desktop Analytique pour votre organisation.  



## <a name="initial-onboarding"></a>Intégration initiale

1. Ouvrez le portail d’Analytique de bureau dans Gestion des appareils Microsoft 365 en tant qu’utilisateur avec **administrateur d’entreprise** autorisations. Sélectionnez **Démarrer**.  

2. Sur le **accepter le contrat de service** page, passez en revue le contrat de service, puis sélectionnez **Accept**.  

3. Sur le **confirmer votre abonnement** passez en revue la liste des requis les licences éligibles. Basculer le paramètre sur **Oui** regard **avez-vous un des abonnements pris en charge ou une version ultérieure**, puis sélectionnez **suivant**.  

4. Sur le **donner aux utilisateurs accès** page :

    - **Voulez-vous vraiment Analytique de bureau pour gérer les rôles d’annuaire pour vos utilisateurs**: Analytique de postes de travail affecte automatiquement la **propriétaires de l’espace de travail** et **contributeurs de l’espace de travail** regroupe à la **Desktop Analytique Administrator** rôle. Si ces groupes sont déjà un **administrateur général**, il n’existe aucune modification.  

        Si vous ne sélectionnez pas cette option, bureau Analytique ajoute toujours les utilisateurs en tant que membres des groupes de sécurité de deux. Un **administrateur général** doit affecter manuellement la **Desktop Analytique Administrator** rôle pour les utilisateurs.  

        Pour plus d’informations sur l’attribution d’autorisations de rôle d’administrateur dans Azure Active Directory et les autorisations affectées aux **les administrateurs de bureau Analytique**, consultez [autorisations du rôle administrateur dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Postes de travail Analytique préconfigure les deux groupes de sécurité dans Azure Active Directory :  

        - **Propriétaires de l’espace de travail**: Un groupe de sécurité pour créer et gérer des espaces de travail. Ces comptes ont besoin d’un accès propriétaire à l’abonnement Azure.  

        - **Contributeurs de l’espace de travail**: Un groupe de sécurité pour créer et gérer des plans de déploiement dans cet espace de travail. Ils ne doivent tout accès Azure supplémentaires.  

        Pour ajouter un utilisateur au groupe, tapez son nom ou l’adresse électronique dans le **Entrez le nom ou adresse de messagerie** section du groupe approprié. Lorsque vous avez terminé, sélectionnez **suivant**.

L’étape suivante peut être effectuée par un **propriétaire de l’espace de travail** ou **contributeur**. Consultez [conditions préalables.](/sccm/desktop-analytics/overview#prerequisites) 

5. Sur la page pour **configurer votre espace de travail**:  

    - Pour utiliser un espace de travail pour l’Analytique de bureau, sélectionnez-le, puis passez à l’étape suivante.  

        > [!Note]  
        > Si vous utilisez déjà Windows Analytique, sélectionnez ce même espace de travail. Vous devez réinscrire les appareils pour l’Analytique de bureau que vous avez précédemment inscrit dans Windows Analytique.
        >
        > Vous ne pouvez avoir qu’un espace de travail Analytique de bureau par le locataire Azure AD. Appareils peuvent envoyer uniquement les données de diagnostic pour un espace de travail.  

    - Pour créer un espace de travail pour l’Analytique de bureau, sélectionnez **ajouter l’espace de travail**.  

        1. Entrez un **nom de l’espace de travail**.<!--do we have any guidance for this name?-->  

        2. Sélectionnez la liste déroulante à **sélectionnez le nom de l’abonnement Azure pour cet espace de travail**, puis choisissez l’abonnement Azure pour cet espace de travail.  
        
        3. **Créer de nouveaux** groupe de ressources ou **utiliser l’existant**. 

        4. Sélectionnez le **région** dans la liste, puis sélectionnez **ajouter**.  

6. Sélectionnez un espace de travail nouveau ou existant, puis **définir comme espace de travail Analytique de bureau**.  Puis sélectionnez **continuer** dans le **confirmer et accorder l’accès** boîte de dialogue.  

7. Dans le nouvel onglet de navigateur, choisissez un compte à utiliser pour vous connecter. Sélectionnez l’option **donner son consentement au nom de votre organisation** et sélectionnez **Accept**.  

    > [!Note]  
    > Ce consentement consiste à affecter l’application MALogAnalyticsReader le rôle de lecture du journal Analytique à l’espace de travail. Ce rôle d’application est requise par l’Analytique de bureau. Pour plus d’informations, consultez [rôle d’application MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Revenez à la page à **configurer votre espace de travail**, sélectionnez **suivant**.  

9. Sur le **dernières étapes** page, sélectionnez **accéder au bureau Analytique**.

Le portail Azure affiche l’Analytique de Desktop **accueil** page.



## <a name="create-app-for-configuration-manager"></a>Créer des applications pour Configuration Manager

Créer une application dans Azure AD pour Configuration Manager.

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



## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour connecter Configuration Manager avec l’Analytique de bureau.
> [!div class="nextstepaction"]  
> [Connecter Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
