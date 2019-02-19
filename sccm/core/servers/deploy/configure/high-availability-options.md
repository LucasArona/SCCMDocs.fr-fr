---
title: Haute disponibilité
titleSuffix: Configuration Manager
description: Découvrez comment déployer Configuration Manager avec des options qui garantissent une haute disponibilité des services.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9b69fac83283963e49b01c733fb8fa3000702cfb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132164"
---
# <a name="high-availability-options-for-configuration-manager"></a>Options de haute disponibilité pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article explique comment déployer Configuration Manager avec des options qui garantissent une haute disponibilité des services.   

Les options suivantes de Configuration Manager permettent une haute disponibilité :   

- Depuis la version 1806, il est possible de configurer n’importe quel site principal avec un serveur de site supplémentaire en mode passif.  
 
- Configurez un groupe de disponibilité SQL Server Always On pour la base de données de site sur les sites principaux et sur le site d’administration centrale.

- Les sites prennent en charge plusieurs instances de rôles de système de site qui fournissent des services importants aux clients. Par exemple, des points de gestion et des points de distribution.  

- Les sites d'administration centrale et les sites principaux prennent en charge la sauvegarde de la base de données de site. La base de données de site stocke toutes les configurations des sites et des clients. Les sites d’une même hiérarchie partagent ces données de configuration.  

- Les options de récupération de site intégrées peuvent réduire les temps d’arrêt du serveur. Ces options avancées simplifient la récupération lorsque vous disposez d’une hiérarchie comprenant un site d’administration centrale.  

- Les clients peuvent corriger automatiquement les problèmes typiques sans intervention de l'administrateur.  

- Les sites génèrent des alertes concernant les clients qui ne soumettent pas de données récentes, ce qui a pour effet d'informer les administrateurs d'éventuels problèmes.  

- Configuration Manager fournit plusieurs rapports et tableaux de bord intégrés. Vous pouvez les utiliser pour identifier les problèmes liés aux opérations des serveurs et des clients, ainsi que pour identifier les tendances avant qu’elles ne deviennent des problèmes.  


Configuration Manager comprend plusieurs fonctionnalités qui fournissent un service en quasi temps réel. Si ces fonctionnalités sont essentielles pour répondre aux besoins de votre entreprise, planifiez et configurez vos sites et vos hiérarchies pour la haute disponibilité. Par exemple :  

- [Actions de notification du client](/sccm/core/clients/manage/manage-clients), telles qu’un redémarrage, le lancement des analyses Windows Defender ou le Bureau à distance.  

- Des messages basés sur l’état pour les fonctionnalités de surveillance, telles que les mises à jour logicielles et la protection des points de terminaison. 

- [Scripts](/sccm/apps/deploy-use/create-deploy-scripts), à compter de la version 1706  

- [CMPivot](/sccm/core/servers/manage/cmpivot), à compter de la version 1806  


Les autres fonctionnalités de Configuration Manager ne fournissent pas de services en temps réel. Ces fonctionnalités incluent notamment les paramètres du client, l’inventaire matériel et logiciel, les déploiements de logiciels et les paramètres de conformité. Leur fonctionnement implique une certaine latence des données. Dans la plupart des scénarios, il est rare qu’une interruption temporaire du service se transforme en problème critique. Pour réduire le temps d’arrêt, maintenir l’autonomie des opérations et fournir un niveau élevé de service, configurez vos sites et vos hiérarchies en gardant à l’esprit la haute disponibilité.  

Par exemple, les clients Configuration Manager fonctionnent généralement de manière autonome en se basant sur les planifications et configurations connues pour les opérations, ainsi que sur les planifications d’envoi des données à traiter au site.  

- Lorsque les clients ne parviennent pas à contacter le site, ils mettent en cache les données à envoyer jusqu’à ce qu’ils puissent contacter le site.  

- Les clients qui ne peuvent pas contacter le site continuent de fonctionner. Ils utilisent les dernières planifications connues et les informations mises en cache, jusqu’à ce qu’ils parviennent à contacter le site et à recevoir les nouvelles stratégies. Par exemple, un client peut conserver une application précédemment téléchargée qu’il doit exécuter ou installer.   

- Le site surveille ses systèmes de site et ses clients pour voir les mises à jour d’état périodiques. Il peut générer des alertes lorsque ces composants ne parviennent pas à s’inscrire.  

- Les rapports intégrés fournissent des insights sur les opérations en cours, ainsi que sur les opérations d’historique et les tendances actuelles. Configuration Manager prend en charge des messages basés sur l’état qui fournissent des informations presque en temps réel sur les opérations en cours.  



##  <a name="bkmk_snh"></a> Haute disponibilité pour les sites et les hiérarchies  

#### <a name="use-a-site-server-in-passive-mode"></a>Utiliser un serveur de site en mode passif
Depuis la version 1806, il est possible d’installer un serveur de site supplémentaire en mode *passif* pour un site principal autonome. Le serveur de site en mode passif s’ajoute à votre serveur de site existant, qui est en mode *actif*. Un serveur de site en mode passif est disponible pour une utilisation immédiate, en cas de besoin. Pour plus d’informations, consultez [Haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability).  

#### <a name="use-a-remote-content-library"></a>Utiliser une bibliothèque de contenu distante
Depuis la version 1806, il est possible de déplacer la bibliothèque de contenu du site vers un emplacement distant qui fournit un stockage hautement disponible. Cette fonctionnalité est nécessaire à la haute disponibilité du serveur de site. Pour plus d’informations, consultez [Bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library#bkmk_remote).

#### <a name="centralize-content-sources"></a>Centraliser les sources de contenu
Dans Configuration Manager, tout le contenu des logiciels nécessite un emplacement source de package sur le réseau. Utilisez un stockage centralisé et hautement disponible pour héberger un emplacement source de package commun à tout le contenu. 

#### <a name="use-a-sql-server-always-on-availability-group-to-host-the-site-database"></a>Utiliser un groupe de disponibilité SQL Server AlwaysOn pour héberger la base de données de site  
Hébergez la base de données de site sur les sites principaux, et le site d’administration centrale dans les groupes de disponibilité AlwaysOn SQL Server. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site hautement disponible](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

#### <a name="use-a-sql-server-cluster-to-host-the-site-database"></a>Utiliser un cluster SQL Server pour héberger la base de données de site  
Lorsque vous utilisez un cluster SQL Server pour la base de données sur un site d'administration centrale ou sur un site principal, vous utilisez la prise en charge de basculement intégrée à SQL Server.  

Les sites secondaires ne peuvent pas utiliser un cluster SQL Server et ne prennent pas en charge la sauvegarde et la restauration de leur base de données de site. La récupération d’un site secondaire s’effectue en le réinstallant à partir de son site principal parent.  

#### <a name="deploy-a-hierarchy-of-sites-with-a-central-administration-site-and-one-or-more-child-primary-sites"></a>Déployer une hiérarchie de sites avec un site d'administration centrale et un ou plusieurs sites enfants principaux  
Cette configuration peut fournir une tolérance aux pannes lorsque vos sites gèrent des segments se chevauchant de votre réseau. Cette configuration propose également une option de récupération supplémentaire pour utiliser les informations de la base de données partagée qui est disponible sur un autre site, afin de reconstruire la base de données de site sur le site récupéré. Utilisez cette option lorsque la sauvegarde de la base de données du site ayant connu une panne a échoué ou est indisponible.  

#### <a name="create-regular-backups-at-central-administration-sites-and-primary-sites"></a>Créer des sauvegardes régulières sur des sites d'administration centrale et des sites principaux  
Lorsque vous créez et testez une sauvegarde de site habituelle, vous avez la garantie que vous disposez des données nécessaires pour récupérer un site. Cela vous permet également de vous entraîner à récupérer un site rapidement.  

#### <a name="install-multiple-instances-of-site-system-roles"></a>Installer plusieurs instances de rôles de système de site  
Lorsque vous installez plusieurs instances de rôles de système de site critiques, vous fournissez des points de contact redondants pour les clients. Par exemple, plusieurs points de gestion et points de distribution fournissent des services redondants au cas où un serveur serait hors ligne.  

#### <a name="install-multiple-instances-of-the-sms-provider-at-a-site"></a>Installer plusieurs instances du fournisseur SMS sur un site  
Le fournisseur SMS fournit le point de contact administratif pour une ou plusieurs consoles Configuration Manager. Pour fournir une redondance aux points de contact en vue d’administrer votre site et votre hiérarchie, installez plusieurs fournisseurs SMS.  



##  <a name="bkmk_ssr"></a> Haute disponibilité pour les rôles système de site  
Sur chaque site, vous déployez des rôles de système de site pour fournir les services que vous souhaitez voir les clients utiliser sur ce site. La base de données du site contient les informations de configuration du site et de tous les clients. Utilisez une ou plusieurs des options disponibles pour fournir une haute disponibilité de la base de données de site et la récupération du site et de la base de données de site, le cas échéant.  

#### <a name="redundancy-for-important-site-system-roles"></a>Redondance pour les rôles de système de site importants  
-   Point de service web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de distribution  

-   Point de gestion  

-   Point de mise à jour logicielle  

-   Point de migration d’état  

Si vous souhaitez fournir la redondance pour la création de rapports sur les sites et les clients, installez plusieurs instances du point de Reporting Services.

Pour que le basculement soit pris en charge avec le point de mise à jour logicielle, utilisez Windows PowerShell pour installer ce rôle sur un cluster d’équilibrage de la charge réseau (NLB) Windows.  

#### <a name="built-in-site-backup"></a>Sauvegarde de site intégrée  
Configuration Manager inclut une tâche de sauvegarde intégrée pour vous aider à sauvegarder votre site et vos informations critiques à intervalles réguliers. En outre, l’Assistant Installation de Configuration Manager prend en charge des actions de restauration de site pour vous aider à restaurer l’état de fonctionnement d’un site.  

#### <a name="publishing-to-active-directory-domain-services-and-dns"></a>Publication vers les services de domaine Active Directory et DNS  
Configurez chaque site de manière à publier les données le concernant dans Active Directory Domain Services et DNS. Cette publication permet aux clients d’identifier le serveur le plus accessible du réseau. Les clients l’utilisent également afin de déterminer à quel moment les nouveaux serveurs de système de site sont disponibles pour fournir des services importants, tels que les points de gestion.  

#### <a name="sms-provider-and-configuration-manager-console"></a>Fournisseur SMS et console Configuration Manager  
Configuration Manager permet d’installer plusieurs fournisseurs SMS sur des serveurs différents, comme plusieurs points d’accès à la console. Quand un serveur de fournisseur SMS est hors connexion, vous pouvez toujours afficher et gérer les sites et les clients.  

Quand une console Configuration Manager se connecte à un site, elle se connecte à une instance du fournisseur SMS sur ce site. L’instance du fournisseur SMS est sélectionnée de façon aléatoire. Si le fournisseur SMS sélectionné n’est pas disponible, vous disposez des options suivantes :  

-   Reconnectez la console au site. Une instance du fournisseur SMS est attribuée de façon aléatoire à chaque nouvelle demande de connexion. Il est possible qu’une instance disponible soit attribuée à la nouvelle connexion.  

-   Connectez la console à un autre site Configuration Manager, puis gérez la configuration à partir de cette connexion. Avec cette option, l’apport de modifications à la configuration prend quelques minutes. Lorsque le fournisseur SMS pour le site est en ligne, reconnectez votre console Configuration Manager directement au site à gérer.  

Installez la console Configuration Manager sur plusieurs ordinateurs afin que les utilisateurs administratifs puissent l’utiliser. Chaque fournisseur SMS prend en charge des connexions provenant de plusieurs consoles.  

#### <a name="management-point"></a>Point de gestion  
Installez plusieurs points de gestion sur chaque site principal et activez les sites pour publier des données de site vers votre infrastructure Active Directory et vers DNS.  

Des points de gestion multiples permettent d'équilibrer la charge d'utilisation d'un point de gestion unique par plusieurs clients. Vous pouvez également installer un ou plusieurs réplicas de base de données pour les points de gestion. Cette configuration réduit le nombre d’opérations sollicitant beaucoup le processeur dans le point de gestion. Cela augmente également la disponibilité de ce rôle de système de site critique.  

Les sites secondaires ne peuvent prendre en charge l’installation que d’un seul point de gestion, qui doit se trouver sur le serveur de site secondaire. Les points de gestion des sites secondaires ne sont pas considérés comme ayant une configuration hautement disponible.  

> [!NOTE]  
>  Les appareils gérés par une gestion des appareils mobiles locale se connectent à un seul point de gestion sur un site principal. Configuration Manager attribue le point de gestion à l’appareil mobile au moment de l’inscription, et ne le change pas par la suite. Lorsque vous installez plusieurs points de gestion et que vous en activez plusieurs pour les appareils mobiles, le point de gestion qui est attribué à un client d’appareil mobile n’est pas déterministe.  
>   
>  Si le point de gestion utilisé par un client d’appareil mobile n’est plus disponible, vous devez résoudre le problème au niveau de ce point de gestion, ou réinitialiser l’appareil mobile et le réinscrire pour qu’il puisse être attribué à un autre point de gestion disponible pour les appareils mobiles.  

#### <a name="distribution-point"></a>Point de distribution  
Installez plusieurs points de distribution et déployez du contenu sur plusieurs points de distribution. Ajoutez plusieurs points de distribution par groupe de limites pour que les clients aient plusieurs options dans leur demande de contenu. Configurez des relations entre les groupes de limites pour que ces derniers aient un comportement de secours prévisible en basculant vers un autre groupe de limites ou point de distribution cloud. Pour plus d’informations, consultez [Configurer des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).  

#### <a name="application-catalog-web-service-point-and-application-catalog-website-point"></a>Point de service web du catalogue des applications et point du site web du catalogue des applications  
Installez plusieurs instances de chaque rôle de système de site. Pour de meilleures performances, déployez une instance de chaque sur le même serveur de système de site.  

Chaque rôle de système de site du catalogue d’applications fournit les mêmes informations que les autres instances de ce rôle, quel que soit son emplacement dans la hiérarchie. Quand un client envoie une demande pour le catalogue d’applications lorsque les clients sont configurés pour détecter automatiquement le point de site web du catalogue d’applications, le client est redirigé vers une instance disponible. Par défaut, les clients choisissent les instances locales du catalogue d’applications, en fonction de leur propre emplacement réseau.  

Pour plus d’informations sur ce paramètre client et sur le fonctionnement de la détection automatique, consultez la section [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent) de l’article [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings).  



##  <a name="bkmk_client"></a> Haute disponibilité pour les clients  

#### <a name="client-operations-are-autonomous"></a>Les opérations du client sont autonomes.  
L’autonomie du client Configuration Manager suit les comportements suivants :  

-   Les clients ne nécessitent pas un contact permanent avec un serveur de système de site spécifique. Ils utilisent de configurations connues pour effectuer des actions préconfigurées selon une planification.  

-   Les clients peuvent utiliser n’importe quelle instance disponible d’un rôle de système de site fournissant des services aux clients. Ils tentent de contacter des serveurs connus jusqu’à ce qu’ils en localisent un de disponible.  

-   Les clients peuvent exécuter un inventaire, des déploiements de logiciels et autres actions planifiées similaires indépendamment d'un contact direct avec les serveurs de système de site.  

-   Les clients qui sont configurés pour utiliser un point d’état de secours peuvent envoyer des détails au point d’état de secours lorsque la communication avec un point de gestion n’est pas possible.  

#### <a name="clients-can-repair-themselves"></a>Les clients peuvent se réparer eux-mêmes.  
Les clients corrigent automatiquement les problèmes les plus courants, sans intervention directe de l’administrateur.  

-   Régulièrement, les clients évaluent leur propre état. Ils prennent les mesures nécessaires pour corriger les problèmes courants, à l’aide d’un cache local d’étapes de mise à jour et de fichiers sources pour la réparation.  

-   Lorsqu'un client ne soumet des informations d'état sur son site, le site génère une alerte. Les utilisateurs administratifs qui reçoivent ces alertes peuvent prendre des mesures immédiates pour restaurer le fonctionnement normal du client.  

#### <a name="clients-cache-information-to-use-in-the-future"></a>Les clients mettent en cache des informations pour les utiliser par la suite.  
Lorsqu'un client communique avec un point de gestion, le client peut obtenir et mettre en cache les informations suivantes :  

-   Paramètres du client  

-   Planifications du client  

-   Des informations sur les déploiements de logiciels et un téléchargement du logiciel que le client doit installer, lorsque le déploiement est configuré pour cette action.  

Quand un client ne peut pas contacter un point de gestion, il met en cache localement les informations relatives à l’état et au client qu’il souhaite envoyer au site. Il transfère ensuite ces données lorsque le contact est établi avec un point de gestion.  

#### <a name="client-can-submit-status-to-a-fallback-status-point"></a>Le client peut soumettre l'état à un point d'état de secours.  
Quand vous configurez un client pour qu’il utilise un point d’état de secours, vous fournissez au client un point de contact supplémentaire vers lequel il peut envoyer des informations détaillées importantes sur son fonctionnement. Les clients qui sont configurés de manière à utiliser un point d’état de secours continuent à envoyer des informations sur l’état de leurs opérations vers ce rôle de système de site, lorsque la communication avec un point de gestion n’est pas possible.  

#### <a name="central-management-of-client-data-and-client-identity"></a>Gestion centralisée des données du client et de l'identité du client  
La base de données de site, plutôt que le client, conserve les informations importantes sur l’identité de chaque client et associe ces données à un utilisateur ou un ordinateur spécifique.  

-   Les fichiers source du client sur un ordinateur peuvent être désinstallés et réinstallés sans modifier les enregistrements historiques de l’ordinateur sur lequel est installé le client.  

-   La défaillance d’un ordinateur client n’affecte pas l’intégrité des informations qui sont stockées dans la base de données. Ces informations peuvent rester disponibles pour les rapports.  



##  <a name="bkmk_nonHAoptions"></a> Options pour les sites et les rôles de système de site qui n’ont pas un haut niveau de disponibilité  
Plusieurs systèmes de site ne permettent pas d’avoir plusieurs instances sur un même site ou dans une hiérarchie. Aidez-vous des informations ci-dessous pour préparer la mise hors connexion de ces systèmes de site.  

#### <a name="site-server-site"></a>Serveur de site (site)  

> [!Note]  
> Cette section s’applique uniquement aux versions 1802 et antérieures de Configuration Manager. Depuis la version 1806, Configuration Manager fournit une option de haute disponibilité pour le serveur de site. Pour plus d’informations, consultez [Haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability).  

Configuration Manager ne prend pas en charge l’installation du serveur de site pour chaque site d’un cluster Windows Server ou d’équilibrage de la charge réseau (NLB).  

Les informations suivantes peuvent vous aider à vous préparer au cas où un serveur de site tomberait en panne ou ne serait pas opérationnel :  

-   La tâche de sauvegarde intégrée permet de faire une sauvegarde régulière du site. Dans un environnement de test, pratiquez régulièrement la restauration de sites à partir d'une sauvegarde.  

-   Déployez plusieurs sites principaux Configuration Manager dans une hiérarchie avec un site d’administration centrale pour créer un système redondant. En cas de panne du site, envisagez d'utiliser la stratégie de groupe Windows ou des scripts d'ouverture de session pour réattribuer des clients à un site fonctionnel.  

-   Si votre hiérarchie dispose d'un site d'administration centrale, vous pouvez restaurer celui-ci ou un site principal enfant en utilisant l'option de restauration d'une base de donnée de site à partir d'un autre site de la hiérarchie.  

-   Les sites secondaires ne peuvent pas être restaurés et doivent être réinstallés.  

#### <a name="asset-intelligence-synchronization-point-hierarchy"></a>Point de synchronisation Asset Intelligence (hiérarchie)  
Ce rôle de système de site n’est pas stratégique et fournit des fonctionnalités facultatives dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

#### <a name="endpoint-protection-point-hierarchy"></a>Point Endpoint Protection (hiérarchie)  
Ce rôle de système de site n’est pas stratégique et fournit des fonctionnalités facultatives dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

#### <a name="enrollment-point-site"></a>Point d'inscription (site)  
Ce rôle de système de site n’est pas stratégique et fournit des fonctionnalités facultatives dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

#### <a name="enrollment-proxy-point-site"></a>Point proxy d'inscription (site)  
Ce rôle de système de site n’est pas stratégique et fournit des fonctionnalités facultatives dans Configuration Manager. Vous pouvez toutefois installer plusieurs instances de ce rôle de système de site sur un site et sur plusieurs sites dans la hiérarchie. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

Lorsque vous disposez de plusieurs serveurs proxy d'inscription sur un site, utilisez un alias DNS pour le nom du serveur. Lorsque vous utilisez cette configuration, le tourniquet DNS tolère des erreurs et l'équilibrage de charge dans une certaine mesure lorsque les utilisateurs inscrivent leurs périphériques mobiles.  

#### <a name="fallback-status-point-site-or-hierarchy"></a>Point d'état de secours (site ou hiérarchie)  
Ce rôle de système de site n’est pas stratégique et fournit des fonctionnalités facultatives dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur. Étant donné que les clients sont affectés au point d’état de secours lors de leur installation, vous devez modifier les clients existants pour qu’ils utilisent le nouveau serveur de système de site.  


#### <a name="service-connection-point-hierarchy"></a>Point de connexion de service (hiérarchie)
Ce rôle de système de site est essentiel pour maintenir à jour le Current Branch Configuration Manager. Toutefois, il n’est pas utilisé très fréquemment. Si ce système devient hors ligne, utilisez l’une des options suivantes :

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  



## <a name="see-also"></a>Voir aussi  
- [Configurations prises en charge](/sccm/core/plan-design/configs/supported-configurations)  

- [Matériel recommandé](/sccm/core/plan-design/configs/recommended-hardware)  

- [Systèmes d’exploitation pris en charge pour les serveurs de système de site](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers)   

- [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites)  

- [Impacts des défaillances du site](/sccm/core/servers/manage/site-failure-impacts)  

