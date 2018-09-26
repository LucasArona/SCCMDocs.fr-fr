---
title: Créer une séquence de tâches de mise à niveau du système d’exploitation
titleSuffix: Configuration Manager
description: Utiliser une séquence de tâches automatiquement mise à niveau à partir de Windows 7 ou ultérieur vers Windows 10
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bddcd356a3ee221d5b67935a5be91bbe89d2afc2
ms.sourcegitcommit: be8c0182db9ef55a948269fcbad7c0f34fd871eb
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/23/2018
ms.locfileid: "42756052"
---
# <a name="create-a-task-sequence-to-upgrade-an-os-in-configuration-manager"></a>Créer une séquence de tâches pour mettre à niveau un système d’exploitation dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, utilisez des séquences de tâches pour automatiquement mettre à niveau un système d’exploitation sur un ordinateur de destination. Cette mise à niveau peut être effectuée à partir de Windows 7 ou une version ultérieure vers Windows 10, ou à partir de Windows Server 2012 ou une version ultérieure vers Windows Server 2016. Créez une séquence de tâches qui référence le package de mise à niveau du système d’exploitation et tout autre contenu à installer, comme des applications ou des mises à jour logicielles. La séquence de tâches de mise à niveau d’un système d’exploitation fait partie intégrante du scénario [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md).  



## <a name="prerequisites"></a>Prérequis

Avant de créer la séquence de tâches, vous devez vous assurer que les conditions requises suivantes sont remplies :    

#### <a name="required"></a>Obligatoire  

- Le [package de mise à niveau du système d’exploitation](/sccm/osd/get-started/manage-operating-system-upgrade-packages) doit être disponible dans la console Configuration Manager.  

- Lors d’une mise à niveau vers Windows Server 2016, sélectionnez le paramètre **Ignorer les messages de compatibilité révocables** au cours de l’étape de la séquence de tâches Mettre à niveau le système d’exploitation. Sinon, la mise à niveau échoue.  

#### <a name="required-if-used"></a>Obligatoire (si utilisé)  

-   Les [mises à jour logicielles](/sccm/sum/get-started/synchronize-software-updates) doivent être synchronisées dans la console Configuration Manager.  

-   Les [applications](/sccm/apps/deploy-use/create-applications) doivent être ajoutées à la console Configuration Manager.  



##  <a name="BKMK_UpgradeOS"></a> Créer une séquence de tâches pour mettre à niveau un système d’exploitation  

Pour mettre à niveau le système d’exploitation sur des clients, créez une séquence de tâches et sélectionnez **Mettre à niveau un système d’exploitation à partir du package de mise à niveau** dans l’Assistant Création d’une séquence de tâches. L’Assistant ajoute les étapes de la séquence de tâches permettant de mettre à niveau le système d’exploitation, d’appliquer des mises à jour logicielles et d’installer des applications. 

#### <a name="to-create-a-task-sequence-that-upgrades-an-os"></a>Pour créer une séquence de tâches qui met à niveau un système d’exploitation  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis cliquez sur **Séquences de tâches**.  

2.  Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, cliquez sur **Créer une séquence de tâches**.  

3.  Dans la page **Créer une séquence de tâches** de l’Assistant Création d’une séquence de tâches, sélectionnez **Mettre à niveau un système d’exploitation à partir du package de mise à niveau**, puis cliquez sur **Suivant**.  

4.  Dans la page **Informations sur la séquence de tâches**, spécifiez les paramètres suivants et cliquez sur **Suivant** :  

    -   **Nom de la séquence de tâches**: spécifiez un nom qui identifie la séquence de tâches.  

    -   **Description** : si vous le souhaitez, ajoutez une description.  

5.  Dans la page **Mettre à niveau le système d’exploitation Windows**, spécifiez les paramètres suivants et cliquez sur **Suivant** :  

    -   **Package de mise à niveau** : spécifiez le package de mise à niveau qui contient les fichiers sources de mise à niveau du système d’exploitation. Vérifiez que vous avez sélectionné le bon package de mise à niveau en examinant les informations contenues dans le volet **Propriétés**. Pour plus d’informations, consultez [Gérer les packages de mise à niveau de système d’exploitation](/sccm/osd/get-started/manage-operating-system-upgrade-packages).  

    -   **Index d’édition** : si plusieurs index d’édition de système d’exploitation sont disponibles dans le package, sélectionnez l’index d’édition souhaité. Par défaut, l’Assistant sélectionne le premier index.  

    -   **Clé de produit** : spécifiez la clé de produit Windows du système d’exploitation à installer. Spécifiez des clés de licence en volume codées ou des clés de produit standard. Si vous utilisez une clé de produit standard, séparez chaque groupe de cinq caractères par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quand la mise à niveau concerne une édition de licence en volume, la clé de produit n’est pas toujours requise.  

        > [!Note]  
        > Cette clé de produit peut être une clé d’activation multiple (MAK) ou une clé de licence en volume générique (GVLK). La clé GVLK est aussi connue sous le nom de clé d’installation de client de service de gestion de clés (KMS). Pour plus d’informations, consultez [Planifier l’activation en volume](https://docs.microsoft.com/windows/deployment/volume-activation/plan-for-volume-activation-client). Pour obtenir la liste des clés d’installation de client KMS, consultez [l’Annexe A](https://docs.microsoft.com/windows-server/get-started/kmsclientkeys) du guide d’activation de Windows Server. 

    -   **Ignore any dismissable compatibility messages** (Ignorer les messages de compatibilité révocables) : sélectionnez ce paramètre si vous effectuez la mise à niveau vers Windows Server 2016. Si vous ne sélectionnez pas ce paramètre, l’exécution de la séquence de tâches échoue, car le programme d’installation de Windows attend que l’utilisateur clique sur **Confirmer** dans la boîte de dialogue de compatibilité d’une application Windows.   

7.  Dans la page **Inclure les mises à jour**, spécifiez s’il faut installer toutes les mises à jour logicielles, seulement celles qui sont obligatoires ou aucune. Cliquez ensuite sur **Suivant**. Si vous spécifiez l’installation des mises à jour logicielles, Configuration Manager installe uniquement les mises à jour ciblant les regroupements dont l’ordinateur de destination est membre.  

8.  Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous sélectionnez plusieurs applications, indiquez également si la séquence de tâches doit continuer à s’exécuter en cas d’échec de l’installation d’une des applications.  

9. Effectuez toutes les étapes de l'Assistant.  


> [!Important]  
> Lorsque la séquence de tâches s’exécute sur un appareil, le client Configuration Manager crée plusieurs scripts qui contrôlent le comportement de la séquence de tâches dans différents scénarios. À la fin de la séquence de tâches, le client ne supprime pas ces scripts tant que l’ordinateur n’a pas redémarré. Ces fichiers de script ne contiennent pas d’informations sensibles.  


À partir de la version 1802, le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend des groupes supplémentaires, avec des actions recommandées à ajouter avant ou après le processus de mise à niveau. Ces actions sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils sur Windows 10. Pour plus d’informations, consultez les étapes de séquence de tâches recommandées [pour préparer la mise à niveau](#recommended-task-sequence-steps-to-prepare-for-upgrade) et pour le [post-traitement](#recommended-task-sequence-steps-for-post-processing).

À partir de la version 1806, ce modèle de séquence de tâches comprend aussi un groupe avec des actions qu’il est recommandé d’ajouter en cas d’échec de la mise à niveau. Ces actions facilitent la résolution des problèmes. Pour plus d’informations, consultez [Étapes de séquence de tâches recommandées en cas d’échec](#recommended-task-sequence-steps-on-failure).<!--1358500-->  



## <a name="configure-pre-cache-content"></a>Configurer la mise en cache préalable du contenu
<!--1021244--> La fonctionnalité de mise en cache préalable pour les déploiements disponibles de séquences de tâches permet aux clients de télécharger le contenu de package de mise à niveau de système d’exploitation approprié avant l’installation de la séquence de tâches par l’utilisateur.  

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Par exemple, vous voulez une seule séquence de tâches de mise à niveau sur place pour tous les utilisateurs, et vous avez plusieurs architectures et langues. Dans les versions précédentes, le téléchargement du contenu commence quand l’utilisateur installe un déploiement de séquences de tâches disponible à partir du Centre logiciel. Ce délai a pour effet de retarder la disponibilité de l’installation. Tout le contenu référencé dans la séquence de tâches est téléchargé. Ce contenu comprend tous les packages de mise à niveau du système d’exploitation pour chaque langue et chaque architecture. Si chaque package de mise à niveau fait environ 3 Go, le contenu total est très volumineux.

La mise en cache préalable du contenu vous permet de laisser le client télécharger uniquement le package de mise à niveau de système d’exploitation applicable et tout le contenu référencé supplémentaire dès qu’il reçoit le déploiement. Lorsque l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est prêt. L’installation démarre rapidement, du fait que le contenu se trouve sur le disque dur local.

> [!NOTE]  
> Actuellement, ce comportement s’applique uniquement au package de mise à niveau de système d’exploitation. Ce package est le seul contenu pour lequel vous spécifiez l’architecture ou la langue correspondante. Par exemple, si la séquence de tâches référence également plusieurs packages de pilotes, le client les télécharge tous. Le moteur de séquence de tâches évalue les conditions à chaque étape pendant l’exécution de la séquence de tâches, et non à l’avance. Le client utilise les balises sur les propriétés de package pour déterminer le contenu à mettre en cache préalablement.


### <a name="to-configure-the-pre-cache-feature"></a>Pour configurer la fonctionnalité de mise en cache préalable

1. Créez des packages de mise à niveau de système d’exploitation pour des architectures et des langues spécifiques. Spécifiez l’architecture et la langue sous l’onglet **Source de données** du package. Pour la langue, utilisez la conversion décimale. Par exemple, **1033** est la valeur décimale pour l’anglais et **0x0409** est son équivalent hexadécimal.  

    Le client évalue les valeurs d’architecture et de langue pour déterminer le package de mise à niveau de système d’exploitation qu’il télécharge pendant la mise en cache préalable.  

2. Créez une séquence de tâches avec des étapes conditionnelles pour les différentes langues et architectures. Par exemple, l’étape suivante utilise la version anglaise :  

    ![Éditeur de séquence de tâches montrant plusieurs étapes de mise à niveau de système d’exploitation pour ENU, DEU et JPN](../media/precacheproperties2.png)

    ![Éditeur de séquence de tâches, onglet Options, affichant la requête WQL WMI pour les paramètres régionaux et l’architecture de système d’exploitation](../media/precacheoptions2.png)  

3. déployer la séquence de tâches. Pour configurer la fonctionnalité de mise en cache préalable, configurez les paramètres suivants :  

    - Sous l’onglet **Général**, sélectionnez **Prétélécharger le contenu pour cette séquence de tâches**.  

    - Sous l’onglet **Paramètres de déploiement**, configurez la séquence de tâches comme **Disponible**.  

    - Sous l’onglet **Planification**, choisissez l’heure actuellement sélectionnée pour le paramètre **Planifier la disponibilité de ce déploiement**. Le client commence à préalablement mettre en cache le contenu pendant le temps de mise à disposition du déploiement. Quand un client ciblé reçoit cette stratégie, le temps de mise à disposition est passé. Par conséquent, le téléchargement de la mise en cache préalable commence immédiatement. Si le client reçoit cette stratégie, mais que le temps de mise à disposition se situe dans le futur, le client commence la mise en cache du contenu uniquement au début du temps de mise à disposition.  

    - Sous l’onglet **Points de distribution**, configurez les paramètres **Options de déploiement**. Si le contenu n’a pas été préalablement mis en cache au moment du démarrage de l’installation par l’utilisateur, le client utilise ces paramètres.  
  

### <a name="user-experience"></a>Expérience utilisateur

- Quand le client reçoit la stratégie de déploiement, il commence la mise en cache préalable du contenu après le temps de mise à disposition du déploiement. Ce contenu comprend tous les packages référencés, mais uniquement le package de mise à niveau de système d’exploitation qui correspond aux attributs d’architecture et de langue du package.  

- Quand le client met le déploiement à la disposition des utilisateurs, une notification s’affiche pour les informer du nouveau déploiement. La séquence de tâches est alors visible dans le Centre logiciel. L’utilisateur peut accéder au Centre logiciel et cliquer sur **Installer** pour démarrer l’installation.  

- Si le client n’a pas préalablement mis en cache le contenu quand l’utilisateur installe la séquence de tâches, il utilise les paramètres spécifiés sous l’onglet **Option de déploiement** du déploiement.  



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Étapes de séquence de tâches recommandées pour préparer la mise à niveau

À partir de la version 1802, le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend des groupes supplémentaires, avec des actions recommandées à ajouter avant le processus de mise à niveau. Ces actions du groupe **Préparer la mise à niveau** sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils vers Windows 10. Pour les sites sur les versions antérieures à 1802, ajoutez manuellement ces actions à votre séquence de tâches dans le groupe **Préparer la mise à niveau**.  

- **Vérification de la batterie** : ajoutez des étapes dans ce groupe pour contrôler si l’ordinateur est sur batterie ou sur secteur. Cette action doit être effectuée par un utilitaire ou un script personnalisé.  

- **Vérification de la connexion réseau/câblée** : ajoutez des étapes dans ce groupe pour contrôler si l’ordinateur est connecté à un réseau et n’utilise pas de connexion sans fil. Cette action doit être effectuée par un utilitaire ou un script personnalisé.  

- **Supprimer les applications incompatibles** : ajoutez des étapes dans ce groupe pour supprimer toutes les applications incompatibles avec cette version de Windows 10. Il existe différentes façons de désinstaller une application selon les cas.  

    - Si l’application utilise Windows Installer, copiez la ligne de commande **Programme de désinstallation** de l’onglet **Programmes** dans les propriétés de type de déploiement de Windows Installer de l’application. Ensuite, ajoutez dans ce groupe une étape **Exécuter la ligne de commande** comportant la ligne de commande du programme de désinstallation. Par exemple : </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br>  

- **Supprimer les pilotes incompatibles** : ajoutez des étapes dans ce groupe pour supprimer tous les pilotes incompatibles avec cette version de Windows 10.  

- **Supprimer/suspendre la sécurité tierce** : ajoutez des étapes dans ce groupe pour supprimer ou suspendre des programmes de sécurité tiers, par exemple, des antivirus.  

   - Si vous utilisez un programme de chiffrement de disque tiers, indiquez son pilote de chiffrement à l’installation de Windows avec [l’option de ligne de commande](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#23) `/ReflectDrivers`. Ajoutez une étape [Définir une variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) à la séquence de tâches dans ce groupe. Affectez la valeur **OSDSetupAdditionalUpgradeOptions** à la variable de séquence de tâches. Définissez la valeur `/ReflectDrivers` avec le chemin du pilote. Cette [variable de séquence de tâches](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) ajoute la ligne de commande d’installation de Windows utilisée par la séquence de tâches. Contactez votre éditeur de logiciels pour obtenir de l’aide sur ce processus.  


### <a name="download-package-content-task-sequence-step"></a>Étape de séquence de tâches Télécharger le contenu du package  

Exécutez l’étape [Télécharger le contenu du package](/sccm/osd/understand/task-sequence-steps#BKMK_DownloadPackageContent) avant l’étape **Mettre à niveau le système d’exploitation** dans les scénarios suivants :  

-   Vous utilisez une seule séquence de tâches de mise à niveau pour les deux plateformes x86 et x64. Incluez deux étapes **Télécharger le contenu du package** dans le groupe **Préparer pour la mise à niveau**. Définissez des conditions sur chaque étape pour détecter l’architecture du client. Du fait de cette condition, l’étape télécharge uniquement le package de mise à niveau du système d’exploitation approprié. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable et utilisez cette variable pour le chemin du support à l’étape **Mettre à niveau le système d’exploitation** .  

-   Pour télécharger dynamiquement un package de pilotes applicable, utilisez deux étapes **Télécharger le contenu du package** avec des conditions pour détecter le type de matériel approprié pour chaque package de pilotes. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable. Utilisez ensuite cette variable comme valeur **Contenu intermédiaire** dans la section des pilotes sur l’étape **Mettre à niveau le système d’exploitation**.  

    > [!NOTE]  
    > Quand il y a plusieurs packages, Configuration Manager ajoute un suffixe numérique au nom de la variable. Par exemple, si vous spécifiez la variable personnalisée `%mycontent%`, le client stocke tout le contenu référencé à cet emplacement. Quand vous faites référence à la variable dans une étape ultérieure, comme **Mettre à niveau le système d’exploitation**, utilisez la variable avec un suffixe numérique. Dans cet exemple, utilisez `%mycontent01%` ou `%mycontent02%`, où le numéro correspond à l’ordre dans lequel l’étape **Télécharger le contenu du package** répertorie ce contenu spécifique.  



## <a name="recommended-task-sequence-steps-for-post-processing"></a>Étapes de séquence de tâches recommandées pour le post-traitement   

Une fois la séquence de tâches créée, ajoutez des étapes supplémentaires dans le groupe **Post-traitement** de la séquence de tâches.  

> [!NOTE]  
>  Cette séquence de tâches n’est pas linéaire. Des conditions sur les étapes peuvent affecter les résultats de la séquence de tâches. Ce comportement dépend du résultat de la mise à niveau de l’ordinateur client : si elle a été appliquée ou si la séquence de tâches a dû restaurer le système d’exploitation d’origine.  

À partir de la version 1802, le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend des groupes supplémentaires, avec des actions recommandées à ajouter après le processus de mise à niveau. Ces actions du groupe **Post-traitement** sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils vers Windows 10. Pour les sites sur les versions antérieures à 1802, ajoutez manuellement ces actions à votre séquence de tâches dans le groupe **Post-traitement**.  

- **Appliquer les pilotes basés sur le programme d’installation** : ajoutez des étapes dans ce groupe pour installer des pilotes basés sur le programme d’installation (.exe) à partir de packages.  

- **Installer/activer la sécurité tierce** : ajoutez des étapes dans ce groupe pour installer ou activer des programmes de sécurité tiers, par exemple, des antivirus.  

- **Définir les associations et applications Windows par défaut** : ajoutez des étapes dans ce groupe pour définir des associations de fichiers et des applications Windows par défaut. Tout d’abord, préparez un ordinateur de référence avec les associations d’applications de votre choix. Ensuite, exécutez la commande suivante pour exporter : </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Ajoutez le fichier XML à un package. Ensuite, ajoutez une étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) dans ce groupe. Indiquez le package contenant le fichier XML, puis spécifiez la ligne de commande suivante : </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> Pour plus d’informations, consultez la page [Exporter ou importer des associations d’applications par défaut](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).  

- **Appliquez les personnalisations** : ajoutez des étapes dans ce groupe pour appliquer des personnalisations du menu Démarrer, par exemple, l’organisation des groupes de programmes. Pour plus d’informations, consultez la section [Personnaliser l’écran de démarrage](/windows-hardware/manufacture/desktop/customize-the-start-screen).  



## <a name="optional-task-sequence-steps-for-rollback"></a>Étapes de séquence de tâches de restauration facultatives  

En cas de problème pendant le processus de mise à niveau après le redémarrage de l’ordinateur, l’installation de Windows restaure le système d’exploitation précédent. La séquence de tâches se poursuit alors avec toutes les étapes du groupe **Restauration**. Après avoir créé la séquence de tâches, ajoutez les étapes supplémentaires nécessaires dans ce groupe. Par exemple, annulez toutes les modifications apportées au système dans le groupe Préparer la mise à niveau, comme la désinstallation des logiciels incompatibles.



## <a name="recommended-task-sequence-steps-on-failure"></a>Étapes de séquence de tâches recommandées en cas d’échec
<!--1358500-->

À compter de la version 1806, le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 inclut un groupe permettant **d’exécuter des actions en cas d’échec**. Ce groupe contient les actions recommandées à ajouter en cas d’échec de la mise à niveau. Ces actions facilitent la résolution des problèmes.

- **Collecter les journaux** : pour collecter les journaux du client, ajoutez des étapes dans ce groupe.  

    - L’une des pratiques courantes consiste à copier les fichiers journaux sur un partage réseau. Pour établir cette connexion, utilisez l’étape [Se connecter à un dossier réseau](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder).  

    - Pour effectuer la copie, utilisez un script personnalisé ou un utilitaire en suivant l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) ou [Exécuter le script PowerShell](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).  

    - Les fichiers à collecter peuvent inclure les journaux suivants :  
         `%_SMSTSLogPath%\*.log`   
         `%SystemDrive%\$Windows.~BT\Sources\Panther\setupact.log`  

    - Pour plus d’informations sur setupact.log et sur les autres journaux d’installation de Windows, consultez [Journaux d’installation de Windows](https://docs.microsoft.com/windows/deployment/upgrade/log-files).  

    - Pour plus d’informations sur les journaux du client Configuration Manager, consultez [Journaux du client Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).  

    - Pour plus d’informations sur **_SMSTSLogPath** et sur d’autres variables utiles, consultez [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables).  

- **Exécuter les outils de diagnostic** : pour exécuter d’autres outils de diagnostic, ajoutez des étapes dans ce groupe. Automatisez ces outils pour collecter des informations supplémentaires à partir du système aussitôt après un échec.  

    - Un exemple est l’outil Windows [SetupDiag](https://docs.microsoft.com/windows/deployment/upgrade/setupdiag). Il s’agit d’un outil de diagnostic autonome qui vous permet d’obtenir des informations détaillées sur la raison de l’échec d’une mise à niveau Windows 10.  

        - Dans Configuration Manager, [créez un package](/sccm/apps/deploy-use/packages-and-programs#create-a-package-and-program) pour l’outil.  

        - Ajoutez l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) au groupe de votre séquence de tâches. Utilisez l’option **Package** pour référencer l’outil. La chaîne suivante est un exemple de **ligne de commande** :  
             `SetupDiag.exe /Output:"%_SMSTSLogPath%\SetupDiagResults.log" /Mode:Online`  



## <a name="additional-recommendations"></a>Recommandations supplémentaires

- Consultez la documentation Windows pour [Résoudre les erreurs de mise à niveau de Windows 10](https://docs.microsoft.com/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Cet article comporte également des informations détaillées sur le processus de mise à niveau.  

- À l’étape **Vérifier la préparation** par défaut, activez **Garantir un espace disque libre minimal (Mo)**. Choisissez une valeur au moins égale à **16384** (16 Go) pour un package de mise à niveau d’un système d'exploitation 32 bits, ou à **20480** (20 Go) pour 64 bits.  

- Utilisez la [variable de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSDownloadRetryCount) **SMSTSDownloadRetryCount** pour essayer à nouveau de télécharger la stratégie. Actuellement, le client retente deux fois par défaut ; cette variable est définie sur deux (2). Si vos clients ne sont pas connectés à un réseau intranet, les tentatives supplémentaires les aideront à récupérer la stratégie. Cette variable n’a aucun effet secondaire, en dehors du fait qu’elle retarde l’échec si elle ne parvient pas à télécharger la stratégie.<!--501016--> Augmentez également la variable **SMSTSDownloadRetryDelay** (valeur par défaut : 15 secondes).  

- Effectuez une évaluation de compatibilité inline :  

   - Ajoutez une deuxième étape **Mettre à niveau le système d’exploitation** au début du groupe **Préparer la mise à niveau**. Nommez-la *Mettre à niveau l’évaluation*. Spécifiez le même package de mise à niveau, puis activez l’option **Effectuer l’analyse de compatibilité de l’installation de Windows sans démarrer la mise à niveau**. Activez **Continuer en cas d’erreur** dans l’onglet Options.  

   - Juste après cette étape *Mettre à niveau l’évaluation*, ajoutez une étape **Exécuter la ligne de commande**. Spécifiez la ligne de commande suivante :</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Dans l'onglet **Options**, ajoutez la condition suivante : </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Ce code de retour est l’équivalent décimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), qui correspond à la réussite d’une analyse de compatibilité sans problème. Si l’étape *Évaluation de la mise à niveau* réussit et retourne ce code, la séquence de tâches ignore cette étape. En revanche, si l’étape d’évaluation retourne un autre code de retour, cette étape échoue à effectuer la séquence de tâches avec le code de retour issu de l’analyse de compatibilité de l’installation de Windows. Pour plus d'informations sur **_SMSTSOSUpgradeActionReturnCode**, consultez [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSOSUpgradeActionReturnCode).  

   - Pour plus d’informations, consultez la section [Mettre à niveau le système d’exploitation](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).  

- Si vous souhaitez faire passer l’appareil du BIOS au standard UEFI au cours de cette séquence de tâches, consultez la section [Passer du BIOS au standard UEFI pendant une mise à niveau sur place](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).  

- Si vous utilisez le Chiffrement de lecteur BitLocker, par défaut, l’installation de Windows l’interrompt automatiquement durant la mise à niveau. À partir de Windows 10 version 1803, l’installation de Windows inclut le paramètre de ligne de commande `/BitLocker` qui contrôle ce comportement. Si vos exigences de sécurité impliquent que le chiffrement du disque reste toujours activé, utilisez la [variable de séquence de tâches](/sccm/osd/understand/task-sequence-variables#OSDSetupAdditionalUpgradeOptions) **OSDSetupAdditionalUpgradeOptions** dans le groupe **Préparer la mise à niveau** afin d’inclure `/BitLocker TryKeepActive`. Pour plus d’informations, consultez [Options de ligne de commande du programme d’installation de Windows](https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-setup-command-line-options#33).<!--SCCMDocs issue #494-->  

- Certains clients suppriment les applications provisionnées par défaut dans Windows 10. (par exemple, l’application Bing Météo ou Microsoft Solitaire Collection). Dans certains cas, ces applications sont restaurées après la mise à jour de Windows 10. Pour plus d’informations, consultez [Empêcher la restauration d’applications supprimées dans Windows 10](https://docs.microsoft.com/windows/application-management/remove-provisioned-apps-during-update). Ajoutez une étape **Exécuter la ligne de commande** à la séquence de tâches dans le groupe **Préparer la mise à niveau**. Spécifiez une ligne de commande semblable à l’exemple suivant :</br> `cmd /c reg delete "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Appx\AppxAllUserStore\Deprovisioned\Microsoft.BingWeather_8wekyb3d8bbwe" /f` <!--SCCMDocs issue #526-->  
