---
title: 'Installer un site à l’aide du support de la base de référence 1606 '
titleSuffix: Configuration Manager
description: Installer ou mettre à niveau vers LTSB for System Center Configuration Manager.
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0a4369e9c302c687f15b29b0daafbf4329e22a5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media-for-system-center-configuration-manager"></a>Installer et mettre à niveau avec le support de la base de référence de la version 1606 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch), (Long-Term Servicing Branch)*

Lorsque vous exécutez le programme d’installation à partir du support de la base de référence 1606 pour Configuration Manager, vous pouvez installer Long-Term Servicing Branch ou à un site Current Branch de System Center Configuration Manager.

Le support de la base de référence est disponible sous forme de DVD dans le cadre de Microsoft System Center 2016 ou de System Center Configuration Manager (Current Branch et Long-Term Servicing Branch 1606). Pour en savoir plus sur le support de la base de référence, consultez [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#baseline-and-udpate-versions).


Quand vous utilisez le média de la base de référence de la version 1606, le site que vous installez (ou vers lequel vous effectuez la mise à niveau) est le suivant :
- Un *site Current Branch* qui équivaut à un site initialement installé à l’aide du média de la base de référence 1511, puis mis à jour vers la version 1606 plus le correctif cumulatif 1606 (KB3186654).
-   Un *site LTSB* qui équivaut au site Current Branch exécutant la version 1606 plus le correctif cumulatif 1606 (KB3186654). Le média de la base de référence contient déjà le correctif cumulatif.  Toutefois, le site LTSB ne prend pas en charge toutes les fonctionnalités disponibles avec Current Branch, comme cela est indiqué dans [Présentation de Long-Term Servicing Branch dans System Center Configuration Manager](introduction-to-the-ltsb.md).

Si vous ne connaissez pas déjà les différentes branches de System Center Configuration Manager, consultez [Déterminer la branche de Configuration manager à utiliser](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Modifications apportées au programme d’installation avec le support de la base de référence 1606
Le support de la base de référence 1606 inclut les modifications suivantes dans l’installation de Configuration Manager.

### <a name="branch-and-edition"></a>Branche et édition
Quand vous exécutez le programme d’installation, une page dédiée à la gestion des licences vous est proposée, où vous pouvez sélectionner la branche de Configuration Manager à installer. Vous pouvez choisir une installation sous licence Current Branch ou LTSB, ou une version d’évaluation de Current Branch dans le cadre d’une installation sans licence.

Pour plus d’informations, consultez [Licences et branches pour System Center Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Expiration de Software Assurance
Pendant l’installation, vous avez la possibilité d’entrer la valeur de la **date d’expiration de Software Assurance**. Il s’agit d’une valeur facultative que vous pouvez spécifier pour des raisons pratiques.

> [!NOTE]
> Microsoft ne valide pas la date d’expiration que vous entrez et ne l’utilise pas pour la validation de la licence.  Vous pouvez ainsi l’utiliser en guise de rappel de votre date d’expiration. Ce rappel est pratique, car Configuration Manager vérifie régulièrement les nouvelles mises à jour logicielles proposées en ligne, et l’état de votre licence Software Assurance doit être actualisé pour être éligible à ces mises à jour supplémentaires.    

- Vous pouvez spécifier cette valeur de date dans la page **Clé de produit** de l’Assistant Installation quand vous exécutez le programme d’installation à partir du média de la base de référence de la version 1606 de System Center Configuration Manager.
- Vous pouvez également spécifier cette date en sélectionnant **Propriétés des paramètres de hiérarchie** > **Licences** dans la console Configuration Manager.

Pour plus d’informations, consultez « Contrats Software Assurance » dans [Licences et branches pour System Center Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Autres configurations préalables à la mise à niveau
Avant de démarrer une mise à niveau de System Center 2012 Configuration Manager vers LTSB, vous devez exécuter les étapes supplémentaires suivantes dans le cadre de la liste de contrôle préalable à la mise à niveau.  
Désinstallez les rôles de système de site que LTSB ne prend pas en charge :
- Point de synchronisation Asset Intelligence
- Connecteur Microsoft Intune
- Points de distribution cloud

Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).


### <a name="new-scripted-installation-options"></a>Nouvelles options d’installation par script
Le média de la base de référence de la version 1606 prend en charge une nouvelle clé de fichier de script sans assistance pour les installations par script d’un nouveau site de niveau supérieur. Elle s’applique à l’installation d’un nouveau site principal autonome ou à l’ajout d’un site d’administration centrale dans le cadre d’un scénario de développement de site.

Quand vous utilisez un script sans assistance pour installer une branche sous licence, vous devez ajouter la section, les noms de clés et les valeurs ci-dessous dans la section Options de votre script. Vous n’avez pas besoin d’utiliser ces valeurs pour l’installation par script d’une version d’évaluation de Current Branch :  

 **SABranchOptions**
-   **Nom de clé : SAActive**
  - Valeurs : 0 ou 1.  
  - Détails : 0 installe une édition d’évaluation sans licence de Current Branch et 1 installe une édition sous licence.   

- **CurrentBranch**
  - Valeurs : 0 ou 1.  
  - Détails : 0 installe Long-Term Servicing Branch et 1 installe Current Branch.  

Par exemple, pour installer une édition de Current Branch sous licence, vous utiliseriez :

  **Nom de clé : SABranchOptions**
   -    **SSActive = 1**
   - **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** ne fonctionne qu’avec le programme d’installation à partir du support de la base de référence. Cette option ne s’applique pas quand vous exécutez le programme d’installation à partir du dossier CD.Latest d’un site vous avez précédemment installé à l’aide du support de la base de référence de la version 1606.
>
> **SABranchOptions** ne s’applique pas aux mises à niveau par script de System Center 2012 Configuration Manager et donne toujours Current Branch.

Pour plus d’informations, consultez [Utiliser une ligne de commande pour installer des sites System Center Configuration Manager](/sccm/core/servers/deploy/install/use-a-command-line-to-install-sites).


## <a name="install-a-new-site"></a>Installer un nouveau site
Quand vous utilisez le support de la base de référence 1606 pour installer un nouveau site de l’une des deux branches, utilisez les procédures de planification, préparation et installation de sites décrites dans la rubrique [Installation de sites System Center Configuration Manager](/sccm/core/servers/deploy/install/installing-sites) en tenant également compte des points suivants :

- Pendant l’installation, vous devez choisir la branche de Configuration Manager à installer et vous pouvez spécifier les détails de votre contrat Software Assurance.
- Tous les sites d’une même hiérarchie doivent exécuter la même branche. Une hiérarchie ne peut pas comporter un mélange de LTSB et Current Branch sur des sites différents.
-   Nouvelle installation par script. Pour plus d’informations, consultez « Nouvelles options d’installation par script », plus haut dans cet article.

## <a name="expand-a-stand-alone-primary-site"></a>Étendre un site principal autonome
Vous pouvez développer un site principal autonome qui exécute LTSB.  Le processus n’est pas différent de celui utilisé pour un site Current Branch avec tout de même une particularité :

- Quand vous installez le nouveau site d’administration centrale, vous devez utiliser le programme d’installation disponible à partir du support de source d’installation d’origine que vous avez utilisé pour installer le site LTSB. L’exécution du programme d’installation à partir du dossier CD.Latest n’est pas prise en charge pour ce scénario.

Pour plus d’informations sur l’extension d’un site, consultez « Étendre un site principal autonome » dans [Installer un site à l’aide de l’Assistant Installation](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Mettre à niveau à partir de System Center 2012 Configuration Manager
Quand vous effectuez une mise à niveau à partir de System Center 2012 Configuration Manager, utilisez les procédures de planification, de préparation et d’installation de site décrites dans la rubrique [Mettre à niveau vers System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager), en tenant compte des changements suivants :

**Mise à niveau vers Current Branch :**
- Pendant l’installation, vous devez choisir Current Branch et vous pouvez spécifier les détails de votre contrat Software Assurance.
-   Nouvelle installation par script. Pour plus d’informations, consultez « Nouvelles options d’installation par script », plus haut dans cet article.

**Mise à niveau vers LTSB :**  
- Autres étapes à suivre incluses dans la liste de vérification préalable à la mise à niveau.
- Pendant l’installation, vous devez choisir la branche LTSB et vous pouvez spécifier les détails de votre contrat Software Assurance.
- Vous pouvez uniquement mettre à niveau un site qui exécute System Center 2012 Configuration Manager avec Service Pack 1 ou Service Pack 2, ou System Center 2012 R2 Configuration Manager avec Service Pack 1 ou sans Service Pack.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Chemins de mise à niveau sur place pour le support de la base de référence 1606
Vous pouvez utiliser le support de la base de référence 1606 pour mettre à niveau les produits suivants vers une édition sous licence de System Center Configuration Manager :
- System Center 2012 R2 Configuration Manager avec Service Pack 1
- System Center 2012 R2 Configuration Manager sans service Pack (requiert l’utilisation de médias de référence pour la version 1606 republiée le 15 décembre 2016)
- System Center 2012 Configuration Manager avec Service Pack 2
- System Center 2012 Configuration Manager avec Service Pack 1 (utilisation exigée du support de base de référence pour la version 1606 qui a été republiée le 15 décembre 2016)


Vous pouvez également utiliser ce support pour mettre à niveau une édition d’évaluation sans licence de Current Branch vers une version sous licence complète de Current Branch.

Ce média ne prend pas en charge la mise à niveau des produits suivants :
- Autres versions de System Center 2012 Configuration Manager.
- Configuration Manager 2007 ou version antérieure.
- Une installation de la version RC de System Center Configuration Manager.

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>À propos du dossier CD.Latest et de LTSB
Voici les limitations relatives à l’utilisation du média que Configuration Manager crée dans le dossier CD.Latest sur le serveur de site. Ces limitations s’appliquent aux sites qui exécutent LTSB :

Le média fourni dans le dossier CD.Latest est pris en charge pour les opérations suivantes :
- Récupération de site.
- Maintenance de site.
- Installation de sites principaux enfants supplémentaires.

Le support inclus dans le dossier CD.Latest n’est pas pris en charge pour les éléments suivants :  
- Installation d’un site d’administration centrale dans le cadre d’un scénario de développement de site

Pour plus d’informations, consultez [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Sauvegarde, récupération et maintenance de site pour LTSB
Pour sauvegarder ou récupérer un site qui exécute LTSB, ou en effectuer la maintenance, suivez les instructions et procédures décrites dans [Sauvegarde et récupération pour System Center Configuration Manager](/sccm/protect/understand/backup-and-recovery).  

Utilisez le programme d’installation de Configuration Manager à partir du dossier CD.Latest de la sauvegarde de votre site LTSB.
