---
title: Profils OneDrive Entreprise
titleSuffix: Configuration Manager
description: Redirigez les dossiers Windows connus vers OneDrive Entreprise à l’aide d’un profil OneDrive Entreprise dans Configuration Manager.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 22fcc8704651d75b4123e7942d14b861b3f6c099
ms.sourcegitcommit: d4b0e44e6bb06a830d0887493528d9166a15154b
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 04/11/2019
ms.locfileid: "59506305"
---
# <a name="onedrive-for-business-profiles"></a>Profils OneDrive Entreprise

À compter de Configuration Manager version 1902, vous pouvez créer des profils OneDrive Entreprise afin de déplacer les dossiers Windows connus vers OneDrive Entreprise. Ces dossiers sont les suivants : Bureau, Documents et Images. Dans chaque profil, vous pouvez spécifier les paramètres du déplacement des dossiers Windows connus. Pour plus d’informations sur OneDrive Entreprise, consultez [Rediriger et déplacer les dossiers Windows connus vers OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Prérequis

- [Rechercher votre ID de locataire Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id)  

- Déployez la version de client de synchronisation OneDrive 18.111.0603.0004 ou ultérieur. Pour plus d’informations, consultez [Déployer des applications OneDrive à l’aide de System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

## <a name="bkmk_odfb"></a> Déplacer les dossiers Windows connus vers OneDrive
<!--3556021-->
Utilisez Configuration Manager pour déplacer les dossiers Windows connus vers OneDrive Entreprise. Ces dossiers sont les suivants : Bureau, Documents et Images. Pour simplifier vos mises à niveau Windows 10, déployez ces paramètres sur les clients Windows 7 avant de déployer une séquence de tâches. 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis sélectionnez le nœud **Profils OneDrive Entreprise**.  

   ![Nœud de profils OneDrive Entreprise](media/onedrive-for-business-profiles-node.png)
2. Dans le ruban, sélectionnez **Créer un profil OneDrive Entreprise**.  

3. Spécifiez un nom pour identifier cette stratégie, puis sélectionnez **Suivant**.  

4. Sélectionnez les plateformes à approvisionner avec le profil OneDrive Entreprise. Lorsque vous avez fini de sélectionner les plateformes, cliquez sur **Suivant**.

    ![Sélectionner des plateformes pour le profil OneDrive Entreprise](media/onedrive-for-business-profile-select-platforms.png) 

5. Dans la page **Paramètres** :

    1. Spécifiez votre ID de locataire Office 365.  

    2. Sélectionnez l’une des options suivantes pour déplacer les dossiers connus vers OneDrive :  

        - **Inviter les utilisateurs à déplacer les dossiers connus Windows vers OneDrive** : avec cette option, l’utilisateur voit un Assistant permettant de déplacer ses fichiers. S’ils choisissent de reporter ou de refuser le déplacement de leurs dossiers, OneDrive le leur rappelle régulièrement.  

        - **Déplacer silencieusement les dossiers connus Windows vers OneDrive** : quand cette stratégie s’applique à l’appareil, le client OneDrive redirige automatiquement les dossiers connus vers OneDrive Entreprise.  

            - **Afficher une notification aux utilisateurs après la redirection des dossiers** : si vous activez cette option, le client OneDrive informe l’utilisateur une fois ses dossiers déplacés.  

    3. **Empêcher les utilisateurs de rediriger leurs dossiers connus Windows vers leur PC** : désactive l’option dans OneDrive Entreprise sur le client pour que les utilisateurs replacent ces dossiers sur l’appareil.  

       ![Paramètres de déplacement des dossiers connus de OneDrive Entreprise](media/onedrive-for-business-profile-move-folder-settings.png)

6. Effectuez l’Assistant, puis déployez la stratégie.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Déployer le profil OneDrive Entreprise

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis sélectionnez le nœud **Profils OneDrive Entreprise**.  


2. Sélectionnez le profil, puis choisissez **Déployer** dans le ruban.

3. Spécifiez les paramètres suivants pour votre déploiement :

   1. **Regroupement** : cliquez sur **Parcourir**, puis sélectionnez le regroupement dans lequel vous souhaitez déployer le profil.  
   1. **Générer une alerte** :

      - **Lorsque la conformité est inférieure à** : pourcentage minimal de conformité du client à maintenir avant qu’une alerte soit générée.
      -  **Date et heure** : les alertes de date sont d’abord générées selon la conformité du profil.
      - **Générer une alerte de System Center Operations Manager** : envoyer une alerte de conformité à System Center Operations Manager.
   1. **Calendrier** :

      - **Calendrier simple** : par défaut, ce paramètre utilise un calendrier simple pour lancer l’évaluation de la conformité tous les sept jours.
      - **Calendrier personnalisé** : définissez la date d’exécution de l’évaluation de conformité. L’heure de début est établie sur la base de l’heure locale de l’ordinateur qui exécute la console Configuration Manager au moment où vous créez le calendrier, mais vous pouvez utiliser l’heure universelle coordonnée (UTC).
 
      ![Déployer un profil OneDrive Entreprise](media/onedrive-for-business-deploy-profile.png)

4. Cliquez sur **OK** pour déployer le profil OneDrive Entreprise.


## <a name="next-steps"></a>Étapes suivantes

[Créer des profils de connexion à distance](/sccm/compliance/deploy-use/create-remote-connection-profiles)
