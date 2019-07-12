---
title: Modifier l’autorité de gestion des appareils mobiles
titleSuffix: Configuration Manager
description: Découvrez comment changer l’autorité MDM de MDM hybride vers Intune autonome pour des utilisateurs spécifiques (autorité MDM mixte).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 05/21/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9ca39be68074213e4bb0a3f667ae69d5257f7a3c
ms.sourcegitcommit: 9670e11316c9ec6e5f78cd70c766bbfdf04ea3f9
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67818067"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte)

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez configurer une autorité MDM mixte dans le même client. Gérer certains utilisateurs dans Microsoft Intune et d’autres avec des appareils mobiles hybride Cet article fournit des informations sur comment commencer à déplacer les utilisateurs vers Intune autonome. Il part du principe que vous avez effectué les étapes suivantes :  

- Utilisation de l’outil d’importation de données pour [importer des objets Configuration Manager dans Intune](migrate-import-data.md) (facultatif).  

- [Préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md) pour garantir que les utilisateurs et leurs appareils restent gérés après la migration.  

> [!Note]  
> Une réinitialisation complète de votre client supprime toutes les stratégies, applications et les inscriptions d’appareils. Si vous décidez que vous voulez faire de ce processus, appelez le support pour obtenir une assistance.  

Gérer les utilisateurs migrés et leurs appareils dans Intune. Continuer à gérer d’autres appareils dans Configuration Manager. Pour vérifier que tout fonctionne comme prévu, démarrez avec un petit groupe test d’utilisateurs. Ensuite migrer progressivement les autres groupes d’utilisateurs. Lorsque vous êtes prêt, faire basculer l’autorité de gestion des appareils mobiles au niveau du locataire depuis Configuration Manager vers Intune autonome.

> [!Important]  
> Depuis le 13 août 2018, la gestion hybride des appareils mobiles est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, consultez [Qu’est-ce que la gestion hybride des appareils mobiles ?](/sccm/mdm/understand/hybrid-mobile-device-management)<!--Intune feature 2683117-->  



## <a name="things-to-know-before-you-migrate-users"></a>Éléments à connaître avant de lancer la migration des utilisateurs

- Lors de la migration en plusieurs phases, toutes les stratégies ou applications MDM existantes dans Configuration Manager continuent à s’appliquer aux appareils MDM hybrides.  

- Les appareils des utilisateurs inclus dans le regroupement associé à l’abonnement Intune peuvent s’inscrire à la gestion hybride des appareils mobiles. Tous les appareils associés à des utilisateurs non inclus dans la collection sont gérés dans Intune tant que l’utilisateur dispose d’une licence Intune/EMS.  

    > [!Note]  
    > Les utilisateurs peuvent s’inscrire dans la version autonome d’Intune, même si vous les avez bloqués via la console Configuration Manager. Pour empêcher un utilisateur de s’inscrire, ne concédez pas de licence aux utilisateurs indésirables pour Intune. Ils ne peuvent pas inscrire sans licence.<!--SCCMDocs issue 738-->  

- Lorsque vous faites migrer un utilisateur vers Intune, ses appareils et lui apparaissent dans Intune dans le portail Azure après 15 minutes environ.  

- Lorsque vous faites migrer des utilisateurs vers la version autonome d’Intune, continuez à gérer les paramètres suivants à partir de Configuration Manager pour les appareils MDM hybrides et de la version autonome d’Intune :  

    - [Certificat Apple Push Notification Service (APNs)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)  

    - [Programme d’inscription des appareils](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)  

        > [!Note]  
        > Vous n’avez pas besoin de recréer votre jeton DEP ou le supprimer à partir du Gestionnaire de Configuration. Il migre automatiquement à Intune 24 heures après le passage autorité de gestion des appareils mobiles du locataire depuis Configuration Manager à Intune. Cette modification est la dernière étape de la migration. (Si le jeton DEP ne migrez dans les 24 heures, contactez le support Microsoft pour obtenir une assistance.)  

    - Profils d’inscription  

    - [Licences du programme d’achat en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps)  

    - Identificateurs d’entreprise  

    - [Certificats de signature de code](/sccm/mdm/deploy-use/enroll-hybrid-windows)  

    - [Catégories d’appareils](/sccm/core/clients/manage/collections/automatically-categorize-devices-into-collections)  

    - [Gestionnaires d’inscription](/sccm/mdm/plan-design/device-enrollment-methods)  

    - Terms and conditions  

    - SLK Windows  

    - Personnalisation du portail d’entreprise  

    > [!Important]  
    > Continuez à modifier les stratégies au niveau du locataire à l’aide de la console Configuration Manager. Après avoir [autorité MDM au niveau du locataire](/sccm/mdm/deploy-use/change-mdm-authority) à Intune, les stratégies au niveau du locataire qui vous ont été la gestion dans le Gestionnaire de Configuration automatiquement migrent vers Intune sur Azure. Un exemple d’une telle stratégie est pour les certificats de service (APNs) de notifications Push Apple.<!--SCCMDocs issue #971-->  

- Si vous utilisez des certificats de signature de code, il est recommandé de migrer les utilisateurs selon une approche progressive. Une fois un appareil mobile migré, il effectue une demande de nouveau certificat auprès d’une autorité de certification. Le fait d’utiliser une approche progressive pour migrer des utilisateurs (et leurs appareils) limite le nombre de demandes simultanées d’autorité de certification.  

- Ne faites pas migrer de comptes d’utilisateur qui ont été ajoutés en tant que gestionnaires d’inscription d’appareil dans Configuration Manager. Plus tard, quand vous remplacerez votre autorité MDM au niveau du locataire par Intune, ces comptes d’utilisateur migreront correctement. Si vous ne migrez pas le compte d’utilisateur DEM avant le changement d’autorité de gestion des appareils mobiles au niveau du locataire, vous devez ajouter manuellement l’utilisateur en tant qu’une inscription dans Intune sur Azure. Toutefois, les appareils inscrits à l’aide d’un gestionnaire Device Emulator ne migrent correctement. Appelez le support technique pour faire migrer ces appareils. Pour plus d’informations, consultez [Ajouter un gestionnaire d’inscription d’appareil](https://docs.microsoft.com/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).  

    > [!Note]  
    > En mode autorité mixte, ne déplacez pas ces comptes vers Intune en les supprimant de la collection cloud de ConfigMgr. Si vous le faites, l’utilisateur devient un utilisateur standard et ne peut pas inscrire plus de 15 appareils. Au lieu de cela, migrez ces utilisateurs et leurs appareils une fois que vous passez entièrement l’autorité MDM du locataire.<!--Intune bug 2174210-->  

- Les appareils inscrits à l’aide d’un gestionnaire Device Emulator et les appareils sans [l’affinité utilisateur](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) ne sont pas migrés automatiquement vers la nouvelle autorité MDM. Pour modifier l’autorité de gestion de ces appareils MDM, consultez [Migrer des appareils sans affinité utilisateur](#migrate-devices-without-user-affinity).  



## <a name="migrate-users-to-intune"></a>Faire migrer des utilisateurs vers Intune

Pour tester si vos configurations Intune fonctionnent comme prévu, commencez par faire migrer un petit ensemble d’utilisateurs et leurs appareils. Ensuite, après avoir vérifié que tout fonctionne normalement, vous pouvez commencer la migration d’autres groupes AAD contenant davantage d’utilisateurs et leurs appareils.



## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Faire migrer un groupe d’utilisateurs de test vers la version autonome d’Intune

Les appareils des utilisateurs inclus dans le regroupement associé à l’abonnement Intune peuvent s’inscrire à la gestion hybride des appareils mobiles. Lorsque vous supprimez un utilisateur de la collection, si l’utilisateur possède une licence Intune, leurs appareils inscrits sont migrées vers la version autonome d’Intune. Si vous n’avez pas déjà affecté des licences aux utilisateurs que vous souhaitez migrer, consultez [attribuer des licences Intune à vos comptes utilisateur](https://docs.microsoft.com/intune/licenses-assign). Dans le regroupement de l’abonnement Intune, vous pouvez exclure des regroupements d’utilisateurs de votre regroupement principal pour faire migrer les utilisateurs inclus dans le regroupement exclu.

Dans l’exemple suivant, le regroupement d’utilisateurs hybrides contient tous les membres du regroupement de tous les utilisateurs. Cette configuration permet à tous chaque utilisateur d’inscrire un appareil à la gestion hybride des appareils mobiles. Pour faire migrer des utilisateurs vers la version autonome d’Intune, vous sélectionnez Exclure des regroupements et vous ajoutez un regroupement contenant les utilisateurs à faire migrer. Lorsque vous êtes prêt à faire migrer d’autres utilisateurs, ajoutez d’autres regroupements exclus qui incluent ces utilisateurs.

![Exclure des regroupements](../media/migrate-excludecollections.png)

> [!Note]  
>   Lorsque vous avez le **tous les utilisateurs** regroupement sélectionné pour l’abonnement Intune, vous n’êtes pas autorisé à ajouter une règle pour exclure des regroupements. Au lieu de cela, créez une nouvelle collection basée sur le **tous les utilisateurs** collection, vérifiez que la collection contient les utilisateurs attendent, puis modifiez l’abonnement Intune pour utiliser la nouvelle collection. Vous pouvez exclure des regroupements d’utilisateurs du nouveau regroupement pour faire migrer des utilisateurs. Si vous excluez un utilisateur à partir d’une collection, mais incluez un groupe dont l’utilisateur est membre, l’utilisateur n’est pas exclu de la collection.

Pour migrer un groupe d’utilisateurs test vers Intune, créez un regroupement d’utilisateurs contenant les utilisateurs pour effectuer la migration. Puis excluez le regroupement d’utilisateurs à partir de la collection qui est utilisée pour l’abonnement Intune.  

Le diagramme suivant donne une vue d’ensemble du fonctionnement de la migration d’utilisateurs.

![Vue d’ensemble de l’autorité mixte](../media/migrate-mixedauthority.svg)

1. Vérifiez que l’utilisateur dispose d’une licence Intune/EMS.  

2. Créez un regroupement à exclure du regroupement de l’abonnement Intune. Dans cet exemple, le regroupement **Tous les utilisateurs hybrides** contient une règle pour exclure des utilisateurs du regroupement **Pilote de migration**. **User1** est membre du regroupement **Pilote de migration** et exclu du regroupement **Tous les utilisateurs hybrides**.  

3. **User1**d’appareils sont désormais gérés à partir d’Intune dans le portail Azure.  

4. Tous les autres appareils continuent d’être gérés à partir de la console Configuration Manager.  

> [!Important]  
> Lorsque vous déplacez un utilisateur de la version hybride à la version autonome, la suppression de la stratégie est suspendue pendant sept jours.<!-- SCCMDocs issue #1066 -->


## <a name="verify-intune-standalone-functionality"></a>Vérifier la fonctionnalité de la version autonome d’Intune

Après avoir fait migrer un petit ensemble d’utilisateurs, vérifiez que leurs appareils sont répertoriés dans Intune. Accédez à **Appareils** et sélectionnez **Tous les appareils**.

Ensuite, vérifiez que vos stratégies, profils et applications fonctionnent comme prévu sur les appareils des utilisateurs.



## <a name="migrate-additional-users"></a>Faire migrer d’autres utilisateurs

Après avoir vérifié que la version autonome d’Intune fonctionne comme prévu, vous pouvez commencer la migration d’autres utilisateurs. Tout comme vous avez créé une collection avec un ensemble d’utilisateurs de test, créer des regroupements qui incluent les utilisateurs à faire migrer. Excluez ces regroupements à partir de la collection qui est associé à l’abonnement Intune. Pour plus d’informations, consultez [migrer un groupe d’utilisateurs test vers Intune autonome](#migrate-a-test-group-of-users-to-intune-standalone).



## <a name="migrate-devices-without-user-affinity"></a>Migrer des appareils sans affinité utilisateur

Pour migrer des appareils individuels formulaire Configuration Manager vers Intune qui ont été inscrits sans affinité utilisateur, utilisez l’applet de commande Switch-MdmDeviceAuthority PowerShell.  Une fois la migration des appareils sélectionnés à l’aide de l’applet de commande, valider dans Intune dans Azure qui s’est produite lors de la migration en tant que prévu pour les appareils sélectionnés. Puis, lorsque vous êtes prêt, vous pouvez changer l’autorité MDM sur Intune pour le client effectuer la migration pour tous les appareils restants que Configuration Manager comme leur autorité de gestion des appareils mobiles.

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>RÉSUMÉ

La cmdlet change l’autorité de gestion des appareils MDM sans affinité utilisateur (par exemple, appareils inscrits en bloc). L’applet de commande bascule entre Intune et Configuration Manager autorités de gestion. Il bascule pour les périphériques spécifiés selon leurs autorités de gestion lorsque vous exécutez l’applet de commande.

### <a name="syntax"></a>SYNTAXE

`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARAMÈTRES

#### `-Credential <PSCredential>`

Objet d’informations d’identification PowerShell pour le compte d’utilisateur Azure AD qui est utilisé lors du changement des autorités de gestion de l’appareil. Si le paramètre n’est pas spécifié, l’utilisateur est invité pour les informations d’identification. Le rôle d’annuaire de ce compte d’utilisateur doit être **Administrateur général** ou **Administrateur limité** avec le rôle d’administration **Administrateur Intune**.

#### `-DeviceIds <Guid[]>`

Les ID des appareils de gestion des appareils mobiles dont l’autorité de gestion doit être modifiée. Les ID d’appareil sont des identificateurs uniques pour les appareils affichés par la console Configuration Manager.

#### `-Force [<SwitchParameter>]`

Spécifiez le paramètre pour désactiver l’invite Doit continuer.

#### `-LogFilePath <string>`

Chemin vers l’emplacement du fichier journal.

#### `-LoggingLevel <SourceLevels>`

Niveau de journal utilisé pour déterminer le type de journaux qui doivent être écrits dans le fichier journal.

Voici les valeurs possibles pour LoggingLevel :

- ActivityTracing
- Tous
- Critique
- Error
- Information
- Hors tension
- Détaillé
- Warning

#### `-Confirm [<SwitchParameter>]`

Vous invite à confirmer l’opération avant d’exécuter la commande.

#### `-WhatIf [<SwitchParameter>]`

Décrit ce qui se passerait si vous avez exécuté la commande sans exécuter la commande.

#### `<CommonParameters>`

Cette applet de commande prend en charge les paramètres communs : Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable et OutVariable. Pour plus d'informations, consultez [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216).

### <a name="example-1"></a>Exemple 1

``` powershell
C:\PS>Switch-MdmDeviceAuthority -Credential $creds -DeviceIds $deviceIds

  DeviceId       : 62e6ea43-18f8-4278-bcd4-a4baed2c6d24
  Success        : True
  FailureReason  :
  NewAuthority   : Intune
  CompletionTime : 11/15/2017 8:00:11 PM

Description

-----------

Successfully switched the management authority of the device from Configuration Manager to Intune.
```

### <a name="remarks"></a>REMARQUES

- Pour voir les exemples, tapez : `get-help Switch-MdmDeviceAuthority -examples`  
- Pour plus d’informations, tapez : `get-help Switch-MdmDeviceAuthority -detailed`  
- Pour des informations techniques, tapez : `get-help Switch-MdmDeviceAuthority -full`  
- Pour de l’aide en ligne, tapez : `get-help Switch-MdmDeviceAuthority -online`  



## <a name="next-steps"></a>Étapes suivantes

Après avoir effectué la migration d’utilisateurs et testé la fonctionnalité d’Intune, déterminez si vous êtes prêt à [faire passer l’autorité de gestion des appareils mobiles](migrate-change-mdm-authority.md) de votre locataire Intune de Configuration Manager vers Intune.
