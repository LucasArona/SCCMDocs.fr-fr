---
title: Capacités de la version Technical Preview 1701
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans Technical Preview 1701 System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 18598eaa-1131-44ff-8f8b-6093e87ac7a1
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 894d268151f9c9dfb05ded812eb642f8025dc459
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1701-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1701 System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*



Cet article présente les fonctionnalités qui sont disponibles dans Technical Preview 1701 System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.    


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

## <a name="boundary-groups-improvements-for-software-update-points"></a>Améliorations des groupes de limites pour les points de mise à jour logicielle
À compter de cette préversion, vous pouvez utiliser les groupes de limites pour associer les clients à des points de mise à jour logicielle. Ce changement intervient dans le cadre des travaux en cours destinés à modifier les groupes de limites de manière à ce qu’ils puissent gérer davantage de rôles de système de site.  Les premières modifications des groupes de limites sont apparues dans Technical Preview 1609 et dans la version Current Branch de Technical Preview 1610.  

Avec cette préversion, vous pouvez désormais utiliser le nouveau comportement des groupes de limites pour gérer les points de mise à jour logicielle qu’un client peut utiliser, de la même manière dont vous gérez les points de distribution qu’un client peut utiliser :  

- Vous configurez des groupes de limites pour associer un ou plusieurs serveurs qui hébergent un point de mise à jour logicielle.
- Les clients qui recherchent un nouveau point de mise à jour logicielle tentent d’utiliser celui qui est associé à leur groupe de limites actuel.
- Lorsqu’un client ne parvient pas à contacter le point de mise à jour logicielle auquel il est associé, ni à trouver un autre point appartenant à son groupe de limites actuel, il utilise le comportement de secours afin d’élargir le pool des points de mise à jour logicielle qu’il peut utiliser.    

Pour plus d’informations sur les groupes de limites, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups) dans le contenu concernant la version Current Branch.

Toutefois, avec cette préversion, les groupes de limites des points de mise à jour logicielle ne sont que partiellement implémentés. Vous pouvez ajouter des points de mise à jour logicielle et configurer des groupes de limites voisins contenant des points de mise à jour logicielle. Cependant, étant donné qu’il n’est pas encore possible de définir un délai avant utilisation du comportement de secours pour les points de mise à jour logicielle, les clients attendent deux heures avant de lancer le comportement de secours.

Les points suivants décrivent le comportement des points de mise à jour logicielle dans cette préversion :  

-   **Les nouveaux clients utilisent des groupes de limites pour sélectionner des points de mise à jour logicielle**. Si vous installez un client après avoir installé la version 1701, celui-ci sélectionnera l’un des points de mise à jour logicielle associés à son groupe de limites.

  Ce comportement vient remplacer celui qui consistait, pour les clients, à sélectionner un point de mise à jour logicielle de manière aléatoire dans la liste des points partageant la même forêt de clients.   

-   **Les clients déjà installés continuent d’utiliser leur point de mise à jour logicielle actuel jusqu’à ce qu’ils en recherchent un nouveau une fois le comportement de secours lancé.**
Les clients déjà installés qui disposent déjà d’un point de mise à jour logicielle continueront d’utiliser ce point jusqu’à ce que le comportement de secours soit lancé. Cela comprend les points de mise à jour logicielle qui ne sont pas associés au groupe de limites actuel du client. Ils ne tentent pas immédiatement de rechercher et d’utiliser un point de mise à jour logicielle appartenant à leur groupe de limites actuel.

  Un client qui dispose déjà d’un point de mise à jour logicielle ne commencera à utiliser ce nouveau comportement de groupe de limites qu’après avoir échoué à contacter son point de mise à jour logicielle actuel et lancé le comportement de secours.
Le délai de basculement vers le nouveau comportement est voulu. En effet, le changement de point de mise à jour logicielle peut entraîner une utilisation importante de la bande passante, car le client synchronise ses données avec le nouveau point de mise à jour logicielle. Ce délai se révèle donc utile. Le délai de transition peut permettre d’éviter la saturation du réseau, si tous vos clients devaient basculer vers le nouveau point de mise à jour logicielle en même temps.

-   **Configuration du délai de basculement vers le comportement de secours**. Cette préversion ne permet pas de configurer quand les clients peuvent commencer à basculer vers le comportement de secours et rechercher un nouveau point de mise à jour logicielle. Elle comprend les options **Durées du secours (en minutes)** et **Ne jamais activer le secours**, que vous pouvez configurer pour différentes relations de groupes de limites.

  Au lieu de cela, les clients conservent leur comportement actuel qui consiste à tenter de se connecter à leur point de mise à jour logicielle actuel pendant deux heures, avant de basculer vers le comportement de secours pour rechercher un nouveau point de mise à jour logicielle.

  Lorsqu’un client bascule vers le comportement de secours, il utilise les configurations du groupe de limites relatives au comportement de secours, afin de créer un pool de points de mise à jour logicielle disponibles. Cette liste comprend tous les points de mise à jour logicielle des clients provenant du *groupe de limites actuel*, des *groupes de limites voisins* et du *groupe de limites de site par défaut*.

- **Configurer le groupe de limites de site par défaut :**  
 Ajoutez un point de mise à jour logicielle au *groupe-limites-site-par-défaut&lt;codesite>*. Vous permettez ainsi aux clients qui ne sont pas membres d’un autre groupe de limites de basculer vers le comportement de secours pour rechercher un point de mise à jour logicielle.


Pour gérer les points de mise à jour logicielle pour les groupes de limites, utilisez les [procédures de la documentation relative à la version Current Branch](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#procedures-for-boundary-groups). Toutefois, n’oubliez pas qu’il n’est pas encore possible de configurer des durées de secours pour les points de mise à jour logicielle.


## <a name="hardware-inventory-collects-uefi-information"></a>L’inventaire matériel collecte des informations UEFI
Une nouvelle classe d’inventaire matériel (**SMS_Firmware**) et une nouvelle propriété (**UEFI**) sont disponibles pour vous aider à déterminer si un ordinateur démarre ou non en mode UEFI. Quand un ordinateur démarre en mode UEFI, la propriété **UEFI** est définie sur **TRUE**. Cette option est activée dans l’inventaire matériel par défaut. Pour plus d’informations sur l’inventaire matériel, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

## <a name="improvements-to-operating-system-deployment"></a>Améliorations apportées au déploiement des systèmes d’exploitation
Les améliorations suivantes ont été apportées au déploiement des systèmes d’exploitation, la plupart d’entre elles ayant été inspirées par vos commentaires.
- [**Prise en charge d’un plus grand nombre d’applications dans la séquence de tâches Installer les applications**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17062207-task-sequence-allow-more-than-9-applications-in-t) : Le nombre maximal d’applications qu’il est possible d’installer s’élève désormais à 99 pour la séquence de tâches **Installer les applications**. Auparavant, le maximum était de 9 applications.
- [**Sélection de plusieurs applications dans la séquence de tâches Installer l’application**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/15459978-when-adding-items-to-an-install-application-step) : Lorsque vous ajoutez une application dans la séquence de tâches Installer l’application dans l’éditeur de séquences de tâches, il vous est désormais possible de sélectionner plusieurs applications dans le volet **Sélectionner l’application à installer**.
- [**Expiration des supports autonomes**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/14448564-provide-a-method-for-expiring-standalone-media) : Lorsque vous créez un support autonome, de nouvelles options vous permettent de définir des dates facultatives de début et d’expiration pour ce support. Ces paramètres sont désactivés par défaut. Les dates sont comparées à l’heure système de l’ordinateur avant l’exécution du support autonome. Lorsque l’heure du système est antérieure à l’heure de début ou ultérieure à l’heure d’expiration, le support autonome n’est pas démarré. Ces options sont également disponibles avec l’applet de commande New-CMStandaloneMedia PowerShell.
- [**Prise en charge de nouveaux types de contenu dans les supports autonomes**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8341257-support-installation-of-packages-apps-via-dynamic) : D’autres types de contenu sont désormais pris en charge dans les supports autonomes. Vous pouvez sélectionner des packages supplémentaires, des packages de pilotes et des applications en vue d’effectuer une copie intermédiaire sur les supports, ainsi que d’autres types de contenu référencés dans la séquence de tâches. Auparavant, seul le contenu référencé dans la séquence de tâches était copié sur les supports autonomes.
- [**Délai d’expiration configurable pour la séquence de tâches Appliquer automatiquement les pilotes**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17153660-auto-apply-driver-timeout) : De nouvelles variables de séquence de tâches sont désormais disponibles pour configurer le délai d’expiration dans la séquence de tâches Appliquer automatiquement les pilotes lorsque vous effectuez des demandes de catalogue HTTP. Les variables et valeurs par défaut (en secondes) suivantes sont disponibles :
   - SMSTSDriverRequestResolveTimeOut Default: 60
   - SMSTSDriverRequestConnectTimeOut Default: 60
   - SMSTSDriverRequestSendTimeOut Default: 60
   - SMSTSDriverRequestReceiveTimeOut Default: 480
- [**L’ID de package s’affiche désormais dans les séquences de tâches**](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16167430-display-packageid-when-viewing-a-task-sequence-ste) : Toutes les étapes de séquence de tâches qui font référence à un package, un package de pilotes, une image de système d’exploitation, une image de démarrage ou un package de mise à niveau de système d’exploitation affichent désormais l’ID de package de l’objet référencé. Lorsqu’une séquence de tâches fait référence à une application, elle affiche l’ID de l’objet.
- **Le kit de déploiement et d’évaluation Windows 10 (ADK) est désormais suivi par le numéro de version** : Le kit de déploiement et d’évaluation Windows 10 est désormais suivi par le numéro de version pour garantir une meilleure prise en charge lors de la personnalisation d’images de démarrage Windows 10. Par exemple, si le site utilise la version 1607 du Windows ADK pour Windows 10, seules les images de démarrage dont la version est 10.0.14393 pourront être personnalisées dans la console. Pour plus d’informations sur la personnalisation des versions de WinPE, consultez [Personnaliser les images de démarrage](/sccm/osd/get-started/customize-boot-images).
- **Le chemin source par défaut de l’image de démarrage ne peut plus être modifié** : Les images de démarrage par défaut sont gérées par Configuration Manager et le chemin source par défaut de l’image de démarrage ne peut donc plus être modifié dans la console Configuration Manager ni à l’aide du SDK Configuration Manager. Vous pouvez toutefois continuer à configurer un chemin source personnalisé pour les images de démarrage personnalisées.

## <a name="host-software-updates-on-cloud-based-distribution-points"></a>Héberger des mises à jour logicielles sur des points de distribution cloud
À compter de cette préversion, les points de distribution cloud peuvent être utilisés pour héberger un package de mise à jour logicielle. Toutefois, étant donné qu’il est possible de configurer les clients pour qu’ils téléchargent des mises à jour logicielles directement à partir de Microsoft Update, vous devez tenir compte des coûts supplémentaires que représente le déploiement d’un package de mise à jour logicielle sur un point de distribution cloud.

Pour plus d’informations sur l’utilisation des points de distribution cloud, consultez [Utiliser un point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) dans le contenu relatif à la version Current Branch de Configuration Manager.

## <a name="validate-device-health-attestation-data-via-management-points"></a>Valider les données de l’attestation d’intégrité de l’appareil via des points de gestion

À compter de cette préversion, il est possible de configurer des points de gestion dans le but de valider les données de rapport d’attestation d’intégrité pour le service d’attestation d’intégrité cloud ou local. Le nouvel onglet **Options avancées** de la boîte de dialogue **Propriétés du composant du point de gestion** vous permet d’**ajouter**, de **modifier** et de **supprimer** l’**URL du service local d’attestation d’intégrité de l’appareil**. Dans **Paramètres de périphérique personnalisés**, vous pouvez également sélectionner **Utiliser le service d’attestation d’intégrité local** pour l’agent client.  La valeur **Oui** active la création de rapports pour le point de gestion local et non pour le service cloud.

### <a name="try-it-out"></a>Faites un essai

- **Activer le service local d’attestation d’intégrité de l’appareil pour un point de gestion**<br>  Dans la console Configuration Manager, naviguez jusqu’au point de gestion, ouvrez **Propriétés du composant du point de gestion**, puis cliquez sur l’onglet **Options avancées**. Cliquez sur **Ajouter**, puis indiquez l’URL locale (par exemple, https://10.10.10.10)) pour les **URL du service local d’attestation d’intégrité de l’appareil**.
- **Activer la création de rapports à partir du service local d’attestation d’intégrité des points de gestion pour l’agent client**<br>Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client**, puis double-cliquez, ou créez de nouveaux **Paramètres de périphérique personnalisés**. Sélectionnez **Agent ordinateur**, puis définissez **Utiliser le service d’attestation d’intégrité local** sur **Oui**. Si l’option **Activer la communication avec le service d’attestation d’intégrité** est définie sur **Oui** et l’option **Utiliser le service d’attestation d’intégrité local** est définie sur **Non**, le point de gestion utilise le service cloud d’attestation d’intégrité de l’appareil.

## <a name="use-the-oms-connector-for-microsoft-azure-government-cloud"></a>Utiliser le connecteur OMS pour Microsoft Azure Government Cloud
Avec cette préversion, vous pouvez désormais utiliser le connecteur Microsoft Operations Management Suite (OMS) pour vous connecter à un espace de travail OMS se trouvant dans Microsoft Azure Government Cloud.  

Pour cela, vous modifiez un fichier de configuration pour qu’il pointe vers Azure Government Cloud, puis vous installez le connecteur OMS.

### <a name="set-up-an-oms-connector-to-microsoft-azure-government-cloud"></a>Configurer un connecteur OMS pour qu’il pointe vers Microsoft Azure Government Cloud
1.  Sur les ordinateurs où est installée la console Configuration Manager, modifiez le fichier de configuration suivant pour qu’il pointe vers Azure Government Cloud : ***&lt;Chemin d’installation de Configuration Manager>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Modifications :**

    Changez la valeur du nom de paramètre *FairFaxArmResourceID* pour qu’elle corresponde à « https://management.usgovcloudapi.net/ »

   - **Avant modification :** &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Après modification :**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String"> &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Changez la valeur du nom de paramètre *FairFaxAuthorityResource* pour qu’elle corresponde à « https://login.microsoftonline.com/ »

  - **Avant modification :** &lt;nom de paramètre="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

    - **Après modification :** &lt;nom du paramètre="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.com/&lt;/value>

2.  Après avoir apporté ces deux modifications et enregistré le fichier, redémarrez la console Configuration Manager sur le même ordinateur, puis utilisez cette console pour installer le connecteur OMS. Pour installer le connecteur, utilisez les informations situées sous [Synchroniser les données de System Center Configuration Manager vers Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), puis sélectionnez l’**Espace de travail Operations Management Suite** qui se trouve dans Microsoft Azure Government Cloud.

3.  Une fois le connecteur OMS installé, une connexion à Azure Government Cloud est disponible lorsque vous utilisez une console se connectant au site.

## <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride

À compter de cette version Technical Preview, vous n’avez plus besoin de cibler des versions Android et iOS spécifiques quand vous créez des stratégies et des profils pour des appareils gérés par Intune dans le cadre d’une gestion des appareils mobiles (MDM) hybride. Au lieu de cela, vous choisissez l’un des types d’appareils suivants :

- Android
- Samsung KNOX Standard 4.0 et versions supérieures
- iPhone
- iPad

Cette modification affecte les Assistants de création des éléments suivants :

- Éléments de configuration
- Stratégies de conformité
- Profils de certificat
- Profils de messagerie
- Profils VPN
- Profils Wi-Fi

Grâce à cette modification, les déploiements hybrides peuvent prendre en charge plus rapidement les nouvelles versions Android et iOS sans avoir besoin d’une nouvelle version de Configuration Manager ou d’une extension. Quand une nouvelle version est prise en charge dans Intune autonome, les utilisateurs peuvent mettre à niveau leurs appareils mobiles avec cette version.

Pour éviter tout problème lors de la mise à niveau de versions antérieures de Configuration Manager, les versions des systèmes d’exploitation des appareils mobiles restent disponibles dans les pages de propriétés de ces éléments. Si vous avez encore besoin de cibler une version spécifique, créez l’élément, puis spécifiez la version ciblée dans la page de propriétés du nouvel élément.
