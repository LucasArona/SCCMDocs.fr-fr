---
title: 'Surveiller les clients '
titleSuffix: Configuration Manager
description: Obtenez des instructions détaillées sur la façon de surveiller les clients dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 976aeaacfadfa7d2f189f20ab001486d486b764e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335879"
---
# <a name="how-to-monitor-clients-in-system-center-configuration-manager"></a>Guide pratique pour surveiller des clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


 Une fois l’application cliente System Center Configuration Manager installée sur les ordinateurs et appareils Windows de votre site, vous pouvez surveiller leur intégrité et leur activité dans la console Configuration Manager.  

##  <a name="bkmk_about"></a> À propos du statut du client  
 Configuration Manager présente les types d’informations suivants sous forme d’état du client :  

-   **État en ligne du client** : à compter de la version 1602 de Configuration Manager, cet état indique si l’ordinateur est en ligne ou non. Un ordinateur est considéré comme étant en ligne s’il est connecté au point de gestion qui lui est affecté.  Pour indiquer que le client est en ligne, il envoie des messages de type ping au point de gestion. Si le point de gestion n’a pas reçu de message après environ 5 minutes, le client est considéré comme étant hors connexion.  

-   **Activité du client** : cet état indique si le client a été activement en contact avec Configuration Manager au cours des 7 derniers jours. Si le client n’a pas demandé de mise à jour de la stratégie, a envoyé un message de pulsation, ou a envoyé un inventaire matériel dans les 7 jours, il est considéré comme inactif.  

-   **Intégrité du client** : cet état indique la réussite de l’évaluation périodique de l’exécution du client Configuration Manager sur l’ordinateur.  L’évaluation vérifie l’ordinateur et peut corriger certains problèmes détectés. Pour plus d’informations, consultez [Vérifications et corrections effectuées par la fonction d’intégrité du client](#BKMK_ClientHealth).  

     Sur les ordinateurs qui exécutent Windows 7, l'intégrité du client s'exécute en tant que tâche planifiée. Sur les systèmes d'exploitation ultérieurs, l'intégrité du client s'exécute automatiquement pendant la fenêtre de maintenance de Windows.  

     Vous pouvez configurer la mise à jour de manière à ne pas l'exécuter sur des ordinateurs spécifiques, par exemple, sur un serveur essentiel pour l'entreprise. En outre, si vous souhaitez évaluer d’autres éléments, vous pouvez utiliser les paramètres de compatibilité de Configuration Manager pour fournir une solution complète de surveillance de l’intégrité, de l’activité et de la conformité globales des ordinateurs de votre organisation. Pour plus d’informations sur les paramètres de compatibilité, consultez [Planifier et configurer les paramètres de compatibilité dans System Center Configuration Manager](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

##  <a name="bkmk_indStatus"></a> Surveiller le statut de clients individuels  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Appareils** ou choisissez un regroupement sous **Regroupements d’appareils**.  

     À compter de la version 1602 de Configuration Manager, les icônes au début de chaque ligne indiquent le statut de connexion de l’appareil :  

    |||  
    |-|-|  
    |![icône de statut de connexion des clients](../../../core/clients/manage/media/online-status-icon.png)|L’appareil est en ligne.|  
    |![icône de statut déconnecté des clients](../../../core/clients/manage/media/offline-status-icon.png)|L’appareil est hors connexion.|  
    |![icône de statut inconnu des clients](../../../core/clients/manage/media/unknown-status-icon.png)|Le statut de connexion est inconnu.|  
    |![client non installé](../../../core/clients/manage/media/client-not-installed.png)|Le client n’est pas installé sur l’appareil.|  

2.  Pour obtenir un statut de connexion plus détaillé, ajoutez les informations de statut de connexion du client à l’affichage du périphérique, en double-cliquant sur l’en-tête de colonne et en cliquant sur les champs de statut de connexion que vous souhaitez ajouter. Les colonnes que vous pouvez ajouter sont les suivantes :  

    -   **Statut de connexion de l’appareil** indique si le client est actuellement en ligne ou hors connexion. (Il s’agit des mêmes informations que celles fournies par les icônes).  

    -   **Heure de la dernière connexion** indique à quel moment le statut de connexion du client est passé en ligne.  

    -   **Heure de la dernière déconnexion** indique à quel moment le statut est passé hors connexion.  

3.  Cliquez sur un client individuel dans le volet Liste pour voir plus d’informations sur le statut dans le volet Détails, dont des informations sur l’activité du client et l’intégrité du client.  

##  <a name="bkmk_allStatus"></a> Surveiller le statut de tous les clients  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance** > **État du client**. Dans cette page de la console, vous pouvez consulter les statistiques générales relatives à l’activité du client et à l’intégrité du client sur le site.  Vous pouvez également modifier l’étendue des informations en choisissant un autre regroupement.  

2.  Pour explorer en détail les statistiques renvoyées, cliquez sur le nom des informations communiquées (par exemple, **Clients actifs ayant réussi la vérification ou sans résultats**) et passez en revue les informations sur les différents clients.  

3.  Cliquez sur **Activité des clients** pour afficher des graphiques illustrant l’activité des clients sur votre site Configuration Manager.  

4.  Cliquez sur **Intégrité du client** pour afficher des graphiques illustrant l’état de vérification de l’intégrité des clients de votre site Configuration Manager.  

 Vous pouvez configurer des alertes pour vous avertir lorsque les résultats de l'intégrité des clients ou l'activité des clients passent au-dessous d'un pourcentage de clients spécifié dans un enregistrement ou lorsque la mise à jour échoue sur un pourcentage de clients spécifié. Pour plus d’informations sur la configuration de l’état du client, consultez [Comment configurer l’état du client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-status.md).  

##  <a name="BKMK_ClientHealth"></a> Vérifications et corrections effectuées par la fonction d'intégrité du client  
 Les vérifications et corrections suivantes peuvent être effectuées par la fonction d'intégrité du client.  

|Intégrité du client|Action corrective|Plus d'informations|  
|------------------|------------------------|----------------------|  
|Vérifier que la fonction d'intégrité du client a été exécutée récemment|Exécuter l'intégrité du client|Vérifie que l'intégrité du client a été exécutée au moins une fois au cours des trois derniers jours.|  
|Vérifier que la configuration requise du client est installée|Installer la configuration requise du client|Vérifie que la configuration requise du client est installée. Lit le fichier ccmsetup.xml dans le dossier d'installation client pour découvrir les composants requis.|  
|Test d'intégrité de l'espace de stockage WMI|Réinstaller le client Configuration Manager|Vérifie que les entrées de client Configuration Manager sont présentes dans WMI.|  
|Vérifier que le service client est en cours d'exécution|Démarrer le service client (Hôte de l'agent SMS)|Aucune information supplémentaire|  
|Test du récepteur d'événements WMI.|Redémarrer le service client|Vérifier si le récepteur d’événements WMI lié à Configuration Manager est perdu|  
|Vérifier l'existence du service WMI (Windows Management Instrumentation)|Aucune correction|Aucune information supplémentaire|  
|Vérifier que le client a été installé correctement|Réinstaller le client|Aucune information supplémentaire|  
|Test de lecture/d'écriture de l'espace de stockage WMI|Réinitialiser le référentiel WMI et réinstaller le client Configuration Manager|La correction de cette intégrité du client est effectuée uniquement sur les ordinateurs qui exécutent Windows Server 2003, Windows XP (64 bits) ou des versions antérieures.|  
|Vérifier que le type de démarrage du service anti-programme malveillant est automatique|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le service anti-programme malveillant est en cours d'exécution|Démarrer le service anti-programme malveillant|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service Windows Update est automatique ou manuel|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service client (Hôte de l'agent SMS) est automatique|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le service WMI (Windows Management Instrumentation) est en cours d'exécution|Démarrer le service WMI (Windows Management Instrumentation)|Aucune information supplémentaire|  
|Vérifier l'intégrité de la base de données Microsoft SQL CE|Réinstaller le client Configuration Manager|Aucune information supplémentaire|  
|Test d'intégrité WMI Microsoft Policy Platform|Réparer Microsoft Policy Platform|Aucune information supplémentaire|  
|Vérifier que le service Microsoft Policy Platform existe|Réparer Microsoft Policy Platform|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service Microsoft Policy Platform est manuel|Réinitialiser le type de démarrage du service sur manuel|Aucune information supplémentaire|  
|Vérifier l'existence du service de transfert intelligent en arrière-plan|Aucune correction|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service de transfert intelligent en arrière-plan est automatique ou manuel|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service d'inspection du réseau est manuel|Réinitialiser le type de démarrage du service sur manuel, s'il est installé|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service WMI (Windows Management Instrumentation) est automatique|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service Windows Update sur les ordinateurs Windows 8 est automatique ou manuel|Réinitialiser le type de démarrage du service sur manuel|Aucune information supplémentaire|  
|Vérifier l'existence du service client (hôte d'Agent SMS)|Aucune correction|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service de contrôle à distance de Configuration Manager est automatique ou manuel|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le service de contrôle à distance de Configuration Manager est en cours d'exécution|Démarrer le service de contrôle à distance|Aucune information supplémentaire|  
|Vérifier l'intégrité du fournisseur WMI du client|Redémarrer le service WMI (Windows Management Instrumentation)|La correction de cette intégrité du client est effectuée uniquement sur les ordinateurs qui exécutent Windows Server 2003, Windows XP (64 bits) ou des versions antérieures.|  
|Vérifier que le service de proxy de mise en éveil (proxy de mise en éveil ConfigMgr) est en cours d'exécution|Démarrer le service de proxy de mise en éveil ConfigMgr|Cette vérification du client est effectuée uniquement si le paramètre client **Gestion de l’alimentation**: **Autoriser le proxy de mise en éveil** est défini sur **Oui** sur les systèmes d’exploitation clients pris en charge.|  
|Vérifier que le type de démarrage du service de proxy de mise en éveil (proxy de mise en éveil ConfigMgr) est automatique|Réinitialiser le type de démarrage du service de proxy de mise en éveil ConfigMgr sur automatique|Cette vérification du client est effectuée uniquement si le paramètre client **Gestion de l’alimentation**: **Autoriser le proxy de mise en éveil** est défini sur **Oui** sur les systèmes d’exploitation clients pris en charge.|  

## <a name="client-deployment-log-files"></a>Fichiers journaux de déploiement du client
Pour plus d’informations sur les fichiers journaux utilisés par les opérations de déploiement et de gestion du client, consultez [Fichiers journaux dans System Center Configuration Manager](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
