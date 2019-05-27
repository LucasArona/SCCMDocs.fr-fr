---
title: Configurer la découverte
titleSuffix: Configuration Manager
description: Configurez des méthodes de découverte pour trouver des ressources à gérer à partir de votre réseau, d’Active Directory et d’Azure Active Directory.
ms.date: 08/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38b2355159e3ce0472a5a5ceb0ff0a5f2275358d
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65499539"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Configurer les méthodes de découverte de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Configurez des méthodes de découverte pour trouver des ressources à gérer à partir de votre réseau, d’Active Directory et d’Azure Active Directory (Azure AD). Commencez par activer et configurer chaque méthode à utiliser pour explorer votre environnement. Vous pouvez aussi désactiver une méthode en suivant la même procédure que pour l’activer. La découverte par pulsations d’inventaire et la découverte de serveurs constituent les seules exceptions à ce processus :  

-   Par défaut, la **découverte par pulsations d’inventaire** est déjà activée au moment où vous installez un site principal Configuration Manager. Elle est configurée pour s’exécuter selon une planification de base. Maintenez la découverte par pulsations d’inventaire activée, car cette méthode garantit que les enregistrements de données de découverte (DDR) des appareils sont à jour. Pour plus d’informations sur la découverte par pulsations d’inventaire, consultez [Découverte par pulsations d’inventaire](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  

-   La **découverte de serveurs** est une méthode de découverte automatique. Elle recherche les ordinateurs que vous utilisez comme systèmes de site. Elle n’est ni configurable ni désactivable.  

### <a name="enable-a-configurable-discovery-method"></a>Activer une méthode de découverte configurable  
 > [!NOTE]  
 > Les informations suivantes ne s’appliquent pas à la découverte d’utilisateurs Azure AD. Consultez plutôt [Configurer la découverte d’utilisateurs Azure AD](#azureaadisc) plus loin dans cet article.

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie**, puis sélectionnez **Méthodes de découverte**.  

2.  Sélectionnez la méthode de découverte pour le site sur lequel vous voulez activer la découverte.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**. Ensuite, dans l’onglet **Général**, sélectionnez l’option **Activer la &lt;méthode de découverte\>** .  

     Si cette option est déjà activée, vous pouvez désactiver la méthode de découverte en décochant la case.  

4.  Cliquez sur **OK** pour enregistrer la configuration.  



##  <a name="BKMK_ConfigADForestDisc"></a> Configurer la découverte de forêts Active Directory  

Pour terminer la configuration de la découverte de forêts Active Directory, configurez les paramètres aux emplacements suivants de la console Configuration Manager :  

- Dans le nœud **Méthodes de découverte** :

    - Activer cette méthode de découverte.  

    - Définir un calendrier d’interrogation.  

    - Indiquez si la découverte doit créer automatiquement des limites pour les sites Active Directory et les sous-réseaux qui sont découverts.  

- Dans le nœud **Forêts Active Directory** :

    - Ajouter les forêts à découvrir.  

    - Activer la découverte des sites et sous-réseaux Active Directory dans cette forêt.  

    - Configurer les paramètres permettant aux sites Configuration Manager de publier leurs informations de site dans la forêt.  

    - Attribuer un compte à utiliser comme compte de forêt Active Directory pour chaque forêt.  

Utilisez les procédures suivantes pour activer la découverte de forêts Active Directory et configurer chaque forêt à utiliser avec la découverte de forêts Active Directory.  


### <a name="enable-active-directory-forest-discovery"></a>Activer la découverte de forêts Active Directory  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie** et sélectionnez le nœud **Méthodes de découverte**.  

2.  Sélectionnez la méthode Découverte de forêts Active Directory pour le site sur lequel vous voulez configurer la découverte.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4.  Dans l’onglet **Général**, cochez la case permettant d’activer la découverte. Vous pouvez aussi configurer la découverte maintenant et l’activer ultérieurement.  

5.  Spécifiez les options nécessaires pour créer des limites de site des emplacements découverts.  

6.  Spécifiez une planification du moment d'exécution de la découverte.  

7.  Cliquez sur **OK** pour enregistrer la configuration.  


### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Configurer une forêt pour permettre la découverte de forêts Active Directory  

1.  Dans l’espace de travail **Administration**, développez **Configuration de la hiérarchie** et sélectionnez le nœud **Forêts Active Directory**. Si la découverte de forêts Active Directory a été exécutée précédemment, vous pouvez voir chaque forêt découverte dans le volet des résultats. La forêt locale et toutes les forêts approuvées sont découvertes lorsque la Découverte de forêts Active Directory s'exécute. Seules les forêts non approuvées doivent être ajoutées manuellement.  

    -   Pour configurer une forêt déjà découverte, sélectionnez-la dans le volet de résultats. Ensuite, dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés** pour ouvrir les propriétés de la forêt. Passez à l'étape 3.  

    -   Pour configurer une nouvelle forêt, qui n’apparaît pas dans la liste, sélectionnez **Ajouter une forêt** dans le groupe **Créer** de l’onglet **Accueil** du ruban. Cette action ouvre la boîte de dialogue **Ajouter une forêt**. Passez à l'étape 3.  

2.  Dans l’onglet **Général**, finalisez la configuration de forêt que vous souhaitez découvrir et spécifiez le **Compte de forêt Active Directory**. Pour plus d’informations sur ce compte, voir [Comptes](/sccm/core/plan-design/hierarchy/accounts#active-directory-forest-account).  

    > [!NOTE]  
    >  La découverte de forêts Active Directory requiert un compte global pour découvrir et publier les forêts non approuvées. Si vous n’utilisez pas le compte d’ordinateur du serveur de site, vous ne pouvez sélectionner qu’un compte global.  

3.  Si vous prévoyez d’autoriser des sites à publier des données de site dans cette forêt, dans l’onglet **Publication**, terminez la configuration de la publication dans cette forêt.  

    > [!NOTE]  
    >  Si vous autorisez les sites à publier dans une forêt, étendez le schéma Active Directory de cette forêt à Configuration Manager. Le compte de forêt Active Directory doit avoir des autorisations Contrôle total sur le conteneur système dans cette forêt.  

4.  Cliquez sur **OK** pour enregistrer la configuration.  



##  <a name="BKMK_ConfigADDiscGeneral"></a>Configurer la découverte Active Directory d’ordinateurs, d’utilisateurs ou de groupes  

Pour configurer la découverte d’ordinateurs, d’utilisateurs ou de groupes, commencez par ces étapes communes :

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie** et sélectionnez le nœud **Méthodes de découverte**.  

2.  Sélectionnez la méthode pour le site sur lequel vous voulez configurer la découverte.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4.  Dans l’onglet **Général**, cochez la case permettant d’activer la découverte. Vous pouvez aussi configurer la découverte maintenant et l’activer ultérieurement.  

Appuyez-vous ensuite sur les informations des sections suivantes pour configurer les méthodes de découverte spécifiques :  

- [Découverte de groupes Active Directory](#bkmk_config-adgd)  

- [Découverte de systèmes Active Directory](#bkmk_config-adgd)  

- [Découverte d’utilisateurs Active Directory](#bkmk_config-adud)  

> [!NOTE]  
>  Les informations dans cette section ne s’appliquent pas à la découverte de forêts Active Directory.  

 Bien qu’indépendantes, ces méthodes de découverte partagent des options similaires. Pour plus d’informations sur ces options de configuration, voir [Options partagées pour la découverte de groupes, de systèmes et d’utilisateurs](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_shared).  

> [!WARNING]  
>  Le processus d'interrogation Active Directory par chacune de ces méthodes de découverte peut entraîner un trafic réseau important. Pensez à planifier l’exécution de chaque méthode de découverte à des moments où ce trafic ne risque pas de nuire à l’usage commercial de votre réseau.  


### <a name="bkmk_config-adgd"></a>Configurer la découverte de groupes Active Directory  

1. Dans l’onglet **Général** de la fenêtre Propriétés de découverte de groupes Active Directory, sélectionnez **Ajouter** pour configurer une étendue de découverte. Sélectionnez **Groupes** ou **Emplacement**. Ensuite, terminez les configurations suivantes dans la boîte de dialogue **Ajouter des groupes** ou **Ajouter un emplacement Active Directory** :  

    1.  Spécifiez un **Nom** pour cette étendue de découverte.  

    2.  Spécifiez un **Domaine Active Directory** ou un **Emplacement** à rechercher :  

        -   Si vous avez choisi **Groupes**, spécifiez un ou plusieurs groupes Active Directory à découvrir.  

        -   Si vous avez choisi **Emplacement**, spécifiez un conteneur Active Directory comme emplacement à découvrir. Vous pouvez également activer une recherche récursive des conteneurs enfants Active Directory pour cet emplacement.  

    3.  Spécifiez le **Compte de découverte de groupes Active Directory** utilisé par le site pour rechercher dans cette étendue de découverte. Pour plus d’informations, voir [Comptes](/sccm/core/plan-design/hierarchy/accounts#active-directory-group-discovery-account).  

    4.  Sélectionnez **OK** pour enregistrer la configuration de l’étendue de découverte.  

2.  Répétez les étapes précédentes pour chaque étendue de découverte supplémentaire à définir.  

3.  Dans l'onglet **Calendrier d'interrogation** , configurez le calendrier d'interrogation de découverte complet et la découverte delta.  

4.  Dans l’onglet **Option**, configurez les paramètres de façon à filtrer ou à exclure de la découverte les enregistrements d’ordinateur obsolètes. Configurez également la découverte de l’appartenance des groupes de distribution.  

    > [!NOTE]  
    >  Par défaut, le processus de découverte de groupes Active Directory ne découvre que l'appartenance aux groupes de sécurité.  

5. Cliquez sur **OK** pour enregistrer la configuration.  


### <a name="bkmk_config-adsd"></a>Configurer la découverte de systèmes Active Directory  

1. Dans l’onglet **Général** de la fenêtre Propriétés de la découverte de systèmes Active Directory, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour spécifier un nouveau conteneur Active Directory. Dans la boîte de dialogue **Conteneur Active Directory**, finalisez les configurations suivantes :  

    1.  Tapez ou recherchez un emplacement pour le **Chemin d’accès**. Cette valeur est un chemin d’accès LDAP valide vers un conteneur ou une unité d’organisation (UO). Le site interroge ce chemin d’accès pour trouver les ressources. Par exemple, `LDAP://CN=Computers,DC=contoso,DC=com`  

    2.  Spécifiez des options qui modifient le comportement de recherche :  

        - **Découvrir des objets dans les groupes Active Directory** : Le site examine également l’appartenance aux groupes dans ce chemin d’accès.  

        - **Rechercher les conteneurs enfants Active Directory de manière récursive** : si cette option est activée, le site examine des conteneurs ou des unités d’organisation supplémentaires dans le chemin d’accès ci-dessus. Sinon, le site ne recherche des ressources que dans le chemin d’accès proprement dit.  

            Depuis la version 1806, vous pouvez sélectionner des sous-conteneurs à exclure de cette recherche récursive. Cette option permet de réduire le nombre d’objets découverts. Sélectionnez **Ajouter** pour choisir les conteneurs sous le chemin d’accès ci-dessus. Dans la boîte de dialogue Sélectionner un nouveau conteneur, sélectionnez un conteneur enfant à exclure. Sélectionnez **OK** pour fermer la boîte de dialogue Sélectionner un nouveau conteneur.<!--1358143-->

            > [!Tip]  
            > La liste des conteneurs Active Directory dans la fenêtre Propriétés de la découverte de systèmes Active Directory comporte une colonne **Comporte des exclusions**. Si vous sélectionnez des conteneurs à exclure, cette valeur est **Oui**.  

    3.  Pour chaque emplacement, spécifiez le compte à utiliser en tant que **Compte de découverte Active Directory**. Pour plus d’informations, voir [Comptes](/sccm/core/plan-design/hierarchy/accounts#active-directory-system-discovery-account).  

        > [!TIP]  
        >  Pour chaque emplacement spécifié, vous pouvez configurer un ensemble d’options de découverte et un compte de découverte Active Directory unique.  

    4.  Sélectionnez **OK** pour enregistrer la configuration des conteneurs Active Directory.  

2.  Dans l'onglet **Calendrier d'interrogation** , configurez le calendrier d'interrogation de découverte complet et la découverte delta.  

3.  Dans l’onglet **Attributs Active Directory**, configurez des attributs Active Directory supplémentaires pour les ordinateurs à découvrir. Cet onglet liste également les attributs d’objets par défaut.  

     > [!Tip]  
     > Par exemple, votre organisation utilise l’attribut **Description** sur le compte d’ordinateur dans Active Directory. Sélectionnez **Personnalisé** et ajoutez `Description` comme attribut personnalisé. Une fois que cette méthode de découverte s’exécute, cet attribut s’affiche sous l’onglet Propriétés de l’appareil dans la console Configuration Manager.<!--513948-->  

4.  Dans l’onglet **Option**, configurez les paramètres de façon à filtrer ou à exclure de la découverte les enregistrements d’ordinateur obsolètes.  

5. Cliquez sur **OK** pour enregistrer la configuration.  


### <a name="bkmk_config-adud"></a>Configurer la découverte d’utilisateurs Active Directory  

1.  Dans l’onglet **Général** de la fenêtre Propriétés de la découverte d’utilisateurs Active Directory, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour spécifier un nouveau conteneur Active Directory. Dans la boîte de dialogue **Conteneur Active Directory**, finalisez les configurations suivantes :  

    1.  Spécifiez un ou plusieurs emplacements à rechercher.  

    2.  Pour chaque emplacement, spécifiez les options qui modifient le comportement de la recherche.  

    3.  Pour chaque emplacement, spécifiez le compte à utiliser en tant que **Compte de découverte Active Directory**. Pour plus d’informations, voir [Comptes](/sccm/core/plan-design/hierarchy/accounts#active-directory-user-discovery-account).  

        > [!NOTE]  
        >  Pour chaque emplacement spécifié, vous pouvez configurer un ensemble d’options de découverte et un compte de découverte Active Directory uniques.  

    4.  Sélectionnez **OK** pour enregistrer la configuration des conteneurs Active Directory.  

6.  Dans l'onglet **Calendrier d'interrogation** , configurez le calendrier d'interrogation de découverte complet et la découverte delta.  

7.  Dans l’onglet **Attributs Active Directory**, configurez des attributs Active Directory supplémentaires pour les ordinateurs à découvrir. Cet onglet liste également les attributs d’objets par défaut.  

8.  Cliquez sur **OK** pour enregistrer la configuration.  



## <a name="azureaadisc"></a> Configurer la découverte des utilisateurs Azure AD

La découverte d’utilisateurs Azure AD n’est pas activée ni configurée de la même façon que d’autres méthodes de découverte. Configurez-la quand vous intégrez le site Configuration Manager à Azure AD. Quand vous [configurez les services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**, vous pouvez également activer et configurer cette méthode de découverte. 

Lors de la configuration du service Azure de **gestion cloud** : 
- Sur la page **Découverte** de l’Assistant, sélectionnez l’option **Activer la découverte d’utilisateurs Azure Active Directory**. 
- Sélectionnez **Paramètres**. 
- Dans la boîte de dialogue Paramètres de découverte d’utilisateurs Azure AD, configurez une planification pour déterminer quand la découverte survient. Vous pouvez également activer la découverte delta, qui vérifie uniquement les comptes nouveaux ou modifiés dans Azure AD. 

Pour plus d’informations, consultez [Découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 > [!Important]  
 > Avant *d’importer* l’application Azure AD dans Configuration Manager, vous devez accorder l’autorisation d’application serveur pour lire les données d’annuaire Azure AD. 
 >  - Dans le [portail Azure](https://portal.azure.com), accédez au panneau **Azure Active Directory**. 
 >  - Cliquez sur **Inscriptions d’applications**, puis basculez vers **Toutes les applications** si nécessaire. 
 >  - Sélectionnez l’application serveur de type *API/application web*, puis **Paramètres**. 
 >  - Sélectionnez **Autorisations nécessaires**, puis **Accorder des autorisations**.
 >  
 > Si vous *créez* l’application serveur à partir de Configuration Manager, Azure AD crée automatiquement les autorisations avec l’application. Vous devez néanmoins donner votre consentement à l’application dans le portail Azure.

 > [!Note]  
 > Si l’utilisateur est une identité fédérée ou synchronisée, vous devez utiliser la [découverte d’utilisateurs Active Directory](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) de Configuration Manager ainsi que la découverte d’utilisateurs Azure AD. Pour plus d’informations sur les identités hybrides, consultez [Définir une stratégie d’adoption des identités hybrides](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->



##  <a name="BKMK_ConfigHBDisc"></a> Configurer la découverte par pulsations d’inventaire  

Configuration Manager active la méthode de découverte par pulsations d’inventaire au moment de l’installation d’un site principal. Si vous souhaitez utiliser le calendrier par défaut (tous les sept jours), il n’y a rien d’autre à configurer. Sinon, vous ne devez configurer que la fréquence d’envoi par les clients de l’enregistrement de données de découverte par pulsations d’inventaire au point de gestion.  

> [!NOTE]  
>  Si vous activez à la fois l’installation Push du client et la tâche de maintenance de site **Effacer l’indicateur d’installation** sur le même site, définissez pour la découverte par pulsations d’inventaire une planification inférieure à la **Période de redécouverte client** de la tâche de maintenance de site **Effacer l’indicateur d’installation**. Pour plus d’informations sur les tâches de maintenance de site, voir [Tâches de maintenance](/sccm/core/servers/manage/maintenance-tasks).  


### <a name="configure-the-heartbeat-discovery-schedule"></a>Configurer la planification de la découverte par pulsations d’inventaire  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie** et sélectionnez le nœud **Méthodes de découverte**.  

2.  Sélectionnez la méthode **Découverte par pulsations d’inventaire** pour le site sur lequel vous souhaitez la configurer.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4.  Configurez la fréquence d’envoi par les clients d’un enregistrement de données de découverte par pulsations d’inventaire. Ensuite, sélectionnez **OK** pour enregistrer la configuration.  



<a name="BKMK_AboutConfigNetworkDisc"></a>

##  <a name="BKMK_ConfigNetworkDisc"></a> Configurer la découverte du réseau  

 Avant de configurer la découverte du réseau, familiarisez-vous avec les sujets suivants :  

-   Niveaux disponibles de découverte du réseau  

-   Options disponibles de découverte du réseau  

-   Limitation de la découverte du réseau sur le réseau  

Pour plus d’informations, consultez la section [Découverte du réseau](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutNetwork).  

Les sections suivantes fournissent des informations sur les configurations courantes pour la découverte du réseau. Vous pouvez configurer une ou plusieurs de ces configurations pour l'utilisation pendant la même exécution de la découverte. Si vous utilisez plusieurs configurations, tenez compte des interactions pouvant affecter les résultats de la découverte.  

Par exemple, vous découvrez tous les appareils SNMP (Simple Network Management Protocol) qui utilisent un certain nom de communauté SNMP. Vous désactivez la découverte sur un sous-réseau spécifique pour la même exécution de la découverte. Lors de l’exécution de la découverte, la découverte du réseau ne découvre pas les unités SNMP avec le nom de communauté spécifié sur le sous-réseau que vous avez désactivé.  


###  <a name="BKMK_DetermineNetTopology"></a> Déterminer la topologie de votre réseau  

 La découverte pour la topologie uniquement vous permet de mapper votre réseau. Ce type de découverte ne découvre pas les clients potentiels. La découverte du réseau pour la topologie uniquement s'appuie sur SNMP.  

 Lors du mappage de la topologie de réseau, configurez le **Nombre maximal de sauts** dans l’onglet **SNMP** de la boîte de dialogue **Propriétés de la découverte du réseau**. Quelques sauts permettent de contrôler la bande passante réseau utilisée lors de l’exécution de la découverte. À mesure que vous découvrez votre réseau, augmentez le nombre de sauts pour mieux comprendre votre topologie de réseau.  

 Une fois que vous avez compris votre topologie de réseau, configurez des propriétés supplémentaires pour la découverte du réseau. Elles permettent de découvrir des clients potentiels et leurs systèmes d’exploitation. Configurez également la découverte du réseau de façon à limiter les segments de réseau qu’elle peut examiner.  

 Pour plus d’informations, voir [Guide pratique pour déterminer la topologie de réseau](#bkmk_proc-top).


### <a name="network-discovery-search-options"></a>Options de recherche de la découverte du réseau

Configuration Manager prend en charge les méthodes de recherche sur le réseau suivantes :
- [Limiter les recherches à l’aide de sous-réseaux](#BKMK_LimitBySubnet)
- [Rechercher dans un domaine en particulier](#BKMK_SearchByDomain)
- [Limiter les recherches à l’aide de noms de communauté SNMP](#BKMK_LimitBySNMPname)
- [Rechercher sur un serveur DHCP en particulier](#BKMK_SearchByDHCP)

####  <a name="BKMK_LimitBySubnet"></a> Limiter les recherches en utilisant des sous-réseaux  

 Vous pouvez configurer la découverte du réseau pour rechercher des sous-réseaux spécifiques au cours d'une opération de découverte. Par défaut, la découverte du réseau recherche le sous-réseau du serveur qui exécute la découverte. Tous les sous-réseaux supplémentaires configurés et activés s’appliquent exclusivement aux options de recherche SNMP et DHCP. Quand la découverte du réseau effectue des recherches dans des domaines, elle n’est pas limitée par les configurations des sous-réseaux.  

 Si un ou plusieurs sous-réseaux sont spécifiés dans l’onglet **Sous-réseaux** de la boîte de dialogue **Propriétés de la découverte du réseau**, seuls les sous-réseaux marqués **Activé** sont examinés.  

 Lorsqu’un sous-réseau est désactivé, le site l’exclut de la découverte, et les conditions suivantes s’appliquent :  

-   Les requêtes SNMP ne s’exécutent pas sur le sous-réseau.  

-   Les serveurs DHCP ne renvoient pas la liste des ressources situées sur le sous-réseau.  

-   Les requêtes basées sur le domaine peuvent découvrir des ressources situées sur le sous-réseau.  


####  <a name="BKMK_SearchByDomain"></a> Rechercher dans un domaine spécifique  

 La découverte du réseau peut être configurée pour rechercher dans un domaine spécifique ou dans plusieurs domaines au cours d'une opération de découverte. Par défaut, la découverte du réseau recherche dans le domaine local du serveur qui exécute la découverte.  

 Si un ou plusieurs domaines sont spécifiés dans l’onglet **Domaines** de la boîte de dialogue **Propriétés de la découverte du réseau**, seuls les domaines marqués **Activé** sont examinés.  

 Lorsqu’un domaine est désactivé, le site l’exclut de la découverte, et les conditions suivantes s’appliquent :  

-   La découverte du réseau n’interroge pas les contrôleurs de domaine dans ce domaine.  

-   Les requêtes SNMP s’exécutent sur les sous-réseaux du domaine.  

-   Les serveurs DHCP renvoient toujours une liste des ressources situées dans le domaine.  


#### <a name="BKMK_LimitBySNMPname"></a> Limiter les recherches en utilisant des noms de communautés SNMP  

 La découverte du réseau peut être configurée pour rechercher une communauté SNMP spécifique ou plusieurs communautés au cours d'une opération de découverte. Par défaut, la méthode configure le nom de communauté **public**.  

 La fonction de découverte du réseau utilise des noms de communautés pour accéder à des routeurs qui constituent des périphériques SNMP. Un routeur permet d'informer le service de découverte du réseau sur les autres routeurs et les sous-réseaux liés au premier routeur.  

> [!NOTE]  
>  Les noms de communautés SNMP sont semblables aux mots de passe. Le service de découverte du réseau peut uniquement obtenir des informations d’une unité SNMP pour laquelle vous avez spécifié un nom de communauté. Chaque périphérique SNMP peut disposer de son propre nom de communauté mais souvent, plusieurs périphériques partagent le même nom de communauté. En outre, la plupart des périphériques SNMP disposent d'un nom de communauté par défaut dit **Public**. Toutefois, certaines organisations suppriment le nom de communauté **Public** de leurs appareils pour des raisons de sécurité.  

 Si plusieurs communautés SNMP sont présentes dans l’onglet **SNMP** de la boîte de dialogue **Propriétés de la découverte du réseau**, la recherche s’effectue dans l’ordre d’affichage. Mettez les noms les plus fréquents en haut de la liste. Cette configuration permet de réduire le trafic réseau généré par le site lorsqu’il tente de contacter un appareil par différents noms.

> [!NOTE]  
>  Outre le nom de communauté SNMP, vous pouvez spécifier l’adresse IP ou le nom pouvant être résolu d’une unité SNMP. Pour ce faire, utilisez l’onglet **Unités SNMP** de la boîte de dialogue **Propriétés de la découverte du réseau**.  


####  <a name="BKMK_SearchByDHCP"></a> Rechercher sur un serveur DHCP spécifique  

 La découverte du réseau peut être configurée pour utiliser un serveur DHCP spécifique ou plusieurs serveurs en vue de découvrir des clients DHCP au cours d'une opération de découverte.  

 La découverte du réseau recherche sur chaque serveur DHCP que vous spécifiez sous l'onglet **DHCP** de la boîte de dialogue **Propriétés de la découverte du réseau**. Si le serveur qui exécute la découverte loue son adresse IP à partir d’un serveur DHCP, vous pouvez configurer la découverte de façon à rechercher sur ce serveur DHCP. Activez ce comportement avec l’option **Inclure le serveur DHCP que le serveur de site est configuré pour utiliser**.  

> [!NOTE]  
>  Pour configurer avec succès un serveur DHCP dans la découverte du réseau, votre environnement doit prendre en charge IPv4. Vous ne pouvez pas configurer la découverte du réseau de sorte qu’elle utilise un serveur DHCP dans un environnement IPv6 natif.  


###  <a name="BKMK_HowToConfigNetDisc"></a> Guide pratique pour configurer la découverte du réseau  

 Procédez comme suit pour d'abord découvrir uniquement la topologie de votre réseau, puis configurer la découverte du réseau afin de découvrir des clients potentiels à l'aide de l'une ou de plusieurs options disponibles de découverte du réseau.  

#### <a name="bkmk_proc-top"></a>Identifier la topologie de réseau  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie** et sélectionnez le nœud **Méthodes de découverte**.  

2.  Sélectionnez la méthode **Découverte du réseau** pour le site sur lequel vous voulez découvrir des ressources réseau.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

    -   Dans l’onglet **Général**, sélectionnez l’option **Activer la découverte du réseau**. Ensuite, sélectionnez **Topologie** parmi les options **Type de découverte**.  

    -   Dans l’onglet **Sous-réseaux**, sélectionnez l’option **Rechercher dans les sous-réseaux locaux**.  

        > [!TIP]  
        >  Si vous connaissez les sous-réseaux qui constituent votre réseau, décochez la case **Rechercher dans les sous-réseaux locaux**. Ensuite, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) et ajoutez les sous-réseaux à examiner. Si le réseau est grand, restreignez la recherche à un ou deux sous-réseaux à la fois, afin de limiter l’utilisation de la bande passante réseau.  

    -   Dans l’onglet **Domaines**, sélectionnez l’option **Rechercher dans le domaine local**.  

    -   Dans l’onglet **SNMP**, sélectionnez une option dans la liste déroulante **Nombre maximal de sauts**. Cette option spécifie le nombre de sauts de routeur possibles pour la découverte du réseau lors du mappage de la topologie.  

        > [!TIP]  
        >  Lorsque vous mappez la topologie de votre réseau pour la première fois, configurez quelques sauts de routeur pour réduire l'utilisation de la bande passante du réseau.  

4.  Dans l’onglet **Calendrier**, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) et définissez un calendrier d’exécution de la découverte.  

    > [!NOTE]  
    >  Vous ne pouvez pas attribuer une configuration de découverte différente à des planifications de découverte du réseau distinctes. La découverte du réseau utilise la configuration de découverte en cours à chaque exécution.  

5.  Sélectionnez **OK** pour accepter les configurations. La découverte du réseau s'exécute à l'heure planifiée.  


#### <a name="bkmk_proc-config"></a> Guide pratique pour configurer la découverte du réseau  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration de la hiérarchie** et sélectionnez le nœud **Méthodes de découverte**.  

2.  Sélectionnez la méthode **Découverte du réseau** pour le site sur lequel vous voulez découvrir des ressources réseau.  

3.  Dans le groupe **Propriétés** de l’onglet **Accueil** du ruban, sélectionnez **Propriétés**.  

4.  Dans l’onglet **Général**, sélectionnez l’option **Activer la découverte du réseau**.  

    - Sélectionnez le type de découverte que vous souhaitez exécuter dans les options **Type de découverte**.  

    - Activez l’option **Réseau lent** afin que Configuration Manager effectue des ajustements automatiques pour les réseaux à faible bande passante.  

5.  Pour configurer la découverte de façon à rechercher dans les sous-réseaux, basculez vers l’onglet **Sous-réseaux**. Ensuite, configurez les options suivantes :  

    -   Pour lancer la découverte sur les sous-réseaux locaux de l’ordinateur exécutant la découverte, activez l’option **Rechercher dans les sous-réseaux locaux**.  

    -   Pour rechercher un sous-réseau spécifique, celui-ci doit figurer dans la liste **Sous-réseaux à rechercher** et son paramètre **Rechercher** doit avoir pour valeur **Activé** :  

        1.  Si le sous-réseau ne figure pas dans la liste, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouvelle attribution de sous-réseau**, renseignez les champs **Sous-réseau** et **Masque**, puis sélectionnez **OK**. Par défaut, un nouveau sous-réseau est activé pour la recherche.  

        2.  Pour modifier la valeur **Rechercher** d’un des sous-réseaux de la liste, sélectionnez-le. Ensuite, sélectionnez l’icône **Bascule** pour basculer la valeur entre **Désactivé** et **Activé**.  

6.  Pour configurer la découverte de façon à rechercher dans les domaines, basculez vers l’onglet **Domaines**. Ensuite, configurez les options suivantes :  

    -   Pour lancer la découverte sur le domaine de l’ordinateur exécutant la découverte, activez l’option **Rechercher dans le domaine local**.  

    -   Pour rechercher un domaine spécifique, vérifiez que celui-ci figure dans la liste **Domaines** et que son paramètre **Rechercher** a pour valeur **Activé** :  

        1.  Si le domaine ne figure pas dans la liste, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Propriétés de domaine**, renseignez le champ **Domaine**, puis sélectionnez **OK**. Par défaut, un nouveau domaine est activé pour la recherche.  

        2.  Pour modifier la valeur **Rechercher** d’un des domaines de la liste, sélectionnez-le. Ensuite, sélectionnez l’icône **Bascule** pour basculer la valeur entre **Désactivé** et **Activé**.  

7.  Pour configurer la découverte de façon à rechercher des appareils SNMP dans des noms de communauté SNMP en particulier, basculez vers l’onglet **SNMP**. Ensuite, configurez les options suivantes :  

    - Pour ajouter un nom de communauté SNMP à la liste **Noms de communauté SNMP**, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouveau nom de communauté SNMP**, spécifiez le **Nom** de la communauté SNMP, puis sélectionnez **OK**.  

    - Pour supprimer un nom de communauté SNMP, sélectionnez-le, puis sélectionnez l’icône **Supprimer** ![Icône Supprimer](media/Disc_delete_Icon.gif).  

    - Pour modifier l’ordre de recherche des noms de communauté SNMP, sélectionnez-en un dans la liste. Ensuite, sélectionnez l’icône **Déplacer l’élément vers le haut** ![Icône Déplacer vers le haut](media/Disc_moveUp_Icon.gif) ou l’icône **Déplacer l’élément vers le bas** ![Icône Déplacer vers le bas](media/Disc_moveDown_Icon.gif). Lors de l'exécution de la découverte, la recherche des noms de communauté est effectuée dans un ordre de haut en bas. 

    - Pour configurer le nombre maximal de sauts de routeur pour les recherches SNMP, sélectionnez-le dans la liste déroulante **Nombre maximal de sauts**.  

8. Pour configurer un appareil SNMP, basculez vers l’onglet **Appareils SNMP**. Si l’appareil ne figure pas dans la liste, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouvel appareil SNMP**, spécifiez l’adresse IP ou le nom de l’appareil SNMP, puis sélectionnez **OK**.  

    > [!NOTE]  
    >  Si vous spécifiez un nom de périphérique, Configuration Manager doit pouvoir résoudre le nom NetBIOS en adresse IP.  

9. Pour configurer la découverte de façon à interroger des serveurs DHCP en particulier, basculez vers l’onglet **DHCP**. Ensuite, configurez les options suivantes :  

    -   Pour interroger le serveur DHCP sur l’ordinateur exécutant la découverte, activez l’option **Toujours utiliser le serveur DHCP du serveur de site**.  

        > [!NOTE]  
        >  Pour utiliser cette option, le serveur doit louer son adresse IP à un serveur DHCP, et il ne peut pas utiliser une adresse IP statique.  

    -   Pour interroger un serveur DHCP en particulier, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif). Dans la boîte de dialogue **Nouveau serveur DHCP**, spécifiez l’adresse IP ou le nom du serveur DHCP, puis sélectionnez **OK**.  

        > [!NOTE]  
        >  Si vous spécifiez un nom de serveur, Configuration Manager doit pouvoir résoudre le nom NetBIOS en adresse IP.  

10. Pour configurer le calendrier d’exécution de la découverte, basculez vers l’onglet **Calendrier**. Ensuite, sélectionnez l’icône **Nouveau** ![Icône Nouveau](media/Disc_new_Icon.gif) pour définir un calendrier d’exécution de la découverte du réseau. Vous pouvez configurer plusieurs calendriers récurrents et plusieurs calendriers non récurrents.  

    > [!NOTE]  
    >  Si l’onglet **Calendrier** comporte plusieurs calendriers à la fois, la découverte du réseau s’exécute pour tous les calendriers suivant l’heure indiquée. Ce comportement s’applique également aux planifications périodiques.  

11. Sélectionnez **OK** pour enregistrer vos configurations.  


###  <a name="BKMK_HowToVerifyNetDisc"></a> Guide pratique pour vérifier que la découverte du réseau est terminée  

 La durée d’exécution de la découverte du réseau peut varier selon un ou plusieurs des facteurs suivants :  

-   Taille de votre réseau  

-   Topologie de votre réseau  

-   Nombre maximal de sauts configurés pour la recherche de routeurs sur le réseau  

-   Type de découverte en cours d'exécution  

La découverte du réseau ne crée pas de messages pour vous avertir lorsqu’elle est terminée. Utilisez la procédure suivante pour vérifier qu’elle est finie :  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**. Développez **État du système**, puis sélectionnez le nœud **Requêtes sur les messages d’état**.  

2.  Sélectionnez la requête **Tous les messages d’état**.  

3.  Dans le groupe **Requêtes sur les messages d’état** de l’onglet **Accueil** du ruban, sélectionnez **Afficher les messages**.  

4.  Dans la fenêtre Tous les messages d’état, sélectionnez dans la liste déroulante **Sélectionner la date et l’heure** une valeur qui précise le temps écoulé depuis le début de la découverte. Ensuite, sélectionnez **OK** pour ouvrir  **l’Afficheur des messages d’état de Configuration Manager**.  

    > [!TIP]  
    >  Vous pouvez également utiliser l'option **Spécifier la date et l'heure** pour sélectionner la date et l'heure auxquelles vous avez exécuté la découverte. Cette option s'avère utile si vous avez exécuté une découverte du réseau à une date donnée et que vous voulez récupérer uniquement les messages ayant été générés à cette date.  

5.  Pour valider que la découverte du réseau est terminée, recherchez un message d'état contenant les détails suivants :  

    -   ID de message : **502**  

    -   Composant : **SMS_NETWORK_DISCOVERY**  

    -   Description : **Ce composant s’est arrêté**  

    Si ce message d’état ne s’affiche pas, la découverte de réseau n’est pas terminée.  

7.  Pour valider le moment de démarrage de la découverte du réseau, recherchez un message d'état contenant les détails suivants :  

    -   ID de message : **500**  

    -   Composant : **SMS_NETWORK_DISCOVERY**  

    -   Description : **Ce composant a démarré**  

    Ces informations vérifient que la découverte du réseau a démarré. Si ces informations ne s’affichent pas, replanifiez une découverte du réseau.  
