---
title: Mettre à niveau l’infrastructure locale
titleSuffix: Configuration Manager
description: Découvrez comment mettre à niveau l’infrastructure, telles que SQL Server et le système d’exploitation de site des systèmes de site.
ms.date: 02/15/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 09cce65bd4bb4ccb8a9cfee6927aa86409e691a0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="upgrade-on-premises-infrastructure-that-supports-system-center-configuration-manager"></a>Mettre à niveau l’infrastructure locale qui prend en charge System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les informations de cet article pour mettre à niveau l’infrastructure de serveur qui exécute System Center Configuration Manager.  

 - Si vous voulez effectuer la mise à niveau à partir d’une version antérieure de Configuration Manager vers System Center Configuration Manager, consultez [Mettre à niveau vers System Center Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).

- Si vous voulez mettre à jour votre infrastructure System Center Configuration Manager vers une nouvelle version, consultez [Mises à jour pour System Center Configuration Manager](/sccm/core/servers/manage/updates).

##  <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Mettre à niveau le système d’exploitation des systèmes de site  
 Configuration Manager prend en charge la mise à niveau sur place du système d’exploitation de serveurs qui hébergent un serveur de site et des serveurs distants hébergeant un rôle de système de site, dans les situations suivantes :  

-   Mise à niveau sur place vers un Service Pack Windows Server ultérieur si le niveau du Service Pack de Windows résultant est pris en charge par Configuration Manager.  
-   Mise à niveau sur place à partir de :
    - Windows Server 2012 R2 vers Windows Server 2016 ([afficher des informations supplémentaires](#bkmk_2016)).
    - Windows Server 2012 vers Windows Server 2016 ([afficher des informations supplémentaires](#bkmk_2016)).
    - Windows Server 2012 vers Windows Server 2012 R2 ([afficher des informations supplémentaires](#bkmk_2012r2)).
    - Quand vous utilisez Configuration Manager version 1602 ou ultérieur, la mise à niveau de Windows Server 2008 R2 vers Windows Server 2012 R2 est également prise en charge ([afficher des informations supplémentaires](#bkmk_from2008r2).

    > [!WARNING]  
    >  Avant d’effectuer une mise à niveau vers un autre système d’exploitation, *vous devez désinstaller WSUS* du serveur. Vous pouvez conserver la base de données SUSDB et l’attacher de nouveau après la réinstallation de WSUS. Pour plus d’informations sur cette étape critique, consultez la section « Fonctionnalités nouvelles et modifiées » de la rubrique [Vue d’ensemble des services WSUS (Windows Server Update Services)](https://technet.microsoft.com/library/hh852345.aspx) dans la documentation de Windows Server.  

Pour mettre à niveau un serveur, utilisez les procédures de mise à niveau fournies par le système d’exploitation vers lequel vous effectuez la mise à niveau.  Consultez les rubriques suivantes :
  -  [Options de mise à niveau pour Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) dans la documentation de Windows Server.  
  - [Options de mise à niveau et de conversion pour Windows Server 2016](https://technet.microsoft.com/windows-server-docs/get-started/supported-upgrade-paths) dans la documentation de Windows Server.

### <a name="bkmk_2016"></a> Mise à niveau de Windows Server 2012 ou Windows Server 2012 R2 vers la version 2016
Lorsque vous mettez à niveau Windows Server 2012 ou Windows Server 2012 R2 vers Windows Server 2016, ce qui suit s’applique :


**Avant la mise à niveau :**  
-   Supprimez le client SCEP (System Center Endpoint Protection). Windows Defender, qui remplace le client SCEP, est intégré à Windows Server 2016. La présence du client SCEP peut empêcher une mise à niveau vers Windows Server 2016.
-   Supprimez le rôle WSUS du serveur, s’il est installé. Vous pouvez conserver la base de données SUSDB et l’attacher de nouveau après la réinstallation de WSUS.

**Après la mise à niveau :**
-   Vérifiez que Windows Defender est activé, configuré pour démarrer automatiquement et en cours d’exécution.
-   Vérifiez que les services Configuration Manager suivants sont en cours d’exécution :
  -     SMS_EXECUTIVE
  -     SMS_SITE_COMPONENT_MANAGER


-   Vérifiez que le **service d’activation des processus Windows** et le **service WWW/W3SVC** sont activés, configurés pour démarrer automatiquement et en cours d’exécution pour les rôles de système de site suivants (ces services sont désactivés pendant la mise à niveau) :
  -     Serveur de site
  -     Point de gestion
  -     Point de service web du catalogue des applications
  -     Point du site web du catalogue des applications

-   Vérifiez que chaque serveur qui héberge un rôle de système de site respecte l’ensemble des [prérequis pour les rôles de système de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) qui s’exécutent sur ce serveur. Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.

-   Après avoir restauré les prérequis manquants, redémarrez le serveur une fois de plus pour être sûr que les services sont démarrés et en cours d’exécution.

-   Si vous mettez à niveau le serveur de site principal, [exécutez une réinitialisation du site](/sccm/core/servers/manage/modify-your-infrastructure#bkmk_reset).

**Problème connu lié aux consoles Configuration Manager distantes :**  
Une fois la mise à niveau du serveur de site ou d’un serveur qui héberge une instance de SMS_Provider vers Windows Server 2016 effectuée, il se peut que les utilisateurs administratifs ne puissent pas connecter une console Configuration Manager au site. Pour contourner ce problème, vous devez restaurer manuellement les autorisations pour le groupe Administrateurs SMS dans WMI. Les autorisations doivent être définies sur le serveur de site, ainsi que sur chaque serveur distant qui héberge une instance de SMS_Provider :

1. Sur les serveurs applicables, ouvrez la console MMC (Microsoft Management Console) et ajoutez le composant logiciel enfichable pour le **Contrôle WMI**, puis sélectionnez **Ordinateur local**.
2. Dans la console MMC, ouvrez les **Propriétés** du **Contrôle WMI (local)**, puis sélectionnez l’onglet **Sécurité**.
3. Développez l’arborescence sous la racine, sélectionnez le nœud **SMS**, puis choisissez **Sécurité**.  Vérifiez que le groupe **Administrateurs SMS** dispose des autorisations suivantes :
  -     Activer le compte
  -     Appel à distance autorisé
4. Dans **l’onglet Sécurité** sous le nœud **SMS**, sélectionnez le nœud **site_&lt;sitecode**>, puis choisissez **Sécurité**. Vérifiez que le groupe **Administrateurs SMS** dispose des autorisations suivantes :
  -   Méthodes d’exécution
  -   Écriture fournisseur
  -   Activer le compte
  -   Appel à distance autorisé
5. Enregistrez les autorisations pour restaurer l’accès à la console Configuration Manager.

### <a name="bkmk_2012r2"></a> Windows Server 2012 vers Windows Server 2012 R2

**Avant la mise à niveau :**
-   Supprimez le rôle WSUS du serveur, s’il est installé. Vous pouvez conserver la base de données SUSDB et l’attacher de nouveau après la réinstallation de WSUS.

**Après la mise à niveau :**
  - Vérifiez que le service de déploiement Windows est démarré et en cours d’exécution pour les rôles de système de site suivants (ce service est arrêté pendant la mise à niveau) :
    - Serveur de site
    - Point de gestion
    - Point de service web du catalogue des applications
    - Point du site web du catalogue des applications

  -     Vérifiez que le **service d’activation des processus Windows** et le **service WWW/W3SVC** sont activés, configurés pour démarrer automatiquement et en cours d’exécution pour les rôles de système de site suivants (ces services sont désactivés pendant la mise à niveau) :
    -   Serveur de site
    -   Point de gestion
    -   Point de service web du catalogue des applications
    -   Point du site web du catalogue des applications


  -     Vérifiez que chaque serveur qui héberge un rôle de système de site respecte l’ensemble des [prérequis pour les rôles de système de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) qui s’exécutent sur ce serveur. Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.

  Après avoir restauré les prérequis manquants, redémarrez le serveur une fois de plus pour être sûr que les services sont démarrés et en cours d’exécution.

### <a name="bkmk_from2008r2"></a> Mise à niveau de Windows Server 2008 R2 vers Windows Server 2012 R2
Ce scénario de mise à niveau du système d’exploitation a les conditions suivantes :  

**Avant la mise à niveau :**
-   Désinstallez WSUS 3.2.  
    Avant de mettre à niveau le système d’exploitation d’un serveur vers Windows Server 2012 R2, vous devez désinstaller WSUS 3.2 du serveur. Pour plus d’informations sur cette étape critique, consultez la section Fonctionnalités nouvelles et modifiées de la rubrique Vue d’ensemble des services WSUS (Windows Server Update Services) dans la documentation de Windows Server.

**Après la mise à niveau :**
  - Vérifiez que le service de déploiement Windows est démarré et en cours d’exécution pour les rôles de système de site suivants (ce service est arrêté pendant la mise à niveau) :
    - Serveur de site
    - Point de gestion
    - Point de service web du catalogue des applications
    - Point du site web du catalogue des applications


  -     Vérifiez que le **service d’activation des processus Windows** et le **service WWW/W3SVC** sont activés, configurés pour démarrer automatiquement et en cours d’exécution pour les rôles de système de site suivants (ces services sont désactivés pendant la mise à niveau) :
    -   Serveur de site
    -   Point de gestion
    -   Point de service web du catalogue des applications
    -   Point du site web du catalogue des applications


  -     Vérifiez que chaque serveur qui héberge un rôle de système de site respecte l’ensemble de la [configuration requise pour les rôles de système de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) qui s’exécutent sur ce serveur. Par exemple, il se peut que vous deviez réinstaller le service BITS ou le service WSUS, ou de configurer des paramètres spécifiques pour IIS.

  Après avoir restauré les prérequis manquants, redémarrez le serveur une fois de plus pour être sûr que les services sont démarrés et en cours d’exécution.


### <a name="unsupported-upgrade-scenarios"></a>Scénarios de mise à niveau non pris en charge
Les scénarios de mise à niveau de Windows Server suivants font souvent l’objet de questions, mais ils ne sont pas pris en charge par Configuration Manager :  

-   Windows Server 2008 vers Windows Server 2012 ou version ultérieure  
-   Windows Server 2008 R2 vers Windows Server 2012



##  <a name="BKMK_SupConfigUpgradeClient"></a> Mettre à niveau le système d’exploitation de clients Configuration Manager  
 Configuration Manager prend en charge une mise à niveau sur place du système d’exploitation pour les clients Configuration Manager dans les situations suivantes :  

-   La mise à niveau sur place vers un Service Pack Windows ultérieur si le niveau du Service Pack résultant est pris en charge par Configuration Manager.  

-   Mise à niveau sur place de Windows à partir d’une version prise en charge vers Windows 10. Pour plus d’informations, consultez [Mettre à niveau Windows vers la dernière version avec System Center Configuration Manager](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

-   Mises à niveau de la maintenance de build à build de Windows 10.  Pour plus d’informations, consultez [Gérer Windows as a Service (WaaS) à l’aide de System Center Configuration Manager](../../../osd/deploy-use/manage-windows-as-a-service.md).  

##  <a name="BKMK_SupConfigUpgradeDBSrv"></a> Mettre à niveau SQL Server sur le serveur de base de données de site  
  Configuration Manager prend en charge une mise à niveau sur place de SQL Server à partir d’une version prise en charge de SQL sur le serveur de base de données de site. Les scénarios de mise à niveau de SQL Server décrits dans cette section sont pris en charge par Configuration Manager et incluent la configuration requise pour chaque scénario.

 Pour plus d’informations sur les versions de SQL Server prises en charge par Configuration Manager, consultez [Prise en charge des versions de SQL Server pour System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

 **Mettre à niveau la version du Service Pack de SQL Server**    
 Configuration Manager prend en charge la mise à niveau sur place de SQL Server vers un Service Pack ultérieur si le niveau du Service Pack SQL Server résultant est pris en charge par Configuration Manager.

 Quand une hiérarchie comprend plusieurs sites Configuration Manager, chaque site peut exécuter une version différente du Service Pack de SQL Server, et il n’existe pas de limitation quant à l’ordre dans lequel les sites mettent à niveau la version du Service Pack de SQL Server qui est utilisé pour la base de données du site.

 **Mise à niveau vers une nouvelle version de SQL Server :**   
 Configuration Manager prend en charge la mise à niveau sur place de SQL Server vers les versions suivantes :

 - SQL Server 2012  
 - SQL Server 2014  
 - SQL Server 2016  

Quand vous mettez à niveau la version de SQL Server qui héberge la base de données du site, vous devez mettre à niveau la version de SQL Server qui est utilisée sur les sites dans l’ordre suivant :

 1. Mettez d'abord à niveau SQL Server sur le site administration centrale.
 2. Mettez à niveau les sites secondaires avant de mettre à niveau le site principal parent d’un site secondaire.
 3. Mettez à niveau les sites principaux parents en dernier. Ceci inclut les sites principaux enfants qui dépendent d'un site d'administration centrale et les sites principaux autonomes qui constituent les sites de plus haut niveau d'une hiérarchie.

**Niveau Estimation de cardinalité SQL Server et base de données de site :**   
Quand une base de données de site est mise à niveau à partir d’une version antérieure de SQL Server, la base de données conserve son niveau Estimation de cardinalité SQL Server (SQL Server CE) existant s’il est au minimum autorisé pour cette instance de SQL Server. En mettant à niveau SQL Server avec une base de données à un niveau de compatibilité inférieur que celui autorisé automatiquement, vous définissez la base de données sur le niveau de compatibilité le plus bas autorisé par SQL Server.

Le tableau suivant identifie les niveaux de compatibilité recommandés pour les bases de données de site Configuration Manager :

|Version SQL Server | Niveaux de compatibilité pris en charge |Niveau conseillé|
|----------------|--------------------|--------|
| SQL Server 2016| 130, 120, 110, 100 | 130|
| SQL Server 2014| 120, 110, 100      | 110|

Pour identifier le niveau de compatibilité SQL Server CE en cours d’utilisation pour votre base de données de site, exécutez la requête SQL suivante sur le serveur de base de données de site : **SELECT name, compatibility_level FROM sys.databases**

 Pour plus d’informations sur les niveaux de compatibilité SQL CE et comment les définir, consultez [Niveau de compatibilité ALTER DATABASE (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx).


Pour plus d’informations sur SQL Server, consultez la documentation de SQL Server sur TechNet :
-   [Mise à niveau vers SQL Server 2012](http://technet.microsoft.com/library/ms143393\(v=sql.110))
-   [Mise à niveau vers SQL Server 2014](http://technet.microsoft.com/library/ms143393\(v=sql.120))  
-   [Mise à niveau vers SQL Server 2016](https://technet.microsoft.com/library/bb677622(v=sql.130))



### <a name="to-upgrade-sql-server-on-the-site-database-server"></a>Pour mettre à niveau SQL Server sur le serveur de base de données de site  

1.  Arrêtez tous les services de Configuration Manager sur le site.  
2.  Mettez à niveau SQL Server vers une version prise en charge.  
3.  Redémarrez les services de Configuration Manager.  

> [!NOTE]  
>  Quand vous changez l'édition de SQL Server utilisée sur le site d'administration centrale d'une édition Standard en une édition Enterprise ou Datacenter, la partition de base de données qui limite le nombre de clients que la hiérarchie prend en charge ne change pas.
