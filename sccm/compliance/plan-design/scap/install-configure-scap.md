---
title: Installer et configurer des extensions SCAP
titleSuffix: Configuration Manager
description: Installez et configurez les extensions SCAP (Security Content Automation Protocol) pour Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4fd440905bb736dfbfac01de804373d29c9fbb59
ms.sourcegitcommit: 1826664216c61691292ea2a79e836b11e1e8a118
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39384612"
---
# <a name="install-and-configure-the-scap-extensions-for-configuration-manager"></a>Installer et configurer les extensions SCAP pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une fois [l’infrastructure préparée](/sccm/compliance/plan-design/scap/about-scap#bkmk_prepare), vous êtes prêt à installer et à configurer les extensions SCAP pour Configuration Manager sur l’ordinateur à partir duquel vous souhaitez exécuter ce processus.



## <a name="bkmk_install"></a> Installer les extensions SCAP

Le fichier d’installation se trouve à l’emplacement suivant dans le répertoire d’installation sur le serveur de site Configuration Manager :  
`cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi`

1. Copiez **ConfigMgrExtensionsforSCAP.msi** sur l’ordinateur doté de la console Configuration Manager où vous souhaitez exécuter ce processus.  

2. Dans l’Explorateur Windows, accédez au dossier où vous avez copié **ConfigMgrExtensionsforSCAP.msi**. Double-cliquez sur le fichier pour l’ouvrir et démarrer l’Assistant d’installation des extensions SCAP pour Configuration Manager.  

3. Consultez le contrat de licence. Cliquez sur **I accept the terms in the License Agreement** (J’accepte les termes du contrat de licence), puis cliquez sur **Install**.  

4. Une fois l’installation terminée, cliquez sur **Finish** (Terminer) pour fermer l’Assistant d’installation.  

L’Assistant d’installation installe les extensions SCAP dans le dossier d’installation de la console Configuration Manager. Par défaut, le dossier d’installation de la console est `C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole`.  



## <a name="bkmk_scap-data-stream-files"></a> Télécharger et installer les fichiers de flux de données SCAP

Avant de pouvoir exécuter les extensions SCAP, vous devez télécharger les fichiers de flux de données SCAP à partir de la [page de téléchargement](https://csrc.nist.gov/Projects/United-States-Government-Configuration-Baseline) NVD (National Vulnerability Database). Ensuite, copiez-les dans le dossier où vous avez installé les extensions SCAP.

Selon votre environnement, vous n'aurez peut-être pas besoin de tous les fichiers de flux de données SCAP répertoriés dans la page de téléchargement.

### <a name="install-the-scap-data-streams"></a>Installer les flux de données SCAP

1. Accédez au [site web NVD](http://nvd.nist.gov/) pour identifier les flux de données SCAP nécessaires pour votre organisation.
Les flux de données SCAP publiés par le NIST sont organisés en plusieurs bundles, également appelés _listes de contrôle_.  

2. Téléchargez les flux de données SCAP provenant du [site web NVD](http://nvd.nist.gov/home.cfm), qui sont stockés dans des fichiers compressés avec une extension de nom de fichier .zip ou marqués comme fichiers XML DataStream.  

    > [!IMPORTANT]  
    > Il existe de nombreux fichiers de flux de données SCAP avec l'extension .xml téléchargeables à partir du site web NVD. Toutefois, seuls les fichiers .xml qui incluent du contenu XCCDF (SCAP1.0 et 1.1)/ DataStream (SCAP1.2) peuvent être utilisés avec les extensions SCAP.  

3. Extrayez les fichiers .zip/XML DataStream de flux de données que vous avez téléchargés dans le même dossier que celui où vous avez installé les extensions SCAP.  



## <a name="bkmk_convert-and-import"></a> Convertir et importer manuellement les fichiers de flux de données SCAP 

Une fois que vous avez obtenu les flux de données SCAP, vous êtes prêt à importer les flux de données et à les convertir en bases de référence de configuration. Les flux de données SCAP publiés par le NIST sont organisés en plusieurs lots. Suivez les instructions du NIST pour identifier les lots à utiliser dans votre environnement. Par exemple, il existe un bundle distinct pour chaque version de Windows, un autre bundle spécifique à la version pour la configuration du pare-feu et un bundle pour Internet Explorer. Appliquez les procédures suivantes pour accomplir cette tâche.  

> [!Note]  
> Cette section explique comment manuellement convertir et importer les fichiers de flux de données avec la console Configuration Manager. Pour automatiser ce processus, consultez la section suivante [Convertir et importer automatiquement les fichiers de flux de données SCAP](#bkmk_auto-convert-and-import).  

1. Cliquez sur l’Assistant **Importation du contenu SCAP** dans le ruban à partir du groupe de bases de référence de configuration.

     ![Bouton Importer du contenu SCAP dans le ruban de la console](./media/import-scap-content.png)

2. Sélectionnez l’option de contenu SCAP.

      ![Page de l’Assistant d’importation permettant de sélectionner l’option de contenu SCAP](./media/import-new-scap-content.png)

3. Sélectionnez le fichier de flux de données SCAP, le fichier XCCDF, ainsi que le fichier de dictionnaire CPE ou le fichier de contenu Oval.

     ![Sélectionner le fichier de flux de données SCAP](./media/select-datastream-file.png)

4. Si vous utilisez SCAP 1.2, sélectionnez le flux de données. Sélectionnez ensuite le point de référence et le profil pour SCAP 1.x. Cliquez sur **Next** (Suivant) pour convertir le contenu. 

      ![Sélectionner le point de référence et le profil pour SCAP 1.2](./media/select-benchmark-and-profile.png)

      > [!Tip]  
      > Cette page de l’Assistant affiche la ligne de commande qui permet d’automatiser le même processus avec l’outil **ScapToDcm.exe**.  

5. Confirmez les données de configuration à importer.

      ![Capture d’écran de confirmation de la configuration](./media/confirm-configuration.png)

6. Cliquez sur **Next** (Suivant) pour importer les données de configuration.

      ![Terminer l’importation](./media/complete-import.png)



## <a name="bkmk_auto-convert-and-import"></a> Convertir et importer automatiquement les fichiers de flux de données SCAP 

### <a name="import-with-the-command-line-tool"></a>Importer avec l’outil en ligne de commande

Après avoir obtenu les flux de données SCAP, vous pouvez utiliser l’outil **Microsoft.Sces.ScapToDcm.exe** pour convertir les flux de données SCAP en fichiers .cab conformes aux paramètres de conformité. Importez ensuite les fichiers .cab dans Configuration Manager. L’outil Microsoft.Sces.ScapToDcm.exe convertit les flux de données SCAP en éléments de configuration et en bases de référence de configuration que vous pouvez utiliser dans Configuration Manager. L’outil Microsoft.Sces.ScapToDcm.exe convertit les flux de données SCAP en manifestes XML. Il empaquète ensuite les manifestes XML dans un fichier .cab que vous pouvez importer dans Configuration Manager.

> [!Tip]  
> L’étape 4 du processus manuel dans la section précédente montre la page de l’Assistant qui affiche la ligne de commande permettant d’automatiser le même processus avec l’outil **ScapToDcm.exe**.  


#### <a name="use-microsoftscesscaptodcmexe-to-convert-scap-data-streams-into-cab-files"></a>Utiliser Microsoft.Sces.ScapToDcm.exe pour convertir des flux de données SCAP en fichiers .cab

Depuis l’invite de commandes, accédez au dossier **AdminConsole\Bin**, puis exécutez **Microsoft.Sces.ScapToDcm.exe**. Cet outil génère un fichier .cab conforme aux paramètres de conformité et l’importe dans le site Configuration Manager.

   > [!NOTE]  
   > Votre compte doit disposer d’autorisations en lecture/écriture pour le dossier de sortie.

**Utilisation pour le contenu SCAP 1.0/1.1 (fichier XML XCCDF, tel que le contenu USGCB et DISA) :**  

`Microsoft.Sces.ScapToDcm.exe –xccdf <xccdf.xml> -cpe <cpe.xml> -out <outputFolder> [-select benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Si vous ne spécifiez pas le profil/point de référence à l’aide du paramètre `–select`, l’outil génère un fichier .cab pour chaque point de référence dans le fichier de contenu.  

**Utilisation pour le contenu SCAP1.1.2 (fichier XML DataStream, tel que le contenu USGCB le plus récent) :**  

`Microsoft.Sces.ScapToDcm.exe –scap <scapdatastreamfile.xml> -out <outputFolder> [-select datastream/benchmark/profile] [-log LogFileName]`  

   > [!NOTE]  
   > Si vous ne spécifiez pas le profil/point de référence/flux de données à l’aide du paramètre `–select`, l’outil génère un fichier .cab pour chaque point de référence dans le fichier de contenu.

**Utilisation pour un seul fichier OVAL avec des variables externes :**  

`Microsoft.Sces.ScapToDcm.exe –oval <singleOvalFile.xml> [-variable <externalVariableFile.xml>] -out <outputFolder> [-log LogFileName]`  

   > [!NOTE]  
   > S’il existe plusieurs valeurs pour une même variable dans le fichier de variable externe, l’outil Microsoft.Sces.ScapToDcm.exe traite les valeurs comme un tableau pour cette variable.  



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Paramètres de ligne de commande Microsoft.Sces.ScapToDcm.exe

| Paramètre | Utilisation | Obligatoire |
| --- | --- | --- |
| `-scap [scap data stream file]` | Spécifier le fichier de flux de données SCAP | Oui (pour le flux de données SCAP 1.2, s’exclut mutuellement avec –xccdf et –oval / -variable) |
| `-xccdf [xccdf file]` | Spécifier le fichier XCCDF | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| `-cpe [cpe file]` | Spécifier le fichier CPE | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| `-oval [oval file]` | Spécifier le fichier OVAL | Oui (pour le fichier OVAL autonome, s’exclut mutuellement avec –xccdf et -scap) |
| `-variable [oval external variable file]` | Spécifier le fichier de variable externe OVAL | Non (facultatif pour le fichier OVAL autonome quand il existe un fichier de variable OVAL externe, s’exclut mutuellement avec –xccdf et –scap) |
| `-select [xccdf benchmark/profile]` | Sélectionner le point de référence XCCDF ou le profil à partir du flux de données SCAP ou du fichier XCCDF | Non (ce paramètre n’est pas nécessaire mais recommandé. Si vous ne le spécifiez pas, l’outil génère un fichier cab pour tous les profils dans tous les points de référence/flux de données incorporés) |
| `-out [output directory]` | Spécifier où générer la sortie du fichier cab DCM | Non (si vous ne spécifiez pas ce paramètre, l’outil affiche uniquement le contenu sans conversion) |
| `-log [log file]` | Spécifier le fichier journal | Non (si vous ne spécifiez pas ce paramètre, le journal est écrit dans le fichier Microsoft.Sces.ScapToDcm.log) |
| `-help` ou `-?` | Imprimer les instructions d’utilisation de l’outil | Non |


#### <a name="microsoftscesscaptodcmexe-examples"></a>Exemples Microsoft.Sces.ScapToDcm.exe

**Contenu SCAP 1.2 :**  

`Microsoft.Sces.ScapToDcm.exe –scap scap_gov.nist_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID`  

**Contenu SCAP 1.0/1.1 :**  

`Microsoft.Sces.ScapToDcm.exe–xccdf scap_gov.nist_Test-WinXP_xccdf.xml –cpe scap_gov.nist_Test-WinXP_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID`  

**Contenu SCAP OVAL :**  

`Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder`  


#### <a name="sample-output-from-microsoftscesscaptodcmexe"></a>Exemple de sortie de Microsoft.Sces.ScapToDcm.exe

```
  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT_Test_Data_Stream.xml

  Process XCCDF Benchmark xccdf_tst.bvt_benchmark_Windows-F

  Process XCCDF Profile: xccdf_tst.bvt_profile_version_1.0.0.0-BVT Profile #1

  Process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-oval.xml

  Process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap_tst.bvt_comp_Windows-F-cpe-oval.xml
   Process SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip
    SCAP Data Stream: [scap_tst.bvt_datastream_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml]
  Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf_tst.bvt_benchmark_Windows-F]

  Version:       [v1.0.0.0]
   Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf_tst.bvt_profile_version_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap_tst.bvt_datastream_Windows-F.zip

  Processing CPE dictionary: scap_tst.bvt_comp_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf_tst.bvt_profile_version_1.0.0.0 into DCM baseline xccdf_tst.bvt_benchmark_Windows-F[xccdf_tst.bvt_profile_version_1.0.0.0].cab
```


### <a name="import-the-cab-file"></a>Importer le fichier .cab

L’étape suivante du processus consiste à utiliser la console Configuration Manager pour importer les fichiers .cab conformes aux paramètres de compatibilité dans Configuration Manager. Lorsque vous importez les fichiers .cab que vous avez créé précédemment lors de ce processus, un ou plusieurs éléments de configuration et lignes de base de configuration sont créés dans la base de données de Configuration Manager. Plus loin dans le processus, vous pouvez déployer les bases de référence de configuration sur des regroupements d’appareils. Pour plus d’informations, consultez [Importer des données de configuration](/sccm/compliance/deploy-use/import-configuration-data).

L’emplacement du fichier .cab que vous avez créé est le dossier spécifié par le paramètre `–output` de l’outil Microsoft.Sces.ScapToDcm.exe.

> [!IMPORTANT]  
> Répétez ce processus pour chaque fichier .cab que vous avez créé plus tôt dans le processus. Il existe un fichier .cab par profil sélectionné dans le fichier XCCDF/DataStreamXML que vous avez téléchargé à partir du site web NVD. Vous pouvez traiter ces fichiers en exécutant l’outil Microsoft.Sces.ScapToDcm.exe.  

La base de référence de configuration importée est en lecture seule, son état est *Enabled* (Activé) et son état déployé est *No*. La propriété **Date Modified** (Date de modification) indique l’heure à laquelle vous avez importé la base de référence. Le nom de la base de référence de configuration provient de la section de nom d’affichage du fichier XML Datastream/XCCDF. Le nom est construit selon la convention `ABC[XYZ]`, où **ABC** désigne l’ID de point de référence XCCDF et **XYZ** désigne l’ID de profil XCCDF (si un profil est sélectionné).



## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Déployer et surveiller la conformité SCAP et exporter les résultats de conformité](/sccm/compliance/plan-design/scap/deploy-monitor-export)
