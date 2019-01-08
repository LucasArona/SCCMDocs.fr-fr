---
title: Versions Technical Preview
titleSuffix: Configuration Manager
description: Découvrez la branche Technical Preview qui permet de tester les nouvelles fonctionnalités de Configuration Manager.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d2c1e93378711a19b10f9b67fcaad9973e53ee2e
ms.sourcegitcommit: d36e4c7082a5144e79035dd8847c8e741fa04667
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53444635"
---
# <a name="technical-preview-for-configuration-manager"></a>Version Technical Preview de Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*

Cet article fournit des détails sur la branche Technical Preview mensuelle de Configuration Manager. La version Technical Preview présente les nouvelles fonctionnalités sur lesquelles travaille Microsoft. Elle introduit les nouvelles fonctionnalités qui ne sont pas encore incluses dans la version Current Branch de Configuration Manager. Ces fonctionnalités seront peut-être ajoutées dans une mise à jour de la version Current Branch. Avant de finaliser les fonctionnalités, nous souhaitons que vous les essayiez et que vous nous fassiez part de vos commentaires.  

Comme il s’agit d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

Ces informations s’appliquent à toutes les versions de la branche Technical Preview de Configuration Manager. Cet article liste chaque nouvelle fonctionnalité avec la version Technical Preview où elle apparaît pour la première fois. Par exemple, la version **1809** pour septembre (09) 2018 (18). Des articles distincts dédiés à chaque préversion détaillent les différentes fonctionnalités.  

Pour plus d’informations sur les nouveautés de la *version Current Branch* de Configuration Manager, consultez [Nouveautés des versions incrémentielles de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).



##  <a name="bkmk_reqs"></a> Configuration requise et limitations  

> [!IMPORTANT]     
>  La préversion technique est concédée sous licence exclusivement pour une utilisation dans un environnement lab. Microsoft peut ne pas fournir de services de support technique, et certaines fonctionnalités peuvent ne pas être disponibles dans la préversion du logiciel. De plus, la préversion du logiciel peut utiliser des standards de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

Pour la plupart des prérequis du produit, utilisez les informations contenues dans les [configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations). Les exceptions suivantes s’appliquent à la branche Technical Preview :  

-   Chaque installation est active pendant 90 jours avant de devenir inactive.  

-   L'anglais est la seule langue prise en charge.  

-   Elle prend uniquement en charge les paramètres de ligne de commande d’installation suivants :  
    -   `/silent`  
    -   `/testdbupgrade`    

-   Le point de connexion de service est installé en mode en ligne. Il ne prend pas en charge le mode hors connexion.  

-   Les articles dédiés à chaque version Technical Preview décrivent les limitations ou les spécifications supplémentaires, le cas échéant.

-   Les fonctionnalités suivantes ne sont pas prises en charge avec la branche Technical Preview :  

    - [Migration](/sccm/core/migration/migrate-data-between-hierarchies) vers ou depuis cette branche de préversion.  

    - [Mise à niveau](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) vers cette branche de préversion.  

    - [Récupération de site](/sccm/core/servers/manage/recover-sites) depuis le dossier cd.latest.  <!--507106-->

-   Il n’existe aucune prise en charge de la mise à jour vers la version Current Branch à partir de cette branche de préversion.  

    > [!Note]  
    > Quand des mises à jour sont disponibles pour une préversion, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour accéder à une vidéo du processus de mise à niveau dans la console, consultez [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  

-   Seul un site principal autonome est pris en charge. Il n’existe aucune prise en charge pour un site d’administration centrale, plusieurs sites principaux ou des sites secondaires.  

La branche Technical Preview de Configuration Manager prend en charge les produits et technologies suivants : 

-   Seules les versions suivantes de **SQL Server** sont prises en charge :  

    -   SQL Server 2017 (avec mise à jour cumulative 2 et ultérieure) à compter de Configuration Manager version 1710
    -   SQL Server 2016 (sans Service Pack et versions ultérieures)
    -   SQL Server 2014 (avec Service Pack 1 et version ultérieure)
    -   SQL Server 2012 (avec Service Pack 3 ou version ultérieure)  


-   Le site prend en charge jusqu’à 10 clients, qui doivent exécuter l’une des versions suivantes de Windows :  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

> [!Note]  
> L’inclusion de ces produits dans ce contenu n’implique pas une extension de la prise en charge d’une version ayant dépassé son cycle de vie. Configuration Manager ne prend pas en charge les produits qui ont dépassé leur cycle de vie. Pour plus d’informations, consultez [Politique de support Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  



##  <a name="bkmk_install"></a> Installer et mettre à jour  

La branche Technical Preview de Configuration Manager pour l’utilisation lab se distingue de la version Current Branch de Configuration Manager pour l’utilisation en production.  

Commencez par installer une version de référence de la branche Technical Preview. Après avoir installé une version de référence, utilisez les mises à jour dans la console pour actualiser votre installation avec la préversion la plus récente. En règle générale, de nouvelles versions Technical Preview sont disponibles chaque mois.

Microsoft prend en charge chaque version Technical Preview jusqu’à ce que trois versions successives soient disponibles. Par exemple, quand la version 1708 a été publiée, la version 1704 a cessé d’être prise en charge. Les versions 1705, 1706 et 1707 ont continué à être prises en charge. Quand une version de référence n’est plus prise en charge, elle est quand même prise en charge pour l’installation d’un nouveau site Technical Preview, à condition que vous la mettiez immédiatement à jour vers une version prise en charge. L’ancienne version de référence est prise en charge jusqu’à ce qu’une nouvelle version de référence soit disponible. Effectuez une mise à jour vers la dernière version disponible à partir de la version de référence, puis répétez le processus de mise à jour jusqu’à ce que vous installiez la dernière version Technical Preview.

> [!TIP]  
>  Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation avec cette nouvelle version Technical Preview. Une installation de version Technical Preview ne permet jamais d’effectuer une mise à niveau vers une installation de version Current Branch. De même, elle ne reçoit jamais les mises à jour de la version Current Branch. 
> 
> À plusieurs reprises au cours de l’année, des versions Technical Preview et des versions Current Branch sont mises à disposition avec le même numéro de version. Par exemple, il existe une version Technical Preview 1802 et une version Current Branch 1802. 


### <a name="active-baseline-versions"></a>Versions de référence actives
   
Vous pouvez installer une version de référence jusqu’à un an après sa sortie. Quand vous installez un nouveau site de Technical Preview, si plusieurs versions de référence sont disponibles, utilisez la dernière version de référence.

-  **Préversion technique 1810.2** : La préversion technique 1810.2 de Configuration Manager est disponible à la fois en tant que mise à jour dans la console et en tant que nouvelle version de référence. Téléchargez les versions de référence à partir du [Centre d’évaluation TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Envoi de commentaires  

Faites-nous part de vos commentaires sur les nouvelles fonctionnalités Technical Preview. Pour plus d’informations, consultez [Commentaires produit](/sccm/core/understand/find-help#product-feedback).

Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n’hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter les idées soumises par d’autres personnes, [visitez notre page UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Fonctionnalités de la version la plus récente  

Les fonctionnalités suivantes sont disponibles dans la version Technical Preview la plus récente de Configuration Manager : 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1812"></a>Préversion technique 1812

<!--capabilities-in-technical-preview-1812.md#bkmk_anchor-->

- [Améliorations apportées à l’étape de séquence de tâches Exécuter le script PowerShell](capabilities-in-technical-preview-1812.md#bkmk_posh) <!--3556028 fka 1359389-->  
- [Améliorations des approbations d'applications par e-mail](capabilities-in-technical-preview-1812.md#bkmk_email) <!--3594063-->  
- [Configurer l'affinité entre utilisateur et périphérique dans le Centre logiciel](capabilities-in-technical-preview-1812.md#bkmk_uda) <!--3485366-->  
- [Améliorations apportées à la console Configuration Manager](capabilities-in-technical-preview-1812.md#bkmk_console) <!--3594151-->  
- [Télécharger des rapports depuis le Hub Communauté](capabilities-in-technical-preview-1812.md#bkmk_hub)<!--3555936-->  


> [!Note]  
> Les fonctionnalités disponibles dans une version antérieure de la version Technical Preview restent disponibles dans les versions ultérieures. De même, les fonctionnalités ajoutées à la version Current Branch de Configuration Manager restent disponibles dans la branche Technical Preview.   



## <a name="features-in-recent-supported-technical-previews"></a>Fonctionnalités des dernières versions Technical Preview prises en charge

Les fonctionnalités suivantes ont été publiées avec les versions antérieures de la branche Technical Preview de Configuration Manager, qui sont encore prises en charge : 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 | Fonctionnalité | Version Technical Preview | Version Current Branch |  
 |---------|---------------------------|------------------------|
 | Ne pas charger les profils Windows PowerShell <!--1359239--> | [Préversion technique 1811](capabilities-in-technical-preview-1811.md#bkmk_noprofile) | ![Non ajouté](media/Red_X.gif) | 
 | Une connexion Intune n’est plus nécessaire pour MDM au niveau local <!--1359124--> | [Préversion technique 1811](capabilities-in-technical-preview-1811.md#bkmk_opmdm) | ![Non ajouté](media/Red_X.gif) | 
 | Notifications de la console Configuration Manager <!--1318035--> | [Préversion technique 1811](capabilities-in-technical-preview-1811.md#bkmk_notify) | ![Non ajouté](media/Red_X.gif) | 
 | Améliorations apportées à la création d’un média de séquence de tâches <!--1359388--> | [Préversion technique 1811](capabilities-in-technical-preview-1811.md#bkmk_tsmedia) | ![Non ajouté](media/Red_X.gif) | 
 | Amélioration apportée à l’étape de séquence de tâches Exécuter le script PowerShell <!--1359389--> | [Préversion technique 1811](capabilities-in-technical-preview-1811.md#bkmk_posh) | ![Non ajouté](media/Red_X.gif) | 
 | Améliorations apportées à l’évaluation de regroupement <!--1358981--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_colleval) | Version 1810 | 
 | Authentification administrateur Configuration Manager <!--1357013--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_auth) | Version 1810 | 
 | Règle d’insights de gestion pour la version cliente de la source de cache d’homologue <!--1358008--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_insights) | Version 1810 | 
 | Améliorations apportées à l’installation de clients basés sur Internet <!--1359181--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_cmg) | Version 1810 | 
 | Convertir des applications en MSIX <!--1359029--> | [Tech Preview 1810.2](capabilities-in-technical-preview-1810-2.md#bkmk_msix) | Version 1810 | 
 | Amélioration apportée à l’installation du client <!--1358840--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_ccmsetup) | Version 1810 | 
 | Stratégie de conformité des applications nécessaires pour les appareils cogérés <!--1358196--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_app-compliance) | Version 1810 | 
 | Amélioration apportée au tableau de bord Cogestion <!--1358980--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_comgmt-report) | Version 1810 | 
 | Nouvelles options de groupe de limites <!--1358749--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_bgoptions) | Version 1810 | 
 | Système de site sur un nœud de cluster Windows <!--1359132--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_cluster) | Version 1810 | 
 | Améliorations apportées à CMPivot <!--1359068--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_cmpivot) | Version 1810 | 
 | Améliorations apportées aux scripts <!--1358239--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_scripts) | Version 1810 | 
 | Nouvelle action de notification du client pour sortir de veille un appareil <!--1317364--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_wakeup) | Version 1810 | 
 | Prise en charge des séquences de tâches pour les groupes de limites <!--1359025--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_bgr-osd) | Version 1810 | 
 | Tableau de bord Management insights <!--1357979--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_insights) | Version 1810 | 
 | Tableau de bord Documentation dans la console <!--1357546--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_doc-dashboard) | ![Non ajouté](media/Red_X.gif) | 
 | Améliorations apportées à la maintenance des pilotes <!--1358270--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_drivers) | Version 1810 | 
 | Prise en charge de la séquence de tâches de Windows Autopilot pour les appareils existants <!--1358333--> | [Tech Preview 1810](capabilities-in-technical-preview-1810.md#bkmk_autopilot) | Version 1810 | 



## <a name="features-in-previous-technical-previews"></a>Fonctionnalités des précédentes préversions techniques

Les fonctionnalités suivantes ont été publiées avec les versions antérieures de la branche Technical Preview de Configuration Manager. Ces fonctionnalités restent disponibles dans les versions ultérieures, mais ne sont pas encore disponibles dans la branche Current Branch. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Fonctionnalité        | Version Technical Preview |  
|----------------|---------------------------|
| Hub Communauté <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | 
| Activité de synchronisation d’appareil cogéré avec Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | 
| Service de répondeur PXE basé sur le client <!--1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Prise en charge du démarrage réseau PXE pour IPv6 <!--1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Utiliser Azure Active Directory <!--1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Évaluation de la conformité des mises à jour Windows Update pour Entreprise <!--1235390--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
| Améliorations apportées à Asset Intelligence <!--1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise <!--1037233?--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |



## <a name="see-also"></a>Voir aussi  

Pour plus d’informations, consultez les articles suivants :  

- [Évaluer Configuration Manager dans un laboratoire](/sccm/core/get-started/evaluate-with-lab-environment)
- [Nouveautés des versions incrémentielles de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Présentation de Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Pour plus d’informations sur les fonctionnalités Current Branch qui nécessitent un consentement pour être activées, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).  
> 
> Pour plus d’informations sur les fonctionnalités Current Branch qui doivent être activées en premier, consultez [Activation de fonctionnalités facultatives de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
