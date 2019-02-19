---
title: Extensions de schéma
titleSuffix: Configuration Manager
description: Étendre le schéma Active Directory pour prendre en charge System Center Configuration Manager.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8a4d9bdbf50998ec47c5ac650aba014ed6194a2c
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142287"
---
# <a name="schema-extensions-for-system-center-configuration-manager"></a>Extensions de schéma pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez étendre le schéma Active Directory pour prendre en charge Configuration Manager. Cette opération modifie le schéma Active Directory d’une forêt pour ajouter un nouveau conteneur et plusieurs attributs grâce auxquels les sites Configuration Manager peuvent publier dans Active Directory des informations clés utilisables par les clients de manière sécurisée. Ces informations peuvent simplifier le déploiement et la configuration des clients et aider ces derniers à localiser les ressources du site, comme les serveurs sur lesquels le contenu a été déployé ou qui fournissent différents services aux clients.  

-   Il est conseillé d’étendre le schéma Active Directory, mais ceci n’est pas obligatoire.  

Avant d’ [étendre le schéma Active Directory](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema), vous devez être familiarisé avec les services de domaine Active Directory et la [modification du schéma Active Directory](https://technet.microsoft.com/library/cc759402\(v=ws.10\).aspx).  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Considérations relatives à l’extension du schéma Active Directory pour Configuration Manager  

-   Les extensions de schéma Active Directory pour System Center Configuration Manager sont identiques à celles utilisées par Configuration Manage 2007 et Configuration Manager 2012. Si vous avez déjà étendu le schéma pour l’une de ces versions, vous n’avez plus besoin de l’étendre.  

-   L’extension du schéma est une action irréversible, unique et à l’échelle de la forêt.  

-   Seul un utilisateur membre du groupe Administrateurs du schéma ou disposant d’autorisations suffisantes pour modifier le schéma peut étendre ce dernier.  

-   Bien que vous puissiez étendre le schéma avant ou après l’exécution du programme d’installation de Configuration Manager, nous vous conseillons d’étendre le schéma avant de commencer à configurer vos sites et vos paramètres de hiérarchie. Ce procédé simplifie la plupart des étapes de configuration ultérieures.  

-   Une fois le schéma étendu, le catalogue global Active Directory est répliqué dans toute la forêt. Ainsi, choisissez une période calme, afin de ne pas affecter d’autres processus dépendant du réseau :  

    -   Dans les forêts Windows 2000, l’extension du schéma entraîne une synchronisation complète du catalogue global.  

    -   À partir des forêts Windows 2003, seuls les attributs ajoutés récemment sont répliqués.  

**Appareils et clients qui n’utilisent pas le schéma Active Directory :**  

-   Appareils mobiles gérés par le connecteur du serveur Exchange Server  

-   Client des ordinateurs Mac  

-   Client des serveurs Linux et UNIX  

-   Appareils mobiles inscrits par Configuration Manager  

-   Appareils mobiles inscrits par Microsoft Intune  

-   Clients d'appareil mobile hérités  

-   Clients Windows configurés pour être gérés uniquement via Internet  

-   Clients Windows détectés par Configuration Manager comme étant connectés à Internet  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Fonctionnalités qui bénéficient de l’extension du schéma  
**Installation de l’ordinateur client et attribution de site** : quand un ordinateur Windows installe un nouveau client, ce dernier recherche des propriétés d’installation dans Active Directory Domain Services.  

-   **Solutions de contournement :** Si vous n’étendez pas le schéma, utilisez l’une des options suivantes pour fournir les détails de configuration que les ordinateurs doivent installer :  

    -   **Utiliser l’installation poussée du client**. Avant d’utiliser une méthode d’installation du client, vérifiez que tous les prérequis sont remplis. Pour plus d’informations, consultez la section « Dépendances liées aux méthodes d’installation » dans [Prérequis au déploiement de clients sur des ordinateurs Windows](/sccm/core/clients/deploy/prerequisites-for-deploying-clients-to-windows-computers).  

    -   **Installer les clients manuellement** et fournir les propriétés d'installation du client en utilisant les propriétés de ligne de commande d'installation CCMSetup. Ces méthodes doivent inclure :  

        -   Spécifiez un point de gestion ou un chemin source à partir duquel l’ordinateur peut télécharger les fichiers d’installation en utilisant la propriété CCMSetup **/mp:&lt;nom_ordinateur_nom_point_de_gestion\>** ou **/source:&lt;chemin_fichiers_sources_client\>** sur la ligne de commande CCMSetup lors de l’installation du client.  

        -   Spécifiez une liste de points de gestion initiale pour le client pour qu’il puisse les attribuer au site et ensuite télécharger les paramètres de stratégie client et du site. Pour ce faire, utilisez la propriété CCMSetup Client.msi de SMSMP.  

    -   **Publier le point de gestion dans DNS ou WINS** et configurer des clients pour utiliser cette méthode d’emplacement de service.  

**Configuration du port pour la communication client à serveur** : quand un client est installé, il est configuré avec les informations du port stockées dans Active Directory. Si vous modifiez ultérieurement le port de communication client à serveur pour un site, un client peut obtenir ce nouveau paramètre de port par les services de domaine Active Directory.  

-   **Solutions de contournement :** Si vous n’étendez pas le schéma, utilisez l’une des options suivantes pour fournir de nouvelles configurations de port aux clients existants :  

    -   **Réinstaller les clients** à l’aide d’options qui configurent le nouveau port.  

    -   **Déployer sur les clients un script personnalisé qui met à jour les informations de port**. Si les clients ne peuvent pas communiquer avec un site en raison d’une modification du port, vous ne pouvez pas utiliser Configuration Manager pour déployer ce script. Vous pouvez par exemple utiliser la Stratégie de groupe.  

**Scénarios de déploiement de contenu** : quand vous créez du contenu sur un site et que vous déployez ce contenu vers un autre site de la hiérarchie, le site récepteur doit être capable de vérifier la signature des données du contenu signé. Cela nécessite un accès à la clé publique du site source dans lequel vous créez ces données. Quand vous étendez le schéma Active Directory pour Configuration Manager, la clé publique d’un site est accessible à tous les sites de la hiérarchie.  

-   **Solution de contournement :** Si vous n’étendez pas le schéma, utilisez l’outil de maintenance de hiérarchie, **preinst.exe**, pour échanger les informations de la clé sécurisées entre les sites.  

     Par exemple, si vous envisagez de créer du contenu sur un site principal et le déployer sur un site secondaire inférieur à un site principal différent, vous devez soit étendre le schéma Active Directory pour permettre au site secondaire d’obtenir la clé publique de la source des sites principaux, soit utiliser preinst.exe pour partager les clés directement entre les deux sites.  

## <a name="active-directory-attributes-and-classes"></a>Classes et attributs Active Directory  
Quand vous étendez le schéma pour System Center Configuration Manager, les classes et les attributs suivants sont ajoutés au schéma et sont accessibles à tous les sites Configuration Manager dans cette forêt Active Directory.  

-   Attributs :  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        sur  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Classes :  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]
> 
>  Les extensions de schéma peuvent inclure des attributs et des classes issus de versions précédentes du produit, qui ne sont plus utilisés par System Center Configuration Manager. Par exemple :  
> 
> 
> - Attribut : cn=MS-SMS-Site-Boundaries  
>   -   Classe : cn=MS-SMS-Server-Locator-Point  

Vous pouvez vous assurer que les listes précédentes sont à jour en consultant le fichier **ConfigMgr_ad_schema.LDF**, situé dans le dossier **\SMSSETUP\BIN\x64** du support d’installation de System Center Configuration Manager.  
