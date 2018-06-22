---
title: Créer une séquence de tâches pour capturer un système d’exploitation
titleSuffix: Configuration Manager
description: Une séquence de tâches de création et de capture génère un ordinateur de référence qui peut inclure des pilotes et des mises à jour logicielles spécifiques en même temps que le système d’exploitation.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 25e4ac68-0e78-4bbe-b8fc-3898b372c4e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1ef2883bfeb61df55ff045b76e9bc45a11b4da2
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352167"
---
# <a name="create-a-task-sequence-to-capture-an-operating-system-in-system-center-configuration-manager"></a>Créer une séquence de tâches pour capturer un système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Quand vous utilisez une séquence de tâches pour déployer un système d’exploitation sur un ordinateur dans System Center Configuration Manager, l’ordinateur installe l’image du système d’exploitation que vous spécifiez dans la séquence de tâches. Pour personnaliser l’image de système d’exploitation pour qu’elle comporte entre autres des pilotes, applications ou mises à jour logicielles spécifiques, vous utilisez une séquence de tâches de création et de capture pour créer un ordinateur de référence, puis vous capturez l’image du système d’exploitation à partir de cet ordinateur de référence. Si vous avez déjà un ordinateur de référence disponible pour la capture, vous pouvez créer une séquence de tâches pour capturer le système d’exploitation. Utilisez les sections suivantes pour capturer un système d’exploitation personnalisé.  

##  <a name="BKMK_BuildCaptureTS"></a> Utiliser une séquence de tâches pour créer et capturer un ordinateur de référence  
 La séquence de tâches de création et de capture partitionne et formate l’ordinateur de référence, installe le système d’exploitation, ainsi que le client, les applications et les mises à jour logicielles Configuration Manager, puis capture le système d’exploitation à partir de l’ordinateur de référence. Les packages associés à la séquence de tâches, tels que les applications, doivent être disponibles sur les points de distribution avant la création de la séquence de tâches de création et de capture.  

###  <a name="BKMK_CreatePackages"></a> Préparer des déploiements de système d’exploitation  
 Il existe de nombreux scénarios pour déployer un système d’exploitation sur les ordinateurs de votre environnement. Dans la plupart des cas, vous créez une séquence de tâches et vous sélectionnez **Installer un package d’images existant** dans l’Assistant Création d’une séquence de tâches pour installer le système d’exploitation, migrer des paramètres utilisateur, appliquer des mises à jour logicielles et installer des applications. Avant de créer une séquence de tâches pour installer un système d’exploitation, les conditions suivantes doivent être remplies :  

-   **Obligatoire**  

    -   L’[image de démarrage](../get-started/manage-boot-images.md) doit être disponible dans la console Configuration Manager.  

    -   Une [image de système d’exploitation](../get-started/manage-operating-system-images.md) doit être disponible dans la console Configuration Manager.  

-   **Obligatoire (si utilisé)**  

    -   Les[packages de pilotes](../get-started/manage-drivers.md) qui contiennent les pilotes Windows nécessaires à la prise en charge du matériel sur l’ordinateur de référence doivent être disponibles dans la console Configuration Manager. Pour plus d’informations sur les étapes de séquence de tâches liées à la gestion des pilotes, consultez [Utiliser des séquences de tâches pour installer des pilotes de périphérique](../get-started/manage-drivers.md#BKMK_TSDrivers).  

    -   Les[mises à jour logicielles](../../sum/get-started/synchronize-software-updates.md) doivent être synchronisées dans la console Configuration Manager.  

    -   Les [applications](../../apps/deploy-use/create-applications.md) doivent être ajoutées à la console Configuration Manager.  

###  <a name="BKMK_CreateBuildCaptureTS"></a> Créer une séquence de tâches de création et de capture  
 Appliquez la procédure suivante pour utiliser une séquence de tâches pour créer un ordinateur de référence et capturer le système d’exploitation.  

#### <a name="to-create-a-task-sequence-that-builds-and-captures-an-operating-system-image"></a>Pour créer une séquence de tâches qui crée et capture une image du système d'exploitation  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4.  Sur la page **Créer une séquence de tâches** , sélectionnez **Créez et capturez une image de système d'exploitation de référence**.  

5.  Sur la page **Informations sur la séquence de tâches** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Nom de la séquence de tâches**: spécifiez un nom qui identifie la séquence de tâches.  

    -   **Description**: spécifiez une description de la tâche effectuée par la séquence de tâches, telle qu’une description du système d’exploitation créé par la séquence de tâches.  

    -   **Images de démarrage**: spécifiez l’image de démarrage qui installe l’image du système d’exploitation.  

        > [!IMPORTANT]  
        >  L'architecture de l'image de démarrage doit être compatible avec l'architecture matérielle de l'ordinateur de destination.  

6.  Sur la page **Installer Windows** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Package d’images**: spécifiez le package d’images du système d’exploitation, qui contient les fichiers nécessaires à l’installation du système d'exploitation.  

    -   **Index d’images**: spécifiez le système d’exploitation à installer. Si l’image du système d’exploitation contient plusieurs versions, sélectionnez la version que vous souhaitez installer.  

    -   **Clé du produit**: spécifiez la clé de produit pour le système d’exploitation Windows à installer. Vous pouvez spécifier des clés de licence en volume codées et des clés de produit standard. Si vous utilisez une clé de produit non codée, chaque groupe de 5 caractères doit être séparé par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    -   **Mode de licence serveur :** spécifiez que la licence serveur est **Par siège**, **Par serveur**ou qu’aucune licence n’est spécifiée. Si la licence serveur est **Par serveur**, spécifiez également le nombre maximal de connexions au serveur.  

    -   Spécifiez comment gérer le compte administrateur qui est utilisé lors du déploiement du système d'exploitation.  

        -   **Générer de façon aléatoire le mot de passe de l’administrateur local et désactiver le compte sur toutes les plates-formes prises en charge** : spécifiez s’il faut que Configuration Manager crée un mot de passe aléatoire pour le compte administrateur local et désactive le compte quand le système d’exploitation est déployé.  

        -   **Activer le compte et spécifier le mot de passe administrateur local**: spécifiez si le même mot de passe est utilisé pour le compte d’administrateur local sur tous les ordinateurs où est déployé le système d’exploitation.  

7.  Sur la page **Configurer le réseau** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Joindre un groupe de travail**: spécifiez si vous souhaitez ajouter l’ordinateur de destination à un groupe de travail lors du déploiement du système d’exploitation.  

    -   **Joindre un domaine**: spécifiez si vous souhaitez ajouter l’ordinateur de destination à un domaine lors du déploiement du système d’exploitation. Dans **Domaine**, spécifiez le nom du domaine.  

        > [!IMPORTANT]  
        >  Vous pouvez rechercher des domaines dans la forêt locale, mais vous devez spécifier le nom de domaine d'une forêt distante.  

         Vous pouvez également spécifier une unité d'organisation (UO). Il s'agit d'un paramètre facultatif qui spécifie le nom unique LDAP X.500 de l'UO dans laquelle vous créez le compte d'ordinateur s'il n'existe pas déjà.  

    -   **Compte**: spécifiez le nom d’utilisateur et le mot de passe du compte qui dispose des autorisations pour joindre le domaine spécifié. Par exemple : *domaine\utilisateur* ou *%variable%*.  

        > [!IMPORTANT]  
        >  Vous devez entrer les informations d'identification de domaine appropriées si vous prévoyez de migrer les paramètres du domaine ou les paramètres du groupe de travail.  

8.  Dans la page **Installer Configuration Manager**, spécifiez le package client Configuration Manager qui contient les fichiers sources pour installer le client Configuration Manager, ajoutez toutes les propriétés supplémentaires nécessaires à l’installation du client, puis cliquez sur **Suivant**.  

     Pour plus d’informations sur les propriétés qui peuvent être utilisées pour installer un client, consultez [À propos des propriétés d’installation du client](../../core/clients/deploy/about-client-installation-properties.md).  

9. Sur la page **Inclure les mises à jour** , spécifiez si vous souhaitez installer les mises à jour logicielles requises, toutes les mises à jour logicielles ou aucune mise à jour logicielle, puis cliquez sur **Suivant**. Si vous spécifiez l’installation des mises à jour logicielles, Configuration Manager installe uniquement les mises à jour logicielles ciblant les regroupements auxquels l’ordinateur de destination appartient.  

10. Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous spécifiez plusieurs applications, vous pouvez également spécifier que la séquence de tâches continue si l'installation d'une application spécifique échoue.  

11. Sur la page **Préparation du système** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Package** : spécifiez le package Configuration Manager qui contient la version appropriée de Sysprep à utiliser pour capturer les paramètres de l’ordinateur de référence.  

         Si la version du système d'exploitation que vous utilisez est Windows Vista ou version ultérieure, Sysprep est automatiquement installé sur l'ordinateur et il n'est pas nécessaire de spécifier de package.  

12. Sur la page **Propriétés de l'image** , spécifiez les paramètres suivants pour l'image du système d'exploitation, puis cliquez sur **Suivant**.  

    -   **Créé par**: spécifiez le nom de l’utilisateur qui a créé l’image du système d’exploitation.  

    -   **Version**: spécifiez un numéro de version défini par l’utilisateur qui est associé à l’image du système d’exploitation.  

    -   **Description**: spécifiez une description définie par l’utilisateur de l’image du système d’exploitation de l’ordinateur.  

13. Sur la page **Capturer l'image** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

    -   **Chemin d’accès**: spécifiez un dossier réseau partagé où est stocké le fichier .WIM de sortie. Ce fichier contient l'image du système d'exploitation basée sur les paramètres que vous spécifiez à l'aide de cet Assistant. Si vous spécifiez un dossier qui contient un fichier .WIM existant, ce fichier est remplacé.  

    -   **Compte**: spécifiez le compte Windows qui dispose des autorisations d’accès au partage réseau où l’image est stockée.  

14. Effectuez toutes les étapes de l'Assistant.  

15. Pour ajouter des étapes supplémentaires à la séquence de tâches, sélectionnez la séquence de tâches que vous avez créée et cliquez sur **Modifier**. Pour plus d’informations sur la modification d’une séquence de tâches, consultez [Modifier une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

 Déployez la séquence de tâches sur un ordinateur de référence de l’une des manières suivantes :  

-   Si l’ordinateur de référence est un client Configuration Manager, vous pouvez déployer la séquence de tâches de création et de capture dans le regroupement qui contient l’ordinateur de référence. Pour plus d’informations sur le déploiement de l’image du système d’exploitation, consultez [Créer une séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md).  

    > [!NOTE]  
    >  Si la séquence de tâches est une étape d'une séquence de tâches de partitionnement de disque, ne sélectionnez pas l'option **Télécharger le programme** lorsque vous déployez la séquence de tâches.  

-   Si l’ordinateur de référence n’est pas un client Configuration Manager ou si vous souhaitez exécuter manuellement la séquence de tâches sur l’ordinateur de référence, exécutez l’**Assistant Création d’un média de séquence de tâches** pour créer un média de démarrage. Pour plus d’informations sur la création d’un média de démarrage, consultez [Créer un média de démarrage](create-bootable-media.md).  

##  <a name="BKMK_CaptureExistingRefComputer"></a> Capturer une image de système d’exploitation à partir d’un ordinateur de référence existant  
 Quand vous avez déjà un ordinateur de référence prêt à capturer, vous pouvez créer une séquence de tâches qui capture le système d’exploitation à partir de l’ordinateur de référence. Vous utiliserez l’étape de séquence de tâches **Capturer l’image du système d’exploitation** pour capturer une ou plusieurs images à partir d’un ordinateur de référence et les stocker dans un fichier image (.wim) sur le partage réseau spécifié. L’ordinateur de référence est démarré dans Windows PE à l’aide d’une image de démarrage, chaque disque dur sur l’ordinateur de référence étant capturé comme image distincte dans le fichier .wim. Si l’ordinateur référencé comporte plusieurs volumes, le fichier .wim obtenu contient une image distincte pour chaque volume. Seuls les volumes formatés au format NTFS ou FAT32 sont capturés. Les volumes d'un autre format et les volumes USB sont ignorés.  

 Appliquez la procédure suivante pour capturer une image de système d’exploitation à partir d’un ordinateur de référence existant.  

#### <a name="to-capture-an-operating-system-from-an-existing-reference-computer"></a>Pour capturer un système d’exploitation à partir d’un ordinateur de référence existant  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4.  Sur la page **Créer une nouvelle séquence de tâches** , sélectionnez **Créez une séquence de tâches personnalisée**.  

5.  Dans la page **Informations sur la séquence de tâches** , spécifiez le nom et la description de la séquence de tâches.  

6.  Spécifiez une image de démarrage pour la séquence de tâches. Cette image de démarrage est utilisée pour démarrer l’ordinateur de référence avec Windows PE.  Pour plus d’informations, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

7.  Effectuez toutes les étapes de l'Assistant.  

8.  Dans **Séquences de tâches**, sélectionnez la séquence de tâches personnalisée puis, sous l’onglet **Accueil** , dans le groupe **Séquence de tâches** , cliquez sur **Modifier** pour ouvrir l’Éditeur de séquence de tâches.  

9. Effectuez cette étape uniquement si le client Configuration Manager est installé sur l’ordinateur de référence.  

     Cliquez sur **Ajouter**, sur **Images**, puis sur [Préparer le client ConfigMgr pour capture](../understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture). Cette étape de séquence de tâches prend le client Configuration Manager sur l’ordinateur de référence et le prépare pour la capture pendant le processus de création d’images.  

    > [!Note]  
    >  La séquence de tâches ne prend pas en charge la désinstallation du client Configuration Manager.

10. Cliquez sur **Ajouter**, sur **Images**, puis sur [Préparer Windows pour capture](../understand/task-sequence-steps.md#BKMK_PrepareWindowsforCapture). Cette action de séquence de tâches exécute Sysprep, puis redémarre l'ordinateur dans l'image de démarrage Windows PE spécifiée pour la séquence de tâches. L'ordinateur de référence ne doit pas être lié à un domaine pour que cette action s'effectue correctement.  

11. Cliquez sur **Ajouter**, sur **Images**, puis sur [Capturer l’image du système d’exploitation](../understand/task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  Cette étape de séquence de tâches s’exécute uniquement à partir de Windows PE pour capturer les disques durs sur l’ordinateur de référence. Configurez les paramètres suivants pour l’étape de séquence de tâches.  

    -   **Nom** et **Description**: si vous le souhaitez, vous pouvez modifier le nom de l’étape de séquence de tâches et fournir une description.  

    -   **Destination**: spécifiez un dossier réseau partagé où est stocké le fichier .WIM. Ce fichier contient l'image du système d'exploitation basée sur les paramètres que vous spécifiez à l'aide de cet Assistant. Si vous spécifiez un dossier qui contient un fichier .WIM existant, ce fichier est remplacé.  

    -   **Description**, **Version**et **Créé par**: si vous le souhaitez, fournissez des détails sur l’image que vous allez capturer.  

    -   **Compte de capture de l’image du système d’exploitation**: spécifiez le compte Windows qui dispose des autorisations d’accès au partage réseau que vous avez spécifié. Cliquez sur **Définir** pour indiquer le nom de ce compte Windows.  

     Cliquez sur **OK** pour fermer l’Éditeur de séquence de tâches.  

 Déployez la séquence de tâches sur un ordinateur de référence de l’une des manières suivantes :  

-   Si l’ordinateur de référence est un client Configuration Manager, vous pouvez déployer la séquence de tâches dans le regroupement qui contient l’ordinateur de référence. Pour plus d’informations sur le déploiement de l’image du système d’exploitation, consultez [Créer une séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md).  

-   Si l’ordinateur de référence n’est pas un client Configuration Manager ou si vous souhaitez exécuter manuellement la séquence de tâches sur l’ordinateur de référence, exécutez l’**Assistant Création d’un média de séquence de tâches** pour créer un média de démarrage. Pour plus d’informations sur la création d’un média de démarrage, consultez [Créer un média de démarrage](create-bootable-media.md).  

##  <a name="BKMK_BuildandCaptureTSExample"></a> Exemple de séquence de tâches de création et de capture d’une image de système d’exploitation  
 Utilisez le tableau suivant comme référence lorsque vous créez une séquence de tâches visant à générer et capturer l'image d'un système d'exploitation. Ce tableau vous aidera à définir la séquence générale des étapes de votre séquence de tâches. Il vous permettra également d'organiser et de structurer ces étapes en groupes logiques. La séquence de tâches que vous créez peut être différente de celle de cet exemple et elle peut contenir un nombre de groupes et d'étapes de séquence de tâches plus ou moins important.  

> [!IMPORTANT]  
>  Utilisez toujours l’Assistant Création d’une séquence de tâches pour créer ce type de séquence de tâches.  

 Quand vous utilisez l’ **Assistant Nouvelle séquence de tâches** pour créer cette séquence de tâches, les noms de certaines étapes diffèrent de ce qu’ils seraient normalement si vous ajoutiez manuellement ces étapes à une séquence de tâches existante. Le tableau suivant présente les différences de dénomination :  

|Nom de l'étape de séquence de tâches de l'Assistant Nouvelle séquence de tâches|Nom équivalent de l'étape dans l'Éditeur de séquence de tâches|  
|------------------------------------------------------|-----------------------------------------------|  
|Redémarrer dans Windows PE|Redémarrer sur Windows PE ou disque dur|  
|Partitionner le disque 0|Formater et partitionner le disque|  
|Appliquer les pilotes de périphériques|Appliquer automatiquement les pilotes|  
|Installer les mises à jour|Installer les mises à jour logicielles|  
|Joindre le groupe de travail|Joindre le domaine ou le groupe de travail|  
|Préparer le client ConfigMgr|Prepare ConfigMgr Client for Capture|  
|Préparer le système d'exploitation|Prepare Windows for Capture|  
|Capturer la machine de référence|Capturer l’image du système d’exploitation|  

|Groupe/étape de la séquence de tâches|Référence|  
|-------------------------------|---------------|  
|Créer l'ordinateur de référence - **(nouveau groupe de séquence de tâches)**|Créez un groupe de séquences de tâches. Un groupe de séquences de tâches regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.<br /><br /> Ce groupe contient les actions nécessaires à la création d'un ordinateur de référence.|  
|Redémarrer dans Windows PE|Utilisez cette étape de séquence de tâches pour spécifier les options de redémarrage pour l'ordinateur de destination. Cette étape affichera un message notifiant l'utilisateur que l'ordinateur sera redémarré afin de poursuivre l'installation.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSInWinPE** en lecture seule. Si la valeur associée est **false,** l'étape de la séquence de tâches se poursuivra.|  
|Partitionner le disque 0|Utilisez cette étape de séquence de tâches pour déterminer les actions nécessaires au formatage du disque dur sur l'ordinateur de destination. Le numéro de disque par défaut est **0**.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSMediaType** en lecture seule. Elle sera exécutée en l’absence de mémoire cache du client Configuration Manager.|  
|Appliquer le système d'exploitation|Utilisez cette étape de séquence de tâches pour installer une image de système d'exploitation spécifiée sur l'ordinateur de destination. Cette étape applique toutes les images de volume contenues dans le fichier WIM au volume de disque séquentiel correspondant sur l’ordinateur cible après avoir d’abord supprimé tous les fichiers sur ce volume (à l’exception des fichiers de contrôle propres à Configuration Manager).|  
|Appliquer les paramètres Windows|Utilisez cette étape de séquence de tâches pour configurer les informations de configuration des paramètres Windows pour l'ordinateur de destination.|  
|Appliquer les paramètres réseau|Utilisez cette étape de séquence de tâches pour spécifier les informations de configuration du réseau ou du groupe de travail pour l'ordinateur de destination.|  
|Appliquer les pilotes de périphériques|Utilisez cette étape de séquence de tâches pour faire correspondre et installer des pilotes dans le cadre du déploiement d'un système d'exploitation. Vous pouvez autoriser le programme d'installation Windows à rechercher toutes les catégories de pilotes existantes en sélectionnant **Considérer les pilotes de toutes les catégories** . Vous pouvez également limiter les catégories de pilotes que le programme d'installation Windows doit rechercher en sélectionnant **Limiter la correspondance des pilotes aux pilotes des catégories sélectionnées uniquement**.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSMediaType** en lecture seule. Si la valeur associée n'est pas **FullMedia** , cette étape de la séquence de tâches s'exécute.|  
|Configurer Windows et ConfigMgr|Cette étape de séquence de tâches permet d’installer le logiciel client Configuration Manager. Configuration Manager installe et inscrit le GUID du client Configuration Manager. Vous pouvez définir les paramètres d'installation nécessaires à partir de la fenêtre **Propriétés d'installation** .|  
|Installer les mises à jour|Utilisez cette étape de séquence de tâches pour spécifier la façon dont sont installées les mises à jour logicielles sur l'ordinateur de destination. L'ordinateur de destination n'est pas évalué pour déterminer les mises à jour logicielles applicables avant l'exécution de cette séquence de tâches. À ce stade, l’ordinateur de destination est évalué pour déterminer les mises à jour logicielles comme n’importe quel autre client géré par Configuration Manager.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSMediaType** en lecture seule. Si la valeur associée n'est pas **FullMedia** , cette étape de la séquence de tâches s'exécute.|  
|Capturer l'ordinateur de référence - **(nouveau groupe de séquence de tâches)**|Créez un autre groupe de séquences de tâches. Ce groupe contient les étapes nécessaires pour préparer et capturer un ordinateur de référence.|  
|Joindre le groupe de travail|Utilisez cette étape de séquence de tâches pour spécifier les informations requises pour que l'ordinateur de destination rejoigne un groupe de travail.|  
|Prepare ConfigMgr Client for Capture|Utilisez cette étape pour prendre le client Configuration Manager sur l’ordinateur de référence et le préparer pour la capture pendant le processus de création d’image.|  
|Préparer le système d'exploitation|Utilisez cette étape de séquence de tâches pour spécifier les options Sysprep à utiliser lors de la capture des paramètres Windows sur l'ordinateur de référence. Cette étape de séquence de tâches exécute Sysprep puis redémarre l'ordinateur dans l'image de démarrage Windows PE spécifiée pour la séquence de tâches.|  
|Capturer l’image du système d’exploitation|Utilisez cette étape de séquence de tâches pour entrer un partage réseau existant et un fichier .WIM à utiliser lors de l'enregistrement de l'image. Cet emplacement est utilisé comme emplacement source du package lors de l'ajout d'un package d'images de système d'exploitation via l' **Assistant Ajout d'un package d'image de système d'exploitation**.|  

 Après avoir capturé une image à partir d'un ordinateur de référence, ne capturez pas une autre image du système d'exploitation à partir de l'ordinateur de référence car des entrées de Registre sont créées pendant la configuration initiale. Créez un ordinateur de référence chaque fois que vous capturez l'image du système d'exploitation. Si vous prévoyez d’utiliser le même ordinateur de référence pour créer de futures images du système d’exploitation, commencez par désinstaller le client Configuration Manager, puis réinstallez-le.  

## <a name="next-steps"></a>Étapes suivantes  
[Méthodes de déploiement de systèmes d’exploitation d’entreprise](methods-to-deploy-enterprise-operating-systems.md)
