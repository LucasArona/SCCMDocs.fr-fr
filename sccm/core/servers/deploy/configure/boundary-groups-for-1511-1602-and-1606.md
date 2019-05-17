---
title: Groupes de limites pour 1511, 1602 et 1606
titleSuffix: Configuration Manager
description: Utilisez des groupes de limites avec les versions 1511, 1602 et 1606 de Configuration Manager.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f70ff9b3be4c9f1e1726bbdd887d86760e9808
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499023"
---
# <a name="boundary-groups-for-system-center-configuration-manager-version-1511-1602-and-1606"></a>Groupes de limites pour les versions 1511, 1602 et 1606 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*
<!-- This topic drops from TOC with the release of version 1706 -->

Les informations contenues dans cette rubrique sont spécifiques à l’utilisation des groupes de limites avec les versions 1511, 1602 et 1606 de System Center Configuration Manager.
Si vous utilisez la version 1610 ou une version ultérieure, consultez la page [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups) pour plus d’informations sur la façon d’utiliser les groupes de limites remaniés.  


##  <a name="BKMK_BoundaryGroups"></a> Groupes de limites  
 Créer des groupes de limites vous permet de regrouper de façon logique des emplacements réseau (limites) pour faciliter la gestion de votre infrastructure. Vous devez attribuer des limites à des groupes de limites avant de pouvoir utiliser le groupe de limites. Les clients utilisent la configuration du groupe de limites pour les opérations suivantes :  

-   Attribution automatique du site  

-   Emplacement du contenu  

-   Points de gestion préférés

    Si vous utilisez des points de gestion préférés, vous devez activer cette option pour la hiérarchie et non pas à partir de la configuration du groupe de limites. Consultez la procédure *Pour activer l’utilisation des points de gestion préférés* plus loin dans cette rubrique.  

Quand vous configurez des groupes de limites, vous ajoutez une ou plusieurs limites au groupe de limites. Vous configurez ensuite des paramètres supplémentaires utilisables par les clients situés sur ces limites.  

#### <a name="to-create-a-boundary-group"></a>Pour créer un groupe de limites  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un groupe limite**.  

3.  Dans la boîte de dialogue **Créer un groupe limite**, choisissez l’onglet **Général**, puis entrez un **Nom** pour ce groupe de limites.  

4.  Choisissez **OK** pour enregistrer le nouveau groupe de limites.  

#### <a name="to-set-up-a-boundary-group"></a>Pour configurer un groupe de limites  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Choisissez le groupe de limites que vous souhaitez modifier.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, choisissez l’onglet **Général** pour modifier les limites membres de ce groupe de limites :  

    -   Pour ajouter des limites, choisissez **Ajouter**, cochez la case d’une ou plusieurs limites, puis cliquez sur **OK**.  

    -   Pour supprimer des limites, sélectionnez la limite, puis choisissez **Supprimer**.  

5.  Choisissez l’onglet **Références** pour modifier l’attribution de site et la configuration de serveur de système de site associée :  

    -   Pour autoriser ce groupe de limites à être utilisé par les clients pour l’attribution de site, cochez la case **Utiliser ce groupe limite pour l’attribution de site**, puis choisissez un site dans la liste déroulante **Site attribué**.  

    -   Pour configurer les serveurs de système de site disponibles associés à ce groupe de limites :  

    1.  Choisissez **Ajouter**, puis cochez la case d’un ou plusieurs serveurs. Les serveurs sont ajoutés en tant que serveurs de système de site associés à ce groupe de limites. Seuls les serveurs sur lesquels un rôle de système de site pris en charge est installé sont disponibles.  

        > [!NOTE]  
        >  Vous pouvez sélectionner n'importe quelle combinaison de systèmes de site disponibles à partir de n'importe quel site dans la hiérarchie. Les systèmes de site sélectionnés figurent sous l'onglet **Systèmes de site** des propriétés de chaque limite appartenant à ce groupe de limites.  

    2.  Pour supprimer un serveur de ce groupe de limites, choisissez le serveur, puis **Supprimer**.  

        > [!NOTE]  
        >  Pour ne plus utiliser ce groupe de limites pour l’association des systèmes de site, vous devez supprimer tous les serveurs répertoriés comme serveurs de système de site associés.  

    3.  Pour modifier la vitesse de connexion réseau d’un serveur de système de site pour ce groupe de limites, choisissez le serveur, puis **Modifier la connexion**.  

         Par défaut, la vitesse de connexion pour chaque système de site est **Rapide**, mais vous pouvez sélectionner une vitesse **Lente**. La vitesse de connexion réseau et la configuration d'un déploiement déterminent si un client peut télécharger du contenu à partir du serveur.  

6.  Choisissez **OK** pour fermer les propriétés du groupe de limites et enregistrer la configuration.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>Pour associer un serveur de déploiement de contenu ou un point de gestion à un groupe de limites  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de la hiérarchie** >  **Groupes de limites**.  

2.  Choisissez le groupe de limites que vous souhaitez modifier.  

3.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans la boîte de dialogue **Propriétés** du groupe de limites, choisissez l’onglet **Références**.  

5.  Sous **Sélectionner des serveurs de système de site**, choisissez **Ajouter**, cochez la case des serveurs de système de site que vous souhaitez associer à ce groupe de limites, puis choisissez **OK**.  

6.  Choisissez **OK** pour fermer la boîte de dialogue et enregistrer la configuration du groupe de limites.  

#### <a name="to-enable-use-of-preferred-management-points"></a>Pour activer l’utilisation des points de gestion préférés  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Configuration de site** > **Sites** puis, sous l’onglet **Accueil**, choisissez **Paramètres de hiérarchie**.  

2.  Sous l’onglet **Général** de **Paramètres de hiérarchie**, choisissez **Les clients préfèrent utiliser les points de gestion spécifiés dans les groupes de limites**.  

3.  Choisissez **OK** pour fermer la boîte de dialogue et enregistrer la configuration.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>Pour configurer un site de secours pour l’attribution de site automatique  

1. Dans la console Configuration Manager, choisissez **Administration** > **Configuration du site** >  **Sites**.  

2. Sous l’onglet **Accueil**, dans le groupe **Sites**, choisissez **Paramètres de hiérarchie**.  

3. Sous l’onglet **Général**, cochez la case **Utiliser un site de secours**, puis choisissez un site dans la liste déroulante **Site de secours**.  

4. Choisissez **OK** pour enregistrer la configuration.  

   Les sections suivantes fournissent des détails supplémentaires sur les configurations de groupes de limites.  

###  <a name="BKMK_BoundarySiteAssignment"></a> À propos de l’attribution de site  
 Vous pouvez configurer chaque groupe de limites avec un site attribué pour les clients.  

-   Quand un client récemment installé utilise l’attribution automatique de site, il rejoint le site attribué d’un groupe de limites qui englobe l’emplacement réseau actuel du client.  

-   Un client attribué à un site ne modifie pas son attribution de site quand il change d’emplacement réseau. Par exemple, si le client est en itinérance sur un nouvel emplacement réseau représenté par une limite dans un groupe de limites disposant d’une attribution de site différente, le site attribué au client n’est pas modifié.  

-   Lorsque la découverte de systèmes Active Directory détecte une nouvelle ressource, les informations sur le réseau de la ressource découverte sont évaluées en fonction des limites dans les groupes de limites. Ce processus associe la nouvelle ressource à un site attribué pour une utilisation par la méthode d'installation poussée du client.  

-   Quand une limite est membre de plusieurs groupes de limites auxquels différents sites sont attribués, les clients sélectionnent l’un des sites de manière aléatoire.  

-   Les modifications apportées à un site attribué à des groupes de limites s’appliquent uniquement aux nouvelles actions d’attribution de site. Les clients déjà attribués à un site ne ré-évaluent pas leur attribution à un site en fonction des changements apportés à la configuration du groupe de limites (ou à leur emplacement réseau).  

Pour en savoir plus sur l’attribution de site client, consultez [Utilisation de l’attribution automatique de site pour les ordinateurs](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment) dans [Guide pratique pour attribuer des clients à un site dans System Center Configuration Manager](../../../../core/clients/deploy/assign-clients-to-a-site.md).  

###  <a name="BKMK_BoundaryContentLocation"></a> À propos de l’emplacement du contenu  
 Vous pouvez configurer chaque groupe de limites avec un ou plusieurs points de distribution et points de migration d’état, mais aussi associer les mêmes points de distribution et points de migration d’état à plusieurs groupes de limites.  

-   **Lors de la distribution de logiciels**, les clients demandent un emplacement pour le contenu de déploiement. Configuration Manager envoie au client une liste de points de distribution associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client.  

-   **Durant le déploiement de système d’exploitation**, les clients demandent un emplacement où envoyer ou recevoir des informations sur la migration de leur état. Configuration Manager envoie au client une liste de points de migration d’état associés à chaque groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche à partir duquel transférer le contenu ou les informations sur la migration de l’état.  

###  <a name="BKMK_PreferredMP"></a> À propos des points de gestion préférés  
 Les points de gestion préférés permettent à un client d’identifier un point de gestion associé à son emplacement réseau actuel (limite) avec celui-ci.  

-   Un client essaie d’utiliser un point de gestion préféré de son site attribué avant d’en utiliser un qui n’est pas configuré comme préféré.  

-   Pour utiliser cette option, vous devez l’activer pour la hiérarchie, puis configurer des groupes de limites au niveau de chaque site principal pour inclure les points de gestion à associer aux limites de ces groupes de limites.  

-   Quand les points de gestion préférés sont configurés et qu’un client organise sa propre liste de points de gestion, il place les points de gestion préférés en haut de sa liste de points de gestion attribués (qui comprend tous les points de gestion du site attribué du client).  

> [!NOTE]  
>  Quand un client est en itinérance, comme dans le cas d’un ordinateur portable déplacé vers un emplacement de bureau distant, et change d’emplacement réseau, il peut utiliser un point de gestion (ou un point de gestion proxy) du site local à son nouvel emplacement avant d’essayer d’utiliser un point de gestion de son site attribué (qui comprend les points de gestion préférés).  Consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md) pour plus d’informations.  

###  <a name="BKMK_BoundaryOverlap"></a> À propos du chevauchement des limites  
 Configuration Manager prend en charge les configurations de limites se chevauchant pour l’emplacement du contenu :  

-   **Quand un client demande du contenu** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de distribution qui disposent du contenu.  

-   **Quand un client demande à un serveur d’envoyer ou de recevoir des informations sur la migration de son état** et que l’emplacement réseau du client appartient à plusieurs groupes de limites, Configuration Manager envoie au client une liste de tous les points de migration d’état associés à un groupe de limites qui inclut l’emplacement réseau actuel du client.  

Ce comportement permet au client de sélectionner le serveur le plus proche à partir duquel transférer le contenu ou les informations sur la migration de l’état.  

###  <a name="BKMK_BoudnaryNetworkSpeed"></a> À propos de la vitesse de connexion réseau  
 Vous pouvez définir la vitesse de connexion réseau pour chaque serveur de système de site dans un groupe de limites. Ce paramètre s’applique aux clients qui se connectent à un système de site basé sur cette configuration de groupes de limites. Le même serveur de système de site peut avoir une autre vitesse de connexion définie dans des groupes de limites différents.  

 Par défaut, la vitesse de connexion réseau est **Rapide**, mais vous pouvez sélectionner une vitesse **Lente**. La vitesse de connexion réseau et la configuration de déploiement vérifient si un client peut télécharger du contenu à partir d’un point de distribution quand le client est dans un groupe de limites associé.  

 Pour en savoir plus sur les effets de la vitesse de connexion réseau sur l’obtention du contenu par les clients, consultez [Scénarios d’emplacement source de contenu](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
