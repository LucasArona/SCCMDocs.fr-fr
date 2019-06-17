---
title: Surveiller les clients
titleSuffix: Configuration Manager
description: Obtenir des instructions détaillées sur la façon de surveiller les clients dans Configuration Manager
ms.date: 05/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2c8f57cf-1968-48de-87fb-4897432ed6e0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55fd698ac5213a3b11b207d0625d953f687e319f
ms.sourcegitcommit: 65753c51fbf596f233fc75a5462ea4a44005c70b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/03/2019
ms.locfileid: "66463035"
---
# <a name="how-to-monitor-clients-in-configuration-manager"></a>Comment surveiller des clients dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé le client Configuration Manager sur les appareils Windows de votre site, surveillez leur intégrité et leur activité dans la console Configuration Manager.  


## <a name="bkmk_about"></a> À propos du statut du client

Configuration Manager présente les types d’informations suivants sous forme d’état du client :  

- **État de connexion du client** : Le site considère qu’un appareil est **en ligne** s’il est connecté au point de gestion qui lui est affecté. Pour indiquer que le client est en ligne, il envoie des messages de type ping au point de gestion. Si le point de gestion n’a pas reçu de message après cinq minutes, le site considère que le client est **hors connexion**.  

- **Activité des clients** : Le site considère que le client est **actif** si ce dernier a communiqué avec Configuration Manager au cours des sept derniers jours. Le site considère que le client est **inactif** si ce dernier n’a pas effectué les actions suivantes au cours des sept derniers jours :  

    - Demandé la mise à jour d’une stratégie  
    - Envoyé un message de pulsation  
    - Envoyé un inventaire matériel  

- **Intégrité du client** : État de l’évaluation périodique de l’exécution du client Configuration Manager sur l’appareil. L’évaluation vérifie l’appareil et peut corriger certains problèmes détectés. Pour plus d’informations, consultez [Vérifications d’intégrité du client](#BKMK_ClientHealth).  

     Sur les appareils qui exécutent Windows 7, l'intégrité du client s'exécute en tant que tâche planifiée. Sur les versions de système d'exploitation ultérieures, l'intégrité du client s'exécute automatiquement pendant la fenêtre de maintenance de Windows.  

     Vous pouvez configurer la mise à jour de manière à ne pas l'exécuter sur des appareils spécifiques, par exemple, sur un serveur essentiel pour l'entreprise. Si vous souhaitez évaluer d’autres éléments, utilisez les paramètres de compatibilité de Configuration Manager pour surveiller les configurations supplémentaires. Pour plus d’informations sur les paramètres de compatibilité, consultez [Planifier et configurer les paramètres de compatibilité](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

- **Hors service** : Le site a marqué l’enregistrement d’appareil en vue d’une suppression. Ce comportement peut survenir lorsqu’une nouvelle inscription d’un même appareil est affectée au même site ou à un autre site primaire dans une hiérarchie. Le site supprime ces appareils la prochaine fois qu’il exécute la tâche de maintenance de site **Supprimer les données de découverte anciennes**.<!-- SCCMDocs issue #1418 -->  

- **Obsolète** : Le site a découvert un nouvel enregistrement d’appareil avec le même ID de matériel, et il marque donc l’ancien enregistrement comme étant obsolète. Les rapports ne comptabilisent pas plusieurs fois les enregistrements obsolètes d’un même appareil. Vous pouvez toujours cibler des stratégies pour les appareils obsolètes. Si le site n’obtient aucune pulsation pour un enregistrement obsolète après 90 jours d’inactivité, il supprime l’appareil obsolète lorsqu’il exécute la tâche de maintenance de site **Supprimer les données obsolètes de découverte des clients**.


## <a name="bkmk_indStatus"></a> Surveiller des clients individuels

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Actifs et conformité**. Sélectionnez le nœud **Appareils** ou choisissez un regroupement sous **Regroupements d’appareils**.  

    Les icônes au début de chaque ligne indiquent le statut de connexion de l’appareil :  

    |||  
    |-|-|  
    |![icône de statut de connexion des clients](../../../core/clients/manage/media/online-status-icon.png)|L’appareil est en ligne|  
    |![icône de statut déconnecté des clients](../../../core/clients/manage/media/offline-status-icon.png)|L’appareil est hors connexion|  
    |![icône de statut inconnu des clients](../../../core/clients/manage/media/unknown-status-icon.png)|Le statut de connexion est inconnu|  
    |![client non installé](../../../core/clients/manage/media/client-not-installed.png)|Le client n’est pas installé sur l’appareil|  

2. Pour obtenir un statut de connexion plus détaillé, ajoutez les informations de statut de connexion du client à l’affichage de l’appareil. Cliquez avec le bouton droit sur l’en-tête de colonne et sélectionnez les champs de statut de connexion que vous voulez ajouter :

    - **Statut de connexion de l’appareil** : indique si le client est actuellement en ligne ou hors connexion. (Ce statut affiche les mêmes informations que celles fournies par les icônes).  

    - **Heure de la dernière connexion** : indique à quel moment le statut de connexion du client est passé en ligne  

    - **Heure de la dernière déconnexion** indique à quel moment le statut est passé hors connexion  

3. Sélectionnez un client individuel dans le volet Liste pour voir plus d’informations sur le statut dans le volet Détails, dont des informations sur l’activité du client et l’intégrité du client.  


## <a name="bkmk_allStatus"></a> Surveiller le statut de tous les clients

1. Dans la console Configuration Manager, accédez à l’espace de travail **Supervision**, puis sélectionnez le nœud **État du client**. Consultez les statistiques générales relatives à l’activité du client et à l’intégrité du client sur le site. Modifiez l’étendue des informations en choisissant un autre regroupement.  

2. Pour explorer en détail les statistiques renvoyées, cliquez sur le nom des informations communiquées. Par exemple, **Clients actifs ayant réussi la vérification ou sans résultats**. Puis passez en revue les informations sur les différents clients.  

3. Sélectionnez **Activité des clients** pour afficher des graphiques montrant l’activité des clients sur votre site Configuration Manager.  

4. Sélectionnez **Intégrité du client** pour afficher des graphiques montrant l’état de vérification de l’intégrité des clients de votre site Configuration Manager.  

    Configurez des alertes pour être averti lorsque les résultats de la l’intégrité du client ou de l’activité du client passe sous un pourcentage spécifié. Le site peut également vous alerter en cas d’échec d’une mise à jour pour un pourcentage donné de clients. Pour plus d’informations, consultez [Guide pratique pour configurer l’état du client](/sccm/core/clients/deploy/configure-client-status).  


## <a name="BKMK_ClientHealth"></a> Vérification de l’intégrité du client

L’intégrité du client effectue les vérifications et corrections suivantes :  

|Intégrité du client|Action corrective|Informations complémentaires|  
|------------------|------------------------|----------------------|  
|Vérifier que la fonction d'intégrité du client a été exécutée récemment|Exécuter l'intégrité du client|Vérifie que l'intégrité du client a été exécutée au moins une fois au cours des trois derniers jours.|  
|Vérifier que la configuration requise du client est installée|Installer la configuration requise du client|Vérifie que la configuration requise du client est installée. Lit le fichier ccmsetup.xml dans le dossier d'installation client pour découvrir les composants requis.|  
|Test d'intégrité de l'espace de stockage WMI|Réinstaller le client Configuration Manager|Vérifie que les entrées de client Configuration Manager sont présentes dans WMI.|  
|Vérifier que le service client est en cours d'exécution|Démarrer le service client (Hôte de l'agent SMS)|Aucune information supplémentaire|  
|Test du récepteur d'événements WMI.|Redémarrer le service client|Vérifier si le récepteur d’événements WMI lié à Configuration Manager est perdu|  
|Vérifier l'existence du service WMI (Windows Management Instrumentation)|Aucune correction|Aucune information supplémentaire|  
|Vérifier que le client a été installé correctement|Réinstaller le client|Aucune information supplémentaire|  
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
|Vérifier que le type de démarrage du service Windows Update sur les appareils Windows 8 est automatique ou manuel|Réinitialiser le type de démarrage du service sur manuel|Aucune information supplémentaire|  
|Vérifier l'existence du service client (hôte d'Agent SMS)|Aucune correction|Aucune information supplémentaire|  
|Vérifier que le type de démarrage du service de contrôle à distance de Configuration Manager est automatique ou manuel|Réinitialiser le type de démarrage du service sur automatique|Aucune information supplémentaire|  
|Vérifier que le service de contrôle à distance de Configuration Manager est en cours d'exécution|Démarrer le service de contrôle à distance|Aucune information supplémentaire|  
|Vérifier que le service de proxy de mise en éveil (proxy de mise en éveil ConfigMgr) est en cours d'exécution|Démarrer le service de proxy de mise en éveil ConfigMgr|Cette vérification du client est effectuée uniquement si le paramètre client **Gestion de l’alimentation** : **Autoriser le proxy de mise en éveil** est défini sur **Oui** sur les systèmes d’exploitation client pris en charge.|  
|Vérifier que le type de démarrage du service de proxy de mise en éveil (proxy de mise en éveil ConfigMgr) est automatique|Réinitialiser le type de démarrage du service de proxy de mise en éveil ConfigMgr sur automatique|Cette vérification du client est effectuée uniquement si le paramètre client **Gestion de l’alimentation** : **Autoriser le proxy de mise en éveil** est défini sur **Oui** sur les systèmes d’exploitation client pris en charge.|  


<!-- 
5/31/2019 ACz: need to confirm if these checks are still applicable
|WMI repository read and write test|Reset the WMI repository and reinstall the Configuration Manager client|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier versions.|  
|Verify that the client WMI provider is healthy|Restart the Windows Management Instrumentation service|Remediation of this client check is only performed on devices that run Windows Server 2003, Windows XP (64-bit) or earlier.|  
 -->


## <a name="client-deployment-log-files"></a>Fichiers journaux de déploiement du client

Pour plus d’informations sur les fichiers journaux utilisés par les opérations de déploiement et de gestion du client, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#BKMK_ClientLogs).
