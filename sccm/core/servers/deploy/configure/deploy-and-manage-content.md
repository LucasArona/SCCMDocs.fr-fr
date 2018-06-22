---
title: Déployer du contenu
titleSuffix: Configuration Manager
description: Après avoir installé des points de distribution pour System Center Configuration Manager, voici comment commencer à y déployer du contenu.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: d50dcca0-4419-449d-a487-73abcadf328f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c6a2a69047a8fee5ab0c1f4f0f13197178334f05
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32342186"
---
# <a name="deploy-and-manage-content-for-system-center-configuration-manager"></a>Déployer et gérer du contenu pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir installé des points de distribution pour System Center Configuration Manager, vous pouvez commencer à y déployer du contenu. En règle générale, le contenu est transféré aux points de distribution via le réseau, mais il existe d’autres options pour placer du contenu aux points de distribution. Une fois le contenu transféré vers un point de distribution, vous pouvez mettre à jour, redistribuer, supprimer et valider ce contenu sur les points de distribution.  

##  <a name="bkmk_distribute"></a> Distribuer du contenu  
 En règle générale, vous distribuez du contenu sur des points de distribution pour le rendre accessible aux ordinateurs clients. (Ceci ne s’applique pas si vous utilisez la distribution de contenu à la demande pour un déploiement spécifique.)  Quand vous distribuez du contenu, Configuration Manager stocke les fichiers de contenu dans un package, puis distribue ce package sur le point de distribution. Les types de contenu que vous pouvez distribuer incluent les suivants :  

-   Types de déploiement d’application  

-   Packages  

-   Packages de déploiement  

-   Packages de pilotes  

-   Images du système d'exploitation  

-   Programmes d’installation de système d’exploitation  

-   Images de démarrage  

-   Séquences de tâches  

Quand vous créez un package qui contient des fichiers sources, tels qu'un type de déploiement d'application ou un package de déploiement, le site sur lequel le package est créé devient le site propriétaire de la source de contenu du package. Configuration Manager copie les fichiers sources à partir du chemin de fichier source spécifié pour l’objet vers la bibliothèque de contenu située sur le serveur de site propriétaire de la source de contenu du package.  Ensuite, Configuration Manager réplique les informations vers les sites supplémentaires. (Pour plus d’informations à ce sujet, consultez [Bibliothèque de contenu](../../../../core/plan-design/hierarchy/the-content-library.md).)  

Pour distribuer du contenu vers les points de distribution, procédez comme suit.  

#### <a name="to-distribute-content-on-distribution-points"></a>Pour distribuer du contenu vers les points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une des étapes suivantes pour le type de contenu que vous souhaitez distribuer :  

    -   **Applications** : Développez **Gestion d’applications** > **Applications**, puis sélectionnez les applications à distribuer.  

    -   **Packages** : Développez **Gestion d’applications** >  **Packages**, puis sélectionnez les packages à distribuer.  

    -   **Packages de déploiement** : Développez **Mises à jour logicielles** >  **Packages de déploiement**, puis sélectionnez les packages de déploiement à distribuer.  

    -   **Packages de pilotes** : Développez **Systèmes d’exploitation** >  **Packages de pilotes**, puis sélectionnez les packages de pilotes à distribuer.  

    -   **Images de système d’exploitation** : Développez **Systèmes d’exploitation** >  **Images du système d’exploitation**, puis sélectionnez les images de système d’exploitation à distribuer.  

    -   **Programmes de système d’exploitation** : Développez **Systèmes d’exploitation** > **Programmes d’installation de système d’exploitation**, puis sélectionnez les programmes d’installation de système d’exploitation à distribuer.  

    -   **Images de démarrage** : Développez **Systèmes d’exploitation** >  **Images de démarrage**, puis sélectionnez les images de démarrage à distribuer.  

    -   **Séquences de tâches** : Développez **Systèmes d’exploitation** >  **Séquences de tâches**, puis sélectionnez la séquence de tâches à distribuer. Les séquences de tâches ne contiennent pas de contenu, mais elles comportent des dépendances de contenu associées qui sont distribuées.  

        > [!NOTE]  
        >  Si vous modifiez la séquence de tâches, vous devez redistribuer le contenu.  

3.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Distribuer du contenu**. L'Assistant Distribuer du contenu s'ouvre.  

4.  Sur la page **Général**, vérifiez que le contenu affiché correspond bien au contenu que vous voulez distribuer, indiquez si vous voulez que Configuration Manager détecte les dépendances de contenu associées au contenu sélectionné et ajoutez les dépendances à la distribution avant de cliquer sur **Suivant**.  

    > [!NOTE]  
    >  Vous pouvez configurer le paramètre **Détecter les dépendances de contenu associées et les ajouter à cette distribution** pour le type de contenu d'application uniquement. Configuration Manager configure automatiquement ce paramètre pour les séquences de tâches et il ne peut pas être modifié.  

5.  Dans l'onglet **Contenu** , s'il s'affiche, vérifiez que le contenu répertorié correspond au contenu que vous voulez distribuer, puis cliquez sur **Suivant**.  

    > [!NOTE]  
    >  La page **Contenu** s'affiche uniquement lorsque le paramètre **Détecter les dépendances de contenu associées et les ajouter à cette distribution** est sélectionné sur la page **Général** de l'Assistant.  

6.  Sur la page **Destination du contenu** , cliquez sur **Ajouter**, choisissez l'une des opérations suivantes, puis suivez l'étape associée :  

    -   **Regroupements**: sélectionnez **Regroupements d'utilisateurs** ou **Regroupements d'appareils**, cliquez sur le regroupement associé à un ou plusieurs groupes de points de distribution, puis sur **OK**.  

        > [!NOTE]  
        >  Seuls les regroupements qui sont associés à un groupe de points de distribution sont affichés. Pour plus d’informations sur l’association des regroupements et des groupes de points de distribution, consultez [Gérer les groupes de points de distribution](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) dans la rubrique [Installer et configurer des points de distribution pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    -   **Point de distribution**: sélectionnez un point de distribution existant, puis cliquez sur **OK**. Les points de distribution ayant précédemment reçu le contenu ne sont pas affichés.  

    -   **Groupe de points de distribution**: sélectionnez un groupe de points de distribution existant, puis cliquez sur **OK**. Les groupes de points de distribution ayant précédemment reçu le contenu ne sont pas affichés.  

    Lorsque vous avez terminé d'ajouter des destinations de contenu, cliquez sur **Suivant**.  

7.  Sur la page **Résumé** , vérifiez les paramètres de la distribution avant de continuer. Pour distribuer le contenu vers les destinations sélectionnées, cliquez sur **Suivant**.  

8.  La page **Progression** affiche la progression de la distribution.  

9. La page **Confirmation** affiche si le contenu a été bien attribué avec succès aux points de distribution. Pour surveiller la distribution de contenu, consultez [Surveiller le contenu que vous avez distribué avec System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

##  <a name="bkmk_prestage"></a> Utiliser le contenu préparé  
 Vous pouvez préparer des fichiers de contenu pour les applications et les types de packages :  

-   Dans la console Configuration Manager, vous sélectionnez le contenu dont vous avez besoin, puis utilisez l’**Assistant Création du fichier de contenu préparé** pour créer un fichier de contenu préparé compressé qui contient les fichiers et les métadonnées associées pour le contenu que vous avez sélectionné.  

-   Vous pouvez ensuite importer manuellement le contenu au niveau d'un serveur de site, d'un site secondaire ou d'un point de distribution.  

-   Lorsque vous importez le fichier de contenu préparé sur un serveur de site, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le serveur de site, puis enregistrés dans la base de données du serveur de site.  

-   Lorsque vous importez le fichier de contenu préparé sur un point de distribution, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le point de distribution, et un message d'état est envoyé au serveur de site qui informe le site que le contenu est disponible sur le point de distribution.  

**Limitations et éléments à prendre en compte pour le contenu préparé :**  

-   **Si le point de distribution est situé sur le serveur de site**, n’activez pas le point de distribution pour le contenu préparé. Au lieu de cela, procédez comme indiqué dans [Guide pratique pour préparer du contenu sur un point de distribution situé sur un serveur de site](#bkmk_dpsiteserver).  

-   **Si le point de distribution est configuré en tant que point de distribution d’extraction**, n’activez pas le point de distribution pour le contenu préparé. La configuration de contenu préparé pour un point de distribution se substitue à la configuration du point de distribution d'extraction. Un point de distribution d'extraction configuré pour du contenu préparé n'extrait pas de contenu auprès d'un point de distribution source et ne reçoit pas de contenu du serveur de site.  

-   **Vous devez créer la bibliothèque de contenu sur le point de distribution avant de préparer le contenu pour ce point de distribution**. Distribuez le contenu sur le réseau au moins une fois avant de préparer le contenu vers le point de distribution.  

-   **Lorsque vous préparez du contenu pour un package dont le chemin source est particulièrement long** (plus de 140 caractères, par exemple), l’outil en ligne de commande d’extraction de contenu risque de ne pas réussir à extraire le contenu de ce package vers la bibliothèque de contenu.  

Pour plus d’informations sur le moment propice à la préparation des fichiers de contenu, consultez *Contenu préparé* dans la rubrique [Gérer la bande passante du réseau pour la gestion de contenu](/sccm/core/plan-design/hierarchy/manage-network-bandwidth).  

Utilisez les sections suivantes pour préparer du contenu.  

###  <a name="BKMK_CreatePrestagedContentFile"></a> Étape 1 : Créer un fichier de contenu préparé  
 Vous pouvez créer un fichier de contenu préparé et compressé qui contient les fichiers et les métadonnées associées pour le contenu que vous sélectionnez dans la console Configuration Manager. Pour créer un fichier de contenu préparé, procédez comme suit.  

##### <a name="to-create-a-prestaged-content-file"></a>Pour créer un fichier de contenu préparé  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une des étapes suivantes pour le type de contenu que vous souhaitez préparer :  

    -   **Applications**: développez **Gestion d'applications**, cliquez sur **Applications**, puis sélectionnez les applications que vous souhaitez préparer.  

    -   **Packages**: développez **Gestion d'applications**, cliquez sur **Packages**, puis sélectionnez les packages que vous souhaitez préparer.  

    -   **Packages de pilotes**: développez **Systèmes d'exploitation**, cliquez sur **Packages de pilotes**, puis sélectionnez les packages de pilotes que vous souhaitez préparer.  

    -   **Images du système d'exploitation**: développez **Systèmes d'exploitation**, cliquez sur **Images du système d'exploitation**, puis sélectionnez les images du système d'exploitation que vous souhaitez préparer.  

    -   **Programmes d'installation de système d'exploitation**: développez **Systèmes d'exploitation**, cliquez sur **Programmes d'installation de système d'exploitation**, puis sélectionnez les programmes d'installation de système d'exploitation que vous souhaitez préparer.  

    -   **Images de démarrage**: développez **Systèmes d'exploitation**, cliquez sur **Images de démarrage**, puis sélectionnez les images de démarrage que vous souhaitez préparer.  

    -   **Séquences de tâches**: Développez **Systèmes d'exploitation**, cliquez sur **Séquences de tâches**, puis sélectionnez les séquences de tâches que vous souhaitez préparer.  

3.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Créer un fichier de contenu préparé**. L'Assistant Création du fichier de contenu préparé s'ouvre.  

    > [!NOTE]  
    >  **Pour les applications :** Sous l’onglet **Accueil**, dans le groupe **Application**, cliquez sur **Créer un fichier de contenu préparé**.  
    >   
    >  **Pour les packages :** Sous l’onglet **Accueil**, dans le groupe &lt;*nom_package*>, cliquez sur **Créer un fichier de contenu préparé**.  

4.  Sur la page **Général** , cliquez sur **Parcourir**, choisissez l'emplacement pour le fichier de contenu préparé, spécifiez un nom pour le fichier, puis cliquez sur **Enregistrer**. Vous utilisez ce fichier de contenu préparé sur des serveurs de site principaux, des serveurs de site secondaires ou des points de distribution afin d'importer le contenu et les métadonnées.  

5.  Pour les applications, sélectionnez **Exporter toutes les dépendances** afin que Configuration Manager détecte et ajoute les dépendances associées à l’application au fichier de contenu préparé. Ce paramètre est activé par défaut.  

6.  Dans **Commentaires de l'administrateur**, saisissez des commentaires facultatifs concernant le fichier de contenu préparé, puis cliquez sur **Suivant**.  

7.  Sur la page **Contenu** , vérifiez que le contenu répertorié correspond au contenu que vous souhaitez ajouter au fichier de contenu préparé, puis cliquez sur **Suivant**.  

8.  Sur la page **Emplacements du contenu** , spécifiez les points de distribution à partir desquels vous souhaitez récupérer les fichiers de contenu pour le fichier de contenu préparé. Vous pouvez sélectionner plusieurs points de distribution pour récupérer le contenu. Les points de distribution sont répertoriés dans la section Emplacements du contenu. La colonne **Contenu** affiche le nombre de packages ou applications sélectionnés disponibles sur chaque point de distribution. Configuration Manager commence par le premier point de distribution de la liste pour récupérer le contenu sélectionné, puis descend dans la liste afin de récupérer le contenu restant requis pour le fichier de contenu préparé. Cliquez sur **Monter** ou **Descendre** pour modifier l'ordre de priorité des points de distribution. Si les points de distribution de la liste ne contiennent pas tout le contenu sélectionné, vous devez ajouter des points de distribution à la liste contenant le contenu ou fermer l'Assistant, distribuer le contenu à un point de distribution au moins, puis redémarrer l'Assistant.  

9. Sur la page **Résumé** , vérifiez les détails. Vous pouvez revenir aux pages précédentes et apporter des modifications. Cliquez sur **Suivant** pour créer le fichier de contenu préparé.  

10. La page **Progression** affiche le contenu qui est ajouté au fichier de contenu préparé.  

11. Sur la page **Dernière étape** , vérifiez que le fichier de contenu préparé a été créé correctement, puis cliquez sur **Fermer**.  

###  <a name="BKMK_AssignContentToDistributionPoint"></a> Étape 2 : Affecter le contenu aux points de distribution  
 Après avoir préparé le fichier de contenu, attribuez le contenu aux points de distribution.  

> [!NOTE]  
>  Si vous utilisez un fichier de contenu préparé pour récupérer la bibliothèque de contenu sur un serveur de site et n'êtes pas obligé de préparer les fichiers de contenu sur un point de distribution, vous pouvez ignorer cette procédure.  

 Pour affecter le contenu du fichier de contenu préparé aux points de distribution, procédez comme suit.  

> [!IMPORTANT]  
>  Vérifiez que les points de distribution que vous souhaitez préparer sont configurés comme des points de distribution préparés ou que le contenu est distribué aux points de distribution via le réseau.  

##### <a name="to-assign-the-content-to-distribution-points"></a>Pour affecter le contenu aux points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une des étapes suivantes pour le type de contenu que vous avez sélectionné lorsque vous avez créé le fichier de contenu préparé :  

    -   **Applications**: développez **Gestion d'applications**, cliquez sur **Applications**, puis sélectionnez les applications que vous avez préparées.  

    -   **Packages**: développez **Gestion d'applications**, cliquez sur **Packages**, puis sélectionnez les Packages que vous avez préparés.  

    -   **Packages de déploiement**: développez **Mises à jour logicielles**, cliquez sur **Packages de déploiement**, puis sélectionnez les packages de déploiement que vous avez préparés.  

    -   **Packages de pilotes**: développez **Systèmes d'exploitation**, cliquez sur **Packages de pilotes**, puis sélectionnez les packages de pilotes que vous avez préparés.  

    -   **Images du système d'exploitation**: développez **Systèmes d'exploitation**, cliquez sur **Images du système d'exploitation**, puis sélectionnez les images du système d'exploitation que vous avez préparées.  

    -   **Programmes d'installation de système d'exploitation**: développez **Systèmes d'exploitation**, cliquez sur **Programmes d'installation de système d'exploitation**, puis sélectionnez les programmes d'installation de système d'exploitation que vous avez préparés.  

    -   **Images de démarrage**: développez **Systèmes d'exploitation**, cliquez sur **Images de démarrage**, puis sélectionnez les images de démarrage que vous avez préparées.  

3.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Distribuer du contenu**. L'Assistant Distribuer du contenu s'ouvre.  

4.  Sur la page **Général** , vérifiez que le contenu affiché correspond bien au contenu que vous avez préparé, indiquez si vous voulez que Configuration Manager détecte les dépendances de contenu associées au contenu sélectionné et ajoutez les dépendances à la distribution avant de cliquer sur **Suivant**.  

    > [!NOTE]  
    >  Vous pouvez configurer le paramètre **Détecter les dépendances de contenu associées et les ajouter à cette distribution** pour le type de contenu d'application uniquement. Configuration Manager configure automatiquement ce paramètre pour les séquences de tâches et il ne peut pas être modifié.  

5.  Sur la page **Contenu** , si elle s'affiche, vérifiez que le contenu répertorié correspond au contenu que vous voulez distribuer, puis cliquez sur **Suivant**.  

    > [!NOTE]  
    >  La page **Contenu** s'affiche uniquement lorsque le paramètre **Détecter les dépendances de contenu associées et les ajouter à cette distribution** est sélectionné sur la page **Général** de l'Assistant.  

6.  Sur la page **Destination du contenu** , cliquez sur **Ajouter**, choisissez l'une des opérations suivantes qui inclut les points de distribution à préinstaller, puis suivez l'étape associée :  

    -   **Regroupements**: sélectionnez **Regroupements d'utilisateurs** ou **Regroupements d'appareils**, cliquez sur le regroupement associé à un ou plusieurs groupes de points de distribution, puis sur **OK**.  

        > [!NOTE]  
        >  Seuls les regroupements qui sont associés à un groupe de points de distribution sont affichés.  Pour plus d’informations, consultez [Gérer les groupes de points de distribution](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_manage) dans la rubrique [Installer et configurer des points de distribution pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  

    -   **Point de distribution**: sélectionnez un point de distribution existant, puis cliquez sur **OK**. Les points de distribution ayant précédemment reçu le contenu ne sont pas affichés.  

    -   **Groupe de points de distribution**: sélectionnez un groupe de points de distribution existant, puis cliquez sur **OK**. Les groupes de points de distribution ayant précédemment reçu le contenu ne sont pas affichés.  

    Lorsque vous avez terminé d'ajouter des destinations de contenu, cliquez sur **Suivant**.  

7.  Sur la page **Résumé** , vérifiez les paramètres de la distribution avant de continuer. Pour distribuer le contenu vers les destinations sélectionnées, cliquez sur **Suivant**.  

8.  La page **Progression** affiche la progression de la distribution.  

9. La page **Confirmation** affiche si le contenu a été bien attribué avec succès aux points de distribution. Pour surveiller la distribution de contenu, consultez [Surveiller le contenu que vous avez distribué avec System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

###  <a name="BKMK_ExportContentFromPrestagedContentFile"></a> Étape 3 : Extraire le contenu du fichier de contenu préparé  
 Une fois que vous avez créé le fichier de contenu préparé et que vous avez attribué le contenu aux points de distribution, vous pouvez extraire les fichiers de contenu vers la bibliothèque de contenu d'un serveur de site ou d'un point de distribution. Généralement, vous avez copié le fichier de contenu préparé vers un lecteur portable, tel qu’un lecteur USB, ou gravé le contenu sur un support, tel qu’un DVD, puis vous l’avez mis à disposition à l’emplacement du serveur de site ou du point de distribution qui demande le contenu.  

 Pour exporter manuellement les fichiers de contenu à partir du fichier de contenu préparé à l'aide de l'outil de ligne de commande Extraire le contenu, procédez comme suit.  

> [!IMPORTANT]  
>  Lorsque vous exécutez l'outil d'extraction de contenu en ligne de commande, l'outil crée un fichier temporaire lors de la création du fichier de contenu préparé. Le fichier est ensuite copié dans le dossier de destination, puis supprimé. Vous devez disposer de suffisamment d'espace disque pour stocker ce fichier temporaire. Sinon, le processus échoue. Le fichier temporaire est créé à l'emplacement suivant :  
>   
>  -   Le fichier temporaire est créé dans le même dossier que celui spécifié comme dossier de destination du fichier de contenu préparé.  

> [!IMPORTANT]  
>  L’utilisateur qui exécute l’outil en ligne de commande d’extraction de contenu doit disposer de droits d’**administrateur** sur l’ordinateur à partir duquel vous extrayez le contenu préparé.  

##### <a name="to-extract-the-content-files-from-the-prestaged-content-file"></a>Pour extraire les fichiers de contenu du fichier de contenu préparé  

1.  Copiez le fichier de contenu préparé à l'ordinateur à partir duquel vous souhaitez extraire le contenu.  

2.  Copiez l’outil en ligne de commande d’extraction de contenu depuis &lt;*chemin_installation_Configuration_Manager*>\bin\\&lt;*plateforme*> sur l’ordinateur à partir duquel vous souhaitez extraire le fichier de contenu préparé.  

3.  Ouvrez l'invite de commandes et accédez à l'emplacement du dossier du fichier de contenu préparé et l'outil Extraire le contenu.  

    > [!NOTE]  
    >  Vous pouvez extraire un ou plusieurs fichiers de contenu préparé sur un serveur de site, un serveur de site secondaire ou un point de distribution.  

4.  Tapez **extractcontent /P:**&lt;*emplacement_fichier_préparé*>**\\**&lt;*nom_fichier_préparé*> **/S** pour importer un seul fichier.  

     Tapez **extractcontent /P:**&lt;*emplacement_fichier_préparé*> **/S** pour importer tous les fichiers préparés dans le dossier spécifié.  

     Par exemple, tapez **extractcontent /P:D:\PrestagedFiles\MyPrestagedFile.pkgx /S** où `D:\PrestagedFiles\` est l’emplacement du fichier préparé, `MyPrestagedFile.pkgx` est le nom du fichier préparé et `/S` informe Configuration Manager d’extraire uniquement les fichiers de contenu qui sont plus récents que ce qui se trouve actuellement sur le point de distribution.  

     Lorsque vous extrayez le fichier de contenu préparé sur un serveur de site, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le serveur de site, puis la disponibilité du contenu est enregistrée dans la base de données du serveur de site. Lorsque vous exportez le fichier de contenu préparé sur un point de distribution, les fichiers de contenu sont ajoutés à la bibliothèque de contenu sur le point de distribution, ce dernier envoie un message d'état au serveur de site principal parent, puis la disponibilité du contenu est enregistrée dans la base de données du site.  

    > [!IMPORTANT]  
    >  Dans le scénario suivant, vous devez mettre à jour le contenu que vous avez extrait à partir d'un fichier de contenu préparé lorsque le contenu est mis à jour vers une nouvelle version :  
    >   
    >  1.  Vous créez un fichier de contenu préparé pour la version 1 d'un package.  
    >  2.  Vous mettez à jour les fichiers sources pour le package avec la version 2.  
    >  3.  Vous extrayez le fichier de contenu préparé (version 1 du package) sur un point de distribution.  
    >   
    > Configuration Manager ne distribue pas automatiquement le package version 2 vers le point de distribution. Vous devez créer un nouveau fichier de contenu préparé contenant la nouvelle version du fichier, puis extraire le contenu, mettre à jour le point de distribution pour distribuer les fichiers qui ont été modifiés ou redistribuer tous les fichiers du package.  

###  <a name="bkmk_dpsiteserver"></a> Guide pratique pour préparer du contenu sur un point de distribution situé sur un serveur de site  
 Lorsqu'un point de distribution est installé sur un serveur de site, vous devez suivre la procédure suivante pour préparer correctement le contenu. Cela est dû au fait que les fichiers de contenu se trouvent déjà dans la bibliothèque de contenu.  

 Lorsqu’un point de distribution n’est pas activé pour préparer le contenu ou lorsque le point de distribution ne se trouve pas sur un serveur de site, consultez la section [Utilisation de contenu préparé](#bkmk_prestage) dans cette rubrique.  

##### <a name="to-prestage-content-on-distribution-points-located-on-a-site-server"></a>Pour préparer du contenu sur des points de distribution situés sur un serveur de site  

1.  Utilisez les étapes suivantes pour vérifier que le point de distribution n'est pas activé pour le contenu préparé.  

    1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

    2.  Dans l'espace de travail **Administration** , cliquez sur **Points de distribution**et sélectionnez le point de distribution situé sur le serveur de site.  

    3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

    4.  Dans l'onglet **Général** , vérifiez que la case **Activer ce point de distribution pour le contenu préparé** est décochée.  

2.  Créez le fichier de contenu préparé en suivant la section [Étape 1 : Créer un fichier de contenu préparé](#BKMK_CreatePrestagedContentFile) dans cette rubrique.  

3.  Affectez le contenu au point de distribution en suivant la section [Étape 2 : Affecter le contenu aux points de distribution](#BKMK_AssignContentToDistributionPoint) dans cette rubrique.  

4.  Sur le serveur de site, extrayez le contenu du fichier de contenu préparé en suivant la section [Étape 3 : Extraire le contenu du fichier de contenu préparé](#BKMK_ExportContentFromPrestagedContentFile) dans cette rubrique.  

    > [!NOTE]  
    >  Lorsque le point de distribution est situé sur un site secondaire, patientez au moins 10 minutes, puis utilisez une console Configuration Manager connectée au site principal parent pour affecter le contenu au point de distribution sur le site secondaire.  

##  <a name="bkmk_manage"></a> Gérer le contenu que vous avez distribué  
 Vous disposez des options suivantes pour gérer le contenu :  
 - [Mettre à jour le contenu](#update-content)
 - [Redistribuer le contenu](#redistribute-content)
 - [Supprimer le contenu](#remove-content)
 - [Valider le contenu](#validate-content)

### <a name="update-content"></a>Mettre à jour le contenu
Si l’emplacement du fichier source d’un déploiement est mis à jour par l’ajout de nouveaux fichiers ou le remplacement de fichiers existants par d’autres plus récents, vous pouvez mettre à jour les fichiers de contenu sur les points de distribution à l’aide de l’action **Mettre à jour les points de distribution** ou **Mettre à jour le contenu** :  
-   Les fichiers de contenu sont copiés du chemin source vers la bibliothèque de contenu sur le site propriétaire de la source du contenu du package.  
-   La version du package est incrémentée.  
-   Chaque instance de la bibliothèque de contenu sur les serveurs de site et sur les points de distribution est mise à jour uniquement avec les fichiers qui ont été modifiés.  

> [!WARNING]  
>  La version du package pour les applications est toujours 1. Quand vous mettez à jour le contenu pour un type de déploiement d’application, Configuration Manager crée un ID de contenu pour le type de déploiement, et le package fait référence à ce nouvel ID de contenu.  

#### <a name="to-update-content-on-distribution-points"></a>Pour mettre à jour du contenu sur les points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une des étapes suivantes pour le type de contenu que vous souhaitez distribuer :  

    -   **Applications** : Développez **Gestion d’applications** > **Applications**, puis sélectionnez les applications à distribuer. Cliquez sur l'onglet **Types de déploiement** , puis sélectionnez le type de déploiement à mettre à jour.  

    -   **Packages** : Développez **Gestion d’applications** > **Packages**, puis sélectionnez les packages à mettre à jour.  

    -   **Packages de déploiement** : Développez **Mises à jour logicielles** > **Packages de déploiement**, puis sélectionnez les packages de déploiement à mettre à jour.  

    -   **Packages de pilotes** : Développez **Systèmes d’exploitation** > **Packages de pilotes**, puis sélectionnez les packages de pilotes à mettre à jour.  

    -   **Images de système d’exploitation** : Développez **Systèmes d’exploitation** > **Images du système d’exploitation**, puis sélectionnez les images de système d’exploitation à mettre à jour.  

    -   **Programmes de système d’exploitation** : Développez **Systèmes d’exploitation** > **Programmes d’installation de système d’exploitation**, puis sélectionnez les programmes d’installation de système d’exploitation à mettre à jour.  

    -   **Images de démarrage** : Développez **Systèmes d’exploitation** >  **Images de démarrage**, puis sélectionnez les images de démarrage à mettre à jour.  

3.  Dans l'onglet **Accueil** , cliquez sur le groupe **Déploiement** , cliquez sur **Mettre à jour les points de distribution**, puis cliquez sur **OK** pour confirmer la mise à jour du contenu.  

    > [!NOTE]  
    >  Pour mettre à jour le contenu pour les applications, cliquez sur l'onglet **Types de déploiement** , cliquez avec le bouton droit sur le type de déploiement, cliquez sur **Mettre à jour le contenu**, puis cliquez sur **OK** pour confirmer l'actualisation du contenu.  

    > [!NOTE]  
    >  Lorsque vous mettez à jour du contenu pour les images de démarrage, l'Assistant Gestion des points de distribution s'ouvre. Vérifiez les informations sur la **Résumé** , puis effectuez toutes les étapes de l'Assistant pour mettre à jour le contenu.  

### <a name="redistribute-content"></a>Redistribuer le contenu
Vous pouvez redistribuer un package pour copier tous les fichiers de contenu dans le package vers des points de distribution ou des groupes de points de distribution, et remplacer les fichiers existants.  

 Utilisez cette option pour réparer les fichiers de contenu dans le package ou pour renvoyer le contenu après un échec de la distribution initiale. Vous pouvez redistribuer un package à partir des propriétés suivantes :  

-   Propriétés du package  
-   Propriétés du point de distribution  
-   Propriétés du groupe de points de distribution  


#### <a name="to-redistribute-content-from-package-properties"></a>Pour redistribuer du contenu à partir des propriétés de package  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une des étapes suivantes pour le type de contenu que vous souhaitez distribuer :  

    -   **Applications** : Développez **Gestion d’applications** >  **Applications**, puis sélectionnez l’application à redistribuer.  

    -   **Packages** : Développez **Gestion d’applications** > **Packages**, puis sélectionnez le package à redistribuer.  

    -   **Packages de déploiement** : Développez **Mises à jour logicielles** >  **Packages de déploiement**, puis sélectionnez le package de déploiement à redistribuer.  

    -   **Packages de pilotes** : Développez **Systèmes d’exploitation** > **Packages de pilotes**, puis sélectionnez le package de pilote à redistribuer.  

    -   **Images de système d’exploitation** : Développez **Systèmes d’exploitation** > **Images du système d’exploitation**, puis sélectionnez l’image du système d’exploitation à redistribuer.  

    -   **Programmes de système d’exploitation** : Développez **Systèmes d’exploitation** > **Programmes d’installation de système d’exploitation**, puis sélectionnez le programme d’installation de système d’exploitation à redistribuer.  

    -   **Images de démarrage** : Développez **Systèmes d’exploitation** >  **Images de démarrage**, puis sélectionnez l’image de démarrage à redistribuer.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Cliquez sur l'onglet **Emplacements du contenu** , sélectionnez le point de distribution ou le groupe de points de distribution dans lequel vous souhaitez redistribuer le contenu, cliquez sur **Redistribuer**, puis cliquez sur **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-properties"></a>Pour redistribuer du contenu à partir des propriétés de package de point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Points de distribution**, puis sélectionnez le point de distribution dans lequel vous souhaitez redistribuer du contenu.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Cliquez sur l'onglet **Contenu** , sélectionnez le contenu à redistribuer, cliquez sur **Redistribuer**, puis cliquez sur **OK**.  

#### <a name="to-redistribute-content-from-distribution-point-group-properties"></a>Pour redistribuer du contenu des propriétés du groupe de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Groupes de points de distribution**, puis sélectionnez le groupe de points de distribution dont vous souhaitez redistribuer du contenu.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Cliquez sur l'onglet **Contenu** , sélectionnez le contenu à redistribuer, cliquez sur **Redistribuer**, puis cliquez sur **OK**.  

    > [!IMPORTANT]  
    >  Le contenu du package est redistribué à tous les points de distribution du groupe de points de distribution.  


#### <a name="use-the-sdk-to-force-replication-of-content"></a>Utiliser le SDK pour forcer la réplication de contenu
Vous pouvez utiliser la méthode de classe WMI (Windows Management Instrumentation) **RetryContentReplication** à partir du SDK Configuration Manager pour forcer le gestionnaire de distribution à copier le contenu de l’emplacement source vers la bibliothèque de contenu.  

Utilisez uniquement cette méthode pour forcer la réplication quand vous devez redistribuer le contenu après avoir rencontré des problèmes lors de la réplication normale de contenu (généralement validée à l’aide du nœud Surveillance de la console).   

Pour plus d’informations sur cette option SDK, consultez [RetryContentReplication Method in Class SMS_CM_UpdatePackages](https://msdn.microsoft.com/library/mt762092(CMSDK.16).aspx) (Méthode RetryContentReplication dans la classe SMS_CM_UpdatePackages) sur MSDN.Microsoft.com.

### <a name="remove-content"></a>Supprimer le contenu
Si vous n'avez plus besoin de contenu sur vos points de distribution, vous pouvez supprimer les fichiers de contenu sur le point de distribution.  

-   Propriétés du package  
-   Propriétés du point de distribution  
-   Propriétés du groupe de points de distribution  

Cependant, si le contenu est associé à un autre package qui a été distribué au même point de distribution, vous ne pouvez pas le supprimer.  

#### <a name="to-remove-package-content-files-from-distribution-points"></a>Pour supprimer les fichiers de contenu de package de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une de ces étapes pour le type de contenu que vous souhaitez supprimer :  

    -   **Applications** : Développez **Gestion d’applications** > **Applications**, puis sélectionnez l’application à supprimer.  

    -   **Packages** : Développez **Gestion d’applications** > **Packages**, puis sélectionnez le package à supprimer.  

    -   **Packages de déploiement** : Développez **Mises à jour logicielles** > **Packages de déploiement**, puis sélectionnez le package de déploiement à supprimer.  

    -   **Packages de pilotes** : Développez **Systèmes d’exploitation** > **Packages de pilotes**, puis sélectionnez le package de pilotes à supprimer.  

    -   **Images de système d’exploitation** : Développez **Systèmes d’exploitation** > **Images du système d’exploitation**, puis sélectionnez l’image du système d’exploitation à supprimer.  

    -   **Programmes de système d’exploitation** : Développez **Systèmes d’exploitation** > **Programmes d’installation de système d’exploitation**, puis sélectionnez le programme d’installation de système d’exploitation à supprimer.  

    -   **Images de démarrage** : Développez **Systèmes d’exploitation** > **Images de démarrage**, puis sélectionnez l’image de démarrage à supprimer.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Cliquez sur l'onglet **Emplacements du contenu** , sélectionnez le point de distribution ou le groupe de points de distribution à partir duquel vous souhaitez supprimer le contenu, cliquez sur **Supprimer**, puis cliquez sur **OK**.  

#### <a name="to-remove-package-content-from-distribution-point-properties"></a>Pour supprimer le contenu du package des propriétés du point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Points de distribution**, puis sélectionnez le point de distribution dans lequel vous souhaitez supprimer le contenu.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Cliquez sur l'onglet **Contenu** , sélectionnez le contenu à supprimer, cliquez sur **Supprimer**, puis cliquez sur **OK**.  

#### <a name="to-remove-content-from-distribution-point-group-properties"></a>Pour supprimer du contenu des propriétés du groupe de points de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Groupes de points de distribution**, puis sélectionnez le groupe de points de distribution dans lequel vous souhaitez supprimer du contenu.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Cliquez sur l'onglet **Contenu** , sélectionnez le contenu à supprimer, cliquez sur **Supprimer**, puis cliquez sur **OK**.  


### <a name="validate-content"></a>Valider le contenu
Le processus de validation du contenu vérifie l'intégrité des fichiers de contenu sur les points de distribution. Vous pouvez activer la validation du contenu selon une planification, ou vous pouvez démarrer manuellement la validation du contenu à partir des propriétés des points de distribution et des packages.  

 Lors du démarrage du processus de validation du contenu, Configuration Manager vérifie les fichiers de contenu sur les points de distribution et si le hachage du fichier est inattendu pour les fichiers du point de distribution, Configuration Manager crée un message d’état que vous pouvez consulter dans l’espace de travail **Surveillance**.  

 Pour plus d’informations sur la configuration de la planification de la validation du contenu, consultez [Configurations des points de distribution](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs) dans la rubrique [Installer et configurer des points de distribution pour System Center Configuration Manager](../../../../core/servers/deploy/configure/install-and-configure-distribution-points.md).  


#### <a name="to-initiate-content-validation-for-all-content-on-a-distribution-point"></a>Pour initier la validation du contenu de tout le contenu d'un point de distribution  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , cliquez sur **Points de distribution**, puis sélectionnez le point de distribution dont vous voulez valider le contenu.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Dans l'onglet **Accueil** , sélectionnez le package dans lequel vous souhaitez valider le contenu, cliquez sur **Valider**, sur **OK**, puis de nouveau sur **OK**. Le processus de validation du contenu démarre pour le package sur le point de distribution.  

5.  Pour afficher les résultats du processus de validation du contenu, dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur le nœud **État du contenu** . Le contenu de chaque type de package (par exemple, application, package de mises à jour logicielles et image de démarrage) s'affiche. Pour plus d’informations sur la surveillance de l’état du contenu, consultez [Surveiller le contenu que vous avez distribué avec System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  

#### <a name="to-initiate-content-validation-for-a-package"></a>Pour initier la validation du contenu d'un package  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , sélectionnez l'une de ces étapes pour le type de contenu que vous souhaitez valider :  

    -   **Applications** : Développez **Gestion d’applications** > **Applications**, puis sélectionnez l’application à valider.  

    -   **Packages** : Développez **Gestion d’applications** > **Packages**, puis sélectionnez le package à valider.  

    -   **Packages de déploiement** : Développez **Mises à jour logicielles** > **Packages de déploiement**, puis sélectionnez le package de déploiement à valider.  

    -   **Packages de pilotes** : Développez **Systèmes d’exploitation** > **Packages de pilotes**, puis sélectionnez le package de pilotes à valider.  

    -   **Images de système d’exploitation** : Développez **Systèmes d’exploitation** > **Images du système d’exploitation**, puis sélectionnez l’image du système d’exploitation à valider.  

    -   **Programmes de système d’exploitation** : Développez **Systèmes d’exploitation** >  **Programmes d’installation de système d’exploitation**, puis sélectionnez le programme d’installation de système d’exploitation à valider.  

    -   **Images de démarrage** : Développez **Systèmes d’exploitation** > **Images de démarrage**, puis sélectionnez l’image de démarrage à préparer.  

3.  Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  

4.  Dans l'onglet **Emplacements du contenu** , sélectionnez le point de distribution ou le groupe de points de distribution dans lequel vous souhaitez valider le contenu, cliquez sur **Valider**, sur **OK**, puis de nouveau sur **OK**. Le processus de validation du contenu démarre pour le contenu situé sur le point de distribution ou le groupe de points de distribution sélectionné.  

5.  Pour afficher les résultats du processus de validation du contenu, dans l'espace de travail **Surveillance** , développez **État de distribution**, puis cliquez sur le nœud **État du contenu** . Le contenu de chaque type de package (par exemple, application, package de mises à jour logicielles et image de démarrage) s'affiche. Pour plus d’informations sur la surveillance de l’état du contenu, consultez [Surveiller le contenu que vous avez distribué avec System Center Configuration Manager](../../../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  
