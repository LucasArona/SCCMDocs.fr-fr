---
title: Protection d’applications à l’aide de stratégies de gestion des applications mobiles
titleSuffix: Configuration Manager
description: Modifiez les fonctionnalités des applications que vous déployez pour qu’elles respectent les stratégies de sécurité et de conformité de votre entreprise.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 28115475-e563-4e16-bf30-f4c9fe704754
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d7da4767bd8ef26ebf3f56010e99bc1cbd0b0c10
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62227860"
---
# <a name="protect-apps-using-mobile-application-management-policies-in-system-center-configuration-manager"></a>Protéger des applications à l’aide de stratégies de gestion des applications mobiles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les stratégies de gestion des applications System Center Configuration Manager vous permettent de modifier les fonctionnalités des applications que vous déployez pour qu’elles respectent les stratégies de conformité et de sécurité de votre entreprise. Par exemple, vous pouvez restreindre les opérations Couper, Copier et Coller au sein d’une application limitée, ou configurer une application pour ouvrir toutes les URL dans Managed Browser. Les stratégies de gestion des applications prennent en charge :  

-   appareils qui exécutent Android 4 et versions ultérieures ;  

-   Appareils qui exécutent iOS 9 et versions ultérieures  

Vous pouvez également utiliser des stratégies de gestion des applications mobiles pour protéger des applications sur des appareils non gérés par Intune. Grâce à cette nouvelle fonctionnalité, vous pouvez appliquer des stratégies de gestion des applications mobiles aux applications se connectant aux services Office 365. Ces stratégies ne sont pas prises en charge pour les applications qui se connectent à Exchange ou SharePoint au niveau local.  

Pour utiliser cette nouvelle fonctionnalité, vous devez utiliser le portail Azure en version préliminaire. Les rubriques suivantes peuvent vous aider dans la prise en main :  
- [Prise en main des stratégies de gestion des applications mobiles dans le portail Azure](https://technet.microsoft.com/library/mt627830.aspx)  
- [Créer et déployer des stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](https://technet.microsoft.com/library/mt627829.aspx)  

  Contrairement aux éléments de configuration et aux bases de référence dans Configuration Manager, vous ne déployez pas une stratégie de gestion des applications directement. Au lieu de cela, vous associez la stratégie au type de déploiement d’application que vous voulez restreindre. Quand le type de déploiement d’application est déployé et installé sur les appareils, les paramètres que vous spécifiez prennent effet.  

Pour appliquer des restrictions à une application, celle-ci doit intégrer le Kit de développement logiciel (SDK) d’application Microsoft Intune. Il existe deux méthodes pour obtenir ce type d'application :  

-   **Utiliser une application gérée par stratégie** (Android et iOS) : Ces applications ont le SDK d’application. Pour ajouter ce type d'application, spécifiez un lien vers l'application à partir d'un magasin d'applications tel que l'iTunes Store ou Google Play. Aucun traitement supplémentaire n'est nécessaire pour ce type d'application. Pour obtenir une liste des applications gérées par une stratégie qui sont disponibles pour les appareils iOS et Android, consultez [Applications gérées pour les stratégies de gestion des applications mobiles Microsoft Intune](https://technet.microsoft.com/library/dn708489.aspx).  

-   **Utiliser une application « encapsulée »** (Android et iOS) : Ces applications sont réempaquetées pour inclure le SDK d’application à l’aide de la **Microsoft Intune App Wrapping Tool**. On utilise généralement cet outil pour traiter les applications d'entreprise qui ont été créées en interne. Vous ne pouvez pas l'utiliser pour traiter les applications qui ont été téléchargées à partir du magasin d'applications. Pour plus d’informations, consultez les articles suivants :
    - [Préparer des applications iOS pour la gestion des applications mobiles avec l’outil de création de package de restrictions d’application Microsoft Intune](https://technet.microsoft.com/library/dn878028.aspx)

    - [Préparer des applications Android pour la gestion des applications mobiles avec l’outil de création de package de restrictions d’application Microsoft Intune](https://technet.microsoft.com/library/mt147413.aspx)  

## <a name="create-and-deploy-an-app-with-a-mobile-application-management-policy"></a>Créer et déployer une application avec une stratégie de gestion des applications mobiles  

##  <a name="step-1-obtain-the-link-to-a-policy-managed-app-or-create-a-wrapped-app"></a>Étape 1 : Obtenir le lien vers une application gérée par stratégie ou créer une application encapsulée  

-   **Pour obtenir un lien à une stratégie d’application gérée**: À partir de l’app store, recherchez et notez l’URL de l’application gérée de stratégie à déployer.  

     Par exemple, l’URL de l’application Microsoft Word pour iPad est **https://itunes.apple.com/us/app/microsoft-word-for-ipad/id586447913?mt=8**  

-   **Pour créer une application encapsulée**: Utilisez les informations dans les rubriques [préparer des applications iOS pour la gestion des applications mobiles avec Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/library/dn878028.aspx) et [préparer des applications Android pour la gestion des applications mobiles avec Microsoft Intune App Wrapping Tool](https://technet.microsoft.com/library/mt147413.aspx) pour créer une application encapsulée.  

     L'outil crée une application traitée et un fichier manifeste associé. Vous utilisez ces fichiers quand vous créez une application Configuration Manager contenant l’application.  

##  <a name="step-2-create-a-configuration-manager-application-that-contains-an-app"></a>Étape 2 : Créer une application Configuration Manager qui contient une application  
 La procédure de création de l’application Configuration Manager diffère selon que vous utilisez une application gérée par une stratégie (lien externe) ou une application qui a été créée avec l’outil de création de package de restrictions d’application Microsoft Intune pour iOS (package d’application pour iOS). Utilisez l’une des procédures suivantes pour créer l’application Configuration Manager.  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

2. Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application** pour ouvrir l’Assistant **Création d’une application**.  

3. Sous l'onglet **Général** , sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d'installation**.  

4. Dans la liste déroulante **Type**, sélectionnez **Package d’application pour iOS (fichier \*.ipa)**.  

5. Choisissez **Parcourir** pour sélectionner le package d’application à importer, puis **Suivant**.  

6. Sur la page **Informations générales** , entrez le texte descriptif et les informations de catégorie que vous souhaitez montrer aux utilisateurs sur le portail d'entreprise.  

7. Effectuez toutes les étapes de l'Assistant.  

   La nouvelle application s'affiche dans le nœud **Applications** de l'espace de travail **Bibliothèque de logiciels** .  

### <a name="create-an-application-that-contains-a-link-to-a-policy-managed-app"></a>Créer une application contenant un lien vers une application gérée par une stratégie  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.  

2. Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une application** pour ouvrir l’Assistant **Création d’une application**.  

3. Sous l'onglet **Général** , sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d'installation**.  

4. Dans la liste déroulante **Type** , sélectionnez l'un des éléments suivants :  

   -   Pour iOS : **Package d’application pour iOS depuis l’App Store**  

   -   Pour Android : **Package d’application pour Android sur Google Play**  

5. Entrez l’URL de l’application (obtenue à l’étape 1), puis choisissez **Suivant**.  

6. Sur la page **Informations générales** , entrez le texte descriptif et les informations de catégorie que vous souhaitez montrer aux utilisateurs sur le portail d'entreprise.  

7. Effectuez toutes les étapes de l'Assistant.  

   La nouvelle application s'affiche dans le nœud **Applications** de l'espace de travail **Bibliothèque de logiciels** .  

##  <a name="step-3-create-an-application-management-policy"></a>Étape 3 : Créer une stratégie de gestion des applications  
 Ensuite, créez une stratégie de gestion d’application que vous associez à l’application. Vous pouvez créer une stratégie générale ou Managed Browser.  

1)  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de gestion d’application**.  

2)  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une stratégie de gestion d’application**.  

3)  Dans la page **Général**, entrez le nom et la description de la stratégie, puis choisissez **Suivant**.  

4)  Dans la page **Type de stratégie**, sélectionnez la plateforme et le type de cette stratégie, puis choisissez **Suivant**. Les types de stratégies suivants sont disponibles :  

-   **Général**: Le type de stratégie général vous permet de modifier les fonctionnalités des applications que vous déployez pour aider à les aligner sur la conformité et votre entreprise des stratégies de sécurité. Par exemple, vous pouvez limiter les opérations Couper, Copier et Coller dans une application restreinte.  

-   **Managed Browser**: La stratégie Managed Browser vous permet de décider s’il faut autoriser ou empêcher managed browser d’ouvrir une liste d’URL. Le type de stratégie Managed Browser vous permet de modifier les fonctionnalités de l'application Intune Managed Browser. Il s'agit d'un navigateur web qui vous permet de gérer les actions que les utilisateurs peuvent effectuer, y compris les sites qu'ils peuvent visiter et le mode d'ouverture des liens vers du contenu dans le navigateur. En savoir plus sur l’  [application Intune Managed Browser pour iOS](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) et [l’application Intune Managed Browser pour Android](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en).

5)  Dans la page **Stratégie iOS** ou **Stratégie Android**, configurez les valeurs suivantes selon les besoins, puis choisissez **Suivant**. Les options peuvent différer selon le type d'appareil pour lequel vous configurez la stratégie.  

|Valeur|Informations complémentaires|  
|-----------|----------------------|  
|**Afficher le contenu web uniquement dans Managed Browser**|Autorise l’ouverture de tous les liens de l’application dans Managed Browser. Pour que cette option fonctionne, vous devez avoir déployé cette application sur des appareils.|  
|**Interdire les sauvegardes Android** ou **Interdire les sauvegardes iTunes et iCloud**|Désactive la sauvegarde de toutes les informations à partir de l'application.|  
|**Autoriser l'application à transférer des données vers d'autres applications**|Spécifie les applications auxquelles cette application peut envoyer des données. Vous pouvez choisir de n’autoriser le transfert de données vers aucune application, d’autoriser le transfert vers d’autres applications restreintes ou d’autoriser le transfert vers toute application.<br /><br /> Pour les appareils iOS, pour empêcher le transfert de documents entre les applications gérées et non gérées, vous devez aussi configurer et déployer une stratégie de sécurité d'appareil mobile qui désactive le paramètre **Autoriser les documents gérés dans d'autres applications non gérées**.<br /><br /> Si vous choisissez d’autoriser uniquement le transfert vers d’autres applications restreintes, les visionneuses d’images et PDF Intune (si elles sont déployées) sont utilisées pour ouvrir le contenu des types respectifs.|  
|**Autoriser l'application à recevoir des données d'autres applications**|Spécifie les applications à partir desquelles cette application peut recevoir des données. Vous pouvez choisir de n’autoriser le transfert de données à partir d’aucune application, d’autoriser le transfert uniquement à partir d’autres applications restreintes, ou d’autoriser le transfert à partir de toute application.|  
|**Interdire « Enregistrer sous »**|Désactive l’utilisation de l’option **Enregistrer sous** dans toute application qui utilise cette stratégie.|  
|**Restreindre les opérations couper, copier et coller avec d'autres applications**|Spécifie comment les opérations couper, copier et coller peuvent être utilisées avec l'application. Choisissez parmi :<br /><br /> **Bloqué** : n’autorise pas les opérations couper, copier et coller entre cette application et d’autres applications.<br /><br /> **Applications gérées par la stratégie** : autorise les opérations couper, copier et coller entre cette application uniquement et d’autres applications restreintes.<br /><br /> **Applications gérées par la stratégie avec Coller dans** : autorise le collage de données coupées ou copiées à partir de cette application uniquement dans d’autres applications restreintes. Autorise le collage dans cette application de données coupées ou copiées à partir de n’importe quelle application.<br /><br /> **N’importe quelle application** : aucune restriction pour les opérations couper, copier et coller vers ou à partir de cette application.|  
|**Demander un code confidentiel simple pour l'accès**|Oblige l’utilisateur à entrer un code confidentiel qu’il spécifie pour utiliser cette application. L’utilisateur est invité à définir ce code la première fois qu’il exécute l’application.|  
|**Nombre de tentatives avant réinitialisation du code confidentiel**|Spécifie le nombre de tentatives dont dispose l’utilisateur pour taper le code confidentiel avant d’être obligé de réinitialiser le code confidentiel.|  
|**Exiger des informations d'identification d'entreprise pour l'accès**|Exige que l’utilisateur entre ses informations de connexion d’entreprise pour accéder à l’application.|  
|**Exiger la conformité à la stratégie d'entreprise pour l'accès**|Autorise l’utilisation de l’application uniquement si l’appareil n’est pas jailbroken ou rooté.|  
|**Revérifier les exigences d'accès après (minutes)**|Indique le délai au bout duquel les conditions d’accès pour l’application sont revérifiées après son démarrage (dans le champ **Délai**).<br /><br /> Dans le champ **Période de grâce hors connexion**, si l’appareil est hors connexion, spécifie le délai au bout duquel les conditions d’accès pour l’application sont revérifiées.|  
|**Chiffrer les données de l'application**|Spécifie que toutes les données associées à cette application sont chiffrées, notamment les données stockées en externe, comme les données stockées sur des cartes SD.<br /><br /> **Chiffrement pour iOS**<br /><br /> Pour les applications associées à une stratégie de gestion des applications mobiles Configuration Manager, les données sont chiffrées au repos à l’aide du chiffrement au niveau de l’appareil fourni par le système d’exploitation. Cette option est activée par le biais de la stratégie de code confidentiel d’appareil qui doit être définie par l’administrateur informatique. Quand un code confidentiel est nécessaire, les données sont chiffrées selon les paramètres de la stratégie de gestion des applications mobiles. Comme indiqué dans la documentation Apple, [les modules utilisés par iOS 7 sont certifiés FIPS 140-2](http://support.apple.com/en-us/HT202739).<br /><br /> **Chiffrement pour Android**<br /><br /> Pour les applications associées à une stratégie de gestion des applications mobiles Configuration Manager, le chiffrement est fourni par Microsoft. Les données sont chiffrées de manière synchrone durant les opérations d'E/S de fichier conformément au paramètre indiqué dans la stratégie de gestion des applications mobiles. Les applications gérées sur Android utilisent le chiffrement AES-128 en mode CBC, avec utilisation des bibliothèques de chiffrement de plateforme. La méthode de chiffrement n'est pas certifiée FIPS 140-2. Le contenu figurant sur le stockage de l’appareil est toujours chiffré.|  
    |**Bloquer la capture d'écran** (appareils Android uniquement)|Spécifie que les fonctionnalités de capture d'écran de l'appareil sont bloquées lors de l'utilisation de cette application.|  
    |**Désactiver la synchronisation des contacts**| À compter de la version 1710, cette option empêche l’application d’enregistrer des données sur l’application Contacts native de l’appareil. Si vous choisissez Non, l’application peut enregistrer des données sur l’application Contacts native sur l’appareil.|  
    |**Désactiver l’impression**| À compter de la version 1710, cette option empêche l’application d’imprimer des données scolaires ou de travail. |  

6)  Dans la page **Managed Browser**, indiquez si Managed Browser est autorisé à ouvrir uniquement les URL figurant dans la liste ou si vous souhaitez l’empêcher d’ouvrir les URL figurant dans la liste, puis choisissez **Suivant**.  
Pour plus d’informations, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](manage-internet-access-using-managed-browser-policies.md).  

7)  Effectuez toutes les étapes de l'Assistant.  

 La nouvelle stratégie s'affiche dans le nœud **Stratégies de gestion d'application** de l'espace de travail **Bibliothèque de logiciels** .  

##  <a name="step-4-associate-the-application-management-policy-with-a-deployment-type"></a>Étape 4 : Associer la stratégie de gestion des applications avec un type de déploiement  

 Quand un type de déploiement est créé pour une application qui nécessite une stratégie de gestion des applications, Configuration Manager vous invite à associer une stratégie de gestion des applications. Pour Managed Browser, vous devez associer une stratégie Général et une stratégie Managed Browser. Pour plus d’informations, consultez [Créer des applications](create-applications.md).  

> [!IMPORTANT]  
>  Si l’application est déjà déployée, le déploiement du nouveau type de déploiement échoue tant que cette association n’est pas effectuée. Vous pouvez créer l'association dans les **Propriétés** de l'application, sous l'onglet **Gestion des applications** .  

> [!IMPORTANT]  
>  Pour les appareils qui exécutent des systèmes d’exploitation antérieurs à iOS 7.1, les stratégies associées ne sont pas supprimées quand l’application est désinstallée.  
>   
>  Si l’inscription de l’appareil dans Configuration Manager est annulée, les stratégies ne sont pas supprimées des applications. Les applications pour lesquelles des stratégies étaient appliquées conservent les paramètres de stratégie après la désinstallation et la réinstallation de l’application.  

##  <a name="step-5-monitor-the-app-deployment"></a>Étape 5 : Surveiller le déploiement de l’application  
 Une fois que vous avez créé et déployé une application associée à une stratégie de gestion des applications mobiles, vous pouvez analyser l’application et résoudre les éventuels conflits de stratégie.  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Vue d’ensemble** > **Déploiements**.  

2. Sélectionnez le déploiement que vous avez créé. Sous l’onglet **Accueil**, choisissez **Propriétés**.  

3. Dans le volet de détails du déploiement, sous **Objets associés**, choisissez **Stratégies de gestion d’application**.  

   Pour plus d’informations sur la surveillance des applications, consultez [Surveiller des applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

##  <a name="learn-how-policy-conflicts-are-resolved"></a>Découvrir comment les conflits de stratégie sont résolus  
 En cas de conflit de stratégie de gestion des applications mobiles lors du premier déploiement vers l’utilisateur ou l’appareil, la valeur de paramètre spécifique en conflit est supprimée de la stratégie déployée sur l’application. L’application utilise ensuite une valeur de conflit intégrée.  

 En cas de conflit de stratégie de gestion des applications mobiles lors de déploiements ultérieurs vers l’application ou l’utilisateur, la valeur de paramètre spécifique en conflit n’est pas mise à jour sur la stratégie de gestion des applications mobiles déployée vers l’application et celle-ci utilise la valeur existante pour ce paramètre.  

 Dans les cas où l'appareil ou l'utilisateur reçoit deux stratégies en conflit, le comportement suivant s'applique :  

-   Si une stratégie a été déployée sur l’appareil, les paramètres de stratégie existants ne sont pas remplacés.  

-   Si aucune stratégie n’a encore été déployée sur l’appareil et que deux paramètres en conflit sont déployés, le paramètre par défaut intégré à l’appareil est utilisé.  

##  <a name="see-a-list-of-available-policy-managed-apps"></a>Afficher la liste des applications gérées par la stratégie disponibles  
 Pour obtenir la liste des applications gérées par une stratégie disponibles pour les appareils iOS et Android, consultez [Partenaires d’application Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-partners).  
