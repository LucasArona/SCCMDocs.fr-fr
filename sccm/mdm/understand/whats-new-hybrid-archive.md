---
title: Archive des nouveautés de la gestion hybride des appareils mobiles
titleSuffix: Configuration Manager
description: Archive des précédentes fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Intune.
ms.date: 03/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 420026065caf619f51a5ebf84d7ae2f61a2248e1
ms.sourcegitcommit: ec4411fe30770f90128cf6cbd181047db90040cb
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/14/2019
ms.locfileid: "57881926"
---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>Précédentes fonctionnalités hybrides avec System Center Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les précédentes fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  

 Chaque section de cet article répertorie les fonctionnalités hybrides sous 3 catégories différentes. Utilisez les indications suivantes pour déterminer la compatibilité des fonctionnalités dans chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|
|-|  
|**Nouveautés de Microsoft Intune** : en général, toutes les fonctionnalités répertoriées dans cette catégorie doivent fonctionner avec toutes les versions de Configuration Manager, notamment les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités nécessitent uniquement le service Intune et pas de fonctionnalités supplémentaires dans Configuration Manager.<br /><br /> **Nouveautés de Configuration Manager Technical Preview** : toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version d’évaluation technique spécifiée. Pour tester ces fonctionnalités, vous devez installer la version d’évaluation technique spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md).<br /><br /> **Nouveautés de Configuration Manager (Current Branch)**  : toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch), telle que la version 1511 ou 1602. Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, vous devez effectuer la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|  



## <a name="april-2017"></a>Avril 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Mes apps disponible pour Managed Browser**  
  Mes apps Microsoft bénéficie à présent d’une meilleure prise en charge dans Managed Browser. Les utilisateurs Managed Browser qui ne sont pas ciblés pour la gestion sont directement redirigés vers le service Mes apps, où ils peuvent accéder à leurs applications SaaS configurées par l’administrateur. Les utilisateurs ciblés pour la gestion Intune peuvent toujours accéder à Mes apps à partir du signet Managed Browser intégré.

- **Nouvelles icônes pour Managed Browser et le portail d’entreprise**  
  Managed Browser reçoit des icônes mises à jour pour les versions iOS et Android de l’application. La nouvelle icône contient le badge Intune mis à jour qui devient plus cohérent avec les autres applications dans Enterprise Mobility + Security (EM+S). Vous pouvez voir la nouvelle icône Managed Browser dans la page sur les [nouveautés de l’interface utilisateur pour les applications Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

  Le portail d’entreprise reçoit également des icônes mises à jour pour les versions Android, iOS et Windows de l’application pour améliorer la cohérence avec les autres applications EM+S. Ces icônes seront disponibles progressivement sur les différentes plateformes, sur une période allant d’avril à fin mai.

- **Indicateur de progression de la connexion dans le portail d’entreprise Android**  
  Une mise à jour de l’application Portail d’entreprise Android affiche un indicateur de progression de la connexion lorsque l’utilisateur lance ou rouvre l’application. L’indicateur passe par différents états (en commençant par « Connexion en cours... », « Connexion en cours... », puis « Vérification des exigences de sécurité... ») avant d’autoriser l’utilisateur à accéder à l’application. Vous pouvez voir les nouveaux écrans de l’application Portail d’entreprise pour Android dans la page sur les [nouveautés de l’interface utilisateur pour les applications Intune](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Bloquer l’accès des applications à SharePoint Online**  
  Vous pouvez maintenant créer une stratégie d’accès conditionnel basée sur l’application pour empêcher les applications auxquelles aucune stratégie de protection d’application n’a été appliquée d’accéder à [SharePoint Online](https://docs.microsoft.com/intune-classic/deploy-use/mam-ca-for-sharepoint-online). Dans le cadre d’un scénario faisant appel à l’accès conditionnel basé sur l’application, vous pouvez spécifier les applications que vous souhaitez autoriser à accéder à SharePoint Online à l’aide du portail Azure.

### <a name="new-in-configuration-manager-technical-preview-1704"></a>Nouveautés de Configuration Manager Technical Preview 1704

- **Configurer des applications Android avec des stratégies de configuration des applications**  
  Vous pouvez utiliser des stratégies de configuration des applications disponibles dans Configuration Manager pour distribuer les paramètres préconfigurés quand un utilisateur exécute une application sur des appareils Android for Work. Les stratégies de configuration des applications Android sont disponibles uniquement sur les appareils Android for Work. Ces stratégies s’appliquent aux applications approuvées du magasin Play for Work. Pour plus d’informations, consultez [Configurer des applications Android avec des stratégies de configuration des applications](/sccm/core/get-started/capabilities-in-technical-preview-1704#configure-android-apps-with-app-configuration-policies).



## <a name="march-2017"></a>Mars 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Nouvelle expérience utilisateur pour l’application Portail d’entreprise pour Android**  
  L’application Portail d’entreprise pour Android a une interface utilisateur d’apparence plus moderne. Les mises à jour importantes sont :

  - Couleurs : En-têtes d’onglet portail entreprise sont colorés selon une personnalisation définie par l’informatique.
  - Applications : Dans le **applications** onglet, le **applications proposées** et **toutes les applications** boutons sont mis à jour.
  - Recherche : Dans le **applications** onglet, le **recherche** bouton est un bouton d’action flottant.
  - Navigation dans les applications : **Toutes les applications** vue affiche une vue comprenant les onglets **en vedette**, **tous les**, et **catégories** pour faciliter la navigation.
  - Prise en charge : **Mes appareils** et **contacter le service informatique** onglets sont mis à jour pour améliorer la lisibilité.

  Pour plus d’informations sur ces modifications, consultez [Mises à jour de l’interface utilisateur pour les applications Intune de l’utilisateur final](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Script de signature pour le portail d’entreprise Windows 10**  
  Si vous avez besoin de télécharger et charger de façon indépendante l’application Portail d’entreprise Windows 10, vous pouvez désormais utiliser un script pour simplifier et fluidifier le processus de signature des applications pour votre organisation. Pour télécharger le script et les instructions pour son utilisation, consultez [Script de signature Microsoft Intune pour le portail d’entreprise Windows 10](https://aka.ms/win10cpscript) sur la Galerie TechNet. Pour plus d’informations sur cette annonce, consultez [Mise à jour de votre application Portail d’entreprise Windows 10](https://blogs.technet.microsoft.com/intunesupport/2017/03/13/updating-your-windows-10-company-portal-app/) sur le Blog de l’équipe de support technique Intune.

- **Prise en charge améliorée pour les utilisateurs Android basés en Chine**  
  En raison de l’absence du Google Play Store en Chine, les appareils Android doivent obtenir des applications des places de marché chinoises. Le Portail d’entreprise prend en charge ce flux de travail. Il redirige les utilisateurs Android en Chine pour télécharger les applications Portail d’entreprise et Outlook à partir de Stores d’applications locaux. Ce comportement améliore l’expérience utilisateur quand les stratégies d’accès conditionnel sont activées, à la fois pour la gestion des appareils mobiles et pour la gestion des applications mobiles. Les applications Portail d’entreprise et Outlook pour Android sont disponibles sur les magasins d’applications chinois suivants :

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)

- **Vérifiez que vos applications de portail d’entreprise sont à jour**  
  En décembre 2016, nous avons publié une mise à jour qui permettait d’appliquer l’authentification multifacteur (MFA) sur un groupe d’utilisateurs lors de l’inscription d’un appareil iOS, Android, Windows 8.1+ ou Windows Phone 8.1+. Cette fonctionnalité ne peut pas être utilisée sans certaines versions de référence de l’application Portail d’entreprise pour Android (v5.0.3419.0+) et iOS (v2.1.17+).

  Les fonctionnalités de gestion d’Intune sont en constante évolution. De nombreuses améliorations ont nécessité des mises à jour des applications Portail d’entreprise sur toutes les plateformes prises en charge. Nous vous recommandons de conserver les dernières versions des applications Portail d’entreprise installées sur les appareils. Cette pratique tire parti des améliorations dans Intune et offre une expérience utilisateur optimale.

  >[!Tip]
  > Demandez à vos utilisateurs de configurer la mise à jour automatique des applications sur leurs appareils à partir de l’App Store approprié. Si vous avez rendu l’application Portail d’entreprise Android disponible sur un partage réseau, vous pouvez télécharger la dernière version à partir du [Centre de téléchargement Microsoft](https://www.microsoft.com/download/details.aspx?id=49140).

- **Microsoft Teams est maintenant activé pour la gestion des applications mobiles sur iOS et Android**  
  Les applications Microsoft Teams pour iOS et Android sont désormais activées avec les fonctionnalités de gestion des applications mobiles d’Intune. Permettez à vos équipes de travailler librement sur différents appareils, tout en garantissant que les conversations et les données d’entreprise sont protégées. Pour plus d’informations, consultez [l’annonce de Microsoft Teams](https://blogs.technet.microsoft.com/enterprisemobility/2017/03/14/microsoft-teams-is-now-generally-available-and-mam-enabled-on-ios-and-android/) sur le blog Enterprise Mobility and Security.

### <a name="new-in-configuration-manager-technical-preview-1703"></a>Nouveautés de Configuration Manager Technical Preview 1703

- **Prise en charge supplémentaire des scénarios du Programme d’achat en volume (VPP) Apple**  
   À compter de la version Technical Preview 1703, vous disposez de la prise en charge des scénarios VPP suivants :

   - Licences d’appareil : les applications prenant en charge les licences d’appareil et qui sont déployées sur des regroupements d’appareils ne nécessitent désormais qu’une seule licence par appareil. Auparavant, vous deviez utiliser une licence pour chaque utilisateur sur un appareil. Pour plus d’informations, consultez [Déployer des applications iOS achetées en volume sur des regroupements d’appareils](/sccm/core/get-started/capabilities-in-technical-preview-1703#deploy-volume-purchased-ios-apps-to-device-collections).
   - Utilisation de plusieurs jetons VPP pour un locataire hybride unique avec les deux jetons utilisés pour gérer les applications VPP.
   - Utilisation de jetons scolaires VPP avec la possibilité de faire la distinction entre les jetons d’entreprise et scolaires.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes étaient précédemment disponibles dans les versions Configuration Manager Technical Preview. Ces fonctionnalités sont désormais disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1702.

- [Prise en charge d’Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1702##android-for-work-support)
- [Paramètres de conformité des applications non conformes](/sccm/core/plan-design/changes/whats-new-in-version-1702#conditional-access-device-compliance-policy-improvements)
- [Création et distribution de certificats PFX et prise en charge de S/MIME](/sccm/core/plan-design/changes/whats-new-in-version-1702#improvements-to-certificate-profiles)
- [es versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride](/sccm/core/plan-design/changes/whats-new-in-version-1702#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm)

Les fonctionnalités hybrides supplémentaires suivantes sont également incluses dans la version 1702 de Configuration Manager (Current Branch) :

- **Prise en charge améliorée du Programme d’achat en volume Apple (VPP)**  
  - Vous pouvez désormais déployer des applications sous licence sur des appareils ainsi que des utilisateurs. En fonction de la capacité des applications à prendre en charge les licences d’appareils, une licence appropriée est réclamée lors du déploiement, comme suit :

    | Version de Configuration Manager | L’application prend-elle en charge les licences d’appareil ? | Type de regroupement de déploiement | Licence demandée |
    |-|-|-|-|
    |Antérieure à 1702|Oui|utilisateur|Licence utilisateur|
    |Antérieure à 1702|Non|utilisateur|Licence utilisateur|
    |Antérieure à 1702|Oui|Appareil|Licence utilisateur|
    |Antérieure à 1702|Non|Appareil|Licence utilisateur|
    |1702 et versions ultérieures|Oui|utilisateur|Licence utilisateur|
    |1702 et versions ultérieures|Non|utilisateur|Licence utilisateur|
    |1702 et versions ultérieures|Oui|Appareil|Licence d’appareil|
    |1702 et versions ultérieures|Non|Appareil|Licence utilisateur|

  - Désormais, vous pouvez également déployer et suivre les applications que vous avez achetées via le Programme d’achat en volume iOS pour l’éducation.

  - Vous pouvez maintenant associer plusieurs jetons de programme d’achat en volume Apple à Configuration Manager.

  Pour plus d’informations sur les applications achetées en volume, consultez [Gérer des applications iOS achetées en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

- **Prise en charge des applications métier dans le Microsoft Store pour Entreprises**  
  Vous pouvez désormais synchroniser des applications métier personnalisées à partir du Microsoft Store pour Entreprises.

- **Nouveaux outils de surveillance de protection contre les menaces mobiles**  
    Vous disposez maintenant de nouveaux moyens pour surveiller l’état de conformité avec votre fournisseur de services de protection contre les menaces mobiles.

    Pour plus d’informations, consultez [Comment surveiller la conformité de la protection contre les menaces mobiles](/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).





## <a name="february-2017"></a>Février 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Modernisation du site web du portail d’entreprise**

  Le site web du portail d’entreprise prend en charge les applications destinées aux utilisateurs ne disposant pas d’appareils gérés. Le site web s’aligne sur les autres produits et services Microsoft grâce à un nouveau jeu de couleurs contrastées, des illustrations dynamiques et un « menu hamburger » qui fournit les coordonnées du support technique et des informations sur les appareils gérés existants. La nouvelle page d’accueil réorganisée met en évidence les applications disponibles aux utilisateurs, avec des tapis roulants pour les applications proposées et les applications récemment mises à jour. Vous pouvez trouver des images antérieures et postérieures sur la page [Mises à jour de l’interface utilisateur](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nouvelle adresse du serveur MDM pour les appareils Windows**

  L’adresse du serveur MDM utilisée pour inscrire des appareils Windows et Windows Phone est maintenant enrollment.manage.microsoft.com (au lieu de manage.microsoft.com ). Demandez à votre utilisateur d’employer enrollment.manage.microsoft.com comme adresse du serveur MDM, lors de l’inscription d’un appareil Windows ou Windows Phone. Cette mise à jour requiert également le remplacement d’un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers manage.microsoft.com, par un enregistrement CNAME DNS qui redirige EnterpriseEnrollment.contoso.com vers EnterpriseEnrollment-s.manage.microsoft.com. Pour plus d’informations sur ce changement, consultez http://aka.ms/intuneenrollsvrchange.

### <a name="new-in-configuration-manager-technical-preview-1702"></a>Nouveautés de Configuration Manager Technical Preview 1702

- **Prise en charge d’Android for Work**

  Vous pouvez désormais gérer les appareils Android à l’aide d’Android for Work dans les environnements de gestion des appareils mobiles hybrides à l’aide de Configuration Manager Technical Preview 1702. Les appareils Android pris en charge peuvent maintenant être inscrits comme appareils Android for Work, ce qui crée un profil professionnel sur l’appareil sur lequel les applications approuvées dans Play for Work peuvent être déployées. Vous pouvez également configurer et déployer des éléments de configuration, des stratégies de conformité et des profils d’accès aux ressources pour ces appareils. Pour plus d’informations, consultez [Prise en charge d’Android for Work](/sccm/core/get-started/capabilities-in-technical-preview-1702#android-for-work-support).

- **Paramètres de conformité des applications non conformes**

  Vous pouvez maintenant créer des règles d’applications non conformes pour les applications Android et iOS dans les stratégies de conformité. Si des appareils disposent des applications spécifiées, ils sont marqués comme « non conformes » et perdent l’accès aux ressources d’entreprise en fonction des stratégies d’accès conditionnel en place. Pour plus d’informations, consultez [Améliorations apportées aux stratégies de conformité des appareils pour l’accès conditionnel](/sccm/core/get-started/capabilities-in-technical-preview-1702#conditional-access-device-compliance-policy-improvements).

- **Création et distribution de certificats PFX et prise en charge de S/MIME**

  Vous pouvez désormais créer et déployer des certificats PFX sur les utilisateurs dans un environnement hybride. Ces certificats peuvent ensuite être utilisés pour le chiffrement et le déchiffrement S/MIME par les appareils que l’utilisateur a inscrits. Pour plus d’informations, consultez [Créer des certificats PFX avec prise en charge S/MIME](/sccm/core/get-started/capabilities-in-technical-preview-1702#create-pfx-certificates-with-s-mime-support).

- **Prise en charge des paramètres de configuration supplémentaires iOS**
   
    Vous disposez désormais de 42 paramètres iOS supplémentaires que vous pouvez configurer dans le cadre d’un élément de configuration. La plupart des paramètres (35 au total) ont été ajoutés pour les appareils iOS supervisés. Pour plus d’informations, consultez [Nouveaux paramètres de conformité pour les appareils iOS](/sccm/core/get-started/capabilities-in-technical-preview-1702#new-compliance-settings-for-ios-devices).



## <a name="january-2017"></a>Janvier 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Prise en charge d'Android 7.1.1**

  Intune prend désormais en charge entièrement et gère Android 7.1.1.

- **Résoudre les problèmes dans lesquels des appareils iOS sont inactifs ou la console d’administration ne peut pas communiquer avec eux**

  Lorsque les appareils des utilisateurs perdent le contact avec Intune, vous pouvez utiliser les nouvelles étapes de dépannage pour les aider à récupérer l’accès aux ressources d’entreprise. Voir [Résoudre les problèmes dans lesquels des appareils iOS sont inactifs ou la console d’administration ne peut pas communiquer avec eux](https://docs.microsoft.com/intune/troubleshoot/troubleshoot-device-enrollment-in-intune#devices-are-inactive-or-the-admin-console-cannot-communicate-with-them).

### <a name="new-in-configuration-manager-technical-preview-1701"></a>Nouveautés de Configuration Manager Technical Preview 1701

- **es versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride**

  Depuis Technical Preview 1701, vous n’avez plus besoin de cibler des versions Android et iOS spécifiques quand vous créez des stratégies et des profils pour des appareils gérés par Intune dans le cadre d’une gestion des appareils mobiles (MDM) hybride. Grâce à cette modification, les déploiements hybrides peuvent prendre en charge plus rapidement les nouvelles versions Android et iOS sans avoir besoin d’une nouvelle version de Configuration Manager ou d’une extension. Pour en savoir plus, consultez [Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création](/sccm/core/get-started/capabilities-in-technical-preview-1701#android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm).



## <a name="december-2016"></a>Décembre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **L’authentification multifacteur sur l’inscription est déplacée dans le portail Azure**

  Auparavant, vous deviez accéder à la console Intune ou à la console Configuration Manager pour définir l’authentification multifacteur pour les inscriptions Intune. Avec cette fonctionnalité de mise à jour, vous vous connectez maintenant à la [portail Microsoft Azure](https://manage.windowsazure.com) à l’aide de vos informations d’identification Intune et configurer les paramètres d’authentification Multifacteur via Azure AD. Pour en savoir plus, voir [Authentification multifacteur pour les inscriptions d’appareils Intune](https://aka.ms/mfa_ad).

- **Application Portail d’entreprise pour Android maintenant disponible en Chine**

  L’application Portail d’entreprise pour Android est maintenant disponible en Chine. En raison de l’absence de Google Play Store en Chine, les appareils Android doivent obtenir les applications des places de marché d’applications chinoises. L’application Portail d’entreprise pour Android est disponible pour téléchargement sur les magasins suivants :

  - [Baidu](https://go.microsoft.com/fwlink/?linkid=836946)
  - [Huawei](https://go.microsoft.com/fwlink/?linkid=836948)
  - [Tencent](https://go.microsoft.com/fwlink/?linkid=836949)
  - [Wandoujia](https://go.microsoft.com/fwlink/?linkid=836950)
  - [Xiaomi](https://go.microsoft.com/fwlink/?linkid=836947)

  L’application Portail d’entreprise pour Android utilise Google Play Services pour communiquer avec le service Microsoft Intune. Comme Google Play Services n’est pas encore disponible en Chine, la réalisation des tâches suivantes peut prendre jusqu’à 8 heures.

  | Configuration de la console d’administration de Configuration Manager | Application Portail d’entreprise Intune pour Android | Site web du portail d’entreprise Intune |
  |----|----|----|      
  | Mettre hors service/réinitialiser (supprimer toutes les données)   | Supprimer un appareil distant | Supprimer un appareil (local et distant) |
  | Mettre hors service/réinitialiser (supprimer les données d’entreprise)   | Réinitialiser un appareil | Réinitialiser un appareil|
  | Déploiements d’applications nouvelles ou mises à jour | Installer des applications métier disponibles | Réinitialisation du code secret d’un appareil|
  | Verrouillage à distance | | |
  | Réinitialiser le code secret | | |        


## <a name="november-2016"></a>Novembre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Nouveau portail d’entreprise Microsoft Intune disponible pour les appareils Windows 10**

  Microsoft a publié une nouvelle [application Portail d’entreprise pour les appareils Windows 10](https://www.microsoft.com/store/apps/9wzdncrfj3pz). Cette application, qui tire parti du nouveau format Windows 10 universel, fournit une nouvelle expérience utilisateur qui est identique sur tous les appareils Windows 10, qu’il s’agisse de PC ou de mobiles, tout en offrant exactement les mêmes fonctionnalités que celles fournies par les applications Portail d’entreprise précédentes.

  La nouvelle application tire parti des fonctionnalités de la plateforme, comme l’authentification unique (SSO) et l’authentification basée sur les certificats sur les appareils Windows 10. L’application est disponible auprès du Windows Store en tant que mise à niveau des installations existantes de portail d’entreprise Windows 8.1 et de portail d’entreprise Windows Phone 8.1. Pour plus d’informations, consultez le [blog de l’équipe de support Intune](http://aka.ms/intunecp_universalapp).

  La nouvelle application Portail d’entreprise affiche également toutes les applications du Windows Store pour Entreprises marquées comme étant **disponibles** dans la console Configuration Manager.


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes qui étaient précédemment disponibles dans les versions Configuration Manager Technical Preview sont maintenant disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1610.

* [Paramètres supplémentaires et expérience améliorée pour les éléments de configuration](/sccm/core/plan-design/changes/whats-new-in-version-1610#new-compliance-settings-for-configuration-items)
* [Paramètres supplémentaires pour les profils DEP](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Applications payantes dans le Windows Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business)
* [Types de connexion natifs pour les profils VPN Windows 10](whats-new-hybrid-archive.md#new-in-configuration-manager-technical-preview-1609)
* [Graphiques de conformité Intune](/sccm/protect/deploy-use/create-compliance-policy#monitor-the-compliance-policy)
* [Demande de synchronisation de stratégie à partir de la console](/sccm/mdm/deploy-use/sync-intune-device)
* [Paramètres de configuration de Windows Defender](/sccm/compliance/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client#windows-defender)

Les fonctionnalités hybrides supplémentaires suivantes sont également incluses dans la version 1610 de Configuration Manager (Current Branch) :

- **Nombre accru d’appareils inscrits**

  Vous pouvez maintenant permettre aux utilisateurs d’inscrire jusqu’à 15 appareils. La limite précédente était de 5 appareils par utilisateur.


- **Prise en charge supplémentaire de la sécurité**

  En plus d’Administrateur complet, les rôles de sécurité intégrés suivants ont maintenant un accès complet aux éléments dans le nœud Appareils d’entreprise, notamment Appareils prédéclarés, Profils d’inscription iOS et Profils d’inscription Windows :

    - Gestionnaire de ressources
    - Gestionnaire d’accès aux ressources de l’entreprise

  L’accès en lecture seule à ces zones de la console Configuration Manager est toujours accordé au rôle Analyste en lecture seule.

- **Accès VPN à déclenchement automatique à partir d’applications de protection des informations Windows**

  Vous pouvez ajouter un domaine principal de protection des informations Windows aux profils VPN de Windows 10 qui provoque le déclenchement automatique d’une connexion VPN par les applications associées quand elles sont exécutées sur l’appareil. Cette option est disponible seulement quand vous choisissez un type de connexion natif.

- **Accès conditionnel pour les profils VPN Windows 10**

    Vous pouvez maintenant exiger que les appareils Windows 10 inscrits dans Azure Active Directory soient conformes pour pouvoir avoir un accès VPN via les profils VPN Windows 10 créés dans la console Configuration Manager. Ceci est possible via la nouvelle case à cocher **Activer l’accès conditionnel pour cette connexion VPN** dans la page Méthode d’authentification de l’Assistant Profil VPN et les propriétés de profil VPN pour les profils VPN Windows 10. Cette option est disponible seulement quand vous choisissez un type de connexion natif.

    Vous pouvez également spécifier un certificat distinct pour l’authentification unique si vous activez l’accès conditionnel pour le profil.

## <a name="october-2016"></a>Octobre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en octobre 2016 fonctionnent dans les déploiements hybrides.

- **Accès conditionnel pour la gestion des applications mobiles**

  Vous pouvez restreindre l’accès à Exchange Online afin que l’accès soit fourni uniquement à partir d’applications qui prennent en charge les stratégies de gestion des applications mobiles Intune, telles qu’Outlook. [Cette nouvelle fonctionnalité](/intune/deploy-use/allow-policy-managed-apps-access-to-o365) s’associe parfaitement aux stratégies de gestion des applications mobiles (GAM) Intune, car vous pouvez bloquer l’accès aux clients de messagerie intégrés ou à d’autres applications qui n’ont pas été configurées avec les stratégies GAM Intune. Cela garantit que vos utilisateurs accèdent aux données de votre organisation avec des applications qui peuvent être protégées à l’aide de la GAM Intune. Vous pouvez bien démarrer avec la gestion des applications mobiles Intune à l’aide du portail Azure. Recherchez la nouvelle section Accès conditionnel dans le panneau « Paramètres ».

- **Outil de création de package de restrictions d’application Intune pour Android**

  Vous pouvez activer vos applications pour utiliser les stratégies de gestion des applications mobiles (MAM) Intune à l’aide de l’outil de création de package de restrictions d’application Intune.

- **Compatibilité d’Android Samsung KNOX Standard avec Intune**

  Certains modèles de téléphone Samsung Galaxy Ace ne peuvent pas être gérés par Intune comme les appareils Samsung KNOX Standard. Quand vous inscrivez ces appareils auprès d’Intune, ils sont gérés comme des appareils Android standard.

  Les numéros de modèle concernés sont les suivants :

  - SM-G313HU
  - SM-G313HY
  - SM-G313M
  - SM-G313MY
  - SM-G313U

  Vous et vos utilisateurs finaux n’avez aucune action supplémentaire à effectuer. Pour plus d’informations, visitez le site web de Samsung KNOX.

### <a name="new-in-configuration-manager-technical-preview-1610"></a>Nouveautés de Configuration Manager Technical Preview 1610

Les nouvelles fonctionnalités hybrides suivantes ont été introduites en octobre 2016 pour Configuration Manager Technical Preview 1610.

- **Demander une synchronisation de la stratégie à partir de la console d’administration**

  Vous pouvez demander une synchronisation de la stratégie sur un appareil mobile inscrit à partir de la console Configuration Manager, au lieu d’avoir à demander la synchronisation dans l’application Portail d’entreprise sur l’appareil lui-même. Il s’agit d’une nouvelle action appelée **Envoyer une demande de synchronisation** dans le menu Actions de l’appareil à distance, qui s’affiche dans le ruban quand un appareil mobile est sélectionné dans le nœud Périphériques.

- **Paramètres de configuration de Windows Defender**

  Vous pouvez maintenant configurer les paramètres du client Windows Defender sur des ordinateurs Windows 10 inscrits auprès d’Intune à l’aide d’éléments de configuration de la console Configuration Manager. Il existe un nouveau groupe de paramètres nommé **Windows Defender** dans l’Assistant Nouvel élément de configuration. Notez que ces paramètres sont pris en charge uniquement sur Windows 10 version 1511 et versions ultérieures.


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Aucune nouvelle fonctionnalité hybride n’a été introduite en août 2016 pour Configuration Manager (Current Branch).

## <a name="september-2016"></a>Septembre 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en septembre 2016 fonctionnent dans les déploiements hybrides.

- **Ajout de « Notifications » au portail d’entreprise pour Android**

  Une nouvelle icône Notifications a été ajoutée sur la page d’accueil du portail d’entreprise pour Android. Appuyez sur cette icône pour accéder à la page Notifications, ce qui affiche à vos utilisateurs finaux tous les éléments qui nécessitent votre attention dans l’application Portail d’entreprise, comme la non-conformité de l’appareil, la mise à jour de l’inscription et l’activation de l’inscription. L’application Portail d’entreprise iOS bénéficie déjà de cette expérience de notifications. Grâce à cette nouvelle page Notifications, la page Configuration de l’accès à l’entreprise ne s’affichera plus à l’utilisateur chaque fois qu’il lancera ou reprendra le portail d’entreprise tant que l’appareil est déjà inscrit. Si vous créez votre propre aide pour les utilisateurs finaux, vous pouvez mettre à jour votre documentation pour refléter cette modification. Des captures d’écran mises à jour sont disponibles [ici](https://aka.ms/androidcpupdate).

- **Modifications en termes de prise en charge de l’application Portail d’entreprise iOS**

  Tous les utilisateurs de l’application Portail d’entreprise Microsoft Intune pour iOS sont maintenant tenus d’utiliser sa version la plus récente. Les nouveaux utilisateurs ne peuvent télécharger que la dernière version, et les utilisateurs actuels sont tenus d’effectuer une mise à jour vers celle-ci. La dernière version exige iOS 8.0 ou une version ultérieure. Par conséquent, les appareils exécutant des versions d’iOS plus anciennes ne peuvent pas utiliser le portail d’entreprise ou s’inscrire tant qu’ils n’ont pas effectué une mise à jour de leur appareil vers iOS 8.0 ou une version ultérieure, puis une mise à jour de l’application Portail d’entreprise vers la dernière version. Les appareils inscrits qui exécutent des versions antérieures à iOS 8.0 continueront à être gérés et répertoriés dans la console d’administration Intune.

- **Bouton d’envoi de commentaires ajouté à l’application Portail d’entreprise Windows Phone 8.1**

  L’application Portail d’entreprise Windows Phone 8.1 permet aux utilisateurs finaux d’envoyer des commentaires concernant l’application à l’aide d’un nouveau bouton « Envoyer des commentaires ». Pour trouver ce bouton, les utilisateurs appuient sur le menu « points de suspension » situé en bas à droite de l’écran de l’application Portail d’entreprise, puis sélectionnent **Envoyer des commentaires**. Les commentaires collectés anonymement permettent à Microsoft d’améliorer l’expérience d’application Portail d’entreprise des utilisateurs.

### <a name="new-in-configuration-manager-technical-preview-1609"></a>Nouveautés de Configuration Manager Technical Preview 1609

Les nouvelles fonctionnalités hybrides suivantes ont été introduites en septembre 2016 pour Configuration Manager Technical Preview 1609.

- **Paramètres supplémentaires et expérience améliorée pour les paramètres d’élément de configuration**

  De nouveaux paramètres ont été ajoutés pour Android, iOS et Windows, et seuls les paramètres qui s’appliquent aux plateformes que vous sélectionnez dans la page Plateformes prises en charge s’affichent dans l’Assistant. Pour plus d’informations, consultez [Nouveaux paramètres de compatibilité pour les éléments de configuration dans TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#new-compliance-settings-for-configuration-items).

- **Paramètres supplémentaires pour les profils DEP**

  TouchID, ApplePay et Zoom ont été ajoutés en tant que paramètres configurables dans les profils DEP pour les appareils iOS.

- **Applications payantes dans le Windows Store pour Entreprises**

  Vous pouvez maintenant ajouter des applications payantes et des applications gratuites au Windows Store pour Entreprises, et les déployer auprès des utilisateurs de votre organisation. Pour plus d’informations, consultez [Améliorations apportées au Windows Store pour Entreprises dans TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#enhancements-to-windows-store-for-business-integration-with-configuration-manager).

- **Types de connexion natifs pour les profils VPN Windows 10**

  Vous pouvez maintenant créer des profils VPN Windows 10 pour la gestion des appareils mobiles avec des types de connexion Microsoft Automatic, IKEv2 et PPTP dans la console Configuration Manager sans utiliser de paramètre OMA-URI.

- **Graphiques de conformité Intune**

  Vous pouvez obtenir un aperçu rapide de la compatibilité globale des appareils et les principales raisons de non-compatibilité à l’aide de nouveaux graphiques sous l’espace de travail Analyse. Pour plus d’informations, consultez [Graphiques de conformité Intune dans TP 1609](/sccm/core/get-started/capabilities-in-technical-preview-1609#intune-compliance-charts).

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

La nouvelle fonctionnalité suivante introduite en septembre 2016 est disponible dans les déploiements hybrides avec Microsoft Intune et Configuration Manager version 1606 (Current Branch).

- **Prise en charge d’iOS 10**

  Si vous avez des profils ou des éléments de configuration destinés à toutes les plateformes iOS, ils feront également l’objet d’un push vers iOS 10. Nous avons également publié une mise à jour vers Configuration Manager version 1606 qui vous permet de cibler des profils et des éléments de configuration sur des plateformes iOS individuelles, notamment iOS 10. Vous pouvez installer la mise à jour avec la console d’administration Configuration Manager dans **Administration > Vue d’ensemble > Services cloud > Mises à jour et maintenance**. Vous pouvez obtenir plus d’informations sur cette mise jour sur [http://support.microsoft.com/kb/3192616](http://support.microsoft.com/kb/3192616).

## <a name="august-2016"></a>Août 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en août 2016 fonctionnent dans les déploiements hybrides.

- **Prise en charge d’Android 7 dans l’application Portail d’entreprise**

  L’application Portail d’entreprise Intune pour Android fournit une prise en charge au « jour 0 » pour le prochain système d’exploitation Android 7.0 pour les appareils mobiles.

- **Suppression, par Google, de la capacité de réinitialisation à distance des codes secrets sur les appareils Android 7.0**

  Google supprime la possibilité, pour les utilisateurs finaux et les administrateurs informatiques, de réinitialiser à distance le code secret des appareils Android 7.0. Auparavant, les administrateurs informatiques pouvaient réinitialiser à distance le code secret d’un utilisateur, et les utilisateurs finaux pouvaient réinitialiser leurs codes secrets à partir du site web du portail d’entreprise.

- **Stratégie d’applications autorisées et bloquées pour les appareils Samsung KNOX Standard**

  Vous pouvez maintenant configurer une stratégie personnalisée pour les appareils Samsung KNOX Standard qui vous permet de créer un des éléments suivants :

  - Une liste d’applications dont l’exécution sur l’appareil est bloquée. Même si elle est installée, une application définie dans la liste bloquée ne peut pas être activée sur l’appareil.
  - Une liste d’applications que les utilisateurs de l’appareil sont autorisés à installer à partir de Google Play Store. Aucune autre application ne peut être installée à partir du Store.

  Ces paramètres peuvent être utilisés seulement par des appareils qui exécutent Samsung KNOX Standard. Pour plus d’informations, consultez [Utiliser des stratégies personnalisées pour autoriser et bloquer des applications pour les appareils Samsung KNOX Standard](/intune/deploy-use/custom-policy-to-allow-and-block-samsung-knox-apps).

- **Lien Commentaires du portail d’entreprise vers Microsoft**

   Le site web du portail d’entreprise permet aux utilisateurs finaux d’appuyer sur un nouveau lien « Commentaires », situé en bas de la page, pour envoyer des commentaires à Microsoft concernant leur expérience avec le site. Les commentaires collectés anonymement permettent à Microsoft d’améliorer l’expérience du site web du portail d’entreprise pour les utilisateurs.

- **Version minimale de Managed Browser iOS mise à jour vers 8.0**

  L’application Microsoft Intune Managed Browser pour iOS a été mise à jour pour prendre en charge les appareils exécutant iOS 8.0 ou version ultérieure. Même si les appareils iOS 7.1 peuvent toujours utiliser l’application Managed Browser existante, encouragez vos utilisateurs à effectuer la mise à jour vers iOS 8.0 ou une version ultérieure pour tirer pleinement parti des nouvelles fonctionnalités de Managed Browser.

### <a name="new-in-configuration-manager-technical-preview"></a>Nouveautés de Configuration Manager Technical Preview

Aucune nouvelle fonctionnalité hybride n’a été introduite en août 2016 pour Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Aucune nouvelle fonctionnalité hybride n’a été introduite en août 2016 pour Configuration Manager (Current Branch).

## <a name="july-2016"></a>Juillet 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

Les fonctionnalités Intune suivantes introduites en juillet 2016 fonctionnent dans les déploiements hybrides.

- **Le composant Xamarin pour les applications Intune est disponible**

  Le composant Xamarin du SDK de l’application Intune vous permet d’activer les fonctionnalités de gestion des applications mobiles Intune dans vos applications iOS et Android mobiles avec Xamarin. Ce composant est disponible dans le [Store Xamarin](https://components.xamarin.com/view/Microsoft.Intune.MAM) ou dans la [page Github Microsoft Intune](https://github.com/msintuneappsdk).

- **Amélioration de l’expérience utilisateur final lors de l’inscription d’appareils Windows**

  Quand vous utilisez l’accès conditionnel, les étapes d’inscription pour Windows 8.1, Windows 10 Desktop et Windows 10 Mobile ont été clarifiées dans le site web Portail d’entreprise. Les utilisateurs verront à présent des étapes **Inscription de l’appareil** et **Jonction d’espace de travail** distinctes, ce qui leur permet de voir plus facilement l’état de leur appareil et de terminer le processus s’ils rencontrent un échec de jonction d’espace de travail. Les étapes distinctes sont également supposées simplifier le processus de dépannage pour les administrateurs informatiques. Auparavant, quand les utilisateurs finaux tentaient d’effectuer une inscription et que toutes les étapes d’inscription réussissaient à l’exception de la jonction d’espace de travail, l’appareil inscrit n’apparaissait pas dans la liste des appareils pour être identifiés par les utilisateurs, ce qui est une source de confusion pour les utilisateurs.

  - **Réinitialisation complète désormais disponible pour les appareils Windows 10**

    Les PC Windows 10 et les ordinateurs portables inscrits en tant qu’appareils mobiles peuvent être réinitialisés pour rétablir les paramètres d’usine de l’appareil. Pour plus d’informations, consultez [Guide pratique pour protéger vos appareils avec la réinitialisation à distance](/sccm/mdm/deploy-use/wipe-lock-reset).

- **Modifications apportées aux comptes Gestionnaires d’inscription d’appareil dans l’application Portail d’entreprise iOS**

  Pour des performances et une évolutivité optimales, Intune n’affiche plus tous les appareils gestionnaires d’inscription d’appareil dans le volet Mes appareils de l’application Portail d’entreprise iOS. Seul l’appareil local exécutant l’application est affiché, et uniquement s’il est inscrit à l’aide de l’application Portail d’entreprise.

  L’utilisateur d’un gestionnaire d’inscription d’appareil peut effectuer des actions sur l’appareil local, mais la gestion à distance d’autres appareils inscrits ne peut être effectuée qu’à partir de la console d’administration Intune. De plus, Intune déprécie l’utilisation de comptes gestionnaires d’inscription d’appareil avec le programme d’inscription des appareils Apple ou l’outil Configurateur Apple. Ces deux méthodes d’inscription prennent déjà en charge l’inscription sans utilisateur pour les appareils iOS partagés.

  Utilisez uniquement des comptes gestionnaires d’inscription d’appareil quand l’inscription sans utilisateur pour les appareils partagés n’est pas disponible. Pour plus d’informations, consultez [Inscrire des appareils d’entreprise avec le Gestionnaire d’inscription d’appareil dans Microsoft Intune](../deploy-use/enroll-devices-with-device-enrollment-manager.md).

- **Changements apportés à l’application Portail d’entreprise Android**

  Si les utilisateurs finaux Android voient un message d’erreur indiquant qu’un certificat nécessaire pour leur appareil est manquant, ils peuvent appuyer sur un bouton « Comment résoudre ce problème » pour connaître la procédure d’installation du certificat manquant. Si les utilisateurs effectuent ces étapes, mais qu’un autre message d’erreur « Certificat manquant » s’affiche, ils sont invités à contacter leur administrateur informatique et de fournir ce lien, qui contient les étapes que les administrateurs informatiques peuvent utiliser pour résoudre le problème de certificat.

- **Limiter les installations d’applications à chargement indépendant sur des appareils Android inscrits**

  Les appareils Android ne peuvent plus installer d’applications via le site web Portail d’entreprise, sauf si les appareils ont été inscrits dans Intune à l’aide de l’application Portail d’entreprise Intune pour Android.


### <a name="new-in-configuration-manager-technical-preview"></a>Nouveautés de Configuration Manager Technical Preview

Aucune nouvelle fonctionnalité hybride n’a été introduite en juillet 2016 pour Configuration Manager Technical Preview.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes qui étaient précédemment disponibles dans les versions Configuration Manager Technical Preview sont maintenant disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1606.

* Rechercher, gérer et distribuer des applications du Windows Store pour Entreprises pour des appareils Windows 10 à partir de la console Configuration Manager ([1604](#new-in-1604-technical-preview))
*   Paramètre SmartLock pour les appareils Android ([1604](#new-in-1604-technical-preview))
*   VPN déclenché par les applications pour les appareils Windows 10 ([1605](#new-in-1605-technical-preview))
*   Nouvelle expérience pour les actions d’appareils distants ([1605](#new-in-1605-technical-preview))
*   Applications du Windows Store pour Entreprises ([1605](#new-in-1605-technical-preview))
*   Améliorations générales pour les applications achetées en volume ([1605](#new-in-1605-technical-preview))
*   Protection des informations Windows (WIP) ([1605](#new-in-1605-technical-preview))
*   Prédéclarer des appareils d’entreprise avec numéro IMEI ou numéro de série iOS ([1605](#new-in-1605-technical-preview))
*   Classer automatiquement des appareils dans des regroupements ([1606](#new-in-1606-technical-preview))

Pour plus d’informations sur les nouvelles fonctionnalités, consultez la documentation de la version Technical Preview spécifiée.

## <a name="june-2016"></a>Juin 2016

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune
Les fonctionnalités Intune suivantes introduites en juin 2016 fonctionnent dans les déploiements hybrides.

- Les informations sur l’**état du service Intune** pour Intune ont été déplacées vers un emplacement central avec d’autres services Microsoft. Vous trouverez maintenant ces informations dans le centre d’administration Microsoft 365 sous état du Service. Pour plus d’informations, consultez ce [billet de blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/).

- **Expérience de configuration de la stratégie de données d’entreprise Windows 10 améliorée**

  Intune propose maintenant une expérience améliorée pour la configuration de la stratégie Protection des informations Windows 10. Les améliorations comprennent de meilleures méthodes pour créer des règles d’application et spécifier la définition des limites réseau ainsi que d’autres paramètres de la Protection des informations Windows. Pour en savoir plus, consultez [Créer une stratégie Protection des informations Windows (WIP) à l’aide de Microsoft Intune](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune).

- **Stratégie de contrôle d’accès réseau Cisco ISE pour Intune**

  Les clients qui utilisent Cisco ISE (Identity Service Engine) 2.1 et aussi Microsoft Intune peuvent définir une stratégie de contrôle d’accès réseau dans ISE. À l’aide de cette stratégie, les appareils qui doivent se connecter au réseau Wi-Fi ou VPN doivent respecter les conditions suivantes avant que l’accès ne leur soit accordé :

  - Ils doivent être gérés par Intune
  - Ils doivent être conformes à toutes les stratégies de conformité Intune déployées

  Les utilisateurs finaux d’appareils non conformes sont invités à les inscrire et corriger tout problème de conformité pour obtenir l’accès.

- **Accès conditionnel pour le navigateur**

  Vous pouvez définir une stratégie d’accès conditionnel pour Exchange Online et SharePoint Online afin qu’ils soient seulement accessibles à partir de navigateurs web pris en charge sur des appareils iOS et Android gérés et conformes. Les utilisateurs finaux qui essaient de se connecter aux sites OWA (Outlook Web Access) et SharePoint avec des appareils iOS et Android sont invités à inscrire leurs appareils avec Intune, ainsi qu’à résoudre les problèmes de non-conformité avant de se connecter. Pour plus d'informations, voir

  * [Restreindre l’accès à la messagerie Exchange Online et Exchange Online Dedicated (nouvel environnement) avec Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Restreindre l’accès à SharePoint Online avec Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online prend en charge l’accès conditionnel**

  Vous pouvez définir une stratégie d’accès conditionnel pour Dynamics CRM Online afin qu’il soit accessible uniquement par les appareils iOS et Android gérés et conformes. Les utilisateurs finaux qui essaient de se connecter à l’application mobile Dynamics CRM sur iOS et Android sont invités à inscrire leurs appareils avec Intune, ainsi qu’à résoudre les problèmes de non-conformité avant de se connecter. Pour plus d’informations, consultez [Restreindre l’accès à Dynamics CRM Online avec Microsoft Intune](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune).

- **Mises à jour apportées à l’application Portail d’entreprise Android**

  Intune comporte désormais les nouvelles stratégies suivantes qui affectent les utilisateurs de l’application Portail d’entreprise Android :   

  Stratégie  |Effet sur les utilisateurs  
  ---------|---------
  Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues (Android 4.0+)     |  Les utilisateurs finaux équipés d’appareils Android 4.0 ou version ultérieure voient le message « L’installation à partir de sources inconnues doit être désactivée ». Les utilisateurs doivent accéder à **Paramètres > Sécurité** sur leurs appareils et désactiver l’option **Sources inconnues**. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir plus d’informations sur le message et de savoir pourquoi ils doivent désactiver le paramètre.
  Exiger que les appareils interdisent l’installation des applications provenant de sources inconnues (Android 4.0+)  |    Les utilisateurs finaux équipés d’appareils Android 4.0 ou version ultérieure voient le message « Rechercher les menaces de sécurité sur l’appareil ». Les utilisateurs doivent accéder à **Paramètres > Google > Sécurité** sur leurs appareils et activer l’option **Rechercher les menaces de sécurité sur l’appareil**. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir plus d’informations sur le message et de savoir pourquoi ils doivent activer le paramètre.     
  Exiger que le débogage USB soit désactivé (Android 4.2+)  | Les utilisateurs finaux équipés d’appareils Android 4.2 ou version ultérieure voient le message « Le débogage USB doit être désactivé ». Les utilisateurs doivent accéder à **Paramètres > Options pour développeurs** sur leurs appareils et désactiver l’option **Débogage USB**. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir plus d’informations sur le message et de savoir pourquoi ils doivent désactiver le paramètre.
  Niveau minimal du correctif de sécurité Android (Android 6.0+)  | Les utilisateurs finaux équipés d’appareils Android 6.0 ou version ultérieure voient le message « Cet appareil n’est pas au niveau minimal du correctif de sécurité Android ». Les utilisateurs doivent installer le correctif de sécurité requis. Un lien dans le message de compatibilité permet aux utilisateurs d’obtenir des informations sur la façon d’installer le correctif de sécurité requis et d’identifier le correctif de sécurité actuellement installé.

- **Mises à jour apportées à l’application Portail d’entreprise iOS**

  * Quand les utilisateurs finaux installent des applications métier, ils bénéficient désormais d’une expérience améliorée en termes d’installation d’applications. Si l’installation de l’application prend beaucoup de temps, les utilisateurs peuvent synchroniser manuellement leur appareil pour forcer la reprise du processus de synchronisation. Pour passer en revue les instructions pour l’utilisateur final, consultez Synchroniser manuellement votre appareil iOS.
  * L’application Portail d’entreprise Microsoft Intune pour iOS a été mise à jour pour prendre en charge iOS versions 8.0 et ultérieure. Cette mise à jour signifie que les utilisateurs finaux peuvent installer l’application Portail d’entreprise et inscrire de nouveaux appareils dans Intune uniquement si l’appareil exécute iOS version 8.0 ou ultérieure. Les utilisateurs qui ont déjà inscrit des appareils exécutant une version non prise en charge d'iOS peuvent continuer à utiliser l'application Portail d'entreprise qui figure sur leur appareil.


### <a name="new-in-1606-technical-preview"></a>Nouveautés de la version d’évaluation technique 1606
Les nouvelles fonctionnalités suivantes introduites en juin 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager Technical Preview 1606.

- **Classer automatiquement des appareils dans des regroupements**

  Vous pouvez créer des catégories d’appareils, qui permettent de placer automatiquement les appareils dans des regroupements d’appareils quand vous utilisez Configuration Manager avec Intune. Les utilisateurs doivent ensuite choisir une catégorie d’appareils quand ils inscrivent un appareil dans Intune. Vous pouvez aussi modifier la catégorie d’un appareil à partir de la console Configuration Manager. Pour plus d’informations, consultez [Classer automatiquement des appareils dans des regroupements](/sccm/core/get-started/capabilities-in-technical-preview-1606#dmp_category) dans [Fonctionnalités de la version d’évaluation technique 1606 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1606).

  > [!IMPORTANT]
  > Cette fonctionnalité est opérationnelle avec la version de juin 2016 de Microsoft Intune. Vérifiez que vous avez effectué la mise à jour vers cette version avant d’essayer ces procédures.

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)
Aucune nouvelle fonctionnalité hybride n’a été introduite en juin 2016 pour Configuration Manager (Current Branch).

##  <a name="may-2016"></a>Mai 2016  

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  
 Les fonctionnalités Intune suivantes introduites en mai 2016 fonctionnent dans les déploiements hybrides.

- **SDK GAM : Configuration de longueur de code confidentiel de prise en charge**

  Vous pouvez désormais spécifier une longueur de code confidentiel pour les applications GAM semblable à un code confidentiel d’appareil. Cela nécessite que les utilisateurs finaux se conforment aux nouvelles restrictions que vous définissez. L’écran de saisie du code confidentiel est légèrement modifié pour tenir compte de l’entrée la plus longue. Pour plus d’informations, consultez [Paramètres de stratégie GAM pour Android](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) et [Paramètres de stratégie GAM pour iOS](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings).  

- **Skype Entreprise pour iOS et Android**

  Vous pouvez maintenant cibler Skype Entreprise avec [GAM sans stratégie d’inscription](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune). Une fois les utilisateurs connectés, les stratégies GAM sont appliquées.  

- **Nouvelles applications disponibles pour la gestion avec des stratégies GAM**

  Les applications Microsoft Word, Excel et PowerPoint pour Android peuvent maintenant être associées à des stratégies GAM sur les appareils qui ne sont pas inscrits avec Intune. Pour obtenir une liste complète des applications prises en charge, accédez à la galerie des applications mobiles Microsoft Intune dans la page [Partenaires d’application Microsoft Intune](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx).  

- **Application portail d’entreprise Android : Notifications toast l’utilisateur final**

  Les notifications toast de l’application Portail d’entreprise Android apparaissent quand les utilisateurs finaux inscrivent ou suppriment leurs appareils dans le portail d’entreprise.  

- **Site Web du portail d’entreprise : Bannière d’identification de l’appareil fournit d’autres informations aux utilisateurs finaux**

  Les utilisateurs finaux peuvent désormais identifier plus facilement l’appareil qu’ils ont sélectionné quand ils utilisent le site web du portail d’entreprise. Si l’appareil choisi n’est pas correct, ils peuvent sélectionner l’appareil approprié en appuyant sur le lien **Appuyer ici** dans la bannière de la page d’accueil.  


### <a name="new-in-1605-technical-preview"></a>Nouveautés de la version d’évaluation technique 1605  
 Les nouvelles fonctionnalités suivantes introduites en mai 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager Technical Preview 1605. Ces fonctionnalités exigent que vous utilisiez la console Configuration Manager pour les configurer et les gérer.  

- **VPN déclenché par les applications pour les appareils Windows 10**

  Pour les appareils Windows 10 gérés à l’aide de Configuration Manager avec Intune, vous pouvez ajouter une liste d’applications qui ouvrent automatiquement une connexion VPN que vous avez configurée via la console d’administration Configuration Manager. Pour plus d’informations, consultez [VPN déclenché par les applications pour les appareils Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1605) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605)  

- **Nouvelle expérience pour les actions des appareils à distance**

  L’exécution des actions des appareils à distance à partir de la console Configuration Manager a été améliorée.

  Des actions courantes telles que **Mettre hors service/Réinitialiser**, **Réinitialisation du code secret**, **Verrouillage à distance** et **Contourner le verrou d’activation** figurent désormais dans le menu **Actions de l’appareil à distance** accessible à partir de l’espace de travail **Ressources et Conformité**

  Pour plus d’informations, consultez [Nouvelle expérience pour les actions des appareils à distance](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Applications du Windows Store pour Entreprises**

  Le [Windows Store pour Entreprises](https://www.microsoft.com/en-us/business-store) est l’emplacement où vous pouvez trouver et acheter des applications pour votre organisation, isolément ou en volume. En connectant le Store à Configuration Manager, vous pouvez gérer les applications achetées en volume à partir de la console Configuration Manager. Pour plus d’informations, consultez [Applications du Windows Store pour Entreprises](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Améliorations générales pour les applications achetées en volume**

  Les applications achetées en volume dans le Windows Store pour Entreprises et App Store iOS ont été consolidées dans une même vue, **Informations de licence pour les applications du Store**. En outre, la façon dont vous créez des applications achetées en volume pour iOS a été améliorée. Pour plus d’informations, consultez [Améliorations générales pour les applications achetées en volume](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Prédéclarer des appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS**

  Vous pouvez désormais identifier des appareils d’entreprise en important leur numéro IMEI (International Mobile Equipment Identity). Vous pouvez charger un fichier de valeurs séparées par des virgules (.csv) contenant les numéros IMEI des appareils ou saisir manuellement les informations sur les appareils.  Vous pouvez également importer des numéros de série pour les appareils iOS.  Pour plus d’informations, consultez [Prédéclarer des appareils d’entreprise avec leur numéro IMEI ou leur numéro de série iOS](../../core/get-started/capabilities-in-technical-preview-1605.md#BKMK_IMEI) dans [Fonctionnalités de la version d’évaluation technique 1605 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1605).  

- **Protection des informations Windows (WIP)**

  Vous pouvez créer des éléments de configuration qui vous permettent de déployer vos stratégies Protection des informations Windows (WIP), notamment de choisir vos applications protégées, de définir le niveau de protection assuré par WIP et de rechercher des données d’entreprise sur le réseau. Pour plus d’informations sur WIP, consultez les rubriques suivantes :  

  -   [Protéger les données d’entreprise avec Protection des informations Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [Créer et déployer une stratégie Protection des informations Windows (WIP) à l’aide de System Center Configuration Manager](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)  
 Aucune nouvelle fonctionnalité hybride n’a été introduite en mai 2016 pour Configuration Manager (Current Branch).  

##  <a name="april-2016"></a>Avril 2016  

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  
 Les fonctionnalités Intune suivantes introduites en avril 2016 fonctionnent dans les déploiements hybrides.  

- **Conformité des utilisateurs GAM**

  Vous pouvez désormais afficher l’état de vos stratégies de gestion des applications pour tous les utilisateurs dans votre client Azure Active Directory (AAD).  Pour plus d’informations, consultez [Analyser les stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) dans la bibliothèque Intune.  

- **Contrôles GAM pour empêcher la synchronisation des contacts Outlook (Android)**

  Un nouveau paramètre est disponible, qui vous permet d’empêcher une application de synchroniser des contacts dans le carnet d’adresses natif sur les appareils Android. Ce nouveau paramètre est initialement pris en charge par l’application Outlook sur les appareils Android. Pour plus d’informations, consultez [Créer et déployer des stratégies de gestion des applications mobiles à l’aide de Microsoft Intune](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) dans la bibliothèque Intune.  

- **Améliorations apportées au site web du portail d’entreprise**

  Quand les utilisateurs Windows 10 Mobile et Windows Phone 8.1 installent des applications métier, ils voient à présent les nouveaux états suivants, qui leur fournissent plus de détails sur l’état de leur installation :  

  -   **En attente de la synchronisation de l’appareil** : l’utilisateur a appuyé sur Installer et l’appareil tente à présent la synchronisation avec l’infrastructure Intune. La synchronisation est nécessaire avant de procéder à l’installation. Le message « En attente de la synchronisation de l’appareil » est également un lien sur lequel les utilisateurs peuvent appuyer pour afficher des instructions sur la façon de synchroniser manuellement leur appareil avec Intune si le processus de synchronisation dure longtemps ou se bloque.  

  -   **Téléchargement** : la demande de téléchargement de l’utilisateur est en cours de traitement et l’appareil télécharge et installe l’application.  

- **Améliorations apportées à l’application Portail d’entreprise Android**

  Les utilisateurs qui n’ont pas inscrit leur appareil dans Intune et qui n’ont pas le bon certificat installé ne peuvent pas se connecter à l’application Portail d’entreprise Android et le message « Vous ne pouvez pas vous connecter, car il manque un certificat obligatoire à votre appareil. » s’affiche. Le message inclut un lien « Comment résoudre ce problème » sur lequel les utilisateurs peuvent appuyer pour afficher des instructions sur l’installation du certificat. Pour connaître les étapes que les utilisateurs finaux suivent pour résoudre ce problème, consultez [Un certificat obligatoire est manquant sur votre appareil](/intune/enduser/using-your-android-device-with-intune) dans la bibliothèque Intune.  

- **Améliorations apportées à l’application Portail d’entreprise iOS**

  La prise en charge de l’action Extraire pour actualiser a été ajoutée pour actualiser le contenu de l’écran d’accueil, qui inclut les applications répertoriées, les appareils répertoriés et les coordonnées du service informatique. L’action Extraire pour actualiser ne vérifie pas les informations de conformité ni de la stratégie ; cette vérification peut être effectuée en sélectionnant la vignette de votre appareil et en appuyant sur le bouton **Synchroniser**.  

- **Améliorations apportées à l’application Portail d’entreprise Windows 10 Mobile et Windows Phone 8.1**

  Quand les utilisateurs finaux installent des applications métier, ils bénéficient désormais d’une expérience améliorée en termes d’installation d’applications. Si l’installation de l’application prend beaucoup de temps, les utilisateurs peuvent synchroniser manuellement leur appareil pour forcer la reprise du processus de synchronisation. Pour passer en revue les instructions pour l’utilisateur final, consultez [Synchroniser votre appareil manuellement à l’aide du site web Portail d’entreprise](/intune/enduser/using-your-windows-device-with-intune) dans la bibliothèque Intune.  

###  <a name="new-in-1604-technical-preview"></a>Nouveautés de la version d’évaluation technique 1604
 Les nouvelles fonctionnalités suivantes introduites en avril 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager Technical Preview 1604. Ces fonctionnalités exigent que vous utilisiez la console Configuration Manager pour les configurer et les gérer.  

- **Rechercher, gérer et distribuer des applications du Windows Store pour Entreprises pour des appareils Windows 10 à partir de la console Configuration Manager**


  La prise en charge du Windows Store pour Entreprises est disponible dans Configuration Manager Technical Preview 1604 pour vous aider à rechercher, gérer et distribuer des applications pour les appareils Windows 10 que vous gérez. Pour plus d’informations, consultez [Gérer les applications achetées en volume à partir du Windows Store pour Entreprises](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business) dans [Fonctionnalités de la version d’évaluation technique 1604 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604).  

- **Paramètre SmartLock pour les appareils Android**

  Un nouveau paramètre a été ajouté à l’élément de configuration Android et Samsung KNOX Standard, qui vous permet de contrôler la fonctionnalité SmartLock sur les appareils Android compatibles.  Vous pouvez utiliser ce paramètre pour empêcher des utilisateurs finaux de configurer SmartLock. Consultez [Paramètre SmartLock pour les appareils Android](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices) dans [Fonctionnalités de la version d’évaluation technique 1604 pour System Center Configuration Manager](/sccm/core/get-started/capabilities-in-technical-preview-1604.md).  

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)  
 Aucune nouvelle fonctionnalité hybride n’a été introduite en avril 2016 pour Configuration Manager (Current Branch).  

##  <a name="march-2016"></a>Mars 2016  

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  
 Les fonctionnalités Intune suivantes introduites en mars 2016 fonctionnent dans les déploiements hybrides.  

- **Contrôles GAM pour empêcher la synchronisation des contacts Outlook (iOS)**

  Un nouveau paramètre est disponible, qui vous permet d’empêcher une application de synchroniser des contacts dans le carnet d’adresses natif sur les appareils iOS. Ce nouveau paramètre est pris en charge par l’application Outlook sur les appareils iOS. Pour plus d’informations sur ce paramètre et d’autres paramètres, consultez [Créer et déployer des stratégies GAM](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune) dans la bibliothèque Intune.  

- **Skype Entreprise Online prend en charge l’accès conditionnel**

  Vous pouvez définir une stratégie d’accès conditionnel pour Skype Entreprise Online afin qu’il soit accessible uniquement par les appareils iOS et Android gérés et conformes.  Pour plus d’informations, consultez [Gérer l’accès à Skype Entreprise Online](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune) dans la bibliothèque Intune.  

- **Prise en charge d’iOS 9.3**

  Lundi 21 mars, Apple a annoncé la disponibilité d’iOS 9.3. Toutes les fonctionnalités Intune existantes actuellement disponibles pour la gestion des appareils iOS continuent de fonctionner en toute transparence quand les utilisateurs effectuent la mise à niveau de leurs appareils vers iOS 9.3.  

- **Packages d’application Windows disponibles directement depuis le site web du portail d’entreprise**

  Les utilisateurs de PC exécutant Windows RT, Windows 8 et Windows 8.1 peuvent désormais installer les packages d’application Windows (avec l’extension .appx) directement depuis le site web du portail d’entreprise. Auparavant, vous deviez déployer l’application Portail d’entreprise, ou les utilisateurs devaient l’installer sur leurs appareils, pour installer des applications.  

- **Les utilisateurs peuvent verrouiller à distance leurs appareils depuis le site web du portail d’entreprise**

  Une nouvelle option Verrouillage à distance a été ajoutée au site web du portail d’entreprise pour permettre aux utilisateurs de verrouiller à distance leur appareil depuis le portail s’il est perdu ou volé.  

- **Tirer parti de la fonctionnalité de gestion iOS Open In pour les appareils inscrits dans une solution de gestion des appareils mobiles tierce**

  Vous pouvez utiliser votre fournisseur de solution de gestion des appareils mobiles tierce pour tirer parti de la fonctionnalité de gestion iOS Open In. Vous pouvez définir les restrictions dans les paramètres de profil de configuration et déployer l’application à l’aide de votre logiciel de gestion des appareils mobiles. Quand l’utilisateur installe l’application gérée, les restrictions sont appliquées. Lire les détails : [Stratégies de gestion des applications mobiles Microsoft Intune et iOS Open In](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune) dans la bibliothèque Intune.  

- **Applications Microsoft qui prennent en charge GAM**

  La liste des applications Microsoft que vous pouvez utiliser avec les stratégies de gestion des applications mobiles Intune a été mise à jour pour inclure les dernières applications (pour les appareils inscrits avec Intune uniquement).  

- **Déployer Adobe Reader pour Microsoft Intune sur des appareils iOS gérés par Intune dans votre entreprise**

  L’application Adobe Reader pour iOS peut maintenant être gérée sur les appareils inscrits avec la stratégie de gestion des applications mobiles Intune.  

- L’application de partage Rights Management est prise en charge pour Android

  Les administrateurs informatiques peuvent déployer des stratégies de gestion des applications mobiles afin que les utilisateurs finaux puissent afficher des images, des fichiers PDF et AV en toute sécurité, que le service informatique utilise ou non Intune pour gérer les appareils.  

- **Améliorations apportées à l’application Portail d’entreprise Android et iOS**

  -   Quand vos utilisateurs lancent une application qui est gérée par la gestion des applications mobiles (GAM), ils voient un message qui leur indique que l’application est gérée par leur société. Les utilisateurs peuvent désormais appuyer sur un lien « En savoir plus » pour obtenir plus d’informations ici sur ce que signifie « applications gérées ». Ils peuvent aussi appuyer sur « Ne plus afficher ce message » afin que le message ne s’affiche plus lors du lancement de l’application.  

  -   De nouveaux écrans ont été ajoutés pour guider les utilisateurs dans le processus d’inscription et fournir plus d’informations sur la raison pour laquelle les utilisateurs doivent s’inscrire ainsi que sur ce que les administrateurs informatiques peuvent et ne peuvent pas voir sur leurs appareils inscrits.  

  -   Des messages d’erreur d’inscription s’affichent maintenant dans l’application Portail d’entreprise.  

### <a name="new-in-configuration-manager-technical-preview"></a>Nouveautés de Configuration Manager Technical Preview  
 Aucune nouvelle fonctionnalité hybride n’a été introduite en mars 2016 pour Configuration Manager Technical Preview.  

### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)  
 Les nouvelles fonctionnalités suivantes introduites en mars 2016 sont disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1602. Ces fonctionnalités exigent que vous utilisiez la console Configuration Manager pour les configurer et les gérer.  

- **Stratégies de configuration d’applications iOS**

  Dans la version 1602 de Configuration Manager (Current Branch), vous pouvez utiliser des stratégies de configuration d’applications pour fournir des paramètres pouvant être requis si l’utilisateur exécute une application iOS. Pour plus d’informations, consultez [Configurer des applications iOS avec des stratégies de configuration des applications dans System Center Configuration Manager](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).  

- **Gérer les applications iOS achetées en volume**

  Dans la version 1602 de Configuration Manager (Current Branch), vous pouvez déployer et gérer des applications que vous avez achetées en volume dans le cadre d’un Programme d’achat en volume (VPP) Apple, en important les informations de licence à partir de l’App Store et en suivant le nombre de licences que vous avez utilisées. Pour plus d’informations, consultez [Gérer les applications iOS achetées en volume avec System Center Configuration Manager](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps).  

- **Création automatique d’applications mobiles Office**

  Depuis la version 1602 de Configuration Manager (Current Branch), les applications mobiles Microsoft Office suivantes pour Android et iOS sont créées quand vous effectuez la mise à niveau à partir de la version 1511 :  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote (iOS uniquement)  
  -   Microsoft Outlook  

  Vous trouverez ces applications dans le nœud Applications de la console Configuration Manager. Pour plus d’informations sur le déploiement d’applications, consultez [Déployer des applications avec System Center Configuration Manager](../../apps/deploy-use/deploy-applications.md).  

- **Paramètres du mode plein écran pour les appareils Samsung KNOX Standard Android**

  Le mode kiosque vous permet de verrouiller un appareil pour n'autoriser que le fonctionnement de certaines fonctionnalités.  À partir de la version 1602 de Configuration Manager (Current Branch), vous pouvez désormais spécifier les paramètres du mode plein écran pour les appareils Samsung KNOX Standard. Pour plus d’informations, consultez [Guide pratique pour créer des éléments de configuration pour des appareils Android et Samsung KNOX Standard gérés sans le client System Center Configuration Manager](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client).  

- **Verrou d’activation iOS**

  Depuis la version 1602 de Configuration Manager (Current Branch), vous pouvez gérer le verrou d’activation iOS, fonctionnalité de l’application Rechercher mon iPhone pour les appareils iOS 7.1 et versions ultérieures. Le verrou d'activation est activé automatiquement quand l'application Rechercher mon iPhone est utilisée sur un appareil.  Pour plus d’informations, consultez [Gérer le contournement du verrou d’activation iOS pour System Center Configuration Manager](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock).  



## <a name="notices"></a>Remarques

### <a name="system-center-2012-configuration-sp1-and-system-center-2012-r2-configuration-manager-rtm-support-for-hybrid-mobile-device-management-ending-on-april-10-2017"></a>System Center 2012 Configuration SP1 et System Center 2012 R2 Configuration Manager (RTM) : Prise en charge pour la gestion des appareils mobiles hybride fin le 10 avril 2017
*11 janvier 2017*

La prise en charge de System Center 2012 Configuration Manager SP1 et de System Center 2012 R2 Configuration Manager RTM a pris fin le 12 juillet 2016. Par conséquent, la prise en charge de ces versions se connectant au service Microsoft Intune pour la gestion hybride des appareils mobiles prendra fin le 10 avril 2017. Après cette date, la gestion hybride des appareils mobiles cessera de fonctionner avec ces versions. Les appareils gérés deviendront essentiellement non gérés car le connecteur Intune ne se connectera plus au service Intune. Les données de Configuration Manager (par exemple, les stratégies et les applications) ne seront plus transmises à Intune et les données d’appareil mobile ne parviendront plus à Configuration Manager jusqu’à ce qu’une mise à niveau soit appliquée.

Si vous exécutez un déploiement hybride avec Configuration Manager 2012 SP1 ou R2 RTM, nous vous recommandons de mettre à niveau vers Configuration Manager (Current Branch) ou vers le dernier service pack pris en charge pour Configuration Manager 2012 (R2 SP1 ou SP2) avant le 10 avril 2017 afin d’éviter toute interruption du service.

Ressources supplémentaires :
-   [Mettre à niveau vers System Center Configuration Manager (Current Branch)](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager)
-   [Planification de la mise à niveau vers System Center 2012 R2 Configuration Manager SP1](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningR2SP1Upgrade)
-   [Planification de la mise à niveau vers System Center 2012 Configuration Manager SP2](https://technet.microsoft.com/library/jj822981.aspx#BKMK_PlanningSP2Upgrade)

### <a name="windows-phone-8-company-portal-upload-deprecated"></a>Chargement du portail d’entreprise Windows Phone 8 obsolète
*25 octobre 2016*

La possibilité de charger une application Portail d’entreprise signée a été supprimée de la console Configuration Manager, car le support technique Intune est déprécié pour Windows 8, Windows Phone 8 et Windows RT, le support pour le portail d’entreprise Windows Phone 8 se termine au mois de novembre.  Les appareils Windows 8, Windows Phone 8 et Windows RT qui sont déjà inscrits continueront à être pris en charge, mais l’inscription d’appareils supplémentaires auprès de ces plateformes ne sera pas prise en charge.
