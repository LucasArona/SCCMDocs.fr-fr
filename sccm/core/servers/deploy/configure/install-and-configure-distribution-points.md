---
title: Gestion des points de distribution
titleSuffix: Configuration Manager
description: Utilisez des points de distribution pour héberger le contenu que vous déployez pour des appareils et des utilisateurs.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3bd5a2b483551fc760b0dc69cd488bf1e3671732
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65498657"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Installer et configurer des points de distribution dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Installez des points de distribution Configuration Manager pour héberger les fichiers de contenu que vous déployez sur des appareils et des utilisateurs. Créez des groupes de points de distribution pour simplifier la gestion des points de distribution, ainsi que la distribution du contenu aux points de distribution.  

*Installez un nouveau point de distribution* à l’aide de l’Assistant Installation. Pour plus d’informations, consultez [Installer un point de distribution](#bkmk_install). Pour *gérer les propriétés d’un point de distribution existant*, modifiez ses propriétés. Pour plus d’informations, consultez [Configurer un point de distribution](#bkmk_configs). 

La plupart des paramètres de point de distribution peuvent être configurés avec l’une de ces méthodes. Certains paramètres ne sont disponibles que lorsque vous effectuez une installation ou une modification, mais pas les deux :  

-   Paramètres disponibles uniquement lors de l’installation d’un point distribution :  

    -   **Allow Configuration Manager to install IIS on the distribution point computer (Autoriser Configuration Manager à installer IIS sur l’ordinateur du point de distribution)**

    -   **Configure drive space settings for the distribution point (Configurer les paramètres d’espace disque pour le point de distribution)**  

-   Paramètres disponibles seulement pendant lorsque vous modifiez les propriétés d’un point distribution :  

    -   **Manage distribution point group relationships (Gérer les relations d’un groupe de points de distribution)**  

    -   **View Content deployed to the distribution point (Afficher le contenu déployé sur le point de distribution)**  

    -   **Configure Rate limits for data transfers to distribution points (Configurer des limites de taux pour les transferts de données vers les points de distribution)**  

    -   **Configure Schedules for data transfers to distribution points (Configurer des planifications pour les transferts de données vers les points de distribution)**  



##  <a name="bkmk_install"></a> Installer un point de distribution  

Choisissez un serveur de système de site comme point de distribution avant que le contenu ne soit disponible pour les ordinateurs clients. Affectez un point de distribution à au moins un [groupe de limites](/sccm/core/servers/deploy/configure/boundary-groups#distribution-points) pour que les ordinateurs clients locaux puissent utiliser ce point de distribution comme emplacement source de contenu. Ajoutez le rôle de site de point de distribution à un nouveau serveur de système de site, ou à un serveur de système de site existant.


### <a name="bkmk_install-prereq"></a> Conditions préalables

Quand vous installez un nouveau point de distribution, vous utilisez un Assistant d’installation qui vous guide à travers les paramètres disponibles. Avant de commencer, tenez compte des prérequis suivants :  

-   Pour créer et configurer un point de distribution, vous devez disposer des autorisations de sécurité suivantes :  

    -   **Lecture** pour l'objet **Point de distribution**  

    -   **Copier vers le point de distribution** pour l'objet **Point de distribution**  

    -   **Modifier** pour l'objet **Site**  

    -   **Gérer des certificats pour le déploiement de système d'exploitation** pour l'objet **Site**  

-   Installez Internet Information Services (IIS) sur le serveur Windows qui héberge le point de distribution. Sinon, quand vous installez le rôle de système de site, Configuration Manager peut installer et configurer IIS automatiquement.  


### <a name="bkmk_install-procedure"></a> Procédure d’installation d’un point de distribution  

Suivez cette procédure pour ajouter un nouveau point de distribution. Pour modifier la configuration d’un point de distribution existant, consultez la section [Configurer un point de distribution](#bkmk_configs).  

Démarrez par la procédure générale [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Sélectionnez le rôle **Point de distribution** dans la page **Sélection du rôle système** de l’Assistant Création d’un serveur de système de site. Cette action ajoute les pages suivantes à l’Assistant :  
- [Point de distribution](#bkmk_config-general)
- [Paramètres du lecteur](#bkmk_config-drive)
- [Point de distribution d’extraction](#bkmk_config-pull)
- [Paramètres PXE](#bkmk_config-pxe)
- [Multidiffusion](#bkmk_config-multicast)
- [Validation du contenu](#bkmk_config-valid)
- [Groupes de limites](#bkmk_config-boundary)

> [!Important]  
> Les paramètres suivants sont disponibles uniquement lors de l’installation d’un point distribution :  
> 
> - **Allow Configuration Manager to install IIS on the distribution point computer (Autoriser Configuration Manager à installer IIS sur l’ordinateur du point de distribution)**  
> 
> - **Configure drive space settings for the distribution point (Configurer les paramètres d’espace disque pour le point de distribution)**  

Pour plus d’informations sur les pages de l’Assistant qui concernent le rôle de point de distribution, consultez la section [Configurer un point de distribution](#bkmk_configs). Par exemple, si vous souhaitez installer le point de distribution comme un [point de distribution d’extraction](#bkmk_config-pull), choisissez l’option **Activer ce point de distribution pour extraire le contenu à partir d’autres points de distribution**. Procédez aux configurations supplémentaires dont ont besoin les points de distribution d’extraction.  

À la fin de l’Assistant Création d’un serveur de système de site, le site ajoute le rôle de point de distribution au serveur de système de site.  



##  <a name="bkmk_manage"></a> Gérer les groupes de points de distribution  

Les groupes de points de distribution fournissent un regroupement logique de points de distribution pour la distribution de contenu. Utilisez ces groupes pour gérer et surveiller de manière centralisée le contenu des points de distribution qui s’étendent sur plusieurs sites. Gardez à l’esprit les points suivants :

-   Sélectionnez un ou plusieurs points de distribution provenant d’un des sites de la hiérarchie afin de les ajouter à un groupe de points de distribution.  

-   Ajoutez un point de distribution à plusieurs groupes de points de distribution.  

-   Lorsque vous distribuez du contenu à un groupe de points de distribution, Configuration Manager le distribue à tous les points de distribution membres de ce groupe.  

-   Si vous ajoutez un point de distribution au groupe après une première distribution de contenu, Configuration Manager distribue automatiquement le contenu au nouveau membre du groupe.  

-   Associez un regroupement à un groupe de points de distribution. Lorsque vous distribuez du contenu à ce regroupement, Configuration Manager identifie les groupes de points de distribution qui sont associés au regroupement. Le contenu est ensuite distribué à tous les points de distribution qui sont membres de ces groupes.  

    > [!NOTE]  
    >  Si, après avoir distribué du contenu à un regroupement, vous associez ce regroupement à un nouveau groupe de points de distribution, vous devez redistribuer le contenu au regroupement pour pouvoir distribuer le contenu au nouveau groupe.  

Les sections suivantes répertorient les procédures permettant de gérer les groupes de points de distribution :  
- [Créer et configurer un nouveau groupe de points de distribution](#bkmk_dpgroup-create)
- [Modifier un groupe de points de distribution existant](#bkmk_dpgroup-modify)
- [Ajouter les points de distribution sélectionnés à des groupes de points de distribution existants](#bkmk_dpgroup-addexist)


### <a name="bkmk_dpgroup-create"></a> Procédure pour créer et configurer un nouveau groupe de points de distribution  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Groupes de points de distribution**.  

2.  Dans le ruban, cliquez sur **Créer un groupe**.  

3.  Dans la fenêtre Créer un nouveau groupe de points de distribution, entrez un **Nom** et éventuellement une **Description** pour le groupe.  

4.  Sous l’onglet **Membres**, cliquez sur **Ajouter**.  

5.  Dans la fenêtre Ajouter des points de distribution, sélectionnez un ou plusieurs points de distribution à ajouter comme membres du groupe. Cliquez ensuite sur **OK**.  

6.  Si nécessaire, basculez vers l’onglet **Regroupements** de la fenêtre Créer un nouveau groupe de points de distribution, puis cliquez sur **Ajouter**.  

7.  Dans la page Sélectionner des regroupements, sélectionnez les regroupements que vous souhaitez associer au groupe de points de distribution, puis cliquez sur **OK**.  

8.  Dans la fenêtre Créer un nouveau groupe de points de distribution, cliquez sur **OK** pour créer le groupe.  


#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Créer un groupe à partir d’un point de distribution existant

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Points de distribution**. Sélectionnez un ou plusieurs points de distribution à ajouter au nouveau groupe de points de distribution.  

2.  Dans le ruban, cliquez sur **Ajouter les éléments sélectionnés**, puis cliquez sur **Ajouter les éléments sélectionnés au nouveau groupe de points de distribution**.  

Ce processus remplit automatiquement l’onglet **Membres** de la fenêtre Créer un nouveau groupe de points de distribution avec les serveurs sélectionnés.


### <a name="bkmk_dpgroup-modify"></a> Procédure pour modifier un groupe de points de distribution existant  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Groupes de points de distribution**.  

2.  Sélectionnez un groupe de points de distribution existant pour le modifier. Dans le ruban, cliquez sur **Propriétés**.  

3.  Pour associer les nouveaux regroupements à ce groupe, basculez vers l’onglet **Regroupements**, puis cliquez sur **Ajouter**. Sélectionnez les regroupements, puis cliquez sur **OK**.  

4.  Pour ajouter de nouveaux points de distribution à ce groupe, basculez vers l’onglet **Membres**, puis cliquez sur **Ajouter**. Sélectionnez les points de distribution, puis cliquez sur **OK**.  

5.  Choisissez **OK** pour enregistrer les modifications apportées au groupe de points de distribution.  


### <a name="bkmk_dpgroup-addexist"></a> Procédure pour ajouter les points de distribution sélectionnés à des groupes de points de distribution existants  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Points de distribution**. Sélectionnez un ou plusieurs points de distribution à ajouter au groupe existant.  

2.  Dans le ruban, cliquez sur **Ajouter les éléments sélectionnés**, puis cliquez sur **Ajouter les éléments sélectionnés aux groupes de points de distribution existants**.  

3.  Dans **Groupes de points de distribution disponibles**, sélectionnez les groupes auxquels les points de distribution sélectionnés doivent être ajoutés en tant que membres. Cliquez ensuite sur **OK**.  



## <a name="bkmk_reassign"></a> Réaffecter un point de distribution
<!-- 1306937 -->
De nombreux clients ont de grandes infrastructures Configuration Manager et réduisent le nombre de sites principaux ou secondaires pour simplifier leur environnement. Ils doivent néanmoins toujours conserver des points de distribution aux emplacements des filiales pour délivrer du contenu aux clients gérés. Ces points de distribution contiennent souvent plusieurs téraoctets ou plus de contenus. Ce contenu est coûteux en termes de temps et de bande passante réseau pour le distribuer à ces serveurs distants. 

Depuis la version 1802, cette fonctionnalité vous permet de réaffecter un point de distribution à un autre site principal sans redistribuer le contenu. Cette action met à jour l’affectation du système de site tout en conservant la totalité du contenu sur le serveur. Si vous devez réaffecter plusieurs points de distribution, commencez avec un seul point de distribution. Poursuivez ensuite avec les autres serveurs, l’un après l’autre.

> [!IMPORTANT]  
> Le serveur cible peut seulement héberger le rôle de point de distribution. Si le serveur de système de site héberge un autre rôle serveur Configuration Manager, comme le point de migration d’état, vous ne pouvez pas réaffecter le point de distribution. Vous ne pouvez pas réaffecter un point de distribution cloud. 

Avant de réaffecter un point de distribution, ajoutez le compte d’ordinateur du serveur de site de destination au groupe Administrateur local sur le serveur de point de distribution cible. 

Effectuez les étapes suivantes pour réaffecter un point de distribution :

1. Dans la console Configuration Manager, connectez-vous au site d’administration centrale.  

2. Accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Points de distribution**.  

3. Cliquez avec le bouton droit sur le point de distribution cible, puis sélectionnez **Réaffecter le point de distribution**.  

4. Sélectionnez le serveur de site cible auquel vous voulez réaffecter ce point de distribution ainsi que le code de site.  

Surveillez la réaffectation de la même façon que quand vous ajoutez un nouveau rôle. La méthode la plus simple consiste à actualiser l’affichage de la console après quelques minutes. Ajoutez la colonne de code de site à l’affichage. Cette valeur change quand Configuration Manager réaffecte le serveur. Si vous essayez d’effectuer une autre action sur le serveur cible avant d’actualiser l’affichage de la console, une erreur « objet introuvable » se produit. Vérifiez que le processus est terminé et actualisez l’affichage de la console avant de démarrer d’autres actions sur le serveur.

Après la réaffectation d’un point de distribution, actualisez le certificat du serveur. Le nouveau serveur de site doit chiffrer à nouveau ce certificat à l’aide de sa clé publique et le stocker dans la base de données de site. Pour plus d’informations, consultez le paramètre **Créez un certificat auto-signé ou importez un certificat client d’infrastructure à clé publique (PKI) pour le point de distribution** sous l’onglet [Général](#bkmk_config-general) des propriétés du point de distribution. 

- Pour les certificats d’infrastructure à clé publique, vous n’avez pas besoin de créer un certificat. Importez le même fichier .PFX et entrez le mot de passe.  

- Pour les certificats auto-signés, réglez la date ou l’heure d’expiration pour la mettre à jour.  

- Si vous n’actualisez pas le certificat, le point de distribution continue de diffuser le contenu, mais les fonctions suivantes échouent :  

    - Messages de validation du contenu (le fichier distmgr.log indique qu’il ne peut pas déchiffrer le certificat)  

    - Prise en charge PXE pour les clients  


### <a name="tips"></a>Conseils 

- Effectuez cette action à partir du site d’administration centrale. Cette pratique facilite la réplication vers les sites principaux.  

- Ne distribuez pas de contenu vers le serveur cible pour tenter ensuite de le réaffecter. Les tâches de distribution de contenu en cours risquent d’échouer pendant le processus de réaffectation, mais elles sont retentées comme d’habitude.  

- Si le serveur est également un client Configuration Manager, veillez à réaffecter également le client au nouveau site principal. Cette étape est particulièrement importante pour les points de distribution d’extraction, qui utilisent des composants clients pour télécharger du contenu.  

- Ce processus supprime le point de distribution du groupe de limites par défaut de l’ancien site. Vous devez l’ajouter manuellement au groupe de limites par défaut du nouveau site, si nécessaire. Toutes les autres affectations de groupes de limites restent les mêmes.  



##  <a name="bkmk_configs"></a> Configurer un point de distribution  

Chaque point de distribution prend en charge plusieurs configurations différentes. Toutefois, tous les types de point de distribution ne prennent pas en charge toutes les configurations. Par exemple, les points de distribution cloud ne prennent pas en charge les déploiements PXE ou avec multidiffusion. Pour plus d’informations sur les limitations, consultez les articles suivants :  

-   [Utiliser un point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

-   [Utiliser un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point)  

Les sections suivantes décrivent les configurations des points de distribution lorsque vous [installez un nouveau point de distribution](#bkmk_install-procedure) ou [modifiez un point de distribution existant](#bkmk_change-procedure) :  
- [Paramètres généraux](#bkmk_config-general)
- [Paramètres du lecteur](#bkmk_config-drive)
- [Point de distribution d’extraction](#bkmk_config-pull)
- [Paramètres PXE](#bkmk_config-pxe)
- [Multidiffusion](#bkmk_config-multicast)
- [Validation du contenu](#bkmk_config-valid)
- [Groupes de limites](#bkmk_config-boundary)


#### <a name="bkmk_change-procedure"></a> Procédure pour modifier un point de distribution  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Points de distribution**.  

2.  Sélectionnez le point de distribution à configurer. Dans le ruban, cliquez sur **Propriétés**.  

3.  Utilisez les informations des sections suivantes lorsque vous modifiez les propriétés du point de distribution.  

4.  Après avoir apporté les modifications souhaitées, cliquez sur **OK** pour enregistrer vos paramètres, puis fermez la page des propriétés.  


### <a name="bkmk_config-general"></a> Général  

Les paramètres suivants se trouvent dans la page **Point de distribution** de l’Assistant Création d’un serveur de système de site, et sous l’onglet **Général** de la fenêtre de propriétés des points de distribution :  

-   **Installer et configurer IIS si requis par Configuration Manager** : Si IIS n’est pas déjà installé sur le serveur, Configuration Manager l’installe et le configure. Configuration Manager a besoin qu’IIS soit installé sur tous les points de distribution. Si vous ne choisissez pas ce paramètre, et qu’IIS n’est pas installé sur le serveur, installez IIS pour que Configuration Manager puisse installer correctement le point de distribution.  

    > [!NOTE]  
    >  Cette option se trouve uniquement dans la page **Point de distribution** de l’Assistant Création d’un serveur de système de site. Elle n’est disponible que lorsque vous [installez un nouveau point de distribution](#bkmk_install-procedure).  

- **Activer et configurer BranchCache pour ce point de distribution** : Sélectionnez ce paramètre pour permettre à Configuration Manager de configurer Windows BranchCache sur le serveur de point de distribution. Pour plus d’informations, consultez [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache).  

- **Régler la vitesse de téléchargement afin d’utiliser la bande passante réseau inutilisée (Windows LEDBAT)**<!--1358112-->: À compter de la version 1806, configurez les points de distribution pour utiliser le contrôle de surcharge du réseau. Pour plus d’informations, consultez [Windows LEDBAT](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#windows-ledbat). Configuration minimale nécessaire à la prise en charge LEDBAT :<!-- SCCMDocs issue 883 -->  

    - Configuration Manager version 1806 (grand public)  

        - Windows Server version 1709 ou ultérieure  

    - Configuration Manager version 1806 avec mise à jour cumulative (4462978), ou version ultérieure  

        - Windows Server version 1709 ou ultérieure
        - Windows Server 2016 avec les mises à jour KB4132216 et KB4284833

    - Configuration Manager version 1810 ou ultérieure :

        - Windows Server version 1709 ou ultérieure
        - Windows Server 2016 avec les mises à jour KB4132216 et KB4284833
        - Windows Server 2019  

- **Description** : Description facultative du rôle du point de distribution.  

-   **Configurez la manière dont les appareils clients communiquent avec le point de distribution** : L’utilisation du protocole **HTTP** ou **HTTPS** présente des avantages et des inconvénients. Pour plus d’informations, voir [Bonnes pratiques de sécurité pour la gestion de contenu](/sccm/core/plan-design/hierarchy/security-and-privacy-for-content-management#BKMK_Security_ContentManagement).  

-   **Autoriser les clients à se connecter anonymement** : Ce paramètre spécifie si le point de distribution autorise les connexions anonymes des clients Configuration Manager à la bibliothèque de contenu.  

    > [!Important]  
    > Si vous n’utilisez pas ce paramètre, appliquez les modifications décrites dans l’article de la Base de connaissances Microsoft [2619572](https://support.microsoft.com/help/2619572/) sur les clients Windows 7. Sinon, la réparation des applications Windows Installer peut échouer.  
    >   
    >  Lorsque vous déployez une application Windows Installer, le client Configuration Manager télécharge le fichier dans son cache local. Une fois l’installation terminée, le client supprime ces fichiers. Le client Configuration Manager met à jour la liste des sources Windows Installer pour l’application. Il définit le chemin du contenu sur la bibliothèque de contenu pour les points de distribution associés. Si vous essayez plus tard de réparer l’application sur l’appareil, MSIExec tentera d’accéder au chemin du contenu en tant qu’utilisateur anonyme.  
    >   
    >  Après l’installation de la mise à jour sur les clients et la modification de la clé de Registre documentée, MSIExec accède au chemin du contenu en utilisant le compte de l’utilisateur connecté.  

-   **Créer un certificat auto-signé ou importer un certificat client PKI** : Configuration Manager utilise ce certificat aux fins suivantes :  

    -   Il authentifie le point de distribution à un point de gestion avant que le point de distribution n'envoie des messages d'état.  

    -   Lorsque vous sélectionnez l’option **Activer la prise en charge PXE pour les clients** dans la page **Paramètres PXE**, le point de distribution l’envoie aux ordinateurs qui effectuent un démarrage PXE. Ces ordinateurs l’utilisent alors pour se connecter à un point de gestion pendant le processus de déploiement du système d’exploitation.  

    Lorsque vous configurez tous les points de gestion du site pour le protocole HTTP, sélectionnez l’option **Créer un certificat auto-signé**. Lorsque vous configurez les points de gestion pour HTTPS, utilisez l’option **Importer un certificat** à partir de l’infrastructure à clé publique (PKI).  

    Pour importer le certificat, accédez à un fichier PKCS #12 valide. Ce fichier PFX ou CER comprend le certificat PKI avec les spécifications suivantes concernant Configuration Manager :  

    -   L’utilisation prévue comprend l’authentification du client.  

    -   La clé privée est activée pour l’exportation.  

    > [!TIP]  
    >  Il n’existe aucune exigence particulière pour l’objet du certificat ou l’autre nom de l’objet. Si nécessaire, vous pouvez utiliser le même certificat pour plusieurs points de distribution.  

     Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  

     Pour obtenir un exemple de déploiement de ce certificat, consultez [Déploiement du certificat client pour les points de distribution](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clientdistributionpoint2008_cm2012).  

-   **Activer ce point de distribution pour le contenu préparé** : Ce paramètre vous permet d’ajouter du contenu sur le serveur avant de distribuer des logiciels. Comme les fichiers de contenu figurent déjà dans la bibliothèque de contenu, ils ne sont pas transférés sur le réseau quand vous distribuez les logiciels. Pour plus d’informations, consultez [Contenu préparé](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  


### <a name="bkmk_config-drive"></a> Paramètres du lecteur  

> [!NOTE]  
>  Ces options ne sont disponibles que lorsque vous installez un nouveau point de distribution.  

Spécifiez les paramètres du lecteur pour le point de distribution. Vous pouvez configurer jusqu’à deux lecteurs de disque pour la bibliothèque de contenu, et deux lecteurs de disque pour le partage de package. Configuration Manager peut utiliser des lecteurs supplémentaires lorsque les deux premiers atteignent la réserve d’espace disque configurée. La page **Paramètres du lecteur** permet de configurer la priorité des lecteurs de disque et la quantité d'espace disque libre restant sur chaque lecteur de disque.  

-   **Réserve d’espace libre sur le lecteur (Mo)** : Cette valeur détermine la quantité d’espace libre sur un lecteur avant que Configuration Manager ne choisisse un autre lecteur et poursuive le processus de copie sur ce lecteur. Les fichiers de contenu peuvent s'étendre sur plusieurs lecteurs.  

-   **Emplacements du contenu** : Spécifiez les emplacements pour la bibliothèque de contenu et le partage de package sur ce point de distribution. Par défaut, tous les emplacements du contenu sont définis sur **Automatique**. Configuration Manager copie le contenu à l’emplacement de contenu principal jusqu’à ce que la quantité d’espace libre atteigne la valeur spécifiée dans **Réserve d’espace libre sur le lecteur (Mo)** . Lorsque vous sélectionnez **Automatique**, Configuration Manager définit les emplacements de contenu principaux sur le lecteur de disque qui a le plus d’espace disque au moment de l’installation. Il définit les emplacements secondaires sur le lecteur de disque qui a l’espace disque le plus important après le premier. Quand l’emplacement principal et l’emplacement secondaire atteignent la réserve d’espace libre du lecteur, Configuration Manager sélectionne le lecteur disponible ayant le plus d’espace disque libre et poursuit le processus de copie.  

> [!Tip]  
>  Pour empêcher l’installation de Configuration Manager sur un lecteur spécifique, créez un fichier vide intitulé **no_sms_on_drive.sms** et copiez-le dans le dossier racine du lecteur avant d’installer le point de distribution.  

Pour plus d’informations, consultez [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library).


### <a name="bkmk_config-pull"></a> Point de distribution d’extraction  

Lorsque vous sélectionnez l’option **Activer ce point de distribution pour extraire le contenu à partir d’autres points de distribution**, le point de distribution devient un point de distribution d’extraction. Vous modifiez la façon dont le point de distribution obtient le contenu que vous lui distribuez. Pour plus d’informations, consultez [Utiliser un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

Pour chaque point de distribution d’extraction que vous configurez, spécifiez un ou plusieurs points de distribution sources à partir desquels obtenir le contenu :  

-   Cliquez sur **Ajouter**, puis sélectionnez un ou plusieurs des points de distribution pouvant servir de sources.  

-   Utilisez les boutons fléchés pour définir la priorité des points de distribution. Lorsque le point de distribution d’extraction tente de transférer du contenu, la priorité correspond à l’ordre dans lequel il contacte les points de distribution sources. Il contacte d’abord les points de distribution avec la valeur la plus basse.  


### <a name="bkmk_config-pxe"></a> Environnement PXE  

Indiquez si vous souhaitez activer l'environnement PXE sur le point de distribution. Utilisez un environnement PXE (Preboot Execution Environment) pour démarrer les déploiements de système d’exploitation sur les clients. Pour plus d’informations sur l’utilisation de l’environnement PXE dans Configuration Manager, consultez [Utiliser PXE pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).

Quand vous activez l’environnement PXE, Configuration Manager installe les services de déploiement Windows (WDS) sur le serveur, si nécessaire. WDS est le service qui démarre PXE pour installer les systèmes d’exploitation. Après avoir effectué toutes les étapes de l’Assistant pour créer le point de distribution, Configuration Manager installe dans WDS un fournisseur qui utilise les fonctions de démarrage PXE. 

À partir de la version 1806, vous pouvez activer PXE sur un point de distribution sans WDS. 

Sélectionnez l’option **Activer la prise en charge PXE pour les clients**, puis configurez les paramètres suivants :  

 > [!Note]  
 > Cliquez sur **Oui** dans la boîte de dialogue **Consulter les ports requis pour PXE** pour confirmer que vous souhaitez activer PXE. Configuration Manager configure automatiquement les ports par défaut dans le Pare-feu Windows. Si vous utilisez un autre pare-feu, configurez manuellement les ports.  
 >   
 > Si WDS et DHCP sont installés sur le même serveur, configurez WDS pour écouter sur un port différent. Par défaut, DHCP écoute sur le même port. Pour plus d’informations, consultez [Considérations quand vous avez WDS et DHCP sur le même serveur](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#BKMK_WDSandDHCP).  

- **Autoriser ce point de distribution à répondre aux requêtes PXE entrantes** : Spécifiez s’il faut activer WDS pour répondre aux requêtes de service PXE. Utilisez ce paramètre pour activer et désactiver le service sans supprimer la fonctionnalité PXE du point de distribution.  

- **Activer la prise en charge d’ordinateur inconnu** : Indiquez si la prise en charge des ordinateurs non gérés par Configuration Manager doit être activée. Pour plus d’informations, voir [Préparer les déploiements d’ordinateurs inconnus](/sccm/osd/get-started/prepare-for-unknown-computer-deployments).  

- **Activer un répondeur PXE sans service de déploiement Windows** : À compter de la version 1806, cette option active un répondeur PXE sur le point de distribution, qui n’a pas besoin des services WDS. Ce répondeur PXE prend en charge les réseaux IPv6. Si vous activez cette option sur un point de distribution qui est déjà compatible PXE, Configuration Manager suspend le service WDS. Si vous la désactivez tout en choisissant **Activer la prise en charge PXE pour les clients**, le point de distribution réactive le service WDS.<!--1357580-->  

    > [!Note]  
    > Dans la version 1810 et les précédentes, il n’est pas possible d’utiliser le répondeur PXE sans les Services de déploiement Windows sur des serveurs qui exécutent également un serveur DHCP.
    >
    > À compter de la version 1902, un répondeur PXE activé sur un point de distribution sans les Services de déploiement Windows peut se trouver sur le même serveur que le service DHCP. <!--3734270-->  

- **Exiger un mot de passe lorsque les ordinateurs utilisent PXE** : pour renforcer la sécurité de vos déploiements PXE, spécifiez un mot de passe fort.  

- **Affinité entre appareil et utilisateur** : indiquez de quelle manière le point de distribution doit associer les utilisateurs à l’ordinateur de destination dans le cadre des déploiements PXE. Choisissez l'une des options suivantes :  

  - **Autoriser une affinité entre appareil et utilisateur avec approbation automatique** : Choisissez ce paramètre pour associer automatiquement les utilisateurs à l’ordinateur de destination sans attendre l’approbation.  

  - **Autoriser une affinité entre appareil et utilisateur en attente de l’approbation de l’administrateur** : Choisissez ce paramètre pour attendre l’approbation d’un utilisateur administratif avant d’associer des utilisateurs à l’ordinateur de destination.  

  - **Ne pas autoriser d’affinité entre appareil et utilisateur** : Choisissez ce paramètre pour empêcher l’association d’utilisateurs à l’ordinateur de destination. Ce paramètre est la valeur par défaut.  

    Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  

- **Interfaces réseau** : Spécifiez que le point de distribution répond aux requêtes PXE à partir de toutes les interfaces réseau ou d'interfaces réseau spécifiques. Si le point de distribution répond à certaines interfaces réseau, vous devez fournir l’adresse MAC pour chaque interface réseau.  

    > [!Note]  
    > Lorsque vous modifiez l’interface réseau, redémarrez le service WDS pour garantir qu’il enregistre correctement la configuration. Depuis la version 1806, lorsque vous utilisez le service de répondeur PXE, vous pouvez redémarrer le **service de répondeur PXE ConfigMgr** (SccmPxe).<!--SCCMDocs issue 642-->  

- **Spécifier le délai de réponse du serveur PXE (secondes)** : Lorsque vous utilisez plusieurs serveurs PXE, spécifiez la durée que doit attendre le point de distribution compatible PXE avant de répondre aux requêtes des ordinateurs. Par défaut, le point de distribution compatible PXE de Configuration Manager répond immédiatement.  


### <a name="bkmk_config-multicast"></a> Multidiffusion  

Indiquez si vous souhaitez activer la multidiffusion sur le point de distribution. Les déploiements de multidiffusion économisent la bande passante réseau en envoyant de manière simultanée des données à plusieurs clients Configuration Manager. Sans multidiffusion, le serveur envoie une copie des données à chaque client sur une connexion distincte. Pour plus d’informations sur l’utilisation de la multidiffusion pour le déploiement de systèmes d’exploitation, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).

Quand vous activez la multidiffusion, Configuration Manager installe les services de déploiement Windows (WDS) sur le serveur, si nécessaire.  

Sélectionnez l’option **Activer la multidiffusion pour envoyer simultanément des données à plusieurs clients**, puis configurez les paramètres suivants :  

- **Compte de connexion multidiffusion** : Spécifiez le compte à utiliser lorsque vous configurez des connexions de base de données Configuration Manager pour la multidiffusion. Pour plus d’informations, consultez [Compte de connexion multidiffusion](/sccm/core/plan-design/hierarchy/accounts#multicast-connection-account).  

- **Paramètres de l’adresse de multidiffusion** : Spécifiez les adresses IP d’envoi de données aux ordinateurs de destination. Par défaut, il obtient l’adresse IP d’un serveur DHCP chargé de distribuer des adresses de multidiffusion. Selon l’environnement réseau, vous pouvez spécifier une plage d’adresses IP entre 239.0.0.0 et 239.255.255.255.  

    > [!IMPORTANT]  
    >  Les adresses IP que vous configurez doivent être accessibles par les ordinateurs de destination qui demandent l’image du système d’exploitation. Vérifiez que les routeurs et les pare-feu autorisent le trafic multidiffusion entre l’ordinateur de destination et le point de distribution.  

- **Étendue du port UDP pour la multidiffusion** : Spécifiez la plage de ports UDP utilisés pour envoyer des données aux ordinateurs de destination.  

    > [!IMPORTANT]  
    >  Les ports UDP doivent être accessibles par les ordinateurs de destination qui demandent l’image du système d’exploitation. Vérifiez que les routeurs et pare-feu autorisent le trafic de multidiffusion entre l'ordinateur de destination et le serveur de site.  

- **Nombre maximum de clients** : Spécifiez le nombre maximum d’ordinateurs de destination qui peuvent télécharger l’image du système d’exploitation à partir de ce point de distribution.  

- **Activer la multidiffusion planifiée** : Indiquez comment Configuration Manager contrôle le lancement du déploiement des systèmes d’exploitation sur les ordinateurs de destination. Configurez les options suivantes :  

    - **Délai de démarrage de session (minutes)** : Indiquez le nombre de minutes écoulé avant que Configuration Manager réponde à la première requête de déploiement.  

    - **Taille minimale de la session (clients)** : Indiquez le nombre de requêtes qui doivent être reçues avant que Configuration Manager commence à déployer le système d’exploitation.  


> [!IMPORTANT]  
> À compter de la version 1806, pour activer et configurer la multidiffusion sous l’onglet **Multidiffusion** des propriétés du point de la distribution, il faut que ce dernier utilise le service WDS.  
> - Si vous choisissez les options **Activer la prise en charge de PXE pour les clients** et **Activer la multidiffusion pour envoyer des données simultanément à plusieurs clients**, vous ne pouvez pas utiliser l’option **Activer un répondeur PXE sans les Services de déploiement Windows**.  
> - Si vous choisissez les options **Activer la prise en charge PXE pour les clients** et **Activer un répondeur PXE sans service de déploiement Windows**, vous ne pouvez pas utiliser l’option **Activer la multidiffusion pour envoyer des données simultanément à plusieurs clients**.  


### <a name="bkmk_config-group"></a> Relations de groupe  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  

Gérez les groupes de points de distribution dont ce point de distribution est membre.  

Pour ajouter ce point de distribution en tant que membre à un groupe de points de distribution existant, cliquez sur **Ajouter**. Dans la fenêtre Ajouter aux groupes de points de distribution, sélectionnez un groupe existant, puis cliquez sur **OK**.  

Pour supprimer ce point de distribution d’un groupe de points de distribution, sélectionnez le groupe dans la liste, puis cliquez sur **Supprimer**. La suppression du point de distribution d’un groupe de points de distribution ne supprime aucun contenu du point de distribution.

### <a name="bkmk_config-content"></a> Contenu  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  

Gérez le contenu que vous avez distribué au point de distribution. Sélectionnez un package dans la liste des packages de déploiement, puis effectuez les actions suivantes :  

- **Valider** : Démarrez le processus de validation de l’intégrité des fichiers de contenu pour le logiciel. Pour afficher les résultats du processus de validation du contenu, dans l’espace de travail **Surveillance**, développez **État de distribution**, puis choisissez le nœud **État du contenu**. Pour plus d’informations, consultez [Valider du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content).   

- **Redistribuer** : Copie tous les fichiers de contenu du logiciel sélectionné dans le point de distribution, et remplace les fichiers existants. Cette action permet généralement de réparer les fichiers de contenu. Pour plus d’informations, consultez [Redistribuer le contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#redistribute-content).  

-   **Supprimer** : Supprime les fichiers de contenu du logiciel dans le point de distribution. Pour plus d’informations, consultez [Supprimer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#remove-content).    


### <a name="bkmk_config-valid"></a> Validation du contenu  

Définissez une planification pour valider l’intégrité des fichiers de contenu sur le point de distribution. Quand vous activez la validation de contenu selon une planification, Configuration Manager démarre le processus à l’heure planifiée. Il vérifie tout le contenu du point de distribution selon la classe locale SMS_PackagesInContLib SCCMDP. Vous pouvez également configurer la priorité de la validation du contenu. Par défaut, la priorité est définie sur **La plus faible**. Le fait d’élever le niveau de priorité peut accroître l’utilisation du processeur et du disque sur le serveur pendant le processus de validation. Toutefois, le processus doit se terminer plus rapidement. 

Pour afficher les résultats du processus de validation du contenu, dans l’espace de travail **Surveillance**, développez **État de distribution**, puis choisissez le nœud **État du contenu**. Vous y voyez le contenu de chaque type de logiciel (par exemple, application, package de mises à jour logicielles et image de démarrage).  

> [!WARNING]  
>  Même si vous planifiez la validation du contenu en utilisant l’heure locale de l’ordinateur, la planification affichée dans la console Configuration Manager est exprimée en heure UTC.  

Pour plus d’informations, consultez [Valider du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#validate-content).


### <a name="bkmk_config-boundary"></a> Groupes de limites  

Gérez les groupes de limites auxquels vous avez attribué ce point de distribution. Ajoutez le point de distribution à au moins un groupe de limites. Au cours du déploiement de contenu, les clients doivent se trouver dans un groupe de limites associé à un point de distribution pour utiliser ce dernier comme emplacement source de contenu.

Configurez des *relations* qui définissent à quel moment et auprès de quels groupes de limites un client peut effectuer une action de secours pour trouver du contenu. Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#boundary-groups).

Cliquez sur **Ajouter**, puis sélectionnez un groupe de limites existant dans la liste.

Si vous souhaitez créer un groupe de limites pour ce point de distribution, cliquez sur **Créer**. Pour plus d’informations sur la création et la configuration d’un groupe de limites, consultez [Procédures pour les groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#procedures-for-boundary-groups).

Lorsque vous modifiez les propriétés d’un point de distribution déjà installé, gérez l’option **Activer pour la distribution à la demande**. Cette option permet à Configuration Manager de distribuer automatiquement le contenu vers ce serveur quand un client le demande. Pour plus d’informations, consultez [Distribution de contenu à la demande](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#on-demand-content-distribution).


### <a name="bkmk_config-sched"></a> Planification  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé. 
> 
>  Cet onglet n’est disponible que lorsque vous modifiez les propriétés d’un point de distribution distant du serveur de site.  

Configurez une planification qui limite la période de transfert de données de Configuration Manager vers le point de distribution. Limitez les données par priorité ou fermez la connexion durant une période sélectionnée.   

Pour limiter les données, sélectionnez la période dans la grille, puis choisissez l’un des paramètres suivants sous **Disponibilité** :  

- **Ouvrir pour toutes les priorités** : Configuration Manager envoie les données au point de distribution sans restriction. Ce paramètre est sélectionné par défaut pour toutes les périodes.  

- **Autoriser les priorités moyennes et élevées** : Configuration Manager n’envoie au point de distribution que les données de priorité moyenne et élevée.  

- **Autoriser uniquement la priorité élevée** : Configuration Manager n’envoie au point de distribution que les données de priorité élevée.  

- **Fermé** : Configuration Manager n’envoie pas de données au point de distribution.  

Configurez la **Priorité de distribution** des logiciels sous l’onglet **Paramètres de distribution** des propriétés du logiciel. 

> [!IMPORTANT]  
>  La planification est basée sur le fuseau horaire du site émetteur, et non sur celui du point de distribution.  


### <a name="bkmk_config-rate"></a> Limites du taux de transfert  

> [!NOTE]  
>  Ces options ne sont disponibles que quand vous modifiez les propriétés d’un point de distribution déjà installé.  
>   
>  Cet onglet n’est disponible que lorsque vous modifiez les propriétés d’un point de distribution distant du serveur de site.  

Configurez des limites du taux de transfert pour contrôler la bande passante réseau utilisée lorsque Configuration Manager transfère du contenu vers le point de distribution. Choisissez parmi les options suivantes :  

- **Illimité lors de l’expédition de données à cette destination** : Configuration Manager envoie le contenu au point de distribution sans aucune limite de taux de transfert. Ce paramètre est la valeur par défaut.  

- **Mode impulsion** : Cette option spécifie la taille des blocs de données qui sont envoyés par le serveur de site au point de distribution. Vous pouvez également spécifier un délai entre l'envoi de chaque bloc de données. Utilisez cette option lorsque vous devez envoyer des données au point de distribution via une connexion réseau à très faible bande passante. Par exemple, vous pouvez être limité à l’envoi de 1 Ko de données toutes les cinq secondes, quelle que soit la vitesse de la liaison ou son utilisation.  

- **Limité aux taux de transfert maximaux indiqués par heure** : spécifiez ce paramètre pour qu’un site envoie des données à un point de distribution en utilisant uniquement le pourcentage de temps que vous avez configuré. Lorsque vous utilisez cette option, Configuration Manager n’identifie pas la bande passante disponible sur le réseau. Au lieu de cela, il envoie les données en plusieurs fois. Le serveur envoie des données pendant une courte période, puis n’envoie rien durant les périodes qui suivent. Par exemple, si vous avez défini **Limiter la bande passante disponible** sur **50 %** , Configuration Manager transmet les données sur une période, qui est suivie d’une période égale où aucune donnée n’est envoyée. La taille effective des données et celle des blocs de données ne sont pas gérées. Il gère uniquement la durée pendant laquelle il envoie des données.  
