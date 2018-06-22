---
title: Version Technical Preview 1710 | Microsoft Docs
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1710 de System Center Configuration Manager.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 730d14c5985c088d964761bb83043f3a34924486
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340333"
---
# <a name="capabilities-in-technical-preview-1710-for-system-center-configuration-manager"></a>Fonctionnalités de Technical Preview 1710 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version 1710 de Technical Preview pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Problèmes connus dans cette version d’évaluation technique :**
-   **Prise en charge de Windows 10, version 1709 (également appelée Fall Creators Update)**.  À partir de cette version de Windows, Windows Media inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour utiliser un package de mise à niveau de système d’exploitation ou une image de système d’exploitation, veillez à sélectionner une [édition prise en charge par Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **La mise à jour vers une nouvelle préversion échoue s’il existe un serveur de site en mode passif**. Si vous exécutez une préversion qui a un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez désinstaller ce dernier pour pouvoir correctement mettre à jour votre site de préversion vers cette nouvelle préversion. Vous pouvez réinstaller le serveur de site en mode passif une fois votre site mis à jour.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Améliorations du déploiement de scripts PowerShell à partir de Configuration Manager
Avec cette version, les scripts PowerShell que vous déployez prennent désormais en charge les améliorations suivantes : 
- **Étendues de sécurité**.  Les scripts utilisent désormais des étendues de sécurité pour contrôler leur création et leur exécution. Leur utilisation passe par l’affectation d’étiquettes qui représentent des groupes d’utilisateurs. Pour plus d’informations sur l’utilisation des étendues de sécurité, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Surveillance en temps réel**. Lorsque vous surveillez l’exécution d’un script, vous le faites maintenant en temps réel pendant qu’il s’exécute.
- **Validation du paramètre**. Chaque paramètre inclus dans votre script a une boîte de dialogue **Propriétés du paramètre de script** qui vous permet d’ajouter la validation de ce paramètre. Après avoir ajouté la validation, vous devez obtenir des erreurs si vous entrez une valeur pour un paramètre qui ne satisfait pas à sa validation.

Le déploiement de scripts PowerShell a été introduit pour la première fois dans Technical Preview [Tech Preview 1706](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console). D’autres améliorations ont été apportées dans [Tech Preview 1707](/sccm/core/get-started/capabilities-in-technical-preview-1707#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager), puis [Tech Preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager).


### <a name="try-it-out"></a>Essayez !

Pour tester l’utilisation de la fonctionnalité Exécuter les scripts, consultez [Créer et exécuter des scripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-telemetry-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Limiter la télémétrie avancée dans Windows 10 pour envoyer uniquement les données pertinentes à Windows Analytics Device Health
<!-- 1356148 -->

Avec cette version, vous pouvez désormais définir la collecte de données de télémétrie dans Windows 10 sur le niveau **Avancé (limité)**. Ce paramètre vous permet d’obtenir un insight actionnable sur les périphériques de votre environnement sans que ces derniers aient à envoyer toutes les données au niveau de télémétrie **Avancé** avec Windows 10 version 1709 ou ultérieure.

Le niveau de télémétrie Avancé (limité) inclut les mesures du niveau de base, ainsi qu’un sous-ensemble de données collectées au niveau **Avancé** et pertinentes pour Windows Analytics. Pour plus d’informations sur les niveaux de télémétrie, consultez [Niveaux de télémétrie](https://docs.microsoft.com/windows/configuration/configure-windows-telemetry-in-your-organization#telemetry-levels).

### <a name="try-it-out"></a>Essayez !
Pour configurer la collecte de données de télémétrie dans Windows 10 sur les clients, consultez [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings). Ouvrez la fenêtre **Services cloud** et définissez le niveau de télémétrie dans Windows 10 sur **Avancé**.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Le Centre logiciel ne déforme plus les grandes icônes aux dimensions supérieures à 250 x 250  
<!-- 1356194 -->

Avec cette version, le Centre logiciel ne déforme plus les icônes aux dimensions supérieures à 250 x 250. Auparavant, il rendait ces icônes floues. Désormais, vous pouvez définir une icône avec des dimensions maximales de 512 x 512 pixels et l’afficher sans déformation.

### <a name="try-it-out"></a>Essayez !
Ajoutez une icône pour votre application dans le Centre logiciel. Pour ce faire, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Vérifier auprès du Centre logiciel la conformité des périphériques cogérés
<!-- 1356374 -->
Dans cette version, les utilisateurs peuvent utiliser le Centre logiciel pour vérifier la conformité de leurs appareils Windows 10 cogérés, même quand l’accès conditionnel est géré par Intune. Pour plus d’informations, consultez [Cogestion pour les appareils Windows 10](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Prise en charge d’Exploit Guard
Cette version inclut désormais la prise en charge de Windows Defender Exploit Guard. Vous pouvez configurer et déployer des stratégies pour gérer les quatre composants d’Exploit Guard. Ces composants sont les suivants :
-   Règles de réduction de la surface d’attaque
-   Accès contrôlé aux dossiers
-   Exploit Protection
-   Protection du réseau

Les données de conformité pour le déploiement de stratégie Exploit Guard sont disponibles dans la console Configuration Manager.

Pour plus d’informations sur Exploit Guard ainsi que sur ses règles et composants spécifiques, consultez [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard) dans la bibliothèque de documentation de Windows.

### <a name="prerequisites"></a>Prérequis
Les appareils gérés doivent exécuter Windows 10 Fall Creators Update version 1709 ou ultérieure et respecter les conditions suivantes, selon les composants et les règles configurés :

|Composant Exploit Guard |Configuration requise supplémentaire|
|------------------------|------------------------|
| Règles de réduction de la surface d’attaque  | La[protection en temps réel de Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) doit être activée sur les appareils.  |
| Accès contrôlé aux dossiers  | La[protection en temps réel de Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) doit être activée sur les appareils.   |
| Exploit Protection  | Aucun  |
| Protection du réseau  |  La[protection en temps réel de Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) doit être activée sur les appareils.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Créer une stratégie Exploit Guard  <!--1355468 -->
1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Endpoint Protection**, puis cliquez sur **Windows Defender Exploit Guard**.
2.  Dans l'onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Créer une stratégie Exploit**.
3.  Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.
4.  Sélectionnez ensuite les composants Exploit Guard que vous souhaitez gérer avec cette stratégie. Pour chaque composant que vous sélectionnez, vous pouvez ensuite configurer des détails supplémentaires.
  - **Règles de réduction de la surface d’attaque :** configurez la menace Office, les menaces liées aux scripts et les menaces de messagerie électronique que vous souhaitez bloquer ou auditer. Vous pouvez également exclure certains fichiers ou dossiers à partir de cette règle.
  - **Accès contrôlé aux dossiers :** configurez le blocage ou l’audit, puis ajoutez des applications qui peuvent contourner cette stratégie.  Vous pouvez également spécifier des dossiers supplémentaires qui ne sont pas protégés par défaut.
  - **Exploit Protection :** spécifiez un fichier XML contenant les paramètres pour atténuer les attaques de processus système et d’applications. Vous pouvez exporter ces paramètres à partir de l’application Centre de sécurité Windows Defender sur un appareil Windows 10.
  - **Protection du réseau :** définissez la protection du réseau pour bloquer ou auditer l’accès aux domaines suspects.
5.  Terminez l’Assistant pour créer la stratégie, que vous pouvez déployer ultérieurement sur des appareils.

### <a name="deploy-an-exploit-guard-policy"></a>Déployer une stratégie Exploit Guard     
Après avoir créé des stratégies Exploit Guard, utilisez l’assistant de déploiement de stratégies Exploit Guard pour les déployer. Pour ce faire, ouvrez la console Configuration Manager, accédez à **Ressources et Conformité** > **Endpoint Protection**, puis cliquez sur **Déployer la stratégie Exploit Guard**.

## <a name="limited-support-for-cng-certificates"></a>Prise en charge limitée des certificats CNG
<!-- 1356191 -->
À partir de cette version, vous pouvez désormais utiliser les modèles de certificat [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) pour les scénarios suivants :

- L’inscription du client et la communication avec un point de gestion HTTPS.   
- La distribution de logiciels et le déploiement d’applications avec un point de distribution HTTPS.   
- Le déploiement de système d'exploitation.  
- Le Kit SDK de messagerie du client (avec la dernière mise à jour) et proxy ISV.   
- La configuration de passerelle de gestion cloud.  

Pour utiliser des certificats CNG, votre autorité de certification (CA) doit fournir des modèles de certificat CNG pour les machines cibles.  Bien que les détails du modèle varient selon le scénario, les propriétés suivantes sont requises :

- Onglet **Compatibilité**

    - L’**autorité de certification** doit être Windows Server 2008 ou version ultérieure. (Windows Server 2012 recommandé)

    - Le **destinataire du certificat** doit être Windows Vista/Server 2008 ou version ultérieure. (Windows 8/Windows Server 2012 recommandé)

- Onglet **Chiffrement**

    - La **catégorie de fournisseur** doit être **Fournisseur de stockage de clés**.  (obligatoire)

Pour de meilleurs résultats, nous vous recommandons de créer le nom du sujet à partir des informations Active Directory.  Utilisez le nom DNS pour le **format du nom du sujet** et incluez le nom DNS dans le nom de substitution du sujet.  Dans le cas contraire, vous devez fournir ces informations au moment de l’inscription de l’appareil dans le profil de certificat.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Descriptions améliorées pour les redémarrages d’ordinateur en attente   <!--1356283 -->
Dans [Technical Preview 1708](/sccm/core/get-started/capabilities-in-technical-preview-1708#restart-computers-from-the-configuration-manager-console), il est désormais possible d’identifier les appareils en attente d’un redémarrage à partir de la console Configuration Manager.

À partir de cette version de Technical Preview, la console affiche des détails supplémentaires qui fournissent des informations sur le processus ou l’action qui demande le redémarrage.

## <a name="device-guard-policy-changes----1355092---"></a>Modifications des stratégies Device Guard <!-- 1355092 -->
Avec la version Technical Preview 1710, les trois modifications suivantes ont été apportées au niveau des stratégies Device Guard :

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Les stratégies Device Guard s’appellent désormais les stratégies Windows Defender Application Control
Les stratégies Device Guard s’appellent désormais les stratégies Windows Defender Application Control. Ainsi, par exemple, l’**Assistant Créer une stratégie Device Guard** s’appelle désormais l’**Assistant Créer une stratégie Windows Defender Application Control**.

### <a name="restart-is-not-required-to-apply-policies"></a>Le redémarrage n’est pas nécessaire pour appliquer des stratégies
À partir de Fall Creators Update pour Windows version 1709, les appareils utilisant la nouvelle version de Windows ne nécessitent pas de redémarrage pour appliquer les stratégies Windows Defender Application Control.

Le redémarrage est le paramètre par défaut.

#### <a name="try-it-out"></a>Essayez !  

Si vous souhaitez désactiver les redémarrages, procédez comme suit :

1.  Ouvrez l’Assistant **Créer une stratégie Windows Defender Application Control**.
2.  Sur la page**Général**, décochez la case **Forcer le redémarrage des appareils pour appliquer cette stratégie à tous les processus**.
3.  Cliquez sur **Suivant** jusqu'à ce que l'Assistant ait terminé.

Pour les versions antérieures de Windows, un redémarrage automatique est toujours appliqué.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Exécuter automatiquement les logiciels approuvés par Intelligent Security Graph

Les administrateurs peuvent désormais autoriser les appareils verrouillés à exécuter des logiciels approuvés jouissant d’une bonne réputation, tel que déterminé par Microsoft Intelligent Security Graph (ISG). ISG se compose de Windows Defender SmartScreen et d’autres services Microsoft.

Les appareils doivent exécuter Windows Defender SmartScreen pour que les logiciels soient approuvés.

#### <a name="try-it-out"></a>Essayez !  

Pour permettre à un appareil exécutant Windows Defender SmartScreen d’exécuter des logiciels approuvés, procédez comme suit :

1.  Ouvrez l’**Assistant Créer une stratégie Windows Defender Application Control**.
2.  Sur la page **Inclusions**, cochez la case **Autoriser les logiciels approuvés par Intelligent Security Graph**.
3.  Dans la zone **Fichiers ou dossiers approuvés**, ajoutez les fichiers et dossiers que vous souhaitez approuver.
4.  Cliquez sur **Suivant** jusqu'à ce que l'Assistant ait terminé.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Configurer et déployer des stratégies Windows Defender Application Guard <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) est une nouvelle fonctionnalité de Windows qui permet de protéger vos utilisateurs en ouvrant les sites web non approuvés dans un conteneur isolé et sécurisé qui n’est pas accessible par les autres parties du système d’exploitation. Dans cette version Technical Preview, nous avons ajouté la prise en charge pour configurer cette fonctionnalité à l’aide des paramètres de conformité de Configuration Manager que vous configurez, puis déployez sur une collection. Cette fonctionnalité sera disponible dans la version préliminaire de la version 64 bits de mise à jour de Windows 10 Creators Update (nom de code : RS2). Pour tester cette fonctionnalité maintenant, vous devez utiliser une version préliminaire de cette mise à jour.

### <a name="before-you-start"></a>Avant de commencer
Pour créer et déployer des stratégies Windows Defender Application Guard, les appareils Windows 10 sur lesquels vous déployez la stratégie doivent être configurés avec une stratégie d’isolation de réseau. Pour plus d’informations, consultez le billet de blog référencé plus loin. Cette fonctionnalité fonctionne uniquement avec les versions actuelles de Windows 10 Insider. Pour la tester, vos clients doivent exécuter une version récente de Windows 10 Insider.

### <a name="try-it-out"></a>Essayez !

Pour comprendre les principes de base de Windows Defender Application Guard, lisez le [billet de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

Pour créer une stratégie et pour parcourir les paramètres disponibles :
1. Dans la console **Configuration Manager**, choisissez **Ressources et Conformité**.
2. Dans l’espace de travail **Biens et conformité**, choisissez **Vue d’ensemble** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie Windows Defender Application Guard**.
4. À l’aide du billet de blog comme référence, vous pouvez parcourir et configurer les paramètres disponibles pour tester la fonctionnalité.
5. Dans cette version, nous avons ajouté la nouvelle page Définition du réseau à l’Assistant. Vous pouvez y spécifier l’identité d’entreprise et définir les limites du réseau de votre entreprise.

    > [!NOTE]
    > Les PC Windows 10 stockent une seule liste d’isolements réseau sur le client. Dans cette version, vous pouvez créer deux types de listes d’isolements réseau (une de la Protection des informations Windows et une de Windows Defender Application Guard) et les déployer sur le client. Si vous déployez les deux stratégies, les listes d’isolements réseau doivent correspondre. Si vous déployez des listes qui ne correspondent pas au même client, le déploiement échoue.

    Vous trouverez plus d’informations sur la façon de spécifier des définitions de réseau dans la [documentation sur la Protection des informations Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

6. Lorsque vous avez terminé, effectuez l’Assistant et déployez la stratégie sur un ou plusieurs appareils Windows 10.

### <a name="further-reading"></a>Articles complémentaires

Pour en savoir plus sur Windows Defender Application Guard, consultez [ce billet de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). En outre, pour en savoir plus sur le mode autonome de Windows Defender Application Guard, consultez [ce billet de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
