---
title: Créer un média préparé
titleSuffix: Configuration Manager
description: Utilisez les médias préparés de Configuration Manager pour simplifier le déploiement de Windows dans plusieurs scénarios.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8cba7fff1ec7144abfa5f92c25c73d36d5d7c749
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082790"
---
# <a name="create-prestaged-media"></a>Créer un média préparé

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, un média préparé est un fichier image Windows (WIM). Il peut être installé sur un système nu par le fabricant ou dans un centre intermédiaire non relié à l’environnement Configuration Manager de production. Un média préparé contient l’image de démarrage servant à démarrer l’ordinateur de destination et l’image de système d’exploitation appliquée à l’ordinateur de destination. Vous pouvez aussi spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. La séquence de tâches qui déploie le système d’exploitation n’est pas incluse dans le média. Un média préparé est appliqué au disque dur d'un nouvel ordinateur avant que l'ordinateur soit envoyé à l'utilisateur final.

Utilisez un média préparé dans les scénarios de déploiement de système d’exploitation suivants :  

- [Créer une image pour un fabricant OEM en usine ou dépôt local](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)  

- [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](/sccm/osd/deploy-use/install-new-windows-version-new-computer-bare-metal)  

- [Déployer Windows To Go](/sccm/osd/deploy-use/deploy-windows-to-go)  


## <a name="usage"></a>Utilisation

Pour son premier démarrage après application du média préparé, l’ordinateur démarre dans Windows PE. Il se connecte à un point de gestion pour localiser la séquence de tâches qui effectue le processus de déploiement de système d’exploitation. Lors du déploiement d’une séquence de tâches utilisant un média préparé, le client vérifie d’abord que le contenu du cache local de la séquence de tâches est valide. Si ce contenu est introuvable ou a été modifié, le client le télécharge à partir d’un point de distribution ou d’un homologue.  


## <a name="prerequisites"></a>Prérequis

Avant de créer un média préparé avec l’Assistant Création d’un média de séquence de tâches, vérifiez que toutes les conditions sont remplies.

### <a name="boot-image"></a>Image de démarrage

Prenez en considération les points suivants concernant l’image de démarrage utilisée dans la séquence de tâches pour déployer le système d’exploitation :

- L’architecture de l’image de démarrage doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.
- Vérifiez que l’image de démarrage contient les pilotes de réseau et de stockage nécessaires pour approvisionner l’ordinateur de destination.

### <a name="create-a-task-sequence-to-deploy-an-os"></a>Créer une séquence de tâches pour déployer un système d’exploitation

Dans le cadre du média préparé, spécifiez la séquence de tâches permettant de déployer le système d’exploitation. Pour plus d’informations, voir [Créer une séquence de tâches pour installer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-install-an-operating-system).

### <a name="distribute-all-content-associated-with-the-task-sequence"></a>Distribuer tout le contenu associé à la séquence de tâches

Distribuez auprès d’au moins un point de distribution tout le contenu exigé par la séquence de tâches, à savoir l’image de démarrage, l’image de système d’exploitation et les autres fichiers associés. L’Assistant collecte le contenu sur le point de distribution quand il crée le média préparé.

Votre compte d’utilisateur doit au moins disposer de droits d’accès en **Lecture** à la bibliothèque de contenu de ce point de distribution. Pour plus d’informations, consultez [Distribuer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_distribute).

### <a name="hard-drive-on-the-destination-computer"></a>Disque dur de l’ordinateur de destination

Le disque dur de l’ordinateur de destination doit être formaté avant application du média préparé. Dans le cas contraire, la séquence de tâches qui déploie le système d’exploitation échouera lorsqu’elle tentera de démarrer l’ordinateur de destination.

> [!NOTE]  
> L’Assistant Création d’un média de séquence de tâches définit la condition de variable de séquence de tâches suivante sur le média : **_SMSTSMediaType = OEMMedia**. Vous pouvez utiliser cette même condition dans votre séquence de tâches.  


## <a name="process"></a>Processus

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Créer un média de séquence de tâches** dans le groupe **Créer** pour lancer l’Assistant Création d’un média de séquence de tâches.  

3. Sur la page **Sélectionner le type de média**, spécifiez les options suivantes :  

    - Sélectionnez **Média préparé**.  

    - Si vous souhaitez autoriser seulement le déploiement du système d’exploitation sans intervention de l’utilisateur, sélectionnez **Autoriser le déploiement sans assistance du système d’exploitation**.  

        > [!IMPORTANT]  
        > Avec cette option, l’utilisateur n’est pas invité à fournir des informations sur la configuration réseau ou des séquences de tâches facultatives. Si le média est configuré avec une protection par mot de passe, l’utilisateur est quand même invité à entrer un mot de passe.  

4. Sur la page **Gestion du média**, spécifiez l’une des options suivantes :  

    - **Média dynamique** : autorisez un point de gestion à rediriger le média vers un autre point de gestion, en fonction de l’emplacement du client dans les limites du site.  

    - **Média basé sur le site** : le média ne contacte que le point de gestion spécifié.  

5. Sur la page **Propriétés du média**, spécifiez les informations suivantes :  

    - **Créé par**: spécifiez qui a créé le média.  

    - **Version**: spécifiez le numéro de version du média.  

    - **Commentaire**: spécifiez une description unique de ce pour quoi le média est utilisé.  

    - **Fichier multimédia**: spécifiez le nom et le chemin des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Exemple : `\\servername\folder\outputfile.wim`  

    - **Dossier intermédiaire**<!--1359388-->: le processus de création de média est susceptible de prendre beaucoup d’espace lecteur temporaire. Par défaut, cet emplacement est semblable au suivant : `%UserProfile%\AppData\Local\Temp`. À compter de la version 1902, remplacez cette valeur par un autre lecteur et un autre chemin d’accès pour choisir où stocker ces fichiers temporaires.  

6. Sur la page **Sécurité**, spécifiez les options suivantes :  

    - **Activer la prise en charge des ordinateurs inconnus** : autorisez le média à déployer un système d’exploitation sur un ordinateur non géré par Configuration Manager. Il n’y a aucun enregistrement de ces ordinateurs dans la base de données Configuration Manager. Pour plus d’informations, voir [Préparer les déploiements d’ordinateurs inconnus](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

    - **Protéger le média par un mot de passe** : entrez un mot de passe fort pour mieux protéger le média contre les accès non autorisés. Lorsque vous spécifiez un mot de passe, l'utilisateur doit fournir ce mot de passe pour utiliser le média préparé.  

        > [!IMPORTANT]  
        > Pour une sécurité optimale, il vous est conseillé de toujours attribuer un mot de passe pour protéger les médias préparés.  

    - Pour les communications HTTP, sélectionnez **Créer un certificat de média auto-signé**. Ensuite, spécifiez la date de début et la date d’expiration du certificat.  

    - Pour les communications HTTPS, sélectionnez **Importer un certificat PKI**. Ensuite, spécifiez le certificat à importer et son mot de passe.  

        Pour plus d’informations sur ce certificat client utilisé par les images de démarrage, voir [Exigences des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

    - **Affinité entre utilisateur et périphérique** : pour prendre en charge la gestion centrée sur l’utilisateur dans Configuration Manager, spécifiez la manière dont le média devra associer les utilisateurs à l’ordinateur de destination. Pour plus d’informations sur la prise en charge de l’affinité entre utilisateur et périphérique par le déploiement de système d’exploitation, voir [Associer des utilisateurs à un ordinateur de destination](/sccm/osd/get-started/associate-users-with-a-destination-computer).  

        - **Autoriser l’affinité entre utilisateur et périphérique avec approbation automatique** : le média associe automatiquement les utilisateurs à l’ordinateur de destination. Cette fonctionnalité dépend des actions de la séquence de tâches qui déploie le système d’exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination lors du déploiement du système d’exploitation sur l’ordinateur de destination.  

        - **Autoriser l’affinité entre utilisateur et périphérique dans l’attente de l’approbation de l’administrateur** : le média associe les utilisateurs à l’ordinateur de destination une fois l’approbation accordée. Cette fonctionnalité dépend de l’étendue de la séquence de tâches qui déploie le système d’exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l’ordinateur de destination, mais attend l’approbation d’un utilisateur administratif avant le déploiement du système d’exploitation.  

        - **Ne pas utiliser d’affinité entre utilisateur et périphérique** : le média n’associe pas les utilisateurs à l’ordinateur de destination. Dans ce scénario, la séquence de tâches n’associe pas les utilisateurs à l’ordinateur de destination lors du déploiement du système d’exploitation.  

7. Sur la page **Séquence de tâches**, sélectionnez la séquence de tâches qui s’exécutera sur l’ordinateur de destination. Vérifiez la liste de contenu associée à la séquence de tâches.  

    - **Détecter les dépendances d’applications associées et les ajouter à ce média** : ajoutez également du contenu au média pour les dépendances d’applications.  

        > [!TIP]  
        > Si les dépendances d’applications attendues n’apparaissent pas, désélectionnez, puis resélectionnez cette option pour actualiser la liste.  

8. Sur la page **Image de démarrage**, spécifiez les options suivantes :  

    > [!IMPORTANT]  
    > L’architecture de l’image de démarrage distribuée doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.  

    - **Image de démarrage** : sélectionnez l’image de démarrage permettant de démarrer l’ordinateur de destination.  

    - **Point de distribution** : sélectionnez le point de distribution comportant l’image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

        > [!NOTE]  
        > Votre compte d’utilisateur doit au moins disposer d’autorisations d’accès en **Lecture** à la bibliothèque de contenu du point de distribution.  

    - **Point de gestion** : uniquement pour *Média basé sur le site*, sélectionnez un point de gestion issu d’un site principal.  

    - **Points de gestion associés** : uniquement pour *Média dynamique*, sélectionnez les points de gestion de site principal à utiliser et un ordre de priorité pour la communication initiale.  

9. Sur la page **Images**, spécifiez les options suivantes :  

    - **Package d’images** : spécifiez l’image de système d’exploitation à utiliser. Pour plus d’informations, consultez [Gérer les images de système d’exploitation](/sccm/osd/get-started/manage-operating-system-images).  

    - **Index d’images** : si le package contient plusieurs images de système d’exploitation, spécifiez l’index de l’image à déployer.  

    - **Point de distribution** : spécifiez le point de distribution comportant le package d’images de système d’exploitation. L’Assistant récupère l’image de système d’exploitation auprès du point de distribution et l’écrit sur le média.  

10. Sur la page **Sélectionner des applications**, sélectionnez des applications supplémentaires à ajouter au fichier de média préparé.  

11. Sur la page **Sélectionner des packages**, sélectionnez des packages supplémentaires à ajouter au fichier de média préparé.  

12. Sur la page **Sélectionner des packages de pilotes**, sélectionnez des packages de pilotes supplémentaires à ajouter au fichier de média préparé.  

13. Sur la page **Points de distribution**, sélectionnez un ou plusieurs points de distribution permettant de récupérer le contenu.  

    Configuration Manager n’affiche que les points de distribution qui disposent du contenu. Distribuez tout le contenu associé à la séquence de tâches sur au moins un point de distribution avant de continuer. Après avoir distribué le contenu, actualisez la liste des points de distribution. Supprimez les points de distribution que vous avez déjà sélectionnés dans cette page, accédez à la page précédente, puis revenez à la page **Points de Distribution**. Vous pouvez également redémarrer l’Assistant. Pour plus d’informations, consultez [Distribuer du contenu référencé par une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DistributeTS) et [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  

14. Sur la page **Personnalisation**, spécifiez les options suivantes :  

    - Ajoutez toutes les variables utilisées par la séquence de tâches.  

    - **Activer les commandes de prédémarrage** : spécifiez les commandes de prédémarrage à exécuter avant l’exécution de la séquence de tâches. Il s’agit d’un script ou d’un exécutable capable d’interagir avec l’utilisateur dans Windows PE avant que la séquence de tâches ne commence. Pour plus d’informations, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](/sccm/osd/understand/prestart-commands-for-task-sequence-media).  

        > [!TIP]  
        > Lors de la création du média, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des éventuelles variables de la séquence de tâches, dans le fichier **CreateTSMedia.log** sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

        Si certains contenus sont nécessaires à la commande de prédémarrage, sélectionnez l’option **Inclure les fichiers de la commande de prédémarrage**.  

15. Effectuez toutes les étapes de l'Assistant.  


## <a name="next-steps"></a>Étapes suivantes

[Créer une image pour un fabricant OEM en usine ou dépôt local](/sccm/osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot)
