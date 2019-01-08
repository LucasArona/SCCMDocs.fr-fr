---
title: 'Créer des éléments de configuration pour les ordinateurs Windows gérés par le client '
titleSuffix: Configuration Manager
description: Gérer les paramètres des ordinateurs et des serveurs Windows avec un élément de configuration Ordinateurs de bureau et serveurs Windows.
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbdb2ecdd0057b52586a7fa19e22cafa0319b039
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422230"
---
# <a name="how-to-create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration personnalisés pour les ordinateurs et serveurs Windows gérés par le client System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez l’élément de configuration **Ordinateurs de bureau et serveurs Windows (personnalisés)** pour gérer les paramètres des ordinateurs de bureau et serveurs Windows qui sont gérés par le client  Configuration Manager.  

## <a name="start-the-create-configuration-item-wizard"></a>Démarrer l'Assistant Création d'élément de configuration

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Éléments de configuration**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4.  Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  

5.  Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Ordinateurs et serveurs Windows (personnalisés)**.  

    > [!TIP]  
    >  Si vous voulez fournir des paramètres de méthode de détection pour vérifier l’existence d’une application, sélectionnez **Cet élément de configuration contient des paramètres d’application**.  

6.  Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  

## <a name="provide-detection-method-information"></a>Fournir des informations de méthode de détection  
 Utilisez cette procédure pour fournir les informations de méthode de détection de l'élément de configuration.  

> [!NOTE]  
>  S'applique uniquement si vous avez sélectionné **cet élément de configuration contient des paramètres d'application** sur la **Général** page de l'Assistant.  

 Une méthode de détection dans Configuration Manager contient des règles qui sont utilisées pour déterminer si une application est installée sur un ordinateur. La détection a lieu avant l'évaluation de la compatibilité de l'élément de configuration. Pour déterminer si une application est installée, vous pouvez détecter la présence du Windows Installer de l'application, utiliser un script personnalisé ou sélectionner **Toujours partir du principe que l'application est installée** pour évaluer la compatibilité de l'élément de configuration, que l'application soit installée ou non.  

 Utilisez ces procédures pour configurer des méthodes de détection dans System Center Configuration Manager.  

### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Pour détecter une installation d'application en utilisant le fichier Windows Installer  

1.  Sur le **des méthodes de détection** page de la **Assistant Création d'un élément de Configuration**, sélectionnez le **utiliser Windows Installer detection** case à cocher.  

2.  Cliquez sur **Open**, recherchez le fichier Windows Installer (.msi) que vous souhaitez détecter, puis cliquez sur **Open**.  

3.  Le **Version** zone est automatiquement renseignée avec le numéro de version du fichier Windows Installer que vous avez sélectionné. Si la valeur affichée est incorrecte, vous pouvez entrer un nouveau numéro de version dans cette zone.  

4.  Cochez la case **Cette application n’est pas installée pour un ou plusieurs utilisateurs** pour détecter chaque profil utilisateur sur l’ordinateur.  

### <a name="to-detect-a-specific-application-and-deployment-type"></a>Pour détecter un type d’application et de déploiement spécifique  

1.  Dans la page **Méthodes de détection** de l’ **Assistant Création d’élément de configuration**, cochez la case **Détecter un type d’application et de déploiement spécifique** , puis cliquez sur **Sélectionner**.  

2.  Dans la boîte de dialogue **Spécifier une application** , sélectionnez l’application et un type de déploiement associé à détecter.  

### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Pour détecter une installation d’application à l’aide d’un script personnalisé  

1.  Sur le **méthodes de détection** page de la **Assistant Création d'un élément de Configuration**, sélectionnez le **utiliser un script personnalisé pour détecter cette application** case à cocher.  

2.  Dans la liste, sélectionnez la langue du script que vous souhaitez ouvrir. Choisissez les scripts suivants :  

    -   **VBScript**  

    -   **JScript**  

    -   **PowerShell**  

3.  Cliquez sur **Ouvrir**, accédez au script à utiliser, puis cliquez sur **Ouvrir**.  

##  <a name="configure-settings"></a>Configurer les paramètres  
 Utilisez cette procédure pour configurer les paramètres dans l'élément de configuration.  

 Représentent les paramètres de l'entreprise ou critères techniques sont utilisées pour évaluer la conformité des périphériques clients. Vous pouvez configurer un nouveau paramètre ou accéder à un paramètre existant sur un ordinateur de référence.  

1. Dans la page **Paramètres** de l' **Assistant Création d'élément de configuration**, cliquez sur **Nouveau**.  

2. Sur l'onglet **Général** de la boîte de dialogue **Créer un paramètre** , fournissez les informations suivantes :  

   - **Nom :** entrez un nom unique pour le paramètre. Vous pouvez utiliser jusqu'à 256 caractères.  

   - **Description :** entrez la description du paramètre. Vous pouvez utiliser jusqu'à 256 caractères.  

   - **Type de paramètre :** dans la liste, choisissez et configurez l’un des types de paramètres suivants à utiliser pour ce paramètre :  

     - **Requête Active Directory**  

        **Préfixe LDAP** : désigne un préfixe valide pour la requête des services de domaine Active Directory afin d’évaluer la compatibilité sur les ordinateurs clients. Vous pouvez utiliser **LDAP: / /** pour un ou **GC: / /** pour effectuer une recherche de catalogue global...  

        **Nom unique (DN)** -spécifier le nom unique de l'objet Services de domaine Active Directory qui est évaluée pour la conformité sur les ordinateurs clients.  

        Par exemple, si vous voulez évaluer une valeur associée à un utilisateur nommé John Smith dans le domaine corp.contoso.com, entrez ce qui suit :  

       - **Filtre de recherche** : indique le filtre LDAP facultatif permettant d'affiner les résultats de la requête Services de domaine Active Directory pour évaluer la compatibilité sur les ordinateurs clients.  

          Pour renvoyer tous les résultats de la requête, entrez **(objectclass=\*)**.  

       - **Zone de recherche :** indique la zone de recherche dans les services de domaine Active Directory. Les choix sont les suivants :  

         -   **Base** -interroge uniquement l'objet spécifié.  

         -   **Un niveau** : cette option n’est pas utilisée dans cette version de Configuration Manager.  

         -   **Sous-arborescence** -interroge l'objet spécifié et son sous-arbre dans l'annuaire.  

       - **Propriété** -spécifier la propriété de l'objet Services de domaine Active Directory qui est utilisé pour évaluer la conformité sur les ordinateurs clients.  

          Par exemple, si vous souhaitez interroger la propriété Active Directory **badPwdCount**, qui stocke le nombre de fois qu'un utilisateur entre incorrectement un mot de passe, entrez **badPwdCount** dans ce champ.  

       - **Requête** -affiche la requête créée à partir des entrées dans **préfixe LDAP**, **nom unique (DN)**, **filtre de recherche** (si spécifiée), et **propriété**, qui sont utilisés pour évaluer la conformité sur les ordinateurs clients.  

         Pour plus d'informations sur la construction des requêtes LDAP, voir la documentation de Windows Server.  

     - **Assembly**  

        Configurez les éléments suivants pour ce type de paramètre :  

       - **Nom de l’assembly :** spécifie le nom de l’objet assembly à rechercher. Ce nom doit être différent des autres objets assembly de même type et il doit être enregistré dans le GAC (Global Assembly Cache). Le nom de l'assembly peut comporter jusqu'à 256 caractères.  

         Un assembly est un fragment de code qui peut être partagé entre plusieurs applications. Les assemblys peuvent comporter l'extension de fichier .dll ou .exe. Le Global Assembly Cache est un dossier appelé *%systemroot%\Assembly* sur client ordinateurs où tous les assemblys partagés sont stockés.  

     - **Système de fichiers**  

       - **Type** : dans la liste, indiquez si vous voulez rechercher un **fichier** ou un **dossier**.  

       - **Chemin** -spécifier le chemin d'accès du fichier spécifié ou du dossier sur les ordinateurs clients. Vous pouvez spécifier des variables d'environnement système et la variable d'environnement *%USERPROFILE%* dans le chemin.  

         > [!NOTE]  
         >  Si vous utilisez la variable d’environnement *%USERPROFILE%* dans les zones **Chemin** ou **Nom de fichier ou de dossier** , tous les profils utilisateur sont recherchés sur l’ordinateur client et plusieurs instances du fichier ou du dossier peuvent être trouvées.  
         >   
         >  Si les paramètres de compatibilité n’ont pas accès au chemin spécifié, une erreur de découverte est générée. En outre, si le fichier que vous recherchez est actuellement en cours d'utilisation, une erreur de découverte est générée.  

       - **Nom de fichier ou dossier** -spécifiez le nom de l'objet fichier ou dossier à rechercher. Vous pouvez spécifier des variables d'environnement système et la variable d'environnement *%USERPROFILE%* dans le nom de fichier ou de dossier. Vous pouvez aussi utiliser les caractères génériques * et ? dans le nom du fichier.  

         > [!NOTE]  
         >  Si vous spécifiez un nom de fichier ou dossier en utilisant des caractères génériques, cette combinaison peut produire un grand nombre de résultats et entraîner une forte utilisation des ressources sur l’ordinateur client ainsi qu’un trafic réseau élevé lors du signalement des résultats à System Center 2012 Configuration Manager.  

       - **Inclure les sous-dossiers** : activez cette option si vous voulez également effectuer la recherche dans les sous-dossiers dans le chemin spécifié.  

       - **Ce fichier ou dossier est associé à une application 64 bits** - si activé, seuls les emplacements de fichiers 64 bits (tel que *% ProgramFiles%*) sera vérifié sur les ordinateurs 64 bits. Si cette option n’est pas activée, les emplacements 32 bits (tels que *%ProgramFiles(x86)%*) et 64 bits sont vérifiés.  

         > [!NOTE]  
         >  Si le même fichier ou dossier existe dans les emplacements de systèmes de fichiers 64 bits et 32 bits sur le même ordinateur 64 bits, la condition globale détecte plusieurs fichiers.  

         Le paramètre **Système de fichiers** ne permet pas de définir un chemin UNC de partage réseau dans la zone **Chemin** .  

     - **Métabase IIS**  

       -   **Chemin de la métabase** : spécifiez un chemin valide à la métabase Internet Information Services (IIS).  

       -   **ID de propriété** : indique la propriété numérique du paramètre Métabase IIS.  

     - **Clé du Registre**  

       -   **Ruche** : dans la liste, sélectionnez la ruche du Registre dans laquelle vous voulez effectuer la recherche.  

       -   **Clé** : indiquez le nom de clé de Registre à rechercher. Utilisez le format *clé\sous-clé*.  

       -   **Cette clé de Registre est associée à une application 64 bits** -Spécifie si les clés de Registre 64 bits doivent être recherchés en plus des clés de Registre 32 bits sur les clients qui exécutent une version 64 bits de Windows.  

           > [!NOTE]  
           >  Si la même clé de Registre existe dans les emplacements de Registre 64 bits et 32 bits sur un même ordinateur 64 bits, les deux clés de Registre sont détectées par la condition globale.  

     - **Valeur de Registre**  

       - **Ruche** : dans la liste, sélectionnez la ruche du Registre dans laquelle vous voulez effectuer la recherche.  

       - **Clé** : indiquez le nom de clé de Registre à rechercher. Utilisez le format *clé\sous-clé*.  

       - **Valeur** : indiquez la valeur qui doit être contenue dans la clé de Registre spécifiée.  

       - **Cette clé de Registre est associée à une application 64 bits** : indique si la recherche doit être effectuée dans les clés de Registre 64 bits en plus des clés de Registre 32 bits sur les clients qui exécutent une version Windows 64 bits.  

         > [!NOTE]  
         >  Si la même clé de Registre existe dans les emplacements de Registre 64 bits et 32 bits sur un même ordinateur 64 bits, les deux clés de Registre sont détectées par la condition globale.  

         Vous pouvez également cliquer sur **Parcourir** pour accéder à un emplacement de Registre sur l’ordinateur ou sur un ordinateur distant. Pour rechercher un ordinateur distant, vous devez disposer des droits d'administrateur sur l'ordinateur distant et l'ordinateur distant doit exécuter le service Registre distant.  

     - **Script**  

       -   **Script de découverte** : cliquez sur **Ajouter** pour entrer ou rechercher le script que vous souhaitez utiliser. Vous pouvez utiliser des scripts Windows PowerShell, VBScript ou Microsoft JScript.  

       -   **Exécuter des scripts avec les informations d’identification d’utilisateur dont la session est ouverte** : si vous activez cette option, le script s’exécute sur les ordinateurs clients qui utilisent les informations d’identification des utilisateurs connectés.  

           > [!NOTE]  
           >  La valeur renvoyée par le script est utilisée pour évaluer la compatibilité de la condition globale. Par exemple, quand vous utilisez VBScript, vous pouvez utiliser la commande **WScript.Echo Result** pour renvoyer la valeur de la variable *Result* vers la condition globale.  

     - **Requête SQL**  

       -   **Instance SQL Server** : indiquez si vous préférez que la requête SQL soit exécutée sur l'instance par défaut, sur toutes les instances ou sur le nom d'une instance de base de données spécifique.  

           > [!NOTE]  
           >  Le nom de l'instance doit faire référence à une instance locale de SQL Server. Pour faire référence à une instance SQL Server en cluster, utilisez plutôt un paramètre de script.  

       -   **Base de données** -spécifiez le nom de la base de données Microsoft SQL Server sur lequel vous souhaitez exécuter la requête SQL.  

       -   **Colonne** -Indiquez le nom de la colonne renvoyée par l'instruction Transact-SQL qui est utilisée pour évaluer la conformité de la condition globale.  

       -   **Instruction Transact-SQL** : permet d'indiquer la requête SQL complète que vous souhaitez utiliser pour la condition globale. Vous pouvez également cliquer sur **Ouvrir** pour ouvrir une requête SQL existante.  

           > [!IMPORTANT]  
           >  Les paramètres de requête SQL ne prennent pas en charge les commandes SQL qui modifient la base de données. Vous pouvez uniquement utiliser les commandes SQL qui lisent des informations à partir de la base de données.  

     - **Requête WQL**  

       -   **Espace de noms** -spécifiez l'espace de noms Windows Management Instrumentation (WMI) qui est utilisé pour créer une requête WQL qui est évaluée pour la conformité sur les ordinateurs clients. La valeur par défaut est Root\cimv2.  

       -   **Classe** -spécifie la classe WMI qui permet de créer une requête WQL qui est évaluée pour la conformité sur les ordinateurs clients.  

       -   **Propriété** -spécifie la propriété WMI qui permet de créer une requête WQL qui est évaluée pour la conformité sur les ordinateurs clients.  

       -   **Clause WHERE de la requête WQL** : vous pouvez utiliser l'élément **Clause WHERE de la requête WQL** pour indiquer la clause WHERE à appliquer à l'espace de noms, à la classe et à la propriété spécifiés sur les ordinateurs clients.  

     - **Requête XPath**  

       - **Chemin** : spécifiez le chemin du fichier .xml sur les ordinateurs clients utilisé pour évaluer la compatibilité. Configuration Manager prend en charge l’utilisation de toutes les variables d’environnement système Windows et de la variable utilisateur *% USERPROFILE%* dans le nom de chemin.  

       - **Nom du fichier XML** -spécifier le nom du fichier contenant la requête XML qui est utilisée pour évaluer la conformité sur les ordinateurs clients.  

       - **Inclure les sous-dossiers** : activez cette option si vous voulez également rechercher dans tous les sous-dossiers sous le chemin spécifié.  

       - **Ce fichier est associé à une application 64 bits** : indiquez si la recherche doit porter également sur l’emplacement de fichier système 64 bits (*%windir%* \System32) en plus de l’emplacement de fichier système 32 bits (*%windir%* \Syswow64) sur les clients Configuration Manager qui exécutent une version 64 bits de Windows.  

       - **Requête XPath** -spécifier une valide complet requête XML path language (XPath) qui est utilisée pour évaluer la conformité sur les ordinateurs clients.  

       - **Espaces de noms** : ouvre la boîte de dialogue **Espaces de noms XML** pour identifier les espaces de noms et les préfixes à utiliser pendant la requête XPath.  

         Si vous tentez de détecter un fichier .xml chiffré, les paramètres de compatibilité trouvent le fichier, mais la requête XPath ne produit aucun résultat, et aucune erreur n’est générée.  

         Si la requête XPath n’est pas valide, le paramètre est évalué comme étant non compatible sur les ordinateurs clients.  

   - **Type de données :** dans la liste, choisissez le format dans lequel la condition retourne les données avant de les utiliser pour évaluer le paramètre. Le **type de données** liste n'est pas affichée pour tous les types de paramètre.  

     > [!NOTE]  
     >  Le type de données **Virgule flottante** prend en charge uniquement 3 chiffres après la virgule décimale.  

3. Configurer des détails supplémentaires sur ce paramètre sous la **définition de type** liste. Les éléments que vous pouvez configurer varient selon le type de paramètre que vous avez sélectionné.  

   > [!NOTE]  
   >  Lorsque vous créez des paramètres de type **système de fichiers**, **clé de Registre**, et **valeur de Registre**, vous pouvez cliquer sur **Parcourir** pour configurer le paramètre à partir de valeurs sur un ordinateur de référence. Pour accéder à une clé de Registre ou une valeur sur un ordinateur distant, l'ordinateur distant doit avoir le service Registre distant est activé.  

4. Cliquez sur **OK** pour enregistrer le paramètre et fermer la boîte de dialogue **Créer un paramètre** .  

##  <a name="configure-compliance-rules"></a>Configurer des règles de compatibilité  
 Procédez comme suit pour configurer des règles de compatibilité pour l'élément de configuration.  

 Les règles de compatibilité spécifient les critères qui définissent la compatibilité d'un élément de configuration. Avant que la compatibilité d'un paramètre puisse être évaluée, celui-ci doit comporter au moins une règle de compatibilité. WMI, Registre et les paramètres de script vous permettent de corriger les valeurs qui sont identifiés comme étant non conforme. Vous pouvez créer de nouvelles règles ou accédez à un paramètre existant dans n'importe quel élément de configuration pour sélectionner les règles qu'il contient.  

### <a name="to-create-a-compliance-rule"></a>Pour créer une règle de compatibilité  

1.  Sur la page **Règles de compatibilité** de l' **Assistant Création d'élément de configuration**, cliquez sur **Nouveau**.  

2.  Dans la boîte de dialogue **Créer une règle** , indiquez les informations suivantes :  

    -   **Nom :** Entrez un nom pour la règle de compatibilité.  

    -   **Description :** Entrez une description pour la règle de compatibilité.  

    -   **Paramètre sélectionné :** Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Paramètre de sélection**. Sélectionnez le paramètre que vous souhaitez définir une règle, ou cliquez sur **nouveau paramètre**. Lorsque vous avez terminé, cliquez sur **Sélectionner**.  

        > [!NOTE]  
        >  Vous pouvez également cliquer sur **Propriétés** pour afficher des informations sur le paramètre actuellement sélectionné.  

    -   **Type de règle :** Sélectionnez le type de règle de compatibilité que vous souhaitez utiliser :  

        -   **Valeur** créer une règle qui compare la valeur renvoyée par l'élément de configuration par rapport à une valeur que vous spécifiez.  

        -   **Existentiel** créer une règle qui évalue le paramètre, selon qu'elle existe sur un périphérique client ou sur le nombre de fois où il se trouve.  

    -   Pour un type de règle **Valeur**, spécifiez les informations suivantes :  

        -   **Le paramètre doit respecter la règle suivante** – sélectionnez un opérateur et une valeur d'évaluation de la compatibilité avec le paramètre sélectionné. Vous pouvez utiliser les opérateurs suivants :  

            |Opérateur|Informations complémentaires|  
            |--------------|----------------------|  
            |Égal à|Aucune information supplémentaire|  
            |N'est pas égal à|Aucune information supplémentaire|  
            |Supérieur à|Aucune information supplémentaire|  
            |Inférieur à|Aucune information supplémentaire|  
            |Entre|Aucune information supplémentaire|  
            |Supérieur ou égal à|Aucune information supplémentaire|  
            |Inférieur ou égal à|Aucune information supplémentaire|  
            |L'un des|Dans la zone de texte, spécifiez une entrée sur chaque ligne.|  
            |Aucun des|Dans la zone de texte, spécifiez une entrée sur chaque ligne.|  

        -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** : sélectionnez cette option si vous voulez que Configuration Manager corrige automatiquement les règles non compatibles. Configuration Manager.peut corriger automatiquement les types de règles suivants :  

            -   **Valeur de Registre** – la valeur de Registre est mis à jour si elle est non conforme et créé s'il n'existe pas.  

            -   **Script** (en exécutant automatiquement un script de correction).  

            -   **Requête WQL**  

            > [!IMPORTANT]  
            >  Vous ne pouvez corriger que les règles non compatibles lorsque l'opérateur de règle est défini sur **Égal à**.  

        -   **Rapport de non-conformité si cette définition de l'instance est introuvable** : l'élément de configuration des rapports non-conformité si ce paramètre n'est pas disponible sur les ordinateurs clients.  

        -   **Gravité de la non conformité pour les rapports :** spécifiez le niveau de gravité signalé (dans les rapports Configuration Manager) si cette règle de conformité échoue. Les niveaux de gravité disponibles sont les suivants :  

            -   **Aucun** : les ordinateurs non conformes à cette règle de compatibilité ne signalent pas de gravité d'échec.  

            -   **Information** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Informations**.  

            -   **Avertissement** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Avertissement**.  

            -   **Critique** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Critique**.  

            -   **Critique avec événement** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Critique**. Ce niveau de gravité est également enregistré comme un événement Windows dans le journal des événements des applications.  

        -   Pour un type de règle **Existentiel**, spécifiez les informations suivantes :  

            > [!NOTE]  
            >  Les options affichées peuvent varier selon le type de paramètre pour lequel vous configurez une règle.  

            -   **Le paramètre doit exister sur les appareils clients**  

            -   **Le paramètre ne doit pas exister sur les appareils clients**  

            -   **Le paramètre se produit le nombre de fois suivant :**  

        -   **Gravité de la non conformité pour les rapports :** spécifiez le niveau de gravité signalé (dans les rapports Configuration Manager) si cette règle de conformité échoue. Les niveaux de gravité disponibles sont les suivants :  

            -   **Aucun** : les ordinateurs non conformes à cette règle de compatibilité ne signalent pas de gravité d'échec.  

            -   **Information** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Informations**.  

            -   **Avertissement** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Avertissement**.  

            -   **Critique** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Critique**.  

            -   **Critique avec événement** : les ordinateurs non conformes à cette règle de compatibilité signalent une gravité d'échec **Critique**. Ce niveau de gravité est également enregistré comme un événement Windows dans le journal des événements des applications.  

3.  Cliquez sur **OK** pour fermer la boîte de dialogue **Créer une règle** .  

##  <a name="specify-supported-platforms"></a>Spécifier les plateformes prises en charge  
 Les plateformes prises en charge sont les systèmes d’exploitation sur lesquels la compatibilité d’un élément de configuration est évaluée.  

Dans la page **Plateformes prises en charge** de l’ **Assistant Création d’élément de configuration**, dans la liste, sélectionnez les versions Windows sur lesquelles vous voulez évaluer la compatibilité de l’élément de configuration ou cliquez sur **Sélectionner tout**.  

## <a name="complete-the-wizard"></a>Effectuer toutes les étapes de l'Assistant  
 Dans la page **Résumé** de l’Assistant, passez en revue les actions qui seront exécutées, puis terminez l’Assistant. Le nouvel élément de configuration est affiché dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité**.  
