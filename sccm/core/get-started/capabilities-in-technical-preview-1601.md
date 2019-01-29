---
title: Capacités de la version Technical Preview 1601
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique 1601 pour System Center Configuration Manager.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ed6da304f689430d1d141b823646b07deb087928
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54897710"
---
# <a name="capabilities-in-technical-preview-1601-for-system-center-configuration-manager"></a>Fonctionnalités de la version d’évaluation technique 1601 pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique 1601 pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview.      Avant d’installer cette version d’évaluation technique, passez en revue la rubrique de présentation, [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md), pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.  

 **Problèmes connus relatifs à cette version d’évaluation technique :**  

-   quand vous gérez les **Options de mise à jour des clients** pour promouvoir un client de préproduction en production, le texte de la case à cocher affiche zéro (0) pour la version du client, au lieu du numéro réel de la build du client. La version du client de préproduction correcte est affichée sur la zone située au-dessus de cette option : il s’agit de la version du client qui est promue en production quand vous sélectionnez cette option.  

-   Quand vous effectuez une mise à jour vers Technical Preview 1601  et que vous choisissez de tester le client Configuration Manager dans un regroupement de préproduction, le package du client pour le regroupement n’est pas mis à niveau. Ce problème concerne uniquement Technical Preview 1601.  

     Pour contourner ces problèmes, procédez de l’une des façons suivantes :  

    -   Exécutez le script SQL suivant sur la base de données du site principal :  

        ```  
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Ajoutez un nouveau rôle système de site de point de distribution à votre site de laboratoire. Le nouveau point de distribution met à niveau le regroupement de préproduction avec le nouveau package du client.  

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

##  <a name="bkmk_hybrid1"></a> Améliorations apportées à l’intégration de Microsoft Intune  
Dans la version Technical Preview 1601, nous avons ajouté la prise en charge des fonctionnalités suivantes :  

### <a name="improvements-to-conditional-access"></a>Améliorations apportées à l’accès conditionnel  

-   **Prise en charge de l’accès conditionnel pour les PC gérés par System Center Configuration Manager**  

     Vous pouvez maintenant définir des stratégies d’accès conditionnel pour les PC gérés par System Center Configuration Manager, qui exige que les PC soient conformes à la stratégie de conformité pour accéder aux services Exchange Online et SharePoint Online.  Avec cette nouvelle fonctionnalité, vous pouvez également inscrire des PC auprès d’Azure AD via la stratégie de conformité, et surveiller et générer des rapports sur l’inscription Azure Active Directory.  

    > [!NOTE]  
    >  L’accès conditionnel n’est pas encore pris en charge sur Windows 10.  

    Voici la configuration requise pour utiliser cette fonctionnalité :  

    -   Abonnement Premium à Azure Active Directory et Synchronisation ADFS.  

    -   Abonnement Microsoft Intune L’abonnement Microsoft Intune doit être configuré dans la console Configuration Manager.  

    -   [Conditions requises pour l’inscription automatique à Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    Pour utiliser cette option, vous devez créer une stratégie de conformité dans Configuration Manager avec des règles spécifiques décrites ci-dessous, et définir une stratégie d’accès conditionnel dans la console Intune.  En outre, pour que l’accès soit autorisé seulement aux PC conformes, vous devez activer l’option **Les appareils doivent être conformes** comme spécification requise pour les PC Windows. Voici les règles de stratégie de conformité qui sont applicables aux ordinateurs gérés par System Center Configuration Manager.  

    -   **Exiger l’inscription dans Azure Active Directory :** Cette règle vérifie si l’appareil de l’utilisateur a fait l’objet d’une jonction d’espace de travail à Azure AD. Dans le cas contraire, l’appareil est automatiquement inscrit dans Azure AD. L’inscription automatique est prise en charge seulement sur Windows 8.1. Pour les PC Windows 7, déployez un fichier MSI pour effectuer l’inscription automatique. Pour plus d’informations, cliquez [ici](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Toutes les mises à jour requises installées avec une échéance supérieure à un certain nombre de jours :** cette règle vérifie si l’appareil de l’utilisateur a toutes les mises à jour obligatoires (spécifiées dans la règle **Mises à jour automatiques requises**) dans le délai et la période de grâce que vous avez spécifiés. Elle installe automatiquement toutes les mises à jour obligatoires en attente.  

    -   **Exiger le chiffrement de lecteur BitLocker :** cette règle vérifie si le lecteur principal (par exemple C:\\) de l’appareil est chiffré avec BitLocker. Si le chiffrement BitLocker n’est pas activé sur le lecteur principal, l’accès de l’appareil aux services de messagerie et SharePoint est bloqué.  

    -   **Exiger un logiciel anti-programme malveillant :** cette règle vérifie si le logiciel anti-programme malveillant (System Center Endpoint Protection ou Windows Defender uniquement) est activé et en cours d’exécution.  
         S’il n’est pas activé, l’accès aux services de messagerie et SharePoint est bloqué.  

    Les utilisateurs finaux bloqués en raison d’une non-conformité peuvent consulter des informations sur la conformité dans le Centre logiciel SCCM et lancer une nouvelle évaluation de la stratégie quand les problèmes de conformité sont résolus.  

-   **Accès conditionnel avec le service d’attestation d’intégrité** Vous pouvez maintenant limiter l’accès aux services de messagerie et Office 365 en fonction de l’intégrité des appareils, qui est signalée par le service d’attestation d’intégrité.  En outre, les appareils gérés par Intune sont inclus dans les rapports d’intégrité des appareils.  

    Une nouvelle règle de conformité a été ajoutée à la console Configuration Manager pour vous permettre de spécifier si l’accès doit être autorisé ou refusé aux appareils en fonction de leur état d’intégrité.  Pour créer cette règle, ouvrez l’**Assistant Création de stratégies de conformité** et ajoutez une nouvelle règle.  Sélectionnez comme condition **Signalé comme ne posant aucun problème d’intégrité par le service HAS (Health Attestation Service)** pour la condition et affectez la valeur **True**.  Cette opération permet de garantir que seuls les appareils qui sont signalés comme étant en état d’intégrité auront accès aux ressources de votre entreprise. Pour plus d’informations sur le service d’attestation d’intégrité et sur la façon dont l’intégrité des appareils est signalée dans Intune, consultez [Attestation d’intégrité de l’appareil](#bkmk_devicehealth).  

-   **Nouveaux paramètres de stratégie de conformité :** les nouveaux paramètres de stratégie de conformité vous aident à améliorer la sécurité et la protection sur les appareils utilisés pour accéder aux services de messagerie d’entreprise et SharePoint :  

    -   **Exiger les mises à jour automatiques :** vous pouvez obliger les appareils dotés de Windows 8.1 ou version ultérieure à autoriser l’installation automatique des mises à jour, et spécifier la classe des mises à jour qui sont installées.  Vous pouvez choisir d’installer uniquement les mises à jour marquées comme importantes ou d’installer toutes les mises à jour recommandées.  

         Pour créer une règle pour les mises à jour automatiques, ouvrez l’**Assistant Création de stratégies de conformité** et ajoutez une nouvelle règle.  Sélectionnez **Classification minimale des mises à jour nécessaires** comme condition et définissez-la sur une des valeurs disponibles : **Aucun**, **Recommandé** et **Important**.  

        -   **Aucun :** les mises à jour logicielles ne sont pas installées automatiquement.  

        -   **Recommandé :** toutes les mises à jour recommandées sont installées  

        -   **Important :** seules les mises à jour classifiées comme importantes sont installées.  

    -   **Exiger un mot de passe pour déverrouiller des appareils mobiles :** Si ce paramètre est défini sur **Oui**, les utilisateurs finaux doivent entrer un mot de passe pour pouvoir accéder à leur appareil.  

         Pour créer une règle exigeant un mot de passe pour déverrouiller les appareils mobiles, ouvrez l’**Assistant Création de stratégies de conformité** et ajoutez une nouvelle règle. Sélectionnez **Exiger un mot de passe pour déverrouiller un appareil inactif** comme condition et définissez la valeur sur **True**.  

    -   **Minutes d’inactivité avant demande du mot de passe :**  Spécifie la durée d'inactivité au terme de laquelle l'utilisateur doit entrer à nouveau sont mot de passe.  

         Pour créer cette règle, ouvrez l’**Assistant Création de stratégies de conformité** et ajoutez une nouvelle règle. Sélectionnez **Minutes d’inactivité avant qu’un mot de passe soit demandé** comme condition et définissez la valeur sur l’une des options disponibles : 1 minute, 5 minutes, 15 minutes, 30 minutes et 1 heure.  

-   **Remplacer la règle par défaut : toujours autoriser les appareils inscrits et conformes à Intune à accéder à Exchange sur site :**  

     Quand vous activez cette option, les appareils inscrits dans Intune et conformes aux stratégies de conformité sont autorisés à accéder à Exchange sur site. Cette règle remplace la règle par défaut, ce qui signifie que même si vous définissez la règle par défaut de façon à mettre en quarantaine ou à bloquer l’accès, les appareils inscrits et conformes peuvent néanmoins toujours accéder à Exchange sur site.  
     Utilisez ce paramètre quand vous voulez que les appareils inscrits et conformes aient toujours accès à la messagerie via Exchange sur site.  

     Ceci est pris en charge sur les plateformes suivantes :  Windows Phone 8 et versions ultérieures, iOS 6 et versions ultérieures. Android 4.0 et ultérieur, Samsung Knox Standard 4.0 et ultérieur  

     Pour utiliser cette option, accédez à la page **Général** de l’**Assistant Configuration de la stratégie d’accès conditionnel** pour Exchange sur site.  

##  <a name="bkmk_clientStatus"></a> État de connexion du client  
Depuis la version d’évaluation technique 1601, vous pouvez identifier rapidement dans la console Configuration Manager si un client est en ligne ou hors connexion. Avec des icônes et des colonnes mises à jour dans les listes d’appareils de la console, vous pouvez évaluer l’état des clients dans votre environnement pour identifier les zones à problème et d’autres problèmes nécessitant votre attention.  

Un client est en ligne s’il est actuellement connecté à un rôle de système de site du point de gestion Configuration Manager. Tant que le point de gestion reçoit des messages de type test ping du client, son état est en ligne. Si la gestion ne reçoit pas de message pendant environ 5 minutes, l’état du client devient hors connexion.  

### <a name="icons-for-client-status"></a>Icônes d’état du client  

|||  
|-|-|  
|![icône de statut de connexion des clients](media/online-status-icon.png)|Le client est en ligne.|  
|![icône de statut déconnecté des clients](media/offline-status-icon.png)|Le client est hors connexion.|  
|![icône de statut inconnu des clients](media/unknown-status-icon.png)|L’état du client est inconnu.|  

### <a name="prerequisites"></a>Prérequis  
 L’état de connexion du client n’a pas de conditions préalables. Vous pouvez commencer à l’utiliser dès que la version d’évaluation technique 1601 de Configuration Manager est installée.  

### <a name="limitations"></a>Limitations  
 L’état de connexion du client est disponible seulement pour les ordinateurs Windows où le client Configuration Manager est installé. L’état de connexion du client n’est pas pris en charge pour les ordinateurs Mac, Linux ou UNIX, ni pour les appareils gérés à l’aide de la gestion des appareils mobiles sur site.  

### <a name="to-view-client-online-status"></a>Pour afficher l’état de connexion du client  

1. Dans la console Configuration Manager, accédez à **Ressources et Conformité > Vue d’ensemble > Appareils**.  

2. Cliquez avec le bouton droit dans l’en-tête de colonne, puis cliquez sur un des champs de l’état de connexion du client pour l’ajouter à la vue des appareils. Les champs sont :  

   -   **Statut de connexion de l’appareil** indique si le client est actuellement en ligne ou hors connexion.  

   -   **Heure de la dernière connexion** : indique quand l’état de connexion du client est passé de hors connexion à en ligne.  

   -   **Heure de la dernière déconnexion** : indique quand l’état de connexion du client est passé de en ligne à hors connexion.  

   Pour afficher les modifications récentes apportées à l’état du client, actualisez la console.  

##  <a name="bkmk_appmgmt1601"></a> Améliorations de la gestion d’applications  
 Dans la version Technical Preview 1601, nous avons ajouté la prise en charge des fonctionnalités suivantes :  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Gérer les applications pour appareils iOS achetées en volume  
 Certains magasins d’applications vous permettent d’acheter plusieurs licences pour une application que vous voulez utiliser dans votre entreprise. Vous pouvez ainsi réduire les coûts d’administration liés au suivi de plusieurs copies d’application achetées.  

 Configuration Manager vous aide maintenant à gérer les applications que vous avez achetées par le biais d’un programme de ce type, en important les informations de licence depuis le magasin d’applications et en effectuant le suivi du nombre de licences que vous avez utilisées.  

 Pour plus de détails, consultez [Gérer les applications que vous avez achetées par le biais d’un programme d’achat en volume avec Configuration Manager](https://technet.microsoft.com/library/mt627954.aspx).  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS : configuration d’applications pour les applications<br />Hybride  
 Certaines applications iOS prennent en charge les paramètres de préconfiguration, comme un serveur ou une base de données auquel l’application doit se connecter. Configuration Manager prend maintenant en charge le déploiement de stratégies de configuration d’applications sur l’appareil, ce qui permet à l’utilisateur d’utiliser l’application immédiatement sans avoir besoin de connaître ces informations. Les développeurs doivent activer cette fonctionnalité dans leurs applications.  

 Un nombre limité d’applications distribuées publiquement prennent actuellement en charge la préconfiguration des paramètres. Vous pouvez également disposer d’applications d’entreprise développées en interne et prenant en charge cette préconfiguration.  

#### <a name="prerequisites-for-this-scenario"></a>Conditions requises pour ce scénario  

-   Vous devez avoir ajouté un abonnement Microsoft Intune à Configuration Manager.  

-   Vous devez avoir ajouté un certificat APNs d’Apple valide à l’abonnement Intune.  

-   Vous devez avoir déployé une application iOS qui prend en charge la configuration d’applications.  

#### <a name="try-it-out"></a>Essayez !  
 Une fois que les conditions ci-dessus sont remplies, vous devez créer une application Configuration Manager qui utilise un type de déploiement iOS. L’application que vous utilisez doit prendre en charge la configuration d’applications. Reportez-vous à la documentation du fournisseur de l’application pour savoir quels éléments spécifiques (paires nom/valeur) vous pouvez configurer.  

 Ensuite, vous associez la stratégie de configuration d’applications avec le type de déploiement iOS lors du déploiement de l’application. Vous pouvez également déployer la stratégie à partir du nœud **Stratégies de configuration des applications**, ciblée vers une application et un regroupement existants.  

 Essayez d'exécuter les tâches suivantes, puis utilisez les informations fournies au début de cette rubrique pour nous dire si tout a fonctionné comme prévu :  

-   Si vous avez une application iOS qui prend en charge la configuration d’applications, consultez la documentation du fournisseur de l’application pour rechercher les paires nom/valeur que vous devez spécifier pour configurer l’application.  

-   Démarrez l’**Assistant Création d’une stratégie de configuration d’applications**. Dans la page **Stratégie iOS** de l’Assistant, essayez d’ajouter les paires nom/valeur trouvées dans la documentation du fournisseur de l’application. Vous pouvez aussi importer un fichier XML contenant les valeurs requises.  

-   Dans l’**Assistant Déploiement logiciel**, dans la page **Stratégie de configuration des applications**, associez la stratégie de configuration d’application que vous avez créée à un type de déploiement compatible de l’application.  

##  <a name="bkmk_compliance1601"></a> Améliorations apportées aux paramètres de conformité  
 Dans la version Technical Preview 1601, nous avons ajouté la prise en charge des fonctionnalités suivantes :  

### <a name="microsoft-edge-browser-settings"></a>Paramètres du navigateur Microsoft Edge  
 De nouveaux paramètres du navigateur Microsoft Edge ont été ajoutés à l’élément de configuration de **Windows 8.1 et Windows 10** (les paramètres s’appliquent seulement aux appareils Windows 10).  

 Pour afficher les nouveaux paramètres, choisissez **Microsoft Edge** dans la page **Paramètres de l’appareil** de l’élément de configuration de l’**Assistant Création d’élément de configuration**.  

 Pour plus d’informations, consultez [Comment créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Paramètres de conformité pour les appareils Windows 10 Collaboration  
 Utilisez ces nouveaux paramètres de conformité pour configurer les appareils qui exécutent Windows 10 Collaboration, comme des appareils Surface Hub.  

 Pour afficher les nouveaux paramètres, cliquez sur **Windows 10 Collaboration** dans la page **Paramètres de l’appareil** de l’élément de configuration de l’**Assistant Création d’élément de configuration**.  

 Pour plus d’informations, consultez [Comment créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android : mode plein écran pour Samsung KNOX Standard<br />Hybride  
 Le mode plein écran vous permet de verrouiller un appareil pour autoriser seulement certaines fonctionnalités. Par exemple, vous pouvez autoriser un appareil à exécuter seulement une application gérée que vous spécifiez ou vous pouvez désactiver les boutons de volume sur un appareil. Ces paramètres peuvent être utilisés pour un modèle de démonstration d'un appareil ou pour un appareil dédié à l'exécution d'une seule fonction, par exemple dans un point de vente. Ces paramètres ne sont pas disponibles pour les appareils Samsung KNOX Standard dans l’élément de configuration **Windows 8.1 et Windows 10** (les paramètres s’appliquent seulement aux appareils Windows 10).  

 Pour afficher les nouveaux paramètres, choisissez **Mode plein écran - Samsung KNOX** dans la page **Paramètres de l’appareil** de l’élément de configuration de l’**Assistant Création d’élément de configuration**.  

 Pour plus d’informations, consultez [Comment créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
