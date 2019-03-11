---
title: Planifier le fournisseur SMS
titleSuffix: Configuration Manager
description: Découvrez-en plus sur le rôle de système de site du fournisseur SMS dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: aec16c4b55afd8c4baf7486794e07f29fa84aebf
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951832"
---
# <a name="plan-for-the-sms-provider"></a>Planifier le fournisseur SMS 

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour gérer Configuration Manager, vous devez utiliser une console Configuration Manager qui se connecte à une instance du **fournisseur SMS**. Par défaut, un fournisseur SMS est installé sur le serveur de site durant l’installation d’un site d’administration centrale ou d’un site principal. 



##  <a name="BKMK_PlanSMSProv"></a> À propos du fournisseur SMS  

Le fournisseur SMS est un fournisseur WMI (Windows Management Instrumentation) qui affecte un accès en **lecture** et en **écriture** à la base de données Configuration Manager d’un site.  

- Chaque site d’administration centrale et site principal doit posséder au moins un fournisseur SMS. Vous pouvez installer d’autres fournisseurs en fonction des besoins.  

- Le groupe de sécurité **Administrateurs SMS** fournit l’accès au fournisseur SMS. Configuration Manager crée automatiquement ce groupe sur le serveur de site et sur chaque ordinateur sur lequel vous installez une instance du fournisseur SMS. Pour plus d’informations, consultez [Administrateurs SMS](/sccm/core/plan-design/hierarchy/accounts#sms-admins).  

- Les sites secondaires ne prennent pas en charge le rôle de fournisseur SMS.  

Les utilisateurs administratifs de Configuration Manager utilisent un fournisseur SMS pour accéder aux informations stockées dans la base de données. Pour ce faire, les administrateurs peuvent utiliser la console Configuration Manager, l’Explorateur de ressources, des outils et des scripts personnalisés. Le fournisseur SMS n’interagit pas avec les clients Configuration Manager. Quand une console Configuration Manager se connecte à un site, elle interroge le service WMI sur le serveur de site pour localiser une instance du fournisseur SMS à utiliser.  

Le fournisseur SMS contribue à l’application de la sécurité de Configuration Manager. Il retourne uniquement les informations que l’utilisateur de la console est autorisé à voir.  

> [!IMPORTANT]  
>  Lorsque chaque instance du fournisseur SMS d’un site est hors connexion, les consoles Configuration Manager ne peuvent pas se connecter au site.  

 Pour plus d’informations sur la façon de gérer le fournisseur SMS, consultez [Gérer le fournisseur SMS](/sccm/core/servers/manage/modify-your-infrastructure#BKMK_ManageSMSprovider).  



## <a name="installation-prerequisites"></a>Conditions préalables d'installation  

 Pour prendre en charge le fournisseur SMS, le serveur cible doit satisfaire aux prérequis suivants :  

-   Dans le même domaine que les systèmes de site du serveur et de la base de données de site  

-   Il ne peut pas utiliser un rôle de système de site d’un autre site.  

-   Il ne peut pas déjà avoir un fournisseur SMS d’un autre site.  

-   Il doit exécuter une version de système d’exploitation prise en charge.  

-   Il doit disposer d’au moins 650 Mo d’espace disque libre pour prendre en charge les composants Windows ADK. Pour plus d’informations sur Windows ADK et le fournisseur SMS, consultez [Exigences du déploiement de système d’exploitation](#BKMK_WAIKforSMSProv).  



##  <a name="bkmk_location"></a> Emplacements  

Quand vous installez un site, le premier fournisseur SMS du site est installé automatiquement. Vous pouvez spécifier l'un des emplacements suivants pris en charge pour le fournisseur SMS :  

-   Serveur de site  

-   Serveur de bases de données du site  

-   Un autre serveur qui satisfait les [prérequis d’installation](#installation-prerequisites)  


Pour voir les emplacements de chaque fournisseur SMS d’un site : 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Sélectionnez le site souhaité dans la liste, puis choisissez **Propriétés** dans le ruban.  

3. Sous l’onglet **Général** des **Propriétés** du site, regardez le champ **Emplacement du fournisseur SMS**.    


Chaque fournisseur SMS prend en charge des connexions simultanées à partir de plusieurs demandes. Les seules limites sur ces connexions sont le nombre de connexions au serveur disponibles pour Windows et les ressources disponibles sur le serveur pour répondre aux demandes de connexion.  

Après avoir installé un site, vous pouvez réexécuter le programme d’installation de Configuration Manager sur le serveur de site. Utilisez le programme d’installation pour modifier l’emplacement d’un fournisseur SMS existant ou installer d’autres fournisseurs SMS sur ce site. Installez un seul fournisseur SMS sur un ordinateur. Un ordinateur ne peut pas héberger un fournisseur SMS depuis plusieurs sites.  


### <a name="choosing-a-location"></a>Choix d’un emplacement 

Les sections suivantes décrivent les avantages et inconvénients liés à l’installation d’un fournisseur SMS sur chaque emplacement pris en charge :  

#### <a name="configuration-manager-site-server"></a>Serveur de site Configuration Manager

- **Avantages :**  

    -   Le fournisseur SMS n’utilise pas les ressources système de l’ordinateur de base de données du site.  

    -   Cet emplacement peut fournir de meilleures performances qu'un fournisseur SMS situé sur un ordinateur autre que le serveur de site ou l'ordinateur de base de données du site.  

- **Inconvénients :**  

    -   Le fournisseur SMS utilise des ressources réseau et système qui pourraient être dédiées aux opérations du serveur de site.  


#### <a name="sql-server-that-hosts-the-site-database"></a>SQL Server qui héberge la base de données du site

- **Avantages :**  

    -   Le fournisseur SMS n’utilise pas les ressources système sur le serveur de site.  

    -   Parmi les trois emplacements, cet emplacement peut fournir les meilleures performances, si des ressources serveur suffisantes sont disponibles.  

- **Inconvénients :**  

    -   Le fournisseur SMS utilise des ressources réseau et système qui pourraient être dédiées aux opérations de la base de données de site.  

    -   Quand la base de données du site est hébergée sur une instance en cluster de SQL Server, vous ne pouvez pas utiliser cet emplacement.  


#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Ordinateur autre que le serveur de site ou le serveur de base de données de site

- **Avantages :**  

    -   Le fournisseur SMS n’utilise pas les ressources du serveur de site ou du système de base de données du site.  

    -   Ce type d'emplacement vous permet de déployer d'autres fournisseurs SMS afin de fournir une haute disponibilité pour les connexions.  

- **Inconvénients :**  

    -   Les performances du fournisseur SMS peuvent être réduites. Ce comportement est dû à l’activité réseau supplémentaire dont il a besoin pour se coordonner avec le serveur de site et l’ordinateur de base de données du site.  

    -   Le serveur de bases de données du site et tous les ordinateurs sur lesquels la console Configuration Manager est installée doivent toujours pouvoir accéder à ce serveur.  

    -   Cet emplacement peut utiliser les ressources système qui, dans le cas contraire, seraient dédiées à d'autres services.  



## <a name="bkmk_auth"></a> Authentification
<!--1357013-->

Depuis la version 1810, vous pouvez spécifier le niveau d’authentification minimal pour les administrateurs qui accèdent aux sites Configuration Manager. Cette fonctionnalité force les administrateurs à se connecter à Windows avec le niveau requis. Cela s’applique à tous les composants qui accèdent au fournisseur SMS. Par exemple, la console Configuration Manager, les méthodes SDK et les cmdlets Windows PowerShell. 


### <a name="configure-authentication"></a>Configurer l’authentification

Pour configurer ce paramètre, connectez-vous d’abord à Windows avec le niveau d’authentification souhaité. 

> [!Important]  
> Cette configuration est un paramètre à l’échelle de la hiérarchie. Avant de modifier ce paramètre, assurez-vous que tous les administrateurs Configuration Manager peuvent se connecter à Windows avec le niveau d’authentification requis. 

Pour configurer ce paramètre, utilisez les étapes suivantes :

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Sélectionnez **Paramètres de hiérarchie** dans le ruban.  

3. Basculez vers l’onglet **Authentification**. Sélectionnez le [niveau d’authentification](#authentication-levels) souhaité, puis sélectionnez **OK**.  

    - Uniquement lorsque cela est nécessaire, sélectionnez **Ajouter** pour exclure des utilisateurs ou groupes spécifiques. Pour plus d’informations, consultez [Exclusions](#exclusions).  


### <a name="authentication-levels"></a>Niveaux d’authentification

Les niveaux ci-dessous sont disponibles :

- **Authentification Windows** : exige une authentification avec les informations d’identification du domaine Active Directory. Ce paramètre correspond au comportement précédent et constitue le paramètre par défaut actuel. Lorsque vous mettez à jour le site, le niveau d’authentification n’est pas modifié.  

- **Authentification par certificat** : exige l’authentification avec un certificat valide émis par une autorité de certification PKI approuvée. Vous ne configurez pas ce certificat dans Configuration Manager. Configuration Manager requiert que l’administrateur soit connecté à Windows à l’aide de PKI.  

- **Authentification Windows Hello Entreprise** : exige une authentification forte à deux facteurs liée à un appareil et utilisant la biométrie ou un code PIN. Pour plus d’informations, consultez [Windows Hello Entreprise](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).   


### <a name="exclusions"></a>Exclusions

Dans l’onglet **Authentification** de Paramètres de la hiérarchie, vous pouvez également exclure certains utilisateurs ou groupes. Utilisez cette option à bon escient. Par exemple, lorsque des utilisateurs spécifiques requièrent l’accès à la console Configuration Manager, mais ne peuvent pas s’authentifier auprès de Windows avec le niveau requis. Cela peut également s’avérer nécessaire pour l’automatisation ou les services qui s’exécutent dans le contexte d’un compte système.



##  <a name="BKMK_SMSProvLanguages"></a> À propos des langues du fournisseur SMS  

Le fournisseur SMS fonctionne indépendamment de la langue d’affichage du serveur sur lequel vous l’installez.  

Quand un utilisateur administratif ou un processus Configuration Manager sollicite des données à l’aide du fournisseur SMS, ce dernier tente de retourner les données dans un format correspondant à la langue du système d’exploitation de l’ordinateur émetteur de la requête.

La méthode utilisée pour tenter de déterminer la langue est indirecte. Le fournisseur SMS ne traduit pas les informations d’une langue à l’autre. Quand les données sont retournées pour être affichées dans la console Configuration Manager, leur langue d’affichage varie en fonction de la source de l’objet et du type de stockage.  

Lorsque Configuration Manager stocke les données d’un objet dans la base de données, les langues disponibles varient selon les facteurs suivants :  

-   Configuration Manager stocke les objets qu’il crée à l’aide de la prise en charge de plusieurs langues. L’objet est stocké dans la base de données du site en utilisant les langues que vous configurez pour le site lorsque vous exécutez le programme d’installation. La console Configuration Manager affiche ces objets dans la langue d’affichage de l’ordinateur qui émet la requête, quand cette langue est disponible pour l’objet. Si la console ne peut pas afficher l’objet dans la langue d’affichage de l’ordinateur qui émet la requête, elle l’affiche dans la langue par défaut, à savoir l’anglais.  

-   Configuration Manager stocke les objets créés par un utilisateur administratif en utilisant la langue qui a été utilisée pour créer ces objets. Ces objets s’affichent dans la console Configuration Manager dans la même langue. Le fournisseur SMS ne peut pas les traduire et ils n’ont pas plusieurs options de langue.  



##  <a name="BKMK_MultiSMSProv"></a> Utiliser plusieurs fournisseurs SMS  

 Après l'installation d'un site, vous pouvez installer des fournisseurs SMS supplémentaires pour ce site. Pour installer d’autres fournisseurs SMS, exécutez le programme d’installation de Configuration Manager sur le serveur de site. 

Envisagez d’installer d’autres fournisseurs SMS lorsque l’une des affirmations suivantes est vraie :  

- Un grand nombre d’utilisateurs administratifs ont besoin d’utiliser la console Configuration Manager et de se connecter à un site en même temps.  

- Vous utilisez le SDK Configuration Manager, ou d’autres produits, qui peuvent générer des appels fréquents au fournisseur SMS.  

- Votre activité exige une haute disponibilité du fournisseur SMS.  

Quand vous installez plusieurs fournisseurs SMS sur un site et qu’une demande de connexion est effectuée, le site attribue de façon aléatoire à chaque nouvelle demande de connexion l’utilisation d’un fournisseur SMS installé. Vous ne pouvez pas spécifier le fournisseur SMS à utiliser avec une session de connexion spécifique.  

> [!NOTE]  
>  Tenez compte des avantages et des inconvénients de chaque emplacement du fournisseur SMS. Pour plus d’informations, consultez [Emplacements](#bkmk_location). Trouvez un équilibre entre ces considérations et le fait que vous ne pouvez pas contrôler le fournisseur SMS qui est utilisé pour chaque nouvelle connexion.  

Lorsque vous connectez pour la première fois une console Configuration Manager à un site, la connexion interroge WMI sur le serveur de site. Cette requête identifie une instance du fournisseur SMS que la console utilise. Cette instance spécifique du fournisseur SMS continue à être utilisée par la console jusqu’à ce que la session se termine. Si la session se termine parce que le serveur du fournisseur SMS n’est pas disponible sur le réseau, la requête initiale est répétée quand vous reconnectez la console au site. Il est possible que le site attribue la même instance du fournisseur SMS qui n’est pas disponible. Si ce comportement se produit, tentez de reconnecter la console jusqu’à ce que le site retourne un fournisseur SMS disponible.  



##  <a name="BKMK_SMSProvNamespace"></a> À propos de l’espace de noms du fournisseur SMS  

Le schéma WMI de Configuration Manager définit la structure du fournisseur SMS. Les espaces de noms du schéma décrivent l’emplacement des données Configuration Manager dans le schéma du fournisseur SMS. Le tableau ci-dessous contient certains des espaces de noms communs que le fournisseur SMS utilise :  

|Espace de noms|Description|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Fournisseur SMS, qui est utilisé de façon intensive par la console Configuration Manager, l’Explorateur de ressources, les outils Configuration Manager et les scripts.|  
|`Root\SMS\SMS_ProviderLocation`|Emplacement des ordinateurs du fournisseur SMS pour un site.|  
|`Root\CIMv2`|Emplacement inventorié pour des informations d’espaces de noms WMI au cours de l’inventaire matériel et logiciel.|  
|`Root\CCM`|Stratégies de configuration et données du client Configuration Manager.|  
|`Root\CIMv2\SMS`|Emplacement des classes de rapports d’inventaire que l’Agent du client d’inventaire collecte. Les clients compilent ces paramètres lors de l’évaluation de la stratégie de l’ordinateur. Ces paramètres se basent sur la configuration des paramètres du client de l’ordinateur.|  



##  <a name="BKMK_WAIKforSMSProv"></a> Exigences du déploiement de système d’exploitation

L’ordinateur où vous installez une instance du fournisseur SMS requiert une version prise en charge de Windows ADK.  

Pour plus d’informations sur cette exigence, consultez [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](/sccm/osd/plan-design/infrastructure-requirements-for-operating-system-deployment#windows-adk-for-windows-10) et [Prise en charge de Windows 10](/sccm/core/plan-design/configs/support-for-windows-10).  

Quand vous gérez des déploiements de système d’exploitation, Windows ADK permet au fournisseur SMS d’effectuer diverses tâches, notamment :  

-   Afficher les informations du fichier WIM  

-   Ajouter des fichiers de pilote aux images de démarrage existantes  

-   Créer des fichiers ISO de démarrage  


L’installation du kit Windows ADK peut nécessiter jusqu’à 650 Mo d’espace disque libre sur chaque ordinateur où le fournisseur SMS est installé. Cet espace disque élevé est nécessaire pour permettre à Configuration Manager d’installer les images de démarrage Windows PE.  
