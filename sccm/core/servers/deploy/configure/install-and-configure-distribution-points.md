---
title: Gestion des points de distribution
titleSuffix: Configuration Manager
description: Héberger le contenu que vous déployez sur des appareils et des utilisateurs à l’aide de points de distribution
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1c9e6dc50b47a1cfcf12f23eaf607eb55837a57d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-configure-distribution-points-for-system-center-configuration-manager"></a>Installer et configurer des points de distribution pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Installez des points de distribution Configuration Manager pour héberger les fichiers de contenu que vous déployez sur des appareils et des utilisateurs. Créez des groupes de points de distribution pour simplifier la gestion des points de distribution, ainsi que la distribution du contenu aux points de distribution.  

 Lorsque vous *installez un nouveau point de distribution* (à l’aide de l’Assistant Installation) ou que vous *gérez les propriétés d’un point de distribution* (en les modifiant), vous pouvez configurer la plupart des paramètres du point de distribution. Certains paramètres ne sont disponibles que lorsque vous effectuez une installation ou une modification, mais pas les deux :  

-   Paramètres disponibles uniquement lors de l’installation d’un point distribution :  

    -   **Allow Configuration Manager to install IIS on the distribution point computer (Autoriser Configuration Manager à installer IIS sur l’ordinateur du point de distribution)**

    -   **Configure drive space settings for the distribution point (Configurer les paramètres d’espace disque pour le point de distribution)**  

-   Paramètres disponibles seulement pendant lorsque vous modifiez les propriétés d’un point distribution :  

    -   **Manage distribution point group relationships (Gérer les relations d’un groupe de points de distribution)**  

    -   **View Content deployed to the distribution point (Afficher le contenu déployé sur le point de distribution)**  

    -   **Configure Rate limits for data transfers to distribution points (Configurer des limites de taux pour les transferts de données vers les points de distribution)**  

    -   **Configure Schedules for data transfers to distribution points (Configurer des planifications pour les transferts de données vers les points de distribution)**  

##  <a name="bkmk_install"></a> Installer un point de distribution  
Désignez un serveur de système de site comme point de distribution pour rendre le contenu disponible pour les ordinateurs clients. Affectez un point de distribution à au moins un [groupe de limites](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points) pour que les ordinateurs clients locaux puissent utiliser ce point de distribution comme emplacement source de contenu. Ajoutez le rôle de site de point de distribution à un nouveau serveur de système de site ou ajoutez le rôle de site à un serveur de système de site existant.


 Quand vous installez un nouveau point de distribution, vous utilisez un Assistant d’installation qui vous guide à travers les paramètres disponibles. Avant de commencer, tenez compte des prérequis suivants :  

-   Pour créer et configurer un point de distribution, vous devez disposer des autorisations de sécurité suivantes :  

    -   **Lecture** pour l'objet **Point de distribution**  

    -   **Copier vers le point de distribution** pour l'objet **Point de distribution**  

    -   **Modifier** pour l'objet **Site**  

    -   **Gérer des certificats pour le déploiement de système d'exploitation** pour l'objet **Site**  

-   Installez IIS (Internet Information Services) sur le serveur qui héberge le point de distribution. Quand vous installez le rôle de système de site, Configuration Manager peut installer et configurer IIS automatiquement.  

Utilisez les procédures de base suivantes pour installer ou modifier un point de distribution. Pour plus d’informations sur les options de configuration disponibles, consultez la section [Configurer un point de distribution](#bkmk_configs) de cette rubrique.  

#### <a name="to-install-a-distribution-point"></a>Pour installer un point de distribution  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Serveurs et rôles de système de site**.  

2.  Ajoutez le rôle de système de site de point de distribution à un serveur de système de site nouveau ou existant :  

    -   **Nouveau serveur de système de site** : dans l’onglet **Accueil** puis dans le groupe **Créer**, choisissez **Créer un serveur de système de site**. L'Assistant Création de serveur de système de site s'ouvre.  

    -   **Serveur de système de site existant** : choisissez le serveur sur lequel vous souhaitez installer le rôle de système de site du point de distribution. Lorsque vous choisissez un serveur, la liste des rôles de système de site déjà installés sur le serveur s’affiche dans le panneau des résultats.  

         Dans l’onglet **Accueil** puis dans le groupe **Serveur**, choisissez **Ajouter des rôles de système de site**. L'Assistant Ajout de rôles de système de site s'ouvre.  

3.  Sur la page **Général** , spécifiez les paramètres généraux du serveur de système de site. Lorsque vous ajoutez le point de distribution à un serveur de système de site existant, vérifiez les valeurs qui ont été précédemment configurées.  

4.  Dans la page **Sélection du rôle système**, choisissez **Point de distribution** dans la liste des rôles disponibles, puis choisissez **Suivant**.  

5.  Pour les pages suivantes de l’Assistant, consultez les informations fournies dans la section [Configurer un point de distribution](#bkmk_configs).  

     Par exemple, si vous souhaitez installer le point de distribution en tant que point de distribution d’extraction, choisissez **Activer ce point de distribution pour extraire le contenu à partir d’autres points de distribution**, puis procédez aux configurations supplémentaires requises par les points de distribution d’extraction.  

6.  Après avoir fermé l’Assistant, le rôle de site du point de distribution est ajouté au serveur de système de site.  

#### <a name="to-change-a-distribution-point"></a>Pour modifier un point de distribution  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Points de distribution**, puis sélectionnez le point de distribution à configurer.  

2.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

3.  Utilisez les informations de la section [Configurer un point de distribution](#bkmk_configs) pour modifier les propriétés du point de distribution.  

4.  Après avoir apporté les modifications souhaitées, enregistrez vos paramètres et fermez la page des propriétés.  

##  <a name="bkmk_manage"></a> Gérer les groupes de points de distribution  
 Les groupes de points de distribution fournissent un regroupement logique de points de distribution pour la distribution de contenu. Vous pouvez utiliser ces groupes pour gérer et surveiller de manière centralisée le contenu des points de distribution qui s’étendent sur plusieurs sites. Gardez à l’esprit les points suivants :

-   Vous pouvez ajouter un ou plusieurs points de distribution à partir de n’importe quel site de la hiérarchie, dans un groupe de points de distribution.  

-   Vous pouvez ajouter un point de distribution à plusieurs groupes de points de distribution.  

-   Lorsque vous diffusez du contenu à un groupe de points de distribution, Configuration Manager le distribue à tous les points de distribution membres de ce groupe.  

-   Si vous ajoutez un point de distribution au groupe de points de distribution après une distribution de contenu initiale, Configuration Manager distribue automatiquement le contenu au nouveau membre du groupe.  

-   Vous pouvez associer un regroupement à un groupe de points de distribution. Lorsque vous distribuez du contenu à ce regroupement, Configuration Manager identifie les groupes de points de distribution associés au regroupement. Le contenu est ensuite distribué à tous les points de distribution qui sont membres de ces groupes de points de distribution.  

    > [!NOTE]  
    >  Si, après avoir distribué du contenu à un regroupement, vous associez ce regroupement à un nouveau groupe de points de distribution, vous devez redistribuer le contenu au regroupement pour pouvoir distribuer le contenu au nouveau groupe.  

#### <a name="to-create-and-configure-a-new-distribution-point-group"></a>Pour créer et configurer un nouveau groupe de points de distribution  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Groupes de points de distribution**.  

2.  Dans l’onglet **Accueil** puis dans le groupe **Créer**, choisissez **Créer un groupe**.  

3.  Entrez le nom et la description du groupe de points de distribution.  

4.  Dans l’onglet **Regroupements**, cliquez sur **Ajouter**, sélectionnez les regroupements à associer au groupe de points de distribution, puis choisissez **OK**.  

5.  Dans l’onglet **Membres**, choisissez **Ajouter**, sélectionnez les points de distribution à ajouter comme membres du groupe de points de distribution, puis choisissez **OK**.  

6.  Choisissez **OK** pour créer le groupe de points de distribution.  

#### <a name="to-add-distribution-points-and-associate-collections-with-an-existing-distribution-point-group"></a>Pour ajouter des points de distribution et associer des regroupements à un groupe de points de distribution  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Groupes de points de distribution**.  

2.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

3.  Dans l’onglet **Regroupements**, choisissez **Ajouter** pour sélectionner les regroupements à associer au groupe de points de distribution, puis choisissez **OK**.  

4.  Dans l’onglet **Membres**, choisissez **Ajouter** pour sélectionner les points de distribution à ajouter comme membres du groupe de points de distribution, puis choisissez **OK**.  

5.  Choisissez **OK** pour enregistrer les modifications apportées au groupe de points de distribution.  

#### <a name="to-add-selected-distribution-points-to-a-new-distribution-point-group"></a>Pour ajouter les points de distribution sélectionnés à un nouveau groupe de points de distribution  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Points de distribution**, puis sélectionnez les points de distribution à ajouter au nouveau groupe de points de distribution.  

2.  Dans l’onglet **Accueil** puis dans le groupe **Point de distribution**, développez **Ajouter les éléments sélectionnés**, puis choisissez **Ajouter les éléments sélectionnés au nouveau groupe de points de distribution**.  

3.  Entrez le nom et la description du groupe de points de distribution.  

4.  Dans l’onglet **Regroupements**, choisissez **Ajouter** pour sélectionner les regroupements à associer au groupe de points de distribution, puis choisissez **OK**.  

5.  Sous l’onglet **Membres**, confirmez votre souhait de voir Configuration Manager ajouter les points de distribution répertoriés en tant que membres du groupe de points de distribution. Choisissez **Ajouter** pour ajouter les points de distribution, puis choisissez **OK**.  

6.  Choisissez **OK** pour créer le groupe de points de distribution.  

#### <a name="to-add-selected-distribution-points-to-existing-distribution-point-groups"></a>Pour ajouter les points de distribution sélectionnés à des groupes de points de distribution existants  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Points de distribution**, puis sélectionnez les points de distribution à ajouter au nouveau groupe de points de distribution.  

2.  Dans l’onglet **Accueil** puis dans le groupe **Point de distribution**, développez **Ajouter les éléments sélectionnés**, puis choisissez **Ajouter les éléments sélectionnés aux groupes de points de distribution existants**.  

3.  Dans **Groupes de points de distribution disponibles**, sélectionnez les groupes de points de distribution auxquels les points de distribution sélectionnés doivent être ajoutés en tant que membres, puis choisissez **OK**.  



## <a name="reassign-a-distribution-point"></a>Réaffecter un point de distribution
<!-- 1306937 -->
De nombreux clients ont de grandes infrastructures Configuration Manager et réduisent le nombre de sites principaux ou secondaires pour simplifier leur environnement. Ils doivent néanmoins toujours conserver des points de distribution aux emplacements des filiales pour délivrer du contenu aux clients gérés. Ces points de distribution contiennent souvent plusieurs téraoctets ou plus de contenus. Ce contenu est coûteux en termes de temps et de bande passante réseau pour le distribuer à ces serveurs distants. 

Depuis la version 1802, cette fonctionnalité vous permet de réaffecter un point de distribution à un autre site principal sans redistribuer le contenu. Cette action met à jour l’affectation du système de site tout en conservant la totalité du contenu sur le serveur. Si vous devez réaffecter plusieurs points de distribution, effectuez d’abord cette action sur un seul point de distribution, puis poursuivez avec les serveurs supplémentaires, un par un.

> [!IMPORTANT]
> Le serveur cible peut seulement héberger le rôle de point de distribution. Si le serveur de système de site héberge un autre rôle serveur Configuration Manager, comme le point de migration d’état, vous ne pouvez pas réaffecter le point de distribution. Vous ne pouvez pas réaffecter un point de distribution cloud. 

Avant de réaffecter un point de distribution, ajoutez le compte d’ordinateur du serveur de site de destination au groupe Administrateur local sur le serveur de point de distribution cible. 

Effectuez les étapes suivantes pour réaffecter un point de distribution :
1. Dans la console Configuration Manager, connectez-vous au site d’administration centrale. 
2. Accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Points de distribution**.
3. Cliquez avec le bouton droit sur le point de distribution cible, puis sélectionnez **Réaffecter le point de distribution**. 
4. Sélectionnez le serveur de site cible auquel vous voulez réaffecter ce point de distribution ainsi que le code de site. 

Surveillez la réaffectation de la même façon que quand vous ajoutez un nouveau rôle. La méthode la plus simple consiste à actualiser l’affichage de la console après quelques minutes. Ajoutez la colonne de code de site à l’affichage. Cette valeur change quand Configuration Manager réaffecte le serveur. Si vous essayez d’effectuer une autre action sur le serveur cible avant d’actualiser l’affichage de la console, une erreur « objet introuvable » se produit. Vérifiez que le processus est terminé et actualisez l’affichage de la console avant de démarrer d’autres actions sur le serveur.

Après la réaffectation d’un point de distribution, actualisez le certificat du serveur. Le nouveau serveur de site doit chiffrer à nouveau ce certificat à l’aide de sa clé publique et le stocker dans la base de données de site. Pour plus d’informations, consultez le paramètre **Créez un certificat auto-signé ou importez un certificat client d’infrastructure à clé publique (PKI) pour le point de distribution** sous l’onglet [Général](#general) des propriétés du point de distribution. 
- Pour les certificats d’infrastructure à clé publique, vous n’avez pas besoin de créer un certificat. Importez le même fichier .PFX et entrez le mot de passe.
- Pour les certificats auto-signés, réglez la date ou l’heure d’expiration pour la mettre à jour.
Si vous n’actualisez pas le certificat, le point de distribution délivre toujours le contenu, mais les fonctions suivantes échouent :
    - Messages de validation du contenu (le fichier distmgr.log indique qu’il ne peut pas déchiffrer le certificat)
    - Prise en charge PXE pour les clients 

### <a name="tips"></a>Conseils
- Effectuez cette action à partir du site d’administration centrale. Cette pratique facilite la réplication vers les sites principaux.
- Ne distribuez pas de contenu vers le serveur cible pour tenter ensuite de le réaffecter. Les tâches de distribution de contenu en cours risquent d’échouer pendant le processus de réaffectation, mais elles sont retentées comme d’habitude.
- Si le serveur est également un client Configuration Manager, veillez à réaffecter également le client au nouveau site principal. Cette étape est particulièrement importante pour les points de distribution d’extraction, qui utilisent des composants clients pour télécharger du contenu.
- Ce processus supprime le point de distribution du groupe de limites par défaut de l’ancien site. Vous devez l’ajouter manuellement au groupe de limites par défaut du nouveau site, si nécessaire. Toutes les autres affectations de groupes de limites restent les mêmes.



##  <a name="bkmk_configs"></a> Configurer un point de distribution  
 Chaque point de distribution prend en charge plusieurs configurations différentes. Toutefois, tous les types de point de distribution ne prennent pas en charge toutes les configurations. Par exemple, les points de distribution cloud ne prennent pas en charge les déploiements de contenu activés pour PXE ou la multidiffusion. Les rubriques suivantes contiennent des informations sur certaines limitations :  

-   [Utiliser un point de distribution cloud avec System Center Configuration Manager](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

-   [Utiliser un point de distribution d’extraction avec System Center Configuration Manager](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

Les sections suivantes décrivent les configurations que vous pouvez sélectionner pendant l’installation d’un nouveau point de distribution ou la modification des propriétés d’un point de distribution.  

### <a name="general"></a>Général  
 Configurez les paramètres généraux des points de distribution :  

-   **Installer et configurer IIS si requis par Configuration Manager** : sélectionnez ce paramètre pour permettre à Configuration Manager d’installer et de configurer IIS sur le serveur si IIS n’est pas déjà installé. Les services Internet doivent être installés sur tous les points de distribution. Si IIS n’est pas installé sur le serveur et si vous ne sélectionnez pas ce paramètre, vous devez installer IIS pour pouvoir installer le point de distribution.  

    > [!NOTE]  
    >  Cette option n’est disponible que lorsque vous installez un nouveau point de distribution.  

- **Activer et configurer BranchCache pour ce point de distribution** : sélectionnez ce paramètre pour permettre à Configuration Manager de configurer Windows BranchCache sur le serveur de point de distribution. Pour plus d’informations sur l’utilisation de Windows BranchCache avec System Center Configuration Manager, consultez [BranchCache](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#a-namebkmkbranchcachea-branchcache) dans *Prise en charge des fonctionnalités de Windows et des réseaux dans System Center Configuration Manager*.

-   **Configure how client devices communicate with the distribution point (Configurer comment les appareils clients communiquent avec le point de distribution)** : l’utilisation de HTTP et de HTTPS présente des avantages et des inconvénients. Pour plus d’informations, consultez Meilleures pratiques de sécurité pour la gestion de contenu dans [Principes de base de la gestion de contenu dans System Center Configuration Manager](../../../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

-   **Autoriser les clients à se connecter anonymement** : ce paramètre indique si le point de distribution autorise les connexions anonymes des clients Configuration Manager à la bibliothèque de contenu.  

    > [!IMPORTANT]  
    >  La réparation d’une application Windows Installer sur un client peut échouer si vous n’utilisez pas ce paramètre.  
    >   
    >  Lorsque vous déployez une application Windows Installer sur un client Configuration Manager, Configuration Manager télécharge le fichier dans le cache local du client. Les fichiers sont supprimés, une fois l’installation terminée.
    >  
    >  Le client Configuration Manager met à jour la liste source Windows Installer des applications Windows Installer installées avec le chemin de contenu de la bibliothèque de contenu sur les points de distribution associés. Par la suite, si vous démarrez l’action de réparation via Ajout/Suppression de programmes sur un client Configuration Manager, MSIExec tente d’accéder au chemin de contenu avec un compte d’utilisateur anonyme.  
    >   
    >  Vous pouvez toutefois changer ce comportement en installant la mise à jour décrite dans l’article [2619572](http://go.microsoft.com/fwlink/?LinkId=279699) de la Base de connaissances Microsoft, puis en modifiant une clé de Registre.  
    >   
    >  Une fois la mise à jour installée sur les clients, MSIExec accède au chemin du contenu en utilisant le compte d’utilisateur connecté, lorsque vous ne choisissez pas le paramètre **Autoriser les clients à se connecter anonymement**.  

-   **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point (Créer un certificat auto-signé ou importer un certificat client d’infrastructure à clé publique (PKI) pour le point de distribution)** : le certificat remplit les fonctions suivantes :  

    -   Il authentifie le point de distribution à un point de gestion avant que le point de distribution n'envoie des messages d'état.  

    -   Lorsque vous activez la case à cocher **Activer la prise en charge PXE pour les clients** sur la page **Paramètres PXE**, le certificat est envoyé aux ordinateurs qui redémarrent PXE pour pouvoir se connecter à un point de gestion pendant le déploiement du système d’exploitation.  

    Lorsque tous vos points de gestion du site sont configurés pour le protocole HTTP, créez un certificat auto-signé. Lorsque vos points de gestion sont configurés pour le protocole HTTPS, importez un certificat client PKI.  

    Pour importer le certificat, accédez à un fichier PKCS #12 (Public Key Cryptography Standard #12) qui contient un certificat PKI avec les spécifications suivantes pour Configuration Manager :  

    -   L'utilisation prévue doit inclure l'authentification du client.  

    -   La clé privée doit être activée pour l’exportation.  

    > [!TIP]  
    >  Il n'existe aucune exigence particulière pour l'objet du certificat ou le nom alternatif d'objet du certificat (SAN), et vous pouvez utiliser le même certificat pour plusieurs points de distribution.  

     Pour plus d’informations sur la configuration requise pour les certificats, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

     Pour obtenir un exemple de déploiement de ce certificat, consultez la section Déployer le certificat client pour les points de distribution de la rubrique [Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

-   **Activer ce point de distribution pour le contenu préparé** : choisissez ce paramètre pour activer le point de distribution du contenu préparé. Lorsque ce paramètre est sélectionné, vous pouvez configurer le comportement de distribution lors de la distribution du contenu. Vous pouvez choisir de toujours effectuer l’une des actions suivantes :

 - Préparer le contenu sur le point de distribution.
 - Préparer le contenu initial du package, puis utiliser le processus de distribution de contenu standard lorsque le contenu fait l’objet de mises à jour.
 - Utiliser le processus de distribution standard pour le contenu du package.  

### <a name="drive-settings"></a>Paramètres du lecteur  

> [!NOTE]  
>  Ces options ne sont disponibles que lorsque vous installez un nouveau point de distribution.  

Spécifiez les paramètres du lecteur pour le point de distribution. Vous pouvez configurer jusqu’à deux lecteurs de disque pour la bibliothèque de contenu et deux lecteurs de disque pour le partage de package. Configuration Manager peut utiliser des lecteurs supplémentaires lorsque les deux premiers atteignent la réserve d’espace disque configurée. La page **Paramètres du lecteur** permet de configurer la priorité des lecteurs de disque et la quantité d'espace disque libre restant sur chaque lecteur de disque.  

-   **Réserve d’espace libre sur le lecteur (Mo)**  : la valeur que vous configurez pour ce paramètre détermine la quantité d’espace libre sur un lecteur avant que Configuration Manager choisisse un autre lecteur et poursuive le processus de copie sur ce lecteur. Les fichiers de contenu peuvent s'étendre sur plusieurs lecteurs.  

-   **Emplacements du contenu**: Spécifiez les emplacements de contenu pour le partage de bibliothèque et de package de contenu. Configuration Manager copie le contenu à l’emplacement de contenu principal jusqu’à ce que la quantité d’espace libre atteigne la valeur spécifiée dans **Réserve d’espace libre sur le lecteur (Mo)**. Par défaut, les emplacements du contenu sont définis sur **Automatique**. L’emplacement de contenu principal est défini sur le lecteur de disque disposant le plus d’espace lors de l’installation. L’emplacement secondaire, quant à lui, est attribué au deuxième lecteur de disque disposant le plus d’espace. Quand le lecteur principal et le lecteur secondaire atteignent la réserve d’espace libre sur le lecteur, Configuration Manager sélectionne un autre lecteur disponible ayant le plus d’espace disque libre et poursuit le processus de copie.  

> [!NOTE]  
>  Pour empêcher l’installation de Configuration Manager sur un lecteur spécifique, créez un fichier vide intitulé **no_sms_on_drive.sms** et copiez-le dans le dossier racine du lecteur avant d’installer le point de distribution.  

### <a name="pull-distribution-point"></a>Point de distribution d'extraction  
Quand vous choisissez **Activer ce point de distribution pour extraire le contenu à partir d’autres points de distribution**, vous modifiez la méthode employée par l’ordinateur pour obtenir le contenu que vous distribuez au point de distribution. Ce point de distribution devient un point de distribution d’extraction.  

Pour chaque point de distribution d’extraction que vous configurez, vous devez spécifier un ou plusieurs points de distribution sources à partir desquels le point de distribution d’extraction obtient le contenu :  

-   Choisissez **Ajouter**, puis sélectionnez un ou plusieurs des points de distribution disponibles comme points de distribution sources.  

-   Choisissez **Supprimer** pour supprimer le point de distribution sélectionné comme point de distribution source.  

-   Utilisez les boutons fléchés pour définir l’ordre dans lequel le point de distribution d’extraction contacte les points de distribution sources lorsqu’il tente de transférer du contenu. Les points de distribution associés à la valeur la plus faible sont contactés en premier.  

### <a name="pxe"></a>Environnement PXE  
Indiquez si vous souhaitez activer l'environnement PXE sur le point de distribution. Quand vous activez l’environnement PXE, Configuration Manager installe les services de déploiement Windows (WDS) sur le serveur, si nécessaire. WDS est le service qui démarre PXE pour installer les systèmes d’exploitation. Après avoir effectué toutes les étapes de l’Assistant pour créer le point de distribution, Configuration Manager installe dans WDS un fournisseur qui utilise les fonctions de démarrage PXE. 

Lorsque vous choisissez **Activer la prise en charge PXE pour les clients**, configurez les paramètres suivants :  

 > [!Note]  
 > Cliquez sur **Oui** dans la boîte de dialogue **Consulter les ports requis pour PXE** pour confirmer que vous souhaitez activer PXE. Configuration Manager configure automatiquement les ports par défaut dans le Pare-feu Windows. Vous devez configurer manuellement les ports si vous utilisez un autre pare-feu.  
 >   
 > Si WDS et DHCP sont installés sur le même serveur, vous devez configurer WDS pour écouter sur un port différent. Par défaut, DHCP écoute sur le même port. Pour plus d’informations, consultez [Considérations quand vous avez WDS et DHCP sur le même serveur](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#BKMK_WDSandDHCP).  

-   **Autoriser ce point de distribution à répondre aux requêtes PXE entrantes** : indiquez si WDS doit être activé pour répondre aux demandes de service PXE. Utilisez cette case à cocher pour activer et désactiver le service sans supprimer la fonctionnalité PXE du point de distribution.  

-   **Activer la prise en charge d’ordinateur inconnu** : indiquez si la prise en charge des ordinateurs non gérés par Configuration Manager doit être activée. 

-   **Exiger un mot de passe lorsque les ordinateurs utilisent PXE**: pour renforcer la sécurité de vos déploiements PXE, spécifiez un mot de passe fort.  

-   **Affinité entre appareil et utilisateur**: indiquez de quelle manière le point de distribution doit associer les utilisateurs à l'ordinateur de destination dans le cadre des déploiements PXE. Choisissez l'une des options suivantes :  

    -   **Autoriser une affinité entre périphérique et utilisateur avec approbation automatique** : choisissez ce paramètre pour associer automatiquement les utilisateurs à l’ordinateur de destination sans attendre l’approbation.  

    -   **Autoriser une affinité entre périphérique et utilisateur en attente de l’approbation de l’administrateur** : choisissez ce paramètre pour attendre l’approbation d’un utilisateur administratif avant d’associer des utilisateurs à l’ordinateur de destination.  

    -   **Ne pas autoriser d’affinité entre périphérique et utilisateur** : choisissez ce paramètre pour empêcher l’association d’utilisateurs à l’ordinateur de destination.  

     Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

-   **Interfaces réseau**: Spécifiez que le point de distribution répond aux requêtes PXE à partir de toutes les interfaces réseau ou d'interfaces réseau spécifiques. Si le point de distribution répond à des interfaces réseau spécifiques, vous devez fournir l’adresse MAC pour chaque interface réseau.  

-   **Spécifier le délai de réponse du serveur PXE (secondes)** : indiquez, en secondes, le délai d’attente à l’issue duquel le point de distribution répond aux requêtes de l’ordinateur lorsque plusieurs points de distribution PXE sont utilisés. Par défaut, le point de service PXE de Configuration Manager répond d’abord aux demandes PXE du réseau.  

> [!NOTE]  
>  Le protocole PXE permet de démarrer les déploiements de système d’exploitation sur les ordinateurs clients Configuration Manager. Configuration Manager utilise le rôle de site du point de distribution PXE pour lancer le processus de déploiement du système d’exploitation. Le point de distribution PXE doit être configuré pour :
>
> 1. Répondre aux demandes de démarrage PXE émanant des clients Configuration Manager sur le réseau.
> 2. Interagir avec l’infrastructure Configuration Manager pour déterminer les actions de déploiement appropriées à entreprendre.  

### <a name="multicast"></a>Multidiffusion  
Indiquez si vous souhaitez activer la multidiffusion sur le point de distribution. Quand vous activez la multidiffusion, Configuration Manager installe les services de déploiement Windows (WDS) sur le serveur, si nécessaire.  

Quand vous cochez la case **Activer la multidiffusion pour envoyer simultanément des données à plusieurs clients**, configurez les paramètres suivants :  

-   **Compte de connexion multidiffusion** : indiquez le compte à utiliser quand vous configurez des connexions de base de données Configuration Manager pour la multidiffusion.  

-   **Paramètres de l’adresse de multidiffusion** : spécifiez les adresses IP pour envoyer des données vers les ordinateurs de destination. Par défaut; l'adresse IP est fournie par un serveur DCHP chargé de distribuer des adresses de multidiffusion. Selon l’environnement réseau, vous pouvez spécifier une plage d’adresses IP entre 239.0.0.0 et 239.255.255.255.  

    > [!IMPORTANT]  
    >  Les adresses IP que vous configurez doivent être accessibles par les ordinateurs de destination qui demandent l'image du système d'exploitation. Vérifiez que les routeurs et pare-feu autorisent le trafic de multidiffusion entre l'ordinateur de destination et le serveur de site.  

-   **Étendue du port UDP pour la multidiffusion** : spécifiez la plage de ports UDP (User Datagram Protocol) utilisés pour envoyer des données aux ordinateurs de destination.  

    > [!IMPORTANT]  
    >  Les ports UDP doivent être accessibles par les ordinateurs de destination qui demandent l'image du système d'exploitation. Vérifiez que les routeurs et pare-feu autorisent le trafic de multidiffusion entre l'ordinateur de destination et le serveur de site.  

-   **Taux de transfert client**: Sélectionnez la vitesse de transfert utilisée pour télécharger des données sur les ordinateurs de destination.  

-   **Nombre maximum de clients**: Spécifiez le nombre maximal d'ordinateurs de destination qui peuvent télécharger le système d'exploitation à partir de ce point de distribution.  

-   **Activer la multidiffusion planifiée** : indiquez comment Configuration Manager contrôle le lancement du déploiement des systèmes d’exploitation sur les ordinateurs de destination. Configurez les options suivantes :  

    -   **Délai de démarrage de session (en minutes)**  : indiquez le nombre de minutes écoulé avant que Configuration Manager réponde à la première demande de déploiement.  

    -   **Taille minimale de la session (clients)**  : indiquez le nombre de demandes qui doivent être reçues avant que Configuration Manager commence à déployer le système d’exploitation.  

> [!NOTE]  
>  Les déploiements de multidiffusion économisent la bande passante réseau en envoyant de manière simultanée des données à plusieurs clients Configuration Manager au lieu d’envoyer une copie des données à chaque client via une connexion distincte. Pour plus d’informations sur l’utilisation de la multidiffusion pour le déploiement de systèmes d’exploitation, consultez [Utiliser la multidiffusion pour Windows sur le réseau avec System Center Configuration Manager](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  



### <a name="group-relationships"></a>Relations de groupe  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  

Gérez les groupes de points de distribution dont ce point de distribution est membre.  

Pour ajouter ce point de distribution en tant que membre à un groupe de points de distribution, choisissez **Ajouter**. Sélectionnez un groupe de points de distribution dans la liste de la boîte de dialogue **Ajouter aux groupes de points de distribution**, puis choisissez **OK**.  

Pour supprimer ce point de distribution d’un groupe de points de distribution, sélectionnez le groupe dans la liste, puis choisissez **Supprimer**.  

### <a name="content"></a>Content  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  

Gérez le contenu qui a été distribué au point de distribution. La section **Packages de déploiement** fournit la liste des packages distribués à ce point de distribution. Vous pouvez sélectionner un package dans la liste, puis effectuer les actions suivantes :  

-   **Valider**: Démarre le processus de validation de l'intégrité des fichiers de contenu dans le package. Pour afficher les résultats du processus de validation du contenu, dans l’espace de travail **Surveillance**, développez **État de distribution**, puis choisissez le nœud **État du contenu**.  

-   **Redistribuer**: Copie tous les fichiers de contenu dans le package vers le point de distribution et remplace les fichiers existants. Vous utilisez généralement cette opération pour réparer les fichiers de contenu dans le package.  

-   **Supprimer**: Supprime les fichiers de contenu du point de distribution du package.  

### <a name="content-validation"></a>Validation du contenu  
Indiquez si vous souhaitez définir une planification pour valider l'intégrité des fichiers de contenu sur le point de distribution. Quand vous activez la validation de contenu selon une planification, Configuration Manager démarre le processus à l’heure planifiée, et tout le contenu est vérifié sur le point de distribution. Vous pouvez également configurer la priorité de la validation du contenu. Par défaut, la priorité est définie sur **La plus faible**.  

Pour afficher les résultats du processus de validation du contenu, dans l’espace de travail **Surveillance**, développez **État de distribution**, puis choisissez le nœud **État du contenu**. Le contenu de chaque type de package (par exemple, application, package de mises à jour logicielles et image de démarrage) s’affiche.  

> [!WARNING]  
>  Même si vous planifiez la validation du contenu en utilisant l’heure locale de l’ordinateur, la planification affichée dans la console Configuration Manager est exprimée en heure UTC.  

### <a name="boundary-group"></a>Groupes de limites  
Gérez les groupes de limites pour lesquels ce point de distribution est attribué. Prévoyez d’ajouter le point de distribution à au moins un groupe de limites. Au cours du déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé à un point de distribution pour utiliser ce dernier comme emplacement source de contenu.

Configurez des *relations* qui définissent à quel moment et auprès de quels groupes de limites un client peut effectuer une action de secours pour trouver du contenu. Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).


### <a name="schedule"></a>Planification  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  

> [!TIP]  
>  Cet onglet n’est disponible que lorsque vous modifiez les propriétés d’un point de distribution distant de l’ordinateur du serveur de site.  

 Indiquez s’il convient de configurer une planification qui limite la période de transfert de données de Configuration Manager vers le point de distribution.  

> [!IMPORTANT]  
>  La planification est basée sur le fuseau horaire du site émetteur, et non sur celui du point de distribution.  

Pour restreindre les données, sélectionnez la période, puis choisissez l’un des paramètres suivants sous **Disponibilité** :  

-   **Ouvrir pour toutes les priorités** : indique que Configuration Manager envoie les données au point de distribution sans restriction.  

-   **Autoriser les priorités moyennes et élevées** : indique que Configuration Manager n’envoie au point de distribution que les données de priorité moyenne et élevée.  

-   **Autoriser uniquement la priorité élevée** : indique que Configuration Manager n’envoie au point de distribution que les données de priorité élevée.  

-   **Fermé** : indique que Configuration Manager n’envoie pas de données au point de distribution.  

Vous pouvez limiter les données par priorité ou fermer la connexion durant des périodes sélectionnées.  

### <a name="rate-limits"></a>Limites du taux de transfert  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  

> [!TIP]  
>  Cet onglet n’est disponible que lorsque vous modifiez les propriétés d’un point de distribution distant de l’ordinateur du serveur de site.  

Spécifiez si vous souhaitez configurer des limites du taux de transfert pour contrôler la bande passante réseau utilisée lorsque Configuration Manager transfère du contenu vers le point de distribution. Vous pouvez choisir parmi les options suivantes :  

-   **Illimité lors de l’expédition de données à cette destination** : cette option spécifie que Configuration Manager envoie le contenu au point de distribution sans aucune limite de taux de transfert.  

-   **Mode impulsion** : cette option spécifie la taille des blocs de données qui sont envoyés au point de distribution. Vous pouvez également spécifier un délai entre l'envoi de chaque bloc de données. Utilisez cette option lorsque vous devez envoyer des données au point de distribution via une connexion réseau à très faible bande passante. Par exemple, vous pouvez forcer l'envoi de 1 Ko de données toutes les cinq secondes, quelle que soit la vitesse de la liaison ou son utilisation.  

-   **Limité aux taux de transfert maximaux indiqués par heure**: spécifiez ce paramètre pour qu'un site envoie des données à un point de distribution en utilisant uniquement le pourcentage de temps que vous avez configuré. Quand vous utilisez cette option, Configuration Manager n’identifie pas la bande passante disponible du réseau, mais divise le temps pendant lequel il peut envoyer des données. Puis les données sont envoyées pendant une courte plage horaire, suivie de plages horaires pendant lesquelles aucune donnée n'est envoyée. Par exemple, si le taux maximal est fixé à **50 %**, Configuration Manager transmet les données sur une période, qui est suivie d’une période égale où aucune donnée n’est envoyée. La taille effective des donnés ou la taille des blocs de données ne sont pas gérées. En revanche, seule la durée pendant laquelle des données sont envoyées est gérée.  
