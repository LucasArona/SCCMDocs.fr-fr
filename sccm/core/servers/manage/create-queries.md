---
title: Créer des requêtes
titleSuffix: Configuration Manager
description: Découvrez comment créer et importer des requêtes dans System Center Configuration Manager. Inclut des conseils et des exemples de requêtes.
ms.date: 12/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6ba7adf52ce084d640bf53aef32678576d5828f5
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32340201"
---
# <a name="how-to-create-queries-in-system-center-configuration-manager"></a>Comment créer des requêtes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous pouvez utiliser cette rubrique pour créer ou importer des requêtes dans System Center Configuration Manager.  

##  <a name="BKMK_Create"></a> Comment créer des requêtes  
 Procédez comme suit pour créer des requêtes dans Configuration Manager.  

#### <a name="to-create-a-query"></a>Pour créer une requête  

1.  Dans la console Configuration Manager, choisissez **Surveillance**.  

2.  Dans l'espace de travail **Surveillance**, choisissez **Requêtes**. Puis, sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une requête**.  

3.  Sous l’onglet **Général** de l’ **Assistant Création de requête**, spécifiez un nom unique et un commentaire facultatif pour la requête.  

4.  Si vous souhaitez importer une requête existante à utiliser comme base de la nouvelle requête, choisissez **importer la déclaration de requête**. Dans le **parcourir la requête** boîte de dialogue, sélectionnez une requête existante que vous souhaitez importer, puis choisissez **OK**.  

5.  Dans la liste **Type d’objet** , sélectionnez le type d’objet que vous voulez que la requête renvoie. Le tableau suivant décrit certains exemples du type d’objet que vous pouvez rechercher :  

    |Type d’objet|Description|  
    |-----------------|-----------------|  
    |**Ressource système**|Utilisé pour rechercher des attributs système standard tels que le nom NetBIOS d’un périphérique, la version du client, l’adresse IP du client et les informations des services de domaine Active Directory.|  
    |**Ressource utilisateur**|Utilisé pour rechercher des informations utilisateur standard, telles que des noms d’utilisateur, des noms de groupes d’utilisateurs et des noms de groupes de sécurité.|  
    |**Déploiement**|Utilisé pour rechercher les attributs standard d’un déploiement, tels que le nom du déploiement, la planification et le regroupement vers lequel il a été déployé.|  

6.  Choisissez **Modifier l’instruction de la requête** pour ouvrir la boîte de dialogue *Propriétés de l’instruction de* **&lt;Nom de la requête\>**.  

7.  Sous l’onglet **Général** de la boîte de dialogue **Propriétés de l’instruction de** *&lt;Nom de la requête\>*, spécifiez les attributs que cette requête renvoie et comment ils doivent être affichés. Choisissez l’icône **Nouveau** pour ajouter un nouvel attribut. Vous pouvez également choisir **Afficher la requête** pour entrer ou modifier la requête directement en langage de requêtes WMI (WQL). Pour obtenir des exemples de requêtes WMI, consultez la section [Exemples de requêtes WQL](#BKMK_Example) dans cette rubrique.  

    > [!TIP]  
    > Vous pouvez utiliser la documentation de référence MSDN suivante pour vous aider à créer vos propres requêtes WQL :  
    >   
    > -   [WQL (SQL pour WMI)](http://go.microsoft.com/fwlink/p/?LinkId=256653)  
    > -   [Clause WHERE](http://go.microsoft.com/fwlink/p/?LinkId=256654)  
    > -   [Opérateurs WQL](http://go.microsoft.com/fwlink/p/?LinkId=256655)  

8.  Sous l’onglet **Critères** de la boîte de dialogue **Propriétés de l’instruction de** *&lt;Nom de la requête\>*, spécifiez les critères utilisés pour affiner les résultats de la requête. Par exemple, vous pouvez renvoyer uniquement les ressources dont le code de site est **XYZ** dans les résultats de la requête. Vous pouvez configurer plusieurs critères pour une requête.  

    > [!IMPORTANT]  
    > Si vous créez une requête qui ne contient aucun critère, elle retourne tous les appareils du regroupement **Tous les systèmes** .  

9. Sous l’onglet **Jointures** de la boîte de dialogue **Propriétés de l’instruction de** *&lt;Nom de la requête\>*, vous pouvez combiner des données de deux attributs différents dans les résultats de votre requête. Bien que Configuration Manager crée automatiquement des jointures de requête lorsque vous choisissez différents attributs pour les résultats de votre requête, l'onglet **Jointures** fournit d'autres options avancées. Les classes d’attributs prises en charge par System Center 2012 Configuration Manager sont indiquées dans le tableau ci-dessous :  

    |Type de jointure|Description|  
    |---------------|-----------------|  
    |Interne|Affiche uniquement les résultats ayant une correspondance ; ce type est toujours utilisé par les jointures qui sont créées automatiquement.|  
    |Gauche|Affiche tous les résultats pour l'attribut de base et uniquement les résultats ayant une correspondance pour l'attribut de jointure.|  
    |Droit|Affiche tous les résultats pour l'attribut de jointure et seulement les résultats ayant une correspondance pour l'attribut de base.|  
    |Complète|Affiche tous les résultats à la fois pour l'attribut de base et pour l'attribut de jointure.|  

     Pour plus d’informations sur la manière d’utiliser des opérations de jointure, consultez votre documentation SQL Server.  

10. Choisissez **OK** pour fermer la boîte de dialogue **Propriétés de l’instruction de** *&lt;Nom de la requête\>*.  

11. Sous l’onglet **Général** de l’**Assistant Création de requête**, spécifiez si les résultats de cette requête ne sont pas limités aux membres d’un regroupement, s’ils sont limités aux membres d’un regroupement spécifique ou s’ils affichent une invite pour choisir un regroupement à chaque exécution de la requête.  

12. Terminez l'assistant pour créer la requête. La nouvelle requête s’affiche dans le nœud **Requêtes** de l’espace de travail **Surveillance** .  

##  <a name="BKMK_Import"></a> Comment importer des requêtes  
 Procédez comme suit pour importer une requête dans Configuration Manager. Pour plus d'informations sur l’exportation des requêtes, voir [Guide pratique pour gérer des requêtes dans System Center Configuration Manager](../../../core/servers/manage/manage-queries.md).  

#### <a name="to-import-a-query"></a>Pour importer une requête  

1.  Dans la console Configuration Manager, choisissez **Surveillance**.  

2.  Dans l'espace de travail **Surveillance**, choisissez **Requêtes**. Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Importer des objets**.  

3.  Dans la page **Nom du fichier MOF** de l’**Assistant Importation d’objets**, choisissez **Parcourir** pour sélectionner le fichier MOF (Managed Object Format) contenant la requête à importer.  

4.  Passez en revue les informations relatives à la requête à importer, puis terminez l’Assistant. La nouvelle requête s’affiche dans le nœud **Requêtes** de l’espace de travail **Surveillance**.  

##  <a name="BKMK_Example"></a> Example WQL queries

Cette section contient des exemples de requêtes WMI que vous pouvez utiliser dans votre hiérarchie ou modifier à d’autres fins. Pour utiliser ces requêtes, choisissez **Afficher la requête** dans la boîte de dialogue **Propriétés de l'instruction de la requête**. Puis copiez et collez la requête dans le champ **Instruction de la requête**.  

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

Utilisez la requête suivante pour retourner le nom NetBIOS et le nom du package logiciel de tous les ordinateurs dotés d’un package logiciel spécifique installé. Cet exemple affiche tous les ordinateurs sur lesquels une version de Microsoft Visio est installée. Remplacez `%Visio%` par le package logiciel à rechercher.  

> [!TIP]  
> Cette requête recherche le package logiciel en utilisant les noms figurant dans la liste des programmes inclus dans le Panneau de configuration Windows.  

```  
select SMS_R_System.NetbiosName,   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from    
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on   
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =   
SMS_R_System.ResourceId where   
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "%Visio%"  
```  

### <a name="computers-that-are-in-a-specific-active-directory-domain-services-organizational-unit"></a>Ordinateurs situés dans une unité d’organisation (UO) des services de domaine Active Directory spécifique

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

Les types d’appareils sont stockés dans la base de données Configuration Manager sous la classe de ressource **sms_r_system** et le nom d’attribut **AgentEdition**. Utilisez la requête suivante pour récupérer uniquement les appareils correspondant à l’édition agent du type d’appareil que vous spécifiez :  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Utilisez l’une des valeurs suivantes pour *&lt;ID d’appareil\>*  :  

|Type d'appareil|Valeur de AgentEdition|  
|-----------------|---------------------------|  
|Ordinateur portable ou de bureau Windows|0|  
|Appareil ARM Windows (exécutant Windows RT)|1|  
|Windows Mobile 6.5|2|  
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

 Par exemple, si vous voulez que la requête retourne uniquement des ordinateurs Mac, utilisez la requête suivante :  

```  
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="see-also"></a>Voir aussi  
 [Opérations et maintenance pour les requêtes dans System Center Configuration Manager](../../../core/servers/manage/operations-and-maintenance-for-queries.md)
