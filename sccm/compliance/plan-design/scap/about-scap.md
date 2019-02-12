---
title: Extensions SCAP
titleSuffix: Configuration Manager
description: Découvrez les extensions SCAP (Security Content Automation Protocol) pour Configuration Manager.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a315489d-5e12-46d6-903e-3a35235b72c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e42027663f06bff715cb7e9087ececbc421cc495
ms.sourcegitcommit: 013ca76d5a3c07306de7b5bfd985b0289d1be599
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/31/2019
ms.locfileid: "55482450"
---
# <a name="about-the-security-content-automation-protocol-scap-extensions"></a>À propos des Extensions SCAP (Security Content Automation Protocol)

*S’applique à : System Center Configuration Manager (Current Branch)*

Les extensions SCAP pour Configuration Manager vous permettent d’analyser et d’évaluer votre environnement réseau pour la conformité avec le protocole SCAP (Security Content Automation Protocol). Le protocole SCAP est défini et géré par l’organisme NIST (National Institute of Standards and Technology). Pour plus d’informations, consultez [SCAP Project Overview](https://csrc.nist.gov/projects/security-content-automation-protocol) (Vue d’ensemble du projet SCAP).

> [!Note]  
> Cette version de l’outil est une fonctionnalité en préversion uniquement disponible dans la version 1806. Cette version n’est pas validée par NIST. <!--SCCMDocs-pr issue 3323-->
> 
> Si vous avez besoin d’un outil certifié, ou si vous utilisez une autre version de Configuration Manager Current Branch, utilisez la version suivante des extensions SCAP :
> - [Télécharger des extensions SCAP pour System Center Configuration Manager](https://www.microsoft.com/download/details.aspx?id=48741)
> - [Documentation des extensions SCAP version 3.0](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/mt228311\(v%3dtechnet.10\))

Les extensions SCAP pour Configuration Manager utilisent la fonctionnalité de paramètres de conformité pour analyser les ordinateurs de votre environnement dans un premier temps. Leur niveau de conformité à l’initiative USGCB (United States Government Configuration Baseline) fait ensuite l’objet d’une description.

Les extensions permettent à Configuration Manager de consommer des flux de données SCAP, d’évaluer la compatibilité des systèmes et de générer des résultats de rapports au format SCAP. Votre organisation peut utiliser votre infrastructure Configuration Manager existante pour s’assurer que les ordinateurs que vous gérez répondent à cette exigence de conformité fédérale. Utilisez également Configuration Manager pour générer les rapports USGCB requis par les organismes NIST et OMB (Office of Management and Budget).

Cet article fournit des informations pour vous aider à installer, configurer et exécuter les extensions SCAP dans votre infrastructure Configuration Manager.



## <a name="whats-new"></a>Nouveautés

Cette version des extensions SCEP pour Configuration Manager inclut et prend en charge les fonctionnalités suivantes :  

- Une extension de console Configuration Manager, qui prend en charge la conversion du contenu SCAP en bases de référence de paramètres de conformité.  

- SCAP version 1.2, qui inclut les composants suivants :  

  - XCCDF (Extensible Configuration Checklist Description Format) version 1.2
  - OVAL (Open Vulnerability and Assessment Language), toutes les versions jusqu’à la version 5.10
  - Génération de rapports ARF (Asset Reporting Format) 1.1
  - CPE (Common Platform Enumeration) 2.3
  - CVE (Common Vulnerabilities and Exposures)
  - CCE (Common Configuration Enumeration) version 5
  - Internet Explorer 8 USGCB, Windows 7 USGCB et le Pare-feu Windows 7 USGCB  

- Compatibilité descendante avec les versions 1.1 et 1.0 de SCAP.  

- Assistant de console pour importer du contenu SCAP 1.2/1.1/1.0 et OVAL pour la conversion en bases de référence de configuration.  

  - Autorise la sélection de flux de données sources SCAP, ainsi que les points de référence et profils XCCDF pour la conversion.

- Assistant de console pour exporter des résultats d’évaluation de la configuration vers un rapport XML au format SCAP.  

  - Affiche le fichier source, le flux de données SCAP, le point de référence XCCDF et le profil XCCDF utilisés pour générer la base de référence.
  - Génère le rapport LASR (Cyberscope Lightweight Asset Summary Results).  

- Génère des rapports SCAP basés sur le déploiement de la base de référence de configuration. Ce composant inclut un nouveau tableau de bord pour visualiser la conformité des clients, ainsi que la conformité aux règles XCCDF. Le tableau de bord prend en charge l’extraction de rapports plus détaillés dans lesquels vous pouvez effectuer des recherches et sur lesquels vous pouvez appliquer des filtres.  

- Amélioration des performances de plusieurs types d’éléments de configuration convertis à partir de tests OVAL, ce qui permet une évaluation plus rapide.  

- Résout plusieurs problèmes survenus dans du contenu Windows 10 DISA v1r3.  



## <a name="terms"></a>Terminologie

- **ID OVAL** : Identificateur d’une définition OVAL spécifique qui est conforme au format des ID OVAL.  

- **Flux de données de résultat SCAP** : Bundle de composants SCAP, ainsi que les mappages de références entre des composants SCAP, qui contiennent un contenu de sortie (résultat).  

- **Flux de données de sources SCAP** : Bundle de composants SCAP, ainsi que les mappages de références entre des composants SCAP, qui contiennent un contenu d’entrée (source).



## <a name="deployment-process"></a>Processus de déploiement

Voici un récapitulatif du processus de déploiement global :  

- [Préparer l’infrastructure](#bkmk_prepare) pour utiliser les extensions  

- [Installer et configurer les extensions SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_install) pour Configuration Manager  

- [Télécharger et installer les fichiers de flux de données SCAP](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_scap-data-stream-files) à partir du site de l’organisme NIST  

- Convertir et importer les fichiers de flux de données SCAP dans une base de référence de paramètres de conformité Configuration Manager. Utilisez l’une des deux méthodes suivantes :   

    - [Processus manuel](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) au moyen de l’Assistant d’importation dans la console Configuration Manager  

    - [Processus automatisé](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_auto-convert-and-import) avec l’outil en ligne de commande Microsoft.Sces.ScapToDcm.exe  

- [Déployer](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_deploy) les bases de référence de configuration sur des regroupements  

- [Surveiller](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_monitor) les données de conformité  

- Exporter les résultats de conformité au format SCAP à l’aide d’une des deux méthodes suivantes :  

    - [Processus manuel](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_export) au moyen de l’Assistant d’exportation dans la console  

    - [Processus automatisé](/sccm/compliance/plan-design/scap/deploy-monitor-export#bkmk_auto-export) à l’aide de l’outil en ligne de commande Microsoft.Sces.DcmToScap.exe  



## <a name="bkmk_prepare"></a> Préparer l’infrastructure

### <a name="software-requirements"></a>Configuration logicielle requise

Pour installer, configurer et exécuter les extensions SCAP pour Center Configuration Manager, vous devez disposer d’un ordinateur avec les logiciels suivants :

- Une [version prise en charge](/sccm/core/servers/manage/current-branch-versions-supported) de la console Configuration Manager Current Branch.  

- Une version de système d’exploitation compatible avec la console Configuration Manager. Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les consoles Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).  

En plus de l’ordinateur exécutant les extensions SCAP, vous devez disposer des éléments suivants :

- Une infrastructure Configuration Manager Current Branch. Pour plus d’informations sur la configuration requise d’un déploiement de Configuration Manager, consultez l’article [Configurations prises en charge pour Configuration Manager](/sccm/core/plan-design/configs/supported-configurations).  

Les ordinateurs dont vous voulez évaluer la conformité SCAP doivent disposer des logiciels et configurations suivants :

- Client Configuration Manager.  

- Windows PowerShell 2.0 ou supérieur.  

- La stratégie d’exécution PowerShell de Configuration Manager définie avec la valeur **Ignorer**. Pour plus d’informations, consultez l’article [Stratégie d’exécution PowerShell](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

- L'un des systèmes d'exploitation suivants :  
  - Windows 7 SP1, 32 bits ou 64 bits
  - Windows 10, 32 bits ou 64 bits
  - Windows Server 2012 R2

### <a name="hardware-requirements"></a>Configuration matérielle requise

Pour plus d’informations sur la configuration minimale requise pour Configuration Manager, consultez [Planification des configurations matérielles pour Configuration Manager](/sccm/core/plan-design/configs/recommended-hardware).



## <a name="accessibility-features"></a>Fonctionnalités d'accessibilité

Les extensions SCAP pour Configuration Manager incluent des outils en ligne de commande Windows. Ces outils peuvent tirer parti des fonctionnalités et outils d’accessibilité dans Windows.

- Les paramètres de ligne de commande sont décrits pour Microsoft.Sces.ScapToDcm.exe et Microsoft.Sces.DcmToScap.exe. Pour plus d’informations, consultez [Paramètres de ligne de commande Microsoft.Sces.ScapToDcm.exe. ](/sccm/compliance/plan-design/scap/install-configure-scap#microsoftscesscaptodcmexe-command-line-parameters) et [Paramètres de ligne de commande Microsoft.Sces.DcmToScap.exe](/sccm/compliance/plan-design/scap/import-scap-compliance-settings#microsoftscesdcmtoscapexe-command-line-parameters).  

- Les paramètres de ligne de commande `-help` et `-?` de chaque outil affichent des informations sur son utilisation. Ces détails d’utilisation sont ensuite disponibles pour les lecteurs d’écran et autres technologies d’assistance.  

- Pour plus d’informations, consultez [Accessibilité Windows](http://windows.microsoft.com/windows/help/accessibility).

Les extensions SCAP exploitent également les fonctionnalités d’accessibilité dans Configuration Manager. Pour plus d’informations, consultez [Fonctionnalités d’accessibilité dans Configuration Manager](/sccm/core/understand/accessibility-features).

Pour plus d’informations sur les produits et services d’accessibilité de Microsoft, consultez le [site web Accessibilité Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=9212).



## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Installer et configurer des extensions SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)
