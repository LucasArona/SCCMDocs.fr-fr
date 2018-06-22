---
title: Prise en charge du serveur proxy
titleSuffix: Configuration Manager
description: En savoir plus sur la prise en charge de System Center Configuration Manager pour les serveurs proxy utilisés par les clients et les serveurs de système de site.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 9123a87a-0b6f-43c7-b5c2-fac5d09686b1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 480ab29bbd97f2cdc173019b1b3cccd90403d011
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337817"
---
# <a name="proxy-server-support-in-system-center-configuration-manager"></a>Prise en charge du serveur proxy dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les clients aussi bien que les serveurs de système de site System Center Configuration Manager peuvent utiliser un serveur proxy.  

## <a name="site-system-servers"></a>Serveurs de système de site  
Quand les rôles de système de site doivent se connecter à Internet, vous pouvez les configurer pour qu’ils utilisent un serveur proxy.  

-   Un ordinateur qui héberge un serveur de système de site prend en charge une configuration de serveur proxy unique partagée par tous les rôles de système de site sur ce même ordinateur. Si vous avez besoin de serveurs proxy distincts pour les différents rôles ou les différentes instances d’un rôle, vous devez placer ces rôles sur des serveurs de système de site distincts.  

-   Quand vous configurez de nouveaux paramètres de serveur proxy pour un serveur de système de site qui possède déjà une configuration de serveur proxy, la configuration d’origine est remplacée.  

-   Les connexions au serveur proxy utilisent le compte **Système** de l’ordinateur qui héberge le rôle de système de site.  

Les rôles de système de site suivants se connectent à Internet et peuvent nécessiter un serveur proxy.  À une exception près, les rôles de système de site qui peuvent utiliser un proxy le font sans aucune configuration supplémentaire. Cette exception concerne le point de mise à jour logicielle. La liste suivante contient des informations sur les configurations supplémentaires exigées par un point de mise à jour logicielle :  

**Point de synchronisation Asset Intelligence** : ce rôle de système de site se connecte à Microsoft et utilise une configuration de serveur proxy sur l’ordinateur hébergeant le point de synchronisation Asset Intelligence.  

**Point de distribution cloud** : pour configurer un serveur proxy pour un point de distribution cloud, configurez le proxy sur le site principal qui gère le point de distribution cloud.  

Pour cette configuration, le serveur de site principal :  

-   doit pouvoir se connecter à Microsoft Azure pour configurer le contenu, le surveiller et le distribuer au point de distribution ;  

-   utilise le compte Système de cet ordinateur pour établir la connexion ;  

-   utilise le navigateur web par défaut de cet ordinateur.  

Vous ne pouvez pas configurer un serveur proxy sur le point de distribution cloud dans Microsoft Azure.  

**Point de connexion cloud** : ce rôle de système de site se connecte au service cloud de Configuration Manager pour télécharger des mises à jour de version de Configuration Manager, et utilise un serveur proxy configuré sur l’ordinateur hébergeant le point de connexion de service.  

**Connecteur du serveur Exchange Server** : ce rôle de système de site se connecte à un serveur Exchange Server et utilise une configuration de serveur proxy sur l’ordinateur hébergeant le connecteur Exchange Server.  

**Point de connexion de service** : ce rôle de système de site se connecte à Microsoft Intune et utilise une configuration de serveur proxy sur l’ordinateur hébergeant le point de connexion de service.  

**Point de mise à jour logicielle** : ce rôle de système de site peut utiliser le proxy quand il se connecte à Microsoft Update pour télécharger des correctifs et synchroniser les informations sur les mises à jour. Les points de mise à jour logicielle utilisent un proxy uniquement pour les options suivantes, quand vous activez cette option au moment de la configuration du point de mise à jour logicielle :  

-   **Utiliser un serveur proxy lors de la synchronisation des mises à jour logicielles**  

-   **Utiliser un serveur proxy lors du téléchargement du contenu avec des règles de déploiement automatiques** (Bien que disponible, ce paramètre n’est pas utilisé par les points de mise à jour logicielle sur des sites secondaires).  

Configurez les paramètres du serveur proxy dans la page Point de mise à jour logicielle actif de l’Assistant Ajout des rôles de système de site ou sous l’onglet **Général** des **Propriétés du composant du point de mise à jour logicielle**.  

-   Les paramètres du serveur proxy sont associés uniquement au point de mise à jour logicielle au niveau du site.  

-   Les options de serveur proxy sont disponibles uniquement quand un serveur proxy est déjà configuré pour le serveur de système de site qui héberge le point de mise à jour logicielle.  

> [!NOTE]  
>  Par défaut, le compte **Système** pour le serveur sur lequel une règle de déploiement automatique a été créée est utilisé pour se connecter à Internet et télécharger les mises à jour logicielles lors de l’exécution des règles de déploiement automatique.  
>   
>  Si ce compte n’a pas accès à Internet, les mises à jour logicielles ne peuvent pas être téléchargées et l’entrée suivante est consignée dans le fichier ruleengine.log : **Échec du téléchargement de la mise à jour sur Internet. Erreur = 12007.**  

#### <a name="to-set-up-the-proxy-server-for-a-site-system-server"></a>Pour configurer le serveur proxy d’un serveur de système de site  

1.  Dans la console Configuration Manager, choisissez **Administration**, développez **Configuration du site**, puis choisissez **Serveurs et rôles de système de site**.  

2.  Sélectionnez le serveur de système de site à modifier, puis dans le volet d’informations, cliquez avec le bouton droit sur **Système de site**, puis choisissez **Propriétés**.  

3.  Dans Propriétés du système de site, sélectionnez l’onglet **Proxy**, puis configurez les paramètres de proxy de ce serveur de site principal.  

4.  Cliquez sur **OK** pour enregistrer la nouvelle configuration de serveur proxy.  
