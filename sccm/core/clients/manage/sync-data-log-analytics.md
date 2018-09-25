---
title: Synchroniser les données avec Log Analytics
titleSuffix: Configuration Manager
description: Synchronisez les données de Configuration Manager vers Azure Log Analytics.
ms.date: 09/04/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0fd4c36ed03f0e0b158fe637a045553dab31ade
ms.sourcegitcommit: 0d7efd9e064f9d6a9efcfa6a36fd55d4bee20059
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/06/2018
ms.locfileid: "43995346"
---
#  <a name="sync-data-from-configuration-manager-to-azure-log-analytics"></a>Synchroniser les données de Configuration Manager vers Azure Log Analytics

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1258052--> Utilisez **l’Assistant des services Azure** pour configurer une connexion de Configuration Manager vers le service cloud Azure Log Analytics. Cette connexion synchronise les données de regroupement d’appareils avec Log Analytics. 

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  

> [!TIP]
> À compter de Configuration Manager 1802, le connecteur Log Analytics n’est plus une fonctionnalité en préversion. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/pre-release-features).



## <a name="prerequisites-for-the-log-analytics-connector"></a>Prérequis pour le connecteur Log Analytics

> [!Note]  
> Cet article fait référence au *Connecteur Log Analytics*, précédemment appelé *Connecteur OMS*. Il n’existe aucune différence fonctionnelle. Pour plus d’informations, consultez [Gestion Azure - Surveillance](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

- Avant d’installer le connecteur Log Analytics dans Configuration Manager, accordez des autorisations à Configuration Manager. Accordez un *accès Contributeur* au *groupe de ressources* Azure qui contient votre espace de travail Log Analytics. Pour plus d’informations, consultez [Accorder à Configuration Manager les autorisations d’accès à Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics).  

- Installez le connecteur Log Analytics sur l’ordinateur qui héberge le [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) en mode en ligne.  

- Installez un Microsoft Monitoring Agent pour Log Analytics sur le point de connexion de service contenant le connecteur. Configurez cet agent et le connecteur pour qu’ils utilisent le même espace de travail Log Analytics. Pour plus d’informations sur l’installation de cet agent, consultez [Télécharger et installer l’agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent).  

- Après avoir installé le connecteur et l’agent, configurez Log Analytics pour utiliser les données Configuration Manager. Pour plus d'informations, consultez [Importer les regroupements Configuration Manager](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).  



## <a name="configure-the-connection-to-log-analytics"></a>Configurer la connexion à Log Analytics

Utilisez **l’Assistant des services Azure** pour configurer une connexion de Configuration Manager vers le service cloud Azure Log Analytics. Pour plus d’informations sur ce processus, consultez [Configurer des services Azure](https://docs.microsoft.com/sccm/core/servers/deploy/configure/azure-services-wizard). Sélectionnez l’option dans l’Assistant pour le **connecteur OMS**. 

> [!Note]  
> Cet article fait référence au *Connecteur Log Analytics*, précédemment appelé *Connecteur OMS*. Il n’existe aucune différence fonctionnelle. Pour plus d’informations, consultez [Gestion Azure - Surveillance](https://docs.microsoft.com/azure/monitoring/#operations-management-suite).  

Si vous avez suivi toutes les autres procédures avec succès, les informations sur l’écran **Configuration de la connexion** s’affichent automatiquement après l’importation de l’application web. Les informations pour les paramètres de connexion devraient s’afficher pour votre **Abonnement Azure**, votre **Groupe de ressources Azure** et votre **Espace de travail Operations Management Suite**.

L’Assistant se connecte au service Log Analytics en utilisant les informations que vous avez saisies. Sélectionnez les regroupements d’appareils que vous souhaitez synchroniser avec le service cloud, puis cliquez sur **Ajouter**.


## <a name="verify-the-connector-properties"></a>Vérifier les propriétés du connecteur

Après avoir lié Configuration Manager à Log Analytics, affichez les propriétés de la connexion pour ajouter ou supprimer des regroupements. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Services Azure**.  

2. Sélectionnez votre connexion Log Analytics. Dans le ruban, sélectionnez **Propriétés**.  

La page Propriétés comporte les deux onglets suivants :  

#### <a name="azure-active-directory"></a>Azure Active Directory
Cet onglet affiche les attributs suivants : 
- **Locataire**  
- **ID de client**  
- **Expiration de la clé secrète du client**  

Vérifiez aussi la date d’expiration de la clé secrète du client.

#### <a name="connection-properties"></a>Propriétés de la connexion
Cet onglet affiche les attributs suivants : 
- **Abonnement Azure**  
- **Groupe de ressources Azure**  
- **Espace de travail Log Analytics**  

Il montre également la liste des **regroupements d’appareils**. Utilisez les boutons **Ajouter** et **Supprimer** pour modifier les regroupements à synchroniser.
