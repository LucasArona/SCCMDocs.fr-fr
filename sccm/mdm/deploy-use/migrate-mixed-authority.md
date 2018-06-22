---
title: Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte)
titleSuffix: Configuration Manager
description: Découvrez comment changer l’autorité MDM en passant de MDM hybride à la version autonome d’Intune pour certains utilisateurs.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: 6f0201d7-5714-4ba0-b2bf-d1acd0203e9a
ms.openlocfilehash: 46fb1333c58f3010acde4d064044a124050d211a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350603"
---
# <a name="change-the-mdm-authority-for-specific-users-mixed-mdm-authority"></a>Changer l’autorité MDM pour des utilisateurs spécifiques (autorité MDM mixte) 

*S’applique à : System Center Configuration Manager (Current Branch)*    

Vous pouvez configurer une autorité MDM mixte dans le même locataire en choisissant de gérer certains utilisateurs dans Intune et d’autres avec MDM hybride (Intune intégré à Configuration Manager). Cet article fournit des informations sur la façon de commencer à déplacer les utilisateurs vers la version autonome d’Intune autonome et part du principe que vous avez terminé les étapes suivantes :
- Utilisation de l’outil d’importation de données pour [importer des objets Configuration Manager dans Intune](migrate-import-data.md) (facultatif).
- [préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md) pour que les utilisateurs et leurs appareils restent gérés après la migration ;

> [!Note]    
> Si vous décidez d’effectuer une réinitialisation complète de votre locataire, ce qui supprime toutes les stratégies, applications et inscriptions d’appareils, appelez le support pour obtenir de l’aide.

Les utilisateurs qui ont migré et leurs appareils sont gérés dans Intune tandis que les autres appareils continuent d’être gérés dans Configuration Manager. Vous commencez avec un petit groupe d’utilisateurs de test pour vérifier que tout fonctionne comme prévu. Ensuite, vous faites migrer progressivement les autres groupes d’utilisateurs jusqu’à ce que vous soyez prêt à faire basculer l’autorité MDM au niveau du locataire depuis Configuration Manager vers la version autonome d’Intune. 

## <a name="things-to-know-before-you-migrate-users"></a>Éléments à connaître avant de lancer la migration des utilisateurs
- Lors de la migration en plusieurs phases, toutes les stratégies ou applications MDM existantes dans Configuration Manager continuent à s’appliquer aux appareils MDM hybrides.
- Les appareils des utilisateurs inclus dans le regroupement associé à l’abonnement Intune peuvent s’inscrire à la gestion hybride des appareils mobiles. Tous les appareils associés à des utilisateurs non inclus dans la collection sont gérés dans Intune tant que l’utilisateur dispose d’une licence Intune/EMS. 
- Lorsque vous faites migrer un utilisateur vers Intune, ses appareils et lui apparaissent dans Intune dans le portail Azure après 15 minutes environ.  
- Lorsque vous faites migrer des utilisateurs vers la version autonome d’Intune, continuez à gérer les paramètres suivants à partir de Configuration Manager pour les appareils MDM hybrides et de la version autonome d’Intune :
    - [Certificat Apple Push Notification Service (APNs)](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac)
    - [Programme d’inscription des appareils](/sccm/mdm/deploy-use/ios-device-enrollment-program-for-hybrid)
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
  > Continuez à modifier les stratégies au niveau du locataire à l’aide de la console Configuration Manager. Après avoir [remplacé votre autorité MDM au niveau du locataire](change-mdm-authority.md) par Intune, vous gérez ces stratégies dans Intune sur Azure. 
-   Si vous utilisez des certificats de signature de code, il est recommandé de migrer les utilisateurs selon une approche progressive. Une fois un appareil mobile migré, il effectue une demande de nouveau certificat auprès d’une autorité de certification. Le fait d’utiliser une approche progressive pour migrer des utilisateurs (et leurs appareils) limite le nombre de demandes simultanées d’autorité de certification.
- Nous vous recommandons de ne pas faire migrer des comptes d’utilisateur qui ont été ajoutés en tant que gestionnaires d’inscription d’appareil dans Configuration Manager. Plus tard, quand vous remplacerez votre autorité MDM au niveau du locataire par Intune, ces comptes d’utilisateur migreront correctement. Si vous faites migrer le compte d’utilisateur gestionnaire d’inscription d’appareil avant de modifier l’autorité MDM au niveau du locataire, vous devez ajouter manuellement l’utilisateur en tant que gestionnaire d’inscription d’appareil dans Intune sur Azure. Toutefois, les appareils inscrits à l’aide d’un gestionnaire d’inscription d’appareil ne migrent pas correctement. Vous devez appeler le support technique pour faire migrer ces appareils. Pour plus d’informations, consultez [Ajouter un gestionnaire d’inscription d’appareil](https://docs.microsoft.com/en-us/intune/device-enrollment-manager-enroll#add-a-device-enrollment-manager).
- Les appareils inscrits à l’aide d’un gestionnaire d’inscription d’appareil et les appareils sans [affinité utilisateur](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) ne migrent automatiquement pas vers la nouvelle autorité MDM. Pour modifier l’autorité de gestion de ces appareils MDM, consultez [Migrer des appareils sans affinité utilisateur](#migrate-devices-without-user-affinity).

## <a name="migrate-users-to-intune"></a>Faire migrer des utilisateurs vers Intune
Pour tester si vos configurations Intune fonctionnent comme prévu, commencez par faire migrer un petit ensemble d’utilisateurs et leurs appareils. Ensuite, après avoir vérifié que tout fonctionne normalement, vous pouvez commencer la migration d’autres groupes AAD contenant davantage d’utilisateurs et leurs appareils.

## <a name="migrate-a-test-group-of-users-to-intune-standalone"></a>Faire migrer un groupe d’utilisateurs de test vers la version autonome d’Intune
Les appareils des utilisateurs inclus dans le regroupement associé à l’abonnement Intune peuvent s’inscrire à la gestion hybride des appareils mobiles. Lorsque vous supprimez un utilisateur du regroupement, ses appareils inscrits migrent vers la version autonome d’Intune si une licence Intune lui est attribuée. Si vous n’avez pas déjà attribué des licences aux utilisateurs que vous envisagez de faire migrer, consultez [Affecter des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/licenses-assign). Dans le regroupement de l’abonnement Intune, vous pouvez exclure des regroupements d’utilisateurs de votre regroupement principal pour faire migrer les utilisateurs inclus dans le regroupement exclu. 

Dans l’exemple suivant, le regroupement d’utilisateurs hybrides contient tous les membres du regroupement de tous les utilisateurs. Ainsi, tout utilisateur peut inscrire un appareil à la gestion hybride des appareils mobiles. Pour faire migrer des utilisateurs vers la version autonome d’Intune, vous sélectionnez Exclure des regroupements et vous ajoutez un regroupement contenant les utilisateurs à faire migrer. Lorsque vous êtes prêt à faire migrer d’autres utilisateurs, vous pouvez ajouter d’autres regroupements exclus qui incluent ces utilisateurs. 

![Exclure des regroupements](../media/migrate-excludecollections.png)

> [!Note] 
> Lorsque le regroupement **Tous les utilisateurs** est sélectionné pour l’abonnement Intune, vous n’êtes pas autorisé à ajouter une règle pour exclure des regroupements. Créez un nouveau regroupement basé sur le regroupement **Tous les utilisateurs**, vérifiez que le regroupement contient les utilisateurs attendus, puis modifiez l’abonnement Intune pour utiliser le nouveau regroupement. Vous pouvez exclure des regroupements d’utilisateurs du nouveau regroupement pour faire migrer des utilisateurs. 

Pour faire migrer un groupe d’utilisateurs de test vers Intune, créez un regroupement d’utilisateurs contenant les utilisateurs à faire migrer, puis excluez le regroupement d’utilisateurs du regroupement utilisé pour l’abonnement Intune.   

Le diagramme suivant donne une vue d’ensemble du fonctionnement de la migration d’utilisateurs.

 ![Vue d’ensemble de l’autorité mixte](../media/migrate-mixedauthority.svg)

1. Vérifiez que l’utilisateur dispose d’une licence Intune/EMS. 
2. Créez un regroupement à exclure du regroupement de l’abonnement Intune. Dans cet exemple, le regroupement **Tous les utilisateurs hybrides** contient une règle pour exclure des utilisateurs du regroupement **Pilote de migration**. **User1** est membre du regroupement **Pilote de migration** et exclu du regroupement **Tous les utilisateurs hybrides**. 
3. Les appareils de **User1** sont désormais gérés à partir d’Intune dans le portail Azure. 
4. Tous les autres appareils continuent d’être gérés à partir de la console Configuration Manager. 

## <a name="verify-intune-standalone-functionality"></a>Vérifier la fonctionnalité de la version autonome d’Intune
Après avoir fait migrer un petit ensemble d’utilisateurs, vérifiez que leurs appareils sont répertoriés dans Intune. Accédez au panneau **Appareils** et sélectionnez **Tous les appareils**. 

Ensuite, vérifiez que vos stratégies, profils, applications, etc. fonctionnent comme prévu sur les appareils des utilisateurs.

## <a name="migrate-additional-users"></a>Faire migrer d’autres utilisateurs
Après avoir vérifié que la version autonome d’Intune fonctionne comme prévu, vous pouvez commencer la migration d’autres utilisateurs. Tout comme vous avez créé un regroupement avec un ensemble d’utilisateurs de test, créez des regroupements qui contiennent des utilisateurs à faire migrer et excluez ces regroupements du regroupement associé à l’abonnement Intune. Pour plus d’informations, consultez [Regroupement associé à votre abonnement Intune](#collection-associated-with-your-intune-subscription).

## <a name="migrate-devices-without-user-affinity"></a>Migrer des appareils sans affinité utilisateur
Les appareils inscrits à l’aide d’un gestionnaire d’inscription d’appareil et les appareils sans [affinité utilisateur](/sccm/mdm/deploy-use/user-affinity-for-hybrid-managed-devices) ne migrent automatiquement pas vers la nouvelle autorité MDM. Vous pouvez utiliser la cmdlet PowerShell *Switch-MdmDeviceAuthority* pour basculer entre les autorités de gestion Intune et Configuration Manager dans les scénarios suivants : 

-   Scénario 1 : utilisez la cmdlet *Switch-MdmDeviceAuthority* pour migrer les appareils sélectionnés et valider qu’ils peuvent être gérés à l’aide d’Intune dans Azure. Puis, lorsque vous êtes prêt, vous pouvez [utiliser Intune comme autorité MDM pour le locataire](migrate-change-mdm-authority.md) afin de terminer la migration des appareils. 
-   Scénario 2 : lorsque vous êtes prêt à utiliser Intune comme autorité MDM pour le locataire, vous pouvez exécuter les actions suivantes pour migrer vos appareils sans affinité utilisateur :
    - Utilisez la cmdlet pour changer l’autorité MDM pour vos appareils sans affinité utilisateur avant [d’utiliser Intune comme autorité MDM pour le locataire](migrate-change-mdm-authority.md).    
    - Contactez le support technique pour commuter les appareils sans affinité utilisateur après avoir choisi d’utiliser Intune comme autorité MDM pour le locataire.

Pour changer l’autorité de gestion pour ces appareils MDM, vous pouvez utiliser la cmdlet *Switch-MdmDeviceAuthority* pour basculer entre les autorités de gestion Intune et Configuration Manager. 

### <a name="cmdlet-switch-mdmdeviceauthority"></a>Cmdlet *Switch-MdmDeviceAuthority*

#### <a name="synopsis"></a>SYNOPSIS
La cmdlet change l’autorité de gestion des appareils MDM sans affinité utilisateur (par exemple, appareils inscrits en bloc). La cmdlet bascule entre les autorités de gestion Intune et Configuration Manager pour les appareils spécifiés en fonction des autorités de gestion spécifiées sur ces appareils lorsque vous exécutez la cmdlet.

### <a name="syntax"></a>SYNTAXE
`Switch-MdmDeviceAuthority -DeviceIds <Guid[]> [-Credential <PSCredential>] [-Force] [-LogFilePath <string>] [-LoggingLevel {Off | Critical | Error | Warning | Information | Verbose | ActivityTracing | All}] [-Confirm] [-WhatIf] [<CommonParameters>]`


### <a name="parameters"></a>PARAMÈTRES
#### `-Credential <PSCredential>`
Objet d’informations d’identification PowerShell pour le compte d’utilisateur Azure AD qui est utilisé lors du changement des autorités de gestion de l’appareil. Si le paramètre n’est pas spécifié, l’utilisateur est invité à fournir les informations d’identification. Le rôle d’annuaire de ce compte d’utilisateur doit être **Administrateur général** ou **Administrateur limité** avec le rôle d’administration **Administrateur Intune**.

#### `-DeviceIds <Guid[]>`
Les ID des appareils MDM qui ont besoin de leur autorité de gestion ont changé. Les ID d’appareil sont des identificateurs uniques pour les appareils affichés par la console Configuration Manager.

#### `-Force [<SwitchParameter>]`
Spécifiez le paramètre pour désactiver l’invite Doit continuer.<br>
 
#### `-LogFilePath <string>`
Chemin vers l’emplacement du fichier journal.
 
#### `-LoggingLevel <SourceLevels>`
Niveau de journal utilisé pour déterminer le type de journaux qui doivent être écrits dans le fichier journal.
 
Voici les valeurs possibles pour LoggingLevel :

  - ActivityTracing
  - Tout
  - Critique
  - Erreur
  - Informations
  - Désactivé
  - Verbose
  - Avertissement
 
#### `-Confirm [<SwitchParameter>]`
Vous demande confirmation avant d'exécuter la commande.
 
#### `-WhatIf [<SwitchParameter>]`
Décrit ce qui se passerait si vous exécutiez la commande sans réellement l'exécuter.
 
#### `<CommonParameters>`
Cette applet de commande prend en charge les paramètres courants : Verbose, Debug, ErrorAction, ErrorVariable, WarningAction, WarningVariable, OutBuffer, PipelineVariable et OutVariable. Pour plus d'informations, consultez [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

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
Après avoir fait migrer des utilisateurs et testé la fonctionnalité d’Intune, déterminez si vous êtes prêt à [faire passer l’autorité MDM](migrate-change-mdm-authority.md) de votre locataire Intune de Configuration Manager vers Intune. 