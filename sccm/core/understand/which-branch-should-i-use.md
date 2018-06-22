---
title: Quelle branche utiliser ?
titleSuffix: Configuration Manager
description: Découvrez les différences entre les branches disponibles de System Center Configuration Manager.
ms.date: 05/01/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a3be4f8f-3d44-4e3c-9fa1-e85f30a36e72
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 258d8ac160e9ee31189f8771fd6109d1bb17f714
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341336"
---
# <a name="which-branch-of-configuration-manager-should-i-use"></a>Quelle branche de Configuration Manager dois-je utiliser ?

*S’applique à : System Center Configuration Manager (Current Branch, Long-Term Servicing Branch et Technical Preview)*


Il existe trois branches pour System Center Configuration Manager : Current Branch, Long-Term Servicing Branch et Technical Preview. Utilisez cette rubrique pour mieux choisir la branche qui vous convient.

> [!TIP]  
> Tous les sites d’une hiérarchie doivent exécuter la même branche. Il est impossible de prendre en charge une hiérarchie avec des branches différentes sur des sites distincts.


## <a name="current-branch"></a>Current Branch
Cette branche est concédée sous licence pour une utilisation dans un environnement de production. Utilisez cette branche pour obtenir les dernières fonctionnalités. Si vous avez l’une des licences suivantes, vous pouvez utiliser cette branche :  
- System Center Datacenter
- System Center Standard
- System Center Configuration Manager
- Droits d’abonnement équivalents  

Pour plus d’informations sur la Software Assurance et les options de licence, consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md), ainsi que [Questions fréquentes (FAQ) sur les branches et la gestion des licences de Configuration Manager](/sccm/core/understand/product-and-licensing-faq).

La branche Current Branch est mise à jour plusieurs fois par an avec de nouvelles fonctionnalités. Chaque version de mise à jour est prise en charge pendant un an après sa publication. Effectuez la mise à jour vers une version plus récente de Current Branch avant l’expiration de ce délai d’un an. Les mises à jour vers des versions plus récentes sont proposées sous forme de mises à jour dans la console.

Pour installer Current Branch en tant que nouveau site, utilisez le [support de la base de référence](/sccm/core/servers/manage/updates#baseline-and-update-versions). Utilisez également le support de la base de référence pour mettre à niveau System Center 2012 Configuration Manager avec Service Pack 2, ou System Center 2012 R2 Configuration Manager avec Service Pack 1. L’accès à ce support dépend de la manière dont votre organisation a acquis la licence de System Center Configuration Manager. 

Vous pouvez également utiliser le support de la base de référence pour installer un nouveau site en tant qu’édition d’évaluation de Current Branch. L’édition d’évaluation ne nécessite aucune licence. Vous pouvez utiliser l’édition d’évaluation pendant 180 jours. Elle prend en charge la mise à niveau vers une édition sous licence de Current Branch. Pour installer uniquement une édition d’évaluation, accédez au site [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection).

>  [!NOTE]  
> Utilisez uniquement le média de référence pour installer des sites pour une nouvelle hiérarchie Configuration Manager. Si vous avez installé une version de base de référence, utilisez les mises à jour dans la console pour mettre à jour vos sites vers une nouvelle version.  
>  
> Les sites mis à jour à l’aide de mises à jour dans la console sont équivalents au nouveau site installé à l’aide du média de référence.
>
> Pour plus d’informations, consultez [Mises à jour pour System Center Configuration Manager](/sccm/core/servers/manage/updates).  


### <a name="features-of-the-current-branch"></a>Fonctionnalités de la branche Current Branch
- Elle reçoit des [mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates) qui mettent à votre disposition de nouvelles fonctionnalités.
- Elle reçoit des mises à jour dans la console qui offrent des correctifs de sécurité et de qualité aux fonctionnalités existantes.
- Elle prend en charge les mises à jour hors bande lorsque cela est nécessaire. Pour plus d’informations, consultez [Utiliser l’outil Inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes) ou [Utiliser le programme d’installation de correctif logiciel](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).
- Elle s’intègre à Microsoft Intune et d’autres services cloud.
- Elle prend en charge la [migration des données](/sccm/core/migration/migrate-data-between-hierarchies) vers et à partir d’autres installations de Configuration Manager.
- Elle prend en charge la mise à niveau à partir de versions précédentes de Configuration Manager.
- Elle prend en charge l’installation en tant qu’édition d’évaluation, à partir de laquelle vous pourrez ultérieurement effectuer une mise à niveau vers une installation sous licence.

La version 1511 était la version initiale de Current Branch. Les mises à jour ultérieures incluent les versions 1602, 1606, etc. Chaque version est prise en charge pendant un an et Microsoft vous recommande d’effectuer la mise à jour vers la dernière version peu après sa publication. Vous pouvez attendre jusqu’à une année avant d’effectuer la mise à jour vers une version plus récente et vous pouvez également ignorer une mise à jour pour installer la dernière version disponible. Dans la mesure où chaque version est cumulative, si vous ignorez une mise à jour et installez la version la plus récente, vous bénéficiez tout de même de l’ensemble des fonctionnalités et améliorations apportées par les versions précédentes.

Pour plus d’informations, consultez [Prise en charge des versions Current Branch](/sccm/core/servers/manage/current-branch-versions-supported).


### <a name="update-options"></a>Options de mise à jour
- Avec la Software Assurance active, vous pouvez installer des mises à jour dans la console pour les versions Current Branch.  
- Il n’existe aucune option permettant de convertir Current Branch en Technical Preview. Les branches Technical Preview sont des installations distinctes qui ne nécessitent pas de licence.
- Il n’existe aucune option permettant de convertir Current Branch en LTSB (Long-Term Servicing Branch). Vous devez désinstaller Current Branch, puis installer LTSB en tant que nouvelle installation.



##  <a name="long-term-servicing-branch"></a>Long-Term Servicing Branch 
Il s’agit d’une branche sous licence à utiliser en production pour les clients Configuration Manager qui utilisent Current Branch et ont autorisé Configuration Manager SA (Software Assurance) ou des droits d’abonnement équivalents à expirer après le 1er octobre 2016. Pour plus d’informations sur la Software Assurance et les options de licence, consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md), ainsi que [Questions fréquentes (FAQ) sur les branches et la gestion des licences de Configuration Manager](/sccm/core/understand/product-and-licensing-faq).

La branche LTSB est basée sur la version 1606. Cette branche ne reçoit pas les mises à jour dans la console, qui fournissent de nouvelles fonctionnalités ou mettent à jour des fonctionnalités existantes. Toutefois, des correctifs de sécurité critiques sont fournis. Pour installer la branche LTSB, vous devez utiliser le [support de la base de référence](/sccm/core/servers/manage/updates#baseline-and-update-versions) de la version 1606 fourni avec System Center 2016. Les versions de base de référence ultérieures ne prennent pas en charge l’installation de LTSB.

Pour installer la branche LTSB en tant que nouveau site ou en tant que mise à niveau d’un site Configuration Manager 2012 pris en charge, utilisez le [support de la base de référence](/sccm/core/servers/manage/updates#baseline-and-update-versions) de la version 1606 fourni avec System Center 2016. Vous pouvez utiliser le support de la base de référence pour installer un nouveau site qui exécute la version 1606 de Current Branch, ou un nouveau site qui exécute Long-Term Servicing Branch.

> [!TIP]  
> Pour en savoir plus sur System Center 2016, consultez la [documentation de System Center 2016](https://docs.microsoft.com/system-center/index). Cette documentation indique également comment obtenir System Center 2016, qui requiert un contrat de licence Microsoft ou des droits similaires.  
>  
> Pour trouver la version 1606 de System Center Configuration Manager dans le VLSC (Centre de gestion des licences en volume), accédez à l’onglet **Téléchargements et clés** du [VLSC](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx), recherchez `System Center 2016`, puis sélectionnez **System Center 2016 Datacenter** ou **System Center 2016 Standard**.  
>  
> Vous pouvez également obtenir une version d’évaluation de System Center 2016 à partir du site [TechNet Evaluation Center](https://www.microsoft.com/evalcenter/evaluate-system-center-technical-preview).  


### <a name="features-of-the-ltsb"></a>Fonctionnalités de la branche LTSB
-   Elle reçoit des mises à jour dans la console qui fournissent des correctifs de sécurité critiques.
- Elle fournit une option d’installation lorsque votre contrat SA ou vos droits équivalents sur Configuration Manager ont expiré.
- Elle prend en charge la mise à niveau (conversion) vers Current Branch quand vous avez un contrat SA ou des droits équivalents sur Configuration Manager.


### <a name="limitations"></a>Limitations  
La branche LTSB est basée sur la version 1606 de Current Branch et présente les limitations suivantes :
- Vous bénéficiez pendant 10 ans de mises à jour de sécurité critiques pour LTSB après sa disponibilité générale (octobre 2016), après quoi la prise en charge de cette branche expire. Pour plus d’informations sur la politique de support, consultez la page [Politique de support Microsoft](https://support.microsoft.com/lifecycle).
- Elle prend en charge une liste limitée de systèmes d’exploitation serveur et client et les technologies associées, telles que les versions de SQL Server. Pour plus d’informations sur ce qui est pris en charge avec cette branche, consultez [Configurations prises en charge pour Long-Term Servicing Branch](supported-configurations-for-ltsb.md).
- Elle ne reçoit pas de mises à jour pour les nouvelles fonctionnalités.
- Elle ne prend pas en charge fonctionnalités suivantes : 
   - Ajout d’un abonnement Microsoft Intune, ce qui vous empêche d’utiliser :
     -  Intune dans une configuration de gestion des appareils mobiles hybride ;
     - Gestion des appareils mobiles locale
   -    Tableau de bord de maintenance de Windows 10, plans de maintenance ou canal semi-annuel Windows 10
   - Versions futures de Windows 10 LTSB et Windows Server
   -    Asset Intelligence
   -    Points de distribution cloud
   -    Exchange Online en tant que connecteur Exchange
   -    Fonctionnalités de préversion


### <a name="update-options"></a>Options de mise à jour
- Vous pouvez convertir votre installation LTSB en installation Current Branch. La conversion en On-premises MDM est prise en charge avant ou après l’expiration du support de la branche LTSB.

  Pour effectuer la conversion, vous devez disposer d’un contrat Software Assurance actif avec Microsoft. Pour plus d’informations, suivez les liens ci-dessous :
  - [Mettre à niveau Long-Term Servicing Branch vers Current Branch](convert-to-current-branch.md)
  - [Licences et branches pour System Center Configuration Manager](learn-more-editions.md)
  - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#baseline-and-update-versions) 
- Il n’existe aucune option permettant de convertir LTSB en branche Technical Preview. Les branches Technical Preview sont des installations distinctes qui ne nécessitent pas de licence.
-   Vous ne pouvez pas mettre à niveau une édition d’évaluation de Current Branch vers une installation LTSB.



## <a name="technical-preview-branch"></a>Branche Technical Preview
La branche Technical Preview est destinée à un environnement lab. Découvrez et testez les dernières fonctionnalités développées pour Configuration Manager. Il n’est pas pris en charge dans un environnement de production et ne nécessite pas de contrat de licence Software Assurance.

Pour installer un nouveau site qui exécute la branche Technical Preview, utilisez le dernier [support de la base de référence pour la branche Technical Preview](/sccm/core/get-started/technical-preview#install-and-update-the-technical-preview). Une fois que vous avez installé la branche Technical Preview, de nouvelles versions sont disponibles chaque mois sous forme de mises à jour dans la console.


### <a name="features-of-the-technical-preview-branch"></a>Fonctionnalités de la branche Technical Preview
-  Elle est basée sur les versions de base de référence récentes de Current Branch
-  Elle reçoit des mises à jour dans la console pour mettre à jour votre installation vers la dernière version de la branche Technical Preview
-  Elle inclut de nouvelles fonctionnalités en cours de développement, pour lesquelles Microsoft souhaite recevoir vos commentaires
-  Elle reçoit des mises à jour qui s’appliquent uniquement à la branche Technical Preview


### <a name="limitations"></a>Limitations
-  [La prise en charge est limitée](/sccm/core/get-started/technical-preview#requirements-and-limitatins-for-the-techincal-preview), avec seulement un site principal et jusqu’à 10 clients.  
-  Elle ne peut pas être mise à niveau vers une branche Current Branch ou LTSB.
-  Elle ne prend pas en charge les comportements suivants :
   - Utilisation de la migration pour importer ou exporter des données vers une autre installation de Configuration Manager
   - Mise à niveau à partir d’une version antérieure de Configuration Manager
   - Installation en tant qu’édition d’évaluation

Les fonctionnalités introduites initialement dans une branche Technical Preview sont souvent ajoutées à Current Branch au cours d’une mise à jour ultérieure. Chaque nouvelle version de branche Technical Preview inclut les fonctionnalités des branches Technical Preview précédentes, même après l’ajout de ces fonctionnalités à Current Branch.

Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).


### <a name="update-options"></a>Options de mise à jour
-   Vous pouvez installer n’importe quelle mise à jour dans la console pour une nouvelle version de branche Technical Preview.
-   Il n’existe aucune option permettant de convertir une branche Technical Preview en branche Current Branch ou LTSB.



## <a name="identify-your-version-and-branch"></a>Identifier votre version et votre branche

### <a name="version"></a>Version   
Pour vérifier la version de votre site, en haut à gauche de la console, accédez à **À propos de System Center Configuration Manager**. Cette boîte de dialogue affiche la **version du site**. Pour obtenir la liste des versions de site, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#bkmk_Baselines).

### <a name="branch"></a>Branche
Pour vérifier la branche de votre site, dans la console, accédez à **Administration** > **Configuration du site** > **Sites**, puis ouvrez **Paramètres de hiérarchie**. Si vous voyez une option de conversion en Current Branch et si elle est active, cela signifie que le site exécute la version LTSB. Quand le site exécute Current Branch, cette option est grisée.

Pour plus d’informations sur les différentes versions de Configuration Manager, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#bkmk_Baselines).
