---
title: Considérations relatives à la planification de l’automatisation des tâches
titleSuffix: Configuration Manager
description: Planifiez les tâches avant de les automatiser dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 485f295e83d94ed5282003c7179a5f2c1e37773e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="planning-considerations-for-automating-tasks-in-system-center-configuration-manager"></a>Considérations relatives à la planification de l’automatisation des tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez créer des séquences de tâches pour automatiser les tâches dans votre environnement System Center Configuration Manager. Ces tâches vont de la capture d'un système d'exploitation sur un ordinateur de référence au déploiement du système d'exploitation sur un ou plusieurs ordinateurs de destination. Les actions de la séquence de tâches sont définies dans les étapes individuelles de la séquence. Lors de l’exécution de la séquence de tâches, les actions de chaque étape sont effectuées au niveau de la ligne de commande dans le contexte de Système local sans intervention de l’utilisateur. Aidez-vous des sections suivantes pour planifier l’automatisation des tâches dans Configuration Manager.

##  <a name="BKMK_TSStepsActions"></a> Actions et étapes de séquence de tâches  
 Les étapes constituent le composant de base d'une séquence de tâches. Elles peuvent contenir des commandes de configuration et de capture du système d’exploitation d’un ordinateur de référence, ou des commandes d’installation du système d’exploitation, des pilotes, du client Configuration Manager et des logiciels sur l’ordinateur de destination. Les commandes d'une étape de séquence de tâches sont définies par les actions de l'étape. Il existe deux types d'action. Une action que vous définissez à l'aide d'une chaîne de ligne de commande est appelée action personnalisée. Une action prédéfinie par Configuration Manager s’appelle une action intégrée. Une séquence de tâches peut effectuer n'importe quelle combinaison d'actions personnalisées et intégrées.  

 Des étapes de séquence de tâches peuvent également inclure des conditions qui contrôlent le comportement de l'étape, telles que l'arrêt de la séquence de tâches ou la poursuite de la séquence de tâches si une erreur se produit. Des conditions sont ajoutées à l'étape en incluant une variable de séquence de tâches à l'étape. Par exemple, vous pouvez utiliser la variable **SMSTSLastActionRetCode** pour tester la condition de l’étape précédente. Des variables peuvent être ajoutées à une seule étape ou à un groupe d'étapes.  

 Les étapes de séquence de tâches sont traitées de manière séquentielle, ce qui comprend l'action de l'étape et les conditions qui sont attribuées à l'étape. Quand Configuration Manager commence à traiter une étape de séquence de tâches, l’étape suivante ne démarre pas tant que l’action précédente n’a pas été effectuée. Une séquence de tâches est considérée comme effectuée une fois que toutes ses étapes ont abouti ou que l’échec d’une étape oblige Configuration Manager à arrêter l’exécution de la séquence de tâches avant la fin de toutes ses étapes. Par exemple, si l’étape d’une séquence de tâches ne parvient pas à localiser une image ou un package référencé sur un point de distribution, la séquence de tâches contient une référence incorrecte et Configuration Manager arrête l’exécution de la séquence de tâches à ce stade, sauf si l’étape en échec présente une condition qui lui permet de continuer en cas d’erreur.  

> [!IMPORTANT]  
>  Par défaut, une séquence de tâches échoue après l'échec d'une étape ou d'une action. Si vous voulez que la séquence de tâches se poursuive dans le cas où une étape échouerait, modifiez la séquence de tâches, cliquez sur l’onglet **Options** , puis sélectionnez **Continuer en cas d’erreur**.  

 Pour plus d’informations sur les étapes qui peuvent être ajoutées à une séquence de tâches, consultez [Étapes de séquence de tâches](../understand/task-sequence-steps.md).  

##  <a name="BKMK_TSGroups"></a> Groupes de séquence de tâches  
 Les **groupes** désignent plusieurs étapes dans une séquence de tâches. Un groupe de séquence de tâches comprend un nom, une description facultative et des conditions facultatives qui sont évaluées comme un tout avant que la séquence de tâches passe à l'étape suivante. Les groupes peuvent être imbriqués les uns dans les autres et un groupe peut contenir un mélange d'étapes et de sous-groupes. Les groupes sont utiles pour associer plusieurs étapes qui possèdent une condition commune.  

> [!IMPORTANT]  
>  Par défaut, un groupe de séquence de tâches échoue lorsque toute étape ou groupe incorporé au sein du groupe échoue. Si vous voulez que la séquence de tâches se poursuive en cas d’échec d’une étape ou d’un groupe incorporé, modifiez la séquence de tâches, cliquez sur l’onglet **Options** , puis sélectionnez **Continuer en cas d’erreur**.  

 Le tableau suivant illustre le fonctionnement de l’option **Continuer en cas d’erreur** quand vous regroupez des étapes.  

 Dans cet exemple, deux groupes de séquences de tâches contiennent trois étapes de séquence de tâches chacun.  

|Groupe de séquences de tâches ou étape|Paramètre Continuer en cas d'erreur|  
|---------------------------------|-------------------------------|  
|**Groupe de séquence de tâches 1**|**Continuer en cas d’erreur** sélectionné.|  
|Étape de séquence de tâches 1|**Continuer en cas d’erreur** sélectionné.|  
|Étape de séquence de tâches 2|Non défini.|  
|Étape de séquence de tâches 3|Non défini.|  
|**Groupe de séquence de tâches 2**|Non défini.|  
|Étape de séquence de tâches 4|Non défini.|  
|Étape de séquence de tâches 5|Non défini.|  
|Étape de séquence de tâches 6|Non défini.|  

-   Si l'étape de séquence de tâches 1 échoue, la séquence de tâches continue avec l'étape de séquence de tâches 2.  

-   Si l'étape de séquence de tâches 2 échoue, la séquence de tâches n'exécute pas l'étape de séquence de tâches 3 mais continue d'exécuter les étapes de séquence de tâches 4 et 5, qui se trouvent dans un autre groupe de séquence de tâches.  

-   Si l’étape de séquence de tâches 4 n’aboutit pas, aucune autre étape n’est exécutée et la séquence de tâches se solde par un échec, car le paramètre **Continuer en cas d’erreur** n’a pas été configuré pour le groupe de séquences de tâches 2.  

 Même si le nom du groupe n'est pas nécessairement unique, vous devez attribuer un nom aux groupes de séquences de tâches. Vous devez également fournir une description facultative pour le groupe de séquence de tâches.  

##  <a name="BKMK_TSVariables"></a> Variables de séquence de tâches  
 Les variables de séquence de tâches se composent de paires nom-valeur qui fournissent des paramètres de configuration et de déploiement du système d’exploitation pour des tâches de configuration de l’ordinateur, du système d’exploitation et de l’état utilisateur sur un ordinateur client Configuration Manager. Les variables de séquence de tâches fournissent un mécanisme de configuration et de personnalisation des étapes d'une séquence de tâches.  

 Lorsque vous exécutez une séquence de tâches, la plupart de ses paramètres sont stockés sous la forme de variables d'environnement. Vous pouvez accéder aux variables de séquence de tâches intégrées et en modifier les valeurs, et vous pouvez créer de nouvelles variables de séquence de tâches afin de personnaliser son exécution sur un ordinateur de destination.  

 Vous pouvez réaliser les opérations suivantes à l'aide des variables de séquences de tâches utilisées dans l'environnement de séquence de tâches :  

-   configurer les paramètres d'une action de séquence de tâches ;  

-   fournir des arguments de ligne de commande pour une étape de séquence de tâches ;  

-   évaluer une condition qui détermine si un groupe ou une étape de séquence de tâches est exécuté ;  

-   fournir des valeurs aux scripts personnalisés utilisés dans une séquence de tâches.  

 Par exemple, vous disposez peut-être d’une séquence de tâches incluant une étape **Joindre le domaine ou le groupe de travail**. Vous pouvez déployer la séquence de tâches dans différents regroupements, pour lesquels l'appartenance au regroupement est déterminée par l'appartenance au domaine. Dans ce cas, vous pouvez spécifier une variable de séquence de tâches par regroupement pour le nom de domaine de chaque regroupement, puis utiliser cette variable pour fournir le nom de domaine approprié dans la séquence de tâches.  

###  <a name="BKMK_TSCreateVariables"></a> Créer des variables de séquence de tâches  
 Vous pouvez ajouter des nouvelles variables de séquence de tâches pour personnaliser et contrôler les étapes d'une séquence de tâches. Vous pouvez, par exemple, créer une variable de séquence de tâches qui remplace le paramètre d'une étape de séquence de tâches intégrée. Vous pouvez également créer une variable de séquence de tâches personnalisée à utiliser avec les conditions, lignes de commande ou étapes personnalisées de la séquence de tâches. Lorsque vous créez une variable de séquence de tâches, elle est conservée, avec la valeur qui lui est associée dans l'environnement de séquence de tâches, même lorsque la séquence redémarre l'ordinateur de destination. La variable et sa valeur peuvent être utilisées dans la séquence de tâches à travers différents environnements de système d'exploitation. Par exemple, elle peut être utilisée à la fois dans un système d’exploitation Windows complet et dans l’environnement Windows PE.  

 Le tableau suivant décrit les méthodes de création d'une variable de séquence de tâches et d'autres informations sur l'utilisation.  

|Méthode de création|Utilisation|  
|-------------------|-----------|  
|Définition de champs dans les étapes de séquence de tâches à l'aide de l'Éditeur de séquence de tâches|Spécifie des valeurs par défaut pour l'étape de séquence de tâches. La variable et sa valeur ne sont accessibles que lorsque l'étape s'exécute dans la séquence de tâches. Elles ne font pas partie de l'environnement de séquences global et ne sont pas accessibles pour d'autres étapes de la séquence de tâches.<br /><br /> Pour obtenir la liste des variables intégrées avec leurs actions associées, consultez [Variables d’action de séquence de tâches](../understand/task-sequence-action-variables.md).|  
|Ajout d'une étape de variable de séquence de tâches dans une séquence de tâches|Spécifie la variable de séquence de tâches et sa valeur dans l'environnement de séquence de tâches lorsque l'étape de séquence de tâches est exécutée dans le cadre d'une séquence de tâches. Toutes les étapes de séquence de tâches suivantes peuvent accéder à la variable d'environnement et à sa valeur.|  
|Définition d'une variable par regroupement|Spécifie des variables de séquence de tâches et des valeurs pour un regroupement d'ordinateurs. Toutes les séquences de tâches ciblées vers le regroupement peuvent accéder aux variables de séquence de tâches et à leurs valeurs.|  
|Définition d'une variable par ordinateur|Spécifie des variables de séquence de tâches et des valeurs pour un ordinateur particulier. Toutes les séquences de tâches ciblées vers l'ordinateur peuvent accéder aux variables de séquence de tâches et à leurs valeurs.|  
|Ajout d’une variable de séquence de tâches dans la page **Personnalisation** de l’Assistant Média de séquence de tâches|Spécifie les variables et valeurs de séquence de tâches pour la séquence de tâches exécutée à partir du média ayant accès à la variable de séquence de tâches et à sa valeur.|  

 Pour remplacer la valeur par défaut d'une variable de séquence de tâches intégrée, vous devez donner à la variable de séquence de tâches que vous définissez le même nom que la variable de séquence de tâches intégrée. Pour obtenir la liste des variables de séquence de tâches intégrées avec les actions et les utilisations associées, consultez [Variables intégrées de séquence de tâches](../understand/task-sequence-built-in-variables.md).  

 Vous pouvez supprimer une variable de séquence de tâches de l'environnement de séquence de tâches de la même manière que vous la créez. Dans ce cas, pour supprimer une variable de l'environnement de séquence de tâches, définissez la valeur de la variable sur une chaîne vide.  

 Vous pouvez combiner les méthodes pour définir une variable de séquence de tâches sur plusieurs valeurs pour la même séquence. Dans un scénario avancé, vous pourriez définir les valeurs par défaut des étapes d'une séquence à l'aide de l'Éditeur de séquence de tâches, puis définir une valeur de variable personnalisée à l'aide de méthodes de création différentes. La liste suivante décrit les règles déterminant la valeur utilisée lorsqu'une variable de séquence de tâches est créée à l'aide de plusieurs méthodes.  

1.  L’étape **Définir la variable de séquence de tâches** est prioritaire sur toutes les autres méthodes de création.  

2.  Les variables par ordinateur ont préséance sur les variables par regroupement. Si vous donnez le même nom à une variable par ordinateur et une variable par regroupement, la valeur de la première est utilisée lorsque l'ordinateur de destination exécute la séquence de tâches déployée.  

3.  Des séquences de tâches peuvent être exécutées à partir du média. Utilisez les variables de média à la place des variables par ordinateur ou par regroupement. Si la séquence de tâches est exécutée à partir du média, les variables par ordinateur et par regroupement ne s'appliquent pas et ne sont pas utilisées. En revanche, les variables définies dans la page **Personnalisation** de l’Assistant Média de séquence de tâches sont utilisées pour définir des valeurs spécifiques à une séquence de tâches exécutée à partir du média  

4.  Si aucune variable de séquence de tâches n'est définie dans l'environnement de séquences global, les actions intégrées utilisent la valeur par défaut de l'étape, telle que définie dans l'Éditeur de séquence de tâches.  

 Outre l'écrasement des valeurs des paramètres d'étape de séquence de tâches intégrés, vous avez également la possibilité de créer une nouvelle variable d'environnement à utiliser dans une étape, un script, une ligne de commande ou une condition de séquence de tâches. Lorsque vous spécifiez un nom pour une nouvelle variable de séquence de tâches, suivez ces instructions :  

-   Le nom de variable de séquence de tâches spécifié peut contenir des lettres, des chiffres, le caractère de soulignement (_) et le tiret (-).  

-   La longueur des noms de variable de séquence de tâches doit être comprise entre 1 et 256 caractères.  

-   Les variables définies par l'utilisateur doivent commencer par une lettre (A-Z ou a-z).  

-   Les variables définies par l'utilisateur ne peuvent pas commencer par le caractère de soulignement. Seules les variables de séquence de tâches en lecture seule sont précédées de ce caractère.  

    > [!NOTE]  
    >  Les variables de séquence de tâches en lecture seule peuvent être lues par les étapes d'une séquence de tâches, mais elles ne peuvent pas être définies. Par exemple, vous pouvez utiliser ce type de variable dans une ligne de commande pour exécuter une action de séquence de tâches **Exécuter la ligne de commande**, mais vous ne pouvez pas définir une variable en lecture seule à l’aide de l’action **Définir la variable de séquence de tâches**.  

-   Les noms de variable de séquence de tâches ne tiennent pas compte de la casse. Par exemple, OSDVAR et osdvar représentent la même variable.  

-   Les noms de variable de séquence de tâches ne peuvent ni commencer ni se terminer par un espace, ni contenir des espaces incorporés. Les espaces laissés au début ou à la fin d'un nom de variable sont ignorés.  

 Le tableau suivant contient des exemples de noms de variable de séquence de tâches valides et non valides définis par l'utilisateur.  

|Exemples de noms de variable définis par l'utilisateur valides|Exemples de noms de variable définis par l'utilisateur non valides|  
|-------------------------------------------------------|----------------------------------------------------------|  
|MaVariable|1Variable<br /><br /> Les variables définies par l'utilisateur ne peuvent pas commencer par un chiffre.|  
|Ma_Variable|MyV@riable<br /><br /> Les variables définies par l'utilisateur ne peuvent pas contenir le symbole @.|  
|Ma_Variable_2|_MaVariable<br /><br /> Les variables définies par l'utilisateur ne peuvent pas commencer par un caractère de soulignement.|  

 Limitations générales pour les variables de séquence de tâches :  

-   Les valeurs de variable de séquence de tâches ne peuvent pas dépasser 4 000 caractères.  

-   Vous ne pouvez pas créer ou remplacer une variable de séquence de tâches en lecture seule. Les variables en lecture seule sont désignées par des noms commençant par un caractère de soulignement (_). Vous pouvez accéder à la valeur d'une variable en lecture seule dans votre séquence de tâches ; toutefois, vous ne pouvez pas en modifier les valeurs associées.  

-   Les valeurs des variables de séquence de tâches peuvent être sensibles à la casse selon l'utilisation de la valeur. Dans la plupart des cas, les valeurs des variables de séquence de tâches ne sont pas sensibles à la casse. Cependant, certaines valeurs peuvent être sensibles à la casse, comme par exemple une variable contenant un mot de passe.  

-   Il n'existe aucune limite quant au nombre de variables de séquence de tâches qui peuvent être créées. Toutefois, le nombre de variables est limité par la taille de l'environnement de séquence de tâches. La limite de taille totale pour l’environnement de séquence de tâches est de 32 Mo.  

###  <a name="BKMK_TSEnvironmentVariables"></a> Accéder aux variables d’environnement  
 Une fois la variable de séquence de tâches et sa valeur spécifiées à l'aide d'une des méthodes fournies dans la section précédente, vous pouvez l'utiliser dans vos séquences de tâches. Vous pouvez accéder aux valeurs par défaut des variables de séquence de tâches intégrées, spécifier une nouvelle valeur pour une variable intégrée ou encore utiliser une variable de séquence de tâches personnalisée dans une ligne de commande ou un script.  

 Le tableau suivant présente les opérations de séquence de tâches que vous pouvez effectuer en accédant aux variables d'environnement de séquence de tâches.  

|Opération de séquence de tâches|Utilisation|  
|-----------------------------|-----------|  
|Configurer les paramètres de l'action|Vous pouvez indiquer qu'un paramètre d'étape de séquence de tâches est fourni par une valeur de variable à l'exécution de la séquence.<br /><br /> Pour cela, utilisez l'Éditeur de séquence de tâches, modifiez l'étape, puis spécifiez le nom de la variable en tant que valeur de champ. Le nom de la variable doit être mis entre symboles de pourcentage (%) pour indiquer qu'il s'agit d'une variable d'environnement.|  
|Fournir des arguments de ligne de commande|Vous pouvez spécifier tout ou partie d'une ligne de commande personnalisée à l'aide d'une valeur de variable d'environnement.<br /><br /> Pour fournir un paramètre de ligne de commande avec une variable d’environnement, intégrez le nom de la variable dans le champ **Ligne de commande** de l’étape de séquence de tâches **Exécuter la ligne de commande**. Il convient de mettre le nom de la variable entre symboles de pourcentage (%).<br /><br /> Par exemple, la ligne de commande suivante utilise une variable d'environnement intégrée pour enregistrer le nom de l'ordinateur dans le fichier C:\File.txt.<br /><br /> <br /><br /> **Cmd /C %_SMSTSMachineName% > C:\File.txt**|  
|Évaluer une condition d'étape|Vous pouvez utiliser des variables d'environnement de séquence de tâches intégrées ou personnalisées dans le cadre d'une condition de groupe ou d'étape de séquence de tâches. La valeur de variable d'environnement sera évaluée avant l'exécution de l'étape de séquence de tâches ou du groupe de séquences de tâches.<br /><br /> Pour ajouter une condition qui prend la valeur d'une variable, effectuez les opérations suivantes :<br /><br /> 1.  Sélectionnez l'étape ou le groupe auquel vous souhaitez ajouter la condition.<br />2.  Sous l’onglet **Options** de l’étape ou du groupe, sélectionnez **Variable de séquence de tâches** dans la liste déroulante **Ajouter une condition**.<br />3.  Dans la boîte de dialogue **Variable de séquence de tâches**, spécifiez le nom de la variable, la condition testée et la valeur de la variable.|  
|Fournir des informations pour un script personnalisé|Vous pouvez lire et écrire les variables de séquence de tâches à l'aide de l'objet Microsoft.SMS.TSEnvironment pendant l'exécution de la séquence de tâches.<br /><br /> L’exemple suivant illustre un fichier de script Visual Basic qui interroge la variable de séquence de tâches **_SMSTSLogPath** pour obtenir l’emplacement actuel du fichier journal. Le script définit également une variable personnalisée.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' You can query the environment to get an existing variable.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' You can also set a variable in the OSD environment.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> Pour plus d'informations sur l'utilisation des variables de séquence de tâches dans les scripts, consultez la documentation du SDK.|  

###  <a name="BKMK_ComputerCollectionVariables"></a> Variables d’ordinateur et de regroupement  
 Vous pouvez configurer des séquences de tâches pour qu'elles s'exécutent sur plusieurs ordinateurs ou regroupements en même temps. Vous pouvez spécifier des informations uniques par ordinateur ou par regroupement, par exemple indiquer une clé de produit de système d'exploitation unique ou regrouper tous les membres d'un regroupement dans un domaine spécifique.  

 Vous pouvez affecter des variables de séquence de tâches à un seul ordinateur ou regroupement. Lorsque l'exécution de la séquence de tâches commence sur l'ordinateur ou le regroupement cible, les valeurs spécifiées y sont appliquées.  

 Vous pouvez spécifier des variables de séquence de tâches pour un seul ordinateur ou regroupement. Lorsque l'exécution de la séquence de tâches commence sur l'ordinateur ou le regroupement cible, les variables spécifiées sont ajoutées à l'environnement et les valeurs sont disponibles à toutes les étapes de la séquence de tâches.  

> [!WARNING]  
>  Si vous utilisez le même nom pour une variable par regroupement et une variable par ordinateur, la deuxième a préséance sur la première. Les variables de séquence de tâches que vous attribuez aux regroupements ont préséance sur les variables de séquence de tâches intégrées.  

 Pour plus d’informations sur la création de variables de séquence de tâches pour des ordinateurs et des regroupements, consultez [Créer des variables de séquence de tâches pour les ordinateurs et les regroupements](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="BKMK_TSMediaVariables"></a> Variables de média de séquence de tâches  
 Vous pouvez spécifier des variables de séquence de tâches pour les séquences de tâches exécutées à partir du média. Lorsque vous utilisez un média pour déployer le système d'exploitation, vous ajoutez les variables de séquence de tâches et en spécifiez les valeurs lors de la création du média ; les variables et leurs valeurs sont stockées sur le média.  

> [!NOTE]  
>  Les séquences de tâches sont stockées sur des médias autonomes. Cependant, tous les autres types de médias, tels que les médias préparés, récupèrent la séquence de tâches à partir d'un point de gestion.  

 Vous pouvez spécifier les variables de séquence de tâches dans la page **Personnalisation** de l’Assistant Média de séquence de tâches. Pour plus d’informations sur la création d’un média, consultez [Créer un média de séquence de tâches](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  La séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, notamment la valeur des variables de séquence de tâches, dans le fichier journal CreateTSMedia.log sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

##  <a name="BKMK_TSCreate"></a> Créer une séquence de tâches  
 Vous créez des séquences de tâches à l'aide de l'Assistant Création d'une séquence de tâches. L'Assistant peut créer des séquences de tâches intégrées qui effectuent des tâches spécifiques ou des séquences de tâches personnalisées qui peuvent effectuer de nombreuses tâches différentes.  

 Par exemple, vous pouvez créer des séquences de tâches qui créent et capturent une image de système d'exploitation d'un ordinateur de référence, installent une image de système d'exploitation existante sur un ordinateur de destination ou créent une séquence de tâches personnalisée pour exécuter une tâche personnalisée. Vous pouvez utiliser des séquences de tâches personnalisées pour effectuer des déploiements de système d'exploitation spécialisés.  

 Pour plus d’informations sur la création de séquences de tâches, consultez [Créer des séquences de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="BKMK_TSEdit"></a> Modifier une séquence de tâches  
 Vous modifiez la séquence de tâches à l’aide de l’**Éditeur de séquence de tâches**. L'éditeur peut apporter les modifications suivantes à la séquence de tâches :  

-   Vous pouvez ajouter ou supprimer des étapes de la séquence de tâches.  

-   Vous pouvez modifier l'ordre des étapes de la séquence de tâches.  

-   Vous pouvez ajouter ou supprimer des groupes d'étapes.  

-   Vous pouvez spécifier si la séquence de tâches continue lorsqu'une erreur se produit.  

-   Vous pouvez ajouter des conditions aux étapes et aux groupes d'une séquence de tâches.  

> [!IMPORTANT]  
>  Si la séquence de tâches possède des références qui ne sont pas associées à un package ou à un programme suite à la modification, vous devez corriger la référence, supprimer le programme sans référence de la séquence de tâches ou désactiver temporairement l'étape de séquence de tâches qui a échoué jusqu'à la correction ou la suppression de la référence incorrecte.  

 Pour plus d’informations sur la modification de séquences de tâches, consultez [Modifier une séquence de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="BKMK_TSDeploy"></a> Déployer une séquence de tâches  
 Vous pouvez déployer une séquence de tâches sur les ordinateurs de destination situés dans un regroupement Configuration Manager. Il peut s’agir du regroupement **Tous les ordinateurs inconnus** qui est utilisé pour déployer des systèmes d’exploitation sur des ordinateurs inconnus. Toutefois, vous ne pouvez pas déployer une séquence de tâches sur des regroupements d'utilisateurs.  

> [!IMPORTANT]  
>  Ne déployez pas de séquences de tâches qui installent des systèmes d’exploitation sur des regroupements inappropriés, tels que le regroupement **Tous les systèmes** . N'oubliez pas que le regroupement sur lequel vous déployez la séquence de tâches contient uniquement les ordinateurs sur lesquels vous souhaitez installer le système d'exploitation. Pour éviter les déploiements de systèmes d’exploitation non souhaités, vous pouvez gérer les paramètres de déploiement. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Chaque ordinateur de destination qui reçoit la séquence de tâches exécute la séquence de tâches conformément aux paramètres spécifiés dans le déploiement. La séquence de la tâche elle-même ne contient pas de programmes ou de fichiers associés. Tous les fichiers qui sont référencés par une séquence de tâches doivent déjà être présents sur l'ordinateur de destination ou résider sur un point de distribution auxquels les clients peuvent accéder. En outre, la séquence de tâches installe les packages qui sont référencés par les programmes, même si le programme ou le package est déjà installé sur l'ordinateur de destination.  

> [!NOTE]  
>  Par rapport aux packages et aux programmes, si la séquence de tâches installe une application, l'application s'installe uniquement si ses règles de spécification sont satisfaites et si elle n'est pas déjà installée, en fonction de la méthode de détection spécifiée pour l'application.  

 Le client Configuration Manager exécute un déploiement de séquence de tâches quand il télécharge la stratégie du client. Pour déclencher cette action au lieu d’attendre le prochain cycle d’interrogation, consultez [Lancer une récupération de stratégie pour un client Configuration Manager](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 Quand vous déployez des séquences de tâches sur des appareils Windows Embedded dont les filtres d’écriture sont activés, vous pouvez faire en sorte que le filtre d’écriture soit désactivé sur l’appareil pendant le déploiement et que ce dernier soit redémarré à l’issue du déploiement. Si le filtre d'écriture n'est pas désactivé, la séquence de tâches est déployée sur un segment de recouvrement temporaire et elle n'est pas disponible au redémarrage de l'appareil.  

> [!NOTE]  
>  Lorsque vous déployez une séquence de tâches sur un appareil Windows Embedded, assurez-vous que celui-ci appartient à un regroupement pour lequel une fenêtre de maintenance a été configurée. Cela vous permet de contrôler à quel moment le filtre d'écriture est désactivé et activé, et à quel moment l'appareil redémarre.  
>   
>  Si les clients téléchargent des séquences de tâches en dehors d'une fenêtre de maintenance, la séquence de tâches est téléchargée deux fois. Dans ce cas, les clients téléchargent la séquence de tâches, désactivent les filtres d'écriture, redémarrent l'ordinateur, puis téléchargent de nouveau la séquence de tâches, car celle-ci a été téléchargée dans le segment de recouvrement temporaire, qui est effacé au redémarrage de l'appareil.  

 Pour plus d’informations sur le déploiement de séquences de tâches, consultez [Déployer une séquence de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_TSExportImport"></a> Exporter et importer une séquence de tâches  
 Configuration Manager vous permet d’exporter et d’importer des séquences de tâches. Lorsque vous exportez une séquence de tâches, vous pouvez inclure les objets qui sont référencés par la séquence de tâches. Citons notamment une image de système d'exploitation, une image de démarrage, un package de l'agent du client, un package de pilotes et des applications qui ont des dépendances.  

> [!NOTE]  
>  Le processus d’exportation et d’importation de séquences de tâches est très similaire au processus d’exportation et d’importation d’applications dans Configuration Manager.  

 Pour plus d’informations sur l’exportation et l’importation de séquences de tâches, consultez [Exporter et importer des séquences de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="BKMK_TSRun"></a> Exécuter une séquence de tâches  
 Par défaut, les séquences de tâches sont toujours exécutées à l’aide du compte système local. L'étape de ligne de commande de séquence de tâches offre la possibilité d'exécuter la séquence de tâches en tant que compte différent. Quand la séquence de tâches est exécutée, le client Configuration Manager commence par rechercher les packages référencés avant de démarrer les étapes de la séquence de tâches. Si un package référencé n'est pas validé ou n'est pas disponible sur un point de distribution, la séquence de tâches renvoie une erreur pour l'étape de séquence de tâches associée.  

 Si une séquence de tâches distribuée est configurée pour le téléchargement et l’exécution, tous les packages et toutes les applications qui en dépendent sont téléchargés dans le cache du client Configuration Manager. Les applications et packages nécessaires sont obtenus à partir de points de distribution. Si la taille du cache du client Configuration Manager est insuffisante, ou si l’application ou le package sont introuvables, la séquence de tâches se solde par un échec et un message d’état est généré. Vous pouvez aussi préciser que le client ne télécharge le contenu que s’il est nécessaire en sélectionnant **Télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches**. Vous pouvez aussi utiliser l’option **Exécuter le programme à partir du point de distribution** pour indiquer que le client installe les fichiers directement à partir du point de distribution sans les télécharger préalablement dans le cache. L’option **Exécuter le programme à partir du point de distribution** est disponible uniquement si le paramètre **Copier le contenu de ce package dans un partage de package sur les points de distribution** des packages référencés est activé sous l’onglet **Accès aux données** des propriétés du **Package**.  

 Si le client exécutant la séquence de tâches ne parvient pas à localiser une application ou un package dépendant, il envoie immédiatement une erreur quand le déploiement est configuré comme étant **Disponible**. Cependant, si le déploiement est configuré comme étant **Obligatoire**, le client Configuration Manager attend avant de réessayer de télécharger le contenu jusqu’à l’expiration du délai, au cas où le contenu ne serait pas encore répliqué sur un point de distribution auquel le client a accès.  

 Qu’une séquence de tâches soit réussie ou non, Configuration Manager enregistre le résultat dans l’historique du client Configuration Manager. Vous ne pouvez pas annuler ou arrêter une séquence de tâches une fois qu'elle est lancée sur un ordinateur.  

> [!IMPORTANT]  
>  Si une étape de séquence de tâches requiert le redémarrage de l'ordinateur client, le client doit pouvoir démarrer sur une partition de disque formatée. Sinon, la séquence de tâches échoue, quel que soit le traitement d'erreur défini par la séquence de tâches.  

 Lorsqu'un objet dépendant d'une séquence de tâches, tel qu'un package de distribution de logiciels, est mis à jour vers une nouvelle version, toute séquence de tâches qui fait référence à ce package est automatiquement mise à jour et fait référence à la nouvelle version, quel que soit le nombre de mises à jour qui ont été déployées.  

> [!NOTE]  
>  Avant d’exécuter une séquence de tâches, le client Configuration Manager vérifie toutes les séquences de tâches à la recherche d’éventuelles dépendances et des disponibilités de ces dépendances sur un point de distribution. Si le client trouve un objet supprimé dont dépend la séquence de tâches, le client génère une erreur et n'exécute pas la séquence de tâches.  

###  <a name="BKMK_RunProgram"></a> Exécuter un programme avant l’exécution de la séquence de tâches  
 Vous pouvez sélectionner un programme qui s'exécute avant l'exécution de la séquence de tâches. Pour spécifier un programme à exécuter en premier, ouvrez la boîte de dialogue **Propriétés** de la séquence de tâches, puis sélectionnez l’onglet **Avancé** pour définir les options suivantes :  

> [!IMPORTANT]  
>  Pour exécuter un programme avant d'exécuter la séquence de tâches, tout le contenu de la séquence de tâches et du programme doit être mis à la disposition du package sur un partage de package. Le partage de package peut être configuré sous l’onglet **Accès aux données** des propriétés du package.  

-   **Exécuter un autre programme en premier** : indiquez qu’un autre programme doit être exécuté avant la séquence de tâches.  

    > [!IMPORTANT]  
    >  Ce paramètre s'applique uniquement aux séquences de tâches qui s'exécutent dans le système d'exploitation complet. Configuration Manager ignore ce paramètre si la séquence de tâches est démarrée à l’aide de l’environnement PXE ou d’un média de démarrage.  

-   **Package** : indiquez le package qui contient le programme.  

-   **Programme** : spécifiez le programme à exécuter.  

-   **Toujours exécuter ce programme en premier** : indiquez que Configuration Manager doit exécuter ce programme chaque fois qu’il exécute la séquence de tâches sur le même client. Par défaut, après l'exécution d'un programme avec succès, le programme n'est pas exécuté à nouveau si la séquence de tâches est réexécutée sur le même client.  

 Si l'exécution du programme sélectionné échoue sur un client, la séquence de tâches n'est pas exécutée.  

##  <a name="BKMK_TSMaintenanceWindow"></a> Utiliser une fenêtre de maintenance pour spécifier quand une séquence de tâches peut s’exécuter  
 Vous pouvez définir à quel moment la séquence de tâches peut être exécutée. Pour cela, définissez une fenêtre de maintenance pour le regroupement contenant vos ordinateurs de destination. La configuration des fenêtres de maintenance consiste à définir une date de début, une heure de début et de fin, ainsi qu'une périodicité. En outre, lorsque vous définissez le calendrier de la fenêtre de maintenance, vous pouvez faire en sorte que la fenêtre de maintenance s'applique uniquement aux séquences de tâches. Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
>  Lorsque vous configurez une fenêtre de maintenance en vue d'exécuter une séquence de tâches, une fois que la séquence de tâches démarrée, elle se poursuit jusqu'à son terme, même si la fenêtre de maintenance arrive à terme entre temps. Une séquence de tâches aboutit entièrement ou échoue entièrement.  

##  <a name="BKMK_TSNetworkAccessAccount"></a> Séquences de tâches et compte d’accès réseau  
 Même si les séquences de tâches s'exécutent uniquement dans le contexte du compte Système local, il peut être nécessaire de configurer le compte d'accès réseau dans les circonstances suivantes :  

-   Vous devez configurer correctement le compte d’accès réseau, sinon la séquence de tâches ne pourra pas accéder aux packages Configuration Manager des points de distribution pour s’effectuer. Pour plus d’informations sur le compte d’accès réseau, consultez [Compte d’accès réseau](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

    > [!NOTE]  
    >  Le compte d'accès réseau n'est jamais utilisé comme contexte de sécurité pour l'exécution de programmes, l'installation d'applications ou de mises à jour ou bien l'exécution de séquences de tâches. En revanche, il est utilisé pour accéder aux ressources associées sur le réseau.  

-   Quand vous utilisez une image de démarrage pour lancer un déploiement du système d’exploitation, Configuration Manager utilise l’environnement Windows PE, qui n’est pas un système d’exploitation complet. Windows PE utilise un nom aléatoire généré automatiquement qui ne fait partie d’aucun domaine. Si vous ne configurez pas correctement le compte d’accès réseau, l’ordinateur risque de ne pas disposer des autorisations nécessaires pour accéder aux packages Configuration Manager et effectuer la séquence de tâches.  

##  <a name="BKMK_TSCreateMedia"></a> Créer un média pour les séquences de tâches  
 Vous pouvez écrire des séquences de tâches et leurs fichiers et dépendances associés sur plusieurs types de média. Ces média sont notamment les média amovibles, tels que les ensembles de CD ou DVD ou bien les disques mémoire flash USB pour les média de capture, autonomes et amovibles ou bien les fichiers WIM pour les média préparés.  

 Vous pouvez créer les types de média suivants :  

-   **Média de capture**. Ce type de média capture une image de système d’exploitation qui est configurée et créée en dehors de l’infrastructure Configuration Manager. Il peut contenir des programmes personnalisés qui sont exécutés avant l'exécution d'une séquence de tâches. Le programme personnalisé peut interagir avec le bureau, inviter l'utilisateur à entrer des valeurs ou créer des variables à utiliser par la séquence de tâches.  

     Pour plus d’informations, consultez [Créer un média de capture](../deploy-use/create-capture-media.md).  

-   **Média autonome**. ce média contient la séquence de tâches et tous les objets associés qui sont nécessaires à l’exécution de la séquence de tâches. Les séquences de tâches d’un média autonome peuvent s’exécuter quand Configuration Manager dispose d’une connectivité limitée ou nulle au réseau. Un média autonome peut être exécuté comme suit :  

    -   Si l’ordinateur de destination n’a pas démarré, l’image Windows PE associée à la séquence de tâches est utilisée à partir du média autonome, et la séquence de tâches commence.  

    -   Le média autonome peut être démarré manuellement si un utilisateur est connecté au réseau et lance l'installation.  

    > [!IMPORTANT]  
    >  Les étapes d'une séquence de tâches de média autonome doivent pouvoir être exécutées sans extraire de données du réseau. Dans le cas contraire, l'étape de séquence de tâches qui tente de récupérer les données échoue. Par exemple, une étape de séquence de tâches qui nécessite un point de distribution pour obtenir un package échoue. Toutefois, si le package requis se trouve sur le média autonome, l'étape de séquence de tâches est exécutée correctement.  

     Pour plus d’informations, consultez [Créer un média autonome](../deploy-use/create-stand-alone-media.md).  

-   **Média de démarrage**. Un média de démarrage contient les fichiers nécessaires au démarrage d’un ordinateur de destination, lequel peut ainsi se connecter à l’infrastructure Configuration Manager et déterminer les séquences de tâches à exécuter en fonction de son appartenance à un regroupement. La séquence de tâches et les objets dépendants ne se trouvent pas sur le média. Ils s’obtiennent auprès du client Configuration Manager via le réseau. Cette méthode est utile pour les déploiements de nouveaux ordinateurs ou de systèmes nus, mais aussi quand aucun système d’exploitation ou client Configuration Manager n’est installé sur l’ordinateur de destination.  

     Pour plus d’informations, consultez [Créer un média de démarrage](../deploy-use/create-bootable-media.md).  

-   **Média préparé**. le média préparé déploie une image de système d’exploitation sur un ordinateur de destination qui n’est pas configuré. Le média préparé est stocké sous forme de fichier WIM (Windows Imaging Format) installable sur un ordinateur nu par le fabricant ou dans un centre préproduction d’entreprise non connecté à l’environnement Configuration Manager.  

     Pour plus d’informations, consultez [Créer un média préparé](../deploy-use/create-prestaged-media.md).  

 Lorsque vous créez un média, spécifiez un mot de passe pour le média afin de contrôler l'accès aux fichiers contenus sur le média. Si vous spécifiez un mot de passe, un utilisateur doit être présent pour entrer le mot de passe sur l'ordinateur cible lors de l'exécution de la séquence de tâches.  

 Lorsque vous exécutez une séquence de tâches à l'aide d'un média, l'architecture de puce d'ordinateur spécifiée contenue sur le média n'est pas reconnue et la séquence de tâches tente de s'exécuter, même si l'architecture spécifiée ne correspond pas à celle effectivement installée sur l'ordinateur cible. Si l'architecture de puce contenue sur le média ne correspond pas à celle installée sur l'ordinateur cible, l'installation échoue.  

 Pour plus d’informations sur le déploiement de systèmes d’exploitation à l’aide d’un média, consultez [Créer un média de séquence de tâches](../deploy-use/create-task-sequence-media.md).  
