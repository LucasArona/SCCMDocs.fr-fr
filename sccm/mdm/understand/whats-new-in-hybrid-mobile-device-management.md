---
title: Nouveautés de la gestion MDM hybride
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec Configuration Manager et Intune.
ms.date: 08/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87a40300cfe13ec097d155093fbb7b70af3b459c
ms.sourcegitcommit: 8661f10596f565ca2b7bdb5951388b44b3b622ee
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2018
ms.locfileid: "43193916"
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Nouveautés de la gestion hybride des appareils mobiles avec Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.     

> [!Important]  
> Depuis le 14 août 2018, la gestion des appareils mobiles hybride est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures). Pour plus d’informations, consultez [Qu’est-ce que la gestion MDM hybride ?](/sccm/mdm/understand/hybrid-mobile-device-management).<!--Intune feature 2683117-->  


> [!Note]    
> Intune sur Azure est la solution MDM recommandée de Microsoft.     
> - Pour plus d’informations sur les nouvelles fonctionnalités et mises à jour de la version autonome d’Intune, consultez [Nouveautés de Microsoft Intune](https://docs.microsoft.com/intune/whats-new).    
> - Pour plus d’informations sur la procédure de migration vers la version autonome d’Intune, consultez [Migrer appareils et utilisateurs MDM hybrides vers Intune autonome](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - Pour plus d’informations sur les mises à jour de l’interface utilisateur pour Intune et la gestion MDM hybride, consultez [Mises à jour de l’interface utilisateur pour les applications utilisateur final Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 



##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  

Chaque section de cet article répertorie les fonctionnalités hybrides sous trois catégories différentes. Utilisez l’aide suivante pour déterminer la compatibilité des fonctionnalités de chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|Description|
|-|-|
|**Nouveautés de Microsoft Intune** | En règle générale, toutes les fonctionnalités listées dans cette catégorie fonctionnent avec chacune des versions de Configuration Manager. Sont notamment comprises les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités ont seulement besoin du service Intune, sans aucune fonctionnalité supplémentaire dans Configuration Manager.|
|**Nouveautés de Configuration Manager Technical Preview**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la branche Technical Preview spécifiée. Pour tester ces fonctionnalités, vous devez installer la version Technical Preview spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour Configuration Manager](/sccm/core/get-started/technical-preview).|
|**Nouveautés de Configuration Manager (Current Branch)**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch). Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, effectuez la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers Configuration Manager](/sccm/core/servers/deploy/install/upgrade-to-configuration-manager).|


## <a name="august-2018"></a>Août 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

### <a name="new-user-experience-update-for-the-company-portal-website"></a>Nouvelle mise à jour de l’expérience utilisateur du site web Portail d’entreprise
<!--2000968--> Sur la base de vos retours, nous avons ajouté de nouvelles fonctionnalités au site web Portail d’entreprise. Vous constaterez une amélioration significative des fonctionnalités existantes et de la convivialité de vos appareils Android, iOS et Windows. Certaines rubriques du site présentent un nouveau design, à la fois moderne et réactif. Ces rubriques incluent les détails de l’appareil, les commentaires, le support technique et la vue d’ensemble de l’appareil. Vous remarquerez également les améliorations suivantes :

- Des flux de travail simplifiés sur toutes les plateformes d’appareil
- Des flux d’identification et d’inscription d’appareil améliorés
- Des messages d’erreur plus utiles
- Un langage plus convivial, avec moins de jargon technique
- La possibilité de partager des liens directs vers les applications
- Des performances améliorées pour les grands catalogues d’applications
- Une meilleure accessibilité pour tous les utilisateurs



## <a name="july-2018"></a>Juillet 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="updated-intune-app-sdk-for-android-is-now-available"></a>Une mise à jour du Kit de développement logiciel (SDK) Intune pour Android est maintenant disponible
<!--2744271--> Une version mise à jour du Kit SDK de l’application Intune pour Android est disponible pour prendre en charge la version Android 9 Pie. Si vous êtes un développeur d’application et que vous utilisez le SDK Intune pour Android, installez la version mise à jour du SDK de l’application Intune. Cette mise à jour permet de s’assurer que cette fonctionnalité Intune au sein de vos applications Android continuera de fonctionner comme prévu sur les appareils Android 9 Pie. Cette version du SDK de l’application Intune fournit un plug-in intégré qui effectue les mises à jour du Kit de développement logiciel (SDK). Vous n’avez pas besoin de réécrire le code existant qui est intégré. Pour plus d’informations, consultez [SDK Intune pour Android](https://github.com/msintuneappsdk/ms-intune-app-sdk-android). 

Si vous utilisez l’ancien style de badgeage pour Intune, utilisez l’icône en forme de porte-documents. Pour plus d’informations sur la personnalisation, consultez la rubrique [Système de badgeage de l’application Intune](https://github.com/msintuneappsdk/intune-app-partner-badge).


#### <a name="support-for-security-enhancement-in-intune-service"></a>Prise en charge de l’amélioration de la sécurité dans le service Intune
<!--2520152--> Vous pouvez désormais spécifier que les appareils auxquels aucune stratégie de conformité n’est affectée ne sont pas conformes en mode hybride. Configurez ce paramètre dans Intune sur le portail Azure. Nous vous recommandons vivement d’activer cette fonctionnalité pour sécuriser vos ressources internes.

Cette fonctionnalité est désactivée par défaut dans les locataires hybrides. Quand vous activez cette fonctionnalité, les appareils auxquels aucune stratégie de conformité n’est affectée sont considérés comme non conformes. Si vous activez également l’accès conditionnel, ces appareils n’ont plus accès aux ressources internes. Ces ressources peuvent être Outlook ou SharePoint, selon les stratégies d’accès conditionnel dans votre environnement. Si vous laissez ce paramètre désactivé, ces appareils conservent le même niveau d’accès que celui dont ils disposent actuellement.

Pour vous aider à déterminer l’impact de l’activation de cette fonctionnalité, nous mettons à votre disposition un [script dans la galerie TechNet](https://gallery.technet.microsoft.com/SQL-Query-for-Hybrid-MDM-5bcb8695). Quand vous exécutez ce script sur votre base de données de Configuration Manager, il répertorie les appareils qui ne sont pas ciblés par des stratégies de conformité.

Pour plus d’informations, consultez les articles suivants :
- [Security Enhancements in the Intune Service](https://aka.ms/compliance_policies) (billet de blog) 
- [Stratégies de conformité d’appareils dans Configuration Manager](/sccm/mdm/deploy-use/device-compliance-policies)

#### <a name="updates-to-out-of-compliance-messages-in-company-portal-app"></a>Mises à jour des messages hors de conformité dans l’application Portail d’entreprise 
<!--1832222--> Nous avons modifié les messages que les utilisateurs voient quand un appareil est hors de conformité. Les messages conservent leurs significations d’origine, mais ils ont été mis à jour avec un langage plus convivial et moins de jargon technique. Nous avons également actualisé des liens vers la documentation et des étapes de correction afin de les tenir à jour.  

Le texte suivant constitue un exemple des améliorations visibles dans les messages :  

- Avant : *Cet appareil n’a pas contacté le service Intune dans l’intervalle spécifié requis par votre administrateur informatique. Pour résoudre ce problème, veuillez ouvrir l’application Portail d’entreprise sur votre appareil et cliquer sur le bouton Vérifier la conformité.*  

- Après : *Votre appareil ne s’est pas connecté à votre organisation depuis un moment. Pour rétablir la connexion, ouvrez l’application Portail d’entreprise sur votre appareil, puis appuyez sur Vérifier les paramètres pour votre appareil.*  

#### <a name="select-device-categories-by-using-the-access-work-or-school-settings"></a>Sélectionner des catégories d’appareils à l’aide des paramètres Accès Professionnel ou Scolaire 
<!--1058963--> Si vous avez activé le [mappage de groupe d’appareils](https://docs.microsoft.com/intune/device-group-mapping), les utilisateurs de Windows 10 sont maintenant invités à sélectionner une catégorie d’appareils après s’être inscrits par le biais du bouton **Se connecter** dans **Paramètres** > **Comptes** > **Accès Professionnel ou Scolaire**.  

#### <a name="new-browsing-experiences-in-the-company-portal-app-for-windows"></a>Nouvelles expériences de navigation dans l’application Portail d’entreprise pour Windows 
<!--2317227--> Désormais, quand vous parcourez ou recherchez des applications dans l’application Portail d’entreprise pour Windows, vous pouvez basculer entre la vue **Vignettes** existante et la nouvelle vue **Détails**. La nouvelle vue affiche des informations détaillées sur chaque application, comme le nom, l’éditeur, la date de publication et l’état d’installation. 

La vue **Installée** de la page **Applications** vous permet de voir les détails concernant les installations d’application terminées et en cours. Pour voir à quoi ressemble la nouvelle vue, consultez [Nouveautés de l’interface utilisateur](https://docs.microsoft.com/intune/whats-new-app-ui).

#### <a name="more-opportunities-to-sync-in-the-company-portal-app-for-windows"></a>Améliorations apportées à la synchronisation dans l’application Portail d’entreprise pour Windows  
<!--2683177--> L’application Portail d’entreprise pour Windows vous permet désormais de lancer une synchronisation directement à partir de la barre des tâches Windows et du menu Démarrer. Cette fonctionnalité est particulièrement utile si vous avez seulement besoin de synchroniser des appareils et d’accéder aux ressources d’entreprise. Pour accéder à la nouvelle fonctionnalité, cliquez avec le bouton droit sur l’icône Portail d’entreprise qui est épinglée à la barre des tâches ou au menu Démarrer. Dans les options de menu, sélectionnez **Synchroniser cet appareil**. (Ce menu est également appelé liste de raccourcis.) Le Portail d’entreprise s’ouvre à la page **Paramètres** et lance la synchronisation. Pour connaître la procédure mise à jour, consultez [Synchroniser votre appareil Windows manuellement](https://docs.microsoft.com/intune/intune-user-help/sync-your-device-manually-windows#sync-from-device-taskbar-or-start-menu).



## <a name="june-2018"></a>Juin 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="access-to-macos-company-portal-pre-release-build"></a>Accès aux builds de préversion du portail d’entreprise macOS 
<!--1734766--> À l’aide de Microsoft AutoUpdate, vous pouvez vous inscrire pour recevoir des builds de manière anticipée en rejoignant le programme Insider. L’inscription vous permet d’utiliser le Portail d’entreprise mis à jour avant qu’il soit accessible à vos utilisateurs finaux.

#### <a name="intune-app-protection-policies-and-microsoft-edge"></a>Stratégies de protection des applications Intune et Microsoft Edge 
<!--1818968,1818969--> Le navigateur Microsoft Edge pour appareils mobiles (iOS et Android) prend désormais en charge les stratégies de protection des applications de Microsoft Intune. Les utilisateurs d’appareils iOS et Android qui se connectent à leur compte d’entreprise Azure Active Directory dans l’application Edge sont protégés par Intune. Sur les appareils iOS, la stratégie **Exiger un navigateur géré pour le contenu web** permet aux utilisateurs d’ouvrir les liens dans Edge lorsque celui-ci est géré.



## <a name="may-2018"></a>Mai 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Demande d’aide sur l’application Portail d’entreprise pour Windows 10 
<!--1874137--> Le portail d’entreprise pour Windows 10 envoie maintenant les journaux d’application directement à Microsoft quand l’utilisateur démarre le flux de travail permettant d’obtenir de l’aide. Ce comportement facilite la résolution des problèmes qui sont signalés à Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

#### <a name="android-for-work-and-lookout-onboarding-moved-to-intune-on-azure"></a>L’intégration d’Android for Work et de Lookout a été déplacée vers Intune sur Azure
<!--2355022,2357366--> Avec la dernière mise à jour d’Intune, vous pouvez activer et gérer l’intégration d’Android for Work et de Lookout Mobile Threat Defense sur les locataires de gestion d’appareils mobiles hybrides sur le portail Azure, dans Intune. Avant la mise à jour, ces paramètres pouvaient uniquement être configurés dans le portail Intune classique (Silverlight).
 
Remarque : Lookout est le seul fournisseur de Mobile Threat Defense (MTD) pris en charge dans les environnements hybrides. Si vous avez déjà intégré un autre fournisseur MTD, celui-ci continue d’apparaître dans Intune sur le portail Microsoft Azure. Si vous supprimez son connecteur, vous ne pourrez pas le rajouter.
 
Ces modifications n’impactent pas les fonctionnalités existantes. Continuez à utiliser la console Configuration Manager pour la gestion des applications, des rapports et des stratégies associés.
 
Pour plus d’informations, consultez les articles suivants :
- [Configurer la gestion d’appareils hybrides Android](/sccm/mdm/deploy-use/enroll-hybrid-android)
- [Gérer l’accès aux ressources d’entreprise en fonction du risque évalué pour l’appareil, le réseau et l’application](/sccm/mdm/deploy-use/lookout-mobile-threat-defense-in-configuration-manager)


#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Prise en charge de nouvelles versions du client Cisco AnyConnect pour iOS
<!--1357393--> Vous pouvez activer la prise en charge de Cisco AnyConnect pour iOS version 4.0.7 ou ultérieure. Si vous le faites, les profils VPN de Cisco AnyConnect existants sont nommés **Cisco Legacy AnyConnect** et continuent de fonctionner comme avant. L’option **Cisco AnyConnect** est pour les nouveaux profils VPN qui fonctionnent avec Cisco AnyConnect sur iOS version 4.0.7 ou ultérieure.

  > [!Tip]  
  > Cisco AnyConnect 4.0.07x et versions ultérieures pour iOS ont été introduits dans la version 1802 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la [mise à jour 4163547](https://support.microsoft.com/help/4163547) de la version 1802, cette fonctionnalité n’est plus en préversion.  

> [!Note]  
> Continuez à utiliser l’option **Cisco Legacy AnyConnect** pour les profils VPN macOS. 



## <a name="april-2018"></a>Avril 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune s’adapte au système Fluent Design dans l’application Portail d’entreprise pour Windows 10 
<!--1195010--> La [vue de navigation du système Fluent Design](/windows/uwp/design/basics/navigation-basics) a été ajoutée à l’application Portail d’entreprise Intune pour Windows 10. Sur le côté de l’application, vous voyez la liste statique et verticale de toutes les pages de niveau supérieur. Cliquez sur un lien pour passer rapidement d’une page à l’autre. Cette mise à jour est la première d’une série, destinée à rendre Intune plus souple et plus intuitif. Pour voir à quoi ressemble la mise à jour, consultez [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Amélioration des vignettes d’appareil dans le portail d’entreprise Windows 10
<!--2213364--> Les vignettes ont été mises à jour pour être plus accessibles aux utilisateurs malvoyants et plus performantes pour les outils de lecture d’écran.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>Test du portail d’entreprise pour macOS sur les machines virtuelles
<!--2216679--> Nous avons publié des conseils pour aider les administrateurs informatiques à tester l’application Portail d’entreprise pour macOS sur des machines virtuelles dans Parallels Desktop et VMware Fusion. Pour plus d’informations, consultez [Inscrire des machines virtuelles macOS pour les tester](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Envoyer des rapports de diagnostic dans l’application Portail d’entreprise pour macOS
<!--2216677--> L’application Portail d’entreprise pour les appareils macOS a été mise à jour afin d’améliorer la façon dont les utilisateurs signalent les erreurs relatives à Intune. À partir de l’application Portail d’entreprise, vos collaborateurs peuvent :

- Charger des rapports de diagnostic directement pour l’équipe de développement Microsoft.
- Envoyer par e-mail un ID d’incident à l’équipe du support informatique de votre entreprise.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Mise à jour de l’expérience de l’aide sur l’application Portail d’entreprise pour Android 
<!--1631531--> Nous avons mis à jour l’expérience de l’aide dans l’application Portail d’entreprise pour Android de façon à l’aligner sur les bonnes pratiques pour la plateforme Android. Quand les utilisateurs rencontrent un problème dans l’application, ils peuvent désormais appuyer sur **Menu** > **Aide** et :
- Charger les journaux de diagnostic à destination de Microsoft.
- Envoyer un e-mail qui décrit le problème et l’ID d’incident à une personne assurant le support dans l’entreprise.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Changement de l’endroit où vous configurez vos stratégies de protection d’application 
<!--2144597--> Dans le portail Azure, dans le service Microsoft Intune, nous allons vous rediriger temporairement de la zone **Intune App Protection** vers la section **Application mobile**. Toutes vos stratégies de protection d’application sont déjà répertoriées dans la section **Application mobile** dans Intune, sous la configuration de l’application. Au lieu d’accéder à Intune App Protection, vous accédez simplement à Intune. En avril 2018, nous mettrons fin à la redirection et nous supprimerons complètement **Intune App Protection**. Il n’y aura alors plus qu’un seul emplacement pour les stratégies de protection d’application dans Intune. 

**Quel est l’impact de ce changement ?** Ce changement affecte les clients autonomes et les clients hybrides Intune (Intune avec Configuration Manager). Cette intégration permet de simplifier l’administration de la gestion de votre cloud.

**Que faire pour se préparer à ce changement ?** Mettez **Intune** en favori à la place **d’Intune App Protection**. Familiarisez-vous avec le workflow de stratégie de protection d’application dans la zone **Application mobile** d’Intune. Nous vous redirigerons vers cette zone pendant une courte période, puis nous supprimerons **App Protection**. Rappelez-vous que toutes les stratégies de protection d’application sont déjà dans Intune et que vous pouvez modifier les stratégies d’accès conditionnel. Pour plus d’informations sur la modification des stratégies d’accès conditionnel, consultez [Accès conditionnel dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Pour plus d’informations, consultez [Que sont les stratégies de protection des applications ?](https://docs.microsoft.com/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Mise à jour de l’expérience utilisateur de l’application Portail d’entreprise pour iOS 
<!--1412866--> Nous avons publié une mise à jour majeure de l’expérience utilisateur de l’application Portail d’entreprise pour iOS. La mise à jour présente une toute nouvelle conception visuelle qui offre une apparence actualisée. Nous avons conservé les fonctionnalités de l’application, mais amélioré sa facilité d’utilisation et son accessibilité.  

Vous verrez également :
- Une prise en charge de l’iPhone X.
- Un lancement des applications et un chargement des réponses plus rapides pour faire gagner du temps aux utilisateurs.
- Des barres de progression supplémentaires pour fournir aux utilisateurs les informations d’état les plus à jour.
- Une amélioration du chargement des journaux pour signaler plus facilement les problèmes.  

Pour voir à quoi ressemble la mise à jour, consultez [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui).



## <a name="march-2018"></a>Mars 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>L’option Envoyer des commentaires du portail d’entreprise Windows risque de ne plus fonctionner
<!--2070166--> L’application Portail d’entreprise Windows dispose d’une option «Envoyer des commentaires » permettant aux utilisateurs d’envoyer des commentaires sur l’application à Microsoft. À compter du 30 avril 2018, cette option continue d’être prise en charge uniquement sur l’application Portail d’entreprise Windows 10 s’exécutant sur Windows 10 versions 1607 et ultérieures.   

**Quel est l’impact de ce changement ?**

Si l’application Portail d’entreprise Windows n’est pas installée pour les utilisateurs finaux, ignorez ce message.

Pour les utilisateurs finaux qui disposent de l’application Portail d’entreprise, depuis le 30 avril, le bouton « Envoyer des commentaires » ne fonctionne plus pour l’application dans les scénarios suivants :  

 - Application Portail d’entreprise Windows 10 sur Windows 10 version 1507 et version 1511  

 - Application Portail d’entreprise Windows Phone 8.1  

Pour les appareils concernés, l’option « Envoyer des commentaires » échoue, même lors des nouvelles tentatives. Pour envoyer des commentaires à Microsoft concernant les expériences sur ces plateformes, il existe d’autres canaux de retour répertoriés ci-dessous.

**Que faire pour se préparer à ce changement ?**

Informez les utilisateurs finaux de ce changement et mettez à jour toutes les instructions destinées aux utilisateurs, si nécessaire. 

Informez les utilisateurs finaux qui se servent du portail d’entreprise sur Windows Phone 8.1, Windows 10 version 1507 et Windows 10 version 1511 que deux autres canaux de retour sont disponibles. Ils peuvent :  

- Utiliser l’application Hub de commentaire sur Windows 10  
- Envoyer un e-mail à WinCPfeedback@microsoft.com  

Demandez aux utilisateurs finaux sur Windows 10 versions 1607 ou ultérieures d’effectuer une mise à jour vers la dernière version du portail d’entreprise Windows disponible dans le Microsoft Store.



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Les sites web Azure Active Directory peuvent nécessiter l’application Intune Managed Browser et prendre en charge l’authentification unique pour Managed Browser (Préversion publique)
<!-- 710595 --> Avec Azure Active Directory (Azure AD), vous pouvez maintenant restreindre l’accès aux sites web à l’application Intune Managed Browser sur les appareils mobiles. Dans Managed Browser, les données de site web restent sécurisées et séparées des données personnelles de l’utilisateur final. De plus, Managed Browser prend en charge les fonctionnalités d’authentification unique pour les sites protégés par Azure AD. La connexion à Managed Browser ou l’utilisation de Managed Browser sur un appareil avec une autre application gérée par Intune permet à Managed Browser d’accéder à des sites d’entreprise protégés par Azure AD sans que l’utilisateur ait à entrer ses informations d’identification. Cette fonctionnalité s’applique à des sites comme Outlook Web Access (OWA) et SharePoint Online, ainsi qu’à d’autres sites d’entreprise comme les ressources intranet accessibles via le proxy d’application Azure.



## <a name="february-2018"></a>Février 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Prise en charge du portail d’entreprise macOS pour les inscriptions qui utilisent le Gestionnaire d’inscription d’appareil**  
    Les utilisateurs peuvent désormais utiliser le Gestionnaire d’inscription d’appareil lors de l’inscription avec le Portail d’entreprise macOS.
    <!-- 1352411 -->


## <a name="january-2018"></a>Janvier 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Approuver l’application Portail d’entreprise pour Android for Work**  
  Si votre organisation utilise Android for Work, approuvez manuellement l’application Portail d’entreprise pour Android. Elle continue alors à recevoir les mises à jour automatiques à partir de Google Play Store managé.
  <!--1797090 -->  

- **Les stratégies d’accès conditionnel pour Intune sont disponibles uniquement à partir du portail Azure**   
  À compter de cette version, vous devez configurer et gérer vos stratégies d’accès conditionnel dans le [portail Azure](https://portal.azure.com) à partir d’**Azure Active Directory** > **Accès conditionnel**. Par souci pratique, vous pouvez également accéder à ces paramètres à partir d’Intune dans le portail Microsoft Azure (**Intune** > **Accès conditionnel**).
  <!-- 1737088 1634311 --> 

- **E-mails de mises à jour de conformité**    
  Quand un e-mail est envoyé pour signaler un appareil non conforme, des détails sur l’appareil non conformes sont inclus. 
  <!--1637547 -->

- **Nouvelles fonctionnalités de l’action « Résoudre » pour les appareils Android**    
  L’application Portail d’entreprise pour Android étend l’action « Résoudre » sur **Mettre à jour les paramètres d’appareil** afin de résoudre les [problèmes de chiffrement d’appareil](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Verrouillage à distance disponible dans l’application Portail d’entreprise pour Windows 10**    
  Les utilisateurs finaux peuvent désormais verrouiller à distance leurs appareils à partir de l’application Portail d’entreprise pour Windows 10. Cette action ne s’affiche pas pour l’appareil local qu’ils sont en train d’utiliser.
  <!--676506-->

- **Résolution plus rapide des problèmes de conformité affectant l’application Portail d’entreprise pour Windows 10**   
  Les utilisateurs finaux d’appareils Windows peuvent indiquer la raison de la non-conformité dans l’application Portail d’entreprise. Lorsque cela est possible, cette action leur permet d’accéder directement à l’emplacement approprié dans l’application Paramètres pour résoudre le problème.
  <!--676546-->    



## <a name="december-2017"></a>Décembre 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Déploiements d’applications disponibles maintenant pris en charge pour Android Entreprise**    
  Vous pouvez désormais déployer des applications Android Entreprise (anciennement Android for Work) comme **disponibles**, en plus d’**obligatoires**. Pour plus d’informations, consultez [Créer des applications Android avec System Center Configuration Manager](/sccm/mdm/deploy-use/creating-android-applications).



## <a name="november-2017"></a>Novembre 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Protocole de texte autorisé à partir d’applications managées**  
  Les applications gérées par le SDK d’application Intune peuvent envoyer des SMS.
  <!-- 1414050  -->   

- **L’application Portail d’entreprise pour macOS est disponible**   
  Le Portail d’entreprise Intune sur macOS offre une expérience mise à jour. Il est optimisé pour afficher clairement toutes les informations et les avis de conformité dont vos utilisateurs ont besoin pour tous les appareils qu’ils ont inscrits. Et une fois que le Portail d’entreprise Intune a été déployé sur un appareil, Microsoft AutoUpdate pour macOS fournit les mises à jour requises. Téléchargez le nouveau Portail d’entreprise Intune pour macOS en vous connectant au site web Portail d’entreprise Intune sur un appareil macOS.
  <!--1541700-->   

- **Microsoft Planner fait désormais partie de la liste des applications approuvées pour la gestion des applications mobiles (MAM)**    
  L’application Microsoft Planner pour iOS et Android fait désormais partie des applications approuvées pour la gestion des applications mobiles (MAM). Configurez l’application à partir d’Intune App Protection dans le portail Microsoft Azure de tous les locataires. Pour plus de détails, consultez [Liste GAM d’applications approuvées](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
  <!-- 1248473 -->    

- **Accès aux journaux d’applications managées pour iOS**    
  Les utilisateurs finaux disposant de Managed Browser peuvent maintenant afficher l’état de gestion de toutes les applications Microsoft publiées et envoyer des journaux afin de résoudre les problèmes liés à leurs applications iOS gérées.
  <!-- 1469920 -->    

  Pour découvrir comment activer le mode dépannage dans Managed Browser sur un appareil iOS, consultez [Guide pratique pour accéder aux journaux des applications gérées à l’aide de Managed Browser sur iOS](https://docs.microsoft.com/intune/app-configuration-managed-browser#how-to-access-to-managed-app-logs-using-the-managed-browser-on-ios).

- **Améliorations apportées au workflow de configuration des appareils dans l’application Portail d’entreprise pour iOS version 2.9.0**    
  Nous avons amélioré le workflow de configuration d’appareils dans l’application Portail d’entreprise pour iOS. La langue est plus conviviale et spécifique à votre entreprise, et nous avons regroupé des écrans quand cela était possible. Le processus est également plus spécifique à votre entreprise car nous utilisons son nom dans le texte de configuration. Vous pouvez voir ces derniers sur la page [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-november-13-2017).

- **Invites pour la saisie de commentaires pour l’application Portail d’entreprise pour Android**    
  L’application Portail d’entreprise pour Android demande désormais aux utilisateurs finaux d’envoyer leurs commentaires. Ces commentaires sont envoyés directement à Microsoft et permettent aux utilisateurs finaux de passer l’application en revue dans Google Play Store. La saisie de commentaires n’est pas obligatoire et peut être facilement ignorée, permettant ainsi aux utilisateurs finaux de continuer à utiliser l’application. 
  <!--1165249-->    

- **Informer les utilisateurs finaux des informations sur l’appareil qui peuvent être affichées pour les appareils Windows 10**    
  Nous avons ajouté **Type de propriété** dans l’écran Détails sur l’appareil de l’application Portail d’entreprise pour Windows 10. Ces informations permettent aux utilisateurs d’en savoir plus sur la confidentialité directement à partir de la documentation utilisateur Intune. Les utilisateurs peuvent également ces informations sur l’écran **À propos de**.
  <!--1337920-->    

- **Nouvelle action « Resolve » (Résoudre) disponible pour les appareils Android**    
  L’application Portail d’entreprise pour Android dispose désormais d’une action « Resolve » (Résoudre) sur la page _Mettre à jour les paramètres de l’appareil_. Si l’utilisateur final sélectionne cette option, il est directement dirigé vers le paramètre à cause duquel son appareil n’est pas conforme. L’application Portail d’entreprise pour Android prend en charge actuellement cette action pour les paramètres [code d’accès de l’appareil](https://docs.microsoft.com/intune-user-help/set-your-pin-or-password-android), [chiffrement de l’appareil](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android), [débogage USB](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-usb-debugging-android) et [Sources inconnues](https://docs.microsoft.com/intune-user-help/you-need-to-turn-off-unknown-sources-android). 
  <!--1583480-->    


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

- **Actions en cas de non-conformité**    
  Vous pouvez désormais configurer une séquence chronologique d’actions appliquées aux appareils qui ne sont pas conformes. Par exemple, vous pouvez notifier les utilisateurs d’appareils non conformes par e-mail ou marquer ces appareils comme non conformes. Pour plus d’informations, consultez [Configurer des actions en cas de non-conformité](/sccm/mdm/deploy-use/actions-for-noncompliance).
  <!--1321366 -->

- **Nouveaux paramètres de stratégie de gestion des applications mobiles**     
  Les paramètres suivants ont été ajoutés aux paramètres de stratégie de gestion des applications mobiles :
  - **Désactiver la synchronisation des contacts :** empêche l’application d’enregistrer des données sur l’application Contacts native de l’appareil.
  - **Désactiver l’impression :** empêche l’application d’imprimer des données scolaires ou de travail.
  <!-- 1324760 -->    

  Consultez [Protéger les applications à l’aide des stratégies de protection des applications de Configuration Manager](/sccm/mdm/deploy-use/protect-apps-using-mam-policies) pour essayer de nouveaux paramètres de stratégie de protection d’application.

- **Prise en charge des appareils Windows 10 ARM64**     
  Les scénarios de gestion hybride des appareils mobiles sont pris en charge sur les appareils ARM64 exécutant Windows 10 quand ces appareils sont disponibles. Pour plus de détails, consultez [Prise en charge des appareils Windows 10 ARM64](/sccm/core/plan-design/changes/whats-new-in-version-1710#windows-10-arm64-device-support).
  <!-- 1355000 -->    

- **Expérience de profil VPN améliorée dans la console Configuration Manager**     
  Avec cette version, nous avons mis à jour l’Assistant Création d’un profil VPN et les pages de propriétés pour afficher uniquement les paramètres propres à la plateforme sélectionnée. Cette fonctionnalité était précédemment disponible dans Configuration Manager Technical Preview 1709. Elle est désormais disponible dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1710. Pour plus d’informations, consultez [Expérience de profil VPN améliorée dans la console Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Nouveautés de Configuration Manager Technical Preview 1711

- **Nouvelles options des stratégies de conformité pour Windows 10**   
  Vous pouvez maintenant configurer de nouvelles options de stratégie de conformité pour les appareils Windows 10. Les nouveaux paramètres incluent des stratégies pour les éléments suivants : Pare-feu, Contrôle de compte utilisateur, Antivirus Windows Defender et gestion des versions de build OS. Pour plus de détails, consultez [Nouvelles options des stratégies de conformité pour Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Octobre 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Nouveautés de Configuration Manager Technical Preview 1709

- **Expérience de profil VPN améliorée dans la console Configuration Manager**      
  Les paramètres de profil VPN sont désormais filtrés en fonction de la plateforme. Quand vous créez des profils VPN, chaque plateforme prise en charge contient uniquement les paramètres appropriés pour la plateforme. Les profils VPN existants ne sont pas impactés. Pour en savoir plus sur ce changement, cliquez [ici](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1313282 -->


### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune  

- **Rendre vos utilisateurs autonomes avec l’application Portail d’entreprise pour Android**     
  L’application Portail d’entreprise pour Android a ajouté des indications permettant aux utilisateurs finaux de comprendre et, si possible, de résoudre eux-mêmes les nouveaux cas d’usage.
    - Les utilisateurs finaux sont redirigés vers le [portail Azure Active Directory](https://account.activedirectory.windowsazure.com/r/#/profile) pour supprimer un appareil s’ils ont atteint le nombre maximal d’appareils qu’ils sont autorisés à ajouter.
    - Les utilisateurs finaux reçoivent des instructions pour les aider à [corriger les erreurs d’activation sur les appareils Samsung Knox](https://go.microsoft.com/fwlink/?linkid=859718) ou à [désactiver le mode d’économie d’énergie](https://docs.microsoft.com/intune-user-help/power-saving-mode-android). Si aucune de ces solutions ne résout leur problème, nous indiquons comment [envoyer les journaux à Microsoft](https://docs.microsoft.com/intune-user-help/send-logs-to-microsoft-android).
  <!-- 1573324, 1573150, 1558616, 1564878 -->      

- **Indicateur de progression de la connexion dans le Portail d’entreprise Android**    
  L’application Portail d’entreprise pour Android affiche un indicateur de progression du programme d’installation de l’appareil quand un utilisateur inscrit son appareil. L’indicateur affiche de nouveaux états, qui apparaissent dans l’ordre suivant : « Configuration de votre appareil… », « Inscription de votre appareil... », « Fin de l’inscription de votre appareil... », puis « Fin de la configuration de votre appareil... ».  
  <!--1565657-->    

- **Prise en charge de l’authentification basée sur un certificat dans le Portail d’entreprise pour iOS**    
  Nous avons ajouté la prise en charge de l’authentification basée sur un certificat (CBA) dans l’application Portail d’entreprise pour iOS. Les utilisateurs ayant accès à l’authentification CBA entrent leur nom d’utilisateur, puis cliquent sur le lien pour se connecter avec un certificat. L’authentification CBA est déjà prise en charge dans les applications Portail d’entreprise pour Android et Windows. Pour en savoir plus, consultez la page [Comment faire pour se connecter à l’application Portail d’entreprise ?](https://docs.microsoft.com/intune-user-help/sign-in-to-the-company-portal)
  <!--1029830-->   

- **Améliorations apportées au workflow de configuration des appareils dans Portail d’entreprise**     
  Nous avons amélioré le workflow de configuration des appareils dans l’application Portail d’entreprise pour Android. La langue est plus conviviale et spécifique à votre entreprise, et nous avons regroupé des écrans quand cela était possible. Vous pouvez voir ces améliorations sur la page [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-october-2-2017).
  <!--1490692-->     

- **Amélioration des indications sur la demande d’accès aux contacts sur les appareils Android**     
  L’application Portail d’entreprise pour Android nécessite souvent que l’utilisateur final accepte l’autorisation pour permettre l’accès des contacts. Si un utilisateur final refuse cet accès, il voit une notification dans l’application l’invitant à autoriser un accès conditionnel. 
  <!--1484985-->     

- **Mise à jour du démarrage sécurisé pour Android**     
  Les utilisateurs finaux d’appareils Android peuvent indiquer la raison de la non-conformité dans l’application Portail d’entreprise. Lorsque cela est possible, cette action leur permet d’accéder directement à l’emplacement approprié dans l’application Paramètres pour résoudre le problème. 
  <!--1490712-->    

- **Notifications Push supplémentaires pour les utilisateurs finaux sur l’application Portail d’entreprise pour Android Oreo**    
  Les utilisateurs finaux voient des notifications supplémentaires leur indiquant si l’application Portail d’entreprise pour Android Oreo effectue des tâches en arrière-plan, par exemple récupérer des stratégies auprès du service Intune. Les notifications améliorent la transparence pour les utilisateurs finaux, qui savent quand le Portail d’entreprise effectue des tâches d’administration sur leur appareil. Cette amélioration fait partie de [l’optimisation générale de l’interface utilisateur du Portail d’entreprise](https://blogs.technet.microsoft.com/intunesupport/2017/08/21/android-8-0-o-behaviour-changes-and-microsoft-intune), et en particulier de l’application Portail d’entreprise pour Android Oreo. 
  <!--1475932 -->     

- **Nouveaux comportements pour l’application Portail d’entreprise pour Android avec des profils professionnels**     
  Quand vous inscrivez un appareil Android for Work avec un profil professionnel, c’est l’application Portail d’entreprise dans le profil professionnel qui effectue les tâches de gestion sur l’appareil. 

  À moins que vous n’utilisiez une application GAM dans le profil personnel, l’application Portail d’entreprise pour Android n’a plus d’utilité. Pour améliorer l’expérience de profil professionnel, Intune masque automatiquement l’application Portail d’entreprise personnelle après une inscription de profil professionnel réussie.

  L’application Portail d’entreprise pour Android peut être activée à tout moment dans le profil personnel en recherchant [Portail d’entreprise dans le Play Store](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal) et en appuyant sur **Activer**.
  <!--1485783-->    

- **Portail d’entreprise pour Windows 8.1 et Windows Phone 8.1 désormais simplement maintenu**    
  Une notification a été ajoutée pour annoncer que les applications Portail d’entreprise pour Windows 8.1 et Windows Phone 8.1 seront désormais simplement maintenues. Pour plus d’informations, consultez [Notifications](#notices).  
  <!--1428681-->    

- **Empêcher l’inscription des appareils Samsung Knox non pris en charge**   
  L’application Portail d’entreprise tente uniquement d’inscrire des appareils Samsung Knox pris en charge. Pour éviter les erreurs d’activation KNOX qui empêchent l’inscription MDM, l’inscription d’un appareil est uniquement tentée si l’appareil figure dans la [liste des périphériques publiée par Samsung](https://www.samsungknox.com/knox-supported-devices/knox-workspace). Certains appareils Samsung peuvent avoir des numéros de modèle prenant en charge KNOX, mais pas tous. Vérifiez la compatibilité de votre appareil avec Knox auprès de votre revendeur avant de l’acheter et de le déployer. Vous trouverez la liste complète des périphériques vérifiés dans les [paramètres de stratégie Android et Samsung KNOX Standard](https://docs.microsoft.com/intune-classic/deploy-use/android-policy-settings-in-microsoft-intune#supported-samsung-knox-standard-devices).
  <!-- 1490695 -->     

- **Fin du support pour Android 4.3 et versions antérieures**     
  Une notification a été ajoutée concernant la fin du support pour Android 4.3 et versions antérieures. Pour plus d’informations, consultez [Notifications](#notices).
  <!--1171126, 1326920 -->     

- **Informer les utilisateurs finaux au sujet des informations sur les appareils inscrits qui sont consultables**     
  Nous sommes en train d’ajouter le **Type de propriété** à l’écran Détails de l’appareil sur toutes les applications Portail d’entreprise. Ces informations permettent aux utilisateurs d’en savoir plus sur la confidentialité directement à partir de l’article [Quelles informations mon entreprise peut-elle voir quand j’inscris mon appareil ?](https://docs.microsoft.com/intune-user-help/what-info-can-your-company-see-when-you-enroll-your-device-in-intune). Cette amélioration sera introduite dans toutes les applications Portail d’entreprise dans un futur proche. Nous avons annoncé cette fonctionnalité pour iOS en [septembre](https://docs.microsoft.com/intune/whats-new#week-of-september-11-2017). 
  <!--1165314-->     



## <a name="september-2017"></a>Septembre 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune     

- **Actualiser l’action ajoutée à l’application Portail d’entreprise pour Windows 10**    
    L’application Portail d’entreprise pour Windows 10 permet aux utilisateurs d’actualiser les données dans l’application d’un geste vers le bas, ou via la touche F5 pour les ordinateurs de bureau.
    <!-- 1132468 -->     

- **Informer les utilisateurs finaux au sujet des informations sur les appareils qui sont consultables pour iOS**   
    Nous avons ajouté le **Type de propriété** à l’écran Détails de l’appareil sur l’application Portail d’entreprise pour iOS. Ces informations permettent aux utilisateurs d’en savoir plus sur la confidentialité directement à partir de la documentation utilisateur Intune. Les utilisateurs peuvent également ces informations sur l’écran À propos de. 
    <!--739894-->    

- **Formulations plus claires dans l’application Portail d’entreprise pour Android**   
    Le processus d’inscription des utilisateurs finaux sur l’application Portail d’entreprise pour Android a été simplifié grâce à de nouveaux textes. Si vous disposez d’une documentation personnalisée sur l’inscription, mettez-la à jour pour voir les nouveaux écrans. Vous trouverez des exemples d’images sur notre page [Mises à jour de l’interface utilisateur des applications Intune pour utilisateur final](https://docs.microsoft.com/intune/whats-new-app-ui#week-of-september-11-2017).
    <!---1396349-->    

- **Application Portail d’entreprise Windows 10 ajoutée à la stratégie d’autorisation Protection des informations Windows**    
    L’application Portail d’entreprise Windows 10 a été mise à jour pour prendre en charge la Protection des informations Windows. L’application peut être ajoutée à la stratégie d’autorisation Protection des informations Windows. Avec cette modification, il n’est plus nécessaire d’ajouter l’application à la liste **Exempt**. 

    Un seul élément de configuration de Protection des informations Windows peut être remis à un appareil. Si deux éléments de configuration de Protection des informations Windows ciblent le même appareil, aucune stratégie de Protection des informations Windows n’est appliquée.
    <!-- 677129 -->    

- **Information préalable de fin du support ajoutée pour iOS 8.0**    
    Une notification a été ajoutée au sujet de la fin du support d’iOS 8.0. Pour plus d’informations, consultez [Notifications](#notices).



## <a name="august-2017"></a>Août 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune     

- **Nouvelle expérience pour les utilisateurs connectés du Portail d’entreprise Android et de la stratégie App Protection**    
  Les utilisateurs peuvent maintenant parcourir les applications, gérer les appareils et consulter les coordonnées du service informatique sur l’application du Portail d’entreprise Android sans inscrire leurs appareils Android. En outre, s’ils utilisent déjà une application protégée par les stratégies Intune App Protection et lancent le Portail d’entreprise Android, ils ne sont plus invités à inscrire l’appareil.
  <!-- 621669 -->



## <a name="notices"></a>Remarques

### <a name="plan-for-change-use-intune-on-azure-now-for-your-mdm-management"></a>Modification planifiée : utilisez désormais Intune sur Azure pour votre gestion des appareils mobiles 
<!--1227338--> Il y plus d’un an, nous annoncions la [préversion publique d’Intune sur Azure](https://cloudblogs.microsoft.com/enterprisemobility/2016/12/07/public-preview-of-intune-on-azure/), puis il y a six mois la [disponibilité générale de la nouvelle expérience administrateur](https://cloudblogs.microsoft.com/enterprisemobility/2017/06/08/the-new-intune-and-conditional-access-admin-consoles-are-ga/) pour Intune. Depuis le 31 août 2018, nous avons désactivé la gestion des appareils mobiles (MDM) dans la console Silverlight classique pour les clients qui utilisent la version autonome d’Intune. Utilisez plutôt [Intune sur Azure](https://aka.ms/Intune_on_Azure) pour vos besoins de gestion des appareils mobiles. Si vous utilisez toujours la console classique pour la gestion des appareils mobiles, arrêtez-vous et familiarisez-vous avec Intune sur Azure. Cette modification ne devrait avoir aucun impact pour l’utilisateur final. La gestion PC classique avec Intune s’effectuera toujours dans Silverlight. Pour plus d’informations, voir le [billet de blog de l’équipe du support Intune](https://aka.ms/Intune_on_Azure_mdm).


### <a name="plan-for-change-upcoming-macos-and-intune-password-enforcement-change"></a>Changement à venir : nouveau paramètre de changement de mot de passe macOS dans Intune
<!--1873216--> Dans la version de septembre du service, Intune prévoit d’intégrer le nouveau paramètre Apple de changement de mot de passe à la prochaine authentification sur les appareils exécutant les versions macOS 10.13 et ultérieures. Sans l’introduction de ce paramètre, les fournisseurs MDM ne peuvent pas vérifier que le code secret de l’appareil a bien été changé conformément aux exigences de sécurité. Jusqu’à présent, les stratégies de configuration et de conformité d’Intune vérifiaient uniquement que le mot de passe qui était changé sur un appareil était marqué comme conforme. Du fait de l’ajout de cette nouvelle fonctionnalité Apple, les utilisateurs macOS reçoivent une demande de mise à jour de leur mot de passe, même si celui-ci est déjà conforme.

#### <a name="how-does-this-change-affect-me"></a>Quel est l’impact de ce changement ?
Ce changement a un impact uniquement pour les clients avec une stratégie d’appareil macOS qui utilisent Intune ou une gestion MDM hybride. Maintenant qu’Apple a introduit ce paramètre de changement de mot de passe à la prochaine authentification, Intune peut forcer les utilisateurs à mettre à jour leur mot de passe pour le rendre conforme quand une stratégie de mot de passe est appliquée. Si vous bloquez les ressources d’entreprise tant que l’appareil n’est pas marqué comme conforme, les utilisateurs finaux peuvent se voir refuser l’accès aux ressources d’entreprise (telles que la messagerie ou les sites SharePoint) tant qu’ils ne réinitialisent pas leur mot de passe. À l’avenir, toutes les mises à jour des stratégies de configuration et de conformité des mots de passe forceront les utilisateurs ciblés à mettre à jour leurs mots de passe.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Que faire pour se préparer à ce changement ?
Prévenez votre support technique. Si vous ne souhaitez pas appliquer cette stratégie d’appareil macOS, supprimez votre stratégie macOS existante, ou annulez son attribution. D’après nos études réalisées sur les clients avant d’appliquer ce changement, peu de clients seront impactés. La plupart des utilisateurs finaux mettent à jour leur mot de passe après avoir reçu une demande d’inscription avec un mot de passe, ou de réinitialisation de leur mot de passe pour garantir la conformité.  


### <a name="plan-for-change-intune-moving-to-support-ios-10-and-later-in-september-2018"></a>Modification planifiée : mise à jour d’Intune pour prendre en charge iOS 10 et versions ultérieures en septembre 2018 
<!--2454656-->

Apple prévoit de publier iOS 12 en septembre 2018. Peu après la publication, nous mettrons à jour l’inscription Intune, le Portail d’entreprise et Managed Browser de façon à prendre en charge iOS 10 et versions ultérieures.

#### <a name="how-does-this-change-affect-me"></a>Quel est l’impact de ce changement ?

Les applications mobiles Office 365 étant prises en charge sur iOS 10 et versions ultérieures, il est possible que vous ayez déjà mis à niveau votre système d’exploitation ou vos appareils. Dans ce cas, vous n’êtes pas concerné par cette mise à jour.

Toutefois, si vous utilisez ou souhaitez inscrire l’un des appareils répertoriés ci-dessous, sachez qu’ils prennent uniquement en charge iOS 9 et versions antérieures. Pour continuer à accéder au portail d’entreprise Intune, vous devez mettre à niveau ces appareils en septembre et utiliser des appareils qui prennent en charge iOS 10 ou version ultérieure : 

- iPhone4s
- iPod Touch 
- iPad 2
- iPad (troisième génération)
- iPad Mini (première génération)

À compter du mois de juillet, les appareils inscrits auprès de MDM avec iOS 9 et le portail d’entreprise recevront une invitation de mise à niveau de leur système d’exploitation ou appareil. Si vous utilisez des stratégies de protection des applications, vous pouvez également définir le paramètre d’accès « Exiger une version minimale du système d’exploitation iOS (avertissement seulement) ».  

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Que faire pour se préparer à ce changement ?

Recherchez les appareils ou utilisateurs qui sont concernés dans votre organisation. Dans Intune dans le portail Azure, accédez à **Appareils** > **Tous les appareils** et filtrez par **Système d’exploitation**.  Cliquez sur **Colonnes** pour afficher des détails tels que la version du système d’exploitation. Demandez à vos utilisateurs de mettre à niveau leurs appareils vers une version de système d’exploitation prise en charge avant septembre.


### <a name="plan-for-change-intune-moving-to-tls-12"></a>Modification planifiée : mise à jour d’Intune vers TLS 1.2

À compter du 31 octobre 2018, Intune prendra en charge la version 1.2 du protocole de sécurité TLS (Transport Layer Security) afin de fournir un chiffrement de qualité, de garantir une meilleure sécurisation par défaut de notre service et de s’aligner avec d’autres services Microsoft tels que Microsoft Office 365. Office a publié une communication concernant cette modification dans MC128929.

#### <a name="how-does-this-change-affect-me"></a>Quel est l’impact de ce changement ?

À compter du 31 octobre 2018, Intune ne prendra plus en charge les versions 1.0 et 1.1 du protocole TLS. Toutes les combinaisons client-serveur et navigateur-serveur doivent utiliser TLS version 1.2 afin de garantir une connexion sans problème à Intune. Ce changement impacte les appareils des utilisateurs finaux qui ne sont pas pris en charge par Intune, mais qui reçoivent toujours la stratégie par le biais d’Intune et qui ne peuvent pas utiliser la version 1.2 du protocole TLS. Sont notamment concernés les appareils qui exécutent Android 4.3 et versions antérieures. Pour obtenir la liste des appareils et navigateurs impactés, consultez le lien ci-dessous.

Après le 31 octobre 2018, si vous rencontrez un problème lié à l’utilisation d’une ancienne version de TLS, vous devrez effectuer une mise à jour vers TLS 1.2 ou vers un appareil qui prend en charge TLS 1.2 dans le cadre du processus de résolution.

#### <a name="what-do-i-need-to-do-to-prepare-for-this-change"></a>Que faire pour se préparer à ce changement ?

Nous vous recommandons de supprimer les dépendances TLS 1.0 et 1.1 de manière proactive dans vos environnements, et de désactiver TLS 1.0 et 1.1 au niveau du système d’exploitation dans la mesure du possible. Commencez à planifier votre migration vers TLS 1.2 dès aujourd’hui. Consultez le billet de blog de support ci-dessous pour obtenir la liste des appareils qui ne sont pas pris en charge par Intune aujourd’hui, mais qui peuvent encore recevoir la stratégie et qui ne pourront pas communiquer à l’aide du protocole TLS version 1.2. Vous devrez informer ces utilisateurs qu’ils perdront l’accès aux ressources d’entreprise.

Pour plus d’informations, consultez le billet de blog [Intune moving to TLS 1.2 for encryption](https://blogs.technet.microsoft.com/intunesupport/2018/06/05/intune-moving-to-tls-1-2-for-encryption/).


### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portail d’entreprise pour Windows 8.1 et Windows Phone 8.1 désormais simplement maintenu 
<!--1428681-->
*6 octobre 2017*   
 
Depuis octobre 2017, les applications Portail d’entreprise pour Windows 8.1 et Windows Phone 8.1 sont simplement maintenues. Ce mode signifie que les applications et les scénarios existants, tels que l’inscription et la conformité, continuent d’être pris en charge pour ces plateformes. Ces applications peuvent toujours être téléchargées par le biais des canaux de distribution existants, tels que Microsoft Store. 

Mais une fois qu’elles sont simplement maintenues, ces applications reçoivent uniquement les mises à jour de sécurité critiques. Il n’y aura aucune mise à jour supplémentaire ou nouvelle fonctionnalité disponible pour ces applications. Pour bénéficier des nouvelles fonctionnalités, nous vous recommandons de mettre à jour vos appareils vers Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fin du support d’iOS 8.0 
<!---1164477---> Les applications gérées et l’application Portail d’entreprise pour iOS nécessitent iOS 9.0 ou version ultérieure pour accéder aux ressources de l’entreprise. Les appareils qui ne sont pas mis à jour avant le mois de septembre ne peuvent plus accéder au Portail d’entreprise ou à ces applications. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Rappel relatif au support de la plateforme : le support standard de Windows Phone 8.1 a pris fin le 11 juillet 2017
<!-- 1327781 -->
*11 juillet 2017*

La plateforme Windows Phone 8.1 a atteint la fin du support standard. Le support des PC Windows 8.1 n’est pas affecté.

Il n’y a aucun impact immédiat pour les appareils Windows Phone 8.1 qui sont gérés par le service Intune, y compris les appareils inscrits dans la gestion MDM hybride. Les appareils inscrits continuent de fonctionner. Toutes les stratégies, configurations et applications continuent à fonctionner comme prévu. Remarque : aucune amélioration n’est prévue pour la plateforme Windows Phone 8.1 au sein du service Intune et pour l’application Portail d’entreprise Windows Phone 8.1.

Nous vous recommandons de mettre à niveau les appareils Windows Phone 8.1 éligibles vers Windows 10 Mobile dès que possible.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fin du support pour Android 4.3 et versions antérieures
<!---1171127--->
*6 juillet 2017*

Les applications gérées et l’application Portail d’entreprise pour Android nécessitent Android 4.4 et versions ultérieures accéder aux ressources d’entreprise. Les appareils qui ne sont pas mis à jour avant le début du mois d’octobre ne peuvent plus accéder au Portail d’entreprise ou à ces applications. En décembre, tous les appareils inscrits sont mis hors service, provoquant ainsi la perte de l’accès aux ressources d’entreprise. Si vous utilisez des stratégies de protection d’application sans gestion MDM, les applications ne reçoivent pas les mises à jour, ce qui diminue progressivement la qualité de l’expérience utilisateur.



## <a name="see-also"></a>Voir aussi

- [Anciennes fonctionnalités de gestion des appareils mobiles hybride et remarques](whats-new-hybrid-archive.md)
- [Nouveautés de MDM dans System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
