---
title: Utiliser une séquence de tâches pour gérer des disques durs virtuels
titleSuffix: Configuration Manager
description: Créez et modifiez un disque dur virtuel, ajoutez des applications et des mises à jour logicielles et publiez le disque dur virtuel dans System Center Virtual Machine Manager (VMM) à partir de Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0212b023-804a-4f84-b880-7a59cdb49c67
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 413c2a40e6745cfaa94a99aa2147eacb8ea90f9e
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67516183"
---
# <a name="use-a-task-sequence-to-manage-virtual-hard-disks-in-system-center-configuration-manager"></a>Utiliser une séquence de tâches pour gérer des disques durs virtuels dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


   > [!NOTE] 
   >  La prise en charge de cette fonctionnalité est dépréciée depuis la version 1710. Pour plus d’informations, consultez [Fonctionnalités supprimées et dépréciées pour Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).

Dans System Center Configuration Manager, vous pouvez gérer des disques durs virtuels (VHD) et intégrer les disques durs virtuels créés dans votre centre de données à partir de la console Configuration Manager. Plus précisément, vous pouvez créer et modifier un disque dur virtuel, ajouter des applications et des mises à jour logicielles au disque dur virtuel, ainsi que publier le disque dur virtuel dans System Center Virtual Machine Manager (VMM) à partir de la console Configuration Manager.  

 Pour gérer les disques durs virtuels dans Configuration Manager, utilisez les sections suivantes :

## <a name="prerequisites"></a>Prérequis  
 Vérifiez la configuration requise suivante avant de commencer :  

-   L'ordinateur à partir duquel vous gérez des disques durs virtuels doit exécuter l'un des systèmes d'exploitation suivants :  

    -   Windows 8.1 x64  

    -   Windows 8 x64  

    -   Windows Server 2008 R2  

    -   Windows Server 2012  

    -   Windows Server 2012 R2  

-   La fonction de virtualisation doit être activée dans le BIOS et Hyper-V doit être installé sur l'ordinateur à partir duquel vous exécutez la console Configuration Manager pour gérer les disques durs virtuels. Comme meilleures pratiques, installez également les outils de gestion Hyper-V pour vous aider à tester et résoudre les problèmes liés à vos disques durs virtuels. Par exemple, pour surveiller le fichier smsts.log et suivre la progression de la séquence de tâches dans Hyper-V, les outils de gestion Hyper-V doivent être installés. Pour plus d'informations sur la configuration requise pour Hyper-V, voir [Conditions préalables à l'installation d'Hyper-V](https://technet.microsoft.com/library/cc731898.aspx).  

    > [!IMPORTANT]  
    >  Le processus de création d'un disque dur virtuel consomme du temps de processeur et de la mémoire. Par conséquent, il est recommandé de gérer les disques durs virtuels à partir d'une console Configuration Manager qui ne soit pas installée sur le serveur de site.  

-   Le serveur de site doit disposer de l'autorisation d'accès **Écriture** sur le dossier devant contenir le fichier VHD lorsque vous gérez les disques durs virtuels à partir d'un ordinateur distant du serveur de site.  

-   Vérifiez que vous disposez de suffisamment d'espace disque disponible sur l'ordinateur à partir duquel vous gérez les disques durs virtuels. La configuration requise d'espace de disque dur pour le disque dur virtuel varie en fonction du système d'exploitation et des applications que vous installez.  

-   Vérifiez que vous disposez de suffisamment de mémoire sur l'ordinateur à partir duquel vous gérez les disques durs virtuels. Au cours du processus de création du disque dur virtuel, la machine virtuelle est configurée pour utiliser 2 Go de mémoire.  

-   Installez la console System Center Virtual Machine Manager (VMM) sur l'ordinateur à partir duquel vous téléchargez le disque dur virtuel dans VMM. Vous pouvez installer la console VMM sur un ordinateur distinct à partir duquel vous gérez vos disques durs virtuels, ce qui signifie que vous n'avez pas besoin d'installer Hyper-V pour importer le disque dur virtuel dans VMM.  

    > [!NOTE]  
    >  Si vous installez la console VMM alors que la console Configuration Manager est ouverte, vous devez redémarrer la console Configuration Manager une fois que l'installation de la console VMM est terminée. Dans le cas contraire, Configuration Manager ne se connectera pas correctement au serveur de gestion VMM pour télécharger un disque dur virtuel.  

##  <a name="BKMK_CreateVHDSteps"></a> Étapes de création d'un disque dur virtuel  
 Pour créer un disque dur virtuel, vous devez créer une séquence de tâches qui contient les étapes de création du disque dur virtuel, puis utiliser la séquence de tâches dans l'Assistant Création d'un disque dur virtuel pour créer le disque dur virtuel. Les sections suivantes fournissent les étapes nécessaires pour créer le disque dur virtuel.  

###  <a name="BKMK_CreateTS"></a> Créer une séquence de tâches pour le disque dur virtuel  
 Vous devez créer une séquence de tâches contenant les étapes de création du disque dur virtuel. L'option **Installer un package d'images existant sur un disque dur virtuel** de l'Assistant Création d'une séquence de tâches, vous permet de créer les étapes nécessaires à la création du disque dur virtuel. Par exemple, l’Assistant ajoute les étapes obligatoires suivantes : Redémarrer dans Windows PE, Formater et partitionner le disque, Appliquer le système d’exploitation et Arrêter l’ordinateur. Vous ne pouvez pas créer le disque dur virtuel dans le système d'exploitation complet. De plus, Configuration Manager doit attendre l'arrêt de la machine virtuelle pour pouvoir terminer le package. Par défaut, l'Assistant attend 5 minutes avant d'arrêter la machine virtuelle. Après avoir créé la séquence de tâches, vous pouvez ajouter des étapes supplémentaires si nécessaire.  

> [!IMPORTANT]  
>  La procédure suivante permet de créer la séquence de tâches à l'aide de l'option **Installer un package d'images existant sur un disque dur virtuel** qui inclut automatiquement les étapes nécessaires à la création correcte du disque dur virtuel. Si vous choisissez d'utiliser une séquence de tâches existante ou d'en créer une manuellement, assurez-vous d'ajouter l'étape Arrêter l'ordinateur à la fin de la séquence. Sans cette étape, la machine virtuelle temporaire n'est pas supprimée, et le processus de création du disque dur virtuel ne se termine pas. Toutefois, l'Assistant se termine et signale une réussite.  

 Utilisez la procédure suivante pour créer la séquence de tâches nécessaire à la création du disque dur virtuel :  

#### <a name="to-create-the-task-sequence-to-create-the-vhd"></a>Pour créer la séquence de tâches nécessaire à la création du disque dur virtuel  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4.  Sur la page **Créer une séquence de tâches** , cliquez sur **Installer un package d'images existant sur un disque dur virtuel**, puis cliquez sur **Suivant**.  

5.  Sur la page **Informations sur la séquence de tâches** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Nom de la séquence de tâches**: spécifiez un nom qui identifie la séquence de tâches.  

    -   **Description**: spécifiez une description de la séquence de tâches.  

    -   **Images de démarrage**: spécifiez l'image de démarrage qui installe le système d'exploitation sur l'ordinateur de destination. Pour plus d’informations, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

6.  Sur la page **Installer Windows** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Package d’images :** spécifiez le package qui contient l’image du système d’exploitation à installer.  

    -   **Image**: si le package d’images du système d’exploitation comporte plusieurs images, spécifiez l’index de l’image du système d’exploitation à installer.  

    -   **Clé du produit**: spécifiez la clé de produit pour le système d’exploitation Windows à installer. Vous pouvez spécifier des clés de licence en volume codées et des clés de produit standard. Si vous utilisez une clé de produit non codée, chaque groupe de 5 caractères doit être séparé par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Mode de licence serveur :** spécifiez que la licence serveur est **Par siège**, **Par serveur**ou qu’aucune licence n’est spécifiée. Si la licence serveur est **Par serveur**, spécifiez également le nombre maximal de connexions au serveur.  

    -   Spécifiez comment gérer le compte administrateur qui est utilisé lors du déploiement de l'image du système d'exploitation.  

        -   **Générer de façon aléatoire le mot de passe de l’administrateur local et désactiver le compte sur toutes les plates-formes prises en charge (recommandé)** : utilisez ce paramètre pour permettre à l’Assistant de créer aléatoirement un mot de passe pour le compte administrateur local et désactiver le compte quand l’image du système d’exploitation est déployée.  

        -   **Activer le compte et spécifier le mot de passe de l’administrateur local**: ce paramètre permet d’utiliser un mot de passe spécifique pour le compte d’administrateur local sur tous les ordinateurs où l’image du système d’exploitation est déployée.  

7.  Sur la page **Configurer le réseau** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Joindre un groupe de travail**: indiquez si vous souhaitez ajouter l'ordinateur de destination à un groupe de travail.  

    -   **Joindre un domaine**: indiquez si vous souhaitez ajouter l'ordinateur de destination à un domaine. Dans **Domaine**, spécifiez le nom du domaine.  

        > [!IMPORTANT]  
        >  Vous pouvez rechercher des domaines dans la forêt locale, mais vous devez spécifier le nom de domaine d'une forêt distante.  

         Vous pouvez également spécifier une unité d'organisation (UO). Il s'agit d'un paramètre facultatif qui spécifie le nom unique LDAP X.500 de l'UO dans laquelle vous créez le compte d'ordinateur s'il n'existe pas déjà.  

    -   **Compte**: spécifiez le nom d’utilisateur et le mot de passe du compte qui dispose des autorisations pour joindre le domaine spécifié. Par exemple : *domaine\utilisateur* ou *%variable%* .  

8.  Sur la page **Installer Configuration Manager**, spécifiez le package client Configuration Manager à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**.  

9. Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous spécifiez plusieurs applications, vous pouvez également spécifier que la séquence de tâches continue si l'installation d'une application spécifique échoue.  

10. Effectuez toutes les étapes de l'Assistant.  

###  <a name="BKMK_CreateVHD"></a> Créer un disque dur virtuel  
 Après avoir créé une séquence de tâches pour le disque dur virtuel, utilisez l'Assistant Nouveau disque dur virtuel pour créer le disque dur virtuel.  

> [!IMPORTANT]  
>  Avant d'exécuter cette procédure, vérifiez que vous respectez la configuration requise indiquée au début de cette rubrique.  

 Utilisez la procédure suivante pour créer un disque dur virtuel.  

#### <a name="to-create-a-vhd"></a>Pour créer un disque dur virtuel  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Disques durs virtuels**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un disque dur virtuel** pour démarrer l'Assistant Nouveau disque dur virtuel.  

   > [!NOTE]  
   >  Pour activer l'option **Créer un disque dur virtuel** , Hyper-V doit être installé sur l'ordinateur exécutant la console Configuration Manager à partir de laquelle vous gérez les disques durs virtuels. Pour plus d'informations sur la configuration requise pour Hyper-V, voir [Conditions préalables à l'installation d'Hyper-V](https://technet.microsoft.com/library/cc731898.aspx).  

   > [!TIP]  
   >  Pour organiser vos disques durs virtuels, créez un dossier ou sélectionnez-en un dans le nœud **Disques durs virtuels** , puis cliquez sur **Créer un disque dur virtuel** dans le dossier.  

4. Sur la page **Général** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

   -   **Nom**: spécifiez un nom unique pour le disque dur virtuel.  

   -   **Version**: spécifiez un numéro de version pour le disque dur virtuel. Ce paramètre est facultatif.  

   -   **Commentaire**: spécifiez la description du disque dur virtuel.  

   -   **Chemin d’accès :** spécifiez le chemin et le nom de fichier utilisés par l’Assistant lors de la création du fichier de disque dur virtuel.  

        Vous devez entrer un chemin d'accès réseau valide au format UNC. Par exemple : **\\\nom_serveur\\<nom_partage\>\\<nom_fichier\>.vhd**.  

       > [!WARNING]  
       >  Configuration Manager doit disposer de l'autorisation d'accès **Écriture** vers le chemin spécifié pour créer le disque dur virtuel. Lorsque Configuration Manager ne parvient pas à accéder au chemin, l'erreur associée est consignée dans le fichier distmgr.log sur le serveur de site.  

5. Sur la page **Séquence de tâches** , spécifiez la séquence de tâches que vous avez créée dans la section précédente, puis cliquez sur **Suivant**.  

6. Sur la page **Points de distribution** , sélectionnez un ou plusieurs points de distribution comprenant le contenu requis par la séquence de tâches, puis cliquez sur **Suivant**.  

7. Sur la page **Personnalisation** , cliquez sur **Suivant**. Le processus de création du disque dur virtuel ignore tous les paramètres que vous spécifiez sur cette page.  

8. Vérifiez les paramètres, puis cliquez sur **Suivant**. L'Assistant crée le disque dur virtuel.  

   > [!TIP]
   >  Le temps requis pour compléter le processus de création du disque dur virtuel peut varier. Pendant que l'Assistant effectue ce processus, vous pouvez surveiller les fichiers journaux suivants pour suivre la progression. Par défaut, les fichiers journaux sont situés sur l'ordinateur qui exécute la console Configuration Manager dans %*ProgramFiles(x86)* %\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
   > 
   > - **CreateTSMedia.log**: l’Assistant écrit les informations dans ce fichier journal lors de la création du média de séquence de tâches. Consultez ce fichier journal pour suivre la progression de l'Assistant lors de la création du média autonome.  
   >   -   **DeployToVHD.log**: l’Assistant écrit les informations dans ce fichier journal lors du processus de création du disque dur virtuel. Consultez ce fichier journal pour suivre la progression de l'Assistant sur toutes les étapes après la création du média autonome.  
   > 
   >   Au démarrage de l'installation du système d'exploitation, vous pouvez ouvrir le Gestionnaire Hyper-V (si vous avez installé les outils de gestion Hyper-V sur l'ordinateur) et vous connecter à la machine virtuelle temporaire créé par l'Assistant pour suivre l'exécution de la séquence. À partir de la machine virtuelle, vous pouvez surveiller le fichier smsts.log pour suivre la progression de la séquence de tâches. En cas de problèmes avec de finalisation d'une étape de la séquence de tâches, vous pouvez utiliser ce fichier journal pour résoudre le problème. Le fichier smsts.log se trouve dans x: \windows\temp\smstslog\smsts.log avant le formatage du disque dur et dans c:\\_SMSTaskSequence\Logs\Smstslog\ après le formatage du disque dur. Une fois les étapes de séquence de tâches terminées, la machine virtuelle est arrêtée après 5 minutes (par défaut), puis supprimée.  

   Une fois que Configuration Manager a créé le disque dur virtuel, il est situé dans le nœud **Disques durs virtuels** dans la console Configuration Manager sous le nœud **Déploiement du système d'exploitation** de l'espace de travail **Bibliothèque de logiciels**.  

> [!NOTE]  
>  Configuration Manager récupère la taille du disque dur virtuel en se connectant à l'emplacement source du disque dur virtuel. Si Configuration Manager ne peut pas accéder au fichier de disque dur virtuel, **0** est affiché dans la colonne **Taille (Ko)** pour le disque dur virtuel.  

##  <a name="BKMK_ModifyVHDSteps"></a> Étapes de modification d'un disque dur virtuel existant  
 Pour modifier un disque dur virtuel, vous devez créer une séquence de tâches avec les étapes requises pour modifier le disque dur virtuel. Ensuite, sélectionnez la séquence de tâches dans l'Assistant Modifier un disque dur virtuel. L'Assistant attache le disque dur virtuel à la machine virtuelle, exécute la séquence de tâches dans le disque dur virtuel, puis met à jour le fichier de disque dur virtuel. Les sections suivantes fournissent les étapes nécessaires pour modifier le disque dur virtuel.  

###  <a name="BKMK_ModifyTS"></a> Créer une séquence de tâches pour modifier le disque dur virtuel  
 Pour modifier un disque dur virtuel existant, vous devez d'abord créer une séquence de tâches. Choisissez uniquement les étapes qui sont requises pour modifier la séquence de tâches. Par exemple, si vous voulez ajouter une application au disque dur virtuel, créez une séquence de tâches personnalisée, puis ajoutez uniquement l'étape d'installation de l'application.  

 Utilisez la procédure suivante pour créer la séquence de tâches nécessaire à la modification du disque dur virtuel.  

#### <a name="to-create-a-custom-task-sequence-to-modify-the-vhd"></a>Pour créer une séquence de tâches personnalisée pour modifier le disque dur virtuel  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4. Sur la page **Créer une nouvelle séquence de tâches** , sélectionnez **Créez une séquence de tâches personnalisée**, puis cliquez sur **Suivant**.  

5. Sur la page **Informations sur la séquence de tâches** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

   -   **Nom de la séquence de tâches**: spécifiez un nom qui identifie la séquence de tâches.  

   -   **Description**: spécifiez une description de la séquence de tâches.  

   -   **Images de démarrage**: spécifiez l'image de démarrage qui installe le système d'exploitation sur l'ordinateur de destination. Pour plus d'informations, voir [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

6. Effectuez toutes les étapes de l'Assistant.  

   Utilisez la procédure suivante pour ajouter des étapes de séquence de tâches à la séquence de tâches personnalisée.  

#### <a name="to-add-task-sequence-steps-to-the-custom-task-sequence"></a>Pour ajouter des étapes de séquence de tâches à la séquence de tâches personnalisée  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, cliquez sur **Séquences de tâches**, puis sélectionnez la séquence de tâches personnalisée que vous avez créée au cours de la procédure précédente.  

3.  Dans l'onglet **Accueil** , dans le groupe **Séquence de tâches** , cliquez sur **Modifier** pour démarrer l'éditeur de séquence de tâches.  

4.  Ajoutez les étapes de séquence de tâches à utiliser pour modifier le disque dur virtuel.  

5.  Cliquez sur **OK** pour quitter l'éditeur de séquence de tâches.  

###  <a name="BKMK_ModifyVHD"></a> Modifier un disque dur virtuel  
 Après avoir créé une séquence de tâches pour le disque dur virtuel, utilisez l'Assistant Modifier un disque dur virtuel pour modifier le disque dur virtuel.  

 Utilisez la procédure suivante pour modifier un disque dur virtuel.  

#### <a name="to-modify-a-vhd"></a>Pour modifier un disque dur virtuel  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, cliquez sur **Disques durs virtuels**, puis sélectionnez le disque dur virtuel à modifier.  

3. Dans l'onglet **Accueil** , dans le groupe **Disque dur virtuel** , cliquez sur **Modifier un disque dur virtuel** pour démarrer l'Assistant Modifier un disque dur virtuel.  

   > [!NOTE]  
   >  Pour activer l'option **Modifier un disque dur virtuel** , Hyper-V doit être installé sur l'ordinateur exécutant la console Configuration Manager à partir de laquelle vous gérez les disques durs virtuels. Pour plus d'informations sur la configuration requise pour Hyper-V, voir [Conditions préalables à l'installation d'Hyper-V](https://technet.microsoft.com/library/cc731898.aspx).  

4. Sur la page **Général** , confirmez les paramètres suivants, puis cliquez sur **Suivant**.  

   -   **Nom**: spécifie le nom unique du disque dur virtuel.  

   -   **Version**: spécifie le numéro de version du disque dur virtuel. Ce paramètre est facultatif.  

   -   **Commentaire**: spécifie la description du disque dur virtuel.  

   -   **Chemin d’accès**: spécifie le chemin et le nom du fichier dans lequel se trouve le fichier de disque dur virtuel. Vous ne pouvez pas modifier ce paramètre.  

       > [!WARNING]  
       >  Configuration Manager doit disposer de l'autorisation d'accès **Écriture** vers le chemin spécifié pour créer le disque dur virtuel. Lorsque Configuration Manager ne parvient pas à accéder au chemin, l'erreur associée est consignée dans le fichier distmgr.log sur le serveur de site.  

5. Sur la page **Séquence de tâches** , spécifiez la séquence de tâches personnalisée que vous avez créée dans la section précédente, puis cliquez sur **Suivant**.  

6. Sur la page **Points de distribution** , sélectionnez un ou plusieurs points de distribution comprenant le contenu requis par la séquence de tâches, puis cliquez sur **Suivant**.  

7. Sur la page **Personnalisation** , cliquez sur **Suivant**. Le processus de modification du disque dur virtuel ignore tous les paramètres que vous spécifiez sur cette page.  

8. Vérifiez les paramètres, puis cliquez sur **Suivant**. L'Assistant crée le disque dur virtuel modifié.  

   > [!TIP]
   >  Le temps requis pour effectuer le processus de modification du disque dur virtuel peut varier. Pendant que l'Assistant effectue ce processus, vous pouvez surveiller les fichiers journaux suivants pour suivre la progression. Par défaut, les fichiers journaux sont situés sur l'ordinateur qui exécute la console Configuration Manager dans %*ProgramFiles(x86)* %\Microsoft Configuration Manager\AdminConsole\AdminUILog.  
   > 
   > - **CreateTSMedia.log**: l’Assistant écrit les informations dans ce fichier journal lors de la création du média de séquence de tâches. Consultez ce fichier journal pour suivre la progression de l'Assistant lors de la création du média autonome.  
   >   -   **DeployToVHD.log**: l’Assistant écrit les informations dans ce fichier journal lors du processus de modification du disque dur virtuel. Consultez ce fichier journal pour suivre la progression de l'Assistant sur toutes les étapes après la création du média autonome.  
   > 
   >   Vous pouvez aussi ouvrir le Gestionnaire Hyper-V (si vous avez installé les outils de gestion Hyper-V sur l'ordinateur) et vous connecter à la machine virtuelle temporaire créée par l'Assistant pour suivre l'exécution de la séquence. À partir de la machine virtuelle, vous pouvez surveiller le fichier smsts.log pour suivre la progression de la séquence de tâches. En cas de problèmes avec de finalisation d'une étape de la séquence de tâches, vous pouvez utiliser ce fichier journal pour résoudre le problème. Le fichier smsts.log se trouve dans x: \windows\temp\smstslog\smsts.log avant le formatage du disque dur et dans c:\\_SMSTaskSequence\Logs\Smstslog\ après le formatage du disque dur. Une fois les étapes de séquence de tâches terminées, la machine virtuelle est arrêtée après 5 minutes (par défaut), puis supprimée.  

##  <a name="BKMK_ApplyUpdates"></a> Appliquer des mises à jour logicielles à un disque dur virtuel  
 De nouvelles mises à jour logicielles applicables au système d'exploitation figurant dans votre disque dur virtuel sont régulièrement publiées. Vous pouvez appliquer ces mises à jour logicielles à un disque dur virtuel selon un calendrier défini. Sur le calendrier spécifié, Configuration Manager applique les mises à jour logicielles que vous sélectionnez au disque dur virtuel.  

 Les informations sur le disque dur virtuel sont stockées dans la base de données du site, y compris les mises à jour logicielles qui ont été appliquées au moment de la création du disque dur virtuel. Les mises à jour logicielles appliquées au disque dur virtuel depuis sa création sont également stockées dans la base de données du site. Lorsque vous ouvrez l'Assistant pour appliquer des mises à jour logicielles au disque dur virtuel, l'Assistant récupère une liste des mises à jour logicielles applicables qui n'ont pas encore été appliquées au disque dur virtuel, pour vous permettre de les sélectionner.  

 Vous pouvez sélectionner le paramètre **Continuer en cas d'erreur** pour que Configuration Manager continue à appliquer les mises à jour logicielles lorsqu'une erreur survient lors de l'application d'une ou plusieurs mises à jour logicielles sélectionnées.  

> [!NOTE]  
>  Les mises à jour logicielles sont copiées à partir de la bibliothèque de contenu du serveur de site.  

 Pour appliquer des mises à jour logicielles à un disque dur virtuel, suivez la procédure ci-dessous.  

#### <a name="to-apply-software-updates-to-a-vhd"></a>Pour appliquer des mises à jour logicielles à un disque dur virtuel  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Disques durs virtuels**.  

3.  Sélectionnez le disque dur virtuel auquel appliquer les mises à jour logicielles.  

4.  Dans l'onglet **Accueil** , dans le groupe **Disque dur virtuel** , cliquez sur **Planifier les mises à jour** pour démarrer l'Assistant.  

5.  Sur la page **Choisir des mises à jour** , sélectionnez les mises à jour logicielles à appliquer au disque dur virtuel, puis cliquez sur **Suivant**.  

6.  Sur la page **Définir le calendrier** , spécifiez les paramètres suivants, puis cliquez sur **Suivant**.  

    1.  **Calendrier**: définissez le calendrier d’application des mises à jour logicielles au disque dur virtuel.  

    2.  **Continuer en cas d’erreur**: sélectionnez cette option pour continuer à appliquer les mises à jour logicielles à l’image même si une erreur survient.  

7.  Vérifiez les informations figurant sur la page **Résumé** , puis cliquez sur **Suivant**.  

8.  Sur la page **Dernière étape** , vérifiez que les mises à jour logicielles ont été correctement appliquées à l'image de système d'exploitation.  

##  <a name="BKMK_ImportToVMM"></a> Importer le disque dur virtuel vers System Center Virtual Machine Manager  
 System Center VMM est une solution de gestion du centre de données virtualisé, vous permettant de configurer et de gérer vos ordinateurs hôtes de virtualisation, la mise en réseau et les ressources de stockage pour créer et déployer des ordinateurs virtuels et des services vers des clouds privés que vous avez créés. Après avoir créé un disque dur virtuel dans Configuration Manager, vous pouvez importer et gérer votre disque dur virtuel à l'aide de VMM.  

> [!TIP]  
>  Avant de télécharger un disque dur virtuel dans VMM, vérifiez que la console VMM se connecte correctement au serveur de gestion VMM.  

 Utilisez la procédure suivante pour importer un disque dur virtuel dans VMM.  

#### <a name="to-import-a-vhd-to-vmm"></a>Pour importer un disque dur virtuel dans VMM  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Disques durs virtuels**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Disque dur virtuel** , cliquez sur **Télécharger vers Virtual Machine Manager** pour démarrer l'Assistant Téléchargement vers Virtual Machine Manager.  

4.  Sur la page **Général** , configurez les paramètres suivants, puis cliquez sur **Suivant**.  

    -   **Nom du serveur VMM :** spécifiez le nom de domaine complet de l’ordinateur sur lequel est installé le serveur de gestion VMM. L'Assistant se connecte au serveur de gestion VMM pour télécharger les partages de bibliothèque pour le serveur.  

    -   **Partage de bibliothèque VMM**: spécifiez le partage de bibliothèque VMM dans la liste déroulante.  

    -   **Utilisez un transfert non chiffré**: sélectionnez ce paramètre pour transférer le fichier de disque dur virtuel sur le serveur de gestion VMM sans utiliser de chiffrement.  

5.  Sur la page Synthèse, vérifiez les paramètres, puis terminez l'Assistant. Le temps de téléchargement du disque dur virtuel peut varier en fonction de la taille du fichier VHD et de la bande passante réseau vers le serveur de gestion VMM.  
