---
title: Créer des éléments de configuration personnalisée
titleSuffix: Configuration Manager
description: Gérez les paramètres des ordinateurs et des serveurs Windows avec un élément de configuration pour les ordinateurs de bureau et les serveurs Windows.
ms.date: 03/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4253fdd94985a8a9adbc9e782f8397c2f76f5f2c
ms.sourcegitcommit: 4ab85212268e76d3fd22f00e6c74edaa5abde60c
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 03/05/2019
ms.locfileid: "57426887"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Créer des éléments de configuration personnalisés pour les ordinateurs de bureau et les serveurs Windows gérés avec le client Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Utilisez l’élément de configuration **personnalisé Ordinateurs de bureau et serveurs Windows** Configuration Manager pour gérer les paramètres des ordinateurs et des serveurs Windows gérés par le client Configuration Manager.  



## <a name="start-the-wizard"></a>Démarrer l’Assistant

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, développez **Paramètres de conformité**, puis sélectionnez le nœud **Éléments de configuration**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Créer un élément de configuration** dans le groupe **Créer**.  

3. Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  

4. Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Ordinateurs et serveurs Windows (personnalisés)**.  

    > [!TIP]  
    > Si vous voulez fournir des paramètres de méthode de détection pour vérifier l’existence d’une application, sélectionnez **Cet élément de configuration contient des paramètres d’application**.  

5. Pour rechercher et filtrer plus facilement des éléments de configuration dans la console Configuration Manager, sélectionnez **Catégories** afin de créer et d’attribuer des catégories.  



## <a name="detection-methods"></a>Méthodes de détection  

Utilisez cette procédure pour fournir les informations de méthode de détection de l'élément de configuration.  

> [!NOTE]  
> Cette information ne s’applique que si **Cet élément de configuration contient des paramètres d’application** est sélectionné sur la page **Général** de l’Assistant.  

Une méthode de détection dans Configuration Manager contient des règles qui sont utilisées pour déterminer si une application est installée sur un ordinateur. Cette détection se produit avant que le client évalue sa conformité pour l’élément de configuration. Pour déterminer si une application est installée, vous pouvez détecter la présence du Windows Installer de l'application, utiliser un script personnalisé ou sélectionner **Toujours partir du principe que l'application est installée** pour évaluer la compatibilité de l'élément de configuration, que l'application soit installée ou non.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>Pour détecter une installation d’application avec le fichier Windows Installer  

1. Sur la page **Méthodes de détection** de **l’Assistant Création d’un élément de Configuration**, sélectionnez l’option **Utiliser la détection Windows Installer**.  

2. Sélectionnez **Ouvrir**, recherchez le fichier Windows Installer (.msi) à détecter, puis sélectionnez **Open**.  

3. Le **Version** champ remplit automatiquement avec le numéro de version du fichier Windows Installer. Si la valeur affichée est incorrecte, entrez un nouveau numéro de version ici.  

4. Pour détecter chacun des profils utilisateur de l’ordinateur, sélectionnez **Cette application est installée pour un ou plusieurs utilisateurs**.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>Pour détecter un type d’application et de déploiement spécifique  

1. Sur la page **Méthodes de détection** de **l’Assistant Création d’un élément de configuration**, sélectionnez **Détecter un type d’application et de déploiement spécifique**. Choisissez **sélectionnez**.   

2. Dans la boîte de dialogue **Spécifier une application** , sélectionnez l’application et un type de déploiement associé à détecter.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>Pour détecter une installation d’application à l’aide d’un script personnalisé  

1. Sur la page **Méthodes de détection** de **l’Assistant Création d’un élément de Configuration**, sélectionnez l’option **Utiliser un script personnalisé pour détecter cette application**.  

2. Dans la liste, sélectionnez la langue du script. Choisissez l’un des formats suivants :  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Depuis la version 1810, quand un script Windows PowerShell s’exécute comme une méthode de détection, le client Configuration Manager appelle PowerShell avec le `-NoProfile` paramètre. Cette option démarre PowerShell sans aucun profil. Un profil PowerShell est un script qui s’exécute au démarrage de PowerShell. <!--3607762-->  

3. Sélectionnez **Ouvrir**, accédez au script à utiliser, puis sélectionnez **Ouvrir**.  



##  <a name="specify-supported-platforms"></a>Spécifier les plateformes prises en charge  

Sur la page **Plateformes prises en charge** de **l’Assistant Création d’un élément de configuration**, sélectionnez les versions de Windows sur lesquelles vous voulez évaluer la conformité de l’élément de configuration, ou choisissez **Tout sélectionner**. 

Il est également possible de **Spécifier manuellement la version de Windows**. Sélectionnez **ajouter** et spécifiez le numéro de build de chaque partie de la Windows. 



##  <a name="configure-settings"></a>Configurer les paramètres  

Utilisez cette procédure pour configurer les paramètres dans l'élément de configuration.  

Représentent les paramètres de l'entreprise ou critères techniques sont utilisées pour évaluer la conformité des périphériques clients. Vous pouvez configurer un nouveau paramètre ou accéder à un paramètre existant sur un ordinateur de référence.  

1. Sur la page **Paramètres** de **l’Assistant Création d’un élément de configuration**, sélectionnez **Nouveau**.  

2. Sur l'onglet **Général** de la boîte de dialogue **Créer un paramètre** , fournissez les informations suivantes :  

    - **Nom** : donnez un nom unique au paramètre. Vous pouvez utiliser jusqu'à 256 caractères.  

    - **Description** : entrez la description du paramètre. Vous pouvez utiliser jusqu'à 256 caractères.  

    - **Type de paramètre** : choisissez l’un des types de paramètres de la liste suivante et configurez-le de façon à l’utiliser pour ce paramètre :  
        - [Requête Active Directory](#bkmk_adquery)
        - [Assembly](#bkmk_assembly)
        - [Système de fichiers](#bkmk_file)
        - [Métabase IIS](#bkmk_iis)
        - [Clé du Registre](#bkmk_regkey)
        - [Valeur de Registre](#bkmk_regval)
        - [Script](#bkmk_script)
        - [Requête SQL](#bkmk_sql)
        - [Requête WQL](#bkmk_wql)
        - [Requête XPath](#bkmk_xpath)

    - **Type de données** : choisissez le format dans lequel la condition retourne les données avant de les utiliser pour évaluer le paramètre. La liste **Type de données** ne s’affiche pas pour tous les types de paramètres.  

        > [!Tip]  
        > Le type de données **Virgule flottante** ne gère que trois chiffres après la virgule décimale.  

3. Configurer des détails supplémentaires sur ce paramètre sous la **définition de type** liste. Les éléments configurables dépendent du type de paramètre sélectionné.  

4. Sélectionnez **OK** pour enregistrer le paramètre et fermer la boîte de dialogue **Créer un paramètre**.  


### <a name="bkmk_adquery"></a> Requête Active Directory

- **Préfixe LDAP** : indiquez un préfixe valide permettant à la requête Active Directory Domain Services d’évaluer la conformité sur les ordinateurs clients. Pour effectuer une recherche de catalogue global, utilisez `LDAP://` ou `GC://`.  

- **Nom unique** : indiquez le nom unique de l’objet Active Directory Domain Services dont la conformité est évaluée sur les ordinateurs clients.  

- **Filtre de recherche** : indiquez un filtre LDAP facultatif permettant d’affiner les résultats de la requête Active Directory Domain Services pour évaluer la conformité sur les ordinateurs clients. Pour renvoyer tous les résultats de la requête, entrez `(objectclass=*)`.  

- **Zone de recherche** : indiquez l’étendue de recherche dans Active Directory Domain Services :  

    - **Base** : interroge uniquement l’objet spécifié.  

    - **Un niveau** : cette option n’est pas utilisée dans cette version de Configuration Manager.  

    - **Sous-arborescence** : interroge l’objet spécifié et la totalité de sa sous-arborescence dans le répertoire.  

- **Propriété** : indiquez la propriété de l’objet Active Directory Domain Services utilisé pour évaluer la conformité sur les ordinateurs clients.  

    Par exemple, pour interroger la propriété Active Directory qui stocke le nombre de saisies incorrectes du mot de passe par un utilisateur, entrez `badPwdCount` dans ce champ.  

- **Requête** : affiche la requête créée à partir des entrées **Préfixe LDAP**, **Nom unique**, **Filtre de recherche** (s’il est défini) et **Propriété**.  


### <a name="bkmk_assembly"></a> Assembly

Un assembly est un fragment de code qui peut être partagé entre plusieurs applications. Les assemblys peuvent comporter l'extension de fichier .dll ou .exe. Le global assembly cache est le dossier `%SystemRoot%\Assembly` sur les ordinateurs clients. Ce cache est l’emplacement où Windows stocke tous les assemblys partagés.  

- **Nom de l'assembly :** Spécifie le nom de l'objet de l'assembly que vous souhaitez rechercher. Le nom ne peut pas être le même que les autres objets assembly du même type. Tout d’abord l’inscrire dans le global assembly cache. Le nom de l'assembly peut comporter jusqu'à 256 caractères.  


### <a name="bkmk_file"></a> Système de fichiers

- **Type** : indiquez dans la liste si vous voulez rechercher un **Fichier** ou un **Dossier**.  

- **Chemin** : indiquez le chemin d’accès du fichier ou du dossier spécifié sur les ordinateurs clients. Vous pouvez spécifier des variables d'environnement système et la variable d'environnement `%USERPROFILE%` dans le chemin.  

    > [!NOTE]  
    > Si vous utilisez le `%USERPROFILE%` variable d’environnement dans le **chemin d’accès** ou **nom de fichier ou dossier** zones, le client Configuration Manager recherche dans tous les profils utilisateur sur l’ordinateur client. Ce comportement peut entraîner il recherche plusieurs instances du fichier ou du dossier.  
    >   
    > Si les paramètres de conformité n’ont pas accès au chemin spécifié, une erreur de découverte est générée. En outre, si le fichier que vous recherchez est actuellement en cours d'utilisation, une erreur de découverte est générée.  

    > [!Tip]  
    > Sélectionnez **Parcourir** pour configurer le paramètre à partir de valeurs sur un ordinateur de référence.   

- **Nom du fichier ou du dossier** : indiquez le nom de l’objet fichier ou dossier à rechercher. Vous pouvez spécifier des variables d'environnement système et la variable d'environnement `%USERPROFILE%` dans le nom de fichier ou de dossier. Il est également possible d’utiliser les caractères génériques `*` et `?` dans le nom de fichier.  

    > [!NOTE]  
    > Si vous spécifiez un nom de fichier ou de dossier avec des caractères génériques, la combinaison risque de produire de nombreux résultats, ou d’engendrer une utilisation élevée des ressources sur l’ordinateur client et une augmentation du trafic réseau lors de la transmission des résultats à Configuration Manager.  

- **Inclure les sous-dossiers**: également rechercher tous les sous-dossiers sous le chemin d’accès spécifié.  

- **Ce fichier ou dossier est associé à une application 64 bits**: si activé, uniquement rechercher les emplacements de fichiers 64 bits tel que `%ProgramFiles%` sur les ordinateurs 64 bits. Si cette option n’est pas activée, une recherche les emplacements 64 bits et 32 bits emplacements telles que `%ProgramFiles(x86)%`.  

    > [!NOTE]  
    > Si le même fichier ou dossier existe dans les emplacements de systèmes de fichiers 64 bits et 32 bits sur le même ordinateur 64 bits, la condition globale détecte plusieurs fichiers.  

    Le type de paramètre **Système de fichiers** ne permet pas de spécifier un chemin d’accès UNC à un partage réseau dans la zone **Chemin**.  


### <a name="bkmk_iis"></a> Métabase IIS

- **Chemin de la métabase** : indiquez un chemin d’accès valide à la métabase Internet Information Services (IIS). Par exemple, `/LM/W3SVC/`.  

- **ID de propriété** : indiquez la propriété numérique du paramètre de la métabase IIS.  


### <a name="bkmk_regkey"></a> Clé de Registre

- **Hive**: sélectionnez la ruche du Registre que vous souhaitez rechercher

    > [!Tip]  
    > Sélectionnez **Parcourir** pour configurer le paramètre à partir de valeurs sur un ordinateur de référence. Pour accéder à une clé de Registre sur un ordinateur distant, vous devez activer le **Registre distant** service sur l’ordinateur distant.  

- **Clé** : indiquez le nom de la clé de Registre à rechercher. Utilisez le format `key\subkey`.  

- **Cette clé de Registre est associée à une application 64 bits** : recherchez les clés de Registre 64 bits en plus des clés de Registre 32 bits sur les clients qui utilisent une version 64 bits de Windows.  

    > [!NOTE]  
    > Si la même clé de Registre existe dans les emplacements de Registre 64 bits et 32 bits sur un même ordinateur 64 bits, les deux clés de Registre sont détectées par la condition globale.  


### <a name="bkmk_regval"></a> Valeur de Registre

- **Hive**: sélectionnez la ruche du Registre à rechercher.  

    > [!Tip]  
    > Sélectionnez **Parcourir** pour configurer le paramètre à partir de valeurs sur un ordinateur de référence. Pour accéder à une valeur de Registre sur un ordinateur distant, vous devez activer le **Registre distant** service sur l’ordinateur distant. Vous devez également des autorisations d’administrateur pour accéder à l’ordinateur distant.  

- **Clé**: spécifiez le nom de clé de Registre à rechercher. Utilisez le format `key\subkey`.  

- **Valeur** : indiquez la valeur qui doit être contenue dans la clé de Registre spécifiée.  

- **Cette clé de Registre est associée à une application 64 bits** : recherchez les clés de Registre 64 bits en plus des clés de Registre 32 bits sur les clients qui utilisent une version 64 bits de Windows.  

    > [!NOTE]  
    > Si la même clé de Registre existe dans les emplacements de Registre 64 bits et 32 bits sur un même ordinateur 64 bits, les deux clés de Registre sont détectées par la condition globale.  


### <a name="bkmk_script"></a> Script

La valeur renvoyée par le script est utilisée pour évaluer la compatibilité de la condition globale. Par exemple, quand vous utilisez VBScript, vous pouvez utiliser la commande **WScript.Echo Result** pour renvoyer la valeur de la variable *Result* vers la condition globale.  

- **Script de découverte**: sélectionnez **ajouter un Script**, puis entrez ou accédez à un script. Ce script est utilisé pour rechercher la valeur. Vous pouvez utiliser des scripts Windows PowerShell, VBScript ou Microsoft JScript.  

- **Script de correction (facultatif)**: sélectionnez **ajouter un Script**, puis entrez ou accédez à un script. Ce script est utilisé pour corriger les valeurs de paramètre non conforme. Vous pouvez utiliser des scripts Windows PowerShell, VBScript ou Microsoft JScript.  

- **Exécuter des scripts avec les informations d’identification de l’utilisateur connecté** : si cette option est activée, le script s’exécute sur les ordinateurs clients qui utilisent les informations d’identification de l’utilisateur connecté.  

> [!Note]  
> Depuis la version 1810, lorsque vous utilisez Windows PowerShell en tant qu’un script de découverte ou la mise à jour, le client Configuration Manager appelle PowerShell avec le `-NoProfile` paramètre. Cette option démarre PowerShell sans aucun profil. Un profil PowerShell est un script qui s’exécute au démarrage de PowerShell. <!--3607762-->  


### <a name="bkmk_sql"></a> Requête SQL

- **Instance SQL Server** : indiquez si vous préférez que la requête SQL soit exécutée sur l’instance par défaut, sur toutes les instances ou sur une instance de base de données portant un nom spécifique.  

    > [!NOTE]  
    > Le nom de l'instance doit faire référence à une instance locale de SQL Server. Pour faire référence à une instance SQL Server en cluster, utilisez plutôt un paramètre de script.  

- **Base de données** : indiquez le nom de la base de données Microsoft SQL Server sur laquelle vous souhaitez exécuter la requête SQL.  

- **Colonne** : indiquez le nom de colonne retourné par l’instruction Transact-SQL utilisée pour évaluer la conformité de la condition globale.  

- **Instruction Transact-SQL** : indiquez la requête SQL complète à utiliser pour la condition globale. Pour utiliser une requête SQL existante, sélectionnez **Open**.  

    > [!IMPORTANT]  
    > Les paramètres de requête SQL ne prennent pas en charge les commandes SQL qui modifient la base de données. Vous pouvez uniquement utiliser les commandes SQL qui lisent des informations à partir de la base de données.  


### <a name="bkmk_wql"></a> Requête WQL

- **Namespace**: spécifiez l’espace de noms WMI qui est évaluée pour la conformité sur les ordinateurs clients. La valeur par défaut est `root\cimv2`.  

- **Classe**: spécifier la cible de classe WMI dans l’espace de noms ci-dessus.  

- **Propriété**: spécifiez la propriété WMI cible dans la classe ci-dessus.  

- **Clause WHERE de la requête WQL**: spécifiez une clause qualifiante pour réduire les résultats. Par exemple, pour interroger uniquement le service DHCP dans la classe Win32_Service, la clause WHERE peut être `Name = 'DHCP' and StartMode = 'Auto'`.   


### <a name="bkmk_xpath"></a> Requête XPath

- **Chemin** : indiquez le chemin sur les ordinateurs clients du fichier .xml utilisé pour évaluer la conformité. Configuration Manager prend en charge toutes les variables d’environnement système Windows et de la variable utilisateur `%USERPROFILE%` dans le nom de chemin.  

- **Nom du fichier XML**: spécifiez le nom de fichier contenant la requête XML dans le chemin d’accès ci-dessus.  

- **Inclure les sous-dossiers** : activez cette option pour effectuer la recherche dans les sous-dossiers du chemin spécifié.  

- **Ce fichier est associé à une application 64 bits**: rechercher l’emplacement du fichier système 64 bits `%Windir%\System32` en plus de l’emplacement du fichier système 32 bits `%Windir%\Syswow64` sur les clients Configuration Manager qui exécutent une version 64 bits de Windows.  

- **Requête XPath**: spécifier une valide complet requête XML path language (XPath).  

- **Espaces de noms**: identifier les espaces de noms et préfixes à utiliser lors de la requête XPath.  

Si vous tentez de détecter un fichier .xml chiffré, les paramètres de conformité trouvent le fichier, mais la requête XPath ne produit aucun résultat. Le client Configuration Manager ne génère une erreur.  

Si la requête XPath n’est pas valide, le paramètre est évalué comme étant non conforme sur les ordinateurs clients.  



##  <a name="configure-compliance-rules"></a>Configurer des règles de compatibilité  

Les règles de compatibilité spécifient les critères qui définissent la compatibilité d'un élément de configuration. Avant que la compatibilité d'un paramètre puisse être évaluée, celui-ci doit comporter au moins une règle de compatibilité. WMI, Registre et les paramètres de script vous permettent de corriger les valeurs qui sont identifiés comme étant non conforme. Vous pouvez créer de nouvelles règles ou accédez à un paramètre existant dans n'importe quel élément de configuration pour sélectionner les règles qu'il contient.  


### <a name="to-create-a-compliance-rule"></a>Pour créer une règle de compatibilité  

1. Sur la page **Règles de conformité** de **l’Assistant Création d’un élément de configuration**, sélectionnez **Nouveau**.  

2. Dans la boîte de dialogue **Créer une règle** , indiquez les informations suivantes :  

    - **Nom** : donnez un nom à la règle de conformité.  

    - **Description** : entrez la description de la règle de conformité.  

    - **Paramètre sélectionné** : sélectionnez **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner le paramètre**. Sélectionnez le paramètre pour lequel vous souhaitez définir une règle ou bien **Nouveau paramètre**. Lorsque vous avez terminé, choisissez **sélectionnez**.  

        > [!Tip]  
        > Pour afficher des informations sur le paramètre actuellement sélectionné, sélectionnez **propriétés**.  

    - **Type de règle**: Sélectionnez le type de règle de compatibilité que vous souhaitez utiliser :  

        - **Valeur** : créez une règle qui compare la valeur retournée par l’élément de configuration à une valeur spécifiée. Pour plus d’informations sur les paramètres supplémentaires, consultez [valeur règles](#bkmk_value).  

        - **Existentiel** : créez une règle qui évalue la présence du paramètre sur un appareil client ou bien le nombre d’occurrences. Pour plus d’informations sur les paramètres supplémentaires, consultez [Existentiels règles](#bkmk_exist).  

3. Sélectionnez **OK** pour fermer la boîte de dialogue **Créer une règle**.  




### <a name="bkmk_value"></a> Règles de valeur  

- **Propriété**: la propriété de l’objet à vérifier varie en fonction du paramètre sélectionné. Les propriétés disponibles varient en fonction du type de paramètre. 

- **Le paramètre doit être compatible avec les éléments suivants...** : Les règles disponibles ou les autorisations varient en fonction du type de paramètre.

- **Corriger les règles non conformes prises en charge** : sélectionnez cette option pour que Configuration Manager corrige automatiquement les règles non conformes. Configuration Manager prend en charge cette action avec les types de règles suivants :  

    - **Valeur de Registre**: si elle n’est pas conforme, le client définit la valeur de Registre. S’il n’existe pas, le client crée la valeur.  

    - **Script**: le client utilise le script de mise à jour que vous avez spécifié avec le paramètre.  

    - **Requête WQL**  

    > [!IMPORTANT]  
    > Vous ne pouvez corriger que les règles non compatibles lorsque l'opérateur de règle est défini sur **Égal à**.  

- **Signaler la non-compatibilité si l’instance de ce paramètre n’est pas trouvée**: Si ce paramètre n’est pas disponible sur les ordinateurs clients, activez cette option pour l’élément de configuration signaler une non-conformité.  

- **Gravité de non-conformité pour les rapports** : indiquez le niveau de gravité signalé dans les rapports Configuration Manager si cette règle de conformité échoue. Les niveaux de gravité suivants sont disponibles :  
    - **Aucun**  
    - **Information**  
    - **Avertissement**  
    - **Critique**  
    - **Critique avec événement** : les ordinateurs non conformes à cette règle signalent une gravité d’échec **Critique**. Ce niveau de gravité est également enregistré comme un événement Windows dans le journal des événements des applications.  


### <a name="bkmk_exist"></a> Règles existentiels 

> [!NOTE]  
> Les options affichées peuvent varier selon le type de paramètre pour lequel la règle est configurée.  

- **Le paramètre doit exister sur les appareils clients**  

- **Le paramètre ne doit pas exister sur les appareils clients**  

- **Le paramètre se produit le nombre de fois suivant :**  

- **Gravité de non-conformité pour les rapports** : indiquez le niveau de gravité signalé dans les rapports Configuration Manager si cette règle de conformité échoue. Les niveaux de gravité suivants sont disponibles :  
    - **Aucun**  
    - **Information**  
    - **Avertissement**  
    - **Critique**  
    - **Critique avec événement** : les ordinateurs non conformes à cette règle signalent une gravité d’échec **Critique**. Ce niveau de gravité est également enregistré comme un événement Windows dans le journal des événements des applications.  



## <a name="next-steps"></a>Étapes suivantes

[Créer des bases de référence de configuration](/sccm/compliance/deploy-use/create-configuration-baselines)
