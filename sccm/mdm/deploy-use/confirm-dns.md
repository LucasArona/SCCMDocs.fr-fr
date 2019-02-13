---
title: Confirmer les exigences relatives aux noms de domaine
titleSuffix: Configuration Manager
description: Confirmez les exigences relatives aux noms de domaine via System Center Configuration Manager.
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 522c2e82-20eb-4f38-859b-d55640b24e32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0e80a001153012763f56686df66ab7c6fcbf9b88
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127386"
---
# <a name="confirm-domain-name-requirements-with-system-center-configuration-manager-and-microsoft-intune"></a>Confirmer les exigences relatives aux noms de domaine via System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Si nécessaire, procédez comme suit pour satisfaire les éventuelles dépendances externes à Configuration Manager :

1. Chaque utilisateur doit disposer d’une licence Intune pour l’inscription des appareils. Pour que la solution puisse associer des licences Intune avec des utilisateurs, chaque utilisateur doit disposer d’un nom d’utilisateur principal (UPN) qui peut être résolu publiquement (par exemple johndoe@contoso.com) ou un ID de connexion de substitution configuré dans Azure Active Directory. La configuration d’un ID de connexion de substitution permet aux utilisateurs de se connecter avec une adresse e-mail, même si leur UPN est au format NetBIOS (par exemple, CONTOSO\johndoe).

   - Si votre entreprise utilise des UPN qui peuvent être résolues publiquement (par exemple johndoe@contoso.com), aucune configuration supplémentaire n’est nécessaire.
   - Si votre entreprise utilise un UPN qui ne peut pas être résolu (par exemple CONTOSO\johndoe), vous devez [configurer un ID de substitution dans Azure Active Directory](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect-get-started-custom/#pages-under-the-section-sync).

2. Déployez et configurez les services ADFS (Active Directory Federation Services). (Facultatif)

    Quand vous configurez l’authentification unique, vos utilisateurs peuvent se connecter à l’aide de leurs informations d’identification d’entreprise pour accéder aux services d’Intune.

    Pour plus d'informations, consultez les rubriques suivantes :
   -   [Préparer l’authentification unique](http://go.microsoft.com/fwlink/?LinkID=271124)
   -   [Planifier et déployer AD FS 2.0 en vue d’une utilisation avec l’authentification unique](http://go.microsoft.com/fwlink/?LinkID=271125)

3. Déploiement et configuration de la synchronisation d'annuaires

    La synchronisation de répertoires vous permet de remplir Intune avec des comptes d’utilisateur synchronisés. Les comptes d’utilisateur et les groupes de sécurité synchronisés sont ajoutés à Intune. L’échec d’activation de la synchronisation d’annuaires est une cause courante de l’incapacité des appareils à s’inscrire lors de la configuration du MDM Configuration Manager avec Microsoft Intune.

    Pour plus d’informations, consultez [Intégration d’annuaire](http://go.microsoft.com/fwlink/?LinkID=271120) dans la bibliothèque de documentation d’Active Directory.

4. Facultatif et non recommandé : Si vous n’utilisez pas Active Directory Federation Services, réinitialiser les mots de passe utilisateurs Microsoft Online.

    Si vous n'utilisez pas AD FS, vous devez définir un mot de passe Microsoft Online pour chaque utilisateur.

> [!div class="button"]
> [< Étape précédente](create-mdm-collection.md) [Étape suivante >](configure-intune-subscription.md)
