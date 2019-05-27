---
title: Nouvelle version 1706
titleSuffix: Configuration Manager
description: Obtenez des détails sur les nouvelles fonctionnalités et les changements introduits dans la version 1706 de System Center Configuration Manager.
ms.date: 08/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ac034143-003e-4629-aac2-99eaffef4db1
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: cc88e70360599391c84e54e41e73b53ef3b70678
ms.sourcegitcommit: 18ad7686d194d8cc9136a761b8153a1ead1cdc6b
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66177043"
---
# <a name="what39s-new-in-version-1706-of-system-center-configuration-manager"></a>Nouveautés de la version 1706 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1706 de la version Current Branch de System Center Configuration Manager est une mise à jour dans la console des sites déjà installés qui exécutent la version 1606, 1610 ou 1702.

> [!TIP]  
> Pour installer un nouveau site, vous devez utiliser une version de base de Configuration Manager.  
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installation de mises à jour sur les sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Les sections suivantes fournissent des détails sur les nouvelles fonctionnalités et les changements introduits dans la version 1706 de Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1706 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastructure de site

### <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Prise en charge du cache d’homologue client pour les fichiers d’installation rapide de Windows 10 et Office 365  
<!-- 1352486 -->
À partir de cette version, le cache d’homologue prend en charge la distribution des fichiers d’installation rapide de Windows 10 et des fichiers de mise à jour d’Office 365. Aucune configuration supplémentaire n’est nécessaire pour prendre en charge ce changement.

### <a name="updates-for-the-data-warehouse"></a>Mises à jour de l’entrepôt de données
<!-- 1277922 -->
L’entrepôt de données n’est plus une fonctionnalité en préversion. Nous avons également mis à jour les prérequis pour prendre en charge la base de données sur les groupes de disponibilité SQL Server Always On et les clusters de basculement. Pour en savoir plus, consultez la section relative au [point de service de l’entrepôt de données](/sccm/core/servers/manage/data-warehouse).

### <a name="accessibility-improvements"></a>Améliorations d’accessibilité
<!-- 1253000 -->
Des améliorations supplémentaires ont été apportées aux fonctionnalités d’accessibilité de la console Configuration Manager. Pour plus d’informations, consultez [Fonctionnalités d’accessibilité](/sccm/core/understand/accessibility-features).

### <a name="improvements--for-sql-server-always-on-availability-groups"></a>Améliorations pour les groupes de disponibilité Always On SQL Server
<!-- 1352094 -->
Avec cette version, vous pouvez maintenant utiliser les réplicas avec validation asynchrone dans les groupes de disponibilité Always On SQL Server que vous utilisez avec Configuration Manager. Cela signifie que vous pouvez ajouter des réplicas supplémentaires à vos groupes de disponibilité à utiliser en tant que sauvegardes hors site (à distance) puis de les utiliser dans un scénario de récupération d’urgence.  
  -   Configuration Manager prend en charge l’utilisation du réplica avec validation asynchrone pour récupérer votre réplica synchrone. Consultez les [options de récupération de base de données de site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) dans la rubrique Sauvegarde et récupération pour plus d’informations sur la façon d’y parvenir.
  -   Cette version ne prend pas en charge le basculement pour utiliser le réplica avec validation asynchrone en tant que base de données de votre site.
Pour plus d’informations, consultez [Se préparer à l’utilisation de groupes de disponibilité SQL Server Always On](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).

### <a name="update-reset-tool"></a>Outil de réinitialisation des mises à jour
<!-- 1324589 -->
À compter de la version 1706, les sites d’administration centrale et les sites principaux Configuration Manager incluent l’outil de réinitialisation des mises à jour Configuration Manager (**CMUpdateReset.exe**). Utilisez cet outil avec n’importe quelle version de Current Branch prise en charge pour résoudre les problèmes de téléchargement ou de réplication des mises à jour dans la console. Pour plus d’informations, consultez [Outil de réinitialisation des mises à jour](/sccm/core/servers/manage/update-reset-tool).

### <a name="high-dpi-console-support"></a>Prise en charge des consoles à résolution élevée  
<!-- 1353476 -->
Avec cette version, les problèmes liés à la façon dont la console Configuration Manager met à l’échelle et affiche les différentes parties de l’interface utilisateur lors de son affichage sur des appareils à résolution élevée (comme un livre) devraient être corrigés.

### <a name="improved-boundary-groups-for-software-update-points"></a>Améliorations des groupes de limites pour les points de mise à jour logicielle
<!-- 1324591 -->
Cette version inclut des améliorations pour le fonctionnement des points de mise à jour logicielle avec des groupes de limites. Voici qui résume le nouveau comportement de secours :
-   L’action de secours pour les points de mise à jour logicielle utilise désormais un temps configurable pour le repli sur les groupes de limites voisins.
-   Indépendamment de la configuration de secours, un client essaie d’atteindre le dernier point de mise à jour logicielle qu'il a utilisé pendant 120 minutes. Après l’échec de communication avec ce serveur pendant 120 minutes, le client vérifie ensuite son pool de points de mise à jour logicielle disponibles, afin d’en trouver un nouveau.
-   Après avoir échoué pendant deux heures à atteindre le serveur d’origine, le client passe à un cycle plus court pour contacter un nouveau point de mise à jour logicielle. Cela signifie que si un client ne parvient pas à se connecter avec un nouveau serveur, il sélectionne rapidement le serveur suivant à partir de son pool de serveurs disponibles et tente de le contacter.

Pour plus d’informations, consultez la section [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) dans la rubrique Groupes de limites pour Current Branch.

### <a name="azure-ad-integration-with-configuration-manager"></a>Intégration d’Azure AD à Configuration Manager
<!-- 1248187, 1290765, 1258052, 1298097, 1319334, 1319883, 1352135, 1353331 -->
Dans cette version, nous avons amélioré l’intégration de Configuration Manager et d’Azure Active Directory (Azure AD).  Ces améliorations simplifient non seulement la configuration des services Azure que vous utilisez avec Configuration Manager, mais aussi la gestion des clients et des utilisateurs qui s’authentifient par le biais d’Azure AD.

Grâce à l’intégration améliorée, les opérations suivantes sont possibles :  
  -   Assistant Services Azure : cet Assistant propose une expérience de configuration commune qui remplace les différents flux de travail associés à la configuration des services Azure suivants que vous utilisez avec Configuration Manager.
      - **Gestion cloud** Donnez aux clients la possibilité de s’authentifier à l’aide d’Azure Active Directory (Azure AD). Vous pouvez également configurer la découverte des utilisateurs Azure AD.
      - Le **connecteur Log Analytics** se connecte à Azure Log Analytics et synchronise les données de regroupement.
      - **Upgrade Readiness** Connectez-vous à Upgrade Readiness et consultez les données de compatibilité de mise à niveau des clients.
      - **Microsoft Store pour Entreprises** Connectez-vous au Microsoft Store pour Entreprises et obtenez des applications pour votre organisation que vous pouvez déployer avec Configuration Manager.


  Pour cela, une [application web serveur Azure](/azure/azure/app-service/app-service-authentication-overview#service-to-service-authentication) fournit les détails de l’abonnement et de la configuration, ce qui vous évite de les entrer chaque fois que vous configurez un nouveau service ou composant Configuration Manager avec Azure. Pour plus d’informations, consultez [Assistant Services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard).

-   Utiliser Azure AD pour authentifier les clients sur Internet pour l’accès à vos sites Configuration Manager. Azure AD élimine le besoin de configurer et d’utiliser des certificats d’authentification client. Vous devez pour cela utiliser le rôle de système de site Passerelle de gestion cloud. Pour plus d’informations, consultez [Installer et attribuer des clients Configuration Manager à partir d’Internet à l’aide de l’authentification Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Installez et gérez le client Configuration Manager sur les ordinateurs qui se trouvent sur Internet. Vous devez pour cela utiliser le rôle de système de site Passerelle de gestion cloud. Pour plus d’informations, consultez [Installer et attribuer des clients Configuration Manager à partir d’Internet à l’aide de l’authentification Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure).

-   Configurer la découverte des utilisateurs Azure AD.  Utilisez l’Assistant Services Azure pour configurer cette nouvelle méthode de découverte. Cette nouvelle méthode exécute une requête sur votre annuaire Azure AD pour extraire des données utilisateur que vous pouvez utiliser avec vos données de découverte traditionnelles.  La synchronisation complète et la synchronisation delta sont prises en charge.  Pour plus d’informations, consultez [Découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

### <a name="peer-cache-improvements"></a>Améliorations du cache d’homologue
<!-- 1252345 -->
Le cache d’homologue n’utilise plus le compte d’accès réseau pour authentifier les demandes de téléchargement à partir d’homologues. Cela pose problème quand les clients ont besoin de ce compte. Il est en effet exigé par les clients qui démarrent dans WinPE et qui accèdent ensuite au contenu à partir d’une source de cache d’homologue. Pour plus d’informations, consultez [Exigences et considérations relatives au cache d’homologue](/sccm/core/plan-design/hierarchy/client-peer-cache#requirements-and-considerations-for-peer-cache).


<!-- ## Migration  -->


<!-- ## Client management  -->


## <a name="compliance-settings"></a>Paramètres de conformité

### <a name="new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client"></a>Nouveaux paramètres de configuration pour les appareils Windows 10 qui ne sont pas gérés avec le client Configuration Manager
<!-- 1354715 -->
Dans cette version, nous avons ajouté de nouveaux paramètres de configuration pour les appareils Windows 10 inscrits auprès d’Intune ou gérés localement par Configuration Manager. Ces paramètres sont les suivants :

- **Mot de passe**
    - Chiffrement de l’appareil
- **Appareil**
    - Modification des paramètres de région (Desktop uniquement)
    - Modification des paramètres d’alimentation et de mise en veille
    - Modification des paramètres de langue
    - Modification de l’heure du système
    - Modification du nom de l’appareil
- **Store**
    - Mettre à jour automatiquement les applications du store
    - Utiliser uniquement un store privé
    - Lancement des applications provenant du store
- **Microsoft Edge**
    - Bloquer l’accès à about:flags
    - Remplacement de l’invite SmartScreen
    - Remplacement de l’invite SmartScreen pour les fichiers
    - Adresse IP localhost WebRTC
    - Moteur de recherche par défaut
    - URL OpenSearch XML
    - Pages d’accueil (Desktop uniquement)

Pour plus de détails sur tous les paramètres de Windows 10, consultez [Comment créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager](/sccm/mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).

### <a name="new-device-compliance-policy-rules"></a>Nouvelles règles de stratégie de conformité d’appareil

* **Type de mot de passe requis**. Spécifie si les utilisateurs doivent créer un mot de passe de type alphanumérique ou numérique. Pour les mots de passe alphanumériques, vous spécifiez également le nombre minimal de jeux de caractères que le mot de passe doit avoir. Les quatre jeux de caractères sont : lettres minuscules, lettres majuscules, symboles et chiffres.

  **Pris en charge sur :**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
  <br></br>
* **Bloquer le débogage USB sur l’appareil**. Vous n’avez pas à configurer ce paramètre, car le débogage USB est déjà désactivé pour les appareils Android for Work.

  **Pris en charge sur :**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Bloquer les applications provenant de sources inconnues**. Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues. Vous n’avez pas à configurer ce paramètre, car les appareils Android for Work limitent toujours l’installation à partir de sources inconnues.

  **Pris en charge sur :**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
  <br></br>
* **Exiger l’analyse des menaces sur les applications**. Ce paramètre spécifie que la fonction Vérifier les applications est activée sur l’appareil.

  **Pris en charge sur :**
  * Android 4.2 à 4.4
  * Samsung KNOX Standard 4.0+

Pour essayer les nouvelles règles de conformité d’appareil, consultez [Créer et déployer une stratégie de conformité d’appareil](https://docs.microsoft.com/sccm/mdm/deploy-use/create-compliance-policy).

## <a name="application-management"></a>Gestion des applications

### <a name="run-powershell-scripts-from-the-configuration-manager-console"></a>Exécuter des scripts PowerShell à partir de la console Configuration Manager
<!-- 1236459 -->

Dans Configuration Manager, vous pouvez déployer des scripts sur des appareils clients à l’aide de packages et de programmes. Dans cette version, nous avons ajouté de nouvelles fonctionnalités qui vous permettent d’effectuer les actions suivantes :

- Importer des scripts PowerShell dans Configuration Manager
- Modifier les scripts à partir de la console Configuration Manager (pour les scripts non signés uniquement)
- Marquer les scripts comme Approuvés ou Refusés pour améliorer la sécurité
- Exécuter des scripts sur des collections d’ordinateurs clients Windows, et des ordinateurs Windows gérés localement. Vous ne pouvez pas déployer des scripts : ils sont exécutés en temps quasi réel sur les appareils clients.
- Examinez les résultats retournés par le script dans la console Configuration Manager.

Pour plus d’informations, consultez [Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).

### <a name="new-mobile-application-management-policy-settings"></a>Nouveaux paramètres de stratégie de gestion d’application mobile    
<!--1324760-->
À partir de cette version, vous pouvez utiliser trois nouveaux paramètres de stratégie de gestion des applications mobiles (MAM) :

- **Bloquer la capture d’écran (appareils Android uniquement) :** Spécifie que les fonctionnalités de capture d'écran de l'appareil sont bloquées lors de l'utilisation de cette application.

Consultez [Protéger les applications à l’aide des stratégies de protection des applications de Configuration Manager](https://docs.microsoft.com/sccm/mdm/deploy-use/protect-apps-using-mam-policies) pour essayer de nouveaux paramètres de stratégie de protection d’application.


## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation

### <a name="hardware-inventory-collects-secure-boot-information"></a>L’inventaire matériel collecte des informations sur le démarrage sécurisé
L’inventaire matériel collecte désormais des informations indiquant si le démarrage sécurisé est activé sur les clients. Ces informations sont stockées dans la classe **SMS_Firmware** (introduite dans la version 1702) et activées dans l’inventaire matériel par défaut. Pour plus d’informations sur l’inventaire matériel, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="collapsible-task-sequence-groups"></a>Groupes de séquences de tâches réductibles
Cette version permet de développer et réduire des groupes de séquences de tâches. Vous pouvez développer ou réduire des groupes individuels ou tous les groupes à la fois.

### <a name="reload-boot-images-with-current-windows-pe-version"></a>Recharger les images de démarrage avec la version actuelle de Windows PE
Lorsque vous exécutez l’option **Mise à jour des points de distribution** sur une image de démarrage sélectionnée, vous pouvez maintenant choisir de recharger la dernière version de Windows PE (depuis le répertoire d’installation de Windows ADK) dans l’image de démarrage. Pour plus d’informations, consultez [Mettre à jour des points de distribution avec l’image de démarrage](/sccm/osd/get-started/manage-boot-images#update-distribution-points-with-the-boot-image).

## <a name="software-updates"></a>Mises à jour logicielles

### <a name="improvements-to-express-update-download-time"></a>Amélioration de la durée de téléchargement des mises à jour rapides
Dans cette version, nous avons considérablement amélioré la durée de téléchargement des mises à jour rapides. Pour plus d’informations, consultez [Gérer les fichiers d’installation rapide pour les mises à jour de Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).

### <a name="manage-microsoft-surface-driver-updates"></a>Gérer les mises à jour du pilote Microsoft Surface
<!-- 1098490 -->
Vous pouvez maintenant utiliser Configuration Manager pour gérer les mises à jour du pilote Microsoft Surface.    


#### <a name="prerequisites"></a>Prérequis
- Tous les points de mise à jour logicielle doivent exécuter Windows Server 2016.    
- Il s’agit d’une fonctionnalité en préversion que vous devez activer pour pouvoir y accéder. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversions de mises à jour](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

#### <a name="to-manage-surface-driver-updates"></a>Pour gérer les mises à jour du pilote Surface

1. Activer la synchronisation pour les pilotes Microsoft Surface. Utilisez la procédure décrite dans [Configurer la classification et les produits](/sccm/sum/get-started/configure-classifications-and-products) et cochez la case **Inclure les mises à jour du microprogramme et des pilotes Microsoft Surface** sous l’onglet **Classifications** pour activer les pilotes Surface.
2. [Synchroniser les pilotes Microsoft Surface](/sccm/sum/get-started/synchronize-software-updates).
3. [Déployer des pilotes Microsoft Surface synchronisés](/sccm/sum/deploy-use/deploy-software-updates)

### <a name="configure-windows-update-for-business-deferral-policies"></a>Configuration de Windows Update pour les stratégies d’entreprise de report d’entreprise
<!-- 1290890 -->
Vous pouvez maintenant configurer des stratégies de report pour les appareils Windows 10 avec mises à jour de fonctionnalités ou de qualité gérés directement par Windows Update for Business. Vous pouvez gérer les stratégies de report du nouveau nœud **Stratégies Windows Update for Business** sous **Bibliothèque de logiciels** > **Maintenance de Windows 10**.

Pour plus d’informations, consultez [Intégration à Windows Update for Business dans Windows 10](/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).

### <a name="improved-user-notifications-for-office-365-updates"></a>Amélioration des notifications à l’utilisateur pour les mises à jour d’Office 365
Des améliorations ont été apportées pour tirer parti de l’expérience utilisateur « Cliquer pour exécuter » d’Office lorsqu’un client installe une mise à jour d’Office 365. Cela inclut des fenêtres contextuelles et des notifications dans l’application, ainsi qu’une expérience de compte à rebours. Pour plus d’informations, consultez [Comportement de redémarrage et notifications des clients pour les mises à jour d’Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#restart-behavior-and-client-notifications-for-office-365-updates).

## <a name="reporting"></a>Rapports

### <a name="use-windows-analytics-with-configuration-manager"></a>Utiliser Windows Analytics avec Configuration Manager
<!-- 1318608 -->
Windows Analytics regroupe un ensemble de solutions qui vous permettent d’obtenir des insights sur l’état actuel de votre environnement. Les appareils de votre environnement envoient des données de télémétrie Windows. Les données sont accessibles via le portail Azure. Dans le cadre d’Upgrade Readiness, les données sont directement disponibles dans le nœud de surveillance de la console Configuration Manager.

Pour plus d’informations, consultez [Utiliser Windows Analytics avec Configuration Manager](/sccm/core/clients/manage/monitor-windows-analytics).


<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestion des appareils mobiles

### <a name="updates-to-android-for-work-sharing-configuration"></a>Mises à jour apportées à la configuration de partage Android for Work
<!-- 1338403 -->
Dans cette version, les valeurs du paramètre **Autoriser le partage de données entre les profils professionnel et personnel** dans le groupe de paramètres **Profil professionnel** ont été mises à jour. Nous avons également ajouté un paramètre personnalisé pour bloquer les opérations copier-coller entre les profils professionnels et personnels.

Pour plus d’informations, consultez [Éléments de configuration pour les appareils Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client).

### <a name="android-and-ios-enrollment-restrictions"></a>Restrictions de l’inscription Android et iOS
<!-- 1290826 -->
Avec cette version, vous pouvez à présent spécifier que les utilisateurs ne peuvent pas inscrire des appareils Android ou iOS personnels. Les nouveaux paramètres de restriction des appareils permettent de limiter l’inscription des appareils Android aux appareils prédéclarés. Pour les appareils iOS, vous pouvez bloquer l’inscription de tous les appareils à l’exception de ceux qui sont inscrits auprès du Programme d’inscription des appareils d’Apple, d’Apple Configurator ou du compte du gestionnaire d’inscription des appareils Intune.
- Pour plus d’informations sur les restrictions d’inscription Android, consultez la page [Configurer la gestion des appareils Android](/sccm/mdm/deploy-use/enroll-hybrid-android).
- Pour plus d’informations sur les restrictions d’inscription iOS, consultez la page [Configurer des restrictions d’inscription iOS](/sccm/mdm/deploy-use/enroll-hybrid-ios-mac#configure-enrollment-restrictions).

## <a name="protect-devices"></a>Protéger les appareils

### <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Inclure la confiance pour des fichiers et dossiers spécifiques dans une stratégie de protection des appareils
<!--1324676-->
Dans cette version, nous avons ajouté des fonctionnalités supplémentaires à la gestion des stratégies Device Guard.

Vous pouvez éventuellement ajouter l’approbation pour des fichiers spécifiques pour les dossiers dans une stratégie Device Guard. Cela vous permet de :

- Résoudre les problèmes avec les comportements des programmes d’installation gérés
- Approuver les applications métier qui ne peuvent pas être déployées avec Configuration Manager
- Approuver des applications qui sont incluses dans une image de déploiement de système d’exploitation

Pour plus d’informations, consultez [Gestion de Device Guard avec Configuration Manager](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
