---
title: Versions Technical Preview
titleSuffix: Configuration Manager
description: Découvrez la branche Technical Preview qui permet de tester les nouvelles fonctionnalités de Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4be568e997a85acf49c3c86971f8d678d916aef0
ms.sourcegitcommit: 7eebd112a9862bf98359c1914bb0c86affc5dbc0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/22/2018
ms.locfileid: "42589523"
---
# <a name="technical-preview-for-configuration-manager"></a>Version Technical Preview de Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article fournit des détails sur la branche Technical Preview mensuelle de Configuration Manager. La version Technical Preview présente les nouvelles fonctionnalités sur lesquelles travaille Microsoft. Elle introduit les nouvelles fonctionnalités qui ne sont pas encore incluses dans la version Current Branch de Configuration Manager. Ces fonctionnalités seront peut-être ajoutées dans une mise à jour de la version Current Branch. Avant de finaliser les fonctionnalités, nous souhaitons que vous les essayiez et que vous nous fassiez part de vos commentaires.  

Comme il s’agit d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

Ces informations s’appliquent à toutes les versions de la branche Technical Preview de Configuration Manager. Cet article liste chaque nouvelle fonctionnalité avec la version Technical Preview où elle apparaît pour la première fois. Par exemple, la version **1806** pour juin (06) 2018 (18). Des articles distincts dédiés à chaque préversion détaillent les différentes fonctionnalités.  

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

-  **Technical Preview version 1806** : la version Technical Preview 1806 de Configuration Manager est disponible à la fois en tant que mise à jour dans la console et en tant que nouvelle version de référence. Téléchargez les versions de référence [à partir du Centre d’évaluation TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).



##  <a name="BKMK_TPFeedback"></a> Envoi de commentaires  

Faites-nous part de vos commentaires sur les nouvelles fonctionnalités Technical Preview. Pour plus d’informations, consultez [Commentaires produit](/sccm/core/understand/find-help#product-feedback).

Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n’hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter les idées soumises par d’autres personnes, [visitez notre page UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->



##  <a name="bkmk_tpCaps"></a> Fonctionnalités de la version la plus récente  

Les fonctionnalités suivantes sont disponibles dans la version Technical Preview la plus récente de Configuration Manager : 

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1808"></a>Version Technical Preview 1808

- [Déploiement par phases de mises à jour logicielles](capabilities-in-technical-preview-1808.md#bkmk_pod) <!--1358146-->
- [Améliorations de la réparation d’applications](capabilities-in-technical-preview-1808.md#bkmk_repair) <!--1357866-->


> [!Note]  
> Les fonctionnalités disponibles dans une version antérieure de la version Technical Preview restent disponibles dans les versions ultérieures. De même, les fonctionnalités ajoutées à la version Current Branch de Configuration Manager restent disponibles dans la branche Technical Preview.   



## <a name="features-in-recent-supported-technical-previews"></a>Fonctionnalités des dernières versions Technical Preview prises en charge

Les fonctionnalités suivantes ont été publiées avec les versions antérieures de la branche Technical Preview de Configuration Manager, qui sont encore prises en charge : 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Fonctionnalité |Version Technical Preview |Version Current Branch|  
 |----------------|---------------------|--------------------|
 | Hub Communauté <!--1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) | ![Non ajouté](media/Red_X.gif) | 
 | Spécifier le lecteur pour la maintenance des images de système d’exploitation hors connexion <!--1358924--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_osd) | ![Non ajouté](media/Red_X.gif) | 
 | Activité de synchronisation d’appareil cogéré avec Intune <!--1358565--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_comgmt) | ![Non ajouté](media/Red_X.gif) | 
 | Réparer des applications <!--1357866--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_app-repair) | ![Non ajouté](media/Red_X.gif) | 
 | Approuver les requêtes des applications par e-mail<!--1321550--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_email-approve) | ![Non ajouté](media/Red_X.gif) | 
 | Amélioration de la sortie de script<!--1236459--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_script) | ![Non ajouté](media/Red_X.gif) | 
 | Amélioration des mises à jour des logiciels tiers<!--1358714--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_3pupdate) | ![Non ajouté](media/Red_X.gif) | 
 | Améliorations apportées aux déploiements par phases <!--1358577,1358147,1358578--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_pod)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Prise en charge de nouveaux formats de package d’application Windows <!--1357427--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_msix)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Amélioration apportée à la sécurité d’envoi (push) du client <!--1358204--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_client-push)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Insights d’administration pour la maintenance proactive <!--1352184,et al--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_insights)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Transférer la charge de travail des applications mobiles pour les appareils cogérés <!--1357892--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_comgmt)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Options de groupe de limites pour les téléchargements à partir de pairs <!--1356193--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_bgoptions)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Prise en charge de mises à jour de logiciels tiers pour les catalogues personnalisés <!--1358714--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées aux fonctionnalités de gestion cloud <!--511980,515854--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_cloud)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Nouveau rapport sur la conformité des mises à jour logicielles <!--1357775--> | [Tech Preview 1806.2](capabilities-in-technical-preview-1806-2.md#bkmk_report)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Mises à jour des logiciels tiers <!--1352101--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#bkmk-3pupdate)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configurer les paramètres Windows Defender SmartScreen pour Microsoft Edge <!--1353701--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#configure-windows-defender-smartscreen-settings-for-microsoft-edge)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Synchroniser la stratégie MDM de Microsoft Intune pour un appareil cogéré <!--1357377--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Transférer la charge de travail Office 365 vers Intune avec la cogestion <!--1357841--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#transition-office-365-workload-to-intune-using-co-management)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Package Conversion Manager <!--1357861--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#package-conversion-manager)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Déployer des mises à jour logicielles sans contenu <!--1357933--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#deploy-software-updates-without-content)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Intégration de l’Outil de personnalisation Office au programme d’installation d’Office 365 <!--1358149--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#office-customization-tool-integration-with-the-office-365-installer)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à la passerelle de gestion cloud <!--1358215,1358651,503899--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-cloud-management-gateway)   | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Amélioration des communications clientes sécurisées <!--1358278,1358279--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-secure-client-communications)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à l’infrastructure du Centre logiciel <!--1358309--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#software-center-infrastructure-improvements)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Provisionner les packages d’application Windows pour tous les utilisateurs sur un appareil <!--1358310--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#provision-windows-app-packages-for-all-users-on-a-device)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées au tableau de bord Surface <!--1358654--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#improvements-to-the-surface-dashboard)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Révision de l’unité par défaut pour l’inventaire matériel <!--514442--> | [Tech Preview 1806](capabilities-in-technical-preview-1806.md#hardware-inventory-default-unit-revision)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Créer un déploiement en plusieurs phases configurées manuellement pour une séquence de tâches <!--1358148--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Prise en charge du point de distribution cloud pour Azure Resource Manager <!--1322209--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Agir en fonction des insights de gestion <!--1357930--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Transférer la charge de travail de configuration des appareils vers Intune avec la cogestion <!--1357903--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Configurer les points de distribution pour utiliser le contrôle de surcharge du réseau <!--1358112--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Tableau de bord de gestion cloud <!--1358461--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cloud-management-dashboard)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMPivot <!--1358456--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmpivot)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Amélioration des communications clientes sécurisées <!--1356889,1358228,1358460--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improved-secure-client-communications)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations concernant la prise en charge des mises à jour des logiciels tiers <!--1357605--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10 <!--1358500--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | CMTrace installé avec le client <!--1357971--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à la console Configuration Manager <!--1358202--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à la fonctionnalité Commentaires de la console <!--1357542--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées aux points de distribution compatibles PXE <!--1357580--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à l’inventaire matériel pour les valeurs d’entiers longs <!--1357880--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à la maintenance de WSUS <!--1357898--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  
 | Améliorations apportées à la prise en charge des certificats CNG <!--1357314--> | [Tech Preview 1805](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates)  | [Version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806) |  

  

## <a name="features-in-previous-technical-previews"></a>Fonctionnalités des précédentes préversions techniques

Les fonctionnalités suivantes ont été publiées avec les versions antérieures de la branche Technical Preview de Configuration Manager. Ces fonctionnalités restent disponibles dans les versions ultérieures, mais ne sont pas encore disponibles dans la branche Current Branch. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

|Fonctionnalité |Version Technical Preview |  
|----------------|---------------------|
|Centre d’aide et de support <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | 
|Service de répondeur PXE basé sur le client <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
|Prise en charge du démarrage réseau PXE pour IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
|Utiliser Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
|Évaluation de la conformité des mises à jour Windows Update pour Entreprise <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
|Accès aux données de point de terminaison OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
|Améliorations apportées à Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
|Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Voir aussi  

Pour plus d’informations, consultez les articles suivants :  

- [Évaluer Configuration Manager dans un laboratoire](/sccm/core/get-started/evaluate-with-lab-environment)
- [Nouveautés des versions incrémentielles de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Présentation de Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Pour plus d’informations sur les fonctionnalités Current Branch qui nécessitent un consentement pour être activées, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).  
> 
> Pour plus d’informations sur les fonctionnalités Current Branch qui doivent être activées en premier, consultez [Activation de fonctionnalités facultatives de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
