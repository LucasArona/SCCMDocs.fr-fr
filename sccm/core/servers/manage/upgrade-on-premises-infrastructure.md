---
title: Mettre à niveau l’infrastructure locale
titleSuffix: Configuration Manager
description: Découvrez comment mettre à niveau l’infrastructure, telles que SQL Server et le système d’exploitation des systèmes de site.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7ff6d885ca635e15c62eddcdfa06abdc1a09cdf8
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456598"
---
# <a name="upgrade-on-premises-infrastructure-that-supports-configuration-manager"></a>Mettre à niveau l’infrastructure locale qui prend en charge Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cet article pour mettre à niveau l’infrastructure de serveur qui exécute Configuration Manager.  

- Si vous voulez effectuer la *mise à niveau* à partir d’une version antérieure de Configuration Manager, Current Branch, consultez [Mettre à niveau vers Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).  

- Si vous voulez *mettre à jour* votre infrastructure Configuration Manager, Current Branch, vers une nouvelle version, consultez [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).  



## <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Mettre à niveau le système d’exploitation des systèmes de site  

Configuration Manager prend en charge la mise à niveau sur place du système d’exploitation serveur qui héberge un serveur de site et un rôle de système de site, dans les situations suivantes :  

- Si Configuration Manager prend toujours en charge le niveau du Service Pack Windows résultant, il prend en charge la mise à niveau sur place vers un Service Pack Windows Server plus récent.  

- Mise à niveau sur place de :  

    - Windows Server 2016 vers Windows Server 2019   

    - Windows Server 2012 R2 vers Windows Server 2019   

    - Windows Server 2012 R2 vers Windows Server 2016   

    - Windows Server 2012 vers Windows Server 2016   

    - Windows Server 2012 vers Windows Server 2012 R2   

    - Windows Server 2008 R2 vers Windows Server 2012 R2   

Pour mettre à niveau un serveur, utilisez les procédures de mise à niveau fournies par le système d’exploitation vers lequel vous effectuez la mise à niveau. Consultez les articles suivants :  

- [Centre de mise à niveau de Windows Server](http://aka.ms/upgradecenter)  

- [Options de mise à niveau et de conversion pour Windows Server 2016](https://docs.microsoft.com/windows-server/get-started/supported-upgrade-paths)  

- [Options de mise à niveau pour Windows Server 2012 R2](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416\(v=ws.11))   


### <a name="bkmk_2016-2019"></a> Mise à niveau vers Windows Server 2016 ou 2019

Utilisez les étapes de cette section pour les scénarios de mise à niveau suivantes :  

- Mise à niveau de Windows Server 2012 R2 ou Windows Server 2016 vers Windows Server 2019  

- Mise à niveau de Windows Server 2012 ou Windows Server 2012 R2 vers Windows Server 2016  


#### <a name="before-upgrade"></a>Avant la mise à niveau  
- (Windows Server 2012 or Windows Server 2012 R2) : Supprimez le client SCEP (System Center Endpoint Protection). Windows Server intègre désormais Windows Defender, qui remplace le client SCEP. La présence du client SCEP peut empêcher une mise à niveau vers Windows Server.  

- Supprimez le rôle WSUS du serveur s’il est installé. Vous pouvez conserver la base de données SUSDB et l’attacher de nouveau après la réinstallation de WSUS.  

#### <a name="after-upgrade"></a>Après la mise à niveau   
- Vérifiez que Windows Defender est activé, configuré pour démarrer automatiquement et en cours d’exécution.  

- Vérifiez que les services Configuration Manager suivants sont en cours d’exécution :  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Vérifiez que les services d’**activation des processus Windows** et **WWW/W3svc** sont activés et configurés pour démarrer automatiquement. Sachant que le processus de mise à niveau désactive ces services, vérifiez qu’ils s’exécutent pour les rôles de système de site suivants :  

    - Serveur de site  

    - Point de gestion  

    - Point de service web du catalogue des applications  

    - Point du site web du catalogue des applications  

- Vérifiez que chaque serveur qui héberge un rôle de système de site continue de respecter tous les [prérequis](/sccm/core/plan-design/configs/site-and-site-system-prerequisites). Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.  

- Après avoir restauré les prérequis manquants, redémarrez le serveur une fois de plus pour être certain que les services sont démarrés et opérationnels.  

- Si vous mettez à niveau le serveur de site principal, [exécutez une réinitialisation du site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).  

#### <a name="known-issue-for-remote-configuration-manager-consoles"></a>Problème connu lié aux consoles Configuration Manager distantes   
Après avoir mis à niveau le serveur de site ou une instance du fournisseur SMS, vous ne pouvez pas vous connecter avec la console Configuration Manager. Pour contourner ce problème, restaurez manuellement les autorisations pour le groupe **Administrateurs SMS** dans WMI. Les autorisations doivent être définies sur le serveur de site, ainsi que sur chaque serveur distant qui héberge une instance du fournisseur SMS :

1. Sur les serveurs applicables, ouvrez la console MMC (Microsoft Management Console) et ajoutez le composant logiciel enfichable pour le **Contrôle WMI**, puis sélectionnez **Ordinateur local**.  

2. Dans la console MMC, ouvrez les **Propriétés** du **Contrôle WMI (local)**, puis sélectionnez l’onglet **Sécurité**.  

3. Développez l’arborescence sous la racine, sélectionnez le nœud **SMS**, puis choisissez **Sécurité**.  Vérifiez que le groupe **Administrateurs SMS** dispose des autorisations suivantes :  

    - Activer le compte  

    - Appel à distance autorisé  

4. Dans **l’onglet Sécurité** sous le nœud **SMS**, sélectionnez le nœud **site_&lt;sitecode**>, puis choisissez **Sécurité**. Vérifiez que le groupe **Administrateurs SMS** dispose des autorisations suivantes :  

    - Méthodes d’exécution  

    - Écriture fournisseur  

    - Activer le compte  

    - Appel à distance autorisé  

5. Enregistrez les autorisations pour restaurer l’accès à la console Configuration Manager.  


### <a name="bkmk_2012r2"></a> Mise à niveau vers Windows Server 2012 R2

Quand vous procédez à une mise à niveau de Windows Server 2008 R2 ou Windows Server 2012 vers Windows Server 2012 R2, voici les conditions qui s’appliquent :

#### <a name="before-upgrade"></a>Avant la mise à niveau  
- Sur Windows Server 2012 : Supprimez le rôle WSUS du serveur s’il est installé. Vous pouvez conserver la base de données SUSDB et l’attacher de nouveau après la réinstallation de WSUS.  

- Sur Windows Server 2008 R2 : Avant d’effectuer la mise à niveau vers Windows Server 2012 R2, vous devez désinstaller WSUS 3.2 du serveur. Vous pouvez conserver la base de données SUSDB et l’attacher de nouveau après la réinstallation de WSUS. Pour plus d’informations, consultez [Vue d’ensemble de Windows Server Update Services](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345\(v=ws.11)#new-and-changed-functionality).  

#### <a name="after-upgrade"></a>Après la mise à niveau  
- Le processus de mise à niveau désactive les services de déploiement Windows. Vérifiez que ce service est démarré et en cours d’exécution pour les rôles de système de site suivants :  

    - Serveur de site  

    - Point de gestion  

    - Point de service web du catalogue des applications  

    - Point du site web du catalogue des applications  

- Vérifiez que les services d’**activation des processus Windows** et **WWW/W3svc** sont activés et configurés pour démarrer automatiquement. Sachant que le processus de mise à niveau désactive ces services, vérifiez qu’ils s’exécutent pour les rôles de système de site suivants :  

    - Serveur de site  

    - Point de gestion  

    - Point de service web du catalogue des applications  

    - Point du site web du catalogue des applications  

- Vérifiez que chaque serveur qui héberge un rôle de système de site continue de respecter tous les [prérequis](/sccm/core/plan-design/configs/site-and-site-system-prerequisites). Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.  

    Après avoir restauré les prérequis manquants, redémarrez le serveur une fois de plus pour être certain que les services sont démarrés et opérationnels.  


### <a name="unsupported-upgrade-scenarios"></a>Scénarios de mise à niveau non pris en charge

Les scénarios de mise à niveau de Windows Server suivants font souvent l’objet de questions, mais ils ne sont pas pris en charge par Configuration Manager :  

- Windows Server 2008 vers Windows Server 2012 ou version ultérieure  

- Windows Server 2008 R2 vers Windows Server 2012  



##  <a name="BKMK_SupConfigUpgradeClient"></a> Mise à niveau du système d’exploitation des clients  

Configuration Manager prend en charge une mise à niveau sur place du système d’exploitation pour les clients Configuration Manager dans les situations suivantes :  

- Si Configuration Manager prend en charge le niveau du Service Pack résultant, il prend en charge la mise à niveau sur place vers un Service Pack Windows plus récent.  

- Mise à niveau sur place de Windows à partir d’une version prise en charge vers Windows 10. Pour plus d’informations, consultez [Effectuer une mise à niveau de Windows vers la dernière version](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version).  

- Mises à niveau de la maintenance de build à build de Windows 10. Pour plus d’informations, consultez [Gérer Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service).  



##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Mise à niveau de SQL Server  

Configuration Manager prend en charge une mise à niveau sur place de SQL Server sur le serveur de base de données de site. 

Pour plus d’informations sur les versions de SQL Server que prend en charge Configuration Manager, consultez [Prise en charge des versions de SQL Server](/sccm/core/plan-design/configs/support-for-sql-server-versions).  


### <a name="upgrade-the-service-pack-version-of-sql-server"></a>Mise à niveau de la version du Service Pack de SQL Server    

Si Configuration Manager prend toujours en charge le niveau du Service Pack SQL Server résultant, il prend en charge la mise à niveau sur place de SQL Server vers un Service Pack plus récent.

Si vous utilisez plusieurs sites Configuration Manager dans une hiérarchie, chaque site peut exécuter une version différente du Service Pack SQL Server. Il n’existe aucune limitation quant à l’ordre dans lequel les sites mettent à niveau la version du Service Pack SQL Server.


### <a name="upgrade-to-a-new-version-of-sql-server"></a>Mise à niveau vers une nouvelle version de SQL Server   

Configuration Manager prend en charge la mise à niveau sur place de SQL Server vers les versions suivantes :

- SQL Server 2017  

- SQL Server 2016  

- SQL Server 2014  

Quand vous mettez à niveau la version de SQL Server qui héberge la base de données de site, vous devez mettre à niveau la version de SQL Server qui est utilisée sur les sites dans l’ordre suivant :

1. Mettez d’abord à niveau SQL Server sur le site administration centrale.  

2. Mettez à niveau les sites secondaires avant de mettre à niveau le site principal parent d’un site secondaire.  

3. Mettez à niveau les sites principaux parents en dernier. Ces sites incluent les sites principaux enfants qui dépendent d'un site d'administration centrale et les sites principaux autonomes qui constituent les sites de plus haut niveau d'une hiérarchie.  


### <a name="sql-server-cardinality-estimation-level"></a>Niveau d’estimation de cardinalité SQL Server   

Quand vous mettez à niveau une base de données de site à partir d’une version antérieure de SQL Server, la base de données conserve son niveau d’estimation de cardinalité SQL existant, s’il est au minimum autorisé pour cette instance de SQL Server. En mettant à niveau SQL Server avec une base de données à un niveau de compatibilité inférieur que celui autorisé automatiquement, vous définissez la base de données sur le niveau de compatibilité le plus bas autorisé par SQL Server.

Le tableau suivant identifie les niveaux de compatibilité recommandés pour les bases de données de site Configuration Manager :

|Version SQL Server | Niveaux de compatibilité pris en charge | Niveau conseillé |
|----------------|--------------------|--------|
| SQL Server 2017 | 140, 130, 120, 110  | 140 |
| SQL Server 2016 | 130, 120, 110  | 130 |
| SQL Server 2014 | 120, 110      | 110 |

Pour identifier le niveau de compatibilité de l’estimation de cardinalité SQL Server utilisé pour votre base de données de site, exécutez la requête SQL suivante sur le serveur de base de données de site :  
```SQL
SELECT name, compatibility_level FROM sys.databases
```

Pour plus d’informations sur les niveaux de compatibilité SQL CE et comment les définir, consultez [Niveau de compatibilité ALTER DATABASE (Transact-SQL)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017).


Pour plus d’informations sur la mise à niveau de SQL Server, consultez les articles SQL Server suivants :  

- [Mise à niveau vers SQL Server 2017](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Mise à niveau vers SQL Server 2016](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2016)  

- [Mise à niveau vers SQL Server 2014](https://docs.microsoft.com/sql/database-engine/install-windows/supported-version-and-edition-upgrades?view=sql-server-2014)  



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Pour mettre à niveau SQL Server sur le serveur de base de données de site  

1. Arrêtez tous les services Configuration Manager sur le site.  

2. Mettez à niveau SQL Server vers une version prise en charge.  

3. Redémarrez les services Configuration Manager.  

> [!NOTE]  
> Quand vous passez de l’édition Standard de SQL Server sur le site administration centrale à l’édition Datacenter ou Enterprise, la partition de la base de données ne change pas. Cette partition de la base de données limite le nombre de clients pris en charge dans la hiérarchie.  
