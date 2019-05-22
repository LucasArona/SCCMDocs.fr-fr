---
title: Créer un média de séquence de tâches
titleSuffix: Configuration Manager
description: Créez un média de séquence de tâches pour déployer un système d’exploitation sur un ordinateur de destination dans un environnement Configuration Manager.
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 101cee8ed63cacfc41481b2df69b42e1760d8837
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082818"
---
# <a name="create-task-sequence-media"></a>Créer un média de séquence de tâches

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser un média pour capturer une image de système d’exploitation sur un ordinateur de référence ou pour déployer un système d’exploitation sur un ordinateur de destination dans votre environnement Configuration Manager. Le média que vous créez peut être un CD, un ensemble DVD, ou un disque mémoire flash USB.  

Les médias servent principalement à déployer des systèmes d’exploitation sur des ordinateurs de destination qui ne disposent pas de connexion réseau ou qui possèdent une connexion à faible bande passante au site Configuration Manager. Cependant, il est également possible de les utiliser pour lancer un déploiement de système d’exploitation en dehors d’un système d’exploitation Windows. Cette méthode est utile s’il n’y a pas de système d’exploitation, si le système d’exploitation ne fonctionne pas ou s’il faut repartitionner le disque dur.  

Le média de déploiement inclut le média de démarrage, le média autonome et le média préparé. Le contenu du média varie selon le type de média utilisé. Par exemple, un média autonome contient la séquence de tâches qui déploie le système d’exploitation. D’autres types de médias récupèrent les séquences de tâches auprès du point de gestion.  

> [!IMPORTANT]  
> Pour créer un média de séquence de tâches, vous devez être administrateur sur l’ordinateur où s’exécute la console Configuration Manager. Dans le cas contraire, il vous sera demandé d’entrer des informations d’identification d’administration lors du lancement de l’Assistant Création d’un média de séquence de tâches.  


## <a name="BKMK_PlanCaptureMedia"></a> Média de capture

Un média de capture permet de capturer une image de système d’exploitation sur un ordinateur de référence. Il contient l’image de démarrage qui démarre l’ordinateur de référence et la séquence de tâches qui capture l’image de système d’exploitation.

Pour plus d’informations sur la création de médias de capture, voir [Créer un média de capture](/sccm/osd/deploy-use/create-capture-media).  


## <a name="BKMK_PlanBootableMedia"></a> Média de démarrage

Un média de démarrage contient les composants suivants :

- l’image de démarrage ;
- des [commandes de prédémarrage](/sccm/osd/understand/prestart-commands-for-task-sequence-media) facultatives et les fichiers associés ;
- les binaires Configuration Manager.

Au démarrage, l’ordinateur de destination se connecte au réseau et récupère la séquence de tâches, l’image de système d’exploitation et tout autre contenu nécessaire sur le réseau. Comme la séquence de tâches ne se trouve pas sur le média, il est possible de modifier la séquence de tâches ou le contenu sans avoir à recréer le média.  

> [!IMPORTANT]  
> Les packages qui se trouvent sur le média de démarrage ne sont pas chiffrés. Prenez les mesures de sécurité qui s’imposent (par exemple, ajoutez un mot de passe au média), pour protéger le contenu des packages contre les utilisateurs non autorisés.  

Pour plus d’informations sur la création d’un média de démarrage, voir [Créer un média de démarrage](/sccm/osd/deploy-use/create-bootable-media).  


## <a name="BKMK_PlanPrestagedMedia"></a> Média préparé

Un média préparé permet d’appliquer un média de démarrage et une image de système d’exploitation à un disque dur avant le processus de déploiement. Il s’agit d’un fichier image Windows (WIM). Il peut être installé sur un système nu par le fabricant ou dans un centre intermédiaire non relié à l’environnement Configuration Manager de production.  

Un média préparé contient l’image de démarrage servant à démarrer l’ordinateur de destination et l’image de système d’exploitation appliquée à l’ordinateur de destination. Vous pouvez aussi spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. La séquence de tâches qui déploie le système d’exploitation n’est pas incluse dans le média. Lors du déploiement d’une séquence de tâches utilisant un média préparé, le client vérifie d’abord que le contenu du cache local de la séquence de tâches est valide. Si ce contenu est introuvable ou a été modifié, le client le télécharge à partir d’un point de distribution ou d’un homologue.  

Un média préparé est appliqué au disque dur d'un nouvel ordinateur avant que l'ordinateur soit envoyé à l'utilisateur final. Pour son premier démarrage après application du média préparé, l’ordinateur démarre dans Windows PE. Il se connecte à un point de gestion pour localiser la séquence de tâches qui effectue le processus de déploiement de système d’exploitation.  

> [!IMPORTANT]  
> Les packages qui se trouvent sur le média préparé ne sont pas chiffrés. Prenez les mesures de sécurité qui s’imposent (par exemple, ajoutez un mot de passe au média), pour protéger le contenu des packages contre les utilisateurs non autorisés.  

Pour plus d’informations sur la création d’un média préparé, voir [Créer un média préparé](/sccm/osd/deploy-use/create-prestaged-media).  


## <a name="BKMK_PlanStandaloneMedia"></a> Média autonome

Un média autonome contient tout ce qui est nécessaire au déploiement du système d’exploitation, à savoir la séquence de tâches et tout autre contenu requis. Dans la mesure où tous ces éléments sont stockés sur le média autonome, l’espace disque requis est plus important que pour d’autres types de médias.  

Pour plus d’informations sur la création d’un média autonome, voir [Créer un média autonome](/sccm/osd/deploy-use/create-stand-alone-media).  


## <a name="considerations-when-using-https"></a>Considérations sur le protocole HTTPS

Si vous configurez vos points de gestion et de distribution de façon à utiliser le protocole HTTPS, créez un média de démarrage et un média préparé sur le site principal et non sur le site d’administration centrale. Prenez également en compte les points suivants pour choisir entre une configuration comme média dynamique ou comme média basé sur le site :  

- Pour configurer le média comme média dynamique, il faut que tous les sites principaux possèdent l’autorité de certification racine du site ayant servi à la création du média. Vous pouvez importer l'autorité de certification racine sur tous les sites principaux de votre hiérarchie.  

- Quand les sites principaux de votre hiérarchie Configuration Manager utilisent des autorités de certification racines différentes, vous devez utiliser sur chaque site des médias basés sur le site.  
