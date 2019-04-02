---
title: Utiliser Azure AD pour la cogestion
titleSuffix: Configuration Manager
description: Avec Azure AD, vous pouvez tirer parti d’une productivité accrue pour vos utilisateurs et de la sécurité pour vos ressources, à la fois dans des environnements cloud et local
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3b773c0bfe8cd0f8253a67ac96f5a0113b7206c0
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754936"
---
# <a name="use-azure-ad-for-co-management"></a>Utiliser Azure AD pour la cogestion

Dans le cloud, l’identité est le nouveau plan de contrôle. Azure AD (Azure Active Directory) vous permet de lier vos utilisateurs, appareils et applications à la fois dans des environnements cloud et local. L’inscription de vos appareils sur Azure AD vous permet d’améliorer la productivité des utilisateurs et la sécurité des ressources. La présence des appareils dans Azure AD représente le point de départ pour la cogestion et l’accès conditionnel en fonction de l’appareil. 

Pour plus d’informations sur l’accès conditionnel en fonction de l’appareil, consultez [Guide pratique pour exiger des appareils gérés pour accéder aux applications cloud avec l’accès conditionnel](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

Dans la vidéo suivante, le program manager senior, Sandeep Deo, et le directeur du marketing produit, Adam Harbour, parlent et font la démonstration d’Azure AD pour la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD fournit deux options pour les appareils appartenant à l’entreprise afin de répondre aux besoins de votre organisation :  

- **Appareil joint à Azure AD** : Joignez vos appareils Windows 10 à Azure AD sans avoir besoin de les joindre à votre annuaire Active Directory local  

    - Prend en charge Windows 10

    - Installation sans exiger de configuration supplémentaire sur vos environnements locaux  

    - En activant quelques paramètres dans Azure AD, vous pouvez permettre à vos utilisateurs de joindre des appareils à Azure AD via l’installation Windows (OOBE)  

    - Pour plus d'informations, consultez la rubrique [Procédure : planifier une implémentation de jonction Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Appareil joint à Azure AD hybride** : Joignez vos appareils joints à un domaine existants à Azure AD  

    - Prend en charge Windows 10, Windows 8.1 et Windows 7

    - Installation en utilisant des revendications AD FS ou Azure AD Connect  

    - Pour Windows 10, la jointure ayant lieu dans le contexte de l’ordinateur, les utilisateurs n’ont pas à effectuer des étapes supplémentaires  

    - Pour plus d’informations, consultez [Guide pratique pour planifier l’implémentation de la jonction Azure Active Directory hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Les deux options fournissent des fonctionnalités similaires aux utilisateurs. Il vous revient de choisir l’une des deux selon vos besoins. Par exemple, vous pouvez [accéder à vos ressources locales](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) à partir des machines jointes à Azure AD même si elles ne sont pas jointes à Active Directory. 

Vous pouvez joindre des appareils à Azure AD dans différents environnements, quelle que soit votre [méthode d’authentification](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Par exemple, l’authentification fédérée ou l’authentification cloud. 

Si vous avez déjà un annuaire Active Directory local, la configuration des deux options est simple. 



## <a name="benefits"></a>Avantages

La jonction d’appareils à Azure AD offre les avantages suivants à votre organisation :

#### <a name="single-sign-on-to-cloud-resources"></a>Authentification unique pour les ressources cloud
Sur les appareils joints à Azure AD, vous bénéficiez d’une expérience intégrée en matière d’accès à toutes les ressources cloud ou en local. Une fois que vous êtes connecté à un ordinateur Windows qui est joint à Azure AD, vous obtenez l’authentification unique pour toutes les applications sans invites de connexion supplémentaires.  

#### <a name="windows-hello-for-business"></a>Windows Hello Entreprise
Windows Hello Entreprise apporte une authentification sans mot de passe renforcée pour Windows 10. En joignant vos appareils à Azure AD, vous pouvez activer Windows Hello Entreprise sur votre base d’utilisateurs pour les ressources cloud et en local. Windows Hello Entreprise élimine le problème de la mémorisation de mots de passe complexes ou de leur exposition par inadvertance. Son processus de connexion est simple et sécurisé. 

Pour plus d’informations, consultez [Windows Hello Entreprise](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Accès conditionnel en fonction de l’appareil
Activez l’accès conditionnel basé sur l’état de l’appareil pour mieux protéger les données de votre organisation. L’accès conditionnel en fonction de l’appareil nécessite un appareil géré. Cet appareil doit être un appareil conforme ou un appareil joint à Azure AD hybride. Pour les appareils joints à Azure AD, vous avez besoin d’Intune pour marquer l’appareil comme conforme. En revanche, pour les appareils joints à Azure AD hybride, l’état de l’appareil est utilisé pour évaluer l’accès conditionnel. La cogestion vous fournit l’avantage supplémentaire de l’évaluation de la conformité via Intune pour les appareils joints à Azure AD hybride. Cette fonctionnalité permet de s’assurer que la configuration de l’appareil est intacte. 

Pour plus d’informations sur l’accès conditionnel en fonction de l’appareil, consultez [Guide pratique pour exiger des appareils gérés pour accéder aux applications cloud avec l’accès conditionnel](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Gestion automatique des licences des appareils
Tous les appareils Windows 10 joints à Azure AD passent par des vérifications de licences. Ces vérifications vous permettent d’effectuer automatiquement leur mise à niveau de la version Pro vers la version Enterprise via le cloud Microsoft. Quand vous supprimez l’abonnement approprié de l’utilisateur, l’appareil passe automatiquement à une version antérieure de sa licence. Cette fonctionnalité fournit un seul volet de contrôle pour la gestion des licences Windows, sans aucun processus complexe ni système local.

#### <a name="self-service-functionality"></a>Fonctionnalité de libre-service
La fonctionnalité de libre-service inclut la réinitialisation du mot de passe libre-service et la clé de récupération BitLocker. Azure AD vous offre également des options directes pour réinitialiser votre mot de passe ou accéder aux clés de récupération BitLocker. Vous pouvez utiliser Azure AD pour réinitialiser votre mot de passe directement à partir de l’écran de verrouillage Windows, et non à partir d’un navigateur web. Ces fonctionnalités réduisent les frictions pour les utilisateurs et aident à réduire les coûts du support technique pour votre organisation.  

Pour plus d’informations, consultez [Démarrage rapide : réinitialisation du mot de passe libre-service](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>Enterprise State Roaming
Tous les appareils joints à Azure AD peuvent synchroniser leurs paramètres vers le cloud. Tout appareil auquel un utilisateur se connecte synchronise tous ses paramètres pour une expérience plus productive.  



## <a name="value-proposition"></a>Proposition de valeur

La jonction de vos appareils à Azure AD via les deux méthodes accélère votre transformation numérique. Elle active davantage de fonctionnalités fournies par Microsoft 365. Vos expériences seront meilleures et la sécurité de vos données sera renforcée. 

Azure AD offre plusieurs options pour atténuer votre charge de travail, par exemple :

- Gérer toutes les identités d’appareils dans votre organisation à partir d’un emplacement unique  

- Réduire vos coûts de support technique en activant la réinitialisation du mot de passe libre-service. Vos utilisateurs peuvent alors réinitialiser le mot de passe à partir de l’écran de verrouillage Windows 10 sur votre appareil à tout moment.  



## <a name="configure"></a>Configurer

Si vous disposez déjà d’un environnement Active Directory local et que vous souhaitez joindre vos appareils joints à un domaine à Azure AD, configurez des appareils joints à Azure AD hybride. Pour plus d’informations, consultez [Guide pratique pour planifier l’implémentation de la jonction Azure Active Directory hybride](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

Configuration Manager a un paramètre du client pour [Inscrire automatiquement les nouveaux appareils joints au domaine Windows 10 auprès d’Azure Active Directory](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Pour plus d’informations sur la configuration des paramètres du client, consultez [Guide pratique pour configurer les paramètres des clients](/sccm/core/clients/deploy/configure-client-settings).

Si vous souhaitez configurer la jonction à Azure AD pour vos appareils sans les joindre également à votre domaine local, passez en revue les considérations pour la jonction à Azure AD dans votre environnement. Une fois que vous avez choisi d’utiliser la jonction à Azure AD, vous disposez de nombreuses options pour la déployer en fonction des besoins de votre organisation. Pour plus d’informations, consultez les articles suivants :
- [Comment : planifier une implémentation de jonction Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Comprendre vos options de provisionnement](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

