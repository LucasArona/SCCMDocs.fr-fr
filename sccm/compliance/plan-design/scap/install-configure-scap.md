---
title: Installer et configurer les Extensions SCAP (Security Content Automation Protocol)
titleSuffix: Configuraton Manager
description: Installer et configurer les Extensions SCAP (Security Content Automation Protocol)
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: f53b484b-5123-48f0-be2f-4e30318f3d39
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 891d21b44ed6efca73413a46d0483519b76f9cae
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-configure-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Installer et configurer les Extensions SCAP pour Microsoft System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Cette fonctionnalité a été introduite dans Technical Preview version 1803 sous la forme d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). Cette préversion des Extensions SCAP peut être installée sur toutes les versions actuellement prises en charge de Configuration Manager Current Branch et LTSB 1606. À compter de Technical Preview 1803, le fichier d’installation se trouve dans cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi.   

Une fois l’infrastructure requise préparée, vous êtes prêt à installer et à configurer les Extensions SCAP pour Microsoft System Center Configuration Manager sur l’ordinateur à partir duquel vous souhaitez exécuter ce processus.

## <a name="install-scap-extensions-configuration-manager"></a>Installer les Extensions SCAP pour Configuration Manager

1. Exécutez ConfigMgr\_Extensions\_for\_SCAP.msi pour installer l’outil.
2. Dans l’Explorateur Windows, accédez au dossier où vous avez téléchargé le fichier **ConfigMgr\_Extensions\_for\_SCAP.msi**, puis double-cliquez sur le fichier **ConfigMgr\_Extensions\_for\_SCAP.msi**. Cette opération démarre l’Assistant Installation des Extensions SCAP pour Microsoft System Center Configuration Manager.

Terminez l’**Assistant Installation des Extensions SCAP pour Microsoft System Center Configuration Manager** en vous appuyant sur les informations du tableau suivant et en acceptant les valeurs par défaut de l’Assistant, sauf si vous avez besoin de les spécifier.

**Table 1.0** Processus de l’Assistant Installation des Extensions SCAP pour Microsoft System Center Configuration Manager

| Nom de la page de l'Assistant | Action de l'utilisateur |
| --- | --- |
| Bienvenue et contrat de licence utilisateur final |1. Consultez le contrat de licence.|
| Bienvenue et contrat de licence utilisateur final|2. Cliquez sur **J’accepte les termes du contrat de licence**.|
| Bienvenue et contrat de licence utilisateur final|3. Cliquez sur **Suivant**.|
| Fin de l'Assistant Installation des Extensions SCAP pour Microsoft System Center Configuration Manager |4. Cliquez sur **Terminer**.|
 



L’Assistant Installation des Extensions SCAP pour Microsoft System Center Configuration Manager installe par défaut dans le dossier d’installation de la console Configuration Manager.



## <a name="download-and-install-the-scap-data-stream-files"></a>Télécharger et installer les fichiers de flux de données SCAP

Avant de pouvoir exécuter les Extensions SCAP pour convertir des fichiers de flux de données SCAP et les importer dans la fonctionnalité Paramètres de conformité, vous devez télécharger les fichiers de flux de données SCAP à partir du site web de la [page de téléchargement](http://nvd.nist.gov/fdcc/download_fdcc.cfm) National Vulnerability Database (NVD). Ensuite, copiez-les dans le dossier où vous avez installé les Extensions SCAP.

Selon votre environnement, vous n'aurez peut-être pas besoin de tous les fichiers de flux de données SCAP répertoriés dans la page de téléchargement.

Pour installer les flux de données SCAP

1. Accédez au [site web NVD](http://nvd.nist.gov/) pour identifier les flux de données SCAP nécessaires pour votre organisation.
Les flux de données SCAP publiés par le NIST sont organisés en plusieurs bundles, également appelés _listes de contrôle_.

2. Téléchargez les flux de données SCAP provenant du [site web NVD](http://nvd.nist.gov/home.cfm), qui sont stockés dans des fichiers compressés avec une extension de nom de fichier .zip ou marqués comme fichiers XML DataStream.

    >[!IMPORTANT] 
    >Il existe de nombreux fichiers de flux de données SCAP avec l'extension .xml téléchargeables à partir du site web NVD. Toutefois, seuls les fichiers .xml qui incluent du contenu XCCDF (SCAP1.0 et 1.1)/ DataStream (SCAP1.2) peuvent être utilisés avec les Extensions SCAP.

3. Extrayez les fichiers .zip/XML DataStream de flux de données que vous avez téléchargés dans le même dossier que celui où vous avez installé les Extensions SCAP.

## <a name="convert-and-import-the-scap-data-stream-files-using-the-import-scap-content-wizard"></a>Convertir et importer les fichiers de flux de données SCAP à l’aide de l’Assistant Importation du contenu SCAP

Une fois que vous avez obtenu les flux de données SCAP, vous êtes prêt à importer les flux de données et à les convertir en bases de référence de configuration. Les flux de données SCAP publiés par le NIST sont organisés en plusieurs lots. Suivez les instructions du NIST pour identifier les bundles à utiliser dans votre environnement. Par exemple, il existe un bundle distinct pour chaque version de Windows, un autre bundle spécifique à la version pour la configuration du pare-feu et un bundle pour Internet Explorer 8.0. Appliquez les procédures suivantes pour accomplir cette tâche.

### <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Pour importer les flux de données SCAP dans Configuration Manager

1. Démarrez l’Assistant Importation du contenu SCAP à partir du ruban de la base de référence de configuration.

     ![Démarrer l’Assistant Importation du contenu SCAP à partir du ruban de la base de référence de l’élément de configuration](./media/import-scap-content.png)

2. Sélectionnez Type de contenu.

      ![Sélectionner Type de contenu](./media/import-new-scap-content.png)

3. Sélectionnez le fichier de flux de données SCAP, le fichier XCCDF, ainsi que le fichier de dictionnaire CPE ou le fichier de contenu Oval.

     ![Sélectionner le fichier de flux de données SCAP](./media/select-datastream-file.png)

4. Si vous utilisez SCAP 1.2, sélectionnez le flux de données. Sélectionnez ensuite le point de référence et le profil pour SCAP 1.x.  Sélectionnez **Suivant** pour convertir le contenu. Une barre de progression s’affiche alors.

      ![Sélectionner le point de référence et le profil pour SCAP 1.2](./media/select-benchmark-and-profile.png)

5. Confirmez les données de configuration à importer.

      ![Capture d’écran de confirmation de la configuration](./media/confirm-configuration.png)

6. Cliquez sur**Suivant** pour importer les données de configuration.

      ![Terminer l’importation](./media/complete-import.png)

## <a name="alternate-method-convert-and-import-the-scap-data-stream-files-using-the-cmd-line-tool"></a>(Autre méthode) Convertir et importer les fichiers de flux de données SCAP à l’aide de l’outil en ligne de commande

Après avoir obtenu les flux de données SCAP, vous pouvez utiliser l’outil Microsoft.Sces.ScapToDcm.exe pour convertir les flux de données SCAP en fichiers .cab conformes aux paramètres de conformité. Importez ensuite les fichiers .cab dans Configuration Manager. L’outil Microsoft.Sces.ScapToDcm.exe convertit les flux de données SCAP en éléments de configuration et en bases de référence de configuration auxquels vous pouvez accéder à l’aide de la fonctionnalité Paramètres de conformité dans Configuration Manager. L’outil Microsoft.Sces.ScapToDcm.exe convertit les flux de données SCAP en manifestes XML. Il empaquète ensuite les manifestes XML dans un fichier .cab que vous pouvez importer dans Configuration Manager.

Les flux de données SCAP publiés par le NIST sont organisés en plusieurs lots. Suivez les instructions du NIST pour identifier les bundles à utiliser dans votre environnement. Par exemple, il existe un bundle distinct pour chaque version de Windows, un autre bundle spécifique à la version pour la configuration du pare-feu et un bundle pour Internet Explorer 8.0. Appliquez les procédures suivantes pour accomplir cette tâche.





## <a name="to-import-the-scap-data-streams-into-configuration-manager"></a>Pour importer les flux de données SCAP dans Configuration Manager

1. Convertissez les flux de données SCAP en fichier .cab conforme aux Paramètres de compatibilité.
2. Importez le fichier .cab dans Configuration Manager.

### <a name="convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files"></a>Convertir les flux de données SCAP en fichiers .cab conformes aux paramètres de conformité

Avant de pouvoir analyser et évaluer la compatibilité de vos systèmes, vous devez convertir les flux de données SCAP au format XML en manifestes XML conformes aux éléments de configuration et aux lignes de base de configuration des Paramètres de compatibilité. L’outil Microsoft.Sces.ScapToDcm.exe convertit les flux de données SCAP en manifestes XML. Il empaquète ensuite les manifestes XML dans un fichier .cab que vous pouvez importer ultérieurement dans Configuration Manager.

#### <a name="to-convert-the-scap-data-streams-into-compliance-settings-compliant-cab-files-using-the-microsoftscesscaptodcmexe-tool"></a>**Pour convertir les flux de données SCAP en fichiers .cab conformes aux paramètres de conformité à l’aide de l’outil Microsoft.Sces.ScapToDcm.exe**

À l’invite de commandes, accédez au dossier AdminConsole\Bin, exécutez Microsoft.Sces.ScapToDcm.exe pour générer un fichier cab conforme aux paramètres de conformité, puis importez-le dans le site Configuration Manager.

   >[!NOTE] 
   > Votre compte doit disposer d’autorisations en lecture/écriture pour le dossier de sortie

**Pour le contenu SCAP 1.0/1.1 (fichier XML XCCDF, tel que le contenu USGCB et DISA) :**

 Microsoft.Sces.ScapToDcm.exe –xccdf &lt;xccdf.xml&gt; -cpe &lt;cpe.xml&gt; -out &lt;outputFolder&gt; [-select benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   >Si vous ne spécifiez pas le point de référence/profil à l’aide du paramètre –select, l’outil génère un fichier cab DCM pour chaque point de référence dans le fichier de contenu.

**Pour le contenu SCAP1.2 (fichier XML DataStream, tel que le contenu USGCB le plus récent) :**

Microsoft.Sces.ScapToDcm.exe –scap &lt;scapdatastreamfile.xml&gt; -out &lt;outputFolder&gt; [-select datastream/benchmark/profile] [-log LogFileName]

   >[!NOTE] 
   > Si vous ne spécifiez pas le point de référence/profil/flux de données à l’aide du paramètre –select, l’outil génère un fichier cab DCM pour chaque point de référence dans le fichier de contenu.

**Pour un seul fichier OVAL avec des variables externes :**

Microsoft.Sces.ScapToDcm.exe –oval &lt;singleOvalFile.xml&gt; [-variable &lt;externalVariableFile.xml&gt;] -out &lt;outputFolder&gt; [-log LogFileName]

   >[!NOTE] 
   > S’il existe plusieurs valeurs pour une même variable dans le fichier de variable externe, l’outil Microsoft.Sces.ScapToDcm.exe traite les valeurs comme un tableau pour cette variable.



#### <a name="microsoftscesscaptodcmexe-command-line-parameters"></a>Microsoft.Sces.ScapToDcm.exe. Paramètres de ligne de commande

| **Paramètre** | **Utilisation** | **Obligatoire** |
| --- | --- | --- |
| -scap [fichier_de_flux_de_données_scap] | Spécifier le fichier de flux de données SCAP | Oui (pour le flux de données SCAP 1.2, s’exclut mutuellement avec –xccdf et –oval / -variable) |
| -xccdf [fichier_xccdf] | Spécifier le fichier XCCDF | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| -cpe [cpe file] | Spécifier le fichier CPE | Oui (pour SCAP 1.0/1.1 XCCDF, s’exclut mutuellement avec –scap et –oval / -variable) |
| -oval [fichier_oval] | Spécifier le fichier OVAL | Oui (pour le fichier OVAL autonome, s’exclut mutuellement avec –xccdf et -scap) |
| -variable [fichier_variable_externe_oval] | Spécifier le fichier de variable externe OVAL | Non (Facultatif pour le fichier OVAL autonome quand il existe un fichier de variable OVAL externe, s’exclut mutuellement avec –xccdf et –scap) |
| -select [xccdf benchmark/profile] | Sélectionner le point de référence XCCDF ou le profil à partir du flux de données SCAP ou du fichier XCCDF | Non (Nous vous suggérons de spécifier ce commutateur. Si vous ne le spécifiez pas, l'outil génère un fichier cab pour tous les profils dans tous les points de référence/DataStream incorporés) |
| -out [répertoire_sortie] | Spécifier où générer la sortie du fichier cab DCM | Non (si vous ne spécifiez pas ce paramètre, l’outil affiche uniquement le contenu sans conversion) |
| -log [fichier_journal] | Spécifier le fichier journal | Non (si vous ne spécifiez pas ce paramètre, le journal est écrit dans le fichier Microsoft.Sces.ScapToDcm.log) |
| -help / -? | Imprimer les instructions d’utilisation de l’outil | Non |





#### <a name="the-following-command-lines-are-samples-for-the-microsoftscesscaptodcmexe-tool"></a>Les lignes de commande suivantes sont des exemples de l’outil Microsoft.Sces.ScapToDcm.exe :

**SCAP1.2 Content:**

  Microsoft.Sces.ScapToDcm.exe –scap scap\_gov.nist\_USTCB-ie8.xml –out .\mytestfolder –select mySCAPDataStreamID/myBenchMarkID/myProfileID

**SCAP1.0/1.1 Content:**

   Microsoft.Sces.ScapToDcm.exe–xccdf scap\_gov.nist\_Test-WinXP\_xccdf.xml –cpe scap\_gov.nist\_Test-WinXP\_cpe.xml –out .\mytestfolder –select XCCDFBenchmarkID/MyProfileID

**SCAP OVAL Content:**

  Microsoft.Sces.ScapToDcm.exe –oval myOvalFile.xml –variable myOvalExternalVariableFile.xml –out .\mytestfolder

**La sortie suivante est un exemple de l’outil Microsoft.Sces.ScapToDcm.exe :**

  Compliance Settings compliant cab file created:

  Validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Successfully validate the schema of SCAP data stream file C:\24SCAP\BVT\_Test\_Data\_Stream.xml

  Process XCCDF Benchmark xccdf\_tst.bvt\_benchmark\_Windows-F

  Process XCCDF Profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0-BVT Profile #1

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-oval.xml

  Process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml

  Successfully finished process OVAL: scap\_tst.bvt\_comp\_Windows-F-cpe-oval.xml Process SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip SCAP Data Stream: [scap\_tst.bvt\_datastream\_Windows-F.zip]

  Version:        [1.2]

  Timestamp:      [2/24/2012]

  Use-case:       [CONFIGURATION]

  CPE Dictionary:  [scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml]

  OVAL:              [Windows-F-cpe-oval.xml] Product name:    [National Institute of Standards and Technology]

  Product version: []

  Schema version:  [5.3]

  Timestamp:       [2/24/2012]

  XCCDF Benchmark: [xccdf\_tst.bvt\_benchmark\_Windows-F]

  Version:       [v1.0.0.0] Update:        [http://usgcb.nist.gov]

  Timestamp:     [2/24/2012]

  Status:        [accepted]

  Status date:   [2/24/2012]

  Title:         [Ohh New BVT for SCAP 1.2]

 Description:   [My description]

  XCCDF Profile: [xccdf\_tst.bvt\_profile\_version\_1.0.0.0]
 
  OVAL:              [Windows-F-oval.xml]

   Product name:    [scaptool]

   Product version: []

   Schema version:  [5.4]

   Timestamp:       [2/24/2012]

  Start SCAP to DCM conversion...

  Processing SCAP data stream: scap\_tst.bvt\_datastream\_Windows-F.zip

  Processing CPE dictionary: scap\_tst.bvt\_comp\_Windows-F-cpe-dictionary.xml

  …

  Generating CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully generated CI baseline cab file: C:\28\bbt\xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

  Successfully converted XCCDF profile: xccdf\_tst.bvt\_profile\_version\_1.0.0.0 into DCM baseline xccdf\_tst.bvt\_benchmark\_Windows-F[xccdf\_tst.bvt\_profile\_version\_1.0.0.0].cab

## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Importer les paramètres de conformité SCAP et exporter les résultats de conformité](/sccm/compliance/plan-design/scap/import-scap-compliance-settings)
