---
title: Capacités de la version Technical Preview 1511
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1511 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 69473706-21b3-498b-a67e-670fdc988f0d
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: a02fc742ddb975c06bc7e919914ad46ae455bf92
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127964"
---
# <a name="capabilities-in-technical-preview-1511-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1511 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1511 pour System Center Configuration Manager. Cette version est une installation de base de référence pour la version d’évaluation technique que vous pouvez utiliser pour installer un nouveau site de version d’évaluation technique ou pour effectuer la mise à niveau à partir d’une version antérieure de la version d’évaluation technique.   Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](/sccm/core/get-started/technical-preview), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.  

Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.  

##  <a name="BKMK_WUfB"></a> Intégration à Windows Update for Business dans Windows 10  
 Configuration Manager peut désormais différencier un ordinateur Windows 10 directement connecté par le biais de Windows Update for Business (WUfB) de ceux connectés à WSUS pour obtenir les mises à jour et mises à niveau Windows 10.  Pour les ordinateurs connectés via WUFB, les mises à jour et les mises à niveau peuvent être gérées à la cadence définie par un utilisateur administratif via des stratégies de groupe ou des stratégies MDM. Par ailleurs, ces mises à jour/mises à niveau peuvent être installées directement à partir de WUFB.    
Pour les ordinateurs connectés via WUfB, Configuration Manager ne peut pas créer de rapports sur l’état de conformité (dont les mises à jour Windows ou les mises à jour de définition). De plus, Configuration Manager ne peut pas déployer des mises à jour Microsoft ni tierces sur ces ordinateurs.  

 **Conditions requises pour ce scénario :**  

-   Windows 10 Desktop Pro ou Windows 10 Édition Entreprise version 1511 ou ultérieure  

-   Ordinateurs à gérer via [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx).  

### <a name="try-it-out"></a>Essayez !  
 Essayez d'exécuter la tâche suivante, puis utilisez les informations fournies au début de cette rubrique pour nous dire si tout a fonctionné comme prévu :  

1.  Désactivez l’Agent Windows Update, s’il était précédemment activé, afin qu’il n’effectue pas l’analyse par rapport à WSUS.   
    La clé de Registre **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\useWSUSServer** peut être définie pour indiquer si l’ordinateur effectue l’analyse par rapport à Windows Update ou à WSUS.  Lorsque la valeur est 2, il n’effectue pas l’analyse par rapport à WSUS.  

2.  Notez le nouvel attribut **UseWUServer**, sous le nœud **Windows Update** dans l’Explorateur de ressources Configuration Manager.  

3.  Créez un regroupement basé sur l’attribut **UseWUServer** pour tous les ordinateurs connectés via WUFB pour les mises à jour et les mises à niveau.  

4.  Créez un paramètre d’agent du client pour désactiver le flux de travail des mises à jour logicielles et déployer le paramètre sur le regroupement d’ordinateurs connectés directement à WUFB.  

5.  Les ordinateurs qui sont gérés via WUFB affichent **Inconnu** dans l’état de conformité et ne sont pas comptabilisés dans le pourcentage de conformité global.  

##  <a name="BKMK_Office365ProPlus"></a> Gestion des mises à jour du client Office 365 ProPlus via System Center Configuration Manager  
 Configuration Manager peut désormais gérer les mises à jour du client du bureau Office 365 à l’aide du flux de travail de gestion des mises à jour logicielles de Configuration Manager.    
Quand Microsoft publie une nouvelle mise à jour du client de bureau Office 365 pour WSUS (Windows Server Updates Services), Configuration Manager peut synchroniser la mise à jour avec son catalogue si la mise à jour d’Office 365 est configurée pour faire partie de la synchronisation du catalogue.  Le serveur de site Configuration Manager télécharge les mises à jour du client Office 365 et distribue le package aux points de distribution Configuration Manager.  Le client Configuration Manager indique ensuite aux clients du bureau Office 365 où obtenir les mises à jour et quand commencer le processus d’installation des mises à jour.  

**Conditions requises pour ce scénario :**  

### <a name="try-it-out"></a>Essayez !  
 Essayez d'exécuter la tâche suivante, puis utilisez les informations fournies au début de cette rubrique pour nous dire si tout a fonctionné comme prévu :  

1. Vous pouvez synchroniser les mises à jour d’Office 365 avec le serveur de site Configuration Manager et les afficher à partir de la console Configuration Manager.  

2. Vous pouvez approuver et déployer avec succès les mises à jour d’Office 365.  

3. Vous pouvez télécharger et installer correctement les mises à jour d’Office 365 sur les clients.  

4. Vous pouvez vérifier la compatibilité pour les mises à jour d’Office 365 à l’aide de rapports ou de la surveillance dans la console.  

   Pour une procédure détaillée, consultez [Gérer les mises à jour du client Office 365 avec System Center Configuration Manager Technical Preview](https://technet.microsoft.com/library/mt628083.aspx).  

##  <a name="BKMK_AlwasyOn"></a> Prise en charge de SQL Server AlwaysOn pour les bases de données à haute disponibilité  
 Configuration Manager prend désormais en charge l’utilisation d’un groupe de disponibilité SQL Server AlwaysOn pour héberger la base de données de site.  Quand vous installez un nouveau site, vous pouvez indiquer au programme d’installation d’utiliser le groupe de disponibilité au lieu d’une instance normale de SQL Server.  

> [!NOTE]  
>  Pour pouvoir configurer et utiliser des groupes de disponibilité, vous devez savoir comment configurer des groupes de disponibilité SQL Server et vous appuyer sur la documentation et les procédures fournies dans la bibliothèque de documentation de SQL Server.  

Le processus de haut niveau pour configurer et utiliser des groupes de disponibilité comprend les tâches suivantes :  

1.  Configurer le groupe de disponibilité dans SQL Server.  

2.  Installez un nouveau site Configuration Manager et, lors de l’installation, indiquez au site d’utiliser le groupe de disponibilité en spécifiant le point de terminaison du groupe.  

**Conditions requises pour ce scénario :**  

-   Nécessite une version de SQL Server prise en charge par Configuration Manager Technical Preview.  

-   Vous devez créer et configurer le groupe de disponibilité SQL Server avant d’installer Configuration Manager  

-   Le groupe de disponibilité doit avoir un réplica principal et peut avoir jusqu'à deux réplicas secondaires synchrones.  

-   Le groupe de disponibilité doit avoir au moins un point de terminaison.  

-   Vous devez avoir un emplacement réseau accessible par chaque serveur SQL Server du groupe de disponibilité. Cet emplacement est utilisé par le programme d'installation lors de la configuration du groupe de disponibilité. Vous pouvez le supprimer une fois l'installation terminée.  

**Problèmes connus pour cette version :**  

-   Vous ne pouvez pas ajouter un nouveau membre de réplica à un groupe de disponibilité qui est déjà utilisé comme base de données de site. Au lieu de cela, vous devez réinstaller le site après avoir ajouté le nouveau membre de réplica.  

-   Pour ce scénario, vous devrez peut-être installer le **client natif SQL Server 2012** ([à partir de SQL Server 2012 Feature Pack](http://www.microsoft.com/download/details.aspx?id=29065)) sur le serveur de point de gestion. Cela empêche toute erreur de connexion SQL (qui sont enregistrées dans le fichier **mp_getauth.log** sur le serveur de point de gestion).  

### <a name="try-it-out"></a>Essayez !  
Essayez d'exécuter les tâches suivantes, puis utilisez les informations fournies au début de cette rubrique pour nous dire si tout a fonctionné comme prévu :  

-   Je peux installer un site principal qui utilise un serveur de bases de données configuré pour les groupes de disponibilité AlwaysOn.  

-   J'ai réussi à faire basculer mon groupe de disponibilité SQL AlwaysOn vers un nouveau réplica dans le groupe et le site principal est toujours opérationnel.  

### <a name="configuring-sql-server-alwayson-for-configuration-manager"></a>Configuration de SQL Server AlwaysOn pour Configuration Manager  
 Appliquez les procédures suivantes pour tout d’abord créer et configurer le groupe de disponibilité, puis installez un nouveau site Configuration Manager qui utilise le groupe de disponibilité.  

#### <a name="to-create-a-sql-server-alwayson-availability-group"></a>Pour créer un groupe de disponibilité SQL Server AlwaysOn  
Le processus de [création d'un groupe de disponibilité SQL Server](https://technet.microsoft.com/library/ff878265\(v=sql.120\).aspx) est documenté dans la bibliothèque de documentation de SQL Server.  Quand vous créez le groupe de disponibilité, vérifiez que les conditions suivantes pour une utilisation avec Configuration Manager sont remplies :  

-   Un maximum de trois membres :  

    -   un réplica principal et deux réplicas secondaires ;  

    -   les réplicas secondaires doivent être synchrones.  

        > [!TIP]  
        >  Nous recommandons de configurer les réplicas secondaires en lecture seule. Cela vous permet d'utiliser un réplica secondaire pour des fonctions telles que la création de rapports tout en préservant les performances du réplica principal pour les opérations de site.  

-   Au moins un point de terminaison. Le nom virtuel de ce point de terminaison est utilisé quand vous installez le site Configuration Manager.  

    > [!TIP]  
    >  Bien que le groupe puisse contenir plusieurs points de terminaison, Configuration Manager ne peut en utiliser qu’un seul.  

#### <a name="to-install-a-configuration-manager-site-that-uses-the-availability-group"></a>Pour installer un site Configuration Manager qui utilise le groupe de disponibilité  
Pour installer un site qui utilise un groupe de disponibilité SQL Server  

1.  Remplacez les éléments suivants quand le programme d’installation de Configuration Manager vous y invite :  

    -   **Nom du serveur SQL Server** : entrez le nom virtuel du point de terminaison que vous avez configuré lors de la création du groupe de disponibilité. Le nom virtuel doit être un nom DNS complet, comme **&lt;serveur_point_de_terminaison\>.fabrikam.com**.  

    -   **Instance** :  cette valeur doit rester vierge. Il n'y a aucune instance dans cette configuration.  

    -   **Base de données** : entrez le nom de la base de données que vous avez créée sur le réplica principal du groupe de disponibilité.  

2.  Ensuite, vous devez fournir un emplacement réseau accessible par chaque serveur SQL Server du groupe :  

    -   Le compte d'ordinateur et le compte de service de chaque serveur SQL Server nécessitent un accès en contrôle total à cet emplacement.  

    -   Cet emplacement est utilisé uniquement lors de l'installation. Vous pouvez annuler son partage ou le supprimer une fois l'installation terminée et le site installé.  

3.  Après avoir fourni ces informations, terminez l'installation avec vos processus et configurations ordinaires.  

##  <a name="BKMK_ClusterServerUpdates"></a> Assurer la maintenance d’un cluster de serveurs  
Vous pouvez maintenant créer un regroupement qui contient des serveurs dans un cluster, puis configurer les paramètres de cluster à utiliser lorsque vous déployez des mises à jour sur le cluster. Vous pouvez contrôler le pourcentage de serveurs qui sont en ligne à un moment donné et configurer l'exécution de scripts PowerShell de prédéploiement et de post-déploiement pour exécuter des actions personnalisées.  

**Problèmes connus pour cette version :**  

-   La création de rapports n'est pas disponible pour vérifier l'état du déploiement des mises à jour logicielles pour les serveurs de cluster.  

-   L'option de séquence de maintenance dans la page **Paramètres du cluster** est désactivée et non disponible dans cette version.  

### <a name="try-it-out"></a>Essayez !  
Essayez d'exécuter la tâche suivante, puis utilisez les informations fournies au début de cette rubrique pour nous dire si tout a fonctionné comme prévu :  

-   Je peux créer un regroupement qui représente un cluster de serveurs. Pour ce test, vous pouvez configurer vos règles d'appartenance pour avoir deux ordinateurs dans ce regroupement.  

-   Je peux spécifier que seuls 50 % des serveurs du cluster puissent être hors connexion à tout moment dans le service de cluster. Utilisez les exemples de scripts dans la procédure pour spécifier les scripts de prédéploiement et de post-déploiement.  

-   Déployez une mise à jour vers ce regroupement. Examinez les fichiers start.txt et end.txt dans C:\temp et vérifiez les heures de début et de fin du déploiement sur les serveurs du cluster. Examinez le fichier UpdatesDeployment.log pour obtenir plus d'informations.  

#### <a name="to-create-a-collection-for-a-server-cluster"></a>Pour créer un regroupement pour un cluster de serveurs  

1.  [Créez un regroupement d’appareils](https://technet.microsoft.com/library/gg712295.aspx) contenant les serveurs du cluster.  

2.  Dans l’espace de travail **Ressources et Conformité**, cliquez sur **Regroupements d’appareils**, cliquez avec le bouton droit sur le regroupement qui contient les serveurs du cluster, puis cliquez sur **Propriétés**.  

3.  Sous l’onglet **Général**, sélectionnez **Tous les appareils font partie du même cluster de serveurs**, puis cliquez sur **Paramètres**.  

4.  Dans la page **Paramètres du cluster**, sélectionnez le pourcentage de serveurs pouvant être mis hors connexion simultanément pour que les mises à jour logicielles soient installées. Un seul serveur de cluster peut être mis hors connexion à la fois, quel que soit le pourcentage que vous fournissez. Configuration Manager arrondit à la valeur inférieure lors de la sélection du nombre de serveurs à traiter en même temps. Par exemple, si vous choisissez 51 % et que le cluster contient 4 serveurs, 2 serveurs sont mis hors connexion en même temps.  

5.  Indiquez s’il convient d’utiliser un script de prédéploiement (drainage de nœud) ou un script de post-déploiement (relance de nœud).  

    > [!TIP]  
    >  Voici des exemples que vous pouvez utiliser dans des tests de scripts de prédéploiement et de post-déploiement qui enregistrent l’heure actuelle dans un fichier texte :  
    >   
    >  **Prédéploiement**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\start.txt`  
    >   
    >  **Post-déploiement**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\temp\end.txt`  

#### <a name="to-deploy-software-updates-to-the-server-cluster"></a>Pour déployer des mises à jour logicielles sur le cluster de serveurs  

1.  [Déployez les mises à jour logicielles](https://technet.microsoft.com/library/gg712304.aspx) sur le regroupement du cluster de serveurs.  

2.  [Surveillez le déploiement des mises à jour logicielles](https://technet.microsoft.com/library/gg712304.aspx).  
