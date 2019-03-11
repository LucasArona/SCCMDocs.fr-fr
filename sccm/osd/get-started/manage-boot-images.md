---
title: Gérer les images de démarrage
titleSuffix: Configuration Manager
description: Dans Configuration Manager, apprenez à gérer les images de démarrage Windows PE que vous utilisez pendant le déploiement d’un système d’exploitation.
ms.date: 02/28/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 97f2d81a-2c58-442c-88bc-defd5a1cd48f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d4ed731b9b931e76e6d6b6d1399bf5a273bf561b
ms.sourcegitcommit: 56ec6933cf7bfc93842f55835ad336ee3a1c6ab5
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57211650"
---
# <a name="manage-boot-images-with-configuration-manager"></a>Gérer les images de démarrage avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une image de démarrage dans Configuration Manager est une image [Windows PE](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-intro) (WinPE) utilisée pendant le déploiement d’un système d’exploitation. Les images de démarrage sont utilisées pour démarrer un ordinateur dans WinPE. Ce système d’exploitation minimal contient des services et des composants limités. Configuration Manager utilise WinPE pour préparer l’ordinateur de destination à l’installation de Windows. 



## <a name="BKMK_BootImageDefault"></a> Images de démarrage par défaut

Configuration Manager propose deux images de démarrage par défaut : Une pour prendre en charge les plates-formes x86 et l'autre pour prendre en charge les plates-formes x64. Ces images sont stockées dans les dossiers *x64* ou *i386* du partage suivant sur le serveur de site : `\\<SiteServerName>\SMS_<sitecode>\osd\boot\`. Les images de démarrage par défaut sont mises à jour ou régénérées selon l’action que vous effectuez.

Prenez en compte les comportements suivants des actions décrites pour les images de démarrage par défaut :

- Les objets de pilote sources doivent être valides. Ces objets sont notamment les fichiers sources du pilote. Si les objets ne sont pas valides, le site n’ajoute pas les pilotes aux images de démarrage.  

- Les images de démarrage non basées sur les images de démarrage par défaut, même si elles utilisent la même version de Windows PE, ne sont pas modifiées.  

- Redistribuez les images de démarrage modifiées aux points de distribution.  

- Recréez tous les médias qui utilisent les images de démarrage modifiées.  

- Si vous ne souhaitez pas que vos images de démarrage personnalisées/par défaut soient automatiquement mises à jour, ne les stockez pas à l’emplacement par défaut.  

> [!NOTE]
> L’outil de journal de Configuration Manager (**CMTrace**) est ajouté à toutes les images de démarrage dans la **bibliothèque de logiciels**. Quand vous êtes dans Windows PE, démarrez l’outil en tapant `cmtrace` dans l’invite de commandes. 
> 
> À partir de la version 1802, quand vous lancez CMTrace dans Windows PE, vous n’êtes plus invité à choisir s’il faut utiliser ce programme comme visionneuse par défaut pour les fichiers journaux.


### <a name="use-updates-and-servicing-to-install-the-latest-version-of-configuration-manager"></a>Utiliser les mises à jour et la maintenance pour installer la dernière version de Configuration Manager

Lorsque vous mettez à niveau la version du Kit de déploiement et d’évaluation Windows (Windows ADK) et que vous utilisez les mises à jour et la maintenance pour installer la dernière version de Configuration Manager, le site regénère les images de démarrage par défaut. Cette mise à jour comprend la nouvelle version de WinPE du Windows ADK mis à jour, la nouvelle version du client Configuration Manager, les pilotes et les personnalisations. Le site ne modifie pas les images de démarrage personnalisées.


### <a name="upgrade-from-configuration-manager-2012-to-current-branch"></a>Mettre à niveau Configuration Manager 2012 vers la branche actuelle

Lorsque vous mettez à niveau Configuration Manager 2012 vers la branche actuelle, le site regénère les images de démarrage par défaut. Cette mise à jour comprend la nouvelle version de WinPE du Windows ADK mis à jour et la nouvelle version du client Configuration Manager. Toutes les personnalisations d’image de démarrage restent inchangées. Le site ne modifie pas les images de démarrage personnalisées.


### <a name="update-distribution-points-with-the-boot-image"></a>Mettre à jour les points de distribution avec l’image de démarrage

Quand vous utilisez l’action **Mettre à jour les points de distribution** à partir du nœud **Images de démarrage** dans la console, le site met à jour l’image de démarrage cible avec les composants, les pilotes et les personnalisations du client.    

Vous pouvez recharger l’image de démarrage avec la dernière version de WinPE dans le répertoire d’installation de Windows ADK. La page **Général** de l’Assistant Mise à jour des points de distribution fournit les informations suivantes : 
 - La version actuelle de Windows ADK installée sur le serveur de site
 - La version actuelle du client de production
 - La version du Windows ADK de WinPE dans l’image de démarrage
 - La version du client Configuration Manager dans l’image de démarrage

Si les versions dans l’image de démarrage sont obsolètes, utilisez l’option pour **recharger cette image de démarrage avec la version actuelle de Windows PE à partir de Windows ADK**. 

> [!Important]  
> Cette action est à la fois disponible pour les images de démarrage par défaut et personnalisées. Pendant ce processus de recharge de l’image de démarrage, le site ne conserve pas les personnalisations manuelles effectuées en dehors de Configuration Manager. Ceci concerne également les extensions tierces. Cette option reconstruit l’image de démarrage à l’aide de la dernière version de WinPE et de la dernière version du client. Seules les configurations que vous spécifiez dans les propriétés de l’image de démarrage sont réappliquées. <!--SCCMDocs issue #1283-->

Le nœud **Images de démarrage** comprend également une nouvelle colonne pour (**Version de client**). Utilisez cette colonne pour afficher rapidement la version du client Configuration Manager dans chaque image de démarrage.    



##  <a name="BKMK_BootImageCustom"></a> Personnaliser une image de démarrage  

Quand une image de démarrage est basée sur la version WinPE de la version prise en charge du Windows ADK, vous pouvez personnaliser ou [modifier une image de démarrage](#BKMK_ModifyBootImages) dans la console. Lorsque vous mettez à niveau un site et que vous installez une nouvelle version de Windows ADK, les images de démarrage personnalisées ne sont pas mises à jour avec la nouvelle version de Windows ADK. Dans ce cas, vous ne pouvez pas personnaliser les images de démarrage dans la console Configuration Manager. En revanche, elles continuent à fonctionner comme avant la mise à niveau.  

Quand une image de démarrage est basée sur une autre version du Windows ADK installé sur un site, vous devez personnaliser les images de démarrage. Utilisez une autre méthode pour personnaliser ces images de démarrage, comme l’utilisation de l’outil en ligne de commande Gestion et maintenance des images de déploiement (DISM). DISM fait partie du Windows ADK. Pour plus d’informations, consultez [Personnaliser les images de démarrage](customize-boot-images.md).  



##  <a name="BKMK_AddBootImages"></a> Ajouter une image de démarrage  

Au moment de l’installation du site, Configuration Manager ajoute automatiquement des images de démarrage qui sont basées sur une version de WinPE de la version prise en charge de Windows ADK. Dans certaines versions de Configuration Manager, vous pouvez ajouter des images de démarrage basées sur une version de WinPE différente de la version prise en charge de Windows ADK. Une erreur se produit si vous essayez d’ajouter une image de démarrage qui contient une version non prise en charge de WinPE. Voici la liste des versions de WinPE et Windows ADK actuellement prises en charge : 


|  |  |
|---------|---------|
| Version de Windows ADK | Windows ADK pour Windows 10 |
| Versions de Windows PE pour les images de démarrage personnalisables à partir de la console Configuration Manager | Windows PE 10 |
| Versions de Windows PE prises en charge pour les images de démarrage *non personnalisables* à partir de la console Configuration Manager | -Windows PE 3.1<sup>[Remarque 1](#bkmk_note1)</sup> <br> - Windows PE 5 |

Par exemple, utilisez la console Configuration Manager pour personnaliser les images de démarrage basées sur Windows PE 10 du Windows ADK pour Windows 10. Pour une image de démarrage basée sur Windows PE 5, personnalisez-la sur un autre ordinateur à l’aide de la version de DISM du Windows ADK pour Windows 8. Ensuite, ajoutez l’image de démarrage personnalisée à la console Configuration Manager. Pour plus d’informations, consultez les articles suivants :
- [Personnaliser les images de démarrage](/sccm/osd/get-started/customize-boot-images)
- [Prise en charge pour Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk)
- [Plateformes prises en charge par DISM](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-supported-platforms)

#### <a name="bkmk_note1"></a>Remarque 1 : Prise en charge de Windows PE 3.1

Vous pouvez ajouter une image de démarrage à Configuration Manager uniquement si elle est basée sur Windows PE, *version3.1*. Mettez à niveau le Kit d’installation automatisée (Windows AIK) pour Windows 7 (basé sur Windows PE 3.0) avec le supplément Windows AIK pour Windows 7 SP1 (basé sur Windows PE 3.1). Téléchargez le supplément Windows AIK pour Windows 7 SP1 à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=5188).  


#### <a name="process-to-add-a-boot-image"></a>Processus d’ajout d’une image de démarrage  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Images de démarrage**.  

2. Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, sélectionnez **Ajouter une image de démarrage**. Cette action démarre l’Assistant Ajout d’une image de démarrage.  

3. Sur la page **Source de données**, spécifiez les options suivantes :  

    - Dans la zone **Chemin d'accès** , indiquez le chemin d'accès au fichier WIM de l'image de démarrage. Le chemin d'accès spécifié doit être un chemin d'accès réseau valide au format UNC. Exemple : `\\ServerName\ShareName\BootImageName.wim`

    - Sélectionnez l'image de démarrage dans la liste déroulante **Image de démarrage** . Si le fichier WIM contient plusieurs images de démarrage, sélectionnez l’image appropriée.  

4. Sur la page **Général**, spécifiez les options suivantes :  

    - Dans la zone **Nom** , spécifiez un nom unique pour l'image de démarrage.  

    - Dans la zone **Version** , spécifiez un numéro de version pour l'image de démarrage.  

    - Dans la zone **Commentaire** , décrivez brièvement comment vous utilisez l'image de démarrage.  

5. Effectuez toutes les étapes de l'Assistant.  

L'image de démarrage est maintenant répertoriée dans le nœud **Image de démarrage**. Avant d’utiliser l’image de démarrage pour déployer un système d’exploitation, distribuez l’image de démarrage aux points de distribution. 

> [!Tip]  
> Dans le nœud **Image de démarrage** de la console, la colonne **Taille (Ko)** affiche la taille décompressée de chaque image de démarrage. Quand le site envoie une image de démarrage sur le réseau, il envoie une copie compressée. Cette copie est généralement inférieure à la taille indiquée dans la colonne **Taille (Ko)**.  



##  <a name="BKMK_DistributeBootImages"></a> Distribuer des images de démarrage  

Les images de démarrage sont distribuées aux points de distribution de la même façon que vous distribuez d'autre contenu. Avant de déployer un système d’exploitation ou de créer des médias, distribuez l’image de démarrage vers au moins un point de distribution.   

Pour plus d’informations sur la distribution d’une image de démarrage, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).  

Pour utiliser PXE afin de déployer un système d’exploitation, tenez compte des points suivants avant de distribuer l’image de démarrage :  
- Configurez le point de distribution pour accepter les demandes PXE.  
- Distribuez aussi bien une image de démarrage PXE x86 que x64 à au moins un point de distribution PXE.  
- Configuration Manager distribue les images de démarrage vers le dossier **RemoteInstall** du point de distribution compatible PXE.  
  
Pour plus d’informations sur l’utilisation de PXE pour déployer des systèmes d’exploitation, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  



##  <a name="BKMK_ModifyBootImages"></a> Modifier une image de démarrage  

Ajouter ou supprimer des pilotes de périphériques à l’image ou modifier les propriétés de l’image de démarrage. Les pilotes que vous ajoutez ou supprimez peuvent inclure des pilotes de stockage ou réseau. Quand vous modifiez des images de démarrage, tenez compte des facteurs suivants :  

- Avant d’ajouter des pilotes à l’image de démarrage, importez et activez-les dans le catalogue de pilotes de périphériques.  

- Quand vous modifiez une image de démarrage, cette image ne modifie aucun des packages associés auxquels l’image de démarrage fait référence.  

- Quand vous modifiez une image de démarrage, **mettez-la à jour** sur les points de distribution qui l’ont déjà. Ce processus rend la version la plus récente de l’image de démarrage disponible pour les clients. Pour plus d’informations, voir [Gérer le contenu que vous avez distribué](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_manage).  


### <a name="process-to-modify-the-properties-of-a-boot-image"></a>Processus de modification des propriétés d'une image de démarrage  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Images de démarrage**.  

2. Sélectionnez l'image de démarrage à modifier.  

3. Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4. Définissez les paramètres suivants pour modifier le comportement de l'image de démarrage :  

#### <a name="images"></a>Images
Sous l'onglet **Images** , si vous avez modifié les propriétés de l'image de démarrage à l'aide d'un outil externe, cliquez sur **Recharger**.  

#### <a name="drivers"></a>Pilotes
Sous l’onglet **Pilotes** , ajoutez les pilotes de périphérique Windows nécessaires pour démarrer WinPE. Tenez compte des points suivants quand vous ajoutez des pilotes de périphérique :  

- Vérifiez que les pilotes que vous ajoutez à l’image de démarrage correspondent à l’architecture de l’image de démarrage.  

- Pour afficher uniquement les pilotes de l’architecture de l’image de démarrage, sélectionnez **Masquer les pilotes qui ne correspondent pas à l’architecture de l’image de démarrage**. L’architecture du pilote est basée sur celle indiquée dans le fichier INF du fabricant.  

- WinPE est fourni avec de nombreux pilotes intégrés. Ajoutez uniquement des pilotes de stockage et réseau qui ne sont pas inclus dans WinPE.  

- Ajoutez uniquement des pilotes de stockage et réseau à l’image de démarrage, sauf si d’autres pilotes sont nécessaires pour WinPE.  

- Pour afficher uniquement les pilotes de stockage et réseau, sélectionnez **Masquer les pilotes qui ne sont pas dans une classe de stockage ou réseau (pour les images de démarrage)**. Cette option masque également d’autres pilotes qui ne sont pas généralement nécessaires pour les images de démarrage, tels que les pilotes de modem ou vidéo.  

- Pour masquer les pilotes qui n’ont pas de signature numérique valide, sélectionnez **Masquer les pilotes qui ne sont pas signés numériquement**.  

> [!NOTE]  
> Importez les pilotes de périphérique dans le catalogue de pilotes avant de les ajouter à une image de démarrage. Pour plus d’informations sur l’importation de pilotes de périphérique, consultez [Gérer les pilotes](manage-drivers.md).  

#### <a name="customization"></a>Personnalisation
Dans l'onglet **Personnalisation** , sélectionnez l'un des paramètres suivants :  

- Sélectionnez l’option **Activer les commandes de prédémarrage** pour spécifier une commande à exécuter avant la séquence de tâches. Quand vous activez cette option, spécifiez également la ligne de commande à exécuter et les fichiers de support demandés par la commande.  

    > [!WARNING]  
    > Ajoutez **cmd /c** au début de la ligne de commande. Si vous ne spécifiez pas **cmd /c**, la commande ne se ferme pas après son exécution. Le déploiement continue d’attendre la fin de l’exécution de la commande et ne démarre aucune autre commande ou action configurée.  

    > [!TIP]  
    > Pendant la création de la séquence de tâches, l’Assistant écrit l’ID du package et la ligne de commande de prédémarrage dans le fichier journal CreateTSMedia.log. Ces informations incluent la valeur des variables de séquence de tâches. Ce journal se trouve sur l’ordinateur qui exécute la console Configuration Manager. Consultez ce fichier journal pour vérifier les valeurs des variables de séquence de tâches.  

- Définissez les paramètres **Arrière-plan Windows PE** pour spécifier si vous souhaitez utiliser l’arrière-plan de WinPE par défaut ou un arrière-plan personnalisé.  

- Sélectionnez **Activer la prise en charge des commandes (test uniquement)** pour ouvrir une invite de commande à l’aide de la touche **F8** durant le déploiement de l’image de démarrage. Cette option est utile pour la résolution des problèmes quand vous testez votre déploiement. Il n’est pas recommandé d’utiliser ce paramètre dans un déploiement de production en raison de problèmes de sécurité.  

- Configurez l’espace de travail de l’image Windows PE, qui correspond au stockage temporaire (disque RAM) utilisé par WinPE. Par exemple, quand une application est exécutée dans WinPE et doit écrire des fichiers temporaires, WinPE redirige les fichiers vers l’espace de travail en mémoire afin de simuler la présence d’un disque dur. Par défaut, cette quantité est de 512 Mo pour les appareils de plus de 1 Go de RAM, sinon la valeur par défaut est 32 Mo.  

#### <a name="optional-components"></a>Composants facultatifs
Sous l’onglet **Composants facultatifs**, spécifiez les composants à ajouter à Windows PE pour être utilisés avec Configuration Manager. Pour plus d'informations sur les composants facultatifs disponibles, consultez la page [WinPE : Ajouter des packages (informations de référence sur les composants facultatifs)](https://docs.microsoft.com/windows-hardware/manufacture/desktop/winpe-add-packages--optional-components-reference).  

Les composants suivants sont requis par Configuration Manager et toujours ajoutés aux images de démarrage :
- Script (WinPE-Scripting)
- Démarrage (WinPE-SecureStartup)
- Réseau (WinPE-WDS-Tools)
- Script (WinPE-WMI)

La liste des **composants** affiche des éléments supplémentaires qui sont ajoutés à cette image de démarrage. Pour ajouter d’autres composants, sélectionnez l’astérisque doré. Pour supprimer un composant, sélectionnez-le dans la liste, puis sélectionnez le X rouge. 

Les composants suivants sont couramment utilisés par les clients :
- Microsoft .NET (WinPE-NetFX) : ce composant est un prérequis pour PowerShell. C’est l’un des grands composants facultatifs.  
- Windows PowerShell (WinPE-PowerShell) : ce composant nécessite .NET et ajoute la prise en charge limitée de PowerShell. Si vous exécutez des scripts PowerShell personnalisés pendant la phase WinPE de votre séquence de tâches, ajoutez ce composant. D’autres composants peuvent être requis pour les autres applets de commande PowerShell.   
- HTML (WinPE-HTA) : si vous exécutez des applications HTML personnalisées pendant la phase WinPE de votre séquence de tâches, ajoutez ce composant. 

Pour plus d’informations sur l’ajout de langues, consultez [Configurer plusieurs langues](#BKMK_BootImageLanguage). 

#### <a name="data-source"></a>source de données
Dans l'onglet **Source de données** , mettez à jour les paramètres suivants :  

- Pour changer le fichier source de l’image de démarrage, définissez **Chemin de l’image** et **Index de l’image**.  

- Pour créer une planification des mises à jour de l’image de démarrage par le site, sélectionnez **Mettre à jour les points de distribution avec une planification**.  

- Si vous ne voulez pas que le contenu de ce package soit conservé en dehors du cache du client pour libérer de l’espace pour un autre contenu, sélectionnez **Conserver le contenu dans le cache du client**.  

- Pour spécifier que le site distribue uniquement les fichiers modifiés quand il met à jour le package d’images de démarrage sur le point de distribution, sélectionnez **Activer la réplication différentielle binaire**. Ce paramètre réduit le trafic réseau entre les sites. La réplication différentielle binaire est particulièrement utile quand le package d’image de démarrage est volumineux et que les changements sont relativement petits.  

- Si vous utilisez l’image de démarrage dans un déploiement PXE, sélectionnez **Déployer cette image de démarrage à partir du point de distribution PXE**. Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  

#### <a name="data-access"></a>Accès aux données
Sous l’onglet **Accès aux données**, vous pouvez configurer les paramètres de partage de package. Si nécessaire dans votre environnement, définissez l’option sur **Copier le contenu de ce package dans un partage de package sur les points de distribution**. Vous pouvez ensuite choisir l’option supplémentaire pour **utiliser un nom personnalisé pour le partage de package** et spécifier le **nom de partage** personnalisé. Lorsque vous activez cette option, les points de distribution nécessitent davantage d'espace disque. Ceci concerne tous les points de distribution qui reçoivent cette image de démarrage. 

#### <a name="distribution-settings"></a>Paramètres de distribution
Dans l'onglet **Paramètres de distribution** , sélectionnez l'un des paramètres suivants :  

- Dans la liste **Priorité de distribution**, spécifiez le niveau de priorité. Configuration Manager utilise cette liste de priorités quand le site distribue plusieurs packages au même point de distribution.  

- Si vous voulez activer la distribution de contenu à la demande sur des points de distribution préférés, sélectionnez **Activer pour la distribution à la demande**. Quand vous activez ce paramètre, si le client demande le contenu du package et que celui-ci n’est disponible sur aucun point de distribution préféré, le point de gestion distribue le contenu. Pour plus d’informations, consultez [Distribution de contenu à la demande](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).  

- Pour spécifier le mode de distribution de l’image de démarrage aux points de distribution qui sont activés pour le contenu préparé, définissez les **Paramètres du point de distribution préparé**. Pour plus d’informations sur le contenu préparé, consultez [Prestage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  

#### <a name="content-locations"></a>Emplacements du contenu
Sous l'onglet **Emplacements du contenu** , sélectionnez le point de distribution ou le groupe de points de distribution et effectuez l'une des actions suivantes :  

- **Valider** : vérifiez l'intégrité du package d'images de démarrage sur le point de distribution ou le groupe de points de distribution sélectionné.  

- **Redistribuer** : distribuez à nouveau l'image de démarrage vers le point de distribution ou le groupe de points de distribution sélectionné.  

- **Supprimer** : supprimez l'image de démarrage du point de distribution ou du groupe de points de distribution sélectionné.  

#### <a name="security"></a>Sécurité
Sous l’onglet **Sécurité**, afficher les utilisateurs administratifs qui disposent d’autorisations pour cet objet.



## <a name="BKMK_BootImagePXE"></a> Configurer une image de démarrage pour PXE  

Avant de pouvoir utiliser une image de démarrage pour un déploiement basé sur PXE, configurez l’image de démarrage pour un déploiement à partir d’un point de distribution PXE.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Images de démarrage**.  

2. Sélectionnez l'image de démarrage à modifier.  

3. Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4. Sous l’onglet **Source de données** , sélectionnez **Déployer cette image de démarrage depuis le point de distribution PXE**. Pour plus d’informations, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).  



## <a name="BKMK_BootImageLanguage"></a> Configurer plusieurs langues

Les images de démarrage sont indépendantes de la langue. Cette fonctionnalité vous permet d’utiliser une image de démarrage pour afficher le texte de la séquence de tâches dans plusieurs langues en mode WinPE. Ajoutez la prise en charge de langue appropriée à partir de l’onglet **Composants facultatifs** de l’image de démarrage. Ensuite, définissez la variable de séquence de tâches appropriée pour indiquer la langue à afficher. La langue du système d’exploitation déployé est indépendante de la langue de WinPE. La langue que WinPE affiche est déterminée comme suit :  

- Quand un utilisateur exécute la séquence de tâches à partir d’un système d’exploitation existant, Configuration Manager utilise automatiquement la langue configurée pour l’utilisateur. Quand la séquence de tâches est exécutée automatiquement à une échéance de déploiement obligatoire, Configuration Manager utilise la langue du système d’exploitation.  

- Dans le cas des déploiements de système d’exploitation qui utilisent PXE ou un média, définissez la valeur de l’ID de langue dans la variable **SMSTSLanguageFolder**, dans le cadre d'une commande de prédémarrage. Quand l’ordinateur démarre dans WinPE, les messages sont affichés dans la langue que vous avez spécifiée dans la variable. En cas d’erreur durant l’accès au fichier de ressources de langue figurant dans le dossier spécifié, ou si vous ne définissez pas la variable, WinPE affiche les messages dans la langue par défaut.  

    > [!NOTE]  
    > Quand vous protégez le média avec un mot de passe, le texte qui invite l’utilisateur à entrer le mot de passe est toujours affiché dans la langue de WinPE.  

Pour définir la langue de WinPE pour les déploiements PXE ou les déploiements de système d’exploitation établis par un média, suivez la procédure ci-dessous.  

#### <a name="process-to-set-the-windows-pe-language-for-a-pxe-or-media-initiated-os-deployment"></a>Processus pour définir la langue de Windows PE pour un déploiement PXE ou un déploiement de système d'exploitation établi par un média  

1. Avant de mettre à jour l’image de démarrage, vérifiez que le fichier de ressources de séquence de tâche approprié (tsres.dll) se trouve dans le dossier de langue correspondant sur le serveur de site. Par exemple, le fichier de ressources anglais se trouve à l'emplacement suivant : `<ConfigMgrInstallationFolder>\OSD\bin\x64\00000409\tsres.dll`  

2. Dans le cadre de votre commande de prédémarrage, affectez l'ID de langue approprié à la variable d'environnement **SMSTSLanguageFolder**. Vous devez spécifier l'ID de langue au format décimal, et non hexadécimal. Par exemple, pour définir l’ID de langue sur Anglais, spécifiez la valeur décimale **1033** au lieu de la valeur hexadécimale 00000409 du nom de dossier.  
