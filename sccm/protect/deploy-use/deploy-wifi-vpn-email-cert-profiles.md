---
title: Déployer des profils de certificat, de messagerie, VPN et Wi-Fi
titleSuffix: Configuration Manager
description: Découvrez comment déployer des profils de certificat, de messagerie, VPN et Wi-Fi dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: faf8d48614bc3e27381d57d86fc24da9356aa3f0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-profiles-in-system-center-configuration-manager"></a>Déployer des profils dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les profils doivent être déployés dans un ou plusieurs regroupements avant de pouvoir être utilisés.  

 Utilisez la boîte de dialogue **Déployer le profil Wi-Fi**, **Déployer le profil VPN**, **Déployer un profil Exchange ActiveSync** ou **Déployer le profil de certificat** pour configurer le déploiement de ces profils. Dans le cadre de la configuration, vous définissez le regroupement sur lequel le profil doit être déployé et spécifiez la fréquence à laquelle la conformité du profil est évaluée.  

> [!NOTE]  
>  Si vous déployez plusieurs profils d'accès aux ressources de l'entreprise pour le même utilisateur, le comportement suivant se produit :  
>   
>  -   Si un paramètre en conflit contient une valeur facultative, elle ne sera pas envoyée à l'appareil.  
> -   Si un paramètre en conflit contient une valeur obligatoire, la valeur par défaut est envoyée à l'appareil. S'il n'existe aucune valeur par défaut, le profil d'accès aux ressources de l'entreprise échoue. Par exemple, si vous déployez deux profils de messagerie pour le même utilisateur et que les valeurs spécifiées pour **Hôte Exchange ActiveSync** ou **Adresse de messagerie** sont différents, les deux profils de messagerie échouent car il s'agit de paramètres obligatoires.  

> -   Pour déployer des profils de certificat, vous devez d'abord configurer l'infrastructure et créer des profils de certificat. Pour plus d'informations, consultez les rubriques suivantes :  
>   
>  -   [Configuration d’une infrastructure de certificats dans System Center Configuration Manager](certificate-infrastructure.md)  
> -   [Guide pratique pour créer des profils de certificat dans System Center Configuration Manager](create-certificate-profiles.md)    

> [!IMPORTANT]  
>  Quand un déploiement de profil VPN est supprimé, il n’est pas supprimé des appareils clients. Si vous souhaitez supprimer le profil des appareils, vous devez le supprimer manuellement.
>   

## <a name="deploying--profiles"></a>Déploiement de profils  


1.  Dans la console System Center Configuration Manager, choisissez **Ressources et Conformité**.  

2.  Dans l’espace de travail **Ressources et Conformité**, développez **Paramètres de compatibilité** et **Accès aux ressources de l’entreprise**, puis choisissez le type de profil approprié, tel que **Profils Wi-Fi**.  

3.  Dans la liste des profils, sélectionnez le profil que vous souhaitez déployer, puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Déployer**.  

4.  Dans la boîte de dialogue de déploiement de profil, spécifiez les informations suivantes :  

    -   **Regroupement**: cliquez sur **Parcourir** pour sélectionner le regroupement dans lequel vous souhaitez déployer le profil.  

    -   **Générer une alerte** : activez cette option pour configurer une alerte qui est générée si la conformité du profil est inférieure à un pourcentage spécifié à une date et une heure spécifiques. Vous pouvez également spécifier si vous souhaitez qu'une alerte soit envoyée à System Center Operations Manager.  

    -   -   **Délai aléatoire (heure)**  : (uniquement pour les profils de certificat contenant des paramètres de protocole d’inscription de certificats simple) spécifie un délai pour éviter un traitement excessif sur le service d’inscription de périphérique réseau. La valeur par défaut est **64** heures.  

    -   **Spécifier le calendrier d’évaluation de la compatibilité pour ce profil <type>**  : spécifie le calendrier par rapport auquel le profil déployé est évalué sur les ordinateurs clients. Il peut s'agir d'un calendrier simple ou d'un calendrier personnalisé.  

        > [!NOTE]  
        >  Lorsque l'utilisateur ouvre une session, le profil est évalué par les ordinateurs clients.  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue et pour créer le déploiement.

### <a name="see-also"></a>Voir aussi  

[Guide pratique pour surveiller les profils de messagerie, VPN et Wi-Fi dans System Center Configuration Manager](monitor-wifi-email-vpn-profiles.md)

[Guide pratique pour surveiller les profils de certificat dans System Center Configuration Manager](monitor-certificate-profiles.md)
