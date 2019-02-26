---
title: Utiliser Azure AD pour la cogestion
titleSuffix: Configuration Manager
description: Avec Azure AD vous pouvez tirer parti d’une productivité accrue pour vos utilisateurs et de la sécurité pour vos ressources, dans des environnements cloud et local
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
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754936"
---
# <a name="use-azure-ad-for-co-management"></a>Utiliser Azure AD pour la cogestion

Dans le cloud, identité est le nouveau plan de contrôle. Azure Active Directory (Azure AD) vous permet de lier vos utilisateurs, les appareils et les applications dans des environnements cloud et locales. Inscrire vos appareils à Azure AD vous permet d’améliorer la productivité de vos utilisateurs et de sécurité pour vos ressources. Avoir des appareils dans Azure AD est la fondation pour la cogestion et accès conditionnel basé sur l’appareil. 

Pour plus d’informations sur l’accès conditionnel basé sur un appareil, consultez [How To : Exiger que les appareils gérés pour accéder aux applications de cloud avec l’accès conditionnel](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices)

Dans la vidéo suivante, responsable de programme senior Sandeep Deo et de produits marketing manager Adam Harbour discuter et démonstration Azure AD pour la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD fournit deux options pour les appareils d’entreprise en fonction des besoins de votre organisation :  

- **Appareils joints à AD Azure**: Joindre vos appareils Windows 10 à Azure AD sans avoir besoin de les joindre à votre annuaire local Active Directory.  

    - Prend en charge de Windows 10

    - Configurer sans configuration supplémentaire pour vos environnements locaux  

    - En activant quelques paramètres dans Azure AD, vous pouvez autoriser vos utilisateurs joindre des appareils à Azure AD via l’expérience d’installation de Windows (OOBE)  

    - Pour plus d'informations, consultez la rubrique [Procédure : Planifier votre implémentation de la jointure Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  

- **Hybride des appareils joints à AD Azure**: Joindre vos appareils joints à un domaine existants à Azure AD  

    - Prend en charge de Windows 10, Windows 8.1 et Windows 7

    - Configurer à l’aide de revendications AD FS ou Azure AD Connect  

    - Pour Windows 10 la jointure ayant lieu dans le contexte de l’ordinateur, les utilisateurs n’êtes pas obligé d’effectuer des étapes supplémentaires  

    - Pour plus d’informations, consultez [comment planifier votre implémentation de jonction hybride Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)  

Les deux options fournissent des fonctionnalités similaires pour les utilisateurs. Il est flexible, vous pouvez choisir le des deux selon vos besoins. Par exemple, vous pouvez [accéder à vos ressources locales](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) à partir des ordinateurs joints à AD Azure même si elles ne sont pas joints à Active Directory. 

Vous pouvez joindre des appareils à Azure AD dans différents environnements, non quel que soit votre [méthode d’authentification](https://docs.microsoft.com/azure/security/azure-ad-choose-authn). Par exemple, l’authentification fédérée, ou l’authentification cloud. 

Si vous avez déjà un annuaire local Active Directory, la configuration de des deux options est simple. 



## <a name="benefits"></a>Avantages

Jonction d’appareils à Azure AD offre les avantages suivants à votre organisation :

#### <a name="single-sign-on-to-cloud-resources"></a>L’authentification unique aux ressources de cloud
Sur les appareils joints à Azure AD, vous obtenez une expérience intégrée, l’accès à toutes les ressources cloud ou en local. Une fois que vous êtes connecté à un ordinateur Windows qui est joint à Azure AD, vous obtenez l’authentification unique à toutes les applications sans les invites d’authentification supplémentaires.  

#### <a name="windows-hello-for-business"></a>Windows Hello entreprise
Windows Hello entreprise apporte une authentification sans mot de passe renforcée pour Windows 10. En joignant vos appareils à Azure AD, vous pouvez activer Windows Hello entreprise sur votre utilisateur de base pour les ressources de cloud et locales. Windows Hello entreprise élimine le problème de mémorisation de mots de passe complexes ou de les exposer par inadvertance. Son processus de connexion est simple et sécurisé. 

Pour plus d’informations, consultez [Windows Hello Entreprise](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

#### <a name="device-based-conditional-access"></a>Accès conditionnel basé sur l’appareil
Activer l’accès conditionnel basé sur l’état de l’appareil pour mieux protéger les données de votre organisation. Accès conditionnel basé sur l’appareil nécessite un appareil géré. Cet appareil doit être un appareil conforme ou un hybride des appareils joints à AD Azure. Pour les appareils joints à AD Azure, vous avez besoin d’Intune pour marquer l’appareil comme conforme. Mais pour hybride Azure les appareils joints à AD, l’état de l’appareil est utilisé pour évaluer l’accès conditionnel. Cogestion vous fournit l’avantage supplémentaire de l’évaluation de conformité via Intune hybride Azure pour les appareils joints à AD. Cette fonctionnalité permet de s’assurer de que la configuration de l’appareil est intacte. 

Pour plus d’informations sur l’accès conditionnel basé sur un appareil, consultez [How To : Exiger que les appareils gérés pour accéder aux applications de cloud avec l’accès conditionnel](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

#### <a name="automatic-device-licensing"></a>Licences d’appareils automatique
Tous les appareils Windows 10 joints à Azure AD passent par la vérification de la licence. Ces vérifications permettent de mettre automatiquement à niveau les à partir de Pro dans l’entreprise via le cloud de Microsoft. Lorsque vous supprimez l’abonnement approprié à partir de l’utilisateur, l’appareil rétrograde automatiquement sa licence. Cette fonctionnalité fournit un seul volet de contrôle pour la gestion des licences de Windows, sans tous les processus complexes ou des systèmes locaux.

#### <a name="self-service-functionality"></a>Fonctionnalité de libre-service
Fonctionnalité de libre-service inclut la réinitialisation de mot de passe libre-service et la clé de récupération BitLocker. Azure AD vous offre également des options directes pour réinitialiser votre mot de passe ou d’accéder aux clés de récupération BitLocker. Vous pouvez utiliser Azure AD pour réinitialiser votre mot de passe directement à partir de l’écran de verrouillage Windows, au lieu d’à partir d’un navigateur web. Ces fonctionnalités réduisent la friction pour les utilisateurs et les aider à réduire les coûts du support technique pour votre organisation.  

Pour plus d’informations, consultez [Guide de démarrage rapide : Réinitialisation de mot de passe libre-service](https://docs.microsoft.com/azure/active-directory/authentication/quickstart-sspr).

#### <a name="enterprise-state-roaming"></a>État entreprise itinérance
Tous les appareils joints à Azure AD peuvent se synchroniser leurs paramètres dans le cloud. N’importe quel appareil auquel un utilisateur connecte dans les synchronisations tous leurs paramètres pour une expérience plus productive.  



## <a name="value-proposition"></a>Proposition de valeur

Jointure de vos appareils à Azure AD via les deux méthodes accélère votre transformation numérique. Il permet davantage de fonctionnalités fournie par Microsoft 365. Vous aurez une meilleure expérience, et vous aurez une meilleure sécurité pour vos données. 

Azure AD offre plusieurs options pour faciliter votre travail de charge, par exemple :

- Gérer toutes les identités d’appareil dans votre organisation à partir d’un emplacement unique  

- Réduisez vos coûts de support technique en activant la réinitialisation de mot de passe libre-service. Puis vous les utilisateurs pourrez réinitialiser votre mot de passe à partir de l’écran de verrouillage Windows 10 sur votre appareil à tout moment.  



## <a name="configure"></a>Configurer

Si vous disposez déjà d’un environnement d’Active Directory en local, et que vous souhaitez joindre vos appareils joints au domaine à Azure AD, configurer hybride Azure appareils joints à AD. Pour plus d’informations, [comment planifier votre implémentation de jonction hybride Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan). 

Configuration Manager a un paramètre du client pour [enregistre automatiquement les nouveaux appareils Windows 10 joints au domaine avec Azure AD](/sccm/core/clients/deploy/about-client-settings#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Pour plus d’informations sur la configuration des paramètres client, consultez [comment configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).

Si vous souhaitez configurer Azure AD-jointure pour vos appareils sans également de les joindre à votre domaine local, passez en revue les considérations pour Azure AD-jointure dans votre environnement. Une fois que vous choisi d’utiliser Azure AD join, vous disposez de nombreuses options pour le déployer en fonction des besoins de votre organisation. Pour plus d’informations, consultez les articles suivants :
- [Comment : Planifier votre implémentation de la jointure Azure AD](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan)  
- [Comprendre vos options d’approvisionnement](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  

