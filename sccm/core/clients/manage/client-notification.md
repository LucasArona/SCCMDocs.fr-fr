---
title: Notification du client
titleSuffix: Configuration Manager
description: Gérez les clients en effectuant une action immédiate à partir de la console centrale Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f190522300090247cdca0affa9d993fe46201668
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122030"
---
# <a name="client-notification-in-configuration-manager"></a>Notification du client dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour effectuer une action immédiate sur les clients distants, envoyez une action de notification du client à partir de la console Configuration Manager. Ces actions peuvent être lancées sur un appareil individuel ou sur un regroupement d’appareils. 



## <a name="actions"></a>Actions

Les actions suivantes se trouvent dans le ruban au niveau du groupe Appareil ou Regroupement de l’onglet Accueil. 


### <a name="install-client"></a>Installer le client

Ouvre l’**Assistant Installer le client**. Cet Assistant utilise la méthode d’installation Push du client pour installer un client Configuration Manager. Pour plus d’informations, consultez [Installation Push du client](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).

#### <a name="permissions"></a>Autorisations
Cette action nécessite les autorisations **Modifier la ressource** et **Lecture** sur l’objet **Regroupement**. 

Les rôles intégrés suivants disposent de ces autorisations par défaut :
- Administrateur de l'application  
- Administrateur complet  
- Administrateur d'infrastructure  
- Administrateur d'opérations  
- Gestionnaire de déploiement de système d’exploitation  

Ajoutez ces autorisations aux rôles personnalisés qui doivent transmettre (push) le client.


### <a name="run-script"></a>Exécuter le script

Ouvre l’Assistant **Exécuter le Script** pour exécuter un script PowerShell sur tous les clients du regroupement. Pour plus d’informations, consultez [Créer et exécuter des scripts PowerShell](/sccm/apps/deploy-use/create-deploy-scripts).

#### <a name="permissions"></a>Autorisations
Cette action nécessite l’autorisation **Exécuter le script** sur l’objet **Regroupement**. 

Les rôles intégrés suivants disposent de cette autorisation par défaut :
- Administrateur complet  
- Administrateur d'infrastructure  
- Administrateur d'opérations  

Ajoutez cette autorisation aux rôles personnalisés qui doivent exécuter des scripts.


### <a name="start-cmpivot"></a>Démarrer CMPivot

Démarre **CMPivot**, qui exécute des requêtes en temps réel sur les appareils ciblés. Pour plus d’informations, consultez [CMPivot](/sccm/core/servers/manage/cmpivot).

#### <a name="permissions"></a>Autorisations
Cette action nécessite les mêmes autorisations que l’action [Exécuter le script](#run-script). 



## <a name="client-notification"></a>Notification du client

Ces actions se trouvent sous le menu **Notification du client**, dans le ruban au niveau du groupe Appareil ou Regroupement de l’onglet Accueil.


#### <a name="permissions"></a>Autorisations
<!--SCCMDocs-pr issue #2972--> Depuis la version 1810, les actions de notification du client nécessitent l’autorisation **Notifier la ressource** sur l’objet Regroupement. Cette autorisation s’applique à toutes les actions du menu **Notification du client**. 

Les rôles intégrés suivants disposent de cette autorisation par défaut :
- Administrateur complet  
- Administrateur d'infrastructure  

Ajoutez cette autorisation aux rôles personnalisés qui doivent utiliser des actions de notification du client.


### <a name="download-computer-policy"></a>Télécharger la stratégie d’ordinateur

Actualisez la stratégie d’appareil. Pour plus d’informations, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  


### <a name="download-user-policy"></a>Télécharger la stratégie utilisateur

Actualisez la stratégie utilisateur.  


### <a name="collect-discovery-data"></a>Collecter les données de détection

Déclenchez sur les clients l’envoi d’un enregistrement de données de découverte (DDR). Pour plus d’informations, consultez [Découverte par pulsations d’inventaire](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutHeartbeat).  


### <a name="collect-software-inventory"></a>Collecter l’inventaire logiciel

Déclenchez sur les clients l’exécution d’un cycle d’inventaire logiciel. Pour plus d’informations, consultez [Présentation de l’inventaire logiciel](/sccm/core/clients/manage/inventory/introduction-to-software-inventory).  


### <a name="collect-hardware-inventory"></a>Collecte de l'inventaire matériel

Déclenchez sur les clients l’exécution d’un cycle d’inventaire matériel. Pour plus d’informations, consultez [Présentation de l’inventaire matériel](/sccm/core/clients/manage/inventory/introduction-to-hardware-inventory).  


### <a name="evaluate-application-deployments"></a>Évaluer les déploiements d’applications

Déclenchez sur les clients l’exécution d’un cycle d’évaluation des déploiements d’applications. Pour plus d'informations, consultez [Planifier la réévaluation des déploiements](/sccm/core/clients/deploy/about-client-settings#schedule-re-evaluation-for-deployments).  


### <a name="evaluate-software-update-deployments"></a>Évaluer les déploiements de mises à jour logicielles

Déclenchez sur les clients l’exécution d’un cycle d’évaluation des déploiements de mises à jour logicielles. Pour plus d’informations, consultez [Présentation de mises à jour logicielles](/sccm/sum/understand/software-updates-introduction).  


### <a name="switch-to-the-next-software-update-point"></a>Passer au point de mise à jour logicielle suivant

Déclenchez sur les clients le passage au prochain point de mise à jour logicielle disponible. Pour plus d’informations, consultez [Basculement de point de mise à jour logicielle](/sccm/sum/plan-design/plan-for-software-updates#BKMK_SUPSwitching).  


### <a name="evaluate-device-health-attestation"></a>Évaluer l’attestation d’intégrité de l’appareil

Déclenchez sur les clients Windows 10 la vérification et l’envoi de leur dernier état d’intégrité d’appareil. Pour plus d’informations, consultez [Attestation d’intégrité](/sccm/core/servers/manage/health-attestation).  


### <a name="check-conditional-access-compliance"></a>Vérifier la conformité de l’accès conditionnel

Déclenchez sur les clients la vérification de leur conformité avec l’accès conditionnel. Pour plus d’informations, consultez [Gérer l’accès aux services O365 pour PC](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm).  


### <a name="wake-up"></a>Sortir de veille

Depuis la version 1810, déclenchez le retour à un état d’alimentation maximale pour les appareils en veille.


### <a name="restart"></a>Redémarrer

Déclenchez le redémarrage des appareils sélectionnés. 



## <a name="endpoint-protection"></a>Endpoint Protection

Les actions suivantes se trouvent dans le menu **Endpoint Protection**. Ce menu se trouve sur le ruban au niveau du groupe Regroupement de l’onglet Accueil. Quand vous sélectionnez un ou plusieurs appareils, ces actions se trouvent sous l’onglet **Objet sélectionné** du ruban.

Pour plus d’informations, consultez [Endpoint Protection dans Configuration Manager](/sccm/protect/deploy-use/endpoint-protection).

#### <a name="permissions"></a>Autorisations
Cette action nécessite l’autorisation **Appliquer la sécurité** sur l’objet **Regroupement**. 

Les rôles intégrés suivants disposent de cette autorisation par défaut :
- Administrateur complet  
- Gestionnaire Endpoint Protection  
- Administrateur d'opérations  

Ajoutez cette autorisation aux rôles personnalisés qui doivent déclencher des actions Endpoint Protection.


### <a name="full-scan"></a>Analyse complète

Déclenchez Endpoint Protection ou Windows Defender pour exécuter une analyse *complète* de logiciel anti-programme malveillant.  


### <a name="quick-scan"></a>Analyse rapide

Déclenchez Endpoint Protection ou Windows Defender pour exécuter une analyse *rapide* de logiciel anti-programme malveillant.  


### <a name="download-definition"></a>Télécharger la définition

Déclenchez Endpoint Protection ou Windows Defender pour télécharger les dernières définitions de logiciel anti-programme malveillant.  



## <a name="see-also"></a>Voir aussi

- [Guide pratique pour gérer les clients](/sccm/core/clients/manage/manage-clients)
- [Guide pratique pour gérer des regroupements](/sccm/core/clients/manage/collections/manage-collections)
