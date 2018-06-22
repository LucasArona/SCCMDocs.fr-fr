---
title: À propos des Extensions SCAP (Security Content Automation Protocol)
titleSuffix: Configuraton Manager
description: Découvrir les Extensions SCAP (Security Content Automation Protocol)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 18463e4f87c60135bdc29d0f7ce4cb2f80a0eea7
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336185"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>À propos des Extensions SCAP (Security Content Automation Protocol)

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Cette fonctionnalité a été introduite dans Technical Preview version 1803 sous la forme d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). Cette préversion des Extensions SCAP peut être installée sur toutes les versions actuellement prises en charge de Configuration Manager Current Branch et LTSB 1606. À compter de Technical Preview 1803, le fichier d’installation se trouve dans cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. 

Les Extensions SCAP pour Microsoft System Center Configuration Manager vous permettent d’analyser et d’évaluer votre environnement réseau pour la conformité avec le protocole SCAP (Security Content Automation Protocol). Le protocole SCAP est défini et géré par le NIST (National Institute of Standards and Technology), un organisme basé aux États-Unis.

Les Extensions SCAP pour Microsoft System Center Configuration Manager utilisent la fonctionnalité Paramètres de conformité de Microsoft System Center Configuration Manager pour analyser les ordinateurs de votre environnement, puis documenter leur niveau de compatibilité avec la norme USGCB (United States Government Configuration Baseline).

Les extensions permettent à Configuration Manager de consommer des flux de données SCAP, d'évaluer la compatibilité des systèmes et de générer des résultats de rapports au format SCAP. Votre organisation utiliser son infrastructure Configuration Manager existante pour garantir que les ordinateurs qu’elle gère satisfont à ces exigences de conformité fédérales et génèrent les rapports USGCB nécessaires pour le NIST et l'OMB (Office of Management and Budget).

Ce guide fournit des informations pour vous aider à installer, configurer et exécuter les Extensions SCAP dans votre infrastructure System Center Configuration Manager.



# <a name="what39s-new-in-scap-extensions-prerelease-for-microsoft-system-center-configuration-manager"></a>Nouveautés de la préversion des Extensions SCAP pour Microsoft System Center Configuration Manager

Utilisez cette section pour découvrir les nouveautés de la dernière version.

La préversion des Extensions SCAP pour System Center Configuration Manager :

- Inclut une extension de la console Configuration Manager qui prend entièrement en charge la conversion de contenu SCAP en bases de référence des paramètres de conformité pour System Center Configuration Manager Current Branch.
- Prend en charge la version 1.2 des extensions SCAP et la compatibilité descendante avec les versions 1.1 et 1.0 de SCAP.


  - Prend en charge la version 1.2 du format XCCDF (Extensible Configuration Checklist Description Format).
  - Prend en charge les versions d'OVAL (Open Vulnerability and Assessment Language) jusqu'à la version 5.10.
  - Prend en charge la génération de rapports ARF (Asset Reporting Format) 1.1.
  - Prend en charge CPE (Common Platform Enumeration) 2.3.
  - Prend en charge CVE (Common Vulnerabilities and Exposures).
  - Prend en charge CCE (Common Configuration Enumeration) version 5.
  - Prend en charge Internet Explorer 8 USGCB, Windows 7 USGCB et le Pare-feu Windows 7 USGCB.

- Inclut un Assistant d’interface utilisateur pour importer du contenu SCAP 1.2/1.1/1.0 et OVAL pour la conversion en bases de référence de configuration.


  - Autorise la sélection de flux de données sources SCAP, ainsi que les bancs d'essai et profils XCCDF pour la conversion.

- Inclut un Assistant d’interface utilisateur pour exporter des résultats d’évaluation de la configuration vers un rapport XML au format SCAP.


  - Affiche le fichier source, les données Datastream SCAP, le point de référence XCCDF et le profil XCCDF utilisés pour générer la base de référence.
  - Prend en charge la génération du rapport Cyberscope Lightweight Asset Summary Results (LASR).

- Prend en charge la génération de rapports SCAP basés sur le déploiement de la base de référence de configuration. Inclut un nouveau tableau de bord pour visualiser la conformité des clients, ainsi que la conformité aux règles XCCDF. Le tableau de bord prend en charge l’extraction de rapports plus détaillés dans lesquels vous pouvez effectuer des recherches et sur lesquels vous pouvez appliquer des filtres.
- Améliore les performances de plusieurs types d’éléments de configuration convertis à partir de tests OVAL, ce qui permet une évaluation plus rapide.

- Résout plusieurs problèmes survenus dans du contenu Windows 10 DISA v1r3.

# <a name="scap-extensions-for-microsoft-system-center-configuration-manager-deployment-process"></a>Processus de déploiement des Extensions SCAP pour Microsoft System Center Configuration Manager

Ce guide décrit comment analyser, évaluer et créer des rapports sur la compatibilité SCAP à l'aide des Extensions SCAP pour Microsoft System Center Configuration Manager. Voici un bref récapitulatif des procédures que vous allez suivre :

- Préparer l'infrastructure requise pour tirer parti des extensions.
- Installer et configurer les Extensions SCAP pour Microsoft System Center Configuration Manager.
- Télécharger, installer et configurer les fichiers de flux de données SCAP à partir de la [base de données NVD (National Vulnerability Database)](http://nvd.nist.gov).
- Convertir et importer les fichiers de flux de données SCAP directement dans une base de référence des paramètres de conformité System Center Configuration Manager à l’aide de l’Assistant Importation **ou** via un fichier CAB (.cab) à l’aide de la ligne de commande de l’outil Microsoft.Sces.ScapToDcm.exe.
- Exporter les résultats de compatibilité au format SCAP à l’aide de l’Assistant Exportation ou de l’outil en ligne de commande Microsoft.Sces.DcmToScap.exe.

# <a name="terms"></a>Terminologie

**ID OVAL :** identificateur d’une définition OVAL spécifique qui est conforme au format des ID OVAL.

**Flux de données de résultat SCAP :** ensemble de composants SCAP, ainsi que les mappages de références entre des composants SCAP, qui contiennent un contenu de sortie (résultat).

**Flux de données de sources SCAP :** ensemble de composants SCAP, ainsi que les mappages de références entre des composants SCAP, qui contiennent un contenu d’entrée (source).

# <a name="prepare-the-prerequisite-infrastructure"></a>Préparer l’infrastructure requise

Vérifiez que la configuration matérielle et logicielle suivante est appliquée pour tirer parti des Extensions SCAP pour Microsoft System Center Configuration Manager.

## <a name="software-requirements"></a>Configuration logicielle

Pour installer, configurer et exécuter les Extensions SCAP pour Microsoft System Center Configuration Manager, vous devez disposer d'un ordinateur avec les logiciels suivants :

- Une [version prise en charge](/sccm/core/servers/manage/current-branch-versions-supported) de la console System Center Configuration Manager Current Branch.
- Un système d’exploitation compatible avec la console System Center Configuration Manager. Pour obtenir la liste des systèmes d’exploitation compatibles, consultez l’article [Systèmes d’exploitation pris en charge pour les consoles System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

En plus de l’ordinateur exécutant les Extensions SCAP, vous devez également disposer des éléments suivants :

- Une infrastructure System Center Configuration Manager Current Branch. Pour plus d’informations sur la configuration requise d’un déploiement de Configuration Manager, consultez l’article [Configurations prises en charge pour Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).

Les ordinateurs dont vous voulez évaluer la conformité SCAP doivent disposer des logiciels et configurations suivants :

- Le composant de gestion de la conformité et des paramètres activé sur le client Configuration Manager.
- Windows PowerShell 2.0 ou supérieur.
- La stratégie d’exécution PowerShell de Configuration Manager définie avec la valeur **Ignorer**. Pour plus d’informations, consultez l’article [Stratégie d’exécution PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).
- L’un des systèmes d’exploitation suivants
  - Version finale ou SP1 de Windows 7, 32 ou 64 bits
  - Windows 10 32 bits ou 64 bits
  - Windows Server 2012 R2

## <a name="hardware-requirements"></a>Configuration matérielle requise

La configuration système minimale requise est fournie dans ici :

[Planification des configurations matérielles pour Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware)



## <a name="accessibility-features"></a>Fonctionnalités d’accessibilité

Les Extensions SCAP pour System Center Configuration Manager incluent des outils en ligne de commande Windows qui peuvent tirer parti des fonctionnalités d’accessibilité et des outils de Windows.

- Les paramètres de ligne de commande sont décrits dans ce guide de l’utilisateur pour Microsoft.Sces.ScapToDcm.exe et Microsoft.Sces.DcmToScap.exe.
- -help et -? affiche le mode d'emploi de l'outil à l'écran, où il sera disponible pour les lecteurs d'écran et autres technologies d'assistance.
- [Accessibilité](http://windows.microsoft.com/windows/help/accessibility) Windows

Les Extensions SCAP exploitent également les fonctionnalités de System Center Configuration Manager.  Configuration Manager inclut des fonctionnalités qui rendent le produit plus accessible pour les personnes en situation de handicap.

- [Fonctionnalités d’accessibilité dans System Center Configuration Manager](/sccm/core/understand/accessibility-features)

Pour obtenir des informations générales sur les produits et services d’accessibilité de Microsoft, consultez le [site web Accessibilité Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=9212).

## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Installer et configurer les extensions SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
