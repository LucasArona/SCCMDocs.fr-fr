---
title: Opérations de migration
titleSuffix: Configuration Manager
description: Créez et exécutez des tâches pour migrer les données et les clients vers System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c28e3492-851a-40fc-ba13-67ebc2d8b41a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a038377e4b29852157fd0d92836f26f1b5e18433
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="operations-for-migrating-to-system-center-configuration-manager"></a>Opérations de migration vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour la migration dans System Center Configuration Manager, vous pouvez migrer des données et des clients une fois que vous avez collecté des données à partir d’un site source dans une hiérarchie source prise en charge. Utilisez les informations des sections suivantes pour créer et exécuter des tâches de migration pour migrer des données et des clients, puis terminer le processus de migration.  

-   [Créer et modifier des tâches de migration](#Create_Edit_migration_Jobs)  

-   [Exécuter des tâches de migration](#Run_Migration_Jobs)  

-   [Mettre à niveau ou réattribuer un point de distribution partagé](#BKMK_ProcUpgrdSS)  

-   [Surveiller l’activité de migration dans l’espace de travail Migration](#Monitor_MIgration)  

-   [Migrer des clients](#BKMK_MigrateClients)  

-   [Terminer la migration](#Complete_Migration)  

##  <a name="Create_Edit_migration_Jobs"></a> Créer et modifier des tâches de migration  
 Procédez comme suit pour créer des tâches de migration de données, modifier la liste d’exclusions pour les tâches de migration basée sur des regroupements, configurer des points de distribution partagés et modifier des planifications de tâches de migration.  

> [!NOTE]  
>  La procédure ci-dessous permet de créer une tâche de migration basée sur des regroupements. Elle s’applique uniquement aux hiérarchies sources qui exécutent une version prise en charge de Configuration Manager 2007. Le type de tâche de migration basée sur les regroupements n’est pas disponible lorsque vous migrez à partir d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager.  

#### <a name="create-a-migration-job-to-migrate-by-collections"></a>Créer une tâche de migration par regroupements  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Tâches de migration**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une tâche de migration**.  

4.  Dans la page **Général** de l’Assistant Création de tâche de migration, configurez les éléments suivants, puis choisissez **OK** :  

    -   Spécifiez un nom pour la tâche de migration.  

    -   Dans la liste déroulante **Type de tâche** , sélectionnez **Migration du regroupement**.  

5.  Dans la page **Sélectionner des regroupements**, configurez les éléments suivants, puis choisissez **Suivant** :  

    -   Sélectionnez les regroupements que vous souhaitez migrer.  

    -   Si vous souhaitez migrer uniquement les regroupements, sans les objets qui leur sont associés, décochez **Migrer les objets qui sont associés aux regroupements spécifiés**. Si vous décochez cette option, aucun objet associé n’est migré au cours de cette tâche. Vous pouvez alors ignorer les étapes 6 et 7.  

6.  Dans la page **Sélectionner des objets**, décochez tous les types d’objet ou les objets disponibles spécifiques que vous ne souhaitez pas migrer. Par défaut, tous les types d'objet associés et les objets disponibles sont sélectionnés. Choisissez **Suivant**.  

7.  Dans la page **Propriété du contenu**, attribuez la propriété du contenu de chaque site source de la liste à un site de la hiérarchie de destination, puis choisissez **Suivant**.  

8.  Dans la page **Étendue de sécurité**, sélectionnez la ou les étendues de sécurité d’administration basée sur un rôle que vous voulez affecter aux objets à migrer dans cette tâche de migration, puis choisissez **Suivant**.  

9. Dans la page **Limitation au regroupement**, configurez un regroupement de la hiérarchie de destination pour limiter l’étendue de chaque regroupement de la liste, puis choisissez **Suivant**. Si aucun regroupement n’est répertorié, choisissez **Suivant**.  

10. Dans la page **Remplacement d’un code de site**, affectez un code de site de la hiérarchie de destination pour remplacer le code de site Configuration Manager 2007 de chaque regroupement répertorié, puis choisissez **Suivant**. Si aucun regroupement n’est répertorié, choisissez **Suivant**.  

11. Dans la page **Consulter les informations**, choisissez **Enregistrer dans un fichier** pour enregistrer les informations affichées en vue de les consulter ultérieurement. Quand vous êtes prêt à continuer, choisissez **Suivant**.  

12. Dans la page **Paramètres**, définissez la période d’exécution de la tâche de migration et tous les autres paramètres nécessaires à cette tâche, puis choisissez **Suivant**.  

13. Confirmez les paramètres et mettez fin à l’Assistant.  

#### <a name="create-a-migration-job-to-migrate-by-objects"></a>Créer une tâche de migration par objets  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Tâches de migration**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une tâche de migration**.  

4.  Dans la page **Général** de l’Assistant Création de tâche de migration, configurez les éléments suivants, puis choisissez **Suivant** :  

    -   Spécifiez un nom pour la tâche de migration.  

    -   Dans la liste déroulante **Type de tâche** , sélectionnez **Migration d'objet**.  

5.  Sur la page **Sélectionner des objets** , sélectionnez les types d'objet que vous souhaitez migrer. Par défaut, tous les objets disponibles sont sélectionnés pour chaque type d'objet que vous sélectionnez.  

6.  Dans la page **Propriété du contenu**, attribuez la propriété du contenu de chaque site source de la liste à un site de la hiérarchie de destination, puis choisissez **Suivant**. Si aucun site source n’est répertorié, choisissez **Suivant**.  

7.  Dans la page **Étendue de sécurité**, sélectionnez la ou les étendues de sécurité d’administration basée sur un rôle que vous voulez affecter aux objets de cette tâche de migration, puis choisissez **Suivant**.  

8.  Dans la page **Consulter les informations**, choisissez **Enregistrer dans un fichier** pour enregistrer les informations affichées en vue de les consulter ultérieurement. Quand vous êtes prêt à continuer, choisissez **Suivant**.  

9. Dans la page **Paramètres**, définissez la période d’exécution de la tâche de migration et tous les autres paramètres nécessaires à cette tâche. Ensuite, choisissez **Suivant**.  

10. Confirmez les paramètres et mettez fin à l’Assistant.  

#### <a name="create-a-migration-job-to-migrate-changed-objects"></a>Créer une tâche de migration pour migrer des objets modifiés  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Tâches de migration**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une tâche de migration**.  

4.  Dans la page **Général** de l’Assistant Création de tâche de migration, configurez les éléments suivants, puis choisissez **Suivant** :  

    -   Spécifiez un nom pour la tâche de migration.  

    -   Dans la liste déroulante **Type de tâche**, sélectionnez **Objets modifiés après la migration**.  

5.  Sur la page **Sélectionner des objets** , sélectionnez les types d'objet que vous souhaitez migrer. Par défaut, tous les objets disponibles sont sélectionnés pour chaque type d'objet que vous sélectionnez.  

6.  Dans la page **Propriété du contenu**, attribuez la propriété du contenu de chaque site source de la liste à un site de la hiérarchie de destination, puis choisissez **Suivant**. Si aucun site source n’est répertorié, choisissez **Suivant**.  

7.  Dans la page **Étendue de sécurité**, sélectionnez la ou les étendues de sécurité d’administration basée sur un rôle que vous voulez affecter aux objets de cette tâche de migration, puis choisissez **Suivant**.  

8.  Dans la page **Consulter les informations**, choisissez **Enregistrer dans un fichier** pour enregistrer les informations affichées en vue de les consulter ultérieurement. Quand vous êtes prêt à continuer, choisissez **Suivant**.  

9. Dans la page **Paramètres**, définissez la période d’exécution de la tâche de migration et tous les autres paramètres nécessaires à cette tâche. À la différence des autres types de tâches de migration, cette tâche de migration doit remplacer les objets migrés précédemment dans la base de données System Center Configuration Manager. Choisissez **Suivant**.  

10. Confirmez les paramètres, puis terminez l’Assistant.  

###  <a name="BKMK_Modify_Exclusion_List"></a> Modifier la liste d’exclusions pour la migration  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, choisissez **Migration** pour accéder à la liste d’exclusions. Vous pouvez également accéder à la liste des exclusions à partir du nœud **Hiérarchie source** ou **Tâches de migration** .  

3.  Sous l’onglet **Accueil**, dans le groupe **Migration**, choisissez **Modifier la liste d’exclusion**.  

4.  Dans la boîte de dialogue **Modifier la liste d’exclusion**, sélectionnez l’objet exclu que vous souhaitez retirer de la liste d’exclusions, puis choisissez **Supprimer**.  

5.  Choisissez **OK** pour enregistrer les modifications et terminer l’opération. Pour annuler les modifications en cours et restaurer tous les objets que vous avez supprimés, choisissez **Annuler**, puis choisissez **Non**. La suppression des objets est annulée et la boîte de dialogue **Modifier la liste d'exclusion** se ferme.  

#### <a name="share-distribution-points-from-the-source-hierarchy"></a>Partager des points de distribution à partir de la hiérarchie source  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, choisissez **Hiérarchie source**, puis sélectionnez le site source que vous souhaitez configurer.  

3.  Sous l’onglet **Accueil**, dans le groupe **Site source**, choisissez **Configurer**.  

4.  Dans la boîte de dialogue **Informations d’identification du site source**, sélectionnez **Activer le partage du point de distribution pour ce serveur de site source**, puis choisissez **OK**.  

5.  Une fois la collecte des données terminée, choisissez **Fermer**.  

#### <a name="change-the-schedule-of-a-migration-job"></a>Modifier la planification d’une tâche de migration  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Tâches de migration**.  

3.  Choisissez la tâche de migration que vous souhaitez modifier. Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

4.  Dans les propriétés de la tâche de migration, sélectionnez l’onglet **Paramètres**, modifiez l’heure d’exécution de la tâche de migration, puis choisissez **OK**.  

##  <a name="Run_Migration_Jobs"></a> Exécuter des tâches de migration  
 Pour exécuter une tâche de migration n'a pas encore commencé, suivez la procédure ci-dessous.  


1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Tâches de migration**.  

3.  Choisissez la tâche de migration que vous souhaitez exécuter. Sous l’onglet **Accueil**, dans le groupe **Tâche de migration**, choisissez **Démarrer**.  

4.  Choisissez **Oui** pour démarrer la tâche de migration.  

##  <a name="BKMK_ProcUpgrdSS"></a> Mettre à niveau ou réattribuer un point de distribution partagé  
 Vous pouvez mettre à niveau un point de distribution pris en charge qui est partagé à partir d’un site source Configuration Manager 2007 (ou réaffecter un point de distribution pris en charge qui est partagé à partir d’un site source System Center Configuration Manager) pour qu’il devienne un point de distribution dans la hiérarchie de destination.  

> [!IMPORTANT]  
>  Avant de mettre à niveau un point de distribution de branche Configuration Manager 2007, vous devez désinstaller le logiciel client Configuration Manager 2007 de l’ordinateur du point de distribution de branche. Si le logiciel client Configuration Manager 2007 est installé lorsque vous essayez de mettre à niveau le point de distribution, la mise à niveau échoue et le contenu précédemment déployé sur le point de distribution de branche est supprimé de l’ordinateur.  

> [!CAUTION]  
>  Quand vous mettez à niveau ou réaffectez un point de distribution partagé, le rôle de système de site et l’ordinateur du système de site du point de distribution sont supprimés du site source et ajoutés comme point de distribution au site sélectionné dans la hiérarchie de destination.  

#### <a name="upgrade-or-reassign-a-shared-distribution-point"></a>Mettre à niveau ou réattribuer un point de distribution partagé  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Hiérarchie source**.  

3.  Sélectionnez le site propriétaire du point de distribution à mettre à niveau, choisissez l’onglet **Points de distribution partagés**, puis sélectionnez le point de distribution éligible que vous souhaitez mettre à niveau ou réaffecter.  

4.  Sous l’onglet **Point de distribution**, dans le groupe **Point de distribution**, choisissez **Réaffecter**.  

5.  Dans l’Assistant Réaffectation du point de distribution partagé, spécifiez les paramètres comme si vous installiez un nouveau point de distribution pour la hiérarchie de destination, en ajoutant les configurations suivantes :  

    -   Dans la page **Conversion du contenu**, prenez connaissance des conseils relatifs à l’espace nécessaire pour convertir le contenu existant. Puis, dans la page **Paramètres du lecteur** de l’Assistant, vérifiez que le lecteur de l’ordinateur du point de distribution sélectionné a la quantité nécessaire d’espace disque disponible.  

6.  Confirmez les paramètres, puis terminez l’Assistant.  

##  <a name="Monitor_MIgration"></a> Surveiller l’activité de migration dans l’espace de travail Migration  
 Utilisez la console Configuration Manager pour surveiller la migration.  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Tâches de migration**.  

3.  Choisissez la tâche de migration que vous souhaitez surveiller.  

4.  Affichez les détails et l'état de la tâche de migration sélectionnée sur les onglets **Synthèse** et **Objets de la tâche**.  

##  <a name="BKMK_MigrateClients"></a> Migrer des clients  
 Effectuez la migration des clients vers la hiérarchie de destination après avoir migré les données des clients entre les hiérarchies, mais avant de terminer le processus de migration. La migration de clients entre les hiérarchies implique la désinstallation du logiciel client Configuration Manager des ordinateurs qui sont affectés à la hiérarchie source, puis l’installation du logiciel client Configuration Manager à partir de la hiérarchie de destination. Lorsque vous installez le client à partir de la hiérarchie de destination, vous affectez également le client à un site principal de cette hiérarchie. Pour en savoir plus sur la migration de clients, consultez [Planification d’une stratégie de migration de clients dans System Center Configuration Manager](../../core/migration/planning-a-client-migration-strategy.md).  

##  <a name="Complete_Migration"></a> Terminer la migration  
 Procédez comme suit pour terminer la migration à partir de la hiérarchie source.  

1.  Dans la console Configuration Manager, choisissez **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Migration**, puis choisissez **Hiérarchie source**.  

3.  Dans le cas d’une hiérarchie source Configuration Manager 2007, sélectionnez un site source qui se trouve au niveau inférieur de la hiérarchie source. Dans le cas d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, sélectionnez le site source disponible.  

4.  Sous l’onglet **Accueil**, dans le groupe **Nettoyer**, choisissez **Arrêter la collecte de données**.  

5.  Choisissez **Oui** pour confirmer l’action.  

6.  Pour une hiérarchie source Configuration Manager 2007, avant de passer à l’étape suivante, répétez les étapes 3, 4 et 5. Effectuez ces étapes au niveau de chaque site de la hiérarchie, du bas vers le haut. Dans le cas d’une hiérarchie source System Center 2012 Configuration Manager ou System Center Configuration Manager, passez à l’étape suivante.  

7.  Sous l’onglet **Accueil**, dans le groupe **Nettoyer**, choisissez **Nettoyer les données de migration**.  

8.  Dans la boîte de dialogue **Nettoyer les données de migration**, dans la liste déroulante **Hiérarchie source**, sélectionnez le code de site et le serveur de site du site de niveau supérieur de la hiérarchie source, puis choisissez **OK**.  

9. Choisissez **Oui** pour terminer le processus de migration pour la hiérarchie source.  
