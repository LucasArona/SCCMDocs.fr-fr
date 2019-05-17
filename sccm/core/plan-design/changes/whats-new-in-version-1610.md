---
title: Nouvelle version 1610
titleSuffix: Configuration Manager
description: Obtenez des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1610 de System Center Configuration Manager.
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f7eb0803-3f8f-4ab6-825a-99ac11f5ba7d
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 04e4f24cee033f46ea69080a423b9ca6e2d4c9d5
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495145"
---
# <a name="what39s-new-in-version-1610-of-system-center-configuration-manager"></a>Nouveautés dans la version 1610 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1610 de la version Current Branch de System Center Configuration Manager est une mise à jour dans la console des sites déjà installés qui exécutent la version 1511, 1602 ou 1606.


> [!TIP]  
> Pour installer un nouveau site, vous devez utiliser une version de base de Configuration Manager.  
>  Informations supplémentaires :    
>  -   [Installation de nouveaux sites](https://technet.microsoft.com/library/mt590197.aspx)  
>  -   [Installation de mises à jour sur les sites](https://technet.microsoft.com/library/mt607046.aspx)  
>  -   [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Les sections suivantes fournissent des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1610 de Configuration Manager.  


## <a name="in-console-monitoring-of-update-installation-status"></a>Surveillance de l’état d’installation des mises à jour dans la console  
À partir de la version 1610, quand vous installez un pack de mises à jour et surveillez l’installation dans la console, une nouvelle phase est disponible : **Après l’installation**. Cette phase inclut l’état des tâches comme le redémarrage des services principaux et le lancement de la surveillance de la réplication. (Cette phase n’est pas disponible dans la console tant que votre site n’est pas mis à jour vers la version 1610.) Pour plus d’informations sur l’état d’installation des mises à jour, consultez [Installer des mises à jour dans la console](/sccm/core/servers/manage/install-in-console-updates#a-namebkmkinstalla-install-in-console-updates).


## <a name="exclude-clients-from-automatic-upgrade"></a>Exclure des clients de la mise à niveau automatique
Vous pouvez empêcher la mise à niveau de clients Windows avec les nouvelles versions du logiciel client. Pour ce faire, vous incluez les ordinateurs clients dans un regroupement spécifié comme devant être exclu de la mise à niveau. Les clients du regroupement exclu ignorent les demandes de mise à jour du logiciel client.  Pour plus d’informations, consultez [Exclure les clients Windows des mises à niveau](../../clients/manage/upgrade/exclude-clients-windows.md).


## <a name="improvements-for-boundary-groups"></a>Améliorations pour les groupes de limites
La version 1610 apporte des modifications importantes aux groupes de limites et à leur fonctionnement avec les points de distribution. Ces modifications permettent de simplifier la conception de votre infrastructure de contenu tout en vous donnant davantage de contrôle sur quand et comment les clients doivent se tourner vers d’autres points de distribution comme emplacements sources de contenu. Cela inclut à la fois les points de distribution cloud et locaux.
Ces améliorations remplacent des concepts et des comportements que vous connaissez peut-être déjà, comme la configuration de la vitesse des points de distribution. Le nouveau modèle est plus facile à configurer et à gérer. Ces modifications servent aussi de base aux futurs changements qui vont améliorer les autres rôles de système de site que vous associez à des groupes de limites.

Quand vous effectuez la mise à jour vers la version 1610, cette dernière convertit les configurations de votre groupe de limites actuel pour les adapter au nouveau modèle, afin que ces modifications ne perturbent pas les configurations de distribution de contenu existantes.

Pour plus d’informations, consultez [Groupes de limites](/sccm/core/servers/deploy/configure/define-site-boundaries-and-boundary-groups#a-namebkmkboundarygroupsa-boundary-groups).


## <a name="peer-cache-for-content-distribution-to-clients"></a>Cache d’homologue pour la distribution de contenu aux clients
À partir de la version 1610, le **cache d’homologue** vous permet de gérer le déploiement de contenu sur les clients distants. Le cache de pair est une solution Configuration Manager intégrée pour permettre aux clients de partager du contenu avec d’autres clients directement à partir de leur cache local.

Une fois que vous avez déployé des paramètres du client qui activent le cache d’homologue sur un regroupement, les membres de ce regroupement peuvent agir comme source de contenu homologue pour d’autres clients du même groupe de limites.

Vous pouvez également utiliser le nouveau tableau de bord **Sources de données du client** pour comprendre l’utilisation des sources de contenu du cache d’homologue dans votre environnement.

> [!TIP]  
> Avec la version 1610, le cache d’homologue et le tableau de bord Sources de données du client sont des fonctionnalités en préversion. Pour les activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

Pour plus d’informations, consultez [Cache de pair pour les clients Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache) et [Tableau de bord Sources de données du client](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed#client-data-sources-dashboard).


## <a name="migrate-multiple-shared-distribution-points-at-the-same-time"></a>Migrer plusieurs points de distribution partagés en même temps
Vous pouvez maintenant utiliser l’option permettant de **Réattribuer un point de distribution** pour que Configuration Manager traite en parallèle la réattribution simultanée de 50 points de distribution partagés. Avant cette version, les points de distribution réattribués étaient traités un par un. Pour plus d’informations, consultez [Migrer plusieurs points de distribution partagés en même temps](/sccm/core/migration/planning-a-content-deployment-migration-strategy#migrate-multiple-shared-distribution-points-at-the-same-time).

## <a name="cloud-management-gateway-for-managing-internet-based-clients"></a>Passerelle de gestion cloud pour la gestion des clients sur Internet

La passerelle de gestion cloud fournit un moyen simple de gérer les clients Configuration Manager sur Internet. Le service de passerelle de gestion cloud, qui est déployé sur Microsoft Azure et nécessite un abonnement Azure, se connecte à votre infrastructure Configuration Manager locale à l’aide d’un nouveau rôle appelé « point de connexion de la passerelle de gestion cloud ». Après son déploiement et sa configuration, les clients peuvent communiquer avec les rôles de système de site Configuration Manager locaux et les points de distribution cloud, qu’ils soient connectés au réseau privé interne ou à Internet. Pour plus d’informations et pour comparer la passerelle de gestion cloud à la gestion des clients sur Internet, consultez [Gérer des clients sur Internet](/sccm/core/clients/manage/manage-clients-internet).

## <a name="improvements-to-the-windows-10-edition-upgrade-policy"></a>Améliorations de la stratégie de mise à niveau de l’édition Windows 10
Dans cette version, les améliorations suivantes ont été apportées à ce type de stratégie :

- Vous pouvez maintenant utiliser la stratégie de mise à niveau d’édition avec des PC Windows 10 qui exécutent le client Configuration Manager en plus des PC Windows 10 inscrits avec Microsoft Intune.
- Vous pouvez effectuer la mise à niveau à partir de Windows 10 Professionnel vers l’une des plateformes de l’Assistant qui sont compatibles avec votre matériel.

## <a name="manage-hardware-identifiers"></a>Gérer les identificateurs de matériel
Vous pouvez désormais fournir la liste des ID de matériel que Configuration Manager doit ignorer dans le cadre du démarrage PXE et de l’inscription des clients. Cette fonctionnalité permet de résoudre deux problèmes courants :

1. De nombreux appareils, comme la Surface Pro 3, n’intègrent pas de port Ethernet. Une carte USB-Ethernet est généralement utilisée pour établir une connexion filaire afin de déployer un système d’exploitation. Toutefois, en raison du coût et de la facilité d’utilisation, il s’agit souvent de cartes partagées. Étant donné que l’adresse MAC de cette carte est utilisée pour identifier l’appareil, la réutilisation de cette carte nécessite l’intervention supplémentaire d’un administrateur entre chaque déploiement. La version 1610 de Configuration Manager permet désormais d’exclure l’adresse MAC de cette carte pour faciliter sa réutilisation dans ce scénario.
2. L’ID SMBIOS est supposé être un identificateur de matériel unique, mais certains appareils spécialisés sont créés avec des ID dupliqués. Ce problème n’est peut-être pas aussi fréquent que le scénario relatif à l’adaptateur USB-Ethernet décrit ci-dessus, mais vous pouvez le résoudre à l’aide de la liste des ID de matériel exclus.

Pour plus d’informations, consultez [Gérer les identificateurs de matériel dupliqués](/sccm/core/clients/manage/manage-clients#manage-duplicate-hardware-identifiers).

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Améliorations de l’intégration du Windows Store pour Entreprises à Configuration Manager
Modifications de cette version :
- Auparavant, vous pouviez uniquement déployer des applications gratuites à partir du Windows Store pour Entreprises. Configuration Manager prend maintenant aussi en charge le déploiement d’applications sous licence en ligne payantes (pour les appareils Intune inscrits uniquement).
- Vous pouvez désormais lancer une synchronisation immédiate entre le Windows Store pour Entreprises et Configuration Manager.
- Vous pouvez maintenant modifier la clé secrète du client que vous avez obtenue à partir d’Azure Active Directory.
- Vous pouvez supprimer un abonnement au Windows Store.

Pour plus d’informations, consultez [Gérer les applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).


## <a name="policy-sync-for-intune-enrolled-devices"></a>Synchronisation de la stratégie pour les appareils inscrits dans Intune
Vous pouvez désormais demander une synchronisation de la stratégie pour un appareil inscrit dans Intune à partir de la console Configuration Manager au lieu de demander une synchronisation dans l’application Portail d’entreprise sur l’appareil. Les informations sur l’état de la demande de synchronisation sont disponibles dans une nouvelle colonne, appelée **État de la synchronisation à distance** dans la vue des appareils. Les informations sont également disponibles dans la section de données de découverte de la boîte de dialogue **Propriétés** pour chaque appareil.
Pour plus d’informations, consultez [Synchroniser à distance la stratégie sur des appareils inscrits dans Intune à partir de la console Configuration Manager](/sccm/mdm/deploy-use/sync-intune-device).


## <a name="use-compliance-settings-to-configure-windows-defender-settings"></a>Utiliser les paramètres de compatibilité pour configurer les paramètres de Windows Defender
Vous pouvez maintenant configurer les paramètres du client Windows Defender sur des ordinateurs Windows 10 inscrits auprès d’Intune à l’aide d’éléments de configuration de la console Configuration Manager.
Pour plus d’informations, consultez la section **Windows Defender** dans [Créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client).



## <a name="general-improvements-to-software-center"></a>Améliorations générales apportées au Centre logiciel
- Les utilisateurs peuvent désormais demander des applications dans le Centre logiciel, ainsi que le catalogue d’applications.
- Améliorations pour aider les utilisateurs à identifier les logiciels nouveaux et pertinents.

## <a name="new-columns-in-device-collection-views"></a>Nouvelles colonnes dans les affichages de regroupement d’appareils
Vous pouvez désormais afficher les colonnes **IMEI** et **Numéro de série** (pour les appareils iOS) dans les affichages de regroupement d’appareils.
Pour plus d’informations, consultez [Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS](https://docs.microsoft.com/sccm/mdm/deploy-use/predeclare-devices-with-hardware-id).

## <a name="customizable-branding-for-software-center-dialogs"></a>Personnalisation des boîtes de dialogue du Centre logiciel
Une marque personnalisée pour le Centre logiciel a été introduite dans Configuration Manager version 1602. Dans la version 1610, cette marque est désormais étendue à toutes les boîtes de dialogue associées pour fournir une expérience plus cohérente aux utilisateurs du Centre logiciel.

Une marque personnalisée pour le Centre logiciel est appliquée selon les règles suivantes :

- Si le rôle de serveur de site du point du site web du catalogue des applications n’est pas installé, le Centre logiciel affiche le nom d’organisation spécifié dans le paramètre client de l’**Agent ordinateur** **Nom d’organisation affiché dans le Centre logiciel**. Pour obtenir des instructions, consultez [Guide pratique pour configurer les paramètres client](../../clients/deploy/configure-client-settings.md).

- Si le rôle de serveur site de point du site web du catalogue des applications est installé, le Centre logiciel affiche le nom d’organisation et la couleur spécifiés dans les propriétés du rôle de serveur de site du point du site web du catalogue des applications. Pour plus d’informations, consultez [Options de configuration pour le point du site web du catalogue des applications](/sccm/core/servers/deploy/configure/configuration-options-for-site-system-roles#Application-Catalog-website-point).

- Si un abonnement Microsoft Intune est configuré et connecté à l’environnement Configuration Manager, le Centre logiciel affiche le nom d’organisation, la couleur et le logo de l’entreprise spécifiés dans les propriétés de l’abonnement Intune. Pour plus d’informations, consultez [Configuration de l’abonnement Microsoft Intune](/sccm/mdm/deploy-use/setup-hybrid-mdm#step-3-configure-intune-subscription).


## <a name="enforcement-grace-period-for-required-application-and-software-update-deployments"></a>Période de grâce d’application pour les déploiements de mises à jour logicielles et d’applications obligatoires
Dans certains cas, vous pouvez accorder plus de temps aux utilisateurs pour installer les mises à jour logicielles ou les déploiements d’applications obligatoires au-delà des échéances que vous avez définies. Par exemple, cela peut être nécessaire lorsqu’un ordinateur a été éteint pendant une période de temps prolongée et qu’il doit installer un grand nombre de déploiements d’applications ou de mises à jour. Par exemple, si un utilisateur final vient de rentrer de congés, il peut être amené à patienter longtemps pendant l’installation des déploiements d’applications en retard. Pour résoudre ce problème, vous pouvez désormais définir une période de grâce de mise en œuvre en déployant des paramètres du client Configuration Manager sur un regroupement. 

Pour configurer la période de grâce, procédez comme suit :
1. Dans la page **Agent ordinateur** des paramètres du client, configurez la nouvelle propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** avec une valeur comprise entre **1** et **120** heures.
2. Dans un nouveau déploiement d’application exigé, ou dans les propriétés d’un déploiement existant, dans la page **Planification**, cochez la case **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres client**. Tous les déploiements pour lesquels cette case est cochée et qui sont destinés à des appareils sur lesquels vous avez également déployé le paramètre du client utilisent la période de grâce de mise en œuvre.

Si vous configurez une période de grâce de mise en œuvre et cochez la case, une fois que l’échéance d’installation d’application est atteinte, l’application est installée dans la première fenêtre non professionnelle que l’utilisateur a configurée jusqu’à cette période de grâce. Toutefois, l’utilisateur peut toujours ouvrir le Centre logiciel et installer l’application à tout moment, s’il le souhaite. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard. Des options similaires ont été ajoutées dans l’Assistant de déploiement de mises à jour logicielles, dans l’Assistant des règles de déploiement automatique et dans les pages de propriétés.



## <a name="improved-functionality-in-dialog-boxes-about-required-software"></a>Fonctionnalités améliorées dans les boîtes de dialogue concernant les logiciels exigés
Quand un utilisateur reçoit des logiciels requis, dans le paramètre **Répéter et me le rappeler :**, il peut choisir parmi les valeurs suivantes de la liste déroulante : 
- **Ultérieurement**. Indique que les notifications sont planifiées selon les paramètres de notification configurés dans les paramètres de l’agent du client.
- **Heure fixe**. Indique que la notification sera programmée pour s’afficher de nouveau après l’heure sélectionnée (par exemple, dans les 30 minutes).

![Page Agent ordinateur dans les paramètres de l’agent du client](media/client-notification-settings.png)

L’heure de répétition maximale est basée sur les valeurs de notification dans les paramètres de l’agent du client. Par exemple, si le paramètre **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)** dans la page Agent ordinateur est configuré pour 10 heures et qu’il reste plus de 24 heures avant l’échéance, l’utilisateur se voit proposer un ensemble d’options de répétition toujours inférieures ou égales à 10 heures. Au fur et à mesure que l’échéance approche, le nombre d’options disponibles diminue, conformément aux paramètres appropriés de l’agent du client, pour chaque composant de la chronologie du déploiement.

Par ailleurs, pour un déploiement à haut risque, comme une séquence de tâches déployant un système d’exploitation, l’expérience de notification à l’utilisateur final est désormais plus intrusive. Au lieu d’une notification temporaire sur la barre des tâches, chaque fois que l’utilisateur est averti qu’une maintenance logicielle critique est nécessaire, une boîte de dialogue similaire à la suivante s’affiche sur l’ordinateur de l’utilisateur :

![Boîte de dialogue Logiciel requis](media/client-toast-notification.png)


Pour plus d’informations :
- [Paramètres de gestion des déploiements à haut risque](../../../protect/understand/settings-to-manage-high-risk-deployments.md)
- [Guide pratique pour configurer les paramètres client](../../clients/deploy/configure-client-settings.md)

## <a name="software-updates-dashboard"></a>Tableau de bord des mises à jour logicielles
Utilisez le nouveau tableau de bord des mises à jour logicielles pour afficher l’état de compatibilité actuel des appareils de votre organisation et analyser rapidement les données pour identifier les appareils vulnérables. Pour afficher le tableau de bord, accédez à **Surveillance** > **Vue d’ensemble** > **Sécurité** > **Tableau de bord des mises à jour logicielles**.

Pour plus d’informations, consultez [Surveiller les mises à jour logicielles](/sccm/sum/deploy-use/monitor-software-updates).


## <a name="improvements-to-the-application-request-process"></a>Améliorations apportées au processus de demande d’application
Une fois que vous avez approuvé l’installation d’une application, vous pouvez ensuite choisir de refuser la demande en cliquant sur **Refuser** dans la console Configuration Manager. Avant, ce bouton était grisé après l’approbation.

Cette action n’entraîne pas la désinstallation de l’application de tous les appareils. Toutefois, elle empêche les utilisateurs d’installer de nouvelles copies de l’application à partir du Centre logiciel.

## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtrer par taille de contenu dans les règles de déploiement automatique
Vous pouvez désormais filtrer sur la taille du contenu des mises à jour logicielles dans les règles de déploiement automatique. Par exemple, pour télécharger uniquement les mises à jour logicielles inférieures à 2 Mo, vous pouvez définir le filtre **Taille du contenu (Ko)** sur  **< 2048**. Ce filtre empêche le téléchargement automatique des mises à jour logicielles volumineuses, d’où une meilleure prise en charge de la maintenance de bas niveau Windows simplifiée quand la bande passante du réseau est limitée. Pour plus d’informations, consultez :
- [Configuration Manager et maintenance Windows simplifiée sur des systèmes d’exploitation de bas niveau](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/)
- [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates)

Pour configurer le champ **Taille du contenu (Ko)**, effectuez l’une des opérations suivantes :
- Quand vous créez une règle de déploiement automatique, dans l’Assistant Création d’une règle de déploiement automatique, accédez à la page **Mises à jour logicielles**.
- Dans les propriétés d’une règle de déploiement automatique existante, accédez à l’onglet **Mises à jour logicielles**.

## <a name="office-365-client-management-dashboard"></a>Tableau de bord Gestion des clients Office 365
Le tableau de bord de gestion des clients Office 365 est désormais disponible dans la console Configuration Manager. Pour afficher le tableau de bord, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.

Le tableau de bord affiche des graphiques pour les éléments suivants :

- Nombre de clients Office 365
- Versions du client Office 365
- Langues du client Office 365
- Canaux du client Office 365     

Pour plus d’informations, consultez [Gérer les mises à jour Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates).

## <a name="task-sequence-steps-to-manage-bios-to-uefi-conversion"></a>Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI
Vous pouvez maintenant personnaliser une séquence de tâches de déploiement de système d’exploitation avec une nouvelle variable, TSUEFIDrive, afin que l’étape **Redémarrer l’ordinateur** prépare une partition FAT32 sur le disque dur pour la transition vers UEFI. La procédure suivante fournit un exemple de création des étapes de séquence de tâches pour préparer le disque dur pour la conversion du BIOS en UEFI. Pour plus d’informations, consultez [Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion).

##  <a name="improvements-to-the-task-sequence-step-prepare-configmgr-client-for-capture"></a>Améliorations apportées à l’étape de séquence de tâches : Prepare ConfigMgr Client for Capture  
L’étape de préparation du client ConfigMgr va désormais supprimer complètement le client Configuration Manager, au lieu de supprimer uniquement des informations clés. Quand la séquence de tâches déploie l’image capturée du système d’exploitation, elle installe un nouveau client Configuration Manager chaque fois. Pour plus d’informations, consultez [Étapes de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_PrepareConfigMgrClientforCapture).



## <a name="intune-compliance-policy-charts"></a>Graphiques de stratégie de conformité Intune
Vous pouvez désormais obtenir un aperçu rapide de la conformité globale des appareils et les principales raisons de non-conformité à l’aide des nouveaux graphiques sous l’espace de travail **Surveillance** dans la console Configuration Manager. Cliquez sur une section dans le graphique pour afficher la liste des appareils dans cette catégorie. Pour plus d’informations, consultez [Surveiller la stratégie de conformité](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy).


## <a name="lookout-integration-for-hybrid-implementations-to-protect-ios-and-android-devices"></a>Intégration de Lookout pour les implémentations hybrides afin de protéger les appareils iOS et Android
Microsoft intègre la solution Mobile Threat Protection de Lookout pour protéger les appareils mobiles iOS et Android en détectant les programmes malveillants, les applications présentant des risques, et bien plus encore, sur les appareils. La solution de Lookout vous permet de déterminer le niveau de menace, qui est configurable. Vous pouvez créer une règle de stratégie de conformité dans System Configuration Manager pour déterminer la conformité des appareils en fonction de l’évaluation des risques par Lookout. À l’aide de stratégies d’accès conditionnel, vous pouvez autoriser ou bloquer l’accès aux ressources d’entreprise en fonction de l’état de conformité de l’appareil. Pour en savoir plus sur l’intégration et son fonctionnement, consultez [Gérer l’accès en fonction de l’appareil, du réseau et du risque encouru au niveau de l’application](/sccm/protect/deploy-use/manage-access-based-on-device-network-app-risk).

Les utilisateurs finaux d’appareils iOS non conformes sont invités à s’inscrire. Ils doivent installer l’application Lookout for Work sur leurs appareils, l’activer et corriger les menaces signalées dans l’application pour avoir accès aux données de la société. Découvrez comment [Configurer et déployer les applications Lookout for Work](/sccm/protect/deploy-use/configure-and-deploy-lookout-for-work-apps).



## <a name="new-compliance-settings-for-configuration-items"></a>Nouveaux paramètres de compatibilité pour les éléments de configuration
Il existe de nombreux nouveaux paramètres que vous pouvez utiliser dans vos éléments de configuration pour diverses plateformes d’appareils. Il s’agit de paramètres qui existaient précédemment dans Microsoft Intune dans une configuration autonome et qui sont maintenant disponibles quand vous utilisez Intune avec Configuration Manager.
Pour plus d’informations, consultez [Éléments de configuration pour les appareils gérés sans le client System Center Configuration Manager](/sccm/compliance/deploy-use/configuration-items-for-devices-managed-without-the-client).

### <a name="new-settings-for-android-devices"></a>Nouveaux paramètres pour les appareils Android
#### <a name="password-settings"></a>Paramètres de mot de passe
- **Mémoriser l’historique des mots de passe**
- **Autoriser le déverrouillage par empreinte digitale**

#### <a name="security-settings"></a>Paramètres de sécurité
- **Exiger le chiffrement sur les cartes de stockage**
- **Autoriser la capture d’écran**
- **Autoriser la soumission des données de diagnostic**

#### <a name="browser-settings"></a>Paramètres du navigateur
- **Autoriser le navigateur web**
- **Autoriser le remplissage automatique**
- **Autoriser le bloqueur de fenêtres publicitaires**
- **Autoriser les cookies**
- **Autoriser les scripts actifs**

#### <a name="app-settings"></a>Paramètres de l’application
- **Autoriser Google Play Store**

#### <a name="device-capability-settings"></a>Paramètres de capacité des appareils
- **Autoriser le stockage amovible**
- **Autoriser la connexion Wi-Fi**
- **Autoriser la géolocalisation**
- **Autoriser NFC**
- **Autoriser Bluetooth**
- **Autoriser l’itinérance vocale**
- **Autoriser l’itinérance des données**
- **Autoriser les messages SMS/MMS**
- **Autoriser l’assistant vocal**
- **Autoriser la composition vocale**
- **Autoriser la fonction copier-coller**

### <a name="new-settings-for-ios-devices"></a>Nouveaux paramètres pour les appareils iOS
#### <a name="password-settings"></a>Paramètres de mot de passe
- **Nombre de caractères complexes requis dans le mot de passe**
- **Autoriser les mots de passe simples**
- **Minutes d’inactivité avant demande du mot de passe**
- **Mémoriser l’historique des mots de passe**

### <a name="new-settings-for-mac-os-x-devices"></a>Nouveaux paramètres pour les appareils Mac OS X
#### <a name="password-settings"></a>Paramètres de mot de passe
- **Nombre de caractères complexes requis dans le mot de passe**
- **Autoriser les mots de passe simples**
- **Mémoriser l’historique des mots de passe**
- **Minutes d’inactivité avant activation de l’écran de veille**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Nouveaux paramètres pour les appareils Windows 10 Desktop et Mobile
#### <a name="password-settings"></a>Paramètres de mot de passe
- **Nombre minimum de jeux de caractères**
- **Mémoriser l’historique des mots de passe**
- **Exiger un mot de passe quand l’appareil quitte un état inactif**

#### <a name="security-settings"></a>Paramètres de sécurité
- **Exiger le chiffrement sur l’appareil mobile**
- **Autoriser la désinscription manuelle**

#### <a name="device-capability-settings"></a>Paramètres de capacité des appareils
- **Autoriser une connexion VPN sur un réseau cellulaire**
- **Autoriser l’itinérance VPN sur un réseau cellulaire**
- **Autoriser la réinitialisation du téléphone**
- **Autoriser la connexion USB**
- **Autoriser Cortana**
- **Autoriser les notifications du centre de notifications**

### <a name="new-settings-for-windows-10-team-devices"></a>Nouveaux paramètres pour les appareils Windows 10 Collaboration
#### <a name="device-settings"></a>Paramètres de l’appareil
- **Activer Azure Operational Insights**
- **Activer la projection sans fil Miracast**
- **Choisir les informations relatives à la réunion affichées sur l’écran d’accueil**
- **URL de l’image d’arrière-plan de l’écran de verrouillage**

### <a name="new-settings-for-windows-81-devices"></a>Nouveaux paramètres pour les appareils Windows 8.1
#### <a name="applicability-settings"></a>Paramètres de mise en application
- **Appliquer toutes les configurations à Windows 10**

#### <a name="password-settings"></a>Paramètres de mot de passe
- **Type de mot de passe requis**
- **Nombre minimum de jeux de caractères**
- **Longueur minimale du mot de passe**
- **Nombre d’échecs de connexion successifs autorisé avant réinitialisation de l’appareil**
- **Minutes d’inactivité avant arrêt de l’écran**
- **Expiration du mot de passe (jours)**
- **Mémoriser l’historique des mots de passe**
- **Empêcher la réutilisation des mots de passe précédents**
- **Autoriser un mot de passe image et un code confidentiel**

#### <a name="browser-settings"></a>Paramètres du navigateur
- **Autoriser la détection automatique des réseaux intranet**

### <a name="new-settings-for-windows-phone-81-devices"></a>Nouveaux paramètres pour les appareils Windows Phone 8.1
#### <a name="applicability-settings"></a>Paramètres de mise en application
- **Appliquer toutes les configurations à Windows 10**

#### <a name="password-settings"></a>Paramètres de mot de passe
- **Nombre minimum de jeux de caractères**
- **Autoriser les mots de passe simples**
- **Mémoriser l’historique des mots de passe**

#### <a name="device-capability-settings"></a>Paramètres de capacité des appareils
- **Autoriser la connexion automatique aux points d’accès Wi-Fi gratuits**
