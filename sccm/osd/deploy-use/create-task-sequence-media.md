---
title: Créer un média de séquence de tâches
titleSuffix: Configuration Manager
description: Créez un média de séquence de tâches, par exemple un CD, pour déployer un système d’exploitation sur un ordinateur de destination dans votre environnement Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e3aa7a1acdd6378e41afe24c869a8ffa898a916b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122609"
---
# <a name="create-task-sequence-media-with-system-center-configuration-manager"></a>Créer un média de séquence de tâches avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser un média pour capturer une image de système d’exploitation à partir d’un ordinateur de référence ou pour déployer un système d’exploitation sur un ordinateur de destination dans votre environnement System Center Configuration Manager. Le média que vous créez peut être un CD, un ensemble DVD, ou un disque mémoire flash USB.  

 Les médias sont utilisés principalement pour déployer des systèmes d’exploitation sur des ordinateurs de destination qui ne disposent pas de connexion réseau ou qui possèdent une connexion avec une faible bande passante vers votre site Configuration Manager. Toutefois, un média de déploiement est également utilisé pour démarrer un déploiement de système d'exploitation en dehors d'un système d'exploitation Windows existant. Cette seconde utilisation du média de déploiement est importante pour les cas où aucun système d'exploitation n'est installé sur l'ordinateur de destination, le système d'exploitation n'est pas un état exécutable ou l'utilisateur administratif souhaite repartitionner le disque dur sur l'ordinateur de destination.  

 Le média de déploiement inclut le média de démarrage, le média autonome et le média préparé. Le contenu du média de déploiement varie selon le type de média que vous utilisez. Par exemple, le média autonome contient la séquence de tâches qui déploie le système d'exploitation, tandis que les autres types de médias extraient les séquences de tâches du point de gestion.  

> [!IMPORTANT]  
>  Pour créer un média de séquence de tâches, vous devez être administrateur sur l’ordinateur à partir duquel vous exécutez la console Configuration Manager. Si vous n’êtes pas administrateur, vous êtes invité à entrer les informations d’identification de l’administrateur lors du démarrage de l’Assistant Création d’un média de séquence de tâches.  

##  <a name="BKMK_PlanCaptureMedia"></a> Média de capture pour des images de système d’exploitation  
 Un média de capture vous permet de capturer une image de système d'exploitation à partir d'un ordinateur de référence. Un média de capture contient l'image de démarrage qui démarre l'ordinateur de référence et la séquence de tâches qui capture l'image du système d'exploitation. Pour plus d’informations sur la façon de créer un média de capture, consultez [Créer un média de capture avec System Center Configuration Manager](create-capture-media.md).  

##  <a name="BKMK_PlanBootableMedia"></a> Déploiements de systèmes d’exploitation de média de démarrage  
 Un média de démarrage contient uniquement l’image de démarrage, les [commandes de prédémarrage](../understand/prestart-commands-for-task-sequence-media.md) facultatives et leurs fichiers requis, ainsi que des fichiers binaires Configuration Manager. Au démarrage de l'ordinateur de destination, il se connecte au réseau et extrait la séquence de tâches, l'image du système d'exploitation et tout autre contenu requis à partir du réseau. Étant donné que la séquence de tâches ne se trouve pas sur le média, vous pouvez modifier la séquence de tâches ou le contenu sans avoir à recréer le média.  

> [!IMPORTANT]  
>  Les packages sur le média de démarrage ne sont pas chiffrés. L'utilisateur administratif doit prendre les mesures de sécurité appropriées, telles que l'ajout d'un mot de passe au média, afin de s'assurer que le contenu du package est protégé contre les utilisateurs non autorisés.  

 Pour plus d’informations sur la création d’un média de démarrage, consultez [Créer un média de démarrage](create-bootable-media.md).  

##  <a name="BKMK_PlanPrestagedMedia"></a> Déploiements de systèmes d’exploitation de média préparé  
 Un média préparé vous permet de préparer un média de démarrage et une image du système d'exploitation sur un disque dur avant de procéder au déploiement. Le média préparé est un fichier WIM (Windows Imaging Format) qui peut être installé sur un ordinateur nu par le fabricant ou dans un centre de reclassement d’entreprise qui n’est pas connecté à l’environnement Configuration Manager.  

 Un média préparé contient l'image de démarrage utilisée pour démarrer l'ordinateur de destination et l'image du système d'exploitation qui est appliquée à l'ordinateur de destination. Vous pouvez aussi spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. La séquence de tâches qui déploie le système d'exploitation n'est pas incluse dans le média. Quand vous déployez une séquence de tâches qui fait appel à un média préparé, le client vérifie tout d’abord la validité du contenu du cache local de la séquence de tâches. Si ce contenu est introuvable ou a été modifié, le client télécharge le contenu auprès du point de distribution.  

 Un média préparé est appliqué au disque dur d'un nouvel ordinateur avant que l'ordinateur soit envoyé à l'utilisateur final. Lorsque l'ordinateur démarre pour la première fois après l'application du média préparé, l'ordinateur démarre Windows PE et se connecte à un point de gestion pour localiser la séquence de tâches qui finalise le processus de déploiement du système d'exploitation.  

> [!IMPORTANT]  
>  Les packages sur le média préparé ne sont pas chiffrés. L'utilisateur administratif doit prendre les mesures de sécurité appropriées, telles que l'ajout d'un mot de passe au média, afin de s'assurer que le contenu du package est protégé contre les utilisateurs non autorisés.  

 Pour plus d’informations sur la création d’un média préparé, consultez [Créer un média préparé](create-prestaged-media.md).  

##  <a name="BKMK_PlanStandaloneMedia"></a> Déploiements de systèmes d’exploitation de média autonome  
 Un média autonome contient tout ce qui est nécessaire au déploiement du système d'exploitation. Cela inclut la séquence de tâches et tout autre contenu requis. Étant donné que tous les éléments requis pour déployer le système d'exploitation sont stockés sur le média autonome, l'espace disque requis pour le média autonome est beaucoup plus important que l'espace disque requis pour d'autres types de média.  

 Pour plus d’informations sur la création d’un média autonome, consultez [Créer un média autonome](create-stand-alone-media.md).  

## <a name="media-considerations-when-using-site-systems-configured-for-https"></a>Considérations relatives au média lors de l’utilisation de systèmes de site configurés pour HTTPS  
 Lorsque votre point de gestion et vos points de distribution sont configurés pour utiliser la communication HTTPS, vous devez créer un média de démarrage et un média préparé sur le site principal et non sur le site d'administration centrale. Prenez également en compte les remarques suivantes pour déterminer si le média doit être configuré comme média dynamique ou comme média basé sur le site :  

-   Pour configurer le média comme média dynamique, tous les sites principaux doivent connaître l'autorité de certification racine du site à partir duquel vous avez créé le média. Vous pouvez importer l'autorité de certification racine sur tous les sites principaux de votre hiérarchie.  

-   Quand les sites principaux de votre hiérarchie Configuration Manager utilisent des autorités de certification racines différentes, vous devez utiliser sur chaque site des médias basés sur le site.  
