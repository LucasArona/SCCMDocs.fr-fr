---
title: Nouveautés dans la version 1606
titleSuffix: Configuration Manager
description: Obtenez des informations détaillées sur les modifications et les nouvelles fonctionnalités introduites dans la version 1606 de System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: df2e57b9-6445-4067-98e7-ace85d4e6aa6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: dfc10695dc238e7020fd9d1b777ce62d80324beb
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133484"
---
# <a name="what39s-new-in-version-1606-of-system-center-configuration-manager"></a>Nouveautés dans la version 1606 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1606 pour System Center Configuration Manager est disponible sous la forme d’une mise à jour dans la console pour les sites précédemment installés qui exécutent la version 1511 ou 1602. La version 1511 est la version de référence initiale qui permet d’installer de nouveaux sites Configuration Manager.
> [!TIP]  
>  Informations supplémentaires :  
>   
>  -   [Installation de nouveaux sites](/sccm/core/servers/deploy/install) (à l’aide d’une version de référence telle que 1511)  
>  -   [Installation de mises à jour sur les sites](/sccm/core/servers/manage/updates) (telles que la mise à jour 1602 ou 1606)  

 Les sections suivantes fournissent des informations détaillées sur les modifications et les nouvelles fonctionnalités introduites dans la version 1606 de Configuration Manager.  



## <a name="updatesandservicing"></a>Mises à jour et maintenance

### <a name="changes-for-the-updates-and-servicing-node"></a>Modifications pour le nœud Mises à jour et maintenance
Les modifications apportées au nœud Mises à jour et maintenance dans la console Configuration Manager sont les suivantes :
> [!NOTE]
> Ces modifications sont disponibles seulement une fois la version 1606 installée.

- **Changement de nom de nœud :**

    Dans l’espace de travail **Surveillance**, le nœud **État de maintenance du site** a été renommé en **État des mises à jour et de la maintenance**.
- **État de l’installation plus détaillé :**

    Quand vous affichez l’état de l’installation d’une mise à jour pour un site, la console affiche maintenant les détails pour chacune des actions suivantes :
    - **Téléchargement** (Ceci s’applique uniquement au site de niveau de plus haut niveau où est installé le rôle de système de site de point de connexion de service.)
    - **Réplication**
    - **Vérification des prérequis**
    - **Installation**

  De plus, des informations plus détaillées sont désormais fournies pour chaque étape, notamment le fichier journal que vous pouvez consulter pour obtenir plus d’informations.  
-   **Nouvelle option pour retenter l’installation après l’échec de la vérification des prérequis :**

    Dans les espaces de travail **Administration** et **Surveillance**, le nœud **Mises à jour et maintenance** comprend un nouveau bouton **Ignorer les avertissements de configuration requise** sur le ruban.

    Quand vous installez des mises à jour sans utiliser l’option Ignorer les avertissements de configuration requise (depuis l’Assistant Mises à jour) et que l’installation des mises à jour s’arrête en raison d’un avertissement, vous pouvez sélectionner **Ignorer les avertissements de configuration requise** dans le ruban. Ceci déclenche une poursuite automatique de l’installation de la mise à jour.  



- **Vue plus claire des mises à jour :**

    Dans le nœud **Mises à jour et maintenance**, vous voyez désormais seulement la dernière mise à jour que vous avez installée, ainsi que les nouvelles mises à jour prêtes à être installées. Pour afficher les mises à jour précédemment installées, cliquez sur le nouveau bouton **Historique** qui apparaît dans le ruban.  

-   **Option renommée pour la pré-production :**

    Dans le nœud **Mises à jour et maintenance**, le bouton **Options du client** s’appelle désormais **Promouvoir le client de préproduction**.


###  <a name="pre-release-features"></a>Fonctionnalités de préversion
À compter de la version 1606, vous devez donner votre consentement pour utiliser les fonctionnalités de préversion de System Center Configuration Manager avant de pouvoir les sélectionner et activer leur utilisation. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversions de mises à jour](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="new-distribution-point-update-behavior"></a>Nouveau comportement de mise à jour des points de distribution
La mise à jour 1606 apporte des modifications qui améliorent la disponibilité des points de distribution quand vous installez les mises à jour ultérieures.

Si, après avoir installé la mise à jour 1606, vous installez une nouvelle mise à jour sur le même site qui nécessite la réinstallation automatique des rôles de système de site pour les points de distribution standard et d’extraction, la mise à jour peut désormais s’effectuer en même temps, sans avoir besoin de mettre tous les points de distribution en mode hors connexion. Au lieu de cela, le serveur de site utilise les paramètres de distribution de contenu du site pour distribuer la mise à jour un sous-ensemble de points de distribution à n’importe quel moment. Le résultat est que seuls certains points de distribution sont mis en mode hors connexion pour installer la mise à jour. Ainsi, les points de distribution dont la mise à jour n’a pas encore commencé ou est terminée restent en ligne et peuvent fournir du contenu aux clients.



## <a name="accessibility"></a> Accessibilité
Vous pouvez désormais accéder aux différents nœuds d’un espace de travail en entrant la première lettre du nom d’un nœud. Chaque appui sur une touche déplace le curseur au nœud suivant qui commence par cette lettre. Pour les utilisateurs disposant d’un lecteur d’écran, le lecteur lit le nom de ce nœud. Pour plus d’informations sur les options d’accessibilité, consultez [Fonctionnalités d’accessibilité dans System Center Configuration Manager](../../../core/understand/accessibility-features.md).

## <a name="administration"></a>Administration
Les modifications apportées au nœud Administration dans la console Configuration Manager sont les suivantes :
### <a name="oms-connector"></a>Connecteur OMS

Vous pouvez désormais connecter Configuration Manager comme des regroupements de System Center Configuration Manager à [Microsoft Operations Management Suite (OMS)](https://azure.microsoft.com/documentation/articles/operations-management-suite-overview/). Les données de votre déploiement Configuration Manager, telles que les regroupements, deviennent alors visibles dans OMS. Pour plus d’informations, consultez [Synchroniser les données de Configuration Manager vers Microsoft Operations Management Suite](../../../core/clients/manage/sync-data-microsoft-operations-management-suite.md).

La fonctionnalité Connecteur OMS est une préversion. Pour savoir comment l’activer, consultez [Utiliser des fonctionnalités de préversion des mises à jour](../../../core/servers/manage/install-in-console-updates.md#bkmk_prerelease).

### <a name="support-for-cache-size-in-client-settings"></a>Configuration de la taille du cache dans les paramètres du client

Vous pouvez désormais configurer la taille du dossier du cache sur les ordinateurs clients à l’aide des **Paramètres du client** dans la console Configuration Manager. Auparavant, vous pouviez définir la taille du cache du client seulement au moment de l’installation ou de la réinstallation du logiciel client. Vous pouvez désormais spécifier la taille du cache comme un paramètre du client (par défaut ou personnalisé), puis appliquer ce paramètre avec la prochaine mise à jour de la stratégie sur le client sans avoir besoin de réinstaller le client. Pour plus d'informations, voir [Configurer le cache du client pour les clients Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_ClientCache).

## <a name="on-premises-mobile-device-management"></a>Gestion locale des appareils mobiles

### <a name="support-for-multiple-device-management-points"></a>Prise en charge de plusieurs points de gestion de l’appareil

La gestion des appareils mobiles (MDM) locale prend désormais en charge une nouvelle fonctionnalité dans la Mise à jour anniversaire Windows 10, qui configure automatiquement un appareil inscrit avec plusieurs points de gestion de l’appareil à sa disposition. Cette fonctionnalité permet à l’appareil de basculer vers un autre point de gestion d’appareil quand celui qu’il utilise normalement n’est pas disponible. Elle peut être utilisée uniquement pour des PC et des appareils où la Mise à jour anniversaire Windows 10 a été installée.


## <a name="application-management"></a>Gestion des applications

### <a name="manage-apps-from-the-windows-store-for-business"></a>Gérer les applications à partir du Windows Store pour Entreprises

Le [Windows Store pour Entreprises](https://www.microsoft.com/business-store) vous permet de trouver et d’acheter individuellement ou en volume des applications Windows pour votre organisation. En connectant le Windows Store à Configuration Manager, vous pouvez synchroniser la liste des applications que vous avez achetées avec Configuration Manager, les afficher dans la console Configuration Manager et les déployer comme n’importe quelle autre application.

Pour plus d’informations, consultez [Gérer les applications à partir du Windows Store pour Entreprises avec System Center Configuration Manager](../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).

### <a name="manage-ios-volume-purchased-apps"></a>Gérer les applications iOS achetées en volume

Le workflow pour gérer et déployer des applications iOS achetées en volume avec Configuration Manager a été amélioré.

Pour plus d’informations, consultez [Gérer les applications iOS achetées en volume avec System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).

### <a name="software-center-user-interface"></a>Interface utilisateur du Centre logiciel

L’interface utilisateur du Centre logiciel a été simplifiée pour faciliter la découverte.
*  Les onglets **État de l’installation** et **Logiciel installé** ont été combinés en un seul onglet **État de l’installation**.
*  Les éléments **Mises à jour**, **Systèmes d’exploitation** et **Applications** ont été séparés en trois onglets distincts.
* Vous pouvez désormais sélectionner plusieurs mises à jour à installer à la fois ou choisir d’installer la totalité des mises à jour en une seule fois en cliquant sur le bouton **Tout installer**.

### <a name="content-status-links"></a>Liens vers des informations sur l’état du contenu
Sur les propriétés d’une application ou d’un package, vous pouvez maintenant cliquer sur un lien qui vous renvoie vers des informations sur l’état de cet objet.

## <a name="software-updates"></a>Mises à jour logicielles

### <a name="client-setting-to-manage-the-office-365-client-agent"></a>Paramètre du client pour gérer l’agent Office 365 Client
Vous pouvez maintenant utiliser un paramètre du client Configuration Manager pour gérer l’agent Office 365 Client. Après avoir configuré ce paramètre et déployé les mises à jour d’Office 365, l’agent client Configuration Manager travaille en combinaison avec l’agent Office 365 Client pour télécharger et installer les mises à jour d’Office 365 à partir d’un point de distribution.

Pour plus d’informations, consultez [Gérer les mises à jour d’Office 365 ProPlus avec Configuration Manager](../../../sum/deploy-use/manage-office-365-proplus-updates.md).

### <a name="manually-switch-clients-to-a-new-software-update-point"></a>Basculement manuel des clients vers un autre point de mise à jour logicielle
Vous pouvez désormais activer l’option permettant aux clients Configuration Manager de basculer vers un autre point de mise à jour logicielle quand ils rencontrent des problèmes avec le point de mise à jour logicielle actif. Une fois l’option activée, les clients rechercheront un autre point de mise à jour logicielle lors de la prochaine analyse.

Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_ManuallySwitchSUPs).

### <a name="restart-options-for-windows-10-clients-after-software-update-installation"></a>Options de redémarrage pour les clients Windows 10 après l’installation de mises à jour logicielles
Quand une mise à jour logicielle nécessitant un redémarrage est déployée à l’aide de Configuration Manager et installée sur un ordinateur, un redémarrage en attente est planifié. Une boîte de dialogue de redémarrage s’affiche également. À compter de Configuration Manager version 1606, les options **Mettre à jour et redémarrer**et **Mettre à jour et arrêter** sont disponibles quand un redémarrage est en attente pour une mise à jour logicielle Configuration Manager. Elles sont disponibles dans les options d’alimentation Windows des ordinateurs Windows 10. Une fois qu’une de ces options a été utilisée, la boîte de dialogue de redémarrage ne s’affiche plus après le redémarrage de l’ordinateur.

Pour plus d’informations, consultez [Planifier les mises à jour logicielles dans Configuration Manager](../../../sum/plan-design/plan-for-software-updates.md#BKMK_RestartOptions).

### <a name="run-software-updates-compliance-scan-immediately-after-a-client-installs-software-updates-and-restarts"></a>Exécuter l’analyse de conformité des mises à jour logicielles immédiatement après l’installation des mises à jour logicielles sur un client et son redémarrage
Vous pouvez désormais exécuter l’analyse de conformité immédiatement après l’installation des mises à jour logicielles sur un client et son redémarrage. Pour configurer ce comportement pour un déploiement, dans la page **Expérience utilisateur** de l’Assistant Déploiement des mises à jour logicielles, sélectionnez **Si une mise à jour dans ce déploiement requiert un redémarrage du système, exécuter le cycle d’évaluation du déploiement des mises à jour après le redémarrage**. Ceci permet au client de vérifier la disponibilité de mises à jour logicielles supplémentaires devenues applicables après le redémarrage, puis de les installer (et de devenir ainsi conforme) au cours d’une même fenêtre de maintenance. Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates) ou [Déployer manuellement des mises à jour logicielles](/sccm/sum/deploy-use/manually-deploy-software-updates).

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation

### <a name="improvements-to-the-task-sequence-step-install-software-updates"></a>Améliorations apportées à l’étape de séquence de tâches : Installer les mises à jour logicielles
Un nouveau paramètre, **Évaluer les mises à jour logicielles à partir des résultats d’analyse mis en cache**, vous permet d’effectuer une analyse complète des mises à jour logicielles au lieu d’utiliser les résultats d’analyse mis en cache. Pour plus d’informations, consultez [Étapes de séquence de tâches dans System Center Configuration Manager](../../../osd/understand/task-sequence-steps.md#BKMK_InstallSoftwareUpdates).

En outre, une nouvelle variable de séquence de tâches, **SMSTSSoftwareUpdateScanTimeout**, est disponible. Cette variable vous permet de contrôler le délai d’attente pour l’analyse des mises à jour logicielles à l’étape de la séquence de tâches Installer les mises à jour logicielles. La valeur par défaut est de 30 minutes. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches dans System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="osdpreservedriveletter-task-sequence-variable-has-been-deprecated"></a>La variable de séquence de tâches OSDPreserveDriveLetter est déconseillée
La variable de séquence de tâches OSDPreserveDriveLetter a été dépréciée. À compter de la version 1606 de Configuration Manager, le programme d’installation de Windows détermine la meilleure lettre de lecteur à utiliser (généralement, C:) pendant le déploiement d’un système d’exploitation, par défaut.

Pour plus d’informations, consultez [Variables intégrées de séquence de tâches dans System Center Configuration Manager](../../../osd/understand/task-sequence-built-in-variables.md).

### <a name="customize-the-ramdisk-tftp-window-size-for-pxe-enabled-distribution-points"></a>Personnalisation de la taille de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE
Vous pouvez maintenant personnaliser la taille de fenêtre TFTP RamDisk pour les points de distribution compatibles PXE. Si vous avez personnalisé votre réseau, ceci peut faire échouer le téléchargement de l’image de démarrage avec une erreur de délai d’attente résultant d’une taille de fenêtre trop grande. La personnalisation de la taille de la fenêtre TFTP (Trivial File Transfer Protocol) RamDisk vous permet d’optimiser le trafic TFTP avec PXE en fonction de la configuration réseau spécifique requise.

Pour plus d’informations, consultez [Préparer les rôles de système de site pour les déploiements de système d’exploitation avec System Center Configuration Manager](../../../osd/get-started/prepare-site-system-roles-for-operating-system-deployments.md#BKMK_RamDiskTFTP).

## <a name="compliance-settings"></a>Paramètres de conformité

### <a name="smart-lock-setting-for-android-devices"></a>Paramètre Smart Lock pour les appareils Android
Un nouveau paramètre, **Autoriser Smart Lock et d’autres agents de confiance**, a été ajouté à l’élément de configuration Android et Samsung KNOX Standard.

Ce paramètre vous permet de contrôler la fonctionnalité Smart Lock sur les appareils Android compatibles. Cette fonctionnalité du téléphone, parfois appelée « agents de confiance », vous permet de désactiver ou de contourner le mot de passe de l’écran de verrouillage de l’appareil si celui-ci se trouve à un emplacement approuvé. Par exemple, il est à un emplacement approuvé quand il est connecté à un appareil Bluetooth spécifique ou quand il se trouve à proximité d’une balise NFC. Vous pouvez utiliser ce paramètre pour empêcher les utilisateurs finaux de configurer Smart Lock.

Pour plus d’informations, consultez [Comment créer des éléments de configuration pour des appareils Android et Samsung KNOX Standard gérés sans le client System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).

## <a name="device-configuration-and-protection"></a>Configuration et protection des appareils

### <a name="product-name-changes"></a>Changements de nom de produit

* Microsoft Passport for Work devient **Windows Hello Entreprise**.
* La protection des données d’entreprise s’appelle maintenant **Protection des informations Windows**.

### <a name="deployment-of-windows-hello-for-business-passport-for-work"></a>Déploiement de Windows Hello Entreprise (anciennement Passport for Work)

Vous pouvez maintenant déployer des stratégies Windows Hello Entreprise sur des appareils Windows 10 joints à un domaine et gérés par le client Configuration Manager.

La console Configuration Manager a été mise à jour pour refléter ces modifications.

### <a name="ios-activation-lock"></a>Verrou d’activation iOS
Configuration Manager peut vous aider à gérer le verrou d’activation iOS, fonctionnalité de l’application Rechercher mon iPhone pour les appareils iOS 7.1 et versions ultérieures. Quand le verrou d’activation est activé, l’ID et le mot de passe Apple de l’utilisateur doivent être entrés pour permettre à quiconque de :
* Désactiver Rechercher mon iPhone.
* Effacer l’appareil.
* Réactiver l’appareil.

Configuration Manager peuvent vous aider à gérer le verrou d’activation de deux façons :

- en activant le verrou d’activation sur les appareils supervisés ;
- en contournant le verrou d’activation sur les appareils supervisés.

Pour plus d’informations, consultez [Gérer le verrou d’activation iOS avec System Center Configuration Manager](../../../mdm/deploy-use/manage-ios-activation-lock.md).


### <a name="windows-defender-advanced-threat-protection"></a>Windows Defender - Protection avancée contre les menaces

Endpoint Protection facilite la gestion et la surveillance du service Windows Defender - Protection avancée contre les menaces. Ce nouveau service aide les entreprises à détecter, analyser et contrer les attaques avancées ciblant leurs réseaux. Les stratégies Configuration Manager facilitent l’intégration et la surveillance des ordinateurs gérés qui exécutent Windows 10 version 1607 (build 14328) ou ultérieure.

Pour plus d’informations, consultez [Windows Defender - Protection avancée contre les menaces](../../../protect/deploy-use/windows-defender-advanced-threat-protection.md).

### <a name="device-categories"></a>Catégories d’appareils
Vous pouvez créer des catégories d’appareils pour classer automatiquement les appareils dans des regroupements d’appareils quand vous utilisez Configuration Manager avec Microsoft Intune. Les utilisateurs doivent ensuite choisir une catégorie d’appareils quand ils inscrivent un appareil dans Intune. Vous pouvez aussi modifier la catégorie d’un appareil à partir de la console Configuration Manager.

Pour plus d’informations, consultez [Guide pratique pour classer automatiquement des appareils dans des regroupements avec System Center Configuration Manager](../../../core/clients/manage/collections/automatically-categorize-devices-into-collections.md).

### <a name="predeclare-devices-with-imei-or-ios-serial-numbers"></a>Prédéclarer des appareils avec leur numéro IMEI ou leur numéro de série iOS

Vous pouvez identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity) ou leur numéro de série iOS. Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) contenant les numéros IMEI des appareils ou bien saisir manuellement les informations sur les appareils. Les informations importées définissent la propriété des appareils inscrits sur « Entreprise » dans les listes d’appareils. Une licence Intune reste nécessaire pour chaque utilisateur qui accède au service.

Pour plus d’informations, consultez [Prédéclarer des appareils avec des numéros IMEI ou numéros de série iOS](../../../mdm/deploy-use/predeclare-devices-with-hardware-id.md).

### <a name="on-premises-health-attestation-service-communication"></a>Communication avec le service local d’attestation d’intégrité

Vous pouvez désormais activer la surveillance des services d’attestation d’intégrité pour les PC Windows 10 en utilisant seulement l’infrastructure locale. Ceci permet aux ordinateurs sans accès Internet de signaler l’attestation d’intégrité de l’appareil.

Pour plus d’informations, consultez [Attestation d’intégrité pour System Center Configuration Manager](../../../core/servers/manage/health-attestation.md#how-to-enable-health-attestation-service-communication-on-configuration-manager-client-computers).  

## <a name="remote-control"></a>Contrôle à distance
Donnez à vos utilisateurs la possibilité d’accepter ou de refuser des transferts de fichiers avant de transférer le contenu du Presse-papiers partagé dans une session de contrôle à distance. Les utilisateurs n’ont besoin d’accorder l’autorisation qu’une seule fois par session tandis que l’observateur ne peut pas s’accorder l’autorisation d’effectuer le transfert de fichiers. Vous pouvez trouver ce nouveau paramètre dans l’espace de travail **Administration**. Accédez à **Paramètres du client** puis, dans **Paramètres par défaut**, ouvrez le panneau **Outils de contrôle à distance**.
