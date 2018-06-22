---
title: Planifier le fournisseur SMS
titleSuffix: Configuration Manager
description: Découvrez comment le fournisseur SMS vous permet de gérer System Center Configuration Manager.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9807bab4a5edd60ebc8a4aaa000cea6b8c25afb0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32341030"
---
# <a name="plan-for-the-sms-provider-for-system-center-configuration-manager"></a>Planifier le fournisseur SMS pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour gérer System Center Configuration Manager, vous devez utiliser une console Configuration Manager qui se connecte à une instance du **fournisseur SMS**. Par défaut, un fournisseur SMS est installé sur le serveur de site durant l’installation d’un site d’administration centrale ou d’un site principal. 


##  <a name="BKMK_PlanSMSProv"></a> À propos du fournisseur SMS  
 Le fournisseur SMS est un fournisseur WMI (Windows Management Instrumentation) qui affecte un accès en **lecture** et en **écriture** à la base de données Configuration Manager d’un site :  

-   Chaque site d’administration centrale et site principal doit posséder au moins un fournisseur SMS. Vous pouvez installer d’autres fournisseurs en fonction des besoins.  
-   Le groupe de sécurité **Administrateurs SMS** fournit l’accès au fournisseur SMS. Configuration Manager crée automatiquement ce groupe sur le serveur de site et sur chaque ordinateur sur lequel vous installez une instance du fournisseur SMS.  

-   Les sites secondaires ne prennent pas en charge le fournisseur SMS.  


Les utilisateurs administratifs de Configuration Manager utilisent un fournisseur SMS pour accéder aux informations stockées dans la base de données. Pour ce faire, les administrateurs peuvent utiliser la console Configuration Manager, l’Explorateur de ressources, des outils et des scripts personnalisés. Le fournisseur SMS n’interagit pas avec les clients Configuration Manager. Quand une console Configuration Manager se connecte à un site, la console Configuration Manager interroge le service WMI sur le serveur de site pour localiser une instance du fournisseur SMS à utiliser.  

 Le fournisseur SMS contribue à l’application de la sécurité de Configuration Manager. Il retourne uniquement les informations que l’utilisateur administratif qui exécute la console Configuration Manager est autorisé à afficher.  

> [!IMPORTANT]  
>  Quand chaque ordinateur qui héberge un fournisseur SMS pour un site est hors connexion, les consoles Configuration Manager ne peuvent pas se connecter à la base de données de ce site.  

 Pour plus d’informations sur la façon de gérer le fournisseur SMS, consultez [Gérer le fournisseur SMS](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider) dans [Modifier votre infrastructure System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  

## <a name="prerequisites-to-install-the-sms-provider"></a>Prérequis à l’installation du fournisseur SMS  

 Pour prendre en charge le fournisseur SMS :  

-   L’ordinateur doit être dans un domaine qui entretient une relation d’approbation bidirectionnelle avec le serveur de site et les systèmes de site de base de données du site.  

-   L'ordinateur ne peut pas disposer d'un rôle de système de site à partir d'un autre site.  

-   L'ordinateur ne peut pas disposer d'un fournisseur SMS à partir de n'importe quel site.  

-   L'ordinateur doit exécuter un système d'exploitation pris en charge pour un serveur de site.  

-   L’ordinateur doit disposer d’au moins 650 Mo d’espace disque libre pour prendre en charge les composants du kit de déploiement automatisé Windows (Windows ADK) qui sont installés avec le fournisseur SMS. Pour plus d’informations sur le kit Windows ADK et sur le fournisseur SMS, consultez [Configuration de déploiement de système d’exploitation requise pour le fournisseur SMS](#BKMK_WAIKforSMSProv) dans cette rubrique.  

##  <a name="bkmk_location"></a> Emplacements des fournisseurs SMS  
 Quand vous installez un site, le premier fournisseur SMS du site est installé automatiquement. Vous pouvez spécifier l'un des emplacements suivants pris en charge pour le fournisseur SMS :  

-   L'ordinateur de serveur de site  

-   L'ordinateur de base de données du site  

-   Un ordinateur de classe serveur qui ne possède pas de fournisseur SMS, ou un rôle de système de site à partir d'un autre site  


Pour afficher les emplacements de chaque fournisseur SMS installé sur un site, sélectionnez l’onglet **Général** de la boîte de dialogue **Propriétés** du site.  

 Chaque fournisseur SMS prend en charge des connexions simultanées à partir de plusieurs demandes. Les seules limites sur ces connexions sont le nombre de connexions au serveur qui sont disponibles sur l'ordinateur du fournisseur SMS et les ressources disponibles sur l'ordinateur du fournisseur SMS pour répondre aux demandes de connexion.  

 Après avoir installé un site, vous pouvez procéder à nouveau à l'installation sur le serveur de site pour modifier l'emplacement d'un fournisseur SMS existant ou pour installer d'autres fournisseurs SMS sur ce site. Vous pouvez installer un seul fournisseur SMS sur un ordinateur et un ordinateur ne peut pas installer un fournisseur SMS à partir de plusieurs sites.  

 Utilisez la section suivante pour identifier les avantages et inconvénients liés à l’installation d’un fournisseur SMS sur chaque emplacement pris en charge :  

 **Serveur de site Configuration Manager**  

-   **Avantages :**  

    -   Le fournisseur SMS n'utilise pas les ressources système de l'ordinateur de base de données du site.  

    -   Cet emplacement peut fournir de meilleures performances qu'un fournisseur SMS situé sur un ordinateur autre que le serveur de site ou l'ordinateur de base de données du site.  

-   **Inconvénients :**  

    -   Le fournisseur SMS utilise des ressources réseau et système qui pourraient être dédiées aux opérations du serveur de site.  


**SQL Server qui héberge la base de données du site**  

-   **Avantages :**  

    -   Le fournisseur SMS n'utilise pas les ressources du système de site sur le serveur de site.  

    -   Parmi les trois emplacements, cet emplacement peut fournir les meilleures performances, si des ressources serveur suffisantes sont disponibles.  

-   **Inconvénients :**  

    -   Le fournisseur SMS utilise des ressources réseau et système qui pourraient être dédiées aux opérations de la base de données de site.  

    -   Quand la base de données du site est hébergée sur une instance en cluster de SQL Server, vous ne pouvez pas utiliser cet emplacement.  


**Ordinateur autre que le serveur de site ou l'ordinateur de base de données du site**  

-   **Avantages :**  

    -   Le fournisseur SMS n'utilise pas le serveur de site ou les ressources informatiques de base de données du site.  

    -   Ce type d'emplacement vous permet de déployer d'autres fournisseurs SMS afin de fournir une haute disponibilité pour les connexions.  

-   **Inconvénients :**  

    -   Les performances du fournisseur SMS peuvent être réduites en raison de l’augmentation de l’activité réseau nécessaire à sa coordination avec le serveur de site et l’ordinateur de base de données du site.  

    -   L’ordinateur de la base de données du site et tous les ordinateurs sur lesquels la console Configuration Manager est installée doivent toujours pouvoir accéder à ce serveur.  

    -   Cet emplacement peut utiliser les ressources système qui, dans le cas contraire, seraient dédiées à d'autres services.  

##  <a name="BKMK_SMSProvLanguages"></a> À propos des langues du fournisseur SMS  
 Le fournisseur SMS fonctionne indépendamment de la langue d'affichage de l'ordinateur sur lequel il est installé.  

 Quand un utilisateur administratif ou un processus Configuration Manager sollicite des données à l’aide du fournisseur SMS, ce dernier tente de retourner les données dans un format correspondant à la langue du système d’exploitation de l’ordinateur émetteur de la requête.

La méthode utilisée pour tenter de déterminer la langue est indirecte. Le fournisseur SMS ne traduit pas les informations d'une langue à l'autre. À la place, quand les données sont retournées pour être affichées dans la console Configuration Manager, leur langue d’affichage varie en fonction de la source de l’objet et du type de stockage.  

 Lorsque les données d'un objet sont stockées dans la base de données, les langues qui seront disponibles dépendent des éléments suivants :  

-   Les objets créés par Configuration Manager sont stockés dans la base de données via la prise en charge de plusieurs langues. L'objet est stocké à l'aide des langues qui sont configurées sur le site sur lequel l'objet est créé lorsque vous procédez à l'installation. Ces objets sont affichés dans la console Configuration Manager dans la langue d’affichage de l’ordinateur qui émet la requête, quand cette langue est disponible pour l’objet. Si l'objet ne peut pas être affiché dans la langue d'affichage de l'ordinateur qui émet la demande, il est affiché dans la langue par défaut, à savoir l'anglais.  

-   Les objets créés par un utilisateur administratif sont stockés dans la base de données à l'aide de la langue utilisée pour créer l'objet. Ces objets s’affichent dans la console Configuration Manager dans la même langue. Ils ne peuvent pas être traduits par le fournisseur SMS et ne possèdent pas plusieurs options de langue.  

##  <a name="BKMK_MultiSMSProv"></a> Utiliser plusieurs fournisseurs SMS  
 Après l'installation d'un site, vous pouvez installer des fournisseurs SMS supplémentaires pour ce site. Pour installer des fournisseurs SMS supplémentaires, exécutez le programme d’installation de Configuration Manager sur le serveur de site. Envisagez l'installation de fournisseurs SMS supplémentaires lorsque l'une des affirmations suivantes est vraie :  

-   Un grand nombre d’utilisateurs administratifs exécutent une console Configuration Manager et se connectent à un site en même temps.  

-   Vous comptez utiliser le SDK Configuration Manager, ou d’autres produits, qui peuvent générer des appels fréquents au fournisseur SMS.  

-   Vous voulez garantir une haute disponibilité pour le fournisseur SMS.  


Quand plusieurs fournisseurs SMS sont installés sur un site et qu’une demande de connexion est effectuée, le site attribue de façon aléatoire à chaque nouvelle demande de connexion l’utilisation d’un fournisseur SMS installé. Vous ne pouvez pas spécifier l'emplacement du fournisseur SMS à utiliser avec une session de connexion spécifique.  

> [!NOTE]  
>  Tenez compte des avantages et des inconvénients de chaque emplacement du fournisseur SMS. Trouvez un équilibre entre ces considérations et le fait que vous ne pouvez pas contrôler le fournisseur SMS qui est utilisé pour chaque nouvelle connexion.  

Par exemple, quand vous connectez une console Configuration Manager à un site pour la première fois, la connexion interroge le service WMI sur le serveur de site pour identifier l’instance du fournisseur SMS à utiliser. Cette instance spécifique du fournisseur SMS reste utilisée par la console Configuration Manager jusqu’à la fin de sa session. Si la session prend fin car l’ordinateur du fournisseur SMS n’est plus disponible sur le réseau, quand vous reconnectez la console Configuration Manager, le site répète simplement la tâche d’identification d’une instance du fournisseur SMS à laquelle se connecter. Il est possible que le même ordinateur du fournisseur SMS non disponible soit attribué. Si cela se produit, vous pouvez tenter de reconnecter la console Configuration Manager jusqu’à ce qu’un ordinateur du fournisseur SMS disponible soit affecté.  

##  <a name="BKMK_AboutSMSAdmins"></a> À propos du groupe Administrateurs SMS  
 Le groupe Administrateurs SMS permet de fournir aux utilisateurs administratifs l'accès au fournisseur SMS. Le groupe est créé automatiquement sur le serveur de site au moment de l'installation du site, et sur chaque ordinateur qui installe un fournisseur SMS. Informations supplémentaires concernant le groupe Administrateurs SMS :  

-   Lorsque l'ordinateur est un serveur membre, le groupe Administrateurs SMS est créé en tant que groupe local.  

-   Lorsque l'ordinateur est un contrôleur de domaine, le groupe Administrateurs SMS est créé en tant que groupe de domaine local.  

-   Lorsque le fournisseur SMS est désinstallé d'un ordinateur, le groupe Administrateurs SMS n'est pas supprimé de l'ordinateur.  


Avant qu'un utilisateur puisse établir une connexion correcte à un fournisseur SMS, son compte d'utilisateur doit être un membre du groupe Administrateurs SMS. Chaque utilisateur administratif que vous configurez dans la console Configuration Manager est automatiquement ajouté au groupe Administrateurs SMS sur chaque serveur de site et chaque ordinateur du fournisseur SMS de la hiérarchie. Quand vous supprimez un utilisateur administratif de la console Configuration Manager, cet utilisateur est supprimé du groupe Administrateurs SMS sur chaque serveur de site et chaque ordinateur du fournisseur SMS de la hiérarchie.  

Une fois la connexion au fournisseur SMS réussie, l’administration basée sur des rôles permet de déterminer les ressources Configuration Manager auxquelles cet utilisateur peut accéder ou qu’il peut gérer.  

Vous pouvez afficher et configurer les autorisations et les droits du groupe Administrateurs SMS à l'aide du composant logiciel enfichable MMC Contrôle WMI. Par défaut, **Tout le monde** dispose des autorisations **Méthodes d'exécution**, **Écriture fournisseur**et **Activer le compte** . Une fois connecté au fournisseur SMS, l’utilisateur se voit accorder l’accès aux données dans la base de données du site en fonction des droits de sécurité d’administration basée sur des rôles définis dans la console Configuration Manager. Les autorisations **Activer le compte**  et **Appel à distance autorisé** sont accordées explicitement au groupe Administrateurs SMS dans l’espace de noms **Root\SMS**.  

> [!NOTE]  
>  Chaque utilisateur administratif qui utilise une console Configuration Manager distante doit avoir des autorisations DCOM d’activation à distance à la fois sur le serveur de site et sur l’ordinateur du fournisseur SMS. Même si ces droits peuvent être accordés à des utilisateurs ou des groupes, il est conseillé de les accorder au groupe Administrateurs SMS pour simplifier l’administration. Pour plus d'informations, consultez la section [Configurer les autorisations DCOM pour les consoles Configuration Manager distantes](../../../core/servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole) dans la rubrique [Modifier votre infrastructure System Center Configuration Manager](../../../core/servers/manage/modify-your-infrastructure.md).  


##  <a name="BKMK_SMSProvNamespace"></a> À propos de l’espace de noms du fournisseur SMS  
La structure du fournisseur SMS est définie par le schéma WMI. Les espaces de noms du schéma décrivent l’emplacement des données Configuration Manager dans le schéma du fournisseur SMS. Le tableau ci-dessous contient certains des espaces de noms communs utilisés par le fournisseur SMS.  

|Espace de noms|Description|  
|---------------|-----------------|  
|Root\SMS\site_*&lt;code de site\>*|Fournisseur SMS, qui est utilisé de façon intensive par la console Configuration Manager, l’Explorateur de ressources, les outils Configuration Manager et les scripts.|  
|Root\SMS\SMS_ProviderLocation|Emplacement des ordinateurs du fournisseur SMS pour un site.|  
|Root\CIMv2|Emplacement inventorié pour des informations d’espaces de noms WMI au cours de l’inventaire matériel et logiciel.|  
|Root\CCM|Stratégies de configuration et données du client Configuration Manager.|  
|root\CIMv2\SMS|Emplacement des classes de rapports d’inventaire collectées par l’Agent du client d’inventaire. Ces paramètres compilés par des clients au cours de l’évaluation des stratégies de l’ordinateur sont basés sur la configuration des paramètres du client de l’ordinateur.|  

##  <a name="BKMK_WAIKforSMSProv"></a> Exigences liées au déploiement de système d’exploitation pour le fournisseur SMS  
L’ordinateur sur lequel vous installez une instance du fournisseur SMS doit disposer de la version du Windows ADK exigée par la version de Configuration Manager que vous utilisez.  

 -   Par exemple, la version 1511 de Configuration Manager exige la version Windows 10 RTM (10.0.10240) du Windows ADK.  

 -   Pour plus d’informations sur cette configuration requise, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment).  

Quand vous gérez des déploiements de système d’exploitation, le Windows ADK permet au fournisseur SMS d’effectuer diverses tâches, notamment :  

-   Afficher les informations du fichier WIM.  

-   Ajouter des fichiers de pilote aux images de démarrage existantes.  

-   Créer des fichiers .ISO de démarrage.  


L’installation du kit Windows ADK peut nécessiter jusqu’à 650 Mo d’espace disque libre sur chaque ordinateur où le fournisseur SMS est installé. Cet espace disque élevé est nécessaire pour permettre à Configuration Manager d’installer les images de démarrage Windows PE.  
