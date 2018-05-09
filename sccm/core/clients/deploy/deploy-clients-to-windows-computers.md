---
title: Déployer des clients sur Windows
titleSuffix: Configuration Manager
description: Apprenez à déployer le client Configuration Manager sur des ordinateurs Windows.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5efca393afe2fc6441d074f987549228e7d0418f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-clients-to-windows-computers-in-system-center-configuration-manager"></a>Comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’installer des clients Configuration Manager, vérifiez que toutes les [conditions préalables](../../../core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) sont réunies et que vous avez réalisé toutes les configurations de déploiement requises.   



##  <a name="BKMK_ClientPush"></a> Guide pratique pour installer des clients à l’aide d’une installation poussée du client  

Vous pouvez configurer une installation Push du client pour un site. L’installation du client s’exécute automatiquement sur les ordinateurs qui sont découverts dans les limites configurées du site, dans la mesure où ces limites sont configurées en tant que groupe de limites. Vous pouvez également lancer une installation poussée du client en exécutant l'Assistant Installation poussée du client pour un regroupement ou une ressource spécifique dans un regroupement.  

L’Assistant Installation poussée du client permet également d’installer le client Configuration Manager selon les résultats d’une [requête](../../../core/servers/manage/queries-technical-reference.md). Pour que l’installation réussisse, l’un des éléments retournés par la requête doit correspondre à l’attribut **ResourceID** de la classe **Ressource système**.   

Si le serveur de site ne parvient pas à contacter l’ordinateur client ou à démarrer le processus d’installation, il tente à nouveau l’installation de façon automatique toutes les heures. Le serveur renouvelle les tentatives pendant sept jours, au maximum.  

Pour vous aider à suivre le processus d’installation du client, installez un point d’état de secours avant d’installer les clients. Du moment qu’un point d'état de secours est installé, il est automatiquement attribué aux clients quand ces derniers sont installés selon la méthode d’installation Push du client. Pour suivre la progression d’installation du client, consultez les rapports de déploiement et d’attribution du client. 

Les fichiers journaux du client fournissent des informations plus détaillées pour le dépannage. Les fichiers journaux ne nécessitent pas de point d’état de secours. Par exemple, le fichier **CCM.log** du serveur de site enregistre tous les problèmes de ce dernier au moment de se connecter à l’ordinateur. Le fichier **CCMSetup.log** du client enregistre le processus d’installation.  

> [!IMPORTANT]  
>  Afin que l'installation poussée du client réussisse, assurez-vous que toutes les conditions préalables sont respectées. Pour plus d'informations, consultez [Dépendances liées aux méthodes d’installation](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).  

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurer le site en vue de l’utilisation automatique de l’installation Push du client pour les ordinateurs découverts

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** > **Sites**.  

3.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation poussée du client automatique à l’échelle du site.  

4.  Dans l’onglet **Accueil** du groupe **Paramètres**, choisissez **Paramètres d’installation du client** > **Installation poussée du client**.  

5.  Dans l’onglet **Général** de la boîte de dialogue **Propriétés de l’installation poussée du client**, sélectionnez **Activer l’installation poussée du client automatique à l’échelle du site**. Sélectionnez les types de systèmes vers lesquels Configuration Manager doit transférer (push) le logiciel client.  

6.  Indiquez si vous souhaitez installer le client sur les contrôleurs de domaine.  

7.  Sous l’onglet **Comptes**, spécifiez le ou les comptes que Configuration Manager doit utiliser au moment de se connecter à l’ordinateur cible. Cliquez sur l’icône **Créer**, entrez le **nom d’utilisateur** et le **mot de passe** (pas plus de 38 caractères), confirmez le mot de passe, puis cliquez sur **OK**. Spécifiez au moins un compte d’installation Push du client. Ce compte doit disposer de droits d’administrateur local sur l’ordinateur cible pour pouvoir installer le client. Si vous ne spécifiez pas de compte d’installation Push du client, Configuration Manager essaie d’utiliser le compte d’ordinateur du système de site. L’utilisation du compte d’ordinateur système fait échouer l’installation Push du client sur plusieurs domaines.  
    > [!NOTE]  
    >  Pour utiliser l’installation Push du client sur un site secondaire, spécifiez le compte du site secondaire qui lance l’installation Push du client.  
    >   
    >  Pour plus d’informations sur le compte d’installation Push du client, consultez la procédure suivante, [Utiliser l’Assistant Installation Push du client](#use-the-client-push-installation-wizard).  

8.  Renseignez l’onglet **Propriétés de l’installation**.

     Si le schéma est étendu pour Configuration Manager, le site publie dans Active Directory Domain Services les [Propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md) que vous spécifiez sous cet onglet. Ces propriétés sont lues par les installations du client dans lesquelles CCMSetup s’exécute sans propriétés d’installation.  

    > [!NOTE]  
    >  Si vous activez l’installation Push du client sur un site secondaire, veillez à ce que la propriété **SMSSITECODE** soit définie sur le nom de site Configuration Manager de son site principal parent. Si le schéma Active Directory est étendu pour Configuration Manager, vous pouvez aussi définir cette propriété sur AUTO pour rechercher automatiquement l’attribution de site correcte.  

### <a name="use-the-client-push-installation-wizard"></a>Utiliser l’Assistant Installation Push du client

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Configuration du site** > **Sites**.  

3.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation poussée du client automatique à l’échelle du site.  

4.  Dans l’onglet **Accueil** du groupe **Paramètres**, choisissez **Paramètres d’installation du client** > **Installation poussée du client**.  

5.  Renseignez l’onglet **Propriétés de l’installation**.  

     Si le schéma est étendu pour Configuration Manager, le site publie dans Active Directory Domain Services les [Propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md) que vous spécifiez sous cet onglet. Ces propriétés sont lues par les installations du client dans lesquelles CCMSetup s’exécute sans propriétés d’installation.   

6.  Dans la console Configuration Manager, choisissez **Ressources et Conformité**.  

7.  Dans l'espace de travail **Ressources et Conformité** , sélectionnez un ou plusieurs ordinateurs ou un regroupement d'ordinateurs.  

8.  Sous l’onglet **Accueil**, choisissez l’une des options suivantes :  

    -   Si vous souhaitez installer le client sur un seul ordinateur ou plusieurs ordinateurs, dans le groupe **Appareil**, choisissez **Installer le client**.  

    -   Si vous souhaitez installer le client dans un regroupement d’ordinateurs, dans le groupe **Regroupement**, choisissez **Installer le client**.  

9. Dans la page **Avant de commencer** de l’**Assistant Installation du client**, consultez les informations, puis choisissez **Suivant**.  

10. Renseignez la page **Options d’installation**.  

11. Passez en revue les paramètres d'installation, puis fermez l'Assistant.  

> [!NOTE]  
>  Vous pouvez utiliser l’Assistant pour installer des clients même si le site n’est pas configuré pour l’installation Push du client.  



##  <a name="BKMK_ClientSUP"></a> Guide pratique pour installer des clients à l’aide d’une installation basée sur une mise à jour logicielle  
 L’installation du client en fonction des mises à jour logicielles publie le client sur un point de mise à jour logicielle, sous forme de mise à jour logicielle. Utilisez cette méthode pour une première installation ou une mise à niveau.  

 Si le client Configuration Manager est installé sur un ordinateur, celle-ci reçoit la stratégie de configuration du client du site. Cette stratégie inclut le nom du serveur du point de mise à jour logicielle et le port à partir duquel les mises à jour logicielles sont obtenues.   

> [!IMPORTANT]  
>  Pour pouvoir utiliser l'installation basée sur les mises à jour logicielles, vous devez utiliser le même serveur Windows Server Update Services (WSUS) pour l'installation du client et les mises à jour logicielles. Ce serveur doit être utilisé comme le point de mise à jour logicielle actif dans un site principal. Pour plus d’informations, consultez [Installer un point de mise à jour logicielle](../../../sum/get-started/install-a-software-update-point.md).  

Si le client Configuration Manager n’est pas installé sur un ordinateur, configurez et attribuez un objet de stratégie de groupe dans Active Directory Domain Services pour spécifier le nom du serveur du point de mise à jour logicielle.  

Il est impossible d’ajouter des propriétés de ligne de commande à une installation du client basée sur des mises à jour logicielles. Si vous avez étendu le schéma Active Directory pour Configuration Manager, les ordinateurs clients demandent automatiquement les propriétés d’installation à Active Directory Domain Services au moment de l’installation.  

Si vous n’avez pas étendu le schéma Active Directory, vous pouvez utiliser la stratégie de groupe pour fournir les paramètres d’installation du client aux ordinateurs de votre site. Ces paramètres s'appliquent automatiquement à toutes les installations du client basé sur les mises à jour logicielles. Pour plus d’informations, consultez [Comment fournir des propriétés d’installation du client (installation basée sur une stratégie de groupe et sur les mises à jour logicielles)](#BKMK_Provision) et [Comment attribuer des clients à un site](../../../core/clients/deploy/assign-clients-to-a-site.md).  

Les procédures ci-dessous vous permettent de configurer des ordinateurs sans client Configuration Manager pour qu’ils utilisent le point de mise à jour logicielle pour l’installation du client et les mises à jour logicielles, et pour qu’ils publient le logiciel client sur le point de mise à jour logicielle.  

> [!NOTE]  
>  Si les ordinateurs sont dans un état de redémarrage en attente suite à une précédente installation de logiciel, une installation du client basée sur une mise à jour logicielle peut entraîner le redémarrage de l'ordinateur.  

### <a name="configure-a-group-policy-object-in-active-directory-domain-services-to-specify-the-software-update-point-for-client-installation-and-software-updates"></a>Configurez un objet de stratégie de groupe dans Active Directory Domain Services de façon à spécifier le point de mise à jour logicielle pour l’installation du client et les mises à jour logicielles :  

1.  Utilisez la console de gestion des stratégies de groupe pour ouvrir un objet de stratégie de groupe nouveau ou existant.  

2.  Dans la console, développez **Configuration ordinateur**, **Modèles d’administration**, **Composants Windows**, puis choisissez **Windows Update**.  

3.  Ouvrez les propriétés du paramètre **Spécifier l’emplacement intranet du service de mise à jour Microsoft**, puis choisissez **Activé**.  

4.  Dans la zone **Set the intranet update service for detecting updates** (Définir le service intranet de mise à jour pour la détection des mises à jour), spécifiez le nom et le port du serveur du point de mise à jour logicielle  :  

    -   Si le système de site Configuration Manager est configuré pour utiliser un nom de domaine complet (FQDN), utilisez le format de domaine complet.  

    -   Si le système de site Configuration Manager n’est pas configuré pour utiliser un nom de domaine complet (FQDN), utilisez un format de nom court.  

    > [!NOTE]  
    >  Pour déterminer le numéro de port, consultez [Comment déterminer les paramètres de port utilisés par WSUS](../../../sum/plan-design/plan-for-software-updates.md).  

     Exemple : **http://server1.contoso.com:8530**  

5.  Dans la zone **Configurer le serveur intranet de statistiques**, spécifiez le nom du serveur intranet de statistiques. Cela ne doit pas être nécessairement le serveur du point de mise à jour logicielle. S’il s’agit du même serveur, le format ne doit pas nécessairement correspondre.  

6.  Attribuez l’objet de stratégie de groupe aux ordinateurs sur lesquels vous voulez installer le client et recevoir les mises à jour logicielles.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publier le client Configuration Manager sur le point de mise à jour logicielle  

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration de site** > **Sites**.  

3.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation du client en fonction des mises à jour logicielles.  

4.  Dans l’onglet **Accueil** du groupe **Paramètres**, choisissez **Paramètres d’installation du client**, puis **Installation du client en fonction des mises à jour logicielles**.  

5.  Sélectionnez **Activer l’installation du client basée sur les mises à jour logicielles**.  

6.  Si la version du logiciel client est plus récente sur le serveur de site Configuration Manager que celle sur le point de mise à jour logicielle, la boîte de dialogue **Version plus récente du package client détectée** s’affiche. Cliquez sur **Oui** pour publier la version la plus récente.  

    > [!NOTE]  
    >  Si le logiciel client n’a pas été publié auparavant sur le point de mise à jour logicielle, cette boîte de dialogue est vide.  

La mise à jour logicielle du client Configuration Manager n’est pas mise à jour automatiquement quand il existe une nouvelle version. Si vous mettez à niveau le site, ce qui comprend une nouvelle version du client, répétez cette procédure et cliquez sur **Oui** à l’étape 6.  



##  <a name="BKMK_ClientGP"></a> Guide pratique pour installer des clients à l’aide d’une stratégie de groupe  
 Vous pouvez utiliser la stratégie de groupe dans Active Directory Domain Services pour publier ou attribuer le client Configuration Manager en vue de l’installer sur des ordinateurs de votre entreprise. Le client s’installe au démarrage de l’ordinateur. Quand vous utilisez la stratégie de groupe, le client s’affiche dans **Ajout/Suppression de programmes** dans le Panneau de configuration pour permettre à l’utilisateur de procéder à l’installation.  

 Utilisez le package Windows Installer (CCMSetup.msi) pour les installations basées sur la stratégie de groupe. Ce fichier se trouve dans le dossier **&lt;répertoire d’installation de ConfigMgr\>\bin\i386** sur le serveur de site Configuration Manager. Vous ne pouvez pas ajouter des propriétés à ce fichier pour modifier le comportement à l’installation.  

> [!IMPORTANT]  
>  Vous devez disposer d’autorisations d’administrateur pour accéder aux fichiers d’installation du client.  

-   Si le schéma Active Directory est étendu pour Configuration Manager et que l’option **Publier ce site dans les services d’annuaire Active Directory** est sélectionnée sous l’onglet **Avancé** de la boîte de dialogue **Propriétés du site**, les ordinateurs clients demandent automatiquement les propriétés d’installation aux services de domaine Active Directory. Pour plus d'informations sur les propriétés d’installation publiées, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

-   Si le schéma Active Directory n’a pas été étendu, vous pouvez appliquer la procédure de cette rubrique pour stocker les propriétés d’installation dans le Registre des ordinateurs : [Comment fournir des propriétés d’installation du client (Stratégie de groupe et installation du client basé sur les mises à jour logicielles)](#BKMK_Provision). Ces propriétés d’installation sont utilisées pendant l’installation du client.  

Pour plus d’informations sur l’utilisation de la stratégie de groupe dans Active Directory Domain Services pour installer des logiciels, consultez la documentation Windows Server.  



##  <a name="BKMK_Manual"></a> Guide pratique pour installer des clients manuellement  
 Vous pouvez installer manuellement le logiciel client sur les ordinateurs dans votre entreprise à l’aide du programme CCMSetup.exe. Ce programme et ses fichiers de prise en charge se trouvent dans le dossier **Client** du dossier d’installation de Configuration Manager sur le serveur de site et sur les points de gestion dans votre site. Ce dossier est partagé sur le réseau sous  

 \\\\*&lt;nom du serveur de site\>* \SMS_*&lt;code de site\>* \Client\  

 où *&lt;nom du serveur de site\>* est le nom d’un des serveurs hébergeant un point de gestion et *&lt;code de site\>* est le code du site principal auquel le client est attribué. Pour exécuter CCMSetup.exe à partir de la ligne de commande sur le client, vous devez mapper un lecteur réseau à cet emplacement, puis exécuter la commande.  

> [!IMPORTANT]  
>  Vous devez disposer d’autorisations d’administrateur pour accéder aux fichiers d’installation du client.  

 Le programme CCMSetup.exe copie toutes les conditions préalables nécessaires sur l’ordinateur client, puis fait appel au package Windows Installer (Client.msi) pour installer le client. Vous ne pouvez pas exécuter Client.msi directement.  

 Vous pouvez spécifier des propriétés de ligne de commande pour CCMSetup.exe et Client.msi afin de modifier le comportement de l'installation du client. Spécifiez les propriétés de CCMSetup (propriétés commençant par **/**) avant de spécifier les propriétés de Client.msi. Par exemple :  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`    

et le client s’installe en utilisant les propriétés suivantes :  

|Propriété|Description|  
|--------------|-----------------|  
|**/mp:SMSMP01**|Cette propriété de CCMSetup spécifie le point de gestion SMSMP01 pour télécharger les fichiers requis d'installation du client.|  
|**/logon**|Cette propriété de CCMSetup spécifie que l’installation doit s’arrêter si un client Configuration Manager se trouve déjà sur l’ordinateur.|  
|**SMSSITECODE=AUTO**|Cette propriété de Client.msi spécifie que le client doit essayer de trouver le code de site Configuration Manager à utiliser, par exemple, en utilisant les services de domaine Active Directory.|  
|**FSP=SMSFP01**|Cette propriété de Client.msi précise que le point d’état de secours nommé SMSFP01 est utilisé pour recevoir les messages d’état envoyés par l’ordinateur client.|  

 Pour obtenir des détails sur toutes les propriétés de CCMSetup.exe, consultez [À propos des propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md).  

> [!Tip]  
> Pour plus d’informations sur la procédure d’installation du client Configuration Manager sur un appareil Windows 10 moderne utilisant l’identité Azure AD, consultez [Installer et affecter des clients Windows 10 Configuration Manager à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Cette procédure concerne les clients sur intranet ou Internet.  


### <a name="examples"></a>Exemples
 Ces exemples concernent les clients Active Directory sur intranet. Ils utilisent les valeurs suivantes pour représenter les différents aspects du site :  

 **MPSERVER** = serveur hébergeant le point de gestion   
**FSPSERVER** = serveur hébergeant le point d’état de secours  
**ABC** = code de site  
**contoso.com** = nom de domaine  

 Tous les serveurs de système de site sont configurés avec un nom de domaine complet d’intranet. Le site est publié dans la forêt Active Directory du client.  

 Sur l’ordinateur client, ouvrez une session en tant qu’administrateur local, mappez un lecteur (z:) à \\\MPSERVER\SMS_ABC\Client, indiquez le lecteur z à l’invite de commandes, puis exécutez l’une des commandes suivantes :  

 **Exemple 1 :**  

`CCMSetup.exe`  

Cet exemple installe le client sans propriétés supplémentaires. Le client est configuré automatiquement par rapport aux propriétés d’installation du client publiées dans Active Directory Domain Services. Il est automatiquement configuré pour les paramètres suivants : 
- Code de site. Ce paramètre exige que l’emplacement réseau du client soit inclus dans un groupe de limites configuré pour l’attribution du client. 
- Point de gestion
- Point d’état de secours
- Communiquer à l’aide de HTTPS uniquement  
  
Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

 **Exemple 2 :**  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Cet exemple ignore la configuration automatique fournie par Active Directory Domain Services. Il n’exige pas que l’emplacement réseau du client soit inclus dans un groupe de limites configuré pour l’attribution du client. En revanche, l’installation spécifie les paramètres suivants :
- Code de site
- Point de gestion intranet 
- Point de gestion Internet
- Point d’état de secours qui accepte les connexions en provenance d’Internet
- Utiliser un certificat client PKI (si disponible) qui offre la plus longue période de validité  



##  <a name="BKMK_ClientLogonScript"></a> Guide pratique pour installer des clients à l’aide de scripts d’ouverture de session  
 Configuration Manager prend en charge les scripts d’ouverture de session pour installer le logiciel client Configuration Manager. Vous pouvez utiliser le fichier programme **CCMSetup.exe** dans un script de connexion pour déclencher l'installation du client.  

 L'installation via un script d'ouverture de session utilise les mêmes méthodes que l'installation manuelle du client. Vous pouvez spécifier la propriété d’installation **/logon** pour CCMSsetup.exe. S’il existe déjà une version du client sur l’ordinateur, cette propriété empêche l’installation du client. Ce comportement empêche la réinstallation du client à chaque exécution du script d’ouverture de session.  

 Si aucune source d’installation n’est spécifiée par la propriété **/Source** et qu’aucun point de gestion à partir duquel obtenir l’installation n’est spécifié par la propriété **/MP**, CCMSetup.exe recherche le point de gestion dans Active Directory Domain Services. Ce comportement se produit uniquement si le schéma a été étendu pour Configuration Manager et que le site est publié dans Active Directory Domain Services. Alternativement, le client peut utiliser le service de nom de domaine (DNS) ou WINS pour rechercher un point de gestion.  



##  <a name="BKMK_ClientApp"></a> Guide pratique pour installer des clients à l’aide d’un package et d’un programme  
 Vous pouvez utiliser Configuration Manager pour créer et déployer un package et un programme qui mettent à niveau le logiciel client sur les ordinateurs sélectionnés dans votre hiérarchie. Un fichier de définition de package pour renseigner les propriétés du package avec les valeurs généralement utilisées est fourni avec Configuration Manager. Vous pouvez personnaliser le comportement de l’installation du client en spécifiant des propriétés de ligne de commande supplémentaires.  

> [!NOTE]  
>  Vous ne pouvez pas mettre à niveau des clients Configuration Manager 2007 avec cette méthode. Au lieu de cela, utilisez la mise à niveau automatique des clients, qui crée et déploie automatiquement un package contenant la dernière version du client. Pour plus d’informations, consultez [Mettre à niveau les clients](../../../core/clients/manage/upgrade/upgrade-clients.md).  
>   
>  Pour plus d’informations sur la migration à partir de versions plus anciennes du client Configuration Manager, consultez [Planification d’une stratégie de migration de clients](../../../core/migration/planning-a-client-migration-strategy.md).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Créer un package et un programme pour le logiciel client  

Pour créer un package et un programme Configuration Manager que vous pouvez déployer sur les ordinateurs clients Configuration Manager afin de mettre à niveau le logiciel client, utilisez la procédure suivante.  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un package à partir de la définition**.  

4.  Dans la page **Définition du package** de l’Assistant, sélectionnez **Microsoft** dans la liste déroulante **Éditeur** et **Mise à niveau du client Configuration Manager** dans la liste **Définition du package**.  

5.  Dans la page **Fichiers sources**, sélectionnez **Toujours obtenir les fichiers depuis le dossier source**.  

6.  Dans la page **Dossier source**, sélectionnez **Chemin d’accès réseau (nom UNC)**. Entrez ensuite le chemin réseau de l’ordinateur et du dossier contenant les fichiers d’installation du client.  

    > [!NOTE]  
    >  L’ordinateur sur lequel le déploiement de Configuration Manager s’effectue doit avoir accès au dossier réseau spécifié. Dans le cas contraire, l’installation échoue.  

    Pour modifier l’une des propriétés d’installation du client, modifiez les paramètres de ligne de commande CCMSetup.exe sous l’onglet **Général** de la boîte de dialogue du programme **Propriétés des mises à niveau silencieuses de l’Agent Configuration Manager**. Les propriétés d'installation par défaut sont **/noservice SMSSITECODE=AUTO**.  

9. Distribuez le package à tous les points de distribution qui doivent héberger le package de mise à niveau des clients. Vous pouvez ensuite déployer le package sur des regroupements d’ordinateurs contenant les clients à mettre à niveau.  



## <a name="bkmk_mdm"></a>Comment installer des clients sur des appareils Windows gérés par Intune MDM

Vous pouvez déployer les fichiers d’installation du client sur les ordinateurs qui sont inscrits dans Microsoft Intune. 

Cette procédure s’applique aux clients traditionnels connectés à l’intranet. Elle utilise des méthodes d’authentification de client classiques. Pour que l’appareil reste dans un état géré une fois le logiciel client installé, il doit se trouver sur l’intranet et dans une limite de site Configuration Manager.  

Pour plus d’informations sur la procédure d’installation du client Configuration Manager sur un appareil Windows 10 moderne utilisant l’identité Azure AD, consultez [Installer et affecter des clients Windows 10 Configuration Manager à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]
> Une fois le logiciel client installé, l’appareil est désinscrit d’Intune.
> 
> Depuis la version 1710, les clients ne se désinscrivent pas d’Intune. Ils peuvent disposer à la fois du client Configuration Manager et d’une inscription MDM. Pour plus d’informations, consultez [Cogestion](/sccm/core/clients/manage/co-management-overview).

###  <a name="install-clients-with-intune"></a>Installez les clients avec Intune :

1. Dans Intune, [créez une application](/intune/deploy-use/add-apps-for-mobile-devices-in-microsoft-intune) contenant le fichier d’installation du client Configuration Manager **ccmsetup.msi**. Ce fichier se trouve dans le dossier **&lt;répertoire d’installation de ConfigMgr\>\bin\i386** sur le serveur de site Configuration Manager.

2. Dans l’Éditeur de logiciel Intune, entrez des paramètres de ligne de commande. Par exemple, utilisez la ligne de commande suivante avec un client classique sur l’intranet :

  `CCMSETUPCMD="/MP:&lt;FQDN of management point> SMSMP=&lt;FQDN of management point> SMSSITECODE=&lt;Your site code> DNSSUFFIX=&lt;DNS Suffix of management point>"`  

   > [!Note]  
   > Pour obtenir un exemple de ligne commande à utiliser avec un client Windows 10 moderne exploitant l’authentification Azure AD, consultez [Préparer des appareils Windows 10 à la cogestion](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client).

3. [Déployez l’application](/intune/deploy-use/deploy-apps-in-microsoft-intune) sur les ordinateurs Windows inscrits.



##  <a name="BKMK_ClientImage"></a> Guide pratique pour installer des clients à l’aide d’une image de l’ordinateur  
Vous pouvez préinstaller le logiciel client Configuration Manager sur un ordinateur de référence que vous pouvez utiliser pour créer une image de système d’exploitation.   

> [!Important]
> Quand vous utilisez la séquence de tâches Configuration Manager pour déployer l’image du système d’exploitation, l’étape [Préparer le client ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) de la séquence de tâches supprime entièrement le client Configuration Manager. 

### <a name="prepare-the-client-computer-for-imaging"></a>Préparer l’ordinateur client à la mise en image  

1.  Installez manuellement le logiciel client Configuration Manager sur l’ordinateur de référence. Pour plus d'informations, voir [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Ne spécifiez pas de code de site Configuration Manager pour le client dans les propriétés de ligne de commande CCMSetup.exe.  

2.  À l’invite de commandes, tapez `net stop ccmexec` pour vérifier que le service **Hôte de l’agent SMS** (Ccmexec.exe) ne s’exécute pas sur l’ordinateur de référence.
3.  Supprimez le fichier **SMSCFG.INI** du dossier **Windows** sur l’ordinateur de référence.  
3.  Supprimez les certificats qui sont éventuellement stockés dans le magasin local de l’ordinateur de référence. Par exemple, si vous utilisez des certificats d'infrastructure à clé publique (PKI), vous devez supprimer les certificats dans le magasin **Personnel** de l' **Ordinateur** et de l' **Utilisateur** avant de mettre l'ordinateur en image.

4.  Si les clients sont installés dans une hiérarchie Configuration Manager différente de celle de l’ordinateur de référence, supprimez la clé racine approuvée de cet ordinateur.  
    > [!NOTE]  
    >  Si les clients ne peuvent pas demander aux services de domaine Active Directory de localiser un point de gestion, ils peuvent utiliser une clé racine approuvée pour déterminer les points de gestion approuvés. Si tous les clients mis en image sont déployés dans la même hiérarchie que celle de l’ordinateur maître, conservez la clé racine approuvée. Si les clients sont déployés dans des hiérarchies différentes, supprimez la clé racine approuvée. De même, fournissez la nouvelle clé racine approuvée à ces clients. Pour plus d’informations, voir [Planification de la clé racine approuvée](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK). 

5.  Utilisez votre logiciel d'acquisition d'images pour capturer l'image de l'ordinateur maître.  

6.  Déployez l'image vers les ordinateurs de destination.  



##  <a name="BKMK_ClientWorkgroup"></a> Guide pratique pour installer des clients sur les ordinateurs d’un groupe de travail  
 Configuration Manager prend en charge l’installation du client sur des ordinateurs de groupe de travail. Installez le client sur les ordinateurs du groupe de travail à l'aide de la méthode spécifiée dans [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual).  

 Conditions préalables :  

-   Le client doit être installé manuellement sur chaque ordinateur du groupe de travail. Durant l’installation, l’utilisateur connecté doit disposer des droits d’administrateur local.  

-   Pour accéder aux ressources du domaine du serveur de site Configuration Manager, le compte d’accès réseau doit être configuré pour le site. Spécifiez ce compte comme une propriété du composant de distribution de logiciels. Pour plus d'informations, voir [Site components for System Center Configuration Manager](../../../core/servers/deploy/configure/site-components.md).  

 Limitations :  

-   Les clients du groupe de travail ne peuvent pas localiser les points de gestion depuis les services de domaine Active Directory et doivent à la place utiliser DNS, WINS ou un autre point de gestion.  

-   L'itinérance globale n'est pas prise en charge parce que les clients ne peuvent pas demander d'information de site aux services de domaine Active Directory.  

-   Les méthodes de découverte d'Active Directory ne découvriront pas les ordinateurs dans des groupes de travail.  

-   Vous ne pouvez pas déployer de logiciels vers les utilisateurs d'ordinateurs de groupe de travail.  

-   Vous ne pouvez pas utiliser la méthode d'installation poussée du client pour installer le client sur des ordinateurs du groupe de travail.  

-   Les clients du groupe de travail ne peuvent pas utiliser Kerberos pour l’authentification et peuvent donc nécessiter une approbation manuelle.  

-   Un client de groupe de travail ne peut pas être configuré comme point de distribution. Configuration Manager impose que les ordinateurs faisant office de points de distribution soient membres d’un domaine.  

### <a name="install-the-client-on-workgroup-computers"></a>Installer le client sur les ordinateurs d’un groupe de travail  

Vérifiez les prérequis, puis suivez les instructions de la section [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual).  

   Dans cet exemple, le client est installé pour être géré sur l'intranet, tandis que le code de site et le suffixe DNS sont spécifiés pour localiser un point de gestion. `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     

   Dans cet exemple, le client doit se trouver à un emplacement réseau configuré dans un groupe de limites. Cette exigence vise à ce que l’attribution automatique de site réussisse. La commande inclut un point d’état de secours sur le serveur FSPSERVER. Cette propriété facilite le suivi du déploiement du client et permet d’identifier les éventuels problèmes de communication du client. 
   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Comment installer les clients pour assurer leur gestion sur Internet  
 
> [!Note]
> Cette section ne s’applique pas aux clients utilisant une [passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Pour installer des clients basés sur Internet en utilisant une passerelle de gestion cloud, consultez [Installer et affecter des clients Windows 10 Configuration Manager à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

Si le site Configuration Manager prend en charge la [gestion des clients basée sur Internet](/sccm/core/clients/manage/plan-internet-based-client-management) pour des clients pouvant être sur l’intranet ou sur Internet, deux options s’offrent à vous au moment d’installer les clients sur l’intranet :  

-   Vous pouvez inclure la propriété Client.msi de CCMHOSTNAME=*&lt;nom de domaine complet Internet du point de gestion Internet\>* quand vous installez le client, par exemple avec la méthode d’installation manuelle ou Push du client. Lorsque vous utilisez cette méthode, vous devez également attribuer directement le client au site et vous ne pouvez pas utiliser l'attribution de site automatique. La section [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual) de cette rubrique fournit un exemple de cette méthode de configuration.  

-   Vous pouvez installer le client dans l’optique d’une gestion des clients sur intranet, puis attribuer au client un point de gestion des clients basé sur Internet. Modifiez le point de gestion via les propriétés du client Configuration Manager dans le panneau de configuration ou à l’aide d’un script. Lorsque vous utilisez cette méthode, vous pouvez utiliser l'attribution automatique des clients. Pour plus d’informations, consultez la section [Comment configurer les clients en vue de les gérer via Internet après leur installation](#BKMK_ConfigureIBCM_MP) de cette rubrique.  

 Si vous devez installer des clients qui se trouvent sur Internet, choisissez l’une des méthodes prises en charge suivantes :  

-   Prévoyez un mécanisme permettant à ces clients de se connecter temporairement à l’intranet via un réseau privé virtuel (VPN). Installez ensuite le client en employant une méthode d’installation du client appropriée.  

-   Utilisez une méthode d’installation indépendante de Configuration Manager. Par exemple, empaquetez les fichiers sources d’installation du client sur un média amovible que vous pouvez envoyer aux utilisateurs avec des instructions d’installation. Les fichiers sources d’installation du client se trouvent dans le dossier *&lt;chemin_installation\>* \Client sur le serveur de site et les points de gestion Configuration Manager. Incorporez au support un script à copier manuellement vers le dossier du client et depuis ce dossier, installez le client à l'aide de CCMSetup.exe et de toutes les propriétés de ligne commande CCMSetup appropriées.  

> [!NOTE]  
>  Configuration Manager ne prend pas en charge l’installation directe d’un client à partir du point de gestion Internet ou du point de mise à jour logicielle Internet.  

 Les clients gérés via internet doivent communiquer avec des systèmes de site basés sur Internet. Vérifiez que ces clients possèdent aussi des certificats d’infrastructure à clé publique (PKI) avant d’installer le client. Installez ces certificats indépendamment de Configuration Manager. Pour plus d’informations sur la configuration requise des certificats, consultez [Configuration requise des certificats PKI](../../../core/plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Installer des clients sur Internet en spécifiant des propriétés de ligne de commande CCMSetup  

1.  Suivez les instructions de la section [Comment installer les clients Configuration Manager manuellement](#BKMK_Manual) et incluez toujours les éléments suivants :  

    -   Propriété de ligne de commande CCMSetup **/source:***&lt;chemin local du dossier Client copié\>*  

    -   Propriété de ligne de commande CCMSetup **/UsePKICert:**  

    -   Propriété Client.msi **CCMHOSTNAME=***&lt;nom de domaine complet du point de gestion Internet\>*  

    -   Propriété Client.msi **SMSSIGNCERT=***&lt;chemin local du certificat de signature du serveur de site exporté\>*  

    -   Propriété Client.msi **SMSSITECODE=***&lt;code de site du point de gestion Internet\>*  

    > [!NOTE]  
    >  Si le site comporte plusieurs points de gestion Internet, le choix du point de gestion Internet importe peu pour la propriété CCMHOSTNAME. Quand un client Configuration Manager se connecte au point de gestion Internet spécifié, le point de gestion envoie au client une liste des points de gestion Internet disponibles sur le site. Le client en sélectionne un de façon aléatoire dans la liste.  

2.  Si vous ne souhaitez pas que le client vérifie la liste de révocation de certificats (CRL), spécifiez la propriété de ligne de commande CCMSetup **/NoCRLCheck**.  

3.  Si vous utilisez un point d’état de secours Internet, spécifiez la propriété Client.msi **FSP=***&lt;nom de domaine complet Internet du point d’état de secours Internet\>*.  

4.  Si vous installez le client pour la gestion des clients Internet uniquement, spécifiez la propriété Client.msi **CCMALWAYSINF=1**.  

5.  Vérifiez si vous devez spécifier des propriétés de ligne de commande CCMSetup supplémentaires. Par exemple, vous pouvez avoir besoin de spécifier un critère de sélection de certificat si le client possède plusieurs certificats d’infrastructure à clé publique (PKI) valides. Pour obtenir la liste des propriétés d’installation disponibles, consultez [À propos des propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md).  

   Exemple :  
   `CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

   Cet exemple installe le client avec les comportements suivants :
   - Utilisation des fichiers sources à partir d’un dossier situé sur le lecteur D
   - Utilisation d’un certificat PKI du client 
   - Sélection du certificat présentant la plus longue période de validité 
   - Gestion des clients Internet uniquement
   - Attribuer au client l’utilisation du point de gestion Internet nommé SERVER1
   - Attribuer le point d’état de secours Internet dans le domaine contoso.com
   - Attribuer le client au site ABC  

###  <a name="BKMK_ConfigureIBCM_MP"></a>Pour configurer les clients en vue d’une gestion sur Internet après leur installation  
 Pour attribuer le point de gestion Internet après avoir installé le client, utilisez l’une de ces procédures. La première procédure reposant sur une configuration manuelle, elle est adaptée à un nombre de clients limité. En revanche, si vous avez un grand nombre de clients à configurer, la deuxième procédure est plus appropriée.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-assigning-the-internet-based-management-point-in-configuration-manager-properties"></a>Configurer les clients en vue d’une gestion via Internet après leur installation en leur attribuant le point de gestion Internet dans les propriétés de Configuration Manager  

1.  Accédez à **Configuration Manager** dans le Panneau de configuration de l'ordinateur client, puis double-cliquez dessus pour ouvrir ses propriétés.  

2.  Sous l’onglet **Internet**, entrez le nom de domaine complet du point de gestion Internet dans la zone de texte FQDN Internet.  

    > [!NOTE]  
    >  L'onglet **Internet** est disponible uniquement si le client dispose d'un certificat PKI client.  

3.  Si le client accède à Internet via un serveur proxy, entrez les paramètres de ce dernier.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurer les clients en vue d’une gestion via Internet après leur installation au moyen d’un script  

1.  Ouvrez un éditeur de texte, tel que le Bloc-notes.  

2.  Copiez l’exemple VBScript suivant et insérez-le dans le fichier. Remplacez *mp.contoso.com* par le nom de domaine complet Internet de votre point de gestion Internet.  

    ```  
    on error resume next  

    ' Create variables.  
    Dim newInternetBasedManagementPointFQDN  
    Dim client  

    newInternetBasedManagementPointFQDN = "mp.contoso.com"  

    ' Create the client COM object.  
    Set client = CreateObject ("Microsoft.SMS.Client")  

    ' Set the internet-based management point FQDN by calling the SetCurrentManagementPoint method.  
    client.SetInternetManagementPointFQDN newInternetBasedManagementPointFQDN  

    ' Clear variables.  
    Set client = Nothing  
    Set internetBasedManagementPointFQDN = Nothing  

    ```  

    > [!NOTE]  
    >  Si vous devez supprimer un point de gestion Internet spécifié pour éviter que le client utilise un point de gestion Internet, supprimez la valeur entre guillemets de sorte que cette ligne se présente ainsi : `newInternetBasedManagementPointFQDN = ""`  

4.  Enregistrez le fichier avec une extension .vbs.  

5.  Utilisez cscript.exe pour exécuter le script sur les ordinateurs clients en employant l’une des méthodes suivantes :  

    -   Déployez le fichier sur les clients Configuration Manager existants en utilisant un package et un programme.  

    -   Exécutez le fichier localement sur les clients Configuration Manager existants en double-cliquant sur le fichier de script dans l'Explorateur Windows.  

 Vous devrez peut-être redémarrer le client pour que les modifications prennent effet.  



##  <a name="BKMK_Provision"></a> Guide pratique pour fournir les propriétés d’installation du client (installation basée sur une stratégie de groupe et sur les mises à jour logicielles)  
 Vous pouvez utiliser la stratégie de groupe Windows pour fournir les propriétés d’installation du client Configuration Manager aux ordinateurs. Ces propriétés sont stockées dans le Registre de l’ordinateur et lues quand le logiciel client est installé. Cette procédure n’est généralement pas obligatoire, mais peut s’avérer nécessaire dans certains scénarios d’installation du client, par exemple :  

-   Vous utilisez les paramètres de stratégie de groupe ou des méthodes d’installation du logiciel basée sur des mises à jour logicielles. Vous n’avez pas étendu le schéma Active Directory pour Configuration Manager.  

-   Vous souhaitez redéfinir les propriétés de l'installation du client sur certains ordinateurs.  

> [!NOTE]  
>  Si des propriétés d’installation sont fournies sur la ligne de commande CCMSetup.exe, les propriétés d’installation fournies aux ordinateurs ne sont pas utilisées.  

 Le modèle d’administration de stratégie de groupe nommé ConfigMgrInstallation.adm est fourni sur le média d’installation de Configuration Manager. Ce modèle permet de fournir les propriétés d’installation aux ordinateurs clients.   

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurer et attribuer des propriétés d’installation du client à l’aide d’un objet de stratégie de groupe  

1.  Importez le modèle d’administration ConfigMgrInstallation.adm dans un objet de stratégie de groupe nouveau ou existant, à l’aide d’un éditeur tel que l’Éditeur d'objets de stratégie de groupe Windows. Le fichier se trouve dans le dossier **TOOLS\ConfigMgrADMTemplates** du média d’installation de Configuration Manager.  

2.  Affichez les propriétés du paramètre importé **Configurer les paramètres de déploiement du client**.  

3.  Choisissez **Activé**.  

4.  Dans la zone **CCMSetup** , entrez les propriétés de ligne de commande CCMSetup requises. Pour obtenir la liste de toutes les propriétés de ligne de commande CCMSetup et des exemples montrant comment les utiliser, consultez [À propos des propriétés d’installation du client](../../../core/clients/deploy/about-client-installation-properties.md).  

5.  Attribuez l’objet stratégie de groupe aux ordinateurs auxquels vous souhaitez fournir les propriétés d’installation du client Configuration Manager.  

Pour plus d’informations sur la stratégie de groupe Windows, consultez la documentation Windows Server.  



## <a name="next-steps"></a>Étapes suivantes
Pour obtenir de l’aide sur l’installation du client Configuration Manager, consultez [Méthodes d’installation du client](../../../core/clients/deploy/plan/client-installation-methods.md).