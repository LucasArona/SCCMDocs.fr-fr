---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1705 pour System Center Configuration Manager.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33055f0962ef1220d41a2c8ee463cb2380ff60db
ms.sourcegitcommit: 7dd42b5a280e64feb69a947dae082fdaf1571272
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66715957"
---
# <a name="capabilities-in-technical-preview-1705-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1705 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version Technical Preview 1705 de System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version Technical Preview, passez en revue [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md) pour vous familiariser avec les conditions générales et les limitations d’utilisation d’une version Technical Preview, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités d’une version Technical Preview.    

**Problèmes connus dans cette version Technical Preview :**
-   **Le connecteur Operations Manager Suite ne se met pas à niveau**. Lorsque vous mettez à niveau à partir d’une version précédente de la Technical Preview qui avait le connecteur OMS configuré, ce connecteur n’est pas mis à niveau et n’est plus disponible dans la console. Après la mise à niveau, vous devez [utiliser l’assistant de services Azure](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) et rétablir la connexion à votre espace de travail OMS.
-   **Les pilotes Surface ne se synchronisent pas correctement**. Même si la prise en charge des pilotes Surface est répertoriée dans les **Nouveautés** dans la console Configuration Manager pour Technical Preview, cette fonctionnalité ne fonctionne pas encore comme prévu.
-   **Impossible de créer une stratégie de report Windows Update for Business**. Bien que la possibilité de configurer des stratégies de report Windows Update for Business est répertoriée dans les **Nouveautés** dans la console Configuration Manager pour Technical Preview, l’Assistant ne s’ouvre pas et vous ne parvenez pas à configurer des stratégies.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Outil de réinitialisation des mises à jour  
Vous pouvez utiliser l’outil de réinitialisation des mises à jour Configuration Manager, **CMUpdateReset.exe**, pour résoudre les problèmes lorsque des mises à jour dans la console ont des difficultés à télécharger ou à se répliquer. Cet outil est inclus dans la Technical Preview version 1705. Vous pouvez le trouver sur le serveur du site de votre Technical Preview après avoir installé la préversion dans le dossier ***\cd.latest\SMSSETUP\TOOLS***.

Vous pouvez utiliser cet outil avec les versions Technical Preview 1606 et ultérieures. Cette compatibilité descendante est proposée afin que l’outil puisse être utilisé dans différents scénarios de mise à jour de Technical Preview, sans devoir attendre la disponibilité de la Technical Preview suivante.

Vous pouvez utiliser cet outil lorsqu’une mise à jour dans la console n’a pas encore été installée et se trouve dans un état d’échec. Un état d’échec peut signifier que le téléchargement de la mise à jour est toujours en cours mais est bloqué et prend un temps extrêmement long, peut-être des heures de plus que pour les packages de taille similaire précédemment téléchargés. Il peut également s’agir d’un échec de réplication de la mise à jour sur les sites principaux enfants.  

Lorsque vous exécutez l’outil, il s’exécute sur la mise à jour que vous spécifiez. Par défaut, l’outil ne supprime pas les mises à jour installées ou téléchargées avec succès.  

### <a name="prerequisites"></a>Prérequis
Le compte que vous utilisez pour exécuter l’outil nécessite les autorisations suivantes :
-   Les autorisations en **Lecture** et **Écriture** pour la base de données de site du site d’administration centrale et chaque site principal de votre hiérarchie. Pour définir ces autorisations, vous pouvez ajouter le compte d’utilisateur en tant que membre des [rôles de base de données fixes](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** et **db_datareader** sur la base de données Configuration Manager de chaque site. L’outil n’interagit pas avec les sites secondaires.
-   **Administrateur local** sur le site de niveau supérieur de votre hiérarchie.
-   **L’administrateur local** sur l’ordinateur hébergeant le point de connexion de service.

Vous avez besoin du GUID du package de mise à jour que vous souhaitez réinitialiser. Pour obtenir le GUID :
-   Dans la console, accédez à **Administration** > **Mises à jour et maintenance** puis, dans le volet qui s’affiche, cliquez sur l’en-tête d’une des colonnes (comme **État**), puis sélectionnez **GUID du package**. Cette opération ajoute cette colonne à l’affichage, et la colonne présente le GUID du package de mise à jour.

> [!TIP]  
> Pour copier le GUID, sélectionnez la ligne pour le package de mise à jour que vous souhaitez réinitialiser, puis utilisez CTRL + C pour copier cette ligne. Si vous collez votre sélection copiée dans un éditeur de texte, vous pouvez ensuite copier uniquement le GUID pour une utilisation en tant que paramètre de ligne de commande lorsque vous exécutez l’outil.

### <a name="run-the-tool"></a>Exécution de l'outil    
L’outil doit être exécuté sur le site de niveau supérieur de la hiérarchie.

Lorsque vous exécutez l’outil, vous utilisez les paramètres de ligne de commande pour spécifier l’instance SQL Server sur le site de niveau supérieur de la hiérarchie, le nom de la base de données de site et le GUID du package de mise à jour que vous souhaitez réinitialiser. L’outil identifie les serveurs supplémentaires auxquels il doit accéder, en fonction de l’état des mises à jour.   

Si le package de mise à jour est dans un état *post-téléchargement*, l’outil ne nettoie pas le package. En option, vous pouvez forcer la suppression d’une mise à jour téléchargée avec succès à l’aide du paramètre de suppression de force (voir les paramètres de ligne de commande plus loin dans cette rubrique).

Une fois que l’outil s’exécute :
-   Si un package a été supprimé, redémarrez le service SMS_Executive des sites de niveau supérieur, puis vérifiez les mises à jour pour retélécharger le package.
-   Si un package n’a pas été supprimé, il est inutile d’entreprendre une action, car la mise à jour sera réinitialisée et redémarrera l’installation ou la réplication.

**Paramètres de ligne de commande :**  


|                        Paramètre                         |                                                            Description                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;Nom de domaine complet de l’instance SQL Server de votre site de niveau supérieur >** | *Obligatoire* <br> Vous devez spécifier le nom de domaine complet de l’instance SQL Server qui héberge la base de données de site pour le site de niveau supérieur de votre hiérarchie. |
|                **D - &lt;Nom de la base de données>**                 |                             *Obligatoire* <br> Vous devez spécifier le nom de la base de données des sites de niveau supérieur.                             |
|                 **-P &lt;GUID du package>**                 |                        *Obligatoire* <br> Vous devez spécifier le GUID pour le package de mise à jour que vous souhaitez réinitialiser.                        |
|           **-I &lt;Nom de l'instance SQL Server>**           |                   *Facultatif* <br> Utilisez cela pour identifier l’instance de SQL Server qui héberge la base de données du site.                   |
|                       **-FDELETE**                       |                      *Facultatif* <br> Permet de forcer la suppression d’un package de mise à jour téléchargé avec succès.                      |

 **Exemples :**  
 Dans un scénario classique, vous souhaitez réinitialiser une mise à jour qui présente des problèmes de téléchargement. Votre nom de domaine complet SQL Server est *server1.fabrikam.com*, la base de données du site est *CM_XYZ* et le GUID du package est *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Vous exécutez : ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 Dans un scénario plus extrême, vous souhaitez forcer la suppression du package de mise à jour problématique. Votre nom de domaine complet SQL Server est *server1.fabrikam.com*, la base de données du site est *CM_XYZ* et le GUID du package est *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Vous exécutez : ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Tester l’outil avec la version Technical Preview  
Vous pouvez utiliser cet outil avec les versions Technical Preview 1606 et ultérieures. Cette compatibilité descendante est proposée afin que l’outil puisse être utilisé dans de nombreux scénarios de mise à jour de Technical Preview, sans devoir attendre la disponibilité de la version Technical Preview suivante.

Exécutez l’outil sur un package de mise à jour pour une version Technical Preview avant la fin de la vérification de la configuration requise par la mise à jour. Un état de vérification terminée est identifié par l’un des états suivants pour le package dans **Administration** > **Mises à jour et maintenance** :  
-   **Vérification de configuration requise réussie**
-   **Vérification de configuration réussie avec avertissement**
-   **Échec de vérification de configuration requise**


## <a name="high-dpi-console-support"></a>Prise en charge des consoles à résolution élevée

Avec cette version, les problèmes liés à la façon dont la console Configuration Manager met à l’échelle et affiche les différentes parties de l’interface utilisateur lors de son affichage sur des appareils à résolution élevée (comme un livre) devraient être corrigés.


## <a name="peer-cache-improvements"></a>Améliorations de Cache d’homologue
À partir de cette version Technical Preview, le cache d’homologue [n’utilise plus le compte d’accès réseau](/sccm/core/plan-design/hierarchy/client-peer-cache) pour authentifier les demandes de téléchargement à partir d’homologues.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Améliorations pour les groupes de disponibilité Always On SQL Server  
Avec cette version, vous pouvez maintenant utiliser les réplicas avec validation asynchrone dans les groupes de disponibilité Always On SQL Server que vous utilisez avec Configuration Manager.  Cela signifie que vous pouvez ajouter des réplicas supplémentaires à vos groupes de disponibilité à utiliser en tant que sauvegardes hors site (à distance) puis de les utiliser dans un scénario de récupération d’urgence.  

- Configuration Manager prend en charge l’utilisation du réplica avec validation asynchrone pour récupérer votre réplica synchrone.  Consultez les [options de récupération de base de données de site](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption) dans la rubrique Sauvegarde et récupération pour plus d’informations sur la façon d’y parvenir.

- Cette version ne prend pas en charge le basculement pour utiliser le réplica avec validation asynchrone en tant que base de données de votre site.
  > [!CAUTION]  
  > Étant donné que Configuration Manager ne valide pas l’état du réplica avec validation asynchrone pour vérifier qu’il est à jour, et que, [par définition, un réplica de ce type peut être désynchronisé](https://msdn.microsoft.com/library/ff877884(SQL.120).aspx(d=robot)#Availability%20Modes), l’utilisation d’un réplica avec validation asynchrone comme base de données de site risque de compromettre l’intégrité de votre site et de ses données.  

- Vous pouvez utiliser les mêmes nombres et types de réplicas dans un groupe de disponibilité pris en charge par la version de SQL Server que vous utilisez.   (la prise en charge précédente était limitée à deux réplicas avec validation synchrone).

### <a name="configure-an-asynchronous-commit-replica"></a>Configurer un réplica avec validation asynchrone
Pour ajouter un réplica asynchrone à un [groupe de disponibilité que vous utilisez avec Configuration Manager](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database), vous n’avez pas besoin d’exécuter les scripts de configuration requis pour configurer un réplica synchrone. (en effet, il n’existe aucune prise en charge pour l’utilisation de ce réplica asynchrone en tant que base de données de site.) Consultez [la documentation de SQL Server](https://msdn.microsoft.com/library/hh213247(v=sql.120).aspx(d=robot)) pour plus d’informations sur l’ajout de réplicas secondaires aux groupes de disponibilité.

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Utiliser le réplica asynchrone pour récupérer votre site
Avant d’utiliser un réplica asynchrone pour récupérer la base de données de votre site, vous devez arrêter le site principal actif pour empêcher les écritures supplémentaires sur la base de données de site. Après avoir arrêté le site, vous pouvez utiliser un réplica asynchrone au lieu d’utiliser une [base de données récupérée manuellement](/sccm/protect/understand/backup-and-recovery#BKMK_SiteDatabaseRecoveryOption).

Pour arrêter le site, vous pouvez utiliser [l’outil de maintenance hiérarchique](/sccm/core/servers/manage/hierarchy-maintenance-tool-preinst.exe) pour arrêter les services principaux sur le serveur de site. Utilisez la ligne de commande : **Preinst.exe /stopsite**   

L’arrêt du site est équivalent à l’arrêt du service Gestionnaire de composants de site (sitecomp) suivi du service SMS_Executive sur le serveur de site.


## <a name="improved-user-notifications-for-office-365-updates"></a>Amélioration des notifications à l’utilisateur pour les mises à jour d’Office 365
Des améliorations ont été apportées pour tirer parti de l’expérience utilisateur « Cliquer pour exécuter » d’Office lorsqu’un client installe une mise à jour d’Office 365. Cela inclut des fenêtres contextuelles et des notifications dans l’application, ainsi qu’une expérience de compte à rebours. Avant cette version, lorsqu’une mise à jour Office 365 a été envoyée à un client, les applications Office qui étaient ouvertes ont été fermées automatiquement sans avertissement. Après cette mise à jour, les applications Office ne seront plus fermées inopinément.

### <a name="prerequisites"></a>Prérequis
Cette mise à jour s’applique aux clients Office 365 ProPlus.

### <a name="known-issues"></a>Problèmes connus
Lorsqu’un client évalue une attribution de mise à jour Office 365 pour la première fois et que la mise à jour a une échéance planifiée dans le passé, planifiée immédiatement ou planifiée dans les 30 minutes, l’expérience utilisateur Office 365 peut être incohérente. Par exemple, le client peut recevoir une boîte de dialogue de compte à rebours de 30 minutes pour la mise à jour, alors que son application réelle peut démarrer avant la fin du compte à rebours. Pour éviter ce problème, procédez comme suit :
- Déployez la mise à jour d’Office 365 avec une échéance planifiée plus de 60 minutes après l’heure actuelle.
- Configurez une fenêtre de maintenance pendant les heures creuses sur la collection, ou configurez une période de grâce d’application sur le déploiement.

### <a name="try-it-out"></a>Essayez !
Essayez d’effectuer les tâches suivantes, puis envoyez-nous vos **Commentaires** à partir de l’onglet **Accueil** du ruban pour nous dire comment cela a fonctionné pour vous :
- Sur un client, déployez une mise à jour d’Office 365 avec une échéance définie au moins 60 minutes après l’heure actuelle. Observez le nouveau comportement sur le client.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Configurer et déployer des stratégies Windows Defender Application Guard

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) est une nouvelle fonctionnalité de Windows qui permet de protéger vos utilisateurs en ouvrant les sites web non approuvés dans un conteneur isolé et sécurisé qui n’est pas accessible par les autres parties du système d’exploitation. Dans cette version Technical Preview, nous avons ajouté la prise en charge pour configurer cette fonctionnalité à l’aide des paramètres de conformité de Configuration Manager que vous configurez, puis déployez sur une collection.
Cette fonctionnalité sera disponible dans la préversion de la version 64 bits de mise à jour de Windows 10 Creators Update (nom de code : RS2). Pour tester cette fonctionnalité maintenant, vous devez utiliser une version préliminaire de cette mise à jour.


### <a name="before-you-start"></a>Avant de commencer

Pour créer et déployer des stratégies Windows Defender Application Guard, les appareils Windows 10 sur lesquels vous déployez la stratégie doivent être configurés avec une stratégie d’isolation de réseau. Pour plus d’informations, consultez le billet de blog référencé plus tard.
Cette fonctionnalité fonctionne uniquement avec les versions actuelles de Windows 10 Insider. Pour la tester, vos clients doivent exécuter une version récente de Windows 10 Insider.

### <a name="try-it-out"></a>Essayez !

Vous devez avoir lu le billet de blog pour comprendre les principes de base de Windows Defender Application Guard.

Pour créer une stratégie et pour parcourir les paramètres disponibles :

1.  Dans la console Configuration Manager, choisissez **Ressources et Conformité**.
2.  Dans l’espace de travail **Biens et conformité**, choisissez **Vue d’ensemble** > **Endpoint Protection** > **Windows Defender Application Guard**.
3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une stratégie Windows Defender Application Guard**.
4.  À l’aide du billet de blog comme référence, vous pouvez parcourir et configurer les paramètres disponibles pour tester la fonctionnalité.
5.  Lorsque vous avez terminé, terminez l’assistant et déployez la stratégie sur un ou plusieurs appareils Windows 10.

### <a name="further-reading"></a>Articles complémentaires

Pour en savoir plus sur Windows Defender Application Guard, consultez [ce billet de blog]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
En outre, pour en savoir plus sur le mode autonome de Windows Defender Application Guard, consultez [ce billet de blog](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Nouvelles fonctionnalités pour Azure AD et la gestion du cloud

Dans cette version, vous pouvez configurer les services cloud pour utiliser Azure AD afin de prendre en charge le scénario suivant :

- Installez manuellement le client Configuration Manager à partir d’internet et affectez-le à un site Configuration Manager.
- Utilisez Intune pour déployer le client Configuration Manager sur les appareils sur internet.

### <a name="advantages"></a>Avantages

L’utilisation des services cloud et d’Azure AD supprime la nécessité d’utiliser des certificats d’authentification client.

Vous pouvez découvrir les utilisateurs Azure AD dans votre site à utiliser dans des collections, et d’autres opérations de Configuration Manager.

### <a name="before-you-start"></a>Avant de commencer

- Vous devez disposer d’un client Azure AD.
- Vos appareils doivent exécuter Windows 10 et être joints à Azure AD.  Les clients peuvent également être joints à un domaine en plus d’Azure AD).
- Outre les [conditions préalables existantes](/sccm/core/plan-design/configs/site-and-site-system-prerequisites) pour le rôle système de site du point de gestion, vous devez vous assurer que l’option **ASP.NET 4.5** et les autres options automatiquement sélectionnées avec sont activées sur l’ordinateur qui héberge ce rôle de système de site.
- Pour utiliser Microsoft Intune pour déployer le client Configuration Manager :
    - Vous devez posséder un client Intune fonctionnel (Configuration Manager et Intune n’ont pas à être connectés).
    - Dans Intune, vous avez créé et déployé une application contenant le client Configuration Manager. Pour plus d’informations sur cette procédure, consultez le guide pratique pour installer des clients sur des appareils Windows gérés par la gestion MDM d’Intune.
- Pour utiliser Configuration Manager pour déployer le client :
    - Au moins un point de gestion doit être configuré pour le mode HTTPS.
    - Vous devez configurer une passerelle de gestion cloud.


### <a name="set-up-the-cloud-management-gateway"></a>Configuration de la passerelle de gestion cloud

Configurez la passerelle de gestion cloud pour permettre aux clients d’accéder à votre site Configuration Manager à partir d’Internet sans utiliser de certificats.

Vous trouverez de l’aide sur la procédure à suivre dans les rubriques suivantes :

- [Configurer la passerelle de gestion cloud dans Configuration Manager](/sccm/core/clients/manage/plan-cloud-management-gateway).
- [Configurer la passerelle de gestion cloud pour Configuration Manager](/sccm/core/clients/manage/setup-cloud-management-gateway).
- [Surveiller la passerelle de gestion cloud dans Configuration Manager](/sccm/core/clients/manage/monitor-clients-cloud-management-gateway).

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Configurer l’application de services Azure dans les services cloud de Configuration Manager

Cela connecte votre site Configuration Manager à Azure AD et est requis pour toutes les autres opérations de cette section. Pour cela :

1. Dans l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Services Azure**.
2. Sur l’onglet **Accueil**, sous le groupe **Services Azure**, cliquez sur **Configurer les services Azure**.
3. Sur la page **Services Azure** de l’assistant de services Azure, sélectionnez **Gestion cloud** pour permettre aux clients de s’authentifier auprès de la hiérarchie à l’aide d’Azure AD.
4. Sur la page **Général** de l’assistant, spécifiez un nom et une description pour votre service Azure.
5. Sur la page **Application** de l’assistant, sélectionnez votre environnement Azure dans la liste, puis cliquez sur **Parcourir** pour sélectionner les applications serveur et client qui permettent de configurer le service Azure :
   - Dans la fenêtre **Server App**, sélectionnez l’application serveur à utiliser, puis cliquez sur **OK**. Les applications serveur sont des applications web Azure qui contiennent les configurations pour votre compte Azure, notamment l’ID de locataire, l’ID de client et une clé secrète pour les clients. Si vous ne disposez pas d’une application serveur disponible, choisissez l’une des méthodes suivantes :
       - **Créer** : pour créer une application serveur, cliquez sur **Créer**. Fournissez un nom convivial pour l’application et le locataire. Une fois que vous êtes connecté à Azure, Configuration Manager crée l’application web dans Azure, notamment l’ID de client et la clé secrète à utiliser avec l’application web. Ces informations sont ensuite disponibles dans le portail Azure.
       - **Importer** : pour utiliser une application web qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Indiquez un nom convivial pour l’application et le locataire, puis spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir vérifié les informations, cliquez sur **OK** pour continuer. Cette option n’est actuellement pas disponible dans cette version Technical Preview.
   - Répétez le même processus pour l’application cliente.

   Vous devez accorder l’autorisation d’application *Lire des données d’annuaire* lors de l’importation de l’application, afin de définir les bonnes autorisations dans le portail. Si vous utilisez la création d’application, les autorisations sont automatiquement créées avec l’application, mais vous devez toujours donner votre consentement à l’application dans le portail Azure.
6. Sur la page **Découverte** de l’assistant, vous pouvez éventuellement **Activer la découverte d’utilisateurs Azure Active Directory**. Ensuite, cliquez sur **Paramètres**.
   Dans la boîte de dialogue **Paramètres de découverte d’utilisateurs Azure AD**, configurez une planification pour déterminer quand la détection survient. Vous pouvez également activer la découverte delta, qui vérifie uniquement les comptes nouveaux ou modifiés dans Azure AD.
7. Effectuez toutes les étapes de l'Assistant.

À ce stade, vous avez connecté votre site Configuration Manager à Azure AD.


### <a name="install-the-cm-client-from-the-internet"></a>Installation du client CM à partir d’Internet

Avant de commencer, assurez-vous que les fichiers sources d’installation client sont stockés localement sur l’appareil sur lequel vous souhaitez installer le client.
Ensuite, suivez les instructions de [Comment déployer des clients sur des ordinateurs Windows dans System Center Configuration Manager](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#a-namebkmkmanuala-how-to-install-clients-manually) en utilisant la ligne de commande d’installation suivante (remplacez les valeurs dans l’exemple par vos propres valeurs) :

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=<GUID> AADRESOURCEURI=<https://contososerver>**

- **/NoCrlCheck** : si votre point de gestion ou votre passerelle de gestion cloud utilise un certificat de serveur non public, le client peut ne pas être en mesure d’atteindre l’emplacement de la liste de révocation de certificats.
- **/Source** : Dossier local :   emplacement des fichiers d’installation du client.
- **CCMHOSTNAME** : nom de votre point de gestion Internet. Vous pouvez le trouver en exécutant **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** à partir d’une invite de commandes sur un client géré.
- **SMSMP** : nom de votre point de gestion de recherche : il peut s’agir de votre intranet.
- **SMSSiteCode** : code de site de votre site Configuration Manager.
- **AADTENANTID**, **AADTENANTNAME** : ID et nom du client Azure AD que vous avez lié à Configuration Manager. Vous pouvez les trouver en exécutant dsregcmd.exe /status à partir d’une invite de commandes sur un appareil à Azure AD.
- **AADCLIENTAPPID** : ID d’application cliente Azure AD. Pour vous aider à le trouver, consultez [Utiliser le portail pour créer une application Azure Active Directory et un principal de service pouvant accéder aux ressources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-create-service-principal-portal#get-application-id-and-authentication-key).
- **AADResourceUri** : URI de l’identificateur de l’application de serveur Azure AD intégré.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Utiliser l’assistant de services Azure pour configurer une connexion à OMS
À partir de la version de la version Technical Preview 1705, utilisez **l’assistant de services Azure** pour configurer votre connexion à partir de Configuration Manager pour le service cloud Operations Management Suite (OMS). L’assistant remplace les flux de travail précédents pour configurer cette connexion.

-   L’assistant est utilisé pour configurer les services cloud pour Configuration Manager, comme OMS, Windows Store pour Entreprises (WSfB) et Azure Active Directory (Azure AD).  

-   Configuration Manager se connecte à OMS pour des fonctionnalités comme [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) ou [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).

### <a name="prerequisites-for-the-oms-connector"></a>Conditions préalables pour le connecteur OMS
Les conditions préalables requises pour configurer une connexion à OMS sont identiques à celles [documentées pour la version de Current Branch 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). Ces informations sont répétées ici :  

-   Accorder l’autorisation Configuration Manager à OMS.

-   Le connecteur OMS doit être installé sur l’ordinateur qui héberge un [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) se trouvant en [mode en ligne](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

-   Vous devez installer un Microsoft Monitoring Agent pour OMS sur le point de connexion de service ainsi que le connecteur OMS. L’agent et le connecteur OMS doivent être configurés pour utiliser le même **espace de travail OMS**. Pour installer l’agent, consultez [Télécharger et installer l’agent](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) dans la documentation OMS.
-   Après avoir installé le connecteur et l’agent, vous devez configurer OMS pour utiliser les données Configuration Manager. Pour ce faire, dans le portail OMS, [importez des regroupements Configuration Manager](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Utilisez l’assistant de services Azure pour configurer la connexion à OMS

1.  Dans la console, accédez à **Administration** > **Présentation** > **Services cloud** > **Services Azure**, puis choisissez **Configurer les services Azure** à partir de l’onglet **Accueil** du ruban pour démarrer **l’Assistant Services Azure**.

2.  Sur la page **Services Azure**, sélectionnez le service cloud Operation Management Suite. Saisissez un nom convivial comme **Nom du service Azure** ainsi qu’une description facultative, puis cliquez sur **Suivant**.

3.  Sur la page **Application**, spécifiez votre environnement Azure (la version Technical Preview prend en charge uniquement le cloud public). Ensuite, cliquez sur **Parcourir** pour ouvrir la fenêtre de l’application serveur.

4.  Sélectionnez une application web :

    -   **Importer** : pour utiliser une application web qui existe déjà dans votre abonnement Azure, cliquez sur **Importer**. Indiquez un nom convivial pour l’application et le locataire, puis spécifiez l’ID de locataire, l’ID de client et la clé secrète de l’application web Azure que Configuration Manager doit utiliser. Après avoir **vérifié** les informations, cliquez sur **OK** pour continuer.   

    > [!NOTE]   
    > Lorsque vous configurez OMS avec cette version préliminaire, OMS ne prend en charge la fonction *Importer* pour une application web. La création d’une application web n’est pas prise en charge. De même, vous ne pouvez pas réutiliser une application existante pour OMS.

5.  Si vous avez suivi toutes les autres procédures avec succès, les informations sur l’écran **Configuration de la connexion OMS** s’affichent automatiquement sur cette page. Les informations pour les paramètres de connexion devraient s’afficher pour votre **Abonnement Azure**, votre **Groupe de ressources Azure** et votre **Espace de travail Operations Management Suite**.

6.  L’Assistant se connecte au service OMS en utilisant les informations que vous avez saisies. Sélectionnez les collections d’appareils que vous souhaitez synchroniser avec OMS, puis cliquez sur **Ajouter**.

7.  Vérifiez vos paramètres de connexion dans l’écran **Résumé**, puis sélectionnez **Suivant**. L’écran **Progression** indique l’état de connexion, puis **Terminé**.

8.  Une fois l’Assistant terminé, la console Configuration Manager indique que vous avez configuré **Operation Management Suite** comme **Type de service cloud**.
