---
title: Créer un média autonome
titleSuffix: Configuration Manager
description: Utilisez un média autonome pour déployer le système d’exploitation sur un ordinateur sans connexion réseau.
ms.date: 02/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 35dd110c2566dab945bb0701e113becb3412d65c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351942"
---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Créer un média autonome avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un média autonome dans Configuration Manager contient tous les éléments requis pour déployer le système d’exploitation sur un ordinateur sans connexion réseau. Utilisez un média autonome avec les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md)  

Le média autonome inclut la séquence de tâches qui automatise les étapes d’installation du système d’exploitation, ainsi que tout autre contenu nécessaire. Ce contenu comprend l’image de démarrage, l’image de système d’exploitation et les pilotes de périphériques. Étant donné que le média autonome stocke tous les éléments nécessaires pour déployer le système d’exploitation, il exige davantage d’espace disque que d’autres types de médias. Quand vous créez un média autonome sur un site d’administration centrale, le client récupère le code de site qui lui est attribué à partir d’Active Directory. Le média autonome créé sur les sites enfants attribue automatiquement au client le code de site pour ce site.  

##  <a name="BKMK_CreateStandAloneMedia"></a> Créer un média autonome  
Avant de créer un média autonome à l’aide de l’Assistant Création d’un média de séquence de tâches, vérifiez que les conditions suivantes sont remplies :  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Créer une séquence de tâches pour déployer un système d’exploitation
Dans le cadre du média autonome, vous devez spécifier la séquence de tâches destinée à déployer un système d’exploitation. Pour connaître les étapes permettant de créer une séquence de tâches, consultez [Créer une séquence de tâches pour installer un système d’exploitation dans System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Les actions suivantes ne sont pas prises en charge pour le média autonome :
- Étape **Appliquer automatiquement les pilotes** dans la séquence de tâches. Le média autonome ne prend pas en charge l’application automatique de pilotes de périphériques à partir du catalogue de pilotes. Utilisez l’étape **Appliquer le package de pilotes** afin de rendre un ensemble de pilotes spécifique accessible au programme d’installation de Windows.
- Étape **Télécharger le contenu du package** dans la séquence de tâches. Les informations de point de gestion ne sont pas disponibles sur un média autonome. Par conséquent, l’étape échoue lors de la tentative d’énumération des emplacements de contenu.
- Installation de mises à jour logicielles.
- Installation du logiciel avant le déploiement du système d’exploitation.
- Séquences de tâches pour les déploiements autres que les déploiements de système d’exploitation.
- Association d'utilisateurs à l'ordinateur de destination pour prendre en charge l'affinité entre appareil et utilisateur.
- Le package dynamique s’installe par le biais de la tâche **Installer les packages**.
- L’application dynamique s’installe par le biais de la tâche **Installer l’application**.

> [!NOTE]    
> Une erreur peut se produire si votre séquence de tâches comprend l’étape [Installer le package](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) et que vous créez le média autonome sur un site d’administration centrale. Le site d’administration centrale ne dispose pas des stratégies de configuration du client nécessaires. Ces stratégies sont obligatoires afin d’activer l’agent de distribution logicielle pendant l’exécution de la séquence de tâches. L’erreur suivante peut apparaître dans le fichier CreateTsMedia.log :    
>     
> `WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)`    
> 
> Pour un média autonome qui inclut une étape **Installer le package**, créez le média autonome sur un site principal où l’agent de distribution logicielle est activé. 
>
> Vous pouvez aussi ajouter une étape [Exécuter la ligne de commande](../understand/task-sequence-steps.md#BKMK_RunCommandLine) après l’étape [Configurer Windows et ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) et avant la première étape **Installer le package** dans la séquence de tâches. L’étape **Exécuter la ligne de commande** exécute la commande WMIC suivante pour activer l’agent de distribution logicielle avant la première étape Installer le package :    
>    
> `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`


> [!IMPORTANT]    
> Ne sélectionnez pas le paramètre **Utiliser le package client de préproduction quand il est disponible** dans l’étape de séquence de tâches **Configurer Windows et ConfigMgr** pour le média autonome. Un média autonome ne prend pas en charge l’utilisation de ce paramètre. Pour plus d’informations sur ce paramètre, consultez [Configurer Windows et ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).


### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuer tout le contenu associé à la séquence de tâches
Distribuez tout le contenu exigé par la séquence de tâches à au moins un point de distribution. Ce contenu inclut l’image de démarrage, l’image du système d’exploitation et les autres fichiers associés. L'Assistant collecte les informations à partir du point de distribution lorsqu'il crée le média autonome. Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur ce point de distribution. Pour plus d’informations, consultez [Distribuer du contenu référencé par une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### <a name="prepare-the-removable-usb-drive"></a>Préparer le lecteur USB amovible
*Lecteur USB amovible :*

Si vous utilisez un lecteur USB amovible, connectez le lecteur USB à l’ordinateur sur lequel est exécuté l’Assistant. Le lecteur USB doit être détectable par Windows en tant qu’appareil amovible. L’Assistant écrit directement sur le lecteur USB quand il crée le média. Le média autonome utilise un système de fichiers FAT32. Vous ne pouvez pas créer de média autonome sur un disque mémoire flash USB dont le contenu inclut un fichier d'une taille supérieure à 4 Go.

### <a name="create-an-output-folder"></a>Créer un dossier de sortie
*Ensemble de CD/DVD :*

Avant d'exécuter l'Assistant Création d'un média de séquence de tâches afin de créer un média pour un ensemble de CD ou DVD, vous devez créer un dossier pour les fichiers de sortie créés par l'Assistant. Le média créé pour un ensemble de CD ou DVD est écrit sous forme de fichiers .iso directement dans le dossier.


 Utilisez la procédure suivante pour créer un média autonome pour un lecteur USB amovible ou un ensemble de CD/DVD.  

## <a name="to-create-stand-alone-media"></a>Pour créer un média autonome  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4.  Sur la page **Sélectionner le type de média** , spécifiez les options suivantes, puis cliquez sur **Suivant**.  

    -   Sélectionnez **Média autonome**.  

    -   Éventuellement, si vous souhaitez autoriser le déploiement du système d'exploitation sans intervention de l'utilisateur, sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome**. Lorsque vous sélectionnez cette option, l'utilisateur n'est pas invité à fournir des informations de configuration réseau ou des séquences de tâches facultatives. Si le média est configuré avec une protection par mot de passe, l’utilisateur est quand même invité à fournir un mot de passe.  

5.  Dans la page **Type de média**, spécifiez s’il s’agit d’un lecteur USB amovible ou d’un ensemble CD/DVD :  

    > [!IMPORTANT]  
    >  Par défaut, le média autonome utilise un système de fichiers FAT32. Vous ne pouvez pas créer de média autonome sur un lecteur USB amovible dont le contenu inclut un fichier d’une taille supérieure à 4 Go.  

    -   Si vous sélectionnez **Lecteur USB amovible**, spécifiez le lecteur sur lequel stocker le contenu.  

        - **Formater le lecteur USB amovible (FAT32) et le rendre démarrable** : par défaut, laisser Configuration Manager préparer le lecteur USB. De nombreux appareils UEFI récents nécessitent une partition FAT32 amorçable. Toutefois, ce format limite également la taille des fichiers et la capacité globale du lecteur. Si vous avez déjà formaté et configuré le lecteur amovible, désactivez cette option. 

    -   Si vous sélectionnez **Ensemble CD/DVD**, spécifiez la capacité du média et le nom et le chemin d'accès des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Par exemple : **\\\nom_serveur\dossier\fichier_sortie.iso**  

         Si la capacité du média est insuffisante pour stocker l’ensemble du contenu, plusieurs fichiers sont créés et vous devez stocker le contenu sur plusieurs CD ou DVD. Quand plusieurs médias sont nécessaires, Configuration Manager ajoute un numéro de séquence au nom de chaque fichier de sortie qu’il crée. De plus, si vous déployez une application en même temps que le système d’exploitation et que cette application ne peut pas tenir sur un seul média, Configuration Manager stocke l’application sur plusieurs médias. Quand le média autonome est exécuté, Configuration Manager invite l’utilisateur à insérer le média suivant sur lequel l’application est stockée.   

         > [!IMPORTANT]  
         >  Si vous sélectionnez une image .iso existante, l'Assistant Média de séquence de tâches supprime cette image du lecteur ou du partage dès lors que vous passez à la page suivante de l'Assistant. L'image existante est supprimée même si vous annulez ensuite l'Assistant.  

     Cliquez sur **Suivant**.  

6.  Sur la page **Sécurité**, choisissez parmi les paramètres suivants, puis cliquez sur **Suivant** :
    - **Protéger le média à l’aide d’un mot de passe** : entrez un mot de passe fort pour protéger le média. Si vous spécifiez un mot de passe, celui-ci est requis pour utiliser le média.  

        > [!IMPORTANT]  
        >  Sur un média autonome, seules les étapes de séquence de tâches et leurs variables sont chiffrées. Le reste du contenu du média n'est pas chiffré, donc n'incluez pas d'informations sensibles dans les scripts de séquence de tâches. Stockez et mettez en œuvre toutes les informations sensibles en utilisant des variables de séquence de tâches.  

    - **Sélectionner une plage de dates pour que le média autonome soit valide** (à partir de la version 1702) : définissez des dates de début et d’expiration facultatives sur le média. Ces paramètres sont désactivés par défaut. Les dates sont comparées à l’heure système de l’ordinateur avant l’exécution du support autonome. Lorsque l’heure du système est antérieure à l’heure de début ou ultérieure à l’heure d’expiration, le support autonome n’est pas démarré. Ces options sont également disponibles avec l’applet de commande New-CMStandaloneMedia PowerShell.
7.  Sur la page **CD/DVD autonome** , spécifiez la séquence de tâches qui déploie le système d'exploitation, puis cliquez sur **Suivant**. Pour ajouter du contenu au média autonome pour les dépendances d’application, choisissez **Détecter les dépendances d’application associées et les ajouter à ce média**.
    > [!TIP]
    > Si les dépendances d’application attendues ne s’affichent pas, désélectionnez, puis sélectionnez à nouveau le paramètre **Détecter les dépendances d’application associées et les ajouter à ce média** pour actualiser la liste.

    L'Assistant vous permet de sélectionner uniquement les séquences de tâches qui sont associées à une image de démarrage.  

8. Sur la page **Sélectionner une application** (disponible à partir de la version 1702), spécifiez le contenu d’application à inclure dans le fichier du média, puis cliquez sur **Suivant**.
9. Sur la page **Sélectionner un package** (disponible à partir de la version 1702), spécifiez le contenu de package à inclure dans le fichier du média, puis cliquez sur **Suivant**.
10. Sur la page **Sélectionner le package de pilotes** (disponible à partir de la version 1702), spécifiez le contenu de package de pilotes à inclure dans le fichier du média, puis cliquez sur **Suivant**.
11.  Dans la page **Points de distribution**, spécifiez les points de distribution où se trouve le contenu requis, puis cliquez sur **Suivant**.  

     Configuration Manager n’affiche que les points de distribution qui disposent du contenu. Distribuez tout le contenu associé à la séquence de tâches sur au moins un point de distribution avant de continuer. Après avoir distribué le contenu, actualisez la liste des points de distribution. Supprimez les points de distribution que vous avez déjà sélectionnés dans cette page, accédez à la page précédente, puis revenez à la page **Points de Distribution**. Vous pouvez également redémarrer l’Assistant. Pour plus d’informations, consultez [Distribuer du contenu référencé par une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS) et [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur les points de distribution.  

12. Sur la page **Personnalisation** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Spécifiez les variables que la séquence de tâches utilise pour déployer le système d'exploitation.  

    -   Spécifiez les commandes de prédémarrage que vous voulez exécuter avant la séquence de tâches. Les commandes de prédémarrage sont un script ou un exécutable qui s’exécute dans Windows PE avant le démarrage de la séquence de tâches. Pour plus d’informations, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](../understand/prestart-commands-for-task-sequence-media.md).  

         Si vous le souhaitez, sélectionnez **Inclure les fichiers pour la commande de prédémarrage** pour inclure tous les fichiers requis pour la commande de prédémarrage.  

        > [!TIP]  
        >  Lors de la création du média de séquence de tâches, Configuration Manager écrit l’ID du package et la ligne de commande de prédémarrage dans le fichier journal **CreateTSMedia.log** sur l’ordinateur qui exécute la console Configuration Manager. Cette sortie inclut la valeur des variables de séquence de tâches. Consultez ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

13. Effectuez toutes les étapes de l'Assistant.  

 Les fichiers de média autonome (.iso) sont créés dans le dossier de destination. Si vous avez sélectionné **CD/DVD autonome**, vous pouvez maintenant copier les fichiers de sortie sur un ensemble de CD ou DVD.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Exemple de séquence de tâches pour un média autonome  
 Pour créer une séquence de tâches afin de déployer un système d’exploitation à l’aide d’un média autonome, utilisez le tableau suivant comme guide. Le tableau vous aide à décider de la séquence générale pour vos étapes de séquence de tâches. Il aide également à organiser et à structurer les étapes de séquence de tâches en groupes logiques. La séquence de tâches que vous créez peut être différente de celle de cet exemple, et elle peut contenir un nombre de groupes et d'étapes de séquence de tâches plus ou moins important.  

> [!NOTE]  
>  Vous devez toujours utiliser l'Assistant Média de séquence de tâches pour créer un média autonome.  

|Groupe ou étape de séquence de tâches|Description|  
|---------------------------------|-----------------|  
|Capturer les fichiers et les paramètres - **(Nouveau groupe de séquences de tâches)**|Créez un groupe de séquences de tâches. Un groupe de séquences de tâches regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.|  
|Capturer les paramètres Windows|Utilisez cette étape de séquence de tâches pour capturer les paramètres Windows à partir de l’ordinateur de destination avant de créer de nouvelles images. Capturez le nom de l’ordinateur, les informations utilisateur et organisationnelles et les paramètres des fuseaux horaires.|  
|Capturer les paramètres réseau|Utilisez cette étape de séquence de tâches pour capturer les paramètres réseau à partir de l'ordinateur qui reçoit la séquence de tâches. Vous pouvez capturer l'appartenance au domaine ou au groupe de travail de l'ordinateur et les informations du paramètre de la carte réseau.|  
|Capturer les paramètres et fichiers utilisateur  **(Nouveau sous-groupe de séquences de tâches)**|Créez un groupe de séquences de tâches au sein d'un groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la capture des données d’état utilisateur à partir de l’ordinateur de destination avant de créer de nouvelles images. Comme le groupe initial que vous avez ajouté, ce sous-groupe regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.|  
|Définir l'emplacement d'état local|Utilisez cette étape de séquence de tâches pour spécifier un emplacement local à l'aide de la variable de séquence de tâches du chemin protégé. L'état utilisateur est stocké dans un répertoire protégé sur le disque dur.|  
|Capturer l'état utilisateur|Utilisez cette étape de séquence de tâches pour capturer les fichiers et paramètres utilisateur que vous souhaitez migrer sur le nouveau système d'exploitation.|  
|Installer le système d'exploitation - **(Nouveau groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à l’installation du système d’exploitation.|  
|Redémarrer sur Windows PE ou disque dur|Utilisez cette étape de séquence de tâches pour spécifier les options de redémarrage pour l'ordinateur qui reçoit cette séquence de tâches. Cette étape affiche un message pour signaler à l’utilisateur que l’ordinateur va redémarrer afin de poursuivre l’installation.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSInWinPE** en lecture seule. Si la valeur associée est **false**, l’étape de séquence de tâches se poursuit.|  
|Appliquer le système d'exploitation|Utilisez cette étape de séquence de tâches pour installer une image de système d'exploitation sur l'ordinateur de destination. Cette étape supprime tous les fichiers sur ce volume, sauf les fichiers de contrôle propres à Configuration Manager. Elle applique ensuite toutes les images de volume contenues dans le fichier WIM au volume de disque séquentiel correspondant. Vous pouvez également spécifier un fichier de réponse **sysprep** pour configurer la partition de disque à utiliser pour l’installation.|  
|Appliquer les paramètres Windows|Utilisez cette étape de séquence de tâches pour configurer les informations de configuration des paramètres Windows pour l'ordinateur de destination. Ces paramètres comprennent les informations utilisateur et organisationnelles, les informations sur la clé de produit ou de licence, les fuseaux horaires et le mot passe administrateur local.|  
|Appliquer les paramètres réseau|Utilisez cette étape de séquence de tâches pour spécifier les informations de configuration du réseau ou du groupe de travail pour l'ordinateur de destination. Vous pouvez également indiquer si l'ordinateur utilise un serveur DHCP ou vous pouvez attribuer en mode statique les informations de l'adresse IP.|  
|Appliquer le package de pilotes|Utilisez cette étape de séquence de tâches pour que tous les pilotes de périphérique d'un package de pilotes puissent être utilisés par le programme d'installation de Windows. Tous les pilotes de périphériques nécessaires doivent être contenus sur le média autonome.|  
|Configurer le système d'exploitation - **(Nouveau groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à l’installation du client Configuration Manager.|  
|Configurer Windows et ConfigMgr|Cette étape de séquence de tâches permet d’installer le logiciel client Configuration Manager. Configuration Manager installe et inscrit le GUID du client Configuration Manager. Vous pouvez définir les paramètres d'installation nécessaires à partir de la fenêtre **Propriétés d'installation** .|  
|Restaurer les fichiers et paramètres utilisateur - **(Nouveau sous-groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la restauration de l’état utilisateur.|  
|Restaurer l'état utilisateur|Utilisez cette étape de séquence de tâches pour lancer l’Outil de migration utilisateur Windows (USMT). L’outil USMT restaure l’état utilisateur et les paramètres, précédemment capturés à l’étape Capturer l’état utilisateur, sur l’ordinateur de destination.|  
