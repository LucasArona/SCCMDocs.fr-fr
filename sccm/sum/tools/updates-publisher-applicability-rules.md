---
title: Règles de mise en application
titleSuffix: Configuration Manager
description: Gérer les règles de mise en application pour l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: 3cf0c2cd-397a-4622-b11c-961f334fb7d7
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 30200c9da2ea37ef0868db680d04fe6aae9fd314
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67678084"
---
# <a name="manage-applicability-rules-in-updates-publisher"></a>Gérer les règles de mise en application dans l’éditeur de mise à jour

*S’applique à : l'éditeur de mise à jour System Center*

Avec l’éditeur de mise à jour, les règles de mise en application définissent les exigences qui doivent être remplies pour qu’un appareil puisse installer une mise à jour. Les règles sont également utilisées pour déterminer si une mise à jour a été installée sur un ordinateur. Une règle de mise en application complexe comportant plusieurs parties est appelée ensemble de règles.

Les offres groupées de mises à jour n’utilisent pas de règles de mise en application.

## <a name="overview-of-applicability-rules"></a>Vue d’ensemble des règles de mise en application
Vous gérez les règles de mise en application dans l **’espace de travail Règles**. Lorsque vous créez une règle, vous spécifiez une ou plusieurs conditions. Si plusieurs conditions sont spécifiées, vous pouvez configurer des relations entre ces conditions afin de les évaluer de façon séquentielle ou de les combiner dans des instructions logiques **And** ou **Or**.

Par exemple, voici un ensemble de règles contenant trois règles. La première règle vérifie que le fichier *MyFile* existe, et les deuxième et troisième règles vérifient que la langue du système d’exploitation Windows est l’anglais ou le japonais.

```
And  
  File ‘\[PROGRAM\_FILES\] \\Microsoft\\MyFile’ exists  
  Or  
    Windows Language is English   
    Windows Language is Japanese
```

Toutes les mises à jour requièrent au moins une règle de mise en application. Les mises à jour que vous importez contiennent déjà des règles de mise en application, et lorsque vous créez vos propres mises à jour, vous devez y ajouter une ou plusieurs règles. Vous pouvez modifier et développer les règles de n’importe quelle mise à jour dans l’éditeur de mise à jour.

Pour afficher les règles que vous avez créées, dans l’**espace de travail Règles**, sélectionnez une règle dans la liste **Mes règles enregistrées**. Les conditions individuelles et les opérations logiques de cette règle s’affichent dans le volet **Règles de mise en application** de la console. Les règles des mises à jour que vous importez peuvent uniquement être affichées et modifiées lors de la modification de ces mises à jour.

Vous pouvez créer des règles à deux emplacements dans l’éditeur de mise à jour :

-   Dans l **’espace de travail Règles**, vous créez et **enregistrez** des ensembles de règles que vous pouvez utiliser ultérieurement. Lors de la modification ou de la création d’une mise à jour, vous pouvez sélectionner **Règle enregistrée** comme **type de règle**, puis choisir dans une liste de vos ensembles de règles précréés.

-   Vous pouvez également créer des règles lorsque vous créez ou modifiez une mise à jour. Les règles que vous créez de cette façon ne sont pas enregistrées pour une utilisation ultérieure.

## <a name="create-applicability-rule"></a>Créer une règle de mise en application
Les informations suivantes sont similaires à la création de règles depuis l[’Assistant Création d’une mise à jour](/sccm/sum/tools/create-updates-with-updates-publisher#use-the-create-update-wizard). Mais contrairement à l’Assistant, vous avez la possibilité d’enregistrer vos ensembles de règles pour une utilisation ultérieure.

1. Dans l **’espace de travail Règles**, choisissez **Créer** pour ouvrir l’**Assistant Création d’une règle**.

2. Nommez la règle, puis cliquez sur ![Nouvelle règle](media/newrule.png). Cette opération ouvre la page **Règle de mise en application** dans laquelle vous pouvez configurer des règles.

3. Pour le **type de règle,** sélectionnez l’un des paramètres suivants. Les options que vous devez configurer varient pour chaque type :

   - **Fichier** : cette règle oblige un appareil à utiliser un fichier de propriétés correspondant à un ou plusieurs critères que vous spécifiez, avant de pouvoir appliquer cette mise à jour.

   - **Registre** : ce type permet de spécifier les détails de registre qui doivent être présents avant de pouvoir installer cette mise à jour sur un appareil.

   - **Système** : cette règle utilise les informations système pour déterminer les conditions de mise en application. Vous pouvez choisir entre la définition d’une version de Windows, une langue de Windows, l’architecture du processeur, ou spécifier une requête WMI qui identifie le système d’exploitation des appareils.

   - **Windows Installer** : utilisez ce type de règle pour déterminer les conditions de mise en application en fonction d’un correctif .MSI ou Windows Installer (.MSP) installé. Vous pouvez également déterminer si des composants ou des fonctionnalités spécifiques sont installés dans le cadre des exigences.

     > [!IMPORTANT]   
     > Sur les appareils gérés, l’Agent Windows Update ne peut pas détecter les packages Windows Installer installés par l’utilisateur. Lorsque vous utilisez ce type de règle, configurez des règles de mise en application supplémentaires, notamment les versions des fichiers ou les valeurs de clé de registre, de façon à détecter correctement le package Windows Installer, que ce soit par utilisateur ou par système.

   - **Règle enregistrée** : cette option vous permet de rechercher et d’utiliser les règles que vous avez précédemment configurées et enregistrées.

4. Continuez à ajouter et à configurer d’autres règles selon les besoins.

5. Utilisez les boutons d’opération logique pour réorganiser et regrouper différentes règles afin de mettre en place une vérification plus complexe des exigences.

6. Lorsque l’ensemble de règles est terminé, cliquez sur **OK** pour l’enregistrer. La règle maintenant apparaît dans la liste **Mes règles enregistrées**.

## <a name="edit-applicability-rule-sets"></a>Modifier des ensembles de règles de mise en application
Pour modifier une règle de mise en application, dans l **’espace de travail Règles**, sélectionnez une règle enregistrée dans la liste **Mes règles enregistrées**, puis choisissez **Modifier** dans le ruban. Cette opération ouvre l’Assistant **Modification d’une règle**.

L’Assistant **Modification d’une règle** affiche les règles actuelles de l’ensemble de règles. Vous modifiez des règles de la même façon que vous utilisez l’Assistant **Création d’une règle** pour créer de nouvelles règles. Vous pouvez utiliser cet Assistant pour renommer l’ensemble de règles, supprimer des règles, réorganiser des règles et des relations, ou ajouter de nouvelles règles.

Après avoir effectué vos modifications, choisissez **OK** pour enregistrer les modifications et fermer l’Assistant.

Pour plus d’informations sur l’utilisation de l’Assistant de règles, consultez l **’étape 7**, la page de mise en application, de l[’Assistant Création d’une mise à jour](/sccm/sum/tools/create-updates-with-updates-publisher#use-the-create-update-wizard).

## <a name="delete-applicability-rules"></a>Supprimer des règles de mise en application
Pour supprimer une règle de mise en application enregistrée, dans l **’espace de travail Règles**, sélectionnez la règle ou l’ensemble de règles dans la liste **Mes règles enregistrées**, puis choisissez **Supprimer** dans le ruban. Cette opération supprime la règle ou l’ensemble de règles enregistrés de l’éditeur de mise à jour.

Pour supprimer une règle d’une mise à jour spécifique, vous devez [modifier la mise à jour](/sccm/sum/tools/manage-updates-with-updates-publisher#edit-updates-and-bundles).
