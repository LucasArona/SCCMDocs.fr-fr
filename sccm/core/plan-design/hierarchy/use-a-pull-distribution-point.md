---
title: Point de distribution d'extraction
titleSuffix: Configuration Manager
description: Découvrez plus d’informations sur les configurations et les limites de l’utilisation d’un point de distribution d’extraction avec Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 008da23a6fedf1666a29754dc41a47c61f8bfbda
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384230"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Utiliser un point de distribution d’extraction avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Quand vous distribuez du contenu à un point de distribution standard dans la console Configuration Manager, le serveur de site envoie (push) le contenu au point de distribution. Un point de distribution d’extraction obtient du contenu en le téléchargeant à partir d’un emplacement source, comme un client.  

Quand vous distribuez du contenu à de nombreux points de distribution, les points de distribution d’extraction peuvent vous aider à réduire la charge de traitement sur le serveur de site. Ils peuvent également accélérer le transfert de contenu vers chaque serveur. Normalement le composant Gestionnaire de distribution sur le serveur de site envoie le contenu à chaque point de distribution. Au lieu de cela, le site se décharge du processus de transfert de contenu sur les points de distribution d’extraction.  

Vous configurez des points de distribution comme des points de distribution d’extraction. Pour chaque point de distribution d’extraction, spécifiez un ou plusieurs points de distribution sources auprès desquels il peut obtenir du contenu. Un point de distribution d’extraction peut obtenir du contenu seulement auprès d’un point de distribution que vous spécifiez comme point de distribution source. 

Quand vous distribuez du contenu à un point de distribution d’extraction dans la console, le serveur de site envoie une notification. Le point de distribution d’extraction télécharge alors le contenu d’un point de distribution source. Un point de distribution d’extraction gère le transfert du contenu en téléchargeant à partir d’un point de distribution qui a déjà une copie du contenu.  

Les points de distribution d’extraction prennent en charge les mêmes configurations et fonctionnalités que les points de distribution classiques. Par exemple, un point de distribution d’extraction prend en charge : 
- Configurations de multidiffusion et PXE
- Validation du contenu
- Distribution de contenu à la demande
- Communications HTTP ou HTTPS provenant des clients
- Les mêmes options de certificat que les autres points de distribution
- Gérer individuellement ou en tant que membre d’un groupe de points de distribution  

> [!IMPORTANT]  
> Bien qu’un point de distribution d’extraction prenne en charge les communications via les protocoles HTTP et HTTPS, lorsque vous utilisez la console Configuration Manager, vous pouvez spécifier uniquement des points de distribution sources configurés pour le protocole HTTP. Le Kit de développement logiciel (SDK) Configuration Manager permet de spécifier un point de distribution source configuré pour le protocole HTTPS.  

Configurez un point de distribution d’extraction quand vous installez le point de distribution. Après avoir créé un point de distribution, configurez-le en tant que point de distribution d’extraction en modifiant les propriétés du rôle. Pour plus d’informations sur l’activation d’un point de distribution comme point de distribution d’extraction, consultez [Point de distribution d’extraction](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#pull-distribution-point).  

Supprimez la configuration comme point de distribution d’extraction en modifiant les propriétés du point de distribution. Quand vous supprimez la configuration d’un point de distribution comme point de distribution d’extraction, il revient à un fonctionnement normal. Le serveur de site gère les transferts de contenu futurs vers le point de distribution.  



### <a name="distribution-process"></a>Processus de distribution

Quand vous distribuez du contenu à un point de distribution d’extraction, la séquence d’événements est la suivante :

-   Quand vous distribuez du contenu à un point de distribution d’extraction dans la console, le composant Package Transfer Manager sur le serveur de site vérifie auprès de la base de données de site que le contenu est disponible sur un point de distribution source. Si Package Transfer Manager détermine que le contenu ne se trouve pas sur un point de distribution source pour le point de distribution d’extraction, il revérifie toutes les 20 minutes jusqu’à ce que le contenu soit disponible.  

-   Une fois la disponibilité du contenu confirmée par Package Transfer Manager, une notification est adressée au point de distribution d'extraction pour télécharger le contenu. Si cette notification échoue, il réessaye en fonction des **Paramètres de nouvelle tentative** du composant de distribution de logiciels pour les points de distribution d’extraction. Après avoir reçu cette notification, le point de distribution d’extraction tente de télécharger le contenu auprès de ses points de distribution sources.  

-   Pendant que le point de distribution d’extraction télécharge le contenu, Package Transfer Manager interroge l’état en fonction des **Paramètres d’interrogation de l’état** du composant de distribution de logiciels pour les points de distribution d’extraction.  Une fois le téléchargement du contenu terminé, le point de distribution d’extraction soumet cet état à un point de gestion.  



## <a name="configure-site-component-settings"></a>Configurer les paramètres de composant de site

Quand vous utilisez un point de distribution d’extraction, passez en revue et configurez les paramètres de composant de site suivants :  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2.  Sélectionnez le site. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sélectionnez **Distribution de logiciels**.  

3. Passez à l’onglet **Point de distribution d’extraction**.  

4.  Dans le groupe **Paramètres de nouvelle tentative**, examinez les valeurs suivantes :  

    -   **Nombre de nouvelles tentatives** : nombre de fois où Package Transfer Manager tente de notifier le point de distribution d’extraction pour télécharger le contenu. Après avoir essayé ce nombre de fois, Package Transfer Manager annule le transfert. Par défaut, cette valeur est de 30.  

    -   **Délai avant une nouvelle tentative (en minutes)** : nombre de minutes qu’attend Package Transfer Manager entre des tentatives. Par défaut, cette valeur est de 20.  

5.  Dans le groupe **Paramètres d’interrogation de l’état**, examinez les valeurs suivantes :  

    -   **Nombre d’interrogations** : nombre de fois que Package Transfer Manager contacte le point de distribution d’extraction pour récupérer l’état de la tâche. S’il atteint ce nombre de fois avant la fin de la tâche, Package Transfer Manager annule le transfert. Par défaut, cette valeur est de 72.   

    -   **Délai avant une nouvelle tentative (en minutes)** : nombre de minutes qu’attend Package Transfer Manager entre des tentatives. Par défaut, cette valeur est de 60.   
    
    > [!NOTE]  
    >  Quand Package Transfer Manager annule une tâche en raison du dépassement du nombre de tentatives d’interrogation, le point de distribution d’extraction continue de télécharger le contenu. Quand il a terminé, le point de distribution d’extraction envoie le message d’état approprié, et la console reflète le nouvel état.  
    


## <a name="limitations"></a>Limitations 

-   Vous ne pouvez pas configurer un point de distribution cloud comme point de distribution d’extraction.  

-   Vous ne pouvez pas configurer le rôle de point de distribution sur un serveur de site comme point de distribution d’extraction.  

-   La configuration de contenu préparé remplace la configuration de point de distribution d’extraction. Si vous activez l’option pour **Activer ce point de distribution pour le contenu préparé** sur un point de distribution d’extraction, il attend le contenu. Il n’extrait pas le contenu du point de distribution source. Comme un point de distribution standard activé pour du contenu préparé, il ne reçoit pas de contenu du serveur de site. Pour plus d’informations, consultez [Contenu préparé](/sccm/core/plan-design/hierarchy/manage-network-bandwidth#BKMK_PrestagingContent).  

-   Un point de distribution d’extraction n’utilise pas les configurations de limite planification ou de taux de transfert. Quand vous configurez un point de distribution précédemment installé comme point de distribution d’extraction, les configurations de la planification et des limites de taux de transfert sont enregistrées, mais elles ne sont pas utilisées. Si, par la suite, vous supprimez la configuration du point de distribution d’extraction, les configurations de la planification et des limites de taux de transfert sont implémentées selon la configuration précédente.  

    > [!NOTE]  
    >  Les onglets **Planification** et **Limites du taux de transfert** ne sont pas visibles dans les propriétés du point de distribution.  

-   Les points de distribution d’extraction n’utilisent pas les paramètres de l’onglet **Général** des **Propriétés du composant de distribution de logiciels** de chaque site. Ces paramètres incluent **Distribution simultanée** et **Nouvelle tentative de multidiffusion**.  

-   Pour transférer du contenu depuis un point de distribution source dans une forêt distante, installez le client Configuration Manager sur le point de distribution d’extraction. Configurez également un compte d’accès réseau qui peut accéder au point de distribution source. À compter de la version 1806, si vous activez l’option de site pour **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**, vous n’avez pas besoin d’un compte d’accès réseau.<!--1358228-->  

-   Si le point de distribution d’extraction est également un client Configuration Manager, la version du client doit correspondre à celle du site Configuration Manager qui installe le point de distribution d’extraction. Le point de distribution d’extraction utilise le composant CCMFramework qui est commun au point de distribution d’extraction et au client Configuration Manager.  



## <a name="about-source-distribution-points"></a>À propos des points de distribution sources  

Quand vous configurez le point de distribution d’extraction, spécifiez un ou plusieurs points de distribution sources :  

-   L’Assistant affiche seulement les points de distribution identifiés comme points de distribution sources possibles.  

-   Un point de distribution d'extraction peut être spécifié en tant que point de distribution source d'un autre point de distribution d'extraction.  

-   Si vous utilisez la console Configuration Manager, seuls des points de distribution prenant en charge le protocole HTTP peuvent être spécifiés comme points de distribution sources.  

-   Utilisez le SDK Configuration Manager pour spécifier un point de distribution source configuré pour HTTPS. Pour utiliser un point de distribution source configuré pour HTTPS, installez le client Configuration Manager sur le point de distribution d’extraction.  

-   À compter de la version 1806, si vos bureaux distants ont une meilleure connexion à Internet, ou pour réduire la charge sur vos liaisons WAN, utilisez un [point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) dans Microsoft Azure comme source. Le point de distribution d’extraction a besoin d’un accès Internet pour communiquer avec Microsoft Azure. Le contenu doit être distribué au point de distribution cloud source.<!--1321554-->  

    > [!Note]  
    > Cette fonctionnalité implique des frais sur votre abonnement Azure pour le stockage de données et la sortie de réseau. Pour plus d’informations, consultez [Coût d’utilisation d’un point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_cost).  


> [!Tip]  
> Quand un point de distribution d’extraction télécharge du contenu à partir d’un point de distribution source, il est considéré comme un client dans la colonne **Client consulté (unique)** du rapport **Résumé de l’utilisation des points de distribution** .  


### <a name="source-priorities"></a>Priorités des sources

-   Affectez une priorité distincte à chaque point de distribution source ou affectez la même priorité à plusieurs points de distribution sources.  

-   La priorité détermine l’ordre dans lequel le point de distribution d’extraction demande du contenu auprès de ses points de distribution sources.  

-   Les points de distribution d'extraction contactent initialement le point de distribution source présentant la valeur de priorité la plus basse. Si plusieurs points de distribution sources ont la même priorité, le point de distribution d’extraction sélectionne de façon aléatoire un des points de distribution source avec cette priorité.  

-   Si le contenu n’est pas disponible sur une source sélectionnée, le point de distribution d’extraction tente de télécharger le contenu à partir d’un autre point de distribution avec la même priorité.  

-   Si aucun des points de distribution avec une priorité donnée n’a le contenu, le point de distribution d’extraction tente de télécharger le contenu à partir d’un point de distribution source avec le niveau de priorité suivant. Il poursuit cette recherche jusqu’à ce que le contenu soit trouvé.   

- Si aucun des points de distribution sources n’a le contenu, le point de distribution d’extraction attend 30 minutes, puis recommence le processus.  



## <a name="inside-the-pull-distribution-point"></a>À l’intérieur du point de distribution d’extraction 

-   Pour gérer le transfert de contenu, les points de distribution d’extraction utilisent le composant **CCMFramework**. Le client Configuration Manager inclut ce composant.  

-   Quand vous activez le point de distribution d’extraction, le site installe **pulldp.msi**. Ce programme d’installation ajoute également le composant CCMFramework. Elle n’a pas besoin du client Configuration Manager.  

-   Une fois le point de distribution d’extraction installé, il utilise principalement le service **CCMExec** pour fonctionner.  

-   Quand le point de distribution d’extraction transfère du contenu, il utilise le **Service de transfert intelligent en arrière-plan** (BITS) intégré dans Windows. Un point de distribution d’extraction ne nécessite pas l’installation de l’extension BITS pour le serveur IIS.<!--sms.503672 -Clarified BITS use-->

-  Pour obtenir des détails sur le fonctionnement, consultez les fichiers journaux suivants sur le point de distribution d’extraction :  
    - **DataTransferService.log**
    - **PullDP.log**



## <a name="see-also"></a>Voir aussi  
 [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)   
