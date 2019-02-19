---
title: Tâches de gestion pour les applications
titleSuffix: Configuration Manager
description: Gérer les applications et les types de déploiement System Center Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: d6f66eedd60c759395126363db9e672c45993d48
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123962"
---
# <a name="management-tasks-for-system-center-configuration-manager-applications"></a>Tâches de gestion pour les applications System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Aidez-vous des informations contenues dans cet article pour gérer les applications et les types de déploiement System Center Configuration Manager.  

Pour obtenir de l’aide sur la création d’applications et de types de déploiement, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Selon le type d’application ou le type de déploiement, certaines options de gestion peuvent ne pas être disponibles.  

##  <a name="manage-applications"></a>Gérer des applications  
 Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** > **Applications**, choisissez l’application à gérer, puis une tâche de gestion.  

|Tâche|Détails|  
|----------|-------------|  
|**Gérer des comptes d'accès**|Ouvre la boîte de dialogue **Gérer les comptes d'accès** , dans laquelle vous pouvez spécifier le niveau d'accès autorisé pour le contenu associé à l'application sélectionnée.|  
|**Créer un fichier de contenu préparé**|Ouvre l' **Assistant Création du fichier de contenu préparé** qui vous aide à gérer la distribution du contenu aux points de distribution distants. Lorsque la planification et la limitation n'offrent pas de solution valide pour le point de distribution distant, vous pouvez préparer le contenu sur le point de distribution.<br /><br /> Consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Historique des révisions**|Ouvre la boîte de dialogue **Historique de révision de l’application**, qui vous permet d’afficher les propriétés des révisions de cette application, de supprimer d’anciennes révisions d’application et de restaurer d’anciennes versions de cette application.<br /><br /> Consultez [Guide pratique pour modifier et remplacer des applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Créer un type de déploiement**|Ouvre l’**Assistant Création d’un type de déploiement** qui vous permet d’ajouter un nouveau type de déploiement à l’application sélectionnée.<br /><br /> Consultez [Créer des applications](../../apps/deploy-use/create-applications.md).|  
|**Statistiques de mise à jour**|Met à jour les informations concernant les déploiements de cette application, affichées dans le nœud **Déploiements** de l'espace de travail **Surveillance** .<br /><br /> Consultez [Surveiller des applications à partir de la console System Center Configuration Manager](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Rétablir**|Rétablit une application qui a été mise hors service par le biais de la tâche de gestion **Mettre hors service**.|  
|**Mettre hors service**|Quand une application est mise hors service, elle n’est plus disponible pour le déploiement, mais l’application et les déploiements de l’application ne sont pas supprimés. Les copies existantes de l'application qui ont été installées sur les ordinateurs clients ne seront pas supprimées. Toutes les révisions de l'application seront supprimées de Configuration Manager après 60 jours. Toutefois, les copies installées de l’application ne sont pas supprimées.<br /><br /> Pour supprimer une application, vous devez tout d’abord la mettre hors service, supprimer les déploiements, supprimer les références à cette application présentes dans d’autres déploiements, puis supprimer toutes ses révisions.<br /><br /> Consultez [Modifier et remplacer des applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Exporterer**|Ouvre l’**Assistant Exportation de l’application**, qui vous permet d’exporter les applications sélectionnées dans un fichier .zip que vous pouvez ensuite archiver ou installer sur un autre site. Si vous choisissez d’exporter le contenu de l’application, un dossier avec le contenu sera créé.<br /><br /> Vous pouvez également exporter les dépendances d’applications, les relations de remplacement, les conditions et le contenu de l’application et de ses dépendances.<br /><br /> L’applet de commande Windows PowerShell **Export-CMApplication** permet de réaliser la même opération. Pour plus d’informations, consultez [Export-CMApplication](http://go.microsoft.com/fwlink/p/?LinkID=258880) dans la documentation de référence sur les applets de commande Microsoft System Center 2012 Configuration Manager SP1.|  
|**Supprimer**|Supprime l'application sélectionnée.<br /><br /> Vous ne pouvez pas supprimer une application si d'autres applications en dépendent, si elle a un déploiement actif ou si elle possède des séquences de tâches dépendantes.|  
|**Simuler un déploiement**|Ouvre l' **Assistant Simuler un déploiement d'application** , qui vous permet de tester les résultats du déploiement d'une application sans installer ou désinstaller l'application.<br /><br /> Consultez [Simuler des déploiements d’applications](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Déployer**|Ouvre l' **Assistant Déploiement logiciel** où vous pouvez déployer l'application sélectionnée sur un ensemble d'ordinateurs dans votre hiérarchie.<br /><br /> Consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).|  
|**Distribuer du contenu**|Ouvre l' **Assistant Distribuer du contenu** où vous pouvez copier le contenu de l'application sélectionnée sur les points de distribution dans votre hiérarchie.<br /><br /> Consultez [Gérer le contenu et l’infrastructure de contenu](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Voir les relations**|Affiche un graphique montrant les relations entre les applications sélectionnées et d’autres applications. Choisissez parmi :<br><br><ul><li>**Dépendance** : affiche les applications dépendantes de l’application sélectionnée, ainsi que les applications dont dépend l’application sélectionnée.</li><li>**Remplacement** : affiche les applications remplacées par l’application sélectionnée, ainsi que les applications qui remplacent l’application sélectionnée.</li><li>**Conditions globales** : affiche les conditions globales référencées par cette application.</li></ol><br /> Consultez [Modifier et remplacer des applications](../../apps/deploy-use/revise-and-supersede-applications.md) et [Créer des conditions globales](../../apps/deploy-use/create-global-conditions.md).|  

##  <a name="manage-deployment-types"></a>Gérer les types de déploiement  
 Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications**, choisissez **Applications**, puis l’application avec le type de déploiement que vous voulez gérer. Dans le volet Détails, choisissez l’onglet **Types de déploiement**, le type de déploiement que vous voulez gérer, puis une tâche de gestion.  

|Tâche|Détails|  
|----------|-------------|  
|**Augmenter la priorité**|Augmente la priorité du type de déploiement sélectionné. Les types de déploiement sont évalués dans l'ordre. Quand un type de déploiement répond aux exigences spécifiées, il est exécuté et aucun autre type de déploiement de la liste de priorité ne sera évalué.|  
|**Diminuer la priorité**|Diminue la priorité du type de déploiement sélectionné.|  
|**Supprimer**|Supprime le type de déploiement sélectionné.<br><br>Si un type de déploiement est référencé par un type de déploiement dans une autre application, vous ne pouvez pas le supprimer.<br>Pour supprimer un type de déploiement, vous devez supprimer toutes les dépendances de ce type de déploiement figurant dans d’autres types de déploiement.<br>En outre, vous devez également supprimer les révisions précédentes de toutes les applications qui ont un type de déploiement qui fait référence au type de déploiement que vous souhaitez supprimer.|  
|**Mettre à jour le contenu**|Actualise le contenu pour le type de déploiement sélectionné.<br /><br /> Quand vous démarrez cet Assistant pour un type de déploiement avec une application virtuelle, l’**Assistant Mise à jour du contenu** est lancé. Cet Assistant vous permet de modifier les options de publication et les règles de spécification de l’application virtuelle sélectionnée. Pour plus d’informations, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).<br /><br /> Lorsque vous actualisez le contenu d'un type de déploiement, une nouvelle révision de l'application est créée. Cela peut provoquer la mise à jour d'appareils clients avec la nouvelle application.|  
