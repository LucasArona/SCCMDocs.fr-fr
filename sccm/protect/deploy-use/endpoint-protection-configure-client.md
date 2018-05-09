---
title: Configurer le client Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment configurer des paramètres client personnalisés pour Endpoint Protection, dans le but de les déployer ensuite dans certains regroupements d’ordinateurs de votre hiérarchie.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 10572c367dcdc70bf9c708d3a6bb514c0afa2b24
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurer des paramètres client personnalisés pour Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette procédure permet de configurer des paramètres clients personnalisés pour Endpoint Protection, dans le but de les déployer ensuite dans certains regroupements d’ordinateurs de votre hiérarchie.

> [!IMPORTANT]
>  Configurez les paramètres clients par défaut pour Endpoint Protection uniquement si vous voulez les appliquer à l’ensemble des ordinateurs de la hiérarchie. 

## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>Pour activer Endpoint Protection et configurer des paramètres client personnalisés

1.  Dans la console Configuration Manager, cliquez sur **Administration**.

2.  Dans l'espace de travail **Administration** , cliquez sur **Paramètres client**.

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer des paramètres de périphérique client personnalisés**.

4.  Dans la boîte de dialogue **Créer des paramètres de périphérique client personnalisés** , indiquez un nom et une description pour le groupe de paramètres, puis sélectionnez **Endpoint Protection**.

5.  Configurez les paramètres client nécessaires pour Endpoint Protection. Pour obtenir une liste complète des paramètres client disponibles pour Endpoint Protection, consultez la section Endpoint Protection dans la rubrique [À propos des paramètres client dans System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

   > [!IMPORTANT]
   >  Vous devez avoir installé le rôle de système de site Endpoint Protection pour pouvoir configurer les paramètres client pour Endpoint Protection.

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Créer des paramètres de périphérique client personnalisés** . Les nouveaux paramètres client figurent dans le nœud **Paramètres client** de l'espace de travail **Administration** .

7.  Pour pouvoir utiliser les paramètres client personnalisés, vous devez les déployer dans un regroupement. Sélectionnez les paramètres client personnalisés à déployer, puis, dans l'onglet **Accueil** , dans le groupe **Paramètres client** , cliquez sur **Déployer**.

8.  Dans la boîte de dialogue **Sélectionner des regroupements** , choisissez le regroupement dans lequel vous voulez déployer les paramètres client, puis cliquez sur **OK**. Le nouveau déploiement figure dans l'onglet **Déploiements** du panneau des détails.

Les ordinateurs clients sont configurés avec ces paramètres lorsqu'ils téléchargent la stratégie client. Pour savoir comment lancer une récupération de stratégie pour un seul client, consultez la section « Lancer une récupération de stratégie pour un client Configuration Manager » dans [Guide pratique pour gérer les clients dans System Center Configuration Manager](../../core/clients/manage/manage-clients.md).

## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image-in-configuration-manager"></a>Guide pratique pour configurer le client Endpoint Protection dans une image disque dans Configuration Manager
Vous pouvez installer le client Endpoint Protection sur un ordinateur que vous prévoyez d’utiliser comme source de l’image disque pour le déploiement du système d’exploitation dans Configuration Manager. En général, on appelle cet ordinateur l'ordinateur de référence. Après avoir créé l’image du système d’exploitation, vous pouvez utiliser le déploiement du système d’exploitation dans Configuration Manager pour déployer l’image pouvant contenir des packages logiciels, y compris Endpoint Protection, sur vos ordinateurs clients.

Suivez les procédures de cet article pour vous aider à installer et configurer le client Endpoint Protection sur un ordinateur de référence

### <a name="prerequisites-for-installing-the-endpoint-protection-client-on-the-reference-computer"></a>Conditions requises pour installer le client Endpoint Protection sur l'ordinateur de référence
La liste suivante répertorie les conditions préalables requises pour installer le logiciel client Endpoint Protection sur un ordinateur de référence.

-   Vous devez avoir accès au package d’installation du client Endpoint Protection, **scepinstall.exe**. Ce package est disponible dans le dossier **Client** du dossier d’installation de Microsoft System Center Configuration Manager sur le serveur de site. Windows 10 et Windows Server 2016 ont Windows Defender installé. 

-   Pour vous assurer que le client Endpoint Protection est déployé avec la configuration requise dans votre organisation, créez une stratégie de logiciel anti-programme malveillant et exportez-la. Vous pouvez ensuite spécifier la stratégie de logiciel anti-programme malveillant à utiliser quand vous installez manuellement le client Endpoint Protection. Pour plus d’informations, consultez [Comment créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md).

   > [!NOTE]
   >  La **Stratégie par défaut des logiciels anti-programmes malveillants du client** ne peut pas être exportée.

-   Si vous voulez installer le client Endpoint Protection avec les dernières définitions, téléchargez ces définitions depuis le [Centre de protection Microsoft contre les programmes malveillants](http://go.microsoft.com/fwlink/?LinkID=200965).

>[!NOTE]
> À compter de Configuration Manager 1802, l’agent Endpoint Protection (SCEPInstall) n’a pas besoin d’être installé sur les appareils Windows 10. S’il est déjà installé sur les appareils Windows 10, Configuration Manager ne le supprime pas. Les administrateurs peuvent supprimer l’agent Endpoint Protection sur les appareils Windows 10 qui exécutent au moins la version client 1802. Il est possible que SCEPInstall.exe soit toujours dans C:\Windows\ccmsetup sur certaines machines, mais il ne doit pas être téléchargé sur de nouvelles installations de client. <!--503654-->
### <a name="how-to-install-the-endpoint-protection-client-software-on-the-reference-computer"></a>Comment installer le logiciel du client Endpoint Protection sur l'ordinateur de référence
Vous pouvez installer le client Endpoint Protection localement sur l’ordinateur de référence à partir d’une invite de commande. Pour cela, vous devez d'abord obtenir le fichier d'installation **scepinstall.exe**. Vous pouvez également installer le client avec une stratégie de logiciel anti-programme malveillant préconfigurée ou avec une que vous avez précédemment exportée.

## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a>Pour installer le client Endpoint Protection à partir d'une invite de commande

1.  Copiez **scepinstall.exe** dans le dossier **Client** du média d’installation System Center Configuration Manager sur l’ordinateur où vous voulez installer le logiciel client Endpoint Protection.

2.  Ouvrez une invite de commande avec des privilèges d’administrateur, accédez au dossier qui contient **scepinstall.exe** et exécutez la commande suivante, en ajoutant les propriétés de ligne de commande supplémentaires dont vous avez besoin :

   ```
   scepinstall.exe
   ```

    Vous pouvez spécifier l'une des propriétés de ligne de commande suivantes :

   |Propriété|Description|
   |--------------|-----------------|
   |/s|Indique qu'une installation silencieuse va être effectuée.|
   |/q|Indique qu'une extraction silencieuse des fichiers d'installation va être effectuée.|
   |/i|Indique qu'une installation normale doit être effectuée.|
   |/noreplace|Indique qu'un logiciel anti-programme malveillant tiers n'est pas désinstallé lors de l'installation.|
   |/policy|Indique un fichier de stratégie de logiciel anti-programme malveillant à utiliser pour configurer le client lors de l'installation.|
   |/sqmoptin|Indique que cette installation du logiciel client adhère au programme d'amélioration du produit Microsoft.|

3.  Suivez les instructions à l'écran pour terminer l'installation du client.

4.  Si vous avez téléchargé le dernier package de définition de mise à jour, copiez-le sur l'ordinateur client et double-cliquez dessus pour l'installer.

   > [!NOTE]
   >  Une fois l’installation du client Endpoint Protection terminée, le client effectue automatiquement une vérification des mises à jour des définitions. Si cette vérification des mises à jour réussit, vous n'avez pas à installer manuellement le dernier package de mises à jour des définitions.

## <a name="to-install-the-client-software-with-an-antimalware-policy-from-the-command-prompt"></a>Pour installer le logiciel client avec une stratégie de logiciel anti-programme malveillant à partir de l'invite de commande

1.  Copiez **scepinstall.exe** et la stratégie de logiciel anti-programme malveillant exportée ou préconfigurée sur l’ordinateur sur lequel vous voulez installer le logiciel client Endpoint Protection.

2.  Ouvrez une invite de commande avec des privilèges d'administrateur, accédez au dossier qui contient **scepinstall.exe** et la stratégie de logiciel anti-programme malveillant, puis exécutez la commande suivante :

   ```
   scepinstall.exe /policy <full path>\<policy file>
   ```

3.  Suivez les instructions à l'écran pour terminer l'installation du client.

4.  Si vous avez téléchargé le dernier package de définition, copiez-le sur l'ordinateur client et double-cliquez dessus pour l'installer.

   > [!NOTE]
   >  Une fois l’installation du client Endpoint Protection terminée, le client effectue automatiquement une vérification des mises à jour des définitions. Si cette vérification des mises à jour réussit, vous n'avez pas à installer manuellement le dernier package de mises à jour des définitions.

## <a name="verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Vérifier que le client Endpoint Protection est installé correctement
Une fois le client Endpoint Protection installé sur votre ordinateur de référence, vérifiez qu’il fonctionne correctement.

### <a name="to-verify-that-the-endpoint-protection-client-is-installed-correctly"></a>Pour vérifier que le client Endpoint Protection est installé correctement

1.  Sur l’ordinateur de référence, ouvrez **System Center Endpoint Protection** dans la zone de notification Windows.

2.  Dans l’onglet **Accueil** de la boîte de dialogue **System Center Endpoint Protection**, vérifiez que **Protection en temps réel** est réglé sur **Activé**.

3.  Vérifiez que **À jour** s’affiche pour **Définitions de virus et de logiciels espions**.

4.  Pour vous assurer que votre ordinateur de référence est prêt pour l'acquisition d’images, sous **Options d'analyse**, sélectionnez **Complète**et cliquez sur **Analyser maintenant**.

### <a name="how-to-prepare-the-endpoint-protection-client-for-imaging"></a>Comment préparer le client Endpoint Protection à l'acquisition d'images
Après avoir vérifié que le client Endpoint Protection est installé correctement sur l’ordinateur de référence, vous pouvez préparer l’ordinateur pour l’acquisition d’images. Effectuez les opérations suivantes pour préparer le client Endpoint Protection pour l’acquisition d’images.


Pour plus d’informations sur le déploiement de système d’exploitation dans Configuration Manager, consultez [Gérer les images de système d’exploitation avec System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

### <a name="to-prepare-the-endpoint-protection-client-for-imaging"></a>Pour préparer le client Endpoint Protection pour l'acquisition d'images

1.  Sur l'ordinateur de référence, ouvrez une session en tant qu'utilisateur disposant de privilèges d'administration.

2.  Téléchargez et installez **PsTools** à partir du [site Windows SysInternals](http://go.microsoft.com/fwlink/?LinkId=215263) sur TechNet.

3.  Ouvrez une invite de commande avec élévation de privilèges, accédez au dossier dans lequel vous avez installé PsTools et tapez la commande suivante :

   ```
   Psexec.exe -s -i regedit.exe
   ```

   > [!IMPORTANT]
   >  Soyez prudent quand vous exécutez l’Éditeur du Registre de cette manière, car l’option -s dans PsExec.exe exécute l’Éditeur du Registre avec des privilèges LocalSystem.

4.  Dans l'Éditeur du Registre, accédez à chacune des clés de Registre suivantes et supprimez-les.

   > [!IMPORTANT]
   >  Vous devez supprimer les clés de Registre pour pouvoir effectuer l'acquisition d'images de l'ordinateur de référence. Les clés de Registre sont recréées au démarrage du client Endpoint Protection. Si vous redémarrez l'ordinateur de référence, vous devez supprimer les clés de Registre à nouveau.

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID**

   -   **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID**

Après avoir terminé les étapes ci-dessus, vous pouvez préparer l'ordinateur de référence pour l'acquisition d'images. Pour plus d’informations sur le déploiement de système d’exploitation dans Configuration Manager, consultez [Gérer les images de système d’exploitation avec System Center Configuration Manager](/sccm/osd/get-started/manage-operating-system-images).

Quand une image contenant le logiciel client Endpoint Protection est déployée, le client Endpoint Protection envoie automatiquement les informations au site Configuration Manager dont dépend l’ordinateur, et la stratégie applicable à l’ordinateur client est téléchargée et appliquée.
