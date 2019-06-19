---
title: 'Synchroniser les mises à jour sans connexion Internet '
titleSuffix: Configuration Manager
description: Exécutez la synchronisation des mises à jour logicielles à partir du point de mise à jour logicielle de niveau supérieur qui est déconnecté d’Internet.
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.collection: M365-identity-device-management
ms.openlocfilehash: 67b284e369268b184067e33d2a505585618795e5
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65493984"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Synchroniser les mises à jour logicielles à partir d’un point de mise à jour logicielle déconnecté  

*S’applique à : System Center Configuration Manager (Current Branch)*

 Quand le point de mise à jour logicielle sur le site de niveau supérieur est déconnecté d'Internet, vous devez utiliser les fonctions d'exportation et d'importation de l'outil WSUSUtil pour synchroniser les métadonnées des mises à jour logicielles. Vous pouvez choisir un serveur WSUS existant qui ne fait pas partie de votre hiérarchie Configuration Manager en tant que source de synchronisation. Cette rubrique fournit des informations sur l’utilisation des fonctions d’exportation et d’importation de l’outil WSUSUtil.  

 Pour exporter et importer des métadonnées de mises à jour logicielles, vous devez les exporter de la base de données WSUS sur un serveur d'exportation spécifié, copier les fichiers du contrat de licence stockés localement vers le point de mise à jour logicielle déconnecté, puis importer les métadonnées des mises à jour logicielles dans la base de données WSUS sur le point de mise à jour logicielle déconnecté.  

 Utilisez le tableau suivant pour identifier le serveur d'exportation vers lequel exporter les métadonnées des mises à jour logicielles.  

|Point de mise à jour logicielle|Source de mise à jour en amont pour les points de mise à jour logicielle connectés|Serveur d'exportation d'un point de mise à jour logicielle déconnecté|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Site d'administration centrale|Microsoft Update (Internet)<br /><br /> Serveur WSUS existant|Choisissez un serveur WSUS qui est synchronisé avec Microsoft Update en utilisant les classifications de mise à jour logicielle, les produits et les langues dont vous avez besoin dans votre environnement Configuration Manager.|  
|Site principal autonome|Microsoft Update (Internet)<br /><br /> Serveur WSUS existant|Choisissez un serveur WSUS qui est synchronisé avec Microsoft Update en utilisant les classifications de mise à jour logicielle, les produits et les langues dont vous avez besoin dans votre environnement Configuration Manager.|  

 Avant de commencer le processus d'exportation, vérifiez que la synchronisation des mises à jour logicielles est terminée sur le serveur d'exportation sélectionné pour vous assurer que les métadonnées des mises à jour logicielles les plus récentes sont synchronisées. Pour vérifier que la synchronisation des mises à jour logicielles s'est terminée correctement, procédez comme suit.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>Pour vérifier que la synchronisation des mises à jour logicielles s'est terminée correctement sur le serveur d'exportation  

1.  Ouvrez la console d'administration WSUS et connectez-vous à la base de données WSUS sur le serveur d'exportation.  

2.  Dans la console d'administration WSUS, cliquez sur **Synchronisations**. Une liste des tentatives de synchronisation des mises à jour logicielles s'affiche dans le volet des résultats.  

3.  Dans le volet des résultats, chercher les dernières tentatives de synchronisation des mises à jour logicielles et vérifiez que la synchronisation s'est terminée correctement.  

> [!IMPORTANT]  
>  L'outil WSUSUtil doit être exécuté localement sur le serveur d'exportation afin d'exporter les métadonnées des mises à jour logicielles et il doit également être exécuté sur le serveur du point de mise à jour logicielle déconnecté afin d'importer les métadonnées des mises à jour logicielles. En outre, l'utilisateur qui exécute l'outil WSUSUtil doit être membre du groupe Administrateurs local sur chaque serveur.  

## <a name="export-process-for-software-updates"></a>Processus d’exportation pour les mises à jour logicielles  
 Le processus d'exportation des mises à jour logicielles comporte deux étapes principales : pour copier les fichiers du contrat de licence stockés localement dans le point de mise à jour logicielle déconnecté et pour exporter les métadonnées des mises à jour logicielles de la base de données WSUS sur le serveur d'exportation.  

 Pour copier les métadonnées du contrat de licence local vers le point de mise à jour logicielle déconnecté, procédez comme suit.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>Pour copier les fichiers locaux du serveur d'exportation vers le serveur du point de mise à jour logicielle déconnecté  

1. Sur le serveur d'exportation, accédez au dossier dans lequel les mises à jour logicielles et les termes du contrat de licence des mises à jour logicielles sont stockés. Par défaut, le serveur WSUS stocke les fichiers dans <*lecteur_installation_WSUS*>\WSUS\WSUSContent\\, où *lecteur_installation_WSUS* correspond au lecteur sur lequel WSUS est installé.  

2. Copiez tous les fichiers et dossiers depuis cet emplacement vers le dossier WSUSContent sur le serveur du point de mise à jour logicielle déconnecté.  

   Pour exporter les métadonnées des mises à jour logicielles à partir de la base de données WSUS sur le serveur d'exportation, procédez comme suit.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>Pour exporter les métadonnées des mises à jour logicielles à partir de la base de données WSUS sur le serveur d'exportation  

1.  À l'invite de commandes sur le serveur d'exportation, accédez au dossier qui contient WSUSutil.exe. Par défaut, l'outil se trouve dans %*ProgramFiles*%\Update Services\Tools. Par exemple, si l’outil se trouve à l’emplacement par défaut, tapez **cd %ProgramFiles%\Update Services\Tools**.  

2.  Tapez ce qui suit pour exporter les métadonnées des mises à jour logicielles vers un fichier de package :  

     **wsusutil.exe export** *nompackage* *fichierjournal*  

     Par exemple :  

     **wsusutil.exe export export.cab export.log**  

     Le format peut être résumé comme suit : WSUSutil.exe est suivi de l’option d’exportation, du nom du fichier .cab d’exportation créé pendant l’opération d’exportation et du nom d’un fichier journal. WSUSutil.exe exporte les métadonnées du serveur d'exportation et crée un fichier journal de l'opération.  

    > [!NOTE]  
    >  Le nom du package (fichier .cab) et du fichier journal doivent être uniques dans le dossier actif.  

3.  Déplacez le package d'exportation dans le dossier qui contient WSUSutil.exe sur le serveur d'importation WSUS.  

    > [!NOTE]  
    >  Si vous déplacez le package vers ce dossier, l'expérience d'importation peut s'avérer plus facile. Vous pouvez déplacer le package vers un emplacement accessible au serveur d'importation, puis spécifier l'emplacement pendant l'exécution de WSUSutil.exe.  

## <a name="import-software-updates-metadata"></a>Importer les métadonnées des mises à jour logicielles  
 Pour importer les métadonnées des mises à jour logicielles depuis le serveur d'exportation vers le point de mise à jour logicielle déconnecté, procédez comme suit.  

> [!IMPORTANT]  
>  N'importez jamais de données exportées à partir d'une source non approuvée. Si vous importez du contenu à partir d'une source non approuvée, vous risquez de compromettre la sécurité de votre serveur WSUS.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>Pour importer les métadonnées de la base de données du serveur d'importation  

1.  À l'invite de commandes sur le serveur WSUS d'importation, accédez au dossier qui contient WSUSutil.exe. Par défaut, l'outil se trouve dans %*ProgramFiles*%\Update Services\Tools.  

2.  Tapez la commande suivante :  

     **wsusutil.exe import** *nompackage* *fichierjournal*  

     Par exemple :  

     **wsusutil.exe import export.cab import.log**  

     Le format peut être résumé comme suit : WSUSutil.exe est suivi par la commande d’importation, le nom du fichier de package (.cab) créé pendant l’opération d’exportation, le chemin du fichier de package s’il se trouve dans un autre dossier et le nom d’un fichier journal. WSUSutil.exe importe les métadonnées du serveur d'exportation et crée un fichier journal de l'opération.  

## <a name="next-steps"></a>Étapes suivantes
À l’issue de la première synchronisation de mises à jour logicielles ou après la mise à disposition de nouvelles classifications ou de nouveaux produits, vous devez [configurer les nouvelles classifications et les nouveaux produits](configure-classifications-and-products.md) pour synchroniser les mises à jour logicielles avec les nouveaux critères.

Après avoir synchronisé les mises à jour logicielles avec les critères dont vous avez besoin, [gérez les paramètres des mises à jour logicielles](manage-settings-for-software-updates.md).  
