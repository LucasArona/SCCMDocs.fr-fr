---
title: Méthodes de découverte
titleSuffix: Configuration Manager
description: Découvrez plus en détail les méthodes de découverte disponibles pour rechercher des appareils sur votre réseau, dans Active Directory ou dans Azure Active Directory.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ed931751-18f2-4230-a09e-a0a329fbfa1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59376c5b9846e32cc8b63666956424a11211f1c0
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130790"
---
# <a name="about-discovery-methods-for-system-center-configuration-manager"></a>À propos des méthodes de découverte pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les méthodes de découverte de Configuration Manager permettent de rechercher différents appareils sur votre réseau, des appareils et des utilisateurs dans Active Directory, ou des utilisateurs dans Azure AD (Azure Active Directory). Pour utiliser efficacement une méthode de découverte, vous devez en comprendre les configurations disponibles et les limitations.  



##  <a name="bkmk_aboutForest"></a> Découverte de forêts Active Directory  
 **Configurable :** Oui  

 **Activé par défaut :** Non  

 **Comptes** que vous pouvez utiliser pour exécuter cette méthode :  

-   **Compte de découverte de forêts Active Directory** (défini par l’utilisateur)  

-   **Compte d'ordinateur** du serveur de site  

À la différence des autres méthodes de découverte Active Directory, la découverte de forêts Active Directory ne découvre pas des ressources que vous pouvez gérer. Au lieu de cela, cette méthode découvre les emplacements réseau qui sont configurés dans Active Directory. Elle peut convertir ces emplacements en limites à utiliser dans votre hiérarchie.  

Quand cette méthode est exécutée, elle effectue une recherche dans la forêt Active Directory locale, chaque forêt approuvée et chaque forêt supplémentaire que vous configurez dans le nœud **Forêts Active Directory** de la console Configuration Manager.  

Utilisez la découverte de forêts Active Directory pour :  

-   Découvrir les sites et sous-réseaux Active Directory, puis créer les limites de Configuration Manager en fonction de ces emplacements réseau.  

-   Identifier les sur-réseaux qui sont affectés à un site Active Directory. Convertir chaque sur-réseau en limite de plage d’adresses IP.  

-   Publier sur AD DS (Active Directory Domain Services) dans une forêt quand la publication est activée pour cette forêt. Le compte de forêt Active Directory spécifié doit disposer d’autorisations sur cette forêt.  

Vous pouvez gérer la découverte de forêts Active Directory dans la console Active Directory. Accédez à l’espace de travail **Administration** et développez **Configuration de la hiérarchie**.   

-   **Méthodes de découverte** : Active l’exécution de la découverte de forêts Active Directory au site de niveau supérieur de votre hiérarchie. Vous pouvez également spécifier un calendrier simple pour exécuter la découverte. Configurez-la pour créer automatiquement des limites à partir des sous-réseaux IP et des sites Active Directory qui sont découverts. La découverte de forêts Active Directory ne peut pas s'exécuter sur un site principal enfant ou un site secondaire.  

-   **Forêts Active Directory** : Configurez les forêts supplémentaires à découvrir, spécifiez chaque compte de forêt Active Directory et configurez la publication de chaque forêt. Surveillez le processus de découverte. Ajoutez des sous-réseaux IP ainsi que des sites Active Directory à Configuration Manager en tant que limites et membres des groupes de limites.  

Pour configurer la publication pour les forêts Active Directory pour chaque site de votre hiérarchie, connectez votre console Configuration Manager au site de niveau supérieur de votre hiérarchie. L’onglet **Publication** dans la boîte de dialogue **Propriétés** d’un site Active Directory peut uniquement afficher le site actuel et ses sites enfants. Quand la publication est activée pour une forêt et que le schéma de cette forêt est étendu pour Configuration Manager, les informations suivantes sont publiées pour chaque site autorisé à publier dans cette forêt Active Directory :  

-    **SMS-Site-&lt;code_site>**

-   **SMS-MP-&lt;<code_site>-&lt;nom_serveur_de_site>**  

-   **SMS-SLP-&lt;<code_site>-&lt;nom_serveur_de_site>**  

-   **SMS-&lt;code_site>-&lt;nom_site_Active_Directory_ou sous-réseau>**  

> [!NOTE]  
>  Les sites secondaires utilisent toujours le compte d'ordinateur du serveur de site secondaire pour publier dans Active Directory. Si vous voulez que les sites secondaires publient dans Active Directory, vérifiez que le compte d’ordinateur du serveur de site secondaire dispose d’autorisations de publication dans Active Directory. Un site secondaire ne peut pas publier de données dans une forêt non approuvée.  

> [!CAUTION]  
>  Si vous décochez l’option de publication d’un site sur une forêt Active Directory, toutes les informations publiées précédemment pour ce site, notamment des rôles de systèmes de site disponibles, sont supprimées d’Active Directory.  

Les actions de la découverte de forêts Active Directory sont enregistrées dans les journaux suivants :  

-   Toutes les actions, à l’exception des actions liées à la publication, sont enregistrées dans le fichier **ADForestDisc.Log** du dossier **&lt;Chemin_installation>\Logs** sur le serveur de site.  

-   Les actions de publication de la découverte de forêts Active Directory sont enregistrées dans les fichiers **hman.log** et **sitecomp.log** du dossier **&lt;Chemin_installation>\Logs** sur le serveur de site.  

Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer les méthodes de découverte](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADForestDisc).  



##  <a name="bkmk_aboutGroup"></a> Découverte de groupes Active Directory  
**Configurable :** Oui  

**Activé par défaut :** Non  

**Comptes** que vous pouvez utiliser pour exécuter cette méthode :  

-   **Compte de découverte de groupes Active Directory** (défini par l’utilisateur)  

-   **Compte d'ordinateur** du serveur de site  

> [!TIP]  
>  Pour plus d’informations,voir la section [Fonctionnalités communes de la découverte de groupes, de systèmes et d’utilisateurs Active Directory](#bkmk_shared).  

Utilisez cette méthode pour effectuer une recherche dans Active Directory Domain Services et identifier ce qui suit :  

-   Groupes de sécurité local, global et universel.  

-   Appartenance aux groupes.  

-   Informations limitées sur les ordinateurs des membres d’un groupe et les utilisateurs, notamment quand une autre méthode de découverte n’a pas encore découvert ces ordinateurs et utilisateurs.  

Cette méthode de découverte est prévue pour identifier les groupes et les relations du groupe des membres des groupes. Par défaut, seuls les groupes de sécurité sont découverts. Si vous voulez également découvrir l’appartenance aux groupes de distribution, vous devez cocher la case de l’option **Découvrir l’appartenance aux groupes de distribution** sous l’onglet **Option** de la boîte de dialogue des **propriétés de découverte de groupes Active Directory**.  

La découverte de groupes Active Directory ne prend pas en charge les attributs Active Directory étendus qui peuvent être identifiés à l’aide de la découverte de systèmes Active Directory ou de la découverte d’utilisateurs Active Directory. Puisque cette méthode de découverte n’est pas optimisée pour la découverte des ressources d’ordinateur et d’utilisateur, envisagez de l’exécuter après avoir exécuté la découverte de systèmes Active Directory et la découverte d’utilisateurs Active Directory. En effet, cette méthode crée un enregistrement de données de découverte (DDR) complet pour les groupes, mais seulement un DDR limité pour les ordinateurs et les utilisateurs qui appartiennent à des groupes.  

Vous pouvez configurer les étendues de découverte suivantes, qui contrôlent la manière dont cette méthode recherche des informations :  

-   **Emplacement** : Utilisez un emplacement si vous souhaitez rechercher un ou plusieurs conteneurs Active Directory. Cette option d’étendue prend en charge une recherche récursive des conteneurs Active Directory spécifiés. Ce processus recherche également dans chaque conteneur enfant sous le conteneur que vous spécifiez. Il continue jusqu’à ne plus trouver de conteneur enfant.  

-   **Groupes** : Utilisez les groupes si vous souhaitez rechercher un ou plusieurs groupes Active Directory spécifiques. Vous pouvez configurer **Domaine Active Directory** de manière à utiliser le domaine et la forêt par défaut ou limiter la recherche à un contrôleur de domaine individuel. En outre, vous pouvez spécifier un ou plusieurs groupes à rechercher. Si vous ne spécifiez pas au moins un groupe, tous les groupes trouvés à l'emplacement **Domaine Active Directory** spécifié sont recherchés.  

> [!CAUTION]  
>  Quand vous configurez une étendue de découverte, choisissez uniquement les groupes que vous devez découvrir. En effet, la découverte de groupes Active Directory tente de découvrir chaque membre de chaque groupe dans l’étendue de découverte. La découverte de grands groupes peut demander l'utilisation extensive de bande passante et de ressources Active Directory.  

> [!NOTE]  
>  Pour créer des regroupements basés sur des attributs Active Directory étendus (et assurer des résultats de découverte précis pour les ordinateurs et les utilisateurs), exécutez la découverte de systèmes Active Directory ou la découverte d’utilisateurs Active Directory, en fonction de ce que vous voulez découvrir.  

Les actions de la découverte de groupes Active Directory sont enregistrées dans le fichier **adsgdis.log** du dossier **&lt;Chemin_installation\>\LOGS** sur le serveur de site.  

Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer les méthodes de découverte](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



##  <a name="bkmk_aboutSystem"></a> Découverte de systèmes Active Directory  
**Configurable :** Oui  

**Activé par défaut :** Non  

**Comptes** que vous pouvez utiliser pour exécuter cette méthode :  

-   **Compte de découverte de systèmes Active Directory** (défini par l’utilisateur)  

-   **Compte d'ordinateur** du serveur de site  

> [!TIP]  
>  Pour plus d’informations,voir la section [Fonctionnalités communes de la découverte de groupes, de systèmes et d’utilisateurs Active Directory](#bkmk_shared).  

Utilisez cette méthode de découverte pour rechercher dans les emplacements Active Directory Domain Services spécifiés des ressources d’ordinateurs pouvant être utilisées pour créer des regroupements et des requêtes. Vous pouvez également installer le client Configuration Manager sur un appareil détecté à l’aide de l’installation Push du client.  

Par défaut, cette méthode découvre des informations de base sur l’ordinateur, notamment les attributs suivants :  

-   Nom de l'ordinateur  

-   Système d'exploitation et version  

-   nom du conteneur Active Directory.  

-   Adresse IP  

-   Site Active Directory  

-   Horodateur de la dernière ouverture de session  

Pour réussir la création d’un DDR pour un ordinateur, la découverte de systèmes Active Directory doit pouvoir identifier le compte d’ordinateur, puis traduire correctement le nom de l’ordinateur en une adresse IP.  

Dans la boîte de dialogue **Propriétés de la découverte de systèmes Active Directory**, sous l’onglet **Attributs Active Directory**, vous pouvez afficher la liste complète des attributs d’objets par défaut découverts. Vous pouvez également configurer cette méthode pour découvrir des attributs supplémentaires (étendus).  

Les actions de la découverte de systèmes Active Directory sont enregistrées dans le fichier **adsysdis.log** du dossier **&lt;Chemin_installation\>\LOGS** sur le serveur de site.  

Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer les méthodes de découverte](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



##  <a name="bkmk_aboutUser"></a> Découverte d’utilisateurs Active Directory  
**Configurable :** Oui  

**Activé par défaut :** Non  

**Comptes** que vous pouvez utiliser pour exécuter cette méthode :  

-   **Compte de découverte d’utilisateurs Active Directory** (défini par l’utilisateur)  

-   **Compte d'ordinateur** du serveur de site  

> [!TIP]  
>  Pour plus d’informations,voir la section [Fonctionnalités communes de la découverte de groupes, de systèmes et d’utilisateurs Active Directory](#bkmk_shared).  

Utilisez cette méthode de découverte pour rechercher dans Active Directory Domain Services des comptes d’utilisateur et les attributs associés. Par défaut, cette méthode découvre des informations de base sur le compte d’utilisateur, notamment les attributs suivants :  

-   Nom d'utilisateur  

-   Nom d'utilisateur unique (y compris le nom de domaine)  

-   Domaine  

-   Noms de conteneurs Active Directory  

Dans la boîte de dialogue **Propriétés de la découverte d’utilisateurs Active Directory**, sous l’onglet **Attributs Active Directory**, vous pouvez afficher la liste par défaut complète des attributs d’objets découverts. Vous pouvez également configurer cette méthode pour découvrir des attributs supplémentaires (étendus).

Les actions de la découverte d’utilisateurs Active Directory sont enregistrées dans le fichier **adusrdis.log** du dossier **&lt;Chemin_installation\>\LOGS** sur le serveur de site.  

Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer les méthodes de découverte](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigADDiscGeneral).  



## <a name="azureaddisc"></a> Découverte des utilisateurs Azure Active Directory
Utilisez la découverte d’utilisateurs Azure AD (Azure Active Directory) pour rechercher dans votre abonnement Azure AD les utilisateurs avec une identité de cloud moderne. La découverte d’utilisateurs Azure AD peut trouver les attributs suivants :  
-   objectId
-   displayName
-   messagerie
-   mailNickname
-   onPremisesSecurityIdentifier
-   userPrincipalName
-   AAD tenantID

Cette méthode prend en charge une synchronisation complète et une synchronisation delta des attributs utilisateur à partir d’Azure AD. Vous pouvez ensuite utiliser ces informations avec les données de découverte que vous collectez par le biais des autres méthodes de découverte.

Les actions de la découverte d’utilisateurs Azure AD sont enregistrées dans le fichier **SMS_AZUREAD_DISCOVERY_AGENT.log** sur le serveur de site de niveau supérieur de la hiérarchie.

Pour configurer la découverte d’utilisateurs Azure AD, consultez [Configurer les services Azure](/sccm/core/servers/deploy/configure/Azure-services-wizard) pour la gestion cloud. Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer la découverte des utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).



##  <a name="bkmk_aboutHeartbeat"></a> Découverte par pulsations d’inventaire  
**Configurable :** Oui  

**Activé par défaut :** Oui  

**Comptes** que vous pouvez utiliser pour exécuter cette méthode :  

-   **Compte d'ordinateur** du serveur de site  

La découverte par pulsations d'inventaire diffère des autres méthodes de découverte de Configuration Manager. Elle est activée par défaut et s’exécute sur chaque client de l’ordinateur (et non sur un serveur de site) pour créer un DDR. Pour les clients d’appareils mobiles, ce DDR est créé par le point de gestion qui est utilisé par le client de l’appareil mobile. Pour permettre la tenue à jour de l’enregistrement de base de données des clients Configuration Manager, ne désactivez pas la découverte par pulsations d'inventaire. Par ailleurs, cette méthode peut forcer la découverte d’un ordinateur en tant que nouvel enregistrement de ressource. Elle peut également de nouveau remplir l’enregistrement de base de données d’un ordinateur qui a été supprimé de la base de données.  

La découverte par pulsations d’inventaire est exécutée selon un calendrier configuré pour tous les clients de la hiérarchie. Le calendrier par défaut pour la découverte par pulsations d’inventaire est défini sur tous les sept jours. Si vous modifiez l’intervalle de découverte par pulsations d’inventaire, vérifiez qu’elle est exécutée plus fréquemment que la tâche de maintenance de site **Supprimer les données de découverte anciennes**. Cette tâche supprime les enregistrements de clients inactifs de la base de données du site. Vous pouvez configurer la tâche **Supprimer les données de découverte anciennes** uniquement pour les sites principaux. 

Vous pouvez également appeler manuellement la découverte par pulsations d’inventaire sur un client spécifique. Exécutez le **Cycle de collecte de données de découverte** sous l’onglet **Action** du panneau de configuration Configuration Manager d’un client.  

Durant son exécution, la découverte par pulsations d’inventaire crée un DDR comprenant les informations actuelles du client. Le client copie ensuite ce petit fichier (d’environ 1 Ko) sur un point de gestion pour qu’un site principal puisse le traiter. Le fichier comprend les informations suivantes :  

-   Emplacement réseau  

-   Nom NetBIOS  

-   Version de l’agent client  

-   Détails sur l’état opérationnel  

La découverte par pulsations d'inventaire est la seule méthode de découverte qui fournit des détails sur l'état de l'installation du client. Pour cela, elle met à jour l’attribut du client de la ressource système avec une valeur égale à **Oui**.  

> [!NOTE]  
>  Même lorsque la découverte par pulsations d'inventaire est désactivée, les enregistrements de découverte de données sont toujours créés et soumis pour les clients d’appareils mobiles actifs. Ce comportement garantit que la tâche **Supprimer les données de découverte anciennes** n’affecte pas les appareils mobiles actifs. Quand la tâche **Supprimer les données de découverte anciennes** supprime un enregistrement de base de données pour un appareil mobile, elle révoque également le certificat de l’appareil. Cette action empêche l’appareil mobile de se connecter aux points de gestion.  

Les actions de la découverte par pulsations d'inventaire sont consignées aux emplacements suivants :  

-   Pour les ordinateurs clients, les actions de la découverte par pulsations d’inventaire sont enregistrées sur le client dans le fichier **InventoryAgent.log** du dossier *%Windir%\CCM\Logs*.  

-   Pour les clients d’appareils mobiles, les actions de découverte par pulsations d’inventaire sont enregistrées dans le fichier **DMPRP.log** du dossier *%Program Files%\CCM\Logs* du point de gestion que le client d’appareil mobile utilise.  

Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer les méthodes de découverte](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigHBDisc).  



##  <a name="bkmk_aboutNetwork"></a> Découverte du réseau  
**Configurable :** Oui  

**Activé par défaut :** Non  

**Comptes** que vous pouvez utiliser pour exécuter cette méthode :  

-   **Compte d'ordinateur** du serveur de site  

Utilisez cette méthode pour découvrir la topologie de votre réseau et les appareils de votre réseau qui ont une adresse IP. La découverte du réseau cherche sur votre réseau des ressources sur lesquelles IP est activé en interrogeant les entités suivantes : 
- Serveurs qui exécutent une implémentation Microsoft de DHCP
- Caches ARP (Address Resolution Protocol) dans les routeurs réseau
- périphériques SNMP
- Domaines Active Directory  

Pour utiliser la découverte du réseau, vous devez spécifier le *niveau* de découverte à exécuter. Vous configurez également un ou plusieurs mécanismes de découverte qui permettent à la découverte du réseau d'interroger des segments ou périphériques réseau. Vous pouvez également configurer des paramètres qui permettent de contrôler des actions de découverte sur le réseau. Enfin, vous définissez un ou plusieurs calendriers d'exécution de la découverte du réseau.  

Pour que cette méthode découvre une ressource, elle doit identifier l’adresse IP et le masque de sous-réseau de la ressource. Les méthodes suivantes sont utilisées pour identifier le masque de sous-réseau d'un objet :  

-   **Cache ARP du routeur :** La découverte du réseau interroge la mémoire cache ARP d'un routeur pour rechercher des informations de sous-réseau. En règle générale, les données situées dans la mémoire cache ARP d'un routeur ont une courte durée de vie. Par conséquent, quand la découverte du réseau interroge la mémoire cache ARP, celle-ci peut ne plus avoir d’informations sur l’objet demandé.  

-   **DHCP :** La découverte du réseau interroge chaque serveur DHCP que vous spécifiez pour découvrir les périphériques pour lesquels le serveur DHCP a fourni un bail. La découverte du réseau prend en charge uniquement les serveurs DHCP qui exécutent l'implémentation Microsoft du protocole DHCP.  

-   **Périphérique SNMP :** La découverte du réseau peut interroger directement un périphérique SNMP. Pour que la découverte du réseau puisse interroger un périphérique, celui-ci doit avoir un agent SNMP local installé. Configurez également la découverte du réseau pour utiliser le nom de communauté utilisé par l’agent SNMP.  

Quand la découverte identifie un objet IP et peut déterminer le masque de sous-réseau des objets, elle crée un DDR pour cet objet. Étant donné que différents types d’appareils se connectent au réseau, la découverte du réseau découvre des ressources qui ne prennent pas en charge le client Configuration Manager. Par exemple, parmi les périphériques qui peuvent être découverts mais qui ne peuvent pas être gérés, citons les imprimantes et les routeurs.  

La découverte du réseau peut retourner plusieurs attributs dans le cadre de l’enregistrement de découverte qu’elle crée, Parmi ces attributs, citons notamment :  

-   Nom NetBIOS  

-   Adresses IP  

-   Domaine de la ressource  

-   Rôles de système  

-   Nom de communauté SNMP  

-   Adresses MAC  

L’activité de la découverte du réseau est enregistrée dans le fichier **Netdisc.log** dans *&lt;Chemin_installation\>\Logs* sur le serveur de site qui exécute la découverte.  

 Pour plus d’informations sur la configuration de cette méthode de découverte, consultez [Configurer les méthodes de découverte](/sccm/core/servers/deploy/configure/configure-discovery-methods#BKMK_ConfigNetworkDisc).  

> [!NOTE]  
>  Les réseaux complexes et les connexions à faible bande passante peuvent ralentir la découverte du réseau et générer un important trafic réseau. Comme meilleure pratique, exécutez la découverte du réseau uniquement lorsque les autres méthodes de découverte ne peuvent pas trouver les ressources que vous devez découvrir. Par exemple, utilisez la découverte du réseau si vous devez découvrir des ordinateurs du groupe de travail. D’autres méthodes de découverte ne découvrent pas les ordinateurs du groupe de travail.  

###  <a name="BKMK_NetDiscLevels"></a> Niveaux de découverte du réseau  
Lorsque vous configurez la découverte du réseau, vous spécifiez l'un des trois niveaux de découverte :  

|Niveau de découverte|Détails|  
|------------------------|-------------|  
|Topologie|Ce niveau découvre des routeurs et des sous-réseaux mais n'identifie pas un masque de sous-réseau pour les objets.|  
|Topologie et client ;|En plus de la topologie, ce niveau découvre des clients potentiels, comme des ordinateurs, et des ressources, comme des imprimantes et des routeurs. Ce niveau de découverte tente d’identifier le masque de sous-réseau des objets qu’il trouve.|  
|Topologie, client et système d’exploitation.|Outre la topologie et les clients potentiels, ce niveau tente de découvrir le nom et la version du système d’exploitation de l’ordinateur. Ce niveau utilise l'Explorateur Windows et les appels de gestion de réseau Windows.|  

 Avec chaque niveau incrémentiel, la découverte du réseau augmente son activité et l'utilisation de la bande passante du réseau. Tenez compte du trafic réseau qui peut être généré avant d'activer tous les aspects de la découverte du réseau.  

 Par exemple, lorsque vous utilisez la découverte du réseau pour la première fois, vous pouvez commencer avec le niveau de topologie uniquement pour identifier votre infrastructure réseau. Ensuite, reconfigurez la découverte du réseau pour découvrir des objets et les systèmes d’exploitation de leur appareil. Vous pouvez également configurer des paramètres qui limitent la découverte du réseau à une plage spécifique de segments de réseau. De cette façon, vous découvrez des objets à des emplacements réseau dont vous avez besoin et évitez tout trafic réseau inutile. Ce processus vous permet également de découvrir des objets à partir de routeurs de périphérie ou à l’extérieur de votre réseau.  

###  <a name="BKMK_NetDiscOptions"></a> Options de découverte du réseau  
Pour permettre à la découverte du réseau de rechercher des appareils avec adresse IP, configurez une ou plusieurs des options suivantes.  

> [!NOTE]  
>  La découverte du réseau est exécutée dans le contexte du compte d'ordinateur du serveur de site qui exécute la découverte. Si le compte d’ordinateur ne dispose pas d’autorisation sur un domaine non approuvé, les configurations du domaine et du serveur DHCP peuvent ne pas réussir à découvrir des ressources.  

#### <a name="dhcp"></a>DHCP  

Spécifiez chaque serveur DHCP que la découverte du réseau devra interroger. (La découverte du réseau prend en charge uniquement les serveurs DHCP qui exécutent l’implémentation Microsoft du protocole DHCP.)  

-   La découverte du réseau récupère les informations en émettant des appels de procédure distante vers la base de données sur le serveur DHCP.  

-   La découverte du réseau peut interroger des serveurs DHCP 32 bits et 64 bits pour une liste de périphériques qui sont enregistrés avec chaque serveur.  

-   Pour que la découverte du réseau interroge avec succès un serveur DHCP, le compte d'ordinateur du serveur qui exécute la découverte doit être membre du groupe d'utilisateurs DHCP sur le serveur DHCP. Par exemple, ce niveau d’accès existe quand l’une des affirmations suivantes est vraie :  

    -   Le serveur DHCP spécifié est le serveur DHCP du serveur qui exécute la découverte.  

    -   L'ordinateur qui exécute la découverte et le serveur DHCP se trouvent dans le même domaine.  

    -   Il existe une relation d'approbation bidirectionnelle entre l'ordinateur qui exécute la découverte et le serveur DHCP.  

    -   Le serveur de site est membre du groupe d’utilisateurs DHCP.  

-   Lorsque la découverte du réseau énumère un serveur DHCP, elle ne découvre pas toujours des adresses IP statiques. La découverte du réseau ne trouve pas d’adresses IP appartenant à une plage exclue d’adresses IP sur le serveur DHCP. Par ailleurs, elle ne découvre pas d’adresses IP réservées à l’attribution manuelle.  

#### <a name="domains"></a>Domaines  

Spécifiez chaque domaine que la découverte du réseau devra interroger.  

-   Le compte d’ordinateur du serveur de site qui exécute la découverte doit disposer d'autorisations pour lire les contrôleurs de domaine dans chaque domaine spécifié.  

-   Pour découvrir les ordinateurs du domaine local, vous devez activer le service du navigateur d’ordinateur sur au moins un ordinateur. Cet ordinateur doit se trouver sur le même sous-réseau que le serveur de site qui exécute la découverte du réseau.  

-   La découverte du réseau peut découvrir n'importe quel ordinateur que vous pouvez consulter à partir de votre serveur de site lorsque vous parcourez le réseau.  

-   La découverte du réseau récupère l’adresse IP. Elle utilise ensuite une demande d’écho ICMP (Internet Control Message Protocol) pour effectuer un test ping sur chaque appareil qu’elle trouve. La commande **ping** permet de déterminer quels ordinateurs sont actuellement actifs.  

#### <a name="snmp-devices"></a>Unités SNMP  

Spécifiez chaque unité SNMP que la découverte du réseau devra interroger.  

-   La découverte du réseau récupère la valeur ipNetToMediaTable depuis toute unité SNMP qui répond à la requête. Cette valeur retourne des groupes d’adresses IP qui sont des ordinateurs clients ou autres ressources, comme des imprimantes, des routeurs ou d’autres périphériques IP.  

-   Pour interroger un périphérique, vous devez spécifier l’adresse IP ou le nom NetBIOS du périphérique.  

-   Configurez la découverte du réseau de sorte qu’elle utilise le nom de communauté de l’appareil ; dans le cas contraire, l’appareil rejette la requête basée sur SNMP.  


###  <a name="BKMK_LimitNetDisc"></a> Limitation de la découverte du réseau  
Quand la découverte du réseau interroge un appareil SNMP sur le bord de votre réseau, elle peut identifier des informations sur les sous-réseaux et les appareils SNMP qui sont en dehors de votre réseau immédiat. Utilisez les informations suivantes pour limiter la découverte du réseau en configurant les unités SNMP avec lesquelles la découverte peut communiquer et en spécifiant les segments réseau à interroger.  

#### <a name="subnets"></a>Sous-réseaux  

Configurez les sous-réseaux que la découverte du réseau interroge lorsqu'elle utilise les options DHCP et SNMP. Ces deux options cherchent uniquement les sous-réseaux activés.  

Par exemple, une requête DHCP peut renvoyer des périphériques à partir d'emplacements situés dans l'ensemble de votre réseau. Si vous souhaitez découvrir uniquement des périphériques situés sur un sous-réseau spécifique, spécifiez et activez ce sous-réseau spécifique sous l’onglet **Sous-réseaux** de la boîte de dialogue **Propriétés de la découverte du réseau**. Quand vous spécifiez et activez des sous-réseaux, vous limitez les futures tâches de découverte DHCP et SNMP à ces sous-réseaux.  

> [!NOTE]  
>  Les configurations de sous-réseau ne limitent pas les objets que l’option de découverte **Domaines** découvre.  

#### <a name="snmp-community-names"></a>Noms de communautés SNMP  

Pour permettre à la découverte du réseau d’interroger avec succès un appareil SNMP, configurez la découverte du réseau avec le nom de communauté de l’appareil. Si la découverte du réseau n'est pas configurée à l'aide du nom de communauté du périphérique SNMP, le périphérique rejette la requête.  

#### <a name="maximum-hops"></a>Nombre maximal de sauts  

Lorsque vous configurez le nombre maximal de sauts de routeur, vous limitez le nombre de segments réseau et de routeurs que la découverte du réseau peut interroger à l'aide du protocole SNMP.  

Le nombre de sauts que vous configurez limite le nombre de périphériques supplémentaires et de segments réseau que la découverte du réseau peut interroger.  

Par exemple, une découverte pour la topologie uniquement avec **0** (zéro) saut de routeur découvre le sous-réseau sur lequel réside le serveur d’origine. Elle inclut tous les routeurs de ce sous-réseau.  

Le diagramme suivant illustre le résultat d’une requête de découverte du réseau pour la topologie, uniquement quand elle est exécutée sur le serveur 1 avec 0 saut de routeur spécifié : sous-réseau D et routeur 1.  

 ![Image de découverte avec zéro saut de routeur](media/Disc-0.gif)  

 Le diagramme suivant illustre le résultat d’une requête de découverte du réseau pour la topologie et le client, quand elle est exécutée sur le serveur 1 avec 0 saut de routeur spécifié : sous-réseau D et routeur 1, ainsi que tous les clients potentiels du sous-réseau D.  

 ![Image de découverte avec un saut de routeur](media/Disc-1.gif)  

 Pour mieux comprendre comment les sauts de routeur supplémentaires peuvent augmenter la quantité de ressources réseau découvertes, prenez l'exemple de réseau suivant :  

 ![Image de découverte avec deux sauts de routeur](media/Disc-2.gif)  

 L’exécution d’une découverte du réseau pour la topologie uniquement à partir du serveur 1 avec un saut de routeur permet de découvrir les entités suivantes :  

-   Routeur 1 et sous-réseau 10.1.10.0 (détectés avec zéro saut)  

-   Sous-réseaux 10.1.20.0 et 10.1.30.0, sous-réseau A et routeur 2 (détectés sur le premier saut)  

> [!WARNING]  
>  Chaque augmentation du nombre de sauts de routeur peut considérablement augmenter le nombre de ressources à découvrir et augmenter la bande passante réseau utilisée par la découverte du réseau.  



##  <a name="bkmk_aboutServer"></a> Découverte de serveurs  
**Configurable :** Non  

Outre ces méthodes de découverte pouvant être configurées par l’utilisateur, Configuration Manager utilise un processus appelé **découverte de serveurs** (SMS_WINNT_SERVER_DISCOVERY_AGENT). Cette méthode de découverte crée des enregistrements de ressources pour les ordinateurs qui sont des systèmes de site, par exemple un ordinateur configuré comme point de gestion.  



##  <a name="bkmk_shared"></a> Fonctionnalités communes de la découverte de groupes, de systèmes et d’utilisateurs Active Directory  
Cette section fournit des informations sur les fonctionnalités qui sont communes aux méthodes de découverte suivantes :  

-   Découverte de groupes Active Directory  

-   Découverte de systèmes Active Directory  

-   Découverte d’utilisateurs Active Directory  

> [!NOTE]  
>  Les informations dans cette section ne s'appliquent pas à la découverte de forêts Active Directory.  

Ces trois méthodes de découverte sont similaires au niveau de la configuration et du fonctionnement. Elles peuvent découvrir des ordinateurs, des utilisateurs et des informations sur les appartenances aux groupes des ressources qui sont stockées dans Active Directory Domain Services. Le processus de découverte est géré par un agent de découverte. L’agent s’exécute sur le serveur de site sur chaque site où l’exécution de la découverte est configurée. Vous pouvez configurer chacune de ces méthodes de découverte pour rechercher un ou plusieurs emplacements Active Directory en tant qu'instances d'emplacement dans la forêt locale ou dans les forêts distantes.  

Lorsque la découverte recherche des ressources dans une forêt non approuvée, l'agent de découverte doit être en mesure de résoudre les éléments suivants pour fonctionner correctement :  

-   Pour découvrir une ressource d’ordinateur à l’aide de la découverte de systèmes Active Directory, l’agent de découverte doit pouvoir résoudre le nom de domaine complet de la ressource. Dans le cas contraire, il tente ensuite de résoudre la ressource par son nom NetBIOS.  

-   Pour découvrir une ressource d’utilisateur ou de groupe à l’aide de la découverte d’utilisateurs Active Directory ou de la découverte de groupes Active Directory, l’agent de découverte doit pouvoir résoudre le nom de domaine complet du contrôleur de domaine spécifié pour l’emplacement Active Directory.  

Pour chaque emplacement que vous spécifiez, vous pouvez configurer des options de recherche individuelles, comme l’activation d’une recherche récursive des emplacements de conteneurs enfants Active Directory. Vous pouvez également configurer un compte unique à utiliser lors de la recherche de cet emplacement. Vous bénéficiez ainsi de flexibilité dans la configuration d’une méthode de découverte sur un site pour chercher à plusieurs emplacements Active Directory dans plusieurs forêts. Vous n’avez pas à configurer un compte unique avec des autorisations sur tous les emplacements.  

Quand l’une de ces trois méthodes de découverte s’exécute sur un site spécifique, le serveur de site Configuration Manager sur le site contacte le contrôleur de domaine le plus proche dans la forêt Active Directory spécifiée pour localiser les ressources Active Directory. Le domaine et la forêt peuvent être dans n’importe quel mode Active Directory pris en charge. Le compte que vous attribuez à chaque instance d’emplacement doit disposer de l’autorisation d’accès **Lecture** aux emplacements Active Directory spécifiés.

La découverte recherche des objets aux emplacements spécifiés, puis tente de recueillir des informations sur ces objets. Lorsque suffisamment d'informations sur une ressource sont identifiées, un enregistrement de données de découverte est créé. Les informations requises varient en fonction de la méthode de découverte utilisée.  

Si vous configurez l'exécution d'une même méthode de découverte dans différents sites Configuration Manager pour tirer profit de l'interrogation des serveurs Active Directory locaux, vous pouvez configurer chaque site à l'aide d'un ensemble unique d'options de découverte. Étant donné que les données de découverte sont partagées avec chaque site de la hiérarchie, évitez la superposition entre ces configurations pour découvrir de manière efficace chaque ressource une seule fois.

Dans les environnements plus petits, envisagez d’exécuter chaque méthode de découverte sur un seul site dans votre hiérarchie. Cette configuration réduit les charges administratives supplémentaires et la possibilité de multiples actions de découverte redécouvrant les mêmes ressources. Quand vous limitez le nombre de sites exécutant des découvertes, vous réduisez la bande passante réseau globale utilisée par la découverte. Vous pouvez également réduire le nombre global de DDR qui sont créés et qui doivent être traités par vos serveurs de site.  

De nombreuses configurations de méthode de découverte sont intuitives. Utilisez les sections suivantes pour en savoir plus sur les options de découverte qui requièrent plus d'informations préalables à la configuration.  

Les options suivantes peuvent être utilisées avec plusieurs méthodes de découverte Active Directory :  

-   [Découverte delta](#bkmk_delta)  

-   [Filtrer les enregistrements d’ordinateurs obsolètes par connexion au domaine](#bkmk_stalelogon)  

-   [Filtrer les enregistrements obsolètes par mot de passe de l'ordinateur](#bkmk_stalepassword)  

-   [Rechercher les attributs Active Directory personnalisés](#bkmk_customAD)  


###  <a name="bkmk_delta"></a> Découverte delta  
Disponible pour :  

-   Découverte de groupes Active Directory  

-   Découverte de systèmes Active Directory  

-   Découverte d’utilisateurs Active Directory  

La découverte delta n’est pas une méthode de découverte indépendante, mais une option disponible pour les méthodes de découverte applicables. La découverte delta recherche dans des attributs Active Directory spécifiques des modifications qui ont été apportées depuis le dernier cycle de découverte complète de la méthode de détection applicable. Les modifications d’attributs sont soumises à la base de données Configuration Manager pour mettre à jour l’enregistrement de découverte de la ressource.  

Par défaut, la découverte delta s'exécute sur un cycle de cinq minutes. Autrement dit, elle a lieu beaucoup plus fréquemment qu’un cycle complet de découverte. Cette fréquence est possible car la découverte delta utilise moins de ressources de serveur de site et de ressources réseau qu’un cycle de découverte complète. Lorsque vous utilisez la découverte delta, vous pouvez réduire la fréquence du cycle de découverte complète pour cette méthode de découverte.  

Les modifications les plus courantes détectées par la découverte delta sont les suivantes :  

-   Ajout de nouveaux ordinateurs ou utilisateurs à Active Directory  

-   Modifications des informations de base de l'ordinateur et de l'utilisateur  

-   Ajout de nouveaux ordinateurs ou utilisateurs à un groupe  

-   Suppression d'ordinateurs ou d'utilisateurs d'un groupe  

-   Modifications apportées aux objets de groupes de systèmes  

Bien que la découverte delta puisse détecter de nouvelles ressources et des modifications de l’appartenance à un groupe, elle ne peut pas détecter qu’une ressource a été supprimée d’Active Directory. Les enregistrements de données de découverte (DDR) créés par la découverte delta sont traités de la même manière que les DDR qui sont créés par un cycle de découverte complète.  

Vous configurez la découverte delta à partir de l'onglet **Calendrier d'interrogation** dans les propriétés de chaque méthode de découverte.  


###  <a name="bkmk_stalelogon"></a> Filtrer les enregistrements d’ordinateurs obsolètes par connexion au domaine  
Disponible pour :  

-   Découverte de groupes Active Directory  

-   Découverte de systèmes Active Directory  

Vous pouvez configurer la découverte de manière à exclure les ordinateurs ayant un enregistrement d’ordinateur obsolète. Cette exclusion est basée sur la dernière connexion de l’ordinateur au domaine. Quand cette option est activée, la découverte de systèmes Active Directory évalue chaque ordinateur identifié. La découverte de groupes Active Directory évalue chaque ordinateur membre d'un groupe qui est découvert.  

Pour utiliser cette option :  

-   Les ordinateurs doivent être configurés pour mettre à jour l’attribut **lastLogonTimeStamp** dans les services de domaine Active Directory.  

-   Le niveau fonctionnel du domaine Active Directory doit être défini sur Windows Server 2003 ou version ultérieure.  

Quand vous configurez le délai entre la dernière connexion et l’utilisation de ce paramètre, prenez en compte l’intervalle de réplication entre les contrôleurs de domaine.  

Configurez le filtrage sous l’onglet **Option** dans les boîtes de dialogue des **propriétés de découverte des systèmes Active Directory** et des **propriétés de découverte de groupes Active Directory**. Choisissez l’option **Découvrir uniquement les ordinateurs qui se sont connectés à un domaine pendant une période donnée**.  

> [!WARNING]  
>  Quand vous configurez ce filtre et **Filtrer les enregistrements obsolètes par mot de passe de l’ordinateur**, les ordinateurs qui répondent aux critères de l’un des filtres sont exclus de la découverte.  


###  <a name="bkmk_stalepassword"></a> Filtrer les enregistrements obsolètes par mot de passe de l’ordinateur  
Disponible pour :  

-   Découverte de groupes Active Directory  

-   Découverte de systèmes Active Directory  

Vous pouvez configurer la découverte de manière à exclure les ordinateurs ayant un enregistrement d’ordinateur obsolète. Cette exclusion est basée sur la dernière mise à jour du mot de passe du compte d’ordinateur par l’ordinateur. Quand cette option est activée, la découverte de systèmes Active Directory évalue chaque ordinateur identifié. La découverte de groupes Active Directory évalue chaque ordinateur membre d'un groupe qui est découvert.  

Pour utiliser cette option :  

-   Les ordinateurs doivent être configurés pour mettre à jour l’attribut **pwdLastSet** dans les services de domaine Active Directory.  

Quand vous configurez cette option, prenez en compte l’intervalle pour les mises à jour de cet attribut en plus de l’intervalle de réplication entre les contrôleurs de domaine.  

Configurez le filtrage sous l’onglet **Option** dans les boîtes de dialogue des **propriétés de découverte des systèmes Active Directory** et des **propriétés de découverte de groupes Active Directory**. Choisissez l’option **Découvrir uniquement les ordinateurs qui ont mis à jour le mot de passe de leur compte d’ordinateur pendant une période donnée**.  

> [!WARNING]  
>  Quand vous configurez ce filtre et **Filtrer les enregistrements obsolètes par connexion au domaine**, les ordinateurs qui répondent aux critères de l’un des filtres sont exclus de la découverte.  


###  <a name="bkmk_customAD"></a> Rechercher les attributs Active Directory personnalisés  
 Disponible pour :  

-   Découverte de systèmes Active Directory  

-   Découverte d’utilisateurs Active Directory  

Chaque méthode de découverte prend en charge une liste unique d'attributs Active Directory pouvant être découverts.  

Vous pouvez afficher et configurer les liste des attributs personnalisés sous l’onglet **Attributs Active Directory** des boîtes de dialogue des **propriétés de découverte des systèmes Active Directory** et des **propriétés de découverte d’utilisateurs Active Directory**.  
