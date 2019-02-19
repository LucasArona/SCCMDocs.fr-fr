---
title: Créer un média de capture
titleSuffix: Configuration Manager
description: Utilisez l’Assistant Création d’un média de séquence de tâches pour créer un média de capture dans Configuration Manager pour capturer une image de système d’exploitation à partir d’un ordinateur de référence.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: edf7d7d40e42535a600d127dc0692aee3d7dd857
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56142423"
---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>Créer un média de capture avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans Configuration Manager, un média de capture vous permet de capturer une image de système d’exploitation à partir d’un ordinateur de référence. Utilisez un média de capture dans le scénario suivant :  

-   [Créer une séquence de tâches pour capturer un système d’exploitation](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="BKMK_CreateCaptureMedia"></a> Comment créer un média de capture  
 Utilisez un média de capture pour capturer une image de système d'exploitation à partir d'un ordinateur de référence. Un média de capture contient l'image de démarrage qui démarre l'ordinateur de référence et la séquence de tâches qui capture l'image du système d'exploitation.

Vous créez des média de capture à l'aide de l'Assistant Création d'un média de séquence de tâches. Avant d'exécuter l'Assistant, assurez-vous que toutes les conditions suivantes sont remplies :  

|Tâche|Description|  
|----------|-----------------|  
|Image de démarrage|Prenez en considération les éléments suivants relatifs à l’image de démarrage que vous utiliserez dans la séquence de tâches pour capturer le système d’exploitation :<br /><br /> -   L’architecture de l’image de démarrage doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.<br />-   Vérifiez que l’image de démarrage contient les pilotes de stockage de masse et de réseau nécessaires à l’approvisionnement de l’ordinateur de destination.|  
|Distribuer tout le contenu associé à la séquence de tâches|Vous devez distribuer tout le contenu exigé par la séquence de tâches à au moins un point de distribution. Cela inclut l’image de démarrage, l’image du système d’exploitation et les autres fichiers associés. L'Assistant collecte les informations à partir du point de distribution lorsqu'il crée le média autonome. Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur ce point de distribution.  Pour plus d’informations, voir [Distribute content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute).|  
|Préparer le lecteur USB amovible|Pour un lecteur USB amovible :<br /><br /> Si vous envisagez d’utiliser un lecteur USB amovible, ce dernier doit être connecté à l’ordinateur sur lequel est exécuté l’Assistant et il doit être détectable par Windows en tant que périphérique amovible. L’Assistant écrit directement sur le lecteur USB quand il crée le média.|  
|Créer un dossier de sortie|Pour un ensemble de CD/DVD :<br /><br /> Avant d'exécuter l'Assistant Création d'un média de séquence de tâches afin de créer un média pour un ensemble de CD ou DVD, vous devez créer un dossier pour les fichiers de sortie créés par l'Assistant. Le média créé pour un ensemble de CD ou DVD est écrit sous forme de fichiers .iso directement dans le dossier.|  

 Pour créer un média de capture, procédez comme suit.  

#### <a name="to-create-capture-media"></a>Pour créer un support de capture  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4. Sur la page **Sélectionner le type de média** , sélectionnez **Média de capture**, puis cliquez sur **Suivant**.  

5. Dans la page **Type de média** , spécifiez si le média est un disque mémoire flash ou un ensemble de CD/DVD, puis cliquez pour configurer les éléments suivants :  

   - Si vous sélectionnez **Périphérique flash USB**, spécifiez le lecteur sur lequel stocker le contenu.  

   - Si vous sélectionnez **Ensemble CD/DVD**, spécifiez la capacité du média et le nom et le chemin d'accès des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Par exemple : **\\\nom_serveur\dossier\fichier_sortie.iso**  

      Si la capacité du média est insuffisante pour stocker l’ensemble du contenu, plusieurs fichiers sont créés et vous devez stocker le contenu sur plusieurs CD ou DVD. Quand plusieurs médias sont nécessaires, Configuration Manager ajoute un numéro de séquence au nom de chaque fichier de sortie qu’il crée. De plus, si vous déployez une application en même temps que le système d’exploitation et que cette application ne peut pas tenir sur un seul média, Configuration Manager stocke l’application sur plusieurs médias. Quand le média autonome est exécuté, Configuration Manager invite l’utilisateur à insérer le média suivant sur lequel l’application est stockée.  

     > [!IMPORTANT]  
     >  Si vous sélectionnez une image .iso existante, l'Assistant Média de séquence de tâches supprime cette image du lecteur ou du partage dès lors que vous passez à la page suivante de l'Assistant. L'image existante est supprimée même si vous annulez ensuite l'Assistant.  

     Cliquez sur **Suivant**.  

6. Sur la page **Image de démarrage** , spécifiez les informations suivantes et cliquez sur **Suivant**.  

   > [!IMPORTANT]  
   >  L'architecture de l'image de démarrage que vous spécifiez doit être adaptée à l'architecture de l'ordinateur de référence. Par exemple, un ordinateur de référence x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de référence x86 peut démarrer et exécuter uniquement une image de démarrage x86.  

   -   Dans la zone **Image de démarrage** , spécifiez l'image de démarrage pour démarrer l'ordinateur de référence.  

   -   Dans la zone **Point de distribution** , spécifiez le point de distribution où réside l'image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

       > [!NOTE]  
       >  Vous devez disposer de droits d'accès en lecture à la bibliothèque de contenu sur le point de distribution.  

7. Effectuez toutes les étapes de l'Assistant.  
