---
title: Configurer Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment configurer des paramètres client personnalisés pour Endpoint Protection.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e909f6d291816125415ef712bb00822f23951099
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384346"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurer les paramètres client personnalisés pour Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette procédure permet de configurer des paramètres clients personnalisés pour Endpoint Protection, dans le but de les déployer ensuite dans des regroupements d’appareils de votre hiérarchie.

> [!IMPORTANT]  
>  Configurez les paramètres clients par défaut pour Endpoint Protection uniquement si vous voulez les appliquer à l’ensemble des ordinateurs de la hiérarchie. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Pour activer Endpoint Protection et configurer des paramètres client personnalisés

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer des paramètres de périphérique client personnalisés**.  

4.  Dans la boîte de dialogue **Créer des paramètres de périphérique client personnalisés** , indiquez un nom et une description pour le groupe de paramètres, puis sélectionnez **Endpoint Protection**.  

5.  Configurez les paramètres client nécessaires pour Endpoint Protection. Pour obtenir la liste complète des paramètres client Endpoint Protection que vous pouvez configurer, consultez la section Endpoint Protection dans [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#endpoint-protection).  

   > [!IMPORTANT]  
   >  Installez le rôle de système de site Endpoint Protection afin de configurer les paramètres client pour Endpoint Protection.  

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Créer des paramètres de périphérique client personnalisés** . Les nouveaux paramètres client figurent dans le nœud **Paramètres client** de l'espace de travail **Administration** .  

7.  Ensuite, déployez les paramètres client personnalisés sur un regroupement. Sélectionnez les paramètres client personnalisés à déployer. Sous l’onglet **Accueil**, dans le groupe **Paramètres client**, cliquez sur **Déployer**.  

8.  Dans la boîte de dialogue **Sélectionner des regroupements** , choisissez le regroupement dans lequel vous voulez déployer les paramètres client, puis cliquez sur **OK**. Le nouveau déploiement figure dans l'onglet **Déploiements** du panneau des détails.  

Les clients sont configurés avec ces paramètres lorsqu’ils téléchargent la stratégie client. Pour plus d’informations, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Comment provisionner le client Endpoint Protection dans une image disque

Installez le client Endpoint Protection sur un ordinateur que vous prévoyez d’utiliser comme source de l’image disque pour le déploiement du système d’exploitation dans Configuration Manager. En général, on appelle cet ordinateur l'ordinateur de référence. Après avoir créé l’image du système d’exploitation, utilisez le déploiement de système d’exploitation dans Configuration Manager pour déployer l’image.

> [!Important]  
> Windows 10 et Windows Server 2016 ont Windows Defender installé par défaut. Vous n’avez donc pas besoin d’effectuer cette procédure sur ces versions de Windows.  

Effectuez les procédures suivantes pour vous aider à installer et configurer le client Endpoint Protection sur un ordinateur de référence.


### <a name="prerequisites"></a>Prérequis

La liste suivante répertorie les conditions préalables requises pour installer le logiciel client Endpoint Protection sur un ordinateur de référence.

-   Vous devez avoir accès au package d’installation du client Endpoint Protection, **scepinstall.exe**. Recherchez ce package dans le dossier **Client** du dossier d’installation de Configuration Manager sur le serveur de site.  

-   Pour déployer le client Endpoint Protection avec la configuration requise dans votre organisation, créez et exportez une stratégie de logiciel anti-programme malveillant. Spécifiez ensuite cette stratégie quand vous installez manuellement le client Endpoint Protection. Pour plus d’informations, consultez [Guide pratique pour créer et déployer des stratégies de logiciel anti-programme malveillant](/sccm/protect/deploy-use/endpoint-antimalware-policies).  

   > [!NOTE]  
   >  Vous ne pouvez pas exporter la **stratégie de logiciel anti-programme malveillant par défaut**.  

-   Si vous souhaitez installer le client Endpoint Protection avec les définitions les plus récentes, téléchargez-les à partir de [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi).  

> [!NOTE]  
> À compter de la version 1802 de Configuration Manager, vous n’avez pas besoin d’installer l’agent Endpoint Protection (SCEPInstall) sur les appareils Windows 10. Si cet agent est déjà installé sur les appareils Windows 10, Configuration Manager ne le supprime pas. Les administrateurs peuvent supprimer l’agent Endpoint Protection sur les appareils Windows 10 qui exécutent au moins la version client 1802. Il est possible que SCEPInstall.exe soit encore présent dans C:\Windows\ccmsetup sur certaines machines, mais les nouvelles installations de client ne le téléchargent pas normalement. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Comment installer le client Endpoint Protection sur l’ordinateur de référence

Installez le client Endpoint Protection localement sur l’ordinateur de référence à partir d’une invite de commandes. Obtenez tout d’abord le fichier d’installation **scepinstall.exe**. Pour plus d’informations, consultez [Installer le client Endpoint Protection à partir d’une invite de commandes](#bkmk_manual-install).

Si nécessaire, incluez également une stratégie de logiciel anti-programme malveillant préconfigurée ou une stratégie de logiciel anti-programme malveillant que vous avez précédemment exportée. 



## <a name="bkmk_manual-install"></a> Pour installer le client Endpoint Protection à partir d’une invite de commandes

1.  Copiez le fichier **scepinstall.exe** du dossier **Client**, situé dans le dossier d’installation de Configuration Manager, sur l’ordinateur où vous voulez installer le logiciel client Endpoint Protection.  

2.  Ouvrez une invite de commandes en tant qu’administrateur. Changez le répertoire en indiquant le dossier du programme d’installation. Ensuite, exécutez `scepinstall.exe`, après avoir ajouté les propriétés de ligne de commande supplémentaires nécessaires :

   |Propriété|Description|
   |--------------|-----------------|
   |`/s`|Exécuter le programme d’installation sans assistance|
   |`/q`|Extraire les fichiers d’installation sans assistance|
   |`/i`|Exécuter le programme d’installation normalement|
   |`/policy`|Indiquer un fichier de stratégie de logiciel anti-programme malveillant pour configurer le client lors de l’installation|
   |`/sqmoptin`|Participer au Programme d’amélioration du produit (CEIP) Microsoft|

3.  Suivez les instructions affichées pour continuer l’installation du client.  

4.  Si vous avez téléchargé le dernier package de définition de mise à jour, copiez-le sur l'ordinateur client et double-cliquez dessus pour l'installer.  

   > [!NOTE]  
   >  Une fois l’installation du client Endpoint Protection terminée, le client effectue automatiquement une vérification des mises à jour des définitions. Si cette vérification des mises à jour réussit, vous n'avez pas à installer manuellement le dernier package de mises à jour des définitions.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Exemple d’installation du client avec une stratégie de logiciel anti-programme malveillant

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Vérifier l’installation du client Endpoint Protection

Une fois le client Endpoint Protection installé sur votre ordinateur de référence, vérifiez qu’il fonctionne correctement.

1.  Sur l’ordinateur de référence, ouvrez **System Center Endpoint Protection** dans la zone de notification Windows.  

2.  Dans l’onglet **Accueil** de la boîte de dialogue **System Center Endpoint Protection**, vérifiez que **Protection en temps réel** est réglé sur **Activé**.  

3.  Vérifiez que **À jour** s’affiche pour **Définitions de virus et de logiciels espions**.  

4.  Pour vous assurer que votre ordinateur de référence est prêt pour l’acquisition d’images, sous **Options d’analyse**, sélectionnez **Complète**et cliquez sur **Analyser maintenant**.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Préparer le client Endpoint Protection pour l’acquisition d’images

Effectuez les opérations suivantes afin de préparer le client Endpoint Protection pour l’acquisition d’images :

1.  Sur l’ordinateur de référence, connectez-vous en tant qu’administrateur.  

2.  Téléchargez et installez **PsExec** à partir de [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec).  

3.  Exécutez une invite de commandes en tant qu’administrateur, changez le répertoire en indiquant le dossier d’installation de PsTools et tapez la commande suivante :  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Soyez prudent lorsque vous exécutez l’Éditeur du Registre de cette manière. PsExec.exe l’exécute dans le contexte du compte LocalSystem.  

4.  Dans l’Éditeur du Registre, supprimez les clés de Registre suivantes :  

   > [!IMPORTANT]  
   >  Supprimez ces clés de Registre juste avant d’effectuer l’acquisition d’images de l’ordinateur de référence. Le client Endpoint Protection recrée ces clés à son démarrage. Si vous redémarrez l’ordinateur de référence, supprimez à nouveau les clés de Registre.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Vous êtes maintenant prêt à préparer l’ordinateur de référence pour l’acquisition d’images.

Lors du déploiement d’une image de système d’exploitation contenant le client Endpoint Protection, le processus envoie automatiquement les informations au site Configuration Manager attribué à l’appareil. Le client télécharge et applique la stratégie de logiciel anti-programme malveillant ciblée, le cas échéant.  



## <a name="see-also"></a>Voir aussi

Pour plus d’informations sur le déploiement de système d’exploitation dans Configuration Manager, consultez [Gérer les images de système d’exploitation](/sccm/osd/get-started/manage-operating-system-images).

