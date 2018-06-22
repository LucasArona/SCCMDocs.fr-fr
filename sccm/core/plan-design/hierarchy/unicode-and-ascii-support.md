---
title: Prise en charge Unicode et ASCII
titleSuffix: Configuration Manager
description: Découvrez la prise en charge des caractères ASCII et Unicode dans les objets System Center Configuration Manager.
ms.date: 3/1/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 2bdec799-905f-48bc-aed5-2d92134739e8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 6212a22a8ed2fbce7dda19a0b70b0336812b2827
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338327"
---
# <a name="unicode-and-ascii-support-in-system-center-configuration-manager"></a>Prise en charge Unicode et ASCII dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager crée la plupart des objets à l’aide de caractères Unicode. Cependant, plusieurs objets prennent en charge uniquement des caractères ASCII ou disposent d'autres limitations.  

 Les sections suivantes répertorient les objets qui ne doivent utiliser que les caractères du jeu de caractères ASCII, ou qui ont des limitations supplémentaires.  

-   [Objets qui utilisent des caractères ASCII](#BKMK_ASCIIchar)  

-   [Limitations supplémentaires](#BKMK_OtherCharLimitations)  

-   [Objets Configuration Manager non localisés](#BKMK_LangNonLocalize)  

##  <a name="BKMK_ASCIIchar"></a> Objets qui utilisent des caractères ASCII  
 Configuration Manager prend en charge le jeu de caractères ASCII uniquement lorsque vous créez les objets suivants :  

-   Code de site  

-   Tous les noms des ordinateurs serveurs du système de site  

-   Les comptes de Configuration Manager suivants :  

    > [!NOTE]  
    >  Ces comptes prennent en charge les caractères ASCII et RUS sur un site qui s’exécute en russe.  

    -   Compte d’installation Push du client  

    -   Compte de publication de la référence d'état d'intégrité  

    -   Compte d'interrogation de référence d'état d'intégrité  

    -   Compte de connexion à la base de données du point de gestion  

    -   Compte d'accès réseau  

    -   Compte d'accès au package  

    -   Compte expéditeur standard  

    -   Compte d’installation du système de site  

    -   Compte de connexion de point de mise à jour logicielle  

    -   Compte du serveur proxy du point de mise à jour logicielle  

    > [!NOTE]  
    >  Les comptes que vous spécifiez pour l'administration basée sur des rôles prennent en charge Unicode.  
    >   
    >  Le compte du point de Reporting Services prend en charge Unicode, à l’exception des caractères RUS.  

-   Nom de domaine complet (FQDN) pour les serveurs de site et les systèmes de site  

-   Chemin d'installation de Configuration Manager  

-   Noms d'instance SQL Server  

-   Le chemin d'accès pour les rôles de système de site suivants :  

    -   Point de service web du catalogue des applications  

    -   Point du site web du catalogue des applications  

    -   Point d'inscription  

    -   Point proxy d'inscription  

    -   Point de Reporting Services  

    -   Point de migration d’état  

-   Chemin d'accès pour les dossiers suivants :  

    -   Le dossier qui stocke les données de migration d'état du client  

    -   Le dossier qui contient les rapports Configuration Manager  

    -   Le dossier qui stocke la sauvegarde de Configuration Manager  

    -   Le dossier qui stocke les fichiers sources d’installation pour la configuration de site  

    -   Le dossier qui stocke les téléchargements requis par le programme d’installation  

-   Le chemin d'accès pour les objets suivants :  

    -   Site Web IIS  

    -   Chemin d'installation de l'application virtuelle  

    -   Nom de l'application virtuelle  

-   Les objets suivants pour AMT et la gestion hors bande :  

    -   Le nom de domaine complet de l'ordinateur basé sur AMT  

    -   Le nom d'ordinateur de l'ordinateur basé sur AMT  

    -   Le nom NetBIOS du domaine  

    -   Le nom du profil sans fil et SSID  

    -   Le nom de l'autorité de certification racine de confiance  

    -   Le nom de l'autorité de certification (CA) et les noms de modèle  

    -   Le nom de fichier et le chemin du fichier image de redirection IDE  

    -   Le contenu du stockage de données AMT  

-   Les noms des fichiers ISO des supports de démarrage  

##  <a name="BKMK_OtherCharLimitations"></a> Limitations supplémentaires  
 Voici les limitations supplémentaires pour les versions de langue et les jeux de caractères pris en charge :  

-   Configuration Manager ne prend pas en charge la modification des paramètres régionaux de l’ordinateur serveur de site.  

-   Une autorité de certification (CA) d'entreprise ne gère pas les noms des ordinateurs clients qui utilisent des jeux de caractères codés sur deux octets (DBCS). Les noms d'ordinateur client que vous pouvez utiliser sont limités par la limitation PKI du jeu de caractères IA5. En outre, Configuration Manager ne prend pas en charge les noms d’autorité de certification ou les valeurs de nom d’objet qui utilisent un jeu de caractères DBCS.  

##  <a name="BKMK_LangNonLocalize"></a> Objets Configuration Manager non localisés  
 La base de données Configuration Manager prend en charge le format Unicode pour la plupart des objets qu’elle stocke, et lorsque cela est possible, elle affiche ces informations dans la langue du système d’exploitation correspondant aux paramètres régionaux d’un ordinateur. Pour que l’interface client ou la console Configuration Manager affichent des informations dans la langue du système d’exploitation de l’ordinateur, les paramètres régionaux de l’ordinateur doivent correspondre à la langue du client ou du serveur que vous installez sur un site.  

 Toutefois, plusieurs objets Configuration Manager ne prennent pas en charge le format Unicode et ils sont stockés dans la base de données à l’aide du jeu de caractères ASCII, ou bien les langues supplémentaires sont limitées. Ces informations s'affichent toujours à l'aide du jeu de caractères ASCII défini ou dans la langue utilisée lors de la création de l'objet.  
