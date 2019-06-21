---
title: Notions de base de la sécurité
titleSuffix: Configuration Manager
description: Découvrez-en plus sur les couches de sécurité dans Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a6c6f931271d8cc8f69e3c65de8c4932f5ab5c95
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159264"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Notions de base de la sécurité pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article récapitule les composants fondamentaux de la sécurité d’un environnement Configuration Manager :
- [Couches de sécurité](#bkmk_layers)
- [Administration basée sur des rôles](#bkmk_rba)
- [Sécurisation des points de terminaison des clients](#bkmk_endpoints)
- [Comptes et groupes de Configuration Manager](#bkmk_accounts)
- [Confidentialité](#bkmk_privacy)

## <a name="bkmk_layers"></a> Couches de sécurité

La sécurité pour Configuration Manager se compose des couches suivantes : 
- [Système d’exploitation Windows et sécurité réseau](#bkmk_layer-windows)
- [Infrastructure réseau : pare-feu, détection d’intrusion, infrastructure à clé publique (PKI)](#bkmk_layer-network)
- [Contrôles de sécurité de Configuration Manager](#bkmk_layer-cm)
- [Fournisseur SMS](#bkmk_layer-provider)
- [Autorisations de base de données de site](#bkmk_layer-db)

#### <a name="bkmk_layer-windows"></a> Système d’exploitation Windows et sécurité réseau
La première couche est fournie par les fonctionnalités de sécurité Windows tant pour le système d’exploitation que pour le réseau. Cette couche inclut les composants suivants :  

-   le partage de fichiers pour transférer les fichiers entre des composants Configuration Manager ;  

-   des listes de contrôle d'accès pour sécuriser les fichiers et les clés de Registre ;  

-   La sécurité du protocole Internet (IPsec) pour sécuriser les communications  

-   Une stratégie de groupe pour définir la stratégie de sécurité  

-   Des autorisations DCOM (Distributed Component Object Model) pour les applications distribuées, comme la console Configuration Manager  

-   des services de domaine Active Directory pour stocker les entités de sécurité ;  

-   La sécurité de compte Windows, notamment certains groupes créés par Configuration Manager durant la configuration  

#### <a name="bkmk_layer-network"></a> Infrastructure réseau

Des composants de sécurité supplémentaires, comme les pare-feu et la détection d’intrusion, contribuent à protéger l’ensemble de l’environnement. Les certificats émis par des implémentations d’infrastructure à clé publique (PKI) standard permettent de fournir une authentification, une signature et un chiffrement.  

#### <a name="bkmk_layer-cm"></a> Contrôles de sécurité de Configuration Manager

En plus de la sécurité fournie par l’infrastructure réseau et de serveur Windows, Configuration Manager contrôle l’accès à sa console et à ses ressources de plusieurs façons. Par défaut, seuls les administrateurs locaux disposent de droits d’accès aux fichiers et aux clés de Registre nécessaires à la console Configuration Manager sur les ordinateurs où vous l’installez.  

#### <a name="bkmk_layer-provider"></a> Fournisseur SMS

La couche de sécurité suivante est basée sur l'accès via WMI (Windows Management Instrumentation), en particulier le fournisseur SMS. Le fournisseur SMS est un composant Configuration Manager qui octroie un accès à un utilisateur pour interroger la base de données du site afin d’obtenir des informations. Par défaut, l’accès au fournisseur est restreint aux membres du groupe Administrateurs SMS local. À l’origine, ce groupe contient uniquement l’utilisateur qui a installé Configuration Manager. Pour accorder d'autres autorisations de compte à l'emplacement de stockage CIM (Common Information Model) et au fournisseur SMS, ajoutez les autres comptes au groupe Administrateurs SMS.  

À compter de la version 1810, vous pouvez spécifier le niveau d’authentification minimal pour les administrateurs qui accèdent aux sites Configuration Manager. Cette fonctionnalité force les administrateurs à se connecter à Windows avec le niveau requis. <!--1357013-->  

Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

#### <a name="bkmk_layer-db"></a> Autorisations de base de données de site

Les autorisations d'accès aux objets de la base de données de site constituent la dernière couche de sécurité. Par défaut, le compte système local et le compte d’utilisateur que vous utilisez pour installer Configuration Manager peuvent administrer tous les objets de la base de données du site. Accordez et limitez les autorisations à des utilisateurs administratifs supplémentaires dans la console Configuration Manager à l’aide de l’administration basée sur des rôles.  



## <a name="bkmk_rba"></a> Administration basée sur des rôles  

 Configuration Manager utilise l’administration basée sur des rôles pour sécuriser les objets (regroupements, déploiements, sites, etc.). Ce modèle d'administration définit et gère de façon centralisée les paramètres d'accès de sécurité à l'échelle de la hiérarchie pour tous les sites et les paramètres du site. 

 Un administrateur attribue des *rôles de sécurité* aux utilisateurs administratifs et aux autorisations de groupe. Les autorisations sont connectées à différents types d’objet Configuration Manager, par exemple pour créer ou changer les paramètres du client. 

 Les *étendues de sécurité* regroupent des instances d’objets spécifiques qu’un utilisateur administratif est chargé de gérer, par exemple une application qui installe Microsoft Office. 

 La combinaison des rôles de sécurité, des étendues de sécurité et des regroupements définit les objets qu’un utilisateur administratif peut afficher et gérer. Configuration Manager installe des rôles de sécurité par défaut pour les tâches de gestion classiques. Créez vos propres rôles de sécurité en fonction des besoins propres à votre activité.  

 Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration).  



## <a name="bkmk_endpoints"></a> Sécurisation des points de terminaison des clients  

 Configuration Manager sécurise la communication des clients aux rôles de système de site à l’aide de certificats auto-signés ou PKI ou de jetons Azure AD (Azure Active Directory). Certains scénarios nécessitent l’utilisation de certificats PKI. Citons par exemple la [gestion des clients basés sur internet](/sccm/core/clients/manage/plan-internet-based-client-management) et les [clients d’appareils mobiles](/sccm/mdm/plan-design/plan-on-premises-mdm).  

 Vous pouvez configurer les rôles de système de site auxquels les clients se connectent pour utiliser les protocoles HTTPS ou HTTP dans le cadre de la communication avec les clients. Les ordinateurs clients communiquent toujours à l’aide de la méthode la plus sécurisée disponible. Les ordinateurs clients n’utilisent la méthode de communication moins sécurisée que si vos rôles de système de site autorisent la communication HTTP.  

 Pour plus d’informations, consultez [Planifier la sécurité](/sccm/core/plan-design/security/plan-for-security).



## <a name="bkmk_accounts"></a> Comptes et groupes de Configuration Manager  

 Configuration Manager utilise le compte Système local pour la plupart des opérations de site. Certaines tâches de gestion peuvent nécessiter la création et la gestion de comptes supplémentaires. Configuration Manager crée plusieurs rôles SQL Server et groupes par défaut durant l’installation. Vous devez peut-être ajouter manuellement des comptes d’ordinateur ou d’utilisateur à ces groupes par défaut et à ces rôles SQL Server.  

 Pour plus d’informations, consultez [Comptes utilisés dans Configuration Manager](/sccm/core/plan-design/hierarchy/accounts).  



## <a name="bkmk_privacy"></a> Confidentialité  

 Avant d’implémenter Configuration Manager, réfléchissez à vos besoins en matière de confidentialité. Bien que les produits de gestion d’entreprise offrent de nombreux avantages, car ils permettent de gérer efficacement un grand nombre de clients, ces logiciels peuvent affecter la confidentialité des utilisateurs de votre organisation. Configuration Manager comprend de nombreux outils pour collecter les données et superviser les appareils. Certains outils sont susceptibles de poser des problèmes de confidentialité dans votre organisation.  

 Par exemple, quand vous installez le client Configuration Manager, de nombreux paramètres de gestion sont activés par défaut. Le logiciel client envoie donc des informations au site Configuration Manager. Le site stocke les informations sur le client dans la base de données de site. Les informations sur le client ne sont pas envoyées directement à Microsoft. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).



## <a name="see-also"></a>Voir aussi

- [Planifier la sécurité](/sccm/core/plan-design/security/plan-for-security)  

- [Sécurité et confidentialité pour les clients Configuration Manager](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configurer la sécurité](/sccm/core/plan-design/security/configure-security)   

- [Communications entre points de terminaison](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

- [Informations techniques de référence sur les contrôles de chiffrement](/sccm/core/plan-design/security/cryptographic-controls-technical-reference)  
