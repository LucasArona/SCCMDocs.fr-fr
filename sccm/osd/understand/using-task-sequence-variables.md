---
title: Guide pratique pour utiliser des variables de séquence de tâches
titleSuffix: Configuration Manager
description: Découvrez comment utiliser les variables dans une séquence de tâches Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e8ebea21b735e6b93d73bf6ff5eb842243ef42d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56121860"
---
# <a name="how-to-use-task-sequence-variables-in-configuration-manager"></a>Guide pratique pour utiliser des variables de séquence de tâches dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Le moteur de séquence de tâches dans la fonctionnalité de déploiement de système d’exploitation de Configuration Manager utilise de nombreuses variables pour contrôler ses comportements. Utilisez ces variables pour : 
 - fixer des conditions sur les étapes ;  
 - modifier le comportement de certaines étapes ;  
 - créer des actions plus complexes dans des scripts.  


 Pour une référence listant toutes les variables de séquence de tâches disponibles, voir [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables).



## <a name="bkmk_types"></a>Types de variables

 Il existe plusieurs types de variables :  
 - [Intégrée](#bkmk_built-in)  
 - [Action](#bkmk_action)  
 - [Personnalisé](#bkmk_custom)  
 - [Lecture seule](#bkmk_read-only)  
 - [Matrice](#bkmk_array)  


### <a name="bkmk_built-in"></a>Variables intégrées

 Les variables intégrées fournissent des informations sur l’environnement dans lequel s’exécute la séquence de tâches. Leurs valeurs sont disponibles tout au long de la séquence de tâches. En règle générale, le moteur de séquence de tâches initialise les variables intégrées avant d’exécuter la première étape. 

 Par exemple, **\_SMSTSLogPath** est une variable d’environnement qui spécifie le chemin que les composants Configuration Manager utilisent pour écrire les fichiers journaux. Toutes les étapes de la séquence de tâches peuvent accéder à cette variable d’environnement. 

 La séquence de tâches évalue certaines variables avant chaque étape. Par exemple, **\_SMSTSCurrentActionName** indique le nom de l’étape actuelle. 

### <a name="bkmk_action"></a>Variables d’action

 Les variables d’action de séquence de tâches spécifient les paramètres de configuration utilisés par une seule étape de séquence de tâches. Par défaut, l’étape initialise ses paramètres avant son exécution. Ces paramètres sont disponibles uniquement pendant l’exécution de l’étape de séquence de tâches associée. La séquence de tâches ajoute la valeur de la variable d’action à l’environnement avant d’exécuter l’étape. Ensuite, elle supprime la valeur de l’environnement une fois l’étape exécutée.

 Supposons par exemple que vous ajoutez l’étape **Exécuter la ligne de commande** à une séquence de tâches. Cette étape comporte une propriété **Démarrer dans**. La séquence de tâches stocke une valeur par défaut pour cette propriété comme variable **WorkingDirectory**. Elle initialise cette valeur avant d’exécuter l’étape **Exécuter la ligne de commande**. Pendant que cette étape est en cours d’exécution, elle accède à la valeur de propriété **Démarrer dans** à partir de la valeur **WorkingDirectory**. Une fois l’étape terminée, la séquence de tâches supprime la valeur de la variable **WorkingDirectory** de l’environnement. Si la séquence de tâches comporte une autre étape **Exécuter la ligne de commande**, elle initialise une nouvelle variable **WorkingDirectory**. À ce stade, elle donne à la variable la valeur de départ de l’étape en cours. Pour plus d’informations, voir [WorkingDirectory](using-task-sequence-variables.md#WorkingDirectory).  

 La valeur *par défaut* d’une variable d’action est présente pendant l’exécution de l’étape. Si vous définissez une *nouvelle* valeur, elle est accessible à plusieurs étapes de la séquence de tâches. Si vous remplacez une valeur par défaut, la nouvelle valeur reste dans l’environnement. Elle écrase la valeur par défaut pour les autres étapes de la séquence de tâches. Supposons par exemple que vous ajoutez une étape **Définir une variable de séquence de tâches** au tout début de la séquence de tâches. Elle donne à la variable **WorkingDirectory** la valeur `C:\`. Toutes les étapes **Exécuter la ligne de commande** de la séquence de tâches utilisent la nouvelle valeur de répertoire de départ.  

 Différentes étapes de séquence de tâches marquent certaines variables d’action comme *sortie*. Les étapes ultérieures de la séquence de tâches lisent ces variables de sortie.

 > [!Note]  
 > Toutes les étapes de séquence de tâches n’ont pas de variables d’action. Par exemple, bien qu’il existe des variables associées à l’action **Activer BitLocker**, il n’y a aucune variable pour l’action **Désactiver BitLocker**.  


### <a name="bkmk_custom"></a>Variables personnalisées

 Ces variables correspondent à toutes celles qui ne sont pas créées par Configuration Manager. Initialisez vos propres variables pour les utiliser comme conditions, dans des lignes de commande ou dans des scripts. 

 Lorsque vous spécifiez un nom pour une nouvelle variable de séquence de tâches, suivez ces instructions :  

 - Le nom d’une variable de séquence de tâches peut contenir des lettres, des chiffres, le trait de soulignement (`_`) et un trait d’union (`-`).  

 - La longueur du nom d’une variable de séquence de tâches doit être comprise entre 1 et 256 caractères.  

 - Les variables définies par l’utilisateur doivent commencer par une lettre (`A-Z` ou `a-z`).  

 - Le nom d’une variable définie par l’utilisateur ne peut pas commencer par un trait de soulignement. Seules les variables de séquence de tâches en lecture seule sont précédées de ce caractère.  

 - Le nom d’une variable de séquence de tâches ne respecte pas la casse. Par exemple, `OSDVAR` et `osdvar` correspondent à la même variable de séquence de tâches.  

 - Le nom d’une variable de séquence de tâches ne peut ni commencer ni se terminer par un espace. Il ne peut pas non plus comporter d’espaces enchâssés. La séquence de tâches ignore les espaces au début ou à la fin d’un nom de variable.  


 Il n’existe aucune limite définie quant au nombre de variables de séquence de tâches qui peuvent être créées. Toutefois, le nombre de variables est limité par la taille de l'environnement de séquence de tâches. La limite de taille totale pour l’environnement de séquence de tâches est de 32 Mo.  


### <a name="bkmk_read-only"></a>Variables en lecture seule

 Il n’est pas possible de modifier la valeur de certaines variables, qui sont en lecture seule. Le nom commence en général par un trait de soulignement (\_). La séquence de tâches les utilise pour ses opérations. Les variables en lecture seule sont visibles dans l’environnement de la séquence de tâches. 

 Ces variables sont utiles dans les scripts et les lignes de commande : par exemple, pour exécuter une ligne de commande et diriger la sortie dans un fichier journal dans **\_SMSTSLogPath** avec les autres fichiers journaux.

 > [!NOTE]  
 >  Les variables de séquence de tâches en lecture seule peuvent être lues par les étapes d’une séquence de tâches, mais elles ne peuvent pas être définies. Par exemple, utilisez une variable en lecture seule dans la ligne de commande d’une étape **Exécuter la ligne de commande**. Il est impossible de définir une variable en lecture seule avec l’étape **Définir une variable de séquence de tâches**.  



### <a name="bkmk_array"></a>Variables de matrice

 La séquence de tâches stocke certaines variables sous forme de matrice. Chacun de ses éléments représente les paramètres d’un seul objet. Utilisez ces variables quand l’appareil comporte plusieurs objets à configurer. Les étapes de séquence de tâches suivantes utilisent des variables de matrice :

 - [Appliquer les paramètres réseau](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [Formater et partitionner le disque](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a>Définir des variables

 Il existe différents moyens d’initialiser et de définir la valeur d’une variable personnalisée ou d’une variable qui n’est pas en lecture seule :  

 - [Définir la variable de séquence de tâches](#bkmk_set-ts-step)  
 - [Définir des variables dynamiques](#bkmk_set-dyn-step)  
 - [Variables de regroupement et d’appareil](#bkmk_set-coll-var)  
 - [Objet COM TSEnvironment](#bkmk_set-com)  
 - [Commande de prédémarrage](#bkmk_set-prestart)  
 - [Assistant Média de séquence de tâches](#bkmk_set-media)  


 Supprimez une variable de l’environnement en suivant les mêmes méthodes que pour en créer une. Pour supprimer une variable, définissez comme valeur de la variable une chaîne vide.  

 Vous pouvez combiner les méthodes afin d’attribuer plusieurs valeurs à une variable de séquence de tâches pour la même séquence. Par exemple, définissez les valeurs par défaut à l’aide de l’éditeur de séquence de tâches, puis fixez des valeurs personnalisées à l’aide d’un script. 

 Si la même variable est définie suivant différentes méthodes, le moteur de séquence de tâches applique l’ordre suivant :  

 1. Il évalue d’abord les variables de regroupement.  

 2. Les variables spécifiques de l’appareil remplacent la même variable définie sur un regroupement.  

 3. Les variables définies pendant la séquence de tâches quelle que soit la méthode sont prioritaires sur les variables de regroupement et d’appareil.  


#### <a name="general-limitations-for-task-sequence-variable-values"></a>Limitations générales imposées aux valeurs des variables de séquence de tâches  

 - Les valeurs des variables de séquence de tâches ne peuvent pas dépasser 4 000 caractères.  

 - Il n’est pas possible de modifier une variable de séquence de tâches en lecture seule. Les variables en lecture seule portent un nom qui commence par un trait de soulignement (`_`).  

 - Les valeurs des variables de séquence de tâches peuvent respecter la casse selon leur usage. Dans la plupart des cas, elles ne sont pas sensibles à la casse. Une variable qui comporte un mot de passe respecte la casse.  


### <a name="bkmk_set-ts-step"></a> Définir la variable de séquence de tâches

 Utilisez cette étape dans la séquence de tâches pour attribuer une seule valeur à une variable unique. 

 Pour plus d’informations, voir [Définir une variable de séquence de tâches](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 


### <a name="bkmk_set-dyn-step"></a> Définir des variables dynamiques

 Utilisez cette étape dans la séquence de tâches pour définir une ou plusieurs variables de séquence de tâches. Les règles définies à cette étape déterminent les variables et les valeurs à utiliser. 

 Pour plus d’informations, consultez [Définir des variables dynamiques](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables).


### <a name="bkmk_set-coll-var"></a>Variables de regroupement et d’appareil

 Définissez des variables sur les propriétés d’un regroupement ou d’un appareil en particulier. 

 Pour plus d’informations, voir [Créer des variables de séquence de tâches pour les ordinateurs et les regroupements](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables).


### <a name="bkmk_set-com"></a>Objet COM TSEnvironment

 Pour travailler avec des variables issues d’un script, utilisez l’objet **TSEnvironment**. 

 Pour plus d’informations, voir [Guide pratique pour utiliser des variables dans une séquence de tâches en cours d’exécution](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence) dans le Kit de développement logiciel (SDK) Configuration Manager.


### <a name="bkmk_set-prestart"></a>Commande de prédémarrage

 Les commandes de prédémarrage correspondent à un script ou un exécutable qui s’exécute dans Windows PE avant que l’utilisateur ne sélectionne la séquence de tâches. Elles peuvent interroger une variable ou demander plus d’informations à l’utilisateur, puis les enregistrer dans l’environnement. Utilisez l’objet COM [TSEnvironment](#bkmk_set-com) pour lire et écrire des variables à partir de la commande de prédémarrage. 

 Pour plus d’informations, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](/sccm/osd/understand/prestart-commands-for-task-sequence-media).


### <a name="bkmk_set-media"></a>Assistant Média de séquence de tâches

 Spécifiez des variables pour les séquences de tâches qui s’exécutent à partir d’un média. Lorsque vous utilisez un média pour déployer le système d’exploitation, vous ajoutez les variables de séquence de tâches et en indiquez les valeurs lors de la création du média. Les variables et leurs valeurs sont stockées sur le média.  

 > [!NOTE]  
 >  Les séquences de tâches sont stockées sur des médias autonomes. Cependant, tous les autres types de médias, tels que les médias préparés, récupèrent la séquence de tâches à partir d'un point de gestion.  

 Lorsque vous exécutez une séquence de tâches à partir d’un média, vous pouvez ajouter une variable sur la page **Personnalisation** de l’Assistant. 

 Utilisez les variables de média à la place des variables par ordinateur ou par regroupement. Si la séquence de tâches s’exécute à partir d’un média, les variables par ordinateur et par regroupement ne s’appliquent pas et ne sont pas utilisées.  

 > [!TIP]  
 >  La séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage dans le fichier journal **CreateTSMedia.log** sur l’ordinateur qui exécute la console Configuration Manager. Ce fichier inclut la valeur des variables de séquence de tâches. Consultez ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

 Pour plus d’informations, voir [Créer un média de séquence de tâches](/sccm/osd/deploy-use/create-task-sequence-media).



## <a name="bkmk_access"></a>Accéder aux variables

 Une fois la variable et sa valeur spécifiées suivant l’une des méthodes indiquées dans la section précédente, utilisez-la dans vos séquences de tâches. Par exemple, accédez aux valeurs par défaut des variables de séquence de tâches intégrées, ou créez une étape qui dépend de la valeur d’une variable.  

 Utilisez les méthodes suivantes pour accéder aux valeurs des variables dans l’environnement de la séquence de tâches :
 - [Utiliser dans une étape](#bkmk_access-step)  
 - [Condition d’étape](#bkmk_access-condition)  
 - [Script personnalisé](#bkmk_access-script)  
 - [Fichier de réponses de l’installation de Windows](#bkmk_access-answer)  
  

### <a name="bkmk_access-step"></a>Utiliser dans une étape

 Spécifiez une valeur de variable pour un paramètre dans une étape de séquence de tâches. Dans l’éditeur de séquence de tâches, modifiez l’étape et indiquez le nom de la variable comme valeur de champ. Mettez le nom de la variable entre symboles de pourcentage (`%`). 

 Par exemple, utilisez le nom de la variable dans le champ **Ligne de commande** de l’étape **Exécuter la ligne de commande**. La ligne de commande suivante écrit le nom de l’ordinateur dans un fichier texte. 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a>Condition d’étape

 Utilisez des variables de séquence de tâches intégrées ou personnalisées dans le cadre d’une condition sur une étape ou un groupe. La séquence de tâches évalue la valeur de la variable avant d’exécuter l’étape ou le groupe.

 Pour ajouter une condition qui évalue la valeur d’une variable, suivez les étapes ci-dessous :  

 1. Dans l’éditeur de séquence de tâches, sélectionnez l’étape ou le groupe auquel vous souhaitez ajouter la condition.  

 2. Basculez vers l’onglet **Options** de l’étape ou du groupe. Cliquez sur **Ajouter une condition**, puis sélectionnez **Variable de séquence de tâches**.  

 3. Dans la boîte de dialogue **Variable de séquence de tâches**, spécifiez les paramètres suivants :  

    - **Variable** : Le nom de la variable. Par exemple, `_SMSTSInWinPE`.  

    - **Condition** : La condition permettant d’évaluer la valeur de la variable. Par exemple, **equals**.  

    - **Valeur** : La valeur de la variable à vérifier. Par exemple, `false`.  


 Les trois exemples ci-dessus forment une condition commune pour tester si la séquence de tâches s’exécute à partir d’une image de démarrage dans Windows PE : 

 > **Variable de séquence de tâches** `_SMSTSInWinPE equals "false"`

 Fixez cette condition sur le groupe **Capturer les fichiers et paramètres** du modèle de séquence de tâche par défaut pour installer une image de système d’exploitation existante.


### <a name="bkmk_access-script"></a>Script personnalisé

 Lisez et écrivez des variables à l’aide de l’objet COM **Microsoft.SMS.TSEnvironment** pendant l’exécution de la séquence de tâches.

 L’exemple Windows PowerShell suivant interroge la variable **_SMSTSLogPath** pour obtenir l’emplacement actuel du journal. Le script définit également une variable personnalisée.

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```


###  <a name="bkmk_access-answer"></a>Fichier de réponses de l’installation de Windows

Le fichier de réponses de l’installation de Windows que vous fournissez peut comporter des variables de séquence de tâches. Utiliser le format `%varname%`, où *varname* est le nom de la variable. L’étape **Configurer Windows et ConfigMgr** remplace la chaîne de nom de variable par la valeur réelle de la variable. Vous ne pouvez pas utiliser ces variables de séquence de tâches incorporées dans les champs exclusivement numériques d’un fichier de réponses unattend.xml.

Pour plus d’informations, consultez [Configurer Windows et ConfigMgr](/sccm/osd/understand/task-sequence-steps#BKMK_SetupWindowsandConfigMgr).



## <a name="see-also"></a>Voir aussi

- [Étapes de séquence de tâches](/sccm/osd/understand/task-sequence-steps)
- [Variables de séquence de tâches](/sccm/osd/understand/task-sequence-variables)
- [Considérations relatives à la planification de l’automatisation des tâches](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
