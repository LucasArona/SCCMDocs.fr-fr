---
title: Comment utiliser le plug-in de conversion
titleSuffix: Configuration Manager
description: Utilisez le plug-in Package Conversion Manager pour personnaliser les processus d’analyse et de conversion.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 83cf156c-36de-483f-a9e6-2e06158f3b20
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 9e670cb6afd7186d7dc248bedd6e2ce7d7746b02
ms.sourcegitcommit: 759098de944b8f7d5eedfc2bae2cb9a6ba15276f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43297173"
---
# <a name="how-to-use-the-package-conversion-manager-plug-in"></a>Comment utiliser le plug-in Package Conversion Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357861-->

Le plug-in Package Conversion Manager vous aide à personnaliser les processus d’analyse et de conversion. Pour utiliser le plug-in Package Conversion Manager, écrivez un fichier exécutable ou un script qui effectue des opérations personnalisées. Modifiez ensuite le fichier de configuration Microsoft.ConfigurationManagement.exe.config pour appeler le fichier exécutable ou script. Les langages les plus courants utilisés pour écrire le script sont VBScript et PowerShell.

Le plug-in Package Conversion Manager s’exécute une fois pour chaque package. Si vous analysez ou convertissez plusieurs packages à la fois, le plug-in Package Conversion Manager s’exécute chaque fois.

> [!NOTE]  
> Pour plus d’informations sur les éléments Package Conversion Manager dans le fichier de configuration Configuration Manager, consultez [Informations techniques de référence sur la configuration XML du plug-in Package Conversion Manager](/sccm/apps/pcm/plugin-config-xml).



## <a name="default-process"></a>Processus par défaut

Par défaut, Package Conversion Manager effectue les actions suivantes :

1.  Lire un package Configuration Manager.  

2.  Créer une application à partir du package et ajouter des attributs par défaut.  

3.  Analyser l'application et déterminer un état de préparation du package.  

4.  Effectuer l'une des actions suivantes, selon l'opération Package Conversion Manager :  

    - **Analyser** : afficher l’état de préparation du package dans la console Configuration Manager.  

    - **Convertir** : écrire l’application dans la base de données Configuration Manager.  


## <a name="plug-in-based-process"></a>Processus basé sur plug-in 

Lorsque vous utilisez le plug-in, Package Conversion Manager effectue les actions suivantes :

1.  Lire un package Configuration Manager.  

2.  Créer une application à partir du package et ajouter des attributs par défaut.  

3.  Convertir l’application au format XML. Enregistrer le fichier sur le disque.  

4.  Exécuter le script de plug-in pour modifier le XML de l’application. Pour plus d’informations, consultez [Informations techniques de référence sur la configuration XML du plug-in Package Conversion Manager](/sccm/apps/pcm/plugin-config-xml).  

5.  Convertir l’application XML en une application Configuration Manager.  

6.  Analyser l'application et déterminer l’état de préparation du package.  

7.  Effectuer l'une des actions suivantes, selon l'opération Package Conversion Manager :  

    - **Analyser** : afficher l’état de préparation du package dans la console Configuration Manager.  

    - **Convertir** : écrire l’application dans la base de données Configuration Manager.  



## <a name="see-also"></a>Voir aussi

[Informations techniques de référence sur la configuration XML du plug-in Package Conversion Manager](/sccm/apps/pcm/plugin-config-xml)
