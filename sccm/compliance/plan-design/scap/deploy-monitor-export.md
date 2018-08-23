---
title: Déployer et surveiller la conformité SCAP
titleSuffix: Configuration Manager
description: Déployez les paramètres de conformité SCAP sous la forme de bases de référence de configuration, surveillez la conformité et exportez les résultats.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 0bdcb018-bac2-4540-b786-6242bac73ff4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7b59b7414ad2095d053b1121ba936281559aa5e2
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39386000"
---
# <a name="deploy-and-monitor-scap-compliance-in-configuration-manager"></a>Déployer et surveiller la conformité SCAP dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois que vous avez [converti et importé](/sccm/compliance/plan-design/scap/install-configure-scap#bkmk_convert-and-import) les fichiers de flux de données SCAP, consultez les étapes suivantes :  

- [Déployer](#bkmk_deploy) les bases de référence de configuration sur des regroupements pour évaluer la conformité des appareils à SCAP  

- [Surveiller](#bkmk_monitor) les données de conformité retournées par les clients ciblés  

- [Exporter](#bkmk_export) les résultats de conformité au format SCAP  



## <a name="bkmk_deploy"></a> Déployer des bases de référence de configuration SCAP

Tout d’abord, créez les regroupements d’appareils pour les ordinateurs dont vous souhaitez évaluer la conformité à SCAP. Pour plus d’informations, consultez [Créer des regroupements](/sccm/core/clients/manage/collections/create-collections).  

Vous êtes maintenant prêt à déployer les bases de référence de configuration que vous avez importées sur ces regroupements d’appareils. Pour plus d’informations, consultez [Guide pratique pour déployer des bases de référence de configuration](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

> [!Tip]  
> Répétez ce processus pour chaque base de référence de configuration que vous souhaitez déployer sur chaque regroupement d’appareils. Au minimum, déployez chaque base de référence de configuration sur au moins un regroupement d’appareils.



## <a name="bkmk_monitor"></a> Surveiller les données de conformité SCAP 

Avant de réexporter les données de compatibilité au format SCAP, vous devez vérifier que le site a recueilli les données. Une fois que vous avez déployé une base de référence de configuration sur un regroupement d’appareils, le client Configuration Manager sur chaque ordinateur du regroupement rassemble automatiquement les informations de compatibilité. Ensuite, les informations de compatibilité sont stockées dans la base de données de Configuration Manager.

Affichez l’état du déploiement de la base de référence de configuration dans Configuration Manager pour vous assurer que les données appropriées ont été recueillies par les clients Configuration Manager. Il est important de vérifier que les données de conformité appropriées ont été collectées dans Configuration Manager, car cela peut vous aider à valider les fichiers de résultats XCCDF/DataStream que vous allez créer plus loin dans le processus.

Pour plus d’informations, consultez [Surveiller les paramètres de compatibilité](/sccm/compliance/deploy-use/monitor-compliance-settings).


### <a name="validate-the-xccdfdatastream-results"></a>Valider les résultats XCCDF/Datastream

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis sélectionnez le **tableau de bord SCAP**.  

2. Sélectionnez les valeurs souhaitées pour la base de référence de configuration, Attribution, Fichier SCAP, Flux de données, Point de référence et Profil (le cas échéant).  

3. Cliquez sur **Afficher le rapport**.
 ![Exemple de rapport SCAP](./media/scap-report.png)



## <a name="bkmk_export"></a> Exporter les résultats de conformité au format SCAP

L’étape suivante du processus consiste à exporter les données de conformité au format SCAP, qui est un fichier de rapport ARF au format XML/lisible. L’Assistant Exportation des Extensions SCAP et l’outil en ligne de commande Microsoft.Sces.DcmToScap.exe exportent un fichier de résultats ARF XCCDF/DataStream distinct pour chaque base de référence de configuration. Ces fichiers correspondent à chaque fichier d’entrée XCCDF/DataStream que l’outil Microsoft.Sces.ScapToDcm.exe utilise pour créer chaque base de référence de configuration.


### <a name="manually-export-with-the-console-wizard"></a>Exporter manuellement avec l’Assistant de la console

> [!Note]  
> Cette section explique comment exporter manuellement les résultats de conformité avec la console Configuration Manager. Pour automatiser ce processus, consultez la section suivante [Exporter automatiquement avec l’outil en ligne de commande](#bkmk_auto-export).  


1. Démarrez l’Assistant **Exporter des rapports SCAP** en cliquant avec le bouton droit sur le nœud **Tableau de bord SCAP**.  
![Démarrer l’Assistant Exporter des rapports SCAP à partir du tableau de bord SCAP](./media/import-from-scap-dashboard.png)

2. Sélectionnez la base de référence de configuration, l’attribution et le type de contenu SCAP.  
![Sélectionner une base de référence](./media/select-ci-baseline.png)

3. Choisissez l’emplacement du fichier de flux de données SCAP, du fichier XCCDF/CPE ou encore des fichiers de contenu Oval et de variables.  
![Choisir un flux de données](./media/export-scap-report-datastream.png)

4. Spécifiez le nom d’organisation et choisissez l’emplacement du dossier où exporter le rapport SCAP.  
 ![Choisir un flux de données](./media/specify-org-export.png)
   > [!Tip]  
   > Cette page de l’Assistant affiche la ligne de commande qui permet d’automatiser le même processus avec l’outil **DcmToScap.exe**.  

5. Vérifiez les paramètres.  
 ![Choisir un flux de données](./media/confirm-export.png)

6. Choisissez **Suivant** pour exporter le rapport. Effectuez toutes les étapes de l'Assistant.  
 ![Terminer l’exportation](./media/complete-report-export.png)


### <a name="bkmk_auto-export"></a> Exporter automatiquement avec l’outil en ligne de commande

Ouvrez l’invite de commandes et accédez au dossier **AdminConsole\Bin** de Configuration Manager. Utilisez un des exemples de ligne de commande suivants :  

> [!NOTE]  
> Votre compte doit disposer d’autorisations de lecture pour le fournisseur Configuration Manager. Vous devez également disposer d’autorisations d’écriture pour le dossier spécifié dans le paramètre `–out` de la ligne de commande.

**Pour le contenu SCAP 1.0/1.1 (tel que le contenu USGCB et DISA) :**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –xccdf <xccdf.xml> -cpe <cpe.xml>  -select <xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

  > [!NOTE]  
  > S’il existe plusieurs points de référence/profils dans le contenu, utilisez le paramètre `–select` pour spécifier le point de référence/profil qui a été évalué sur les clients.  

**Pour le contenu SCAP1.2 (tel que le contenu USGCB le plus récent) :**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID -select <datastream/xccdfBenchmark/profile> -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > S’il existe plusieurs points de référence/profils/flux de données dans le contenu, utilisez le paramètre `–select` pour spécifier le point de référence/profil/flux de données qui a été évalué sur les clients.  

**Pour un seul fichier OVAL avec des variables externes :**  

`Microsoft.Sces.DcmToScap.exe -baseline BaselineCIID -assignment AssignmentID –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputResultFolder> [-log logFileName]`  

   > [!NOTE]  
   > L’outil Microsoft.Sces.DcmToScap.exe génère uniquement un rapport sur les résultats de définition OVAL pour chaque machine cible. Le rapport ARF n’est pas généré.  


#### <a name="how-to-get-the-baselineciid-and-assignmentid"></a>Comment obtenir les identificateurs BaselineCIID et AssignmentID

Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis sélectionnez **Bases de référence de configuration**. `BaselineCIID` est l’identificateur (ID) de la base de référence de configuration.  
![Obtenir l’ID d’élément de configuration et l’ID d’affectation](./media/get-to-baselines.png)

Sélectionnez la base de référence de configuration souhaitée, puis cliquez sur l’onglet **Déploiements**. `AssignmentID` est l’identificateur (ID) du déploiement de la base de référence de configuration sur un regroupement d’appareils. Si l’ID d’attribution n’est pas affiché, cliquez avec le bouton droit sur l’en-tête de colonne, puis sélectionnez **ID de l’attribution**.  
![Obtenir l’ID d’élément de configuration et l’ID d’affectation](./media/get-to-baselines.png)


#### <a name="microsoftscesdcmtoscapexe-command-line-parameters"></a>Paramètres de ligne de commande Microsoft.Sces.DcmToScap.exe

| Paramètre | Utilisation | Obligatoire |
| --- | --- | --- |
| `-baseline [Baseline CI ID]` | Spécifier la base de référence de configuration | Oui |
| `-assignment [Assignment ID]` | Spécifier le déploiement de la base de référence de configuration | Oui |
| `-organization [organization name]` | Spécifier le nom de l'organisation, qui sera affiché dans le rapport. Vous pouvez utiliser le caractère `;` pour spécifier un nom d’organisation sur plusieurs lignes. | Non |
| `-type [thin/full/fullnosc]` | Spécifiez le type de résultat OVAL : résultat allégé, résultat complet ou résultat complet sans les caractéristiques du système. | Non (si vous ne spécifiez pas ce paramètre, la valeur par défaut est full) |
| `-scap [scap data stream file]` | Spécifier le fichier de flux de données SCAP | Oui (pour le flux de données SCAP 1.2, s’exclut mutuellement avec –xccdf et –oval / -variable) |
| `-xccdf [xccdf file]` | Spécifier le fichier XCCDF | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| `-cpe [cpe file]` | Spécifier le fichier CPE | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| `-oval [oval file]` | Spécifier le fichier OVAL | Oui (pour le fichier OVAL autonome, s’exclut mutuellement avec –xccdf et -scap) |
| `-variable [oval external variable file]` | Spécifier le fichier de variable externe OVAL | Non (facultatif pour le fichier OVAL autonome quand il existe un fichier de variable OVAL externe, s’exclut mutuellement avec –xccdf et –scap) |
| `-select [xccdf benchmark/profile]` | Sélectionner le point de référence XCCDF ou le profil à partir du flux de données SCAP ou du fichier XCCDF | Oui (vous devez effectuer une sélection pour générer un rapport afin de pouvoir mettre en correspondance la base de référence DCM correspondante dans la base de données Configuration Manager) |
| `-out [output directory]` | Spécifier l’emplacement où générer la sortie du fichier cab des paramètres de conformité | Non (si vous ne spécifiez pas ce paramètre, l’outil affiche uniquement le contenu sans conversion) |
| `-log [log file]` | Spécifier le fichier journal | Non (si vous ne spécifiez pas ce paramètre, le journal est écrit dans le fichier Microsoft.Sces.DcmToScap.log) |
| `-help` ou `-?` | Imprimer les instructions d’utilisation de l’outil | Non |

 > [!TIP]  
 > Vous pouvez spécifier le paramètre `-?`, `–h` ou `–help` pour afficher la syntaxe de l’outil Microsoft.Sces.DcmToScap.exe et une liste des paramètres.

Par défaut, l’outil Microsoft.Sces.DcmToScap.exe accède à la base de données Configuration Manager à l’aide de vos informations d’identification. L’outil Microsoft.Sces.DcmToScap.exe exige au minimum un accès en lecture à la base de données Configuration Manager.

Après avoir exécuté l’outil, vérifiez que les fichiers suivants existent : 
- Rapport **ARF** : `_ARF_xxxx.xml_` et/ou rapport **lisible**  : `xxx.txt`
- Rapport **Cyberscope** : `LASR_xxx.xml`
- Rapport **ConsumedOval** : `xx-oval-<machineName>.xml`
- Rapport **Résultat des points de référence XCCDF** : `xccdf_xxx.xml` 



## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Résolution des problèmes](/sccm/compliance/plan-design/scap/troubleshooting-scap)
