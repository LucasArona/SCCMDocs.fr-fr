---
title: Installation via la ligne de commande
titleSuffix: Configuration Manager
description: Découvrez comment exécuter le programme d’installation de System Center Configuration Manager à partir d’une invite de commandes pour diverses installations de site.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e7cdb1a9-140a-436e-ac71-72d083110223
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3df559dc151950834aab4d909811cb42ec4822d0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338939"
---
# <a name="use-a-command-line-to-install-system-center-configuration-manager-sites"></a>Utiliser la ligne de commande pour installer des sites System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez exécuter le programme d’installation de System Center Configuration Manager à partir d’une invite de commandes pour installer divers types de site.

## <a name="supported-tasks-for-command-line-installations"></a>Tâches prises en charge pour des installations via la ligne de commande
 Cette méthode consistant à exécuter le programme d’installation prend en charge les tâches d’installation de site et de maintenance de site suivantes :

-   **Installer un site d’administration centrale ou un site principal à partir de la ligne de commande**  
  Consultez la rubrique [Options de ligne de commande pour le programme d’installation](../../../../core/servers/deploy/install/command-line-options-for-setup.md).

-  **Modifier les langues utilisées sur un site d’administration centrale ou un site principal**  
    Pour modifier les langues installées sur un site à partir de la ligne de commande (y compris les langues des appareils mobiles), effectuez les opérations suivantes :  

     -   Exécutez le programme d’installation à partir de **&lt;chemin_installation_Configuraton_Manager\>\Bin\X64** sur le serveur de site.
     -   Utilisez l’option de ligne de commande **/MANAGELANGS**.
     -   Spécifiez un fichier de jeu de caractères qui définit les langues à ajouter ou supprimer.  

    Par exemple, utilisez la syntaxe de commande suivante : **setupwpf.exe /MANAGELANGS &lt;fichier de script de langue\>**.  

    Pour créer le fichier de script de langue, utilisez les informations fournies dans [Options de ligne de commande pour gérer les langues](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Lang).  

-  **Utiliser un fichier de script d’installation pour une installation sans assistance de site ou une récupération de site**  
    Vous pouvez exécuter le programme d’installation à partir d’une invite de commandes en utilisant un script d’installation et en effectuant une installation sans assistance de site. Vous pouvez aussi utiliser cette option pour récupérer un site.    

    Pour utiliser un script avec le programme d’installation :  

    -   Exécutez le programme d’installation avec l’option de ligne de commande **/SCRIPT** et spécifiez un fichier de script.  

    -   Le fichier de script doit être configuré avec les clés et les valeurs requises.  

    Pour effectuer une installation sans assistance d’un site d’administration centrale ou d’un site principal, le fichier de script doit comporter les sections suivantes :  

    -   Identification    
    -   Options    
    -   SQLConfigOptions    
      -   HierarchyOptions    
    -   CloudConnectorOptions   

    Pour récupérer un site, vous devez inclure également les sections suivantes du fichier de script :  

    -   Identification  
    -   Récupération

Pour plus d’informations, consultez [Récupération de site sans assistance pour Configuration Manager](/sccm/protect/understand/unattended-recovery).  

Pour obtenir la liste des clés et des valeurs à utiliser dans un fichier de script d’installation sans assistance, consultez [Clés du fichier de script d’installation sans assistance](../../../../core/servers/deploy/install/command-line-options-for-setup.md#bkmk_Unattended).  

## <a name="about-the-command-line-script-file"></a>À propos du fichier de script de ligne de commande  
 Pour réaliser une installation sans assistance de Configuration Manager, vous pouvez exécuter le programme d’installation avec l’option de ligne de commande **/SCRIPT** et spécifier un fichier de script contenant les options d’installation. Avec cette méthode, vous pouvez effectuer les tâches suivantes :  

-   Installer un site d’administration centrale  
-   Installer un site principal  
-   Installer une console Configuration Manager  
-   Récupérer un site  

> [!NOTE]  
>  Vous ne pouvez pas utiliser le fichier de script d’installation sans assistance pour mettre à niveau un site d’évaluation vers une installation sous licence de Configuration Manager.  

### <a name="the-cdlatest-key-name"></a>Le nom de la clé CDLatest
Lorsque vous utilisez un média à partir du dossier CD.Latest pour exécuter une installation scriptée des quatre options d’installation suivantes, votre script doit inclure la clé **CDLatest** avec la valeur **1** :
- Installer un nouveau site d’administration centrale
- Installer un nouveau site principal
- Récupérer un site d’administration centrale
- Récupérer un site principal

Cette valeur n’est pas prise en charge pour l’utilisation avec le média d’installation que vous obtenez à partir du site de licence en volume de Microsoft.
Consultez les [options de ligne de commande](/sccm/core/servers/deploy/install/command-line-options-for-setup) pour plus d’informations sur l’utilisation de ce nom de clé dans le fichier de script.



### <a name="create-the-script"></a>Créer le script
Le script d’installation est automatiquement créé lorsque vous [exécutez le programme d’installation pour installer un site à l’aide de l’interface utilisateur](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md).  Quand vous confirmez les paramètres dans la page **Résumé** de l’Assistant :  

-   Le programme d’installation crée le script **%TEMP%\ConfigMgrAutoSave.ini**.  Vous pouvez renommer ce fichier avant de l’utiliser, en veillant à conserver l’extension de fichier .ini.  
-   Le script d'installation sans assistance contient les paramètres que vous avez sélectionnés dans l'Assistant.  
-   Une fois que le script est créé, vous pouvez le modifier pour installer d'autres sites dans votre hiérarchie.  
-   Vous pouvez ensuite utiliser ce script pour effectuer une installation sans assistance de Configuration Manager.  

Le fichier de script fournit les mêmes informations que l’Assistant Installation demande, à l’exception des paramètres par défaut.   
Vous devez spécifier toutes les valeurs pour les clés d’installation qui s’appliquent au type d’installation utilisé.   

Lorsque le programme d’installation crée le script d’installation sans assistance, la valeur de clé de produit que vous entrez pendant l’installation est renseignée dans le script. Cette valeur peut être une clé de produit valide, ou **EVAL** lorsque vous installez une version d’évaluation de Configuration Manager. La valeur de clé de produit est renseignée dans le script pour permettre à la vérification des prérequis d’aboutir.   

Lorsque le programme d'installation démarre l'installation effective du site, le script créé automatiquement fait l'objet d'une nouvelle écriture pour effacer la valeur de clé de produit dans le script créé. Avant d’utiliser le script pour une installation sans assistance d’un nouveau site, vous pouvez modifier le script pour fournir une clé de produit valide ou spécifier une installation d’évaluation de Configuration Manager.  

### <a name="section-names-key-names-and-values"></a>Noms des sections, noms des clés et valeurs
Le script contient les noms de section, les noms de clé et les valeurs. Gardez à l’esprit les informations suivantes :
-   Les noms des clés de section requis varient en fonction du type d'installation faisant l'objet du script.
-   L’ordre des clés dans les sections et l’ordre des sections dans le fichier n’ont pas d’importance.     
-   Les clés ne tiennent pas compte de la casse.  
-   Lorsque vous attribuez des valeurs aux clés, le nom de la clé doit être suivi du signe égal (=) et de la valeur de la clé.    

> [!TIP]  
>  Pour connaître l’ensemble complet des options, consultez [Options de ligne de commande pour le programme d’installation et les scripts](../../../../core/servers/deploy/install/command-line-options-for-setup.md).  

## <a name="use-the-script-setup-command-line-option"></a>Utiliser l’option de ligne de commande /SCRIPT du programme d’installation

-   Vous devez utiliser un fichier de script d’installation et spécifier le nom du fichier après l’option de ligne de commande **/SCRIPT** du programme d’installation. Gardez à l’esprit les informations suivantes :   
    -   Le nom du fichier doit avoir l’extension de nom de fichier **.ini**.  
    -   Quand vous faites référence au fichier de script du programme d’installation à l’invite de commandes, indiquez le chemin complet du fichier. Par exemple, si votre fichier d’initialisation du programme d’installation est nommé Setup.ini et se trouve dans le dossier C:\Setup, à l’invite de commandes, tapez :  **setup /script c:\setup\setup.ini**.  

-   Le compte qui exécute le programme d’installation doit avoir des droits d’**administrateur** sur l’ordinateur. Si vous exécutez le programme d’installation avec le script sans assistance, ouvrez la fenêtre d’invite de commandes en utilisant l’option **Exécuter en tant qu’administrateur**.   
