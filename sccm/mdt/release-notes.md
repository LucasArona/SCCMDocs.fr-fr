---
title: Notes de publication de MDT
description: Découvrez les plateformes prises en charge, les prérequis et les limitations associés à Microsoft Deployment Toolkit.
ms.date: 06/04/2018
ms.prod: configuration-manager
ms.technology:
- configmgr-osd
ms.topic: article
ms.assetid: 6e32ce6d-585d-4801-a345-ff0f6f2d90ad
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7cb287a17322af8069708268a18d638bd04dddcf
ms.sourcegitcommit: 10b3a571e2a822bbd7b58a25840ee1e6f703a7a2
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/06/2018
ms.locfileid: "34814278"
---
# <a name="microsoft-deployment-toolkit-release-notes"></a>Notes de publication de Microsoft Deployment Toolkit  

Cet article fournit des informations détaillées sur la dernière version de Microsoft Deployment Toolkit (MDT). Ces informations incluent les plateformes prises en charge, les prérequis et les limitations associés à MDT. Cet article suppose que vous êtes familiarisé avec les concepts et les fonctionnalités de la version de MDT.



## <a name="latest-release"></a>Dernière version

**MDT build 8450** est la dernière version disponible sur le [Centre de téléchargement Microsoft](https://aka.ms/mdtdownload). 

Cette mise à jour prend en charge le Kit de déploiement et d’évaluation Windows (ADK) pour Windows 10, version 1709. 

***Mise à jour*** : à compter de mai 2018, cette build prendra également en charge Windows 10, version 1803.

Pour plus d’informations, consultez la section relative aux [plateformes prises en charge](#supported-platforms).


### <a name="significant-changes"></a>Modifications importantes
Voici un récapitulatif des modifications importantes contenues dans cette version à MDT.

#### <a name="supported-configuration-updates"></a>Mises à jour de configuration prises en charge
- Windows ADK pour Windows 10, version 1709
- Windows 10, version 1709
- Configuration Manager, version 1710

#### <a name="quality-updates"></a>Mises à jour qualité
Voici les titres des correctifs de bogues compris dans cette version :
- Les dépendances et la licence des applications Windows 10 chargées indépendamment ne sont pas installées
- La séquence de tâches CaptureOnly n’autorise pas la capture d’une image
- Une erreur s’affiche lors du démarrage d’une séquence de tâches MDT : valeur DeploymentType non valide. Impossible d’effectuer le déploiement
- ZTIMoveStateStore recherche le dossier de stockage des états au mauvais emplacement, ce qui rend son déplacement impossible
- Le code XML contient une erreur de frappe qui provoque un comportement indésirable
- L’installation des rôles et des fonctionnalités ne fonctionne pas pour la console de gestion IIS de Windows Server 2016
- Impossible de rechercher des images de système d’exploitation dans la séquence de tâches de mise à niveau si vous utilisez des dossiers
- L’outil MDT provisionne incorrectement le module TPM avec des fonctionnalités réduites. Pour plus d’informations, consultez [KB 4018657](https://support.microsoft.com/help/4018657/tpm-is-in-reduced-functionality-mode-after-successful-deployment-of-wi).
- Mises à jour de la logique de détection du type de châssis ZTIGather
- Une étape de la mise à niveau du système d’exploitation ignore SetupComplete.cmd, ce qui empêche les futurs déploiements.
- Problème de démarrage UEFI de Windows 10 ADK 1607 et versions ultérieures sur certains types de matériel
- Binaires de séquence de tâches Configuration Manager mis à jour



## <a name="supported-platforms"></a>Plateformes prises en charge

Les versions de MDT ne sont plus balisées avec l’année et la version de mise à jour. Pour mieux s’aligner sur les versions Current Branch de Windows 10 et de Configuration Manager, mais également pour des raisons marketing et pour simplifier le processus de publication, nous avons décidé de parler simplement de **Microsoft Deployment Toolkit**. Le numéro de build est utilisé pour distinguer chaque version. Par exemple, la dernière version disponible au téléchargement est 8450.

Contrairement à Configuration Manager et à sa planification prédéterminée des publications, les nouvelles versions de MDT ne sont publiées qu’au fur et à mesure des besoins, pour prendre en charge les nouvelles versions de Windows 10, de Windows ADK ou de Configuration Manager Current Branch. Les éventuels problèmes connus avec ces composants seront documentés dans cet article.

Les versions de système d’exploitation suivantes sont prises en charge pour le déploiement de MDT :
- Windows 10, version 1803
- Windows 10, version 1709
- Autres [versions prises en charge](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet) de Windows 10
- Windows 8.1
- Windows 7
- Windows Server 2016
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2



## <a name="prerequisites"></a>Prérequis

MDT nécessite les composants suivants, qui sont inclus dans Windows :
- Microsoft .NET Framework 4.0
- Windows PowerShell version 3.0

Utilisez la dernière version de [Windows ADK pour Windows 10](https://docs.microsoft.com/windows-hardware/get-started/adk-install). 

> [!Note]  
> Windows recommande d’utiliser le Windows ADK qui correspond à la version de Windows que vous déployez. Par exemple, utilisez le Windows ADK pour Windows 10 version 1703 quand vous déployez Windows 10 version 1703. Pour plus d’informations sur la prise en charge du composant Windows ADK, consultez [Plateformes prises en charge par DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms) et [Exigences de l’outil USMT](https://docs.microsoft.com/windows/deployment/usmt/usmt-requirements#bkmk-1).

Lors de l’intégration de MDT à Configuration Manager pour les scénarios ZTI et UDI, utilisez la dernière version de Configuration Manager Current Branch.



## <a name="upgrading-mdt"></a>Mise à niveau de MDT

Le processus d’installation de MDT supprime toutes les instances de MDT déjà installées sur l’ordinateur. Cependant, les partages de déploiement, les bases de données et les points de distribution existants sont conservés pendant ce processus. Lorsque l’installation est terminée, ceux-ci doivent être mis à niveau.

La version actuelle de MDT prend en charge la mise à niveau à partir des versions suivantes de MDT :
- MDT build 8443

> [!Tip]  
> Avant de tenter une mise à niveau, créez une sauvegarde de l’infrastructure existante de MDT.

### <a name="lti"></a>LTI
Après l’installation de MDT, vous devez mettre à niveau un partage de déploiement existant en exécutant l’Assistant **Open Deployment Share Wizard** (Ouverture du partage de déploiement)à partir du nœud Deployment Shares (Partages de déploiement) dans Deployment Workbench. Spécifiez le chemin du répertoire du partage de déploiement existant, puis cochez la case **Upgrade** (Mettre à niveau). Ce processus met également à niveau les partages de déploiement réseau et les partages de déploiement de médias existants, de manière à les rendre accessibles. N’effectuez pas cette mise à niveau pendant un déploiement, car les fichiers utilisés peuvent entraîner des problèmes de mise à niveau.

### <a name="zti"></a>ZTI
Les séquences de tâches MDT présentes dans Configuration Manager ne sont pas modifiées pendant le processus d’installation de MDT. Elles doivent continuer de fonctionner sans problème. Aucun mécanisme n’est fourni pour mettre à niveau ces séquences de tâches. Si vous souhaitez utiliser l’une des nouvelles fonctionnalités de MDT, créez de nouvelles séquences de tâches intégrées à MDT dans Configuration Manager.

Lorsque le processus de mise à niveau est terminé :  

- Après la mise à niveau, exécutez l’Assistant **Configure ConfigMgr Integration Wizard** (Configuration de l’intégration ConfigMgr). Celui-ci inscrit les nouveaux composants et installe les modèles de séquences de tâches ZTI mis à jour.  

- Créez un package **Microsoft Deployment Toolkit Files** (Fichiers Microsoft Deployment Toolkit) pour chaque nouvelle séquence de tâches ZTI que vous créez. Vous pouvez utiliser le package Microsoft Deployment Toolkit Files existant pour les séquences de tâches ZTI créées avant la mise à niveau. Toutefois, les nouvelles séquences de tâches ZTI nécessitent la création d’un nouveau package Microsoft Deployment Toolkit Files.



<!--
## Known issues
-->



## <a name="frequently-asked-questions"></a>Forum aux questions

#### <a name="whats-the-mdt-support-life-cycle"></a>Quel est le cycle de vie de prise en charge de MDT ?  
Pour plus d’informations, consultez [Cycle de vie de prise en charge Microsoft Deployment Toolkit](https://support.microsoft.com/help/2872000/microsoft-deployment-toolkit-support-life-cycle).

#### <a name="is-this-release-only-supported-with-windows-10-windows-adk-or-configuration-manager-version-x"></a>Cette version est-elle uniquement prise en charge par Windows 10, Windows ADK et Configuration Manager version *X* ?
Les tests que nous avons effectués pour cette version de MDT ont concerné principalement les configurations ci-dessus. Sauf en cas de problèmes connus explicites, il est très probable que l’outil fonctionne quand même avec les configurations autres que celles mentionnées plus haut. Notez toutefois que cela peut varier, car nous n’avons pas testé explicitement les autres combinaisons.

#### <a name="how-do-i-get-help-with-mdt"></a>Comment obtenir de l’aide pour MDT ?
Pour obtenir de l’aide avec MDT, utilisez l’une des méthodes suivantes (classées par ordre de priorité) :

1. Posez vos questions sur le [forum MDT](https://social.technet.microsoft.com/Forums/en/home?forum=mdt). Les MVP et autres membres de la Communauté répondent aux questions qui y sont posées. Il s’agit probablement du moyen le plus efficace d’obtenir de l’aide.
2. Contactez le support Microsoft. Faites une demande de support pour obtenir l’aide d’un professionnel.
3. Si vous pouvez reproduire systématiquement un même problème et pensez qu’il s’agit d’un bogue du produit, signalez-le nous via le [Hub de commentaires](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) Windows 10. L’équipe Produit étudie tous les problèmes qui lui sont signalés. Pour envoyer vos commentaires, utilisez la catégorie **Gestion d’entreprise** et la sous-catégorie **Déploiement du système d’exploitation**. Cette catégorisation permet de classer et de transmettre vos commentaires à l’équipe MDT.
     - Le Hub de commentaires permet également d’envoyer des suggestions (ou demandes de modification de la conception) concernant le produit.
     - Si vous avez déjà envoyé des commentaires via Connect, il est inutile de les renvoyer dans le Hub de commentaires.