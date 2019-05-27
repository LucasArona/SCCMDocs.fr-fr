---
title: Dossier CD.Latest
titleSuffix: Configuration Manager
description: Découvrez le processus permettant de distribuer des mises à jour du produit à partir de la console Configuration Manager.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b4f69d686a48af3c6e710c6aff592d71de1dbff1
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65496987"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Dossier CD.Latest pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager comporte un processus permettant de distribuer des mises à jour du produit à partir de la console Configuration Manager. Pour gérer cette nouvelle méthode de mise à jour de Configuration Manager, un nouveau dossier est créé, nommé **CD.Latest**. Il contient une copie des fichiers d’installation de Configuration Manager pour la version mise à jour du site.  

Le dossier CD.Latest comporte un dossier nommé **Redist**, dans lequel se trouvent les fichiers redistribuables téléchargés et utilisés par le programme d’installation. Ces fichiers sont mis en correspondance avec la version des fichiers de Configuration Manager dans ce dossier CD.Latest. Quand vous exécutez le programme d’installation à partir d’un dossier CD.Latest, vous devez utiliser les fichiers qui correspondent à cette version du programme d’installation. Vous pouvez faire en sorte que le programme d’installation télécharge les fichiers nouveaux et existants auprès de Microsoft, ou bien qu’il utilise les fichiers présents dans le dossier Redist du dossier CD.Latest.

Les supports de référence ne comportent pas de dossier **Redist**. Le site n’en crée un qu’à l’installation d’une mise à jour dans la console. En attendant, utilisez le dossier Redist auquel vous avez eu recours lors de l’installation de sites à partir du média de base de référence.  

> [!TIP]  
> Veillez à utiliser la dernière version des fichiers redistribuables. Si vous n’en avez pas téléchargé depuis quelque temps, autorisez le programme d’installation à le faire auprès de Microsoft.   

Les scénarios suivants permettent de créer ou de mettre à jour le dossier CD.Latest sur un serveur de site d’administration centrale ou de site principal :  

- Lorsqu’une mise à jour ou un correctif logiciel est installé à partir de la console Configuration Manager, le site crée ou met à jour le dossier dans le dossier d’installation de Configuration Manager.  

- Lorsque vous exécutez la tâche de sauvegarde intégrée de Configuration Manager, le site crée ou met à jour le dossier à l’emplacement du dossier de sauvegarde désigné.  

- Lorsque vous installez un nouveau site avec un support de référence, le site crée le dossier CD.Latest.


## <a name="supported-scenarios"></a>Scénarios pris en charge

Les fichiers sources du dossier CD.Latest sont pris en charge dans les scénarios suivants :  

### <a name="backup-and-recovery"></a>Sauvegarde et récupération
Pour récupérer un site, utilisez les fichiers source d’un dossier CD.Latest correspondant à votre site. Lorsque vous exécutez une sauvegarde de site à l’aide de la tâche de sauvegarde de site intégrée, le dossier CD.Latest est inclus dans le cadre de la sauvegarde.

- Quand vous réinstallez un site dans le cadre d’une récupération de site, vous le faites à partir du dossier CD.Latest inclus dans votre sauvegarde, à l’aide des versions de fichier correspondant à la sauvegarde et à la base de données de votre site.  

    - Si vous n’avez pas accès à la bonne version du dossier CD.Latest et des fichiers qu’il comporte, récupérez-la en installant un site dans un environnement lab. Ensuite, mettez à jour ce site en fonction de la version que vous souhaitez récupérer.  

    - Si le dossier CD.Latest souhaité et son contenu ne sont pas disponibles, il n’est pas possible de récupérer un site. Il faut alors le réinstaller.  

- Si vous n’avez pas de dossier CD.Latest mais disposez d’un site principal enfant ou d’un site d’administration centrale opérationnels, vous pouvez utiliser l’un des deux comme site de référence pour la récupération d’un site.  

### <a name="install-a-child-primary-site"></a>Site principal enfant
Si vous souhaitez installer un nouveau site principal enfant sous un site d’administration centrale ayant installé une ou plusieurs mises à jour dans la console, utilisez le programme d’installation et les fichiers sources figurant dans le dossier CD.Latest du site d’administration centrale. Ce processus utilise les fichiers sources d’installation correspondant à la version du site d’administration centrale. Pour plus d’informations, voir [Utiliser l’Assistant Installation pour installer des sites](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites).  

### <a name="expand-a-stand-alone-primary-site"></a>Étendre un site principal autonome
Lorsque vous développez un site principal autonome en installant un nouveau site d’administration centrale, utilisez le programme d’installation et les fichiers sources figurant dans le dossier CD.Latest du site principal. Ce processus utilise les fichiers sources d’installation correspondant à la version du site principal. Pour plus d’informations, consultez [Étendre un site principal autonome](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_expand).

### <a name="install-a-secondary-site"></a>Installer un site secondaire
<!-- SCCMDocs-pr issue #3164 -->
Si vous souhaitez installer un nouveau site secondaire sous un site principal ayant installé une ou plusieurs mises à jour dans la console, utilisez les fichiers sources figurant dans le dossier CD.Latest du site principal. 

Pour plus d’informations, voir [Installer un site secondaire](/sccm/core/servers/deploy/install/use-the-setup-wizard-to-install-sites#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Scénarios non pris en charge

Les fichiers sources mis à jour du dossier CD.Latest ne sont pas pris en charge pour les opérations suivantes :  
   
- installation d’un nouveau site pour une nouvelle hiérarchie ;  
- Mise à niveau d’un site Microsoft System Center 2012 Configuration Manager vers System Center Configuration Manager Current Branch
- Installation de clients Configuration Manager
- Installation de consoles Configuration Manager

