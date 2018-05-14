---
title: Déployer des clients Mac
titleSuffix: Configuration Manager
description: Découvrez comment déployer des clients sur des ordinateurs Mac dans System Center Configuration Manager.
ms.date: 05/04/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 01e53b80b47b3c1452cd73e408af48bc0283d60b
ms.sourcegitcommit: 526ded222b69b5e75e8068ba09c5dda227c155c4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique décrit comment déployer et gérer le client Configuration Manager sur des ordinateurs Mac. Pour en savoir plus sur les éléments à configurer avant de déployer les clients sur des ordinateurs Mac, consultez [Préparer le déploiement du logiciel client pour ordinateurs Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quand vous installez un nouveau client pour les ordinateurs Mac, vous devez peut-être également installer des mises à jour Configuration Manager pour refléter les nouvelles informations client dans la console Configuration Manager.

Dans ces procédures, vous avez deux options pour l’installation des certificats clients. En savoir plus sur les certificats clients pour Mac dans [Préparer le déploiement du logiciel client pour ordinateurs Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

-   Utilisez l’inscription Configuration Manager à l’aide de l’[outil CMEnroll](#install-the-client-and-then-enroll-the-client-certificate-on-the-mac). Le processus d'inscription ne prenant pas en charge le renouvellement automatique de certificats, vous devez réinscrire les ordinateurs Mac avant l'expiration du certificat installé.    

-   [Utilisez une demande de certificat et une méthode d’installation indépendantes de Configuration Manager](#use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager). 

>[!IMPORTANT]
>  Pour déployer le client sur des appareils macOS Sierra, vous devez configurer correctement le nom du sujet du certificat de point de gestion, par exemple en utilisant le nom de domaine complet du serveur de point de gestion.


## <a name="configure-client-settings-for-enrollment"></a>Configurer les paramètres client pour l’inscription  
 Vous devez utiliser les [paramètres client par défaut](../../../core/clients/deploy/about-client-settings.md) pour configurer l’inscription pour les ordinateurs Mac ; vous ne pouvez pas utiliser de paramètres client personnalisés.  

 Cela est nécessaire pour permettre à Configuration Manager de demander et d’installer le certificat sur l’ordinateur Mac.  

### <a name="to-configure-the-default-client-settings-for-configuration-manager-to-enroll-certificates-for-macs"></a>Pour configurer les paramètres client par défaut pour permettre à Configuration Manager d’inscrire des certificats pour les ordinateurs Mac  

1.  Dans la console Configuration Manager, choisissez **Administration** >  **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Sélectionnez la section **Inscription**, puis configurez ces paramètres :  

    1.  **Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac : Oui**  

    2.  **Profil d’inscription :** choisissez **Définir un profil**.  

6.  Dans la boîte de dialogue **Profil d’inscription d’appareil mobile**, choisissez **Créer**.  

7.  Dans la boîte de dialogue **Créer un profil d'inscription** , entrez un nom pour ce profil d'inscription, puis configurez le **Code du site de gestion**. Sélectionnez le site principal Configuration Manager contenant les points de gestion qui géreront les ordinateurs Mac.  

    > [!NOTE]  
    >  Si vous ne pouvez pas sélectionner le site, vérifiez qu'au moins un point de gestion dans le site est configuré pour la prise en charge des appareils mobiles.  

8.  Choisissez **Ajouter**.  

9. Dans la boîte de dialogue **Ajouter une autorité de certification pour les appareils mobiles**, sélectionnez le serveur de l’autorité de certification émettrice des certificats pour les ordinateurs Mac.  

10. Dans la boîte de dialogue **Créer un profil d’inscription**, sélectionnez le modèle de certificat d’ordinateur Mac que vous avez créé à l’étape 3.  

11. Cliquez sur **OK** pour fermer la boîte de dialogue **Profil d’inscription**, puis la boîte de dialogue **Paramètres client par défaut**.  

    > [!TIP]  
    >  Si vous voulez modifier l’intervalle de la stratégie client, utilisez le paramètre **Intervalle d’interrogation de stratégie client** dans le groupe de paramètres client **Stratégie client**.  

 Tous les utilisateurs sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie du client. Pour lancer la récupération de stratégie pour un seul client, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](../../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Outre les paramètres client d’inscription, vérifiez que vous avez configuré les paramètres d’appareil client suivants :  

-   **Inventaire matériel** : Activez et configurez ce paramètre si vous voulez collecter l’inventaire matériel des ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Comment étendre l’inventaire matériel dans System Center Configuration Manager](../../../core/clients/manage/inventory/extend-hardware-inventory.md).  

-   **Paramètres de compatibilité** : Activez et configurez ce paramètre si vous voulez évaluer et corriger les paramètres sur les ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Planifier et configurer les paramètres de compatibilité](../../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

> [!NOTE]  
>  Pour plus d’informations sur les paramètres client Configuration Manager, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-settings.md).  

## <a name="download-the-client-source-files-for-macs"></a>Télécharger les fichiers sources du client pour les ordinateurs Mac  

1.  Téléchargez le package de fichiers du client Mac OS X, **ConfigmgrMacClient.msi**, et enregistrez-le sur un ordinateur exécutant Windows.  

     Ce fichier n’est pas fourni dans le support d’installation de Configuration Manager. Vous pouvez télécharger ce fichier à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184).  

2.  Sur l’ordinateur Windows, exécutez **ConfigmgrMacClient.msi** pour extraire le package du client Mac (Macclient.dmg) dans un dossier du disque local (par défaut, **C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client\\**).  

3.  Copiez le fichier Macclient.dmg dans un dossier de l'ordinateur Mac.  

4.  Sur l’ordinateur Mac, exécutez le fichier Macclient.dmg pour extraire les fichiers dans un dossier du disque local.  

5.  Dans ce dossier, assurez-vous que les fichiers Ccmsetup et CMClient.pkg ont été extraits, qu'un dossier nommé Outils a été créé et qu'il contient les outils CMDiagnostics, CMUninstall, CMAppUtil et CMEnroll.

    -  **Ccmsetup** : permet d’installer le client Configuration Manager sur les ordinateurs Mac.  

    -   **CMDiagnostics** : permet de collecter les informations de diagnostic relatives au client Configuration Manager sur les ordinateurs Mac.  

    -   **CMUninstall** : permet de désinstaller le client des ordinateurs Mac.  

    -   **CMAppUtil** : permet de convertir les packages d’applications Apple dans un format qui peut être déployé sous forme d’application Configuration Manager.  

    -   **CMEnroll** : permet de demander et d’installer le certificat client d’un ordinateur Mac en vue d’installer le client Configuration Manager.   

## <a name="install-the-client-and-then-enroll-the-client-certificate-on-the-mac"></a>Installer le client, puis inscrire le certificat client sur l’ordinateur Mac  

Vous pouvez inscrire des clients individuels avec l’[Assistant Inscription d’ordinateur Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Pour activer l’automatisation qui permet d’inscrire un grand nombre de clients, servez-vous de l’[outil CMEnroll](#client-and-certificate-automation-with-cmenroll).   


###  <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscrire le client à l’aide de l’Assistant Inscription d’ordinateur Mac  

1.  Quand vous avez terminé l’installation du client, l’Assistant Inscription d’ordinateur s’ouvre. Si l’Assistant ne s’ouvre pas ou si vous le fermez par inadvertance, cliquez sur **Inscription** dans la page des préférences **Configuration Manager** pour l’ouvrir.  

2.  Dans la deuxième page de l’Assistant, entrez les informations suivantes :  

    -   **Nom d'utilisateur** : le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

        -   « domaine\nom ». Par exemple: « contoso\mnorth »  

        -   « user@domain ». Par exemple : « mnorth@contoso.com »  

            > [!IMPORTANT]  
            >  Lorsque vous utilisez une adresse électronique pour renseigner le champ **Nom d’utilisateur**, Configuration Manager utilise automatiquement le nom de domaine de l’adresse électronique et le nom par défaut du serveur de point proxy d’inscription pour renseigner le champ **Nom du serveur**. Si ce nom de domaine et ce nom de serveur ne correspondent pas au nom du serveur de point proxy d’inscription, indiquez aux utilisateurs le nom correct à utiliser lors de l’inscription de leurs ordinateurs Mac.  

         Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de lecture et d'inscription dans le modèle de certificat client Mac.  

    -   **Mot de passe** : entrez un mot de passe correspondant au nom d’utilisateur spécifié.  

    -   **Nom du serveur** : entrez le nom du serveur de point proxy d’inscription.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatisation du client et du certificat avec CMEnroll  

Utilisez cette procédure pour l’automatisation de l’installation du client ainsi que la demande et l’inscription de certificats clients avec l’outil CMEnroll. Pour exécuter l’outil, vous devez disposer d’un compte d’utilisateur Active Directory.

1.  Sur l’ordinateur Mac, accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg.  

2.  Entrez la ligne de commande suivante : **sudo ./ccmsetup**  

3.  Patientez jusqu'à ce que le message **Installation terminée** s'affiche à l'écran. Même si le programme d’installation affiche un message vous demandant de redémarrer maintenant, ne suivez pas cette instruction et passez à l’étape suivante.  

4.  Dans le dossier Outils sur l’ordinateur Mac, tapez la commande suivante : **sudo ./CMEnroll -s &lt;nom_serveur_proxy_inscription> -ignorecertchainvalidation -u &lt;nom_utilisateur>**  

    Une fois le client installé, l’Assistant Inscription d’ordinateur Mac s’ouvre pour vous aider à inscrire l’ordinateur Mac. Pour inscrire le client par cette méthode, consultez [To enroll the client by using the Mac Computer Enrollment Wizard](#BKMK_EnrollR2) dans cette rubrique.  

5. Tapez le mot de passe du compte d’utilisateur Active Directory.  Quand vous entrez cette commande, vous êtes invité à entrer deux mots de passe : la première invite concerne le compte de superutilisateur qui exécute la commande. La seconde invite est pour le compte d'utilisateur Active Directory. Les invites semblent identiques, assurez-vous que vous les spécifiez dans le bon ordre.  

    Le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

    -   « domaine\nom ». Par exemple: « contoso\mnorth »  

    -   « user@domain ». Par exemple : « mnorth@contoso.com »  

     Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de lecture et d'inscription dans le modèle de certificat client Mac.  

     Exemple : si le serveur de point proxy d’inscription se nomme **server02.contoso.com** et que des autorisations ont été accordées au nom d’utilisateur **contoso\mnorth** pour le modèle de certificat client Mac, tapez la ligne suivante : **sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u ’contoso\mnorth’**  

    > [!NOTE]  
    >  Si le nom d’utilisateur contient l’un des caractères **&lt;>"+=,**, l’inscription échoue. Obtenez un certificat hors bande avec un nom d’utilisateur qui ne contient pas ces caractères.  
    >  
    >  Pour une expérience utilisateur plus transparente, vous pouvez mettre les étapes d'installation et les commandes sous forme de script afin que les utilisateurs n'aient qu'à fournir leurs nom d'utilisateur et mot de passe.  

5.  Patientez jusqu'à l'affichage d'un message indiquant que l' **inscription s'est déroulée correctement** .  

6.  Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    a.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Dans la boîte de dialogue **Trousseau d’accès**, dans la zone **Trousseau**, choisissez **Système**, puis dans la zone **Catégorie**, choisissez **Clés**.  

    c.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    d.  Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    e.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    f.  Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

7.  Redémarrez l'ordinateur Mac.  

 Vérifiez que l'installation du client a abouti en ouvrant l'élément **Configuration Manager** dans les **Préférences Système** de l'ordinateur Mac. Vous pouvez également mettre à jour et afficher le regroupement **Tous les systèmes** pour vérifier que l'ordinateur Mac figure désormais dans ce regroupement en tant que client géré.  

> [!TIP]  
>  Pour vous aider à résoudre les problèmes liés au client Mac, vous pouvez utiliser le programme CMDiagnostics inclus avec le package client Mac OS X afin de recueillir les informations de diagnostic suivantes :  
>   
>  -   Liste des processus en cours.  
> -   Version du système d'exploitation Mac OS X.  
> -   Rapports des défaillances du système Mac OS X liées au client Configuration Manager, y compris les fichiers **CCM\*.crash** et **System Preference.crash**.  
> -   Le fichier de nomenclature et le fichier de liste des propriétés (.plist) créés par l’installation du client Configuration Manager.  
> -   Le contenu du dossier /Library/Application Support/Microsoft/CCM/Logs.  
>   
>  Les informations recueillies par le programme CmDiagnostics sont ajoutées à un fichier zip enregistré sur le bureau de l’ordinateur et nommé `cmdiag-<hostname>-<datetime>.zip`.


##  <a name="use-a-certificate-request-and-installation-method-that-is-independent-from-configuration-manager"></a>Utiliser une demande de certificat et une méthode d'installation indépendantes de Configuration Manager  

Tout d’abord, effectuez ces tâches spécifiques à partir de [Préparer le déploiement du logiciel client pour ordinateurs Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients) :

1. [Déployer un certificat de serveur web sur les serveurs de système de site](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-web-server-certificate-to-site-system-servers)

2. [Déployer un certificat d’authentification client sur les serveurs de système de site](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#deploy-a-client-authentication-certificate-to-site-system-servers)

3. [Configurer le point de gestion et le point de distribution](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#configure-the-management-point-and-distribution-point)

4. [Facultatif : Installer le point Reporting Services](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#install-the-reporting-services-point)

Effectuez ensuite ces tâches :

5. [Télécharger les fichiers sources du client pour les ordinateurs Mac](#download-the-client-source-files-for-macs).  
6. Utilisez les instructions qui accompagnent la méthode de déploiement de certificat choisie pour demander et installer le certificat client sur l’ordinateur Mac.  
7.  Accédez au dossier dans lequel vous avez extrait le contenu du fichier macclient.dmg, téléchargé depuis le Centre de téléchargement Microsoft.  

3.  Entrez la ligne de commande suivante : **sudo ./ccmsetup -MP <nom_de_domaine_complet_Internet_du_point_de_gestion\> -SubjectName <valeur_objet_certificat\>**.  La valeur de l'objet Certificat est sensible à la casse, vous devez l'entrer exactement telle qu'elle apparaît dans les détails du certificat.  

     Exemple : si le nom de domaine complet Internet dans les propriétés du système de site est **server03.contoso.com** et que le certificat client Mac porte le nom de domaine complet **mac12.contoso.com** comme nom commun dans l’objet certificat, tapez : **sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com**  

4.  Patientez jusqu'à l'affichage du message d' **installation terminée** , puis redémarrez l'ordinateur Mac.  

5.  Pour vérifier que Configuration Manager peut accéder à ce certificat, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    a.  Entrez la commande **sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access**  

    b.  Dans la boîte de dialogue **Trousseau d’accès**, dans la zone **Trousseau**, choisissez **Système**, puis dans la zone **Catégorie**, choisissez **Clés**.  

    c.  Développez les clés pour afficher les certificats clients. Lorsque vous avez identifié le certificat avec une clé privée que vous venez d'installer, double-cliquez sur la clé.  

    d.  Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    e.  Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    f.  Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

6.  Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, vous devez spécifier le numéro de série du certificat pour identifier le certificat que vous voulez utiliser pour le client Configuration Manager. Pour ce faire, utilisez la commande suivante : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numéro_série\>"**.  

     Exemple : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

 Vérifiez que l’installation du client a abouti en ouvrant l’élément **Configuration Manager** dans les **Préférences système** de l’ordinateur Mac. Vous pouvez également mettre à jour et afficher le regroupement **Tous les systèmes** pour vérifier que l’ordinateur Mac figure désormais dans ce regroupement comme client géré.  

## <a name="renewing-the-mac-client-certificate"></a>Renouvellement du certificat client Mac  
 Utilisez la procédure suivante avant de renouveler le certificat d'ordinateur sur les ordinateurs Mac.  

 Cette procédure supprime l'ID SMS qui est requis par le client pour utiliser un certificat nouveau ou renouvelé sur l'ordinateur Mac.  

> [!IMPORTANT]  
>  Lorsque vous supprimez et remplacez l’ID SMS client, tout historique client stocké, tel que l’inventaire, est supprimé après la suppression du client de la console Configuration Manager.  

### <a name="to-renew-the-mac-client-certificate"></a>Pour renouveler le certificat client Mac  

1.  Créez et remplissez un regroupement d’appareils pour les ordinateurs Mac qui doivent renouveler les certificats d’ordinateur.  

2.  Dans l'espace de travail **Ressources et compatibilité** , démarrez l' **Assistant Création d'élément de configuration**.  

3.  Sur la page **Général** de l'Assistant, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type :Mac OS X**  

4.  Sur la page **Plateformes prises en charge** de l'Assistant, assurez-vous que toutes les versions de Mac OS X sont sélectionnées.  

5.  Sur la page **Paramètres** de l'Assistant, cliquez sur **Nouveau** , puis dans la boîte de dialogue **Créer un paramètre** , spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Type de paramètre :Script**  

    -   **Type de données :Chaîne**  

6.  Dans la boîte de dialogue **Créer un paramètre** , sous **Script de découverte**, cliquez sur **Ajouter un script** pour définir un script de découverte des ordinateurs Mac configurés avec un ID SMS.  

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

12. Dans la page **Règles de compatibilité** de l’Assistant, choisissez **Nouveau**, puis dans la boîte de dialogue **Créer une règle**, spécifiez les informations suivantes :  

    -   **Nom :Supprimer l’ID SMS pour Mac**  

    -   **Paramètre sélectionné :** Choisissez **Parcourir**, puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    -   Dans **les valeurs suivantes** , entrez **la paire domaine/par défaut (com.microsoft.ccmclient, ID SMS) n'existe pas**.  

    -   Activez l'option **Exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant Création d'élément de configuration.  

14. Créez une ligne de base de configuration contenant l'élément de configuration que vous venez de créer et déployez-la sur le regroupement de périphériques créé à l'étape 1.  

     Pour plus d’informations sur la création et le déploiement de bases de référence de configuration, consultez [Comment créer des bases de référence de configuration dans System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-baselines.md).  

15. Après avoir installé un nouveau certificat sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour configurer le client de sorte à utiliser le nouveau certificat :  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <Subject_Name_of_New_Certificate>  
    ```  

16. Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, vous devez spécifier le numéro de série du certificat pour identifier le certificat que vous voulez utiliser pour le client Configuration Manager. Pour ce faire, utilisez la commande suivante : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "<numéro_série\>"**.  

     Exemple : **sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"**  

17. Redémarrer.  


## <a name="see-also"></a>Voir aussi

[Gérer les clients Mac](/sccm/core/clients/manage/maintain-mac-clients)
