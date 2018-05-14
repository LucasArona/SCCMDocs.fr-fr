---
title: Créer et exécuter des scripts
titleSuffix: Configuration Manager
description: Créez et exécutez des scripts Powershell sur les appareils clients.
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fcf3bc335efc4c7436842b29d30c67c118ceb05d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1236459-->
System Center Configuration Manager a la capacité intégrée d’exécuter des scripts PowerShell. Powershell a l’avantage de créer des scripts automatisés et sophistiqués, qui sont compris et partagés par une large communauté. Les scripts simplifient la création d’outils personnalisés pour administrer des logiciels et vous permettent d’accomplir des tâches courantes rapidement, plus facilement et de façon plus cohérente.  

> [!TIP]  
> Cette fonctionnalité a été introduite dans la version 1706 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1802, cette fonctionnalité n’est plus en préversion.  


> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  


Avec cette intégration dans System Center Configuration Manager, vous pouvez utiliser la fonctionnalité *Exécuter les scripts* pour effectuer les opérations suivantes :

- Créer et modifier des scripts à utiliser avec System Center Configuration Manager.
- Gérer l’utilisation des scripts par le biais de rôles et d’étendues de sécurité. 
- Exécuter des scripts sur des regroupements des PC Windows individuels gérés localement.
- Obtenir des résultats de script agrégés rapides des appareils clients.
- Surveiller l’exécution des scripts et afficher les résultats de la création de rapports à partir de la sortie des scripts.

>[!WARNING]
>Étant donné la puissance des scripts, nous vous rappelons de les utiliser avec précaution. Nous avons intégré des protections supplémentaires pour vous aider, à savoir des rôles et des étendues séparés. Vérifiez que les scripts sont exacts avant de les exécuter, puis confirmez qu’ils proviennent d’une source approuvée pour empêcher l’exécution involontaire de scripts. Soyez attentif aux caractères étendus ou toute autre obfuscation et informez-vous sur la sécurisation des scripts. [En savoir plus sur la sécurité des scripts PowerShell](/sccm/apps/deploy-use/learn-script-security)

## <a name="prerequisites"></a>Prérequis

- Pour exécuter des scripts PowerShell, le client doit exécuter PowerShell version 3.0 ou ultérieure. Toutefois, si un script que vous exécutez contient des fonctionnalités d’une version ultérieure de PowerShell, le client sur lequel vous exécutez le script doit exécuter cette version de PowerShell.
- Les clients Configuration Manager doivent exécuter le client à partir de la version Release 1706 ou ultérieure pour exécuter des scripts.
- Pour utiliser des scripts, vous devez être membre du rôle de sécurité Configuration Manager approprié.
- Pour importer et créer des scripts, votre compte doit avoir des autorisations **Créer** pour les **scripts SMS**.
- Pour approuver ou refuser des scripts, votre compte doit avoir des autorisations **Approuver** pour les **scripts SMS**.
- Pour exécuter des scripts, votre compte doit avoir les autorisations **Exécuter le script** pour les **Regroupements**.

Pour plus d’informations sur les rôles de sécurité Configuration Manager :</br>
[Étendues de sécurité pour exécuter des scripts](#BKMK_Scopes)</br>
[Rôles de sécurité pour exécuter des scripts](#BKMK_ScriptRoles)</br>
[Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration).

## <a name="limitations"></a>Limitations

La fonctionnalité Exécuter les scripts prend actuellement en charge :

- Langages de script : PowerShell
- Types de paramètres : entier, chaîne et liste


>[!WARNING]
>Notez bien que quand vous utilisez des paramètres, elle ouvre une surface d’exposition à des risques potentiels d’attaque par injection de code PowerShell. Plusieurs moyens de limitation et de contournement existent, comme utiliser des expressions régulières pour valider l’entrée des paramètres ou utiliser des paramètres prédéfinis. Une bonne pratique courante est de ne pas inclure de secrets dans vos scripts PowerShell (pas de mots de passe, etc.). [En savoir plus sur la sécurité des scripts PowerShell](/sccm/apps/deploy-use/learn-script-security) <!--There are external tools available to validate your PowerShell scripts such as the [PowerShell Injection Hunter](https://www.powershellgallery.com/packages/InjectionHunter/1.0.0) tool. -->


## <a name="run-script-authors-and-approvers"></a>Auteurs et approbateurs de scripts

La fonctionnalité Exécuter les scripts utilise les concepts d’*auteur de script* et d’*approbateur de script* comme rôles distincts pour l’implémentation et l’exécution d’un script. La distinction des rôles d’auteur et d’approbateur permet à l’outil puissant qu’est la fonctionnalité Exécuter les scripts de bénéficier d’un contrôle de processus important. Il existe un autre rôle *d’exécuteurs de script* qui permet l’exécution de scripts, mais pas la création ou l’approbation de scripts. Consultez [Créer des rôles de sécurité pour les scripts](#BKMK_ScriptRoles).

### <a name="scripts-roles-control"></a>Contrôle des rôles des scripts

Par défaut, les utilisateurs ne peuvent pas approuver un script qu'ils ont créé. Étant donné que les scripts sont puissants et flexibles, et qu’ils peuvent potentiellement être déployés sur de nombreux appareils, vous pouvez séparer les rôles entre la personne qui crée le script et celle qui l’approuve. Ces rôles procurent un niveau supplémentaire de sécurité par rapport à l’exécution d’un script sans supervision. Vous avez la possibilité de désactiver l’approbation secondaire pour faciliter le test.

### <a name="approve-or-deny-a-script"></a>Approuver ou refuser un script

Les scripts doivent être approuvés, par le rôle d’*approbateur de script*, pour pouvoir être exécutés. Pour approuver un script :

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans la liste **Script**, sélectionnez le script que vous souhaitez approuver ou refuser puis, dans l’onglet **Accueil**, sous le groupe **Script**, cliquez sur **Approuver/Refuser**.
4. Dans la boîte de dialogue **Approuver ou refuser le script**, sélectionnez **Approuver** ou **Refuser** pour le script. Entrez éventuellement un commentaire sur votre décision.  Si vous refusez un script, il ne peut pas être exécuté sur les appareils clients. <br>
![Script - Approbation](./media/run-scripts/RS-approval.png)
1. Effectuez toutes les étapes de l'Assistant. Dans la liste **Script**, la colonne **État d’approbation** change en fonction de votre action.

### <a name="allow-users-to-approve-their-own-scripts"></a>Autoriser les utilisateurs à approuver leurs propres scripts

Cette approbation est principalement utilisée pour la phase de test du développement de scripts.

1. Dans la console Configuration Manager, cliquez sur **Administration**.
2. Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**.
3. Dans la liste des sites, sélectionnez votre site, puis, dans l’onglet **accueil**, sous le groupe **Sites**, cliquez sur **Paramètres de hiérarchie**.
4. Dans l’onglet **Général** de la boîte de dialogue **Propriétés des paramètres de hiérarchie**, décochez la case **Ne pas autoriser les auteurs à approuver leurs propres scripts**.

>[!IMPORTANT]
>En tant que bonne pratique, vous ne devriez pas autoriser un auteur de script à approuver ses propres scripts. Ceci ne devrait être autorisé que dans un environnement de laboratoire. Mesurez minutieusement l’impact qu’aurait la modification de ce paramètre dans un environnement de production.

## <a name="security-scopes"></a>Étendues de sécurité
*(Fonctionnalité introduite avec la version 1710)*  
La fonctionnalité Exécuter les scripts utilise des étendues de sécurité, fonctionnalité de Configuration Manager, pour contrôler la création et l’exécution des scripts par le biais d’étiquettes représentant des groupes d’utilisateurs. Pour plus d’informations sur l’utilisation des étendues de sécurité, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="bkmk_ScriptRoles"></a> Créer des rôles de sécurité pour les scripts
Les trois rôles de sécurité utilisés pour exécuter des scripts ne sont pas créés par défaut dans Configuration Manager. Pour créer les rôles d’exécuteurs de scripts, de créateurs de scripts et d’approbateurs de scripts, suivez les étapes indiquées.

1. Dans la console Configuration Manager, accédez à **Administration** >**Sécurité** >**Rôles de sécurité**
2. Cliquez avec le bouton droit sur un rôle, puis cliquez sur **Copier**. Des autorisations sont déjà affectées au rôle que vous copiez. Veillez à ne prendre que les autorisations souhaitées. 
3. Donnez un **Nom** et une **Description** au rôle personnalisé. 
4. Affectez les autorisations décrites ci-dessous au rôle de sécurité.  

### <a name="security-role-permissions"></a>Autorisations du rôle de sécurité  

**Nom du rôle** : Exécuteurs de scripts  
- **Description** : ces autorisations permettent à ce rôle d’exécuter seulement des scripts qui ont été précédemment créés et approuvés par d’autres rôles.  
- **Autorisations :** vérifiez que les éléments suivants sont définis sur **Oui**.  

|Catégorie|Autorisation|État|
|---|---|---|
|Collection|Exécuter un script|Oui|
|Site|Lecture|Oui|
|Scripts SMS|Créer|Oui|
|Scripts SMS|Lecture|Oui|


**Nom du rôle** : Créateurs de scripts  
- **Description** : ces autorisations permettent à ce rôle de créer des scripts, mais pas de les approuver ou de les exécuter.  
- **Autorisations** : vérifiez que les autorisations suivantes sont définies.
 
|Catégorie|Autorisation|État|
|---|---|---|
|Collection|Exécuter un script|Non|
|Site|Lecture|Oui|
|Scripts SMS|Créer|Oui|
|Scripts SMS|Lecture|Oui|
|Scripts SMS|Supprimer|Oui|
|Scripts SMS|Modifier|Oui|


**Nom du rôle** : Approbateurs de scripts  
- **Description** : ces autorisations permettent à ce rôle d’approuver des scripts, mais pas de les créer ou de les exécuter.  
- **Autorisations :** vérifiez que les autorisations suivantes sont définies.  

|Catégorie|Autorisation|État|
|---|---|---|
|Collection|Exécuter un script|Non|
|Site|Lecture|Oui|
|Scripts SMS|Lecture|Oui|
|Scripts SMS|Approuver|Oui|
|Scripts SMS|Modifier|Oui|

     
**Exemple d’autorisations de scripts SMS pour le rôle de créateurs de script**  

 ![Exemple d’autorisations de scripts SMS pour le rôle de créateurs de script](./media/run-scripts/script_authors_permissions.png)

   

## <a name="create-a-script"></a>Créer un script

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.
2. Dans l'espace de travail **Bibliothèque de logiciels** , cliquez sur **Scripts**.
3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un script**.
4. Dans la page **Script** de l’assistant **Créer un script**, configurez les paramètres éléments suivants :
    - **Nom de script** : entrez un nom pour le script. Vous pouvez créer plusieurs scripts portant le même nom, mais utiliser des noms en double complique la recherche d’un script spécifique dans la console Configuration Manager.
    - **Langage de script** : seuls les scripts PowerShell sont pris en charge.
    - **Importer** : importez un script PowerShell dans la console. Le script s’affiche dans le champ **Script**.
    - **Effacer**  : supprime le script en cours du champ Script.
    - **Script** : affiche le script actuellement importé. Vous pouvez modifier le script dans ce champ si nécessaire.
5. Effectuez toutes les étapes de l'Assistant. Le nouveau script s’affiche dans la liste **Script** avec l’état **En attente d’approbation**. Avant de pouvoir exécuter ce script sur les appareils clients, vous devez l’approuver. 

> [!IMPORTANT]
    >Évitez de créer un script pour une réinitialisation de l’appareil ou un redémarrage de l’agent Configuration Manager lors de l’utilisation de la fonctionnalité Exécuter les scripts. Cela peut entraîner un état de redémarrage continu. Si nécessaire, il existe des améliorations apportées à la fonctionnalité de notification au client qui permettent de redémarrer les appareils, à compter de Configuration Manager version 1710. La [colonne en attente de redémarrage](/sccm/core/clients/manage/manage-clients#Restart-clients) peut aider à identifier les appareils qui nécessitent un redémarrage. 
<!--SMS503978  -->

## <a name="script-parameters"></a>Paramètres de script
*(Fonctionnalité introduite avec la version 1710)*  
L’ajout de paramètres à un script offre une flexibilité accrue à votre travail. Voici les possibilités actuelles de la fonctionnalité Exécuter les scripts avec des paramètres de script pour des types de données *Chaîne* et *Entier*. Les listes des valeurs prédéfinies sont également disponibles. Si votre script comporte des types de données non pris en charge, vous obtenez un avertissement.

Dans la boîte de dialogue **Créer un script**, cliquez sur **Paramètres de script** sous **Script**.

Chacun des paramètres de votre script a sa propre boîte de dialogue pour l’ajout d’autres informations et la validation.

>[!IMPORTANT]
> Les valeurs des paramètres ne peuvent pas contenir d’apostrophe. </br></br>
> Il existe un problème connu dans Configuration Manager version 1802 qui empêche la bonne transmission des paramètres contenant des espaces au script. Si un espace est utilisé dans un paramètre, seul le premier élément du paramètre est transmis au script et tout ce qui se trouve après cet espace n’est pas transmis. Les administrateurs peuvent contourner ce problème en remplaçant les espaces par d’autres caractères pour les convertir par la suite, ou à en utilisant d’autres méthodes.


### <a name="parameter-validation"></a>Validation du paramètre

Chaque paramètre inclus dans votre script a une boîte de dialogue **Propriétés du paramètre de script** qui vous permet d’ajouter la validation de ce paramètre. Après avoir ajouté la validation, vous devez obtenir des erreurs si vous entrez une valeur pour un paramètre qui ne satisfait pas à sa validation.

#### <a name="example-firstname"></a>Exemple : *FirstName*

Dans cet exemple, vous êtes en mesure de définir les propriétés du paramètre de chaîne *FirstName*.

![Paramètres de script - chaîne](./media/run-scripts/RS-parameters-string.png)


La section de validation de la boîte de dialogue **Propriétés du paramètre de script** contient les champs suivants que vous pouvez utiliser :

- **Longueur minimale** : nombre minimal de caractères du champ *FirstName*.
- **Longueur maximale** : nombre maximal de caractères du champ *FirstName*.
- **RegEx** : forme raccourcie *d’Expression régulière*. Pour plus d’informations sur l’utilisation de l’Expression régulière, consultez la section suivante, *Utilisation de la validation Expression régulière*.
- **Erreur personnalisée** : utile pour ajouter votre propre message d’erreur personnalisé qui remplace les messages d’erreur de validation système.

#### <a name="using-regular-expression-validation"></a>Utilisation de la validation Expression régulière

Une expression régulière est une forme compacte de programmation permettant de valider une chaîne de caractères par rapport à une validation encodée. Vous pouvez, par exemple, vérifier l’absence d’un caractère alphabétique en majuscule dans le champ *FirstName* en plaçant `[^A-Z]` dans le champ *RegEx*.

Le traitement de l’expression régulière pour cette boîte de dialogue est pris en charge par .NET Framework. Pour obtenir des conseils sur l’utilisation des expressions régulières, consultez [Expression régulière .NET](https://docs.microsoft.com/dotnet/standard/base-types/regular-expressions). 


## <a name="script-examples"></a>Exemples de scripts

Voici quelques exemples de scripts utilisables avec cette fonctionnalité.

### <a name="create-a-new-folder-and-file"></a>Créer un dossier et un fichier

Ce script crée un dossier et un fichier dans le dossier, en fonction du nom entré.

``` powershell
Param(
[Parameter(Mandatory=$True)]
[string]$FolderName,
[Parameter(Mandatory=$True)]
[string]$FileName,
)

New-Item $FolderName -type directory
New-Item $FileName -type file
```

### <a name="get-os-version"></a>Obtenir la version du système d’exploitation

Ce script utilise WMI pour interroger l’ordinateur sur sa version du système d’exploitation.

``` powershell
Write-Output (Get-WmiObject -Class Win32_operatingSystem).Caption
```

## <a name="run-a-script"></a>Exécuter un script

Une fois approuvé, un script peut être exécuté sur un seul appareil ou une collection. Une fois que l’exécution de votre script commence, il est lancé rapidement via un système de priorité élevée qui expire dans un délai d’une heure. Les résultats du script sont alors retournés à l’aide d’un système de message d’état.

Pour sélectionner une collection de cibles pour votre script :

1. Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.
2. Dans l’espace de travail Ressources et Conformité, cliquez sur **Regroupements de périphériques**.
3. Dans la liste **Collections d’appareils**, cliquez sur la collection d’appareils sur laquelle vous souhaitez exécuter le script.
4. Sélectionnez une collection de votre choix, cliquez sur **Exécuter le script**.
5. Sur la page **Script** de l’assistant **Exécuter le Script**, choisissez un script dans la liste. Seuls les scripts approuvés sont affichés.
6. Cliquez sur **Suivant**, puis complétez l’Assistant.

>[!IMPORTANT]
>Si un script ne s’exécute pas dans le délai d’une heure, parce qu’un appareil cible est par exemple désactivé, vous devez le réexécuter.

### <a name="target-machine-execution"></a>Exécution de la machine cible

Le script est exécuté en tant que compte *système* ou *d’ordinateur* sur les clients ciblés. Ce compte dispose d’un accès réseau limité. L’accès à des emplacements et systèmes distants par le script doit être provisionné en conséquence.

## <a name="script-monitoring"></a>Surveillance des scripts

Une fois que vous avez lancé l’exécution d’un script sur un regroupement d’appareils, utilisez la procédure suivante pour surveiller l’opération. Depuis la version 1710, vous êtes en mesure de surveiller un script en temps réel pendant qu’il s’exécute et vous pouvez également revenir au rapport d’une exécution du script donnée. <br>

![Surveillance de script - État de l’exécution du script](./media/run-scripts/RS-monitoring-three-bar.png)

1. Dans la console Configuration Manager, cliquez sur **Surveillance**.
2. Dans la liste **Surveillance**, cliquez sur **État du script**.
3. Dans la liste **État du script**, vous pouvez voir les résultats pour chaque script que vous avez exécuté sur des appareils clients. Un code de sortie de script de **0** indique généralement que le script a été exécuté avec succès.
    - À compter de Configuration Manager 1802, la sortie du script est tronquée à 4 Ko pour permettre une meilleure expérience d’affichage.  <!--510013-->
      ![Moniteur de script - Script tronqué](./media/run-scripts/Script-monitoring-truncated.png) 

## <a name="script-output"></a>Sortie du script

- À compter de Configuration Manager version 1802, les scripts retournent un résultat au format JSON. Ce format retourne toujours une sortie de script lisible. 
- Les scripts qui obtiennent un résultat inconnu, ou dans le cas où le client était hors connexion, ne s’affichent pas dans les graphiques ou les jeux de données. <!--507179-->
- Évitez de retourner une sortie de script longue, car elle est tronquée à 4 Ko. <!--508488-->
- Certaines fonctionnalités de mise en forme de la sortie des scripts ne sont pas disponibles lors de l’exécution de Configuration Manager version 1802 ou ultérieure avec une version d’un niveau inférieur du client. <!--508487-->
    - Quand vous disposez d’un client Configuration Manager antérieur à la version 1802, vous obtenez une sortie de type chaîne.
    -  Pour le client Configuration Manager versions 1802 et ultérieures, vous obtenez une sortie au format JSON.
        - Par exemple, vous pouvez obtenir des résultats qui indiquent TEXT sur une version du client et "TEXT" (sortie incluse entre guillemets doubles) sur une autre version, auquel cas ces résultats se présentent dans le graphique sous la forme de deux catégories différentes.
        - Si vous devez éviter ce comportement, exécutez le script sur deux regroupements différents : un avec des clients antérieurs à la version 1802 et un autre avec des clients 1802 et ultérieurs. Vous pouvez également convertir un objet enum en valeur de chaîne dans les scripts pour que ces derniers s’affichent correctement au format JSON. 
- Convertissez un objet enum en valeur de chaîne dans les scripts pour que ces derniers s’affichent correctement au format JSON. <!--508377--> ![Convertir un objet enum en valeur de chaîne](./media/run-scripts/enum-tostring-JSON.png)



## <a name="see-also"></a>Voir aussi

- [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
- [Principes de base de l’administration basée sur des rôles](/sccm/core/understand/fundamentals-of-role-based-administration)
