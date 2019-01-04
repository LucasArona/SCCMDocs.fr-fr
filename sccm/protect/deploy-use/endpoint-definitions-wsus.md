---
title: Définitions de programmes malveillants Endpoint Protection à partir de WSUS
titleSuffix: Configuration Manager
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: aczechowski
description: Découvrez comment configurer Windows Server Update Services pour approuver automatiquement les mises à jour de définition.
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: b66c55da65f65c219b5c961949244f105885ba8f
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424271"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Activer le téléchargement des définitions de programmes malveillants pour Endpoint Protection à partir de Windows Server Update Services (WSUS) pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Si vous utilisez WSUS pour tenir à jour vos définitions de logiciels anti-programmes malveillants, vous pouvez le configurer pour approuver automatiquement les mises à jour de définition. Bien que l’utilisation des mises à jour logicielles Configuration Manager soit la méthode recommandée pour tenir à jour les définitions, vous pouvez aussi configurer WSUS en tant que méthode pour autoriser les utilisateurs à lancer manuellement des mises à jour de définitions. Utilisez les procédures suivantes pour configurer WSUS comme source de mise à jour de définition.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>Pour synchroniser les mises à jour de définitions Endpoint Protection dans les mises à jour logicielles Configuration Manager

1. Dans la console Configuration Manager, cliquez sur **Administration**.

2. Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.

3. Sélectionnez le site qui contient votre point de mise à jour logicielle. Dans le groupe **Paramètres** , cliquez sur **Configurer les composants de site**, puis cliquez sur **Point de mise à jour logicielle**.

4. Sous l’onglet **Classifications** de la boîte de dialogue **Propriétés du composant du point de mise à jour logicielle** , cochez la case **Mises à jour de définitions** .

5. Spécifiez les **Produits** mis à jour avec WSUS :

   -   Pour Windows 8.1 et les versions antérieures, sous l’onglet **Produits** de la boîte de dialogue **Propriétés du composant du point de mise à jour logicielle** , cochez la case **Forefront Endpoint Protection 2010** .

   -   Pour Windows 10 et les versions ultérieures, sous l’onglet **Produits** de la boîte de dialogue **Propriétés du composant du point de mise à jour logicielle**, cochez les cases **Windows Defender**.

6. Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés du composant du point de mise à jour logicielle** .

   Utilisez la procédure suivante pour configurer les mises à jour Endpoint Protection quand votre serveur WSUS n’est pas intégré à votre environnement Configuration Manager.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>Pour synchroniser les mises à jour de définition Endpoint Protection dans WSUS autonome

1.  Dans la console d’administration WSUS, développez **Ordinateurs**, cliquez sur **Options**, puis sur **Produits et classifications**.

2.  Spécifiez les **Produits** mis à jour avec WSUS :

    -   Pour Windows 8.1 et les versions antérieures, sous l’onglet **Produits** de la boîte de dialogue **Propriétés du composant du point de mise à jour logicielle** , cochez la case **Forefront Endpoint Protection 2010** .

    -   Pour Windows 10 et les versions ultérieures, sous l’onglet **Produits** de la boîte de dialogue **Propriétés du composant du point de mise à jour logicielle**, cochez les cases **Windows Defender**.

3.  Sous l’onglet **Classifications** de la boîte de dialogue **Produits et classifications** , cochez les cases **Mises à jour de définitions** et **Mises à jour** .

## <a name="approving-definition-updates"></a>Approbation des mises à jour de définition
 Les mises à jour de définitions Endpoint Protection doivent être approuvés et téléchargées sur le serveur WSUS avant d’être proposées aux clients qui demandent la liste des mises à jour disponibles. Les clients se connectent au serveur WSUS pour rechercher les mises à jour applicables, puis demandent les dernières mises à jour de définition approuvées.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>Pour approuver les définitions et les mises à jour dans WSUS

1. Dans la console d’administration WSUS, cliquez sur **Mises à jour**, puis sur **Toutes les mises à jour** ou sur la classification des mises à jour que vous voulez approuver.

2. Dans la liste des mises à jour, cliquez avec le bouton droit sur la ou les mises à jour dont vous voulez approuver l’installation, puis cliquez sur **Approuver**.

3. Dans la boîte de dialogue **Approuver les mises à jour** , sélectionnez le groupe d’ordinateurs pour lequel vous voulez approuver les mises à jour, puis cliquez sur **Approuvée pour l’installation**.

   Outre l’approbation manuelle, vous pouvez aussi définir une règle d’approbation automatique pour les mises à jour de définitions et les mises à jour Endpoint Protection. Cette opération configure WSUS de façon à approuver automatiquement les mises à jour de définitions Endpoint Protection téléchargées par WSUS.

### <a name="to-configure-an-automatic-approval-rule"></a>Pour configurer une règle d’approbation automatique

1.  Dans la console d’administration WSUS, cliquez sur **Options**, puis sur **Approbations automatiques**.

2.  Sous l’onglet **Règles de mise à jour** , cliquez sur **Nouvelle règle**.

3.  Dans le **ajouter une règle** boîte de dialogue **étape 1 : Sélectionnez les propriétés**, sélectionnez le **quand une mise à jour est dans une classification précise** case à cocher.

4.  Sous **étape 2 : Sous Étape 2 : Modifiez les propriétés**, cliquez sur **toutes les classifications**.

5.  Décochez toutes les cases sauf **Mises à jour de définitions**, puis cliquez sur **OK**.

6.  Dans le **ajouter une règle** boîte de dialogue **étape 1 : Sélectionnez les propriétés**, sélectionnez le **quand une mise à jour se trouve dans un produit spécifique** case à cocher.

7.  Sous **étape 2 : Sous Étape 2 : Modifiez les propriétés**, cliquez sur **tous les produits**.

8.  Décochez toutes les cases sauf **Forefront Endpoint Protection** pour Windows 8.1 et les versions antérieures, ou **Windows Defender** pour Windows 10 et les versions ultérieures, puis cliquez sur **OK**.

9. Sous **étape 3 : Sous Étape 3 : Indiquez un nom**, entrez un nom pour la règle, puis cliquez sur **OK**.

10. Dans la boîte de dialogue **Approbations automatiques** , cochez la case correspondant à la règle nouvellement créée, puis cliquez sur **Exécuter la règle**.

> [!NOTE]
>  Pour optimiser les performances sur votre serveur WSUS et sur les ordinateurs clients, refusez les anciennes mises à jour de définition. Pour ce faire, vous pouvez configurer l’approbation automatique des révisions et le refus automatique des mises à jour expirées. Pour plus d’informations, consultez [l’article 938947 de la Base de connaissances Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=204078).
> 
> [!div class="button"]
> [Étape suivante >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Retour >](endpoint-configure-alerts.md)
