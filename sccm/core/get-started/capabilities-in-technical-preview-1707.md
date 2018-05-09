---
title: Version Technical Preview 1707
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1707 de System Center Configuration Manager.
ms.date: 08/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 375c743e1094f3b3f52090ae520ee9d8e86acbe0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="capabilities-in-technical-preview-1707-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1707 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version Technical Preview 1707 de System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Problèmes connus dans cette version d’évaluation technique :**
-   **La mise à jour vers la préversion 1707 échoue s’il existe un serveur de site en mode passif**. Si vous exécutez la préversion 1706 et que vous avez un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez le désinstaller pour pouvoir mettre à jour votre site de la préversion vers la version 1707. Vous pourrez réinstaller le serveur de site en mode passif lorsque votre site sera passé à la version 1707.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.



**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="client-peer-cache-support-for-express-installation-files-for-windows-10-and-office-365"></a>Prise en charge du cache d’homologue client pour les fichiers d’installation rapide de Windows 10 et Office 365
<!-- 1352486 -->
À partir de cette version, le cache d’homologue prend en charge la distribution des fichiers d’installation rapide de Windows 10 et des fichiers de mise à jour d’Office 365. Aucune configuration supplémentaire n'est requise.

## <a name="surface-device-dashboard"></a>Tableau de bord Surface
<!--1355788-->
Le tableau de bord de la Surface fournit des informations sur les appareils Surface trouvés dans votre environnement. Dans la console, accédez à **Surveillance** > **Appareils Surface**. Vous pouvez voir les informations suivantes :
- Le pourcentage de Surface
- Le pourcentage de modèles de Surface
- Les cinq principales versions de système d’exploitation

Cliquez sur une section du graphique **Modèles de Surface** pour obtenir la liste complète des appareils.  

## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurer et déployer des stratégies Windows Defender Application Guard
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) est une nouvelle fonctionnalité de Windows qui permet de protéger vos utilisateurs en ouvrant les sites web non approuvés dans un conteneur isolé et sécurisé qui n’est pas accessible par les autres parties du système d’exploitation. Dans cette version Technical Preview, nous avons ajouté la prise en charge pour configurer cette fonctionnalité à l’aide des paramètres de conformité de Configuration Manager que vous configurez, puis déployez sur une collection. Cette fonctionnalité sera disponible dans la préversion de la version 64 bits de mise à jour de Windows 10 Fall Creators Update (nom de code : RS3). Pour tester cette fonctionnalité maintenant, vous devez utiliser une version préliminaire de cette mise à jour.

### <a name="before-you-start"></a>Avant de commencer

Pour créer et déployer des stratégies Windows Defender Application Guard, les appareils Windows 10 sur lesquels vous déployez la stratégie doivent être configurés avec une stratégie d’isolation de réseau. Pour plus d’informations, consultez [ce billet de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Cette fonctionnalité fonctionne uniquement avec les versions actuelles de Windows 10 Insider. Pour la tester, vos clients doivent exécuter une version récente de Windows 10 Insider.

### <a name="try-it-out"></a>Essayez !

#### <a name="to-create-a-policy-and-to-browse-the-available-settings"></a>Pour créer une stratégie et pour parcourir les paramètres disponibles :

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité**.
2. Dans l’espace de travail **Biens et conformité**, choisissez **Vue d’ensemble** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie Windows Defender Application Guard**.
4. À l’aide du billet de blog comme référence, vous pouvez parcourir et configurer les paramètres disponibles pour tester la fonctionnalité.
5. Dans cette version, nous avons ajouté la nouvelle page **Définition du réseau** de l’Assistant. Dans cette page, spécifiez l’identité d’entreprise et définissez les limites du réseau de votre entreprise.<br>Les PC Windows 10 stockent une seule liste d’isolements réseau sur le client. Dans cette version, vous pouvez créer deux types de listes d’isolements réseau (une de la Protection des informations Windows et une de Windows Defender Application Guard) et les déployer sur le client. Si vous déployez les deux stratégies, les listes d’isolements réseau doivent correspondre. Si vous déployez des listes qui ne correspondent pas au même client, le déploiement échoue.
Vous trouverez plus d’informations sur la façon de spécifier des définitions de réseau dans la [documentation sur la Protection des informations Windows](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
6. Lorsque vous avez terminé, effectuez l’Assistant et déployez la stratégie sur un ou plusieurs appareils Windows 10.

### <a name="further-reading"></a>Articles complémentaires
Pour en savoir plus sur Windows Defender Application Guard, consultez [ce billet de blog](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). En outre, pour en savoir plus sur le mode autonome de Windows Defender Application Guard, consultez [ce billet de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).

## <a name="add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager"></a>Ajouter des paramètres lorsque vous déployez des scripts PowerShell à partir de Configuration Manager

<!-- 1236459 --->

Dans la dernière version Technical Preview, nous avons introduit une nouvelle fonctionnalité qui vous permet de [créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
Dans cette version, nous avons étendu cette fonctionnalité. Maintenant, Configuration Manager lit le script PowerShell et affiche tous les paramètres dans l’Assistant Création d’un script. Vous pouvez fournir une valeur pour le paramètre de l’Assistant qui sera utilisée lors de l’exécution du script. Vous pouvez également laisser le paramètre vide. Dans ce cas, vous devrez fournir une valeur pour le paramètre lorsque vous exécuterez le script.
Dans cette préversion technique, vous devez fournir tous les paramètres requis par le script. Nous prévoyons de rendre les paramètres de script facultatifs dans une version ultérieure.

### <a name="try-it-out"></a>Essayez !

1. Suivez les instructions dans [Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1706#create-and-run-powershell-scripts-from-the-configuration-manager-console).
2. Sur la nouvelle page **Paramètres du script** de l’**Assistant Création d’un script**, choisissez un paramètre et cliquez sur **Modifier**.
3. Fournissez une valeur de paramètre pour le paramètre sélectionné, puis cliquez sur **OK**.
4. Effectuez toutes les étapes de l'Assistant.

Lorsque le script s’exécute, il utilise les valeurs de paramètre que vous avez définies.
