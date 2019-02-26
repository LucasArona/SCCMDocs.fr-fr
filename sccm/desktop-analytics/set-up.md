---
title: Configurer les Analyses du bureau
titleSuffix: Configuration Manager
description: Guide pratique pour configurer et d’intégration pour l’Analytique de bureau.
ms.date: 01/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9bd3a9efcbc76647ae39eb1a104b401b112d15fb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754836"
---
# <a name="how-to-set-up-desktop-analytics"></a>Comment configurer le bureau Analytique 

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Utilisez cette procédure pour vous connecter à l’Analytique de bureau et le configurer dans votre abonnement. Cette procédure est un processus unique pour configurer Desktop Analytique pour votre organisation.  



## <a name="initial-onboarding"></a>Intégration initiale

1. Ouvrez le [portail d’Analytique de Desktop](https://aka.ms/m365aprod) dans Gestion des appareils Microsoft 365 en tant qu’utilisateur avec **administrateur d’entreprise** autorisations. Sélectionnez **Démarrer**.  

2. Sur le **accepter le contrat de service** page, passez en revue le contrat de service, puis sélectionnez **Accept**.  

3. Sur le **confirmer votre abonnement** passez en revue la liste des requis les licences éligibles. Basculer le paramètre sur **Oui** regard **avez-vous un des abonnements pris en charge ou une version ultérieure**, puis sélectionnez **suivant**.  

4. Sur le **accorder l’accès des utilisateurs et applications** page, bureau Analytique préconfigure les deux groupes de sécurité dans Azure Active Directory :  

    - **Propriétaires de l’espace de travail**: Créer et gérer des espaces de travail. Ces comptes ont besoin d’un accès propriétaire à l’abonnement Azure.  

    - **Contributeurs de l’espace de travail**: Créer et gérer des plans de déploiement dans cet espace de travail. Ils ne doivent tout accès Azure supplémentaires.  
  
   Pour ajouter un utilisateur au groupe, tapez son nom ou l’adresse électronique dans le **Entrez le nom ou adresse de messagerie** section du groupe approprié. Lorsque vous avez terminé, sélectionnez **suivant**. 

5. Sur la page pour **configurer votre espace de travail**:  

    - Pour utiliser un espace de travail pour l’Analytique de bureau, sélectionnez-le, puis passez à l’étape suivante.  

        > [!Note]  
        > Si vous utilisez déjà Windows Analytique, sélectionnez ce même espace de travail. Vous devez réinscrire les appareils pour l’Analytique de bureau que vous avez précédemment inscrit dans Windows Analytique. 
        > 
        > Vous ne pouvez avoir qu’un espace de travail Analytique de bureau par le locataire Azure AD. Appareils peuvent envoyer uniquement les données de diagnostic pour un espace de travail.   

    - Pour créer un espace de travail pour l’Analytique de bureau, sélectionnez **ajouter l’espace de travail**.  

        1. Entrez un **nom de l’espace de travail**.<!--do we have any guidance for this name?-->  

        2. Sélectionnez la liste déroulante à **sélectionnez le nom de l’abonnement Azure pour cet espace de travail**, puis choisissez l’abonnement Azure pour cet espace de travail.  

        3. Sélectionnez le **région** dans la liste, puis sélectionnez **ajouter**.  

6. Sélectionnez un espace de travail nouveau ou existant, puis **définir comme espace de travail Analytique de bureau**.  Puis sélectionnez **continuer** dans le **confirmer et accorder l’accès** boîte de dialogue.  

7. Dans le nouvel onglet de navigateur, choisissez un compte à utiliser pour vous connecter. Sélectionnez l’option **donner son consentement au nom de votre organisation** et sélectionnez **Accept**.  

    > [!Note]  
    > Ce consentement consiste à affecter l’application MALogAnalyticsReader le rôle de lecture du journal Analytique à l’espace de travail. Ce rôle d’application est requise par l’Analytique de bureau. Pour plus d’informations, consultez [rôle d’application MALogAnalyticsReader](/sccm/desktop-analytics/troubleshooting#bkmk_MALogAnalyticsReader).  

8. Revenez à la page à **configurer votre espace de travail**, sélectionnez **suivant**.  

9. Sur le **dernières étapes** page, sélectionnez **accéder au bureau Analytique**. 

Le portail Azure affiche l’Analytique de Desktop **accueil** page.



## <a name="create-app-for-configuration-manager"></a>Créer des applications pour Configuration Manager

Créer une application dans Azure AD pour Configuration Manager.

1. Dans le [Azure portal](http://portal.azure.com), accédez à **Azure Active Directory**, puis sélectionnez **inscriptions**. Puis sélectionnez **nouvelle inscription d’application**.  

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
