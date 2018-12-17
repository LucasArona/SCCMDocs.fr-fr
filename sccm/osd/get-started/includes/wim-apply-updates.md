---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: include
ms.date: 11/27/2018
ms.openlocfilehash: c91cf0abb8cb79fe92e34b6b234a4c8264af75ab
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456938"
---
##  <a name="BKMK_OSImagesApplyUpdates"></a> Appliquer des mises à jour logicielles à une image  

> [!Note]  
> Cette section s’applique aux **images de système d’exploitation** et aux **packages de mise à niveau de système d’exploitation**. Elle utilise le terme général « image » pour faire référence au fichier image Windows (WIM). Ces deux objets ont un fichier WIM qui contient les fichiers d’installation de Windows. Les mises à jour logicielles sont applicables aux fichiers des deux objets. Le comportement de ce processus est le même pour les deux objets.  

Chaque mois, de nouvelles mises à jour logicielles sont applicables à l’image. Avant de pouvoir appliquer des mises à jour logicielles à cette image, les conditions préalables suivantes doivent être réunies : 

- Une infrastructure des mises à jour logicielles  
- Des mises à jour logicielles correctement synchronisées  
- Les mises à jour logicielles ont été téléchargées dans la bibliothèque de contenu sur le serveur de site  

Pour plus d’informations, consultez [Déployer des mises à jour logicielles](/sccm/sum/deploy-use/deploy-software-updates).  

Appliquez les mises à jour logicielles applicables à une image selon un calendrier défini. Ce processus est parfois appelé *maintenance hors connexion*. En fonction du calendrier, Configuration Manager applique les mises à jour logicielles sélectionnées à l’image. Il peut également redistribuer de l’image mise à jour aux points de distribution. 

La base de données du site stocke les informations sur l’image, y compris les mises à jour logicielles qui ont été appliquées au moment de l’importation. Les mises à jour logicielles que vous appliquez à l’image depuis son ajout initial sont également stockées dans la base de données du site. Lorsque vous démarrez l’Assistant pour appliquer les mises à jour logicielles, il récupère la liste des mises à jour logicielles applicables que le site n’a pas encore appliquées à l’image. Configuration Manager copie les mises à jour logicielles que vous sélectionnez à partir de la bibliothèque de contenu sur le serveur de site. Il applique ensuite les mises à jour logicielles à l’image.  


### <a name="servicing-process"></a>Processus de maintenance  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Images du système d’exploitation** ou **Packages de mise à niveau du système d’exploitation**.  

2.  Sélectionnez l’objet auquel appliquer les mises à jour logicielles.  

3.  Dans le ruban, sélectionnez **Planifier les mises à jour** pour démarrer l’Assistant.  

4.  Dans la page **Choisir des mises à jour**, sélectionnez les mises à jour logicielles à appliquer à l’image. La liste des mises à jour peut mettre un certain temps à apparaître dans l’Assistant. Utilisez le **filtre** pour rechercher des chaînes dans les métadonnées. Utilisez la liste déroulante **Architecture système** pour filtrer sur **X86**, **X64** ou **Toutes**. Vous pouvez sélectionner une, plusieurs ou l’ensemble des mises à jour dans la liste. Lorsque vous avez fini de sélectionner les mises à jour, sélectionnez **Suivant**.  

5.  Sur la page **Définir le calendrier** , spécifiez les paramètres suivants, puis cliquez sur **Suivant**.  

    a.  **Calendrier** : spécifiez le calendrier d’application des mises à jour logicielles à l’image par le site.  

    b.  **Continuer en cas d’erreur** : sélectionnez cette option pour continuer à appliquer les mises à jour logicielles à l’image même si une erreur survient.  

    c.  **Mettre à jour les points de distribution avec l’image** : sélectionnez cette option pour mettre à jour l’image sur les points de distribution après l’application des mises à jour logicielles par le site.  

6.  Exécutez l’Assistant Planification des mises à jour.  

> [!NOTE]  
>  Pour réduire la taille de la charge utile, la maintenance des packages de mise à niveau du système d’exploitation et des images de système d’exploitation supprime l’ancienne version.  


### <a name="servicing-operations"></a>Opérations de maintenance

Dans la console Configuration Manager, dans le nœud **Images du système d’exploitation** ou **Packages de mise à niveau du système d’exploitation**, ajoutez les colonnes suivantes dans la vue :
- **Date des mises à jour planifiées** : cette propriété indique la planification suivante que vous avez définie.  
- **État des mises à jour planifiées** : cette propriété indique l’état. Par exemple, **Réussi** ou **En cours**.  

Sélectionnez un objet image spécifique, puis passez à l’onglet **État des mises à jour** dans le volet d’informations. Cet onglet affiche la liste des mises à jour dans l’image. 

Sélectionnez un objet image spécifique, puis **Propriétés** dans le ruban. L’onglet **Mises à jour installées** affiche la liste des mises à jour dans l’image. L’onglet **Maintenance** est une vue en lecture seule du calendrier de maintenance actuel et des mises à jour que vous avez planifiées. 

Lorsque l’état est **En cours**, vous pouvez sélectionner **Annuler les mises à jour planifiées** dans le ruban. Cette action annule le processus de maintenance actif. 

Pour dépanner ce processus, consultez les fichiers **OfflineServicingMgr.log** et **dism.log** sur le serveur de site. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files).


### <a name="bkmk_servicing-drive"></a> Spécifier le lecteur pour la maintenance des images de système d’exploitation hors connexion  
<!--1358924-->

À compter de la version 1810, spécifiez le lecteur utilisé par Configuration Manager durant la maintenance hors connexion des images du système d’exploitation. Ce processus peut consommer une grande quantité d’espace disque avec des fichiers temporaires. Cette option vous donne la possibilité de sélectionner le lecteur à utiliser. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Dans le ruban, cliquez sur **Configurer les composants de site** et sélectionnez **Déploiement du système d’exploitation**.  

2. Sous l’onglet **Maintenance hors connexion**, spécifiez l’option correspondant à **Lecteur local à utiliser pour la maintenance hors connexion des images**.  

Par défaut, ce paramètre a la valeur **Automatique**. Avec cette valeur, Configuration Manager sélectionne le lecteur sur lequel il est installé. 

Si vous sélectionnez un lecteur qui n’existe pas sur le serveur de site, Configuration Manager se comporte comme si vous sélectionnez **Automatique**. 

Durant l’installation hors connexion, Configuration Manager stocke les fichiers temporaires dans le dossier `<drive>:\ConfigMgr_OfflineImageServicing`. Il monte également l’image du système d’exploitation dans ce dossier. 

