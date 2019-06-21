---
title: Prérequis des sites
titleSuffix: Configuration Manager
description: Découvrez comment configurer un ordinateur Windows en tant que serveur de système de site Configuration Manager.
ms.date: 03/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1392797b-76cb-46b4-a3e4-8f349ccaa078
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: daee7a247fd12637736caa9c341798950a66c786
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67251859"
---
# <a name="site-and-site-system-prerequisites-for-configuration-manager"></a>Prérequis des sites et systèmes de site pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les ordinateurs Windows nécessitent des configurations spécifiques qui prennent en charge leur utilisation en tant que serveurs de système de site Configuration Manager. 

Cet article se concentre principalement sur [Windows Server 2012 et les versions ultérieures](#bkmk_2012Prereq). [Windows Server 2008 R2 et Windows Server 2008](#bkmk_2008) sont pris en charge pour le rôle de système de site du point de distribution. Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers). 

Dans certains cas, par exemple Windows Server Update Services (WSUS) pour le point de mise à jour logicielle, vous devez vous référer à la documentation du produit pour connaître les prérequis et limitations supplémentaires liés à l’utilisation. Cet article porte uniquement sur les configurations qui s’appliquent directement à l’utilisation de Configuration Manager.   

> [!NOTE]  
>  Depuis janvier 2016, le support n’est plus assuré pour .NET Framework 4.0, 4.5 et 4.5.1. Pour plus d’informations, consultez [Questions fréquentes (FAQ) sur la politique de support - Microsoft .NET Framework](https://support.microsoft.com/gp/framework_faq?WT.mc_id=azurebg_email_Trans_943_NET452_Update).  



## <a name="bkmk_generalprerewq"></a> Exigences générales et limitations

Les exigences suivantes s’appliquent à tous les serveurs de système de site :

- Chaque serveur de système de site doit utiliser un système d’exploitation 64 bits. La seule exception est le rôle de système de site du point de distribution, que vous pouvez installer sur certains systèmes d’exploitation 32 bits.  

- Les systèmes de site ne sont pas pris en charge sur les installations Server Core des systèmes d’exploitation. Toutefois, il existe une exception : les installations Server Core sont prises en charge pour le rôle de système de site du point de distribution. Pour plus d’informations, consultez [Systèmes d’exploitation pris en charge pour les serveurs de système de site Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

- Une fois que vous avez installé un serveur de système de site, vous ne pouvez plus modifier les éléments suivants :  

    - Le nom du domaine où se trouve l’ordinateur du système de site (également appelé **changement de nom de domaine**).  

    - L’appartenance de l’ordinateur au domaine.  

    - Nom de l’ordinateur.  

  Si vous devez changer l’un de ces éléments, supprimez d’abord le rôle de système de site de l’ordinateur. Réinstallez ensuite le rôle, une fois le changement effectué. Pour les changements qui affectent le serveur de site, désinstallez d’abord le site. Réinstallez ensuite le site, une fois le changement effectué.  

- Les rôles de système de site ne sont pas pris en charge sur une instance d’un cluster Windows Server. La seule exception est le serveur de base de données de site. Pour plus d’informations, consultez [Utiliser un cluster SQL Server pour la base de données du site Configuration Manager](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database).  

    Depuis la version 1810, le processus d’installation de Configuration Manager ne bloque plus l’installation du rôle de serveur de site sur un ordinateur ayant le rôle Windows pour le clustering de basculement. SQL Always On exige ce rôle, ce qui vous empêchait de colocaliser la base de données de site sur le serveur de site. Avec ce changement, vous pouvez créer un site à haut niveau de disponibilité avec moins de serveurs en utilisant SQL Always On et un serveur de site en mode passif. Pour plus d’informations, consultez [Options de haute disponibilité](/sccm/core/servers/deploy/configure/high-availability-options). <!--3607761, fka 1359132-->  

- Vous ne pouvez pas modifier le type de démarrage ou les paramètres d’ouverture de session pour un service Configuration Manager. Dans ce cas, vous risquez d’empêcher des services clés de s’exécuter correctement.  


###  <a name="bkmk_2012Prereq"></a> Conditions préalables pour les systèmes d’exploitation Windows Server 2012 et versions ultérieures  

Consultez les sections principales de cet article pour connaître les prérequis spécifiques aux rôles et aux serveurs de système de site sur Windows Server 2012 et les versions ultérieures :

- [Serveur de site d’administration centrale et serveur de site principal](#bkmk_2012sspreq)
- [Serveur de site secondaire](#bkmk_2012secpreq)
- [Serveur de base de données](#bkmk_2012dbpreq)
- [Serveur de fournisseur SMS](#bkmk_2012smsprovpreq)
- [Point du site web du catalogue des applications](#bkmk_2012acwspreq)
- [Point de service web du catalogue des applications](#bkmk_2012ACwsitepreq)
- [Point de synchronisation Asset Intelligence](#bkmk_2012AIpreq)
- [Point d’enregistrement de certificat](#bkmk_2012crppreq)
- [Point de distribution](#bkmk_2012dppreq)
- [Point Endpoint Protection](#bkmk_2012EPPpreq)
- [Point d’inscription](#bkmk_2012Enrollpreq)
- [Point proxy d’inscription](#bkmk_2012EnrollProxpreq)
- [Point d’état de secours](#bkmk_2012FSPpreq)
- [Point de gestion](#bkmk_2012MPpreq)
- [Point de Reporting Services](#bkmk_2012RSpoint)
- [Point de connexion de service](#bkmk_SCPpreq)
- [Point de mise à jour logicielle](#bkmk_2012SUPpreq)
- [Point de migration d’état](#bkmk_2012SMPpreq)

##  <a name="bkmk_2012sspreq"></a> Serveur de site d’administration centrale et serveur de site principal 

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

- .NET Framework 3.5 SP1 (ou version ultérieure)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - Pour plus d’informations sur les versions du .NET Framework, consultez [Versions et dépendances du .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).

- Compression différentielle à distance  

#### <a name="windows-adk"></a>Windows ADK  

- Avant d’installer ou de mettre à niveau un site d’administration centrale ou un site principal, installez la version de Windows ADK (Kit de déploiement et d’évaluation Windows) nécessaire pour la version de Configuration Manager que vous installez ou vers laquelle vous effectuez une mise à niveau. Pour plus d’informations, consultez [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Pour plus d’informations sur cette configuration requise, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="visual-c-redistributable"></a>Redistributable Visual C++  

- Configuration Manager installe Microsoft Visual C++ 2013 Redistributable Package sur chaque ordinateur sur lequel est installé un serveur de site.  

- Les sites d’administration centrale et les sites principaux nécessitent les versions x86 et x64 du fichier redistribuable applicable.  



##  <a name="bkmk_2012secpreq"></a> Serveur de site secondaire   

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

- .NET Framework 3.5 SP1 (ou version ultérieure)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - Pour plus d’informations sur les versions du .NET Framework, consultez [Versions et dépendances du .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  

- Compression différentielle à distance  

#### <a name="visual-c-redistributable"></a>Redistributable Visual C++  

- Configuration Manager installe Microsoft Visual C++ 2013 Redistributable Package sur chaque ordinateur sur lequel est installé un serveur de site.  

- Les sites secondaires requièrent seulement la version x64.  

#### <a name="default-site-system-roles"></a>Rôles de système de site par défaut  

- Par défaut, un site secondaire installe un **point de gestion** et un **point de distribution**.  

- Assurez-vous que le serveur de site secondaire remplit les conditions préalables pour ces rôles de système de site.  



##  <a name="bkmk_2012dbpreq"></a> Serveur de base de données  

#### <a name="remote-registry-service"></a>Service d'accès à distance au Registre  

- Durant l’installation du site Configuration Manager, activez le service **Registre à distance** sur l’ordinateur qui héberge la base de données du site.  

#### <a name="sql-server"></a>SQL Server  

- Avant d’installer un site d’administration centrale ou un site principal, installez une version prise en charge de SQL Server pour héberger la base de données du site. Pour plus d’informations, consultez [Versions SQL Server prises en charge](/sccm/core/plan-design/configs/support-for-sql-server-versions).  

- Avant d’installer un site secondaire, vous pouvez installer une version prise en charge de SQL Server.  

- Si vous souhaitez que Configuration Manager installe SQL Server Express en même temps que le site secondaire, vérifiez que l’ordinateur présente la configuration requise pour exécuter SQL Server Express.  



##  <a name="bkmk_2012smsprovpreq"></a> Serveur de fournisseur SMS  

#### <a name="windows-adk"></a>Windows ADK  

- L’ordinateur sur lequel vous installez une instance du fournisseur SMS doit disposer de la version de Windows ADK nécessaire à la version de Configuration Manager que vous installez ou vers laquelle vous effectuez une mise à niveau. Pour plus d’informations, consultez [Windows 10 ADK](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-adk).  

- Pour plus d’informations sur cette configuration requise, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

- Si vous utilisez le [service d’administration](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service), le serveur qui héberge le rôle de fournisseur SMS peut requérir .NET 4.5.2 ou une version ultérieure.  <!-- SCCMDocs issue #1203 -->

- Serveur Web (IIS)

##  <a name="bkmk_2012acwspreq"></a> Point du site web du catalogue des applications  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

- .NET Framework 3.5 SP1 (ou version ultérieure)  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2  

    - ASP.NET 4.5  

    - Pour plus d’informations sur les versions du .NET Framework, consultez [Versions et dépendances du .NET Framework](https://docs.microsoft.com/dotnet/framework/migration-guide/versions-and-dependencies).  


#### <a name="iis-configuration"></a>Configuration IIS  

-   Fonctionnalités HTTP communes :  

    -   Document par défaut  

    -   Contenu statique  

-   Développement d'applications :  

    -   ASP.NET 3.5 (et les options sélectionnées automatiquement)  

    -   ASP.NET 4.5 (et les options sélectionnées automatiquement)  

    -   Extensibilité .NET 3.5  

    -   Extensibilité .NET 4.5  

-   Sécurité :  

    -   Authentification Windows  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  



##  <a name="bkmk_2012ACwsitepreq"></a> Point de service web du catalogue des applications  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 3.5 SP1 (ou version ultérieure)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 :  

    -   ASP.NET 4.5 :  

        -   Activation de HTTP (et des options sélectionnées automatiquement)  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Fonctionnalités HTTP communes :  

    -   Document par défaut  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

-   Développement d'applications :  

    -   ASP.NET 3.5 (et les options sélectionnées automatiquement)  

    -   Extensibilité .NET 3.5  

    -   ASP.NET 4.5 (et les options sélectionnées automatiquement)  

    -   Extensibilité .NET 4.5  

#### <a name="computer-memory"></a>Mémoire de l’ordinateur  

-   L’ordinateur hébergeant ce rôle de système de site doit avoir au moins 5 % de mémoire disponible pour permettre au rôle de système de site de traiter les demandes.  

-   Quand ce rôle de système de site est colocalisé avec un autre rôle de système de site ayant la même exigence, la quantité de mémoire nécessaire pour l’ordinateur n’augmente pas, mais elle reste à une valeur minimale de 5 %.  



##  <a name="bkmk_2012AIpreq"></a> Point de synchronisation Asset Intelligence  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 



##  <a name="bkmk_2012crppreq"></a> Point d’enregistrement de certificat  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 :  

    -   Activation HTTP  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Développement d'applications :  

    -   ASP.NET 3.5 (et les options sélectionnées automatiquement)  

    -   ASP.NET 4.5 (et les options sélectionnées automatiquement)  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

    -   Compatibilité WMI d'IIS 6  



##  <a name="bkmk_2012dppreq"></a> Point de distribution  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   Compression différentielle à distance  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Développement d'applications :  

    -   Extensions ISAPI  

-   Sécurité :  

    -   Authentification Windows  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

    -   Compatibilité WMI d'IIS 6  

#### <a name="powershell"></a>PowerShell  

-   Sur Windows Server 2012 et les versions ultérieures, PowerShell 3.0 ou 4.0 est nécessaire pour pouvoir installer le point de distribution.  

#### <a name="visual-c-redistributable"></a>Redistributable Visual C++  

-   Configuration Manager installe Microsoft Visual C++ 2013 Redistributable Package sur chaque ordinateur hébergeant un point de distribution.  

-   La version installée dépend de la plateforme de l’ordinateur (x86 ou x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Pour héberger un point de distribution, vous pouvez utiliser un service cloud dans Microsoft Azure.  

#### <a name="to-support-pxe-or-multicast"></a>Pour prendre en charge PXE ou la multidiffusion  

-   Installez et configurez le rôle WDS (Windows Deployment Services) de Windows Server.  

    > [!NOTE]  
    >  WDS s’installe et se configure automatiquement quand vous configurez un point de distribution pour prendre en charge PXE ou la multidiffusion sur un serveur exécutant Windows Server 2012 ou une version ultérieure.  

-   À partir de la version 1806, activez un répondeur PXE sur un point de distribution sans utiliser les Services de déploiement Windows.  

Pour plus d'informations, consultez [Installer et configurer des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Quand le point de distribution transfère du contenu, il le fait à l’aide du service BITS (**Service de transfert intelligent en arrière-plan**) intégré à Windows. Le rôle du point de distribution ne nécessite pas l’installation de la fonctionnalité facultative BITS IIS Server Extension, car le client n’y charge aucune information.  



##  <a name="bkmk_2012EPPpreq"></a> Point Endpoint Protection  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 3.5 SP1 (ou version ultérieure)  

-   Fonctionnalités de Windows Defender (Windows Server 2016 ou ultérieur)  



##  <a name="bkmk_2012Enrollpreq"></a> Point d’inscription  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

- .NET Framework 3.5 (ou version ultérieure).  

- .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 :  

     Pendant l’installation de ce rôle de système de site, Configuration Manager installe automatiquement .NET Framework 4.5.2. Cette installation peut placer le serveur dans un état d’attente redémarrage. Si un redémarrage est en attente pour .NET Framework, il est possible que les applications .NET ne puissent pas s’exécuter tant que le serveur n’a pas redémarré et que l’installation n’est pas terminée.  

    - Activation de HTTP (et des options sélectionnées automatiquement)  

    - ASP.NET 4.5  

    - Services WCF (Windows Communication Foundation)<!-- SCCMDocs issue #1168 -->  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Fonctionnalités HTTP communes :  

    -   Document par défaut  

-   Développement d'applications :  

    -   ASP.NET 3.5 (et les options sélectionnées automatiquement)  

    -   Extensibilité .NET 3.5  

    -   ASP.NET 4.5 (et les options sélectionnées automatiquement)  

    -   .NET Extensibility 4.5  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

#### <a name="computer-memory"></a>Mémoire de l’ordinateur  

-   L’ordinateur hébergeant ce rôle de système de site doit avoir au moins 5 % de mémoire disponible pour permettre au rôle de système de site de traiter les demandes.  

-   Quand ce rôle de système de site est colocalisé avec un autre rôle de système de site ayant la même exigence, la quantité de mémoire nécessaire pour l’ordinateur n’augmente pas, mais elle reste à une valeur minimale de 5 %.  



##  <a name="bkmk_2012EnrollProxpreq"></a> Point proxy d’inscription  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 3.5 (ou version ultérieure).  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

     Pendant l’installation de ce rôle de système de site, Configuration Manager installe automatiquement .NET Framework 4.5.2. Cette installation peut placer le serveur dans un état d’attente redémarrage. Si un redémarrage est en attente pour .NET Framework, il est possible que les applications .NET ne puissent pas s’exécuter tant que le serveur n’a pas redémarré et que l’installation n’est pas terminée.  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Fonctionnalités HTTP communes :  

    -   Document par défaut  

    -   Contenu statique  

-   Développement d'applications :  

    -   ASP.NET 3.5 (et les options sélectionnées automatiquement)  

    -   ASP.NET 4.5 (et les options sélectionnées automatiquement)  

    -   Extensibilité .NET 3.5  

    -   Extensibilité .NET 4.5  

-   Sécurité :  

    -   Authentification Windows  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

#### <a name="computer-memory"></a>Mémoire de l’ordinateur  

-   L’ordinateur hébergeant ce rôle de système de site doit avoir au moins 5 % de mémoire disponible pour permettre au rôle de système de site de traiter les demandes.  

-   Quand ce rôle de système de site est colocalisé avec un autre rôle de système de site ayant la même exigence, la quantité de mémoire nécessaire pour l’ordinateur n’augmente pas, mais elle reste à une valeur minimale de 5 %.  



##  <a name="bkmk_2012FSPpreq"></a> Point d’état de secours 

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server 

-   Extensions du serveur BITS (et options sélectionnées automatiquement) ou services BITS (et options sélectionnées automatiquement) 

#### <a name="iis-configuration"></a>Configuration IIS 

La configuration IIS par défaut est nécessaire, avec les ajouts suivants :  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  



##  <a name="bkmk_2012MPpreq"></a> Point de gestion  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

-   Extensions du serveur BITS (et options sélectionnées automatiquement) ou services BITS (et options sélectionnées automatiquement)  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Développement d'applications :  

    -   Extensions ISAPI  

-   Sécurité :  

    -   Authentification Windows  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

    -   Compatibilité WMI d'IIS 6  



##  <a name="bkmk_2012RSpoint"></a> Point de Reporting Services  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

#### <a name="sql-server-reporting-services"></a>SQL Server Reporting Services  

-   Installez et configurez au moins une instance de SQL Server pour prendre en charge SQL Server Reporting Services avant d’installer le point de rapport.  

-   L’instance que vous utilisez pour SQL Server Reporting Services peut être la même que celle utilisée pour la base de données du site.  

-   En outre, l’instance que vous utilisez peut être partagée avec d’autres produits System Center, dès lors que ceux-ci n’ont pas de restrictions pour le partage de l’instance de SQL Server.  



##  <a name="bkmk_SCPpreq"></a> Point de connexion de service  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

     Pendant l’installation de ce rôle de système de site, Configuration Manager installe automatiquement .NET Framework 4.5.2. Cette installation peut placer le serveur dans un état d’attente redémarrage. Si un redémarrage est en attente pour .NET Framework, il est possible que les applications .NET ne puissent pas s’exécuter tant que le serveur n’a pas redémarré et que l’installation n’est pas terminée.  

#### <a name="visual-c-redistributable"></a>Redistributable Visual C++  

-   Configuration Manager installe Microsoft Visual C++ 2013 Redistributable Package sur chaque ordinateur hébergeant un point de distribution.  

-   Le rôle de système de site nécessite la version x64.  



##  <a name="bkmk_2012SUPpreq"></a> Point de mise à jour logicielle  

#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 3.5 SP1 (ou version ultérieure)  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 

La configuration IIS par défaut est nécessaire.

#### <a name="windows-server-update-services"></a>Windows Server Update Services  

-   Installez le rôle serveur Windows Server Update Services sur un ordinateur avant d’installer un point de mise à jour logicielle.  

-   Pour plus d’informations, consultez [Planifier les mises à jour logicielles](/sccm/sum/plan-design/plan-for-software-updates).  

> [!NOTE]  
> Lorsque vous utilisez un point de mise à jour logicielle sur un serveur autre que le serveur de site, vous devez installer la console d’administration WSUS sur le serveur de site.   

##  <a name="bkmk_2012SMPpreq"></a> Point de migration d'état  
<!--SCCMDocs issue 645-->
#### <a name="windows-server-roles-and-features"></a>Rôles et fonctionnalités Windows Server  

-   .NET Framework 3.5 (ou version ultérieure).  

-   .NET Framework 4.5.2, 4.6.1, 4.6.2, 4.7, 4.7.1 ou 4.7.2 :  

     Pendant l’installation de ce rôle de système de site, Configuration Manager installe automatiquement .NET Framework 4.5.2. Cette installation peut placer le serveur dans un état d’attente redémarrage. Si un redémarrage est en attente pour .NET Framework, il est possible que les applications .NET ne puissent pas s’exécuter tant que le serveur n’a pas redémarré et que l’installation n’est pas terminée.  

    -   Activation de HTTP (et des options sélectionnées automatiquement)  

    -   ASP.NET 4.5  

#### <a name="iis-configuration"></a>Configuration IIS  

-   Fonctionnalités HTTP communes :  

    -   Document par défaut  

-   Développement d'applications :  

    -   ASP.NET 3.5 (et les options sélectionnées automatiquement)  

    -   Extensibilité .NET 3.5  

    -   ASP.NET 4.5 (et les options sélectionnées automatiquement)  

    -   .NET Extensibility 4.5  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  



##  <a name="bkmk_2008"></a> Conditions préalables pour Windows Server 2008 R2 et Windows Server 2008  

Windows Server 2008 et Windows Server 2008 R2 bénéficient désormais du support étendu au lieu du support standard, comme indiqué dans la [Politique de support Microsoft](https://support.microsoft.com/lifecycle). Pour plus d’informations sur la prise en charge à venir de ces systèmes d’exploitation utilisés comme serveurs de système de site avec Configuration Manager, consultez [Systèmes d’exploitation serveur supprimés et dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#server-os).  

Ces versions de système d’exploitation ne sont pas prises en charge pour les serveurs de site ou la plupart des rôles de système de site. Elles sont toujours prises en charge pour le rôle de système de site du point de distribution, notamment les points de distribution d’extraction, ainsi que pour PXE et la multidiffusion.


###  <a name="bkmk_2008dppreq"></a> Point de distribution  

#### <a name="iis-configuration"></a>Configuration IIS

Vous pouvez utiliser la configuration IIS par défaut ou une configuration personnalisée. Pour utiliser une configuration IIS personnalisée, vous devez activer les options suivantes pour IIS :  

-   Développement d'applications :  

    -   Extensions ISAPI  

-   Sécurité :  

    -   Authentification Windows  

-   Compatibilité avec la gestion IIS 6 :  

    -   Compatibilité avec la métabase de données IIS 6  

    -   Compatibilité WMI d'IIS 6  

Quand vous utilisez une configuration IIS personnalisée, vous pouvez supprimer les options qui ne sont pas nécessaires, comme les éléments suivants :  

-   Fonctionnalités HTTP communes :  

    -   Redirection HTTP  

-   Scripts et outils de gestion IIS  

#### <a name="windows-feature"></a>Fonctionnalité Windows  

-   Compression différentielle à distance  

#### <a name="visual-c-redistributable"></a>Redistributable Visual C++  

-   Configuration Manager installe Microsoft Visual C++ 2013 Redistributable Package sur chaque ordinateur hébergeant un point de distribution.  

-   La version installée dépend de la plateforme de l’ordinateur (x86 ou x64).  

#### <a name="microsoft-azure"></a>Microsoft Azure  

-   Pour héberger un point de distribution, vous pouvez utiliser un service cloud dans Azure.  

#### <a name="to-support-pxe-or-multicast"></a>Pour prendre en charge PXE ou la multidiffusion  

-   Installez et configurez le rôle WDS (Windows Deployment Services) de Windows Server.  

    > [!NOTE]  
    >  WDS s’installe et se configure automatiquement quand vous configurez un point de distribution pour prendre en charge PXE ou la multidiffusion sur un serveur exécutant Windows Server 2012 ou une version ultérieure.  

-   À partir de la version 1806, activez un répondeur PXE sur un point de distribution sans utiliser les Services de déploiement Windows.  

Pour plus d'informations, consultez [Installer et configurer des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_config-pxe).

<!--sms.503672 -Clarified BITS use-->
> [!NOTE]  
> Lorsque le point de distribution transfère du contenu, il le fait à l’aide du **Service de transfert intelligent en arrière-plan** (BITS) intégré au système d’exploitation Windows. Le rôle du point de distribution ne requiert pas que la fonctionnalité BITS IIS Server Extension facultative soit installée car le client n’y charge pas d’informations.   

