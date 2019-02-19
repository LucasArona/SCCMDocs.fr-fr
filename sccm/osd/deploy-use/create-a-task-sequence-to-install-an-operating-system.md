---
title: Créer une séquence de tâches pour installer un système d’exploitation
titleSuffix: Configuration Manager
description: Dans System Center Configuration Manager, utilisez des séquences de tâches pour installer automatiquement une image de système d’exploitation et d’autres contenus sur un ordinateur de destination.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c18d6320397281156e39624ea8dc50e6d0539ed
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56139906"
---
# <a name="create-a-task-sequence-to-install-an-operating-system-in-system-center-configuration-manager"></a>Créer une séquence de tâches pour installer un système d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, utilisez des séquences de tâches pour installer automatiquement une image de système d’exploitation sur un ordinateur de destination. Vous pouvez créer une séquence de tâches qui fasse référence à l’image de démarrage chargée de démarrer l’ordinateur de destination, à l’image du système d’exploitation que vous voulez installer sur l’ordinateur de destination et à tout autre contenu supplémentaire, par exemple les autres applications ou les mises à jour logicielles que vous voulez installer. Vous devez ensuite déployer la séquence de tâches sur le regroupement qui contient l’ordinateur de destination.  

##  <a name="BKMK_InstallOS"></a> Créer une séquence de tâches pour installer un système d’exploitation  
 Il existe de nombreux scénarios pour déployer un système d’exploitation sur les ordinateurs de votre environnement. Dans la plupart des cas, vous créez une séquence de tâches et vous sélectionnez **Installer un package d’images existant** dans l’Assistant Création d’une séquence de tâches pour installer le système d’exploitation, migrer des paramètres utilisateur, appliquer des mises à jour logicielles et installer des applications. Avant de créer une séquence de tâches pour installer un système d’exploitation, les conditions suivantes doivent être remplies :   

-   **Obligatoire**  

    -   L’[image de démarrage](../get-started/manage-boot-images.md) doit être disponible dans la console Configuration Manager.  

    -   Une [image de système d’exploitation](../get-started/manage-operating-system-images.md) doit être disponible dans la console Configuration Manager.  

-   **Obligatoire (si utilisé)**  

    -   Les [mises à jour logicielles](../../sum/get-started/synchronize-software-updates.md) doivent être synchronisées dans la console Configuration Manager.  

    -   Les [applications](../../apps/deploy-use/create-applications.md) doivent être ajoutées à la console Configuration Manager.  

#### <a name="to-create-a-task-sequence-that-installs-an-operating-system"></a>Pour créer une séquence de tâches qui installe un système d’exploitation  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une séquence de tâches** pour démarrer l'Assistant Création d'une séquence de tâches.  

4. Dans la page **Créer une séquence de tâches** , sélectionnez **Installer un package d'images existant**, puis cliquez sur **Suivant**.  

5. Sur la page **Informations sur la séquence de tâches** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

   -   **Nom de la séquence de tâches** : spécifiez un nom qui identifie la séquence de tâches.  

   -   **Description** : spécifiez une description de la tâche qui est effectuée par la séquence de tâches.  

   -   **Image de démarrage** : spécifiez l'image de démarrage qui installe le système d'exploitation sur l'ordinateur de destination. L'image de démarrage contient une version de Windows PE qui est utilisée pour installer le système d'exploitation, ainsi que les pilotes d'appareil supplémentaires qui sont requis. Pour plus d’informations, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

       > [!IMPORTANT]  
       >  L'architecture de l'image de démarrage doit être compatible avec l'architecture matérielle de l'ordinateur de destination.  

6. Sur la page **Installer Windows** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

   -   **Package d’images** : spécifiez le package qui contient l'image du système d'exploitation à installer. Pour plus d’informations, voir [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

   -   **Image** : si le package d'images du système d'exploitation comporte plusieurs images, spécifiez l'index de l'image du système d'exploitation à installer.  

   -   **Partitionnez et formatez l’ordinateur cible avant d’installer le système d’exploitation** : spécifiez si vous souhaitez que la séquence de tâches partitionne et formate l'ordinateur de destination avant que le système d'exploitation soit installé.  

   -   **Clé du produit** : spécifiez la clé de produit pour le système d'exploitation Windows à installer. Vous pouvez spécifier des clés de licence en volume codées et des clés de produit standard. Si vous utilisez une clé de produit non codée, chaque groupe de 5 caractères doit être séparé par un tiret (-). Par exemple : *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

   -   **Mode de licence serveur** : Indiquez que la licence serveur est **Par poste**, **Par serveur** ou qu’aucune licence n’est spécifiée. Si la licence serveur est **Par serveur**, spécifiez également le nombre maximal de connexions au serveur.  

   -   Spécifiez comment gérer le compte administrateur qui est utilisé lors du déploiement de l'image du système d'exploitation.  

       -   **Désactiver le compte administrateur local** : spécifiez si le compte administrateur local est désactivé lorsque l'image du système d'exploitation est déployée.  

       -   **Toujours utiliser le même mot de passe administrateur** : spécifiez si le même mot de passe est utilisé pour le compte administrateur local sur tous les ordinateurs où l'image du système d'exploitation est déployée.  

7. Sur la page **Configurer le réseau** , spécifiez les paramètres suivants et cliquez sur **Suivant**.  

   -   **Rejoindre un groupe de travail** : indiquez si vous souhaitez ajouter l'ordinateur de destination à un groupe de travail.  

   -   **Joindre un domaine** : indiquez si vous souhaitez ajouter l'ordinateur de destination à un domaine. Dans **Domaine**, spécifiez le nom du domaine.  

       > [!IMPORTANT]  
       >  Vous pouvez rechercher des domaines dans la forêt locale, mais vous devez spécifier le nom de domaine d'une forêt distante.  

        Vous pouvez également spécifier une unité d'organisation (UO). Il s'agit d'un paramètre facultatif qui spécifie le nom unique LDAP X.500 de l'UO dans laquelle vous créez le compte d'ordinateur s'il n'existe pas déjà.  

   -   **Compte** : spécifiez le nom d'utilisateur et le mot de passe du compte qui dispose des autorisations pour joindre le domaine spécifié. Par exemple : *domaine\utilisateur* ou *%variable%*.  

       > [!IMPORTANT]  
       >  Vous devez entrer les informations d'identification de domaine appropriées si vous prévoyez de migrer les paramètres du domaine ou les paramètres du groupe de travail.  

8. Dans la page **Installer Configuration Manager**, spécifiez le package client Configuration Manager à installer sur l’ordinateur de destination, puis cliquez sur **Suivant**.  

9. Sur la page **Migration de l'état** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Capturer les paramètres utilisateur** : spécifiez si la séquence de tâches capture l'état utilisateur. Pour plus d’informations sur la capture et la restauration de l’état utilisateur, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

    -   **Capturer les paramètres réseau** : spécifiez si la séquence de tâches capture les paramètres réseau de l'ordinateur de destination. Vous pouvez capturer l'appartenance du domaine ou du groupe de travail avec les paramètres de carte réseau.  

    -   **Capturer les paramètres Microsoft Windows** :  spécifiez si la séquence de tâches capture les paramètres Windows à partir de l'ordinateur de destination avant l'installation de l'image du système d'exploitation. Vous pouvez capturer le nom de l'ordinateur, les noms d'organisations et d'utilisateurs inscrits et les paramètres des fuseaux horaires.  

10. Sur la page **Inclure les mises à jour** , spécifiez si vous souhaitez installer les mises à jour logicielles requises, toutes les mises à jour logicielles ou aucune mise à jour logicielle, puis cliquez sur **Suivant**. Si vous spécifiez l’installation des mises à jour logicielles, Configuration Manager installe uniquement les mises à jour logicielles ciblant les regroupements auxquels l’ordinateur de destination appartient.  

11. Sur la page **Installer les applications** , spécifiez les applications à installer sur l'ordinateur de destination, puis cliquez sur **Suivant**. Si vous spécifiez plusieurs applications, vous pouvez également spécifier que la séquence de tâches continue si l'installation d'une application spécifique échoue.  

12. Effectuez toutes les étapes de l'Assistant.  

    Vous pouvez maintenant déployer la séquence de tâches dans un regroupement d’ordinateurs.  Pour plus d'informations, voir [Déployer une séquence de tâches](manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_InstallExistingOSImageTSExample"></a> Exemple de séquence de tâches pour installer une image de système d’exploitation existante  
 Utilisez le tableau suivant comme guide lorsque vous créez une séquence de tâches qui déploie un système d'exploitation à l'aide d'une image de système d'exploitation existante. Ce tableau vous aidera à définir la séquence générale des étapes de votre séquence de tâches. Il vous permettra également d'organiser et de structurer ces étapes en groupes logiques. La séquence de tâches que vous créez peut être différente de celle de cet exemple et elle peut contenir un nombre de groupes et d'étapes de séquence de tâches plus ou moins important.  

> [!IMPORTANT]  
>  Vous devez toujours utiliser l'Assistant Création d'une séquence de tâches pour créer cette séquence de tâches.  

 Lorsque vous utilisez l'Assistant Création d'une séquence de tâches pour créer cette nouvelle séquence de tâches, certains noms d'étapes de séquence de tâches sont différents des noms indiqués dans le cadre d'un ajout manuel de ces étapes de séquence de tâches à une séquence de tâches existante. Le tableau suivant présente les différences de dénomination :  

|Nom de l'étape de séquence de tâches de l'Assistant Création d'une séquence de tâches|Nom équivalent de l'étape dans l'Éditeur de séquence de tâches|  
|---------------------------------------------------------|-----------------------------------------------|  
|Demander le stockage de l'état utilisateur|Demander le magasin d'état|  
|Capturer les paramètres et fichiers utilisateur|Capturer l'état utilisateur|  
|Libérer le stockage de l'état utilisateur|Libérer le magasin d'état|  
|Redémarrer dans Windows PE|Redémarrer sur Windows PE ou disque dur|  
|Partitionner le disque 0|Formater et partitionner le disque|  
|Restaurer les fichiers et paramètres utilisateur|Restaurer l'état utilisateur|  

|Groupe ou étape de séquence de tâches|Description|  
|---------------------------------|-----------------|  
|Capturer les fichiers et les paramètres - **(Nouveau groupe de séquences de tâches)**|Créez un groupe de séquences de tâches. Un groupe de séquences de tâches regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.<br /><br /> Ce groupe contient les étapes nécessaires pour capturer des fichiers et des paramètres à partir du système d'exploitation d'un ordinateur de référence.|  
|Capturer les paramètres Windows|Utilisez cette étape de séquence de tâches pour identifier les paramètres Microsoft Windows pour capturer à partir de l'ordinateur de référence. Vous pouvez capturer le nom de l'ordinateur, les informations utilisateur et organisationnelles et les paramètres des fuseaux horaires.|  
|Capturer les paramètres réseau|Utilisez cette étape de séquence de tâches pour capturer les paramètres réseau à partir de l'ordinateur de référence. Vous pouvez capturer l'appartenance au domaine ou au groupe de travail de l'ordinateur de référence et les informations du paramètre de la carte réseau.|  
|Capturer les paramètres et fichiers utilisateur - **(Nouveau sous-groupe de séquences de tâches)**|Créez un groupe de séquences de tâches au sein d'un groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la capture des données d'état utilisateur. Comme le groupe initial que vous avez ajouté, ce sous-groupe regroupe des étapes de séquence de tâches similaires pour une meilleure organisation et un contrôle plus efficace des erreurs.|  
|Demander le stockage de l'état utilisateur|Utilisez cette étape de séquence de tâches pour demander l'accès à un point de migration d'état où sont stockées les données d'état utilisateur. Vous pouvez configurer cette étape de la séquence de tâches pour capturer ou restaurer les informations de l'état utilisateur.|  
|Capturer les paramètres et fichiers utilisateur|Utilisez cette étape de séquence de tâches pour utiliser l'outil de migration de l'état utilisateur pour capturer l'état utilisateur et les paramètres à partir de l'ordinateur de référence qui recevra la séquence de tâches associée à cette étape de tâche. Vous pouvez capturer les options standard ou configurer les options à capturer.|  
|Libérer le stockage de l'état utilisateur|Utilisez cette étape de séquence de tâches pour informer le point de migration d'état que l'opération de capture ou de restauration est terminée.|  
|Installer le système d'exploitation - **(Nouveau groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à l'installation et à la configuration de l'environnement Windows PE.|  
|Redémarrer dans Windows PE|Utilisez cette étape de séquence de tâches pour spécifier les options de redémarrage pour l'ordinateur de destination qui reçoit cette séquence de tâches. Cette étape affichera un message destiné à l'utilisateur et lui indiquant que l'ordinateur sera redémarré afin de poursuivre l'installation.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSInWinPE** en lecture seule. Si la valeur associée est **faux** , l'étape de séquence de tâches se poursuit.|  
|Partitionner le disque 0|Cette étape de séquence de tâches détermine les actions nécessaires au formatage du disque dur sur l'ordinateur de destination. Le numéro de disque par défaut est **0**.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSMediaType** en lecture seule. Elle sera exécutée en l’absence de mémoire cache du client Configuration Manager.|  
|Appliquer le système d'exploitation|Utilisez cette étape pour installer l'image de système d'exploitation sur l'ordinateur de destination. Cette étape applique toutes les images de volume contenues dans le fichier WIM au volume de disque séquentiel correspondant sur l’ordinateur cible après avoir d’abord supprimé tous les fichiers sur ce volume (à l’exception des fichiers de contrôle propres à Configuration Manager). Vous pouvez spécifier un fichier de réponse **sysprep** et également configurer la partition de disque utilisée pour l'installation.|  
|Appliquer les paramètres Windows|Utilisez cette étape de séquence de tâches pour configurer les informations de configuration des paramètres Windows pour l'ordinateur de destination. Les paramètres Windows que vous pouvez appliquer sont les informations utilisateur et organisationnelles, les informations principales sur le produit ou la clé de licence, les fuseaux horaires et le mot passe administrateur local.|  
|Appliquer les paramètres réseau|Utilisez cette étape de séquence de tâches pour spécifier les informations de configuration du réseau ou du groupe de travail pour l'ordinateur de destination. Vous pouvez également indiquer si l'ordinateur utilise un serveur DHCP ou vous pouvez attribuer en mode statique les informations de l'adresse IP.|  
|Appliquer les pilotes de périphériques|Utilisez cette étape de séquence de tâches pour installer des pilotes dans le cadre du déploiement de système d'exploitation. Vous pouvez autoriser le programme d'installation Windows à rechercher toutes les catégories de pilotes existantes en sélectionnant **Considérer les pilotes de toutes les catégories** . Vous pouvez également limiter les catégories de pilotes que le programme d'installation Windows doit rechercher en sélectionnant **Limiter la correspondance des pilotes aux pilotes des catégories sélectionnées uniquement**.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSMediaType** en lecture seule. Cette étape de séquence de tâches s'exécute uniquement si la valeur de la variable n'est pas **FullMedia**.|  
|Appliquer le package de pilotes|Utilisez cette étape de séquence de tâches pour que tous les pilotes de périphérique d'un package de pilotes puissent être utilisés par le programme d'installation de Windows.|  
|Configurer le système d'exploitation - **(Nouveau groupe de séquences de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la configuration du système d'exploitation.|  
|Configurer Windows et ConfigMgr|Cette étape de séquence de tâches permet d’installer le logiciel client Configuration Manager. Configuration Manager installe et inscrit le GUID du client Configuration Manager. Vous pouvez définir les paramètres d'installation nécessaires à partir de la fenêtre **Propriétés d'installation** .|  
|Installer les mises à jour|Utilisez cette étape de séquence de tâches pour spécifier la façon dont sont installées les mises à jour logicielles sur l'ordinateur de destination. L'ordinateur de destination n'est pas évalué pour déterminer les mises à jour logicielles applicables avant l'exécution de cette séquence de tâches. À ce stade, l’ordinateur de destination est évalué pour déterminer les mises à jour logicielles applicables comme n’importe quel autre client géré dans Configuration Manager.<br /><br /> Cette étape utilise la variable de séquence de tâches **_SMSTSMediaType** en lecture seule. Cette étape de séquence de tâches s'exécute uniquement si la valeur de la variable n'est pas **FullMedia**.|  
|Restaurer les fichiers et paramètres utilisateur - **(Nouveau sous-groupe de la séquence de tâches)**|Créez un autre sous-groupe de séquences de tâches. Ce sous-groupe contient les étapes nécessaires à la restauration des fichiers utilisateur et des paramètres.|  
|Demander le stockage de l'état utilisateur|Utilisez cette étape de séquence de tâches pour demander l'accès à un point de migration d'état où sont stockées les données d'état utilisateur.|  
|Restaurer les fichiers et paramètres utilisateur|Utilisez cette étape de séquence de tâches pour lancer l'outil de migration de l'état utilisateur afin de restaurer les paramètres et l'état utilisateur sur un ordinateur de destination.|  
|Libérer le stockage de l'état utilisateur|Utilisez cette étape de séquence de tâches pour informer le point de migration d’état que les données d’état d’utilisateur ne sont plus nécessaires.|  
