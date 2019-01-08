---
title: 'Gérer les images de démarrage '
titleSuffix: Configuration Manager
description: Découvrez comment utiliser Configuration Manager pour gérer les images de démarrage Windows PE que vous utilisez pendant un déploiement de système d’exploitation.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0fa269199f7f3bf4299f90faef9e55766f775d4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53421329"
---
# <a name="manage-boot-images-with-system-center-configuration-manager"></a>Gérer les images de démarrage avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une image de démarrage dans Configuration Manager est une image [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) utilisée pendant un déploiement de système d’exploitation. Les images de démarrage sont utilisées pour démarrer un ordinateur dans WinPE. Ce système d’exploitation minimal contient des services et composants limités. Configuration Manager utilise WinPE pour préparer l’ordinateur de destination à l’installation de Windows. Aidez-vous des informations des sections suivantes pour gérer les images de démarrage.

## <a name="BKMK_BootImageDefault"></a> Images de démarrage par défaut
Configuration Manager propose deux images de démarrage par défaut : Une pour prendre en charge les plates-formes x86 et l'autre pour prendre en charge les plates-formes x64. Ces images sont stockées dans le dossier \\\\*nom_serveur*>\SMS_<*code_site*>\osd\boot\\<*x64*> ou <*i386*>. Les images de démarrage par défaut sont mises à jour ou régénérées selon l’action que vous effectuez.

Prenez en compte les comportements suivants des actions décrites pour les images de démarrage par défaut :
- Les objets de pilote sources doivent être valides. Ces objets sont notamment les fichiers sources du pilote. Si les objets ne sont pas valides, le site n’ajoute pas les pilotes aux images de démarrage.
- Les images de démarrage non basées sur les images de démarrage par défaut, même si elles utilisent la même version de Windows PE, ne sont pas modifiées.
- Redistribuez les images de démarrage modifiées aux points de distribution.
- Recréez tous les médias qui utilisent les images de démarrage modifiées.
- Si vous ne souhaitez pas que vos images de démarrage personnalisées/par défaut soient automatiquement mises à jour, ne les stockez pas à l’emplacement par défaut.

> [!NOTE]
> L’outil Journal de suivi de Configuration Manager (CMTrace) est ajouté à toutes les images de démarrage dans la **bibliothèque de logiciels**. Quand vous êtes dans Windows PE, démarrez l’outil en tapant **CMTrace** dans l’invite de commandes. À partir de la version 1802, quand vous lancez cmtrace.exe dans Windows PE, vous n’êtes plus invité à choisir s’il faut utiliser ce programme comme visionneuse par défaut pour les fichiers journaux.

### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Utiliser les mises à jour et la maintenance pour installer la dernière version de Configuration Manager
À partir de la version 1702, quand vous mettez à niveau la version du Kit de déploiement et d’évaluation Windows (Windows ADK) et que vous utilisez les mises à jour et la maintenance pour installer la dernière version de Configuration Manager, le site regénère les images de démarrage par défaut. Cette mise à jour comprend la nouvelle version de WinPE du Windows ADK mis à jour, la nouvelle version du client Configuration Manager, les pilotes et les personnalisations. Le site ne modifie pas les images de démarrage personnalisées.

Avant la version 1702, Configuration Manager met à jour l’image de démarrage existante avec les composants, les pilotes et les personnalisations du client, mais n’utilise pas la dernière version de WinPE du Windows ADK. Modifiez manuellement l’image de démarrage pour utiliser la nouvelle version du Windows ADK.

### <a name="upgrade-from-configuration-manager-2012-to-configuration-manager-current-branch-cb"></a>Mettre à niveau Configuration Manager 2012 vers Configuration Manager Current Branch (CB)
Quand vous mettez à niveau Configuration Manager 2012 vers Configuration Manager CB par le biais du processus d’installation, le site regénère les images de démarrage par défaut. Cette mise à jour comprend la nouvelle version de WinPE du Windows ADK mis à jour et la nouvelle version du client Configuration Manager. Toutes les personnalisations d’image de démarrage restent inchangées. Le site ne modifie pas les images de démarrage personnalisées.

### <a name="update-distribution-points-with-the-boot-image"></a>Mettre à jour les points de distribution avec l’image de démarrage
Quand vous utilisez l’action **Mettre à jour les points de distribution** à partir du nœud **Images de démarrage** dans la console, le site met à jour l’image de démarrage cible avec les composants, les pilotes et les personnalisations du client.    

À partir de Configuration Manager version 1706, rechargez l’image de démarrage avec la dernière version de WinPE dans le répertoire d’installation du Windows ADK. La page **Général** de l’Assistant Mise à jour des points de distribution fournit les informations suivantes : 
 - La version de Windows ADK installée sur le serveur de site
 - La version du Windows ADK de WinPE dans l’image de démarrage
 - La version du client Configuration Manager. Utilisez ces informations pour décider s’il faut ou non recharger l’image de démarrage. Le nœud **Images de démarrage** comprend également une nouvelle colonne pour (**Version de client**). Utilisez cette colonne pour afficher rapidement la version du client Configuration Manager dans chaque image de démarrage.    


##  <a name="BKMK_BootImageCustom"></a> Personnaliser une image de démarrage  
 Quand une image de démarrage est basée sur la version WinPE de la version prise en charge du Windows ADK, vous pouvez personnaliser ou [modifier une image de démarrage](#BKMK_ModifyBootImages) dans la console. Quand un site est mis à niveau avec une nouvelle version et qu’une nouvelle version de Windows ADK est installée, les images de démarrage personnalisées (ne figurant pas dans l’emplacement d’image de démarrage par défaut) ne sont pas mises à jour avec la nouvelle version de Windows ADK. Dans ce cas, vous ne pouvez pas personnaliser les images de démarrage dans la console Configuration Manager. En revanche, elles continuent à fonctionner comme avant la mise à niveau.  

 Quand une image de démarrage est basée sur une autre version du Windows ADK installé sur un site, vous devez personnaliser les images de démarrage. Utilisez une autre méthode pour personnaliser ces images de démarrage, comme l’utilisation de l’outil en ligne de commande Gestion et maintenance des images de déploiement (DISM). DISM fait partie du Windows ADK. Pour plus d’informations, consultez [Personnaliser les images de démarrage](customize-boot-images.md).  

##  <a name="BKMK_AddBootImages"></a> Ajouter une image de démarrage  

 Au moment de l’installation du site, Configuration Manager ajoute automatiquement des images de démarrage qui sont basées sur une version de WinPE de la version prise en charge de Windows ADK. Dans certaines versions de Configuration Manager, vous pouvez ajouter des images de démarrage basées sur une version de WinPE différente de la version prise en charge de Windows ADK. Une erreur se produit si vous essayez d’ajouter une image de démarrage qui contient une version non prise en charge de WinPE. Voici la liste des versions de WinPE et Windows ADK actuellement prises en charge : 

- **Version de Windows ADK**  

   Windows ADK pour Windows 10  

- **Versions de Windows PE pour les images de démarrage personnalisables à partir de la console Configuration Manager**  

   Windows PE 10  

- **Versions prises en charge de Windows PE pour les images de démarrage non personnalisables à partir de la console Configuration Manager**  

   Windows PE 3.1<sup>1</sup> et Windows PE 5  

   <sup>1</sup> Vous pouvez ajouter une image de démarrage à Configuration Manager uniquement si elle est basée sur Windows PE 3.1. Mettez à niveau le Kit d’installation automatisée (Windows AIK) pour Windows 7 (basé sur Windows PE 3.0) avec le supplément Windows AIK pour Windows 7 SP1 (basé sur Windows PE 3.1). Téléchargez le supplément Windows AIK pour Windows 7 SP1 à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  

   Par exemple, utilisez la console Configuration Manager pour personnaliser les images de démarrage basées sur Windows PE 10 du Windows ADK pour Windows 10. Pour une image de démarrage basée sur Windows PE 5, personnalisez-la sur un autre ordinateur à l’aide de la version de DISM du Windows ADK pour Windows 8. Ensuite, ajoutez l’image de démarrage personnalisée à la console Configuration Manager. Pour plus d’informations, consultez [Personnaliser les images de démarrage](customize-boot-images.md).

  Pour ajouter une image de démarrage manuellement, procédez comme suit.  

#### <a name="to-add-a-boot-image"></a>Pour ajouter une image de démarrage  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter une image de démarrage** pour démarrer l'Assistant Ajout d'une image de démarrage.  

4. Sur la page **Source de données** , spécifiez les options suivantes et cliquez sur **Suivant**.  

   -   Dans la zone **Chemin d'accès** , indiquez le chemin d'accès au fichier WIM de l'image de démarrage.  

        Le chemin d'accès spécifié doit être un chemin d'accès réseau valide au format UNC. Exemple : \\\\<*nom_serveur*\\<*nom_partage*>\\<*nom_image_démarrage*>.wim.  

   -   Sélectionnez l'image de démarrage dans la liste déroulante **Image de démarrage** . Si le fichier WIM contient plusieurs images de démarrage, sélectionnez l’image appropriée.  

5. Dans la page **Général**  , spécifiez les options suivantes et cliquez sur **Suivant**.  

   -   Dans la zone **Nom** , spécifiez un nom unique pour l'image de démarrage.  

   -   Dans la zone **Version** , spécifiez un numéro de version pour l'image de démarrage.  

   -   Dans la zone **Commentaire** , spécifiez une description sommaire de l'utilisation de l'image de démarrage.  

6. Effectuez toutes les étapes de l'Assistant.  

   L’image de démarrage est maintenant répertoriée dans le nœud **Image de démarrage** de la console Configuration Manager. Avant d’utiliser l’image de démarrage pour déployer un système d’exploitation, distribuez l’image de démarrage aux points de distribution. 

> [!NOTE]  
>  Dans le nœud **Image de démarrage** de la console, la colonne **Taille (Ko)** affiche la taille décompressée de chaque image de démarrage. Quand le site envoie une image de démarrage sur le réseau, il envoie une copie compressée. Cette copie est généralement inférieure à la taille indiquée dans la colonne **Taille (Ko)**.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuer des images de démarrage à un point de distribution  
 Les images de démarrage sont distribuées aux points de distribution de la même façon que vous distribuez d'autre contenu. Dans la plupart des cas, vous devez distribuer l’image de démarrage à au moins un point de distribution avant de déployer un système d’exploitation et de créer des médias.   

> [!NOTE]  
> Pour utiliser PXE afin de déployer un système d’exploitation, tenez compte des points suivants avant de distribuer l’image de démarrage :  
> - Configurez le point de distribution pour accepter les demandes PXE.  
> - Distribuez aussi bien une image de démarrage PXE x86 que x64 à au moins un point de distribution PXE.  
> - Configuration Manager distribue les images de démarrage vers le dossier **RemoteInstall** du point de distribution compatible PXE.  
>   
> Pour plus d’informations sur l’utilisation de PXE pour déployer des systèmes d’exploitation, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

 Pour découvrir comment distribuer une image de démarrage, consultez [Distribute content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

##  <a name="BKMK_ModifyBootImages"></a> Modifier une image de démarrage  
 Vous pouvez ajouter des pilotes de périphérique à l’image de démarrage, en supprimer de celle-ci ou modifier les propriétés associées à l’image. Les pilotes de périphérique que vous ajoutez ou supprimez peuvent inclure des pilotes de périphérique de stockage de masse ou de cartes réseau. Quand vous modifiez des images de démarrage, tenez compte des facteurs suivants :  

- Importez et activez les pilotes de périphérique dans le catalogue de pilotes de périphérique avant de les ajouter à l’image de démarrage.  

- Quand vous modifiez une image de démarrage, cette image ne modifie aucun des packages associés auxquels l’image de démarrage fait référence.  

- Quand vous modifiez une image de démarrage, **mettez-la à jour** sur les points de distribution qui l’ont déjà. Ce processus rend la version la plus récente de l’image de démarrage disponible pour les clients. Pour plus d’informations, voir [Manage content you have distributed](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  

  Utilisez la procédure suivante pour modifier une image de démarrage.  

#### <a name="to-modify-the-properties-of-a-boot-image"></a>Pour modifier les propriétés d'une image de démarrage  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

3.  Sélectionnez l'image de démarrage à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir la boîte de dialogue **Propriétés** de l'image de démarrage.  

5.  Définissez les paramètres suivants pour modifier le comportement de l'image de démarrage :  

    -   Dans l'onglet **Images** , si vous avez modifié les propriétés de l'image de démarrage à l'aide d'un outil externe, cliquez sur **Recharger**.  

    -   Sous l’onglet **Pilotes** , ajoutez les pilotes de périphérique Windows nécessaires pour démarrer WinPE. Tenez compte des points suivants quand vous ajoutez des pilotes de périphérique :  

        -   Sélectionnez **Masquer les pilotes qui ne correspondent pas à l’architecture de l’image de démarrage** pour afficher uniquement les pilotes de l’architecture de l’image de démarrage. L’architecture est basée sur celle indiquée dans le fichier INF du fabricant.  

        -   Sélectionnez **Masquer les pilotes qui ne sont pas dans une classe de stockage ou réseau (pour les images de démarrage)** pour afficher uniquement les pilotes réseau et de stockage. Cette option masque également les autres pilotes qui ne sont généralement pas nécessaires pour les images de démarrage, comme les pilotes de modem ou vidéo.  

        -   Sélectionnez **Masquer les pilotes qui ne sont pas signés numériquement** pour masquer les pilotes qui n’ont pas de signature numérique valide.  

        -   Nous vous conseillons d’ajouter uniquement des pilotes de stockage de masse à l’image de démarrage, sauf si d’autres pilotes sont nécessaires pour WinPE.  

        -   Parce que WinPE intègre déjà de nombreux pilotes, ajoutez uniquement les pilotes réseau et de stockage de masse qui ne sont pas fournis par WinPE.  

        -   Vérifiez que les pilotes que vous ajoutez à l’image de démarrage correspondent à l’architecture de l’image de démarrage.  

        > [!NOTE]  
        >  Vous devez importer les pilotes de périphérique dans le catalogue de pilotes avant de les ajouter à une image de démarrage. Pour plus d’informations sur l’importation de pilotes de périphérique, consultez [Gérer les pilotes](manage-drivers.md).  

    -   Dans l'onglet **Personnalisation** , sélectionnez l'un des paramètres suivants :  

        -   Activez la case à cocher **Activer une commande de prédémarrage** pour spécifier une commande à exécuter avant l'exécution de la séquence de tâches. Quand vous activez cette option, spécifiez également la ligne de commande à exécuter et les fichiers de support demandés par la commande.  

            > [!WARNING]  
            >  Ajoutez **cmd /c** au début de la ligne de commande. Si vous ne spécifiez pas **cmd /c**, la commande ne se ferme pas après son exécution. Le déploiement continue d’attendre la fin de l’exécution de la commande et ne démarre aucune autre commande ou action configurée.  

            > [!TIP]  
            >  Pendant la création de la séquence de tâches, l’Assistant écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des variables de la séquence de tâches, dans le fichier journal CreateTSMedia.log. Ce journal se trouve sur l’ordinateur qui exécute la console Configuration Manager. Consultez ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

        -   Définissez les paramètres **Arrière-plan Windows PE** pour spécifier si vous souhaitez utiliser l’arrière-plan de WinPE par défaut ou un arrière-plan personnalisé.  

        -   Sélectionnez **Activer la prise en charge des commandes (test uniquement)** pour ouvrir une invite de commande à l’aide de la touche **F8** durant le déploiement de l’image de démarrage. Cette option est utile pour la résolution des problèmes quand vous testez votre déploiement. Il n'est pas conseillé d'utiliser ce paramètre dans un déploiement de production.  

        -   Configurez l’espace de travail de l’image Windows PE, qui correspond au stockage temporaire (disque RAM) utilisé par WinPE. Par exemple, quand une application est exécutée dans WinPE et doit écrire des fichiers temporaires, WinPE redirige les fichiers vers l’espace de travail en mémoire afin de simuler la présence d’un disque dur. Par défaut, WinPE alloue 32 mégaoctets (Mo) de mémoire inscriptible.  

    -   Dans l'onglet **Source de données** , mettez à jour les paramètres suivants :  

        -   Pour changer le fichier source de l’image de démarrage, définissez **Chemin de l’image** et **Index de l’image**.  

        -   Pour créer une planification des mises à jour de l’image de démarrage par le site, sélectionnez **Mettre à jour les points de distribution avec une planification**.  

        -   Si vous ne voulez pas que le contenu de ce package soit conservé en dehors du cache du client pour libérer de l’espace pour un autre contenu, sélectionnez **Conserver le contenu dans le cache du client**.  

        -   Pour spécifier que le site distribue uniquement les fichiers modifiés quand il met à jour le package d’images de démarrage sur le point de distribution, sélectionnez **Activer la réplication différentielle binaire**. Ce paramètre réduit le trafic réseau entre les sites. La réplication différentielle binaire est particulièrement utile quand le package d’image de démarrage est volumineux et que les changements sont relativement petits.  

        -   Si vous utilisez l’image de démarrage dans un déploiement PXE, sélectionnez **Déployer cette image de démarrage à partir du point de distribution PXE**.  

            > [!NOTE]  
            >  Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

    -   Dans l'onglet **Accès aux données** , sélectionnez l'un des paramètres suivants :  

        -   Définissez les **Paramètres de partage de package** si vous voulez que les clients installent le contenu dans ce package à partir du réseau.  

        -   Définissez les **Paramètres de mise à jour de package** pour spécifier de quelle manière Configuration Manager déconnecte les utilisateurs du point de distribution. Il est possible que Configuration Manager ne puisse pas mettre à jour l’image de démarrage quand des utilisateurs sont connectés au point de distribution.  

    -   Dans l'onglet **Paramètres de distribution** , sélectionnez l'un des paramètres suivants :  

        -   Dans la liste **Priorité de distribution**, spécifiez le niveau de priorité. Configuration Manager utilise cette liste de priorités quand le site distribue plusieurs packages au même point de distribution.  

        -   Si vous voulez activer la distribution de contenu à la demande sur des points de distribution préférés, sélectionnez **Distribuer le contenu de ce package aux points de distribution préférés**. Quand vous activez ce paramètre, si le client demande le contenu du package et que celui-ci n’est disponible sur aucun point de distribution préféré, le point de gestion distribue le contenu à tous les points de distribution préférés.  

        -   Pour spécifier le mode de distribution de l’image de démarrage aux points de distribution qui sont activés pour le contenu préparé, définissez les **Paramètres du point de distribution préparé**.  

            > [!NOTE]  
            >  Pour plus d’informations sur le contenu préparé, consultez [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

    -   Dans l'onglet **Emplacements du contenu** , sélectionnez le point de distribution ou le groupe de points de distribution et effectuez l'une des actions suivantes :  

        -   Cliquez sur **Redistribuer** pour distribuer à nouveau l'image de démarrage vers le point de distribution ou le groupe de points de distribution sélectionné.  

        -   Cliquez sur **Valider** pour vérifier l'intégrité du package d'images de démarrage sur le point de distribution ou le groupe de points de distribution sélectionné.  

    -   Sous l’onglet **Composants facultatifs**, spécifiez les composants à ajouter à Windows PE pour être utilisés avec Configuration Manager. Pour plus d'informations sur les composants facultatifs disponibles, consultez la page [WinPE : Ajouter des packages (informations de référence sur les composants facultatifs)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

    -   Dans l'onglet **Sécurité** , sélectionnez un utilisateur administratif et modifiez les opérations qu'il peut effectuer.  

6.  Après avoir configuré les propriétés, cliquez sur **OK**.  

##  <a name="BKMK_BootImagePXE"></a> Configurer une image de démarrage pour un déploiement à partir d’un point de distribution PXE  
 Avant de pouvoir utiliser une image de démarrage pour un déploiement de système d’exploitation PXE, vous devez configurer l’image de démarrage pour un déploiement à partir d’un point de distribution PXE.  

#### <a name="to-configure-a-boot-image-to-deploy-from-a-pxe-enabled-distribution-point"></a>Pour configurer une image de démarrage pour un déploiement à partir d’un point de distribution PXE  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

3.  Sélectionnez l'image de démarrage à modifier.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés** pour ouvrir la boîte de dialogue **Propriétés** de l'image de démarrage.  

5.  Sous l’onglet **Source de données** , sélectionnez **Déployer cette image de démarrage depuis le point de distribution PXE**.  

    > [!NOTE]  
    >  Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](../deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

6.  Après avoir configuré les propriétés, cliquez sur **OK**.  

##  <a name="BKMK_BootImageLanguage"></a> Configurer plusieurs langues pour le déploiement d’images de démarrage  
 Les images de démarrage sont indépendantes de la langue. Cette fonctionnalité vous permet d’utiliser une image de démarrage pour afficher le texte de la séquence de tâches dans plusieurs langues en mode WinPE. Ajoutez la prise en charge de langue appropriée à partir de l’onglet **Composants facultatifs** de l’image de démarrage. Ensuite, définissez la variable de séquence de tâches appropriée pour indiquer la langue à afficher. La langue du système d’exploitation déployé est indépendante de la langue de WinPE. La langue que WinPE affiche est déterminée comme suit :  

- Quand un utilisateur exécute la séquence de tâches à partir d’un système d’exploitation existant, Configuration Manager utilise automatiquement la langue configurée pour l’utilisateur. Quand la séquence de tâches est exécutée automatiquement à une échéance de déploiement obligatoire, Configuration Manager utilise la langue du système d’exploitation.  

- Dans le cas des déploiements de système d’exploitation qui utilisent PXE ou un support, définissez la valeur de l’ID de langue dans la variable **SMSTSLanguageFolder**, dans le cadre d'une commande de prédémarrage. Quand l’ordinateur démarre dans WinPE, les messages sont affichés dans la langue que vous avez spécifiée dans la variable. En cas d’erreur durant l’accès au fichier de ressources de langue figurant dans le dossier spécifié ou si vous ne définissez pas la variable, WinPE affiche les messages dans la langue par défaut.  

  > [!NOTE]  
  >  Quand le média est protégé par un mot de passe, le texte qui invite l’utilisateur à entrer le mot de passe est toujours affiché dans la langue de WinPE.  

  Pour définir la langue de WinPE pour les déploiements PXE ou les déploiements de système d’exploitation établis par un média, suivez la procédure ci-dessous.  

#### <a name="to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-operating-system-deployment"></a>Pour définir la langue de Windows PE pour un déploiement PXE ou un déploiement de système d'exploitation établi par un média  

1.  Avant de mettre à jour l’image de démarrage, vérifiez que le fichier de ressources de séquence de tâche approprié (tsres.dll) se trouve dans le dossier de langue correspondant sur le serveur de site. Par exemple, le fichier de ressources anglais se trouve à l’emplacement suivant : <*dossier_installation_ConfigMgr*> \OSD\bin\x64\00000409\tsres.dll.  

2.  Dans le cadre de votre commande de prédémarrage, affectez l'ID de langue approprié à la variable d'environnement SMSTSLanguageFolder. Vous devez spécifier l'ID de langue au format décimal, et non hexadécimal. Par exemple, pour définir l’ID de langue sur anglais, spécifiez la valeur décimale 1033 au lieu de la valeur hexadécimale 00000409 du nom de dossier.  
