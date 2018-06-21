---
title: Capacités de la version Technical Preview 1605
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1605 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bafd028-1923-4463-9e3e-ee41bc0c437b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 05d87b253f2387dd8428f4b9fadea3fe5f3a48e8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342526"
---
# <a name="capabilities-in-technical-preview-1605-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1605 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.  

 **Problèmes connus dans cette version d’évaluation technique :**  

-   Avec la version d’évaluation technique 1605, si vous mettez à jour les propriétés d’un point de gestion après son installation, vous pouvez voir une erreur de console qui force la fermeture de la console.  Dans ce cas, vous pouvez désinstaller le point de gestion, puis le réinstaller en utilisant les paramètres de votre choix. Vous pouvez également modifier le point de gestion avant d’installer la version d’évaluation technique 1605.  

-   Lorsque vous utilisez la fonctionnalité Windows Store pour Entreprises avec la version d’évaluation technique 1604, puis mettez à niveau cette version vers la version d’évaluation technique 1605, vous ne pouvez plus afficher les données d’intégration. Toutes les autres fonctionnalités continuent à fonctionner. Si vous avez effectué l’intégration avec la version d’évaluation technique 1604, l’intégration demeure après l’installation de la version d’évaluation technique 1605 et vous n’avez aucune action supplémentaire à effectuer.  

 **Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

##  <a name="BKMK_PerAppVPN"></a> VPN par application pour les appareils Windows 10  
 Pour les appareils Windows 10 gérés à l’aide de Configuration Manager avec Intune, vous pouvez ajouter une liste d’applications qui ouvrent automatiquement une connexion VPN que vous avez configurée via la console d’administration Configuration Manager. Vous avez la possibilité de restreindre le trafic VPN à ces applications ou vous pouvez continuer à autoriser tout le trafic via la connexion VPN.  

 **Configuration requise** :  

-   Configuration Manager avec Intune  

-   Un profil VPN Windows 10 déployé sur au moins un appareil  

##  <a name="BKMK_InstallSU"></a> Améliorations apportées à la séquence de tâches Installer les mises à jour logicielles  
 Les améliorations suivantes ont été apportées à la séquence de tâches Installer les mises à jour logicielles :  

-   Une nouvelle variable de séquence de tâches, SMSTSSoftwareUpdateScanTimeout, est disponible. Elle vous permet de contrôler le délai d’attente pour la recherche des mises à jour logicielles pendant l’étape de séquence de tâches Installer les mises à jour logicielles. La valeur par défaut est de 30 minutes.  

-   Des améliorations ont été apportées à la journalisation. Le fichier journal smsts.log contiendra de nouvelles entrées qui référenceront d’autres fichiers journaux qui vous aideront à résoudre les problèmes au cours du processus d’installation des mises à jour logicielles.  

##  <a name="BKMK_PrepareConfigMgrClient"></a> Améliorations apportées à l’étape de séquence de tâches Préparer le client ConfigMgr pour capture  
 L’étape de préparation du client ConfigMgr va désormais supprimer complètement le client Configuration Manager, au lieu de supprimer uniquement des informations clés. Lorsque la séquence de tâches déploie l’image capturée du système d’exploitation, elle installe un nouveau client Configuration Manager chaque fois.  

##  <a name="BKMK_Grace"></a> Période de grâce pour les déploiements d’applications obligatoires  
 Dans certains cas, vous pouvez accorder plus de temps aux utilisateurs pour installer les déploiements d’applications obligatoires au-delà des échéances que vous avez configurées. Par exemple, si un utilisateur final vient de rentrer de congés, il peut être amené à patienter longtemps pendant l’installation des déploiements d’applications en retard. Il peut toutefois encore installer l’application immédiatement ou dès qu’il le souhaite.  

 Pour résoudre ce problème, vous pouvez désormais définir une **période de grâce** en déployant des paramètres du client Configuration Manager sur un regroupement.  

 Pour configurer la période de grâce, procédez comme suit :  

1.  Dans la page **Agent ordinateur** des paramètres du client, configurez la nouvelle propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** avec une valeur comprise entre **1** et **120** heures.  

2.  Dans un nouveau déploiement d’application, ou dans les propriétés d’un déploiement existant, dans la page **Planification**, cochez la case **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres client**.  

     Tous les déploiements pour lesquels cette case à cocher est activée et qui sont destinés à des appareils sur lesquels vous avez également déployé le paramètre du client utiliseront la période de grâce.  

 Dans cette version, la période de grâce que vous configurez n’est pas utilisée par les appareils clients. Si vous configurez une période de grâce et cochez la case, l’application est installée dans la première fenêtre non professionnelle que l’utilisateur a configurée après l’échéance.  

 Des options similaires ont été ajoutées dans l’Assistant de déploiement de mises à jour logicielles, dans l’Assistant des règles de déploiement automatique et dans les pages de propriétés. Toutefois, celles-ci ne sont pas actuellement implémentées dans cette version d’évaluation technique.  

##  <a name="BKMK_Remote"></a> Nouvelle expérience pour les actions des appareils à distance  
 L’exécution des actions des appareils à distance à partir de la console Configuration Manager a été améliorée.  
Des actions courantes telles que **Mettre hors service/réinitialiser**, **Réinitialisation du code secret**, **Verrouillage à distance** et **Contourner le verrou d’activation** figurent désormais dans le menu **Actions de l’appareil à distance**, accessible à partir de l’espace de travail **Ressources et Conformité**.  

 ![Capture d’écran du nouveau menu Actions de l’appareil à distance](media/New-Remote-Device-Actions.png)  

 Vous pouvez rechercher l’état de chacune de ces opérations aux emplacements suivants :  

-   Dans le volet d’informations, lorsque vous sélectionnez un appareil à partir du nœud **Périphériques**.  

-   Dans la page **Propriétés** d’un appareil.  

-   Dans la page principale du nœud **Périphériques** (toutes les colonnes peuvent ne pas être visibles par défaut).  

 Pour plus d’informations sur le contournement du verrou d’activation iOS, consultez [Aider à protéger les appareils iOS avec le contournement du verrou d’activation pour Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock) et notamment la section **Problèmes connus actuels liés au contournement du verrou d’activation dans la version d’évaluation technique de Configuration Manager**.  

##  <a name="BKMK_WSFB"></a> Applications du Windows Store pour Entreprises  
 Le [Windows Store pour Entreprises](https://www.microsoft.com/business-store) est l’emplacement où vous pouvez trouver et acheter des applications pour votre organisation, individuellement ou en volume. En connectant le Store à Configuration Manager, vous pouvez gérer les applications achetées en volume à partir de la console Configuration Manager, par exemple :  

-   Vous pouvez synchroniser la liste des applications achetées avec Configuration Manager.  

-   Les applications synchronisées apparaissent dans la console Configuration Manager et vous pouvez les déployer comme les autres applications.  

-   Toutes les 24 heures, Configuration Manager télécharge les informations de licence d’application à partir du Windows Store, et vous pouvez les consulter dans la console Configuration Manager.  

 Dans la version d’évaluation technique 1604, vous pouviez synchroniser et afficher les applications provenant du Windows Store pour Entreprises dans la console Configuration Manager. Dans cette version, nous avons ajouté la possibilité de créer et de déployer des applications Configuration Manager à partir d’applications du Windows Store synchronisées.  

### <a name="set-up-windows-store-for-business-synchronization"></a>Configurer la synchronisation du Windows Store pour Entreprises  

1.  Dans Azure Active Directory, inscrivez Configuration Manager en tant qu’outil de gestion « Application web et/ou API web ». Vous obtenez ainsi un ID de client dont vous aurez besoin ultérieurement.  

    1.  Dans le nœud Active Directory de [https://manage.windowsazure.com](https://manage.windowsazure.com), sélectionnez votre annuaire Azure Active Directory, puis cliquez sur **Applications** > **Ajouter**.  

    2.  Cliquez sur **Ajouter une application développée par mon organisation**.  

    3.  Attribuez un nom à l’application, sélectionnez **Application web** et/ou **API web**, puis cliquez sur la flèche **Suivant**.  

    4.  Entrez la même URL pour **URL de connexion** et pour **URI ID d’application**. L’URL peut être une chaîne quelconque qui ne doit pas nécessairement correspondre à une adresse réelle. Par exemple, vous pouvez entrer **https://&lt;votredomaine>/sccm**.  

    5.  Effectuez toutes les étapes de l'Assistant.  

2.  Dans Azure Active Directory, créez une clé de client pour l’outil de gestion inscrit.  

    1.  Sélectionnez l’application que vous venez de créer, puis cliquez sur **Configurer**.  

    2.  Sous **Clés**, sélectionnez une durée dans la liste, puis cliquez sur **Enregistrer**. Cela a pour effet de créer une nouvelle clé de client. Ne quittez pas cette page tant que vous n’avez pas correctement intégré le Windows Store pour Entreprises à Configuration Manager.  

3.  Dans le Windows Store pour Entreprises, configurez Configuration Manager en tant qu’outil de gestion du Windows Store.  

    1.  Ouvrez [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/managementtools) et connectez-vous si vous y êtes invité.  

    2.  Acceptez les conditions d’utilisation si nécessaire.  

    3.  Sous **Outils de gestion**, cliquez sur **Ajouter un outil de gestion**.  

    4.  Dans **Rechercher l’outil par son nom**, tapez le nom de l’application que vous avez créée précédemment dans AAD, puis cliquez sur **Ajouter**.  

    5.  Cliquez sur **Activer** en regard de l’application que vous venez d’importer.  

    6.  Dans l’Assistant **Show Offline-Licensed Apps** (Afficher les applications sous licence hors connexion), cliquez sur **Oui** si vous souhaitez autoriser l’achat d’applications sous licence hors connexion.  

4.  Achetez au moins une application au Windows Store pour Entreprises.  

5.  Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Windows Store pour Entreprises**.  

6.  Sous l’onglet **Accueil** du groupe **Créer**, cliquez sur **Ajouter un compte du Windows Store pour Entreprises**.  

7.  Ajoutez vos ID de locataire, ID de client et clé de client à partir d’Azure Active Directory, puis fermez l’Assistant.  

8.  Une fois que vous avez terminé, le compte que vous avez configuré figure dans la liste **Windows Store for Business Accounts** (Comptes Windows Store pour Entreprises) de la console Configuration Manager.  

### <a name="try-it-out"></a>Essayez !  
 Essayez d’exécuter la tâche suivante, puis indiquez-nous comment cela s’est passé en utilisant notre formulaire de commentaires à la page [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) du site Microsoft Connect :  

 Créez et déployez une application Configuration Manager à partir d’une application sous licence hors connexion du Windows Store pour Entreprises.  

1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.  

2.  Choisissez l’application que vous voulez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une application**.  

 Une application Configuration Manager contenant l’application du Windows Store pour Entreprises est alors créée. Vous pouvez ensuite déployer et surveiller cette application comme n’importe quelle autre application Configuration Manager.  

> [!IMPORTANT]  
>  Lorsque vous créez une application Configuration Manager avec un seul type de déploiement à partir d’une application hors connexion sous licence, elle peut être déployée sur des appareils gérés via la gestion des appareils mobiles, ainsi que par le client Configuration Manager. Si vous tentez de déployer une application avec plusieurs types de déploiement, l’installation échoue.  
>   
>  Vous ne pouvez pas déployer actuellement des applications en ligne sous licence à l’aide de Configuration Manager.  

##  <a name="BKMK_VPP2"></a> Améliorations générales pour les applications achetées en volume  

-   Dans cette version, les applications achetées en volume dans le Windows Store pour Entreprises et App Store iOS ont été consolidées dans une même vue, **Informations de licence pour les applications du Store**.  

-   Pour les applications iOS achetées en volume, l’onglet Programme d’achat en volume (VPP) Apple a été supprimé de la boîte de dialogue **Package d’application pour navigateur iOS** de l’Assistant Création d’une application. Pour créer une application achetée en volume pour iOS, procédez comme suit :  

    1.  1.  Dans l’espace de travail **Bibliothèque de logiciels** de la console Configuration Manager, développez **Gestion des applications**, puis cliquez sur **Informations de licence pour les applications du Store**.  

    2.  2.  Choisissez l’application que vous voulez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une application**.  

-   L’emplacement que vous utilisez pour obtenir et télécharger un jeton Apple VPP pour les applications achetées en volume dans la console Configuration Manager a changé. Vous pouvez désormais effectuer cette opération dans l’espace de travail **Admin** sous le nœud **Services cloud** > **Jetons du programme d’achat en volume (VPP) Apple**.  

##  <a name="BKMK_VPP"></a> Protection des données d’entreprise  
 Vous pouvez créer des éléments de configuration qui vous permettent de déployer vos stratégies de protection des données d’entreprise (PDE), notamment de choisir vos applications protégées, de définir le niveau de protection PDE et de rechercher des données d’entreprise sur le réseau. Pour plus d’informations sur PDE, consultez les rubriques suivantes :  

-   [Protéger vos données d’entreprise à l’aide de la protection des données d’entreprise (PDE)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-edp)  

-   [Créer et déployer une stratégie de protection des données d’entreprise (PDE) à l’aide de System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-edp-policy-using-sccm)  

##  <a name="BKMK_End"></a> Les utilisateurs finaux peuvent installer des applications à partir du portail d’entreprise  
 La gestion des appareils mobiles locale a été introduite dans la version 1511 de System Center Configuration Manager. Dans les versions précédentes, vous pouviez déployer des applications sur des appareils Windows 10 gérés par la gestion des appareils mobiles avec un objet de déploiement **Installation requise** pour les appareils gérés par la gestion des appareils mobiles locale.  

 Dans cette version, vous pouvez désormais déployer des applications avec un objet de déploiement **Disponible** pour les utilisateurs d’ordinateurs Windows 10 gérés par la gestion des appareils mobiles locale, et les utilisateurs peuvent désormais installer eux-mêmes ces applications à partir du portail d’entreprise.
Dans cette version d’évaluation technique, si le portail d’entreprise reste ouvert plus de 15 minutes, l’utilisateur final obtient un message d’erreur. Pour contourner ce problème, redémarrez le portail d’entreprise.  

### <a name="before-you-start"></a>Avant de commencer  

#### <a name="server-prerequisites"></a>Configuration requise du serveur  

-   .NET 4.5 ou version ultérieure (nécessite un redémarrage)  

-   PowerShell 3.0 pour le script de configuration (nécessite un redémarrage)  

#### <a name="client-prerequisites"></a>Prérequis pour le client  

-   Windows 10 Desktop 1511 (build 10586.218 du système d’exploitation) ou version ultérieure  

#### <a name="general-prerequisites"></a>Conditions préalables  

-   Assurez-vous d’avoir effectué les [étapes de préparation pour la gestion des appareils mobiles locale](https://technet.microsoft.com/library/mt613153.aspx) et d’avoir [inscrit vos appareils](https://technet.microsoft.com/library/mt627870.aspx).  

-   Pour bénéficier de la meilleure expérience possible d’installation d’application lorsque vous utilisez le portail d’entreprise, assurez-vous que Configuration Manager a une connexion active à Microsoft Intune.  

-   Si vous choisissez l’option d’inscription en bloc, configurez l’affinité entre utilisateur et appareil pour l’appareil inscrit avant d’essayer ce scénario.  

### <a name="configuration-steps"></a>Étapes de configuration  

#### <a name="install-the-application-catalog-roles-and-enable-mobile-device-management-support"></a>Installer les rôles de catalogue d’applications et activer la prise en charge de la gestion des appareils mobiles  

1.  Ajouter les rôles de service web du catalogue des applications et de site web  

    1.  Sélectionnez **Mode HTTPS** et l’option **Autoriser les appareils mobiles à utiliser ce point de service web du catalogue des applications**.  

    2.  Limitations de cette version d’évaluation technique :  

        -   Vous devez désinstaller tous les rôles de catalogue des applications existants avant d’activer l’option pour autoriser les appareils mobiles à se connecter.  

        -   Assurez-vous qu’il existe un seul ensemble de rôles de catalogue des applications et que ces rôles sont localisés sur un même système de site avec les rôles de point d’inscription et de point proxy d’inscription.  

2.  Vérifiez que les composants suivants sont opérationnels à partir du nœud État du composant dans la console Configuration Manager :  

    -   **SMS_AWEBSVC_CONTROL_MANAGER**  

    -   **SMS_DMAPPSVC_CONTROL_MANAGER**  

    -   **SMS_DMCONTENTSVC_CONTROL_MANAGER**  

    -   **SMS_PORTALWEB_CONTROL_MANAGER**  

### <a name="configure-boundaries"></a>Configurer les limites  
 Configurer les limites requises pour les points de distribution d’intranet uniquement.  

> [!NOTE]  
>  Seules les limites de plage IPv4 sont prises en charge pour l’instant pour la gestion des appareils mobiles.  

### <a name="deploy-the-company-portal-application-and-configuration"></a>Déployer l’application et la configuration de portail d’entreprise  

1.  Utilisez le script de configuration fourni avec la version d’évaluation technique pour préparer le déploiement et la configuration du portail d’entreprise :  

    1.  Ouvrez une fenêtre de commande PowerShell avec élévation des privilèges.  

    2.  Exécutez **set-executionPolicy RemoteSigned**  

    3.  À partir du dossier **&lt;répertoire d’installation de SCCM\>\cd.latest\SMSSETUP\TOOLS\MDM**, exécutez **.\ConfigurationScript.ps1**  

     Le script de configuration effectue les opérations suivantes :  

    1.  Il crée une application Configuration Manager avec un type de déploiement Package d’application Windows utilisant **CompanyPortalOnPremisesMDM.appx** dans le même dossier.  

    2.  Il crée un élément de configuration et une base de référence de configuration qui configure le portail d’entreprise.  

    3.  Il déploie la base de référence de configuration et l’application, et il ajoute l’application à tous les points de distribution.  

    > [!NOTE]  
    >  Si les rôles de catalogue d’applications ne sont pas colocalisés avec le site principal, prenez les mesures suivantes :  
    >   
    >  -   Dans l’espace de travail **Ressources et Conformité**, recherchez l’élément de configuration **OnPremMDM Portal Configuration CI - server urls**.  
    > -   Modifiez la valeur **Règles de compatibilité** en spécifiant le nom de domaine complet du système de site dans lequel figurent les rôles de catalogue d’applications.  

2.  Une fois que l’application de portail d’entreprise et sa configuration ont été déployées, vérifiez que l’application et la base de référence de configuration sont compatibles pour l’appareil donné en utilisant la section **Déploiements** de la console Configuration Manager. Le portail d’entreprise apparaît sous la forme de **Portail d’entreprise (version d’évaluation technique)** dans le menu Démarrer de l’appareil.  

### <a name="try-it-out"></a>Essayez !  
 Essayez d’exécuter les tâches suivantes, puis indiquez-nous comment cela s’est passé en utilisant notre formulaire de commentaires à la page [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) du site Microsoft Connect :  

1.  Déployey plusieurs applications avec des types de déploiement pris en charge sur un regroupement d’utilisateurs avec un objet de déploiement **Disponible**. Pour cette version d’évaluation technique, les applications qui requièrent une approbation de l’administrateur ne sont pas prises en charge et ne s’afficheront pas dans le portail d’entreprise.  

2.  Les utilisateurs peuvent rechercher des applications et les installer à partir du portail d’entreprise.  

     Après avoir ouvert le portail d’entreprise, vous voyez une boîte de dialogue d’authentification nommée **System Center Configuration Manager**. Spécifiez les informations d’identification Active Directory de l’utilisateur (sous la forme de user@domain ou de domaine\utilisateur) pour vous connecter.  

##  <a name="BKMK_SW1"></a> Nouveaux onglets pour les mises à jour et les systèmes d’exploitation dans le Centre logiciel  
 Dans cette version, les modifications suivantes ont été apportées pour améliorer la disposition de l’application Centre logiciel :  

-   L’onglet **Applications** a été divisé en trois onglets distincts : **Mises à jour**, **Systèmes d’exploitation** (auparavant accessibles dans la liste **Filtres**) et **Applications**.  

##  <a name="BKMK_ServerGroups"></a> Assurer la maintenance d’un groupe de serveurs  
 La version d’évaluation technique 1511 de System Center Configuration Manager incluait la possibilité de créer un regroupement dans lequel tous les appareils composaient un groupe de serveurs. Ensuite, vous pouviez configurer les paramètres du groupe de serveurs à utiliser pour déployer des mises à jour logicielles sur le groupe de serveurs, contrôler le pourcentage d’ordinateurs qui étaient mis à jour à un moment donné, et configurer des scripts PowerShell de prédéploiement et de post-déploiement pour exécuter des actions personnalisées.  

 La version d’évaluation technique 1605 de System Center Configuration Manager ajoute la possibilité de mettre à jour les ordinateurs dans le groupe de serveurs, dans un ordre spécifié que vous définissez. Elle ajoute une surveillance améliorée pour afficher l’état des ordinateurs dans le groupe de serveurs et elle offre la possibilité de supprimer les verrous de déploiement, ce qui s’avère utile lorsque les clients n’ont pas pu installer les mises à jour logicielles et empêchent les autres clients d’installer leurs mises à jour logicielles.  

### <a name="try-it-out"></a>Essayez !  
 Essayez d’exécuter les tâches suivantes, puis indiquez-nous comment cela s’est passé en utilisant notre formulaire de commentaires à la page [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) du site Microsoft Connect :  

-   Je peux créer un regroupement qui représente un groupe de serveurs. Pour ce test, vous pouvez configurer vos règles d'appartenance pour avoir deux ordinateurs dans ce regroupement.   

-   Je peux spécifier que les ordinateurs figurant dans le groupe de serveurs doivent installer les mises à jour logicielles dans un ordre spécifique en fonction des paramètres du groupe de serveurs pour le regroupement. Utilisez les exemples de scripts dans la procédure pour spécifier les scripts de prédéploiement et de post-déploiement.  

-   Je peux déployer une mise à jour logicielle sur ce regroupement. Examinez les fichiers start.txt et end.txt (créés à partir des exemples de script) dans C:\temp, et vérifiez les heures de début et de fin du déploiement sur les ordinateurs figurant dans le groupe de serveurs. Examinez le fichier UpdatesDeployment.log pour obtenir plus d'informations.  

#### <a name="to-create-a-collection-for-a-server-group"></a>Pour créer un regroupement pour un groupe de serveurs  

1.  [Créez un regroupement d’appareils](https://technet.microsoft.com/library/gg712295.aspx) contenant les ordinateurs du groupe de serveurs.  

2.  Dans l’espace de travail **Ressources et Conformité**, cliquez sur **Regroupements d’appareils**, cliquez avec le bouton droit sur le regroupement qui contient les ordinateurs du groupe de serveurs, puis cliquez sur **Propriétés**.  

3.  Sous l’onglet **Général**, sélectionnez **Tous les appareils font partie du même groupe de serveurs**, puis cliquez sur **Paramètres**.  

4.  Dans la page **Paramètres de groupe de serveurs**, spécifiez l’un des paramètres suivants :  

    -   **Autorisez un pourcentage des machines à être mises à jour en même temps** : Spécifie que seul un certain pourcentage de clients sont mis à jour à un moment quelconque. Si, par exemple, le regroupement compte 10 clients, et qu’il est configuré pour mettre à jour 30 % des clients en même temps, seuls 3 clients installeront les mises à jour logicielles à un moment donné quelconque.  

    -   **Autorisez un nombre de machines à être mises à jour en même temps** : Spécifie que seul un certain nombre de clients sont mis à jour à un moment quelconque.  

    -   **Spécifier la séquence de maintenance** : Spécifie que les clients du regroupement seront mis à jour l’un après l’autre, dans l’ordre que vous configurez. Un client installe les mises à jour logicielles après seulement que le client qui le précède dans la liste a terminé l’installation de ses mises à jour logicielles.  

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

#### <a name="to-deploy-software-updates-to-the-server-group-and-monitor-status"></a>Pour déployer des mises à jour logicielles dans le groupe de serveurs et surveiller leur état  

1.  [Déployez les mises à jour logicielles](https://technet.microsoft.com/library/gg712304.aspx) sur le regroupement du groupe de serveurs.  

2.  [Surveillez le déploiement des mises à jour logicielles](https://technet.microsoft.com/library/gg712304.aspx). Outre les affichages d’analyse standard pour le déploiement des mises à jour logicielles, une nouvelle description d’état est affichée lorsqu’un client attend son tour pour installer les mises à jour logicielles. **En attente d’un verrou** s’affiche pour ce nouvel état.  

#### <a name="to-clear-the-deployment-locks-for-computers-in-a-server-group"></a>Pour désactiver les verrous de déploiement pour les ordinateurs d’un groupe de serveurs  

1.  Dans l’espace de travail **Ressources et Conformité**, cliquez sur **Regroupements d’appareils**, puis cliquez sur le regroupement pour désactiver les verrous de déploiement.  

2.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Supprimer les verrous de déploiement du groupe de serveurs**. Quand des clients ne parviennent pas à installer les mises à jour logicielles et empêchent les autres clients d’installer leurs mises à jour logicielles, les verrous de déploiement peuvent être désactivés manuellement.  

##  <a name="BKMK_ATP"></a> Prise en charge du service Windows Defender - Protection avancée contre les menaces  
 Windows Defender - Protection avancée contre les menaces est un nouveau service qui aide les entreprises à détecter, analyser et contrer les attaques avancées ciblant leurs réseaux. En savoir plus sur [Protection avancée contre les menaces Windows Defender](https://blogs.windows.com/windowsexperience/2016/03/01/announcing-windows-defender-advanced-threat-protection). Configuration Manager peut vous aider à intégrer et surveiller des appareils clients Windows 10 Édition anniversaire gérés.  

### <a name="try-it-now"></a>Essayez maintenant !  
 Essayez d’exécuter les tâches suivantes, puis indiquez-nous comment cela s’est passé en utilisant notre formulaire de commentaires à la page [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) du site Microsoft Connect :  

-   Intégrer des appareils au service en ligne Windows Defender - Protection avancée contre les menaces  

-   Surveiller le déploiement du service Protection avancée contre les menaces Windows Defender sur les appareils gérés  

 **Conditions préalables**  

-   Abonnement au service en ligne Windows Defender - Protection avancée contre les menaces  

-   Clients exécutant Windows 10 Édition anniversaire (build 14328 et supérieure)  

-   Créer un fichier de configuration d’intégration de client  

    ##### <a name="how-to-create-an-onboarding-configuration-file"></a>Guide pratique pour créer un fichier de configuration d’intégration  

    1.  Connectez-vous au service en ligne Protection avancée contre les menaces Windows Defender.  

    2.  Cliquez sur l’élément de menu **Intégration du client**.  

    3.  Sélectionnez **System Center Configuration Manager**, puis cliquez sur **Télécharger le package**.  

    4.  Téléchargez le fichier d’archive compressé (.zip) et extrayez son contenu.  


##### <a name="onboard-devices-for-windows-defender-atp"></a>Intégrer des appareils pour Windows Defender ATP  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Endpoint Protection** > **Stratégies Windows Defender ATP**, puis cliquez sur **Créer une stratégie Windows Defender ATP**. L’Assistant Création d’une stratégie Windows Defender ATP s’ouvre.  

2.  Tapez un **nom** et une **description** pour la stratégie Windows Defender ATP, puis sélectionnez **Intégration**. Cliquez sur Suivant.  

3.  Sélectionnez **Parcourir** pour accéder au fichier de configuration fourni par le locataire du service cloud Windows Defender ATP de votre organisation. Cliquez sur **Suivant**.  

4.  Spécifiez les exemples de fichiers collectés et partagés à partir des appareils gérés pour les besoins d’analyse.  

    -   **Aucun**: aucun fichier d’exemple n’est collecté pour analyse.  

    -   **Fichiers exécutables portables** : des fichiers tels que les fichiers programme (.exe), les fichiers de bibliothèque de liens dynamiques (.dll), les fichiers de polices et des fichiers similaires qui peuvent être exploités dans des attaques informatiques sont collectés et partagés pour analyse.  

     Cliquez sur **Suivant**.  

5.  Passez en revue les informations de résumé et terminez l’Assistant.  

6.  Vous pouvez maintenant déployer la stratégie Windows Defender ATP sur les ordinateurs clients gérés en cliquant sur **Déployer**.  

##### <a name="monitor-windows-defender-atp"></a>Surveiller Windows Defender ATP  

1.  Dans la console Configuration Manager, accédez à **Surveillance** > **Vue d’ensemble** > **Sécurité**, puis cliquez sur **Windows Defender ATP**.  

2.  Examinez le tableau de bord Windows Defender - Protection avancée contre les menaces.  

    -   **État du déploiement de l’agent Windows Defender** : nombre et pourcentage d’ordinateurs clients gérés éligibles avec la stratégie Windows Defender ATP intégrée active.  

    -   **Intégrité de l’agent Windows Defender ATP** : pourcentage d’ordinateurs clients qui signalent l’état de l’agent Windows Defender ATP.  

        -   **Sain** : fonctionnement correct.  

        -   **Inactif** : aucune donnée n’a été envoyée au service durant la période.  

        -   **État de l’agent** : le service système de l’agent dans Windows n’est pas en cours d’exécution.  

        -   **Non intégré** : la stratégie a été appliquée, mais l’agent n’a pas signalé de stratégie intégrée.  

##  <a name="BKMK_DHA"></a> Attestation d’intégrité de l’appareil en local  
 L’attestation d’intégrité pour les appareils Windows 10 peut désormais être configurée pour communiquer à l’aide de l’infrastructure locale. Les administrateurs peuvent spécifier si le signalement s’effectue via des ressources cloud ou locales. Si l’option sur site est sélectionnée pour la création de rapports d’attestation d’intégrité, vous pouvez spécifier une URL pour le service. Les ordinateurs clients sans accès à Internet peuvent utiliser celui-ci pour activer et gérer des appareils à l’aide d’une attestation d’intégrité.  

### <a name="enable-health-attestation-for-on-premises-devices"></a>Activation de l’attestation d’intégrité pour les appareils locaux  
 Dans la version 1605, nous avons résolu quelques bogues découverts dans la version d’évaluation technique 1604.  Pour l’essayer, configurez le service d’attestation d’intégrité local à l’aide des paramètres de l’agent client.  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Paramètres client**, puis affectez à **Utiliser le service d’attestation d’intégrité local** la valeur **Oui**.  

2.  Spécifiez l’ **URL du service d’attestation d’intégrité local**, puis cliquez sur **OK**.  

##  <a name="BKMK_RestartOptions"></a> Nouvelles options de redémarrage pour les clients Windows 10 après l’installation de mises à jour logicielles  
 Quand une mise à jour logicielle nécessitant un redémarrage est déployée à l’aide de Configuration Manager et installée sur un ordinateur, un redémarrage en attente est planifié et une boîte de dialogue de redémarrage s’affiche. Actuellement, pour Windows 8 et versions ultérieures, si vous arrêtez ou redémarrez l’ordinateur à l’aide des options d’alimentation de Windows (et non pas à partir de la boîte de dialogue de redémarrage), la boîte de dialogue de redémarrage reste affichée après le redémarrage de l’ordinateur et celui-ci devra redémarrer à l’échéance configurée. Dans cette version d’évaluation technique, les options **Mettre à jour et redémarrer** et **Mettre à jour et arrêter** sont disponibles sur les ordinateurs Windows 10 dans les options d’alimentation de Windows chaque fois qu’un redémarrage est en attente pour une mise à jour logicielle Configuration Manager. Après l’utilisation de l’une de ces options, la boîte de dialogue de redémarrage ne s’affiche pas quand l’ordinateur redémarre.  

##  <a name="BKMK_IMEI"></a> Prédéclarer des appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS  
 Vous pouvez désormais identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity). Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) contenant les numéros IMEI des appareils ou saisir manuellement les informations sur les appareils.  Vous pouvez également importer les numéros de série des appareils iOS.  Les informations importées définissent l’appartenance des appareils inscrits sur « Entreprise ».  Une licence Intune reste nécessaire pour chaque utilisateur qui accède au service.  

### <a name="try-it-out"></a>Essayez !  
 Essayez d’exécuter les tâches suivantes, puis indiquez-nous comment cela s’est passé en utilisant notre formulaire de commentaires à la page [Configuration Manager feedback program](https://connect.microsoft.com/ConfigurationManagervnext/ConfigMgr%20Customer%20Feedback) du site Microsoft Connect :  

-   Importez un ensemble de numéros IMEI dans un fichier .csv. Chaque ligne peut contenir le numéro IMEI suivi d’un champ de détails.  

-   Importez manuellement des numéros IMEI à partir de la console Configuration Manager.  

-   Importez un ensemble de numéros de série iOS dans un fichier .csv. Là encore, chaque ligne contient un numéro, suivi de détails éventuels sur l’appareil.  

##### <a name="pre-declare-corporate-owned-devices-with-imei-or-ios-serial-number"></a>Prédéclarer des appareils d’entreprise avec numéro IMEI ou numéro de série iOS  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Tous les appareils d’entreprise** > **Appareils prédéclarés**, puis cliquez sur **Créer des appareils prédéclarés**. L’Assistant Appareils prédéclarés s’ouvre.  

2.  Spécifiez la façon dont vous souhaitez ajouter les informations sur les appareils :  

    -   **Charger un fichier CSV contenant des numéros IMEI et des informations détaillées** : pour charger une liste de numéros, consultez l’étape 3.  

    -   **Ajouter manuellement des numéros IMEI et des informations détaillées** : pour saisir manuellement des informations, tapez le numéro IMEI ou le numéro de série iOS, ainsi que des informations détaillées sur les appareils, puis passez à l’étape 4.  

3.  Pour les fichiers chargés, accédez au fichier .csv contenant les informations à utiliser pour prédéclarer les appareils d’entreprise. Le fichier doit avoir le format suivant, à l’exception de la ligne du haut (fournie à titre indicatif uniquement) :  

    |**No IMEI**|**No de série iOS**|**SE**|**Détails**|
    |---|---|---|---|
    |123456789012345||WINDOWS|Appareil d’entreprise Windows|
    |123456789012|A0BCD0EFGH0J|IOS|Appareils d’entreprise iOS|
    |123456789012346||ANDROID|Appareil d’entreprise Android|

     **Colonnes :**  

    -   Colonne 1 : Numéro IMEI : Un numéro IMEI ou un numéro de série iOS est requis pour chaque ligne.  

    -   Colonne 2 : Numéro de série iOS : Seuls des numéros de série iOS peuvent être prédéclarés. Utilisez le numéro IMEI pour d’autres plateformes d’appareil  

    -   Colonne 3 : Système d’exploitation de l’appareil (des majuscules sont requises) :  

        -   IOS : Tous les appareils iOS  

        -   WINDOWS : Inclut les appareils Windows Phone, Windows 10 Mobile et PC Windows  

        -   ANDROID : Tous les appareils Android  

    -   Colonne 4 : Détails : Informations supplémentaires sur l’appareil qui figurent dans la console Configuration Manager.  

     Cliquez sur **Suivant**.  

4.  Vérifiez les résultats de l’importation du fichier. Les informations détaillées des numéros IMEI ou de série précédemment importés seront mises à jour avec de nouvelles informations.  Cliquez sur **Suivant** pour continuer ou sur **Précédent** pour conserver les détails modifiés, puis terminez l’Assistant.  
