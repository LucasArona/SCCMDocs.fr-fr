---
title: Comment fermer votre compte
titleSuffix: Configuration Manager
description: Suppression d’Analytique de bureau à partir de votre compte Azure
ms.date: 07/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6e7d2850-b0af-497e-bbc1-bfc2a7420a7a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e2b1c893204366581eacd0f8e953cb2a6fd0d1a4
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67676169"
---
# <a name="how-to-close-your-account"></a>Comment fermer votre compte

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Si vous configurez Analytique de bureau dans votre environnement et que vous décidez ensuite que vous devez la supprimer, utilisez ce processus pour fermer votre compte.

## <a name="contact-support"></a>Contactez le support technique

La première étape consiste à contacter le Support Microsoft. Ouvrez une demande de support pour fermer votre compte Analytique de bureau. Ne passez pas à des étapes supplémentaires jusqu'à ce que vous recevez la confirmation que votre compte est clôturé par Microsoft.

## <a name="delete-the-solution"></a>Supprimer la solution

1. Se connecter à la [Azure portal](https://portal.azure.com) en tant qu’utilisateur avec le **administrateur général** rôle.

1. Rechercher dans **toutes les ressources** pour le nom de votre espace de travail Analytique de bureau. Ce nom est ce que vous avez créé lors de l’inscription pour le service.

1. Supprimer `Microsoft365Analytics(YourWorkspaceName)` de type **Solution**.

Les données d’Analytique de bureau soient obsolètes en fonction de votre stratégie de rétention de données pour l’espace de travail. Vous pouvez continuer à l’aide d’autres solutions dans le même espace de travail.

> [!Important]  
> Si vous utilisez l’espace de travail Analytique de journal avec d’autres solutions telles que Windows Analytique, ne supprimez pas l’espace de travail.

## <a name="remove-user-and-app-access"></a>Supprimer l’accès utilisateur et l’application

1. Se connecter à la [Azure portal](https://portal.azure.com) en tant qu’utilisateur avec le **administrateur général** rôle. Accédez à **Azure Active Directory**.

1. Dans **rôles et administrateurs**, recherchez le **administrateur de bureau Analytique** rôle. Supprimer ses membres.

1. Dans **groupes**, supprimer les membres des groupes suivants :

    - **M365 Administrateurs de Client Analytique (propriétaires d’Analytique de journal)**
    - **M365 Administrateurs de Client Analytique (contributeurs d’Analytique de journal)**

1. Dans **applications d’entreprise**, supprimer ou de révoquer des autorisations d’accès pour les applications suivantes :

    - `MaLogAnalyticsReader`

    - L’application de ConfigMgr. Pour rechercher le nom de cette application, accédez à la console Configuration Manager. Dans le **Administration** espace de travail, développez **Services Cloud**, puis sélectionnez le **Azure Services** nœud. Ouvrez les propriétés de la **Desktop Analytique** de service, puis basculez vers le **Applications** onglet. Le **application Web** est cette application Azure.

        > [!Important]  
        > Avant d’apporter des modifications à cette application dans Azure AD, assurez-vous que vous n'êtes pas réutiliser avec un autre service dans le Gestionnaire de Configuration.

## <a name="disconnect-configuration-manager"></a>Déconnecter le Gestionnaire de Configuration

1. Ouvrez la console Configuration Manager en tant qu’utilisateur avec le **administrateur complet** rôle.

1. Accédez à la **Administration** espace de travail, développez **Services Cloud**, puis sélectionnez le **Azure Services** nœud.

1. Supprimer le service d’Analytique de bureau.

## <a name="reconfigure-clients"></a>Reconfigurer les clients

### <a name="unenroll-devices"></a>Annuler l’inscription de périphériques

Sur les appareils inscrits, supprimez la valeur de CommercialID de clés de Registre de Windows suivantes :

- `HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection`
- `HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection`

### <a name="windows-diagnostic-data-configuration"></a>Configuration des données de diagnostic de Windows

Si vous ne souhaitez pas vos appareils à continuer à envoyer des données de diagnostic :

- Windows 10 : définissez le niveau de données de diagnostic sur **sécurité**
- Windows 7 SP1 ou 8.1 : désactiver le **données commerciales Opt-in clé**

Définissez ces valeurs en utilisant l’une des méthodes suivantes :

- Dans la stratégie, de groupe **Configuration ordinateur** > **modèles d’administration** > **les composants Windows**  >  **Collecte des données et les versions d’évaluation**
- Gestion des appareils mobiles (MDM), tel que [Microsoft Intune](https://docs.microsoft.com/intune/device-restrictions-windows-10#reporting-and-telemetry)

Pour plus d’informations, consultez [Configurer les données de diagnostic Windows dans votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization).

> [!NOTE]  
> Lorsque vous appliquez ces modifications, les appareils arrêter immédiatement l’envoi des données de diagnostic. Il peut prendre 24 à 48 heures pour Microsoft d’arrêter le traitement des insights pour votre espace de travail. Microsoft supprime ces données à partir de ses services cloud dans les 30 jours ou moins.
