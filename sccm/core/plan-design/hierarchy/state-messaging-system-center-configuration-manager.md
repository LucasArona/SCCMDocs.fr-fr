---
title: Messages d'état
titleSuffix: Configuration Manager
description: Description des messages d’état dans les versions prises en charge de Configuration Manager.
ms.date: 02/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f04c0a71-57bc-4443-a47c-592373050d04
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9e3a30211b95e483b30caf1507b74a7737d156bb
ms.sourcegitcommit: 223549003829fce7c6dc63959ee71e8b88542417
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/27/2019
ms.locfileid: "56951866"
---
# <a name="state-messages-in-configuration-manager"></a>Messages d’état dans Configuration Manager 

*S’applique à : System Center Configuration Manager (Current Branch)*

Les messages d’état contiennent des informations concises sur l’état du client Configuration Manager. Le système de messages d’état est utilisé par des composants spécifiques de Configuration Manager, comme les mises à jour de logiciels et les paramètres de configuration.

Les clients Configuration Manager envoient des messages d’état à des systèmes de site de point d’état de secours ou de point de gestion pour signaler l’état actuel des opérations. Il est possible de créer des rapports pour voir les messages d’état envoyés par les clients Configuration Manager.

Chacune des fonctionnalités Configuration Manager qui utilisent des messages d’état est identifiée grâce au type de sujet du message. Les types présentés dans cet article permettent de définir la fonctionnalité Configuration Manager associée à un message d’état donné.

> [!NOTE]  
> Une valeur d’ID de message d’état de zéro (0) indique généralement un type dont l’état est inconnu.

## <a name="300-statetopictypesumassignmentcompliance"></a>300 STATE_TOPICTYPE_SUM_ASSIGNMENT_COMPLIANCE

|      ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|       0   | État de conformité inconnu|
|   1   | conformité | 
|   2   | Non compatible | 

## <a name="301-statetopictypesumassignmentenforcement"></a>301 STATE_TOPICTYPE_SUM_ASSIGNMENT_ENFORCEMENT

|       ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   0    | État de mise en œuvre inconnu |
|   1    | Installation de la ou des mises à jour        | 
|   2    | Attente du redémarrage              | 
|   3    | Attente de la fin d'une autre installation         | 
|   4    | Installation de la ou des mises à jour réussie             | 
|   5    | Redémarrage du système en attente           | 
|   6    | Impossible d’installer la ou les mises à jour          | 
|   7    | Téléchargement de la ou des mises à jour en cours   | 
|   8    | Mise(s) à jour téléchargée(s)    | 
|   9    | Impossible de télécharger la ou les mises à jour     | 
|   10   | En attente de la fenêtre de maintenance avant l’installation         | 
|   11   | En attente de l’orchestration            | 

## <a name="302-statetopictypesumassignmentevaluation"></a>302 STATE_TOPICTYPE_SUM_ASSIGNMENT_EVALUATION

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|      
|0|        État d'évaluation inconnu|                 
|   1    |Évaluation activée       |
|   2    |Évaluation réussie      |
|   3    |Échec de l’évaluation         |


## <a name="400-statetopictypesumcidetection"></a>400 STATE_TOPICTYPE_SUM_CI_DETECTION

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
| 0  | État de détection inconnu|
|   1|  Non requis      |
|   2|  Non détecté          |
|   3|  Détecté      |

## <a name="401-statetopictypesumcicompliance"></a>401 STATE_TOPICTYPE_SUM_CI_COMPLIANCE

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|0| État de conformité inconnu|
|   1   |conformité         |
|   2   |Non compatible         |
|   3   |Conflit détecté     |
|   4   |Erreur             |
|   5   |Inconnu.           |
|   6   |Conformité partielle   |
|   7   |Conformité non configurée     |

## <a name="402-statetopictypesumcienforcement"></a>402 STATE_TOPICTYPE_SUM_CI_ENFORCEMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
| 0 | État de mise en œuvre inconnu|
|   1   |Début de la mise en œuvre                   |
|   2   |Mise en œuvre en attente du contenu               |
|   3   | Attente de la fin d'une autre installation         |
|   4   |En attente de la fenêtre de maintenance avant l’installation              |
|   5   |Redémarrage requis avant l'installation            |
|   6   |Défaillance générale           |
|   7   |Installation en attente              |
|   8   |Installation de la mise à jour                 |
|   9   |Redémarrage du système en attente        |
|   10  |Installation de la mise à jour réussie             |
|   11  |Impossible d’installer la mise à jour          |
|   12  |Téléchargement de la mise à jour        |
|   13  | Mise à jour téléchargée        |
|   14  |Impossible de télécharger la mise à jour         |

## <a name="500-statetoptctypesumupdatedetection"></a>500 STATE_TOPTCTYPE_SUM_UPDATE_DETECTION

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|0 |État de détection inconnu|
|   1   | Mise à jour non requise     |
|   2   | Mise à jour requise         |
|   3   | Mise à jour installée    |

## <a name="501-statetopictypesumupdatesourcescan"></a>501 STATE_TOPICTYPE_SUM_UPDATE_SOURCE_SCAN

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|0 |État d'analyse inconnu|
|   1   | Analyse en attente de contenu        |
|   2   | Exécution de l'analyse            |
|   3   | Analyse terminée          |
|   4   | Nouvelle tentative d'analyse en attente      |
|   5   | Échec de l'analyse        |
|   6   | Analyse terminée avec des erreurs |

## <a name="700-statetopictyperesyncstatemsg"></a>700 STATE_TOPICTYPE_RESYNC_STATE_MSG

    No State IDs.

## <a name="701-statetopictypesystemheartbeat"></a>701 STATE_TOPICTYPE_SYSTEM_HEARTBEAT

    No State IDs.

## <a name="702-statetopictypeckdupdate"></a>702 STATE_TOPICTYPE_CKD_UPDATE
 
    No State IDs.

## <a name="800-statetopictypeclientdeployment"></a>800 STATE_TOPICTYPE_CLIENT_DEPLOYMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   100 |Démarrage du déploiement du client             |          
|   101 |En attente du téléchargement                  |          
|   102 |Déploiement planifié                  |          
|   103 | En attente de la fenêtre avant le déploiement |
|   104 |Déploiement ignoré                |          
|   301 |Échec de déploiement du client inconnu |          
|   302 |Impossible de créer le service ccmsetup  |         
|   303 |Impossible de supprimer le service ccmsetup |          
|   304 |Installation impossible sur un système d’exploitation embarqué lorsque le filtre d’écriture basé sur des fichiers (FBWF) est activé sur le lecteur système |          
|   305 |Mode de sécurité natif non valide sur Windows 2000  |         
|   306 |Impossible de démarrer le processus de téléchargement de ccmsetup  |         
|   307 |Ligne de commande ccmsetup non valide |        
|   308 |Impossible de télécharger le fichier via WINHTTP à l’adresse |        
|   309 |Impossible de télécharger les fichiers via BITS à l’adresse |       
|   310 |Impossible d'installer la version de BITS |         
|   311 |Impossible de vérifier si le fichier requis est signé MS  |          
|   312 |Impossible de copier le fichier, car le disque est plein |       
|   313 |Échec de l'installation de Client.msi avec erreur MSI |          
|   314 |Impossible de charger le fichier manifeste ccmsetup.xml |          
|   315 |Impossible d’obtenir un certificat client  |         
|   316 |Le fichier requis n'est pas signé MS |         
|   317 |Redémarrage indispensable pour continuer l’installation  |          
|   318 |Impossible d’installer le client sur le point de gestion, car leurs versions ne correspondent pas |        
|   319 |Le système d'exploitation ou le Service Pack n'est pas pris en charge  |        
|   320 |Déploiement non pris en charge                  |          
|   321 |Bits manquants                      |          
|   322 |Dossier source non disponible                  |          
|   323 |Appv non pris en charge                    |          
|   324 |Version du site incorrecte                    |          
|   325 |Incompatibilité du hachage requis                |          
|   326 |Échec de la désinscription à la gestion des appareils mobiles             |          
|   327 |Inscription à la gestion des appareils mobiles détectée             |          
|   328 |Intune détecté                   |          
|   329 |Connexion réseau limitée non autorisée            |          
|   400 |Déploiement du client réussi |  
|   401 |Déploiement réussi, redémarrage requis          |          
|   402 |Déploiement réussi, redémarrage réussi         |
|   500 |Démarrage de l'attribution du client|
|   601 |Échec d'attribution du client inconnu|
|   602 |Le code de site suivant n'est pas valide|
|   603 |Impossible d'attribuer au point de gestion|
|   604 |Impossible de découvrir le point de gestion par défaut|
|   605 |Impossible de télécharger le certificat de signature du site|
|   606 |Échec de la découverte automatique du code de site|
|   607 |Échec de l'attribution du site : la version cliente est supérieure à celle du site|
|   608 |Impossible d'obtenir la version du site depuis les services de domaine Active Directory et le point de recherche de serveur|
|   609 |Impossible d'obtenir la version du client|
|   700 |Attribution du client réussie|

## <a name="801-statetopictypedeviceclientdeployment"></a>801 STATE_TOPICTYPE_DEVICE_CLIENT_DEPLOYMENT

    No State IDs.

## <a name="810-statetopictypeclientcomanagement"></a>810 STATE_TOPICTYPE_CLIENT_COMANAGEMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   100 | État de l'inscription         |
|   101 | Inscription planifiée          |
|   102 | Inscription annulée           |
|   105 | Inscription commencée            |
|   106 | Inscription réussie, mais non approvisionnée   
|   107 | Inscription réussie et approvisionnée   
|   108 | Inscription sans utilisateur actif         |
|   110 | Échec de l’inscription         |


## <a name="820--statetopictypeclientwufb"></a>820 STATE_TOPICTYPE_CLIENT_WUFB

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   | État du client Windows Update pour Entreprise| 

## <a name="900-statetopictypebranchdp"></a>900 STATE_TOPICTYPE_BRANCH_DP

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   | Espace disque      | 

## <a name="901-statetopictyperemotedpmonitoring"></a>901 STATE_TOPICTYPE_REMOTE_DP_MONITORING

    No State IDs.

## <a name="902-statetopictypepulldpmonitoring"></a>902 STATE_TOPICTYPE_PULL_DP_MONITORING

    No State IDs.

## <a name="903-statetopictypedpusage"></a>903 STATE_TOPICTYPE_DP_USAGE

    No State IDs.

## <a name="1000--statetopictypeclientframeworkcomm"></a>1000 STATE_TOPICTYPE_CLIENT_FRAMEWORK_COMM

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1      | Le client communique avec le point de gestion |
|   2      | Le client ne parvient pas à communiquer avec le point de gestion |

## <a name="1001-statetopictypeclientframeworklocal"></a>1001 STATE_TOPICTYPE_CLIENT_FRAMEWORK_LOCAL

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Le client a récupéré le certificat dans le magasin de certificats local       |
|   2   |Le client n’est pas parvenu à récupérer le certificat dans le magasin de certificats local |

## <a name="1002-statetopictypedeviceclientframeworkcomm"></a>1002 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_COMM

    No State IDs.

## <a name="1003-statetopictypedeviceclientframeworklocal"></a>1003 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_LOCAL

    No State IDs.

## <a name="1004-statetopictypedeviceclientframeworkcertificate"></a>1004 STATE_TOPICTYPE_DEVICE_CLIENT_FRAMEWORK_CERTIFICATE

    No State IDs.

## <a name="1005-statetopictypedeviceclientwipe"></a>1005 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE

    No State IDs.

## <a name="1006-statetopictypedeviceclientretire"></a>1006 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE

    No State IDs.

## <a name="1007-statetopictypedeviceclientwipeintune"></a>1007 STATE_TOPICTYPE_DEVICE_CLIENT_WIPE_INTUNE

    No State IDs.

## <a name="1008-statetopictypedeviceclientretireintune"></a>1008 STATE_TOPICTYPE_DEVICE_CLIENT_RETIRE_INTUNE

    No State IDs.

## <a name="1009-statetopictypedeviceclientdevicelock"></a>1009 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK

    No State IDs.

## <a name="1010-statetopictypedeviceclientdevicelockintune"></a>1010 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICELOCK_INTUNE

    No State IDs.

## <a name="1011-statetopictypedeviceclientdevicepinreset"></a>1011 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET

    No State IDs.

## <a name="1012-statetopictypedeviceclientdevicepinresetintune"></a>1012 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_INTUNE

    No State IDs.

## <a name="1013-statetopictypedeviceclientdevicepinresetonprem"></a>1013 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEPINRESET_ONPREM

    No State IDs.

## <a name="1014-statetopictypedeviceclientdevicealbypass"></a>1014 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS

    No State IDs.

## <a name="1015-statetopictypedeviceclientdevicealbypassintune"></a>1015 STATE_TOPICTYPE_DEVICE_CLIENT_DEVICEALBYPASS_INTUNE

    No State IDs.

## <a name="1100-statetopictypeclientframeworkmodereadiness"></a>1100 STATE_TOPICTYPE_CLIENT_FRAMEWORK_MODEREADINESS

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Le client n'est pas prêt pour le mode natif  |
|   2   |Le client est prêt pour le mode natif       |


## <a name="1300-statetopictypeclienthealth"></a>1300 STATE_TOPICTYPE_CLIENT_HEALTH

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |   Opération réussie|    
|   2   |   Échec |    

## <a name="1401-statetopictypestatereport"></a>1401 STATE_TOPICTYPE_STATE_REPORT

    No State IDs.

## <a name="1500-statetopictypecaltrackut"></a>1500 STATE_TOPICTYPE_CAL_TRACK_UT

    No State IDs.

## <a name="1502-statetopictypecaltrackmt"></a>1502 STATE_TOPICTYPE_CAL_TRACK_MT

    No State IDs.

## <a name="1503-statetopictypecaltrackml"></a>1503 STATE_TOPICTYPE_CAL_TRACK_ML

    No State IDs.   

## <a name="1600-statetopictypeuseraffinity"></a>1600 STATE_TOPICTYPE_USER_AFFINITY

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Affinité utilisateur définie        |
|   2   |Affinité utilisateur supprimée        |

## <a name="1700-statetopictypeappciscan"></a>1700 STATE_TOPICTYPE_APP_CI_SCAN

    No State IDs.

## <a name="1701-statetopictypeappcicompliance"></a>1701 STATE_TOPICTYPE_APP_CI_COMPLIANCE

    No State IDs.

## <a name="1702-statetopictypeappcienforcement"></a>1702 STATE_TOPICTYPE_APP_CI_ENFORCEMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1000    |Élément de configuration réussi                      |
|   1001    |Élément de configuration réussi déjà installé            |
|   1002    |Élément de configuration préliminaire réussi                |
|   1003    |État rapide de l’élément de configuration réussi                  |
|   2 000    |Élément de configuration en cours                    |
|   2001    |Élément de configuration en cours, en attente de contenu            |
|   2002    |Élément de configuration en cours d’installation                 |
|   2003    |Élément de configuration en cours, en attente de redémarrage             |
|   2004    |Élément de configuration en cours, en attente de la fenêtre de maintenance         |
|   2005    |Élément de configuration en cours, en attente de la planification               |
|   2006    |Élément de configuration en cours de téléchargement du contenu dépendant     |
|   2007    |Élément de configuration en cours d’installation des dépendances        |
|   2008    |Élément de configuration en cours, en attente de redémarrage             |
|   2009    |Élément de configuration en cours, contenu téléchargé             |
|   2010    |Élément de configuration en cours, en attente de mise à jour             |
|   2011    |Élément de configuration en cours, en attente de la reconnexion de l’utilisateur         |
|   2012    |Élément de configuration en cours, en attente de la déconnexion de l’utilisateur              |
|   2013    |Élément de configuration en cours, en attente de la connexion de l’utilisateur               |
|   2014    |Élément de configuration en cours, en attente de l’installation            |
|   2015    |Élément de configuration en cours, en attente d’une nouvelle tentative              |
|   2016    |Élément de configuration en cours, en attente de presmode               |
|   2017    |Élément de configuration en cours, en attente de l’orchestration          |
|   2018    |Élément de configuration en cours, en attente du réseau            |
|   2019    |Élément de configuration en cours, en attente de la mise à jour VE              |
|   2020    |Élément de configuration en cours de mise à jour VE            |
|   3 000    |Conditions de l’élément de configuration non satisfaites                       |
|   3001    |Conditions de l’élément de configuration non satisfaites, hôte non applicable           |
|   4000    |Élément de configuration inconnu                    |
|   5000    |Erreur de l’élément de configuration                          |
|   5001    |Erreur d’évaluation de l’élément de configuration                   |
|   5002    |Erreur d’installation de l’élément de configuration                   |
|   5003    |Erreur de récupération du contenu de l’élément de configuration               |
|   5004    |Erreur d’installation des dépendances de l’élément de configuration            |
|   5005    |Erreur de récupération des dépendances du contenu de l’élément de configuration        |
|   5006    |Erreur de type conflit entre les règles de l’élément de configuration                   |
|   5007    |Erreur de l’élément de configuration, en attente d’une nouvelle tentative                |
|   5008    |Erreur de désinstallation du remplacement de l’élément de configuration        |
|   5009    |Erreur de téléchargement du remplacement de l’élément de configuration               |
|   5010    |Erreur de mise à jour VE de l’élément de configuration                  |
|   5011    |Erreur d’installation de la licence de l’élément de configuration               |
|   5012    |Erreur de récupération de toutes les applications approuvées de l’élément de configuration       |
|   5013    |Erreur de l’élément de configuration, aucune licence disponible            |
|   5014    |Erreur de l’élément de configuration, système d’exploitation non pris en charge                 |
|   6000    |Lancement de l’élément de configuration réussi                           |
|   6010    |Erreur de lancement de l’élément de configuration                           |
|   6020    |Lancement inconnu de l’élément de configuration|

## <a name="1703-statetopictypeappciassignmentevaluatio"></a>1703 STATE_TOPICTYPE_APP_CI_ASSIGNMENT_EVALUATIO

    No State IDs.

## <a name="1704-statetopictypeappcilaunch"></a>1704 STATE_TOPICTYPE_APP_CI_LAUNCH

    No State IDs.

## <a name="1800-statetopictypeeventintrinsic"></a>1800 STATE_TOPICTYPE_EVENT_INTRINSIC

    No State IDs.

## <a name="1801-statetopictypeeventextrinsic"></a>1801 STATE_TOPICTYPE_EVENT_EXTRINSIC

    No State IDs.

## <a name="1900-statetopictypeepaminfection"></a>1900 STATE_TOPICTYPE_EP_AM_INFECTION

    No State IDs.

## <a name="1901-statetopictypeepamhealth"></a>1901 STATE_TOPICTYPE_EP_AM_HEALTH

    No State IDs.

## <a name="1902-statetopictypeepmalware"></a>1902 STATE_TOPICTYPE_EP_MALWARE

    No State IDs.

## <a name="1950-statetopictypeatphealthstatus"></a>1950 STATE_TOPICTYPE_ATP_HEALTH_STATUS

    No State IDs.

## <a name="2001-statetopictypeepclientdeployment"></a>2001 STATE_TOPICTYPE_EP_CLIENT_DEPLOYMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Endpoint Protection non géré       |
|   2   |Endpoint Protection est en attente d’installation  |
|   3   |Endpoint Protection géré         |
|   4   |Échec de l’installation d’Endpoint Protection     |
|   5   |Redémarrage d’Endpoint Protection en attente  |
|   6   |Endpoint Protection non pris en charge       |
|   7   |Endpoint Protection cogéré      |

## <a name="2002-statetopictypeepclientpolicyapplication"></a>2002 STATE_TOPICTYPE_EP_CLIENT_POLICYAPPLICATION

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   0   |État de l’application de stratégie Endpoint Protection inconnu        |
|   1   |État de l’application de stratégie Endpoint Protection réussi         |
|   2   |État de l’application de stratégie Endpoint Protection en échec        |

## <a name="2003-statetopictypeclientaction"></a>2003 STATE_TOPICTYPE_CLIENT_ACTION

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   0   |  Inconnu.           |
|   1   |  Activé            |
|   2   |  Inactive          |

## <a name="2100-statetopictypewpclientdeployment"></a>2100 STATE_TOPICTYPE_WP_CLIENT_DEPLOYMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   | Proxy de mise en éveil non installé          |
|   2   | Proxy de mise en éveil en attente d’installation       |
|   3   | Proxy de mise en éveil installé          |
|   4   | Échec de l’installation du proxy de mise en éveil       |
|   5   | Proxy de mise en éveil en attente de redémarrage         |
|   6   | Proxy de mise en éveil non pris en charge par ce système d’exploitation   |
|   7   | Refus du serveur proxy de mise en éveil        |
|   8   | Échec de la désinstallation du proxy de mise en éveil      |
|   9   | Runtime du proxy de mise en éveil non pris en charge         |

## <a name="2200-statetopictypefdm"></a>2200 STATE_TOPICTYPE_FDM

    No State IDs.

## <a name="2201-statetopictypeccmcertbinding"></a>2201 STATE_TOPICTYPE_CCM_CERT_BINDING

    No State IDs.

## <a name="2202-statetopictypeserverstatistic"></a>2202 STATE_TOPICTYPE_SERVER_STATISTIC

    No State IDs.

## <a name="3000-statetopictypedmwnschannel"></a>3000 STATE_TOPICTYPE_DM_WNS_CHANNEL

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|0  | Canal des Services de notifications Push Windows défini|

## <a name="4000-statetopictypemdmdeviceproperty"></a>4000 STATE_TOPICTYPE_MDM_DEVICE_PROPERTY

    No State IDs.

## <a name="4002-statetopictypemdmclientidenitity"></a>4002 STATE_TOPICTYPE_MDM_CLIENT_IDENITITY

    No State IDs.

## <a name="4003-statetopictypemdmapplicationrequest"></a>4003 STATE_TOPICTYPE_MDM_APPLICATION_REQUEST

    No State IDs.

## <a name="4004-statetopictypemdmapplicationstate"></a>4004 STATE_TOPICTYPE_MDM_APPLICATION_STATE

    No State IDs.

## <a name="4005-statetopictypemdmlicensedevicerelation"></a>4005 STATE_TOPICTYPE_MDM_LICENSE_DEVICE_RELATION

    No State IDs.

## <a name="4006-statetopictypemdmlicensekeys"></a>4006 STATE_TOPICTYPE_MDM_LICENSE_KEYS

    No State IDs.

## <a name="4007-statetopictypemdmpolicyassignment"></a>4007 STATE_TOPICTYPE_MDM_POLICY_ASSIGNMENT

    No State IDs.

## <a name="4008-statetopictypemdmandroidcount"></a>4008 STATE_TOPICTYPE_MDM_ANDROID_COUNT

    No State IDs.

## <a name="4009-statetopictypemdmslkstatus"></a>4009 STATE_TOPICTYPE_MDM_SLK_STATUS

    No State IDs.

## <a name="4010-statetopictypemdmusercompanytermacceptance"></a>4010 STATE_TOPICTYPE_MDM_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="4022-statetopictypemdmdepsyncnowstatus"></a>4022 STATE_TOPICTYPE_MDM_DEP_SYNCNOW_STATUS

    No State IDs.

## <a name="4023-statetopictypemdmmamstoreappsync"></a>4023 STATE_TOPICTYPE_MDM_MAM_STORE_APP_SYNC

    No State IDs.

## <a name="5000-statetopictypecertificateenrollment"></a>5000 STATE_TOPICTYPE_CERTIFICATE_ENROLLMENT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Stimulation émise                    |
|   2   |Échec de l’émission de la stimulation              |
|   3   |Échec de création de la demande                 |
|   4   |Échec d’envoi de la demande               |
|   5   |Validation de la stimulation réussie          |
|   6   |Échec de validation de la stimulation             |
|   7   |Échec de l’émission                    |
|   8   |Émission en attente                   |
|   9   |Émis                      |
|   10  |Échec du traitement de la réponse          |
|   11  |Réponse en attente                    |
|   12  |Inscription réussie                    |
|   13  |Inscription non réussie                   |
|   14  |Révoqué                         |
|   15  |Supprimé de la collection                 |
|   16  |Renouvellement vérifié                  |
|   17  |Échec de l’installation              |
|   18  |Installé                   |
|   19  |Échec de la suppression                   |
|   20  |Supprimé                     |
|   21  |Renouvellement demandé               |


## <a name="5001-statetopictypecertificatecrp"></a>5001 STATE_TOPICTYPE_CERTIFICATE_CRP

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Stimulation émise                       |
|   2   |Échec de l’émission de la stimulation                 |
|   3   |Échec de création de la demande                    |
|   4   |Échec d’envoi de la demande                  |
|   5   |Validation de la stimulation réussie             |
|   6   |Échec de validation de la stimulation                |
|   7   |Échec de l’émission                       |
|   8   |Émission en attente                      |
|   9   |Émis                         |
|   10  |Échec du traitement de la réponse             |
|   11  |Réponse en attente                       |
|   12  |Inscription réussie                       |
|   13  |Inscription non réussie                      |
|   14  |Révoqué                            |
|   15  |Supprimé de la collection                    |
|   16  |Renouvellement vérifié                     |
|   17  |Échec de l’installation                 |
|   18  |Installé                      |
|   19  |Échec de la suppression                      |
|   20  |Supprimé                        |
|   21  |Renouvellement demandé                  |

## <a name="5200-statetopictyperesourceaccessstatus"></a>5200 STATE_TOPICTYPE_RESOURCE_ACCESS_STATUS

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   | Configuration du code PIN d’état réussie                   |
|   2   | Échec de la configuration du code PIN d’état                  |
|   3   | Configuration du code PIN d’état non prise en charge               |
|   4   | Configuration du code PIN d’état en cours             |

## <a name="6000-statetopictyperemoteappsubscriptionstatus"></a>6000 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_STATUS

    No State IDs.

## <a name="6001-statetopictyperemoteappsubscriptionsyncstatus"></a>6001 STATE_TOPICTYPE_REMOTEAPP_SUBSCRIPTION_SYNC_STATUS

    No State IDs.

## <a name="6002-statetopictyperemoteappauthcookiessyncstatus"></a>6002 STATE_TOPICTYPE_REMOTEAPP_AUTHCOOKIES_SYNC_STATUS

    No State IDs.

## <a name="6003-statetopictyperemoteapplicationssyncstatus"></a>6003 STATE_TOPICTYPE_REMOTEAPPLICATIONS_SYNC_STATUS

    No State IDs.

## <a name="6004-statetopictyperemoteapplockresult"></a>6004 STATE_TOPICTYPE_REMOTEAPP_LOCK_RESULT

    No State IDs.

## <a name="7000-statetopictypeusercompanytermacceptance"></a>7000 STATE_TOPICTYPE_USER_COMPANY_TERM_ACCEPTANCE

    No State IDs.

## <a name="7001-statetopictypepfxcertificate"></a>7001 STATE_TOPICTYPE_PFX_CERTIFICATE

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Stimulation émise               |
|   2   |Échec de l’émission de la stimulation         |
|   3   |Échec de création de la demande            |
|   4   |Échec d’envoi de la demande          |
|   5   |Validation de la stimulation réussie     |
|   6   |Échec de validation de la stimulation        |
|   7   |Échec de l’émission               |
|   8   |Émission en attente              |
|   9   |Émis                 |
|   10  |Échec du traitement de la réponse     |
|   11  |Réponse en attente               |
|   12  |Inscription réussie               |
|   13  |Inscription non réussie              |
|   14  |Révoqué                    |
|   15  |Supprimé de la collection            |
|   16  |Renouvellement vérifié             |
|   17  |Échec de l’installation         |
|   18  |Installé              |
|   19  |Échec de la suppression              |
|   20  |Supprimé                |
|   21  |Renouvellement demandé          |

## <a name="7010-statetopictypeconditionalaccesscompliance"></a>7010 STATE_TOPICTYPE_CONDITIONAL_ACCESS_COMPLIANCE

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
||  1   | Réussite de la conformité             |
|   2   | Échec de la conformité au niveau du pack d’administration      |
|   3   | Échec de la conformité au niveau du client      |
|   4   | Échec de la conformité au niveau d’Intune      |
|   5   | Échec de la conformité au niveau d’AAD         |
|   6   | Cogestion de la conformité Intune       |

## <a name="7200-statetopictypesuperpeerupdatecachemap"></a>7200 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CACHE_MAP

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Source de cache de pair ajoutée                |
|   2   |Source de cache de pair supprimée          |

## <a name="7201-statetopictypesuperpeerupdateconfig"></a>7201 STATE_TOPICTYPE_SUPER_PEER_UPDATE_CONFIG

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Source de cache de pair désactivée              |
|   2   |Source de cache de pair active                |

## <a name="7202-statetopictypedownloadaggregatedata"></a>7202 STATE_TOPICTYPE_DOWNLOAD_AGGREGATE_DATA
|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Chargement des données d’agrégation téléchargées       |

## <a name="7203-statetopictypepeersourcereqrejectionstats"></a>7203 STATE_TOPICTYPE_PEERSOURCE_REQ_REJECTION_STATS

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Chargement des données de rejet de la source de pair     |

## <a name="7300-statetopictypeproxytraffic"></a>7300 STATE_TOPICTYPE_PROXY_TRAFFIC

    No State IDs.

## <a name="7301-statetopictypeproxyconnection"></a>7301 STATE_TOPICTYPE_PROXY_CONNECTION

    No State IDs.

## <a name="7302-statetopictypesrsusagedata"></a>7302 STATE_TOPICTYPE_SRS_USAGE_DATA

    No State IDs.

## <a name="7303-statetopictypeproxytrafficidentity"></a>7303 STATE_TOPICTYPE_PROXY_TRAFFIC_IDENTITY

    No State IDs.

## <a name="8001-statetopictypehasreport"></a>8001 STATE_TOPICTYPE_HAS_REPORT

|     ID du message d'état     |  Description du message d'état |
|:-------------|:------|
|   1   |Attestation d’intégrité prise en charge         |
|   2   |Attestation d’intégrité non prise en charge         |

## <a name="statetopictypedeviceclientedplog"></a>STATE_TOPICTYPE_DEVICE_CLIENT_EDPLOG

    No State IDs.

## <a name="8003-statetopictypeenablelostmode"></a>8003 STATE_TOPICTYPE_ENABLE_LOSTMODE

    No State IDs.

## <a name="8004-statetopictypedisablelostmode"></a>8004 STATE_TOPICTYPE_DISABLE_LOSTMODE

    No State IDs.

## <a name="8005-statetopictypelocatedevice"></a>8005 STATE_TOPICTYPE_LOCATE_DEVICE

    No State IDs.

## <a name="8006-statetopictyperebootdevice"></a>8006 STATE_TOPICTYPE_REBOOT_DEVICE

    No State IDs.

## <a name="8007-statetopictypelogoutuser"></a>8007 STATE_TOPICTYPE_LOGOUTUSER

    No State IDs.

## <a name="8008-statetopictypeuserslist"></a>8008 STATE_TOPICTYPE_USERSLIST

    No State IDs.

## <a name="8009-statetopictypedeleteuser"></a>8009 STATE_TOPICTYPE_DELETEUSER

    No State IDs.

## <a name="8010-statetopictypecleanpcretaininguserdata"></a>8010 STATE_TOPICTYPE_CLEANPCRETAININGUSERDATA

    No State IDs.

## <a name="8011-statetopictypecleanpcwithoutretaininguserdata"></a>8011 STATE_TOPICTYPE_CLEANPCWITHOUTRETAININGUSERDATA

    No State IDs.

## <a name="8012-statetopictypesetdevicename"></a>8012 STATE_TOPICTYPE_SETDEVICENAME

    No State IDs.

## <a name="9000-statetopictypebookcicompliance"></a>9000 STATE_TOPICTYPE_BOOK_CI_COMPLIANCE

    No State IDs.

## <a name="9001-statetopictypebookcienforcement"></a>9001 STATE_TOPICTYPE_BOOK_CI_ENFORCEMENT

    No State IDs.

## <a name="next-steps"></a>Étapes suivantes

- [Description des messages d’état dans Configuration Manager](https://support.microsoft.com/help/4459394/description-of-state-messaging-in-system-center-configuration-manager)
- [Livre blanc sur la gestion des mises à jour logicielles pour Configuration Manager](https://www.microsoft.com/download/details.aspx?id=44578)
