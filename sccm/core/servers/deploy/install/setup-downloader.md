---
title: Téléchargeur d’installation
titleSuffix: Configuration Manager
description: Découvrez les fonctions de cette application autonome, qui a été conçue pour vérifier que votre installation de site utilise les dernières actuelles des fichiers d’installation clés.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bda87fc5-2e4c-4992-98a4-01770365038c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f8948556ebee069e4ea1c8bf16302ef92fe7b3c1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32344059"
---
# <a name="setup-downloader-for-system-center-configuration-manager"></a>Téléchargeur d’installation pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’exécuter le programme d’installation pour installer ou mettre à niveau un site System Center Configuration Manager, vous pouvez utiliser l’application autonome Téléchargeur d’installation correspondant à la version de Configuration Manager que vous souhaitez installer pour télécharger les fichiers d’installation mis à jour.  

L’utilisation des fichiers d’installation mis à jour garantit que votre installation de site utilise les dernières versions des fichiers d’installation clés. En résumé :   
-   Quand vous utilisez le téléchargeur d’installation pour télécharger des fichiers avant de démarrer le programme d’installation, vous devez spécifier le dossier qui contiendra les fichiers.  
-   Le compte que vous utilisez pour exécuter le téléchargeur d’installation doit avoir des autorisations **Contrôle intégral** sur le dossier de téléchargement.  
-   Quand vous exécutez le programme d’installation pour installer ou mettre à niveau un site, vous pouvez lui demander d’utiliser cette copie locale des fichiers téléchargés précédemment. Cela évite au programme d’installation de devoir se connecter à Microsoft au démarrage de l’installation ou de la mise à niveau du site.  
-   Vous pouvez utiliser la même copie locale des fichiers d’installation pour des installations ou mises à niveau de sites ultérieures.  

Le téléchargeur d’installation télécharge les types de fichiers suivants :  
-   Fichiers redistribuables requis  
-   Modules linguistiques  
-   Dernières mises à jour de produit pour le programme d’installation  

Vous avez deux options pour exécuter le téléchargeur d’installation :
- Exécuter l’application avec l’interface utilisateur
- Pour les options de ligne de commande, exécuter l’application à l’invite de commandes


## <a name="run-setup-downloader-with-the-user-interface"></a>Exécuter le téléchargeur d’installation avec l’interface utilisateur  

1.  Sur un ordinateur disposant d’un accès Internet, ouvrez l’Explorateur Windows et accédez à **&lt;support_installation_Configuration_Manager\>\SMSSETUP\BIN\X64**.  

2.  Double cliquez sur **Setupdl.exe** pour ouvrir le téléchargeur d’installation.   

3. Spécifiez le chemin du dossier où seront hébergés les fichiers d’installation mis à jour, puis cliquez sur **Télécharger**. Le téléchargeur d’installation vérifie les fichiers qui figurent dans le dossier de téléchargement. Il télécharge uniquement les fichiers manquants ou plus récents que les fichiers existants. Le téléchargeur d’installation crée des sous-dossiers pour les langues téléchargées et d’autres sous-dossiers requis.  

4.  Pour passer en revue les résultats du téléchargement, ouvrez le fichier **ConfigMgrSetup.log** situé dans le répertoire racine du lecteur C.  

## <a name="run-setup-downloader-from-a-command-prompt"></a>Exécuter le téléchargeur d’installation à partir d’une invite de commandes  

1.  Dans une fenêtre d’invite de commandes, accédez à **&lt;*Support d’installation de Configuration Manager*\>\SMSSETUP\BIN\X64**.   

2.  Exécutez **Setupdl.exe** pour ouvrir le téléchargeur d’installation.

    Vous pouvez utiliser les options de ligne de commande suivantes avec **Setupdl.exe** :   

    -   **/VERIFY**: utilisez cette option pour vérifier les fichiers dans le dossier de téléchargement, notamment les fichiers de langues. Examinez la liste des fichiers obsolètes dans le fichier ConfigMgrSetup.log situé dans le répertoire racine du lecteur C. Aucun fichier n'est téléchargé lorsque vous utilisez cette option.  

    -   **/VERIFYLANG**: utilisez cette option pour vérifier les fichiers de langues dans le dossier de téléchargement. Examinez la liste des fichiers de langue obsolètes dans le fichier ConfigMgrSetup.log situé dans le répertoire racine du lecteur C.

    -   **/LANG**: utilisez cette option pour télécharger uniquement les fichiers de langues dans le dossier de téléchargement.  

    -   **/NOUI**: utilisez cette option pour démarrer le téléchargeur d’installation sans afficher l’interface utilisateur. Quand vous utilisez cette option, vous devez spécifier le **chemin de téléchargement** dans le cadre de la commande, à l’invite de commandes.  

    -   **&lt;chemin_téléchargement\>**: vous pouvez spécifier le chemin du dossier de téléchargement pour démarrer automatiquement la vérification ou le processus de téléchargement. Vous devez spécifier le chemin de téléchargement quand vous utilisez l’option **/NOUI**. Si vous ne spécifiez pas un chemin de téléchargement, vous devez le faire à l’ouverture du téléchargeur d’installation. Le téléchargeur d’installation crée le dossier si celui-ci n’existe pas.  

    Exemples de commandes :

    -   **setupd &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre, vérifie les fichiers dans le dossier de téléchargement spécifié, puis télécharge uniquement les fichiers manquants ou présentant des versions plus récentes que les fichiers existants.     

    -   **setupdl /VERIFY &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d'installation démarre, puis vérifie les fichiers dans le dossier de téléchargement spécifié.  

    -   **setupdl /NOUI &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre, vérifie les fichiers dans le dossier de téléchargement spécifié, puis télécharge uniquement les fichiers manquants ou plus récents que les fichiers existants.  

    -   **setupdl /LANG &lt;chemin_téléchargement\>**  

        -   Le téléchargeur d’installation démarre, vérifie les fichiers de langue dans le dossier de téléchargement spécifié, puis télécharge uniquement les fichiers de langue manquants ou plus récents que les fichiers existants.  

    -   **setupdl /VERIFY**  

        -   Le téléchargeur d'installation démarre, et vous devez alors spécifier le chemin d'accès vers le dossier de téléchargement. Ensuite, une fois que vous avez cliqué sur **Vérifier**, le téléchargeur d’installation vérifie les fichiers dans le dossier de téléchargement.  

3.  Pour passer en revue les résultats du téléchargement, ouvrez le fichier **ConfigMgrSetup.log** situé dans le répertoire racine du lecteur C.
