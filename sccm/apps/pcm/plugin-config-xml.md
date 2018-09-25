---
title: Fichier XML de configuration du plug-in
titleSuffix: Configuration Manager
description: Informations techniques de référence sur les éléments XML du plug-in Package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 863beac218dd493d75294686a00f9bda569fdfbb
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297209"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Informations techniques de référence sur la configuration XML du plug-in Package Conversion Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357861-->

Cet article décrit les éléments XML du fichier de configuration Configuration Manager (Microsoft.ConfigurationManagement.exe.config) qui contrôlent le fonctionnement du plug-in Package Configuration Manager. Pour plus d’informations sur l’utilisation de ce plug-in, consultez [Comment utiliser le plug-in Package Conversion Manager](/sccm/apps/pcm/how-to-use-plug-in).



## <a name="xml-configuration-elements"></a>Éléments du fichier de configuration XML

Le tableau suivant décrit les éléments XML du fichier de configuration Configuration Manager qui se rapportent au plug-in Package Configuration Manager.

|Élément  |Tapez  |Description  |
|---------|---------|---------|
|**PcmPlugIn**|Chaîne|Nom du script ou de l'exécutable à utiliser comme plug-in Package Conversion Manager.|
|**PcmPlugInTimeoutMilliseconds**|Entier|Durée d'attente maximale, en millisecondes, pour que le script ou l'exécutable du plug-in Package Conversion Manager termine le traitement d'un package.|
|**PcmPluginExitCode**|Entier|Code de sortie attendu du processus du plug-in. Cette valeur indique la réussite. Tous les autres codes sont considérés comme une erreur.|
|**ForceRequirementsExtraction**|Booléen|Autoriser la conversion automatique à utiliser les spécifications de regroupement associées à un package. Il doit être défini sur True uniquement quand vous utilisez un plug-in Package Conversion Manager conçu pour prendre des décisions concernant les spécifications à utiliser.|



## <a name="sample-configuration-xml"></a>Exemple de fichier XML de configuration

Cette section fournit un exemple d'éléments de configuration XML de Package Conversion Manager, dans le fichier de configuration de Configuration Manager, **Microsoft.ConfigurationManagement.exe.config**. Par défaut, ce fichier se trouve dans le chemin d’accès suivant :  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

Dans l’exemple, les éléments associés à Package Conversion Manager se trouvent à l’intérieur de l’élément suivant : `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

