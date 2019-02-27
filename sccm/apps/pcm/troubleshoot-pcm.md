---
title: Dépanner Package Conversion Manager
titleSuffix: Configuration Manager
description: En savoir plus sur la résolution des problèmes avec Package Conversion Manager dans Configuration Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: e586990d049119c3cb00a61c56a1b84763104309
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137896"
---
# <a name="troubleshoot-package-conversion-manager"></a>Dépanner Package Conversion Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357861-->

Utilisez les informations de cet article pour vous aider à résoudre les problèmes liés à l'utilisation de Conversion Manager.



## <a name="sms-provider"></a>Fournisseur SMS

Package Conversion Manager utilise le fournisseur SMS. Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).

Si le fournisseur SMS ne fonctionne pas correctement, la console Configuration Manager, y compris Package Console Configuration Manager, ne fonctionne pas.



## <a name="package-readiness"></a>Préparation du package

Avant de convertir un package en application, le package doit être analysé à l’aide de la fonction  **Analyser** de Package Conversion Manager. Après l’analyse, ajoutez la colonne **Préparation** au nœud **Packages** de la console Configuration Manager. La liste des packages affiche un des états de préparation suivants pour le package analysé :

 - **Automatique** : Le package peut être directement converti à l’aide de la fonction **Convertir**.      

    > [!NOTE]  
    > Une conversion automatique ne convertit pas les requêtes WQL en spécifications de l'application. Utilisez le processus **Corriger et convertir** pour convertir ces requêtes.  

 - **Manuel** : Le package nécessite quelques ajouts ou modifications avant de pouvoir être converti à l’aide de la fonction **Corriger et convertir**.  

 - **Non applicable** : Le package ne peut pas être converti. Corrigez les éventuels problèmes liés au package ou continuez à le déployer en tant que package.  

 - **Erreur** : Le package contient des erreurs. Corrigez manuellement ces erreurs avant l’analyser et de convertir ce package.  

Le volet des détails du nœud **Packages** dans la console Configuration Manager affiche les éventuels problèmes de préparation. Sélectionnez un package, puis sélectionnez l’onglet **Résumé** dans le volet des détails.



## <a name="log-files"></a>Fichiers journaux

### <a name="enable-logging"></a>Activer la journalisation

Lorsque vous activez la journalisation pour Package Conversion Manager, cette opération consigne toutes ses actions, exceptions et erreurs. 

Pour activer la journalisation pour ce composant dans Configuration Manager, modifiez le fichier **Microsoft.ConfigurationManagement.exe.Config**. Par défaut, ce fichier de configuration se trouve à l’emplacement suivant :  
`C:\Program Files (x86)\Microsoft Configuration Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

Insérez les éléments XML **switches** et **trace** suivants dans l’élément **system.diagnostics** après le dernier élément **sources** :

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

Cet exemple utilise le fichier **PCMTrace.log**. Ce fichier journal se trouve sur l’ordinateur exécutant la console Configuration Manager, dans le chemin d'accès suivant :  
`%UserProfile%\AppData\Local\Temp`

Pour configurer le niveau de détail, modifiez le paramètre de commutateur de suivi **PcmLogging**. Définissez cette valeur sur quatre niveaux de détail, du moins détaillé (`1`) au plus détaillé (`4`).


### <a name="smsprovlog"></a>SMSProv.log

Dans certains cas, les informations relatives au dépannage du processus de conversion de package se trouvent dans le fichier **SMSProv.log**. Ce fichier capture les informations provenant du fournisseur SMS de Configuration Manager.

Par défaut, ce fichier journal se trouve sur le serveur de site Configuration Manager, à l’emplacement suivant :  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Si l’un des messages d’erreur suivants s’affiche, le fichier **SMSProv.log** peut contenir des informations de dépannage :

- `The SMS Provider reported an error`

- `Generic Failure`

Ces messages d’erreur indiquent généralement qu'une erreur s'est produite sur le serveur de site et que les informations concernant l'erreur n'ont pas été envoyées à la console Configuration Manager.

Pour plus d'informations, voir [Technical Reference for Package Conversion Manager Error Messages](/sccm/apps/pcm/error-messages).



## <a name="changing-package-attributes-after-analysis"></a>Modification des attributs de package après l'analyse

Une fois qu'un package est analysé et reçoit un état de préparation avec la valeur **Automatique** ou **Manuel**, le processus de conversion peut échouer si l'un des attributs correspondants est modifié.

Par exemple, vous analysez un package et son état de préparation indique **Automatique**. Puis vous ajoutez un autre programme au package. La conversion du package risque d’échouer.

Si vous avez besoin d’apporter des modifications à un package après l’analyse, relancez l’analyse avant la conversion. 



## <a name="see-also"></a>Voir aussi

[Informations techniques de référence sur les messages d'erreur de Package Conversion Manager](/sccm/apps/pcm/error-messages)
