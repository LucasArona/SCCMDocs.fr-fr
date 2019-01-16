---
title: Nouvelle version 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Obtenez des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1710 de System Center Configuration Manager.
ms.date: 1/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4dcf5ce0c31f72db1e6af3ac9e024c83afe92337
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250661"
---
# <a name="what39s-new-in-version-1710-of-system-center-configuration-manager"></a>Nouveautés de la version 1710 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1710 de la version Current Branch de System Center Configuration Manager est une mise à jour dans la console des sites déjà installés qui exécutent la version 1610, 1702 ou 1706.

En plus des nouvelles fonctionnalités, cette version inclut également des modifications supplémentaires comme des corrections de bogues. Pour plus d’informations, consultez [Récapitulatif des modifications dans Current Branch de System Center Configuration Manager version 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Les mises à jour supplémentaires suivantes pour cette version sont également disponibles :
- [Correctif cumulatif pour Current Branch de System Center Configuration Manager, version 1710](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Correctif cumulatif 2 pour Current Branch de System Center Configuration Manager, version 1710](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Pour installer un nouveau site, vous devez utiliser une version de base de Configuration Manager.  
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Installation de mises à jour sur les sites](/sccm/core/servers/manage/updates)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Les sections suivantes fournissent des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1710 de Configuration Manager.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastructure de site

### <a name="updates-for-peer-cache-----sms500850---"></a>Mises à jour du Cache d’homologue <!-- sms500850 -->
À compter de cette version, le Cache d’homologue n’est plus une fonctionnalité en préversion.  Aucune nouvelle modification n’est introduite pour le Cache d’homologue avec cette version. Pour plus d’informations, consultez [Cache d’homologue pour les clients Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Prise en charge du point de distribution cloud pour le cloud Azure Government <!-- sms491428 -->
Vous pouvez maintenant utiliser des [points de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point) dans le cloud Azure Government.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Révision de l’unité par défaut pour l’inventaire <!-- sms503697 -->
Les appareils étant désormais équipés de disques durs avec des tailles de plusieurs gigaoctets (Go), téraoctets (To) et plus, cette version utilise le Go (et non plus le mégaoctets (Mo)) comme unité par défaut (SMS_Units) dans de nombreux affichages. Par exemple, la valeur v_gs_LogicalDisk.FreeSpace est désormais exprimée en Go.


<!-- ## Migration  -->


## <a name="client-management"></a>Gestion des clients

### <a name="co-management-for-windows-10-devices"></a>Cogestion pour les appareils Windows 10    
<!-- 1350871 --> Dans les mises à jour précédentes de Windows 10, vous pouvez déjà joindre un appareil Windows 10 simultanément à une instance locale d’Active Directory (AD) et à Azure AD sur le cloud (Azure AD hybride). À compter de Configuration Manager version 1710, la cogestion tire parti de cette amélioration et vous permet de gérer simultanément plusieurs appareils Windows 10, version 1709 (également appelée Fall Creators Update) à l’aide de Configuration Manager et d’Intune. C’est une solution qui établit une passerelle entre la gestion classique et la gestion moderne tout en vous donnant la possibilité d’opérer cette transition selon une approche en plusieurs phases. Pour plus d’informations, consultez [Cogestion pour les appareils Windows 10](/sccm/comanage/overview).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Redémarrer les ordinateurs à partir de la console Configuration Manager <!-- 1356283 -->
À compter de cette version, vous pouvez utiliser la console Configuration Manager pour identifier les périphériques clients qui nécessitent un redémarrage, puis utiliser une action de notification de client pour les redémarrer.

Consultez [Guide pratique pour gérer les clients dans System Center Configuration Manager](/sccm/core/clients/manage/manage-clients#restart-clients)


<!-- ## Compliance settings -->


## <a name="application-management"></a>Gestion des applications
### <a name="improvements-for-run-scripts------1236459---"></a>Améliorations de l’exécution de scripts <!-- 1236459 -->
Cette version apporte plusieurs améliorations à la fonctionnalité **Exécuter les scripts**, ce qui vous permet de déployer des scripts PowerShell à exécuter sur les appareils gérés. Cette fonctionnalité a été introduite dans la version 1706.

Les améliorations apportées incluent :
- Utilisation d’étendues de sécurité pour faciliter le contrôle des utilisateurs autorisés à exécuter des scripts
- Surveillance en temps réel des scripts que vous exécutez
- Paramètres d’affichage des scripts dans l’Assistant Création d’un script, validation prise en charge et identification comme étant obligatoires ou facultatifs.

Pour plus d’informations sur l’utilisation de la fonctionnalité Exécuter les scripts, consultez [Créer et exécuter des scripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Nouveaux paramètres de stratégie de gestion d’application mobile
<!-- 1324760 --> Les paramètres suivants ont été ajoutés aux paramètres de stratégie de gestion des applications mobiles :
- **Désactiver la synchronisation des contacts** : Empêche l’application d’enregistrer des données sur l’application Contacts native de l’appareil.
- **Désactiver l’impression** : Empêche l’application d’imprimer des données scolaires ou de travail.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Le Centre logiciel ne déforme plus les grandes icônes aux dimensions supérieures à 250 x 250  
<!-- 1356194 -->

Avec cette version, le Centre logiciel ne déforme plus les icônes aux dimensions supérieures à 250 x 250. Auparavant, il rendait ces icônes floues. Désormais, vous pouvez définir une icône avec des dimensions maximales de 512 x 512 pixels et l’afficher sans déformation.

Pour ajouter une icône pour votre application dans le Centre logiciel, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications).

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation
 > [!TIP]   
 > <!-- 1354281 --> À compter de la version 1709 de Windows 10 (également appelée Fall Creators Update), Windows Media inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour utiliser un package de mise à niveau de système d’exploitation ou une image de système d’exploitation, veillez à sélectionner une [édition prise en charge par Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Ajouter des séquences de tâches enfants à une séquence de tâches
<!-- 1261338 -->

Vous pouvez ajouter une nouvelle étape de séquence de tâches qui exécute une autre séquence de tâches, créant ainsi une relation parent/enfant entre les séquences de tâches. Cela vous permet de créer et d’utiliser des séquences de tâches plus modulaires.  

Pour plus d’informations sur la séquence de tâches enfant, consultez [Séquence de tâches enfant](/sccm/osd/understand/task-sequence-steps#child-task-sequence).

## <a name="software-center-customization"></a>Personnalisation du Centre logiciel
<!-- 1351224 --> Vous pouvez ajouter des éléments de personnalisation d’entreprise et spécifier la visibilité des onglets du Centre logiciel. Vous pouvez ajouter votre nom de société Centre logiciel spécifique, définir un modèle de couleurs de configuration Centre logiciel, un logo de société et les onglets visibles pour les périphériques clients.

Pour plus d’informations, consultez [Planifier et configurer la gestion des applications dans System Center Configuration Manager](/sccm/apps/plan-design/plan-for-and-configure-application-management).

## <a name="software-updates"></a>Mises à jour logicielles

### <a name="surface-driver-updates-----1098490---"></a>Mises à jour du pilote Surface <!-- 1098490 -->
À partir de cette version, la gestion des mises à jour du pilote Surface n’est plus une fonctionnalité en préversion.  


## <a name="reporting"></a>Rapports

### <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limiter la télémétrie avancée dans Windows 10 pour envoyer uniquement les données pertinentes à Windows Analytics Device Health
<!-- 1356148 -->

Vous pouvez désormais définir la collecte de données de télémétrie dans Windows 10 sur le niveau **Avancé (limité)**. Ce paramètre vous permet d’obtenir un insight actionnable sur les périphériques de votre environnement sans que ces derniers aient à envoyer toutes les données au niveau de télémétrie **Avancé** avec Windows 10 version 1709 ou ultérieure.

Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](/sccm/core/clients/deploy/configure-client-settings).

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Gestion des appareils mobiles

### <a name="actions-for-non-compliance"></a>Actions en cas de non-conformité 
<!--1321366 -->    
Vous pouvez désormais configurer une séquence chronologique d’actions appliquées aux appareils qui ne sont pas conformes. Par exemple, vous pouvez notifier les utilisateurs d’appareils non conformes par e-mail ou marquer ces appareils comme non conformes. Pour plus d’informations, consultez [Configurer des actions en cas de non-conformité](/sccm/mdm/deploy-use/actions-for-noncompliance).

### <a name="windows-10-arm64-device-support"></a>Prise en charge des appareils Windows 10 ARM64
<!-- 1355000 -->

Les scénarios de gestion hybride des appareils mobiles seront pris en charge sur les appareils ARM64 exécutant Windows 10 quand ces appareils seront disponibles.

Ces scénarios sont les suivants :

- [Inscrire des appareils](../../../mdm/deploy-use/enroll-hybrid-windows.md)
- [Effectuer des actions de réinitialisation complète à distance et sélective](../../../mdm/deploy-use/wipe-lock-reset-devices.md)
- [Gérer des paramètres via des éléments de configuration et des lignes de base](../../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md)
- [Gérer la stratégie de conformité](../../../mdm/deploy-use/device-compliance-policies.md) et l’[accès conditionnel](../../../protect/deploy-use/manage-access-to-services.md)
- Activer l’accès aux ressources de l’entreprise par le biais de :
   - [Profils de certificat](../../../mdm/deploy-use/create-pfx-certificate-profiles.md)
   - [Profils VPN](../../../mdm/deploy-use/create-vpn-profiles.md)
   - [Profils Wi-Fi](../../../mdm/deploy-use/create-wifi-profiles.md)
   - [Profils de messagerie](../../../mdm/deploy-use/create-exchange-activesync-profiles.md)
- [Configurer une stratégie Windows Hello Entreprise](../../../mdm/deploy-use/windows-hello-for-business-settings.md)
- [Gérer les applications](../../../mdm/deploy-use/management-tasks-applications.md)

> [!NOTE]
> Le déploiement d’applications .appxbundle générées pour plusieurs architectures peuvent ne pas fonctionner sur ces appareils, et ce scénario n’est pas pris en charge pour l’instant.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Expérience de profil VPN améliorée dans la console Configuration Manager 
<!-- 1318232 -->

Avec cette version, nous avons mis à jour l’Assistant Création d’un profil VPN et les pages de propriétés pour afficher uniquement les paramètres appropriés à la plateforme sélectionnée :


- Chaque plateforme a son propre flux de travail, ce qui signifie que les nouveaux profils VPN ne contiennent que les paramètres pris en charge par la plateforme.
- La page **Plateformes prises en charge** apparaît désormais après la page **Général**.  Maintenant, vous choisissez la plateforme avant de définir les valeurs de propriété.
- Lorsque la plateforme est définie sur **Android**, **Android for Work** ou **Windows Phone 8.1**, la page **Plateformes prises en charge** est inutile et ne s’affiche pas.
- Le flux de travail du client Configuration Manager a été combiné aux flux de travail Windows 10 du client de l’appareil mobile hybride (MDM) ; ils prennent en charge les mêmes paramètres.
- Chaque flux de travail de plateforme inclut uniquement les paramètres appropriés à ce flux de travail.  Par exemple, le flux de travail Android contient les paramètres propres à Android ; les paramètres appropriés pour iOS ou Windows 10 Mobile n’apparaissent donc plus dans le flux de travail Android.
- La page VPN automatique est obsolète et a été supprimée.

Ces modifications s’appliquent aux nouveaux profils VPN.  

Pour réduire les problèmes de compatibilité, les profils VPN existants restent inchangés.  Lorsque vous modifiez un profil existant, les paramètres s’affichent comme au moment de sa création.  

Pour plus d’informations, consultez [Profils VPN sur des appareils mobiles dans System Center Configuration Manager](../../../mdm/deploy-use/create-vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Prise en charge limitée des certificats Cryptography: Next Generation (CNG) <!-- 1356191 -->

Configuration Manager prend en charge de manière limitée les certificats Cryptography: Cryptography: Next Generation (CNG). Les clients Configuration Manager peuvent utiliser un certificat d’authentification client PKI avec une clé privée dans le fournisseur de stockage de clés (KSP) CNG. La prise en charge du KSP permet aux clients Configuration Manager de prendre en charge une clé privée matérielle, comme TPM KSP pour les certificats d’authentification client PKI.

Pour plus d’informations, consultez [Vue d’ensemble des certificats CNG](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Protéger les appareils

### <a name="create-and-deploy-exploit-guard-policies"></a>Créer et déployer des stratégies Exploit Guard
<!-- 1355468 -->

Vous pouvez [créer et déployer des stratégies](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) qui gèrent les quatre composants de Windows Defender Exploit Guard, à savoir la réduction de la surface d’attaque, l’accès contrôlé aux dossiers, Exploit Protection et la protection du réseau.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Créer et déployer une stratégie Windows Defender Application Guard
<!-- 1351960 -->

Vous pouvez [créer et déployer des stratégies Windows Defender Application Guard](/sccm/protect/deploy-use/create-deploy-application-guard-policy) à l’aide de la protection du point de terminaison Configuration Manager.

### <a name="device-guard-policy-changes"></a>Modifications des stratégies Device Guard
<!-- 1355092 --> Les trois modifications suivantes ont été apportées au niveau des stratégies Device Guard :

- Les stratégies Device Guard s’appellent désormais les stratégies Windows Defender Application Control. Ainsi, par exemple, l’**Assistant Créer une stratégie Device Guard** s’appelle désormais l’**Assistant Créer une stratégie Windows Defender Application Control**.
- Les appareils qui utilisent Fall Creators Update pour Windows version 1709 n’ont pas besoin de redémarrage pour appliquer les stratégies Windows Defender Application Control. Le redémarrage est toujours la valeur par défaut, mais vous pouvez [désactiver les redémarrages](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager).
- Vous pouvez [définir les appareils pour qu’ils exécutent automatiquement les logiciels](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) approuvés par Intelligent Security Graph.





## <a name="next-steps"></a>Étapes suivantes
Quand vous êtes prêt à installer cette version, consultez [Mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates).
