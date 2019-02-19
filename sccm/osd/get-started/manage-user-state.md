---
title: 'Gérer l’état utilisateur '
titleSuffix: Configuration Manager
description: System Center Configuration Manager utilise l’outil de migration de l’état utilisateur pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7f2e1521f6746d821258ef301a4df959c3cb559
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56140059"
---
# <a name="manage-user-state-in-system-center-configuration-manager"></a>Gérer l’état utilisateur dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser des séquences de tâches System Center Configuration Manager pour capturer et restaurer les données d’état utilisateur dans les scénarios de déploiement de système d’exploitation où vous souhaitez conserver l’état utilisateur du système d’exploitation actuel. Par exemple :  

- Déploiements dans lesquels vous voulez capturer l’état utilisateur d’un ordinateur pour le restaurer sur un autre ordinateur.  

- Déploiements de mise à jour dans lesquels vous voulez capturer et restaurer l'état utilisateur sur le même ordinateur.  

  Configuration Manager utilise la version 10.0 de l’outil de migration de l’état utilisateur (USMT) pour gérer la migration des données d’état utilisateur d’un ordinateur source vers un ordinateur de destination après l’installation du système d’exploitation. Pour plus d’informations sur les scénarios de migration courants pour la version 10.0 de l’outil USMT, consultez  [Scénarios de migration courants](https://technet.microsoft.com/library/mt299169\(v=vs.85\).aspx).  

  Aidez-vous des informations des sections suivantes pour capturer et restaurer les données d’état utilisateur.


##  <a name="BKMK_StoringUserData"></a> Stocker les données d’état utilisateur  
 Quand vous capturez l’état utilisateur, vous pouvez stocker les données d’état utilisateur sur l’ordinateur de destination ou sur un point de migration d’état. Pour stocker l’état utilisateur sur un point de migration d’état utilisateur, vous devez utiliser un serveur de système de site Configuration Manager qui héberge le rôle de système de site de point de migration d’état. Pour stocker l'état utilisateur sur l'ordinateur de destination, vous devez configurer votre séquence de tâches pour stocker les données utilisant localement des liens.  

> [!NOTE]  
>  Les liens qui sont utilisés pour stocker l'état utilisateur localement sont appelés liens physiques. Les liens physiques sont une fonctionnalité de l’outil USMT 10.0 qui analyse l’ordinateur à la recherche de fichiers et de paramètres utilisateur, et qui crée ensuite un répertoire de liens physiques vers ces fichiers. Les liens physiques sont ensuite utilisés pour restaurer les données utilisateur après le déploiement du nouveau système d'exploitation.  

> [!IMPORTANT]  
>  Vous ne pouvez pas utiliser un point de migration d'état et utiliser des liens physiques pour stocker les données d'état utilisateur en même temps.  

 Lorsque les informations d'état utilisateur sont capturées, elles peuvent être stockées selon l'une des manières suivantes :  

-   Vous pouvez stocker les données d'état utilisateur à distance en configurant un point de migration d'état. La séquence de tâches **Capturer** envoie les données au point de migration d’état. Ensuite, une fois le système d’exploitation déployé, la séquence de tâches **Restaurer** récupère les données et restaure l’état utilisateur sur l’ordinateur de destination.  

-   Vous pouvez stocker les données d'état utilisateur localement à un emplacement spécifique. Dans ce scénario, la séquence de tâches **Capturer** copie les données utilisateur vers un emplacement spécifique sur l’ordinateur de destination. Ensuite, une fois le système d’exploitation déployé, la séquence de tâches **Restaurer** récupère les données utilisateur à partir de cet emplacement.  

-   Vous pouvez spécifier les liens physiques qui peuvent être utilisés pour restaurer les données utilisateur vers leur emplacement d'origine. Dans ce scénario, les données d'état utilisateur restent sur le lecteur lorsque l'ancien système d'exploitation est supprimé. Ensuite, une fois le nouveau système d’exploitation déployé, la séquence de tâches **Restaurer** utilise les liens physiques pour restaurer les données d’état utilisateur vers leur emplacement d’origine.  

###  <a name="BKMK_UserDataSMP"></a> Stocker des données utilisateur sur un point de migration d’état  
 Pour stocker les données d’état utilisateur sur un point de migration d’état, vous devez procéder comme suit :  

1.  [Configure a state migration point](#BKMK_StateMigrationPoint) pour stocker les données d’état utilisateur.  

2.  [Create a computer association](#BKMK_ComputerAssociation) entre l’ordinateur source et l’ordinateur de destination. Vous devez créer cette association avant de capturer l'état utilisateur sur l'ordinateur source.  

3.  [Créez une séquence de tâches pour capturer et restaurer l’état utilisateur dans System Center Configuration Manager](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Plus précisément, vous devez ajouter les étapes de séquence de tâches suivantes pour capturer des données utilisateur à partir d’un ordinateur, stocker les données utilisateur sur un point de migration, puis restaurer les données utilisateur sur un ordinateur :  

    -   [Demandez le magasin d’état](../understand/task-sequence-steps.md#BKMK_RequestStateStore) pour demander l’accès à un point de migration d’état dans le cadre d’une capture d’état d’un ordinateur ou d’une restauration de l’état sur un ordinateur.  

    -   [Capturez l’état utilisateur](../understand/task-sequence-steps.md#BKMK_CaptureUserState) pour capturer et stocker les données d’état utilisateur sur le point de migration d’état.  

    -   [Restaurez l’état utilisateur](../understand/task-sequence-steps.md#BKMK_RestoreUserState) pour restaurer l’état utilisateur sur l’ordinateur de destination en récupérant les données à partir d’un point de migration d’état utilisateur.  

    -   [Libérez le magasin d’état](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore) pour signaler au point de migration d’état que l’action de capture ou de restauration est terminée.  

###  <a name="BKMK_UserDataDestination"></a> Stocker des données utilisateur localement  
 Pour stocker les données d’état utilisateur localement, vous devez procéder comme suit :  

-   [Créez une séquence de tâches pour capturer et restaurer l’état utilisateur](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md). Plus précisément, vous devez ajouter les étapes de séquence de tâches suivantes pour capturer des données utilisateur à partir d’un ordinateur et restaurer les données utilisateur sur un ordinateur à l’aide de liens physiques.  

    -   [Capturez l’état utilisateur](../understand/task-sequence-steps.md#BKMK_CaptureUserState) pour capturer et stocker les données d’état utilisateur dans un dossier local à l’aide de liens physiques.  

    -   [Restaurez l’état utilisateur](../understand/task-sequence-steps.md#BKMK_RestoreUserState) pour restaurer l’état utilisateur sur l’ordinateur de destination en récupérant les données à l’aide de liens physiques.  

        > [!NOTE]  
        >  Les données d'état utilisateur auxquelles font référence les liens physiques restent sur l'ordinateur une fois que la séquence de tâches a supprimé l'ancien système d'exploitation. Il s'agit de données qui sont utilisées pour restaurer l'état utilisateur lors du déploiement du nouveau système d'exploitation.  

##  <a name="BKMK_StateMigrationPoint"></a> Configure a state migration point  
 Le point de migration d'état stocke les données d'état utilisateur qui sont capturées sur un seul ordinateur puis restaurées sur un autre ordinateur. Toutefois, quand vous capturez des paramètres utilisateur pour un déploiement de système d’exploitation sur le même ordinateur, comme un déploiement où vous actualisez le système d’exploitation sur l’ordinateur de destination, vous pouvez stocker les données sur le même ordinateur à l’aide de liens physiques ou sur un point de migration d’état. Pour certains déploiements d’ordinateur, quand vous créez le magasin d’état, Configuration Manager crée automatiquement une association entre le magasin d’état et l’ordinateur de destination. Vous pouvez utiliser les méthodes suivantes afin de configurer un point de migration d'état pour stocker les données d'état utilisateur :  

- Utilisez l' **Assistant Création d'un serveur de système de site** pour créer un nouveau serveur de système de site pour le point de migration d'état.  

- Utilisez l' **Assistant Ajout des rôles de système de site** pour ajouter un point de migration d'état à un serveur existant.  

  Lorsque vous utilisez ces Assistants, vous êtes invité à fournir les informations suivantes pour le point de migration d'état :  

- Les dossiers pour stocker les données d'état utilisateur.  

- Le nombre maximal de clients pouvant stocker des données sur le point de migration d'état.  

- L'espace libre minimum pour le point de migration d'état pour stocker les données d'état utilisateur.  

- La stratégie de suppression du rôle. Vous pouvez spécifier que les données d'état utilisateur sont supprimées immédiatement après leur restauration sur un ordinateur, ou après un nombre de jours spécifique après la restauration des données utilisateur sur un ordinateur.  

- Si le point de migration d’état répond uniquement aux demandes de restauration des données d’état utilisateur. Lorsque vous activez cette option, vous ne pouvez pas utiliser le point de migration d'état pour stocker les données d'état utilisateur.  

  Pour plus d’informations sur le point de migration d’état et les étapes nécessaires pour le configurer, consultez [Point de migration d’état](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

##  <a name="BKMK_ComputerAssociation"></a> Create a computer association  
 Créez une association d’ordinateurs pour définir une relation entre un ordinateur source et un ordinateur de destination quand vous installez un système d’exploitation sur du nouveau matériel et que vous souhaitez capturer et restaurer les paramètres de données utilisateur. L’ordinateur source est un ordinateur existant qui est géré par Configuration Manager. Lorsque vous déployez le nouveau système d'exploitation sur l'ordinateur de destination, l'ordinateur source contient l'état utilisateur qui est migré vers l'ordinateur de destination.  

> [!NOTE]  
>  La création d’une association d’ordinateurs entre des ordinateurs situés dans un site parent Configuration Manager et des ordinateurs situés dans un site enfant n’est pas prise en charge. Les associations d’ordinateurs sont spécifiques à un site et ne sont pas répliquées.  

#### <a name="to-create-a-computer-association"></a>Pour créer une association d'ordinateurs  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  

2.  Dans l'espace de travail **Ressources et Conformité** , cliquez sur **Migration de l'état utilisateur**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une association d'ordinateurs**.  

4.  Dans l'onglet **Association d'ordinateurs** de la boîte de dialogue **Propriétés de l'association d'ordinateurs** , indiquez l'ordinateur source qui contient l'état utilisateur à capturer et l'ordinateur de destination sur lequel les données d'état utilisateur seront restaurées.  

5.  Dans l'onglet **Comptes d'utilisateur** , spécifiez les comptes d'utilisateur à migrer vers l'ordinateur de destination. Spécifiez l'un des paramètres suivants :  

    -   **Capturer et restaurer tous les comptes d’utilisateur :** ce paramètre capture et restaure tous les comptes d'utilisateur. Ce paramètre permet de créer plusieurs associations sur le même ordinateur source.  

    -   **Capturer tous les comptes d’utilisateur et restaurer les comptes spécifiés :** ce paramètre capture tous les comptes d'utilisateur sur l'ordinateur source et restaure uniquement les comptes que vous spécifiez sur l'ordinateur de destination. En outre, vous pouvez utiliser ce paramètre lorsque vous souhaitez créer plusieurs associations sur le même ordinateur source.  

    -   **Capturer et restaurer les comptes d’utilisateur spécifiés :** ce paramètre capture et restaure uniquement les comptes que vous spécifiez. Vous ne pouvez pas créer plusieurs associations sur le même ordinateur source lorsque vous sélectionnez ce paramètre.  

##  <a name="BKMK_MigrationFails"></a> Restaurer des données d’état utilisateur en cas d’échec d’un déploiement de système d’exploitation  
 Si le déploiement de système d’exploitation échoue, utilisez la fonctionnalité LoadState de l’outil USMT 10.0 pour récupérer les données d’état utilisateur capturées pendant le processus de déploiement. Ces données incluent notamment les données stockées sur un point de migration d'état ou les données enregistrées localement sur l'ordinateur de destination. Pour plus d'informations sur cette fonctionnalité d'USMT, voir [Syntaxe LoadState](https://technet.microsoft.com/library/mt299188\(v=vs.85\).aspx).  
