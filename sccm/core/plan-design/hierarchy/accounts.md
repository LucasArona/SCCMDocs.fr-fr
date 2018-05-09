---
title: Comptes utilisés
titleSuffix: Configuraton Manager
description: Identifier et gérer les groupes Windows ainsi que les comptes dans System Center Configuration Manager.
ms.date: 2/9/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b2ca81115207db66a39d2aeb5e07740ae259d54c
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="accounts-used-in-system-center-configuration-manager"></a>Comptes utilisés dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations suivantes pour identifier les groupes Windows et les comptes utilisés dans System Center Configuration Manager, savoir comment ils sont utilisés et connaître les exigences associées.  

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a>Groupes Windows créés et utilisés par Configuration Manager  
 Configuration Manager crée automatiquement et, très souvent, gère automatiquement les groupes Windows suivants :  

> [!NOTE]  
>  Lorsque que Configuration Manager crée un groupe sur un ordinateur qui est membre d'un domaine, ce groupe est un groupe de sécurité local. Si l'ordinateur est un contrôleur de domaine, ce groupe est un groupe de domaine local qui est partagé entre tous les contrôleurs de domaine du domaine.  


### <a name="configmgrcollectedfilesaccess"></a>ConfigMgr_CollectedFilesAccess  
Configuration Manager utilise ce groupe pour autoriser la consultation des fichiers collectés par l’inventaire logiciel.  

Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur le serveur de site principal.<br /><br /> Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement.|  
|Adhésion|Configuration Manager gère automatiquement l'appartenance au groupe. Les membres incluent les utilisateurs administratifs qui disposent de l'autorisation **Afficher les fichiers collectés** pour l'objet sécurisable **Regroupement** depuis un rôle de sécurité attribué.|  
|Autorisations|Par défaut, ce groupe dispose de l'autorisation **Read** pour le dossier suivant sur le serveur de site : **%path%\Microsoft Configuration Manager\sinv.box\FileCol**.|  

### <a name="configmgrdviewaccess"></a>ConfigMgr_DViewAccess  
 Ce groupe est un groupe de sécurité local créé par Configuration Manager sur le serveur de base de données du site ou le serveur réplica de base de données. Il n’est pas utilisé actuellement, mais est réservé à un usage ultérieur.  

### <a name="configmgr-remote-control-users"></a>Utilisateurs du contrôle à distance ConfigMgr  
 Les outils de contrôle à distance de Configuration Manager utilisent ce groupe pour stocker les comptes et les groupes que vous configurez dans la liste Observateurs autorisés qui est attribuée à chaque client.  

 Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur le client Configuration Manager, lorsque le client reçoit une stratégie qui active les outils de contrôle à distance.<br /><br /> Lorsque vous désactivez les outils de contrôle à distance pour un client, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement sur chaque ordinateur client.|  
|Adhésion|Par défaut, ce groupe ne contient aucun membre. Lorsque vous ajoutez des utilisateurs à la liste Observateurs autorisés, ils sont automatiquement ajoutés à ce groupe.<br /><br /> Vous pouvez utiliser la liste Observateurs autorisés pour gérer l’appartenance à ce groupe au lieu d’y ajouter directement des utilisateurs ou des groupes.<br /><br /> En plus d’être un observateur autorisé, un utilisateur administratif doit disposer de l’autorisation **Contrôle à distance** sur l’objet **Regroupement**. Vous pouvez attribuer cette autorisation à l'aide du rôle de sécurité Opérateur d'outils à distance.|  
|Autorisations|Par défaut, ce groupe ne possède pas d’autorisations sur les emplacements de l’ordinateur. Il ne sert qu’à contenir la liste Observateurs autorisés.|  

### <a name="sms-admins"></a>Administrateurs SMS  
 Configuration Manager utilise ce groupe pour autoriser l’accès au fournisseur SMS, via Windows Management Instrumentation (WMI). L’accès au fournisseur SMS est requis pour afficher et modifier des objets dans la console Configuration Manager.  

> [!NOTE]  
>  La configuration de l'administration basée sur les rôles d'un utilisateur administratif détermine quels objets celui-ci peut consulter et gérer, lorsqu'il utilise la console Configuration Manager.  

 Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur chaque ordinateur qui dispose d’un fournisseur SMS.<br /><br /> Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement.|  
|Adhésion|Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, chaque utilisateur administratif d'une hiérarchie et le compte d'ordinateur du serveur de site sont membres du groupe Administrateurs SMS sur chaque ordinateur du fournisseur SMS d'un site.|  
|Autorisations|La définition des autorisations et des droits des administrateurs SMS s'effectue dans le composant logiciel enfichable MMC Contrôle WMI. Par défaut, les autorisations **Enable Account** et **Remote Enable** sont accordées au groupe Administrateurs SMS sur l'espace de noms Root\SMS. Les utilisateurs authentifiés disposent des autorisations **Méthodes d’exécution**, **Écriture fournisseur** et **Activer le compte**.<br /><br /> Les administrateurs qui utiliseront une console Configuration Manager distante doivent posséder des autorisations DCOM d'activation à distance à la fois sur le serveur de site et sur l'ordinateur du fournisseur SMS. Il est recommandé d'accorder ces droits aux Administrateurs SMS pour simplifier l'administration plutôt que d'accorder ces droits directement aux utilisateurs ou groupes. Pour plus d'informations, consultez la section [Configurer les autorisations DCOM pour les consoles Configuration Manager distantes](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) dans l’article [Modifier votre infrastructure System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).|  

### <a name="smssitesystemtositeserverconnectionmpltsitecode"></a>SMS_SiteSystemToSiteServerConnection_MP_&lt;code_site\>  
 Les points de gestion Configuration Manager qui sont distants du serveur de site utilisent ce groupe pour se connecter à la base de données du site. Ce groupe fournit un accès au point de gestion pour les dossiers Boîte de réception sur le serveur de site et la base de données du site.  

 Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur chaque ordinateur qui dispose d’un fournisseur SMS.<br /><br /> Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement.|  
|Adhésion|Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, l'appartenance inclut les comptes d'ordinateur des ordinateurs distants qui disposent d'un point de gestion pour le site.|  
|Autorisations|Par défaut, ce groupe dispose des autorisations **Lecture**, **Lecture et exécution** et **Affichage du contenu du dossier** pour le dossier **%path%\Microsoft Configuration Manager\inboxes** sur le serveur de site. Ce groupe dispose de l’autorisation supplémentaire **Écriture** sur les sous-dossiers de **inboxes** dans lesquels le point de gestion écrit les données client.|  

### <a name="smssitesystemtositeserverconnectionsmsprovltsitecode"></a>SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;code_site\>  
 Les ordinateurs fournisseurs SMS Configuration Manager qui sont distants du serveur de site utilisent ce groupe pour se connecter à celui-ci.  

 Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur le serveur de site.<br /><br /> Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement.|  
|Adhésion|Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, l’appartenance comprend le compte d’ordinateur ou le compte d’utilisateur de domaine utilisé pour se connecter au serveur de site depuis chaque ordinateur distant ayant installé un fournisseur SMS pour le site.|  
|Autorisations|Par défaut, ce groupe dispose des autorisations **Lecture**, **Lecture et exécution** et **Affichage du contenu du dossier** pour le dossier **%path%\Microsoft Configuration Manager\inboxes** sur le serveur de site. Ce groupe dispose de l’autorisation supplémentaire **Écriture** ou des autorisations **Écriture** et **Modifier** sur les sous-dossiers de **inboxes** auxquels le fournisseur SMS doit avoir accès.<br /><br /> Ce groupe dispose des autorisations **Lecture**, **Lecture et exécution**, **Affichage du contenu du dossier**, **Écriture** et **Modification** pour les dossiers situés sous **%path%\Microsoft Configuration Manager\OSD\boot** et **Lecture** pour les dossiers situés sous **%path%\Microsoft Configuration Manager\OSD\Bin** sur le serveur de site.|  

### <a name="smssitesystemtositeserverconnectionstatltsitecode"></a>SMS_SiteSystemToSiteServerConnection_Stat_&lt;code_site\>  
 Le Gestionnaire de répartition de fichiers sur les ordinateurs de système de site distants Configuration Manager utilise ce groupe pour se connecter au serveur de site.  

 Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur le serveur de site.<br /><br /> Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement.|  
|Adhésion|Configuration Manager gère automatiquement l'appartenance au groupe. Par défaut, l'appartenance comprend le compte d'ordinateur ou le compte d'utilisateur de domaine utilisé pour se connecter au serveur de site depuis chaque ordinateur de système de site distant qui exécute le Gestionnaire de répartition de fichiers.|  
|Autorisations|Par défaut, ce groupe dispose des autorisations **Lecture**, **Écriture et exécution** et **Affichage du contenu du dossier** sur le dossier **%path%\Microsoft Configuration Manager\inboxes** et ses sous-dossiers sur le serveur de site. Ce groupe dispose des autorisations supplémentaires **Écriture** et **Modifier** sur le dossier **%path%\Microsoft Configuration Manager\inboxes\statmgr.box** sur ce serveur de site.|  

### <a name="smssitetositeconnectionltsitecode"></a>SMS_SiteToSiteConnection_&lt;code_site\>  
 Configuration Manager utilise ce groupe pour activer la réplication de fichiers entre les sites d’une hiérarchie. Pour chaque site distant qui transfère directement des fichiers vers ce site, ce groupe contient les comptes configurés en tant que **compte de réplication de fichiers**.  

 Le tableau suivant répertorie des détails supplémentaires pour ce groupe :  

|Détail|Plus d'informations|  
|------------|----------------------|  
|Type et emplacement|Ce groupe est un groupe de sécurité local créé sur le serveur de site.|  
|Adhésion|Lorsque vous installez un nouveau site en tant qu’enfant d’un autre site, Configuration Manager ajoute automatiquement le compte de l’ordinateur du nouveau site au groupe situé sur le serveur de site parent. Configuration Manager ajoute également le compte d’ordinateur du site parent au groupe sur le serveur de site. Si vous spécifiez un autre compte pour les transferts de fichiers, ajoutez ce compte à ce groupe sur le serveur de site de destination.<br /><br /> Lorsque vous désinstallez un site, ce groupe n’est pas supprimé automatiquement. Il doit être supprimé manuellement.|  
|Autorisations|Par défaut, ce groupe dispose du **contrôle intégral** pour le dossier **%path%\Microsoft Configuration Manager\inboxes\despoolr.box\receive** .|  

## <a name="accounts-that-configuration-manager-uses"></a>Comptes utilisés par Configuration Manager  
 Vous pouvez utiliser les comptes suivants pour Configuration Manager.  

### <a name="active-directory-group-discovery-account"></a>Compte de découverte de groupes Active Directory  
 Le **compte de découverte de groupes Active Directory** permet de détecter les groupes de sécurité locaux, globaux et universels, les membres de ces groupes et les membres des groupes de distribution à partir des emplacements spécifiés dans Active Directory Domain Services. Les groupes de distribution ne sont pas découverts en tant que ressources de groupe.  

 Ce compte peut être un compte d'ordinateur du serveur de site qui exécute la découverte ou un compte d'utilisateur Windows. Celui-ci doit disposer de l'autorisation d'accès **Lecture** aux emplacements Active Directory spécifiés pour cette découverte.  

### <a name="active-directory-system-discovery-account"></a>Compte de découverte de systèmes Active Directory  
 Le **compte de découverte de systèmes Active Directory** est utilisé pour détecter des ordinateurs partir des emplacements spécifiés dans les services de domaine Active Directory.  

 Ce compte peut être un compte d'ordinateur du serveur de site qui exécute la découverte ou un compte d'utilisateur Windows. Celui-ci doit disposer de l'autorisation d'accès **Lecture** aux emplacements Active Directory spécifiés pour cette découverte.  

### <a name="active-directory-user-discovery-account"></a>Compte de découverte d'utilisateurs Active Directory  
 Le **compte de découverte d’utilisateurs Active Directory** est utilisé pour détecter des comptes d’utilisateur partir des emplacements spécifiés dans les services de domaine Active Directory.  

 Ce compte peut être un compte d'ordinateur du serveur de site qui exécute la découverte ou un compte d'utilisateur Windows. Celui-ci doit disposer de l'autorisation d'accès **Lecture** aux emplacements Active Directory spécifiés pour cette découverte.  

### <a name="active-directory-forest-account"></a>Compte de forêt Active Directory  
 Le **compte de forêt Active Directory** est utilisé pour découvrir l’infrastructure de réseau à partir de forêts Active Directory. Les sites d’administration centrale et les sites principaux l’utilisent également pour publier des données dans les services AD DS d’une forêt.  

> [!NOTE]  
>  Les sites secondaires utilisent toujours le compte d'ordinateur du serveur de site secondaire pour publier dans Active Directory.  

> [!NOTE]  
>  Le Compte de forêt Active Directory doit être un compte global utilisé pour détecter des forêts non approuvées et publier des données dans celles-ci. Si vous n’utilisez pas le compte d’ordinateur du serveur de site, vous ne pouvez sélectionner qu’un compte global.  

 Ce compte doit disposer des autorisations de **Lecture** pour chaque forêt Active Directory dont vous souhaitez découvrir l'infrastructure réseau.  

 Ce compte doit disposer des autorisations **Contrôle intégral** pour le conteneur Gestion du système et tous ses objets enfants dans chaque forêt Active Directory où vous souhaitez publier les données de site.  

### <a name="asset-intelligence-synchronization-point-proxy-server-account"></a>Compte du serveur proxy du point de synchronisation Asset Intelligence  
 Le point de synchronisation Asset Intelligence utilise le **compte du serveur proxy du point de synchronisation Asset Intelligence** pour accéder à Internet via un serveur proxy ou un pare-feu qui exige un accès authentifié.  

> [!IMPORTANT]  
>  Spécifiez un compte qui dispose des autorisations minimales pour le serveur proxy requis ou le pare-feu.  

### <a name="certificate-registration-point-account"></a>Compte de point d'enregistrement de certificat  
 Le **compte du point d'enregistrement du certificat** connecte le point d'enregistrement du certificat à la base de données Configuration Manager. Le compte d’ordinateur du serveur du point d’enregistrement de certificat est utilisé par défaut, mais vous pouvez configurer un compte d’utilisateur à la place. Chaque fois que le point d'enregistrement de certificat est dans un domaine non approuvé du serveur de site, vous devez spécifier un compte d'utilisateur. Ce compte ne requiert qu’un accès en **Lecture** sur la base de données du site, car le système de messages d’état gère les tâches d’écriture.  

### <a name="capture-operating-system-image-account"></a>Compte Capturer l'image du système d'exploitation  
 Configuration Manager utilise le **compte Capturer l’image du système d’exploitation** pour accéder au dossier qui stocke les images capturées lorsque vous déployez des systèmes d’exploitation. Ce compte est requis si vous ajoutez l'étape **Capturer l'image du système d'exploitation** à la séquence de tâches.  

 Le compte doit disposer d'autorisations en **Lecture** et en **Écriture** sur le partage réseau sur lequel l'image capturée est stockée.  

 Si le mot de passe du compte est modifié dans Windows, vous devez mettre à jour la séquence de tâches avec le nouveau mot de passe. Le client Configuration Manager reçoit le nouveau mot de passe quand il télécharge la stratégie du client.  

 Si vous utilisez ce compte, vous pouvez créer un compte d'utilisateur de domaine avec des autorisations minimales pour accéder aux ressources réseau nécessaires et l'utiliser pour tous les comptes de séquence de tâches.  

> [!IMPORTANT]  
>  N’attribuez pas d’autorisations d’ouverture de session interactive à ce compte.  
>   
>  N'utilisez pas le compte d'accès réseau pour ce compte.  

### <a name="client-push-installation-account"></a>Compte d'installation poussée du client  
 Le **compte d’installation push du client** est utilisé pour se connecter à des ordinateurs et installer le logiciel client Configuration Manager si vous déployez des clients via l’installation push du client. Si ce compte n'est pas spécifié, c'est le compte du serveur de site qui est utilisé pour installer le logiciel client.  

 Ce compte doit être membre du groupe **Administrateurs** local sur les ordinateurs où le logiciel client Configuration Manager doit être installé. Il ne nécessite pas de droits **Administrateur de domaine**.  

 Vous pouvez spécifier un ou plusieurs comptes d'installation Push du client, que Configuration Manager teste successivement jusqu'à ce que l'un d'eux fonctionne.  

> [!TIP]  
>  Pour améliorer la coordination des mises à jour de comptes dans des déploiements Active Directory étendus, créez un compte avec un autre nom, puis ajoutez le nouveau compte à la liste des comptes d'installation Push du client dans Configuration Manager. Laissez suffisamment de temps aux services de domaine Active Directory pour répliquer le nouveau compte, puis supprimez l'ancien compte de Configuration Manager et des services de domaine Active Directory.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte le droit d’ouvrir une session locale.  

### <a name="enrollment-point-connection-account"></a>Compte de connexion du point d'inscription  
 Le **compte de connexion du point d'inscription** permet de connecter le point d'inscription à la base de données Configuration Manager. Le compte d’ordinateur du point d’inscription est utilisé par défaut, mais vous pouvez configurer un compte d’utilisateur à la place. Chaque fois que le point d'inscription est dans un domaine non approuvé à partir du serveur de site, vous devez spécifier un compte d'utilisateur. Ce compte requiert un accès en **Lecture** et en **Écriture** à la base de données du site.  

### <a name="exchange-server-connection-account"></a>Compte de connexion Exchange Server  
 Le **compte de connexion du serveur Exchange Server** connecte le serveur de site à l’ordinateur Exchange Server spécifié pour rechercher et gérer des appareils mobiles qui se connectent à Exchange Server. Ce compte nécessite des applets de commande PowerShell Exchange qui fournissent les autorisations requises pour l'ordinateur Exchange Server. Pour plus d’informations sur cette solution, consultez [Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

### <a name="exchange-server-connector-proxy-server-account"></a>Compte du serveur proxy du connecteur Exchange Server  
 Le connecteur Exchange Server utilise le **compte du serveur proxy du connecteur Exchange Server** pour accéder à Internet via un serveur proxy ou un pare-feu qui exige un accès authentifié.  

> [!IMPORTANT]  
>  Spécifiez un compte qui dispose des autorisations minimales pour le serveur proxy requis ou le pare-feu.  

### <a name="management-point-connection-account"></a>Compte de connexion du point de gestion  
 Le **compte de connexion du point de gestion** permet de connecter le point de gestion à la base de données de site Configuration Manager pour permettre l’envoi et la récupération d’informations pour les clients. Le compte d’ordinateur du point de gestion est utilisé par défaut, mais vous pouvez configurer un compte d’utilisateur à la place. Chaque fois que le point de gestion est dans un domaine non approuvé à partir du serveur de site, vous devez spécifier un compte d'utilisateur.  

 Créez le compte comme un compte doté de droits limités, compte local sur l'ordinateur qui exécute Microsoft SQL Server.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations d’ouverture de session interactive.  

### <a name="multicast-connection-account"></a>Compte de connexion multidiffusion  
 Les points de distribution configurés pour la multidiffusion utilisent le **compte de connexion multidiffusion** pour lire les informations de la base de données de site. Le compte d’ordinateur du point de distribution est utilisé par défaut, mais vous pouvez configurer un compte d’utilisateur à la place. Chaque fois que la base de données de site est dans une forêt non approuvée, vous devez spécifier un compte d'utilisateur. Par exemple, si votre centre de données dispose d'un réseau de périmètre dans une forêt autre que celle du serveur de site et de la base de données du site, vous pouvez utiliser ce compte pour lire les informations sur la multidiffusion à partir de la base de données du site.  

 Si vous créez ce compte, créez-le en tant que compte local doté de droits limités sur l’ordinateur qui exécute Microsoft SQL Server.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations d’ouverture de session interactive.  

### <a name="network-access-account"></a>Compte d'accès au réseau  
 Les ordinateurs clients utilisent le **compte d’accès au réseau** lorsqu’ils ne peuvent pas utiliser leur compte d’ordinateur local pour accéder au contenu sur les points de distribution. Par exemple, cela s'applique aux clients du groupe de travail et aux ordinateurs de domaines non approuvés. Ce compte peut également être utilisé pendant le déploiement du système d’exploitation, si l’ordinateur qui installe le système d’exploitation n’a pas encore un compte d’ordinateur sur le domaine.  

> [!NOTE]  
>  Le compte d’accès au réseau n’est jamais utilisé comme contexte de sécurité pour exécuter des applications et des programmes, installer des mises à jour logicielles ou exécuter des séquences de tâches. Il n’est utilisé que pour accéder aux ressources du réseau.  

 Accordez à ce compte les autorisations minimales appropriées sur le contenu dont le client a besoin pour accéder au logiciel. Le compte doit disposer du droit **Accéder à cet ordinateur à partir du réseau** sur le point de distribution ou d'un autre serveur sur lequel se trouve le contenu du package. Vous pouvez configurer jusqu’à 10 comptes d’accès réseau par site.  

> [!WARNING]  
>  Lorsque Configuration Manager tente d’utiliser le compte nomordinateur$ pour télécharger le contenu et qu’il n’y parvient pas, il essaie automatiquement de réutiliser le compte d’accès réseau, même s’il a préalablement fait une tentative qui a échoué.  

 Créez le compte dans n’importe quel domaine fournissant l’accès nécessaire aux ressources. Le compte d'accès réseau doit toujours inclure un nom de domaine. La sécurité directe n’est pas prise en charge pour ce compte. Si vous disposez de points de distribution dans plusieurs domaines, créez le compte dans un domaine approuvé.  

> [!TIP]  
>  Pour éviter les verrouillages de compte, ne modifiez pas le mot de passe d'un compte d'accès réseau existant. Au lieu de cela, créez un compte et configurez-le dans Configuration Manager. Après un délai suffisant pendant lequel tous les clients ont reçu les informations du nouveau compte, supprimez l'ancien compte des dossiers partagés du réseau et supprimez le compte.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations d’ouverture de session interactive.
>   
>  N'accordez pas à ce compte le droit de joindre les ordinateurs au domaine. Si vous devez joindre les ordinateurs au domaine au cours d'une séquence de tâches, utilisez le compte de jonction de domaine de l'Éditeur de séquence de tâches.  

### <a name="package-access-account"></a>Compte d'accès au package  
 Un **compte d’accès au package** vous permet de définir des autorisations NTFS pour spécifier les utilisateurs et les groupes d’utilisateurs autorisés à accéder à un dossier de package sur des points de distribution. Par défaut, Configuration Manager n’accorde cet accès qu’aux comptes d’accès générique **Utilisateurs** et **Administrateurs**. Vous pouvez contrôler l’accès des ordinateurs clients à l’aide d’autres comptes ou groupes Windows. Les appareils mobiles n’utilisent pas les comptes d’accès au package, car ils récupèrent toujours le contenu du package de façon anonyme.  

 Par défaut, lorsque Configuration Manager crée le partage du package sur un point de distribution, il accorde un accès en **Lecture** au groupe **Utilisateurs** local et un **Contrôle intégral** au groupe **Administrateurs** local. Les autorisations requises dépendent du package. Si vous avez des clients dans des groupes de travail ou dans des forêts non approuvées, ceux-ci utiliseront le compte d'accès réseau pour accéder au contenu du package. Assurez-vous que le compte d'accès réseau bénéficie d'autorisations sur le package à l'aide des comptes d'accès au package définis.  

 Utilisez des comptes dans un domaine susceptible d'accéder aux points de distribution. Si vous créez ou modifiez le compte après la création du package, vous devez redistribuer ce dernier. La mise à jour du package ne modifie pas les autorisations NTFS sur le package.  

 Il est inutile d'ajouter le compte d'accès réseau comme un compte d'accès au package, car l'appartenance au groupe Utilisateurs l'ajoute automatiquement. Le fait de restreindre le compte d'accès au package au compte d'accès réseau uniquement n'empêche pas les clients d'accéder au package.  

### <a name="reporting-services-point-account"></a>Compte du point de Reporting Services  
 SQL Server Reporting Services utilise le **compte du point de Reporting Services** pour récupérer les données des rapports Configuration Manager à partir de la base de données de site. Le compte d'utilisateur Windows et le mot de passe que vous spécifiez sont chiffrés et stockés dans la base de données SQL Server Reporting Services.  
>[!NOTE]
>Le compte que vous spécifiez doit avoir des autorisations Connexion locale sur l’ordinateur hébergeant la base de données Reporting Services.

### <a name="remote-tools-permitted-viewer-accounts"></a>Comptes d'observateurs autorisés des outils de contrôle à distance  
 Les comptes que vous spécifiez en tant qu' **Observateurs autorisés** pour le contrôle à distance sont une liste d'utilisateurs autorisés à utiliser la fonctionnalité Outils de contrôle à distance sur les clients.  

### <a name="site-system-installation-account"></a>Compte d'installation du système de site  
 Le serveur de site utilise le **compte d’installation du système de site** pour installer, réinstaller, désinstaller et configurer des systèmes de site. Si vous configurez le système de site afin qu’il établisse des connexions à ce système de site, Configuration Manager utilise également ce compte pour extraire les données de l’ordinateur du système de site après l’installation du système de site et de tous les rôles de ce dernier. Chaque système de site peut avoir un autre compte d’installation du système de site, mais vous ne pouvez configurer qu’un compte d’installation du système de site pour gérer tous les rôles de système de site sur ce système de site.  

 Ce compte nécessite des autorisations d’administrateur locales sur les systèmes de site que les administrateurs installeront et configureront. De plus, ce compte doit disposer du droit **Accéder à cet ordinateur à partir du réseau** dans la stratégie de sécurité sur les systèmes de site que les administrateurs installeront et configureront.  

> [!TIP]  
>  Si vous avez plusieurs contrôleurs de domaine et si ces comptes sont utilisés dans plusieurs domaines, vérifiez qu’ils ont été répliqués avant de configurer le système de site.  
>   
>  Lorsque vous spécifiez un compte local sur chaque système de site à gérer, cette configuration est plus sécurisée que l'utilisation de comptes de domaine, car elle limite les dommages que les personnes malveillantes peuvent provoquer en cas de compromission du compte. Toutefois, les comptes de domaine sont plus faciles à gérer. Examinez le compromis entre sécurité et efficacité d’administration.  

### <a name="smtp-server-connection-account"></a>Compte de connexion au serveur SMTP  
 Le serveur de site utilise le **compte de connexion au serveur SMTP** pour envoyer des alertes par courrier électronique quand le serveur SMTP requiert un accès authentifié.  

> [!IMPORTANT]  
>  Spécifiez un compte qui dispose des autorisations minimales pour envoyer des courriers électroniques.  

### <a name="software-update-point-connection-account"></a>Compte de connexion de point de mise à jour logicielle  
 Le serveur de site utilise le **compte de connexion de point de mise à jour logicielle** pour les deux services de mise à jour logicielle suivants :  

-   Windows Server Update Services (WSUS) Configuration Manager, qui configure des paramètres tels que les définitions de produit, les classifications et les paramètres en amont.  

-   WSUS Synchronization Manager, qui demande la synchronisation à un serveur WSUS en amont ou Microsoft Update.  

Le compte d’installation du système de site peut installer les composants des mises à jour logicielles, mais il ne peut pas exécuter des fonctions de mise à jour logicielle sur le point de mise à jour logicielle. Si vous ne pouvez pas utiliser le compte d'ordinateur du serveur de site pour cette fonctionnalité car le point de mise à jour logicielle se trouve dans une forêt non approuvée, vous devez spécifier ce compte en complément du compte d'installation du système de site.  

Ce compte doit être un administrateur local sur l’ordinateur où WSUS est installé. Il doit également faire partie du groupe Administrateurs de WSUS local.  

### <a name="software-update-point-proxy-server-account"></a>Compte du serveur proxy du point de mise à jour logicielle  
 Le point de mise à jour logicielle utilise le **compte du serveur proxy du point de mise à jour logicielle** pour accéder à Internet via un serveur proxy ou un pare-feu qui requiert un accès authentifié.  

> [!IMPORTANT]  
>  Spécifiez un compte qui dispose des autorisations minimales pour le serveur proxy requis ou le pare-feu.  

### <a name="source-site-account"></a>Compte du site source  
 Le processus de migration utilise le **compte de site source** pour accéder au fournisseur SMS du site source. Ce compte nécessite des autorisations en **Lecture** vers les objets de site du site source pour collecter des données pour les tâches de migration.  

 Si vous mettez à niveau les points de distribution Configuration Manager 2007 ou les sites secondaires ayant des points de distribution au même emplacement vers des points de distribution System Center Configuration Manager, ce compte doit également disposer d'autorisations en **Suppression** sur la classe **Site** pour pouvoir supprimer le point de distribution du site Configuration Manager 2007 au cours de la mise à niveau.  

> [!NOTE]  
>  Le compte de site source et le compte de base de données du site source sont identifiés comme **Gestionnaire de migration** dans le nœud **Comptes** de l’espace de travail **Administration** dans la console Configuration Manager.  

### <a name="source-site-database-account"></a>Compte de base de données du site source  
 Le processus de migration utilise le **compte de base de données du site source** pour accéder à la base de données SQL Server du site source. Pour collecter des données à partir de la base de données SQL Server du site source, le compte de base de données du site source doit disposer des autorisations **Lecture** et **Exécution** sur la base de données SQL Server du site source.  

> [!NOTE]  
>  Si vous utilisez le compte d'ordinateur System Center Configuration Manager, assurez-vous que toutes les conditions suivantes sont remplies pour ce compte :  
>   
> -   Il est membre du groupe de sécurité **Utilisateurs du modèle COM distribué** dans le domaine où le site Configuration Manager 2007 réside.  
> -   Il est membre du groupe de sécurité **Administrateurs SMS** .  
> -   Il possède l’autorisation **Lecture** sur tous les objets de Configuration Manager 2007.  

> [!NOTE]  
>  Le compte du site source et le compte de base de données du site source sont identifiés comme **Gestionnaire de migration** dans le nœud **Comptes** de l'espace de travail **Administration** dans la console Configuration Manager.  

### <a name="task-sequence-editor-domain-joining-account"></a>Compte de jonction de domaine de l'Éditeur de séquence de tâches  
 Le **compte de jonction de domaine de l’Éditeur de séquence de tâches** est utilisé dans une séquence de tâches pour joindre un ordinateur nouvellement mis en image à un domaine. Il est nécessaire si vous ajoutez l'étape **Joindre le domaine ou le groupe de travail** à une séquence de tâches, puis sélectionnez l'option **Joindre un domaine**. Vous pouvez également configurer ce compte si vous ajoutez l’étape **Appliquer les paramètres réseau** à une séquence de tâches, mais cette opération n’est pas obligatoire.  

 Ce compte exige le droit **Jonction de domaine** dans le domaine que l'ordinateur doit joindre.  

> [!TIP]  
>  Si vous avez besoin de ce compte pour vos séquences de tâches, vous pouvez créer un compte d'utilisateur de domaine doté des autorisations d'accès minimales aux ressources réseau nécessaires, puis l'utiliser pour tous les comptes de séquence de tâches.  

> [!IMPORTANT]  
>  N’attribuez pas d’autorisations d’ouverture de session interactive à ce compte.  
>   
>  N'utilisez pas le compte d'accès réseau pour ce compte.  

### <a name="task-sequence-editor-network-folder-connection-account"></a>Compte de connexion à un dossier réseau de l'Éditeur de séquence de tâches  
 Une séquence de tâches utilise le **compte de connexion à un dossier réseau de l’Éditeur de séquence de tâches** pour se connecter à un dossier partagé sur le réseau. Ce compte est obligatoire si vous ajoutez l'étape **Connexion à un dossier réseau** à une séquence de tâches.  

 Ce compte nécessite les autorisations permettant d'accéder au dossier partagé spécifié. Ce doit être un compte de domaine d’utilisateur.  

> [!TIP]  
>  Si vous avez besoin de ce compte pour vos séquences de tâches, vous pouvez créer un compte d'utilisateur de domaine doté des autorisations d'accès minimales aux ressources réseau nécessaires, puis l'utiliser pour tous les comptes de séquence de tâches.  

> [!IMPORTANT]  
>  N’attribuez pas d’autorisations d’ouverture de session interactive à ce compte.  
>   
>  N'utilisez pas le compte d'accès réseau pour ce compte.  

### <a name="task-sequence-run-as-account"></a>Compte d'identification de la séquence de tâches  
 Le **compte d’identification de la séquence de tâches** est utilisé pour exécuter des lignes de commande dans des séquences de tâches avec des informations d’identification différentes de celles du compte système local. Ce compte est requis si vous ajoutez l’étape **Exécuter la ligne de commande** à une séquence de tâches, sans que la séquence s’exécute avec les autorisations du compte système local sur l’ordinateur géré.  

 Configurez le compte pour qu’il dispose des autorisations minimales permettant d’exécuter la ligne de commande spécifiée dans la séquence de tâches. Ce compte requiert des autorisations d’ouverture de session interactive et, en général, la possibilité d’installer des logiciels et d’accéder aux ressources du réseau.  

> [!IMPORTANT]  
>  N'utilisez pas le compte d'accès réseau pour ce compte.  
>   
>  Ne configurez jamais le compte comme un administrateur de domaine.  
>   
>  Ne configurez jamais de profils itinérants pour ce compte. Quand la séquence de tâches s’exécute, elle télécharge le profil itinérant du compte. Le profil devient alors accessible sur l’ordinateur local.  
>   
>  Limitez la portée du compte. Par exemple, créez différents comptes d'identification de la séquence de tâches pour chaque séquence de tâches, de sorte que, si un compte est compromis, seuls les ordinateurs clients auxquels ce compte a accès sont compromis.  
>   
>  Si la ligne de commande nécessite un accès administratif sur l’ordinateur, créez un compte d’administrateur local réservé au compte d’identification de la séquence de tâches sur tous les ordinateurs qui exécutent cette dernière. Supprimez le compte dès que vous n’en avez plus besoin.  
