---
title: Comment analyser et convertir des packages
titleSuffix: Configuration Manager
description: En savoir plus sur l’analyse et la conversion de packages avec Package Conversion Manager dans Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f3bf1737-827d-48fa-8bb1-f48fe71afe0c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9c58e12d906606acc0015d38e543616570d61520
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297217"
---
# <a name="how-to-analyze-and-convert-packages-with-package-conversion-manager"></a>Comment analyser et convertir des packages avec Package Conversion Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357861-->

Avant de convertir un package, analysez-le. Selon les résultats de l'analyse, vous pouvez ensuite effectuer l'une des tâches suivantes :

- **Convertir** le package en application. Dans la liste **Package** de la console, l'état de préparation indique **Automatique**.  

- **Corriger et convertir** le package, attacher des regroupements et créer des conditions globales. Dans la liste **Package** de la console, l'état de préparation indique **Automatique**.  

- **Corriger et convertir** le package. Dans la liste **Package** de la console, l'état de préparation indique **Manuel**.  

- Laissez le package non converti. Dans la liste **Package** de la console, l'état de préparation indique **Non applicable**.  



## <a name="bkmk_analyze"></a> Comment analyser les packages

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Gestion des applications**, puis sélectionnez le nœud **Packages**.  

2. Sélectionnez le package à convertir. Dans l’onglet **Accueil** du ruban, dans le groupe **Package Conversion**, sélectionnez **Analyser le package**. Package Conversion Manager analyse le package.  

3. Pour voir l’état de préparation du package, ajoutez la colonne **Préparation** à la liste des packages. L’état de préparation du package détermine votre prochaine action :  

    - **Automatique** : [comment convertir des packages](#bkmk_convert)  

        Pour attacher également des regroupements et créer des conditions globales avec un état de préparation **Automatique**, consultez [Comment corriger et convertir des packages](#bkmk_fix).  

    - **Manuel** : [Comment corriger et convertir des packages](#bkmk_fix)

    - **Non Applicable** : correspond à un package auquel il manque du contenu ou un programme requis. Ajoutez le contenu ou les programmes manquants puis relancez l’analyse. Ou laissez le package dans un état non converti et continuez à le déployer en tant que package.  



## <a name="bkmk_convert"></a> Comment convertir des packages

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Gestion des applications**, puis sélectionnez le nœud **Packages**.  

2. Sélectionnez le package à convertir dont l'état de préparation est **Automatique**. Dans l’onglet **Accueil** du ruban, dans le groupe **Package Conversion**, sélectionnez **Convertir le package**. L'Assistant Conversion du package en application s'ouvre.  

3. Dans l’assistant Conversion du package en application, passez en revue la liste des packages sélectionnés. Supprimez tous les packages que vous ne souhaitez pas convertir, puis sélectionnez **OK**. Package Conversion Manager convertit le package. La fenêtre Conversion terminée affiche l’état de conversion des nouvelles applications.  

    > [!Note]  
    > Lorsque vous convertissez un package, le site enregistre la date et l’heure de la conversion en tant qu’heure UTC.  

4. Suivez les instructions affichées dans la fenêtre. Sélectionnez **Afficher les applications** ou **Fermer**.  



## <a name="bkmk_fix"></a> Comment corriger et convertir des packages

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Gestion des applications**, puis sélectionnez le nœud **Packages**.  

2. Sélectionnez un package dont l'état de préparation est **Manuel** ou **Automatique**. Dans l’onglet **Accueil** du ruban, dans le groupe **Package Conversion**, sélectionnez **Corriger et convertir**.  

3. Dans l'Assistant Conversion de package, passez en revue les informations de la page **Sélection du package**, en notant les **Éléments à corriger**. Puis sélectionnez **Suivant**.  

4. A la page **Vérification des dépendances**, vérifiez si le package dépend d’autres packages répertoriés, puis sélectionnez **Suivant**.  

    > [!Note]  
    > Si vous n’avez converti aucun des packages dépendants répertoriés, convertissez d’abord ces packages. Redémarrez ensuite le processus de conversion de package.  
    >  
    > Si une dépendance n'est pas nécessaire, supprimez-la ou ignorez-la et continuez le processus de conversion.  

5. A la page **Type de déploiement**, passez en revue les types de déploiement pour la nouvelle application. Modifiez leurs priorités ou supprimez les types de déploiement.  

6. Si un des nouveaux types de déploiement n’est associé à aucune méthode de détection, la colonne **Méthode de détection** affiche une icône d’avertissement. Effectuez les actions suivantes :  

    1. Sélectionnez **Modifier la méthode de détection**.  

    2. Sélectionnez **Ajouter**.  

    3. Dans la boîte de dialogue Règle de détection, spécifiez un **Type de paramètre**.  

    4. Pour le type de paramètre spécifié, entrez les informations supplémentaires requises pour la règle de détection.  

    5. Sélectionnez **OK**. Si nécessaire, répétez ce processus pour ajouter plusieurs méthodes de détection à chaque type de déploiement.  

    6. Sélectionnez **OK**. Vérifiez que la colonne **Méthode de détection** affiche une icône confirmant que la méthode de détection a été correctement spécifiée.  

7. Sélectionnez **Suivant**.  

8. A la page **Sélection des spécifications**, passez en revue les types de déploiement de la nouvelle application. Sélectionnez un type de déploiement, puis passez en revue ses spécifications.  

    > [!Note]  
    > L’assistant affiche uniquement les spécifications converties par Package Conversion Manager. Il ne convertit pas toutes les requêtes WQL des regroupements d'appareils en spécifications.  

9. Ajoutez des spécifications pour un type de déploiement sélectionné, si nécessaire.  

10. Sélectionnez **Suivant**.  

11. Terminez l'assistant pour créer l’application.  

    > [!Note]  
    > Lorsque vous convertissez un package, le site enregistre la date et l’heure de la conversion en tant qu’heure UTC.  



## <a name="bkmk_monitor"></a> Surveiller le déploiement

Accédez à l’espace de travail **Surveillance** de la console Configuration Manager, puis sélectionnez le nœud **État de la conversion de package**. Ce tableau de bord montre l’analyse globale, ainsi que l’état de conversion des packages du site. Une nouvelle tâche d’arrière-plan résume automatiquement les données d’analyse.

> [!Tip]  
> Package Conversion Manager intégré à Configuration Manager ne nécessite pas qu’une analyse de packages soit planifiée. Cette action est gérée par la tâche de totalisation intégrée.

![Capture d’écran d’un exemple de tableau de bord d’état des conversions de packages](media/1357861-pcm-dashboard.png)
