---
title: Notions de base de la sécurité
titleSuffix: Configuration Manager
description: En savoir plus sur les couches de sécurité pour System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 47b03d8e3f0828efc6f32627fb0298645b5998d1
ms.sourcegitcommit: 98c3f7848dc9014de05541aefa09f36d49174784
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/14/2018
ms.locfileid: "42584623"
---
# <a name="fundamentals-of-security-for-system-center-configuration-manager"></a>Notions de base de la sécurité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La sécurité pour System Center Configuration Manager se compose de plusieurs couches. La première couche est fournie par les fonctionnalités de sécurité Windows tant pour le système d’exploitation que pour le réseau, qui incluent :  

-   Le partage de fichiers pour transférer des fichiers entre les composants Configuration Manager.  

-   Des listes de contrôle d’accès pour sécuriser les fichiers et les clés de Registre.  

-   La sécurité du protocole Internet (IPsec) pour sécuriser les communications.  

-   Une stratégie de groupe pour définir la stratégie de sécurité.  

-   Des autorisations DCOM (Distributed Component Object Model) pour les applications distribuées, comme la console Configuration Manager.  

-   Des services de domaine Active Directory pour stocker les entités de sécurité.  

-   La sécurité de compte Windows, notamment certains groupes qui sont créés pendant la configuration de Configuration Manager.  

Des composants de sécurité supplémentaires (pare-feu, détection d’intrusion, par exemple) aident à protéger l’ensemble de l’environnement. Les certificats émis par des implémentations d’infrastructure à clé publique (PKI) standard permettent de fournir une authentification, une signature et un chiffrement.  

Outre la sécurité fournie par l’infrastructure réseau et de serveur Windows, Configuration Manager contrôle l’accès à la console Configuration Manager et à ses ressources de plusieurs façons. Par défaut, seuls les administrateurs locaux disposent d’autorisations sur les fichiers et les clés de Registre nécessaires à l’exécution de la console Configuration Manager sur les ordinateurs où elle est installée.  

La couche de sécurité suivante est basée sur l'accès via WMI (Windows Management Instrumentation), en particulier le fournisseur SMS. Le fournisseur SMS est un composant Configuration Manager qui octroie un accès à un utilisateur pour interroger la base de données du site afin d’obtenir des informations. Par défaut, l’accès au fournisseur est restreint aux membres du groupe Administrateurs SMS local. À l’origine, ce groupe contient uniquement l’utilisateur qui a installé Configuration Manager. Pour accorder d'autres autorisations de compte à l'emplacement de stockage CIM (Common Information Model) et au fournisseur SMS, ajoutez les autres comptes au groupe Administrateurs SMS.  

Les autorisations d'accès aux objets de la base de données de site constituent la dernière couche de sécurité. Par défaut, le compte système local et le compte d’utilisateur que vous utilisez pour installer Configuration Manager peuvent administrer tous les objets de la base de données du site. Vous pouvez accorder et limiter les autorisations à des utilisateurs administratifs supplémentaires dans la console Configuration Manager à l’aide de l’administration basée sur des rôles.  



## <a name="role-based-administration"></a>Administration basée sur des rôles  
 Configuration Manager utilise l’administration basée sur des rôles pour sécuriser les objets (regroupements, déploiements, sites, etc.). Ce modèle d'administration définit et gère de façon centralisée les paramètres d'accès de sécurité à l'échelle de la hiérarchie pour tous les sites et les paramètres du site. Les rôles de sécurité sont attribués aux utilisateurs administratifs et aux autorisations de groupe. Les autorisations sont connectées à différents types d’objet Configuration Manager, comme les autorisations qui sont utilisées pour créer ou modifier les paramètres du client. Les étendues de sécurité regroupent des instances d’objets spécifiques qu’un utilisateur administratif est chargé de gérer, par exemple une application qui installe Microsoft Office. La combinaison des rôles de sécurité, des étendues de sécurité et des regroupements définit les objets qu’un utilisateur administratif peut afficher et gérer. Configuration Manager installe des rôles de sécurité par défaut pour les tâches de gestion classiques. Vous pouvez toutefois créer vos propres rôles de sécurité, en fonction des besoins propres à votre activité.  

 Pour plus d’informations, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="securing-client-endpoints"></a>Sécurisation des points de terminaison des clients  
 La communication du client vers les rôles de système de site est sécurisée à l’aide de certificats auto-signés ou de certificats PKI. Vous devez utiliser un certificat PKI pour les ordinateurs clients que Configuration Manager détecte sur Internet ainsi que pour les clients d’appareil mobile. Le certificat PKI utilise le protocole HTTPS pour sécuriser les points de terminaison clients. Les rôles de système de site auxquels les clients se connectent peuvent être configurés pour utiliser les protocoles HTTPS ou HTTP dans le cadre de la communication avec les clients. Les ordinateurs clients communiquent toujours à l’aide de la méthode la plus sécurisée disponible. Les ordinateurs clients n’utilisent le protocole HTTP sur l’intranet que si vos rôles de système de site permettent la communication HTTP.  

 Pour plus d’informations, consultez [Informations techniques de référence sur les contrôles de chiffrement pour System Center Configuration Manager](../../protect/deploy-use/cryptographic-controls-technical-reference.md).  

## <a name="configuration-manager-accounts-and-groups"></a>Comptes et groupes de Configuration Manager  
 Configuration Manager utilise le compte Système local pour la plupart des opérations de site. Certaines tâches de gestion peuvent nécessiter la création et la gestion de comptes supplémentaires. Plusieurs groupes par défaut et rôles SQL Server sont créés pendant l’installation. Vous devez peut-être ajouter manuellement des comptes d’ordinateur ou d’utilisateur à ces groupes par défaut et à ces rôles SQL Server.  

 Pour plus d’informations, consultez [Comptes utilisés dans System Center Configuration Manager](../../core/plan-design/hierarchy/accounts.md).  

## <a name="privacy"></a>Confidentialité  
 Bien que les produits de gestion d'entreprise offrent de nombreux avantages, car ils permettent de gérer efficacement un grand nombre de clients, vous devez également être conscient de l'impact de ces logiciels sur la confidentialité des utilisateurs de votre organisation. System Center Configuration Manager comprend de nombreux outils pour collecter les données et surveiller les appareils. Certains outils sont susceptibles de poser des problèmes de confidentialité.  

 Par exemple, quand vous installez le client Configuration Manager, de nombreux paramètres de gestion sont activés par défaut. Par conséquent, le logiciel client envoie des informations au site Configuration Manager. Les informations du client sont stockées dans la base de données Configuration Manager et ne sont pas envoyées à Microsoft. Avant d’implémenter System Center Configuration Manager, pensez à vos exigences en matière de confidentialité.  
