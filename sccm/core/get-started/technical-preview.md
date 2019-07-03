---
title: Versions Technical Preview
titleSuffix: Configuration Manager
description: Découvrez la branche Technical Preview qui permet de tester les nouvelles fonctionnalités de Configuration Manager.
ms.date: 06/12/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2041f51714cbed7a9c9a1a3ad14bbb2d8c697ae4
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285967"
---
# <a name="technical-preview-for-configuration-manager"></a>Version Technical Preview de Configuration Manager

*S’applique à : System Center Configuration Manager (préversion technique)*

Cet article fournit des détails sur la branche Technical Preview mensuelle de Configuration Manager. La version Technical Preview présente les nouvelles fonctionnalités sur lesquelles travaille Microsoft. Elle introduit les nouvelles fonctionnalités qui ne sont pas encore incluses dans la version Current Branch de Configuration Manager. Ces fonctionnalités seront peut-être ajoutées dans une mise à jour de la version Current Branch. Avant de finaliser les fonctionnalités, nous souhaitons que vous les essayiez et que vous nous fassiez part de vos commentaires.  

Comme il s’agit d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

Ces informations s’appliquent à toutes les versions de la branche Technical Preview de Configuration Manager. Cet article liste chaque nouvelle fonctionnalité avec la version Technical Preview où elle apparaît pour la première fois. Par exemple, la version **1901** pour janvier (01) 2019 (19). Des articles distincts dédiés à chaque préversion détaillent les différentes fonctionnalités.  

Pour plus d’informations sur les nouveautés de la *version Current Branch* de Configuration Manager, consultez [Nouveautés des versions incrémentielles de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions).

> [!Tip]  
> Pour recevoir une notification en cas de mise à jour de cette page, copiez et collez l’URL suivante dans votre lecteur de flux RSS : `https://docs.microsoft.com/api/search/rss?search=%22technical+preview+releases+-+Configuration+Manager%22&locale=en-us`.

## <a name="bkmk_reqs"></a> Configuration requise et limitations  

> [!IMPORTANT]  
> La préversion technique est concédée sous licence exclusivement pour une utilisation dans un environnement lab. Microsoft peut ne pas fournir de services de support technique, et certaines fonctionnalités peuvent ne pas être disponibles dans les préversions techniques. De plus, la préversion du logiciel technique peut utiliser des standards de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

Pour la plupart des prérequis du produit, utilisez les informations contenues dans les [configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations). Les exceptions suivantes s’appliquent à la branche Technical Preview :  

- Chaque installation est active pendant 90 jours avant de devenir inactive.  

- L'anglais est la seule langue prise en charge.  

- Elle prend uniquement en charge les paramètres de ligne de commande d’installation suivants :  

    - `/silent`  
    - `/testdbupgrade`  

- Le point de connexion de service est installé en mode en ligne. Il ne prend pas en charge le mode hors connexion.  

- Les articles dédiés à chaque version Technical Preview décrivent les limitations ou les spécifications supplémentaires, le cas échéant.

- Les fonctionnalités suivantes ne sont pas prises en charge avec la branche Technical Preview :  

    - [Migration](/sccm/core/migration/migrate-data-between-hierarchies) vers ou depuis cette branche de préversion.  

    - [Mise à niveau](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager) vers cette branche de préversion.  

    - [Récupération de site](/sccm/core/servers/manage/recover-sites) depuis le dossier cd.latest.  <!--507106-->

- Il n’existe aucune prise en charge de la mise à jour vers la version Current Branch à partir de cette branche de préversion.  

    > [!Note]  
    > Quand des mises à jour sont disponibles pour une préversion, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour accéder à une vidéo du processus de mise à niveau dans la console, consultez [Installing Configuration Manager update packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  

- Seul un site principal autonome est pris en charge. Il n’existe aucune prise en charge pour un site d’administration centrale, plusieurs sites principaux ou des sites secondaires.  

La branche Technical Preview de Configuration Manager prend en charge les produits et technologies suivants :

- Seules les versions suivantes de **SQL Server** sont prises en charge :  

    - SQL Server 2017 (avec la mise à jour cumulative 2 ou ultérieure)
    - SQL Server 2016 (sans Service Pack ou ultérieur)
    - SQL Server 2014 (avec Service Pack 1 ou ultérieur)
    - SQL Server 2012 (avec Service Pack 3 ou ultérieur)  

- Le site prend en charge jusqu’à 10 clients, qui doivent exécuter l’une des versions suivantes de Windows :  

    - Windows 10  
    - Windows 8.1  
    - Windows 7  

> [!Note]  
> L’inclusion de ces produits dans ce contenu n’implique pas une extension de la prise en charge d’une version ayant dépassé son cycle de vie. Configuration Manager ne prend pas en charge les produits qui ont dépassé leur cycle de vie. Pour plus d’informations, consultez [Politique de support Microsoft](https://go.microsoft.com/fwlink/p/?LinkId=208270).  

## <a name="bkmk_install"></a> Installer et mettre à jour  

La branche Technical Preview de Configuration Manager pour l’utilisation lab se distingue de la version Current Branch de Configuration Manager pour l’utilisation en production.  

Commencez par installer une version de référence de la branche Technical Preview. Après avoir installé une version de référence, utilisez les mises à jour dans la console pour actualiser votre installation avec la préversion la plus récente. En règle générale, de nouvelles versions Technical Preview sont disponibles chaque mois.

Microsoft prend en charge chaque version Technical Preview jusqu’à ce que trois versions successives soient disponibles. Par exemple, quand la version 1708 a été publiée, la version 1704 a cessé d’être prise en charge. Les versions 1705, 1706 et 1707 ont continué à être prises en charge. Quand une version de référence n’est plus prise en charge, elle est quand même prise en charge pour l’installation d’un nouveau site Technical Preview, à condition que vous la mettiez immédiatement à jour vers une version prise en charge. L’ancienne version de référence est prise en charge jusqu’à ce qu’une nouvelle version de référence soit disponible. Effectuez une mise à jour vers la dernière version disponible à partir de la version de référence, puis répétez le processus de mise à jour jusqu’à ce que vous installiez la dernière version Technical Preview.

> [!TIP]  
> Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation avec cette nouvelle version Technical Preview. Une installation de version Technical Preview ne permet jamais d’effectuer une mise à niveau vers une installation de version Current Branch. De même, elle ne reçoit jamais les mises à jour de la version Current Branch.
>
> À plusieurs reprises au cours de l’année, des versions Technical Preview et des versions Current Branch sont mises à disposition avec le même numéro de version. Par exemple, il existe une version Technical Preview 1802 et une version Current Branch 1802.

### <a name="active-baseline-versions"></a>Versions de référence actives

Vous pouvez installer une version de référence jusqu’à un an après sa sortie. Quand vous installez un nouveau site de Technical Preview, si plusieurs versions de référence sont disponibles, utilisez la dernière version de référence.

- **Technical Preview version 1902.2** : Technical preview version 1902.2 de Configuration Manager est disponible à la fois en tant que mise à jour dans la console et en tant que nouvelle version de référence. Téléchargez les versions de référence à partir du [Centre d’évaluation TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).

## <a name="BKMK_TPFeedback"></a> Envoi de commentaires  

Faites-nous part de vos commentaires sur les nouvelles fonctionnalités Technical Preview. Pour plus d’informations, consultez [Commentaires produit](/sccm/core/understand/find-help#product-feedback).

Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n’hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter les idées soumises par d’autres personnes, [visitez notre page UserVoice](https://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->

## <a name="bkmk_tpCaps"></a> Fonctionnalités de la version la plus récente  

Les fonctionnalités suivantes sont disponibles dans la version Technical Preview la plus récente de Configuration Manager :

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1906"></a>Technical Preview version 1906

<!-- - [title](/sccm/core/get-started/2019/technical-preview-1901#bkmk_anchor) <!--ID-->

- [Améliorations apportées aux tâches de maintenance](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-maintenance-tasks) <!--3555894-->
- [Surveillance de la mise à niveau de la base de données de mise à jour de Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#configuration-manager-update-database-upgrade-monitoring) <!--4200581-->
- [Plusieurs groupes de pilotes pour les charges de travail de cogestion](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt_pilot) <!--3555750-->
- [Logique de notification remaniée pour les logiciels nouvellement disponibles](/sccm/core/get-started/2019/technical-preview-1906#redesigned-notification-logic-for-newly-available-software) <!--3555904-->
- [RBAC sur les dossiers](/sccm/core/get-started/2019/technical-preview-1906#rbac-on-folders) <!--3600867-->
- [Découverte des groupes d’utilisateurs Azure Active Directory](/sccm/core/get-started/2019/technical-preview-1906#bkmk_aad-disco) <!--3611956-->
- [Contrôle à distance n’importe où avec la passerelle de gestion cloud](/sccm/core/get-started/2019/technical-preview-1906#remote-control-anywhere-using-cloud-management-gateway) <!--4575930-->
- [Améliorations apportées au hub Communauté](/sccm/core/get-started/2019/technical-preview-1906#bkmk_hub) <!--3555935-->
- [Ajouter des jointures, des opérateurs supplémentaires et des agrégateurs dans CMPivot](/sccm/core/get-started/2019/technical-preview-1906#bkmk_cmpivot) <!--4054074-->
- [Améliorations apportées à CMPivot](/sccm/core/get-started/2019/technical-preview-1906#improvements-to-cmpivot) <!--4619340,4683130-->
- [Améliorations apportées à la console Configuration Manager](/sccm/core/get-started/2019/technical-preview-1906#bkmk_console) <!--4223683-->
- [Prise en charge de Windows Virtual Desktop](/sccm/core/get-started/2019/technical-preview-1906#bkmk_winsku) <!--3556025-->
- [Notifications de décompte plus fréquentes pour les redémarrages](/sccm/core/get-started/2019/technical-preview-1906#more-frequent-countdown-notifications-for-restarts) <!--3976435-->
- [Inscription automatique de la cogestion avec un jeton d’appareil](/sccm/core/get-started/2019/technical-preview-1906#bkmk_comgmt) <!--4454491-->
- [Options supplémentaires pour les catalogues de mises à jour de tiers](/sccm/core/get-started/2019/technical-preview-1906#additional-options-for-third-party-update-catalogs) <!--4469002-->
- [Contenu de l’application en clair provenant du cache client au cours de la séquence de tâches](/sccm/core/get-started/2019/technical-preview-1906#bkmk_tscache) <!--4485675-->
- [Nouvelle catégorie de produit Windows 10, version 1903 et ultérieure](/sccm/core/get-started/2019/technical-preview-1906#new-windows-10-version-1903-and-later-product-category) <!--4682946-->
- [Règles d’insights de gestion pour le secours NTLM](/sccm/core/get-started/2019/technical-preview-1906#bkmk_ntlm) <!--4572953-->
- [Filtrer les applications déployées sur des appareils](/sccm/core/get-started/2019/technical-preview-1906#bkmk_appcategory) <!--4451056-->
- [Améliorations apportées au déploiement de système d’exploitation](/sccm/core/get-started/2019/technical-preview-1906#bkmk_osd) <!--4668846, 2840337, 4512937-->
- [Lien direct vers des onglets personnalisés dans le Centre logiciel](/sccm/core/get-started/2019/technical-preview-1906#bkmk_swctr) <!--4655176-->

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
 | Contrôle amélioré sur la maintenance de WSUS <!--4110109--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#improved-control-over-wsus-maintenance) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées à la console Configuration Manager <!--4616810--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_console) | ![Non ajouté](media/Red_X.gif) |
 | Configurer la durée maximale d’exécution par défaut pour les mises à jour logicielles <!--3734426--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_timeout) | ![Non ajouté](media/Red_X.gif) |
 | Critères d’approbation des fichiers Windows Defender Application Guard <!--3555858--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_wdag) | ![Non ajouté](media/Red_X.gif) |
 | Groupes d’applications <!--3555907--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_app-group) | ![Non ajouté](media/Red_X.gif) |
 | Séquence de tâches en tant que type de déploiement de modèle d’application <!--3555953--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdt) | ![Non ajouté](media/Red_X.gif) |
 | Gestion de BitLocker <!--3601034--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_bitlocker) | ![Non ajouté](media/Red_X.gif) |
 | Débogueur de séquences de tâches <!--3612274--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_tsdebug) | ![Non ajouté](media/Red_X.gif) |
 | Optimisation de la distribution dans le tableau de bord Sources de données du client <!--3555759--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_do) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées au Hub Communauté <!--4224401--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_hub) | ![Non ajouté](media/Red_X.gif) |
 | Afficher le GUID SMBIOS dans les listes d’appareils <!--4526580--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_smbios) | ![Non ajouté](media/Red_X.gif) |
 | Visionneuse du journal OneTrace <!--3555962--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_onetrace) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées à l’infrastructure du Centre logiciel <!--3555950--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_swctr) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées aux personnalisations d’onglet du Centre logiciel <!--4063773--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#improvements-to-software-center-tab-customizations) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées aux approbations d’applications <!--4224910--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_approve) | ![Non ajouté](media/Red_X.gif) |
 | Recommencer l’installation d’applications préalablement approuvées <!--4336307--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_retry) | ![Non ajouté](media/Red_X.gif) |
 | Installer des applications pour un appareil <!--4402180--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_device-app) | ![Non ajouté](media/Red_X.gif) |
 | Notifications de compte à rebours plus fréquentes pour les redémarrages <!--3976435--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_restart) | ![Non ajouté](media/Red_X.gif) |
 | Synchroniser les résultats d’adhésion à un regroupement dans des groupes Azure Active Directory <!--3607475--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_aadcollsync) | ![Non ajouté](media/Red_X.gif) |
 | Configurer la période de conservation minimale du cache client <!--4485509--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_cache) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées au déploiement de système d’exploitation <!--4512937,4224642--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_osd) | ![Non ajouté](media/Red_X.gif) |
 | Ajouter un nœud SQL AlwaysOn <!--3127336--> | [Tech Preview 1905](/sccm/core/get-started/2019/technical-preview-1905#bkmk_sqlao) | ![Non ajouté](media/Red_X.gif) |
 | Tableau de bord de préparation de la mise à niveau d’Office 365 ProPlus <!--4021125--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_o365) | ![Non ajouté](media/Red_X.gif) |
 | Configurer la mise à jour dynamique lors des mises à jour des fonctionnalités <!--4062619--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#configure-dynamic-update-during-feature-updates) | ![Non ajouté](media/Red_X.gif) |
 | Hub de la communauté et GitHub <!--3555935,3555936--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#community-hub-and-github) | ![Non ajouté](media/Red_X.gif) |
 | CMPivot autonome <!--3555890--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_cmpivot) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées à l’infrastructure du Centre logiciel <!--3555950--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_swctr) | ![Non ajouté](media/Red_X.gif) |
 | Contrôle amélioré sur la maintenance de WSUS <!--4110109--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#improved-control-over-wsus-maintenance) | ![Non ajouté](media/Red_X.gif) |
 | Mettre en cache préalablement des packages de pilotes et des images de système d’exploitation <!--4224642--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_precache) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées au déploiement de système d’exploitation <!--2839943,4447680--> | [Tech Preview 1904](/sccm/core/get-started/2019/technical-preview-1904#bkmk_osd) | ![Non ajouté](media/Red_X.gif) |
 | Estimateur de coût des services cloud <!--3555774--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_cmg) | ![Non ajouté](media/Red_X.gif) |
 | Utiliser votre point de distribution comme serveur de cache local pour l’optimisation de la distribution <!--3555764--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_doinc) | ![Non ajouté](media/Red_X.gif) |
 | Récupérer le verrou pour la modification des séquences de tâches <!--3699337--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_sedo) | ![Non ajouté](media/Red_X.gif) |
 | Explorer les mises à jour obligatoires <!--4224414--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_req-updates) | ![Non ajouté](media/Red_X.gif) |
 | Améliorations apportées à la création d’un média de séquence de tâches <!--4090666--> | [Tech Preview 1903](/sccm/core/get-started/2019/technical-preview-1903#bkmk_tsmedia) | ![Non ajouté](media/Red_X.gif) |


## <a name="features-in-previous-technical-previews"></a>Fonctionnalités des précédentes préversions techniques

Les fonctionnalités suivantes ont été publiées avec les versions antérieures de la branche Technical Preview de Configuration Manager. Ces fonctionnalités restent disponibles dans les versions ultérieures, mais ne sont pas encore disponibles dans la branche Current Branch.

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

| Fonctionnalité        | Version Technical Preview |  
|----------------|---------------------------|
| Télécharger des rapports depuis le Hub Communauté<!--3555936--> | [Tech Preview 1812](capabilities-in-technical-preview-1812.md#bkmk_hub) |
| Hub Communauté <!--3556020, fka 1357766--> | [Tech Preview 1807](capabilities-in-technical-preview-1807.md#bkmk_hub) |
| Service de répondeur PXE basé sur le client <!--3556018, fka 1357148--> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
| Prise en charge du démarrage réseau PXE pour IPv6 <!--3601254, fka 1269793--> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
| Utiliser Azure Active Directory <!--3607315, fka 1322145--> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
| Améliorations apportées à Asset Intelligence <!--3601024, fka 1307390--> | [Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence) |
| Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise <!--3601249, fka 1037233--> | [Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End) |

## <a name="see-also"></a>Voir aussi  

Pour plus d’informations, consultez les articles suivants :  

- [Évaluer Configuration Manager dans un laboratoire](/sccm/core/get-started/evaluate-with-lab-environment)
- [Nouveautés des versions incrémentielles de Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
- [Présentation de Configuration Manager](/sccm/core/understand/introduction)

> [!Tip]  
> Pour plus d’informations sur les fonctionnalités Current Branch qui nécessitent un consentement pour être activées, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).  
>
> Pour plus d’informations sur les fonctionnalités Current Branch qui doivent être activées en premier, consultez [Activation de fonctionnalités facultatives de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
