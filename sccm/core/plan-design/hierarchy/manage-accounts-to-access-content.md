---
title: Comptes pour accéder au contenu
titleSuffix: Configuration Manager
description: En savoir plus sur les comptes où les clients accèdent au contenu System Center Configuration Manager.
ms.date: 2/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a7df9d0f-fbde-47eb-97e7-3d29536424fa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c21601246cb0024837256b7cf8d4c1576c00149d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="manage-accounts-to-access-content-in-system-center-configuration-manager"></a>Gérer les comptes pour accéder au contenu dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de déployer du contenu dans System Center Configuration Manager, déterminez de quelle façon les clients accèderont à ce contenu à partir des points de distribution. Cet article décrit les comptes suivants utilisés à cette fin :

-   **Compte d’accès réseau**. Utilisé par les clients pour se connecter à un point de distribution et accéder au contenu. Par défaut, les clients essaient d’abord d’utiliser leur compte d’ordinateur.

     Ce compte est également utilisé par les points de distribution d’extraction pour obtenir le contenu d’un point de distribution source dans une forêt distante.  

-   **Compte d’accès au package**. Par défaut, Configuration Manager octroie aux comptes intégrés appelés **Utilisateurs** et **Administrateurs** l’accès au contenu d’un point de distribution. Vous pouvez configurer des autorisations supplémentaires pour limiter l’accès.  

-   **Compte de connexion multidiffusion**. Utilisé pour les déploiements de système d’exploitation.  

##  <a name="bkmk_NAA"></a> Compte d’accès réseau  
 Les ordinateurs clients utilisent le compte d’accès réseau quand ils ne peuvent pas utiliser leur compte d’ordinateur local pour accéder au contenu sur les points de distribution. Par exemple, cela s'applique aux clients du groupe de travail et aux ordinateurs de domaines non approuvés. Ce compte peut également être utilisé pendant le déploiement du système d'exploitation si l'ordinateur qui installe le système d'exploitation ne possède pas encore de compte d'ordinateur sur le domaine.  

-   Les clients utilisent le compte d'accès réseau uniquement pour accéder aux ressources du réseau.  

-   Sur chaque site principal, vous pouvez configurer plusieurs comptes à utiliser comme compte d’accès réseau.  

-   Les clients tentent d’abord d’accéder au contenu sur un point de distribution à l’aide de leur compte *nom_ordinateur*$. Si l’accès avec ce compte n’est pas possible, ils tentent alors d’utiliser un compte d’accès réseau. Les clients continuent d’essayer d’utiliser le compte d’accès réseau, même en cas d’échec antérieur.  

### <a name="permissions"></a>Autorisations
Accordez les autorisations minimales appropriées à ce compte, pour qu'il puisse accéder au logiciel pour le contenu que nécessite le client.  

-   Le compte doit avoir le droit **Accéder à cet ordinateur à partir du réseau** sur le point de distribution.  

-   Créez le compte dans n'importe quel domaine fournissant l'accès nécessaire aux ressources. Le compte d'accès réseau doit toujours inclure un nom de domaine. La sécurité directe n’est pas prise en charge pour ce compte. Si vous disposez de points de distribution dans plusieurs domaines, créez le compte dans un domaine approuvé.  

> [!TIP]  
>  Pour éviter les verrouillages de compte, ne modifiez pas le mot de passe d'un compte d'accès réseau existant. Au lieu de cela, créez un compte et configurez le nouveau compte dans Configuration Manager. Après un délai suffisant pendant lequel tous les clients ont reçu les informations du nouveau compte, supprimez l’ancien compte des dossiers partagés du réseau et supprimez le compte.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations d’ouverture de session interactive.  
>   
>  N'accordez pas à ce compte le droit de joindre les ordinateurs au domaine. Si vous devez joindre les ordinateurs au domaine au cours d'une séquence de tâches, utilisez le compte de jonction de domaine de l'Éditeur de séquence de tâches.  

### <a name="to-configure-the-network-access-account"></a>Pour configurer le compte d'accès réseau  

1.  Dans la console Configuration Manager, choisissez **Administration** >   **Configuration du site** >  **Sites**, puis sélectionnez le site.  

2.  Dans le groupe **Paramètres**, choisissez **Configurer les composants de site** > **Distribution de logiciels**.  

3.  Choisissez l’onglet **Compte d’accès réseau**. Configurez un ou plusieurs comptes, puis choisissez **OK**.  

##  <a name="bkmk_Paa"></a> Comptes d’accès aux packages  
 Les comptes d’accès au package vous permettent de définir des autorisations NTFS pour spécifier les utilisateurs et les groupes d’utilisateurs qui peuvent accéder à un contenu de package sur des points de distribution. Par défaut, Configuration Manager n’accorde cet accès qu’aux comptes génériques **Utilisateurs** et **Administrateurs**. Vous pouvez cependant contrôler l’accès pour les ordinateurs clients à l’aide d’autres comptes ou groupes Windows. Les appareils mobiles n’utilisent pas les comptes d’accès au package, car ces appareils récupèrent toujours le contenu du package de façon anonyme.  

 Par défaut, quand Configuration Manager copie les fichiers de contenu d’un package sur un point de distribution, il accorde un accès en **Lecture** au groupe **Utilisateurs** local et un **Contrôle intégral** au groupe **Administrateurs** local. Les autorisations requises dépendent du package. Si vous avez des clients dans des groupes de travail ou dans des forêts non approuvées, ceux-ci utiliseront le compte d'accès réseau pour accéder au contenu du package. Assurez-vous que le compte d'accès réseau bénéficie d'autorisations sur le package à l'aide des comptes d'accès au package définis.  

 Utilisez des comptes dans un domaine susceptible d'accéder aux points de distribution. Si vous créez ou modifiez le compte une fois le package créé, vous devez redistribuer le package. La mise à jour du package ne modifie pas les autorisations de système de fichiers NTFS sur le package.  

 Il est inutile d'ajouter le compte d'accès réseau comme un compte d'accès au package, car l'appartenance au groupe **Utilisateurs** l'ajoute automatiquement. Le fait de restreindre le compte d'accès au package au compte d'accès réseau uniquement n'empêche pas les clients d'accéder au package.  

### <a name="to-manage-access-accounts"></a>Pour gérer les comptes d'accès  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels**.  

2.  Dans l’espace de travail **Bibliothèque de logiciels**, déterminez le type de contenu dont vous souhaitez gérer les comptes d’accès et suivez les étapes indiquées :  

    -   **Applications** : développez **Gestion d’applications**, choisissez **Applications**, puis sélectionnez les applications dont vous souhaitez gérer les comptes d’accès.  

    -   **Packages** : développez **Gestion d’applications**, choisissez **Packages**, puis sélectionnez les packages dont vous souhaitez gérer les comptes d’accès.  

    -   **Packages de déploiement** : développez **Mises à jour logicielles**, choisissez **Packages de déploiement**, puis sélectionnez les packages de déploiement dont vous souhaitez gérer les comptes d’accès.  

    -   **Packages de pilotes** : développez **Systèmes d’exploitation**, choisissez **Packages de pilotes**, puis sélectionnez les packages de pilotes dont vous souhaitez gérer les comptes d’accès.  

    -   **Images du système d’exploitation** : développez **Systèmes d’exploitation**, choisissez **Images du système d’exploitation**, puis sélectionnez les images du système d’exploitation dont vous souhaitez gérer les comptes d’accès.  

    -   **Programmes d’installation de système d’exploitation** : développez **Systèmes d’exploitation**, choisissez **Programmes d’installation de système d’exploitation**, puis sélectionnez les programmes d’installation de système d’exploitation dont vous souhaitez gérer les comptes d’accès.  

    -   **Images de démarrage** : développez **Systèmes d’exploitation**, choisissez **Images de démarrage**, puis sélectionnez les images de démarrage dont vous souhaitez gérer les comptes d’accès.  

3.  Cliquez avec le bouton droit sur l’objet sélectionné, puis choisissez **Gérer des comptes d’accès**.  

4.  Dans la boîte de dialogue **Ajouter un compte**, spécifiez le type du compte auquel les droits d’accès au contenu seront accordés, puis indiquez les droits d’accès associés au compte.  

    > [!NOTE]  
    >  Quand vous ajoutez un nom d’utilisateur au compte et que Configuration Manager trouve un compte d’utilisateur local et un compte d’utilisateur de domaine portant ce nom, Configuration Manager définit les droits d’accès du compte d’utilisateur de domaine.  

##  <a name="bkmk_multi"></a> Compte de connexion multidiffusion  
 Le compte de connexion multidiffusion est utilisé par des points de distribution qui sont configurés pour la multidiffusion pour lire les informations de la base de données de site.  

-   Vous spécifiez un compte à utiliser quand vous configurez des connexions de base de données Configuration Manager pour la multidiffusion.  

-   Le compte d’ordinateur du point de distribution est utilisé par défaut, mais vous pouvez configurer un compte d’utilisateur à la place.  

-   Chaque fois que la base de données de site est dans une forêt non approuvée, vous devez spécifier un compte d'utilisateur.  

-   Le compte doit avoir des autorisations **d’accès en lecture** à la base de données de site.  

Par exemple, si votre centre de données dispose d'un réseau de périmètre dans une forêt autre que celle du serveur de site et de la base de données du site, vous pouvez utiliser ce compte pour lire les informations sur la multidiffusion à partir de la base de données du site.

Si vous créez ce compte, créez-le en tant que compte local doté de droits limités sur l’ordinateur qui exécute Microsoft SQL Server.  

> [!IMPORTANT]  
>  N’accordez pas à ce compte des autorisations d’ouverture de session interactive.  
