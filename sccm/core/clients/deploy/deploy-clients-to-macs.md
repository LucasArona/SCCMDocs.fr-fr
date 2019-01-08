---
title: Déployer des clients Mac
titleSuffix: Configuration Manager
description: Découvrez comment déployer des clients sur des ordinateurs Mac dans Configuration Manager.
ms.date: 12/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e46ad501-5d73-44ac-92de-0de14ef72b83
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ba8182795759a29b4a5c8e4dfaa73f7c764dd7ff
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53424882"
---
# <a name="how-to-deploy-clients-to-macs"></a>How to deploy clients to Macs

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit comment déployer et gérer le client Configuration Manager sur des ordinateurs Mac. Pour en savoir plus sur les éléments à configurer avant de déployer les clients sur des ordinateurs Mac, consultez [Préparer le déploiement du logiciel client pour ordinateurs Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients).

Quand vous installez un nouveau client pour les ordinateurs Mac, vous devez peut-être également installer des mises à jour Configuration Manager pour refléter les nouvelles informations client dans la console Configuration Manager.

Dans ces procédures, vous avez deux options pour l’installation des certificats clients. En savoir plus sur les certificats clients pour Mac dans [Préparer le déploiement du logiciel client pour ordinateurs Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients#certificate-requirements).  

- Utilisez l’inscription Configuration Manager à l’aide de l’[outil CMEnroll](#bkmk_enroll). Le processus d’inscription ne prend pas en charge le renouvellement automatique des certificats. Réinscrivez l’ordinateur Mac avant que le certificat installé arrive à expiration.    

- [Utilisez une demande de certificat et une méthode d’installation indépendantes de Configuration Manager](#bkmk_external).  

> [!IMPORTANT]  
> Pour déployer le client sur des appareils exécutant macOS Sierra, vous devez configurer correctement le **Nom du sujet** du certificat de point de gestion. Par exemple utilisez le nom de domaine complet du serveur de point de gestion.



## <a name="configure-client-settings"></a>Configurer les paramètres client  

Utilisez les [paramètres client par défaut](/sccm/core/clients/deploy/about-client-settings) pour configurer l'inscription d’ordinateurs Mac. Vous ne pouvez pas utiliser de paramètres client personnalisés. Pour demander le certificat et l’installer, le client Configuration Manager pour Mac a besoin des paramètres client par défaut.  

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Sélectionnez le nœud **Paramètres client**, puis sélectionnez **Paramètres client par défaut**.  

2. Dans le ruban, sur l’onglet **Accueil** et dans le groupe **Propriétés**, sélectionnez **Propriétés**.  

3. Sélectionnez la section **Inscription**, puis configurez les paramètres suivants :  

    1. **Autoriser les utilisateurs à inscrire des appareils mobiles et des ordinateurs Mac** : **Oui**  

    2. **Profil d’inscription :** Choisissez **Définir un profil**.  

4. Dans la boîte de dialogue **Profil d’inscription d’appareil mobile**, choisissez **Créer**.  

5. Dans la boîte de dialogue **Créer un profil d'inscription**, entrez un nom pour ce profil d'inscription. Configurez ensuite le **Code du site de gestion**. Sélectionnez le site principal Configuration Manager contenant les points de gestion pour ces ordinateurs Mac.  

    > [!NOTE]  
    >  Si vous ne pouvez pas sélectionner le site, vérifiez que vous avez configuré au moins un point de gestion dans le site pour prendre en charge les appareils mobiles.  

6. Choisissez **Ajouter**.  

7. Dans la fenêtre **Ajouter une autorité de certification pour les appareils mobiles**, sélectionnez le serveur de l’autorité de certification émettrice des certificats pour les ordinateurs Mac.  

8. Dans la boîte de dialogue **Créer un profil d’inscription**, sélectionnez le modèle de certificat d’ordinateur Mac que vous avez créé précédemment.  

9. Sélectionnez **OK** pour fermer la boîte de dialogue **Profil d’inscription**, puis la boîte de dialogue **Paramètres client par défaut**.  

    > [!TIP]  
    > Si vous voulez modifier l’intervalle de la stratégie client, utilisez le paramètre **Intervalle d’interrogation de stratégie client** dans le groupe de paramètres client **Stratégie client**.  

La prochaine fois que les appareils téléchargent la stratégie client, Configuration Manager applique ces paramètres pour tous les utilisateurs. Pour lancer la récupération de stratégie pour un seul client, consultez la page [Lancer une récupération de stratégie pour un client Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

Outre les paramètres du client d’inscription, vérifiez que vous avez configuré les paramètres d’appareil client suivants :  

- **Inventaire matériel** : Activez et configurez cette fonctionnalité si vous souhaitez collecter l'inventaire matériel des ordinateurs clients Mac et Windows. Pour plus d’informations, consultez la page [Guide pratique pour étendre l’inventaire matériel](/sccm/core/clients/manage/inventory/extend-hardware-inventory).  

- **Paramètres de compatibilité** : Activez et configurez cette fonctionnalité si vous souhaitez évaluer et corriger les paramètres sur les ordinateurs clients Mac et Windows. Pour plus d’informations, consultez [Planifier et configurer les paramètres de compatibilité](/sccm/compliance/plan-design/plan-for-and-configure-compliance-settings).  

Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client](/sccm/core/clients/deploy/configure-client-settings).  



## <a name="bkmk_download"></a> Télécharger le client Mac  

1. Téléchargez le package de fichiers du client Mac OS X à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=47719). Enregistrez le fichier **ConfigmgrMacClient.msi** sur un ordinateur exécutant Windows. Ce fichier n’est pas fourni dans le support d’installation de Configuration Manager.  

2. Exécutez le programme d’installation sur l’ordinateur Windows. Extrayez le package client Mac **Macclient.dmg** dans un dossier sur le disque local. Par défaut, le chemin d'accès est `C:\Program Files (x86)\Microsoft\System Center 2012 Configuration Manager Mac Client`.  

3. Copiez le fichier **Macclient.dmg** dans un dossier de l'ordinateur Mac.  

4. Sur l’ordinateur Mac, exécutez le fichier **Macclient.dmg** pour extraire les fichiers dans un dossier du disque local.  

5. Dans ce dossier, assurez-vous que les fichiers suivants sont bien présents : 

    - **Ccmsetup** : Installe le client Configuration Manager sur votre ordinateur Mac à l’aide de **CMClient.pkg**.  

    - **CMDiagnostics** : Collecte les informations de diagnostic relatives au client Configuration Manager sur les ordinateurs Mac.  

    - **CMUninstall** : Désinstalle le client des ordinateurs Mac.  

    - **CMAppUtil** : Convertit les packages d’applications Apple dans un format qui peut être déployé sous forme d’application Configuration Manager.  

    - **CMEnroll** : Demande et installe le certificat client d’un ordinateur Mac en vue d’installer le client Configuration Manager.  



## <a name="bkmk_enroll"></a> Inscrire le client Mac  

Inscrivez des clients individuels avec l’[assistant Inscription d’ordinateur Mac](#enroll-the-client-with-the-mac-computer-enrollment-wizard).

Pour automatiser l’inscription d’un grand nombre de clients, utilisez l’[outil CMEnroll](#client-and-certificate-automation-with-cmenroll).   


### <a name="enroll-the-client-with-the-mac-computer-enrollment-wizard"></a>Inscrire le client à l’aide de l’assistant Inscription d’ordinateur Mac  

1. Une fois que vous avez installé le client, l’assistant Inscription d’ordinateur s’ouvre. Pour démarrer manuellement l’assistant, sélectionnez **Inscrire** sur la page des préférences **Configuration Manager**.  

2. Sur la deuxième page de l’assistant, indiquez les informations suivantes :  

   - **Nom d'utilisateur** : Le nom d'utilisateur peut se présenter sous l'une des formes suivantes :  

     - `domain\name`. Exemple : `contoso\mnorth`  

     - `user@domain`. Exemple : `mnorth@contoso.com`  

         > [!IMPORTANT]  
         >  Lorsque vous utilisez une adresse e-mail dans le champ **Nom d’utilisateur**, Configuration Manager renseigne automatiquement le champ **Nom du serveur**. Il utilise le nom par défaut du serveur de point proxy d’inscription et le nom de domaine de l’adresse e-mail. Si ces noms ne correspondent pas au nom du serveur de point proxy d’inscription, corrigez le **Nom du serveur** lors de l’inscription.  

       Le nom d'utilisateur et le mot de passe correspondant doivent correspondre à un compte d'utilisateur Active Directory disposant des autorisations de **lecture** et d'**inscription** dans le modèle de certificat client Mac.  

   - **Nom du serveur** : Nom du serveur de point proxy d’inscription.  


### <a name="client-and-certificate-automation-with-cmenroll"></a>Automatisation du client et du certificat avec CMEnroll  

Utilisez cette procédure pour l’automatisation de l’installation du client ainsi que la demande et l’inscription de certificats clients avec l’outil CMEnroll. Pour exécuter l’outil, vous devez disposer d’un compte d’utilisateur Active Directory.

1. Sur l’ordinateur Mac, accédez au dossier dans lequel vous avez extrait le contenu du fichier **Macclient.dmg**.  

2. Entrez la commande suivante : `sudo ./ccmsetup`  

3. Patientez jusqu'à ce que le message **Installation terminée** s'affiche à l'écran. Même si le programme d’installation affiche un message vous demandant de redémarrer maintenant, ne suivez pas cette instruction et passez à l’étape suivante.  

4. À partir du dossier **Outils** de l’ordinateur Mac, tapez la ligne de commande suivante : `sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u '<user_name>'`  

    Une fois le client installé, l’Assistant Inscription d’ordinateur Mac s’ouvre pour vous aider à inscrire l’ordinateur Mac. Pour en savoir plus, consultez la page [Inscrire le client à l’aide de l’assistant Inscription d’ordinateur Mac](#bkmk_enroll).  

     Exemple : Si le serveur de point proxy d’inscription se nomme **server02.contoso.com** et que vous avez accordé les autorisations **contoso\mnorth** pour le modèle de certificat client Mac, tapez la ligne de commande suivante : `sudo ./CMEnroll -s server02.contoso.com -ignorecertchainvalidation -u 'contoso\mnorth'`  

    > [!NOTE]  
    > Si le nom d’utilisateur contient l’un des caractères suivants, l’inscription échoue : `<>"+=,`. Utilisez un certificat hors bande avec un nom d’utilisateur qui ne contient pas ces caractères.  
    >  
    > Pour une expérience utilisateur plus transparente, scriptez les étapes d’installation. afin que les utilisateurs fournissent uniquement leur nom d’utilisateur et mot de passe.  

5. Tapez le mot de passe du compte d’utilisateur Active Directory. Lorsque vous saisissez cette commande, vous êtes invité à entrer deux mots de passe. Le premier mot de passe correspond au compte de superutilisateur qui exécute la commande. La seconde invite est pour le compte d'utilisateur Active Directory. Les invites semblent identiques, assurez-vous que vous les spécifiez dans le bon ordre.  

6. Patientez jusqu'à l'affichage d'un message indiquant que l' **inscription s'est déroulée correctement** .  

7. Pour limiter le certificat inscrit à Configuration Manager, sur l’ordinateur Mac, ouvrez une fenêtre de terminal et apportez les modifications suivantes :  

    1. Entrez la commande `sudo /Applications/Utilities/Keychain Access.app/Contents/MacOS/Keychain Access`.  

    2. Dans la fenêtre **Accès au trousseau**, dans la section **Trousseaux**, choisissez **Système**. Ensuite, dans la section **Catégorie**, choisissez **Clés**.  

    3. Développez les clés pour afficher les certificats clients. Recherchez le certificat avec une clé privée que vous avez installée et ouvrez la clé.  

    4. Sous l’onglet **Contrôle d’accès**, choisissez **Confirmer avant d’autoriser l’accès**.  

    5. Accédez à **/Library/Application Support/Microsoft/CCM**, sélectionnez **CCMClient**, puis choisissez **Ajouter**.  

    6. Choisissez **Enregistrer les modifications** et fermez la boîte de dialogue **Trousseau d’accès**.  

8. Redémarrez l'ordinateur Mac.  

Pour vérifier que l'installation du client a abouti, ouvrez l'élément **Configuration Manager** dans les **préférences du système** de l'ordinateur Mac. De plus, mettez à jour et affichez le regroupement **Tous les systèmes** dans la console Configuration Manager. Vérifiez que l’ordinateur Mac apparaît dans ce regroupement sous forme d’un client managé.  

> [!TIP]  
> Pour dépanner le client Mac, utilisez l’outil **CMDiagnostics** qui est inclus dans le package du client Mac. Utilisez-le pour collecter les informations de diagnostic suivantes :  
>   
> - Liste des processus en cours.  
> - Version du système d'exploitation Mac OS X.  
> - Rapports des défaillances du système Mac OS X liées au client Configuration Manager, y compris les fichiers **CCM\*.crash** et **System Preference.crash**.  
> - Le fichier de nomenclature et le fichier de liste des propriétés (.plist) créés par l’installation du client Configuration Manager.  
> - Les contenus du dossier **/Library/Application Support/Microsoft/CCM/Logs**.  
>   
> Les informations recueillies par le programme CmDiagnostics sont ajoutées à un fichier zip enregistré sur le bureau de l’ordinateur et nommé `cmdiag-<hostname>-<datetime>.zip`.



## <a name="bkmk_external"></a> Gérer les certificats externes à Configuration Manager

Vous pouvez utiliser une demande de certificat et une méthode d’installation indépendantes de Configuration Manager. Vous utilisez la même procédure générale, mais les étapes supplémentaires suivantes sont incluses : 

- Lorsque vous installez le client Configuration Manager, utilisez les options de ligne de commande **MP** et **SubjectName**. Entrez la commande suivante : `sudo ./ccmsetup -MP <management point internet FQDN> -SubjectName <certificate subject name>`. Le nom de l'objet du certificat est sensible à la casse, vous devez l'entrer exactement tel qu’il apparaît dans les détails du certificat.  

     Exemple : Le nom de domaine complet Internet du point de gestion correspond à **server03.contoso.com**. Le nom de domaine complet du certificat client Mac correspond à **mac12.contoso.com**, qui apparaît comme nom commun de l’objet du certificat. Utilisez la commande suivante : `sudo ./ccmsetup -MP server03.contoso.com -SubjectName mac12.contoso.com`  

- Si vous disposez de plusieurs certificats qui contiennent la même valeur d’objet, spécifiez le numéro de série du certificat que vous voulez utiliser pour le client Configuration Manager. Utilisez la commande suivante : `sudo defaults write com.microsoft.ccmclient SerialNumber -data "<serial number>"`.  

     Exemple : `sudo defaults write com.microsoft.ccmclient SerialNumber -data "17D4391A00000003DB"`  



## <a name="renew-the-mac-client-certificate"></a>Renouveler le certificat client Mac  

Cette procédure supprime l’ID SMS. Le client Configuration Manager pour Mac nécessite un nouvel ID afin d’utiliser un nouveau certificat ou un certificat renouvelé.  

> [!IMPORTANT]  
> Une fois que vous avez remplacé l’ID SMS client, lorsque vous supprimez les anciennes ressources de la console Configuration Manager, vous supprimez également l’historique client qui est enregistré. Par exemple, vous supprimez l’historique des inventaires matériels pour ce client.  


1. Créez et remplissez un regroupement d’appareils pour les ordinateurs Mac qui doivent renouveler les certificats d’ordinateur.  

2. Dans l'espace de travail **Ressources et compatibilité** , démarrez l' **Assistant Création d'élément de configuration**.  

3. Sur la page **Général** de l'Assistant, spécifiez les informations suivantes :  

    - **Nom** : **Supprimer l'ID SMS pour Mac**  

    - **Type** : **Mac OS X**  

4. Sur la page **Plateformes prises en charge**, sélectionnez toutes les versions de Mac OS X.  

5. Sur la page **Paramètres**, sélectionnez **Nouveau**. Dans la fenêtre **Créer un paramètre**, spécifiez les informations suivantes :  

    - **Nom** : **Supprimer l'ID SMS pour Mac**  

    - **Type de paramètre** : **Script**  

    - **Type de données** : **Chaîne**  

6. Dans la fenêtre **Créer un paramètre**, pour **Script de découverte**, sélectionnez **Ajouter un script**. Cette action spécifie un script permettant de détecter les ordinateurs Mac configurés avec un ID SMS.  

7. Dans la fenêtre **Modifier un script de découverte**, entrez le script Shell suivant :  

    ```  
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8. Choisissez **OK** pour fermer la fenêtre **Modifier un script de découverte**.  

9. Dans la fenêtre **Créer un paramètre**, pour **Script de correction (facultatif)**, choisissez **Ajouter un script**. Cette action spécifie un script permettant de supprimer l’ID SMS lorsqu’il est détecté sur les ordinateurs Mac.  

10. Dans la fenêtre **Créer un script de correction**, entrez le script Shell suivant :  

    ```  
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Choisissez **OK** pour fermer la fenêtre **Créer un script de correction**.  

12. Sur la page **Règles de conformité**, choisissez **Nouveau**. Ensuite, dans la fenêtre **Créer une règle**, spécifiez les informations suivantes :  

    - **Nom** : **Supprimer l'ID SMS pour Mac**  

    - **Paramètre sélectionné** : Choisissez **Parcourir**, puis sélectionnez le script de découverte que vous avez spécifié précédemment.  

    - Dans le champ des **valeurs suivantes** : **La paire domaine/par défaut (com.microsoft.ccmclient, ID SMS) n'existe pas**.  

    - Activez l'option permettant d’**exécuter le script de correction spécifié lorsque ce paramètre n'est pas compatible**.  

13. Effectuez toutes les étapes de l'Assistant.  

14. Créez une base de référence de configuration qui contient cet élément de configuration. Déployez la base de référence sur le regroupement cible.  

     Pour plus d’informations, consultez la page [Créer des bases de référence de configuration](/sccm/compliance/deploy-use/create-configuration-baselines).  

15. Une fois que vous avez installé un nouveau certificat sur les ordinateurs Mac sur lesquels l'ID SMS a été supprimé, exécutez la commande suivante pour configurer le client de sorte à utiliser le nouveau certificat :  

    ```  
    sudo defaults write com.microsoft.ccmclient SubjectName -string <subject_name_of_new_certificate>  
    ```  



## <a name="see-also"></a>Voir aussi

[Préparer le déploiement des clients sur des ordinateurs Mac](/sccm/core/clients/deploy/prepare-to-deploy-mac-clients)

[Gérer les clients Mac](/sccm/core/clients/manage/maintain-mac-clients)
