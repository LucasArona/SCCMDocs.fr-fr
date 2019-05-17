---
title: Publier des données de site
titleSuffix: Configuration Manager
description: Découvrez comment publier des sites Configuration Manager dans les services de domaine Active Directory.
ms.date: 2/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: bce6e2d18da1c2cb87a52fdef545d1b23f602f38
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501424"
---
# <a name="publish-site-data-for-system-center-configuration-manager"></a>Publication de données de site pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Après avoir développé le schéma Active Directory pour System Center Configuration Manager, vous pouvez publier des sites Configuration Manager sur Active Directory Domain Services (AD DS). Les ordinateurs Active Directory peuvent ainsi récupérer en toute sécurité des informations de site à partir d’une source approuvée. La publication des informations de site sur AD DS n’est pas obligatoire pour les fonctionnalités de base de Configuration Manager, mais elle peut réduire la surcharge administrative.  

-   **Quand un site est configuré pour publier dans AD DS**, les clients Configuration Manager peuvent trouver automatiquement des points de gestion par le biais de la publication Active Directory. Ils utilisent une requête LDAP à un serveur de catalogue global.  

-   **Quand un site ne publie pas dans AD DS**, les clients doivent utiliser une autre méthode pour rechercher leur point de gestion par défaut.  

Pour plus d’informations sur la façon dont les clients trouvent un point de gestion, consultez [Comprendre comment les clients recherchent des services et des ressources de site pour System Center Configuration Manager](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Configuration des sites à publier dans AD DS  
 Les étapes principales sont les suivantes :  

-   Vous devez [étendre le schéma Active Directory pour System Center Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) dans chaque forêt où vous allez publier des données de site. Vérifiez aussi que le conteneur **System Management** est présent.  

-   Vous devez accorder au compte d’ordinateur de chaque site principal devant publier des données le **contrôle total** sur le conteneur **System Management** et tous ses objets enfants.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>Pour autoriser un site Configuration Manager à publier des informations de site sur une forêt Active Directory

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l'espace de travail **Administration** , développez **Configuration du site**, puis cliquez sur **Sites**. Sélectionnez le site dont vous souhaitez publier les données. Sous l’onglet **Accueil**, dans le groupe **Propriétés**, cliquez sur **Propriétés**.  

3.  Sous l’onglet **Publication** des propriétés du site, sélectionnez les forêts sur lesquelles ce site devra publier les données de site.  

4.  Cliquez sur **OK** pour enregistrer la configuration.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>Pour configurer des forêts Active Directory pour la publication  

1.  Dans la console Configuration Manager, cliquez sur **Administration**.  

2.  Dans l’espace de travail **Administration**, développez **Configuration de la hiérarchie**, puis cliquez sur **Forêts Active Directory**. Si la découverte de forêts Active Directory a été exécutée précédemment, vous pouvez voir chaque forêt découverte dans le volet des résultats. La forêt locale et toutes les forêts approuvées sont découvertes lorsque la Découverte de forêts Active Directory s'exécute. Seules les forêts non approuvées doivent être ajoutées manuellement.  

    -   Pour configurer une forêt qui a été découverte, sélectionnez la forêt dans le volet de résultats. Ensuite, sous l’onglet **Accueil**, dans le groupe **Propriétés**, cliquez sur **Propriétés** pour ouvrir les propriétés de la forêt. Passez à l'étape 3.  

    -   Pour configurer une nouvelle forêt qui n’est pas répertoriée, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Ajouter une forêt** pour ouvrir la boîte de dialogue **Ajouter une forêt**. Passez à l'étape 3.  

3.  Sous l’onglet **Général**, remplissez les configurations pour la forêt que vous souhaitez découvrir et spécifiez le **Compte de forêt Active Directory**.  

    > [!NOTE]  
    >  La découverte de forêts Active Directory requiert un compte global pour découvrir et publier les forêts non approuvées. Si vous n'utilisez pas le compte d'ordinateur du serveur du site, vous pouvez uniquement sélectionner un compte global.  

4.  Si vous prévoyez d'autoriser des sites à publier des données de site pour cette forêt, dans l'onglet **Publication** , remplissez la configuration de la publication de cette forêt.  

    > [!NOTE]  
    >  Si vous autorisez les sites à publier sur une forêt, vous devez étendre le schéma Active Directory de cette forêt pour Configuration Manager. Le compte de forêt Active Directory doit avoir des autorisations Contrôle total sur le conteneur système dans cette forêt.  

5.  Lorsque vous terminez la configuration de cette forêt pour une utilisation avec la Découverte de forêts Active Directory, cliquez sur **OK** pour enregistrer la configuration.  
