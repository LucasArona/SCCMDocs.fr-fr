---
title: Rôles de système de site pour les clients
titleSuffix: Configuration Manager
description: Déterminez les rôles de système de site pour les clients dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: eac38757ed2147d664b3bdbf2f7e0eb11947dcac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334073"
---
# <a name="determine-the-site-system-roles-for-system-center-configuration-manager-clients"></a>Déterminer les rôles de système de site pour les clients System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique peut vous aider à déterminer les rôles de système de site dont vous avez besoin pour déployer les clients Configuration Manager :  

 Pour plus d’informations sur l’emplacement d’installation des rôles de système de site requis dans la hiérarchie, consultez [Concevoir une hiérarchie de sites pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

 Pour plus d’informations sur l’installation et la configuration des rôles de système de site dont vous avez besoin, consultez [Installer des rôles de système de site](../../../../core/servers/deploy/configure/install-site-system-roles.md).  

##  <a name="determine-if-you-need-a-management-point"></a>Déterminer si vous avez besoin d’un point de gestion  
 Par défaut, tous les ordinateurs clients Windows utilisent un point de distribution pour installer le client Configuration Manager. En cas d’indisponibilité du point de distribution, ils peuvent basculer sur un point de gestion. Toutefois, vous pouvez installer des clients Windows sur les ordinateurs à partir d’une autre source, en utilisant la propriété de ligne de commande CCMSetup **/source:<chemin_accès\>**. Par exemple, ceci peut être approprié si vous installez des clients sur Internet. Un autre scénario est d’éviter l’envoi des paquets réseau entre les ordinateurs et le point de gestion lors de l’installation du client, par exemple car un pare-feu bloque les ports nécessaires ou que vous disposez d’une connexion à faible bande passante. Tous les clients doivent cependant communiquer avec un point de gestion à affecter à un site et pour être gérés par Configuration Manager.  

 Pour plus d’informations sur la propriété de ligne de commande CCMSetup **/source:<chemin_accès\>**, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

 Quand vous installez plusieurs points de gestion dans la hiérarchie, les clients se connectent automatiquement à une seul point en fonction des forêts auxquelles ils appartiennent et de leur emplacement réseau. Vous ne pouvez pas installer plusieurs points de gestion dans un site secondaire.  

 Les ordinateurs clients Mac et les clients d’appareil mobile que vous inscrivez à l’aide de Configuration Manager nécessitent dans tous les cas un point de gestion pour l’installation du client. Ce point de gestion doit se trouver dans un site principal. Il doit en outre être configuré pour prendre en charge les appareils mobiles et doit accepter les connexions de clients via Internet. Ces clients ne peuvent pas utiliser les points de gestion des sites secondaires ni se connecter aux points de gestion d'autres sites principaux.  

##  <a name="determine-if-you-need-a-fallback-status-point"></a>Déterminer si un point d’état de secours est nécessaire  
 Vous pouvez utiliser un point d’état de secours pour surveiller le déploiement du client pour les ordinateurs Windows. Vous pouvez également identifier les ordinateurs clients Windows qui ne sont pas gérés car ils ne peuvent pas communiquer avec un point de gestion. Les ordinateurs Mac, les appareils mobiles inscrits par le biais de Configuration Manager et les appareils mobiles gérés à l’aide du connecteur du serveur Exchange Server n’utilisent pas de point d’état de secours.  

 Un point d'état de secours n'est pas nécessaire pour surveiller l'activité et l'intégrité du client.  

 Le point d’état de secours communique toujours avec les clients via HTTP, qui utilise des connexions non authentifiées et envoie les données en texte clair. Ainsi, le point d'état de secours est vulnérable aux attaques, en particulier lorsqu'il est utilisé avec la gestion de clients basés sur Internet. Pour réduire la surface d'attaque, dédiez toujours un serveur à l'exécution du point d'état de secours et n'installez aucun autre rôle de système de site sur le même serveur, dans un environnement de production.  

 Installez un point d’état de secours si tout ce qui suit s’applique :  

-   Vous souhaitez que les erreurs de communication avec les clients des ordinateurs Windows soient envoyées au site, même si ces ordinateurs clients ne peuvent pas communiquer avec un point de gestion.  

-   Vous souhaitez utiliser les rapports de déploiement de client Configuration Manager, qui contiennent les données envoyées par le point d’état de secours.  

-   Vous disposez d'un serveur dédié pour ce rôle de système de site et avez en outre mis en place des mesures de sécurité pour renforcer la protection du serveur contre les attaques.  

-   Les avantages que présentent l'utilisation d'un point d'état de secours compensent les risques de sécurité liés aux connexions non authentifiées et aux transferts de texte en clair, sur du trafic HTTP.  

 N’installez pas un point d’état de secours si les risques de sécurité liés à l’exécution d’un site web avec des connexions non authentifiées et des transferts de texte en clair dépassent les avantages de l’identification des problèmes de communication du client.  

##  <a name="determine-whether-you-need-a-reporting-services-point"></a>Déterminer si un point Reporting Services est nécessaire  
 Configuration Manager fournit de nombreux rapports pour vous aider à surveiller l’installation, l’attribution et la gestion des clients sur la console Configuration Manager. Certains rapports sur le déploiement du client exigent que des clients soient attribués à un point d'état de secours.  

 Même si les rapports ne sont pas nécessaires pour déployer des clients et si vous pouvez consulter des informations sur le déploiement dans la console Configuration Manager ou des informations détaillées dans les fichiers journaux du client, les rapports du client donnent des informations importantes pour vous aider à surveiller et à résoudre les problèmes de déploiement du client.  

##  <a name="determine-if-you-need-an-enrollment-point-and-an-enrollment-proxy-point"></a>Déterminer si un point d’inscription et un point proxy d’inscription sont nécessaires  
 Configuration Manager a besoin du point d’inscription et du point proxy d’inscription pour inscrire les appareils mobiles et les certificats des ordinateurs Mac. Ces rôles de système de site ne sont pas nécessaires dans les trois cas suivants : si vous avez l’intention de gérer les appareils mobiles à l’aide du connecteur du serveur Exchange Server, si vous installez le client d’appareil mobile hérité (par exemple Windows CE), ou si vous demandez et installez le certificat client sur des ordinateurs Mac indépendamment de Configuration Manager.  

##  <a name="determine-if-you-need-a-distribution-point"></a>Déterminer si un point de distribution est nécessaire  
 Vous n’avez pas besoin d’un point de distribution pour installer les clients Configuration Manager sur les ordinateurs Windows. Cependant, par défaut, Configuration Manager utilise un point de distribution pour installer les fichiers sources du client sur ces ordinateurs. Si nécessaire, il peut également télécharger ces fichiers à partir d’un point de gestion. Les points de distribution ne sont pas utilisés pour installer des clients d’appareils mobiles qui sont inscrits auprès de Configuration Manager, mais ils sont utilisés si vous installez le client hérité de l’appareil mobile. Si vous installez le client Configuration Manager dans le cadre d’un déploiement de système d’exploitation, l’image du système d’exploitation est stockée et récupérée à partir d’un point de distribution.  

 Bien que les points de distribution ne soient pas indispensables pour installer la plupart des clients Configuration Manager, vous en avez besoin pour installer des logiciels comme des applications et des mises à jour logicielles sur les clients.  

##  <a name="determine-if-you-need-an-application-catalog-website-point-and-an-application-catalog-web-services-point"></a>Déterminer si un point du site web du catalogue des applications et un point de service web du catalogue des applications sont nécessaires  
 Le point du site web du catalogue des applications et le point de service web du catalogue des applications ne sont pas nécessaires pour le déploiement du client. Cependant, il peut être utile de les installer dans le cadre du processus de déploiement des clients, pour que les utilisateurs puissent effectuer les actions suivantes dès que le client Configuration Manager est installé sur les ordinateurs Windows :  

-   Réinitialiser les appareils mobiles.  

-   Recherchez et installez des applications à partir du catalogue d'applications.  

-   Déployez des applications auprès des utilisateurs et des appareils en utilisant l'objet de déploiement **Disponible**.  

##  <a name="determine-whether-you-require-a-cloud-management-gateway-connector-point"></a>Déterminer si un point de connecteur de passerelle de gestion cloud est nécessaire 

Vous avez besoin d’un point de connecteur de passerelle de gestion cloud si vous configurez une [passerelle de gestion cloud](/sccm/core/clients/manage/setup-cloud-management-gateway) pour [gérer les clients sur Internet](/sccm/core/clients/manage/manage-clients-internet).


 