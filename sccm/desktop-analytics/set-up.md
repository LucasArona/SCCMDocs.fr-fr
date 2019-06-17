---
title: Configurer les Analyses du bureau
titleSuffix: Configuration Manager
description: Guide pratique pour configurer et d’intégration pour l’Analytique de bureau.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: a54a6ad56e8ae7504314e5147f4d4d5b0b726562
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67145972"
---
# <a name="how-to-set-up-desktop-analytics"></a>Comment configurer le bureau Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Utilisez cette procédure pour vous connecter à l’Analytique de bureau et le configurer dans votre abonnement. Cette procédure est un processus unique pour configurer Desktop Analytique pour votre organisation.  



## <a name="initial-onboarding"></a>Intégration initiale

1. Ouvrez le [portail d’Analytique de Desktop](https://aka.ms/desktopanalytics) dans Gestion des appareils Microsoft 365 en tant qu’utilisateur avec le **administrateur général** rôle. Sélectionnez **Démarrer**.  

    > [!Tip]  
    > Pour accéder au portail de l’Analytique de bureau à partir de la console Configuration Manager, accédez à la **bibliothèque de logiciels** espace de travail, sélectionnez le **Desktop Analytique maintenance** nœud, puis sélectionnez **planifier déploiements**.

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

5. Sur la page pour **configurer votre espace de travail**:  

    > [!Note]  
    > Effectuez cette étape en tant qu’un **propriétaire de l’espace de travail** ou **contributeur**. Pour plus d’informations, consultez [conditions préalables](/sccm/desktop-analytics/overview#prerequisites).  

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


## <a name="next-steps"></a>Étapes suivantes

Passez à l’article suivant pour connecter Configuration Manager avec l’Analytique de bureau.
> [!div class="nextstepaction"]  
> [Connecter Configuration Manager](/sccm/desktop-analytics/connect-configmgr)  
