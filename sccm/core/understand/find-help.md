---
title: Trouver de l’aide
titleSuffix: Configuration Manager
description: Trouvez des ressources pour obtenir plus d’informations sur Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 86810629-cf2a-43e8-86a2-847444119fc1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f9c4b9bdbd67e26962a4de3ff66643f071339795
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139474"
---
# <a name="find-help-for-using-configuration-manager"></a>Trouver de l’aide pour utiliser Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article contient les sections suivantes avec plusieurs ressources permettant de trouver de l’aide pour utiliser Configuration Manager :  

- [Documentation du produit](#bkmk_Info)  

- [Partage de commentaires sur le produit](#product-feedback)  

- [Suivre le blog de l’équipe Configuration Manager](#BKMK_ProductGroupBlog)  

- [Options de support et ressources de la communauté](#BKMK_SupportOptions)  

Pour obtenir de l’aide sur l’accessibilité du produit, consultez [Fonctionnalités d’accessibilité](/sccm/core/understand/accessibility-features).  



##  <a name="bkmk_Info"></a> Documentation du produit  

Pour accéder à la documentation la plus récente du produit, commencez à [l’index de la bibliothèque](https://docs.microsoft.com/sccm/).  

<a name="BKMK_SearchTips"></a>  

Pour des conseils sur la recherche, l’ajout de commentaires et plus d’informations sur l’utilisation de la documentation du produit, consultez [Comment utiliser la documentation](/sccm/core/understand/use-docs).  



<a name="product-feedback"></a>  

## <a name="BKMK_1806Feedback"></a> Commentaires sur le produit à partir de la version 1806

À compter de Configuration Manager version 1806, vous pouvez envoyer des commentaires sur le produit directement de la console. Si vous avez besoin de joindre des journaux, utilisez [Hub de commentaires](#BKMK_FeedbackHub). Voici les options dont vous disposez :<!--1357542-->

  - **Envoyer un sourire** : permet d’envoyer des commentaires sur ce qui vous plaît.
  - **Envoyer un smiley mécontent** : permet d’envoyer des commentaires sur ce qui ne vous plaît pas.
  - **Envoyer une suggestion** : vous amène sur le [site web UserVoice](https://configurationmanager.uservoice.com/) pour partager vos idées.

![Envoyer des commentaires dans Configuration Manager 1806](media/1806-send-a-smile.png)


### <a name="send-a-smile"></a>Envoyer un sourire

Pour envoyer des commentaires sur ce qui vous plaît, suivez les instructions ci-dessous : 
1. En haut à droite de la console, cliquez sur le smiley. 
2. Dans le menu déroulant, sélectionnez **Envoyer un sourire**.
3. Utilisez la zone de texte pour expliquer ce qui vous plaît. 
4. Choisissez si vous souhaitez partager votre adresse e-mail et une capture d’écran. 
5. Cliquez sur **Envoyer des commentaires**.
     - Si vous n’avez pas de connexion Internet, cliquez sur **Enregistrer** en bas. Suivez les instructions de la section [Envoyer les commentaires que vous avez enregistrés pour les soumettre plus tard](#BKMK_NoInternet) afin de les envoyer à Microsoft. 

![Envoyer des commentaires dans Configuration Manager 1806](media/1806-feedback-form.png)


### <a name="send-a-frown"></a>Envoyer un smiley mécontent

Pour envoyer des commentaires sur ce qui ne vous plaît pas, suivez les instructions ci-dessous :

1. En haut à droite de la console, cliquez sur le smiley. 
2. Dans le menu déroulant, sélectionnez **Envoyer un smiley mécontent**.
3. Utilisez la zone de texte pour expliquer ce qui ne vous plaît pas. 
4. Choisissez si vous souhaitez partager votre adresse e-mail et une capture d’écran. 
5. Cliquez sur **Envoyer des commentaires**.
     - Si vous n’avez pas de connexion Internet, cliquez sur **Enregistrer** en bas. Suivez les instructions de la section [Envoyer les commentaires que vous avez enregistrés pour les soumettre plus tard](#BKMK_NoInternet) afin de les envoyer à Microsoft.  


### <a name="information-sent-with-feedback"></a>Informations envoyées avec les commentaires
 
   - Informations sur la build du système d’exploitation
   - ID de hiérarchie de Configuration Manager
   - Informations sur la build du produit
   - Informations de langue
   - Identificateur de l’appareil 
       - HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SQMClient:MachineId


### <a name="BKMK_NoInternet"></a> Envoyer des commentaires que vous avez enregistrés pour les soumettre plus tard

1. Cliquez sur **Enregistrer** en bas de la fenêtre **Fournir des commentaires**. 
2. Enregistrez le fichier .zip. Si l’ordinateur local n’a pas accès à Internet, copiez le fichier dans un ordinateur connecté à Internet. 
3. Si nécessaire, copiez UploadOfflineFeedback.exe qui se trouve dans `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`
    - Pour plus d’informations sur le dossier cd.latest, consultez [Dossier CD.Latest](../servers/manage/the-cd.latest-folder.md).

4. Sur un ordinateur connecté à Internet, ouvrez une invite de commandes. 
5. Exécutez la commande suivante : `UploadOfflineFeedback.exe -f c:\folder\location_of.zip`
    
    - Éventuellement, vous pouvez ajouter les éléments suivants :
        -  `-t, --timeout` Délai d’expiration en secondes pour l’envoi des données. 0 correspond à illimité. La valeur par défaut est 30.
        - `-s --silent` Aucune journalisation dans la console (vous ne pouvez pas combiner avec--verbose)
        - `-v, --verbose` Journalisation détaillée en sortie dans la console (vous ne pouvez pas combiner avec--silent)
        - `--help` Affiche l’écran d’aide



##  <a name="BKMK_FeedbackHub"></a> Commentaires sur le produit pour les versions 1802 et antérieures

Signalez les éventuels défauts du produit à l’aide de [l’application Hub de commentaires](https://support.microsoft.com/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) intégrée à Windows 10. Quand vous **ajoutez de nouveaux commentaires**, veillez à sélectionner la catégorie **Enterprise Management**, puis choisissez parmi les sous-catégories suivantes :
 - Client de Configuration Manager
 - Console Configuration Manager
 - Déploiement de système d’exploitation Configuration Manager
 - Serveur Configuration Manager

Continuez à utiliser la [page UserVoice](https://configurationmanager.uservoice.com/) afin de voter pour de nouvelles idées de fonctionnalités dans Configuration Manager.


##  <a name="BKMK_ProductGroupBlog"></a> Blog de l’équipe Configuration Manager  

Les équipes techniques et partenaires de Configuration Manager utilisent le [blog Enterprise Mobility + Security](https://cloudblogs.microsoft.com/enterprisemobility/?product=system-center-configuration-manager) pour vous donner des informations techniques et d’autres informations sur Configuration Manager et les technologies associées. Les publications de ce blog complètent la documentation et le support du produit.  


##  <a name="BKMK_SupportOptions"></a> Options de support et ressources de la communauté  

Les liens suivants fournissent des informations sur les options de support et les ressources communautaires :  

-   [Support Microsoft](https://aka.ms/cmcbsupport)  

-   [Communauté de Configuration Manager : Guide de survie de System Center Configuration Manager (Current Branch)](https://social.technet.microsoft.com/wiki/contents/articles/33035.system-center-configuration-manager-current-branch-survival-guide.aspx )  

-   [Page Forums de Configuration Manager](https://social.technet.microsoft.com/Forums/en-US/home?category=ConfigMgrCB)  
    <!-- NOTE: the above URL requires "en-US" for the category to work -->
