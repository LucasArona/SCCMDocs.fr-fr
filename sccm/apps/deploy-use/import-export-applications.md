---
title: Importer et exporter des applications
titleSuffix: Configuration Manager
description: Découvrez comment importer et exporter des applications dans Configuration Manager afin de les partager entre des hiérarchies distinctes.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 02bb394de4f3bb947bdc2669a830167089c42311
ms.sourcegitcommit: 3f43fa8462bf39b2c18b90a11a384d199c2822d8
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66411008"
---
# <a name="import-and-export-applications"></a>Importer et exporter des applications

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez Configuration Manager pour importer et exporter des applications entre deux hiérarchies. Par exemple, copiez une application à partir d’un environnement de test vers un environnement de production.

## <a name="export"></a>Exporter

1. Dans la console Configuration Manager, sélectionnez le nœud **Applications**. Dans le groupe Créer du ruban, choisissez **Exporter une application**.
1. Sur l’écran **Général**, entrez un chemin vers un nouveau fichier ZIP vers lequel effectuer l’exportation. Si vous le souhaitez, spécifiez s’il faut exporter les *dépendances, les relations de remplacement, les conditions et les environnements virtuels*, ainsi que le *contenu des applications et dépendances sélectionnées*.  Entrez éventuellement des commentaires d’administrateur, puis sélectionnez **Suivant**.
1. Vérifiez que l’application et toutes les dépendances sont listées dans la page **Objets associés**, puis sélectionnez **Suivant**.
1. Dans la page de synthèse, sélectionnez **Suivant**.
1. Une fois le processus terminé, le fichier ZIP est créé et vous pouvez fermer l’Assistant.

> [!IMPORTANT]
> Si vous prévoyez de copier cette application vers un autre environnement, prenez le fichier ZIP et le dossier qui l’accompagne. Le fichier ZIP doit se trouver dans le même répertoire que le dossier créé.

## <a name="import"></a>Importation

> [!NOTE]
> Vous pouvez importer des applications uniquement à partir de chemins UNC. Vous ne pouvez pas effectuer une importation directement à partir de votre disque local.

1. Dans la console Configuration Manager, sélectionnez le nœud **Applications**. Dans le groupe Créer du ruban, choisissez **Importer une application**.
1. Choisissez le fichier ZIP que vous voulez importer, puis sélectionnez **Suivant**.
1. La fenêtre Contenu du fichier montre ce qui se passe quand vous importez l’application. Sélectionnez **Suivant**.
1. Passez en revue l’écran de synthèse, puis sélectionnez **Suivant**.
1. Fermez l’Assistant. L’application est maintenant disponible sur le site.

## <a name="see-also"></a>Voir aussi
 
Automatiser l’importation et l’exportation d’applications à l’aide de PowerShell

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
