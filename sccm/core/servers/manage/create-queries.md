---
title: Créer des requêtes
titleSuffix: Configuration Manager
description: Découvrez comment créer et importer des requêtes dans System Center Configuration Manager. Inclut des conseils et des exemples de requêtes.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2356547d01df346b8b5db090ea8690377c8d0dc8
ms.sourcegitcommit: f42b9e802331273291ed498ec88f710110fea85a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67551031"
---
# <a name="create-queries-in-system-center-configuration-manager"></a>Créer des requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article décrit comment créer et importer des requêtes dans System Center Configuration Manager.  

##  <a name="BKMK_Create"></a>Créer une requête  
 Procédez comme suit pour créer une requête dans Configuration Manager.  

1.  Dans la console Configuration Manager, sélectionnez **Surveillance**.  

2.  Dans l'espace de travail **Surveillance**, sélectionnez **Requêtes**. Dans l'onglet **Accueil**, dans le groupe **Créer**, sélectionnez **Créer une requête**.  

3.  Dans l’onglet **Général** de l’**Assistant Création de requête**, spécifiez un nom unique et, éventuellement, un commentaire pour la requête.  

4.  Si vous souhaitez importer une requête existante à utiliser comme base de la nouvelle requête, sélectionnez **importer l’instruction de requête**. Dans la boîte de dialogue **Parcourir la requête**, sélectionnez une requête que vous souhaitez importer, puis sélectionnez **OK**.  

5.  Dans la liste **Type d’objet** , sélectionnez le type d’objet que vous voulez que la requête renvoie. Ce tableau décrit certains exemples de types d’objets que vous pouvez rechercher :  

    |Type d’objet|Description|  
    |-----------------|-----------------|  
    |**Ressource système**|Utilisez cette option pour rechercher des attributs système standard, tels que le nom NetBIOS d’un périphérique, la version du client, l’adresse IP du client et les informations sur Active Directory Domain Services.|  
    |**Ressource utilisateur**|Utilisez cette option pour rechercher des informations utilisateur standard, telles que des noms d’utilisateur, des noms de groupes d’utilisateurs et des noms de groupes de sécurité.|  
    |**Déploiement**|Utilisez cette option pour rechercher des attributs standard d’un déploiement, tels que le nom, la planification et le regroupement du déploiement vers lequel il a été déployé.|  

6.  Sélectionnez **Modifier l’instruction de la requête** pour ouvrir la boîte de dialogue &lt;Propriétés de l’instruction de\> **Nom de la requête**.  

7.  Sous l’onglet **Général** de la boîte de dialogue &lt;Propriétés de l’instruction de \> **Nom de la requête**, spécifiez les attributs que cette requête renvoie et comment ils doivent être affichés. Sélectionnez l’icône **Nouveau** pour ajouter un nouvel attribut. Vous pouvez également sélectionner **Afficher le langage de requête** pour entrer ou modifier la requête directement en langage de requêtes WMI (WQL). Pour obtenir des exemples de requêtes WMI, consultez la section [Exemple de requêtes WQL](#BKMK_Example) dans cet article.  

    > [!TIP]  
    > Vous pouvez utiliser la documentation de référence suivante pour vous aider à construire vos propres requêtes WQL :  
    >   
    > -   [WQL (SQL pour WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Clause WHERE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Opérateurs WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Sous l’onglet **Critères** de la boîte de dialogue &lt;Propriétés d’instruction de\> **Nom de requête**, spécifiez les critères utilisés pour affiner les résultats de la requête. Par exemple, vous pouvez renvoyer uniquement les ressources dont le code de site est **XYZ**. Vous pouvez configurer plusieurs critères pour une requête.  

    > [!IMPORTANT]  
    > Si vous créez une requête qui ne contient aucun critère, elle retourne tous les appareils du regroupement **Tous les systèmes** .  

9. Sous l’onglet **Jointures** de la boîte de dialogue &lt;Propriétés de l’instruction de\> **Nom de requête**, vous pouvez combiner des données de deux attributs différents dans les résultats de votre requête. Bien que Configuration Manager crée automatiquement des jointures de requête lorsque vous choisissez différents attributs pour les résultats de votre requête, l'onglet **Jointures** fournit d'autres options avancées. Configuration Manager prend en charge ces classes d’attribut :  

    |Type de jointure|Description|  
    |---------------|-----------------|  
    |Interne|Affiche seulement les résultats en correspondance. Ce type est toujours utilisé par les jointures créées automatiquement.|  
    |Gauche|Affiche tous les résultats pour l'attribut de base et uniquement les résultats ayant une correspondance pour l'attribut de jointure.|  
    |Droit|Affiche tous les résultats pour l'attribut de jointure et uniquement les résultats ayant une correspondance pour l'attribut de base.|  
    |Complète|Affiche tous les résultats à la fois pour l'attribut de base et pour l'attribut de jointure.|  

     Pour plus d’informations sur la manière d’utiliser des opérations de jointure, consultez la documentation SQL Server.  

10. Sélectionnez **OK** pour fermer la boîte de dialogue &lt;Propriétés de l’instruction de\> **Nom de la requête**.  

11. Sous l’onglet **Général** de l’**Assistant Création de requête**, spécifiez si les résultats de cette requête ne sont pas limités aux membres d’un regroupement, s’ils sont limités aux membres d’un regroupement spécifique ou si une invite pour choisir un regroupement s’affiche à chaque exécution de la requête.  

12. Terminez l'assistant pour créer la requête. La nouvelle requête s’affiche dans le nœud **Requêtes** de l’espace de travail **Surveillance**.  

##  <a name="BKMK_Import"></a> Importer une requête  
 Procédez comme suit pour importer une requête dans Configuration Manager. Pour plus d'informations sur l’exportation des requêtes, voir [Guide pratique pour gérer des requêtes dans System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

1.  Dans la console Configuration Manager, sélectionnez **Surveillance**.  

2.  Dans l'espace de travail **Surveillance**, sélectionnez **Requêtes**. Sous l’onglet **Accueil**, dans le groupe **Créer**, sélectionnez **Importer des objets**.  

3.  Dans la page **Nom du fichier au format MOF** de l’**Assistant Importation d’objets**, sélectionnez **Parcourir** pour sélectionner le fichier au format MOF contenant la requête à importer.  

4.  Consultez les informations relatives à la requête à importer, puis terminez l’Assistant. La nouvelle requête s’affiche dans le nœud **Requêtes** de l’espace de travail **Surveillance**.  

##  <a name="BKMK_Example"></a> Example WQL queries

Cette section contient des exemples de requêtes WQL que vous pouvez utiliser dans votre hiérarchie ou modifier à d’autres fins. Pour utiliser ces requêtes, sélectionnez **Afficher la requête** dans la boîte de dialogue **Propriétés de l'instruction de la requête**. Puis copiez et collez la requête dans le champ **Instruction de la requête**.  

> [!TIP]  
> Utilisez le caractère générique `%` pour signifier n’importe quelle chaîne de caractères. Par exemple, `%Visio%` renvoie Microsoft Office Visio 2010.  

### <a name="computers-that-run-windows-7"></a>Ordinateurs qui exécutent Windows 7

Utilisez la requête suivante pour renvoyer le nom NetBIOS et la version du système d’exploitation de tous les ordinateurs qui exécutent Windows 7.  

> [!TIP]  
> Pour retourner les ordinateurs qui exécutent Windows Server 2008 R2, remplacez `%Workstation 6.1%` par `%Server 6.1%`.  

```  
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from    
SMS_R_System where   
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 6.1%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Ordinateurs avec un package logiciel spécifique installé  

Utilisez la requête suivante pour retourner le nom NetBIOS et le nom du package logiciel de tous les ordinateurs dotés d’un package logiciel spécifique installé. Cet exemple retourne tous les ordinateurs sur lesquels une version de Microsoft Visio est installée. Remplacez `Microsoft%Visio%` par le package logiciel à rechercher.  

> [!TIP]  
> Cette requête recherche le package logiciel en utilisant les noms figurant dans la liste des programmes inclus dans le Panneau de configuration Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Ordinateurs situés dans une unité d’organisation (UO) Active Directory Domain Services spécifique

Utilisez la requête suivante pour retourner le nom NetBIOS et le nom d’unité d’organisation (UO) de tous les ordinateurs inclus dans une unité d’organisation spécifiée. Remplacez le texte `OU Name` par le nom de l’UO à rechercher.  

```  
select SMS_R_System.NetbiosName,   
SMS_R_System.SystemOUName from    
SMS_R_System where   
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Ordinateurs portant un nom NetBIOS spécifique

Utilisez la requête suivante pour retourner le nom NetBIOS de tous les ordinateurs dont le nom commence par une chaîne de caractères spécifique. Dans cet exemple, la requête retourne tous les ordinateurs dont le nom NetBIOS commence par `ABC`.  

```  
select SMS_R_System.NetbiosName from    
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="BKMK_DeviceType"></a> Appareils d’un type spécifique

Les types d’appareils sont stockés dans la base de données Configuration Manager sous la classe de ressource **sms_r_system** et le nom d’attribut **AgentEdition**. Utilisez cette requête pour récupérer uniquement les appareils correspondant à l’édition agent du type d’appareil que vous spécifiez :  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Utilisez une de ces valeurs pour &lt;ID d’appareil\> :  

|Type d'appareil|Valeur de AgentEdition|  
|-----------------|---------------------------|  
|Ordinateur portable ou de bureau Windows|0|  
|Appareil ARM Windows (exécutant Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Ordinateur Mac|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|iOS|8|  
|iPad|9|  
|iPod Touch|10|  
|Android|11|  
|Système Intel sur une puce|12|  
|Serveurs Unix et Linux|13|  
|Apple macOS (MDM)|14|
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|
|Android for Work|17|

 Par exemple, si vous voulez retourner uniquement des ordinateurs Mac, utilisez cette requête :  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Étapes suivantes

[Guide pratique pour gérer les requêtes](/sccm/core/servers/manage/manage-queries)
