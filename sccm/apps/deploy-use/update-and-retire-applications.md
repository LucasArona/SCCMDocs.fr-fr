---
title: Mettre à jour et mettre hors service des applications
titleSuffix: Configuration Manager
description: Révisez, remplacez ou désinstallez des applications déployées à l’aide de System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 68ac8a07-8e54-4a3c-91e3-e50dc1cabf5d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 767d6b54d19158a33b582dc3ab605d780914b18e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132814"
---
# <a name="update-and-retire-applications-with-system-center-configuration-manager"></a>Mettre à jour et mettre hors service des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Vous finirez probablement par vouloir apporter des modifications à une application, en désinstaller une ou remplacer une application déjà déployée par une nouvelle. System Center Configuration Manager offre ces fonctionnalités pour vous aider à mettre à jour et mettre hors service des applications :  

- **Réviser des applications**. Quand vous apportez des modifications à un type d’application ou de déploiement, Configuration Manager conserve un historique de ces modifications. Vous pouvez revenir à tout moment à la version révisée précédente de l’application. Vous pouvez également afficher les propriétés de chaque révision, restaurer une révision précédente d’une application ou supprimer une ancienne révision.  

  Pour plus d’informations, consultez [Révisions d’applications](revise-and-supersede-applications.md#application-revisions).  

- **Remplacer des applications**. Une relation de remplacement vous permet de mettre à niveau ou remplacer des applications existantes. Quand vous remplacez une application, vous pouvez spécifier un nouveau type de déploiement pour remplacer le type de déploiement de l’application remplacée. Vous pouvez aussi définir s’il faut mettre à niveau ou désinstaller l’application remplacée avant d’installer l’application de remplacement.  

  Pour plus d’informations, consultez [Remplacement d’applications](revise-and-supersede-applications.md#application-supersedence).  

- **Désinstaller des applications**. Configuration Manager facilite la désinstallation d’une application. La désinstallation peut s’effectuer sans assistance, c’est-à-dire sans intervention de l’utilisateur de l’application ou de l’appareil.  

  Pour plus d’informations, consultez [Désinstaller des applications](uninstall-applications.md).  
