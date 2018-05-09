---
title: Composants de site
titleSuffix: Configuration Manager
description: Apprenez à configurer des composants de site pour modifier le comportement des rôles système de site et la création des rapports d’état de site.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: da7537ff9cda198f938eafdfc5db198e79a2cb5b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="site-components-for-system-center-configuration-manager"></a>Composants de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Sur chaque site System Center Configuration Manager, vous pouvez configurer des composants de site pour modifier le comportement des rôles système de site et la création des rapports d’état de site. Les configurations de composants de site s’appliquent à un site donné et à chaque instance d’un rôle de système de site applicable au niveau de ce site.  

## <a name="about-site-components"></a>À propos des composants de site  
 La plupart des options des différents composants de site sont suffisamment explicites quand elles apparaissent dans la console Configuration Manager. Toutefois, les informations suivantes peuvent être utiles pour mieux comprendre certaines configurations plus complexes ou vous diriger vers du contenu supplémentaire qui les explique.  

### <a name="software-distribution"></a>Distribution de logiciels  

-   **Paramètres de distribution de contenu :** vous pouvez spécifier des paramètres qui modifient la façon dont le serveur de site transfère du contenu vers ses points de distribution. Si vous augmentez les valeurs des paramètres de distribution simultanée, la distribution de contenu risque d’utiliser davantage de bande passante réseau.  

-   **Compte d’accès réseau :** pour plus d’informations sur la configuration et l’utilisation du compte d’accès réseau, consultez [Compte d’accès réseau](../../../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

### <a name="software-update-point"></a>Point de mise à jour logicielle  

-   Pour plus d’informations sur les options de configuration du composant de point de mise à jour logicielle, consultez [Installer un point de mise à jour logicielle](../../../../sum/get-started/install-a-software-update-point.md).  

### <a name="management-point"></a>Point de gestion  

-   **Points de gestion :** vous pouvez configurer le site pour publier des informations sur ses points de gestion dans les services de domaine Active Directory.  

     Les clients Configuration Manager utilisent des points de gestion pour localiser les services et pour rechercher des informations sur le site, telles que les options de sélection de certificats PKI et d’appartenance à des groupes de limites. Les clients utilisent également des points de gestion pour rechercher d’autres points de gestion du site, ainsi que des points de distribution d’où ils peuvent télécharger des logiciels. Les points de gestion aident également les clients à terminer l’attribution de site et à télécharger la stratégie client et leurs informations client.  

     Comme la plus sûre des méthodes pour que les clients trouvent des points de gestion est de publier ceux-ci dans les services de domaines Active Directory, vous aurez généralement toujours besoin de sélectionner tous les points de gestion en fonctionnement pour publier dans les services de domaine Active Directory. Toutefois, pour pouvoir utiliser cette méthode de localisation de service, les éléments suivants doivent être vrais :

     - Le schéma est étendu pour Configuration Manager.
     - Il existe un conteneur **Gestion du système** disposant des autorisations de sécurité appropriées pour que le serveur de site puisse publier dans ce conteneur.
     - Le site Configuration Manager est configuré pour publier dans les services de domaine Active Directory.
     - Les clients appartiennent à la même forêt Active Directory que le serveur de site.  

     Quand les clients sur l’intranet ne peuvent pas utiliser les services de domaine Active Directory pour rechercher des points de gestion, utilisez la publication [DNS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_dns) à la place.  

 Pour obtenir des informations générales sur l’emplacement du service, consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   **Publier les points de gestion intranet sélectionnés dans DNS :** spécifiez cette option quand des clients sur l’intranet ne trouvent pas de points de gestion à partir des services de domaine Active Directory. Au lieu de cela, ils peuvent utiliser un enregistrement de ressource d’emplacement de service DNS (SRV RR) pour trouver un point de gestion dans leur site attribué.  

    Pour que Configuration Manager puisse publier des points de gestion intranet dans DNS, toutes les conditions suivantes doivent être remplies :  

    -   Vos serveurs DNS ont une version de BIND 8.1.2 ou ultérieure.  

    -   Vos serveurs DNS sont configurés pour les mises à jour automatiques et prennent en charge les enregistrements de ressource d’emplacement de service.  

    -   Les noms de domaine complets spécifiés pour les points de gestion dans Configuration Manager ont des entrées d’hôte (enregistrements A ou AAA) dans DNS.  

    > [!WARNING]  
    >  Pour que les clients trouvent des points de gestion publiés dans DNS, vous devez affecter les clients à un site spécifique (plutôt qu’utiliser l’attribution automatique de site). Configurez ces clients pour qu’ils utilisent le code de site avec le suffixe du domaine de leur point de gestion. Pour plus d’informations, consultez [Localisation de points de gestion](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points) dans [Guide pratique pour affecter des clients à un site dans System Center Configuration Manager](/sccm/core/clients/deploy/assign-clients-to-a-site).  

     Si les clients Configuration Manager ne peuvent pas utiliser les services de domaine Active Directory ou DNS pour rechercher des points de gestion sur l’intranet, ils peuvent utiliser [WINS](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#bkmk_wins). Le premier point de gestion installé pour le site est automatiquement publié dans WINS lorsqu’il est configuré pour accepter les connexions client HTTP sur l’intranet.  

### <a name="status-reporting"></a>édition de rapports d’état ;  

-   Ces paramètres configurent directement le niveau de détail qui est fourni dans les rapports d’état à partir de sites et de clients.  

### <a name="email-notification"></a>Notification par courrier électronique  

-   Spécifiez les détails de compte ou de serveur de messagerie pour que Configuration Manager envoie des notifications par e-mail en cas d’alertes.  

### <a name="collection-membership-evaluation"></a>Évaluation de l’appartenance au regroupement  

-   Cette tâche permet de définir la fréquence à laquelle l’appartenance à un regroupement est évaluée de façon incrémentielle. L'évaluation incrémentielle met à jour une appartenance à un regroupement uniquement avec de nouvelles ressources ou des ressources modifiées.  

### <a name="edit-the-site-components-at-a-site"></a>Modifier les composants de site sur un site  

Utilisez la procédure suivante pour modifier les composants de site :

1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Configuration du site** > **Sites**, puis sélectionnez le site comportant les composants de site que vous voulez configurer.  

2.  Sous l’onglet **Accueil**, dans le groupe **Paramètres**, cliquez sur **Configurer les composants de site**. Sélectionnez ensuite le composant de site que vous souhaitez configurer.  

##  <a name="BKMK_ServiceMgr"></a> Utiliser Configuration Manager Service Manager pour gérer les composants de site  
Vous pouvez utiliser Configuration Manager Service Manager pour contrôler les services Configuration Manager et afficher l’état de tout service ou thread de travail Configuration Manager (collectivement appelés composants Configuration Manager). Retenez les points suivants concernant les composant Configuration Manager :  

-   Les composants peuvent s’exécuter sur n’importe quel système de site.  

-   Ils sont gérés de la même façon que les services dans Windows. Vous pouvez les démarrer, les arrêter, les suspendre, les reprendre et les interroger.  

Un service Configuration Manager s’exécute dès qu’il a une tâche à effectuer (quand un fichier de configuration est enregistré dans la boîte de réception d’un composant, par exemple). Si vous devez identifier le composant impliqué dans une opération, vous pouvez utiliser Configuration Manager Service Manager pour agir sur plusieurs services et threads. Vous pouvez ensuite afficher les effets sur le comportement de Configuration Manager. Vous pouvez par exemple arrêter les services Configuration Manager un par un, jusqu’à ce qu’une réponse spécifique disparaisse. Vous pourrez ainsi déterminer le service qui provoque ce comportement.  

> [!TIP]  
>  La procédure suivante peut servir à manipuler des opérations de composants Configuration Manager.  

### <a name="use-the-configuration-manager-service-manager"></a>Utiliser le Gestionnaire de service de Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance** >  **État du système**, puis cliquez sur **État du composant**.  

2.  Sous l’onglet **Accueil**, dans le groupe **Composant**, cliquez sur **Démarrer**. Sélectionnez ensuite **Gestionnaire de service de Configuration Manager**.  

3.  Lorsque le Gestionnaire de service de Configuration Manager s'ouvre, connectez-vous au site que vous souhaitez gérer.  

     Si vous ne voyez pas le site que vous souhaitez gérer, cliquez sur **Site**, puis sur **Connecter**, et entrez le nom du serveur de site du site correct.  

4.  Développez le site et accédez à **Composants** ou à **Serveurs**selon l'emplacement où se trouvent les composants que vous souhaitez gérer.  

5.  Dans le volet de droite, sélectionnez un ou plusieurs composants. Puis, dans le menu **Composant**, cliquez sur **Requête** pour mettre à jour l’état de votre sélection.  

6.  Après la mise à jour de l’état du composant, utilisez l’une des quatre actions en option dans le menu **Composant** pour modifier le fonctionnement du composant. Après avoir demandé une action, vous devez demander au composant d'afficher son nouvel état.  

7.  Fermez Configuration Manager Service Manager quand vous avez fini de modifier l’état opérationnel des composants.  
