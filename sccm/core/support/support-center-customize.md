---
title: Personnaliser le Centre d’aide et de support
titleSuffix: Configuration Manager
description: Personnalisez le fichier de configuration du Centre d’aide et de support.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b100daf91b8bb7c5d4dd5f041c57e7dc9dac390e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156778"
---
# <a name="customize-support-center"></a>Personnaliser le Centre d’aide et de support

*S’applique à : System Center Configuration Manager (Current Branch)*

L’outil [Centre d’aide et de support](/sccm/core/support/support-center) fournit un fichier de configuration que vous pouvez personnaliser. Par défaut, lorsque vous installez le Centre d’aide et de support, ce fichier figure à l’emplacement suivant : `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. Le fichier de configuration modifie le comportement du programme :

  - [Personnaliser la collecte des données](#bkmk_datacoll) : Modifie les ensembles de clés de Registre et les espaces de noms Windows Management Instrumentation inclus pendant la collecte de données  

  - [Personnaliser les groupes de journaux](#bkmk_loggroups) : Définis de nouveaux groupes de fichiers journaux à l’aide d’expressions régulières. Ajoutez également d’autres fichiers journaux aux groupes de journaux.  

  - [Collecter les fichiers journaux supplémentaires à l’aide de caractères génériques](#bkmk_wildcards) : Utiliser les recherches de caractères génériques pour collecter des fichiers journaux supplémentaires  

Pour apporter ces modifications, vous devez disposer d’autorisations administratives sur le client où vous avez installé le Centre d’aide et de support. Effectuez ces personnalisations à l’aide d’un éditeur de texte ou XML, tel que le Bloc-notes ou Visual Studio.

> [!Important]  
> Le fichier de configuration du Centre d’aide et de support est un fichier au format XML. Il est essentiel au fonctionnement du Centre d’aide et de support. Pour modifier ce fichier, vous devez être familiarisé avec le format XML et les expressions régulières.  

Avant de personnaliser le fichier de configuration du Centre d’aide et de support, enregistrez une sauvegarde de l’original. Cette sauvegarde vous permettra de récupérer les fonctionnalités d’origine du Centre d’aide et de support si vous faites des erreurs en modifiant le fichier. Si vous ne créez pas une sauvegarde et que le Centre d’aide et de support ne fonctionne pas correctement une fois que vous avez modifié le fichier de configuration, réinstallez le Centre d’aide et de support. Vous pouvez également copier un fichier de configuration à partir d’une autre installation du Centre d’aide et de support.



## <a name="bkmk_datacoll"></a> Personnaliser la collecte des données

Pour personnaliser la collecte de données sur le client, modifiez le fichier de configuration du Centre d’aide et de support à l’aide des éléments XML contenus dans l’élément `<dataCollectorSettings>`.


### <a name="wmi-data-collection"></a>Collecte des données WMI

L’élément `<CcmWmiDataCollector>` contient un élément `<collectionScopes>`. Utilisez cet élément pour modifier les espaces de noms WMI à partir desquels le Centre d’aide et de support collecte les données. Il contient également un élément `<ignoreScopes>`. Utilisez cet élément pour filtrer la collecte des données sur des parties des espaces de noms définies dans l’élément `<collectionScopes>`.  
    
#### <a name="example"></a>Exemple
Le fichier de configuration par défaut collecte des données à partir de l’espace de noms `root\ccm`. Il inclut ce chemin dans un élément `<add/>` dans `<collectionScopes>`. 

Il ignore également tout ce qui se trouve sous les chemins `\cimodels`, `\invagt`, `\events` et `\policy` pour cet espace de noms. Il inclut ces chemins dans les éléments `<add/>` contenus dans `<ignoreScopes>`.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Collecte des données de Registre

L’élément `<RegistryDataCollector>` contient un élément `<registryKeys>`. Utilisez cet élément pour modifier les clés et sous-clés du Registre que le Centre d’aide et de support collecte sous le chemin `HKEY_LOCAL_MACHINE`. Le Centre d’aide et de support ne prend pas en charge la collecte des données de Registre à partir d’autres chemins de Registre racines.

#### <a name="example"></a>Exemple
Pour collecter les clés de Registre pour les programmes standard installés sur l’appareil, ajoutez l’élément `<add/>` suivant dans l’élément `<registryKeys>` : `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="bkmk_loggroups"></a> Personnaliser les groupes de fichiers journaux

Pour personnaliser quels fichiers journaux le Centre d’aide et de support doit collecter, et comment il doit les présenter dans la liste **Groupes de journaux**, utilisez des éléments dans l’élément `<logGroups>`. Lorsque vous démarrez le Centre d’aide et de support, il analyse cette section du fichier de configuration. Il crée ensuite un groupe sur la liste **Groupes de journaux** pour chaque valeur d’attribut de clé unique figurant dans les éléments `<add/>` contenus dans l’élément `<logGroups>`.

  - **Groupe de journaux de composants** : L’élément `<componentLogGroup>` utilise un attribut de clé pour définir le nom du groupe de journaux qui apparaît dans la liste. Il utilise également un attribut de valeur qui contient une expression régulière (regex). Il utilise cette expression régulière pour collecter un ensemble de fichiers journaux associés.  

  - **Groupe de journaux statique :** L’élément `<staticLogGroup>` utilise un attribut de clé pour définir le nom du groupe de journaux qui apparaît dans la liste. Il utilise également un attribut de valeur qui définit un nom de fichier journal.  

Si la même valeur d’attribut de clé est utilisée dans un élément `<add/>` au sein de l’élément `<componentLogGroup>` et de l’élément `<staticLogGroup>`, le Centre d’aide et de support crée un groupe unique. Ce groupe inclut les fichiers journaux définis par les deux éléments qui utilisent la même clé.

#### <a name="example"></a>Exemple
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="bkmk_wildcards"></a> Collecte de fichiers journaux supplémentaires à l’aide de caractères génériques

Pour collecter des fichiers journaux supplémentaires, utilisez des caractères génériques dans le chemin ou le nom de fichier. Ces caractères génériques incluent des variables d’environnement à l’échelle du système, telles que `%WINDIR%`, mais excluent les variables d’environnement de portée utilisateur telles que `%USERPROFILE%`. Pour collecter des fichiers journaux supplémentaires à l'aide de cette recherche de fichiers journaux non récursive, utilisez un élément `<add/>` dans l'élément `<additionalLogFiles>`. 

Ces exemples montrent comment le Centre d’aide et de support utilise cette fonctionnalité dans le fichier de configuration par défaut.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Exemple 1 : Collecter tous les fichiers journaux de Windows Update dans le répertoire Windows
L’élément suivant collecte tous les fichiers nommés `WindowsUpdate.log` trouvés dans le répertoire Windows : 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Exemple 2 : Collecter tous les fichiers journaux figurant dans le répertoire des journaux Windows
L’élément suivant collecte tous les fichiers qui se terminent par `.log` dans le répertoire des journaux Windows : 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Exemple XML complet
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
