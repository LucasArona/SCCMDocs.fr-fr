---
title: Composants de site
titleSuffix: Configuration Manager
description: Apprenez à configurer des composants de site pour modifier le comportement des rôles système de site et la création des rapports d’état de site.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5fccbbeb-0faa-4943-83c2-e67db62d392d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: af4d3319e94d8dd673f597e4df4dde3e73e15653
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56129049"
---
# <a name="site-components-for-configuration-manager"></a>Composants de site pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour chaque site Configuration Manager, vous pouvez configurer des composants de site afin de modifier le comportement des rôles système de site et la création des rapports d’état de site. Les configurations de composants de site s’appliquent à un site donné et à chaque instance d’un rôle de système de site applicable au niveau de ce site.  

Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez un site. Dans le groupe **Paramètres** du ruban, choisissez **Configurer les composants de site**. Sélectionnez l'une des options suivantes :

- [Distribution de logiciels](#software-distribution)  
- [Point de mise à jour logicielle](#software-update-point)  
- [Point de gestion](#management-point)  
- [Création de rapports d’état](#status-reporting)  
- [Notification par e-mail](#email-notification)
- [Évaluation de l’adhésion au regroupement](#bkmk_colleval)


## <a name="about-site-components"></a>À propos des composants de site  

 La plupart des options des différents composants de site sont suffisamment explicites quand elles apparaissent dans la console Configuration Manager. Toutefois, les informations suivantes peuvent être utiles pour mieux comprendre certaines configurations plus complexes ou vous diriger vers du contenu supplémentaire.  

> [!Note]  
> Les options disponibles pour certains composants varient selon que vous sélectionnez le site d’administration centrale, un site principal ou un site secondaire. Certains composants ne sont pas disponibles du tout pour certains types de sites.  



### <a name="software-distribution"></a>Distribution de logiciels  

#### <a name="content-distribution-settings"></a>Paramètres de distribution de contenu
Sous l’onglet **Général**, spécifiez des paramètres qui modifient la façon dont le serveur de site transfère du contenu vers ses points de distribution. Si vous augmentez les valeurs des paramètres de distribution simultanée, la distribution de contenu risque d’utiliser davantage de bande passante réseau.  

#### <a name="pull-distribution-point"></a>Point de distribution d’extraction
Pour plus d’informations, consultez [Utiliser un point de distribution d’extraction](/sccm/core/plan-design/hierarchy/use-a-pull-distribution-point).

#### <a name="network-access-account"></a>Compte d'accès réseau
Pour plus d’informations, consultez [Compte d’accès réseau](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="software-update-point"></a>Point de mise à jour logicielle  

Pour plus d’informations, consultez [Installer un point de mise à jour logicielle](/sccm/sum/get-started/install-a-software-update-point).  


### <a name="management-point"></a>Point de gestion  

Sous l’onglet **Général**, configurez le site pour publier des informations relatives à ses points de gestion sur Active Directory Domain Services.  

Les clients Configuration Manager utilisent des points de gestion pour localiser les services et pour rechercher des informations sur le site, telles que les options de sélection de certificats PKI et d’appartenance à des groupes de limites. Les clients utilisent également des points de gestion pour rechercher d’autres points de gestion du site, ainsi que des points de distribution d’où ils peuvent télécharger des logiciels. Les points de gestion aident également les clients à terminer l’attribution de site et à télécharger la stratégie client et leurs informations client.  

La méthode la plus sécurisée pour que les clients trouvent les points de gestion consiste à les publier dans Active Directory Domain Services. Cette méthode de localisation de service nécessite que les conditions suivantes soient remplies :

- Le schéma est étendu pour Configuration Manager.
- Il existe un conteneur **Gestion du système** disposant des autorisations de sécurité appropriées pour que le serveur de site puisse publier sur ce conteneur.
- Le site Configuration Manager est configuré pour publier dans les services de domaine Active Directory.
- Les clients appartiennent à la même forêt Active Directory que le serveur de site.  

Quand des clients sur l’intranet ne peuvent pas utiliser Active Directory Domain Services pour rechercher des points de gestion, utilisez la [publication DNS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_dns).  

Pour obtenir des informations générales sur l’emplacement du service, consultez [Comprendre comment les clients recherchent des services et des ressources de site](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services).  


#### <a name="publish-selected-intranet-management-points-in-dns"></a>Publier des points de gestion intranet sélectionnés dans DNS
Spécifiez cette option quand des clients sur l’intranet ne peuvent pas trouver de points de gestion à partir d’Active Directory Domain Services. Au lieu de cela, ils peuvent utiliser un enregistrement de ressource d’emplacement de service DNS (SRV RR) pour trouver un point de gestion dans leur site attribué.  

Pour que Configuration Manager puisse publier des points de gestion intranet dans DNS, toutes les conditions suivantes doivent être remplies :  

-   Vos serveurs DNS ont une version de BIND 8.1.2 ou ultérieure.  

-   Vos serveurs DNS sont configurés pour les mises à jour automatiques et prennent en charge les enregistrements de ressource d’emplacement de service.  

-   Les noms de domaine complets spécifiés pour les points de gestion dans Configuration Manager ont des entrées d’hôte (enregistrements A ou AAA) dans DNS.  

> [!WARNING]  
>  Pour que les clients trouvent des points de gestion publiés dans DNS, vous devez affecter les clients à un site spécifique (plutôt qu’utiliser l’attribution automatique de site). Configurez ces clients pour qu’ils utilisent le code de site avec le suffixe du domaine de leur point de gestion. Pour plus d’informations, consultez [Localisation de points de gestion](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).  

Si les clients Configuration Manager ne peuvent pas utiliser Active Directory Domain Services ou DNS pour rechercher des points de gestion sur l’intranet, ils utilisent [WINS](/sccm/core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services#bkmk_wins). Le premier point de gestion installé pour le site est automatiquement publié sur WINS quand il est configuré pour accepter les connexions client HTTP sur l’intranet.  


### <a name="status-reporting"></a>édition de rapports d’état ;  

Ces paramètres configurent directement le niveau de détail fourni dans les rapports d’état à partir de sites et de clients.  


### <a name="email-notification"></a>Notification par courrier électronique  

Spécifiez les détails de compte ou de serveur de messagerie pour que Configuration Manager envoie des notifications par e-mail en cas d’alertes.  

Pour plus d’informations, consultez [Utiliser des alertes et le système d’état](/sccm/core/servers/manage/use-alerts-and-the-status-system).


### <a name="bkmk_colleval"></a> Évaluation de l’adhésion au regroupement  

Utilisez ce composant pour définir la fréquence à laquelle l’adhésion au regroupement est évaluée de façon incrémentielle. L'évaluation incrémentielle met à jour une appartenance à un regroupement uniquement avec de nouvelles ressources ou des ressources modifiées.  

Pour plus d’informations, consultez [Bonnes pratiques pour les regroupements](/sccm/core/clients/manage/collections/best-practices-for-collections).



##  <a name="BKMK_ServiceMgr"></a> Utiliser Configuration Manager Service Manager pour gérer les composants de site  

Vous pouvez utiliser Configuration Manager Service Manager pour contrôler les services Configuration Manager et afficher l’état de tout service ou thread de travail Configuration Manager. Ces services et threads sont collectivement appelés « composants Configuration Manager ». Retenez les instructions suivantes concernant les composant Configuration Manager :  

-   Les composants peuvent s’exécuter sur n’importe quel système de site.  

-   Ils sont gérés de la même façon que les services dans Windows. Vous pouvez les démarrer, les arrêter, les suspendre, les reprendre et les interroger.  

Un service Configuration Manager s’exécute quand il a quelque chose à faire. C’est généralement le cas quand un fichier de configuration est enregistré dans la boîte de réception d’un composant. 


### <a name="use-the-configuration-manager-service-manager"></a>Utiliser le Gestionnaire de service de Configuration Manager  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, développez **État du système**, puis sélectionnez le nœud **État du composant**.  

2.  Dans le groupe **Composant** du ruban, sélectionnez **Démarrer**, puis choisissez **Gestionnaire de service de Configuration Manager**.  

3.  Lorsque le Gestionnaire de service de Configuration Manager s'ouvre, connectez-vous au site que vous souhaitez gérer.  

     Si vous ne voyez pas le site que vous souhaitez gérer, accédez au menu **Site**, puis sélectionnez **Connecter**. Entrez le nom du serveur de site du site approprié.  

4.  Développez le site et accédez à **Composants** ou à **Serveurs**selon l'emplacement où se trouvent les composants que vous souhaitez gérer.  

5.  Dans le volet de droite, sélectionnez un ou plusieurs composants. Puis, dans le menu **Composant**, sélectionnez **Requête** pour mettre à jour l’état de votre sélection.  

6.  Après la mise à jour de l’état du composant, utilisez l’une des quatre actions en option dans le menu **Composant** pour modifier le fonctionnement du composant. Après avoir demandé une action, vous devez demander au composant d'afficher son nouvel état.  

7.  Fermez Configuration Manager Service Manager quand vous avez fini de modifier l’état opérationnel des composants.  
