---
title: Installer l'éditeur de mise à jour
titleSuffix: Configuration Manager
description: Installer l'éditeur de mise à jour System Center
ms.date: 07/03/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f97decbe40293ee45cdc75c3fb36f4c57662ac06
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896775"
---
# <a name="install-updates-publisher"></a>Installer l'éditeur de mise à jour

*S’applique à : Éditeur de mise à jour System Center*

Les informations de cette rubrique peuvent vous aider à obtenir, installer et configurer l’éditeur de mise à jour pour une utilisation avec votre environnement.


## <a name="prerequisites-and-limitations"></a>Conditions préalables et limitations
Les sections suivantes détaillent la configuration requise pour installer et utiliser l’éditeur de mise à jour ainsi que limitations ou problèmes connus liés à son utilisation.

### <a name="operating-systems"></a>Systèmes d'exploitation
Installez et exécutez l’éditeur de mise à jour sur des éditions 64 bits des systèmes d’exploitation suivants. Il n’existe aucune condition préalable minimale pour les mises à jour cumulatives ou les Service Pack.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Professionnel, Éducation, Professionnel Éducation, Entreprise)
-   Windows 8.1 (Professionnel, Entreprise)

### <a name="prerequisites"></a>Prérequis
Les éléments suivants sont requis sur l’ordinateur qui exécute l’éditeur de mise à jour.

-   **Système d’exploitation 64 bits** : l’ordinateur sur lequel vous installez l’éditeur de mise à jour doit exécuter un système d’exploitation 64 bits.
-   **WSUS 4.0 ou version ultérieure** :
    -   Sur Windows Server, installez la console d’administration par défaut pour répondre à cette exigence.
    -   Pour Windows 10 et Windows 8.1, installez [Remote Server Administration Tools (RSAT) pour les systèmes d’exploitation Windows](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Cette opération installe la prise en charge nécessaire pour utiliser l’éditeur de mise à jour (*applets de commande PowerShell et API*, et *Console de gestion de l’interface utilisateur*).
-   **Autorisations** :
    -   Installation : Administrateur local
    -   La plupart des opérations : utilisateur local
    -   Publication ou autres opérations impliquant WSUS : Membre du groupe Administrateurs WSUS sur le serveur WSUS.

### <a name="supported-languages"></a>Langues prises en charge
L’éditeur de mise à jour est disponible uniquement en anglais mais peut gérer les mises à jour pour d’autres langues. La prise en charge de la langue dépend de la tâche, par exemple la publication, la création ou la modification de mises à jour.

Lors de l’exportation ou de la publication de mises à jour, l’éditeur de mise à jour affiche le titre et la description de la mise à jour en fonction des paramètres régionaux de l’ordinateur sur lequel l’éditeur est installé.

Par exemple, vous créez une mise à jour logicielle avec un titre en anglais et en espagnol.

-   Si vous créez la mise à jour sur un ordinateur dont les paramètres régionaux sont définis sur Anglais, par défaut, le titre et la description s’affichent en anglais.
-   Si vous exportez ou publiez ensuite cette mise à jour sur un ordinateur dont les paramètres régionaux sont définis sur Espagnol, le titre et la description apparaissent en espagnol sur cet ordinateur.

### <a name="publishing"></a>Publication
Lorsque vous publiez des mises à jour logicielles, vous pouvez spécifier la langue du fichier binaire de la mise à jour logicielle. Vous pouvez également spécifier que le fichier binaire est indépendant de la langue. Les langues suivantes sont prises en charge :

-   Arabe
-   Chinois (Hong Kong)
-   Chinois (traditionnel)
-   Chinois (simplifié)
-   Tchèque
-   Danois
-   Néerlandais
-   Anglais
-   Finnois
-   Français
-   Allemand
-   Grec
-   Hébreu
-   Hongrois
-   Italien
-   Japonais
-   Coréen
-   Norvégien
-   Polonais
-   Portugais
-   Portugais (Brésil)
-   Russe
-   Espagnol
-   Suédois
-   Turc

### <a name="software-update-titles-and-descriptions"></a>Titres et descriptions des mises à jour logicielles
Les langues suivantes sont prises en charge pour les titres et les descriptions des mises à jour logicielles.

-   Chinois (traditionnel)
-   Chinois (simplifié)
-   Anglais
-   Français
-   Allemand
-   Italien
-   Japonais
-   Coréen
-   Portugais (Brésil)
-   Russe
-   Espagnol



## <a name="install-updates-publisher"></a>Installer l'éditeur de mise à jour
Obtenez le fichier **UpdatesPubliser.msi** pour installer l’éditeur de mise à jour System Center à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=55543).

Pour installer l’éditeur de mise à jour, exécutez le fichier **UpdatesPublisher.msi** sur un ordinateur remplissant les *conditions préalables*. Le programme d’installation crée le dossier suivant contenant les fichiers nécessaires pour exécuter l’éditeur de mise à jour : *&lt;chemin&gt;\Program Files\Microsoft\UpdatesPublisher*.

Comme ce dossier contient tous les fichiers nécessaires pour utiliser l’éditeur de mise à jour, vous pouvez copier le dossier et son contenu vers un nouvel emplacement ou ordinateur, puis utiliser l’éditeur de mise à jour depuis cet emplacement. Toutefois, le nouvel emplacement ou ordinateur doit remplir les conditions requises pour exécuter l’éditeur de mise à jour.

Une fois l’installation terminée, exécutez le fichier **UpdatesPublisher.exe** depuis le dossier *UpdatesPublisher* pour démarrer l’éditeur de mise à jour.

## <a name="next-steps"></a>Étapes suivantes
 Après avoir installé l’éditeur de mise à jour, nous vous recommandons de [configurer ses options](updates-publisher-options.md). Vous devez configurer quelques options avant de pouvoir utiliser certaines fonctionnalités de l’éditeur de mise à jour.

 Toutefois, si vous souhaitez utiliser les valeurs par défaut et n’envisagez pas de déployer des mises à jour sur un serveur de mise à jour ou sur des appareils gérés, vous pouvez passer directement à la [gestion des catalogues de mises à jour logicielles](updates-publisher-catalogs.md) ou à la [création de mises à jour logicielles](create-updates-with-updates-publisher.md) et créer vos propres catalogues de mises à jour.

