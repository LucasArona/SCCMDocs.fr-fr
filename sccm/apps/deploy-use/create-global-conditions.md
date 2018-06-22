---
title: Créer des conditions globales
titleSuffix: Configuration Manager
description: Créez des conditions globales pour spécifier la manière dont une application est fournie et déployée sur les appareils clients.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: dac47f55a1ad0d287e789d555d2f0a93b40f9376
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32335675"
---
# <a name="how-to-create-global-conditions-in-system-center-configuration-manager"></a>Comment créer des conditions globales dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, les conditions globales sont des règles qui représentent des conditions commerciales ou techniques pouvant être utilisées pour spécifier la manière dont une application est fournie et déployée sur les appareils clients. Les conditions globales sont accessibles à la page **Spécifications** de l’Assistant Création d’un type de déploiement.  

> [!NOTE]  
>  Vous pouvez modifier les conditions globales uniquement à partir du site où elles ont été créées.  

 Utilisez les procédures suivantes pour créer des conditions globales Configuration Manager.  

## <a name="provide-basic-information-about-the-global-condition"></a>Fournir des informations de base sur la condition globale  
 Différents types de conditions globales sont à votre disposition. À chacun de ces types sont associées des options spécifiques. Quand vous sélectionnez un type de condition globale spécifique, Configuration Manager affiche les options qui s’appliquent à votre sélection.  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Conditions globales**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une condition globale**.  

4.  Dans la boîte de dialogue **Créer une condition globale** , indiquez le nom et la description facultative de la condition globale.  

5.  Dans la liste déroulante **Type d’appareil**, choisissez si la condition globale est destinée à un ordinateur **Windows** ou un appareil **Windows Mobile**.  

6.  Dans la liste déroulante **Type de condition** , choisissez l'une des options suivantes :  

    -   **Paramètre** : cette option vérifie l'existence d'un ou plusieurs éléments supplémentaires sur des périphériques clients. Vous pouvez, par exemple, vérifier l’existence d’un fichier, d’un dossier ou d’une clé de Registre sur un appareil client.  

    -   **Expression** : Cette option vous permet de configurer des règles plus complexes pour vérifier que la condition est satisfaite sur des appareils clients. Par exemple, vous pouvez savoir si la mémoire physique d’un ordinateur est comprise entre 2 Go et 4 Go ou si un appareil mobile possède un écran tactile pour la saisie.  

## <a name="set-up-rules-for-the-global-condition"></a>Configurer des règles pour la condition globale  
 La procédure pour définir les règles d’une condition globale est différente selon que vous configurez un paramètre ou une expression. Utilisez la procédure adéquate ci-dessous pour configurer le paramètre ou l’expression d’une condition globale.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>Pour configurer un paramètre pour la condition globale  

1.  Dans la liste déroulante **Type de condition** , choisissez **Paramètre**.  

2.  Dans la liste déroulante **Type de paramètre** , choisissez l'élément que vous souhaitez utiliser comme condition à vérifier. Les configurations et types de paramètres suivants sont disponibles.  

    -   **Requête Active Directory**  

        -   **Préfixe LDAP** : désigne un préfixe LDAP valide pour la requête des services de domaine Active Directory afin d'évaluer la compatibilité sur les ordinateurs clients. Vous pouvez utiliser **LDAP://** ou **GC://**.  

        -   **Nom unique** : Spécifiez le nom unique de l’objet Services de domaine Active Directory dont la compatibilité doit être évaluée sur les ordinateurs clients.  

        -   **Filtre de recherche** : indique le filtre LDAP facultatif permettant d'affiner les résultats de la requête Services de domaine Active Directory pour évaluer la compatibilité sur les ordinateurs clients.  

        -   **Zone de recherche** : indique la zone de recherche dans les services de domaine Active Directory :  

            -   **Base** : Interroge uniquement l’objet spécifié.  

            -   **Un niveau** : cette option n’est pas utilisée dans cette version de Configuration Manager.  

            -   **Sous-arbre** : Interroge l’objet spécifié et son sous-arbre dans le répertoire.  

        -   **Propriété** : désigne la propriété de l'objet Services de domaine Active Directory à utiliser pour évaluer la compatibilité sur les ordinateurs clients.  

        -   **Requête** : Affiche la requête LDAP créée à partir des entrées figurant dans **Préfixe LDAP**, **Nom unique**, **Filtre de recherche** (s’il est défini) et **Propriété**. Cette requête sera utilisée pour évaluer la compatibilité des ordinateurs clients.  

    -   **Assembly**  

        -   **Nom de l’assembly** : indique le nom de l’objet assembly à rechercher. Ce nom doit être différent des autres objets assembly de même type et doit être enregistré dans le GAC (Global Assembly Cache). Le nom de l’assembly ne doit pas contenir plus de 256 caractères.  

        > [!NOTE]  
        >  Un assembly est un fragment de code qui peut être partagé entre plusieurs applications. Les assemblys peuvent avoir l’extension de nom de fichier .dll ou .exe. Le GAC (Global Assembly Cache) est un dossier présent sur les ordinateurs clients, qui porte le nom *%systemroot%\assembly* . Il contient l'ensemble des assemblys partagés.  

    -   **Système de fichiers**  

        -   **Type** : Dans la liste déroulante, indiquez si vous voulez rechercher un **fichier** ou un **dossier**.  

        -   **Chemin** : spécifie le chemin du fichier ou du dossier spécifié sur les ordinateurs clients. Vous pouvez spécifier des variables d'environnement système et la variable d'environnement *%USERPROFILE%* dans le chemin.  

            > [!NOTE]  
            >  Si vous utilisez la variable d'environnement *%USERPROFILE%* dans les champs **Chemin d'accès** ou **Nom de fichier ou de dossier** , la recherche portera sur tous les profils utilisateur stockés sur l'ordinateur client. Dans ce cas, plusieurs instances du fichier ou du dossier peuvent être découvertes.  

        -   **Nom de fichier ou de dossier** : spécifiez le nom de l'objet fichier ou dossier à rechercher. Vous pouvez spécifier des variables d'environnement système et la variable d'environnement *%USERPROFILE%* dans le nom de fichier ou de dossier. Vous pouvez également utiliser les caractères génériques * et ? dans le nom du fichier.  

            > [!NOTE]  
            >  Si vous spécifiez un nom de fichier ou de dossier et utilisez des caractères génériques, vous risquez de générer de nombreux résultats, ce qui peut entraîner une forte utilisation des ressources sur l’ordinateur client et une augmentation du trafic réseau lors de la transmission des résultats à Configuration Manager.  

        -   **Inclure les sous-dossiers** : activez cette option si vous voulez également effectuer la recherche dans les sous-dossiers dans le chemin spécifié.  

        -   **Ce fichier ou dossier est associé à une application 64 bits** : indiquez si la recherche doit porter également sur l’emplacement de fichier système 64 bits (*%windir%* \system32) en plus de l’emplacement de fichier système 32 bits (*%windir%* \syswow64) sur les clients Configuration Manager qui exécutent une version 64 bits de Windows.  

            > [!NOTE]  
            >  Si le même fichier ou dossier existe dans les emplacements de système de fichiers 64 bits et 32 bits sur un même ordinateur 64 bits, la condition globale détecte plusieurs fichiers.  

         Le paramètre **Système de fichiers** ne permet pas de définir un chemin UNC de partage réseau dans le champ **Chemin d'accès** .  

    -   **Métabase IIS**  

        -   **Chemin de la métabase** : spécifiez un chemin d'accès valide à la métabase IIS.  

        -   **ID de propriété** : indique la propriété numérique du paramètre Métabase IIS.  

    -   **Clé du Registre**  

        -   **Ruche** : Dans la liste déroulante, sélectionnez la ruche du Registre dans laquelle vous voulez effectuer la recherche.  

        -   **Clé** : indiquez le nom de clé de Registre à rechercher. Le format à utiliser doit être *clé\sous-clé.*  

        -   **Cette clé de Registre est associée à une application 64 bits** : indique si la recherche doit porter sur les clés de Registre 64 bits en plus des clés de Registre 32 bits, sur les clients qui exécutent une version 64 bits de Windows.  

            > [!NOTE]  
            >  Si la même clé de Registre existe dans les emplacements de Registre 64 bits et 32 bits sur un même ordinateur 64 bits, les deux clés de Registre sont détectées par la condition globale.  

    -   **Valeur de Registre**  

        -   **Ruche** : dans la liste déroulante, sélectionnez la ruche du Registre dans laquelle vous voulez effectuer la recherche.  

        -   **Clé** : indiquez le nom de clé de Registre à rechercher. Le format à utiliser doit être *clé\sous-clé.*  

        -   **Valeur** : indiquez la valeur qui doit être contenue dans la clé de Registre spécifiée.  

        -   **Cette clé de Registre est associée à une application 64 bits** : indique si la recherche doit porter sur les clés de Registre 64 bits en plus des clés de Registre 32 bits, sur les clients qui exécutent une version 64 bits de Windows.  

            > [!NOTE]  
            >  Si la même clé de Registre existe dans les emplacements de Registre 64 bits et 32 bits sur un même ordinateur 64 bits, les deux clés de Registre sont détectées par la condition globale.  

    -   **Script**  

        -   **Script de découverte** : Choisissez **Ajouter** pour entrer ou rechercher le script à utiliser. Vous pouvez utiliser des scripts Windows PowerShell, VBScript ou JScript.  

        -   **Exécuter des scripts avec les informations d’identification d’utilisateur dont la session est ouverte** : Si vous activez cette option, le script est exécuté sur les ordinateurs clients en utilisant les informations d’identification de l’utilisateur connecté.  

            > [!NOTE]  
            >  La valeur renvoyée par le script sera utilisée pour évaluer la compatibilité de la condition globale. Par exemple, quand vous utilisez VBScript, vous pouvez utiliser la commande **WScript.Echo Result** pour retourner la valeur de la variable de résultat à la condition globale.  
            >   
            >  Si votre script retourne plusieurs valeurs, celles-ci doivent être sur une seule ligne, séparées par un point-virgule. Si chaque valeur se trouve sur une ligne distincte, l’évaluation échoue.  

    -   **Requête SQL**  

        -   **Instance SQL Server** : indiquez si vous préférez que la requête SQL soit exécutée sur l'instance par défaut, sur toutes les instances ou sur le nom d'une instance de base de données spécifique.  

            > [!NOTE]  
            >  Le nom de l'instance doit faire référence à une instance locale de SQL Server. Pour faire référence à une instance SQL Server en cluster, utilisez plutôt un paramètre de script.  

        -   **Base de données** : indiquez le nom de la base de données Microsoft SQL Server sur laquelle la requête SQL sera exécutée.  

        -   **Colonne** : indiquez le nom de la colonne renvoyée par l'instruction Transact-SQL utilisée pour évaluer la compatibilité de la condition globale.  

        -   **Instruction Transact-SQL** : indiquez la requête SQL complète à utiliser pour la condition globale. Vous pouvez également choisir **Ouvrir** pour ouvrir une requête SQL existante.  

    -   **Requête WQL**  

        -   **Espace de noms** : indiquez l'espace de noms WMI qui sera utilisé pour créer une requête WQL dont la compatibilité sera évaluée sur les ordinateurs clients. La valeur par défaut est Root\cimv2.  

        -   **Classe** : indique la classe WMI qui sera utilisée pour créer une requête WQL dont la compatibilité sera évaluée sur les ordinateurs clients.  

        -   **Propriété** : indique la propriété WMI qui sera utilisée pour créer une requête WQL dont la compatibilité sera évaluée sur les ordinateurs clients.  

        -   **Clause WHERE de la requête WQL** : vous pouvez utiliser l'élément **Clause WHERE de la requête WQL** pour indiquer la clause WHERE à appliquer à l'espace de noms, à la classe et à la propriété spécifiés sur les ordinateurs clients.  

    -   **Requête XPath**  

        -   **Chemin** : spécifiez le chemin d'accès au fichier XML sur les ordinateurs clients qui seront utilisés pour évaluer la conformité. Configuration Manager prend en charge l’utilisation de toutes les variables d’environnement système Windows et de la variable utilisateur *%USERPROFILE%* dans le nom de chemin.  

        -   **Nom du fichier XML** : Spécifiez le nom du fichier contenant la requête XML à utiliser pour évaluer la conformité des ordinateurs clients.  

        -   **Inclure les sous-dossiers** : activez cette option si vous voulez également rechercher dans tous les sous-dossiers sous le chemin spécifié.  

        -   **Ce fichier est associé à une application 64 bits** : indiquez si la recherche doit porter également sur l’emplacement de fichier système 64 bits (*%windir%* \system32) en plus de l’emplacement de fichier système 32 bits (*%windir%* \syswow64) sur les clients Configuration Manager qui exécutent une version 64 bits de Windows.  

        -   **Requête XPath** : spécifiez une requête XPath (XML path language) complète et valide à utiliser pour évaluer la compatibilité des ordinateurs clients.  

        -   **Espaces de noms** : ouvre la boîte de dialogue **Espaces de noms XML** , qui permet d'identifier les espaces de noms et les préfixes à utiliser dans le cadre de la requête XPath.  

3.  Dans la liste déroulante **Type de données** , choisissez le format auquel les données seront renvoyées par cette condition avant d'être utilisées pour vérifier les exigences.  

    > [!NOTE]  
    >  La liste déroulante **Type de données** n’est pas affichée pour tous les types de paramètre.  

4.  Configurez davantage de détails sur ce paramètre sous la liste déroulante **Type de paramètre** . Les éléments que vous pouvez configurer varient selon le type de paramètre que vous avez sélectionné.  

5.  Choisissez **OK** pour enregistrer la règle et fermer la boîte de dialogue **Créer une condition globale**.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Configurer une expression pour la condition globale  

1.  Dans la liste déroulante **Type de condition** , choisissez **Expression**.  

2.  Choisissez **Ajouter une clause** pour ouvrir la boîte de dialogue **Ajouter une clause**.  

3.  À l'aide de la liste déroulante **Sélectionnez une catégorie** , indiquez si cette expression s'applique à un périphérique ou à un utilisateur. Vous pouvez également sélectionner **Personnalisée** pour utiliser une condition globale configurée précédemment.  

4.  Dans la liste déroulante **Sélectionner une condition** , sélectionnez la condition à utiliser pour évaluer si l'utilisateur ou le périphérique respecte les règles. Le contenu de cette liste varie en fonction de la catégorie sélectionnée.  

5.  Dans la liste déroulante **Choisir un opérateur** , choisissez l'opérateur qui sera utilisé pour comparer la condition sélectionnée à la valeur spécifiée, afin d'évaluer si l'utilisateur ou le périphérique répond aux exigences des règles. Les opérateurs disponibles varient en fonction de la condition sélectionnée.  

6.  Dans le champ **Valeur** , spécifiez les valeurs qui seront utilisées avec la condition et l'opérateur sélectionnés pour évaluer si l'utilisateur ou le périphérique respecte les règles. Les valeurs disponibles varient en fonction de la condition et de l'opérateur sélectionnés.  

7.  Choisissez **OK** pour enregistrer l’expression et fermer la boîte de dialogue **Ajouter une clause**.  

8.  Quand vous avez terminé d’ajouter des clauses à la condition globale, choisissez **OK** pour fermer la boîte de dialogue **Créer une condition globale** et enregistrer la condition globale.  
