---
title: Gérer les images de système d’exploitation
titleSuffix: Configuration Manager
description: Découvrez les différentes méthodes disponibles dans Configuration Manager pour gérer les images de système d’exploitation stockées dans des fichiers WIM (Windows Imaging).
ms.date: 12/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fab13949-371c-4a4c-978e-471db1e54966
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 82909cced6783f73608f155e64b7dd30b4087b06
ms.sourcegitcommit: a52255da16c9f8b0b60a6c299a369347c7e01bef
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/24/2018
ms.locfileid: "49989159"
---
# <a name="manage-operating-system-images-with-system-center-configuration-manager"></a>Gérer les images de système d’exploitation avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les images de système d’exploitation dans Configuration Manager sont stockées au format de fichier WIM (Windows Imaging Format) et représentent un regroupement compressé de fichiers et de dossiers de référence nécessaires pour installer et configurer avec succès un système d’exploitation sur un ordinateur. Pour tous les scénarios de déploiement de système d’exploitation, vous devez sélectionner une image de système d’exploitation.   Vous pouvez utiliser l’image de système d’exploitation par défaut ou créer l’image de système d’exploitation à partir d’un ordinateur de référence que vous configurez. Quand vous créez l’ordinateur de référence, vous pouvez ajouter des fichiers de système d’exploitation, des pilotes, des fichiers de support, des mises à jour logicielles, des outils et d’autres applications logicielles au système d’exploitation avant de le capturer pour créer le fichier image. La section suivante fournit des informations sur chacune de ces méthodes.  

 **Image par défaut**  

 L’image de système d’exploitation par défaut (install.wim) est fournie avec les fichiers d’installation du système d’exploitation Windows. Cette image est une image de système d’exploitation de base qui contient un ensemble standard de pilotes. Quand vous utilisez l’image de système d’exploitation par défaut, vous pouvez installer des applications et effectuer d’autres configurations après l’installation du système d’exploitation à l’aide d’étapes de séquence de tâches.  L’image de système d’exploitation par défaut se trouve dans <*chemin_source_système_exploitation*>\Sources\install.wim.  

-   **Avantages**  

    -   La taille de l’image est inférieure à celle d’une image capturée.  

    -   L’installation d’applications et de configurations avec des étapes de séquence de tâches est plus dynamique. Par exemple, vous pouvez modifier les applications qui s’installeront et les configurations de la séquence de tâches sans avoir à recréer l’image du système d’exploitation.  

-   **Inconvénients**  

    -   L’installation du système d’exploitation peut prendre plus de temps, car l’installation des applications et d’autres configurations s’effectue une fois l’installation du système d’exploitation terminée.  

 **Image capturée**  

 Pour créer une image de système d’exploitation personnalisée, vous créez un ordinateur de référence avec le système d’exploitation souhaité, puis vous installez les applications, vous configurez les paramètres, etc. Vous capturez ensuite l’image du système d’exploitation à partir de l’ordinateur de référence pour créer le fichier WIM. Vous pouvez créer manuellement l'ordinateur de référence ou utiliser une séquence de tâches pour automatiser certaines ou toutes les étapes de construction.   
Pour en savoir plus sur les étapes de création d’une image de système d’exploitation personnalisée, consultez [Personnaliser les images de système d’exploitation](customize-operating-system-images.md).  

-   **Avantages**  

    -   L’installation peut être plus rapide que l’utilisation de l’image par défaut. Par exemple, les applications peuvent être préinstallées avec l’image de système d’exploitation capturée. Vous n’avez alors pas à installer les applications ultérieurement à l’aide d’étapes de séquence de tâches.  

-   **Inconvénients**  

    -   L’installation du système d’exploitation peut prendre plus de temps, car l’installation des applications et d’autres configurations s’effectue une fois l’installation du système d’exploitation terminée.  


##  <a name="BKMK_AddOSImages"></a> Ajouter des images de système d’exploitation à Configuration Manager  
 Avant d’utiliser une image de système d’exploitation, vous devez ajouter l’image à un site Configuration Manager. Utilisez la procédure suivante pour ajouter une image de système d’exploitation à un site.  

#### <a name="to-add-an-operating-system-image-to-a-site"></a>Pour ajouter une image de système d’exploitation à un site  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images du système d'exploitation**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter une image de système d'exploitation** pour démarrer l'Assistant Ajout d'une image de système d'exploitation.  

4.  Sur la page **Source de données** , indiquez le chemin réseau d'accès à l'image de système d'exploitation. Par exemple, spécifiez **\\\serveur\chemin\OS.WIM**.  

5.  Sur la page **Général** , spécifiez les informations suivantes, puis cliquez sur **Suivant**. Ces informations sont utiles à des fins d'identification lorsque vous ajoutez plusieurs images du système d'exploitation sur le même site.  

    -   **Nom** : spécifiez le nom de l'image. Par défaut, le nom de l'image est extrait du fichier WIM.  

    -   **Version** : spécifiez la version de l’image.  

    -   **Commentaire** : spécifiez une brève description de l’image.  

6.  Effectuez toutes les étapes de l'Assistant.  

 Vous pouvez maintenant distribuer l’image du système d’exploitation à des points de distribution.  

##  <a name="BKMK_DistributeBootImages"></a> Distribuer des images de système d’exploitation à des points de distribution  
 Les images de système d’exploitation sont distribuées aux points de distribution de la même façon que vous distribuez d’autre contenu. Dans la plupart des cas, vous devez distribuer l’image de système d’exploitation à au moins un point de distribution avant de déployer le système d’exploitation. Pour découvrir comment distribuer une image de système d’exploitation, consultez [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

##  <a name="BKMK_OSImagesApplyUpdates"></a> Appliquer des mises à jour logicielles à une image de système d’exploitation  
 De nouvelles mises à jour logicielles applicables au système d'exploitation figurant dans votre image de système d'exploitation sont régulièrement publiées. Avant de pouvoir appliquer des mises à jour logicielles à une image, votre infrastructure de mises à jour logicielles doit être en place, vous devez avoir synchronisé correctement les mises à jour logicielles et vous devez avoir téléchargé les mises à jour logicielles dans la bibliothèque de contenu sur le serveur de site. Pour plus d’informations, consultez [Déployer des mises à jour logicielles](../../sum/deploy-use/deploy-software-updates.md).  

 Vous pouvez appliquer ces mises à jour logicielles à une image selon un calendrier défini. Aux heures spécifiées dans ce calendrier, Configuration Manager applique les mises à jour logicielles sélectionnées à l’image de système d’exploitation et, si vous le souhaitez, distribue l’image mise à jour aux points de distribution. Les informations sur l'image de système d'exploitation sont stockées dans la base de données du site, y compris les mises à jour logicielles qui ont été appliquées au moment de l'importation. Les mises à jour logicielles appliquées à l'image depuis son ajout initial sont également stockées dans la base de données du site. Lorsque vous ouvrez l'Assistant pour appliquer des mises à jour logicielles à l'image de système d'exploitation, l'Assistant récupère une liste des mises à jour logicielles applicables qui n'ont pas encore été appliquées à l'image, pour vous permettre de les sélectionner. Configuration Manager copie les mises à jour logicielles de la bibliothèque de contenu sur le serveur de site, puis applique les mises à jour logicielles à l’image de système d’exploitation.  

 Pour appliquer des mises à jour logicielles à une image de système d'exploitation, suivez la procédure ci-dessous.  

#### <a name="to-apply-software-updates-to-an-operating-system-image"></a>Pour appliquer des mises à jour logicielles à une image de système d'exploitation  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images du système d'exploitation**.  

3.  Sélectionnez l'image de système d'exploitation à laquelle appliquer les mises à jour logicielles.  

4.  Sous l'onglet **Accueil** , dans le groupe **Image du système d'exploitation** , cliquez sur **Planifier les mises à jour** pour démarrer l'Assistant.  

5.  Sur la page **Choisir des mises à jour** , sélectionnez les mises à jour logicielles à appliquer à l'image du système d'exploitation, puis cliquez sur **Suivant**.  

6.  Sur la page **Définir le calendrier** , spécifiez les paramètres suivants, puis cliquez sur **Suivant**.  

    1.  **Calendrier**: définissez le calendrier d’application des mises à jour logicielles à l’image du système d’exploitation.  

    2.  **Continuer en cas d’erreur**: sélectionnez cette option pour continuer à appliquer les mises à jour logicielles à l’image même si une erreur survient.  

    3.  **Distribuer l’image aux points de distribution**: sélectionnez cette option pour mettre à jour l’image du système d’exploitation sur les points de distribution après l’application des mises à jour logicielles.  

7.  Vérifiez les informations figurant sur la page **Résumé** , puis cliquez sur **Suivant**.  

8.  Sur la page **Dernière étape** , vérifiez que les mises à jour logicielles ont été correctement appliquées à l'image de système d'exploitation.  

> [!NOTE]  
>  Pour réduire la taille de la charge utile, la maintenance des packages de mise à niveau du système d’exploitation et des images de système d’exploitation supprime l’ancienne version.  

##  <a name="BKMK_OSImageMulticast"></a> Préparer l’image de système d’exploitation pour les déploiements en multidiffusion  
 Utilisez des déploiements en multidiffusion pour permettre à plusieurs ordinateurs de télécharger simultanément une image de système d’exploitation. L’image est multidiffusée aux clients par le point de distribution, au lieu que le point de distribution envoie une copie de l’image à chaque client via une connexion distincte. Si vous choisissez la méthode de déploiement de système d’exploitation [Utiliser la multidiffusion pour déployer Windows sur le réseau](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md), vous devez configurer le package d’image de système d’exploitation pour prendre en charge la multidiffusion avant de distribuer l’image du système d’exploitation vers un point de distribution multidiffusion. Pour définir les options de multidiffusion pour un package d'images du système d'exploitation existant, procédez comme suit.  

#### <a name="to-modify-an-operating-system-image-package-to-use-multicast"></a>Pour modifier un package d'images du système d'exploitation afin d'utiliser la multidiffusion  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images du système d'exploitation**.  

3.  Sélectionnez l'image du système d'exploitation que vous souhaitez distribuer au point de distribution multidiffusion.  

4.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

5.  Sélectionnez l'onglet **Paramètres de distribution** et configurez les options suivantes :  

    -   **Autoriser ce package à être transféré par multidiffusion (WinPE uniquement)**  : sélectionnez cette option pour permettre à Configuration Manager de déployer simultanément plusieurs images de système d’exploitation.  

    -   **Chiffrer les packages de multidiffusion** : spécifiez si l’image est chiffrée avant d'être envoyée au point de distribution. Utiliser cette option si le package contient des informations sensibles. Si l'image n'est pas chiffrée, le contenu du package sera visible en texte clair sur le réseau et pourra être lu par un utilisateur non autorisé.  

    -   **Transférer ce package uniquement par multidiffusion** : spécifiez si vous souhaitez que le point de distribution déploie l’image uniquement pendant une session de multidiffusion.  

         Si vous sélectionnez **Transférer ce package uniquement par multidiffusion**, vous devez également spécifier **Télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches** comme option de déploiement pour l'image du système d'exploitation. Vous pouvez spécifier les options de déploiement pour l'image lorsque vous déployez l'image du système d'exploitation, ou vous pouvez les spécifier ultérieurement en modifiant les propriétés du déploiement. Les options de déploiement se trouvent sur l'onglet **Points de distribution** de la page **Propriétés** de l'objet de déploiement.  

6.  Cliquez sur **OK**.  
