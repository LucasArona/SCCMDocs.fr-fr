---
title: Comptes utilisés
titleSuffix: Configuration Manager
description: Identifiez et gérez les groupes Windows, ainsi que les comptes utilisés dans Configuration Manager.
ms.date: 03/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a05ff407c3787283a58973f2861432a0a26a52b0
ms.sourcegitcommit: deb28cdc95a456d4a38499ef1bc71e765ef6dc13
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/03/2019
ms.locfileid: "58901517"
---
# <a name="accounts-used-in-configuration-manager"></a>Comptes utilisés dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations suivantes afin d’identifier les groupes Windows et les comptes utilisés dans Configuration Manager, de savoir comment ils sont utilisés et de connaître les exigences associées.  

- [Groupes Windows créés et utilisés par Configuration Manager](#bkmk_groups)  
    - [ConfigMgr_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
    - [ConfigMgr_DViewAccess](#configmgr_dviewaccess)  
    - [Utilisateurs du contrôle à distance ConfigMgr](#configmgr-remote-control-users)  
    - [Administrateurs SMS](#sms-admins)  
    - [SMS_SiteSystemToSiteServerConnection_MP_&lt;code_site\>](#bkmk_remotemp)  
    - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;code_site\>](#bkmk_remoteprov)  
    - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;code_site\>](#bkmk_remotestat)  
    - [SMS_SiteToSiteConnection_&lt;code_site\>](#bkmk_filerepl)  

- [Comptes utilisés par Configuration manager](#bkmk_accounts)
    - [Compte de découverte de groupes Active Directory](#active-directory-group-discovery-account)  
    - [Compte de découverte de systèmes Active Directory](#active-directory-system-discovery-account)  
    - [Compte de découverte d’utilisateurs Active Directory](#active-directory-user-discovery-account)  
    - [Compte de forêt Active Directory](#active-directory-forest-account)  
    - [Compte de point d’enregistrement de certificat](#certificate-registration-point-account)  
    - [Compte de capture des images de système d’exploitation](#capture-os-image-account)  
    - [Compte d’installation Push du client](#client-push-installation-account)  
    - [Compte de connexion du point d’inscription](#enrollment-point-connection-account)  
    - [Compte de connexion Exchange Server](#exchange-server-connection-account)  
    - [Compte de connexion du point de gestion](#management-point-connection-account)  
    - [Compte de connexion multidiffusion](#multicast-connection-account)  
    - [Compte d’accès au réseau](#network-access-account)  
    - [Compte d’accès au package](#package-access-account)  
    - [Compte du point de Reporting Services](#reporting-services-point-account)  
    - [Comptes d’observateurs autorisés des outils de contrôle à distance](#remote-tools-permitted-viewer-accounts)  
    - [Compte d’installation du site](#site-installation-account)
    - [Compte d’installation du système de site](#site-system-installation-account)  
    - [Compte du serveur proxy du système de site](#site-system-proxy-server-account)  
    - [Compte de connexion au serveur SMTP](#smtp-server-connection-account)  
    - [Compte de connexion au point de mise à jour logicielle](#software-update-point-connection-account)  
    - [Compte du site source](#source-site-account)  
    - [Compte de base de données du site source](#source-site-database-account)  
    - [Compte de jonction de domaine de séquence de tâches](#task-sequence-domain-join-account)  
    - [Compte de connexion au dossier réseau de la séquence de tâches](#task-sequence-network-folder-connection-account)  
    - [Compte d’identification de la séquence de tâches](#task-sequence-run-as-account)  



## <a name="bkmk_groups"></a> Groupes Windows créés et utilisés par Configuration Manager  

 Configuration Manager crée automatiquement et, très souvent, gère automatiquement les groupes Windows suivants :  

> [!NOTE]  
>  Lorsque Configuration Manager crée un groupe sur un ordinateur qui est membre d’un domaine, ce groupe devient un groupe de sécurité local. Si l’ordinateur est un contrôleur de domaine, le groupe devient un groupe de domaine local. Ce type de groupe est partagé par tous les contrôleurs de domaine du domaine.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess

Configuration Manager utilise ce groupe pour autoriser la consultation des fichiers collectés par l’inventaire logiciel.  

Pour plus d’informations, consultez [Présentation de l’inventaire logiciel](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur le serveur de site principal.

Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désinstallation du site.

#### <a name="membership"></a>Adhésion
Configuration Manager gère automatiquement l'appartenance au groupe. Les membres incluent les utilisateurs administratifs qui disposent de l'autorisation **Afficher les fichiers collectés** pour l'objet sécurisable **Regroupement** depuis un rôle de sécurité attribué.

#### <a name="permissions"></a>Autorisations
Par défaut, ce groupe dispose de l’autorisation **Lecture** pour le dossier suivant situé sur le serveur de site : `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`  


### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  

 Ce groupe est un groupe de sécurité local créé par Configuration Manager sur le serveur de base de données du site ou sur le serveur réplica de base de données pour un site principal enfant. Le site crée ce groupe lorsque vous utilisez des vues distribuées pour la réplication de base de données entre sites au sein d’une hiérarchie. Il contient les comptes d’ordinateurs SQL Server et du serveur de site du site d’administration centrale.

 Pour plus d’informations, consultez [Transferts de données entre sites](/sccm/core/servers/manage/data-transfers-between-sites).


### <a name="configmgr-remote-control-users"></a>Utilisateurs du contrôle à distance ConfigMgr  

 Les outils de contrôle à distance de Configuration Manager utilisent ce groupe pour stocker les comptes et les groupes que vous configurez dans la liste **Observateurs autorisés**. Le site attribue cette liste à chaque client.  

Pour plus d’informations, consultez [Présentation du contrôle à distance](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur le client Configuration Manager, lorsque le client reçoit une stratégie qui active les outils de contrôle à distance.

Lorsque vous désactivez les outils de contrôle à distance pour un client, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désactivation des outils à distance.

#### <a name="membership"></a>Adhésion
Par défaut, ce groupe ne contient aucun membre. Lorsque vous ajoutez des utilisateurs à la liste **Observateurs autorisés**, ils sont automatiquement ajoutés à ce groupe.

Utilisez la liste **Observateurs autorisés** pour gérer l’appartenance à ce groupe, plutôt que d’ajouter des utilisateurs ou des groupes directement à ce groupe.

En plus d’être un observateur autorisé, un utilisateur administratif doit disposer de l’autorisation **Contrôle à distance** sur l’objet **Regroupement**. Vous pouvez attribuer cette autorisation à l’aide du rôle de sécurité **Opérateur d’outils à distance**.  

#### <a name="permissions"></a>Autorisations
Par défaut, ce groupe ne dispose d’aucune autorisation sur les emplacements de l’ordinateur. Il ne sert qu’à contenir la liste **Observateurs autorisés**.  


### <a name="sms-admins"></a>Administrateurs SMS  

 Configuration Manager utilise ce groupe pour accorder l’accès au fournisseur SMS via WMI. L’accès au fournisseur SMS est requis pour afficher et modifier des objets dans la console Configuration Manager.  

> [!NOTE]  
>  La configuration de l'administration basée sur les rôles d'un utilisateur administratif détermine quels objets celui-ci peut consulter et gérer, lorsqu'il utilise la console Configuration Manager.  

Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur chaque ordinateur qui dispose d’un fournisseur SMS. 

Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désinstallation du site.

#### <a name="membership"></a>Adhésion
Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, le compte d’ordinateur du serveur de site, et chaque utilisateur administratif d’une hiérarchie, sont membres du groupe **Administrateurs SMS** sur tous les ordinateurs du fournisseur SMS d’un site.

#### <a name="permissions"></a>Autorisations
Vous pouvez afficher les autorisations du groupe Administrateurs SMS dans le composant logiciel enfichable MMC **Contrôle WMI**. Par défaut, les autorisations **Activer le compte** et **Appel à distance autorisé** sont accordées au groupe dans l’espace de noms WMI `Root\SMS`. Les utilisateurs authentifiés disposent des autorisations **Méthodes d’exécution**, **Écriture fournisseur** et **Activer le compte**.

Lorsque vous utilisez une console Configuration Manager distante, configurez les autorisations DCOM **Activation à distance** à la fois sur l’ordinateur du serveur de site et dans le fournisseur SMS. Accordez ces droits au groupe **Administrateurs SMS**. Cette action simplifie l’administration en vous évitant d’avoir à accorder ces droits directement aux utilisateurs et aux groupes. Pour plus d’informations, consultez [Configurer les autorisations DCOM pour les consoles Configuration Manager distantes](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;code_site\>  
 
Les points de gestion qui sont distants du serveur de site utilisent ce groupe pour se connecter à la base de données du site. Ce groupe fournit un accès au point de gestion pour les dossiers Boîte de réception sur le serveur de site et la base de données du site.  

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur chaque ordinateur qui dispose d’un fournisseur SMS.

Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désinstallation du site.

#### <a name="membership"></a>Adhésion
Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, l'appartenance inclut les comptes d'ordinateur des ordinateurs distants qui disposent d'un point de gestion pour le site.

#### <a name="permissions"></a>Autorisations
Par défaut, ce groupe dispose des autorisations **Lecture**, **Lecture et exécution** et **Affichage du contenu du dossier** pour le dossier suivant situé sur le serveur de site : `C:\Program Files\Microsoft Configuration Manager\inboxes`. Ce groupe dispose de l’autorisation supplémentaire **Écriture** pour les sous-dossiers du dossier **inboxes** dans lesquels le point de gestion écrit les données client.


### <a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;code_site\>  
 
Les ordinateurs distants du fournisseur SMS utilisent ce groupe pour se connecter au serveur de site.  

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur le serveur de site.

Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désinstallation du site.

#### <a name="membership"></a>Adhésion
Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, l’appartenance comprend le compte d’ordinateur ou un compte d’utilisateur de domaine. Il utilise ce compte pour se connecter au serveur de site à partir de chaque fournisseur SMS distant.

#### <a name="permissions"></a>Autorisations
Par défaut, ce groupe dispose des autorisations **Lecture**, **Lecture et exécution** et **Affichage du contenu du dossier** pour le dossier suivant situé sur le serveur de site : `C:\Program Files\Microsoft Configuration Manager\inboxes`. Ce groupe dispose des autorisations supplémentaires **Écriture** et **Modifier** pour les sous-dossiers situés sous le dossier « inboxes ». Le fournisseur SMS a besoin d’accéder à ces dossiers.

Ce groupe dispose également de l’autorisation **Lecture** pour les sous-dossiers du serveur de site situés sous `C:\Program Files\Microsoft Configuration Manager\OSD\Bin`. 

Il dispose également des autorisations suivantes pour les sous-dossiers situés sous `C:\Program Files\Microsoft Configuration Manager\OSD\boot` :
- **Lecture**  
- **Lecture et exécution**  
- **Affichage du contenu du dossier**  
- **Écriture**  
- **Modification**   


### <a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;code_site\>  

Le composant Gestionnaire de répartition de fichier installé sur les ordinateurs de système de site distants Configuration Manager utilise ce groupe pour se connecter au serveur de site.  

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur le serveur de site.

Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désinstallation du site.

#### <a name="membership"></a>Adhésion
Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, l’appartenance comprend le compte d’ordinateur ou le compte d’utilisateur de domaine. Il utilise ce compte pour se connecter au serveur de site à partir de chaque système de site distant qui exécute le Gestionnaire de répartition de fichier.

#### <a name="permissions"></a>Autorisations
Par défaut, ce groupe dispose des autorisations **Lecture**, **Lecture et exécution** et **Affichage du contenu du dossier** pour le dossier suivant et tous ses sous-dossiers situés sur le serveur de site : `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

Ce groupe dispose des autorisations supplémentaires **Écriture** et **Modifie** pour le dossier suivant situé sur le serveur de site : `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;code_site\>  
 Configuration Manager utilise ce groupe pour activer la réplication de fichiers entre les sites d’une hiérarchie. Pour chaque site distant qui transfère directement des fichiers vers ce site, ce groupe contient les comptes configurés en tant que **compte de réplication de fichiers**.  

#### <a name="type-and-location"></a>Type et emplacement
Ce groupe est un groupe de sécurité local créé sur le serveur de site.

#### <a name="membership"></a>Adhésion
Lorsque vous installez un nouveau site en tant qu’enfant d’un autre site, Configuration Manager ajoute automatiquement le compte de l’ordinateur du nouveau serveur de site au groupe situé sur le serveur de site parent. Configuration Manager ajoute également le compte d’ordinateur du site parent au groupe sur le serveur de site. Si vous spécifiez un autre compte pour les transferts de fichiers, ajoutez ce compte à ce groupe sur le serveur de site de destination.

Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Vous devez le supprimer manuellement après la désinstallation du site.

#### <a name="permissions"></a>Autorisations
Par défaut, ce groupe dispose du **contrôle intégral** pour le dossier suivant : `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="bkmk_accounts"></a> Comptes utilisés par Configuration manager  

 Vous pouvez utiliser les comptes suivants pour Configuration Manager.  


### <a name="active-directory-group-discovery-account"></a>Compte de découverte de groupes Active Directory  

 Le site utilise le **compte de découverte de groupes Active Directory** pour découvrir les objets situés aux emplacements Active Directory Domain Services que vous spécifiez :
- Les groupes de sécurité local, global et universel
- L’appartenance au sein de ces groupes
- L’appartenance au sein des groupes de distribution
   - Les groupes de distribution ne sont pas découverts en tant que ressources de groupe

  Ce compte peut être un compte d'ordinateur du serveur de site qui exécute la découverte ou un compte d'utilisateur Windows. Il doit disposer de l’autorisation d’accès **Lecture** pour les emplacements Active Directory que vous avez spécifiés pour la découverte.  

  Pour plus d’informations, consultez [Découverte de groupes Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Compte de découverte de systèmes Active Directory  

 Le site utilise le **compte de découverte de systèmes Active Directory** pour découvrir les ordinateurs situés aux emplacements Active Directory Domain Services que vous spécifiez.  

 Ce compte peut être un compte d'ordinateur du serveur de site qui exécute la découverte ou un compte d'utilisateur Windows. Il doit disposer de l’autorisation d’accès **Lecture** pour les emplacements Active Directory que vous avez spécifiés pour la découverte.  

 Pour plus d’informations, consultez [Découverte de systèmes Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Compte de découverte d’utilisateurs Active Directory  
 
 Le site utilise le **compte de découverte d’utilisateurs Active Directory** pour découvrir les comptes d’utilisateurs situés aux emplacements Active Directory Domain Services que vous spécifiez.  

 Ce compte peut être un compte d'ordinateur du serveur de site qui exécute la découverte ou un compte d'utilisateur Windows. Il doit disposer de l’autorisation d’accès **Lecture** pour les emplacements Active Directory que vous avez spécifiés pour la découverte.  

 Pour plus d’informations, consultez [Découverte d’utilisateurs Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Compte de forêt Active Directory  

 Le site utilise le **compte de forêt Active Directory** pour découvrir l’infrastructure réseau des forêts Active Directory. Les sites d’administration centrale et les sites principaux l’utilisent également pour publier des données dans les services AD DS d’une forêt.  

 > [!NOTE]  
 >  Les sites secondaires utilisent toujours le compte d'ordinateur du serveur de site secondaire pour publier dans Active Directory.  

 Pour la découverte et la publication des forêts non approuvées, le compte de forêt Active Directory doit être un compte global. Si vous n’utilisez pas le compte d’ordinateur du serveur de site, vous ne pouvez sélectionner qu’un compte global.  

 Ce compte doit disposer des autorisations de **Lecture** pour chaque forêt Active Directory dont vous souhaitez découvrir l'infrastructure réseau.  

 Ce compte doit disposer des autorisations **Contrôle intégral** pour le conteneur **Gestion du système** et tous ses objets enfants, dans chaque forêt Active Directory où vous souhaitez publier des données de site. Pour plus d’informations, consultez [Préparer Active Directory pour la publication de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).  

 Pour plus d’informations, consultez [Découverte de forêts Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Compte de point d’enregistrement de certificat  

 Le point d’enregistrement du certificat utilise le **compte de point d’enregistrement de certificat** pour se connecter à la base de données Configuration Manager. Il utilise son compte d’ordinateur par défaut, cependant, vous pouvez configurer un compte d’utilisateur à la place de celui-ci. Lorsque le point d’enregistrement de certificat se trouve dans un domaine non approuvé du serveur de site, vous devez spécifier un compte d’utilisateur. Ce compte ne requiert qu’un accès en **Lecture** sur la base de données du site, car le système de messages d’état gère les tâches d’écriture.  

 Pour plus d’informations, consultez [Présentation des profils de certificat](/sccm/protect/deploy-use/introduction-to-certificate-profiles).


### <a name="capture-os-image-account"></a>Compte de capture des images de système d’exploitation  

 Lorsque vous capturez une image de système d’exploitation, Configuration Manager utilise le **compte de capture des images de système d’exploitation** pour accéder au dossier dans lequel sont stockées les images capturées. Ce compte est nécessaire si vous ajoutez l’étape **Capturer l’image du système d’exploitation** à la séquence de tâches.  

 Le compte doit disposer d’autorisations en **Lecture** et en **Écriture** sur le partage réseau où sont stockées les images capturées.  

 Si vous modifiez le mot de passe du compte dans Windows, mettez à jour la séquence de tâches avec le nouveau mot de passe. Le client Configuration Manager reçoit le nouveau mot de passe quand il télécharge la stratégie du client.  

 Si vous avez besoin d’utiliser ce compte, créez un compte d’utilisateur de domaine. Accordez-lui des autorisations minimales pour accéder aux ressources réseau nécessaires, et utilisez-le pour toutes les séquences de tâches de capture.  

 > [!IMPORTANT]  
 >  N’attribuez pas d’autorisations de connexion interactive à ce compte.  
 >   
 >  N’utilisez pas le compte d’accès réseau pour ce compte.  

 Pour plus d’informations, consultez [Créer une séquence de tâches pour capturer un système d’exploitation](/sccm/osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system).


### <a name="client-push-installation-account"></a>Compte d’installation Push du client  

 Si vous déployez des clients via l’installation Push du client, le site utilise le **compte d’installation Push du client** pour se connecter aux ordinateurs et installer le logiciel client Configuration Manager. Si vous ne spécifiez pas ce compte, le serveur de site tente d’utiliser son propre compte d’ordinateur.  

 Ce compte doit être membre du groupe **Administrateurs** local sur les ordinateurs clients cibles. Ce compte ne nécessite pas d’autorisations **Administrateur de domaine**.  

 Vous pouvez spécifier plusieurs comptes d’installation Push du client. Configuration Manager les essaie les uns après les autres jusqu’à ce que l’un d’eux fonctionne.  

> [!TIP]  
>  Si vous disposez d’un grand environnement Active Directory et que vous devez modifier ce compte, utilisez le processus suivant pour coordonner plus efficacement la mise à jour du compte : 
> 1. Créez un compte avec un nom différent.   
> 2. Ajoutez le nouveau compte à la liste des comptes d’installation Push du client dans Configuration Manager.  
> 3. Attendez qu’Active Directory Domain Services ait fini de répliquer le nouveau compte.  
> 4. Supprimez l’ancien compte de Configuration Manager et d’Active Directory Domain Services.  

> [!IMPORTANT]  
>  Ne permettez pas à ce compte de se connecter localement.  

 Pour plus d’informations, consultez [Installation Push du client](/sccm/core/clients/deploy/plan/client-installation-methods#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Compte de connexion du point d’inscription  

 Le point d’inscription utilise le **compte de connexion du point d’inscription** pour se connecter à la base de données Configuration Manager. Il utilise son compte d’ordinateur par défaut, cependant, vous pouvez configurer un compte d’utilisateur à la place de celui-ci. Si le point d’inscription se trouve dans un domaine non approuvé du serveur de site, vous devez spécifier un compte d’utilisateur. Ce compte requiert un accès en **Lecture** et en **Écriture** à la base de données du site.  

 Pour plus d’informations, consultez [Installer des rôles de système de site pour la gestion des appareils mobiles locale](/sccm/mdm/get-started/install-site-system-roles-for-on-premises-mdm).


### <a name="exchange-server-connection-account"></a>Compte de connexion Exchange Server  

 Le serveur de site utilise le **compte de connexion à Exchange Server** pour se connecter à l’instance Exchange Server spécifiée. Il utilise cette connexion pour rechercher et gérer les appareils mobiles qui se connectent à Exchange Server. Ce compte nécessite des applets de commande PowerShell Exchange qui fournissent les autorisations requises pour l'ordinateur Exchange Server. Pour plus d’informations sur les applets de commande, consultez [Gérer des appareils mobiles à l’aide de Configuration Manager et d’Exchange](/sccm/mdm/deploy-use/manage-mobile-devices-with-exchange-activesync).  


### <a name="management-point-connection-account"></a>Compte de connexion du point de gestion  

 Le point de gestion utilise le **compte de connexion du point de gestion** pour se connecter à la base de données Configuration Manager. Il utilise cette connexion pour envoyer et récupérer des informations concernant les clients. Le point de gestion utilise son compte d’ordinateur par défaut, cependant, vous pouvez configurer un compte d’utilisateur à la place de celui-ci. Si le point de gestion se trouve dans un domaine non approuvé du serveur de site, vous devez spécifier un compte d’utilisateur.  

 Créez le compte comme un compte doté de droits limités, compte local sur l'ordinateur qui exécute Microsoft SQL Server.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations de connexion interactive.  


### <a name="multicast-connection-account"></a>Compte de connexion multidiffusion  

 Les points de distribution configurés pour la multidiffusion utilisent le **compte de connexion multidiffusion** pour lire les informations de la base de données de site. Le serveur utilise son compte d’ordinateur par défaut, cependant, vous pouvez configurer un compte d’utilisateur à la place de celui-ci. Si la base de données de site se trouve dans une forêt non approuvée, vous devez spécifier un compte d’utilisateur. Par exemple, si votre centre de données dispose d’un réseau de périmètre dans une forêt autre que celle du serveur de site et de la base de données du site, utilisez ce compte pour lire les informations de multidiffusion dans la base de données du site.  

 Si vous avez besoin de ce compte, créez-le en tant que compte local doté de droits limités sur l’ordinateur qui exécute Microsoft SQL Server.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations de connexion interactive.  

 Pour plus d’informations, consultez [Utiliser la multidiffusion pour déployer Windows sur le réseau](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network).


### <a name="network-access-account"></a>Compte d'accès réseau  

 Les ordinateurs clients utilisent le **compte d’accès réseau** quand ils ne peuvent pas utiliser leur compte d’ordinateur local pour accéder au contenu des points de distribution. Cela s’applique principalement aux clients du groupe de travail et aux ordinateurs situés dans des domaines non approuvés. Ce compte peut également être utilisé pendant le déploiement du système d’exploitation, si l’ordinateur qui installe le système d’exploitation n’a pas encore de compte d’ordinateur dans son domaine.  

> [!Important]  
>  Le compte d’accès au réseau n’est jamais utilisé comme contexte de sécurité pour exécuter des applications et des programmes, installer des mises à jour logicielles ou exécuter des séquences de tâches. Il n’est utilisé que pour accéder aux ressources du réseau.  

 Un client Configuration Manager tente d’abord d’utiliser son compte d’ordinateur pour télécharger le contenu. En cas d’échec, il essaie automatiquement le compte d’accès réseau.  

 À partir de la version 1806, les groupes de travail et les clients joints à Azure AD peuvent accéder de manière sécurisée au contenu des points de distribution sans avoir besoin d’un compte d’accès réseau. Ce comportement inclut des scénarios de déploiement de système d’exploitation avec une séquence de tâches exécutée à partir d’un support de démarrage, d’un environnement PXE (Preboot Execution Environment) ou du Centre logiciel. Pour plus d’informations, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).<!--1358228,1358278-->

 > [!Note]  
 > Si vous activez **HTTP amélioré** pour ne pas avoir besoin d’un compte d’accès réseau, le point de distribution doit exécuter Windows Server 2008 R2 SP1 ou version ultérieure. <!--SCCMDocs-pr issue #2696-->
>  
> Avant d’activer cette fonctionnalité, mettez à niveau les clients vers la version 1806 ou version ultérieure. Si vous autorisez uniquement les connexions de type **HTTP amélioré**, les clients plus anciens ne pourront plus s’authentifier à l’aide de cette méthode, et ne pourront donc plus télécharger le package de mise à niveau du client à partir d’un point de distribution. <!--vso2841213-->   

#### <a name="permissions"></a>Autorisations

 Accordez à ce compte les autorisations minimales appropriées sur le contenu dont le client a besoin pour accéder au logiciel. Le compte doit avoir le droit **Accéder à cet ordinateur à partir du réseau** sur le point de distribution. Vous pouvez configurer jusqu’à 10 comptes d’accès réseau par site.  

 Créez le compte dans n'importe quel domaine fournissant l'accès nécessaire aux ressources. Le compte d’accès réseau doit toujours inclure un nom de domaine. La sécurité pass-through n’est pas prise en charge pour ce compte. Si vous disposez de points de distribution dans plusieurs domaines, créez le compte dans un domaine approuvé.  

> [!TIP]  
> Pour éviter les verrouillages de compte, ne modifiez pas le mot de passe d’un compte d’accès réseau existant. Au lieu de cela, créez un compte et configurez-le dans Configuration Manager. Après un délai suffisant pendant lequel tous les clients ont reçu les informations du nouveau compte, supprimez l'ancien compte des dossiers partagés du réseau et supprimez le compte.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations de connexion interactive.  
>   
>  N’accordez pas à ce compte le droit de joindre des ordinateurs au domaine. Si vous devez joindre des ordinateurs au domaine au cours d’une séquence de tâches, utilisez le [compte de jonction de domaine de séquence de tâches](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Configurer le compte d’accès réseau  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez ensuite le site.  

2.  Dans le groupe **Paramètres** du ruban, sélectionnez **Configurer les composants de site**, puis choisissez **Distribution de logiciels**.  

3.  Choisissez l’onglet **Compte d’accès réseau**. Configurez un ou plusieurs comptes, puis choisissez **OK**.  


### <a name="package-access-account"></a>Compte d'accès au package  

 Un **compte d’accès au package** vous permet de définir des autorisations NTFS pour spécifier les utilisateurs et les groupes d’utilisateurs autorisés à accéder au contenu de package sur les points de distribution. Par défaut, Configuration Manager n’accorde cet accès qu’aux comptes d’accès générique **Utilisateur** et **Administrateur**. Vous pouvez contrôler l’accès des ordinateurs clients à l’aide d’autres comptes ou groupes Windows. Les appareils mobiles n’utilisent pas les comptes d’accès au package, car ils récupèrent toujours le contenu du package de façon anonyme.  

 Par défaut, quand Configuration Manager copie des fichiers de contenu sur un point de distribution, il accorde un accès en **Lecture** au groupe **Utilisateurs** local, ainsi qu’un **Contrôle intégral** au groupe **Administrateurs** local. Les autorisations nécessaires dépendent du package. Si vos clients se trouvent dans des groupes de travail ou dans des forêts non approuvées, ils utiliseront le compte d’accès réseau pour accéder au contenu du package. Vérifiez que le compte d’accès réseau bénéficie d’autorisations sur le package à l’aide des comptes d’accès au package définis.  

 Utilisez des comptes dans un domaine susceptible d'accéder aux points de distribution. Si vous créez ou modifiez le compte après avoir créé le package, vous devez redistribuer le package. La mise à jour du package ne modifie pas les autorisations NTFS associées au package.  

 Il n’est pas nécessaire d’ajouter le compte d’accès réseau comme un compte d’accès au package, car l’appartenance au groupe **Utilisateurs** l’ajoute automatiquement. Le fait de restreindre le compte d’accès au package au compte d’accès réseau uniquement n’empêche pas les clients d’accéder au package.  

#### <a name="manage-package-access-accounts"></a>Gérer les comptes d’accès au package  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels**, déterminez le type de contenu dont vous souhaitez gérer les comptes d’accès et suivez les étapes indiquées :  

    -   **Application** : Développez **Gestion d’applications**, choisissez **Applications**, puis sélectionnez l’application dont vous souhaitez gérer les comptes d’accès.  

    -   **Package** : Développez **Gestion d’applications**, choisissez **Packages**, puis sélectionnez le package dont vous souhaitez gérer les comptes d’accès.  

    -   **Package de déploiement des mises à jour logicielles** : Développez **Mises à jour logicielles**, choisissez **Packages de déploiement**, puis sélectionnez le package de déploiement dont vous souhaitez gérer les comptes d'accès.  

    -   **Package de pilotes** : Développez **Systèmes d’exploitation**, choisissez **Packages de pilotes**, puis sélectionnez le package de pilotes dont vous souhaitez gérer les comptes d’accès.  

    -   **Image de système d'exploitation** : Développez **Systèmes d’exploitation**, choisissez **Images du système d’exploitation**, puis sélectionnez l’image du système d’exploitation dont vous souhaitez gérer les comptes d’accès.  

    -   **Package de mise à niveau du système d'exploitation** : Développez **Systèmes d’exploitation**, choisissez **Packages de mise à niveau du système d’exploitation**, puis sélectionnez le package de mise à niveau du système d’exploitation dont vous souhaitez gérer les comptes d’accès.  

    -   **Image de démarrage** : Développez **Systèmes d’exploitation**, choisissez **Images de démarrage**, puis sélectionnez l’image de démarrage dont vous souhaitez gérer les comptes d’accès.  

3.  Cliquez avec le bouton droit sur l’objet sélectionné, puis choisissez **Gérer des comptes d’accès**.  

4.  Dans la boîte de dialogue **Ajouter un compte**, spécifiez le type du compte auquel les droits d’accès au contenu seront accordés, puis indiquez les droits d’accès associés au compte.  

    > [!NOTE]  
    >  Quand vous ajoutez un nom d’utilisateur au compte et que Configuration Manager trouve un compte d’utilisateur local et un compte d’utilisateur de domaine portant ce nom, Configuration Manager définit les droits d’accès du compte d’utilisateur de domaine.  


### <a name="reporting-services-point-account"></a>Compte du point de Reporting Services  
 
 SQL Server Reporting Services utilise le **compte du point de Reporting Services** pour récupérer les données des rapports Configuration Manager à partir de la base de données de site. Le compte d'utilisateur Windows et le mot de passe que vous spécifiez sont chiffrés et stockés dans la base de données SQL Server Reporting Services.  

 > [!NOTE]  
 > Le compte que vous spécifiez doit avoir des autorisations **Connexion locale** sur l’ordinateur qui héberge la base de données SQL Reporting Services.

 Pour plus d’informations, consultez [Présentation des rapports](/sccm/core/servers/manage/introduction-to-reporting).


### <a name="remote-tools-permitted-viewer-accounts"></a>Comptes d’observateurs autorisés des outils de contrôle à distance  

 Les comptes que vous spécifiez en tant qu' **Observateurs autorisés** pour le contrôle à distance sont une liste d'utilisateurs autorisés à utiliser la fonctionnalité Outils de contrôle à distance sur les clients.  

Pour plus d’informations, consultez [Présentation du contrôle à distance](/sccm/core/clients/manage/remote-control/introduction-to-remote-control).


### <a name="site-installation-account"></a>Compte d’installation du site
<!--SCCMDocs issue #572-->
Utilisez un compte d’utilisateur de domaine pour vous connecter au serveur où vous exécutez l’installation de Configuration Manager et installez un nouveau site.

Ce compte nécessite les droits suivants :  

- **Administrateur** sur les serveurs suivants :
    - Serveur de site  
    - Chaque serveur qui héberge la base de données du site  
    - Chaque instance du fournisseur SMS pour le site  

- **Sysadmin** sur l’instance de SQL Server qui héberge la base de données du site  

Le programme d’installation Configuration Manager ajoute automatiquement ce compte au groupe [Administrateurs SMS](#sms-admins).

Après l’installation, ce compte est le seul à avoir des droits sur la console Configuration Manager. Avant de supprimer ce compte, attribuez ses droits à un autre utilisateur.

Lorsque vous étendez un site autonome pour y inclure un site d’administration centrale, ce compte doit disposer des droits d’administration basée sur des rôles **Administrateur complet** ou **Administrateur d’infrastructure** sur le site principal autonome.


### <a name="site-system-installation-account"></a>Compte d’installation du système de site  

 Le serveur de site utilise le **compte d’installation du système de site** pour installer, réinstaller, désinstaller et configurer des systèmes de site. Si vous configurez le système de site pour que le serveur de site établisse des connexions vers ce système de site, Configuration Manager utilise également ce compte pour tirer (pull) les données du système de site après l’installation de celui-ci et des rôles qui lui sont associés. Chaque système de site peut avoir un autre compte d’installation. Toutefois, vous ne pouvez configurer qu’un seul compte d’installation pour gérer tous les rôles de ce système de site.  

 Ce compte nécessite des autorisations d’administrateur locales sur les systèmes de site cibles. De plus, ce compte doit disposer du droit **Accéder à cet ordinateur à partir du réseau** dans la stratégie de sécurité, sur les systèmes de site cibles.  

 > [!TIP]  
 >  Si vous avez plusieurs contrôleurs de domaine et si ces comptes sont utilisés dans plusieurs domaines, vérifiez qu’ils ont été répliqués par Active Directory avant de configurer le système de site.  
 >   
 >  Lorsque vous spécifiez un compte local sur chaque système de site à gérer, cette configuration est plus sécurisée que l’utilisation de comptes de domaine. En effet, elle limite les dommages provoqués par les attaquants en cas de compromission du compte. Toutefois, les comptes de domaine sont plus faciles à gérer. Examinez le compromis entre sécurité et efficacité d’administration.  


### <a name="site-system-proxy-server-account"></a>Compte du serveur proxy du système de site
<!--SCCMDocs issue #648-->
 Les rôles de système de site suivants utilisent le **compte de serveur proxy de système de site** pour accéder à Internet via un serveur proxy ou un pare-feu qui exige un accès authentifié :

- Point de synchronisation Asset Intelligence
- Connecteur Exchange Server
- point de connexion de service
- Point de mise à jour logicielle

> [!IMPORTANT]  
>  Spécifiez un compte qui dispose des autorisations minimales pour le serveur proxy requis ou le pare-feu.  

 Pour plus d’informations, consultez [Prise en charge des serveurs proxy](/sccm/core/plan-design/network/proxy-server-support).


### <a name="smtp-server-connection-account"></a>Compte de connexion au serveur SMTP  

 Le serveur de site utilise le **compte de connexion au serveur SMTP** pour envoyer des alertes par e-mail quand le serveur SMTP exige un accès authentifié.  

> [!IMPORTANT]  
>  Spécifiez un compte qui dispose des autorisations minimales pour envoyer des courriers électroniques.  

 Pour plus d’informations, consultez [Utiliser des alertes et le système d’état](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="software-update-point-connection-account"></a>Compte de connexion de point de mise à jour logicielle  

 Le serveur de site utilise le **compte de connexion de point de mise à jour logicielle** pour les deux services de mise à jour logicielle suivants :  

-   Windows Server Update Services (WSUS), qui configure des paramètres tels que les définitions de produit, les classifications et les paramètres en amont.  

-   WSUS Synchronization Manager, qui demande la synchronisation à un serveur WSUS en amont ou Microsoft Update.  

Le [compte d’installation du système de site](#site-system-installation-account) peut installer les composants des mises à jour logicielles, mais il ne peut pas exécuter des fonctions de mise à jour logicielle sur le point de mise à jour logicielle. Si vous ne pouvez pas utiliser le compte d’ordinateur du serveur de site pour cette fonctionnalité parce que le point de mise à jour logicielle se trouve dans une forêt non approuvée, vous devez spécifier ce compte en complément du compte d’installation du système de site.  

Ce compte doit être celui d’un administrateur local de l’ordinateur où vous installez WSUS. Il doit également faire partie du groupe **Administrateurs de WSUS** local.  

Pour plus d’informations, consultez [Planifier les mises à jour logicielles](/sccm/sum/plan-design/plan-for-software-updates).


### <a name="source-site-account"></a>Compte du site source  

 Le processus de migration utilise le **compte de site source** pour accéder au fournisseur SMS du site source. Ce compte nécessite des autorisations en **Lecture** vers les objets de site du site source pour collecter des données pour les tâches de migration.  

 Si vous disposez de points de distribution Configuration Manager 2007 ou de sites secondaires avec des points de distribution colocalisés, et si vous souhaitez les mettre à niveau vers des points de distribution Configuration Manager (Current Branch), ce compte doit également disposer des autorisations **Supprimer** pour la classe **Site**. Cette autorisation permet de supprimer le point de distribution du site Configuration Manager 2007 pendant la mise à niveau.  

> [!NOTE]  
>  Le compte de site source et le [compte de base de données du site source](#source-site-database-account) sont répertoriés sous **Gestionnaire de migration** dans le nœud **Comptes** de l’espace de travail **Administration**, dans la console Configuration Manager.  

 Pour plus d’informations, consultez [Faire migrer des données entre des hiérarchies](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Compte de base de données du site source  

 Le processus de migration utilise le **compte de base de données du site source** pour accéder à la base de données SQL Server du site source. Pour collecter des données à partir de la base de données SQL Server du site source, le compte de base de données du site source doit disposer des autorisations **Lecture** et **Exécution** sur la base de données SQL Server du site source.  

 Si vous utilisez le compte d’ordinateur Configuration Manager (Current Branch), vérifiez que toutes les conditions suivantes sont remplies pour ce compte :  
   
 - Il est membre du groupe de sécurité **Utilisateurs du modèle COM distribué** dans le domaine où se trouve le site Configuration Manager 2007.  
 - Il est membre du groupe de sécurité **Administrateurs SMS**.  
 - Il dispose de l’autorisation **Lecture** sur tous les objets Configuration Manager 2007.  

> [!NOTE]  
>  Le compte de site source et le [compte de base de données du site source](#source-site-database-account) sont répertoriés sous **Gestionnaire de migration** dans le nœud **Comptes** de l’espace de travail **Administration**, dans la console Configuration Manager.  

 Pour plus d’informations, consultez [Faire migrer des données entre des hiérarchies](https://docs.microsoft.com/en-us/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Compte de jonction de domaine de séquence de tâches 

 L’installation de Windows utilise le **compte de jonction de domaine de séquence de tâches** pour joindre à un domaine un ordinateur à partir duquel une image vient d’être créée. Ce compte est exigé par l’étape [Joindre le domaine ou le groupe de travail](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup) de la séquence de tâches, avec l’option **Joindre un domaine**. Ce compte peut également être configuré avec l’étape [Appliquer les paramètres réseau](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyNetworkSettings), mais celle-ci n’est pas obligatoire.  

 Ce compte exige le droit **Jonction de domaine** dans le domaine cible.  

> [!TIP]  
>  Créez un compte d’utilisateur de domaine avec les autorisations minimales pour les jonctions au domaine, et utilisez-le pour toutes les séquences de tâches.  

> [!IMPORTANT]  
>  N’attribuez pas d’autorisations de connexion interactive à ce compte.  
>   
>  N’utilisez pas le compte d’accès réseau pour ce compte.  


### <a name="task-sequence-network-folder-connection-account"></a>Compte de connexion au dossier réseau de la séquence de tâches  

 Le moteur de séquence de tâches utilise le **compte de connexion à un dossier réseau de séquence de tâches** pour se connecter à un dossier partagé sur le réseau. Ce compte est exigé par l’étape [Connexion à un dossier réseau](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder) de la séquence de tâches.  

 Ce compte nécessite les autorisations permettant d'accéder au dossier partagé spécifié. Il doit s’agir d’un compte d’utilisateur de domaine.  

> [!TIP]  
>  Créez un compte d’utilisateur de domaine avec des autorisations minimales pour accéder aux ressources réseau nécessaires, et utilisez-le pour toutes les séquences de tâches.  

> [!IMPORTANT]  
>  N’attribuez pas d’autorisations de connexion interactive à ce compte.  
>   
>  N’utilisez pas le compte d’accès réseau pour ce compte.  


### <a name="task-sequence-run-as-account"></a>Compte d’identification de la séquence de tâches  

 Le moteur de séquence de tâches utilise le **compte d’identification de la séquence de tâches** pour exécuter des lignes de commande avec des informations d’identification autres que celles du compte système local. Ce compte est exigé par l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) de la séquence de tâches, avec l’option **Exécuter cette étape en tant que compte suivant**.  

 Configurez le compte pour qu’il dispose des autorisations minimales permettant d’exécuter la ligne de commande que vous spécifiez dans la séquence de tâches. Le compte exige des droits de connexion interactive. En outre, il exige généralement la possibilité d’installer des logiciels et d’accéder aux ressources du réseau.  

> [!IMPORTANT]  
>  N’utilisez pas le compte d’accès réseau pour ce compte.  
>   
>  Ne configurez jamais le compte comme un administrateur de domaine.  
>   
>  Ne configurez jamais de profils itinérants pour ce compte. Quand la séquence de tâches s’exécute, elle télécharge le profil itinérant du compte. Le profil devient alors accessible sur l’ordinateur local.  
>   
>  Limitez la portée du compte. Par exemple, créez un compte d’identification différent pour chaque séquence de tâches. Si un compte est compromis, seuls les ordinateurs clients auxquels ce compte a accès sont compromis.  
>   
>  Si la ligne de commande nécessite un accès administratif sur l’ordinateur, créez un compte d’administrateur local réservé à ce compte, sur tous les ordinateurs qui exécutent la séquence de tâches. Supprimez le compte lorsque vous n’en avez plus besoin.  

