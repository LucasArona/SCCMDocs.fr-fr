---
title: Créer une séquence de tâches de mise à niveau du système d’exploitation
titleSuffix: Configuration Manager
description: Utiliser une séquence de tâches automatiquement mise à niveau à partir de Windows 7 ou ultérieur vers Windows 10
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7591e386-a9ab-4640-8643-332dce5aa006
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d35a5ea3ebde6ce6ab0934832180223c2a634541
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352530"
---
# <a name="create-a-task-sequence-to-upgrade-an-operating-system-in-system-center-configuration-manager"></a>Créer une séquence de tâches pour mettre à niveau un système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, utilisez des séquences de tâches pour automatiquement mettre à niveau un système d’exploitation sur un ordinateur de destination. Cette mise à niveau peut être effectuée à partir de Windows 7 ou une version ultérieure vers Windows 10, ou à partir de Windows Server 2012 ou une version ultérieure vers Windows Server 2016. Créez une séquence de tâches qui référence le package de mise à niveau du système d’exploitation et tout autre contenu à installer, comme des applications ou des mises à jour logicielles. La séquence de tâches de mise à niveau d’un système d’exploitation fait partie intégrante du scénario [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md).  



##  <a name="BKMK_UpgradeOS"></a> Créer une séquence de tâches pour mettre à niveau un système d’exploitation  
 Pour mettre à niveau le système d’exploitation sur des ordinateurs, vous pouvez créer une séquence de tâches et sélectionner **Mettre à niveau un système d’exploitation à partir du package de mise à niveau** dans l’Assistant Création d’une séquence de tâches. L’Assistant ajoute les étapes de la séquence de tâches permettant de mettre à niveau le système d’exploitation, d’appliquer des mises à jour logicielles et d’installer des applications. Avant de créer la séquence de tâches, vous devez vous assurer que les conditions requises suivantes sont remplies :    

-   **Obligatoire**  

     - Le [package de mise à niveau du système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md) doit être disponible dans la console Configuration Manager.
     - Lors d’une mise à niveau vers Windows Server 2016, sélectionnez le paramètre **Ignorer les messages de compatibilité révocables** au cours de l’étape de la séquence de tâches Mettre à niveau le système d’exploitation. Sinon, la mise à niveau échoue.

-   **Obligatoire (si utilisé)**  

    -   Les [mises à jour logicielles](../../sum/get-started/synchronize-software-updates.md) doivent être synchronisées dans la console Configuration Manager.  

    -   Les [applications](../../apps/deploy-use/create-applications.md) doivent être ajoutées à la console Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-upgrades-an-operating-system"></a>Pour créer une séquence de tâches qui met à niveau un système d’exploitation  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4.  Dans la page **Créer une séquence de tâches** , sélectionnez **Mettre à niveau un système d’exploitation à partir du package de mise à niveau**, puis cliquez sur **Suivant**.  

5.  Sur la page **Informations sur la séquence de tâches** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Nom de la séquence de tâches**: spécifiez un nom qui identifie la séquence de tâches.  

    -   **Description**: spécifiez une description de la tâche qui est effectuée par la séquence de tâches.  

6.  Dans la page **Mettre à niveau le système d’exploitation Windows** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Mettre à niveau le package**: spécifiez le package de mise à niveau qui contient les fichiers sources de mise à niveau du système d’exploitation. Vous pouvez vérifier que vous avez sélectionné le bon package de mise à niveau en examinant les informations contenues dans le volet **Propriétés** . Pour plus d’informations, consultez [Gérer les packages de mise à niveau de système d’exploitation](../get-started/manage-operating-system-upgrade-packages.md).  

    -   **Index d’édition**: si plusieurs index d’édition de système d’exploitation sont disponibles dans le package, sélectionnez l’index d’édition souhaité. Par défaut, le premier élément est sélectionné.  

    -   **Clé du produit**: spécifiez la clé de produit pour le système d’exploitation Windows à installer. Vous pouvez spécifier des clés de licence en volume codées et des clés de produit standard. Si vous utilisez une clé de produit non codée, chaque groupe de cinq caractères doit être séparé par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*. Quand la mise à niveau concerne une édition de licence en volume, la clé de produit n’est pas requise. Vous avez besoin d’une clé de produit seulement quand la mise à niveau concerne une édition commerciale de Windows.  

    -   **Ignore any dismissable compatibility messages** (Ignorer les messages de compatibilité révocables) : sélectionnez ce paramètre si vous effectuez la mise à niveau vers Windows Server 2016. Si vous ne sélectionnez pas ce paramètre, l’exécution de la séquence de tâches échoue car le programme d’installation de Windows attend que l’utilisateur clique sur **Confirmer** dans la boîte de dialogue de compatibilité d’une application Windows.   

7.  Dans la page **Inclure les mises à jour**, spécifiez s’il faut installer toutes les mises à jour logicielles, seulement celles qui sont obligatoires ou aucune. Cliquez ensuite sur **Suivant**. Si vous spécifiez l’installation des mises à jour logicielles, Configuration Manager installe uniquement les mises à jour logicielles ciblées sur les regroupements dont l’ordinateur de destination est membre.  

8.  Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous spécifiez plusieurs applications, vous pouvez également spécifier que la séquence de tâches continue si l'installation d'une application spécifique échoue.  

9. Effectuez toutes les étapes de l'Assistant.  


 > [!Important] 
 > À la fin de la séquence de tâche, le client ne supprime pas les scripts de post-traitement et de restauration tant que l’ordinateur n’a pas redémarré. Ces fichiers de script ne contiennent pas d’informations sensibles.  


 > [!Note]
 > À partir de la version 1802, le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend des groupes supplémentaires, avec des actions recommandées à ajouter avant ou après le processus de mise à niveau. Ces actions sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils sur Windows 10. Pour plus d’informations, consultez les étapes de séquence de tâches recommandées [pour préparer la mise à niveau](#recommended-task-sequence-steps-to-prepare-for-upgrade) et pour le [post-traitement](#recommended-task-sequence-steps-for-post-processing).



## <a name="configure-pre-cache-content"></a>Configurer la mise en cache préalable du contenu
<!--1021244-->
La fonctionnalité de mise en cache préalable pour les déploiements disponibles de séquences de tâches permet aux clients de télécharger le contenu de package de mise à niveau de système d’exploitation approprié avant l’installation de la séquence de tâches par l’utilisateur.  

> [!TIP]  
> Cette fonctionnalité a été introduite dans la version 1702 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1706, cette fonctionnalité n’est plus une fonctionnalité en préversion.  


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Par exemple, vous voulez une seule séquence de tâches de mise à niveau sur place pour tous les utilisateurs, et vous avez plusieurs architectures et langues. Dans les versions précédentes, le téléchargement du contenu commence quand l’utilisateur installe un déploiement de séquences de tâches disponible à partir du Centre logiciel. Ce délai a pour effet de retarder la disponibilité de l’installation. Tout le contenu référencé dans la séquence de tâches est téléchargé. Ce contenu comprend tous les packages de mise à niveau du système d’exploitation pour chaque langue et chaque architecture. Si chaque package de mise à niveau fait environ trois Go, le contenu total est très volumineux.

La mise en cache préalable du contenu vous permet de laisser le client télécharger uniquement le package de mise à niveau de système d’exploitation applicable ainsi que tout autre contenu référencé dès qu’il reçoit le déploiement. Quand l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est prêt et l’installation démarre rapidement, car le contenu se trouve sur le disque dur local.

 > [!NOTE]
 > Actuellement, ce comportement s’applique uniquement au package de mise à niveau de système d’exploitation. Ce package est le seul contenu pour lequel vous spécifiez l’architecture ou la langue correspondante. Par exemple, si la séquence de tâches référence également plusieurs packages de pilotes, le client les télécharge tous. Le moteur de séquence de tâches évalue les conditions à chaque étape pendant l’exécution de la séquence de tâches, et non à l’avance. Le client utilise les balises sur les propriétés de package pour déterminer le contenu à mettre en cache préalablement.

### <a name="to-configure-the-pre-cache-feature"></a>Pour configurer la fonctionnalité de mise en cache préalable

1. Créez des packages de mise à niveau de système d’exploitation pour des architectures et des langues spécifiques. Spécifiez l’architecture et la langue sous l’onglet **Source de données** du package. Pour la langue, utilisez la conversion décimale. Par exemple, 1033 est la valeur décimale pour l’anglais et 0x0409 est son équivalent hexadécimal.

    Le client évalue les valeurs d’architecture et de langue pour déterminer le package de mise à niveau de système d’exploitation qu’il télécharge pendant la mise en cache préalable.

1. Créez une séquence de tâches avec des étapes conditionnelles pour les différentes langues et architectures. Par exemple, l’étape suivante utilise la version anglaise :

    ![Éditeur de séquence de tâches montrant plusieurs étapes de mise à niveau de système d’exploitation pour ENU, DEU et JPN](../media/precacheproperties2.png)

    ![Éditeur de séquence de tâches, onglet Options, affichant la requête WQL WMI pour les paramètres régionaux et l’architecture de système d’exploitation](../media/precacheoptions2.png)  

3. déployer la séquence de tâches. Pour configurer la fonctionnalité de mise en cache préalable, configurez les paramètres suivants :
    - Sous l’onglet **Général**, sélectionnez **Prétélécharger le contenu pour cette séquence de tâches**.
    - Sous l’onglet **Paramètres de déploiement**, configurez la séquence de tâches avec **Disponible** comme **Objectif**.
    - Sous l’onglet **Planification**, pour le paramètre **Planifier la disponibilité de ce déploiement**, choisissez l’heure actuellement sélectionnée. Le client commence à préalablement mettre en cache le contenu pendant le temps de mise à disposition du déploiement. Quand un client ciblé reçoit cette stratégie, le temps de mise à disposition est passé. Par conséquent, le téléchargement de la mise en cache préalable commence immédiatement. Si le client reçoit cette stratégie, mais que le temps de mise à disposition se situe dans le futur, le client commence la mise en cache du contenu uniquement au début du temps de mise à disposition. 
    - Sous l’onglet **Points de distribution**, configurez les paramètres **Options de déploiement**. Si le contenu n’est pas préalablement mis en cache avant le démarrage de l’installation, le client utilise ces paramètres.
  

### <a name="user-experience"></a>Expérience utilisateur
- Quand le client reçoit la stratégie de déploiement, il commence la mise en cache préalable du contenu après le temps de mise à disposition du déploiement. Ce contenu comprend tous les packages référencés, mais uniquement le package de mise à niveau de système d’exploitation qui correspond aux attributs d’architecture et de langue du package.
- Quand le client met le déploiement à la disposition des utilisateurs, une notification s’affiche pour les informer du nouveau déploiement. La séquence de tâches est alors visible dans le Centre logiciel. L’utilisateur peut accéder au Centre logiciel et cliquer sur **Installer** pour démarrer l’installation.
- Si tout le contenu n’est pas préalablement mis en cache quand l’utilisateur installe la séquence de tâches, le client utilise les paramètres que vous spécifiez sous l’onglet **Option de déploiement** du déploiement. 



## <a name="recommended-task-sequence-steps-to-prepare-for-upgrade"></a>Étapes de séquence de tâches recommandées pour préparer la mise à niveau

À partir de la version 1802, le modèle de séquence de tâches par défaut pour la mise à niveau sur place de Windows 10 comprend des groupes supplémentaires, avec des actions recommandées à ajouter avant le processus de mise à niveau. Ces actions du groupe **Préparer la mise à niveau** sont communes à de nombreux clients qui parviennent à mettre à niveau des appareils vers Windows 10. Pour les sites sur les versions antérieures à 1802, ajoutez manuellement ces actions à votre séquence de tâches dans le groupe **Préparer la mise à niveau**.
- **Vérification de la batterie** : ajoutez des étapes dans ce groupe pour contrôler si l’ordinateur est sur batterie ou sur secteur. Cette action doit être effectuée par un utilitaire ou un script personnalisé.
- **Vérification de la connexion réseau/câblée** : ajoutez des étapes dans ce groupe pour contrôler si l’ordinateur est connecté à un réseau et n’utilise pas de connexion sans fil. Cette action doit être effectuée par un utilitaire ou un script personnalisé.
- **Supprimer les applications incompatibles** : ajoutez des étapes dans ce groupe pour supprimer toutes les applications incompatibles avec cette version de Windows 10. Il existe différentes façons de désinstaller une application selon les cas. Si l’application utilise Windows Installer, copiez la ligne de commande **Programme de désinstallation** de l’onglet **Programmes** dans les propriétés de type de déploiement de Windows Installer de l’application. Ensuite, ajoutez dans ce groupe une étape **Exécuter la ligne de commande** comportant la ligne de commande du programme de désinstallation. Par exemple : </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Supprimer les pilotes incompatibles** : ajoutez des étapes dans ce groupe pour supprimer tous les pilotes incompatibles avec cette version de Windows 10.
- **Supprimer/suspendre la sécurité tierce** : ajoutez des étapes dans ce groupe pour supprimer ou suspendre des programmes de sécurité tiers, par exemple, des antivirus.
   - Si vous utilisez un programme de chiffrement de disque tiers, indiquez son pilote de chiffrement à l’installation de Windows avec [l’option de ligne de commande](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) **/ReflectDrivers**. Ajoutez une étape [Définir une variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) à la séquence de tâches dans ce groupe. Affectez la valeur **OSDSetupAdditionalUpgradeOptions** à la variable de séquence de tâches. Définissez la valeur **/ReflectDriver** avec le chemin d’accès au pilote. Cette [variable d’action de séquence de tâches](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) ajoute la ligne de commande d’installation de Windows utilisée par la séquence de tâches. Contactez votre éditeur de logiciels pour obtenir de l’aide sur ce processus.

### <a name="download-package-content-task-sequence-step"></a>Étape de séquence de tâches Télécharger le contenu du package  
 Vous pouvez exécuter l’étape [Télécharger le contenu du package](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent) avant l’étape **Mettre à niveau le système d’exploitation** dans les scénarios suivants :  

-   Vous utilisez une seule séquence de tâches de mise à niveau pour les deux plateformes x86 et x64. Incluez deux étapes **Télécharger le contenu du package** dans le groupe **Préparer pour la mise à niveau**. Définissez des conditions sur chaque étape pour détecter l’architecture du client. Du fait de cette condition, l’étape télécharge uniquement le package de mise à niveau du système d’exploitation approprié. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable et utilisez cette variable pour le chemin du support à l’étape **Mettre à niveau le système d’exploitation** .  

-   Pour télécharger dynamiquement un package de pilotes applicable, utilisez deux étapes **Télécharger le contenu du package** avec des conditions pour détecter le type de matériel approprié pour chaque package de pilotes. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable. Utilisez ensuite cette variable comme valeur **Contenu intermédiaire** dans la section des pilotes sur l’étape **Mettre à niveau le système d’exploitation**.  

   > [!NOTE]
   > Quand il existe plusieurs packages, Configuration Manager ajoute un suffixe numérique au nom de la variable. Par exemple, si vous spécifiez la variable %mycontent% comme variable personnalisée, cet emplacement est celui où le client stocke tout le contenu référencé. Quand vous faites référence à la variable dans une étape ultérieure, comme **Mettre à niveau le système d’exploitation**, utilisez la variable avec un suffixe numérique. Dans cet exemple, %mycontent01% ou %mycontent02%, où le numéro correspond à l’ordre dans lequel l’étape **Télécharger le contenu du package** répertorie ce contenu spécifique.



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
 En cas de problème pendant le processus de mise à niveau après le redémarrage de l’ordinateur, l’installation de Windows annule la mise à niveau et restaure le système d’exploitation précédent. La séquence de tâches se poursuit alors avec toutes les étapes du groupe **Restauration**. Une fois la séquence de tâches créée, vous pouvez ajouter des étapes facultatives au groupe Restauration. Par exemple, annulez toutes les modifications apportées au système dans le groupe Préparer la mise à niveau, comme la désinstallation des logiciels incompatibles.



## <a name="additional-recommendations"></a>Recommandations supplémentaires
- Consultez la documentation Windows pour [Résoudre les erreurs de mise à niveau de Windows 10](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). Cet article comporte également des informations détaillées sur le processus de mise à niveau.
- À l’étape **Vérifier la préparation** par défaut, activez **Garantir un espace disque libre minimal (Mo)**. Choisissez une valeur au moins égale à **16384** (16 Go) pour un package de mise à niveau d’un système d'exploitation 32 bits, ou à **20480** (20 Go) pour 64 bits. 
- Utilisez la [variable de séquence de tâches intégrée](/sccm/osd/understand/task-sequence-built-in-variables) **SMSTSDownloadRetryCount** pour réessayer de télécharger la stratégie. Actuellement, le client retente deux fois par défaut ; cette variable est définie sur deux (2). Si vos clients ne sont pas connectés à un réseau d’entreprise câblé, les tentatives supplémentaires les aideront à récupérer la stratégie. Cette variable n’a aucun effet secondaire, en dehors du fait qu’elle retarde l’échec si elle ne parvient pas à télécharger la stratégie.<!-- 501016 --> Augmentez également la variable **SMSTSDownloadRetryDelay** (valeur par défaut : 15 secondes).
- Effectuez une évaluation de compatibilité inline. 
   - Ajoutez une deuxième étape **Mettre à niveau le système d’exploitation** au début du groupe **Préparer la mise à niveau**. Nommez-la *Mettre à niveau l’évaluation*. Spécifiez le même package de mise à niveau, puis activez l’option **Effectuer l’analyse de compatibilité de l’installation de Windows sans démarrer la mise à niveau**. Activez **Continuer en cas d’erreur** dans l’onglet Options. 
   - Juste après cette étape *Mettre à niveau l’évaluation*, ajoutez une étape **Exécuter la ligne de commande**. Spécifiez la ligne de commande suivante :</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>Dans l'onglet **Options**, ajoutez la condition suivante : </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>Ce code de retour est l’équivalent décimal de MOSETUP_E_COMPAT_SCANONLY (0xC1900210), qui correspond à la réussite d’une analyse de compatibilité sans problème. Si l’étape *Mettre à niveau l’évaluation* réussit et retourne ce code, cette étape est ignorée. En revanche, si l’étape d’évaluation retourne un autre code de retour, cette étape échoue à effectuer la séquence de tâches avec le code de retour issu de l’analyse de compatibilité de l’installation de Windows.
   - Pour plus d’informations, consultez la section [Mettre à niveau le système d’exploitation](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- Si vous souhaitez faire passer l’appareil du BIOS au standard UEFI au cours de cette séquence de tâches, consultez la section [Passer du BIOS au standard UEFI pendant une mise à niveau sur place](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).
