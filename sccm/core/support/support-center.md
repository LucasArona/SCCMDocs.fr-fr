---
title: Centre d’aide et de support
titleSuffix: Configuration Manager
description: Résoudre les problèmes des clients Configuration Manager avec le Centre d’aide et de support.
ms.date: 01/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c631197d-7daa-4faa-9e22-980cd6d604c2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5942f60ea15ad83f5debdf8dd3d53e72770744c6
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122863"
---
# <a name="support-center-for-configuration-manager"></a>Centre d’aide et de support pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357489--> À compter de la version 1810, utilisez le Centre d’aide et de support pour la résolution des problèmes clients, l’affichage des journaux en temps réel ou la capture de l’état d’un ordinateur client Configuration Manager pour l’analyser ultérieurement. Le Centre d’aide et de support est un outil unique permettant de consolider de nombreux outils administrateur de résolution des problèmes. 



## <a name="about"></a>À propos de 

Le Centre d’aide et de support a pour objectif de réduire les défis et la frustration lors du dépannage des ordinateurs clients Configuration Manager. Avant, lorsque vous utilisiez le support technique pour résoudre un problème lié aux clients Configuration Manager, vous deviez collecter manuellement les fichiers journaux et d’autres informations pour aider à résoudre le problème. Vous pouviez facilement oublier un fichier journal essentiel et compliquer ainsi grandement la tâche du service de support technique avec lequel vous étiez en contact.

Utilisez le Centre d’aide et de support pour simplifier l’expérience de support. Il vous permet de :

 - Créer un groupe de résolution des problèmes (fichier .zip) qui contient les fichiers journaux du client Configuration Manager. Vous disposez alors d’un fichier unique à envoyer au support.  

 - Voir les fichiers journaux, certificats, paramètres du Registre, vidages de débogage et stratégies clientes de Configuration Manager.  

 - Bénéficier d’un diagnostic en temps réel de l’inventaire (en remplacement de ContentSpy), de la stratégie (en remplacement de PolicySpy) et du cache client.  


### <a name="support-center-viewer"></a>Visionneuse du Centre d’aide et de support

Le Centre d’aide et de support inclut la visionneuse du Centre d’aide et de support, un outil que le personnel de support utilise pour ouvrir le groupe de fichiers que vous créez à l’aide du Centre d’aide et de support. Le collecteur de données du Centre d’aide et de support collecte et empaquète les journaux de diagnostic d’un client Configuration Manager local ou distant. Pour consulter les groupes du collecteur de données, utilisez la visionneuse.


### <a name="support-center-log-file-viewer"></a>Visionneuse des fichiers journaux du Centre d’aide et de support

Le Centre d’aide et de support inclut une visionneuse de journal moderne. Cet outil remplace CMTrace. OneTrace fournit une interface personnalisable avec prise en charge des fenêtres ancrables et des onglets. Il a une couche de présentation rapide et peut charger des fichiers journaux volumineux en quelques secondes.


### <a name="powershell-cmdlets"></a>Applets de commande PowerShell

Le Centre d’aide et de support contient également les [applets de commande Windows PowerShell](https://go.microsoft.com/fwlink/?linkid=397830). Utilisez ces applets de commande pour créer une connexion à distance à un autre client Configuration Manager, afin de configurer les options de collecte de données et de démarrer la collecte de données.



## <a name="prerequisites"></a>Prérequis

Installez les composants suivants sur l’ordinateur serveur ou client où vous voulez installer le Centre d’aide et de support :

- Une version de système d’exploitation prise en charge par Configuration Manager. Pour plus d’informations, consultez [Versions de système d’exploitation prises en charge pour les clients](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices). Le Centre d’aide et de support ne prend pas en charge les appareils mobiles.  

- .NET Framework 4.5.2 est requis sur l’ordinateur où vous exécutez le Centre d’aide et de support et ses composants.  



## <a name="install"></a>Installez

Recherchez le programme d’installation du Centre d’aide et de support sur le serveur de site à l’emplacement suivant : `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`.

Une fois que vous l’avez installé, recherchez les éléments suivants dans le menu Démarrer, dans le groupe **Microsoft System Center** :  
- Centre d’aide et de support (ConfigMgrSupportCenter.exe)  
- Visionneuse des fichiers journaux du Centre d’aide et de support (CMLogViewer.exe)  
- Visionneuse du Centre d’aide et de support (ConfigMgrSupportCenterViewer.exe)  



## <a name="known-issues"></a>Problèmes connus 

#### <a name="remote-connections-must-include-computer-name-or-domain-as-part-of-the-user-name"></a>Les connexions à distance doivent inclure le nom de l’ordinateur ou du domaine dans le nom de l’utilisateur.
Si vous vous connectez à un client distant à partir du Centre d’aide et de support, vous devez fournir le nom de la machine ou du domaine du compte d’utilisateur lors de l’établissement de la connexion. Si vous utilisez un nom d’ordinateur ou de domaine abrégé (tel que `.\administrator`), la connexion est établie, mais le Centre d’aide et de support ne collecte pas les données du client. 

Pour éviter ce problème, utilisez les formats de nom d’utilisateur suivants pour vous connecter à un client distant : 
- `ComputerName\UserName`  
- `DomainName\UserName`  

#### <a name="scripted-server-message-block-connections-to-remote-clients-might-require-removal"></a>Les connexions SMB (Server Message Block) scriptées aux clients distants devront éventuellement être supprimées
Lors d’une connexion à des clients distants à l’aide de l’applet de commande PowerShell [New-CMMachineConnection](https://go.microsoft.com/fwlink/p/?linkid=390542), le Centre d’aide et de support crée une connexion SMB (Server Message Block) avec chaque client distant. Il conserve ces connexions une fois la collecte de données terminée. Pour éviter de dépasser le nombre maximal de connexions à distance pour Windows, utilisez la commande `net use` pour voir l’ensemble des connexions à distance actives. Désactivez ensuite les connexions inutiles à l’aide de la commande suivante : `net use <connection_name> /d` 
où `<connection_name>` est le nom de la connexion à distance.

#### <a name="application-deployment-evaluation-cycle-request-isnt-sent-correctly-to-remote-machines"></a>La demande de cycle d’évaluation de déploiement d’application n’est pas transmise correctement aux ordinateurs à distance
<!--2849356--> Dans le Centre d’aide et de support, si vous sélectionnez **Évaluation du déploiement d’application** dans l’action **Appeler le déclencheur** de l’onglet **Contenu**, cette action démarre une tâche qui évalue les applications déployées. Si vous êtes connecté à un client local, elle évalue les déploiements d’application machine et utilisateur. Toutefois, si vous êtes connecté à un client à distance, elle évalue uniquement les déploiements d’application machine.


## <a name="next-steps"></a>Étapes suivantes

[Démarrage rapide du Centre d’aide et de support](/sccm/core/support/support-center-quickstart)
