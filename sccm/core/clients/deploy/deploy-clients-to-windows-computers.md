---
title: Déployer des clients sur Windows
titleSuffix: Configuration Manager
description: Apprenez à déployer le client Configuration Manager sur des ordinateurs Windows.
ms.date: 04/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0f560c5bf4ca9a3b58652bc3c53b83d8cf0479cf
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551038"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Guide pratique pour déployer des clients sur des ordinateurs Windows dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations détaillées sur la façon de déployer le client Configuration Manager sur des ordinateurs Windows. Pour plus d’informations sur la planification et la préparation du déploiement des clients, consultez ces articles :
- [Méthodes d’installation du client](/sccm/core/clients/deploy/plan/client-installation-methods)  
- [Prérequis au déploiement de clients sur des ordinateurs Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers)   
- [Sécurité et confidentialité pour les clients Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  
- [Bonnes pratiques de déploiement du client](/sccm/core/clients/deploy/plan/best-practices-for-client-deployment)  



##  <a name="BKMK_ClientPush"></a> Installation Push du client

Il existe trois façons principales d’utiliser l’installation Push du client :  

- Quand vous configurez l’installation Push du client pour un site, l’installation du client s’exécute automatiquement sur les ordinateurs découverts par le site. L’étendue de cette méthode est définie par les limites configurées du site quand celles-ci sont configurées comme un groupe de limites.  

- Démarrez une installation Push du client en exécutant l’Assistant Installation Push du client pour un regroupement ou une ressource spécifique dans un regroupement.  

- Utilisez l’Assistant Installation Push du client pour installer le client Gestionnaire de configuration, qui permet d’[interroger](/sccm/core/servers/manage/introduction-to-queries) le résultat. L’installation est réussie seulement si un des éléments retournés par la requête est l’attribut **ResourceID** de la classe **Ressource système**.

Si le serveur de site ne parvient pas à contacter l’ordinateur client ou à démarrer le processus d’installation, il tente à nouveau l’installation de façon automatique toutes les heures. Le serveur renouvelle les tentatives pendant sept jours, au maximum.  

Pour vous aider à suivre le processus d’installation du client, installez un point d’état de secours avant d’installer les clients. Quand vous installez un point d’état de secours, il est automatiquement attribué aux clients quand ces derniers sont installés selon la méthode d’installation Push du client. Pour suivre la progression d’installation du client, consultez les rapports de déploiement et d’attribution du client.

Les fichiers journaux du client fournissent des informations plus détaillées pour le dépannage. Les fichiers journaux ne nécessitent pas de point d’état de secours. Par exemple, le fichier CCM.log du serveur de site enregistre tous les problèmes qui surviennent lorsque le serveur de site se connecte à l’ordinateur. Le fichier CCMSetup.log du client enregistre le processus d’installation.  

> [!IMPORTANT]  
>  Le Push du client ne réussit que si toutes les conditions préalables sont remplies. Pour plus d'informations, consultez [Dépendances liées aux méthodes d’installation](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers#installation-method-dependencies).


### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Configurer le site en vue de l’utilisation automatique de l’installation Push du client pour les ordinateurs découverts

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation poussée du client automatique à l’échelle du site.  

3.  Sous l’onglet **Accueil** du ruban, dans le groupe **Paramètres**, sélectionnez **Paramètres d’installation du client**, puis sélectionnez **Installation Push du client**.  

4.  Sous l’onglet **Général** de la fenêtre Propriétés de l’installation push du client, sélectionnez **Activer l’installation Push du client automatique à l’échelle du site**.

5. À compter de la version 1806, quand vous mettez à jour le site, une vérification Kerberos pour le Push du client est activée. L’option permettant d’**Autoriser le recours à NTLM en secours pour la connexion** est activée par défaut, ce qui est cohérent avec le comportement précédent. Si le site ne peut pas authentifier le client à l’aide de Kerberos, il retente la connexion à l’aide de NTLM. La configuration recommandée pour améliorer la sécurité consiste à désactiver ce paramètre, qui exige Kerberos sans bascule de secours sur NTLM.<!--1358204-->  

    > [!NOTE]  
    > Quand elle utilise le Push du client pour installer le client Configuration Manager, le serveur de site crée une connexion à distance au client. À compter de la version 1806, le site peut exiger l’authentification mutuelle Kerberos en interdisant le recours à NTLM en secours avant d’établir la connexion. Cette amélioration permet de sécuriser la communication entre le serveur et le client.  
    > 
    > En fonction de vos stratégies de sécurité, il est possible que votre environnement préfère ou demande déjà l’authentification Kerberos plutôt qu’une authentification NTLM plus ancienne. Pour plus d’informations sur les considérations de sécurité de ces protocoles d’authentification, lisez la rubrique [Paramètre de stratégie de sécurité Windows pour restreindre l’authentification NTLM](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    > 
    > Pour pouvoir utiliser cette fonctionnalité, il faut que les clients se trouvent dans une forêt Active Directory approuvée. Dans Windows, Kerberos s’appuie sur Active Directory pour l’authentification mutuelle.  

6.  Sélectionnez les types de systèmes vers lesquels Configuration Manager doit transférer (push) le logiciel client. Indiquez si vous souhaitez installer le client sur les contrôleurs de domaine.  

7.  Sous l’onglet **Comptes**, spécifiez le ou les comptes que Configuration Manager doit utiliser au moment de se connecter à l’ordinateur cible. Sélectionnez l’icône **Créer**, entrez le **Nom d’utilisateur** et le **Mot de passe** (pas plus de 38 caractères), confirmez le mot de passe, puis sélectionnez **OK**. Spécifiez au moins un compte d’installation Push du client. Ce compte doit disposer de droits d’administrateur local sur l’ordinateur cible pour pouvoir installer le client. Si vous ne spécifiez pas de compte d’installation Push du client, Configuration Manager essaie d’utiliser le compte d’ordinateur du système de site. L’utilisation du compte d’ordinateur système fait échouer l’installation Push du client sur plusieurs domaines.  

    > [!NOTE]  
    >  Pour utiliser l’installation Push du client sur un site secondaire, spécifiez le compte du site secondaire qui lance l’installation Push du client.  
    >   
    >  Pour plus d’informations sur le compte d’installation Push du client, consultez la procédure suivante, [Utiliser l’Assistant Installation Push du client](#use-the-client-push-installation-wizard).  

8.  Spécifiez les propriétés d’installation requises sur l’onglet **Propriétés d’Installation**.

     Si vous avez étendu le schéma Active Directory pour Configuration Manager, le site publie les [propriétés d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties) spécifiées dans Active Directory Domain Services. Quand CCMSetup s’exécute sans propriétés d’installation, il lit ces propriétés à partir d’Active Directory.  

    > [!NOTE]  
    >  Si vous activez l’installation Push du client sur un site secondaire, définissez la propriété **SMSSITECODE** sur le code de site Configuration Manager de son site principal parent. Si vous avez étendu le schéma Active Directory pour Configuration Manager, pour rechercher automatiquement l’attribution de site correcte, définissez cette propriété sur **AUTO**.


### <a name="use-the-client-push-installation-wizard"></a>Utiliser l’Assistant Installation Push du client

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation poussée du client automatique à l’échelle du site.  

3.  Sous l’onglet **Accueil** du ruban, dans le groupe **Paramètres**, sélectionnez **Paramètres d’installation du client**, puis sélectionnez **Installation Push du client**.  

4.  Spécifiez les propriétés d’installation requises sur l’onglet **Propriétés d’Installation**.  

    Si vous avez étendu le schéma Active Directory pour Configuration Manager, le site publie les [propriétés d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties) spécifiées dans Active Directory Domain Services. Quand CCMSetup s’exécute sans propriétés d’installation, il lit ces propriétés à partir d’Active Directory.

5.  Dans la console de Configuration Manager, accédez à l’espace de travail **Actifs et conformité**.  

6.  Dans le nœud **Appareils**, sélectionnez un ou plusieurs ordinateurs. Ou sélectionnez un regroupement d’ordinateurs dans le nœud **Regroupements d’appareils**.  

7.  Sous l’onglet **Accueil** du ruban, choisissez une de ces options :  

    -   Pour envoyer (push) le client à un ou plusieurs appareils, dans le groupe **Appareil**, sélectionnez **Installer le client**.  

    -   Pour envoyer (push) le client à un regroupement d’appareils, dans le groupe **Regroupement**, sélectionnez **Installer le client**.  

8. Dans la page **Avant de commencer** de l’Assistant Installation du client Gestionnaire de configuration, consultez les informations, puis sélectionnez **Suivant**.  

9. Sélectionnez les options appropriées sur la page **Options d’Installation**.  

10. Passez en revue les paramètres d’installation, puis effectuez toutes les étapes de l’Assistant.  

> [!NOTE]  
> Utilisez cet Assistant pour installer des clients même si le site n’est pas configuré pour l’installation Push du client.  

##  <a name="BKMK_ClientSUP"></a> Installation basée sur une mise à jour logicielle  

L’installation du client en fonction des mises à jour logicielles publie le client sur un point de mise à jour logicielle, sous forme de mise à jour logicielle. Utilisez cette méthode pour une première installation ou une mise à niveau.  

Si le client Gestionnaire de configuration est installé sur un ordinateur, celui-ci reçoit la stratégie du client du site. Cette stratégie inclut le nom du serveur du point de mise à jour de logiciel et le port à partir duquel les mises à jour de logiciel sont obtenues.

> [!IMPORTANT]  
>  Pour effectuer une installation basée sur des mises à jour logicielles, utilisez le même serveur Windows Server Update Services (WSUS) pour l’installation du client et les mises à jour logicielles. Ce serveur doit être utilisé comme le point de mise à jour logicielle actif dans un site principal. Pour plus d’informations, consultez [Installer un point de mise à jour logicielle](/sccm/sum/get-started/install-a-software-update-point).

Si le client Gestionnaire de configuration n’est pas installé sur l’ordinateur, configurez et attribuez un objet de stratégie de groupe. Cette stratégie de groupe spécifie le nom de serveur du point de mise à jour logicielle.  

Il est impossible d’ajouter des propriétés de ligne de commande à une installation du client basée sur des mises à jour logicielles. Si vous avez étendu le schéma Active Directory pour Configuration Manager, l’installation du client interroge automatiquement Active Directory Domain Services pour connaître les propriétés d’installation.  

Si vous n’avez pas étendu le schéma Active Directory, utilisez la stratégie de groupe pour configurer les paramètres d’installation du client. Ces paramètres s’appliquent automatiquement à toute installation du client basée sur les mises à jour logicielles. Pour plus d’informations, consultez la section [Guide pratique pour provisionner les propriétés d’installation du client](#BKMK_Provision) et l’article [Guide pratique pour attribuer des clients à un site](/sccm/core/clients/deploy/assign-clients-to-a-site).  

Utilisez les procédures suivantes pour configurer des ordinateurs sans client Configuration Manager pour utiliser le point de mise à jour logicielle. Il existe également une procédure pour publier le logiciel client sur le point de mise à jour logicielle.  

> [!TIP]  
>  Si les ordinateurs sont dans un état de redémarrage en attente suite à une précédente installation du logiciel, une installation du client en fonction des mises à jour logicielles peut entraîner le redémarrage de l’ordinateur.  


### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Configurer un objet de stratégie de groupe pour spécifier le point de mise à jour logicielle  

1.  Utilisez la **Console de gestion des stratégies de groupe** pour ouvrir un objet de stratégie de groupe nouveau ou existant.  

2.  Développez **Configuration ordinateur**, **Modèles d’administration**, **Composants Windows**, puis sélectionnez **Windows Update**.  

3.  Ouvrez les propriétés du paramètre **Spécifier l’emplacement intranet du service de mise à jour Microsoft**, puis sélectionnez **Activé**.  

4.  **Configurer le service intranet de mise à jour pour la détection des mises à jour** : Spécifiez le nom et le port du serveur de point de mise à jour de logiciels.  

    -   Si vous avez configuré le système de site Configuration Manager pour utiliser un nom de domaine complet (FQDN), utilisez ce format.  

    -   Si le système de site Configuration Manager n’est pas configuré pour utiliser un nom de domaine complet (FQDN), utilisez un format de nom court.

    > [!TIP]  
    >  Pour déterminer le numéro de port, consultez [Comment déterminer les paramètres de port utilisés par WSUS](/sccm/sum/plan-design/plan-for-software-updates).  

     Exemple au format FQDN : `http://server1.contoso.com:8530`  

5.  **Configurer le serveur intranet de statistiques** : Ce paramètre est généralement configuré avec le même nom de serveur.

6.  Attribuez l’objet de stratégie de groupe aux ordinateurs sur lesquels vous souhaitez installer le client et recevoir les mises à jour logicielles.  


### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Publier le client Configuration Manager sur le point de mise à jour logicielle  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2.  Sélectionnez le site pour lequel vous souhaitez configurer l’installation du client en fonction des mises à jour logicielles.  

3.  Sous l’onglet **Accueil** du ruban, dans le groupe **Paramètres**, sélectionnez **Paramètres d’installation du client**, puis **Installation du client en fonction des mises à jour de logiciel**.  

4.  Sélectionnez **Activer l’installation du client basée sur les mises à jour logicielles**.  

5.  Si la version du client du site est plus récente que la version du point de mise à jour logicielle, la boîte de dialogue **Version plus récente du package client détectée** s’ouvre. Sélectionnez **Oui** pour publier la version la plus récente.  

    > [!NOTE]  
    >  Si vous n’avez pas déjà publié le logiciel client sur le point de mise à jour logicielle, cette boîte de dialogue est vide.

La mise à jour logicielle du client Configuration Manager n’est pas mise à jour automatiquement quand il existe une nouvelle version. Quand vous mettez à jour le site, répétez cette procédure pour mettre à jour le client.  

##  <a name="BKMK_ClientGP"></a> Installation de la stratégie de groupe

Utilisez la stratégie de groupe dans Active Directory Domain Services pour publier ou attribuer le client Gestionnaire de configuration. Le client s’installe au démarrage de l’ordinateur. Lorsque vous utilisez la stratégie de groupe, le client s’affiche dans **Ajouter ou supprimer des programmes** dans le panneau de configuration. L’utilisateur peut l’installer à partir de là.  

Utilisez le package Windows Installer CCMSetup.msi pour les installations en fonction de la stratégie de groupe. Ce fichier se trouve dans le dossier `<ConfigMgr installation directory>\bin\i386` sur le serveur de site. Vous ne pouvez pas ajouter de propriétés à ce fichier pour modifier le comportement à l’installation.  

> [!IMPORTANT]  
>  Vous devez disposer d’autorisations d’administrateur pour accéder aux fichiers d’installation du client.  

-   Si vous avez étendu le schéma Active Directory pour Configuration Manager et que vous avez sélectionné **Publier ce site dans Active Directory Domain Services** sous l’onglet **Avancé** de la boîte de dialogue **Propriétés du site**, les ordinateurs clients recherchent automatiquement les propriétés d’installation dans Active Directory Domain Services. Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  

-   Si vous n’avez pas étendu le schéma Active Directory, consultez la section sur [configuration des propriétés d’installation du client](#BKMK_Provision) pour obtenir des informations sur le stockage des propriétés d’installation dans le registre Windows des ordinateurs. Le client utilise ces propriétés d’installation lors de l’installation.  

Pour plus d’informations, consultez [Comment utiliser la Stratégie de groupe pour installer à distance le logiciel](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

##  <a name="BKMK_Manual"></a> Installation manuelle

Installez manuellement le logiciel client sur des ordinateurs à l’aide de CCMSetup.exe. Vous pouvez rechercher ce programme et ses fichiers de support dans le dossier Client du dossier d’installation de Configuration Manager sur le serveur de site. Le site partage ce dossier sur le réseau de la façon suivante :  

 `\\<site server name>\SMS_<site code>\Client\`  

 `<site server name>` est le nom du serveur de site principal. `<site code>` est le code de site principal auquel le client est attribué. Pour exécuter CCMSetup.exe à partir de la ligne de commande sur le client, connectez-vous à cet emplacement réseau, puis exécutez la commande.  

> [!IMPORTANT]  
>  Vous devez disposer d’autorisations d’administrateur pour accéder aux fichiers d’installation du client.  

Le programme CCMSetup.exe copie toutes les conditions préalables nécessaires sur l’ordinateur client, puis fait appel au package Windows Installer (Client.msi) pour installer le client. Vous ne pouvez pas exécuter Client.msi directement.  

Pour modifier le comportement de l’installation du client, spécifiez des options de ligne de commande pour CCMSetup.exe et Client.msi. Vérifiez que vous spécifiez les paramètres de CCMSetup commençant par `/` avant de spécifier les propriétés de Client.msi. Par exemple :  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

Dans cet exemple, le client s’installe en utilisant les options suivantes :  

|Option|Description|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Ce paramètre de CCMSetup spécifie le point de gestion SMSMP01 pour télécharger les fichiers d’installation du client nécessaires.|  
|`/logon`|Ce paramètre de CCMSetup spécifie que l’installation doit s’arrêter si un client Configuration Manager existant est détecté sur l’ordinateur.|  
|`SMSSITECODE=AUTO`|Cette propriété de Client.msi spécifie que le client doit essayer de trouver le code de site Configuration Manager à utiliser, par exemple, à l’aide de Active Directory Domain Services, par exemple.|  
|`FSP=SMSFP01`|Cette propriété de Client.msi précise que le point d’état de secours nommé SMSFP01 est utilisé pour recevoir les messages d’état envoyés par l’ordinateur client.|  

 Pour plus d’informations, consultez [À propos des propriétés et des paramètres d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).  

> [!TIP]  
> Pour plus d’informations sur la procédure d’installation du client Gestionnaire de configuration sur un appareil Windows 10 moderne en utilisant l’identité Azure Active Directory (Azure AD), consultez [Installer et attribuer des clients Gestionnaire de configuration Windows 10 à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Cette procédure concerne les clients sur intranet ou Internet.  


### <a name="manual-installation-examples"></a>Exemples d’installation manuelle

Ces exemples concernent les clients joints à Active Directory sur l’intranet. Ils utilisent les valeurs suivantes :  

- **MPSERVER** : serveur hébergeant le point de gestion   
- **FSPSERVER** : serveur hébergeant le point d’état de secours  
- **ABC** : code de site  
- **contoso.com** : nom de domaine  

Supposons que vous configurez tous les serveurs de système de site avec un nom de domaine complet intranet et que vous publiez les informations sur le site sur Active Directory.  

Démarrez par les étapes suivantes sur l’ordinateur client :  
1. Connectez-vous en tant qu’administrateur local.  
2. Mappez le lecteur Z sur `\\MPSERVER\SMS_ABC\Client`.  
3. Commutez l’invite de commandes sur le lecteur Z.  

Exécutez ensuite l’une des commandes suivantes :  


#### <a name="manual-example-1"></a>Exemple d’installation manuelle 1  

`CCMSetup.exe`  

Cette commande installe le client sans paramètre ni propriété supplémentaire. Le client est configuré automatiquement par rapport aux propriétés d’installation du client publiées dans Active Directory Domain Services, y compris ces paramètres :  

- Code du site : Ce paramètre exige que l’emplacement réseau du client soit inclus dans un groupe de limites que vous avez configuré pour l’attribution du client.  
- Point de gestion.
- Point d’état de secours.
- Communiquez à l’aide de HTTPS uniquement.  

Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory](/sccm/core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services).  


#### <a name="manual-example-2"></a>Exemple d’installation manuelle 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Cette commande écrase la configuration automatique fournie par Active Directory Domain Services. Elle n’exige pas que l’emplacement réseau du client soit inclus dans un groupe de limites configuré pour l’attribution du client. En revanche, l’installation spécifie les paramètres suivants :
- Code de site.
- Point de gestion intranet.
- Point de gestion Internet.
- Point d’état de secours qui accepte les connexions en provenance d’Internet.
- Utilisez un certificat client d’infrastructure à clé publique (PKI) (si disponible) qui offre la plus longue période de validité.  

##  <a name="BKMK_ClientLogonScript"></a> Installation via un script d’ouverture de session

Configuration Manager prend en charge les scripts d’ouverture de session pour installer le logiciel client Gestionnaire de configuration. Utilisez le fichier programme CCMSetup.exe dans un script d’ouverture de session pour déclencher l’installation du client.  

L'installation via un script d'ouverture de session utilise les mêmes méthodes que l'installation manuelle du client. Spécifiez le paramètre d’installation `/logon` pour CCMSsetup.exe. S’il existe déjà une version du client sur l’ordinateur, ce paramètre empêche l’installation du client. Ce comportement empêche la réinstallation du client à chaque exécution du script d’ouverture de session.  

Si vous ne spécifiez aucune source d’installation en utilisant le paramètre `/Source` et qu’aucun point de gestion à partir duquel obtenir l’installation n’est spécifié par le paramètre `/MP`, CCMSetup.exe recherche le point de gestion dans Active Directory Domain Services. Ce comportement se produit uniquement si vous avez étendu le schéma pour Configuration Manager et que vous avez publié le site dans Active Directory Domain Services. Alternativement, le client peut utiliser le service de nom de domaine (DNS) ou WINS pour rechercher un point de gestion.  



##  <a name="BKMK_ClientApp"></a> Installation de package et de programme  

Utilisez Configuration Manager pour créer et déployer un package et un programme qui mettent à niveau le logiciel client sur des appareils sélectionnés. Configuration Manager fournit un fichier de définition de package pour renseigner les propriétés du package avec les valeurs généralement utilisées. Personnalisez le comportement de l’installation du client en spécifiant des paramètres et des propriétés de ligne de commande supplémentaires.  

> [!NOTE]  
>  Vous ne pouvez pas mettre à niveau des clients Gestionnaire de configuration 2007 avec cette méthode. Au lieu de cela, utilisez la mise à niveau automatique des clients, qui crée et déploie automatiquement un package contenant la dernière version du client. Pour plus d’informations, consultez [Mettre à niveau les clients](/sccm/core/clients/manage/upgrade/upgrade-clients).  
>   
>  Pour plus d’informations sur la migration à partir de versions plus anciennes du client Configuration Manager, consultez [Planification d’une stratégie de migration de clients](/sccm/core/migration/planning-a-client-migration-strategy).  

 
### <a name="create-a-package-and-program-for-the-client-software"></a>Créer un package et un programme pour le logiciel client  

Pour créer un package et un programme Configuration Manager que vous pouvez déployer sur les ordinateurs clients Configuration Manager afin de mettre à niveau le logiciel client, utilisez la procédure suivante.  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications**, puis sélectionnez le nœud **Packages**.  

2.  Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, sélectionnez **Créer un package à partir d’une définition**.  

3.  Dans la page **Définition du package** de l’Assistant, sélectionnez **Microsoft** dans la liste **Éditeur** et **Mise à niveau du client Gestionnaire de configuration** dans la liste **Définition du package**.  

4.  Dans la page **Fichiers sources**, sélectionnez **Toujours obtenir les fichiers depuis le dossier source**.  

5.  Dans la page **Dossier source**, sélectionnez **Chemin d’accès réseau (nom UNC)** . Entrez ensuite le chemin d’accès réseau du serveur et le partage contenant les fichiers d’installation du client.  

    > [!NOTE]  
    >  L’ordinateur sur lequel le déploiement de Configuration Manager est effectué doit avoir accès au dossier réseau spécifié. Sinon, l’installation du client échoue.  

    Pour changer l’une des propriétés d’installation du client, modifiez la ligne de commande de CCMSetup.exe sous l’onglet **Général** de la boîte de dialogue du programme **Propriétés de la mise à niveau silencieuse de l’Agent Configuration Manager**. L’emplacement d’installation par défaut est `/noservice SMSSITECODE=AUTO`.  

6. Distribuez le package à tous les points de distribution qui doivent héberger le package de mise à niveau des clients. Déployez ensuite le package sur des regroupements d’appareils contenant les clients à mettre à niveau.  



## <a name="bkmk_mdm"></a> Appareils Windows gérés par Intune MDM

Déployez le client Configuration Manager sur les appareils qui sont inscrits auprès de Microsoft Intune.

Cette procédure s’applique aux clients traditionnels connectés à l’intranet. Elle utilise des méthodes d’authentification de client classiques. Pour que l’appareil reste dans un état géré après avoir installé le logiciel client, il doit se trouver sur l’intranet et dans une limite de site Configuration Manager.  

Pour plus d’informations sur la procédure d’installation du client Gestionnaire de configuration sur un appareil Windows 10 moderne en utilisant l’identité Azure AD, consultez [Installer et attribuer des clients Gestionnaire de configuration Windows 10 à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

> [!NOTE]  
> Par défaut, dans certaines versions de Configuration Manager, l’appareil est désinscrit d’Intune une fois le logiciel client installé.
> 
> À compter de la version 1710, les clients ne se désinscrivent pas d’Intune. Ils peuvent utiliser à la fois le client Gestionnaire de configuration et l’inscription Gestion des données de référence. Pour plus d’informations, consultez [Vue d’ensemble de la cogestion](/sccm/comanage/overview).  


###  <a name="install-clients-by-using-intune"></a>Installer les clients via Intune  

1. Dans Intune, [ajoutez une application métier Windows](https://docs.microsoft.com/intune/lob-apps-windows) contenant le fichier d’installation du client Gestionnaire de configuration CCMSetup.msi. Vous pouvez trouver ce fichier dans le dossier suivant sur le serveur de site : `<ConfigMgr installation directory>\bin\i386`.  

2. Dans l’Éditeur de logiciel Intune, entrez des paramètres de ligne de commande. Par exemple, utilisez cette commande avec un client classique sur l’intranet :  

   `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

   > [!NOTE]  
   > Pour obtenir un exemple de commande à utiliser avec un client Windows 10 moderne exploitant l’authentification Azure AD, consultez [Comment préparer des appareils sur Internet à la cogestion](/sccm/comanage/how-to-prepare-win10#install-the-configuration-manager-client).  

3. [Attribuez l’application](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune) à un groupe des ordinateurs Windows inscrits.  



##  <a name="BKMK_ClientImage"></a> Installation d’une image de système d’exploitation

Préinstallez le client Configuration Manager sur un ordinateur de référence que vous utilisez pour créer une image de système d’exploitation.

> [!IMPORTANT]  
> Quand vous utilisez la séquence de tâches Configuration Manager pour déployer une image du système d’exploitation, l’étape [Préparer le client ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture) supprime entièrement le client Gestionnaire de configuration.  


### <a name="prepare-the-client-computer-for-imaging"></a>Préparer l’ordinateur client à la mise en image  

1.  Installez manuellement le logiciel client Configuration Manager sur l’ordinateur de référence. Pour plus d’informations, consultez le [Guide pratique pour installer manuellement des clients Configuration Manager](#BKMK_Manual).  

    > [!IMPORTANT]  
    >  Ne spécifiez pas de code de site Configuration Manager pour le client dans les propriétés de ligne de commande CCMSetup.exe.  

2.  À une invite de commandes, tapez `net stop ccmexec` pour arrêter le service hôte de l'Agent SMS (Ccmexec.exe) sur l’ordinateur de référence.  

3.  Supprimez le fichier SMSCFG.INI du dossier Windows sur l’ordinateur de référence.  

4.  Supprimez les certificats qui sont éventuellement stockés dans le magasin local de l’ordinateur de référence. Par exemple, si vous utilisez des certificats d’infrastructure à clé publique (PKI), avant de mettre l’ordinateur en image, supprimez les certificats dans le magasin **Personnel** de l’**Ordinateur** et de l’**Utilisateur**.  

5.  Si les clients sont installés dans une hiérarchie Configuration Manager différente de celle de l’ordinateur de référence, supprimez la clé racine approuvée de l’ordinateur de référence.  

    > [!NOTE]  
    >  Si les clients ne peuvent pas demander à Active Directory Domain Services de localiser un point de gestion, ils utilisent une clé racine approuvée pour déterminer les points de gestion approuvés. Si vous déployez tous les clients mis en image dans la même hiérarchie que celle de l’ordinateur maître, conservez la clé racine approuvée. 
    > 
    > Si vous déployez les clients dans des hiérarchies différentes, supprimez la clé racine approuvée. De même, fournissez la nouvelle clé racine approuvée à ces clients. Pour plus d’informations, voir [Planification de la clé racine approuvée](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForRTK).  

6.  Utilisez votre logiciel d’acquisition d’images pour capturer une image de l’ordinateur de référence.  

7.  Déployez l'image vers les ordinateurs de destination.  



##  <a name="BKMK_ClientWorkgroup"></a> Ordinateurs d’un groupe de travail  

Configuration Manager prend en charge l’installation du client sur des ordinateurs de groupe de travail. Installez le client sur les ordinateurs du groupe de travail à l’aide de la méthode spécifiée dans le [Guide pratique pour installer manuellement des clients Configuration Manager](#BKMK_Manual).  


### <a name="prerequisites"></a>Prérequis  

-   Installez manuellement le client sur chaque ordinateur du groupe de travail. Pendant l’installation, l’utilisateur interactif doit disposer de droits d’administrateur local.  

-   Pour accéder aux ressources du domaine du serveur de site Configuration Manager, configurez le compte d’accès réseau pour le site. Spécifiez ce compte comme un composant de site de distribution de logiciels. Pour plus d’informations, consultez [Composants de site](/sccm/core/servers/deploy/configure/site-components).  


### <a name="limitations"></a>Limitations  

-   Les clients des groupes de travail ne peuvent pas localiser les points de gestion à partir d’Active Directory Domain Services. À la place, ils utilisent DNS, WINS ou un autre point de gestion.  

-   L’itinérance globale n’est pas prise en charge. Les clients des groupes de travail ne peuvent pas demander d’informations sur le site à Active Directory Domain Services.  

-   Les méthodes de découverte Active Directory ne peuvent pas découvrir des ordinateurs dans des groupes de travail.  

-   Vous ne pouvez pas déployer des logiciels sur des utilisateurs d’ordinateurs de groupe de travail.  

-   Vous ne pouvez pas utiliser la méthode d’installation Push du client pour installer le client sur des ordinateurs de groupe de travail.  

-   Les clients des groupes de travail ne peuvent pas utiliser Kerberos pour l’authentification et peuvent donc nécessiter une approbation manuelle.  

-   Vous ne pouvez pas configurer un client de groupe de travail comme point de distribution. Configuration Manager impose que les ordinateurs faisant office de points de distribution soient membres d’un domaine.  


### <a name="install-the-client-on-workgroup-computers"></a>Installer le client sur les ordinateurs d’un groupe de travail  

Vérifiez les composants requis, puis suivez les instructions de la section [Comment installer les clients Gestionnaire de configuration manuellement](#BKMK_Manual).  


#### <a name="workgroup-example-1"></a>Exemple de groupe de travail 1

Cet exemple effectue les actions suivantes :
- Installe le client pour la gestion des clients sur l’intranet
- Spécifie le code du site
- Spécifie le suffixe DNS pour localiser un point de gestion  

 `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

     
#### <a name="workgroup-example-2"></a>Exemple de groupe de travail 2

Dans cet exemple, le client doit se trouver à un emplacement réseau configuré dans un groupe de limites. Si cette exigence est remplie, l’attribution automatique de site ne fonctionne pas. La commande inclut un point d’état de secours sur le serveur FSPSERVER. Cette propriété facilite le suivi du déploiement du client et permet d’identifier les éventuels problèmes de communication du client.

   `CCMSetup.exe FSP=fspserver.constoso.com`  

      

##  <a name="BKMK_ClientInternet"></a> Gestion des clients basée sur Internet  
 
> [!NOTE]  
> Cette section ne s’applique pas aux clients qui utilise une [passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway). Pour installer des clients sur Internet en utilisant une passerelle de gestion cloud, consultez [Installer et attribuer des clients Gestionnaire de configuration Windows 10 à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure).  

Si le site Configuration Manager prend en charge la [gestion des clients sur Internet](/sccm/core/clients/manage/plan-internet-based-client-management) pour des clients pouvant être sur l’intranet ou sur Internet, deux options s’offrent à vous au moment d’installer les clients sur l’intranet :  

-   Vous pouvez inclure la propriété de Client.msi `CCMHOSTNAME=<internet FQDN of the internet-based management point>` lors de l'installation du client, par exemple par le biais de l'installation manuelle ou du Push du client. Quand vous utilisez cette méthode, attribuez directement le client au site. Vous ne pouvez pas utiliser une attribution automatique du site. Consultez la section [Guide pratique pour installer manuellement des clients Configuration Manager](#BKMK_Manual), qui fournit un exemple de cette méthode de configuration.  

-   Installez le client dans l’optique d’une gestion des clients sur l’intranet, puis attribuez au client un point de gestion des clients basé sur Internet. Modifiez le point de gestion à l’aide des propriétés du client dans la page **Configuration Manager** du panneau de configuration ou à l’aide d’un script. Lorsque vous utilisez cette méthode, vous pouvez utiliser l'attribution automatique des clients. Pour plus d’informations, consultez la section [Guide pratique pour configurer les clients en vue d’une gestion basée sur Internet après leur installation](#BKMK_ConfigureIBCM_MP).  

Pour installer des clients qui se trouvent sur Internet, choisissez l’une des méthodes prises en charge suivantes :  

-   Prévoyez un mécanisme permettant à ces clients de se connecter temporairement à l’intranet via un réseau privé virtuel (VPN). Installez ensuite le client en employant une méthode d’installation du client appropriée.  

-   Utilisez une méthode d’installation indépendante de Configuration Manager. Par exemple, empaquetez les fichiers sources d’installation du client sur un média amovible et envoyez-le aux utilisateurs. Les fichiers sources d’installation du client se trouvent dans le dossier `<installation path>\Client` du serveur de site Configuration Manager. Sur le média, incluez un script à copier manuellement dans le dossier du client. À partir de ce dossier, installez manuellement le client en utilisant CCMSetup.exe et toutes les propriétés de ligne de commande CCMSetup appropriées.  

> [!NOTE]  
>  Configuration Manager ne prend pas en charge l’installation directe d’un client à partir du point de gestion Internet ou du point de mise à jour logicielle Internet.

Les clients gérés via internet doivent communiquer avec des systèmes de site basés sur Internet. Vérifiez que ces clients possèdent aussi des certificats d’infrastructure à clé publique (PKI) avant d’installer le client. Installez ces certificats indépendamment de Configuration Manager. Pour plus d’informations, consultez [Configuration requise des certificats PKI](/sccm/core/plan-design/network/pki-certificate-requirements).  


### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Installer des clients sur Internet en spécifiant des propriétés de ligne de commande CCMSetup  

1.  Suivez les instructions de la section [Guide pratique pour installer manuellement des clients Configuration Manager](#BKMK_Manual). Incluez toujours les options suivantes :  

    -   Paramètre de ligne de commande CCMSetup `/source:<local path of the copied Client folder>`  

    -   Paramètre de ligne de commande CCMSetup `/UsePKICert`  

    -   Propriété Client.msi `CCMHOSTNAME=<FQDN of internet-based management point>`  

    -   Propriété Client.msi `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    -   Propriété Client.msi `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    >  Si le site comporte plusieurs points de gestion sur Internet, le choix du point de gestion Internet importe peu pour la propriété `CCMHOSTNAME`. Quand un client Configuration Manager se connecte au point de gestion Internet spécifié, ce dernier envoie au client une liste des points de gestion Internet disponibles sur le site. Le client en sélectionne un de façon aléatoire dans la liste.

2.  Si vous ne souhaitez pas que le client vérifie la liste de révocation de certificats, spécifiez le paramètre de ligne de commande CCMSetup `/NoCRLCheck`.  

3.  Si vous utilisez un point d’état de secours basé sur Internet, spécifiez la propriété Client.msi `FSP=<internet FQDN of the internet-based fallback status point>`.  

4.  Si vous installez le client pour la gestion des clients par Internet uniquement, spécifiez la propriété Client.msi `CCMALWAYSINF=1`.  

5.  Déterminez si vous devez spécifier des paramètres de ligne de commande CCMSetup supplémentaires. Par exemple, si le client possède plusieurs certificats d’infrastructure à clé publique (PKI) valides, vous pouvez devoir spécifier un critère de sélection de certificat. Pour obtenir la liste des propriétés disponibles, consultez [À propos des propriétés et des paramètres d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).  


#### <a name="internet-based-example"></a>Exemple basé sur Internet

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`    

Cet exemple installe le client avec les comportements suivants :
  - Utilisez des fichiers sources à partir d’un dossier situé sur le lecteur D.
  - Utilisez un certificat PKI du client.
  - Sélectionnez le certificat présentant la plus longue période de validité.
  - Gestion des clients Internet uniquement.
  - Attribuez au client l’utilisation du point de gestion Internet nommé SERVER1.
  - Attribuez le point d’état de secours Internet dans le domaine contoso.com.
  - Attribuez le client au site ABC.  


###  <a name="BKMK_ConfigureIBCM_MP"></a> Pour configurer les clients en vue d’une gestion des clients basée sur Internet après leur installation  

Pour attribuer le point de gestion Internet après avoir installé le client, utilisez l’une des procédures suivantes. La première procédure reposant sur une configuration manuelle, elle est adaptée à un nombre de clients limité. En revanche, si vous avez un grand nombre de clients à configurer, la deuxième procédure est plus appropriée.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Configurez les clients en vue de les gérer via Internet après leur installation à partir du panneau de configuration Configuration Manager  

1.  Ouvrez le Panneau de configuration **Configuration Manager** sur le client.  

2.  Sous l’onglet **Internet**, entrez le nom de domaine complet (FQDN) du point de gestion Internet comme **FQDN Internet**.  

    > [!NOTE]  
    >  L'onglet **Internet** est disponible uniquement si le client dispose d'un certificat PKI client.  

3.  Si le client accède à Internet via un serveur proxy, entrez les paramètres de ce dernier.  


#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Configurer les clients en vue d’une gestion via Internet après leur installation au moyen d’un script  

##### <a name="vbscript"></a>VBScript

1.  Ouvrez un éditeur de texte, tel que le Bloc-notes.  

2.  Copiez et insérez le code VBScript suivant et dans le fichier. Remplacez `mp.contoso.com` par le nom de domaine complet Internet de votre point de gestion Internet.  

    ``` VBScript 
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
    >  Pour supprimer un point de gestion Internet spécifié, supprimez la valeur de nom de domaine complet (FQDN) du serveur placée entre guillemets. La ligne devient `newInternetBasedManagementPointFQDN = ""`.

4.  Enregistrez le fichier avec une extension .vbs.  

5.  Utilisez cscript.exe pour exécuter le script sur les ordinateurs clients. Utilisez une de ces méthodes :  

    -   Déployez le fichier sur les clients Configuration Manager existants en utilisant un package et un programme.  

    -   Exécutez le fichier localement sur les clients Gestionnaire de configuration existants en double-cliquant sur le fichier de script dans l'Explorateur de fichiers.  

Vous devrez peut-être redémarrer le client pour que les modifications prennent effet.  

##### <a name="powershell"></a>PowerShell

1. Ouvrez un éditeur en ligne de PowerShell, comme PowerShell ISE ou Visual Studio Code. Vous pouvez également utiliser un éditeur de texte, tel que le Bloc-notes.

2. Copiez et insérez les lignes de code suivantes dans l’éditeur. Remplacez `'mp.contoso.com'` par le nom de domaine complet Internet de votre point de gestion Internet.

    ``` PowerShell
    
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    
    ```

    > [!NOTE]  
    >  La dernière ligne existe uniquement pour vérifier la nouvelle valeur de point de gestion internet.
    >
    >  Pour supprimer un point de gestion Internet spécifié, supprimez la valeur de nom de domaine complet (FQDN) du serveur placée entre guillemets. La ligne devient `$newInternetBasedManagementPointFQDN = ''`.

3. Exécutez ce script avec des droits élevés.


##  <a name="BKMK_Provision"></a> Configurer les propriétés d’installation du client pour les installations de la stratégie de groupe et du client en fonction des mises à jour logicielles

Utilisez la stratégie de groupe Windows pour configurer des ordinateurs avec les propriétés d’installation du client Gestionnaire de configuration. Ces propriétés sont stockées dans le Registre de l’ordinateur. Le client les lit lors de son installation. Cette procédure n’est généralement pas obligatoire, mais peut s’avérer nécessaire dans certains scénarios d’installation du client, par exemple :  

-   Vous utilisez les paramètres de stratégie de groupe ou des méthodes d’installation du client en fonction des mises à jour logicielles. Vous n’avez pas étendu le schéma Active Directory pour Configuration Manager.  

-   Vous souhaitez redéfinir les propriétés de l'installation du client sur certains ordinateurs.  

> [!NOTE]  
>  Si des propriétés d’installation sont fournies sur la ligne de commande CCMSetup.exe, les propriétés d’installation fournies aux ordinateurs ne sont pas utilisées.

Le modèle d’administration de stratégie de groupe nommé ConfigMgrInstallation.adm est fourni sur le média d’installation de Configuration Manager. Utilisez ce modèle pour provisionner des ordinateurs clients avec les propriétés d’installation.


### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Configurer et attribuer des propriétés d’installation du client à l’aide d’un objet de stratégie de groupe  

1.  Importez le modèle d’administration ConfigMgrInstallation.adm dans un objet de stratégie de groupe nouveau ou existant, à l’aide d’un éditeur comme l’Éditeur d’objets de stratégie de groupe Windows. Vous pouvez trouver ce fichier dans le dossier `TOOLS\ConfigMgrADMTemplates` sur le média d’installation de Configuration Manager.  

2.  Affichez les propriétés du paramètre importé **Configurer les paramètres de déploiement du client**.  

3.  Sélectionnez **activé**.  

4.  Dans la zone **CCMSetup** , entrez les propriétés de ligne de commande CCMSetup requises. Pour obtenir la liste de toutes les propriétés de ligne de commande CCMSetup et des exemples montrant comment les utiliser, consultez [À propos des propriétés et des paramètres d’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).  

5.  Attribuez l’objet stratégie de groupe aux ordinateurs auxquels vous souhaitez fournir les propriétés d’installation du client Configuration Manager.  
