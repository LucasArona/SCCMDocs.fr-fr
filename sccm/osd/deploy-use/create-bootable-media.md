---
title: Créer un média de démarrage
titleSuffix: Configuration Manager
description: Utilisez les médias de démarrage de Configuration Manager pour installer une nouvelle version de Windows ou remplacer un ordinateur.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b7a68dd6d0bdbc2fa043d552aba13562dc175fc
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082939"
---
# <a name="create-bootable-media"></a>Créer un média de démarrage

*S’applique à : System Center Configuration Manager (Current Branch)*

Un média de démarrage dans Configuration Manager contient l’image de démarrage, des commandes de prédémarrage facultatives et leurs fichiers associés, ainsi que les fichiers de Configuration Manager. Utilisez un média préparé dans les scénarios de déploiement de système d’exploitation suivants :  

- [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [Remplacement d’un ordinateur existant et transfert des paramètres](/sccm/osd/deploy-use/replace-an-existing-computer-and-transfer-settings)  


## <a name="usage"></a>Utilisation

Le processus suivant se produit en cas de démarrage sur un média de démarrage :

1. L’ordinateur de destination démarre.
1. Il se connecte au réseau.
1. Il récupère le contenu suivant sur le site :
    - séquence de tâches spécifiée
    - image du système d'exploitation
    - tout autre contenu requis

Comme la séquence de tâches ne se trouve pas sur le média, il est possible de modifier la séquence de tâches ou le contenu sans avoir à recréer le média.

Les packages qui se trouvent sur le média de démarrage ne sont pas chiffrés. Pour protéger le contenu des packages contre les utilisateurs non autorisés, prenez les mesures de sécurité qui s’imposent. Par exemple, ajoutez un mot de passe au média.

## <a name="prerequisites"></a>Prérequis

Avant de créer un média de démarrage avec l’Assistant Création d’un média de séquence de tâches, vérifiez que toutes ces conditions sont remplies.

### <a name="boot-image"></a>Image de démarrage

Prenez en considération les points suivants concernant l’image de démarrage utilisée dans la séquence de tâches pour déployer le système d’exploitation :

- L’architecture de l’image de démarrage doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.
- Vérifiez que l’image de démarrage contient les pilotes de réseau et de stockage nécessaires pour approvisionner l’ordinateur de destination.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Créer une séquence de tâches pour déployer un système d’exploitation

Dans le cadre du média de démarrage, spécifiez la séquence de tâches permettant de déployer le système d’exploitation. Pour plus d’informations, voir [Créer une séquence de tâches pour installer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuer tout le contenu associé à la séquence de tâches

Distribuez auprès d’au moins un point de distribution tout le contenu exigé par la séquence de tâches, à savoir l’image de démarrage et les autres fichiers de prédémarrage associés. L’Assistant collecte le contenu sur le point de distribution quand il crée le média de démarrage.

Votre compte d’utilisateur doit au moins disposer de droits d’accès en **Lecture** à la bibliothèque de contenu de ce point de distribution. Pour plus d’informations, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="prepare-the-removable-usb-drive"></a>Préparer le lecteur USB amovible

Si vous utilisez un lecteur USB amovible, branchez-le à l’ordinateur sur lequel s’exécute l’Assistant Création d’un média de séquence de tâches. Il doit être détectable comme appareil amovible par Windows. L’Assistant écrit directement sur le lecteur USB quand il crée le média.

### <a name="create-an-output-folder"></a>Créer un dossier de sortie

Avant d’exécuter l’Assistant Création d’un média de séquence de tâches afin de créer un média pour un ensemble de CD ou de DVD, créez un dossier pour les fichiers de sortie créés. Le média créé pour un ensemble de CD ou de DVD est directement écrit sous forme de fichier .ISO dans le dossier.


## <a name="process"></a>Processus

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Créer un média de séquence de tâches** dans le groupe **Créer** pour lancer l’Assistant Création d’un média de séquence de tâches.  

3. Sur la page **Sélectionner le type de média**, spécifiez les options suivantes :  

    - Sélectionnez **Média de démarrage**.  

    - Si vous souhaitez autoriser seulement le déploiement du système d’exploitation sans intervention de l’utilisateur, sélectionnez **Autoriser le déploiement sans assistance du système d’exploitation**.  

        > [!IMPORTANT]  
        > Avec cette option, l’utilisateur n’est pas invité à fournir des informations sur la configuration réseau ou des séquences de tâches facultatives. Si le média est configuré avec une protection par mot de passe, l’utilisateur est quand même invité à entrer un mot de passe.  

4. Sur la page **Gestion du média**, spécifiez l’une des options suivantes :  

    - **Média dynamique** : autorisez un point de gestion à rediriger le média vers un autre point de gestion, en fonction de l’emplacement du client dans les limites du site.  

    - **Média basé sur le site** : le média ne contacte que le point de gestion spécifié.  

5. Sur la page **Type de média**, spécifiez s’il s’agit d’un **Lecteur USB amovible** ou d’un **Ensemble de CD/DVD**. Ensuite, configurez les options suivantes :  

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

6. Sur la page **Sécurité**, spécifiez les options suivantes :  

    - **Activer la prise en charge des ordinateurs inconnus** : autorisez le média à déployer un système d’exploitation sur un ordinateur non géré par Configuration Manager. Il n’y a aucun enregistrement de ces ordinateurs dans la base de données Configuration Manager. Pour plus d’informations, voir [Préparer les déploiements d’ordinateurs inconnus](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

    - **Protéger le média par un mot de passe** : entrez un mot de passe fort pour mieux protéger le média contre les accès non autorisés. Lorsque vous spécifiez un mot de passe, l'utilisateur doit fournir ce mot de passe pour utiliser le média de démarrage.  

        > [!IMPORTANT]  
        > Une bonne pratique de sécurité consiste à toujours attribuer un mot de passe pour contribuer à protéger les médias de démarrage.  

    - Pour les communications HTTP, sélectionnez **Créer un certificat de média auto-signé**. Ensuite, spécifiez la date de début et la date d’expiration du certificat.  

    - Pour les communications HTTPS, sélectionnez **Importer un certificat PKI**. Ensuite, spécifiez le certificat à importer et son mot de passe.  

        Pour plus d’informations sur ce certificat client utilisé par les images de démarrage, voir [Exigences des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Affinité entre utilisateur et périphérique** : pour prendre en charge la gestion centrée sur l’utilisateur dans Configuration Manager, spécifiez la manière dont le média devra associer les utilisateurs à l’ordinateur de destination. Pour plus d’informations sur la prise en charge de l’affinité entre utilisateur et périphérique par le déploiement de système d’exploitation, voir [Associer des utilisateurs à un ordinateur de destination](/sccm/osd/get-started/associate-users-with-a-destination-computer).  

        - **Autoriser l’affinité entre utilisateur et périphérique avec approbation automatique** : le média associe automatiquement les utilisateurs à l’ordinateur de destination. Cette fonctionnalité dépend des actions de la séquence de tâches qui déploie le système d’exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination lors du déploiement du système d’exploitation sur l’ordinateur de destination.  

        - **Autoriser l’affinité entre utilisateur et périphérique dans l’attente de l’approbation de l’administrateur** : le média associe les utilisateurs à l’ordinateur de destination une fois l’approbation accordée. Cette fonctionnalité dépend de l’étendue de la séquence de tâches qui déploie le système d’exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination, mais attend l’approbation d’un utilisateur administratif avant le déploiement du système d’exploitation.  

        - **Ne pas utiliser d’affinité entre utilisateur et périphérique** : le média n’associe pas les utilisateurs à l’ordinateur de destination. Dans ce scénario, la séquence de tâches n’associe pas les utilisateurs à l’ordinateur de destination lors du déploiement du système d’exploitation.  

7. Sur la page **Image de démarrage**, spécifiez les options suivantes :  

    > [!IMPORTANT]  
    > L’architecture de l’image de démarrage distribuée doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.  

    - **Image de démarrage** : sélectionnez l’image de démarrage permettant de démarrer l’ordinateur de destination.  

    - **Point de distribution** : sélectionnez le point de distribution comportant l’image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

        > [!NOTE]  
        > Votre compte d’utilisateur doit au moins disposer d’autorisations d’accès en **Lecture** à la bibliothèque de contenu du point de distribution.  

    - **Point de gestion** : uniquement pour *Média basé sur le site*, sélectionnez un point de gestion issu d’un site principal.  

    - **Points de gestion associés** : uniquement pour *Média dynamique*, sélectionnez les points de gestion de site principal à utiliser et un ordre de priorité pour la communication initiale.  

8. Sur la page **Personnalisation**, spécifiez les options suivantes :  

    - Ajoutez toutes les variables utilisées par la séquence de tâches.  

    - **Activer les commandes de prédémarrage** : spécifiez les commandes de prédémarrage à exécuter avant l’exécution de la séquence de tâches. Il s’agit d’un script ou d’un exécutable capable d’interagir avec l’utilisateur dans Windows PE avant que la séquence de tâches ne commence. Pour plus d’informations, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](/sccm/osd/understand/prestart-commands-for-task-sequence-media).  

        > [!TIP]  
        > Lors de la création du média, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des éventuelles variables de la séquence de tâches, dans le fichier **CreateTSMedia.log** sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

        Si certains contenus sont nécessaires à la commande de prédémarrage, sélectionnez l’option **Inclure les fichiers de la commande de prédémarrage**.  

9. Effectuez toutes les étapes de l'Assistant.  


## <a name="alternate-method"></a>Autre méthode

Il est possible de créer un média de démarrage sur un lecteur USB amovible lorsque ce dernier n’est pas branché à l’ordinateur sur lequel s’exécute la console Configuration Manager.

1. [Créez le média de démarrage de séquence de tâches](#process). Dans la page **Type de média**, sélectionnez **Ensemble CD/DVD**. L’Assistant écrit les fichiers de sortie à l’emplacement que vous spécifiez. Par exemple : `\\servername\folder\outputfile.iso`.  

2. Préparez le lecteur USB amovible. Le lecteur doit être formaté, vide et démarrable.

3. Montez l’image ISO à partir de l’emplacement du partage, puis transférez les fichiers de l’image ISO sur le lecteur USB.


## <a name="next-steps"></a>Étapes suivantes

[Utiliser un média de démarrage pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-bootable-media-to-deploy-windows-over-the-network)  
