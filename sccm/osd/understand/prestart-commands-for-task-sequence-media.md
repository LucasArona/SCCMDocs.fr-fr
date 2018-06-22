---
title: Commandes de prédémarrage pour les médias de séquence de tâches
titleSuffix: Configuration Manager
description: Créez un script à utiliser avec la commande de prédémarrage, distribuez le contenu associé à la commande de prédémarrage et configurez la commande de prédémarrage dans le média.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ccc9f652-2953-4c38-8a90-c799484105ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc20195824af03a361cb38837a061b68e78d098a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348366"
---
# <a name="prestart-commands-for-task-sequence-media-in-system-center-configuration-manager"></a>Commandes de prédémarrage pour les médias de séquence de tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer une commande de prédémarrage dans System Center Configuration Manager à utiliser avec un média de démarrage, un média autonome et un média préparé. La commande de prédémarrage est un script ou un exécutable qui s'exécute avant la sélection de la séquence de tâches et qui peut interagir avec l'utilisateur dans Windows PE. La commande de prédémarrage peut demander des informations à l'utilisateur et les enregistrer dans l'environnement de la séquence de tâches, ou interroger une variable de séquence de tâches pour obtenir des informations. Au démarrage de l'ordinateur de destination, la ligne de commande est exécutée avant que la stratégie ne soit téléchargée auprès du point de gestion. Suivez les procédures ci-dessous pour créer un script qui sera utilisé avec la commande de prédémarrage, distribuer le contenu associé à la commande de prédémarrage et configurer la commande de prédémarrage dans le média.  

## <a name="create-a-script-file-to-use-for-the-prestart-command"></a>Créer un fichier de script à utiliser avec la commande de prédémarrage  
 Vous pouvez lire et écrire les variables de séquence de tâches à l’aide de l’objet COM Microsoft.SMS.TSEnvironment pendant l’exécution de la séquence de tâches. L'exemple suivant illustre un fichier de script Visual Basic qui interroge la variable de séquence de tâches _SMSTSLogPath afin d'obtenir l'emplacement actuel du fichier journal. Le script définit également une variable personnalisée.  

```  
dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")  
dim logPath  
' You can query the environment to get an existing variable.  
logPath = env("_SMSTSLogPath")  
' You can also set a variable in the OSD environment.  
env("MyCustomVariable") = "varname"  
```  

## <a name="create-a-package-for-the-script-file-and-distribute-the-content"></a>Créer un package pour le fichier de script et distribuer le contenu  
 Une fois que vous avez créé le script ou l'exécutable de la commande de prédémarrage, vous devez créer une source de package pour héberger les fichiers du script ou de l'exécutable, créer un package pour les fichiers (aucun programme n'est requis), puis distribuer le contenu auprès d'un point de distribution.  

 Pour plus d’informations sur la création d’un package, consultez [Packages et programmes](../../apps/deploy-use/packages-and-programs.md).  

 Pour plus d’informations sur la distribution du contenu, consultez [Distribuer du contenu](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).  

## <a name="configure-the-prestart-command-in-media"></a>Configurer la commande de prédémarrage dans le média  
 Vous pouvez configurer une commande de prédémarrage pour un média autonome, un média de démarrage ou un média préparé dans l'Assistant Création d'un média de séquence de tâches. Pour plus d’informations sur les types de médias, consultez [Créer un média de séquence de tâches](../deploy-use/create-task-sequence-media.md). Suivez la procédure ci-dessous pour créer une commande de prédémarrage dans le média.  

#### <a name="to-create-a-prestart-command-in-media"></a>Pour créer une commande de prédémarrage dans le média  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4.  Sur la page **Sélectionner le type de média** , sélectionnez **Média autonome**, **Média de démarrage**ou **Média préparé**, puis cliquez sur **Suivant**.  

5.  Accédez à la page **Personnalisation** de l'Assistant. Pour plus d’informations sur la configuration des autres pages de l’Assistant, consultez [Créer un média de séquence de tâches](../deploy-use/create-task-sequence-media.md).  

6.  Sur la page **Personnalisation** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Sélectionnez **Activer une commande de prédémarrage**.  

    -   Dans la zone de texte **Ligne de commande** , entrez le script ou l'exécutable créé pour la commande de prédémarrage.  

        > [!IMPORTANT]  
        >  Pour spécifier la commande de prédémarrage, exécutez **cmd /C <commande_prédémarrage\>**. Par exemple, si le nom du script de votre commande de prédémarrage est TSScript.vbs, entrez la ligne de commande **cmd /C TSScript.vbs** . **cmd /C** ouvre une nouvelle fenêtre d’interpréteur de commandes Windows et utilise la variable d’environnement Path pour trouver le script ou l’exécutable de la commande de prédémarrage. Vous pouvez également indiquer le chemin d'accès complet à la commande de prédémarrage, mais sachez que la lettre de lecteur peut varier d'un ordinateur à l'autre, selon la configuration des lecteurs.  

    -   Sélectionnez **Inclure les fichiers pour la commande de prédémarrage**.  

    -   Cliquez sur **Définir** pour sélectionner le package associé aux fichiers de la commande de prédémarrage.  

    -   Cliquez sur **Parcourir** pour sélectionner le point de distribution hébergeant le contenu de la commande de prédémarrage.  

7.  Effectuez toutes les étapes de l'Assistant.  
