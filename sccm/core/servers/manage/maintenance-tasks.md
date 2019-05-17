---
title: Tâches de maintenance
titleSuffix: Configuration Manager
description: Comprenez quelles tâches de maintenance effectuer pour les sites et les hiérarchies Configuration Manager, et à quel moment les effectuer.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 26e17b190312dd1d3b1b73f5b1d6b91912938255
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501069"
---
# <a name="maintenance-tasks-for-system-center-configuration-manager"></a>Tâches de maintenance pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les sites et hiérarchies System Center Configuration Manager exigent une maintenance et une surveillance régulières pour fournir en permanence des services efficaces. Une maintenance régulière garantit que le matériel, les logiciels et la base de données Configuration Manager fonctionnent toujours correctement et efficacement. Lorsque les performances sont optimales, les risques de défaillance sont considérablement réduits.  

 Pour configurer des alertes et utiliser le système d’état pour surveiller l’intégrité de Configuration Manager, consultez [Utiliser des alertes et le système d’état pour System Center Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

-   [Tâches de maintenance](#bkmk_MTs)  

##  <a name="bkmk_MTs"></a> Tâches de maintenance  
 Une maintenance régulière est essentielle pour assurer le bon fonctionnement du site. Tenez un journal des tâches de maintenance pour y documenter les dates, les auteurs et tout commentaire de maintenance sur les tâches.  

### <a name="when-to-do-common-maintenance-tasks"></a>Quand effectuer les tâches de maintenance courantes ?  
 Pour maintenir votre site, envisagez une maintenance quotidienne ou hebdomadaire. Certaines tâches peuvent nécessiter une planification différente. Une maintenance courante peut inclure les tâches de maintenance prédéfinies, ainsi que d’autres tâches, telles que la gestion des comptes pour conserver la conformité aux stratégies de l’entreprise.  

 Utilisez les informations suivantes comme guide pour mieux planifier quand effectuer les différentes tâches de maintenance. Utilisez ces listes comme point de départ et ajoutez les tâches éventuellement requises.  

**Tâches quotidiennes**   
Tâches de maintenance que vous pouvez envisager d’effectuer quotidiennement :  

-   Vérifiez que les tâches de maintenance prédéfinies devant être exécutées quotidiennement s’exécutent correctement.  

-   Vérifiez l’état de la base de données Configuration Manager.  

-   Vérifiez l'état du serveur de site.  

-   Vérifiez les boîtes de réception de système de site Configuration Manager pour chercher des backlogs de fichiers.  

-   Vérifiez l'état des systèmes de site.  

-   Vérifiez les journaux d'événements du système d'exploitation sur les systèmes de site.  

-   Vérifiez le journal des erreurs de SQL Server sur l'ordinateur de la base de données de site.  

-   Vérifiez les performances du système.  

-   Vérifiez les alertes Configuration Manager.  

**Tâches hebdomadaires**   
Tâches de maintenance que vous pouvez envisager d’effectuer chaque semaine :  

-   Vérifiez que les tâches de maintenance prédéfinies devant être exécutées chaque semaine s’exécutent correctement.  

-   Supprimez les fichiers inutiles des systèmes de sites.  

-   Si nécessaire, rédigez et distribuez des rapports destinés aux utilisateurs finaux.  

-   Sauvegardez les journaux des applications, de sécurité et des événements système, et effacez-les.  

-   Vérifiez la taille de la base de données du site et assurez-vous que l’espace disque disponible sur le serveur de bases de données du site est suffisant pour permettre à la base de données de grandir.  

-   Effectuez la maintenance de la base de données du site, conformément à votre plan de maintenance de base de données SQL Server.  

-   Vérifiez que tous les systèmes de site disposent d'espace disque disponible.  

-   Exécutez les outils de défragmentation sur tous les systèmes de site.  

**Tâches périodiques**   
Certaines tâches qui ne nécessitent pas de maintenance quotidienne ni hebdomadaire sont importantes pour garantir l’intégrité globale du site. Ces tâches garantissent également que les plans de récupération d’urgence et de sécurité sont à jour. Tâches de maintenance que vous pouvez envisager d’effectuer plus régulièrement que les tâches quotidiennes ou hebdomadaires :  

-   Modifier les comptes et les mots de passe, si nécessaire, en fonction de votre plan de sécurité.  

-   Passez en revue le plan de maintenance pour vérifier si les tâches de maintenance prévues sont planifiées correctement et efficacement en fonction des paramètres de site configurés.  

-   Passez en revue la conception de la hiérarchie Configuration Manager pour repérer toute modification requise.  

-   Vérifiez les performances du réseau pour vous assurer qu’aucune modification effectuée n’affecte le fonctionnement du site.  

-   Vérifiez que les paramètres Active Directory affectant le fonctionnement du site n’ont pas été modifiés. Par exemple, vérifiez que les sous-réseaux qui sont attribués aux sites Active Directory et utilisés comme limites du site Configuration Manager n’ont pas changé.  

-   Examiner dans votre plan de reprise après incident toute modification nécessaire.  

-   Récupérez un site selon le plan de récupération d’urgence dans un laboratoire de test en utilisant une copie de sauvegarde de la dernière sauvegarde créée par la tâche de maintenance Serveur de site de sauvegarde.

-   Examiner les erreurs liées au matériel ou vérifier si des mises à jour matérielles sont disponibles.  

-   Vérifier l'état d'intégrité global du site.  

###  <a name="BKMK_UseMTs"></a> Garantir l’intégrité opérationnelle de votre base de données de site  
 Quand votre site et hiérarchie Configuration Manager effectuent les tâches que vous planifiez et configurez, les composants de site ajoutent continuellement des données à la base de données Configuration Manager. Les performances de la base de données et l'espace de stockage disponible dans la base de données diminuent au fur et à mesure que la quantité de données augmente. Vous pouvez configurer des tâches de maintenance de site pour supprimer les données anciennes dont vous n’avez plus besoin.  

 Configuration Manager propose des tâches de maintenance prédéfinies que vous pouvez utiliser pour garantir l’intégrité de la base de données Configuration Manager. Toutes les tâches de maintenance ne sont pas disponibles sur chaque site, par défaut. Certaines tâches sont activées alors que d’autres ne le sont pas, et toutes prennent en charge une planification que vous pouvez configurer.  

 La plupart des tâches de maintenance prédéfinies suppriment régulièrement les données périmées de la base de données Configuration Manager. La réduction de la taille de la base de données obtenue en supprimant les données inutiles permet d'améliorer les performances et l'intégrité de la base de données, ce qui améliore l'efficacité du site et de la hiérarchie. D’autres tâches, telles que **Reconstruire les index**, aident à maintenir l’efficacité de la base de données. D’autres tâches, telles que la tâche **Serveur de site de sauvegarde**, vous aident à préparer la récupération d’urgence.  

> [!IMPORTANT]  
>  Lorsque vous planifiez l'exécution d'une tâche qui supprime des données, examinez l'utilisation de ces données dans la hiérarchie. Quand une tâche qui supprime des données s’exécute sur un site, les informations sont supprimées de la base de données Configuration Manager, et cette modification est répliquée sur tous les sites dans la hiérarchie. Cette suppression peut affecter d’autres tâches reposant sur ces données. Par exemple, sur le site d’administration centrale, vous pouvez configurer une exécution mensuelle de la découverte afin d’identifier les ordinateurs non clients. Vous planifiez d’installer le client Configuration Manager sur ces ordinateurs dans un délai de deux semaines à compter de leur découverte. Toutefois, sur un site de la hiérarchie, un administrateur configure une exécution hebdomadaire de la tâche Supprimer les données de découverte anciennes. Il en résulte qu’une semaine après la découverte des ordinateurs non clients, ils sont supprimés de la base de données Configuration Manager. De retour sur le site d’administration centrale, vous préparez l’installation push du client Configuration Manager sur ces nouveaux ordinateurs au bout du dixième jour. Toutefois, étant donné que la tâche Supprimer les données de découverte anciennes a récemment été exécutée pour supprimer les données de sept jours ou plus, les ordinateurs récemment découverts ne sont plus disponibles dans la base de données.  

Après l’installation d’un site Configuration Manager, passez en revue les tâches de maintenance disponibles et activez celles nécessaire pour vos opérations. Passez en revue la planification par défaut de chaque tâche et, si nécessaire, modifiez la planification pour ajuster la tâche de maintenance en fonction de votre hiérarchie et de votre environnement. Bien que la planification par défaut de chaque tâche s’adapte à la plupart des environnements, surveillez les performances de vos sites et de votre base de données, et envisagez de reconfigurer ces tâches afin d’optimiser l’efficacité de votre déploiement. Planifiez d’examiner régulièrement les performances du site et de la base de données, ainsi que de reconfigurer les tâches de maintenance et leurs planifications afin de maintenir l’efficacité.  

#### <a name="set-up-maintenance-tasks"></a>Configurer les tâches de maintenance  
 Chaque site Configuration Manager prend en charge des tâches de maintenance qui contribuent à garantir le fonctionnement optimal de la base de données du site. Par défaut, plusieurs tâches de maintenance sont activées pour chaque site, et toutes les tâches prennent en charge des planifications indépendantes. Les tâches de maintenance sont configurées individuellement pour chaque site et s’appliquent à la base de données sur le site. Toutefois, certaines tâches, telles que **Supprimer les données de découverte anciennes**, affectent les informations disponibles dans tous les sites d’une hiérarchie.  

 La console Configuration Manager affiche uniquement les tâches de maintenance que vous pouvez configurer sur un site. Pour obtenir la liste complète des tâches de maintenance par type de site, consultez [Référence des tâches de maintenance pour System Center Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Utilisez la procédure suivante pour mieux configurer les paramètres courants des tâches de maintenance.  

###### <a name="to-set-up-maintenance-tasks-for-configuration-manager"></a>Pour configurer les tâches de maintenance pour Configuration Manager  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration de site** >**Sites**.  

2.  Choisissez le site avec la tâche de maintenance que vous souhaitez configurer.  

3.  Sous l’onglet **Accueil**, dans le groupe **Paramètres**, choisissez **Maintenance de site**, puis choisissez la tâche de maintenance que vous souhaitez configurer.  

    > [!TIP]  
    >  Seules les tâches disponibles sur le site sélectionné sont affichées.  

4.  Pour configurer la tâche, choisissez **Modifier**, veillez à ce que la case **Activer cette tâche** soit cochée, et planifiez l’exécution de la tâche. Si la tâche supprime également les données anciennes, configurez l’ancienneté des données à supprimer de la base de données lors de l’exécution de la tâche. Choisissez **OK** pour fermer les **Propriétés** de la tâche.  

    > [!NOTE]  
    >  Pour **Supprimer les messages d’état anciens**, vous devez configurer l’ancienneté des données à supprimer lorsque vous configurez des règles de filtre d’état.  

5.  Pour activer ou désactiver la tâche sans modifier les propriétés de la tâche, choisissez le bouton **Activer** ou **Désactiver**. L'étiquette du bouton change en fonction de la configuration actuelle de la tâche.  

6.  Une fois que vous avez terminé de configurer les tâches de maintenance, choisissez **OK** pour terminer la procédure.
