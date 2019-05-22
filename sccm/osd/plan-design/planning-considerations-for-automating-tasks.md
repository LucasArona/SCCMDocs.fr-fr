---
title: Prévoir l’automatisation des tâches
titleSuffix: Configuration Manager
description: Avant de créer des séquences de tâches, prévoyez d’automatiser les tâches avec Configuration Manager.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 32a645f95d25c92809723ae735f566535fc4043d
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65083301"
---
# <a name="planning-considerations-for-automating-tasks-in-configuration-manager"></a>Considérations relatives à la planification de l’automatisation des tâches dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez créer des séquences de tâches pour automatiser les tâches dans votre environnement Configuration Manager. Ces tâches vont de la capture d’un système d’exploitation sur un ordinateur de référence au déploiement du système d’exploitation sur un ou plusieurs ordinateurs de destination. Les actions de la séquence de tâches sont définies dans les étapes individuelles de la séquence. Lorsque la séquence de tâches s’exécute, elle exécute les actions de chaque étape au niveau des lignes de commande dans le contexte système local. Ce comportement est entièrement automatisé, sans intervention de l’utilisateur. 



##  <a name="BKMK_TSStepsActions"></a> Actions et étapes de séquence de tâches  

 Les étapes constituent le composant de base d'une séquence de tâches. Elles peuvent comporter les commandes suivantes :  
   - configurer et capturer le système d’exploitation d’un ordinateur de référence ;  
   - installer Windows, des pilotes matériels, le client Configuration Manager et des logiciels sur l’ordinateur de destination.   


 Les actions de l’étape d’une séquence de tâches définissent ses commandes. Il existe deux types d’actions :  
   - Une action définie à l’aide d’une chaîne de ligne de commande se nomme *action personnalisée*.  
   - Une action prédéfinie par Configuration Manager s’appelle *action intégrée*.  


 Une séquence de tâches peut effectuer n'importe quelle combinaison d'actions personnalisées et intégrées.  

 Les étapes des séquences de tâches peuvent également être soumises à des conditions qui contrôlent leur comportement : par exemple, arrêter la séquence de tâches ou bien la poursuivre en cas d’erreur. Parmi ces conditions figurent les variables de séquence de tâches. Utilisez par exemple la variable **SMSTSLastActionRetCode** pour tester la condition de l’étape précédente. Ajoutez des conditions à une seule étape ou à un groupe d’étapes.  

 La séquence de tâches traite les étapes séquentiellement. Cette séquence inclut l’action de l’étape et les conditions à laquelle l’étape est soumise. Quand Configuration Manager commence à traiter une étape de séquence de tâches, il ne lance pas la suivante tant que l’action précédente n’est pas terminée. 

 Une séquence de tâches est considérée comme terminée quand : 
   - Toutes ses étapes sont terminées.  
   - L’échec d’une étape oblige Configuration Manager à interrompre l’exécution de la séquence de tâches avant la fin de toutes ses étapes.  


 Par exemple, si l’étape d’une séquence de tâches ne parvient pas à localiser une image ou un package référencé sur un point de distribution, la séquence de tâches contient une référence incorrecte. Configuration Manager arrête la séquence de tâches à ce stade de son exécution, sauf si l’étape non réussie présente une condition spécifiant de continuer lorsqu’une erreur se produit.  

 > [!IMPORTANT]  
 >  Par défaut, une séquence de tâches échoue après l'échec d'une étape ou d'une action. Si vous voulez que la séquence de tâches se poursuive dans le cas où une étape échouerait, modifiez la séquence de tâches, cliquez sur l’onglet **Options** , puis sélectionnez **Continuer en cas d’erreur**.  

 Pour plus d’informations sur les étapes qui peuvent être ajoutées à une séquence de tâches, consultez [Étapes de séquence de tâches](/sccm/osd/understand/task-sequence-steps).  



##  <a name="BKMK_TSGroups"></a> Groupes de séquence de tâches  

 Il est possible de grouper plusieurs étapes dans une séquence de tâches. Un groupe de séquences de tâches se compose d’un nom, d’une description facultative et de conditions facultatives. La séquence de tâches évalue les conditions du groupe en tant qu’unité avant de passer à l’étape suivante. Imbriquez les groupes ou mêlez étapes et sous-groupes. Les groupes sont utiles pour associer plusieurs étapes qui possèdent une condition commune.  

 Attribuez un nom aux groupes de séquences de tâches. Il n’est pas nécessairement unique. Vous devez également fournir une description facultative pour le groupe de séquence de tâches.  

 > [!IMPORTANT]  
 >  Par défaut, un groupe de séquence de tâches échoue lorsque toute étape ou groupe incorporé au sein du groupe échoue. Si vous voulez que la séquence de tâches se poursuive en cas d’échec d’une étape ou d’un groupe incorporé, définissez l’option **Continuer en cas d’erreur** sur l’étape ou le groupe.  

 Le tableau suivant illustre le fonctionnement de l’option **Continuer en cas d’erreur** quand vous regroupez des étapes.  

 Cet exemple comporte deux groupes de séquences de tâches qui contiennent trois étapes de séquence de tâches chacun.  

 |Groupe de séquences de tâches ou étape|Paramètre Continuer en cas d'erreur|  
 |---------------------------------|-------------------------------|  
 |**Groupe de séquences de tâches 1**|**Continuer en cas d’erreur** sélectionné.|  
 |Étape de séquence de tâches 1|**Continuer en cas d’erreur** sélectionné.|  
 |Étape de séquence de tâches 2|Non défini.|  
 |Étape de séquence de tâches 3|Non défini.|  
 |**Groupe de séquences de tâches 2**|Non défini.|  
 |Étape de séquence de tâches 4|Non défini.|  
 |Étape de séquence de tâches 5|Non défini.|  
 |Étape de séquence de tâches 6|Non défini.|  


 -   Si l'étape de séquence de tâches 1 échoue, la séquence de tâches continue avec l'étape de séquence de tâches 2.  

 -   Si l’étape de séquence de tâches 2 échoue, la séquence de tâches n’exécute pas l’étape de séquence de tâches 3. Le groupe de séquences de tâches 1 étant configuré pour **Continuer en cas d’erreur**, la séquence de tâches passe au groupe de séquences de tâches 2. Il exécute ensuite l’étape de séquence de tâches 4.  

 -   Si l’étape de séquence de tâches 4 échoue, aucune autre étape n’est exécutée. La séquence de tâches échoue, car le paramètre **Continuer en cas d’erreur** n’est pas configuré pour le groupe de séquences de tâches 2.  



## <a name="add-child-task-sequences-to-a-task-sequence"></a>Ajouter des séquences de tâches enfants à une séquence de tâches
 <!--1261338-->
 À partir de Configuration Manager version 1710, vous pouvez ajouter une nouvelle étape de séquence de tâches qui exécute une autre séquence de tâches. Cette étape crée une relation parent-enfant entre les séquences de tâches. Effectuez cette étape pour créer des séquences de tâches plus modulaires réutilisables.  

 Pour plus d’informations, voir [Exécuter une séquence de tâches](/sccm/osd/understand/task-sequence-steps#child-task-sequence). 

 > [!Note]  
 > Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).<!--505213-->  



##  <a name="BKMK_TSVariables"></a> Variables de séquence de tâches  

 Les variables de séquence de tâches sont un ensemble de paires nom/valeur. Elles définissent les paramètres de configuration et de déploiement du système d’exploitation et de l’ordinateur, ainsi que les tâches de configuration de l’état utilisateur sur un client Configuration Manager. Les variables de séquence de tâches fournissent un mécanisme de configuration et de personnalisation des étapes d'une séquence de tâches.  

 À l’exécution, une séquence de tâches stocke la plupart de ses paramètres sous la forme de variables d’environnement. Vous pouvez consulter ou modifier les valeurs des variables des séquences de tâches intégrées. Il est également possible de créer de nouvelles variables de séquence de tâches pour personnaliser la façon dont la séquence de tâches s’exécute sur l’ordinateur de destination.  

 Utilisez des variables de séquence de tâches pour effectuer les actions suivantes :  

 -   configurer les paramètres d'une action de séquence de tâches ;  

 -   fournir des arguments de ligne de commande pour une étape de séquence de tâches ;  

 -   évaluer une condition qui détermine si un groupe ou une étape de séquence de tâches s’exécute ;  

 -   fournir des valeurs aux scripts personnalisés utilisés dans une séquence de tâches.  


 Par exemple, vous avez une séquence de tâches comportant une étape **Joindre un domaine ou un groupe de travail**. Déployez la séquence de tâches dans différents regroupements, dont l’adhésion est déterminée par l’appartenance au domaine. Spécifiez une variable de séquence de tâches par regroupement pour le nom de domaine de chaque regroupement. Ensuite, utilisez-la pour indiquer le nom de domaine approprié dans la séquence de tâches.  

 Pour plus d’informations, voir [Guide pratique pour utiliser des variables de séquence de tâches](/sccm/osd/understand/using-task-sequence-variables).



##  <a name="BKMK_TSCreate"></a>Créer une séquence de tâches  

 Créez des séquences de tâches à l'aide de l'Assistant Création d'une séquence de tâches. L'Assistant peut créer des séquences de tâches intégrées qui effectuent des tâches spécifiques ou des séquences de tâches personnalisées qui peuvent effectuer de nombreuses tâches différentes. L’Assistant permet de créer les types de séquences de tâches suivants :

 - installer une image de système d’exploitation existante sur un ordinateur de destination ;  

 - générer et capturer une image de système d’exploitation d’un ordinateur de référence ;  

 - passer à Windows 10 à partir d’un package de mise à niveau du système d’exploitation sur un ordinateur de destination ;   

 - créer une séquence de tâches personnalisée qui effectue une tâche personnalisée ou un déploiement de système d’exploitation spécialisé.  


 Pour plus d’informations, voir [Créer des séquences de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTaskSequence).  



##  <a name="BKMK_TSEdit"></a> Modifier une séquence de tâches  

 Modifiez la séquence de tâches à l’aide de **l’Éditeur de séquence de tâches**. L'éditeur peut apporter les modifications suivantes à la séquence de tâches :  

 - ajouter ou supprimer des étapes de la séquence de tâches ;  

 - modifier l’ordre des étapes de la séquence de tâches ;  

 - ajouter ou supprimer des groupes d’étapes ;  

 - indiquer si la séquence de tâches continue en cas d’erreur ;  

 - ajouter des conditions aux étapes et aux groupes d’une séquence de tâches.  


 > [!IMPORTANT]  
 >  Si la séquence de tâches possède des références non associées à un objet suite à la modification, l’éditeur impose de les corriger avant de se fermer. Quelques exemples d’actions possibles :  
 > - corriger la référence ;  
 > - supprimer l’objet non référencé de la séquence de tâches ;  
 > - désactiver temporairement l’étape non réussie de séquence de tâche jusqu’à ce que la référence incorrecte soit corrigée ou supprimée.  


 Pour plus d’informations sur la modification de séquences de tâches, consultez [Modifier une séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ModifyTaskSequence).  



##  <a name="BKMK_TSDeploy"></a> Déployer une séquence de tâches  

 Déployez une séquence de tâches sur des ordinateurs de destination situés dans un regroupement Configuration Manager. Utilisez le regroupement **Tous les ordinateurs inconnus** pour déployer des systèmes d’exploitation sur des ordinateurs inconnus. Il n’est pas possible de déployer une séquence de tâches sur des regroupements d’utilisateurs.  

 > [!IMPORTANT]  
 >  Ne déployez pas de séquences de tâches qui installent des systèmes d’exploitation dans des regroupements inappropriés. Veillez à ce que le regroupement sur lequel vous déployez la séquence de tâches ne contienne que les ordinateurs sur lesquels vous souhaitez installer le système d’exploitation. Pour éviter les déploiements indésirables du système d’exploitation, configurez des paramètres de déploiement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

 Chaque ordinateur de destination qui reçoit la séquence de tâches exécute la séquence de tâches conformément aux paramètres spécifiés dans le déploiement. La séquence de la tâche proprement dite ne contient pas de programmes ou de fichiers associés. Tous les fichiers référencés par une séquence de tâches doivent être déjà présents sur l’ordinateur de destination ou résider sur un point de distribution auquel les clients ont accès. 

 > [!NOTE]  
 > La séquence de tâches installe des packages référencés par des programmes, même si le programme ou le package est déjà installé sur l’ordinateur de destination. 
 > 
 > Si la séquence de tâches installe une application, celle-ci ne s’installe que si ses règles de spécification sont satisfaites et si elle n’est pas déjà installée, en fonction de la méthode de détection spécifiée pour l’application.  

 Le client Configuration Manager exécute un déploiement de séquence de tâches quand il télécharge la stratégie du client. Pour déclencher cette action au lieu d’attendre le prochain cycle d’interrogation, voir [Lancer la récupération de stratégie pour un client Configuration Manager](/sccm/core/clients/manage/manage-clients#BKMK_PolicyRetrieval).  

 Quand vous déployez des séquences de tâches sur des appareils Windows Embedded dont le filtre d’écriture est activé, vous pouvez faire en sorte que ce dernier soit désactivé sur l’appareil pendant le déploiement, puis redémarré à l’issue du déploiement. Si le filtre d’écriture n’est pas désactivé, la séquence de tâches est déployée sur un segment de recouvrement temporaire et elle n’est pas disponible au redémarrage de l’appareil.  

 > [!NOTE]  
 >  Lorsque vous déployez une séquence de tâches sur un appareil Windows Embedded, assurez-vous que celui-ci appartient à un regroupement pour lequel une fenêtre de maintenance a été configurée. Cela vous permet de contrôler à quel moment le filtre d'écriture est désactivé et activé, et à quel moment l'appareil redémarre.  
 >   
 >  Si les clients téléchargent des séquences de tâches en dehors d'une fenêtre de maintenance, la séquence de tâches est téléchargée deux fois. Dans ce scénario, le client télécharge la séquence de tâches, désactive le filtre d’écriture, redémarre l’ordinateur, puis télécharge de nouveau la séquence de tâches. En effet, la séquence de tâches a été téléchargée à l’origine dans le segment de recouvrement temporaire, qui est effacé au redémarrage de l’appareil.  

 Pour plus d’informations sur le déploiement de séquences de tâches, consultez [Déployer une séquence de tâches](/sccm/osd/deploy-use/deploy-a-task-sequence).  



##  <a name="BKMK_TSExportImport"></a> Exporter et importer une séquence de tâches  

 Configuration Manager vous permet d’exporter et d’importer des séquences de tâches. Lorsque vous exportez une séquence de tâches, vous pouvez inclure les objets qui sont référencés par la séquence de tâches. 

 Pour plus d’informations, voir [Exporter et importer des séquences de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_ExportImport).  



##  <a name="BKMK_TSRun"></a> Exécuter une séquence de tâches  

 Les séquences de tâches s’exécutent toujours à l’aide du compte système local. Lors de l’exécution, le client Configuration Manager commence par rechercher les packages référencés avant de lancer les étapes de la séquence de tâches. S’il ne parvient pas à valider ou à télécharger un package référencé, la séquence de tâches retourne une erreur pour l’étape associée.  

 > [!Note]  
 > L’étape de séquence de tâches **Exécuter la ligne de commande** offre la possibilité d’exécuter une commande sous un autre compte.  

 Si vous configurez le téléchargement et l’exécution d’un déploiement de séquence de tâches, le client Configuration Manager télécharge tout le contenu dépendant dans son cache. Si la taille du cache client est insuffisante ou que le contenu est introuvable, la séquence de tâches échoue. Le client génère un message d’état. 

 Vous pouvez également spécifier que le client ne télécharge le contenu que lorsqu’il est nécessaire. Pour cela, sélectionnez **Télécharger le contenu localement lorsque la séquence de tâches en cours d’exécution l’exige** dans le déploiement de la séquence de tâches. Il est également possible **d’Exécuter le programme à partir du point de distribution**. Avec cette option, le client installe directement les fichiers à partir du point de distribution sans les télécharger au préalable dans le cache. 

 Lorsque vous configurez le déploiement de la séquence de tâches comme étant **Disponible**, si le client ne parvient pas à localiser le contenu dépendant de la séquence de tâches, il envoie immédiatement une erreur. Pour un déploiement **Obligatoire**, dans cette situation, le client Configuration Manager attend. Il réessaie de télécharger le contenu jusqu’à l’échéance, au cas où le contenu n’ait pas encore été répliqué vers un emplacement de contenu accessible au client.  

 Qu’une séquence de tâches soit réussie ou non, Configuration Manager enregistre cet état dans l’historique du client. 

 Une fois qu’une séquence de tâches a démarré sur un ordinateur, il n’est pas possible de l’annuler ou de l’arrêter.  

 > [!IMPORTANT]  
 >  Si une étape de séquence de tâches impose le redémarrage de l’ordinateur, le client doit pouvoir démarrer sur une partition de disque formatée. Sinon, la séquence de tâches échoue, qu’une gestion des erreurs soit spécifiée ou non dans la séquence de tâches.  

 Lors de la mise à jour d’un objet dépendant d’une séquence de tâches vers une version plus récente, toutes les séquences de tâches qui référencent le package sont automatiquement mises à jour. Elles référencent la nouvelle version, quel que soit le nombre de mises à jour déployées.  



##  <a name="BKMK_TSMaintenanceWindow"></a> Utiliser une fenêtre de maintenance pour spécifier quand une séquence de tâches peut s’exécuter  

 Vous pouvez spécifier à quel moment la séquence de tâches peut s’exécuter en définissant une fenêtre de maintenance pour le regroupement d’appareils : date de début, heure de début et de fin et périodicité. Lorsque vous définissez le calendrier de la fenêtre de maintenance, vous pouvez faire en sorte qu’elle s’applique uniquement aux séquences de tâches. Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).  

 > [!IMPORTANT]  
 >  Lorsque vous configurez une fenêtre de maintenance en vue d'exécuter une séquence de tâches, une fois que la séquence de tâches démarrée, elle se poursuit jusqu'à son terme, même si la fenêtre de maintenance arrive à terme entre temps.  



##  <a name="BKMK_TSNetworkAccessAccount"></a>Séquences de tâches et compte d’accès réseau  

> [!Important]  
> À compter de la version 1806, certains scénarios de déploiement de système d’exploitation ne nécessitent pas l’utilisation du compte d’accès réseau. Pour plus d’informations, consultez [HTTP amélioré](#enhanced-http).

Même si les séquences de tâches s’exécutent seulement dans le contexte du compte système local, il peut être nécessaire de configurer le [compte d’accès réseau](/sccm/core/plan-design/hierarchy/accounts#network-access-account) dans les circonstances suivantes :  

- Si la séquence de tâches tente d’accéder au contenu Configuration Manager sur les points de distribution. Configurez correctement le compte d’accès réseau ; sinon, la séquence de tâches échouera.   

- Si vous utilisez une image de démarrage pour lancer un déploiement de système d’exploitation. Dans ce cas, Configuration Manager utilise l’environnement Windows PE, qui n’est pas un système d’exploitation complet. Cet environnement utilise un nom aléatoire généré automatiquement qui ne fait partie d’aucun domaine. Si vous ne configurez pas correctement le compte d’accès réseau, l’ordinateur ne peut pas accéder au contenu requis pour la séquence de tâches.  

> [!NOTE]  
>  Le compte d’accès réseau n’est jamais utilisé comme contexte de sécurité pour l’exécution de programmes et de séquences de tâches ou pour l’installation d’applications et de mises à jour logicielles. Il ne sert qu’à accéder aux ressources associées sur le réseau.  

Pour plus d’informations sur le compte d’accès réseau, voir [Compte d’accès réseau](/sccm/core/plan-design/hierarchy/accounts#network-access-account).  


### <a name="enhanced-http"></a>HTTP amélioré
<!--1358278-->

À compter de la version 1806, quand vous activez **HTTP amélioré**, les scénarios suivants ne nécessitent pas un compte d’accès réseau pour télécharger du contenu à partir d’un point de distribution :
  
- Séquences de tâches exécutées à partir d’un support de démarrage ou d’un environnement PXE  
- Séquence de tâches exécutées à partir du Centre logiciel  

Ces séquences de tâches conviennent aux déploiements de système d’exploitation et aux déploiements personnalisés. Elles sont également prises en charge par les ordinateurs de groupe de travail.
 
Pour plus d’informations, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).  

> [!Note]  
> Les scénarios de déploiement de système d’exploitation suivants nécessitent toujours l’utilisation d’un compte d’accès réseau :
>  
> - **Accéder au contenu directement à partir d’un point de distribution lorsque la séquence de tâches en cours d’exécution en a besoin** ([option de déploiement](/sccm/osd/deploy-use/deploy-a-task-sequence) de séquence de tâches)   
> - **Si le compte d’ordinateur ne parvient pas à se connecter au magasin d’état, utiliser le compte d’accès réseau** (option de l’étape [Demander le magasin d’état](/sccm/osd/understand/task-sequence-steps#BKMK_RequestStateStore)) 
> - Connexion à un domaine non approuvé ou entre forêts Active Directory 
> - **Accéder au contenu directement depuis le point de distribution** (option de l’étape [Appliquer l’image de système d’exploitation](/sccm/osd/understand/task-sequence-steps#BKMK_ApplyOperatingSystemImage)) 
> - **Exécuter un autre programme en premier** ([paramètre avancé](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#bkmk_prop-advanced) de séquence de tâches) 
> - [Multidiffusion](/sccm/osd/deploy-use/use-multicast-to-deploy-windows-over-the-network)  



##  <a name="BKMK_TSCreateMedia"></a> Créer un média pour les séquences de tâches  

 Vous pouvez écrire des séquences de tâches et leurs fichiers et dépendances associés sur plusieurs types de média. Configuration Manager prend en charge les médias amovibles, par exemple, les DVD et les clés USB, comme médias de démarrage, médias autonomes et médias de capture. Le média préparé utilise un fichier image Windows (WIM).  

 Lorsque vous créez un média, spécifiez un mot de passe pour contrôler l’accès. Il sera alors obligatoire d’entrer le mot de passe sur l’ordinateur cible pour exécuter la séquence de tâches.  

 Lorsque vous exécutez une séquence de tâches à partir d’un média, l’architecture de processeur spécifiée du média n’est pas reconnue. La séquence de tâches tente de s’exécuter même si l’architecture spécifiée ne correspond pas à l’ordinateur cible. Si l’architecture du média ne correspond pas à l’architecture de l’ordinateur cible, la séquence de tâches échoue.  

 Pour plus d’informations, voir [Créer un média de séquence de tâches](/sccm/osd/deploy-use/create-task-sequence-media).  


### <a name="media-types"></a>Types de médias
 Configuration Manager prend en charge les types de médias suivants :  

#### <a name="capture-media"></a>Média de capture
 Ce type de média capture une image de système d’exploitation configurée et créée en dehors de l’infrastructure Configuration Manager. Il peut contenir des programmes personnalisés qui sont exécutés avant l'exécution d'une séquence de tâches. Le programme personnalisé peut interagir avec le bureau, inviter l'utilisateur à entrer des valeurs ou créer des variables à utiliser par la séquence de tâches.  

 Pour plus d’informations, consultez [Créer un média de capture](/sccm/osd/deploy-use/create-capture-media).  

#### <a name="stand-alone-media"></a>Média autonome
 ce média contient la séquence de tâches et tous les objets associés qui sont nécessaires à l’exécution de la séquence de tâches. Les séquences de tâches d’un média autonome peuvent s’exécuter quand Configuration Manager dispose d’une connectivité limitée ou nulle au réseau. Exécutez un média autonome de la façon suivante :  

 - Si l’ordinateur de destination n’a pas démarré, l’image Windows PE associée à la séquence de tâches est utilisée à partir du média autonome, et la séquence de tâches commence.  

 - Démarrez manuellement le média autonome. Un utilisateur connecté à l’ordinateur peut lancer la séquence de tâches à partir du média.  


 > [!IMPORTANT]  
 >  Les étapes d’une séquence de tâches de média autonome doivent pouvoir s’exécuter sans récupérer de données sur le réseau. Celles qui tentent de récupérer des données échouent. Par exemple, une étape de séquence de tâches qui oblige un point de distribution à obtenir un package échoue. Si le média autonome contient le package nécessaire, l’étape aboutit.  


 Pour plus d’informations, voir [Créer un média autonome](/sccm/osd/deploy-use/create-stand-alone-media).  

#### <a name="bootable-media"></a>Média de démarrage
 Un média de démarrage contient les fichiers nécessaires au démarrage d’un ordinateur de destination, lequel peut ainsi se connecter à l’infrastructure Configuration Manager. Il détermine ensuite les séquences de tâches à exécuter en fonction de son adhésion à des collections. Ce média n’inclut pas la séquence de tâches ou les objets dépendants. C’est le client qui télécharge le contenu sur le réseau. Cette méthode est utile pour les nouveaux ordinateurs et les déploiements complets, lorsque aucun système d’exploitation n’est installé sur l’ordinateur de destination.  

 Pour plus d’informations, consultez [Créer un média de démarrage](/sccm/osd/deploy-use/create-bootable-media).  

#### <a name="prestaged-media"></a>Média préparé
 Le média préparé déploie une image de système d’exploitation sur un ordinateur de destination non configuré. Il est stocké sous forme de fichier image Windows (WIM). Ce fichier peut être installé sur un système nu par le fabricant ou dans un centre de gestion intermédiaire d’entreprise. L’un des avantages des médias préparés est que ces emplacements ne nécessitent pas de connexion à votre environnement Configuration Manager.  

 Pour plus d’informations, consultez [Créer un média préparé](/sccm/osd/deploy-use/create-prestaged-media).  
