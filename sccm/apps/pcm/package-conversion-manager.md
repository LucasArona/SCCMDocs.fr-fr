---
title: Package Conversion Manager
titleSuffix: Configuration Manager
description: En savoir plus sur Package Conversion Manager pour convertir des packages en applications dans Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: f053fa73-c553-4522-a6b9-f885f23fe57c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 41dd6ad6f8a0292fdb16a0d727665b17e038f87b
ms.sourcegitcommit: 1439817f1309658b31008d7bafaab32fc5ef8789
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52820039"
---
# <a name="package-conversion-manager"></a>Package Conversion Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357861-->

À partir de la version 1806, Package Conversion Manager vous permet de convertir en applications des packages Configuration Manager hérités. Les applications offrent d’autres avantages tels que les dépendances, les règles de spécification, les méthodes de détection et l’affinité entre utilisateur et appareil.

> [!Tip]  
> Cette fonctionnalité a été introduite dans la version 1806 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). Depuis la version 1810, cette fonctionnalité n’est plus en préversion.  


Une application Configuration Manager contient des fichiers et programmes que vous pouvez déployer sur des appareils clients. Toutefois, contrairement aux packages et programmes hérités, une application fournit des fonctionnalités supplémentaires centrées sur le client. Par exemple, une application peut contenir des types de déploiement pour une installation locale d'un package de logiciel, un package d'application virtuelle ou une version de l'application pour les appareils mobiles.

Pour plus d’informations, consultez les articles suivants : 
- [Introduction à la gestion des applications](/sccm/apps/understand/introduction-to-application-management)  
- [Packages et programmes](/sccm/apps/deploy-use/packages-and-programs)  

> [!Important]  
> Si vous avez installé une ancienne version de Package Conversion Manager, désinstallez-la avant de mettre à niveau votre site. Cette version intégrée ne nécessite pas d’installation, toutefois, elle peut créer un conflit avec les versions existantes.  

Cette version intégrée de Package Conversion Manager fonctionne sur les packages dans le site Current Branch Configuration Manager. Il ne s’agit pas d’un outil autonome. Si vous avez des packages et programmes dans une version antérieure de Configuration Manager, vous devez d’abord migrer les packages vers votre site Current Branch. Pour plus d’informations, consultez [Faire migrer des données entre des hiérarchies](/sccm/core/migration/migrate-data-between-hierarchies).



## <a name="planning"></a>Planning

Avant de commencer la conversion des packages en applications, développez d’abord un plan. Le processus suivant est un exemple de plan :

- [Définir un plan de conversion de packages détaillé](#bkmk_define)  

- [Sélectionner et préparer les packages pour la conversion](#bkmk_prepare)  

- [Sélectionner les packages de test](#bkmk_test)  

- [Analyser, examiner et convertir des packages](#bkmk_analyze)  

- [Tester et déployer les applications](#bkmk_deploy)  


### <a name="bkmk_define"></a> Définir un plan de conversion de packages détaillé

Cette section décrit deux exemples de plans de conversion de packages :  

- [Un environnement de test avec ressources nombreuses](#bkmk_define-high) : vous disposez d'un environnement de test avec les ressources, les autorisations et l'architecture nécessaires pour répliquer entièrement votre environnement de production.  

- [Un environnement de test avec ressources limitées](#bkmk_define-limited) : vous ne disposez pas d’un environnement de test qui réplique entièrement votre environnement de production.  

Ajustez ces plans en fonction d’autres problèmes spécifiques à votre environnement.

#### <a name="bkmk_define-high"></a> Exemple de plan pour un environnement de test avec ressources nombreuses

Votre environnement de test dispose de ressources, d’autorisations et d’une architecture similaires à votre environnement de production. Utilisez l’environnement de test pour analyser et convertir efficacement tous vos packages puis tester toutes vos applications Configuration Manager. Une fois cette tâche terminée, transférez les packages vers l’environnement de production. 

Votre plan de conversion de packages peut être semblable aux étapes suivantes :  

1.  Sélectionner les packages à convertir.  

2.  Migrer les packages à convertir dans votre environnement de test.  

3.  Préparer les packages pour la conversion.  

4.  Sélectionner les packages de test.  

5.  Analyser, examiner et convertir les packages de test.  

6.  Tester les applications converties.  

7.  Analyser et convertir les packages restants (autres que les packages de test).  

8.  Exporter les applications à partir de l’environnement de test. Importer les applications dans votre environnement de production.  

#### <a name="bkmk_define-limited"></a> Exemple de plan pour un environnement de test avec ressources limitées

Votre environnement de test ne dispose pas des ressources, des autorisations et d’une architecture similaires à votre environnement de production. Vous ne pouvez pas analyser, tester et convertir tous vos packages. Dans ce scénario, analysez, examinez, convertissez et testez uniquement vos packages de test. Ensuite, migrez les packages restants vers l’environnement de production pour l’analyse et la conversion. 

Votre plan de conversion de packages peut être semblable aux étapes suivantes :

1.  Sélectionner les packages à convertir.  

2.  Sélectionner les packages de test.  

3.  Migrer les packages de test dans votre environnement de test.  

4.  Préparer les packages de test pour la conversion.  

5.  Analyser, examiner et convertir les packages de test.  

6.  Tester les applications converties.  

7.  Exporter les applications de test à partir de l’environnement de test. Importer ensuite les applications dans votre environnement de production.  

8.  Migrer les packages restants dans l'environnement de production et les préparer pour la conversion.  

9.  Analyser, examiner et convertir les packages restants dans l'environnement de production.  

10. Publier les applications restantes dans l'environnement de production.  


### <a name="bkmk_prepare"></a> Sélectionner et préparer les packages pour la conversion

#### <a name="bkmk_prepare-select"></a> Sélectionner les packages à convertir

Les packages ne conviennent pas tous à la conversion en applications. Avant de commencer à convertir des packages, identifiez ceux qui ne seront pas convertis. 

Les meilleurs types de packages pour la conversion en applications sont ceux qui contiennent des logiciels orientés utilisateur, par exemple :  

 - Fichiers Windows Installer (.msi et .msu)  

 - Programmes Microsoft Application Virtualization (App-V)  

 - Fichiers exécutables Windows (.exe)  

Les types de packages qu'il est préférable de conserver sous forme de packages et de ne pas convertir en applications sont, entre autres, les suivants :

 - Outils de maintenance du système. Par exemple les scripts ou les utilitaires de sauvegarde.  

 - Packages de logiciels non pris en charge.

> [!Tip]  
> Une fois que vous avez identifié les packages qui ne conviennent pas à la conversion en applications, déplacez-les vers un dossier distinct dans la console Configuration Manager. Pour créer un dossier de packages dans la console Configuration Manager :  
> - Cliquez avec le bouton droit sur le nœud **Packages**.  
> - Sélectionnez **Dossiers**, puis **Créer un dossier**.  
> - Entrez le nom du dossier, par exemple `Not Converted`.  
> - Cliquez sur **OK**.  

#### <a name="prepare-the-packages-for-conversion"></a>Préparer les packages pour la conversion

Assurez-vous que chaque package que vous souhaitez convertir remplit les conditions suivantes :  

 - L’emplacement des fichiers source est un chemin d’accès UNC complet, par exemple `\\Server\Share\File`.  

 - Les fichiers Windows Installer n'utilisent qu’un seul code de produit unique.  


### <a name="bkmk_test"></a> Sélectionner les packages de test

Si possible, votre groupe de packages de test doit inclure des packages qui remplissent les critères suivants :  

 - Au moins un package de test est à l'état de préparation **Automatique**.  

 - Au moins un package de test est à l'état de préparation **Manuel**.  

Dans l'idéal, vos packages de test doivent être des packages de base, par exemple :  

 - des packages que vous connaissez bien ,  

 - les packages qui sont les plus importants pour votre organisation ;  

 - les packages les plus faciles à tester.  

Identifiez les packages adaptés au test. Puis déplacez-les vers un dossier distinct dans la console Configuration Manager.


### <a name="bkmk_analyze"></a> Analyser, examiner et convertir des packages

#### <a name="analyze-packages"></a>Analyser des packages

Pour analyser un package individuel ou un petit groupe, utilisez Package Conversion Manager, intégré à la console Configuration Manager. Pour plus d’informations, consultez [Comment analyser et convertir des packages](/sccm/apps/pcm/how-to-analyze-and-convert).  

> [!NOTE]  
> Consultez le nœud **État de la conversion de package** dans l’espace de travail **Analyse**. Il affiche des informations de synthèse sur les processus d'analyse et de conversion.  

#### <a name="investigate-analysis-results"></a>Examiner les résultats de l'analyse

Après avoir analysé les packages de test, examinez les packages dont l'état de préparation est **Manuel** ou **Erreur**. Déterminez les raisons pour lesquelles ils sont dans cet état. Voici quelques causes courantes d'un état de préparation **Manuel** ou **Erreur** :

 - Le package ne contient pas les informations nécessaires pour créer une méthode de détection dans un type de déploiement d'application.  

 - Le package ne contient pas les informations nécessaires pour convertir les regroupements en conditions globales et en spécifications.  

 - Le package contient plusieurs programmes.  

 - Le package dépend d'un autre package que vous n’avez pas converti en application.  

Pour plus d'informations, utilisez les ressources suivantes :  

- Passez en revue les messages d'erreur et les correctifs dans [Informations techniques de référence sur les messages d'erreur de Package Conversion Manager](/sccm/apps/pcm/error-messages)  

- Passez en revue le fichier journal **PCMTrace.log**  

- [Dépanner Package Conversion Manager](/sccm/apps/pcm/troubleshoot-pcm)  

#### <a name="convert-the-packages"></a>Convertir les packages

Pour plus d’informations sur la façon de convertir des packages, consultez [Comment analyser et convertir des packages](/sccm/apps/pcm/how-to-analyze-and-convert).

> [!NOTE]  
> Consultez le nœud **État de la conversion de package** dans l’espace de travail **Analyse**. Il affiche des informations de synthèse sur les processus d'analyse et de conversion.  


### <a name="bkmk_deploy"></a> Tester et déployer les applications

Testez les applications dans votre environnement de test ou votre environnement de production, en fonction de votre plan de conversion de packages détaillé.



## <a name="recommendations"></a>Recommandations

- Utilisez le tableau de bord **État de la conversion de package** dans l’espace de travail **Analyse**. Il affiche des informations de synthèse sur les processus d'analyse et de conversion.  

- Examinez les programmes dans vos packages appelés wrappers. Utilisez le plug-in Package Conversion Manager pour convertir leurs fonctions en fonctionnalités Configuration Manager équivalentes.  

- Assurez-vous de tester minutieusement chaque application convertie avant de la déployer dans un environnement de production.  



## <a name="next-steps"></a>Étapes suivantes

[Comment analyser et convertir des packages](/sccm/apps/pcm/how-to-analyze-and-convert)