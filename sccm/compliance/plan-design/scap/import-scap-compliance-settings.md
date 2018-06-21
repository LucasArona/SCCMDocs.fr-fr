---
title: Importer les paramètres de conformité SCAP
titleSuffix: Configuraton Manager
description: Importer les paramètres de conformité SCAP sous la forme de bases de référence de configuration et exporter les résultats
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 1f6b1fa0dd0775083eff9925a65509083b3f47d3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32336610"
---
# <a name="import-the-compliance-settings-compliant-cab-files-into-system-center-configuration-manager"></a>Importer les fichiers .cab conformes aux paramètres de conformité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Cette fonctionnalité a été introduite dans Technical Preview version 1803 sous la forme d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). Cette préversion des Extensions SCAP peut être installée sur toutes les versions actuellement prises en charge de Configuration Manager Current Branch et LTSB 1606. À compter de Technical Preview 1803, le fichier d’installation se trouve dans cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. 

L'étape suivante du processus consiste à utiliser la console Configuration Manager pour importer les fichiers .cab conformes aux Paramètres de compatibilité dans Configuration Manager. Lorsque vous importez les fichiers .cab que vous avez créé précédemment lors de ce processus, un ou plusieurs éléments de configuration et lignes de base de configuration sont créés dans la base de données de Configuration Manager. Plus loin dans le processus, vous pouvez affecter chacune des lignes de base de configuration à un regroupement d'ordinateurs dans Configuration Manager.

## <a name="to-import-the-compliance-settings-compliant-cab-files-into-configuration-manager"></a>Pour importer les fichiers .cab conformes aux Paramètres de compatibilité dans Configuration Manager

1. Ouvrez la **console Configuration Manager**.
2. Dans le volet de navigation de la  **console Configuration Manager, accédez à \*\* Ressources et Conformité**> **Paramètres de conformité** > **Bases de référence de configuration**.

3. Dans le volet Actions, cliquez sur **Importer des données de configuration** pour démarrer l’Assistant Importer des données de configuration.

1. Terminez l’**Assistant Importer des données de configuration** en vous appuyant sur les informations du tableau suivant et en acceptant les valeurs par défaut, sauf indication contraire.



Processus de l’Assistant Importer des données de configuration

| Nom de la page de l'Assistant | Action de l'utilisateur |
| --- | --- |
| **Choisir des fichiers** |1. Cliquez sur **Ajouter**. </br>La boîte de dialogue Ouvrir s'affiche.|
||2. Dans la boîte de dialogue **Ouvrir**, accédez au **&lt;dossier_\_sortie_cab_conforme&gt;**. Cliquez sur le fichier **&lt; compliant\_cab&gt;**.cab, où **dossier\_sortie**_cab_conforme est le dossier spécifié après le commutateur –output quand vous avez exécuté l’outil Sces.ScapToDcm.exe. **fichier\_conforme** est le nom d’un fichier .cab que vous avez créé plus tôt dans le processus. Cliquez ensuite sur **Ouvrir**. </br> La boîte de dialogue Console Configuration Manager –  Avertissement de sécurité s'affiche.|
||3. Dans la boîte de dialogue **Console Configuration Manager - Avertissement de sécurité**, cliquez sur **Exécuter**. Dans la page Choisir des fichiers, les données de configuration apparaissent dans la liste des lignes de base à importer.|
||3. Cliquez sur **Suivant**.|
| **Résumé** |5. Cliquez sur **Suivant**. |
| **Fin de l’Assistant Importer des données de configuration** |6. Cliquez sur **Fermer**. |

La nouvelle ligne de base de configuration apparaît dans le volet de détails de la console Configuration Manager.

>[!IMPORTANT]
> Vous devez répéter ce processus pour chaque fichier .cab que vous avez créé plus tôt dans le processus. Il existe un fichier .cab pour chaque profil sélectionné dans le fichier XML DataStream/XCCDF que vous avez téléchargé à partir du site web NVD, que vous pouvez traiter en exécutant l’outil Microsoft.Sces.ScapToDcm.exe.

La base de référence de configuration importée est en lecture seule, son État est « Activé » et son état Déployé initial est « Non ».  La propriété« Date de modification » indique l’heure à laquelle la base de référence de configuration a été importée.  Le nom de la base de référence de configuration provient de la section de nom d’affichage du fichier XML Datastream/XCCDF. Il est construit à l’aide de la convention suivante :

ABC[XYZ], où ABC désigne l’ID de point de référence XCCDF et XYZ désigne l’ID de profil XCCDF (si un profil est sélectionné).



## <a name="assign-configuration-baselines-to-the-computer-collections"></a>Affecter des bases de référence de configuration aux regroupements d’ordinateurs

Une fois que vous avez créé les regroupements d’ordinateurs appropriés pour les ordinateurs dont vous souhaitez évaluer la conformité SCAP, vous pouvez affecter les bases de référence de configuration que vous avez importées pour les associer aux regroupements d’ordinateurs. Cette section fournit les informations nécessaires pour affecter une ligne de base de configuration à un regroupement d'ordinateurs à l'aide de la console Configuration Manager.

Pour affecter une base de référence de configuration à un regroupement d’ordinateurs :

1. Ouvrez la **console** **Configuration Manager**.

2. Dans le volet de navigation de la **console Configuration Manager, accédez à **Ressources et Conformité** > **Paramètres de conformité** >** Bases de référence de configuration**.
3. Dans le volet de navigation, cliquez sur &lt; **base_référence\_configuration>, où &lt;_base_référence\_configuration&gt;_ est le nom de la base de référence de configuration que vous souhaitez affecter à un regroupement d’ordinateurs.

    La liste des éléments de configuration de la ligne de base de configuration apparaît dans le volet de détails de Configuration Manager.

4. Dans le volet d'actions, cliquez sur **Déployer**.

5. Remplissez la **boîte de dialogue** **Déployer** **Base de référence de configuration** en vous appuyant sur les informations du tableau suivant et en acceptant les valeurs par défaut, sauf indication contraire.

### <a name="deploy-configuration-baseline-dialog-process"></a>Processus de la boîte de dialogue Base de référence de configuration

| Nom de la page de l'Assistant | Action de l'utilisateur |
| --- | --- |
| **Choisir un regroupement** | 1. Cliquez sur **Parcourir**.|
||2. Dans la boîte de dialogue **Sélectionner un regroupement**, sélectionnez **Regroupements d’appareils**. Cliquez ensuite sur  **&lt;collection\_ordinateurs&gt;**, où &lt; _collection\_ordinateur&gt;_  est le nom du regroupement d’ordinateurs que vous avez créé plus tôt dans le processus. Cliquez sur **OK**.|
| **Définir le calendrier** |3. Sélectionnez le calendrier qui convient à votre organisation.|
 
>[!IMPORTANT]
> Répétez ce processus pour chaque regroupement d'ordinateurs que vous souhaitez affecter à chaque ligne de base de configuration. Au minimum, affectez chaque ligne de base de configuration à au moins un regroupement d'ordinateurs.

## <a name="verify-that-the-compliance-data-has-been-collected"></a>Vérifier que les données de conformité ont été collectées

Avant de réexporter les données de compatibilité au format SCAP, vous devez vérifier que les données ont été recueillies. Une fois que vous avez affecté une ligne de base de configuration à un regroupement d'ordinateurs, le client Configuration Manager sur chaque ordinateur du regroupement rassemble automatiquement les informations de compatibilité. Ensuite, les informations de compatibilité sont stockées dans la base de données de Configuration Manager.

Vous pouvez afficher l'état du déploiement de la ligne de base de configuration dans Configuration Manager pour vous assurer que les données appropriées ont été recueillies par les clients Configuration Manager. Il est important de vérifier que les données de conformité appropriées ont été collectées dans Configuration Manager, car cela peut vous aider à valider les fichiers de résultats XCCDF/DataStream que vous allez créer plus loin dans le processus.



### <a name="verify-that-the-compliance-data-has-been-collected"></a>Vérifier que les données de compatibilité ont été recueillies

1. Ouvrez la console Configuration Manager.
2. Dans le volet de navigation de la console Configuration Manager, accédez à **Surveillance** > **Déploiements**.
3. Cliquez sur le **Type de fonctionnalité** pour effectuer un tri selon le type de déploiement et rechercher les éléments dont le type est **Ligne de base** dans la liste.
4. Cliquez avec le bouton droit dans la liste sur la&lt;base_de_référence_de\_configuration&gt; que vous venez de déployer dans le regroupement, puis cliquez sur **Afficher l’état**.
5. Accédez ensuite au nœud &lt;base_de_référence_de\_configuration&gt; pour afficher l’état de compatibilité. Si un ordinateur est à l’état Inconnu, cela signifie que la collecte de données de conformité n’est pas encore terminée pour cet ordinateur.

### <a name="validate-the-xccdfdatastream-results"></a>Valider les résultats XCCDF/Datastream

1. Ouvrez la console Configuration Manager.
2. Dans le volet de navigation de la console Configuration Manager, accédez à **Paramètres de conformité** > **Tableau de bord SCAP**.
3. Sélectionnez les valeurs souhaitées pour Base de référence de configuration, Affectation, Fichier SCAP, Flux de données, Point de référence et Profil (le cas échéant).
4. Cliquez sur **Afficher le rapport**
 ![Rapport SCAP](./media/scap-report.png)



## <a name="export-compliance-results-to-scap-format"></a>Exporter les résultats de conformité au format SCAP

La tâche suivante du processus consiste à exporter les données de conformité des paramètres de conformité au format SCAP, qui est un fichier de rapport ARF au format XML/lisible par l’utilisateur. L’Assistant Exportation des Extensions SCAP et l’outil Microsoft.Sces.DcmToScap.exe exportent un fichier de résultats ARF XCCDF/DataStream distinct pour chaque base de référence de configuration des paramètres de conformité. Ces fichiers correspondent à chaque fichier d’entrée XCCDF/DataStream que l’outil Microsoft.Sces.ScapToDcm.exe utilise pour créer chaque base de référence de configuration des paramètres de conformité.

### <a name="export-the-compliance-settings-compliance-data-using-the-export-scap-report-wizard"></a>Exporter les données de conformité des paramètres de conformité à l’aide de l’Assistant Exporter des rapports SCAP

1. Démarrez l’Assistant Exporter des rapports SCAP à partir du menu contextuel du tableau de bord SCAP.
![Importer à partir du tableau de bord SCAP](./media/import-from-scap-dashboard.png)

2. Sélectionnez la base de référence de configuration et l’affectation ![Sélectionner une base de référence](./media/select-ci-baseline.png)

3. Choisissez l’emplacement du fichier de flux de données SCAP, du fichier XCCDF/CPE ou encore des fichiers de contenu Oval et de variables.
![Choisir un flux de données](./media/export-scap-report-datastream.png)

4. Spécifiez le nom d’organisation et choisissez l’emplacement du dossier où exporter le rapport SCAP.
 ![Choisir un flux de données](./media/specify-org-export.png)

5. Vérifiez les paramètres.
 ![Choisir un flux de données](./media/confirm-export.png)

6. Choisissez **Suivant pour exporter le rapport.  Une barre de progression s’affiche, puis une page Dernière étape.
 ![Terminer l’exportation](./media/complete-report-export.png)



### <a name="alternate-method-export-the-compliance-settings-compliance-data-using-the-microsoftscesdcmtoscapexe-tool"></a>(Autre méthode) Exporter les données de conformité des paramètres de conformité à l’aide de l’outil Microsoft.Sces.DcmToScap.exe

1. À l’invite de commandes, accédez au dossier AdminConsole\Bin, tapez les paramètres de ligne de commande répertoriés dans le tableau suivant, puis appuyez sur **Entrée :

    >[!NOTE] 
    >Votre compte doit disposer d’autorisations en lecture pour le fournisseur Configuration Manager, ainsi que d’autorisations en écriture pour le dossier de sortie spécifié dans le paramètre –out de la ligne de commande.

**Pour le contenu SCAP 1.0/1.1 (tel que le contenu USGCB et DISA) :**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt;  -select &lt;xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

  >[!NOTE] 
    >Vous devez utiliser le paramètre –select pour spécifier le point de référence/profil qui a été évalué sur les clients s’il existe plusieurs points de référence/profils dans le contenu.

**Pour le contenu SCAP1.2 (tel que le contenu USGCB le plus récent) :**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID  -select &lt;datastream/xccdfBenchmark/profile&gt; -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
   >Vous devez utiliser le paramètre –select pour spécifier le flux de données/point de référence/profil qui a été évalué sur les clients s’il existe plusieurs flux de données/points de référence/profils dans le contenu.

**Pour un seul fichier OVAL avec des variables externes :**

Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;]  -out &lt;outputResultFolder&gt;  [-log logFileName]

   >[!NOTE] 
    >L’outil Microsoft.Sces.DcmToScap.exe génère uniquement un rapport sur les résultats de définition OVAL pour chaque ordinateur cible. Il ne génère pas de rapport ARF.

#### <a name="how-to-get-baseline-ci-id-and-assignment-id"></a>Comment obtenir un ID d’élément de configuration de base de référence et un ID d’affectation

Dans la console d’administration, accédez à **Ressources et Conformité** > **Paramètres de conformité** > **Base de référence de configuration**. L’ID d’élément de configuration est l’ID d’élément de configuration de la base de référence de configuration.

![Obtenir l’ID d’élément de configuration et l’ID d’affectation](./media/get-to-baselines.png)

Sélectionnez la base de référence de configuration souhaitée, puis cliquez sur l’onglet Déploiements. Si l’ID d’affectation n’est pas visible, cliquez avec le bouton droit sur l’en-tête de colonne, puis cliquez sur l’ID d’affectation pour l’activer.
![Obtenir l’ID d’élément de configuration et l’ID d’affectation](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Paramètres de ligne de commande Microsoft.Sces.DcmToScap.exe

| **Paramètre** | **Utilisation** | **Obligatoire** |
| --- | --- | --- |
| -baseline [ID d’élément de configuration de base de référence] | Spécifier la base de référence de configuration | Oui |
| -assignment [ID d’affectation] | Spécifier le déploiement de la base de référence de configuration | Oui |
| -organization [nom_organisation] | Spécifier le nom de l'organisation, qui sera affiché dans le rapport. Vous pouvez utiliser le caractère « ; » pour spécifier un nom d’organisation sur plusieurs lignes. | Non |
| -type [thin/full/fullnosc] | Spécifiez le type de résultat OVAL : résultat allégé, résultat complet ou résultat complet sans les caractéristiques du système. | Non (si vous ne spécifiez pas ce paramètre, la valeur par défaut est full) |
| -scap [fichier_de_flux_de_données_scap] | Spécifier le fichier de flux de données SCAP | Oui (pour le flux de données SCAP 1.2, s’exclut mutuellement avec –xccdf et –oval / -variable) |
| -xccdf [fichier_xccdf] | Spécifier le fichier XCCDF | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| -cpe [cpe file] | Spécifier le fichier CPE | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| -oval [fichier_oval] | Spécifier le fichier OVAL | Oui (pour le fichier OVAL autonome, s’exclut mutuellement avec –xccdf et -scap) |
| -variable [fichier_variable_externe_oval] | Spécifier le fichier de variable externe OVAL | Non (Facultatif pour le fichier OVAL autonome quand il existe un fichier de variables OVAL externe, s’exclut mutuellement avec –xccdf et -scap) |
| -select [xccdf benchmark/profile] | Sélectionner le point de référence XCCDF ou le profil à partir du flux de données SCAP ou du fichier XCCDF | Oui (vous devez effectuer une sélection pour générer un rapport afin de pouvoir mettre en correspondance la base de référence DCM correspondante dans la base de données Configuration Manager) |
| -out [répertoire_sortie] | Spécifier l’emplacement où générer la sortie du fichier cab des paramètres de conformité | Non (si vous ne spécifiez pas ce paramètre, l’outil affiche uniquement le contenu sans conversion) |
| -log [fichier_journal] | Spécifier le fichier journal | Non (si vous ne spécifiez pas ce paramètre, le journal est écrit dans le fichier Microsoft.Sces.DcmToScap.log) |
| -help / -? | Imprimer les instructions d’utilisation de l’outil | Non |



 >[!TIP] 
 >Vous pouvez spécifier le paramètre –?, –h ou –help pour afficher la syntaxe de l’outil Microsoft.Sces.DcmToScap.exe et une liste des paramètres.

Par défaut, l’outil Microsoft.Sces.DcmToScap.exe accède à la base de données Configuration Manager à l’aide de vos informations d’identification. L’outil Microsoft.Sces.DcmToScap.exe exige au minimum un accès en lecture à la base de données Configuration Manager.

Après avoir vérifié que les fichiers de rapport **ARF** _ARF\_xxxx.xml_ et/ou de rapport **lisible par l’utilisateur** xxx.txt, de rapport **Cyberscope**LASR\_xxx.xml, de rapport **ConsumedOval** xx-oval-&lt;nom_ordinateur&gt;.xml, de rapport de **résultat de point de référence XCCDF** xccdf\_xxx.xml existent, sur la ligne de commande, tapez exit, puis appuyez sur **Entrée** pour quitter l’invite de commandes.

## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Résolution des problèmes](/sccm/compliance/plan-design/scap/troubleshooting-scap)
