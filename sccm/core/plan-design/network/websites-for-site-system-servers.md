---
title: Sites web pour les systèmes de site
titleSuffix: Configuration Manager
description: Découvrez les sites web personnalisés et par défaut pour les serveurs de système de site dans System Center Configuration Manager.
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 681f0893-e83b-476e-9ec0-a5dc7c9deeb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5614317639c12813acf61f17de844c8304bed70f
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344345"
---
# <a name="websites-for-site-system-servers-in-system-center-configuration-manager"></a>Sites web pour les serveurs de système de site dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Plusieurs rôles de système de site Configuration Manager nécessitent l’utilisation de Microsoft Internet Information Services (IIS) et utilisent le site web IIS par défaut pour héberger les services du système de site. Si vous devez exécuter d’autres applications web sur le même serveur et que les paramètres ne sont pas compatibles avec Configuration Manager, utilisez plutôt un site web personnalisé pour Configuration Manager.  

> [!TIP]  
>  Une bonne pratique en matière de sécurité consiste à dédier un serveur aux systèmes de site Configuration Manager nécessitant IIS. Quand vous exécutez d’autres applications sur un système de site Configuration Manager, vous augmentez la surface exposée aux attaques de cet ordinateur.  




##  <a name="BKMK_What2Know"></a> Informations à connaître avant d’utiliser des sites web personnalisés  
 Par défaut, les rôles de système de site utilisent le **site web par défaut** dans IIS. Ceci est automatiquement configuré lors de l’installation du rôle de système de site. Toutefois, sur les sites principaux, vous pouvez choisir d’utiliser des sites web personnalisés à la place. Quand vous utilisez des sites web personnalisés :  

-   Les sites web personnalisés sont activés pour l’ensemble du site, et non pas individuellement pour des serveurs ou rôles du système de site.  

-   Sur les sites principaux, chaque ordinateur qui hébergera un rôle de système de site applicable doit être configuré avec un site web personnalisé nommé **SMSWEB**. Tant que ce site web n’aura pas été créé et que les rôles de système de site sur l’ordinateur n’auront pas été configurés pour utiliser le site web personnalisé, les clients ne pourront peut-être pas communiquer avec les rôles de système de site sur cet ordinateur.  

-   Du fait que les sites secondaires sont automatiquement configurés pour utiliser un site web personnalisé quand leur site parent principal est configuré pour cela, vous devez également créer des sites web personnalisés dans IIS sur chaque serveur de système de site secondaire qui nécessite IIS.  


  **Configuration requise pour l’utilisation de sites web personnalisés :**  

 Avant d’activer l’option pour utiliser des sites web personnalisés sur un site, vous devez effectuer les opérations suivantes :  

-   Créez un site web personnalisé nommé **SMSWEB** dans IIS sur chaque serveur de système de site qui nécessite les services IIS. Effectuez cette opération sur le site principal et sur tous les sites secondaires enfants.  

-   Configurez le site web personnalisé pour répondre sur le même port que celui configuré pour la communication client Configuration Manager (port de demande client).  

-   Pour chaque site web personnalisé ou site web par défaut qui utilise un dossier personnalisé, placez une copie du type de document par défaut que vous utilisez dans le dossier racine qui héberge le site web. Par exemple, sur un ordinateur Windows Server 2008 R2 avec des configurations par défaut, **iisstart.htm** est l’un des types de documents par défaut disponibles. Ce fichier se trouve à la racine du site web par défaut. Vous pouvez en placer une copie (ou une copie du type de document par défaut que vous utilisez) dans le dossier racine qui héberge le site web personnalisé SMSWEB. Pour plus d’informations sur les types de documents par défaut, consultez [Document par défaut &lt;defaultDocument\> pour IIS](http://www.iis.net/configreference/system.webserver/defaultdocument).  

**À propos de la configuration requise pour IIS :**
**Les rôles de système de site suivants nécessitent IIS et un site web pour héberger les services de système de site :**  

-   Point de service web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point de distribution  

-   Point d'inscription  

-   Point proxy d'inscription  

-   Point d’état de secours  

-   Point de gestion  

-   Point de mise à jour logicielle  

-   Point de migration d’état  

Autres éléments à prendre en considération  

-   Quand un site principal comporte des sites web personnalisés activés, les clients attribués à ce site sont configurés pour communiquer avec les sites web personnalisés plutôt qu’avec les sites web par défaut sur les serveurs de système de site concernés.  

-   Si vous activez des sites web personnalisés pour un site principal, envisagez d’utiliser des sites web personnalisés pour tous les sites principaux de votre hiérarchie afin d’assurer la bonne itinérance des clients dans la hiérarchie. (L’itinérance désigne le déplacement d’un ordinateur client vers un nouveau segment de réseau qui est géré par un autre site. L’itinérance peut avoir une incidence sur les ressources auxquelles un client peut accéder localement au lieu d’y accéder sur une liaison WAN).  

-   Les rôles de système de site qui utilisent les services IIS mais n’acceptent pas les connexions clientes, comme le point de Reporting Services, utilisent également le site web SMSWEB au lieu du site web par défaut.  

-   Les sites web personnalisés vous permettent d’attribuer des numéros de port différents de ceux utilisés par le site web par défaut des ordinateurs. Un site web par défaut et le site web personnalisé ne peuvent pas s’exécuter simultanément s’ils tentent tous les deux d’utiliser les mêmes ports TCP/IP.  

-   Les ports TCP/IP que vous configurez dans IIS pour le site web personnalisé doivent correspondre aux ports de demande client pour le site.  

## <a name="switch-between-default-and-custom-websites"></a>Basculer entre un site web par défaut et un site web personnalisé  
Vous pouvez cocher ou décocher la case relative à l’utilisation de sites web personnalisés sur un site principal à tout moment (la case à cocher se trouve sous l’onglet Général des propriétés des sites), mais effectuez cette modification avec prudence. Si cette configuration est modifiée, tous les rôles de système de site applicables sur le site principal et sur les sites secondaires enfants doivent être désinstallés, puis réinstallés :  

Les rôles suivants sont **réinstallés automatiquement**:  

-   Point de gestion  

-   Point de distribution  

-   Point de mise à jour logicielle  

-   Point d'état de secours  

-   Point de migration d’état  

Les rôles suivants doivent être **réinstallés manuellement**:  

-   Point de service web du catalogue des applications  

-   Point du site web du catalogue des applications  

-   Point d'inscription  

-   Point proxy d'inscription  

En outre :  

-   Quand vous utilisez un site web personnalisé à la place du site web par défaut, Configuration Manager ne supprime pas les anciens répertoires virtuels. Si vous souhaitez supprimer les fichiers utilisés par Configuration Manager, vous devez supprimer manuellement les répertoires virtuels créés sous le site web par défaut.  

-   Si vous modifiez le site pour utiliser des sites web personnalisés, les clients qui sont déjà attribués au site doivent ensuite être reconfigurés pour utiliser les nouveaux ports de demande client pour les sites web personnalisés. Consultez [Guide pratique pour configurer les ports de communication des clients dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

## <a name="set-up-custom-websites"></a>Configurer des sites web personnalisés  
Du fait que les procédures de création d’un site web personnalisé varient selon la version du système d’exploitation, reportez-vous à la documentation de votre version de système d’exploitation pour connaître les procédures exactes à suivre. Toutefois, suivez les indications ci-dessous, le cas échéant :  

-   Le site web doit être appelé **SMSWEB**.  

-   Si vous configurez le protocole HTTPS, vous devez spécifier un certificat SSL pour pouvoir enregistrer la configuration.  

-   Après avoir créé le site web personnalisé, supprimez les ports de sites web personnalisés que vous utilisez à partir d’autres sites web dans IIS :  

    1.  Modifiez les **liaisons** des autres sites web pour supprimer les ports qui correspondent à ceux attribués au site web **SMSWEB**.  

    2.  Démarrez le site web **SMSWEB**.  

    3.  Redémarrez le service **SMS_SITE_COMPONENT_MANAGER** sur le serveur de site du site.  
