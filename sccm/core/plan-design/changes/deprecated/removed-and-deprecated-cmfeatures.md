---
title: Fonctionnalités dépréciées
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités que Configuration Manager ne prend plus en charge.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 287a6324-ae65-4d38-b2ef-198d47c91231
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 96a9c497f7b8dbcd831fd42de646e836fc91ef29
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496342"
---
# <a name="removed-and-deprecated-features-for-configuration-manager"></a>Fonctionnalités supprimées et dépréciées pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article liste les fonctionnalités dépréciées ou supprimées du support de Configuration Manager. Les fonctionnalités dépréciées seront supprimées dans une prochaine mise à jour. Ces futurs changements risquent d’affecter votre utilisation de Configuration Manager.  

Ces informations sont susceptibles de changer dans les futures versions. Les fonctionnalités Configuration Manager dépréciées ne sont peut-être pas toutes listées ici.



## <a name="deprecated-features"></a>Fonctionnalités dépréciées  

|Fonctionnalité|Désapprobation annoncée|Prise en charge&nbsp;supprimée|  
|-----------|---|--------------|  
|L’implémentation du partage de contenu à partir d’Azure a évolué. Utilisez une passerelle de gestion cloud de gestion compatible avec le contenu. Vous ne pourrez pas créer de point de distribution cloud traditionnel à l’avenir.|Février 2019|Première version publiée après le 1er novembre 2019|
|Déploiement de services classiques sur Azure pour la passerelle de gestion cloud et le point de distribution cloud. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).|Novembre 2018|Première version publiée après le 1er juillet 2019| 
|System Center Endpoint Protection pour Mac et Linux<br>Pour plus d’informations, consultez le [billet de blog sur la fin du support](https://go.microsoft.com/fwlink/?linkid=870182).|Octobre 2018|31 décembre 2018|
|Accès conditionnel local<br>Pour plus d’informations, consultez [Qu’est-ce que la gestion hybride des appareils mobiles ?](/sccm/mdm/understand/hybrid-mobile-device-management)|30 janvier 2019|1er septembre 2019|
|Gestion hybride des appareils mobiles (MDM)<br>Pour plus d’informations, consultez [Qu’est-ce que la gestion hybride des appareils mobiles ?](/sccm/mdm/understand/hybrid-mobile-device-management)<br><br>À compter de la version 1902 du service Intune, attendue fin février 2019, les nouveaux clients ne peuvent plus créer de nouvelle connexion hybride.<!--Intune feature 2683117-->|14 août 2018|1er septembre 2019|
|Paramètres Windows Hello Entreprise dans Configuration Manager<br>Pour plus d’informations, consultez [Paramètres Windows Hello Entreprise](/sccm/protect/deploy-use/windows-hello-for-business-settings).|Décembre 2017|Première version publiée après le 1er novembre 2019|
|L’**expérience utilisateur Silverlight** pour le point du site web du catalogue des applications n’est plus prise en charge. Les utilisateurs doivent utiliser le nouveau Centre logiciel. REMARQUE : Les rôles de point du site web et de point de service web du catalogue des applications sont toujours pris en charge. Dans certains scénarios, le nouveau Centre logiciel communique avec le point du site web du catalogue des applications. Pour plus d’informations, consultez [Configurer le Centre logiciel](/sccm/apps/plan-design/plan-for-software-center#bkmk_userex).<!--1358309-->|11 août 2017| Version 1806|
|Ancienne version du Centre logiciel.<br><br>Pour plus d’informations sur le nouveau Centre logiciel, consultez [Planifier et configurer la gestion des applications](/sccm/apps/plan-design/plan-for-and-configure-application-management##bkmk_userex).|13 décembre 2016|Version 1802|
|Gestion de disques durs virtuels avec Configuration Manager. <br><br>Cette dépréciation inclut la suppression des options permettant de créer un nouveau disque dur virtuel ou de gérer un disque dur virtuel à l’aide d’une séquence de tâches, ainsi que la suppression du nœud Disques durs virtuels dans la console Configuration Manager. <br><br>Les disques durs virtuels existants ne sont pas supprimés, mais ne sont plus accessibles à partir de la console Configuration Manager.  |6 janvier 2017 |Version 1710|
|Séquences de tâches : <br /> - Convertir en disque dynamique <br /> - Installer les outils de déploiement |18 novembre 2016|Version 1710|
|Outil d'évaluation de mise à niveau System Center Configuration Manager. <br><br>L’outil d’évaluation de mise à niveau dépend à la fois de System Center Configuration Manager et des outils d'analyse de compatibilité des applications (ACT) 6.x. La dernière version d’ACT a été intégrée à Windows 10 v1511 ADK. Comme il n’y a plus aucune mise à jour d’ACT, la prise en charge de l’outil d’évaluation de mise à niveau prend fin. <br><br>L’outil d’évaluation de mise à niveau est remplacé par la fonctionnalité [Disponibilité pour la mise à niveau](/sccm/core/clients/manage/upgrade/upgrade-analytics). Une note de dépréciation a été ajoutée à la [page de téléchargement UAT](https://www.microsoft.com/download/details.aspx?id=37145) le 12 septembre 2016. | 12 septembre 2016  | 11 juillet 2017 |
|Points de mise à jour logicielle avec un cluster NLB (équilibrage de la charge réseau) | 27 février 2016 | Version 1702 | 
|Séquences de tâches : <br /> - OSDPreserveDriveLetter  <br /><br /> Lors d’un déploiement de système d’exploitation, par défaut, le programme d’installation Windows détermine désormais la meilleure lettre de lecteur à utiliser (généralement C:). Si vous souhaitez spécifier un autre lecteur à utiliser, vous pouvez modifier l’emplacement dans l’étape de séquence de tâches Appliquer le système d’exploitation. Accédez au paramètre **Sélectionnez l’emplacement où vous souhaitez appliquer ce système d'exploitation**. Sélectionnez **Lettre de lecteur logique spécifique** et choisissez le lecteur que vous souhaitez utiliser. |20 juin 2016 |Version 1606 |
|Protection d’accès réseau (NAP) : telle que dans System Center 2012 Configuration Manager|10 juillet 2015|Version 1511|  
|Gestion hors bande : telle que dans System Center 2012 Configuration Manager|16 octobre 2015|Version 1511|



## <a name="features-removed-in-version-1511"></a>Fonctionnalités supprimées dans la version 1511
Les sections suivantes contiennent des détails supplémentaires sur les fonctionnalités supprimées avec la version 1511 :

###  <a name="bkmk_amt"></a> Gestion hors bande  
 Avec Configuration Manager, la prise en charge native des ordinateurs AMT à partir de la console Configuration Manager est supprimée.  

-   Les ordinateurs AMT restent entièrement gérés quand vous utilisez le [module complémentaire Intel SCS pour Microsoft System Center Configuration Manager](http://www.intel.com/content/www/us/en/software/setup-configuration-software.html). Ce module complémentaire vous permet d’accéder aux dernières fonctionnalités permettant de gérer AMT tout en supprimant les limitations introduites jusqu’à ce que Configuration Manager puisse intégrer ces changements.  

-   La gestion hors bande dans System Center 2012 Configuration Manager n’est pas affectée par cette modification.  

###  <a name="bkmk_nap"></a> Protection d’accès au réseau  
 System Center Configuration Manager ne prend pas en charge la protection d’accès réseau. La fonctionnalité est dépréciée dans Windows Server 2012 R2 et a été supprimée dans Windows 10.  

 Pour les solutions de protection d'accès réseau, consultez la section *Fonctionnalités déconseillées* dans [Vue d'ensemble des services de stratégie et d'accès réseau](https://technet.microsoft.com/library/hh831683.aspx).



## <a name="more-information"></a>Informations complémentaires
Pour plus d'informations, voir :
 - [Supprimé et déprécié](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated)
 - [Politique de support Microsoft](https://support.microsoft.com/lifecycle)
 - [Prise en charge des versions Current Branch de System Center Configuration Manager](/sccm/core/servers/manage/current-branch-versions-supported).
