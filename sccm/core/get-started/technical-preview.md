---
title: Versions Technical Preview
titleSuffix: Configuration Manager
description: Découvrez la version Technical Preview pour tester les nouvelles fonctions et fonctionnalités de Configuration Manager.
ms.date: 05/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9ce0a8cb-f96c-4e41-834c-59ceb54ce44a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a6a4faff728b14fae198f9709ca9ce9ca5d04455
ms.sourcegitcommit: 021272d5858e5dbb650b95644736d1de3dab7d8a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/15/2018
---
# <a name="technical-preview-for-system-center-configuration-manager"></a>Technical Preview pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

**Bienvenue dans System Center Configuration Manager Technical Preview**. Cette rubrique fournit des détails sur la préversion qui présente de nouvelles fonctions et fonctionnalités que nous développons actuellement. Chaque version Technical Preview inaugure de nouvelles fonctionnalités qui ne sont pas présentes dans la version Current Branch de Configuration Manager au moment où la version Technical Preview est publiée. Ces fonctionnalités seront incluses dans une mise à jour de la version Current Branch, mais avant de finaliser et d’ajouter les fonctionnalités, nous souhaitons que vous puissiez les tester et nous faire part de vos commentaires.  

 Comme il s’agit d’une version Technical Preview, les détails et les fonctionnalités sont susceptibles de changer.  

 Cet article contient des informations qui s’appliquent à toutes les versions Technical Preview. Il liste également chaque nouvelle fonctionnalité, ainsi que la version Technical Preview où la fonctionnalité apparaît pour la première fois, par exemple la version 1805 de mai 2018. Ces fonctionnalités sont détaillées dans des rubriques distinctes dédiées à chaque préversion.  

 Pour plus d’informations sur les nouveautés de la version Current Branch de Configuration Manager, consultez [Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/what-has-changed-from-configuration-manager-2012).



##  <a name="bkmk_reqs"></a> Configuration requise et limitations pour Technical Preview  

> [!IMPORTANT]     
>  La licence de la version Technical Preview est destinée uniquement aux environnements de laboratoire.  Microsoft peut ne pas fournir de services de support technique, et certaines fonctionnalités peuvent ne pas être disponibles dans la préversion du logiciel. De plus, la préversion du logiciel peut utiliser des standards de sécurité, de confidentialité, d’accessibilité, de disponibilité et de fiabilité réduites ou différentes par rapport aux logiciels fournis dans le commerce.  

 La plupart des prérequis du produit sont abordés dans [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md). Les exceptions suivantes s'appliquent aux versions Technical Preview :  

-   Chaque installation reste active pendant 90 jours, puis devient inactive.  

-   L'anglais est la seule langue prise en charge.


-   Seuls les indicateurs d'installation (commutateurs) suivants sont pris en charge :  

    -   **/silent**  
    -   **/testdbupgrade**    


-   Par défaut, quand vous utilisez la version Technical Preview, le point de connexion de service est installé en mode en ligne. Le basculement en mode hors connexion n’est pas pris en charge.

-   Les articles dédiés à chaque version Technical Preview décrivent les limitations ou les spécifications supplémentaires, le cas échéant.

-   Il n'existe aucune prise en charge pour la migration vers ou à partir de cette préversion.  

-   Il n'existe aucune prise en charge pour la mise à niveau vers cette préversion. 

-   Il n’existe aucune prise en charge pour la récupération de site à partir du dossier cd.latest.  <!--507106-->

-   Il n’existe aucune prise en charge de mise à niveau vers une build de production (Current Branch) à partir de cette build de version Preview. Cependant, quand des mises à jour sont disponibles pour une version Preview, vous pouvez les rechercher et les installer à partir du nœud **Mises à jour et maintenance** de la console Configuration Manager. Pour obtenir une vidéo du processus de mise à niveau dans la console, consultez [Installing ConfigMgr Update Packages](https://www.youtube.com/embed/KBd_EGFbUT8) sur youtube.com.  
-   Seul un site principal autonome est pris en charge. Il n'existe aucune prise en charge pour un site d'administration centrale, plusieurs sites principaux ou des sites secondaires.  

Les produits et technologies suivants sont pris en charge par cette branche de Configuration Manager. Toutefois, leur inclusion dans ce contenu n’implique pas une extension de prise en charge d’un produit ou d’une version au-delà de leur cycle de vie individuel. L’utilisation de produits qui ont dépassé leur cycle de vie n’est pas prise en charge avec Configuration Manager. Pour plus d’informations sur les politiques de support Microsoft, consultez le site web [Politique de support Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=208270) .  

-   Seules les versions suivantes de SQL Server sont prises en charge :  

    -   SQL Server 2017 (avec mise à jour cumulative 2 et ultérieure) à compter de Configuration Manager version 1710
    -   SQL Server 2016 (sans Service Pack et versions ultérieures)
    -   SQL Server 2014 (avec Service Pack 1 et version ultérieure)
    -   SQL Server 2012 (avec Service Pack 3 ou version ultérieure)


-   Le site prend en charge jusqu’à 10 clients, qui doivent exécuter l’une des versions suivantes de Windows :  

      -   Windows 10  
      -   Windows 8.1  
      -   Windows 7  

##  <a name="bkmk_install"></a> Installer et mettre à jour la version Technical Preview  
 La version Technical Preview de System Center Configuration Manager se distingue de la version actuelle de System Center Configuration Manager.  

 Pour utiliser la version Technical Preview, vous devez d’abord installer une **version de référence** de la build de la version Technical Preview. Après avoir installé une version de base de référence, vous pouvez utiliser des **mises à jour dans la console** pour actualiser votre installation avec la préversion la plus récente. En règle générale, de nouvelles versions Technical Preview sont disponibles chaque mois.

Chaque préversion est prise en charge pendant la durée de disponibilité de trois versions successives. Autrement dit, quand la version 1708 est publiée, la version 1704 n’est plus prise en charge, mais les versions 1705, 1706 et 1707 le sont toujours. Quand une base de référence n’est plus prise en charge, elle l’est toujours pour l’installation d’un nouveau site Technical Preview jusqu’à ce qu’une nouvelle version de base de référence soit disponible, à condition que vous mettez ensuite à jour cette installation avec une version prise en charge. Effectuez une mise à jour avec la version la plus récente, puis répétez ce processus jusqu’à ce que vous puissiez installer la version la plus récente de la version Technical Preview.

> [!TIP]  
>  Quand vous installez une mise à jour de la version Technical Preview, vous mettez à jour votre installation avec cette nouvelle version Technical Preview. Une installation de la version Technical Preview ne donne jamais la possibilité d’effectuer une mise à niveau vers une installation de la version Current Branch, ni de recevoir des mises à jour de la version Current Branch.  

**Versions de référence actives de la version Technical Preview :**
   
Vous pouvez installer une version de référence dans un délai d’un an après sa date de publication. Toutefois, lorsque vous installez un nouveau site Technical Preview, nous vous recommandons d’utiliser la dernière version de base de référence disponible.
-  **Technical Preview 1804** : Configuration Manager Technical Preview 1804 est disponible à la fois sous la forme d’une mise à jour dans la console et en tant que nouvelle version de référence. Téléchargez les versions de référence [à partir du Centre d’évaluation TechNet](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview).


##  <a name="BKMK_TPFeedback"></a> Envoi de commentaires  
 Faites-nous part de vos commentaires sur les capacités de nos versions Technical Preview. Pour plus d’informations, consultez [Commentaires produit](../understand/find-help.md#product-feedback).

Si vous avez des idées sur de nouvelles fonctionnalités que vous aimeriez voir, n’hésitez pas à nous en faire part. Pour soumettre de nouvelles idées et voter pour les idées soumises par d'autres utilisateurs, [visitez notre page dédiée à cet usage](http://configurationmanager.uservoice.com).  

<!--   ##  <a name="bdmk_tpknownissues"></a> General changes introduced in Technical Previews    -->




##  <a name="bkmk_tpCaps"></a> Fonctionnalités fournies dans la dernière version Technical Preview  
Voici la liste des fonctionnalités fournies par la version Technical Preview de Configuration Manager la plus récente.  Les fonctionnalités disponibles dans une version Technical Preview antérieure restent disponibles dans les versions ultérieures. De même, les fonctionnalités qui ont été ajoutées à la version Current Branch de Configuration Manager restent disponibles dans les versions Technical Preview.  Cliquez sur le contenu de chaque version Technical Preview pour en savoir plus sur une fonctionnalité spécifique.  

<!-- This is the full list of new features in the latest TP release -->

### <a name="technical-preview-version-1805"></a>Technical Preview version 1805
- [Créer un déploiement en plusieurs phases configurées manuellement pour une séquence de tâches](capabilities-in-technical-preview-1805.md#create-a-phased-deployment-with-manually-configured-phases-for-a-task-sequence) <!--1358148--> 
- [Prise en charge du point de distribution cloud pour Azure Resource Manager](capabilities-in-technical-preview-1805.md#cloud-distribution-point-support-for-azure-resource-manager) <!--1322209--> 
- [Agir en fonction des insights de gestion](capabilities-in-technical-preview-1805.md#take-actions-based-on-management-insights) <!--1357930--> 
- [Transférer la charge de travail de configuration des appareils vers Intune avec la cogestion](capabilities-in-technical-preview-1805.md#transition-device-configuration-workload-to-intune-using-co-management) <!--1357903--> 
- [Configurer les points de distribution pour utiliser le contrôle de surcharge du réseau](capabilities-in-technical-preview-1805.md#enable-distribution-points-to-use-network-congestion-control) <!--1358112--> 
- [Tableau de bord de gestion cloud](capabilities-in-technical-preview-1805.md#cloud-management-dashboard) <!--1358461--> 
- [CMPivot](capabilities-in-technical-preview-1805.md#cmpivot) <!--1358456--> 
- [Amélioration des communications clientes sécurisées](capabilities-in-technical-preview-1805.md#improved-secure-client-communications) <!--1356889,1358228,1358460--> 
- [Améliorations concernant la prise en charge des mises à jour des logiciels tiers](capabilities-in-technical-preview-1805.md#improvements-for-enabling-third-party-software-update-support) <!--1357605--> 
- [Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10](capabilities-in-technical-preview-1805.md#improvements-to-windows-10-in-place-upgrade-task-sequence) <!--1358500--> 
- [CMTrace installé avec le client](capabilities-in-technical-preview-1805.md#cmtrace-installed-with-client) <!--1357971--> 
- [Améliorations apportées à la console Configuration Manager](capabilities-in-technical-preview-1805.md#improvement-to-the-configuration-manager-console) <!--1358202--> 
- [Améliorations apportées à la fonctionnalité Commentaires de la console](capabilities-in-technical-preview-1805.md#improvements-to-console-feedback) <!--1357542--> 
- [Améliorations des points de distribution compatibles PXE](capabilities-in-technical-preview-1805.md#improvements-to-pxe-enabled-distribution-points) <!--1357580--> 
- [Amélioration apportées à l’inventaire matériel pour les valeurs d’entiers longs](capabilities-in-technical-preview-1805.md#improvement-to-hardware-inventory-for-large-integer-values) <!--1357880--> 
- [Améliorations apportées à la maintenance de WSUS](capabilities-in-technical-preview-1805.md#improvement-to-wsus-maintenance) <!--1357898--> 
- [Améliorations apportées à la prise en charge des certificats CNG](capabilities-in-technical-preview-1805.md#improvement-to-support-for-cng-certificates) <!--1357314--> 






## <a name="capabilities-delivered-in-recent-supported-technical-previews"></a>Fonctionnalités fournies dans les versions Technical Preview prises en charge récentes
Voici la liste des fonctionnalités fournies avec les versions Technical Preview de Configuration Manager précédentes qui sont encore prises en charge. 

<!-- This is the full list of new features in the past THREE (3) TP releases. 
Each month, add features from the list above to the top of this table. 
Then remove the bottom of this list and/or move individual items not in CB to the third table below.
-->

 |Fonctionnalité |Version Technical Preview |Version Current Branch|  
 |----------------|---------------------|--------------------|
 | Configurer une bibliothèque de contenu à distance pour le serveur de site <!--1357525--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configure-a-remote-content-library-for-the-site-server)  | ![Non ajouté](media/Red_X.gif) | 
 | Envoyer des commentaires à partir de la console Configuration Manager <!--1357542--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#bkmk_feedback)  | ![Non ajouté](media/Red_X.gif) | 
 | Centre d’aide et de support <!--1357489--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#support-center)  | ![Non ajouté](media/Red_X.gif) | 
 | Kit de ressources de Configuration Manager <!--1357145--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#configuration-manager-toolkit)  | ![Non ajouté](media/Red_X.gif) | 
 | Désinstaller une application en cas de révocation de l’approbation <!--1357891--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#uninstall-application-on-approval-revocation)  | ![Non ajouté](media/Red_X.gif) | 
 | Exclure les conteneurs Active Directory de la découverte <!--1358143--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#exclude-active-directory-containers-from-discovery)  | ![Non ajouté](media/Red_X.gif) | 
 | Spécifier la visibilité du lien du site web Catalogue d’applications dans le Centre logiciel <!--1358214--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#specify-the-visibility-of-the-application-catalog-website-link-in-software-center)  | ![Non ajouté](media/Red_X.gif) | 
 | Filtrer les règles de déploiement automatique par architecture de mise à jour logicielle <!--1322266--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#filter-automatic-deployment-rules-by-software-update-architecture)  | ![Non ajouté](media/Red_X.gif) | 
 | Améliorations apportées au déploiement de système d’exploitation <!--1358330,1358493--> | [Tech Preview 1804](capabilities-in-technical-preview-1804.md#improvements-to-os-deployment) | ![Non ajouté](media/Red_X.gif) | 
 | Prise en charge des points de distribution cloud comme source par les points de distribution d’extraction <!--1321554--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#pull-distribution-points-support-cloud-distribution-points-as-source)  | ![Non ajouté](media/Red_X.gif) | 
 | Prise en charge du téléchargement partiel dans le cache d’homologue client pour réduire l’utilisation du réseau WAN <!--1357346--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#partial-download-support-in-client-peer-cache-to-reduce-wan-utilization)  | ![Non ajouté](media/Red_X.gif) | 
 | Fenêtres de maintenance dans le Centre logiciel <!--1358131--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#maintenance-windows-in-software-center)  | ![Non ajouté](media/Red_X.gif) | 
 | Onglet personnalisé pour une page web du Centre logiciel <!--1358132--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#custom-tab-for-webpage-in-software-center)  | ![Non ajouté](media/Red_X.gif) | 
 | Activer la prise en charge des mises à jour de logiciels tiers sur des clients <!--1357605--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-third-party-software-update-support-on-clients)  | ![Non ajouté](media/Red_X.gif) | 
 | Activer le copier/coller des détails de composants à partir d’affichages d’analyse <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#enable-copypaste-of-asset-details-from-monitoring-views)  | ![Non ajouté](media/Red_X.gif) | 
 | Extensions SCAP <!--1357552--> | [Tech Preview 1803](capabilities-in-technical-preview-1803.md#scap-extensions)  | ![Non ajouté](media/Red_X.gif) | 
 | Transférer la charge de travail Endpoint Protection vers Intune avec la cogestion <!-- 1357365 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#transition-endpoint-protection-workload-to-intune-using-co-management) | [Version 1802](/sccm/core/clients/manage/co-management-switch-workloads#workloads-able-to-be-transitioned-to-intune) |  
 | Configurer l’Optimisation de la distribution de Windows de façon à utiliser des groupes de limites Configuration Manager <!-- 1324696 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#configure-windows-delivery-optimization-to-use-configuration-manager-boundary-groups) | [Version 1802](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#delivery-optimization) |  
 | Séquence de tâches de mise à niveau sur place de Windows 10 via la passerelle de gestion cloud <!-- 1357149 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#windows-10-in-place-upgrade-task-sequence-via-cloud-management-gateway) | [Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#deploy-windows-10-in-place-upgrade-via-cmg) |  
 | Améliorations apportées à la séquence de tâches de mise à niveau sur place de Windows 10 <!-- 1357425 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-windows-10-in-place-upgrade-task-sequence) | [Version 1802](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system) |  
 | Améliorations apportées aux points de distribution compatibles PXE <!-- 1357580 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-pxe-enabled-distribution-points) | ![Non ajouté](media/Red_X.gif) | 
 | Modèles de déploiement pour les séquences de tâches <!-- 1357391 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#deployment-templates-for-task-sequences) | [Version 1802](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS) |  
 | Tableau de bord Cycle de vie du produit <!--1319632 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#product-lifecycle-dashboard) | ![Non ajouté](media/Red_X.gif) | 
 | Améliorations apportées à la création de rapports <!--1357653 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-reporting) | [Version 1802](/sccm/core/servers/manage/list-of-reports#operating-system) |  
 | Améliorations apportées au Centre logiciel <!--1357592 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-software-center) | [Version 1802](/sccm/core/clients/deploy/about-client-settings#BKMK_HideInstalled) |  
 | Groupe de limites de secours pour les points de gestion <!-- 1324594 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#boundary-group-fallback-for-management-points) | [Version 1802](/sccm/core/servers/deploy/configure/boundary-groups#management-points) |  
 | Prise en charge améliorée des certificats de passerelle de gestion cloud <!-- 1357314 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improved-support-for-cng-certificates) | [Version 1802](/sccm/core/plan-design/network/cng-certificates-overview) |  
 | Prise en charge de la passerelle de gestion cloud pour Azure Resource Manager <!-- 1324735 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#cloud-management-gateway-support-for-azure-resource-manager) | [Version 1802](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager) |  
 | Approuver les demandes d’application pour les utilisateurs appareil par appareil <!-- 1357015 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#approve-application-requests-for-users-per-device) | [Version 1802](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) |  
 | Utiliser le Centre logiciel pour parcourir et installer des applications accessibles aux utilisateurs sur des appareils joints à Azure AD <!-- 1322613 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#use-software-center-to-browse-and-install-user-available-applications-on-azure-ad-joined-devices) | [Version 1802](/sccm/apps/deploy-use/deploy-applications#deploy-user-available-applications-on-azure-ad-joined-devices) |  
 | Générer un rapport sur les informations d’appareil Windows AutoPilot <!-- 1351442 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-on-windows-autopilot-device-information) | [Version 1802](/sccm/core/clients/manage/co-management-prepare#new-windows-10-devices) |  
 | Améliorations apportées aux stratégies de Configuration Manager pour Windows Defender Exploit Guard <!-- 1356220 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#improvements-to-configuration-manager-policies-for-windows-defender-exploit-guard) | [Version 1802](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) |  
 | Stratégies du navigateur Microsoft Edge <!-- 1357310 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#microsoft-edge-browser-policies) | [Version 1802](/sccm/compliance/deploy-use/browser-profiles) | 
 | Rapports pour le nombre de navigateurs par défaut <!-- 1357830 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#report-for-default-browser-counts) | [Version 1802](/sccm/core/servers/manage/list-of-reports#software---companies-and-products) | 
 | Prise en charge des appareils Windows 10 ARM64 <!-- 1353704 --> | [Tech Preview 1802](capabilities-in-technical-preview-1802.md#support-for-windows-10-arm64-devices) | [Version 1802](/sccm/core/plan-design/configs/support-for-windows-10) |  
 
  

## <a name="capabilities-delivered-in-previous-technical-previews"></a>Fonctionnalités fournies dans les versions Technical Preview précédentes
Voici la liste des fonctionnalités spécifiques fournies avec les versions Technical Preview de Configuration Manager précédentes. Ces fonctionnalités restent disponibles dans les versions ultérieures, mais ne sont pas encore disponibles dans une version Current Branch. 

<!-- This is the list of individual features that are still in TP (not in CB). 
**Note there is no third column in this table!**
Copy from the bottom of the list above any individual feature that is still in TP and add to the top of this list (then remove the third column)
With each CB release, review and remove from this list for anything that's now available in CB. 
-->

 |Fonctionnalité |Version Technical Preview |  
 |----------------|---------------------|
 | Service de répondeur PXE basé sur le client <!-- 1357148 --> | [Tech Preview 1712](capabilities-in-technical-preview-1712.md#client-based-pxe-responder-service) |
 |Rôle serveur site haute disponibilité <!-- 1128774 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) |
 |Prise en charge du démarrage réseau PXE pour IPv6 <!-- 1269793 --> |[Tech Preview 1706](capabilities-in-technical-preview-1706.md#pxe-network-boot-support-for-ipv6)|
 |Utiliser Azure Active Directory <!-- 1322145? --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#azurediscovery) |
 |Évaluation de la conformité des mises à jour Windows Update pour Entreprise <!-- 1235390 --> | [Tech Preview 1702](capabilities-in-technical-preview-1702.md#compliance-assessment-for-windows-update-for-business-updates) |
 |Accès aux données de point de terminaison OData <!-- 1321523 --> |[Tech Preview 1612](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access)|
 |Améliorations apportées à Asset Intelligence <!-- 1307390 --> |[Tech Preview 1608](capabilities-in-technical-preview-1608.md#improvements-to-asset-intelligence)|
 |Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise <!-- 1037233? --> |[Tech Preview 1605](capabilities-in-technical-preview-1605.md#BKMK_End)|



## <a name="see-also"></a>Voir aussi  
[Nouveautés de System Center Configuration Manager](/sccm/core/plan-design/changes/whats-new-incremental-versions)  
 [Présentation de System Center Configuration Manager](../../core/understand/introduction.md)

> [!Tip]  
> Pour plus d’informations sur les fonctionnalités Current Branch qui nécessitent un consentement pour être activées, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).  
> Pour plus d’informations sur les fonctionnalités Current Branch qui doivent être activées en premier, consultez [Activation de fonctionnalités facultatives de mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

