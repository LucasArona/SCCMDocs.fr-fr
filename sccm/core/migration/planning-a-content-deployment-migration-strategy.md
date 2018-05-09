---
title: Migrer du contenu
titleSuffix: Configuration Manager
description: Utilisez des points de distribution pour gérer du contenu pendant que vous migrez des données vers une hiérarchie de destination System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 66f7759c-6272-4116-aad7-0d05db1d46cd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d261b246c0718777be56425c7783d05f767575df
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="plan-a-content-deployment-migration-strategy-in-system-center-configuration-manager"></a>Planifier une stratégie de migration de déploiement de contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Durant le processus de migration des données vers une hiérarchie de destination System Center Configuration Manager, les clients Configuration Manager des hiérarchies source et de destination peuvent conserver l’accès au contenu que vous avez déployé dans la hiérarchie source. Vous pouvez aussi utiliser la migration pour mettre à niveau ou réaffecter des points de distribution de la hiérarchie source afin qu’ils deviennent des points de distribution dans la hiérarchie de destination. Lorsque vous partagez et mettez à niveau ou réaffectez des points de distribution, cette stratégie permet d'éviter d'avoir à redéployer du contenu vers de nouveaux serveurs dans la hiérarchie de destination pour les clients dont vous effectuez la migration.  

Bien que vous puissiez recréer et distribuer le contenu dans la hiérarchie de destination, vous pouvez également utiliser les options suivantes pour gérer ce contenu :  

-   Partagez des points de distribution dans la hiérarchie source avec des clients dans la hiérarchie de destination.  

-   Mettez à niveau les points de distribution Configuration Manager 2007 autonomes ou les sites secondaires Configuration Manager 2007 dans la hiérarchie source pour qu’ils deviennent des points de distribution dans la hiérarchie de destination.  

-   Réaffectez les points de distribution d’une hiérarchie source System Center Configuration Manager à un site de la hiérarchie de destination.  

Utilisez les sections suivantes pour vous aider à planifier le déploiement de contenu pendant la migration :  

-   [Partager des points de distribution entre une hiérarchie source et une hiérarchie de destination](#About_Shared_DPs_in_Migration)  

-   [Planifier la mise à niveau des points de distribution partagés Configuration Manager 2007](#Planning_to_Upgrade_DPs)  

    -   [Processus de mise à niveau des points de distribution](#BKIMK_UpgradeProcess)  

    -   [Planifier la mise à niveau des sites secondaires Configuration Manager 2007](#BKMK_UpgradeSS)  

-   [Planifier la réaffectation des points de distribution System Center Configuration Manager](#BKMK_ReassignDistPoint)  

    -   [Processus de réattribution des points de distribution](#BKMK_ReassignProcess)  

-   [Propriété du contenu lors de la migration de contenu](#About_Migrating_Content)  

##  <a name="About_Shared_DPs_in_Migration"></a> Partager des points de distribution entre une hiérarchie source et une hiérarchie de destination  
Lors de la migration, vous pouvez partager les points de distribution d'une hiérarchie source avec la hiérarchie de destination. Vous pouvez utiliser des points de distribution partagés pour rendre le contenu migré à partir d'une hiérarchie source immédiatement accessible aux clients situés dans la hiérarchie de destination sans avoir à recréer ce contenu ni à le redistribuer vers de nouveaux points de distribution dans la hiérarchie de destination. Lorsque les clients situés dans la hiérarchie de destination demandent le contenu déployé sur les points de distribution que vous avez partagés, ces points de distribution partagés peuvent être proposés aux clients comme emplacements de contenu valides.  

 En plus de constituer un emplacement de contenu valide pour les clients dans la hiérarchie de destination pendant que la migration à partir de la hiérarchie source est active, il est possible de mettre à niveau ou de réaffecter un point de distribution dans la hiérarchie de destination. Vous pouvez mettre à niveau des points de distribution partagés Configuration Manager 2007 et réaffecter des points de distribution partagés System Center 2012 Configuration Manager. Lorsque vous mettez à niveau ou réaffectez un point de distribution partagé, le point de distribution est supprimé de la hiérarchie source et il devient un point de distribution dans la hiérarchie de destination. Après avoir mis à niveau ou réaffecté un point de distribution partagé, vous pouvez continuer à utiliser le point de distribution dans la hiérarchie de destination une fois la migration à partir de la hiérarchie source terminée. Pour plus d’informations sur la mise à niveau d’un point de distribution partagé, consultez [Planifier la mise à niveau des points de distribution partagés Configuration Manager 2007](#Planning_to_Upgrade_DPs). Pour plus d’informations sur la façon de réaffecter un point de distribution partagé, consultez [Planifier la réaffectation des points de distribution System Center Configuration Manager](#BKMK_ReassignDistPoint).  

 Vous pouvez choisir de partager des points de distribution de n'importe quel site source de votre hiérarchie source. Quand vous partagez des points de distribution pour un site source, les sites secondaires enfants sont partagés sur chaque point de distribution concerné sur ce site principal et sur chacun des sites principaux. Pour qu’un point de distribution puisse être partagé, le serveur de système de site qui héberge le point de distribution doit être configuré avec un nom de domaine complet (FQDN). Les points de distribution configurés avec un nom NetBIOS sont ignorés.  

> [!TIP]  
>  Avec Configuration Manager 2007, vous n’avez pas besoin de configurer un nom de domaine complet pour les serveurs de système de site.  

Utilisez les informations suivantes pour planifier les points de distribution partagés :  

-   Les points de distribution que vous partagez doivent respecter les conditions préalables applicables aux points de distribution partagés. Pour plus d’informations sur ces prérequis, consultez [Configurations requises pour la migration](../../core/migration/prerequisites-for-migration.md#BKMK_Required_Configurations) dans [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

-   L'action de partage de point de distribution est un paramètre de site qui partage tous les points de distribution admissibles sur un site source et sur les sites secondaires enfants directs. Vous ne pouvez pas sélectionner des points de distribution individuels à partager lorsque vous activez le partage de point de distribution.  

-   Les clients dans la hiérarchie de destination peuvent recevoir des informations d'emplacement du contenu pour les packages distribués sur les points de distribution partagés à partir de la hiérarchie source. Pour les points de distribution d’une hiérarchie source Configuration Manager 2007, cela inclut les points de distribution de branche, les points de distribution sur des partages de serveur et les points de distribution standard.  

    > [!WARNING]  
    >  Si vous modifiez la hiérarchie source, les points de distribution partagés de la hiérarchie source d'origine ne sont plus disponibles et ne peuvent pas être proposés comme emplacements de contenu aux clients dans la hiérarchie de destination. Si vous reconfigurez la migration pour utiliser la hiérarchie source d'origine, les points de distribution partagés précédents sont restaurés en tant que serveurs valides d'emplacement du contenu.  

-   Lorsque vous faites migrer un package qui est hébergé sur un point de distribution partagé, la version du package doit rester la même dans les hiérarchies source et de destination. Lorsque la version du package n'est pas la même dans la hiérarchie source et la hiérarchie de destination, les clients dans la hiérarchie de destination ne peuvent pas récupérer ce contenu à partir du point de distribution partagé. Par conséquent, si vous mettez à jour un package dans la hiérarchie source, vous devez à nouveau faire migrer les données du package pour que les clients dans la hiérarchie de destination puissent récupérer ce contenu à partir d'un point de distribution partagé.  

    > [!NOTE]  
    >  Quand vous affichez les détails d’un package hébergé sur un point de distribution partagé, le nombre de packages qui s’affichent comme **Packages migrés hébergés** sous l’onglet **Points de distribution partagés** des sites source n’est pas mis à jour avant la fin du cycle suivant de collecte des données.  

-   Vous pouvez afficher les points de distribution partagés et leurs propriétés dans le nœud **Hiérarchie source** de l’espace de travail **Administration** dans la console Configuration Manager connectée à la hiérarchie de destination.  

-   Vous ne pouvez pas utiliser un point de distribution partagé d’une hiérarchie source Configuration Manager 2007 pour héberger des packages pour Microsoft Application Virtualization (App-V). Les packages App-V doivent migrer et être convertis pour l'utilisation par les clients dans la hiérarchie de destination. Toutefois, vous pouvez utiliser un point de distribution partagé d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager afin d’héberger des packages App-V pour des clients dans une hiérarchie de destination.  

-   Quand vous partagez un point de distribution protégé d’une hiérarchie source Configuration Manager 2007, la hiérarchie de destination crée un groupe de limites qui inclut les emplacements réseau protégés de ce point de distribution. Vous ne pouvez pas changer ce groupe de limites dans la hiérarchie de destination. Toutefois, si vous changez les informations des limites protégées pour le point de distribution dans la hiérarchie source Configuration Manager 2007, ce changement est reflété dans la hiérarchie de destination après le prochain cycle de collecte des données.  

    > [!NOTE]  
    >  Les sites System Center 2012 Configuration Manager et System Center Configuration Manager utilisent le concept de points de distribution préférés au lieu des points de distribution protégés. Cette condition s’applique uniquement aux points de distribution partagés à partir de sites source Configuration Manager 2007.  

Les points de distribution éligibles ne sont pas visibles dans la console Configuration Manager tant que vous n’avez pas partagé de points de distribution d’un site source. Une fois que vous avez partagé des points de distribution, seuls les points de distribution effectivement partagés sont répertoriés.  

Une fois que vous avez partagé des points de distribution, vous pouvez modifier la configuration de n'importe quel point de distribution partagé dans la hiérarchie source. Les modifications que vous apportez à la configuration d'un point de distribution sont répercutées dans la hiérarchie de destination à l'issue du cycle suivant de collecte des données. Les points de distribution que vous avez mis à jour pour qu'ils puissent être partagés le sont automatiquement, tandis que ceux qui ne peuvent plus l'être cessent de partager des points de distribution. Par exemple, vous pouvez avoir d’un point de distribution qui n’est pas configuré avec un nom de domaine complet d’intranet et qui n’était pas initialement partagé avec la hiérarchie de destination. Après avoir configuré le nom de domaine complet du point de distribution, le cycle suivant de collecte des données identifie cette configuration et le point de distribution est alors partagé avec la hiérarchie de destination.  

##  <a name="Planning_to_Upgrade_DPs"></a> Planifier la mise à niveau des points de distribution partagés Configuration Manager 2007  
Quand vous effectuez une migration à partir d’une hiérarchie source Configuration Manager 2007, vous pouvez mettre à niveau un point de distribution partagé pour en faire un point de distribution System Center Configuration Manager. Vous pouvez mettre à niveau des points de distribution sur des sites principaux et sur des sites secondaires. Le processus de mise à niveau supprime le point de distribution de la hiérarchie Configuration Manager 2007, et le convertit en serveur de système de site dans la hiérarchie de destination. Ce processus copie également le contenu existant qui se trouve sur le point de distribution vers un nouvel emplacement sur l’ordinateur du point de distribution. Le processus de mise à niveau modifie alors la copie du contenu pour créer le magasin d'instances uniques à utiliser avec le déploiement de contenu dans la hiérarchie de destination. Ainsi, quand vous mettez à niveau un point de distribution, vous n’avez pas besoin de redistribuer le contenu migré qui était hébergé sur le point de distribution Configuration Manager 2007.  

Une fois que Configuration Manager a converti le contenu en stockage SIS (Single-Instance-Store), Configuration Manager supprime le contenu source d’origine sur l’ordinateur du point de distribution pour libérer de l’espace disque. Configuration Manager n’utilise pas l’emplacement du contenu source d’origine.  

Tous les points de distribution Configuration Manager 2007 que vous pouvez partager ne remplissent pas les conditions d’une mise à niveau vers System Center Configuration Manager. Pour être éligible à une mise à niveau, un point de distribution Configuration Manager 2007 doit remplir les conditions de la mise à niveau. Ces conditions incluent le serveur de système de site sur lequel le point de distribution est installé et le type de point de distribution Configuration Manager 2007 installé. Par exemple, vous ne pouvez pas mettre à niveau un type de point de distribution qui est installé sur l'ordinateur serveur de site au niveau d'un site principal, mais vous pouvez mettre à niveau un point de distribution standard qui est installé sur l'ordinateur serveur de site au niveau d'un site secondaire.  

> [!NOTE]  
>  Vous ne pouvez mettre à niveau que les points de distribution partagés Configuration Manager 2007 qui se trouvent sur un ordinateur exécutant une version de système d’exploitation prise en charge en tant que point de distribution dans la hiérarchie de destination. Par exemple, bien que vous puissiez partager un point de distribution Configuration Manager 2007 situé sur un ordinateur exécutant Windows Vista, vous ne pouvez pas le mettre à niveau, car System Center Configuration Manager ne prend pas en charge l’utilisation de ce système d’exploitation en tant que point de distribution.  

Le tableau suivant répertorie les emplacements pris en charge pour chaque type de point de distribution Configuration Manager 2007 pouvant être mis à niveau.  

|Type de point de distribution|Point de distribution sur un ordinateur du système de site autre que le serveur de site|Point de distribution sur un ordinateur du système de site autre que le serveur de site et hébergeant d'autres rôles de système de site|Point de distribution sur un serveur de site secondaire|  
|--------------------------------|-----------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|---------------------------------------------------|  
|Point de distribution standard|Oui|Non|Oui|  
|Point de distribution sur des partages de serveur<sup>1</sup>|Oui|Non|Non|  
|Point de distribution de branche|Oui|Non|Non|  

 <sup>1</sup> System Center Configuration Manager ne prend pas en charge les partages de serveur des systèmes de site, mais il prend en charge la mise à niveau d’un point de distribution Configuration Manager 2007 qui se trouve sur un partage de serveur. Quand vous mettez à niveau un point de distribution Configuration Manager 2007 situé sur un partage de serveur, le type de point de distribution est automatiquement converti en serveur. De plus, vous devez sélectionner le lecteur de l’ordinateur du point de distribution destiné à stocker le magasin de contenu d’instances uniques.  

> [!WARNING]  
>  Avant de mettre à niveau un point de distribution de branche, désinstallez le logiciel client Configuration Manager 2007. Quand vous mettez à niveau un point de distribution de branche sur lequel est installé le logiciel client Configuration Manager 2007, le contenu déployé est supprimé de l’ordinateur, ce qui entraîne l’échec de la mise à niveau du point de distribution.  

Pour identifier les points de distribution qui peuvent être mis à niveau, dans la console Configuration Manager, dans le nœud **Hiérarchie source**, sélectionnez un site source, puis l’onglet **Points de distribution partagés**. Les points de distribution éligibles affichent **Oui** dans la colonne **Éligible à la mise à niveau** .  

Quand vous mettez à niveau un point de distribution installé sur un serveur de site secondaire Configuration Manager 2007, le site secondaire est désinstallé de la hiérarchie source. Bien que ce scénario corresponde à une mise à niveau du site secondaire, cela s'applique uniquement au rôle de système de site de point de distribution. Le résultat est que le site secondaire n'est pas mis à niveau et qu'il est désinstallé. Ceci laisse un seul point de distribution de la hiérarchie de destination sur l’ordinateur qui était le serveur de site secondaire. Si vous envisagez de mettre à niveau le point de distribution sur un site secondaire, consultez [Planifier la mise à niveau des sites secondaires Configuration Manager 2007](#BKMK_UpgradeSS) dans cette rubrique.  

###  <a name="BKIMK_UpgradeProcess"></a> Processus de mise à niveau des points de distribution  
Vous pouvez utiliser la console Configuration Manager pour mettre à niveau les points de distribution Configuration Manager 2007 que vous avez partagés avec la hiérarchie de destination. Quand vous mettez à niveau un point de distribution partagé, le point de distribution est désinstallé du site Configuration Manager 2007. Il est ensuite installé comme point de distribution qui est attaché à un site principal ou secondaire que vous spécifiez dans la hiérarchie de destination. Le processus de mise à niveau crée une copie du contenu migré qui est stocké sur le point de distribution, puis convertit cette copie en magasin de contenu d'instances uniques. Quand Configuration Manager convertit un package en magasin de contenu d’instances uniques, il supprime ce package du partage SMSPKG sur l’ordinateur du point de distribution, sauf si le package comporte une ou plusieurs publications configurées pour **Exécuter le programme à partir du point de distribution**.  

Pour mettre à niveau le point de distribution, Configuration Manager utilise le **compte d’accès au site source** configuré pour collecter des données à partir du fournisseur SMS du site source. Bien que ce compte nécessite uniquement l’autorisation de **lecture** pour permettre aux objets de site de collecter des données du site source, il doit disposer également de l’autorisation de **suppression** et de **modification** dans la classe **Site** pour pouvoir supprimer correctement le point de distribution du site Configuration Manager 2007 durant la mise à niveau.  

> [!NOTE]  
>  Configuration Manager peut convertir le contenu en magasin d’instances uniques sur un seul point de distribution à la fois. Quand vous configurez des mises à niveau de plusieurs point de distribution, les points de distribution sont placés en file d’attente pour la mise à niveau et traités un par un.  

Avant la mise à niveau d'un point de distribution partagé, vérifiez que tout le contenu déployé sur le point de distribution a migré. Le contenu que vous ne faites pas migrer avant de mettre à niveau le point de distribution n'est pas disponible dans la hiérarchie de destination après la mise à niveau. Lorsque vous mettez à niveau un point de distribution, le contenu dans les packages migrés est converti dans un format compatible avec le magasin d'instances uniques de la hiérarchie de destination.  

Pour permettre la mise à niveau d’un point de distribution dans la console Configuration Manager, le serveur de système de site Configuration Manager 2007 doit remplir les conditions suivantes :  

-   La configuration de point de distribution et l'emplacement doivent être éligibles à la mise à niveau.  

-   L’ordinateur du point de distribution doit avoir un espace disque suffisant pour que le contenu puisse être converti du format de stockage de contenu Configuration Manager 2007 vers le format de magasin d’instances uniques. Cette conversion nécessite que l’espace disque disponible soit égal à la taille du package le plus volumineux stocké sur le point de distribution.  

-   L'ordinateur de point de distribution doit exécuter une version de système d'exploitation prise en charge comme un point de distribution dans la hiérarchie de destination.  

    > [!NOTE]  
    >  Quand Configuration Manager vérifie si le point de distribution peut être mis à niveau, il ne valide pas la version du système d’exploitation de l’ordinateur du point de distribution.  

Pour mettre à niveau un point de distribution, dans l’espace de travail **Administration**, développez **Migration**et le nœud **Hiérarchie source**, puis sélectionnez le site qui a le point de distribution à mettre à niveau. Ensuite, dans le volet des détails, sous l'onglet **Points de distribution partagés** , sélectionnez le point de distribution à mettre à niveau.  

Vous pouvez vérifier si le point de distribution est prêt pour la mise à niveau en consultant l’état dans la colonne **Éligible à la réaffectation** .  Ensuite, dans le ruban de la console Configuration Manager, sous l’onglet **Points de distribution**, dans le groupe **Point de distribution**, sélectionnez **Réaffecter**. Ceci ouvre un Assistant que vous utilisez pour terminer la mise à niveau du point de distribution.  

Lorsque vous mettez à niveau un point de distribution partagé, vous devez affecter le point de distribution à un site principal ou secondaire de votre choix dans la hiérarchie de distribution. Une fois que le point de distribution est mis à niveau, gérez le point de distribution comme un point de distribution dans la hiérarchie de destination, comme tout autre point de distribution.  

Vous pouvez surveiller la progression de la mise à niveau d’un point de distribution dans la console Configuration Manager en sélectionnant le nœud **Migration de point de distribution** sous le nœud **Migration** de l’espace de travail **Administration**. Vous pouvez également afficher des informations dans le journal **Migmctrl.log** sur le serveur de site d'administration centrale de la hiérarchie de destination ou dans le journal **distmgr.log** sur le serveur de site dans la hiérarchie de destination qui gère le point de distribution mis à niveau.  

> [!NOTE]  
>  Quand vous mettez à niveau un point de distribution sur la hiérarchie de destination, le rôle de système de site de point de distribution est supprimé du site source Configuration Manager 2007. Cependant, les packages qui ont été envoyés au point de distribution ne sont pas mis à jour dans la hiérarchie Configuration Manager 2007. Dans la console Configuration Manager 2007, les packages envoyés vers le point de distribution continuent de répertorier l’ordinateur du système de site en tant que point de distribution de **Type** **Inconnu**. Les mises à jour suivantes du package dans Configuration Manager 2007 génèrent des rapports d’erreurs du gestionnaire de distribution dans le journal distmgr.log relatif à ce site durant la tentative de mise à jour du package sur le système de site inconnu.  

Si vous décidez de ne pas mettre à niveau un point de distribution partagé, vous pouvez toujours installer un point de distribution de la hiérarchie de destination sur un ancien point de distribution Configuration Manager 2007. Pour pouvoir installer le nouveau point de distribution, vous devez d’abord désinstaller tous les rôles de système de site Configuration Manager 2007 sur l’ordinateur du point de distribution. Cela inclut le site Configuration Manager 2007, s’il s’agit de l’ordinateur serveur de site. Quand vous désinstallez un point de distribution Configuration Manager 2007, le contenu qui a été déployé sur le point de distribution n’est pas supprimé de l’ordinateur.  

###  <a name="BKMK_UpgradeSS"></a> Planifier la mise à niveau des sites secondaires Configuration Manager 2007  
 Quand vous utilisez la migration pour mettre à niveau un point de distribution partagé hébergé sur un serveur de site secondaire Configuration Manager 2007, Configuration Manager met à niveau le rôle de système de site du point de distribution de façon à en faire un point de distribution dans la hiérarchie de destination. Il désinstalle également le site secondaire dans la hiérarchie source. Il en résulte un point de distribution System Center Configuration Manager, mais aucun site secondaire.  

 Pour qu’un point de distribution sur l’ordinateur serveur de site puisse être mis à niveau, Configuration Manager doit pouvoir désinstaller le site secondaire et chaque rôle de système de site présent sur cet ordinateur. En général, un point de distribution partagé sur un partage de serveur Configuration Manager 2007 peut être mis à niveau. Toutefois, lorsqu'il existe un partage de serveur sur le serveur de site secondaire, le site secondaire et tout point de distribution partagé sur cet ordinateur ne sont pas éligibles à la mise à niveau. La raison en est que le partage de serveur est traité comme un objet de système de site supplémentaire quand le processus tente de désinstaller le site secondaire, et que ce processus ne peut pas désinstaller cet objet. Dans ce scénario, vous pouvez activer un point de distribution standard sur le serveur de site secondaire, puis redistribuer le contenu vers ce point de distribution standard. Ce processus n’utilise pas la bande passante du réseau et, une fois le processus terminé, vous pouvez désinstaller le point de distribution sur le partage de serveur, puis mettre à niveau le point de distribution et le site secondaire.  

 Avant de mettre à niveau un point de distribution partagé, vérifiez la configuration du point de distribution dans Configuration Manager 2007 pour éviter de mettre à niveau un point de distribution sur site secondaire que vous souhaitez toujours utiliser avec Configuration Manager 2007. Il s’agit d’une pratique recommandée car après la mise à niveau d’un point de distribution partagé du serveur de site secondaire, le serveur de système de site est supprimé de la hiérarchie Configuration Manager 2007 et il ne peut plus être utilisé avec cette hiérarchie. Lorsque le site secondaire est supprimé, les points de distribution restants sur le site secondaire sont orphelins. Cela signifie qu’ils deviennent non gérés à partir de Configuration Manager 2007, et qu’ils ne sont plus partagés ou éligibles pour une mise à niveau.  

> [!WARNING]  
>  Quand vous affichez des points de distribution partagés dans la console Configuration Manager, aucune indication ne montre qu’un point de distribution partagé se trouve sur un serveur de système de site distant ou sur le serveur de site secondaire.  

 Quand un site secondaire se trouve à un emplacement réseau distant principalement utilisé pour contrôler le déploiement de contenu vers cet emplacement distant, vous pouvez envisager de mettre à niveau les sites secondaires qui ont un point de distribution partagé. Pour pouvoir configurer le contrôle de la bande passante quand vous distribuez du contenu à un point de distribution System Center Configuration Manager, vous pouvez souvent mettre à niveau un site secondaire pour en faire un point de distribution, configurer le point de distribution pour les contrôles de bande passante et éviter d’installer un site secondaire à cet emplacement réseau dans la hiérarchie de destination.  

 Le processus de mise à niveau d’un point de distribution partagé sur un serveur de site secondaire est identique à n’importe quelle autre mise à niveau d’un point de distribution partagé. Le contenu est copié et converti dans le stockage SIS (Single-Instance-Store) utilisé par la hiérarchie de destination. Cependant, quand vous mettez à niveau un point de distribution partagé sur un serveur de site secondaire, le processus de mise à niveau désinstalle également le point de gestion (s’il est présent), puis désinstalle le site secondaire du serveur. Ainsi, le site secondaire est supprimé de la hiérarchie Configuration Manager 2007. Pour désinstaller le site secondaire, Configuration Manager utilise le compte configuré pour recueillir des données à partir du site source.  

 Durant la mise à niveau, il existe un retard entre le moment où le site secondaire Configuration Manager 2007 est désinstallé et le moment où l’installation du point de distribution dans la hiérarchie de destination commence. Le cycle de collecte de données détermine ce décalage pouvant aller jusqu’à quatre heures. Le décalage est destiné à laisser le temps au site secondaire d’être désinstallé avant que l’installation du nouveau point de distribution commence.  

 Pour plus d’informations sur la mise à niveau d’un point de distribution partagé, consultez [Planifier la mise à niveau des points de distribution partagés Configuration Manager 2007](#Planning_to_Upgrade_DPs).  

##  <a name="BKMK_ReassignDistPoint"></a> Planifier la réaffectation des points de distribution System Center Configuration Manager  
 Durant la migration d’une version prise en charge de System Center 2012 Configuration Manager vers une hiérarchie de la même version, vous pouvez réaffecter un point de distribution partagé de la hiérarchie source à un site de la hiérarchie de destination. Cela est similaire au concept de mise à niveau d’un point de distribution Configuration Manager 2007 pour en faire un point de distribution dans la hiérarchie de destination. Vous pouvez réaffecter des points de distribution de sites principaux et de sites secondaires. Cette action de réaffectation d’un point de distribution supprime le point de distribution de la hiérarchie source et convertit l’ordinateur et son point de distribution en serveur de système de site pour un site que vous sélectionnez dans la hiérarchie de destination.  

 Lorsque vous réaffectez un point de distribution, il est inutile de redistribuer le contenu migré qui était hébergé sur le point de distribution du site source. De plus, à l’inverse de la mise à niveau d’un point de distribution Configuration Manager 2007, la réaffectation d’un point de distribution ne nécessite aucun espace disque supplémentaire sur l’ordinateur du point de distribution. La raison en est que, à partir de System Center 2012 Configuration Manager, les points de distribution utilisent le format SIS (Single-Instance-Store) pour le contenu. Le contenu sur l’ordinateur du point de distribution n’a pas besoin d’être converti quand le point de distribution est réaffecté entre les hiérarchies.  

 Pour qu’un point de distribution System Center 2012 Configuration Manager puisse être réaffecté, il doit répondre aux critères suivants :  

-   Le point de distribution partagé doit être installé sur un ordinateur autre que le serveur de site.  

-   Le point de distribution partagé ne peut pas être hébergé avec des rôles de système de site supplémentaires.  

Pour identifier les points de distribution qui peuvent être réaffectés, dans la console Configuration Manager, dans le nœud **Hiérarchie source**, sélectionnez un site source, puis l’onglet **Points de distribution partagés**. Les points de distribution éligibles indiquent **Oui** dans la colonne **Éligible à la réaffectation** (avant System Center 2012 R2 Configuration Manager, cette colonne était nommée **Éligible à la mise à niveau**).  

###  <a name="BKMK_ReassignProcess"></a> Processus de réattribution des points de distribution  
 Vous pouvez utiliser la console Configuration Manager pour réaffecter les points de distribution que vous avez partagés à partir d’une hiérarchie source active. Quand vous réaffectez un point de distribution partagé, le point de distribution est désinstallé du site source, puis installé comme point de distribution attaché à un site principal ou secondaire que vous spécifiez dans la hiérarchie de destination.  

 Pour réaffecter le point de distribution, la hiérarchie de destination utilise le compte d’accès au site source configuré pour collecter des données à partir du fournisseur SMS du site source. Pour plus d’informations sur les autorisations nécessaires et les prérequis supplémentaires, consultez [Prérequis de la migration dans System Center Configuration Manager](../../core/migration/prerequisites-for-migration.md).  

## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrer plusieurs points de distribution partagés en même temps
Depuis la version 1610, vous pouvez utiliser l’option **Réaffecter le point de distribution** pour que Configuration Manager traite en parallèle la réaffectation d’un maximum de 50 points de distribution partagés en même temps. Cela inclut les points de distribution partagés des sites sources pris en charge qui exécutent :  
- Configuration Manager 2007
- System Center 2012 Configuration Manager
- System Center 2012 R2 Configuration Manager
- System Center Configuration Manager (branche actuelle)

Quand vous réaffectez les points de distribution, chaque point de distribution doit pouvoir être mis à niveau ou réaffecté. Le nom de l’action et du processus impliqués, mise à niveau ou réaffectation, dépend de la version de Configuration Manager exécutée par le site source. Les résultats finaux des deux actions sont identiques : le point de distribution est affecté à un des sites Current Branch avec son contenu en place.

Avant la version 1610, Configuration Manager ne pouvait traiter qu’un seul point de distribution à la fois. Vous pouvez désormais réaffecter autant de points de distribution que vous le souhaitez avec les remarques suivantes :  
- Même si vous ne pouvez pas effectuer une sélection multiple des points de distribution à réaffecter, quand vous en avez mis plusieurs en file d’attente, Configuration Manager les traite en parallèle au lieu d’attendre d’en terminer un avant de commencer le suivant.  
- Par défaut, jusqu’à 50 points de distribution sont traités en parallèle à la fois. Une fois la réaffectation du premier point de distribution terminée, Configuration Manager commence à traiter le 51ème, et ainsi de suite.  
- Quand vous utilisez le SDK Configuration Manager, vous pouvez modifier **SharedDPImportThreadLimit** pour ajuster le nombre de points de distribution réaffectés que Configuration Manager peut traiter en parallèle.


##  <a name="About_Migrating_Content"></a> Affecter la propriété du contenu lors de la migration de contenu  
 Lorsque vous migrez du contenu pour des déploiements, vous devez attribuer l'objet de contenu à un site dans la hiérarchie de destination. Ce site devient alors le propriétaire de ce contenu dans la hiérarchie de destination. Bien que le site de plus haut niveau de votre hiérarchie de destination soit le site qui migre les métadonnées du contenu, c’est le site affecté qui utilise les fichiers sources d’origine du contenu sur le réseau.  

 Pour réduire la bande passante réseau utilisée lors de la migration de contenu, transférez la propriété du contenu à un site proche dans la hiérarchie de destination sur le réseau vers l'emplacement de contenu dans la hiérarchie de destination. Comme les informations sur le contenu dans la hiérarchie de destination sont partagées globalement, elles seront disponibles sur chaque site.  

 Bien que les informations sur le contenu soient partagées sur tous les sites en utilisant la réplication de base de données, le contenu que vous affectez à un site principal et que vous déployez ensuite sur des points de distribution sur d’autres sites principaux est transféré en utilisant la réplication basée sur les fichiers. Ce transfert est routé via le site administration centrale, puis vers le site principal supplémentaire. Vous pouvez réduire les transferts de données sur les réseaux à faible bande passante en centralisant les packages que vous prévoyez de distribuer sur plusieurs sites principaux avant ou pendant la migration, quand vous définissez un site comme propriétaire du contenu.
