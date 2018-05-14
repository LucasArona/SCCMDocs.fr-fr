---
title: Désinstaller des applications
titleSuffix: Configuration Manager
description: Désinstaller une application à l’aide de System Center Configuration Manager
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0ea3edaa-27c6-4391-9896-cd97d9c5d06d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7587fa6d96d6f8737921c9e5edae992cdd0ea614
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="uninstall-applications-with-system-center-configuration-manager"></a>Désinstaller des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Effectuez les actions suivantes pour désinstaller une application que vous avez déjà déployée.

-   Dans la page **Contenu** de l’Assistant Création d’un type de déploiement, entrez la ligne de commande permettant de désinstaller le contenu du type de déploiement.  

-   Déployez l'application en utilisant l'action de déploiement **Désinstaller**.  

> [!IMPORTANT]  
> Certains types d'application ne permettent pas la désinstallation.  

 Cette liste fournit plus d’informations sur la désinstallation d’applications :  

-   Quand vous désinstallez une application System Center Configuration Manager (Configuration Manager), toutes les applications dépendantes ne sont pas automatiquement désinstallées.  

-   Si vous déployez une application avec l’action **Désinstaller** pour un utilisateur et que l’application a été installée pour tous les utilisateurs de l’ordinateur, la désinstallation peut échouer si le compte de l’utilisateur ne dispose pas des autorisations pour désinstaller l’application.  

-   Si vous supprimez un utilisateur ou un appareil d’un regroupement sur lequel une application est déployée, l’application n’est pas automatiquement supprimée de l’appareil.  

-   Un déploiement dont l'objet est **Désinstaller** ne vérifie pas les règles de spécification. Si l'application est installée sur l'ordinateur sur lequel s'exécute le déploiement, elle sera désinstallée.  

> [!IMPORTANT]  
> Pour pouvoir déployer l'application en utilisant l'action de déploiement **Désinstaller**, vous devez au préalable supprimer les déploiements existants ou les déploiements simulés d'applications sur un regroupement.  

 Pour plus d’informations sur la manière de créer un type de déploiement, consultez [Créer des applications](../../apps/deploy-use/create-applications.md).  

 Pour plus d’informations sur le déploiement d’une application, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).  

## <a name="uninstall-an-application"></a>Désinstaller une application  

1.  Configurez le type de déploiement d'application avec la ligne de commande de désinstallation en utilisant l'une des méthodes suivantes :  

    -   Dans la page **Général** de l’Assistant Création d’un type de déploiement, sélectionnez l’option **Identifier automatiquement les informations sur ce type de déploiement à partir des fichiers d’installation**. Si les informations sont disponibles dans les fichiers d'installation, la ligne de commande de désinstallation est automatiquement ajoutée aux propriétés du type de déploiement.  

    -   Dans la page **Contenu** de l’Assistant Création d’un type de déploiement, dans le champ **Programme de désinstallation**, spécifiez la ligne de commande pour désinstaller l’application.  

        > [!NOTE]  
        >  La page **Contenu** ne s’affiche que si vous sélectionnez l’option **Spécifier manuellement les informations sur le type de déploiement** dans la page **Général** de l’Assistant Création d’un type de déploiement.  

    -   Sous l’onglet **Programmes** de la boîte de dialogue **Propriétés de <*nom_type_déploiement*>**, spécifiez la ligne de commande pour désinstaller l’application dans le champ **Programme de désinstallation**.  

2.  Déployez l’application et sélectionnez l’action de déploiement **Désinstaller** dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel.  

    > [!NOTE]  
    >  Lorsque vous sélectionnez l'action de déploiement **Désinstaller**, l'objet du déploiement est automatiquement configuré comme **Obligatoire**.  
