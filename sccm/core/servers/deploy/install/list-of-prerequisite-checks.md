---
title: Vérifications des prérequis
titleSuffix: Configuration Manager
description: Informations de référence sur les vérifications des prérequis spécifiques pour les mises à jour de Configuration Manager.
ms.date: 12/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6a279624-ffc9-41aa-8132-df1809708dd5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fdc882d63e7bf7d3189e770f230412f17ca0b63
ms.sourcegitcommit: d36e4c7082a5144e79035dd8847c8e741fa04667
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53444652"
---
# <a name="list-of-prerequisite-checks-for-configuration-manager"></a>Liste de vérifications des prérequis pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article détaille les vérifications des prérequis qui s’exécutent lorsque vous installez ou mettez à jour Configuration Manager. Pour plus d’informations, consultez [Outil de vérification des prérequis](/sccm/core/servers/deploy/install/prerequisite-checker).  



##  <a name="BKMK_Security"></a> Droits de sécurité  


### <a name="security-rights-errors"></a>Droits de sécurité : Errors

#### <a name="administrator-rights-on-central-administration-site"></a>Droits d'administrateur sur le site d'administration centrale 
*S’applique à : site principal*

Le compte d’utilisateur qui exécute le programme d’installation de Configuration Manager dispose de droits d’**administrateur** sur le serveur du site d’administration centrale.

#### <a name="administrative-rights-on-expand-primary-site"></a>Droits d'administration sur le site principal développé 
*S’applique à : site d’administration centrale*

Lorsque vous développez un site principal en hiérarchie, le compte d’utilisateur qui exécute le programme d’installation dispose de droits d’**administrateur** sur le serveur de site principal autonome.

#### <a name="administrative-rights-on-site-system"></a>Droits d'administration sur le système de site 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Le compte d’utilisateur qui exécute le programme d’installation de Configuration Manager dispose de droits d’**administrateur** sur le serveur de site.

#### <a name="central-administration-site-server-administrative-rights-on-expand-primary-site"></a>Droits d’administration de serveur de site d’administration centrale sur le site principal développé 
*S’applique à : site d’administration centrale*

Lorsque vous développez un site principal en hiérarchie, le compte d’ordinateur du serveur de site d’administration centrale dispose de droits d’**administrateur** sur le serveur de site principal autonome.

#### <a name="connection-to-sql-server-on-central-administration-site"></a>Connexion à SQL Server sur le site d'administration centrale 
*S’applique à : site principal*

Le compte d’utilisateur qui exécute le programme d’installation de Configuration Manager sur le site principal pour joindre une hiérarchie existante détient le rôle d’**administrateur système** sur l’instance SQL Server du site d’administration centrale.

#### <a name="site-server-computer-account-administrative-rights"></a>Droits d'administration du compte d'ordinateur serveur de site 
*S’applique à : site principal, serveur de bases de données du site*

Le compte d’ordinateur serveur de site dispose de droits d’**administrateur** sur SQL Server et le point de gestion.

#### <a name="sql-server-sysadmin-rights"></a>Droits d'administrateur système SQL Server 
*S’applique à : serveur de bases de données du site*

Le compte d’utilisateur qui exécute le programme d’installation de Configuration Manager détient le rôle d’**administrateur système** sur l’instance SQL Server que vous avez sélectionnée pour l’installation de la base de données du site. Cette vérification échoue également lorsque le programme d’installation ne parvient pas à accéder à l’instance pour que SQL Server vérifie les autorisations.

#### <a name="sql-server-sysadmin-rights-for-reference-site"></a>Droits d'administrateur système SQL Server pour le site de référence 
*S’applique à : serveur de bases de données du site*

Le compte d’utilisateur qui exécute le programme d’installation de Configuration Manager détient le rôle d’**administrateur système** sur l’instance de rôle SQL Server que vous avez sélectionnée comme base de données du site de référence. Les autorisations du rôle d’**administrateur système** SQL Server sont nécessaires pour modifier la base de données de site.


### <a name="security-rights-warnings"></a>Droits de sécurité : Avertissements

#### <a name="site-system-to-sql-server-communication"></a>Communication du système de site au serveur SQL Server  
*S’applique à : site secondaire, point de gestion*

Le compte que vous avez configuré pour exécuter le service SQL Server pour l’instance de base de données du site a un nom de principal du service (SPN) valide dans Active Directory Domain Services. Inscrivez un SPN valide dans Active Directory pour prendre en charge l’authentification Kerberos.

#### <a name="sql-server-security-mode"></a>Mode de sécurité SQL Server 
*S’applique à : serveur de bases de données du site*

SQL Server est configuré pour la sécurité de l’authentification Windows.



##  <a name="BKMK_Dependencies"></a> Dépendances

### <a name="dependencies-errors"></a>Dépendances : Errors

#### <a name="active-migration-mappings-on-the-target-primary-site"></a>Mappages de migration actifs sur le site principal cible 
*S’applique à : site d’administration centrale*

Il n’existe pas de mappages de migration actifs aux sites principaux.

#### <a name="active-replica-mp"></a>Réplica de point de gestion actif 
*S’applique à : site principal*

Il existe un réplica de point de gestion actif.

#### <a name="bits-enabled"></a>Compatible BITS 
*S’applique à : point de gestion*

Le Service de transfert intelligent en arrière-plan (BITS) est installé sur le point de gestion. Cette vérification peut échouer pour l’une des raisons suivantes : 
- BITS n’est pas installé.  
- Le composant de compatibilité WMI IIS 6.0 pour IIS 7.0 n’est pas installé sur le serveur ou l’hôte IIS distant.  
- Le programme d’installation n’a pas pu vérifier les paramètres IIS distants. Les composants communs IIS ne sont pas installés sur le serveur de site.  

#### <a name="case-insensitive-collation-on-sql-server"></a>Classement insensible à la casse sur SQL Server 
*S’applique à : serveur de bases de données du site*

L’installation SQL Server utilise un classement qui ne respecte pas la casse, par exemple, **SQL_Latin1_General_CP1_CI_AS**.

#### <a name="check-existing-stand-alone-primary-site-for-version-and-site-code"></a>Déterminer la version et le code du site principal autonome 
*S’applique à : site d’administration centrale, site principal*

Le site principal que vous prévoyez de développer est un site principal autonome. Il est doté de la même version de Configuration Manager, mais vous devez installer un code de site autre que celui du site d’administration centrale.

#### <a name="check-for-incompatible-collection-references"></a>Rechercher des références de regroupement incompatibles 
*S’applique à : site d’administration centrale*

Au cours d’une mise à niveau, les regroupements font uniquement référence à des regroupements du même type.

#### <a name="client-version-on-management-point-computer"></a>Version du client sur l'ordinateur du point de gestion 
*S’applique à : point de gestion*

Vous installez le point de gestion sur un serveur dont la version du client Configuration Manager installé n’est pas différente.

#### <a name="dedicated-sql-server-instance"></a>Instance SQL Server dédiée 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Vous avez configuré une instance dédiée du serveur SQL Server pour héberger la base de données du site Configuration Manager. 

Si un autre site utilise cette instance, vous devez sélectionner une autre instance pour le nouveau site. Vous pouvez également désinstaller l’autre site ou déplacer sa base de données vers une autre instance du serveur SQL Server.

#### <a name="existing-configuration-manager-server-components-on-server"></a>Composants serveur Configuration Manager existants sur le serveur 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Un rôle de serveur de site ou de système de site n’est pas déjà installé sur le serveur sélectionné pour l’installation du site.

#### <a name="firewall-exception-for-sql-server"></a>Exception de pare-feu pour le serveur SQL Server 
*S’applique à : site d’administration centrale, site principal, site secondaire, point de gestion*

Le Pare-feu Windows est désactivé ou une exception de Pare-feu Windows pertinente existe pour SQL Server. 

Autorisez l’accès à distance à Sqlservr.exe ou aux ports TCP obligatoires. Par défaut, SQL Server écoute le port TCP 1433 et SQL Server Service Broker (SSB) utilise le port TCP 4022.

#### <a name="iis-service-running"></a>Service IIS en cours d'exécution 
*S’applique à : point de gestion, point de distribution*

IIS est installé et en cours d’exécution sur le serveur pour le point de gestion ou le point de distribution.

#### <a name="match-collation-of-expand-primary-site"></a>Reproduire le classement du site principal développé 
*S’applique à : site d’administration centrale*

Quand vous développez un site principal en hiérarchie, la base de données du site principal autonome a le même classement que celle du site d’administration centrale.

#### <a name="microsoft-remote-differential-compression-rdc-library-registered"></a>La bibliothèque RDC (compression différentielle à distance) de Microsoft est enregistrée 
*S’applique à : site d’administration centrale, site principal, site secondaire*

La bibliothèque RDC est enregistrée sur le serveur de site Configuration Manager.

#### <a name="microsoft-windows-installer"></a>Microsoft Windows Installer 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Vérifie la version de Windows Installer. 

L’échec de cette vérification signifie que le programme d’installation n’a pas pu vérifier la version ou que la version installée n’est pas conforme à la configuration minimale requise de Windows Installer 4.5.

#### <a name="minimum-net-framework-version-for-configuration-manager-console"></a>Version minimale de .NET Framework pour la console Configuration Manager 
*S’applique à : console Configuration Manager*

Microsoft .NET Framework 4.0 est installé sur l’ordinateur de la console Configuration Manager. 

#### <a name="minimum-net-framework-version-for-configuration-manager-site-server"></a>Version minimale de .NET Framework pour le serveur de site Configuration Manager 
*S’applique à : site d’administration centrale, site principal, site secondaire*

.NET Framework 3.5 est installé ou activé sur le serveur de site Configuration Manager. 

#### <a name="minimum-net-framework-version-for-sql-server-express-edition-installation-for-configuration-manager-secondary-site"></a>Version minimale de .NET Framework pour l’installation de l’édition SQL Server Express pour un site secondaire Configuration Manager 
*S’applique à : site secondaire*

.NET Framework 4.0 est installé ou activé sur le serveur de site secondaire Configuration Manager. SQL Server Express exige cette version.

#### <a name="parent-database-collation"></a>Classement de base de données parent 
*S’applique à : site principal, site secondaire*

Le classement de la base de données du site correspond à celui de la base de données du site parent. Tous les sites d'une même hiérarchie doivent utiliser le même classement de base de données.

#### <a name="primary-fqdn"></a>Nom de domaine complet principal 
*S’applique à : site d’administration centrale, site principal, site secondaire, serveur de bases de données du site*

Le nom NetBIOS de l’ordinateur correspond au nom d’hôte local dans le nom de domaine complet (FQDN).

#### <a name="required-sql-server-collation"></a>Classement SQL Server obligatoire 
*S’applique à : site d’administration centrale, site principal, site secondaire*

L’instance de SQL Server est configurée pour utiliser le classement **SQL_Latin1_General_CP1_CI_AS**. 

Si la base de données du site Configuration Manager est déjà installée, cette vérification s’y applique également. Pour plus d’informations sur le changement de vos classements d’instance et de base de données SQL Server, consultez [Prise en charge d’Unicode et du classement](https://docs.microsoft.com/sql/relational-databases/collations/collation-and-unicode-support). 

Si vous utilisez un système d’exploitation chinois et que vous avez besoin de prendre en charge GB18030, cette vérification ne s’applique pas. Pour plus d’informations sur l’activation de la prise en charge de la norme GB18030, consultez [Prise en charge internationale](/sccm/core/plan-design/hierarchy/international-support).

#### <a name="setup-source-folder"></a>Dossier source d’installation 
*S’applique à : site secondaire*

Le compte d’ordinateur du site secondaire dispose des autorisations suivantes sur le dossier source d’installation et le partage : 
- Autorisations d’accès en **lecture** sur le système de fichiers NTFS
- Autorisations d’accès en **lecteur** sur le partage 

> [!Note]  
> Si vous utilisez des partages administratifs, par exemple, C$ et D$, le compte d’ordinateur de site secondaire doit être **administrateur** sur le serveur.  

#### <a name="setup-source-version"></a>Version de la source d’installation 
*S’applique à : site secondaire*

La version de Configuration Manager dans le dossier source spécifié pour l’installation du site secondaire correspond à la version de Configuration Manager du site principal.

#### <a name="site-code-in-use"></a>Code de site en cours d'utilisation 
*S’applique à : site principal* Le code de site spécifié n’est pas déjà utilisé dans la hiérarchie Configuration Manager. Spécifiez un code de site unique pour ce site.

#### <a name="sms-provider-in-same-domain-as-site-server"></a>Fournisseur SMS dans le même domaine que le serveur de site 
*S’applique à : fournisseur SMS*

Une instance du fournisseur SMS se trouve dans le même domaine que le serveur de site.

#### <a name="sql-server-edition"></a>Édition SQL Server 
*S’applique à : serveur de bases de données du site*

SQL Server sur le site n’est pas SQL Server Express.

#### <a name="sql-server-express-on-secondary-site"></a>SQL Server Express sur le site secondaire 
*S’applique à : site secondaire*

SQL Server Express peut s’installer correctement sur le serveur de site secondaire.

#### <a name="sql-server-on-the-secondary-site-server"></a>SQL Server sur le serveur de site secondaire 
*S’applique à : site secondaire*

SQL Server est installé sur le serveur de site secondaire. Vous ne pouvez pas installer SQL Server sur un système de site distant pour un site secondaire.

> [!Warning]  
> Cette vérification s’applique quand vous indiquez au programme d’installation d’utiliser une instance existante de SQL Server.  

#### <a name="sql-server-service-running-account"></a>Compte en cours d'exécution du service SQL Server 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Le compte de connexion du service SQL Server n’est pas un compte d’utilisateur local ni **SERVICE LOCAL**. 

Configurez le service SQL Server pour utiliser un compte de domaine valide, **SERVICE RÉSEAU** ou **SYSTÈME LOCAL**.

#### <a name="sql-server-tcp-port"></a>Port TCP SQL Server 
*S’applique à : serveur de bases de données du site*

TCP est activé pour l’instance SQL Server et configuré pour utiliser un port statique.

#### <a name="sql-server-version"></a>Version SQL Server 
*S’applique à : serveur de bases de données du site*

Une version prise en charge de SQL Server est installée sur le serveur de bases de données du site spécifié. 

Pour plus d’informations, consultez [Prise en charge des versions SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).

#### <a name="asset-intelligence-synchronization-point-on-the-expanded-primary-site"></a>Point de synchronisation Asset Intelligence sur le site principal développé 
*S’applique à : site d’administration centrale*

Lorsque vous développez un site principal en hiérarchie, le rôle de point de synchronisation Asset Intelligence n’est pas installé sur le site principal autonome.

#### <a name="endpoint-protection-point-on-the-expanded-primary-site"></a>Point Endpoint Protection sur le site principal développé 
*S’applique à : site d’administration centrale*

Lorsque vous développez un site principal en hiérarchie, le rôle de point Endpoint Protection n’est pas installé sur le site principal autonome.

#### <a name="microsoft-intune-connector-on-the-expanded-primary-site"></a>Connecteur Microsoft Intune sur le site principal développé 
*S’applique à : site d’administration centrale*

Lorsque vous développez un site principal en hiérarchie, le connecteur Microsoft Intune n’est pas installé sur le site principal autonome.

#### <a name="usmt-installed"></a>Outil de migration utilisateur Windows installé 
*S’applique à : site d’administration centrale, site principal (autonome uniquement)*

Le composant Outil de migration utilisateur Windows (USMT) du Kit de déploiement et d’évaluation Windows (ADK) est installé.

#### <a name="validate-fqdn-of-sql-server"></a>Valider le nom de domaine complet de l’ordinateur SQL Server 
*S’applique à : serveur de bases de données du site*

Vous avez spécifié un nom de domaine complet valide pour l’ordinateur SQL Server.

#### <a name="verify-central-administration-site-version"></a>Vérifier la version du site d’administration centrale 
*S’applique à : site principal*

Le site d’administration centrale dispose de la même version de Configuration Manager.

#### <a name="windows-deployment-tools-installed"></a>Outils de déploiement Windows installés 
*S’applique à : fournisseur SMS*

Le composant Outils de déploiement Windows de Windows ADK est installé.

#### <a name="windows-failover-cluster"></a>Cluster de basculement Windows 
*S’applique à : serveur de site, point de gestion, point de distribution*

Le serveur doté des rôles de serveur de site, de point de gestion ou de point de distribution ne fait pas partie d’un cluster Windows.

Depuis la version 1810, le processus d’installation de Configuration Manager ne bloque plus l’installation du rôle de serveur de site sur un ordinateur ayant le rôle Windows pour le clustering de basculement. SQL Always On exige ce rôle, ce qui vous empêchait de colocaliser la base de données de site sur le serveur de site. Avec ce changement, vous pouvez créer un site à haut niveau de disponibilité avec moins de serveurs en utilisant SQL Always On et un serveur de site en mode passif. Pour plus d’informations, consultez [Options de haute disponibilité](/sccm/core/servers/deploy/configure/high-availability-options). <!--1359132-->  

#### <a name="windows-pe-installed"></a>Windows PE installé 
*S’applique à : fournisseur SMS*

L’environnement de préinstallation Windows (WinPE) de Windows ADK est installé.


### <a name="dependencies-warnings"></a>Dépendances : Avertissements

#### <a name="administrative-rights-on-distribution-point"></a>Droits d'administration sur le point de distribution 
*S’applique à : point de distribution*

Le compte d’utilisateur qui exécute le programme d’installation dispose de droits d’**administrateur** sur le point de distribution.

#### <a name="administrative-rights-on-management-point"></a>Droits d'administration sur le point de gestion 
*S’applique à : point de gestion, point de distribution*

Le compte d’ordinateur du serveur de site dispose de droits d’**administrateur** sur le point de gestion et le point de distribution.

#### <a name="administrative-share-site-system"></a>Partage administratif (système de site) 
*S’applique à : point de gestion*

Les partages administratifs obligatoires sont présents sur l’ordinateur du système de site.

#### <a name="application-compatibility"></a>Compatibilité des applications 
*S’applique à : site d’administration centrale, site principal*

Les applications actuelles sont compatibles avec le schéma d’application.

#### <a name="bits-installed"></a>Service BITS installé 
*S’applique à : point de gestion*

Le Service de transfert intelligent en arrière-plan (BITS) est installé et activé dans IIS.

#### <a name="configuration-for-sql-server-memory-usage"></a>Configuration de l'utilisation de mémoire de SQL Server 
*S’applique à : serveur de bases de données du site*

SQL Server est configuré pour une utilisation illimitée de la mémoire. Configurez la mémoire de SQL Server avec une limite maximale.

#### <a name="firewall-exception-for-sql-server-standalone-primary-site"></a>Exception de pare-feu pour SQL Server (site principal autonome) 
*S’applique à : site principal (autonome uniquement)*

Le Pare-feu Windows est désactivé ou une exception de Pare-feu Windows pertinente existe pour SQL Server. 

Autorisez l’accès à distance à Sqlservr.exe ou aux ports TCP obligatoires. Par défaut, SQL Server écoute le port TCP 1433 et Server Service Broker (SSB) utilise le port TCP 4022.

#### <a name="firewall-exception-for-sql-server-for-management-point"></a>Exception de pare-feu pour SQL Server pour le point de gestion 
*S’applique à : point de gestion*

Le Pare-feu Windows est désactivé ou une exception de Pare-feu Windows pertinente existe pour SQL Server.

#### <a name="iis-https-configuration"></a>Configuration HTTPS IIS 
*S’applique à : point de gestion, point de distribution*

Le site web IIS a des liaisons pour le protocole de communication HTTPS. 

Lorsque vous installez des rôles de site qui exigent HTTPS, configurez les liaisons de site IIS sur le serveur spécifié avec un certificat d’infrastructure à clé publique (PKI) valide.

#### <a name="microsoft-xml-core-services-60-msxml60"></a>Microsoft XML Core Services 6.0 (MSXML60) 
*S’applique à : site d’administration centrale, site principal, site secondaire, console Configuration Manager, point de gestion, point de distribution*

Vérifie que MSXML version 6.0 ou ultérieure est installé.

#### <a name="powershell-20-on-site-server"></a>PowerShell 2.0 sur le serveur de site 
*S’applique à : site principal avec connecteur Exchange*

Windows PowerShell version 2.0 ou ultérieure est installé sur le serveur de site pour le connecteur Exchange de Configuration Manager. 

#### <a name="remote-connection-to-wmi-on-secondary-site"></a>Connexion à distance à WMI sur le site secondaire 
*S’applique à : site secondaire*

Le programme d’installation ne peut pas établir une connexion à distance à WMI sur le site secondaire.

#### <a name="sql-server-process-memory-allocation"></a>Allocation de mémoire pour le processus SQL Server 
*S’applique à : serveur de bases de données du site* 

SQL Server réserve un minimum de 8 Go de mémoire au site d’administration centrale et au site principal, ainsi qu’un minimum de 4 Go de mémoire au site secondaire.

Pour plus d’informations, consultez [Comment configurer les options de mémoire à l’aide de SQL Server Management Studio](https://docs.microsoft.com/sql/database-engine/configure-windows/server-memory-server-configuration-options#how-to-configure-memory-options-using-includessmanstudiofullincludesssmanstudiofull-mdmd).

> [!NOTE]  
> Cette vérification ne s’applique pas à SQL Server Express sur un site secondaire. Cette édition est limitée à 1 Go de mémoire réservée.  

#### <a name="unsupported-site-system-os-version-for-upgrade"></a>Version de système d’exploitation de système de site non prise en charge pour la mise à niveau 
*S’applique à : site principal, site secondaire*

Des rôles de système de site autres que des points de distribution sont installés sur des serveurs exécutant Windows Server version 2012 ou ultérieure.

Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

> [!NOTE]  
> Cette vérification ne peut pas résoudre l’état des rôles de système de site installés dans Azure ou pour le stockage cloud utilisé par Microsoft Intune. Ignorez les avertissements qui concernent ces rôles et considérez-les comme des faux positifs.

#### <a name="verify-site-server-permissions-to-publish-to-active-directory"></a>Vérifier les autorisations de publication dans Active Directory du serveur de site 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Le compte d’ordinateur du serveur de site dispose des autorisations de **contrôle total** sur le conteneur **System Management** dans le domaine Active Directory. 

Pour plus d’informations, consultez [Préparer Active Directory pour la publication de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).

> [!NOTE]  
> Si vous vérifiez manuellement les autorisations, vous pouvez ignorer cet avertissement.

#### <a name="windows-remote-management-winrm-v11"></a>Windows Remote Management (WinRM) v1.1 
*S’applique à : site principal, console Configuration Manager*

WinRM 1.1 est installé sur le serveur de site principal ou sur l’ordinateur de la console Configuration Manager pour exécuter la console de gestion hors bande. 

Pour plus d’informations sur la façon de télécharger WinRM 1.1, consultez l’[article de support 936059](https://support.microsoft.com/help/936059).

#### <a name="wsus-on-site-server"></a>WSUS sur le serveur de site 
*S’applique à : site d’administration centrale, site principal*

Une version prise en charge de Windows Server Update Services (WSUS) est installée sur le serveur de site. 

Lorsque vous utilisez un point de mise à jour logicielle sur un serveur autre que le serveur de site, vous devez installer la console d’administration WSUS sur le serveur de site. Pour plus d’informations sur WSUS, consultez [Windows Server Update Services](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus) .

#### <a name="pending-configuration-item-policy-updates"></a>Mises à jour de stratégie d’élément de configuration en attente 
<!--SCCMDocs-pr issue 2814-->
*S’applique à : site principal*

Depuis la version 1806, si vous effectuez une mise à jour à partir de la version 1706 ou ultérieure, vous risquez de voir cet avertissement si vous avez de nombreux déploiements d’applications, dont au moins l’un d’entre eux nécessite une approbation. 

Vous avez deux options :  

- Ignorez l’avertissement et poursuivez la mise à jour. Cette action entraîne un traitement plus important sur le serveur de site pendant la mise à jour parce que celui-ci traite les stratégies. Vous risquez aussi de voir une charge processeur plus grande sur le point de gestion après la mise à jour.  

- Modifiez l’une des applications qui n’a aucune exigence ou des exigences de système d’exploitation spécifiques. Prétraitez une partie de la charge sur le serveur de site à ce moment-là. Consultez **objreplmgr.log**, puis surveillez le processeur sur le point de gestion. Une fois le traitement terminé, mettez à jour le site. Il y aura toujours un surplus de traitement après la mise à jour, mais moins que si vous ignorez l’avertissement avec la première option.  



##  <a name="BKMK_Requirements"></a> Configuration système requise  

### <a name="system-requirements-errors"></a>Configuration système requise : Errors

#### <a name="server-service-is-running"></a>Exécution en cours du service de serveur 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Le service de serveur est démarré et en cours d’exécution.

#### <a name="domain-membership"></a>Appartenance au domaine 
*S’applique à : site d’administration centrale, site principal, site secondaire, fournisseurs SMS, SQL Server*

L’ordinateur Configuration Manager est membre d’un domaine Windows.

#### <a name="free-disk-space-on-site-server"></a>Espace disque disponible sur le serveur de site 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Pour pouvoir installer le serveur de site, celui-ci doit avoir au moins 15 Go d’espace disque libre. Si vous installez le fournisseur SMS sur le même serveur, un espace libre supplémentaire de 1 Go est nécessaire.

#### <a name="pending-system-restart"></a>Redémarrage du système en attente 
*S’applique à : site d’administration centrale, site principal, site secondaire, console Configuration Manager, fournisseur SMS, SQL Server, point de gestion, point de distribution*

Avant d’exécuter le programme d’installation, un autre programme requiert le redémarrage du serveur.

Depuis la version 1810, cette vérification est plus résiliente. Pour voir si l’ordinateur est dans un état de redémarrage en attente, les emplacements de Registre suivants sont vérifiés :<!--SCCMDocs-pr issue 3010-->  

- `HKLM:Software\Microsoft\Windows\CurrentVersion\Component Based Servicing\RebootPending`  
- `HKLM:SOFTWARE\Microsoft\Windows\CurrentVersion\WindowsUpdate\Auto Update\RebootRequired`  
- `HKLM:SYSTEM\CurrentControlSet\Control\Session Manager, PendingFileRenameOperations`  
- `HKLM:Software\Microsoft\ServerManager, CurrentRebootAttempts`  

#### <a name="read-only-domain-controller"></a>Contrôleur de domaine en lecture seule 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Les serveurs de bases de données du site et les serveurs de site secondaire ne sont pas pris en charge sur un contrôleur de domaine en lecture seule. 

Pour plus d’informations, consultez l’article du support Microsoft dans [Problèmes lors de l’installation de SQL Server sur un contrôleur de domaine](https://support.microsoft.com/help/2032911).

#### <a name="site-server-fqdn-length"></a>Longueur du nom de domaine complet du serveur de site 
*S’applique à : site d’administration centrale, site principal, site secondaire*

Longueur du nom de domaine complet du serveur de site.

#### <a name="unsupported-os-for-configuration-manager-console"></a>Système d’exploitation non pris en charge pour la console Configuration Manager
*S’applique à : console Configuration Manager*

Installez la console Configuration Manager sur des ordinateurs qui exécutent une version de système d’exploitation prise en charge. 

Pour plus d’informations, consultez [Versions de système d’exploitation prises en charge pour la console Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-consoles).

#### <a name="unsupported-os-for-site-server"></a>Système d’exploitation non pris en charge pour le serveur de site 
*S’applique à : site d’administration centrale, site principal, site secondaire, console Configuration Manager, point de gestion, point de distribution*

Le serveur exécute une version de système d’exploitation prise en charge. 

Pour plus d’informations, consultez [Versions de système d’exploitation prises en charge pour les serveurs de système de site Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).

#### <a name="verify-database-consistency"></a>Vérifier la cohérence de la base de données 
*S’applique à : site d’administration centrale, site principal*

Vérifie la cohérence de la base de données de site dans SQL Server.  


### <a name="system-requirements-warnings"></a>Configuration système requise : Avertissements

#### <a name="active-directory-domain-functional-level"></a>Niveau fonctionnel du domaine Active Directory 
*S’applique à : site d’administration centrale, site principal*

Le niveau fonctionnel du domaine Active Directory est au moins Windows Server 2008 R2.

#### <a name="domain-membership"></a>Appartenance au domaine 
*S’applique à : point de gestion, point de distribution*

L’ordinateur Configuration Manager est membre d’un domaine Windows.

#### <a name="ntfs-drive-on-site-server"></a>Lecteur NTFS sur le serveur de site 
*S’applique à : site principal*

Le lecteur de disque est formaté avec le système de fichiers NTFS. Pour une meilleure sécurité, installez les composants de serveur de site sur des disques formatés avec le système de fichiers NTFS.

#### <a name="schema-extensions"></a>Extensions de schéma 
*S’applique à : site d’administration centrale, site principal*

Le schéma Active Directory a été étendu. S’il est étendu, version des extensions de schéma qui ont été utilisées. 

Configuration Manager n’exige pas d’extensions de schéma Active Directory pour l’installation du serveur de site. Microsoft les recommande pour exploiter pleinement toutes les fonctionnalités de Configuration Manager. Pour plus d’informations sur les avantages d’étendre le schéma, consultez [Préparer Active Directory pour la publication de site](/sccm/core/plan-design/network/extend-the-active-directory-schema).

#### <a name="bkmk_changetracking"></a> Nettoyage du suivi des modifications SQL
*S’applique à : serveur de bases de données du site*

Depuis la version 1810, vérifiez si la base de données du site a un backlog des données de suivi des modifications SQL.<!--SCCMDocs-pr issue 3023-->  

Faites cette vérification manuellement en exécutant une procédure stockée de diagnostic dans la base de données du site. Commencez par créer une [connexion de diagnostic](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators?view=sql-server-2017) à la base de données du site. La méthode la plus simple consiste à utiliser l’éditeur de requête de SQL Server Management Studio et à vous connecter à `admin:<instance name>`. 

Dans une fenêtre de requête de connexion administrateur dédiée, exécutez les commandes suivantes :

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking
```

En fonction de la taille de votre base de données et de la taille du backlog, cette procédure stockée peut s’exécuter en quelques minutes ou nécessiter plusieurs heures. Lorsque la requête est terminée, vous voyez deux sections de données associées au backlog. Commencez par examiner **CT_Days_Old**. Cette valeur vous indique l’âge (nombre de jours) de l’entrée la plus ancienne dans votre table syscommittab. Elle doit indiquer cinq jours, à savoir la valeur par défaut de Configuration Manager. Ne modifiez pas cette valeur par défaut. Dans certains cas où le traitement de données ou la réplication sont lourds, l’entrée la plus ancienne dans syscommittab peut être supérieure à cinq jours. Si cette valeur est supérieure à sept jours, exécutez un nettoyage manuel des données de suivi des modifications.  

Pour nettoyer les données de suivi des modifications, exécutez la commande suivante dans la connexion administrateur dédiée : 

```SQL
USE <ConfigMgr database name>
EXEC spDiagChangeTracking @CleanupChangeTracking = 1
```

Cette commande démarre un nettoyage de syscommittab et de toutes les tables latérales associées. Elle peut s’exécuter en quelques minutes ou nécessiter plusieurs heures. Pour surveiller sa progression, interrogez la vue **vLogs**. Pour afficher la progression actuelle, exécutez la requête suivante : 

```SQL
SELECT * FROM vLogs WHERE ProcedureName = 'spDiagChangeTracking'
```

#### <a name="sql-native-client"></a>SQL Native Client
<!--SCCMDocs-pr issue 3094-->
*S’applique à : site d’administration centrale, site principal, site secondaire*

Lorsque vous installez un nouveau site, Configuration Manager installe automatiquement SQL Native Client en tant que composant redistribuable. Configuration Manager ne prend pas en charge la mise à niveau de SQL Native Client. Cette vérification permet de vous assurer que le site a une version prise en charge de SQL Native Client. À compter de la version 1810, la version minimale est SQL 2012 SP4 (`11.*.7001.0`). 

Cette version de SQL Native Client prend en charge TLS 1.2. Pour plus d’informations, consultez les articles suivants :
- [TLS 1.2 support for Microsoft SQL Server](https://support.microsoft.com/help/3135244/tls-1-2-support-for-microsoft-sql-server) (Prise en charge TLS 1.2 pour Microsoft SQL Server)  
- [How to enable TLS 1.2 for Configuration Manager](https://support.microsoft.com/help/4040243/how-to-enable-tls-1-2-for-configuration-manager) (Comment activer TLS 1.2 pour Configuration Manager)  
