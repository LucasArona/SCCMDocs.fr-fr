---
title: Créer un média autonome
titleSuffix: Configuration Manager
description: Utilisez un média autonome pour déployer le système d’exploitation sur un ordinateur sans connexion réseau.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a00da1511c6410088f318fc619bbddc537e20708
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083238"
---
# <a name="create-stand-alone-media"></a>Créer un média autonome

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, un média autonome contient tous les éléments requis pour déployer le système d’exploitation sur un ordinateur sans connexion réseau.

Utilisez un média autonome avec les scénarios de déploiement de système d’exploitation suivants :  

- [Actualiser un ordinateur existant avec une nouvelle version de Windows](/sccm/osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows)  

- [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [Effectuer une mise à niveau de Windows vers la dernière version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version)  


## <a name="usage"></a>Utilisation

Le média autonome inclut la séquence de tâches qui automatise les étapes d’installation du système d’exploitation, ainsi que tout autre contenu nécessaire. Ce contenu comprend l’image de démarrage, l’image de système d’exploitation et les pilotes de périphériques. Étant donné que le média autonome stocke tous les éléments nécessaires pour déployer le système d’exploitation, il exige davantage d’espace disque que d’autres types de médias.

Quand vous créez un média autonome sur un site d’administration centrale, le client récupère le code de site qui lui est attribué à partir d’Active Directory. Le média autonome créé sur les sites enfants attribue automatiquement au client le code de site pour ce site.  


## <a name="prerequisites"></a>Prérequis

Avant de créer un média autonome avec l’Assistant Création d’un média de séquence de tâches, vérifiez que toutes ces conditions sont remplies.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Créer une séquence de tâches pour déployer un système d’exploitation

Dans le cadre du média autonome, spécifiez la séquence de tâches permettant de déployer un système d’exploitation. Pour plus d’informations, voir [Créer une séquence de tâches pour installer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

#### <a name="unsupported-actions-for-stand-alone-media"></a>Actions non prises en charge pour les médias autonomes

Les actions suivantes ne sont pas prises en charge pour les médias autonomes :

- Étape [Appliquer automatiquement les pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_AutoApplyDrivers) dans la séquence de tâches. Le média autonome ne prend pas en charge l’application automatique de pilotes de périphériques à partir du catalogue de pilotes. Utilisez l’étape [Appliquer le package de pilotes](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyDriverPackage) afin de rendre un ensemble de pilotes spécifique accessible au programme d’installation de Windows.  

- Étape [Télécharger le contenu du package](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) dans la séquence de tâches. Les informations de point de gestion ne sont pas disponibles sur un média autonome. Par conséquent, l’étape ne parvient pas à énumérer les emplacements de contenu.  

- Installation de mises à jour logicielles.  

- Installation du logiciel avant le déploiement du système d’exploitation.  

- Séquences de tâches personnalisées pour les déploiements hors déploiements de système d’exploitation.  

- Association d'utilisateurs à l'ordinateur de destination pour prendre en charge l'affinité entre appareil et utilisateur.  

- Installation de packages dynamiques à l’étape [Installer les packages](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage).  

- Installation de packages dynamiques à l’étape [Installer l’application](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication).

- Paramètre **Utiliser le package client de préproduction si disponible** de l’étape de séquence de tâches **Configurer Windows et ConfigMgr**. Pour plus d’informations sur ce paramètre, consultez [Configurer Windows et ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).  

> [!NOTE]  
> Une erreur peut se produire si votre séquence de tâches comprend l’étape [Installer le package](/sccm/osd/understand/task-sequence-steps#BKMK_InstallPackage) et que vous créez le média autonome sur un site d’administration centrale. Le site d’administration centrale ne dispose pas des stratégies de configuration de client nécessaires. Ces stratégies sont obligatoires pour activer l’agent de distribution de logiciels pendant l’exécution de la séquence de tâches. L’erreur suivante est susceptible d’apparaître dans le fichier **CreateTsMedia.log** :  
>
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`
>
> Pour un média autonome qui inclut une étape **Installer le package**, créez le média autonome sur un site principal où l’agent de distribution logicielle est activé.
>
> Vous pouvez également utiliser une étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) personnalisée. Ajoutez-la après l’étape [Configurer Windows et ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr) et avant la première étape **Installer le package**. L’étape **Exécuter la ligne de commande** exécute la commande WMIC suivante pour activer l’agent de distribution logicielle avant la première étape Installer le package :  
>
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuer tout le contenu associé à la séquence de tâches

Distribuez auprès d’au moins un point de distribution tout le contenu exigé par la séquence de tâches, à savoir l’image de démarrage, l’image de système d’exploitation et les autres fichiers associés. L’Assistant collecte le contenu sur le point de distribution quand il crée le média.

Votre compte d’utilisateur doit au moins disposer de droits d’accès en **Lecture** à la bibliothèque de contenu de ce point de distribution. Pour plus d’informations, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Préparer le lecteur USB amovible

Si vous utilisez un lecteur USB amovible, branchez-le à l’ordinateur sur lequel s’exécute l’Assistant Création d’un média de séquence de tâches. Il doit être détectable comme appareil amovible par Windows. L’Assistant écrit directement sur le lecteur USB quand il crée le média.

Le média autonome utilise un système de fichiers FAT32. Il n’est pas possible de créer un média autonome sur un lecteur USB amovible contenant un fichier d’une taille supérieure à 4 Go.

### <a name="create-an-output-folder"></a>Créer un dossier de sortie

Avant d’exécuter l’Assistant Création d’un média de séquence de tâches afin de créer un média pour un ensemble de CD ou de DVD, créez un dossier pour les fichiers de sortie créés. Le média créé pour un ensemble de CD ou de DVD est directement écrit sous forme de fichier .ISO dans le dossier.


## <a name="process"></a>Processus

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Créer un média de séquence de tâches** dans le groupe **Créer** pour lancer l’Assistant Création d’un média de séquence de tâches.  

3. Sur la page **Sélectionner le type de média**, spécifiez les options suivantes :  

    - Sélectionnez **Média autonome**.  

    - Si vous souhaitez autoriser seulement le déploiement du système d’exploitation sans intervention de l’utilisateur, sélectionnez **Autoriser le déploiement sans assistance du système d’exploitation**.  

        > [!IMPORTANT]  
        > Avec cette option, l’utilisateur n’est pas invité à fournir des informations sur la configuration réseau ou des séquences de tâches facultatives. Si le média est configuré avec une protection par mot de passe, l’utilisateur est quand même invité à entrer un mot de passe.  

4. Sur la page **Type de média**, spécifiez s’il s’agit d’un **Lecteur USB amovible** ou d’un **Ensemble de CD/DVD**. Ensuite, configurez les options suivantes :  

    > [!IMPORTANT]  
    > Le média utilise un système de fichiers FAT32. Il n’est pas possible de créer un média sur un lecteur USB contenant un fichier d’une taille supérieure à 4 Go.  

    - Si vous sélectionnez **Lecteur USB amovible**, choisissez le lecteur sur lequel le contenu sera stocké.  

        - **Formater le lecteur USB amovible (FAT32) et le rendre démarrable** : par défaut, laisser Configuration Manager préparer le lecteur USB. De nombreux appareils UEFI récents nécessitent une partition FAT32 amorçable. Toutefois, ce format limite également la taille des fichiers et la capacité globale du lecteur. Si vous avez déjà formaté et configuré le lecteur amovible, désactivez cette option.

    - Si vous sélectionnez **Ensemble de CD/DVD**, spécifiez la capacité du média (**Taille du média**) et le nom et le chemin d’accès du fichier de sortie (**Fichier de média**). L'Assistant écrit les fichiers de sortie à cet emplacement. Exemple : `\\servername\folder\outputfile.iso`  

        Si la capacité du média est insuffisante pour stocker l’ensemble du contenu, il crée plusieurs fichiers. Il vous faut alors stocker le contenu sur plusieurs CD ou DVD. Quand plusieurs fichiers de média sont nécessaires, Configuration Manager ajoute un numéro de séquence au nom de chaque fichier de sortie qu’il crée.  

        Si vous déployez une application en même temps que le système d’exploitation et que cette application ne peut pas tenir sur un seul média, Configuration Manager la stocke sur plusieurs médias. Quand le média autonome est exécuté, Configuration Manager invite l’utilisateur à insérer le média suivant sur lequel l’application est stockée.  

        > [!IMPORTANT]  
        > Si vous sélectionnez une image .iso existante, l'Assistant Média de séquence de tâches supprime cette image du lecteur ou du partage dès lors que vous passez à la page suivante de l'Assistant. L'image existante est supprimée même si vous annulez ensuite l'Assistant.  

    - **Dossier intermédiaire**<!--1359388-->: le processus de création de média est susceptible de prendre beaucoup d’espace lecteur temporaire. Par défaut, cet emplacement est semblable au suivant : `%UserProfile%\AppData\Local\Temp`. À compter de la version 1902, remplacez cette valeur par un autre lecteur et un autre chemin d’accès pour choisir où stocker ces fichiers temporaires.  

    - **Étiquette du média**<!--1359388-->: à compter de la version 1902, ajoutez une étiquette au média de séquence de tâches. Cette étiquette vous permet de mieux identifier le média une fois celui-ci créé. La valeur par défaut est `Configuration Manager`. Ce champ de texte s’affiche dans les emplacements suivants :  

        - Si vous montez un fichier ISO, Windows utilise cette étiquette pour nommer le lecteur monté.  

        - Si vous formatez un lecteur USB, les 11 premiers caractères de l’étiquette sont utilisés pour former son nom.  

        - Configuration Manager écrit un fichier texte appelé `MediaLabel.txt` à la racine du média. Par défaut, le fichier comprend une seule ligne de texte : `label=Configuration Manager`. Si vous personnalisez l’étiquette du média, cette ligne utilise votre étiquette personnalisée à la place de la valeur par défaut.  

    - **Inclure le fichier autorun.inf sur le média**<!-- 4090666 -->: à compter de la version 1902, Configuration Manager n’ajoute pas par défaut de fichier autorun.inf. Ce fichier est généralement bloqué par les produits anti-programme malveillant. Pour plus d’informations sur la fonctionnalité d’exécution automatique (AutoRun) de Windows, consultez [Création d’une application sur CD-ROM prenant en charge l’exécution automatique](https://docs.microsoft.com/windows/desktop/shell/autoplay). Si elle reste nécessaire dans votre scénario, sélectionnez cette option pour inclure le fichier.  

5. Sur la page **Sécurité**, spécifiez les options suivantes :

    - **Protéger le média par un mot de passe** : entrez un mot de passe fort pour mieux protéger le média contre les accès non autorisés. Si un mot de passe est spécifié, l’utilisateur doit le fournir pour pouvoir utiliser le média.  

        > [!IMPORTANT]  
        > Pour des raisons de sécurité, il est recommandé d’attribuer systématiquement un mot de passe afin de protéger le média.  
        >
        > Sur un média autonome, seules les étapes de la séquence de tâches et leurs variables sont chiffrées, et non le contenu restant du média. N’ajoutez pas d’informations sensibles dans les scripts de séquence de tâches. Stockez et mettez en œuvre toutes les informations sensibles en utilisant des variables de séquence de tâches.  

    - **Sélectionner une plage de dates pour que ce média autonome soit valide** : définissez une date de début et une date d’expiration facultatives sur le média. Ce paramètre est désactivé par défaut. Les dates sont comparées à l’heure système de l’ordinateur avant l’exécution du support autonome. Si l’heure du système est antérieure à l’heure de début ou ultérieure à l’heure d’expiration, le média autonome ne démarre pas. Ces options sont également disponibles avec la cmdlet PowerShell [New-CMStandaloneMedia](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmstandalonemedia?view=sccm-ps).  

6. Sur la page **CD/DVD autonome**, sélectionnez la séquence de tâches qui déploie le système d’exploitation. Il n’est possible de sélectionner que les séquences de tâches associées à une image de démarrage. Vérifiez la liste de contenu associée à la séquence de tâches.  

    - **Détecter les dépendances d’applications associées et les ajouter à ce média** : ajoutez également du contenu au média pour les dépendances d’applications.  

        > [!TIP]  
        > Si les dépendances d’applications attendues n’apparaissent pas, désélectionnez, puis resélectionnez cette option pour actualiser la liste.  

7. Sur la page **Sélectionner des applications**, spécifiez le contenu d’applications supplémentaires à inclure dans le fichier de média.  

8. Sur la page **Sélectionner des packages**, spécifiez le contenu de packages supplémentaires à inclure dans le fichier de média.  

9. Sur la page **Sélectionner des packages de pilotes**, spécifiez le contenu de packages de pilotes supplémentaires à inclure dans le fichier de média.  

10. Sur la page **Points de distribution**, spécifiez les points de distribution comportant le contenu requis.  

    Configuration Manager n’affiche que les points de distribution qui disposent du contenu. Distribuez tout le contenu associé à la séquence de tâches sur au moins un point de distribution avant de continuer. Après avoir distribué le contenu, actualisez la liste des points de distribution. Supprimez les points de distribution que vous avez déjà sélectionnés dans cette page, accédez à la page précédente, puis revenez à la page **Points de Distribution**. Vous pouvez également redémarrer l’Assistant. Pour plus d’informations, consultez [Distribuer du contenu référencé par une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DistributeTS) et [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

11. Sur la page **Personnalisation**, spécifiez les options suivantes :  

    - Ajoutez toutes les variables utilisées par la séquence de tâches.  

    - **Activer les commandes de prédémarrage** : spécifiez les commandes de prédémarrage à exécuter avant l’exécution de la séquence de tâches. Il s’agit d’un script ou d’un exécutable capable d’interagir avec l’utilisateur dans Windows PE avant que la séquence de tâches ne commence. Pour plus d’informations, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](/sccm/osd/understand/prestart-commands-for-task-sequence-media).  

        > [!TIP]  
        > Lors de la création du média, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des éventuelles variables de la séquence de tâches, dans le fichier **CreateTSMedia.log** sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

        Si certains contenus sont nécessaires à la commande de prédémarrage, sélectionnez l’option **Inclure les fichiers de la commande de prédémarrage**.  

12. Effectuez toutes les étapes de l'Assistant.  

Les fichiers de média autonome (.ISO) sont créés dans le dossier de destination. Si vous avez sélectionné **Ensemble de CD/DVD**, copiez les fichiers de sortie sur un ensemble de CD ou de DVD.


## <a name="next-steps"></a>Étapes suivantes

[Utiliser un média autonome pour déployer Windows sans utiliser le réseau](/sccm/osd/deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network)
