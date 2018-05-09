---
title: Haute disponibilité
titleSuffix: Configuration Manager
description: Découvrez comment déployer System Center Configuration Manager avec des options qui garantissent une haute disponibilité des services.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 1a38421d-24c1-4fef-bf6c-42fce53109ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1011aa1b30661d756d457a38ebc770a61fac07f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="high-availability-options-for-system-center-configuration-manager"></a>Options de haute disponibilité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*



Vous pouvez déployer System Center Configuration Manager avec des options qui garantissent une haute disponibilité des services.   

Les options de haute disponibilité sont les suivantes :   

-   Les sites prennent en charge plusieurs instances de serveurs de système de site qui fournissent des services importants aux clients.  

-   Les sites d'administration centrale et les sites principaux prennent en charge la sauvegarde de la base de données de site. La base de données de site contient toutes les configurations des sites et des clients : de plus, elle est partagée entre les sites d'une hiérarchie contenant un site d'administration centrale.  

-   Les options de récupération de site intégrées permettent de réduire les temps d'arrêt du serveur. En outre, des options avancées permettent de simplifier la récupération lorsque votre hiérarchie comprend un site d'administration centrale.  

-   Les clients peuvent corriger automatiquement les problèmes typiques sans intervention de l'administrateur.  

-   Les sites génèrent des alertes concernant les clients qui ne soumettent pas de données récentes, ce qui a pour effet d'informer les administrateurs d'éventuels problèmes.  

-   Configuration Manager fournit plusieurs rapports intégrés qui vous permettent d’identifier en amont les problèmes et les tendances, et ainsi de garantir le bon fonctionnement du serveur et du client.  

 Configuration Manager ne fournit pas un service en temps réel, ce qui peut entraîner une latence des données dans son fonctionnement. Par conséquent, il est rare pour la plupart des scénarios qui impliquent une interruption du service temporaire de se transformer en problème critique. Lorsque vous configurez vos sites et hiérarchies en tenant compte de la haute disponibilité, vous pouvez minimiser les temps d'arrêt, maintenir l'autonomie des opérations et fournir un niveau de service élevé.  

 Par exemple, les clients Configuration Manager fonctionnent généralement de manière autonome en se basant sur les planifications et configurations connues pour les opérations, ainsi que sur les planifications d’envoi des données à traiter au site.  

-   Lorsque les clients ne parviennent pas à contacter le site, ils mettent en cache données à envoyer jusqu'à ce qu'ils puissent contacter le site.  

-   Les clients qui ne parviennent pas à contacter le site continuent à fonctionner en utilisant les dernières planifications connues, ainsi que les informations mises en cache, concernant par exemple une application précédemment téléchargée qu’ils doivent exécuter ou installer, jusqu’au moment où ils parviennent à contacter le site et à recevoir de nouvelles stratégies.  

-   Le site surveille ses systèmes de site et clients à la recherche de mises à jour d'état périodiques, et peut générer des alertes si ces dernières ne sont pas enregistrées.  

-   Les rapports intégrés fournissent une vision des opérations en cours ainsi que des opérations historiques et des tendances. Configuration Manager prend en charge des messages basés sur l’état qui fournissent des informations presque en temps réel sur les opérations en cours.  

  Utilisez les informations de cette rubrique ainsi que celles contenues dans les articles suivants :
-   [Matériel recommandé](../../core/plan-design/configs/recommended-hardware.md)
-   [Systèmes d’exploitation pris en charge pour les serveurs de système de site](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md)  

-   [Prérequis des sites et systèmes de site](../../core/plan-design/configs/site-and-site-system-prerequisites.md)


##  <a name="bkmk_snh"></a> Haute disponibilité pour les sites et les hiérarchies  
 **Utiliser un cluster SQL Server pour héberger la base de données de site :**  

 Lorsque vous utilisez un cluster SQL Server pour la base de données sur un site d'administration centrale ou sur un site principal, vous utilisez la prise en charge de basculement intégrée à SQL Server.  

 Les sites secondaires ne peuvent pas utiliser un cluster SQL Server et ne prennent pas en charge la sauvegarde ou la restauration de leur base de données de site. La récupération d’un site secondaire s’effectue en le réinstallant à partir de son site principal parent.  

 **Utiliser un groupe de disponibilité SQL Server AlwaysOn pour héberger la base de données de site :**  

 Depuis la version 1602, vous pouvez utiliser des groupes de disponibilité SQL Server AlwaysOn pour héberger la base de données du site sur des sites principaux et le site d’administration centrale, en tant que solution de haute disponibilité et de récupération d’urgence. Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

 **Déployer une hiérarchie de sites avec un site d’administration centrale et un ou plusieurs sites principaux enfants :**  

 Cette configuration peut fournir une tolérance aux pannes lorsque vos sites gèrent des segments se chevauchant de votre réseau. De plus, cette configuration propose une option de récupération supplémentaire pour utiliser les informations dans la base de données partagée disponible sur un autre site afin de reconstruire la base de données de site sur le site récupéré. Vous pouvez utiliser cette option pour remplacer une sauvegarde non réussie ou non disponible de la base de données du site ayant échoué.  

 **Créer des sauvegardes régulières sur des sites d’administration centrale et des sites principaux :**  

 Lorsque vous créez et testez une sauvegarde de site régulière, vous pouvez vous assurer que vous disposez des données nécessaires à la récupération d'un site et de l'expérience pour récupérer un site le plus rapidement possible.  

 **Installer plusieurs instances de rôles de système de site :**  

 Lorsque vous installez plusieurs instances de rôles de système de site critiques, par exemple, le point de gestion et le point de distribution, vous fournissez des points de contact redondants pour les clients dans le cas où un serveur de système de site est hors-ligne.  

 **Installer plusieurs instances du fournisseur SMS sur un site :** le fournisseur SMS fournit le point de contact administratif pour une ou plusieurs consoles Configuration Manager. Lorsque vous installez plusieurs fournisseurs SMS, vous pouvez fournir une redondance pour l'administration de votre site et hiérarchie par des points de contact.  

##  <a name="bkmk_ssr"></a> Haute disponibilité pour les rôles système de site  
 Sur chaque site, vous déployez des rôles de système de site pour fournir les services que vous souhaitez voir les clients utiliser sur ce site. La base de données du site contient les informations de configuration du site et de tous les clients. Utilisez une ou plusieurs des options disponibles pour fournir une haute disponibilité de la base de données de site et la récupération du site et de la base de données de site, le cas échéant.  

 **Redondance pour les rôles de système de site importants :**  

-   Point de service Web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de distribution  

-   Point de gestion  

-   Point de mise à jour logicielle  

-   Point de migration d’état  

 Vous pouvez installer plusieurs instances du rôle de point de Reporting Services pour fournir la redondance des rapports sur les sites et les clients.

 Vous pouvez utiliser PowerShell pour installer le rôle de système de site de point de mise à jour logicielle sur un cluster NLB Windows pour fournir la prise en charge du basculement.  


 **Sauvegarde de site intégrée :**  

 Configuration Manager inclut une tâche de sauvegarde intégrée pour vous aider à sauvegarder votre site et vos informations critiques à intervalles réguliers. En outre, l’Assistant Installation de Configuration Manager prend en charge des actions de restauration de site pour vous aider à restaurer l’état de fonctionnement d’un site.  

 **Publication vers les services de domaine Active Directory et DNS :**  

 Vous pouvez configurer chaque site afin de publier des données concernant les serveurs de système de site et les services vers les services de domaine Active Directory et DNS. Cela permet aux clients d'identifier le serveur le plus accessible sur le réseau, ainsi que la disponibilité de nouveaux serveurs de système de site qui fournissent des services importants, tels que des points de gestion.  

 **Fournisseur SMS et console Configuration Manager :**  

 Configuration Manager permet l’installation de plusieurs fournisseurs SMS, chacun sur un ordinateur distinct, pour mettre plusieurs points d’accès à la disposition de la console Configuration Manager. Cela garantit que, si un ordinateur fournisseur SMS est hors connexion, vous avez la possibilité d’afficher et de reconfigurer les sites et clients Configuration Manager.  

 Quand une console Configuration Manager se connecte à un site, elle se connecte à une instance du fournisseur SMS sur ce site. L’instance du fournisseur SMS est sélectionnée de façon non déterministe. Si le fournisseur SMS sélectionné n’est pas disponible, vous disposez des options suivantes :  

-   Reconnectez la console au site. Une instance du fournisseur SMS est affectée de façon non déterministe à chaque nouvelle demande de connexion. Il se peut également qu’une instance disponible soit affectée à la nouvelle connexion.  

-   Connectez la console à un autre site Configuration Manager, puis gérez la configuration à partir de cette connexion. L'application des modifications apportées à la configuration prend quelques minutes. Lorsque le fournisseur SMS pour le site est en ligne, vous pouvez reconnecter votre console Configuration Manager directement au site à gérer.  

 Vous pouvez installer la console Configuration Manager sur plusieurs ordinateurs afin que les utilisateurs administratifs puissent l’utiliser. Chaque fournisseur SMS prend en charge des connexions à partir de plusieurs consoles Configuration Manager.  

 **Point de gestion :**  

 Installez plusieurs points de gestion sur chaque site principal et activez les sites pour publier des données de site vers votre infrastructure Active Directory et vers DNS.  

 Des points de gestion multiples permettent d'équilibrer la charge d'utilisation d'un point de gestion unique par plusieurs clients. Sans compter que vous pouvez installer une ou plusieurs réplicas de la base de données pour les points de gestion afin de réduire les opérations intensives du point de gestion et d'augmenter la disponibilité de ce rôle de système de site critique.  

 Comme vous ne pouvez installer qu'un seul point de gestion dans un site secondaire et qu'il doit se trouver sur le serveur de site secondaire, les points de gestion des sites secondaires ne sont pas considérés comme ayant une configuration à haute disponibilité.  

> [!NOTE]  
>  Les appareils gérés par une gestion des appareils mobiles locale se connectent à un seul point de gestion sur un site principal. Configuration Manager attribue le point de gestion à l’appareil mobile au moment de l’inscription et ne le change pas par la suite. Lorsque vous installez plusieurs points de gestion et que vous en activez plusieurs pour les appareils mobiles, le point de gestion qui est attribué à un client d'appareil mobile n'est pas déterministe.  
>   
>  Si le point de gestion utilisé par un client d’appareil mobile n’est plus disponible, vous devez résoudre le problème au niveau de ce point de gestion, ou réinitialiser l’appareil mobile et le réinscrire pour qu’il puisse être attribué à un autre point de gestion disponible pour les appareils mobiles.  

 **Point de distribution :**  

 Installez plusieurs points de distribution et déployez du contenu sur plusieurs points de distribution. Vous pouvez configurer des groupes de limites se chevauchant pour l'emplacement de contenu, afin de garantir aux clients sur chaque sous-réseau d'accéder à un déploiement à partir de deux points de distribution ou plus. Enfin, envisagez de configurer un point de distribution ou plus comme emplacements de secours pour le contenu.  

 Pour plus d’informations sur les emplacements de secours pour le contenu, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 **Point de service web du catalogue des applications et point du site web du catalogue des applications :**  

 Vous pouvez installer plusieurs instances de chaque rôle de système de site, et pour obtenir des performances optimales, en déployer une de chaque sur le même ordinateur de système de site.  

 Chaque rôle de système de site du catalogue d'applications fournit les mêmes informations que les autres instances de ce rôle de système de site quel que soit l'emplacement du rôle de serveur de site dans la hiérarchie. Par conséquent, quand un client envoie une demande pour le catalogue d’applications et que vous avez configuré le paramètre de l’appareil client Point du site web du catalogue des applications par défaut sur Détecter automatiquement, le client peut être redirigé vers une instance disponible. La préférence est donnée aux serveurs de système de site du catalogue d’applications locaux, sur la base de l’emplacement réseau actuel du client.  

 Pour plus d’informations sur ce paramètre client et sur le fonctionnement de la détection automatique, consultez la section [Agent ordinateur](../../core/clients/deploy/about-client-settings.md#computer-agent) dans la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).  

##  <a name="bkmk_client"></a> Haute disponibilité pour les clients  
 **Le client fonctionne de manière autonome :**  

 L’autonomie du client Configuration Manager se traduit ainsi :  

-   Les clients ne nécessitent pas un contact permanent avec un serveur de système de site spécifique. Ils utilisent de configurations connues pour effectuer des actions préconfigurées selon une planification.  

-   Les clients peuvent utiliser toute instance disponible d'un rôle de système de site qui fournit des services aux clients. Ils continueront de contacter les serveurs connus jusqu'à localiser un serveur disponible.  

-   Les clients peuvent exécuter un inventaire, des déploiements de logiciels et autres actions planifiées similaires indépendamment d'un contact direct avec les serveurs de système de site.  

-   Les clients qui sont configurés pour utiliser un point d'état de secours peuvent soumettre des détails sur le point d'état de secours lorsque la communication avec un point de gestion n'est pas possible.  

 **Les clients peuvent se réparer eux-mêmes :**  

 Les clients corrigent automatiquement les problèmes les plus typiques sans une intervention directe de l'administrateur :  

-   Régulièrement, les clients évaluent leur état et prennent les mesures nécessaires pour corriger les problèmes typiques à l'aide d'un cache local d'étapes de mise à jour et de fichiers sources pour la réparation.  

-   Lorsqu'un client ne soumet des informations d'état sur son site, le site génère une alerte. Les utilisateurs administratifs qui reçoivent ces alertes peuvent prendre des mesures immédiates pour restaurer le fonctionnement normal du client.  

 **Les clients mettent en cache les informations dont ils auront besoin ultérieurement :**  

 Lorsqu'un client communique avec un point de gestion, le client peut obtenir et mettre en cache les informations suivantes :  

-   Paramètres client.  

-   Planifications du client.  

-   Des informations sur les déploiements de logiciels et un téléchargement du logiciel que le client doit installer, lorsque le déploiement est configuré pour cette action.  

 Quand un client ne réussit pas à contacter un point de gestion, il copie dans le cache local les informations sur le statut, l’état et le client qu’il consigne sur le site. Il transfère ces données dès qu’il réussit à contacter un point de gestion.  

 **Le client peut soumettre l’état à un point d’état de secours :**  

 Quand vous configurez un client pour qu’il utilise un point d’état de secours, vous fournissez au client un point de contact supplémentaire vers lequel il peut envoyer des informations détaillées importantes sur son fonctionnement. Les clients qui sont configurés de manière à utiliser un point d'état de secours continuent à envoyer des informations sur l'état de leurs opérations vers ce rôle de système de site lorsque la communication avec un point de gestion n'est pas possible.  

 **Gestion centralisée des données et de l’identité du client :**  

 La base de données de site, plutôt que le client, conserve les informations importantes sur l’identité de chaque client et associe ces données à un utilisateur ou un ordinateur spécifique. Cela a les conséquences suivantes :  

-   Les fichiers source du client sur un ordinateur peuvent être désinstallés et réinstallés sans modifier les enregistrements historiques de l’ordinateur sur lequel est installé le client.  

-   La défaillance d'un ordinateur client n'affecte pas l'intégrité des informations qui sont stockées dans la base de données. Ces informations peuvent rester disponibles pour les rapports.  

##  <a name="bkmk_nonHAoptions"></a> Options pour les sites et les rôles système de site qui n’ont pas un haut niveau de disponibilité  
 Plusieurs systèmes de site ne prennent pas en charge des instances multiples sur un site ou dans la hiérarchie. Aidez-vous des informations ci-dessous pour préparer la mise hors connexion de ces systèmes de site.  

 **Serveur de site (site) :**  

 Configuration Manager ne prend pas en charge l’installation du serveur de site pour chaque site d’un cluster Windows Server ou NLB.  

 Les informations suivantes peuvent vous aider à vous préparer au cas où un serveur de site tomberait en panne ou ne serait pas opérationnel :  

-   La tâche de sauvegarde intégrée permet de faire une sauvegarde régulière du site. Dans un environnement de test, pratiquez régulièrement la restauration de sites à partir d'une sauvegarde.  

-   Déployez plusieurs sites principaux Configuration Manager dans une hiérarchie avec un site d’administration centrale pour créer un système redondant. En cas de panne du site, envisagez d'utiliser la stratégie de groupe Windows ou des scripts d'ouverture de session pour réattribuer des clients à un site fonctionnel.  

-   Si votre hiérarchie dispose d'un site d'administration centrale, vous pouvez restaurer celui-ci ou un site principal enfant en utilisant l'option de restauration d'une base de donnée de site à partir d'un autre site de la hiérarchie.  

-   Les sites secondaires ne peuvent pas être restaurés et doivent être réinstallés.  

 **Point de synchronisation Asset Intelligence (hiérarchie) :**  

 Ce rôle de système de site n’est pas capital et fournit une fonctionnalité facultative dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

 **Point Endpoint Protection (hiérarchie) :**  

 Ce rôle de système de site n’est pas capital et fournit une fonctionnalité facultative dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

 **Point d’inscription (site) :**  

 Ce rôle de système de site n’est pas capital et fournit une fonctionnalité facultative dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

 **Point proxy d’inscription (site) :**  

 Ce rôle de système de site n’est pas capital et fournit une fonctionnalité facultative dans Configuration Manager. Vous pouvez toutefois installer plusieurs instances de ce rôle de système de site sur un site et sur plusieurs sites dans la hiérarchie. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur.  

 Lorsque vous disposez de plusieurs serveurs proxy d'inscription sur un site, utilisez un alias DNS pour le nom du serveur. Lorsque vous utilisez cette configuration, le tourniquet DNS tolère des erreurs et l'équilibrage de charge dans une certaine mesure lorsque les utilisateurs inscrivent leurs appareils mobiles.  

 **Point d’état de secours (site ou hiérarchie) :**  

 Ce rôle de système de site n’est pas capital et fournit une fonctionnalité facultative dans Configuration Manager. Si ce système de site est mis hors ligne, utilisez l'une des options suivantes :  

-   Résolvez la cause de mise hors ligne du système de site.  

-   Désinstallez le rôle du serveur en cours et installez le rôle sur un nouveau serveur. Comme les clients sont affectés au point d'état de secours lors de leur installation, vous devrez modifier les clients existants pour qu'ils utilisent le nouveau serveur de système de site.  

### <a name="see-also"></a>Voir aussi  
 [Configurations prises en charge pour System Center Configuration Manager](../../core/plan-design/configs/supported-configurations.md)
