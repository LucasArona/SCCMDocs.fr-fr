---
title: Créer un média de capture
titleSuffix: Configuration Manager
description: Utilisez les médias de capture de Configuration Manager pour capturer une image de système d’exploitation sur un ordinateur de référence.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6e1e007387a50146a899bca767aa5d1f2d85a3a
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082759"
---
# <a name="create-capture-media"></a>Créer un média de capture

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, un média de capture permet de capturer une image de système d’exploitation sur un ordinateur de référence. Il contient l’image de démarrage qui démarre l’ordinateur de référence et la séquence de tâches qui capture l’image de système d’exploitation. Utilisez un média de capture dans le scénario [Créer une séquence de tâches pour capturer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).  


## <a name="prerequisites"></a>Prérequis

Avant de créer un média de capture avec l’Assistant Création d’un média de séquence de tâches, vérifiez que toutes ces conditions sont remplies.

### <a name="boot-image"></a>Image de démarrage

Prenez en considération les points suivants concernant l’image de démarrage utilisée dans la séquence de tâches pour déployer le système d’exploitation :

- L’architecture de l’image de démarrage doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.
- Vérifiez que l’image de démarrage contient les pilotes de réseau et de stockage nécessaires pour approvisionner l’ordinateur de destination.

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuer tout le contenu associé à la séquence de tâches

Distribuez auprès d’au moins un point de distribution tout le contenu exigé par la séquence de tâches, à savoir l’image de démarrage, l’image de système d’exploitation et les autres fichiers associés. L’Assistant collecte le contenu sur le point de distribution quand il crée le média de capture.

Votre compte d’utilisateur doit au moins disposer de droits d’accès en **Lecture** à la bibliothèque de contenu de ce point de distribution. Pour plus d’informations, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Préparer le lecteur USB amovible

Si vous utilisez un lecteur USB amovible, branchez-le à l’ordinateur sur lequel s’exécute l’Assistant Création d’un média de séquence de tâches. Il doit être détectable comme appareil amovible par Windows. L’Assistant écrit directement sur le lecteur USB quand il crée le média.

### <a name="create-an-output-folder"></a>Créer un dossier de sortie

Avant d’exécuter l’Assistant Création d’un média de séquence de tâches afin de créer un média pour un ensemble de CD ou de DVD, créez un dossier pour les fichiers de sortie créés. Le média créé pour un ensemble de CD ou de DVD est directement écrit sous forme de fichier .ISO dans le dossier.


## <a name="process"></a>Processus

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Créer un média de séquence de tâches** dans le groupe **Créer** pour lancer l’Assistant Création d’un média de séquence de tâches.  

3. Sur la page **Sélectionner le type de média**, sélectionnez **Média de capture**.  

4. Sur la page **Type de média**, spécifiez s’il s’agit d’un **Lecteur USB amovible** ou d’un **Ensemble de CD/DVD**. Ensuite, configurez les options suivantes :  

    > [!IMPORTANT]  
    > Le média utilise un système de fichiers FAT32. Il n’est pas possible de créer un média sur un lecteur USB contenant un fichier d’une taille supérieure à 4 Go.  

    - Si vous sélectionnez **Lecteur USB amovible**, choisissez le lecteur sur lequel le contenu sera stocké.  

        - **Formater le lecteur USB amovible (FAT32) et le rendre démarrable** : par défaut, laisser Configuration Manager préparer le lecteur USB. De nombreux appareils UEFI récents nécessitent une partition FAT32 amorçable. Toutefois, ce format limite également la taille des fichiers et la capacité globale du lecteur. Si vous avez déjà formaté et configuré le lecteur amovible, désactivez cette option.

    - Si vous sélectionnez **Ensemble de CD/DVD**, spécifiez la capacité du média (**Taille du média**) et le nom et le chemin d’accès du fichier de sortie (**Fichier de média**). L'Assistant écrit les fichiers de sortie à cet emplacement. Exemple : `\\servername\folder\outputfile.iso`  

        Si la capacité du média est insuffisante pour stocker l’ensemble du contenu, il crée plusieurs fichiers. Il vous faut alors stocker le contenu sur plusieurs CD ou DVD. Quand plusieurs fichiers de média sont nécessaires, Configuration Manager ajoute un numéro de séquence au nom de chaque fichier de sortie qu’il crée.  

        > [!IMPORTANT]  
        > Si vous sélectionnez une image .iso existante, l'Assistant Média de séquence de tâches supprime cette image du lecteur ou du partage dès lors que vous passez à la page suivante de l'Assistant. L'image existante est supprimée même si vous annulez ensuite l'Assistant.  

    - **Dossier intermédiaire**<!--1359388-->: le processus de création de média est susceptible de prendre beaucoup d’espace lecteur temporaire. Par défaut, cet emplacement est semblable au suivant : `%UserProfile%\AppData\Local\Temp`. À compter de la version 1902, remplacez cette valeur par un autre lecteur et un autre chemin d’accès pour choisir où stocker ces fichiers temporaires.  

    - **Étiquette du média**<!--1359388-->: à compter de la version 1902, ajoutez une étiquette au média de séquence de tâches. Cette étiquette vous permet de mieux identifier le média une fois celui-ci créé. La valeur par défaut est `Configuration Manager`. Ce champ de texte s’affiche dans les emplacements suivants :  

        - Si vous montez un fichier ISO, Windows utilise cette étiquette pour nommer le lecteur monté.  

        - Si vous formatez un lecteur USB, les 11 premiers caractères de l’étiquette sont utilisés pour former son nom.  

        - Configuration Manager écrit un fichier texte appelé `MediaLabel.txt` à la racine du média. Par défaut, le fichier comprend une seule ligne de texte : `label=Configuration Manager`. Si vous personnalisez l’étiquette du média, cette ligne utilise votre étiquette personnalisée à la place de la valeur par défaut.  

    - **Inclure le fichier autorun.inf sur le média**<!-- 4090666 -->: à compter de la version 1902, Configuration Manager n’ajoute pas par défaut de fichier autorun.inf. Ce fichier est généralement bloqué par les produits anti-programme malveillant. Pour plus d’informations sur la fonctionnalité d’exécution automatique (AutoRun) de Windows, consultez [Création d’une application sur CD-ROM prenant en charge l’exécution automatique](https://docs.microsoft.com/windows/desktop/shell/autoplay). Si elle reste nécessaire dans votre scénario, sélectionnez cette option pour inclure le fichier.  

5. Sur la page **Image de démarrage**, spécifiez les options suivantes :  

    > [!IMPORTANT]  
    > L’architecture de l’image de démarrage distribuée doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.  

    - **Image de démarrage** : sélectionnez l’image de démarrage permettant de démarrer l’ordinateur de destination.  

    - **Point de distribution** : sélectionnez le point de distribution comportant l’image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

        > [!NOTE]  
        > Votre compte d’utilisateur doit au moins disposer d’autorisations d’accès en **Lecture** à la bibliothèque de contenu du point de distribution.  

6. Effectuez toutes les étapes de l'Assistant.  


## <a name="next-steps"></a>Étapes suivantes

[Créer une séquence de tâches pour capturer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system)
