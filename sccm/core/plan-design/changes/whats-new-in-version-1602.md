---
title: Nouveautés dans la version 1602
titleSuffix: Configuration Manager
description: Obtenez des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1602 de System Center Configuration Manager.
ms.date: 12/30/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4021eca1-adfb-4e5a-adee-159263c29637
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 43a976e04358a176852d72301335b14cf484ed3c
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67158809"
---
# <a name="what39s-new-in-version-1602-of-system-center-configuration-manager"></a>Nouveautés dans la version 1602 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


La mise à jour 1602 pour System Center Configuration Manager est disponible seulement sous la forme d’une mise à jour dans la console pour les sites précédemment installés qui exécutent la version 1511. La version 1511 est la version de référence initiale qui permet d’installer de nouveaux sites Configuration Manager.  


> [!TIP]  
>  Informations supplémentaires :  
>   
>   -   [Installation de nouveaux sites](/sccm/core/servers/deploy/install/prepare-to-install-sites) (à l’aide d’une version de référence telle que 1511)  
>   -   [Installation de mises à jour sur les sites](/sccm/core/servers/manage/updates) (telles que la mise à jour 1602)  

 Les sections suivantes fournissent des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1602 de Configuration Manager.  

## <a name="site-infrastructure"></a>Infrastructure de site  

###  <a name="bkmk_UpgradeOS"></a> Mettre à niveau sur place le système d’exploitation de serveurs de site exécutant Windows Server 2008 R2  
 Les sites Configuration Manager exécutant la version 1602 ou ultérieure prennent en charge la mise à niveau sur place du système d’exploitation de serveurs de site de Windows Server 2008 R2 vers Windows Server 2012 R2.  

> [!WARNING]  
>  Avant de mettre à niveau vers Windows Server 2012 R2, vous devez désinstaller WSUS 3.2 du serveur.  
>   
>  Pour plus d’informations sur cette étape critique, consultez la section Fonctionnalités nouvelles et modifiées de [Vue d’ensemble des services WSUS (Windows Server Update Services)](https://technet.microsoft.com/library/hh852345.aspx) dans la documentation de Windows Server.  

 Pour mettre à niveau un serveur, utilisez les procédures de mise à niveau de Windows Server 2012 R2. Vous n’avez pas besoin d’effectuer une restauration du serveur de site Configuration Manager après la mise à niveau. Pour connaître les procédures de mise à niveau, consultez [Options de mise à niveau pour Windows Server 2012 R2](https://technet.microsoft.com/library/dn303416.aspx) dans la documentation de Windows Server.  

###  <a name="bkmk_AOAG"></a> Groupes de disponibilité SQL Server AlwaysOn  
 Utilisez des groupes de disponibilité SQL Server AlwaysOn pour héberger la base de données sur les sites principaux et le site d’administration centrale comme solution de haute disponibilité et de récupération d’urgence.  

 Pour plus d’informations, consultez [SQL Server AlwaysOn pour une base de données de site à haut niveau de disponibilité pour System Center Configuration Manager](../../../core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).  

## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation  

### <a name="windows-10-servicing"></a>Maintenance de Windows 10  
 Les améliorations suivantes pour la maintenance de Windows 10 ont été apportées à Configuration Manager version 1602 :  

-   De nouvelles options de filtre sont disponibles pour les plans de maintenance, qui vous permettent de filtrer les paramètres **Langue**, **Obligatoire** et **Titre**. Seules les mises à jour qui remplissent les critères spécifiés sont ajoutées au déploiement associé.  

-   Quand vous sélectionnez la classification **Mises à niveau** pour la synchronisation des mises à jour logicielles, un avertissement s’affiche. Cet avertissement vous indique que le [correctif 3095113](https://support.microsoft.com/kb/3095113) pour Windows Server Update Services (WSUS) 4.0 est nécessaire pour pouvoir synchroniser les mises à jour logicielles et pour que la maintenance de Windows 10 fonctionne correctement. À partir du message d’avertissement, vous pouvez accéder à l’article de la Base de connaissances associé.  

-   Les mises à niveau Windows 10 disponibles sont maintenant affichées uniquement dans le nœud **Maintenance de Windows 10** \ **Toutes les mises à jour Windows 10** de la console Configuration Manager. Ces mises à jour n’apparaissent plus dans le nœud **Mises à jour logicielles** \ **Toutes les mises à jour logicielles** de la console.  

-   Un plan de maintenance est considéré comme un déploiement à haut risque et la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements personnalisés répondant aux paramètres de vérification de déploiement configurés dans les propriétés du site. Pour plus d’informations, voir [Paramètres de gestion de déploiements à haut risque pour System Center Configuration Manager](../../../protect/understand/settings-to-manage-high-risk-deployments.md).  

-   Les utilisateurs qui démarrent un package de mise à niveau de Windows 10 reçoivent maintenant un message indiquant qu’ils vont mettre à niveau leur système d’exploitation.  

## <a name="application-management"></a>Gestion des applications  

### <a name="ios-app-configuration-policies"></a>Stratégies de configuration d’applications iOS  
 Utilisez des stratégies de configuration d’applications Configuration Manager pour fournir des paramètres pouvant être requis si l’utilisateur exécute une application iOS. Par exemple, une application peut demander à l’utilisateur de spécifier un numéro de port personnalisé, une langue, des paramètres de sécurité ou des paramètres de marque (comme un logo d’entreprise). Si ces paramètres ne sont pas entrés correctement, non seulement la charge du support technique peut être alourdie, mais l’adoption de nouvelles applications est également ralentie.  

 Les stratégies de configuration des applications peuvent vous aider à éliminer ces problèmes en vous permettant de déployer ces paramètres sur des utilisateurs dans une stratégie avant que ceux-ci exécutent l’application. Les paramètres sont ensuite fournis automatiquement, et l’utilisateur n’a aucune action à effectuer. Pour plus d’informations, consultez [Configurer des applications iOS avec des stratégies de configuration des applications dans System Center Configuration Manager](../../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  

### <a name="manage-volume-purchased-ios-apps"></a>Gérer les applications iOS achetées en volume  
 Configuration Manager peut vous aider à déployer et à gérer les applications que vous avez achetées en volume via le Programme d’achat en volume (VPP) Apple. Configuration Manager importe les informations de licence depuis le magasin d’applications et fait le suivi du nombre de licences que vous avez utilisées.  

 Pour plus d’informations, consultez [Gérer des applications iOS achetées en volume avec System Center Configuration Manager](../../../apps/deploy-use/manage-volume-purchased-ios-apps.md).  

### <a name="automatic-creation-of-office-mobile-apps"></a>Création automatique d’applications mobiles Office  
 Quand vous mettez à jour la version 1511 vers la version 1602, Configuration Manager crée automatiquement les applications mobiles Microsoft Office suivantes pour Android et iOS :  

-   Microsoft Word  

-   Microsoft Excel  

-   Microsoft PowerPoint  

-   Microsoft OneDrive  

-   Microsoft OneNote (iOS uniquement)  

-   Microsoft Outlook  

Vous trouverez ces applications dans le nœud **Applications** de la console Configuration Manager.  

 Pour plus d’informations sur le déploiement d’applications, consultez [Déployer des applications avec System Center Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

## <a name="software-updates"></a>Mises à jour logicielles  

### <a name="manage-office-365-client-updates"></a>Gérer les mises à jour de clients Office 365  
 System Center Configuration Manager peut désormais gérer les mises à jour des clients Office 365 à l’aide du flux de travail de gestion des mises à jour logicielles. Pour plus d’informations, consultez [Gérer les mises à jour d’Office 365 ProPlus avec System Center Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates).  

## <a name="compliance-settings"></a>Paramètres de conformité  

### <a name="compliance-settings-for-devices-running-windows-10-team"></a>Paramètres de conformité pour les appareils exécutant Windows 10 Collaboration  
 De nouveaux paramètres ont été ajoutés à l’élément de configuration **Windows 8.1 et Windows 10**. Ces paramètres vous permettent de contrôler les appareils exécutant Windows 10 Collaboration, comme un appareil Surface Hub.  

 Pour plus de détails, consultez [Comment créer des éléments de configuration pour des appareils Windows 8.1 et Windows 10 gérés sans le client System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="kiosk-mode-settings-for-android-samsung-knox-standard-devices"></a>Paramètres du mode plein écran pour les appareils Samsung KNOX Standard Android  
 Le mode plein écran vous permet de verrouiller un appareil de façon à ce que seules certaines fonctionnalités soient activées. Par exemple, vous pouvez autoriser un appareil à exécuter seulement une application gérée que vous spécifiez ou vous pouvez désactiver les boutons de volume sur un appareil. Ces paramètres peuvent être utilisés pour un modèle de démonstration d’un appareil ou pour un appareil dédié à l’exécution d’une seule fonction, par exemple un appareil pour un point de vente. Dans Configuration Manager, vous pouvez désormais spécifier les paramètres du mode plein écran pour des appareils Samsung KNOX Standard.  

 Pour plus d’informations, consultez [Guide pratique pour créer des éléments de configuration pour des appareils Android et Samsung KNOX Standard gérés sans le client System Center Configuration Manager](../../../compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client.md).  

## <a name="conditional-access"></a>Accès conditionnel  

### <a name="conditional-access-for-pcs-managed-by-system-center-configuration-manager"></a>Accès conditionnel pour les PC gérés par System Center Configuration Manager  
 Avant cette version, pour configurer un accès conditionnel pour un PC, celui-ci devait être inscrit dans Intune ou joint à un domaine. À partir de la mise à jour 1602, l’accès conditionnel pour les PC gérés par System Center Configuration manager est pris en charge. Pour les PC gérés par System Center Configuration Manager, vous pouvez restreindre l’accès à Exchange Online et à SharePoint Online aux seuls appareils conformes aux stratégies de conformité que vous définissez.  

 Pour plus d’informations, voir [Gérer l’accès aux services Office 365 des PC gérés par System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm.md).  

### <a name="restricting-access-based-on-the-health-of-devices"></a>Restriction des accès en fonction de l’intégrité des appareils  
 Vous pouvez désormais restreindre l’accès aux services de messagerie et Office 365 en fonction de l’intégrité des appareils, qui est indiquée par le service d’attestation d’intégrité. De plus, les périphériques gérés par Intune sont inclus dans les rapports d’intégrité des périphériques.  

 La console Configuration Manager a une nouvelle règle de conformité qui vous permet de spécifier si l’accès doit être autorisé ou refusé aux appareils en fonction de leur état d’intégrité. Pour plus d’informations sur le service d’attestation d’intégrité et la manière dont l’intégrité des appareils est indiquée dans Intune, consultez [Attestation d’intégrité pour System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="new-compliance-policy-rules"></a>Nouvelles règles de stratégie de conformité  
 De nouvelles règles de stratégie de conformité, comme les mises à jour automatiques et les mots de passe nécessaires pour déverrouiller des appareils, ont été ajoutées pour mieux prendre en charge les exigences de sécurité.

 Pour plus de détails, consultez [Gérer des stratégies de conformité d’appareils dans System Center Configuration Manager](../../../protect/deploy-use/device-compliance-policies.md).  

### <a name="make-sure-enrolled-and-compliant-devices-always-have-access-to-exchange-on-premises"></a>Vérifier que les appareils inscrits et conformes ont toujours accès à Exchange sur site  
 Quand vous activez l’option suivante, les appareils inscrits dans Intune et conformes aux stratégies de conformité sont autorisés à accéder à Exchange sur site : **Remplacer la règle par défaut : toujours autoriser les appareils inscrits et conformes à Intune à accéder à Exchange sur site :** Cette règle est disponible dans la page **Général** de l’**Assistant Configuration de la stratégie d’accès conditionnel** pour Exchange sur site.

 Cette règle remplace la règle par défaut, ce qui signifie que même si vous définissez la règle par défaut de façon à mettre en quarantaine ou à bloquer l’accès, les appareils inscrits et conformes peuvent néanmoins toujours accéder à Exchange sur site. Utilisez ce paramètre quand vous voulez que les périphériques inscrits et conformes aient toujours accès à la messagerie via Exchange sur site.   

 Pour la procédure détaillée, consultez [Gérer l’accès à la messagerie dans System Center Configuration Manager](../../../protect/deploy-use/manage-email-access.md).  

## <a name="client-management"></a>Gestion des clients  

### <a name="client-online-status"></a>État de connexion du client  
 Un nouvel état est disponible, qui permet aux clients de surveiller si un ordinateur est en ligne ou non. Un ordinateur est considéré comme étant en ligne s’il est connecté au point de gestion qui lui est affecté. Pour indiquer que l’ordinateur est en ligne, le client envoie des messages de type ping au point de gestion. Si le point de gestion n’a pas reçu de message après 5 minutes, le client est considéré comme étant hors connexion.  

 Pour plus de détails, consultez [Comment surveiller les clients dans System Center Configuration Manager](../../../core/clients/manage/monitor-clients.md).  

### <a name="refresh-pc-machine-and-user-policy-from-software-center"></a>Actualiser la stratégie ordinateur et utilisateur du PC à partir du Centre logiciel  
 Une nouvelle option, **Stratégie de synchronisation**, a été ajoutée à la page **Options** > **Maintenance de l’ordinateur** du Centre logiciel. Elle force le PC à actualiser sa stratégie ordinateur et utilisateur Configuration Manager.  

### <a name="software-center-branding-changes"></a>Modifications de la personnalisation du Centre logiciel  
 Vous pouvez modifier la couleur, le nom d’organisation et l’icône qui apparaissent dans le Centre logiciel. Ces paramètres sont appliqués selon les règles suivantes :  

- Si le rôle de serveur de site du point du site web du catalogue des applications n’est pas installé, le Centre logiciel affiche le nom d’organisation spécifié dans le paramètre client de l’**Agent ordinateur** appelé **Nom d’organisation affiché dans le Centre logiciel**.  

- Si le rôle de serveur site de point du site web du catalogue des applications est installé, le Centre logiciel affiche le nom d’organisation et la couleur spécifiés dans les propriétés du rôle de serveur de site du point du site web du catalogue des applications.  

- Si un abonnement Microsoft Intune est configuré et connecté à l’environnement Configuration Manager, le Centre logiciel affiche le nom d’organisation, la couleur et le logo de l’entreprise spécifiés dans les propriétés de l’abonnement Intune.  

### <a name="health-attestation"></a>Attestation d’intégrité  
 Les administrateurs peuvent consulter l’état de l’attestation d’intégrité des appareils Windows 10 dans la console Configuration Manager. Ceci est disponible pour Configuration Manager ainsi que pour Configuration Manager avec Microsoft Intune. L’attestation de l’intégrité des appareils permet à l’administrateur de s’assurer que les configurations dignes de confiance suivantes de BIOS, de module de plateforme sécurisée (TPM) et de logiciel de démarrage sont activées sur les ordinateurs clients :  

-   Logiciel anti-programme malveillant à lancement anticipé  

-   BitLocker  

-   Démarrage sécurisé  

-   Intégrité du code  

Pour plus d’informations, consultez [Attestation d’intégrité pour System Center Configuration Manager](../../../core/servers/manage/health-attestation.md).  

### <a name="improvements-to-endpoint-protection-antimalware-settings"></a>Améliorations apportées aux paramètres d’anti-programme malveillant d’Endpoint Protection  
 La mise à jour 1602 ajoute de nouveaux paramètres à la stratégie anti-programme malveillant d’Endpoint Protection pour Windows Defender :  

-   Protection en temps réel : bloquez les applications potentiellement indésirables au moment du téléchargement, avant l’installation.  

-   Paramètres d’analyse : analysez les lecteurs réseau mappés lors d’une analyse complète.  

-   Paramètres d’envoi automatique d’exemples de fichiers :  

     Le moteur du logiciel anti-programme malveillant peut demander à ce que des exemples de fichiers soient envoyés à Microsoft pour une analyse plus approfondie. Par défaut, il affiche toujours une invite avant d’envoyer ces exemples. Les administrateurs peuvent désormais gérer les paramètres suivants pour configurer ce comportement :  

    -   Avancé : activez l’envoi automatique d’échantillons de fichiers pour aider Microsoft à déterminer si certains éléments détectés sont malveillants.  

    -   Avancé : permettez aux utilisateurs de modifier les paramètres d’envoi automatique des échantillons de fichiers.  

    En outre, dans la section « Paramètres d’exclusions » de la stratégie de logiciel anti-programme malveillant d’Endpoint Protection, le paramètre **Exclure des fichiers et des dossiers** existant a été amélioré pour permettre les exclusions d’appareils.  

Pour plus de détails, consultez [Comment créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](../../../protect/deploy-use/endpoint-antimalware-policies.md).  

## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

### <a name="ios-activation-lock"></a>Verrou d’activation iOS  
 Configuration Manager peut vous aider à gérer le verrou d’activation iOS, fonctionnalité de l’application Rechercher mon iPhone pour les appareils iOS 7.1 et versions ultérieures. Le verrou d'activation est activé automatiquement quand l'application Rechercher mon iPhone est utilisée sur un appareil. Une fois qu’il est activé, l’ID et le mot de passe Apple de l’utilisateur doivent être entrés pour pouvoir :  

-   Désactiver Rechercher mon iPhone.  

-   Effacer l’appareil.  

-   Réactiver l’appareil.  

Configuration Manager peut demander l’état du verrou d’activation des appareils supervisés et non supervisés qui exécutent iOS 7.1 et versions ultérieures. Pour les appareils supervisés, Configuration Manager peut récupérer le code de contournement du verrou d’activation et l’envoyer directement à l’appareil.  

 Pour plus de détails, consultez [Aider à protéger les appareils iOS avec le contournement du verrou d’activation dans System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock).  

### <a name="monitor-terms-and-conditions-deployments"></a>Contrôler les déploiements de conditions générales  
 Vous pouvez surveiller les déploiements de conditions générales dans la console Configuration Manager.  

 Sélectionnez le déploiement des conditions générales dans la liste des déploiements. La zone récapitulative affiche les statistiques suivantes :  

-   **Conforme** : les utilisateurs ont accepté la dernière version des conditions générales.  

-   **Erreur**  

-   **Non conforme** : les utilisateurs ont accepté une version des conditions générales, mais pas la dernière.  

-   **Inconnu** : les utilisateurs n’ont jamais accepté les conditions générales, y compris celles concernant un appareil non inscrit.  
