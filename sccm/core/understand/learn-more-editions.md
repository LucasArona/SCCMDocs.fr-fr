---
title: Licences et branches
titleSuffix: Configuration Manager
description: En savoir plus sur les conditions de licence pour les options d’installation disponibles avec Configuration Manager
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02c0839bf7587fa9ee1421bf7035e31a3ca59cd1
ms.sourcegitcommit: a6a6507e01d819217208cfcea483ce9a2744583d
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2019
ms.locfileid: "66748098"
---
# <a name="licensing-and-branches-for-system-center-configuration-manager"></a>Licences et branches pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*

Utilisez cet article pour en savoir plus sur les conditions de licence pour les options d’installation disponibles avec System Center Configuration Manager. Ces options d’installation incluent les branches suivantes :

- Current Branch
- Long-Term Servicing Branch (LTSB)
- Installation d’évaluation de Current Branch
- Branche Technical Preview

## <a name="licensing-overview"></a>Vue d’ensemble des licences

Les clients dotés d’un contrat Software Assurance (SA) sur les licences de System Center Configuration Manager ou dotés de droits d’abonnement équivalents à compter du 1er octobre 2016 ont le droit d’utiliser la version 1606 d’octobre 2016 de System Center Configuration Manager. Les clients dotés de droits sur System Center Configuration Manager à la date du ou après le 1er octobre 2016 se voient proposer deux options de licence lors de l’installation : Current Branch et Long-Term Servicing Branch (LTSB).

Pour consulter les conditions générales complètes des produits que vous achetez par le biais des programmes de licence en volume Microsoft, voir [Licensing Terms and Documentation](https://go.microsoft.com/fwlink/?LinkId=800052) (Conditions d’attribution des licences et documentation).


## <a name="licensed-branches"></a>Branches sous licence

Cet article référence le contrat Software Assurance ou les droits d’abonnement équivalents. Ce contrat de licence Microsoft accorde des droits pour installer et utiliser Configuration Manager.

### <a name="current-branch"></a>Current Branch

Current Branch requiert un contrat Software Assurance actif ou des droits équivalents pour Configuration Manager. Pour plus d’informations, consultez [Software Assurance et Current Branch](#software-assurance-and-the-current-branch).

Cette branche est prise en charge dans les environnements de production qui veulent recevoir des mises à jour de fonctionnalités et qualitatives régulières de Microsoft. Elle donne accès à l’utilisation de toutes les fonctionnalités et améliorations.

À compter de la version 1710, chaque version de mise à jour reste prise en charge pendant 18 mois suivant sa date de disponibilité générale. Pour plus d’informations, consultez [Prise en charge des versions Current Branch de System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).

### <a name="long-term-servicing-branch-ltsb"></a>Long-Term Servicing Branch (LTSB)

LTSB requiert un contrat Software Assurance actif avec Microsoft en date du 1er octobre 2016. Pour plus d’informations, consultez [Software Assurance et LTSB](#software-assurance-and-the-ltsb).

Cette branche est prise en charge dans les environnements de production. Utilisation prévue pour les clients qui ont laissé leur contrat Software Assurance (SA) ou leurs droits d’abonnement équivalents pour Configuration Manager expirer après le 1er octobre 2016. Cette branche est limitée par rapport à Current Branch.

Les mises à jour de sécurité critiques pour Configuration Manager sont disponibles pour cette branche, mais aucune nouvelle fonctionnalité n’est disponible.

### <a name="evaluation-installation-of-the-current-branch"></a>Installation d’évaluation de Current Branch

La version d’évaluation ne requiert pas de contrat Software Assurance avec Microsoft. Une [installation d’évaluation](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) correspond toujours à Current Branch et est utilisable pendant 180 jours.

Vous pouvez mettre à niveau l’installation d’évaluation vers une installation complète de Current Branch. Vous ne pouvez pas mettre à niveau une installation d’évaluation vers Long-Term Servicing Branch.

### <a name="technical-preview-branch"></a>Branche Technical Preview

La [branche Technical Preview](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) est également disponible. Il s’agit d’une build limitée de Configuration Manager qui vous permet d’essayer de nouvelles fonctionnalités. Vous installez la version Technical Preview à l’aide d’un autre support que celui des versions sous licence. Pour plus d’informations, consultez [Technical Preview](/sccm/core/get-started/technical-preview).


## <a name="software-assurance-agreements"></a>Contrats Software Assurance

L’état du contrat Software Assurance sur vos licences System Center Configuration Manager ou vos droits d’abonnement équivalents, à la date du 1er octobre 2016 ou après cette date, déterminent la branche que vous pouvez installer et utiliser.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance et Current Branch

Des droits d’utilisation sur Configuration Manager Current Branch peuvent être octroyés par :

- **System Center** : Les clients dotés d’un contrat SA actif sur des licences System Center Standard ou Datacenter peuvent installer et utiliser l’option Current Branch de Configuration Manager.

- **System Center Configuration Manager** : Les clients dotés d’un contrat SA actif sur des licences System Center Configuration Manager, ou dotés de droits d’abonnement équivalents, peuvent installer et utiliser l’option Current Branch de Configuration Manager.

Si vous disposez d’un contrat SA actif sur des licences System Center Configuration Manager ou des droits d’abonnement équivalents à la date du ou après le 1er octobre 2016 :

- Vous pouvez installer et utiliser Current Branch.
- Si vous laissez votre contrat SA ou votre abonnement expirer, vous devez désinstaller Current Branch.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance et LTSB

Si vous disposez d’un contrat SA actif sur des licences System Center Configuration Manager ou des droits d’abonnement équivalents à la date du ou après le 1er octobre 2016 :

- Vous pouvez installer et utiliser LTSB. Les clients dotés de droits perpétuels sur System Center Configuration Manager, ou qui laissent leur contrat SA ou leur abonnement expirer, peuvent installer la version LTSB de Configuration Manager qui est en vigueur au moment de l’expiration.

LTSB est basé sur Current Branch version 1606 et présente les limitations suivantes :

- Il n’existe aucune prise en charge pour passer de Current Branch à LTSB. Si vous disposez actuellement d’un site Current Branch, vous devez installer LTSB en tant que nouveau site.  

- LTSB ne prend pas en charge toutes les fonctionnalités de Current Branch. Pour plus d’informations, consultez [Présentation de Long-Term Servicing Branch](introduction-to-the-ltsb.md). Ces limitations incluent un ensemble limité de fonctionnalités, des options de mise à niveau limitées et un cycle de vie du support produit distinct.  

### <a name="software-assurance-expiration-date"></a>Date d’expiration de Software Assurance

À partir de la version d’octobre 2016 du support de la base de référence de la version 1606 de Configuration Manager, vous pouvez spécifier la date d’expiration de votre contrat Software Assurance. La **date d’expiration de Software Assurance** est une valeur facultative qui vous servira de rappel. Ajoutez-la lorsque vous exécutez Configuration Manager ou ultérieurement depuis la console Configuration Manager.

> [!NOTE]
> Microsoft ne valide pas la date d’expiration spécifiée et ne l’utilise pas pour la validation de la licence. Vous pouvez vous en servir de rappel. Cette valeur est utile car Configuration Manager vérifie régulièrement les nouvelles mises à jour de logiciels proposées en ligne. Vous devez disposer d’une licence Software Assurance à jour pour pouvoir utiliser ces mises à jour supplémentaires.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>Pour spécifier la date d’expiration de Software Assurance

- Quand vous exécutez le programme d’installation à partir du support Configuration Manager, spécifiez cette valeur dans la page **Clé de produit** de l’Assistant Installation.

- Dans la console Configuration Manager, dans **Paramètres de hiérarchie**, spécifiez cette valeur sous l’onglet **Licences**.


## <a name="licensing-resources"></a>Ressources de licences

Pour plus d’informations sur les licences de produit, utilisez les ressources suivantes.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Centre de gestion des licences en volume Microsoft (VLSC)

- [Vue d’ensemble de VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Termes des contrats de licence en volume Microsoft](https://go.microsoft.com/fwlink/?LinkId=800052)

- Les clients de licences en volume peuvent obtenir un récapitulatif de leurs licences à partir du [Centre de gestion des licences en volume](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Accédez au menu **Licences**, puis sélectionnez **Résumé des licences**.

### <a name="vlsc-videos"></a>Vidéos VLSC

- Pour obtenir des vidéos de formation sur le fonctionnement de VLSC, accédez à [Microsoft Volume Licensing Service Center training and resources](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources) (Formation et ressources du Centre de gestion des licences en volume Microsoft), puis sélectionnez **How-to videos** (Vidéos explicatives).

- [Où rechercher votre contrat Software Assurance actif](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (à 43 secondes du début)  

- [Comment obtenir des autorisations pour VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4). Vous pouvez déléguer des autorisations de lecture et d’écriture VLSC à d’autres personnes de votre organisation.
