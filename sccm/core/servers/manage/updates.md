---
title: Mises à jour et maintenance
titleSuffix: Configuration Manager
description: Découvrez la méthode de service dans la console, appelée « Mises à jour et maintenance », qui facilite la localisation et l’installation des mises à jour recommandées.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3a832943-580a-4a40-b454-961d0854ac2b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd0caf8db2c5d0c29c43f3be1e20a0b8adc01fce
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125270"
---
# <a name="updates-and-servicing-for-configuration-manager"></a>Mises à jour et maintenance pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager utilise une méthode de service dans la console appelée **Mises à jour et maintenance**. Cette méthode dans la console facilite la localisation et l’installation des mises à jour recommandées pour votre infrastructure Configuration Manager. La maintenance dans la console est complétée par des mises à jour hors bande, telles que des correctifs logiciels. Celles-ci s’adressent aux clients qui ont besoin de résoudre des problèmes qui peuvent être propres à leur environnement.  

> [!TIP]  
> Les termes *mise à niveau*, *mise à jour* et *installation* sont utilisés pour décrire trois concepts distincts dans Configuration Manager. Pour plus d’informations sur l’utilisation de chaque terme, consultez [À propos de la mise à niveau, de la mise à jour et de l’installation](/sccm/core/understand/upgrade-update-install).  



##  <a name="bkmk_Baselines"></a> Versions de base et de mise à jour  

La dernière version de base est à utiliser quand il s’agit d’installer un nouveau site dans une nouvelle hiérarchie. 
- Utilisez également une version de base de référence pour effectuer la mise à niveau à partir de System Center 2012 Configuration Manager.  

- Après la mise à niveau vers la version Current Branch de Configuration Manager, n’utilisez pas les versions de base de référence pour rester à jour. À la place, utilisez uniquement les [mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates) pour effectuer une mise à jour vers la version la plus récente.  

- D’autres versions de base sont publiées régulièrement. Quand vous utilisez la dernière version de base de référence pour installer une nouvelle hiérarchie, cela vous évite d’installer une version obsolète ou non prise en charge de Configuration Manager, suivie d’une mise à niveau supplémentaire de votre infrastructure pour la mettre à jour.  

Après avoir installé une version de base, d’autres versions de Configuration Manager sont disponibles sous forme de mises à jour dans la console. Les mises à jour dans la console mettent à jour votre infrastructure vers la dernière version de Configuration Manager.  

-   L’installation des mises à jour dans la console visent à mettre à jour la version de votre site de niveau supérieur.  

-   Les mises à jour que vous installez sur le site d’administration centrale s’installent automatiquement sur les sites principaux enfants. Contrôlez cette synchronisation à l’aide d’une fenêtre de maintenance sur le site principal.  

-   Mettez à jour manuellement les sites secondaires vers une nouvelle version de mise à jour à partir de la console.  

Quand vous installez une mise à jour, elle stocke les fichiers d’installation de cette version sur le serveur de site dans un dossier nommé **CD.Latest**. Pour plus d’informations sur ces fichiers, consultez [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).  

-   Utilisez les fichiers du dossier CD.Latest durant la récupération de site. De même, quand votre hiérarchie n’exécute plus de version de base de référence, utilisez ces fichiers pour installer des sites supplémentaires.  

-   Vous ne pouvez pas vous servir des fichiers d’installation du dossier CD.Latest pour installer le premier site d’une nouvelle hiérarchie, ni pour mettre à niveau un site à partir de System Center 2012 Configuration Manager.  


### <a name="version-details"></a>Détails de la version

Certaines mises à jour de Configuration Manager sont disponibles à la fois comme version de mise à jour dans la console pour l’infrastructure existante et comme nouvelle version de base.  

#### <a name="supported-versions"></a>Versions prises en charge
Les versions prises en charge suivantes de Configuration Manager sont disponibles sous forme de base de référence, de mise à jour ou les deux à la fois :  

| Version | Date de disponibilité | [Date de fin de support](/sccm/core/servers/manage/current-branch-versions-supported) | De base | Mise à jour dans la console |  
|-------------|-----------|------------|--------------|------------------------|  
| [1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)<br /><br /> 5.00.8740.1000 | 27 novembre 2018 | 27 mai 2020 | Non | Oui |
| [1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)<br /><br /> 5.00.8692.1000 | 31 juillet 2018 | 31 janvier 2020 | Non | Oui |
| [1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)<br /><br /> 5.00.8634.1000 | 22 mars 2018 | 22 septembre 2019 | Oui<sup>[Remarque 1](#bkmk_note1)</sup> | Oui |
| [1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)<br /><br /> 5.00.8577.1000 | 20 novembre 2017 | Mai 20, 2019 | Non | Oui |

<a name="bkmk_note1"></a> 

> [!Note]  
> <sup>**Remarque 1 :**</sup> le support de la base de référence 1802 est disponible dans les versions suivantes du [centre MVLS](https://www.microsoft.com/Licensing/servicecenter/Downloads/DownloadsAndKeys.aspx) (Microsoft Volume Licensing Service) :
> - System Center Config Mgr (Current Branch)
> - System Center 2016 Datacenter
> - System Center 2016 Standard  
> 
> Par exemple, recherchez `System Center Config Mgr (current branch)` dans le Centre MVLS. Recherchez le support de la base de référence 1802 dans la liste des fichiers, puis téléchargez-le pour cette version.  

#### <a name="historical-versions"></a>Versions historiques
Le tableau suivant liste les versions historiques de l’édition Current Branch de Configuration Manager qui ne sont plus prises en charge :

| Version | Date de disponibilité | Date de fin du support | De base | Mise à jour dans la console |  
|-------------|-----------|------------|--------------|------------------------|  
| 1706 <br /><br /> 5.00.8540.1000 | 31 juillet 2017 | 31 juillet 2018 | Non | Oui |
| 1702 <br /><br /> 5.00.8498.1000 | 27 mars 2017 | 27 mars 2018 | Oui | Oui |
| 1610 <br /><br /> 5.00.8458.1000 | 18 novembre 2016 | 18 novembre 2017 | Non | Oui |
| 1606 <br /><br /> 5.00.8412.1000 | 22 juillet 2016 | 22 juillet 2017 | Non | Oui |
| 1606 avec le correctif cumulatif 1606 (KB3186654) <br><br>5.00.8412.1307 | 12 octobre 2016 | 12 octobre 2017 | Oui | Non |
| 1602<br /><br /> 5.00.8355.1000 | 11 mars 2016 | 11 mars 2017 | Non | Oui |
| 1511 <br /><br /> 5.00.8325.1000 | 8 décembre 2015 | 8 décembre 2016 | Oui | Non |  

#### <a name="how-to-check-the-version"></a>Comment vérifier la version
Pour vérifier la version de votre site Configuration Manager, en haut à gauche de la console, accédez à **À propos de System Center Configuration Manager**. Cette boîte de dialogue affiche les versions du site et de la console.  

 > [!Note]  
 > À compter de la version 1802, la version de la console est légèrement différente de la version du site. La version mineure de la console correspond maintenant à la version publiée de Configuration Manager. Par exemple, dans Configuration Manager version 1802, la version initiale du site est 5.0.8634.1000, et la version initiale de la console est 5.**1802**.1082.1700. Les numéros de build (1082) et de révision (1700) peuvent changer avec les correctifs logiciels futurs sur la version 1802.



##  <a name="bkmk_inconsole"></a> Mises à jour et maintenance dans la console  

Quand vous utilisez une installation Current Branch de System Center Configuration Manager prête pour la production, la plupart des mises à jour sont disponibles via le canal **Mises à jour et maintenance**. Cette méthode identifie, télécharge et met à disposition les mises à jour qui s’appliquent à la version et à la configuration actuelles de votre infrastructure. Elle inclut uniquement les mises à jour que Microsoft recommande à tous les clients.   

Ces mises à jour comportent :  

-   Les nouvelles versions comme la version 1802, 1806 ou 1810.  

-   Les mises à jour qui comprennent de nouveaux composants pour votre version actuelle

-   Les correctifs logiciels pour votre version de Configuration Manager que tous les clients doivent installer

Les mises à jour dans la console offrent une stabilité accrue et résolvent les problèmes courants. Elles remplacent les types de mise à jour déjà rencontrés pour les versions de produit précédentes, par exemple les Service Packs, les mises à jour cumulatives, les correctifs logiciels applicables à tous les clients et l’extension pour Microsoft Intune. 

Les mises à jour dans la console peuvent s’appliquer à un ou plusieurs des systèmes suivants :  

-   Serveurs de site principal et d’administration centrale  

-   Rôles de système de site et serveurs de système de site  

-   Instances du fournisseur SMS  

-   Consoles Configuration Manager  

-   Clients Configuration Manager  

Configuration Manager découvre de nouvelles mises à jour pour vous. Synchronisez votre point de connexion de service Configuration Manager avec le service cloud Microsoft, en notant les comportements suivants :  

-   Quand votre point de connexion de service est en mode en ligne, votre site se synchronise tous les jours avec Microsoft. Il identifie automatiquement les nouvelles mises à jour qui s’appliquent à votre infrastructure. Pour télécharger les mises à jour et les fichiers redistribuables, l’ordinateur qui héberge le rôle de système de site du point de connexion de service utilise le contexte **System** pour accéder aux emplacements Internet suivants : go.microsoft.com et download.microsoft.com. Pour plus d’informations sur les emplacements supplémentaires utilisés par le point de connexion de service, consultez [Conditions requises pour l’accès Internet](/sccm/core/servers/deploy/configure/about-the-service-connection-point#bkmk_urls).  

-   Quand votre point de connexion de service est en mode hors connexion, utilisez l’outil de connexion de service pour effectuer une synchronisation manuelle avec le cloud Microsoft. Pour plus d’informations, consultez [Utiliser l’outil de connexion de service](/sccm/core/servers/manage/use-the-service-connection-tool).  

-   Les mises à jour dans la console vous évitent d’avoir à localiser et à installer indépendamment les mises à jour, les service packs et les nouveaux composants.  

-   Installez uniquement les mises à jour dans la console de votre choix. Quand vous installez certaines mises à jour, vous pouvez sélectionner des fonctionnalités individuelles à activer et à utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

Quand vous installez une mise à jour dans la console, le processus suivant se produit :  

-   Elle procède automatiquement à une vérification de la configuration requise. Vous pouvez également effectuer cette vérification manuellement avant de commencer l’installation.  

-   Elle s’installe sur le site de niveau supérieur de votre environnement. Ce site est le site d’administration centrale si vous en avez un. Dans une hiérarchie, la mise à jour s’installe automatiquement sur les sites principaux. Contrôlez le moment où chaque serveur de site principal est autorisé à se mettre à jour à l’aide des [fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).  

-   Après la mise à jour d’un serveur de site, tous les rôles de système de site affectés se mettent automatiquement à jour. Ces rôles incluent les instances du fournisseur SMS. Une fois que le site a installé la mise à jour, la console Configuration Manager invite également son utilisateur à la mettre à jour.  

-   Si une mise à jour inclut le client Configuration Manager, possibilité vous est offerte de tester la mise à jour en préproduction ou d’appliquer tout de suite la mise à jour à tous les clients.  

-   Après la mise à jour d’un site principal, les sites secondaires ne sont pas mis à jour automatiquement. Vous devez en effet lancer manuellement leur mise à jour.  

> [!NOTE]  
>  Les branches Current Branch, Long-Term Servicing Branch et Technical Preview de Configuration Manager sont des versions distinctes. Ainsi, les mises à jour qui s’appliquent à une branche ne sont pas disponibles en tant que mises à jour dans la console pour les autres branches. Pour plus d’informations sur les branches disponibles, consultez [Quelle branche de Configuration Manager dois-je utiliser ?](/sccm/core/understand/which-branch-should-i-use)



##  <a name="bkmk_outofband"></a> Correctifs logiciels hors bande  

Certains correctifs logiciels sont publiés avec une disponibilité limitée pour résoudre des problèmes spécifiques. D’autres correctifs logiciels s’appliquent à tous les clients mais ne peuvent pas être installés via la méthode dans la console. Ces correctifs logiciels sont fournis hors bande et ne sont pas détectés à partir du service cloud Microsoft.  

En règle générale, quand vous cherchez à corriger ou à résoudre un problème lié à votre déploiement de Configuration Manager, vous pouvez explorer les correctifs logiciels hors bande par l’intermédiaire des services de support technique Microsoft, via un article de la Base de connaissances du Support Microsoft ou à partir de [billets de l’équipe System Center Configuration Manager](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) dans le blog Enterprise Mobility + Security. 

Installez ces correctifs logiciels manuellement, à l’aide de l’une des deux méthodes suivantes :  

#### <a name="update-registration-tool"></a>Outil Inscription de la mise à jour
Cet outil permet d’importer manuellement le correctif logiciel dans votre console Configuration Manager. Installez ensuite la mise à jour de la même façon que les mises à jour dans la console découvertes automatiquement.  

Cette méthode est utilisée pour les correctifs logiciels qui emploient la structure de nom de fichier suivante :  
  `<Product>-<product version>-<KB article ID>-ConfigMgr.Update.exe`    

Pour plus d’informations, consultez [Importer des correctifs logiciels avec l’outil Inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes).  

#### <a name="hotfix-installer"></a>Programme d’installation de correctif logiciel
Cet outil permet d’installer manuellement un correctif logiciel qui ne peut pas être installé via la méthode dans la console.  

Cette méthode est utilisée pour les correctifs qui emploient la structure de nom de fichier suivante :   
   `<Product>-<product version>-<KB article ID>-<platform>-<language>.exe`  

Pour plus d’informations, consultez [Utiliser le programme d’installation de correctif logiciel pour installer des mises à jour](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates).  



## <a name="next-steps"></a>Étapes suivantes

Les articles suivants peuvent vous aider à comprendre comment rechercher et installer les différents types de mise à jour pour Configuration Manager :  

-   [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates)  

-   [Utiliser l’outil de connexion de service](/sccm/core/servers/manage/use-the-service-connection-tool)  

-   [Importer des correctifs logiciels avec l’outil Inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)  

-   [Utiliser le programme d’installation de correctif logiciel pour installer des mises à jour](/sccm/core/servers/manage/use-the-hotfix-installer-to-install-updates)  


Pour plus d’informations sur la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).
