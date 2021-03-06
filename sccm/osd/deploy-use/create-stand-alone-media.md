---
title: "Créer un média autonome avec System Center Configuration Manager | Documents Microsoft"
description: "Utilisez un média autonome pour déployer le système d’exploitation sur un ordinateur sans connexion à un site Configuration Manager ou utilisant le réseau."
ms.custom: na
ms.date: 12/21/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c6b9ccd2-78d9-4f0e-b25a-70d0866300ba
caps.latest.revision: 21
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 66cd6d099acdd9db2bc913a69993aaf5e17237fe
ms.openlocfilehash: 411ca1d13778521f7fa0dba71980158477cd0735


---
# <a name="create-stand-alone-media-with-system-center-configuration-manager"></a>Créer un média autonome avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un média autonome dans Configuration Manager contient tout ce qui est nécessaire pour déployer le système d’exploitation sur un ordinateur sans connexion à un site Configuration Manager ou utilisant le réseau. Utilisez un média autonome avec les scénarios de déploiement de système d’exploitation suivants :  

-   [Actualiser un ordinateur existant avec une nouvelle version de Windows](refresh-an-existing-computer-with-a-new-version-of-windows.md)  

-   [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Effectuer une mise à niveau de Windows vers la dernière version](upgrade-windows-to-the-latest-version.md)  

 Le média autonome inclut la séquence de tâches qui automatise la procédure d’installation du système d’exploitation et tout autre contenu nécessaire, notamment l’image de démarrage, l’image du système d’exploitation et les pilotes de périphérique. Étant donné que tous les éléments nécessaires au déploiement du système d’exploitation sont stockés sur le média autonome, l’espace disque requis pour le média autonome est beaucoup plus important que l’espace disque requis pour d’autres types de média. Lorsque vous créez un média autonome sur un site d’administration centrale, le client récupère le code de site qui lui est attribué à partir d’Active Directory. Le média autonome créé sur les sites enfants attribue automatiquement au client le code de site pour ce site.  

##  <a name="a-namebkmkcreatestandalonemediaa-create-stand-alone-media"></a><a name="BKMK_CreateStandAloneMedia"></a> Créer un média autonome  
 Avant de créer un média autonome à l’aide de l’Assistant Création d’un média de séquence de tâches, vérifiez que les conditions suivantes sont remplies :  

### <a name="create-a-task-sequence-to-deploy-an-operating-system"></a>Créer une séquence de tâches pour déployer un système d’exploitation
Dans le cadre du média autonome, vous devez spécifier la séquence de tâches destinée à déployer un système d’exploitation. Pour connaître les étapes permettant de créer une séquence de tâches, consultez [Créer une séquence de tâches pour installer un système d’exploitation dans System Center Configuration Manager](create-a-task-sequence-to-install-an-operating-system.md).

Les actions suivantes ne sont pas prises en charge pour le média autonome :
- Étape Appliquer automatiquement les pilotes dans la séquence de tâches. L’application automatique des pilotes de périphérique présents dans le catalogue de pilotes n’est pas prise en charge, mais vous pouvez choisir l’étape Appliquer le package de pilotes pour mettre à la disposition du programme d’installation de Windows un ensemble de pilotes spécifique.
- Étape Télécharger le contenu du package dans la séquence de tâches. Les informations de point de gestion ne sont pas disponibles sur un média autonome. Par conséquent, l’étape échoue lors de la tentative d’énumération des emplacements de contenu.
- Installation de mises à jour logicielles.
- Installation du logiciel avant le déploiement du système d’exploitation.
- Séquences de tâches pour les déploiements autres que les déploiements de système d’exploitation.
- Association d'utilisateurs à l'ordinateur de destination pour prendre en charge l'affinité entre appareil et utilisateur.
- Le package dynamique s'installe via la tâche Installer les packages.
- L'application dynamique s'installe via la tâche Installer l'application.

Si votre séquence de tâches servant à déployer un système d’exploitation comprend l’étape [Installer le package](../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) et que vous créez le média autonome sur un site d’administration centrale, une erreur peut se produire. Le site d'administration centrale ne dispose pas des stratégies de configuration de client requises pour activer l'agent de distribution logicielle au cours de l'exécution de la séquence de tâches. L’erreur suivante peut apparaître dans le fichier CreateTsMedia.log :<br /><br /> "WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"<br /><br /> Dans le cas d’un média autonome qui comprend une étape **Installer le package**, vous devez créer le média autonome sur un site principal sur lequel l’agent de distribution logicielle est activé ou ajouter une étape [Exécuter la ligne de commande](../understand/task-sequence-steps.md#BKMK_RunCommandLine) après l’étape [Configurer Windows et ConfigMgr](../understand/task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr) et avant la première étape **Installer le package** de la séquence de tâches. L'étape **Exécuter la ligne de commande** exécute une commande de ligne de commande WMIC pour activer l'agent de distribution logicielle avant l'exécution de la première étape Installer le package. Vous pouvez utiliser la ligne de commande suivante dans l'étape **Exécuter la ligne de commande** de votre séquence de tâches :<br /><br />
```WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE
```

### Distribute all content associated with the task sequence
You must distribute all content that is required by the task sequence the  to at least one distribution point. This includes the boot image, operating system image, and other associated files. The wizard gathers the information from the distribution point when it creates the stand-alone media. You must have **Read** access rights to the content library on that distribution point.  For details, see [Distribute content referenced by a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS).

### Prepare the removable USB drive
*For a removable USB drive:*

If you are going to use a removable USB drive, the USB  drive must be connected to the computer where the wizard is run and the USB drive must be detectable by Windows as a removal device. The wizard writes directly to the USB drive when it creates the media. Stand-alone media uses a FAT32 file system. You cannot create stand-alone media on a USB flash drive whose content contains a file over 4 GB in size.

### Create an output folder
*For a CD/DVD set:*

Before you run the Create Task Sequence Media Wizard to create media for a CD or DVD set, you must create a folder for the output files created by the wizard. Media that is created for a CD or DVD set is written as .iso files directly to the folder.


 Use the following procedure to create stand-alone media for a removable USB drive or a CD/DVD set.  

## To create stand-alone media  

1.  In the Configuration Manager console, click **Software Library**.  

2.  In the **Software Library** workspace, expand **Operating Systems**, and then click **Task Sequences**.  

3.  On the **Home** tab, in the **Create** group, click **Create Task Sequence Media** to start the Create Task Sequence Media Wizard.  

4.  On the **Select Media Type** page, specify the following options, and then click **Next**.  

    -   Select **Stand-alone media**.  

    -   Optionally, if you want to allow the operating system to be deployed without requiring user input, select **Allow unattended operating system deployment**. When you select this option the user is not prompted for network configuration information or for optional task sequences. However, the user is still prompted for a password if the media is configured for password protection.  

5.  On the **Media Type** page, specify whether the media is a flash drive or a CD/DVD set, and then click configure the following:  

    > [!IMPORTANT]  
    >  Stand-alone media uses a FAT32 file system. You cannot create stand-alone media on a USB flash drive whose content contains a file over 4 GB in size.  

    -   If you select **USB flash drive**, specify the drive where you want to store the content.  

    -   If you select **CD/DVD set**, specify the capacity of the media and the name and path of the output files. The wizard writes the output files to this location. For example: **\\\servername\folder\outputfile.iso**  

         If the capacity of the media is too small to store the entire content, multiple files are created and you must store the content on multiple CDs or DVDs. When multiple media is required, Configuration Manager adds a sequence number to the name of each output file that it creates. In addition, if you deploy an application along with the operating system and the application cannot fit on a single media, Configuration Manager stores the application across multiple media. When the stand-alone media is run, Configuration Manager prompts the user for the next media where the application is stored.  

        > [!IMPORTANT]  
        >  If you select an existing .iso image, the Task Sequence Media Wizard deletes that image from the drive or share as soon as you proceed to the next page of the wizard. The existing image is deleted, even if you then cancel the wizard.  

     Click **Next**.  

6.  On the **Security** page, enter a strong password to help protect the media, and then click **Next**. If you specify a password, the password is required to use the media.  

    > [!IMPORTANT]  
    >  On stand-alone media, only the task sequence steps and their variables are encrypted. The remaining content of the media is not encrypted, so do not include any sensitive information in task sequence scripts. Store and implement all sensitive information by using task sequence variables.  

7.  On the **Stand-Alone CD/DVD** page, specify the task sequence that deploys the operating system, and then click **Next**. Choose **Detect associated application dependencies and add them to this media** to add content to the stand-alone media for application dependencies.
> [!TIP]
> If you do not see expected application dependencies, deselect and then reselect the **Detect associated application dependencies and add them to this media** setting to refresh the list.

The wizard lets you select only those task sequences that are associated with a boot image.  

8.  On the **Distribution Points** page, specify the distribution points that contain the content required by the task sequence, and then click **Next**.  

     Configuration Manager will only display distribution points that have the content. You must distribute all of the content associated with the task sequence (boot image, operating system image, etc.) to at least one distribution point before you can continue. After you distribute the content, you can either restart the wizard or remove any distribution points that you already selected  on this page, go to the previous page, and then back to the **Distribution Points** page to refresh the distribution point list. For more information about distributing content, see [Distribute content referenced by a task sequence](manage-task-sequences-to-automate-tasks.md#BKMK_DistributeTS). For more information about distribution points and content management, see [Manage content and content infrastructure for System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

    > [!NOTE]  
    >  You must have **Read** access rights to the content library on the distribution points.  

9. On the **Customization** page, specify the following information, and then click **Next**.  

    -   Specify the variables that the task sequence uses to deploy the operating system.  

    -   Specify any prestart commands that you want to run before the task sequence. Prestart commands are a script or an executable that can interact with the user in Windows PE before the task sequence runs to install the operating system. For more information about prestart commands for media, see [Prestart commands for task sequence media in System Center Configuration Manager](../understand/prestart-commands-for-task-sequence-media.md).  

         Optionally, select **Files for the prestart command** to include any required files for the prestart command.  

        > [!TIP]  
        >  During task sequence media creation, the task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the CreateTSMedia.log log file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.  

10. Complete the wizard.  

 The stand-alone media files (.iso) are created in the destination folder. If you selected **Stand-Alone CD/DVD**, you can now copy the output files to a set of CDs or DVDs.  

##  <a name="BKMK_StandAloneMediaTSExample"></a> Example task sequence for stand-alone media  
 Use the following table as a guide as you create a task sequence to deploy an operating system using stand-alone media. The table will help you decide the general sequence for your task sequence steps and how to organize and structure those task sequence steps into logical groups. The task sequence that you create might vary from this sample and can contain more or fewer task sequence steps and groups.  

> [!NOTE]  
>  You must always use the Task Sequence Media Wizard to create stand-alone media.  

|Task Sequence Group or Step|Description|  
|---------------------------------|-----------------|  
|Capture File and Settings - **(New Task Sequence Group)**|Create a task sequence group. A task sequence group keeps similar task sequence steps together for better organization and error control.|  
|Capture Windows Settings|Use this task sequence step to identify the Microsoft Windows settings that are captured from the existing operating system on the destination computer prior to reimaging. You can capture the computer name, user and organizational information, and the time zone settings.|  
|Capture Network Settings|Use this task sequence step to capture network settings from the computer that receives the task sequence. You can capture the domain or workgroup membership of the computer and the network adapter setting information.|  
|Capture User Files and Settings - **(New Task Sequence Sub-Group)**|Create a task sequence group within a task sequence group. This sub-group contains the steps needed to capture user state data from the existing operating system on the destination computer prior to reimaging. Similar to the initial group that you added, this sub-group keeps similar task sequence steps together for better organization and error control.|  
|Set Local State Location|Use this task sequence step to specify a local location using the protected path task sequence variable. The user state is stored on a protected directory on the hard drive.|  
|Capture User State|Use this task sequence step to capture the user files and settings you want to migrate to the new operating system.|  
|Install Operating System - **(New Task Sequence Group)**|Create another task sequence sub-group. This sub-group contains the steps needed to install the operating system.|  
|Reboot to Windows PE or hard disk|Use this task sequence step to specify restart options for the computer that receives this task sequence. This step will display a message to the user indicating that the computer will be restarted so that the installation can continue.<br /><br /> This step uses the read-only **_SMSTSInWinPE** task sequence variable. If the associated value equals **false** the task sequence step will continue.|  
|Apply Operating System|Use this task sequence step to install the operating system image onto the destination computer. This step deletes all files on that volume (with the exception of Configuration Manager-specific control files) and then applies all volume images contained in the WIM file to the corresponding sequential disk volume. You can also specify a **sysprep** answer file to configure which disk partition to use for the installation.|  
|Apply Windows Settings|Use this task sequence step to configure the Windows settings configuration information for the destination computer. The windows settings you can apply are user and organizational information, product or license key information, time zone, and the local administrator password.|  
|Apply Network Settings|Use this task sequence step to specify the network or workgroup configuration information for the destination computer. You can also specify if the computer uses a DHCP server or you can statically assign the IP address information.|  
|Apply Driver Package|Use this task sequence step to make all device drivers in a driver package available for use by Windows setup. All necessary device drivers must be contained on the stand-alone media.|  
|Setup Operating System - **(New Task Sequence Group)**|Create another task sequence sub-group. This sub-group contains the steps needed to install the Configuration Manager client.|  
|Setup Windows and ConfigMgr|Use this task sequence step to install the Configuration Manager client software. Configuration Manager installs and registers the Configuration Manager client GUID. You can assign the necessary installation parameters in the **Installation properties** window.|  
|Restore User Files and Settings - **(New Task Sequence Group)**|Create another task sequence sub-group. This sub-group contains the steps needed to restore the user state.|  
|Restore User State|Use this task sequence step to initiate the User State Migration Tool (USMT) to restore the user state and settings that were captured from the Capture User State Action to the destination computer.|  



<!--HONumber=Dec16_HO4-->


