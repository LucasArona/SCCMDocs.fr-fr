---
title: Gérer les clients Mac
titleSuffix: Configuration Manager
description: Tâches de maintenance pour les clients Mac de Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6c8eef0ad8164ce6545264e0a1c229a647383661
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56138923"
---
# <a name="maintain-mac-clients"></a>Gérer les clients Mac
*S’applique à : System Center Configuration Manager (Current Branch)*

Voici des procédures relatives à la désinstallation de clients Mac et au renouvellement de leurs certificats.

##  <a name="uninstalling-the-mac-client"></a>Désinstallation du client Mac  

1.  Sur un ordinateur Mac, ouvrez une fenêtre de terminal et accédez au dossier contenant **macclient.dmg**.  

2.  Accédez au dossier Outils, puis entrez la ligne de commande suivante :  

     **./CMUninstall -c**  

    > [!NOTE]  
    >  La propriété  **-c** demande au programme de désinstallation du client de supprimer aussi les fichier journaux et les journaux d’incidents du client. Nous recommandons d’utiliser cette propriété pour éviter toute confusion si vous réinstallez le client ultérieurement.  

3.  Si nécessaire, supprimez manuellement le certificat d’authentification de client que Configuration Manager utilisait, ou révoquez-le. CMUnistall ne supprime et ne révoque pas ce certificat.  

##  <a name="renewing-the-mac-client-certificate"></a>Renouvellement du certificat client Mac  
 Pour renouveler le certificat client Mac, utilisez une des méthodes suivantes :  

-   [Assistant Renouveler le certificat](#renew-certificate-wizard)  

-   [Renouveler le certificat manuellement](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Assistant Renouveler le certificat  

1. Configurez les valeurs suivantes comme *chaînes* dans le fichier ccmclient.plist qui contrôle l’ouverture de l’Assistant Renouvellement de certificat :  

   - **RenewalPeriod1** : spécifie, en secondes, la première période de renouvellement pendant laquelle les utilisateurs peuvent renouveler le certificat. La valeur par défaut correspond à 3 888 000 secondes (45 jours). Ne configurez pas de valeur inférieure à 300, sinon la période est rétablie à la valeur par défaut. 

   - **RenewalPeriod2** : spécifie, en secondes, la deuxième période de renouvellement pendant laquelle les utilisateurs peuvent renouveler le certificat. La valeur par défaut correspond à 259 200 secondes (3 jours). Si cette valeur est configurée sur une valeur supérieure ou égale à 300 secondes et inférieure ou égale à **RenewalPeriod1**, la valeur configurée est utilisée. Si **RenewalPeriod1** est supérieure à 3 jours, une valeur de 3 jours sera utilisée pour **RenewalPeriod2**.  Si **RenewalPeriod1** est inférieure à 3 jours, **RenewalPeriod2** est définie sur la même valeur que **RenewalPeriod1**.  

   - **RenewalReminderInterval1** : spécifie, en secondes, la fréquence à laquelle l’Assistant Renouveler le certificat sera affiché pour les utilisateurs lors de la première période de renouvellement. La valeur par défaut correspond à 86 400 secondes (1 jour). Si **RenewalReminderInterval1** est supérieur à 300 secondes et inférieur à la valeur configurée pour **RenewalPeriod1**, la valeur configurée sera utilisée. Dans le cas contraire, la valeur par défaut de 1 jour sera utilisée.  

   - **RenewalReminderInterval2** : spécifie, en secondes, la fréquence à laquelle l’Assistant Renouveler le certificat sera affiché pour les utilisateurs lors de la deuxième période de renouvellement. La valeur par défaut correspond à 28 800 secondes (8 heures). Si **RenewalReminderInterval2** est supérieure à 300 secondes, inférieure ou égale à **RenewalReminderInterval1** et inférieure ou égale à **RenewalPeriod2**, la valeur configurée sera utilisée. Sinon, une valeur de 8 heures sera utilisée.  

     **Exemple :** Si les valeurs sont laissées sur leurs valeurs par défaut, 45 jours avant l'expiration du certificat, l'Assistant s'ouvre toutes les 24 heures.  Dans les 3 jours de la date d'expiration du certificat, l'Assistant s'ouvre toutes les 8 heures.  

     **Exemple :** Utilisez la ligne de commande suivante, ou un script, pour définir la première période de renouvellement sur 20 jours.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Quand l’Assistant Renouveler le certificat s’ouvre, les champs **Nom d’utilisateur** et **Nom du serveur** sont en général déjà remplis et l’utilisateur peut simplement entrer qu’un mot de passe pour renouveler le certificat.  

   > [!NOTE]  
   >  Si l'Assistant ne s'ouvre pas ou si vous fermez l'Assistant par inadvertance, cliquez sur **Renouveler** sur la page des préférences **Configuration Manager** pour ouvrir l'Assistant.  

###  <a name="renew-certificate-manually"></a>Renouveler le certificat manuellement  
 La période de validité classique pour le certificat client Mac est de 1 an. Configuration Manager ne renouvelle pas automatiquement le certificat utilisateur demandé à l’inscription ; vous devez donc procéder comme suit pour renouveler manuellement le certificat.  

> [!IMPORTANT]  
>  Si le certificat a expiré, vous devez désinstaller, réinstaller et réinscrire le client Mac.  

 Cette procédure supprime l'ID SMS, qui est requis pour demander un nouveau certificat pour le même ordinateur Mac. Lorsque vous supprimez et remplacez l’ID SMS client, tout historique client stocké, tel que l’inventaire, est supprimé après la suppression du client de la console Configuration Manager.  

1.  Créez et remplissez un regroupement d’appareils pour les ordinateurs Mac qui doivent renouveler les certificats utilisateur.  

    > [!WARNING]  
    >  Configuration Manager ne surveille pas la période de validité du certificat qu’il inscrit pour les ordinateurs Mac. Vous devez surveiller cette validité indépendamment de Configuration Manager pour identifier les ordinateurs Mac à ajouter à ce regroupement.  

2.  Dans l'espace de travail **Ressources et compatibilité** , démarrez l' **Assistant Création d'élément de configuration**.  

3.  Sur la page **Général** , spécifiez informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type :Mac OS X**  

4.  Dans la page **Plateformes prises en charge**, vérifiez que toutes les versions de Mac OS X sont sélectionnées.  

5.  Dans la page **Paramètres**, choisissez **Nouveau**, puis dans la boîte de dialogue **Créer un paramètre**, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type de paramètre :Script**  

    -   **Type de données :Chaîne**  

6.  Dans la boîte de dialogue **Créer un paramètre**, sous **Script de découverte**, choisissez **Ajouter un script** pour spécifier un script de découverte des ordinateurs Mac configurés avec un SMSID configuré.  

7.  Dans la boîte de dialogue **Modifier un script de découverte** , entrez le script Shell suivant :  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Choisissez **OK** pour fermer la boîte de dialogue **Modifier un script de découverte**.  

9. Dans la boîte de dialogue **Créer un paramètre**, sous **Script de correction (facultatif)**, choisissez **Ajouter un script** pour spécifier un script de suppression du SMSID détecté sur les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un script de correction** , entrez le script Shell suivant :  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Choisissez **OK** pour fermer la boîte de dialogue **Créer un script de correction**.  

12. Sur la page **Règles de compatibilité** de l'Assistant, cliquez sur **Nouveau**, puis dans la boîte de dialogue **Créer une règle** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Paramètre sélectionné :** Choisissez **Parcourir**, puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    -   Dans **les valeurs suivantes** , entrez **la paire domaine/par défaut (com.microsoft.ccmclient, ID SMS) n'existe pas**.  

    -   Activez l'option **Exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant Création d'élément de configuration.  

14. Créez une ligne de base de configuration contenant l’élément de configuration que vous venez de créer et déployez-la sur le regroupement d’appareils créé à l’étape 1.  

     Pour plus d’informations sur la création et le déploiement de lignes de base de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md) et [Comment déployer des lignes de base de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour installer un nouveau certificat :  

    ```  
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Lorsque vous y êtes invité, fournissez le mot de passe du compte de superutilisateur qui exécute la commande, puis le mot de passe du compte d'utilisateur Active Directory.  

16. Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    a.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Dans la boîte de dialogue **Trousseau d’accès**, dans la zone **Trousseau**, choisissez **Système**, puis dans la zone **Catégorie**, choisissez **Clés**.  

    c.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    d.  Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    e.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    f.  Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

17. Redémarrez l'ordinateur Mac.  

