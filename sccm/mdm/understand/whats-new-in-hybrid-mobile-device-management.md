---
title: Nouveautés de la gestion MDM hybride
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec Configuration Manager et Intune.
ms.date: 05/09/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 7b127cee-61f1-4681-9760-caebed36ddf5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 72aeff7874456c3866ccb658395b8706057bdfaf
ms.sourcegitcommit: 7bec1331c4f3096e6a278ff9ea0e929cff0a9cb9
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/10/2018
---
# <a name="whats-new-in-hybrid-mobile-device-management-with-configuration-manager-and-microsoft-intune"></a>Nouveautés de la gestion hybride des appareils mobiles avec Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article fournit des informations sur les nouvelles fonctionnalités de gestion des appareils mobiles disponibles pour les déploiements hybrides avec System Center Configuration Manager et Microsoft Intune.     

> [!Note]    
> Intune sur Azure est la solution MDM recommandée de Microsoft.     
> - Pour plus d’informations sur les nouvelles fonctionnalités et mises à jour de la version autonome d’Intune, consultez [Nouveautés de Microsoft Intune](https://docs.microsoft.com/intune/whats-new).    
> - Pour plus d’informations sur la procédure de migration vers la version autonome d’Intune, consultez [Migrer appareils et utilisateurs MDM hybrides vers Intune autonome](https://docs.microsoft.com/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa).
> - Pour plus d’informations sur les mises à jour de l’interface utilisateur pour Intune et la gestion MDM hybride, consultez [Mises à jour de l’interface utilisateur pour les applications utilisateur final Intune](https://docs.microsoft.com/intune/whats-new-app-ui). 

##  <a name="compatibility-with-configuration-manager-versions"></a>Compatibilité avec les versions de Configuration Manager  
Chaque section de cet article répertorie les fonctionnalités hybrides sous trois catégories différentes. Utilisez l’aide suivante pour déterminer la compatibilité des fonctionnalités de chaque catégorie avec différentes versions de Configuration Manager :  

|Catégories de fonctionnalités|Description|
|-|-|
|**Nouveautés de Microsoft Intune** | En règle générale, toutes les fonctionnalités listées dans cette catégorie fonctionnent avec chacune des versions de Configuration Manager. Sont notamment comprises les versions de System Center 2012 R2 Configuration Manager, dans la mesure où ces fonctionnalités ont seulement besoin du service Intune, sans aucune fonctionnalité supplémentaire dans Configuration Manager.|
|**Nouveautés de Configuration Manager Technical Preview**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version d’évaluation technique spécifiée. Pour tester ces fonctionnalités, vous devez installer la version d’évaluation technique spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Technical Preview pour System Center Configuration Manager](../../core/get-started/technical-preview.md).|
|**Nouveautés de Configuration Manager (Current Branch)**| Toutes les fonctionnalités répertoriées dans cette catégorie fonctionnent uniquement avec la version spécifiée de Configuration Manager (Current Branch), comme la version 1511 ou 1602. Si vous utilisez une version antérieure de Configuration Manager pour votre déploiement hybride, vous devez effectuer la mise à niveau vers la version de Configuration Manager (Current Branch) spécifiée dans la description de la fonctionnalité. Pour plus d’informations, consultez [Mettre à niveau vers System Center Configuration Manager](../../core/servers/deploy/install/upgrade-to-configuration-manager.md).|



## <a name="may-2018"></a>Mai 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="requesting-help-in-the-company-portal-for-windows-10"></a>Demande d’aide sur l’application Portail d’entreprise pour Windows 10 
<!--1874137-->
Le portail d’entreprise pour Windows 10 envoie maintenant les journaux d’application directement à Microsoft lorsque l’utilisateur démarre le flux de travail permettant d’obtenir de l’aide. Ce comportement facilite la résolution des problèmes qui sont signalés à Microsoft.  


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

#### <a name="support-for-new-versions-of-cisco-anyconnect-client-for-ios"></a>Prise en charge de nouvelles versions du client Cisco AnyConnect pour iOS
<!--1357393-->
Vous pouvez activer la prise en charge de Cisco AnyConnect pour iOS version 4.0.7 ou ultérieure. Si vous le faites, les profils VPN de Cisco AnyConnect existants sont nommés **Cisco Legacy AnyConnect** et continuent de fonctionner comme avant. L’option **Cisco AnyConnect** est pour les nouveaux profils VPN qui fonctionnent avec Cisco AnyConnect sur iOS version 4.0.7 ou ultérieure.

Pour plus d’informations sur l’activation de cette fonctionnalité, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).

> [!Note]  
> Continuez à utiliser l’option **Cisco Legacy AnyConnect** pour les profils VPN macOS. 



## <a name="april-2018"></a>Avril 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="intune-adapts-to-fluent-design-system-in-the-company-portal-app-for-windows-10"></a>Intune s’adapte au système Fluent Design dans l’application Portail d’entreprise pour Windows 10 
<!--1195010-->
La [vue de navigation du système Fluent Design](/windows/uwp/design/basics/navigation-basics) a été ajoutée à l’application Portail d’entreprise pour Windows 10 d’Intune. Sur le côté de l’application, vous voyez la liste statique et verticale de toutes les pages de niveau supérieur. Cliquez sur un lien pour passer rapidement d’une page à l’autre. Cette mise à jour est la première d’une série, destinée à rendre Intune plus souple et plus intuitif. Pour voir à quoi ressemble la mise à jour, consultez [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).

#### <a name="improved-device-tiles-in-the-windows-10-company-portal"></a>Amélioration des vignettes d’appareil dans le portail d’entreprise Windows 10
<!--2213364-->
Les vignettes ont été mises à jour pour être plus accessibles aux utilisateurs malvoyants et plus visibles pour les outils de lecture d’écran.


#### <a name="test-the-company-portal-for-macos-on-virtual-machines"></a>Test du portail d’entreprise pour macOS sur les machines virtuelles
<!--2216679-->
Nous avons publié des conseils pour aider les administrateurs informatiques à tester l’application Portail d’entreprise pour macOS sur des machines virtuelles dans Parallels Desktop et VMware Fusion. Pour plus d’informations, consultez [Inscrire des machines virtuelles macOS pour les tester](/intune/macos-enroll#enroll-virtual-macos-machines-for-testing).


#### <a name="send-diagnostic-reports-in-company-portal-app-for-macos"></a>Envoyer des rapports de diagnostic dans l’application Portail d’entreprise pour macOS
<!--2216677-->
L’application Portail d’entreprise pour les appareils macOS a été mise à jour afin d’améliorer la façon dont les utilisateurs signalent les erreurs relatives à Intune. À partir de l’application Portail d’entreprise, vos collaborateurs peuvent :

- Charger des rapports de diagnostic directement pour l’équipe de développement Microsoft.
- Envoyer par e-mail un ID d’incident à l’équipe du support informatique de votre entreprise.


#### <a name="updated-help-experience-on-company-portal-app-for-android"></a>Mise à jour de l’expérience de l’aide sur l’application Portail d’entreprise pour Android 
<!--1631531-->
Nous avons mis à jour l’expérience de l’aide dans l’application Portail d’entreprise pour Android de façon à l’aligner sur les bonnes pratiques pour la plateforme Android. Quand les utilisateurs rencontrent un problème dans l’application, ils peuvent désormais appuyer sur **Menu** > **Aide** et :
- Charger les journaux de diagnostic à destination de Microsoft.
- Envoyer un e-mail qui décrit le problème et l’ID d’incident à une personne assurant le support dans l’entreprise.


#### <a name="update-where-to-configure-your-app-protection-policies"></a>Changement de l’endroit où vous configurez vos stratégies de protection d’application 
<!--2144597-->
Dans le portail Azure, dans le service Microsoft Intune, nous allons vous rediriger temporairement du panneau du service **Intune App Protection** vers le panneau **Application Mobile**. Notez que toutes vos stratégies de protection d’application sont déjà sur le panneau **Application mobile** dans Intune, sous la configuration de l’application. Au lieu d’accéder à Intune App Protection, vous accédez simplement à Intune. En avril 2018, nous mettrons fin à la redirection et nous la supprimerons complètement du panneau du service **Intune App Protection** : il n’y aura alors plus qu’un seul emplacement pour les stratégies de protection d’application dans Intune. 

**Comment cela m’affecte-t-il ?** Ce changement affecte les clients autonomes et les clients hybrides Intune (Intune avec Configuration Manager). Cette intégration permet de simplifier l’administration de la gestion de votre cloud.

**Que faire pour se préparer à ce changement ?** Déclarez **Intune** comme favori à la place du panneau du service **Intune App Protection** et familiarisez-vous si nécessaire avec le flux de travail de la stratégie de protection d’application dans le panneau **Application mobile** d’Intune. Nous vous redirigerons pendant une courte période de temps, puis nous supprimerons le panneau **App Protection**. Rappelez-vous que toutes les stratégies de protection d’application sont déjà dans Intune et que vous pouvez modifier les stratégies d’accès conditionnel. Pour plus d’informations sur la modification des stratégies d’accès conditionnel, consultez [Accès conditionnel dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). Pour plus d’informations, consultez [Présentation des stratégies de protection d’application](/intune/app-protection-policy) 




#### <a name="user-experience-update-for-the-company-portal-app-for-ios"></a>Mise à jour de l’expérience utilisateur de l’application Portail d’entreprise pour iOS 
<!--1412866-->
Nous avons publié une mise à jour majeure de l’expérience utilisateur de l’application Portail d’entreprise pour iOS. La mise à jour présente une toute nouvelle conception visuelle qui offre une apparence actualisée. Nous avons conservé les fonctionnalités de l’application, mais amélioré sa facilité d’utilisation et son accessibilité.  

Vous verrez également :
- Une prise en charge de l’iPhone X.
- Un lancement des applications et un chargement des réponses plus rapides pour faire gagner du temps aux utilisateurs.
- Des barres de progression supplémentaires pour fournir aux utilisateurs les informations d’état les plus à jour.
- Une amélioration du chargement des journaux pour signaler plus facilement les problèmes.  

Pour voir à quoi ressemble la mise à jour, consultez [Nouveautés de l’interface utilisateur de l’application](/intune/whats-new-app-ui).



## <a name="march-2018"></a>Mars 2018

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

#### <a name="windows-company-portal-send-feedback-option-may-no-longer-work"></a>L’option Envoyer des commentaires du portail d’entreprise Windows risque de ne plus fonctionner
<!--2070166-->
L’application Portail d’entreprise Windows dispose d’une option « Envoyer des commentaires » permettant aux utilisateurs d’envoyer des commentaires sur l’application à Microsoft. À compter du 30 avril 2018, cette option continue d’être prise en charge uniquement sur l’application Portail d’entreprise Windows 10 s’exécutant sur Windows 10 versions 1607 et ultérieures.   

**Comment cela m’affecte-t-il ?**

Si l’application Portail d’entreprise Windows n’est pas installée pour les utilisateurs finaux, ignorez ce message.

Si certains de vos utilisateurs finaux disposent de l’application Portail d’entreprise, notez qu’à compter du 30 avril, le bouton « Envoyer des commentaires » ne fonctionnera plus pour l’application dans les cas suivants :  

 - Application Portail d’entreprise Windows 10 sur Windows 10 version 1507 et version 1511  

 - Application Portail d’entreprise Windows Phone 8.1  

Pour les appareils concernés, l’option « Envoyer des commentaires » échoue, même lors des nouvelles tentatives. Pour envoyer des commentaires à Microsoft concernant les expériences sur ces plateformes, il existe d’autres canaux de retour répertoriés ci-dessous.

**Que faire pour se préparer à ce changement ?**

Informez vos utilisateurs finaux de ce changement et mettez à jour toutes les instructions destinées aux utilisateurs, si nécessaire. 

Informez les utilisateurs finaux qui se servent du portail d’entreprise sur Windows Phone 8.1, Windows 10 version 1507 et Windows 10 version 1511 que deux autres canaux de retour sont disponibles. Ils peuvent :  

- Utiliser l’application Hub de commentaire sur Windows 10  
- Envoyer un e-mail à WinCPfeedback@microsoft.com  

Demandez aux utilisateurs finaux sur Windows 10 versions 1607 ou ultérieures d’effectuer une mise à jour vers la dernière version du portail d’entreprise Windows disponible dans le Microsoft Store.



#### <a name="azure-active-directory-web-sites-can-require-the-intune-managed-browser-app-and-support-single-sign-on-for-the-managed-browser-public-preview"></a>Les sites web Azure Active Directory peuvent nécessiter l’application Intune Managed Browser et prendre en charge l’authentification unique pour Managed Browser (Préversion publique)
<!-- 710595 --> 
Avec Azure Active Directory (Azure AD), vous pouvez maintenant restreindre l’accès aux sites web à l’application Intune Managed Browser sur les appareils mobiles. Dans Managed Browser, les données de site web restent sécurisées et séparées des données personnelles de l’utilisateur final. De plus, Managed Browser prend en charge les fonctionnalités d’authentification unique pour les sites protégés par Azure AD. La connexion à Managed Browser ou l’utilisation de Managed Browser sur un appareil avec une autre application gérée par Intune permet à Managed Browser d’accéder à des sites d’entreprise protégés par Azure AD sans que l’utilisateur ait à entrer ses informations d’identification. Cette fonctionnalité s’applique à des sites comme Outlook Web Access (OWA) et SharePoint Online, ainsi qu’à d’autres sites d’entreprise comme les ressources intranet accessibles via le proxy d’application Azure.



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
  À compter de cette version, vous devez configurer et gérer vos stratégies d’accès conditionnel dans le [portail Azure](https://portal.azure.com) à partir d’**Azure Active Directory** > **Accès conditionnel**. Par souci pratique, vous pouvez également accéder à ce panneau à partir d’Intune dans le portail Azure (**Intune** > **Accès conditionnel**).
  <!-- 1737088 1634311 --> 

- **E-mails de mises à jour de conformité**    
  Quand un e-mail est envoyé pour signaler un appareil non conforme, des détails sur l’appareil non conformes sont inclus. 
  <!--1637547 -->

- **Nouvelles fonctionnalités de l’action « Résoudre » pour les appareils Android**    
  L’application Portail d’entreprise pour Android étend l’action « Résoudre » sur **Mettre à jour les paramètres d’appareil** afin de résoudre les [problèmes de chiffrement d’appareil](https://docs.microsoft.com/intune-user-help/encrypt-your-device-android).
  <!--1583480-->

- **Verrouillage à distance disponible dans l’application Portail d’entreprise pour Windows 10**    
  Les utilisateurs finaux peuvent désormais verrouiller à distance leurs appareils à partir de l’application Portail d’entreprise pour Windows 10. Cette action ne s’affiche pas pour l’appareil local qu’ils utilisent de manière active.
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
  L’application Microsoft Planner pour iOS et Android fait désormais partie des applications approuvées pour la gestion des applications mobiles (MAM). Configurez l’application par le biais du panneau Intune App Protection dans le portail Azure de tous les locataires. Pour plus de détails, consultez [Liste GAM d’applications approuvées](https://www.microsoft.com/cloud-platform/microsoft-intune-apps).
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
  Avec cette version, nous avons mis à jour l’Assistant Création d’un profil VPN et les pages de propriétés pour afficher uniquement les paramètres appropriés à la plateforme sélectionnée. Cette fonctionnalité était précédemment disponible dans Configuration Manager Technical Preview 1709. Elle est désormais disponible dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1710. Pour plus d’informations, consultez [Expérience de profil VPN améliorée dans la console Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1710#improved-vpn-profile-experience-in-configuration-manager-console).
  <!-- 1318232 -->


### <a name="new-in-configuration-manger-technical-preview-1711"></a>Nouveautés de Configuration Manager Technical Preview 1711

- **Nouvelles options des stratégies de conformité pour Windows 10**   
  Vous pouvez maintenant configurer de nouvelles options de stratégie de conformité pour les appareils Windows 10. Les nouveaux paramètres incluent des stratégies pour les éléments suivants : Pare-feu, Contrôle de compte utilisateur, Antivirus Windows Defender et gestion des versions de build OS. Pour plus de détails, consultez [Nouvelles options des stratégies de conformité pour Windows 10](/sccm/core/get-started/capabilities-in-technical-preview-1711#new-compliance-policy-options-for-windows-10).



## <a name="october-2017"></a>Octobre 2017

### <a name="new-in-configuration-manager-technical-preview-1709"></a>Nouveautés de Configuration Manager Technical Preview 1709

- **Expérience de profil VPN améliorée dans la console Configuration Manager**      
  Les paramètres de profil VPN sont désormais filtrés en fonction de la plateforme. Quand vous créez des profils VPN, chaque plateforme prise en charge contient uniquement les paramètres appropriés pour la plateforme. Les profils VPN existants ne sont pas affectés. Pour en savoir plus sur ce changement, cliquez [ici](/sccm/core/get-started/capabilities-in-technical-preview-1709#improved-vpn-profile-experience-in-configuration-manager-console).
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



## <a name="july-2017"></a>Juillet 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Notifications de fin de support ajoutées pour Android et Windows Phone**    
    De nouvelles informations préalables ont été ajoutées concernant la fin du support des versions Android et Windows Phone. Pour plus d’informations, consultez [Notifications](#notices).


### <a name="new-in-configuration-manager-current-branch"></a>Nouveautés de Configuration Manager (Current Branch)

Les fonctionnalités suivantes étaient précédemment disponibles dans les versions Configuration Manager Technical Preview. Ces fonctionnalités sont désormais disponibles dans les déploiements hybrides avec Intune et Configuration Manager (Current Branch) version 1706.

- [Prise en charge d’Entrust pour les autorités de certification Entrust](/sccm/core/get-started/capabilities-in-technical-preview-1706#support-for-entrust-certification-authorities)
- [Nouveaux paramètres de stratégie de gestion d’application mobile](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-mobile-application-management-policy-settings)
- [Mises à jour apportées à la configuration de partage Android for Work](/sccm/core/plan-design/changes/whats-new-in-version-1706#updates-to-android-for-work-sharing-configuration)
- [Créer une stratégie de conformité des appareils](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-device-compliance-policy-rules)
- [Nouveaux paramètres de configuration pour les appareils Windows 10 qui ne sont pas gérés avec le client Configuration Manager](/sccm/core/plan-design/changes/whats-new-in-version-1706#new-configuration-settings-for-windows-10-devices-that-are-not-managed-with-the-configuration-manager-client)
- [Prise en charge de Cisco (IPsec) pour les profils VPN macOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#cisco-ipsec-support-for-macos-vpn-profiles)
- [Restrictions d’inscription Android et iOS](/sccm/core/plan-design/changes/whats-new-in-version-1706#android-and-ios-enrollment-restrictions) 



## <a name="june-2017"></a>Juin 2017

### <a name="new-in-microsoft-intune"></a>Nouveautés de Microsoft Intune

- **Changer d’autorité MDM**    
  À compter de Configuration Manager version 1610, vous pouvez modifier votre autorité MDM sans avoir à contacter le Support Microsoft. Vous n’avez pas à annuler l’inscription de vos appareils gérés existants et les réinscrire. Pour plus d’informations, consultez [Changer d’autorité MDM](/sccm/mdm/deploy-use/change-mdm-authority).

- **Intégration de Managed Browser avec le proxy d’application**    
  Intune Managed Browser peut à présent s’intégrer avec le service de proxy d’application Azure AD pour permettre aux utilisateurs d’accéder aux sites web internes, même quand ils travaillent à distance. Les utilisateurs du navigateur entrent l’URL du site comme d’habitude, et Managed Browser achemine la demande via la passerelle web du proxy d’application. Pour plus d’informations, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](https://docs.microsoft.com/intune/app-configuration-managed-browser).

- **L’application Portail d’entreprise pour Android a maintenant une nouvelle expérience utilisateur final pour les stratégies de protection d’application**  
  Sur la base des retours des clients, nous avons modifié l’application de portail d’entreprise pour Android afin d’afficher un bouton **Accéder au contenu de l’entreprise**. L’objectif est d’empêcher les utilisateurs finaux d’avoir à passer par le processus d’inscription lorsqu’ils ont seulement besoin d’accéder aux applications qui prennent en charge les stratégies de protection des applications, une fonctionnalité de gestion des applications mobiles d’Intune. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nouvelle action de menu pour supprimer facilement le portail d’entreprise**  
  Sur la base des retours des utilisateurs, l’application de portail d’entreprise pour Android dispose désormais d’une nouvelle action de menu pour initier la suppression du portail d’entreprise à partir de votre appareil. Cette action supprime l’appareil de gestion Intune afin que l’application puisse être supprimée de l’appareil par l’utilisateur. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui) et dans la [documentation utilisateur d’Android](https://docs.microsoft.com/intune-user-help/unenroll-your-device-from-intune-android).

- **Améliorations apportées à la synchronisation des applications avec Windows 10 Creators Update**  
  L’application Portail d’entreprise pour Windows 10 lance désormais automatiquement une synchronisation pour les demandes d’installation d’application pour les appareils avec Windows 10 Creators Update (version 1703). Ce comportement permet de réduire le problème des installations d’application bloquées lorsque l’état est « En attente de synchronisation ». En outre, les utilisateurs peuvent lancer manuellement une synchronisation à partir de l’application. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Nouvelle expérience interactive pour le portail d’entreprise Windows 10**  
  L’application du Portail d’entreprise pour Windows 10 comprend une expérience guidée pas à pas d’Intune pour les appareils non identifiés ni inscrits. La nouvelle expérience fournit des instructions pas à pas qui guident l’utilisateur lors de l’inscription dans Azure Active Directory (obligatoire pour les fonctionnalités d’accès conditionnel) et l’inscription à la gestion des appareils mobiles (requis pour les fonctionnalités de gestion d’appareils). L’expérience interactive est accessible à partir de la page d’accueil du Portail d’entreprise. Les utilisateurs peuvent continuer à utiliser l’application s’ils ne terminent pas l’inscription, mais seront confrontés à des fonctionnalités limitées.

  Cette mise à jour est uniquement visible sur les appareils exécutant la Mise à jour anniversaire Windows 10 (build 1607) ou une version ultérieure. Vous pouvez voir ces modifications sur la page [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Améliorations pour les mosaïques de l’application dans l’application de portail d’entreprise pour iOS**  
  Nous avons mis à jour le design des mosaïques d’application sur la page d’accueil afin de refléter la couleur de personnalisation que vous définissez pour le portail d’entreprise. Pour plus d’informations, consultez [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui).

- **Le sélecteur de compte est désormais disponible pour l’application de portail d’entreprise pour iOS**  
  Les utilisateurs d’appareils iOS peuvent voir notre nouveau sélecteur de compte lorsqu’ils se connectent au Portail d’entreprise s’ils utilisent leur compte scolaire ou de travail pour se connecter aux autres applications Microsoft. Pour plus d’informations, consultez [Nouveautés de l’interface utilisateur de l’application](https://docs.microsoft.com/intune/whats-new-app-ui).

### <a name="new-in-configuration-manager-technical-preview-1706"></a>Nouveautés de Configuration Manager Technical Preview 1706

- **Nouveaux paramètres d’élément de configuration Windows**      
  De nouveaux éléments de configuration de Windows sont disponibles pour les catégories Paramètres, Appareil, Store et Microsoft Edge. Pour plus d’informations, consultez [Nouveaux paramètres d’élément de configuration Windows](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-windows-configuration-item-settings).
  <!-- 1354715 -->

- **Nouvelles règles de stratégie de conformité d’appareil**   
  Vous pouvez maintenant configurer de nouvelles options pour les stratégies de conformité qui étaient auparavant disponibles uniquement dans la version autonome d’Intune. Pour plus de détails, consultez les [Améliorations apportées aux stratégies de conformité des appareils](/sccm/core/get-started/capabilities-in-technical-preview-1706#new-device-compliance-policy-rules).

- **Restrictions d’inscription Android et iOS**       
  Les administrateurs peuvent désormais spécifier que les utilisateurs ne peuvent pas inscrire des appareils Android ou iOS personnels dans leur environnement hybride. Cette action vous permet de limiter les appareils inscrits aux appareils prédéclarés, appareils d’entreprise ou appareils iOS inscrits avec le programme d’inscription des appareils. Pour plus d’informations, consultez [Restrictions de l’inscription Android et iOS](/sccm/core/get-started/capabilities-in-technical-preview-1706#android-and-ios-enrollment-restrictions).
  <!-- 1290826 -->

- **Prise en charge des autorités de certification Entrust**      
  Configuration Manager prend désormais en charge les autorités de certification Entrust. Cette prise en charge permet la remise du certificat PFX aux appareils inscrits dans Microsoft Intune.    
  <!-- 1350740 -->

  Vous pouvez configurer Entrust en tant qu’autorité de certification lors de l’ajout d’un rôle de point d’enregistrement de certificat dans Configuration Manager. Lorsque vous ajoutez un nouveau profil de certificat qui émet des certificats PFX, vous pouvez sélectionner une autorité de certification Microsoft ou Entrust.

  **Problème connu** : dans la Technical Preview 1706, les certificats PFX ne sont pas émis pour les autorités de certification Microsoft. Ce problème n’affecte pas les certificats PFX importés ou les profils SCEP.

- **Prise en charge de Cisco (IPsec) pour les profils VPN macOS**      
  Vous pouvez créer un profil VPN macOS avec Cisco (IPsec) comme type de connexion. Pour plus d’informations, consultez [Créer des profils VPN](/sccm/mdm/deploy-use/create-vpn-profiles#create-vpn-profiles).
  <!-- 1321367 -->


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

  - Couleurs : les en-têtes des onglets du portail d’entreprise sont de la couleur définie dans la personnalisation.
  - Applications : dans l’onglet **Applications**, les boutons **Applications à la une** et **Toutes les applications** ont été mis à jour.
  - Rechercher : Dans l’onglet **Applications**, le bouton **Rechercher** est un bouton d’action flottant.
  - Navigation dans les applications : la vue **Toutes les applications** montre une vue à onglets avec **À la une**, **Toutes** et **Catégories** pour faciliter la navigation.
  - Prise en charge : les onglets **Mes appareils** et **Contacter le service informatique** ont été mis à jour de façon à améliorer la lisibilité.

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



## <a name="notices"></a>Remarques

### <a name="company-portal-for-windows-81-and-windows-phone-81-moving-to-sustaining-mode"></a>Portail d’entreprise pour Windows 8.1 et Windows Phone 8.1 désormais simplement maintenu 
<!--1428681-->
*6 octobre 2017*   
 
Depuis octobre 2017, les applications Portail d’entreprise pour Windows 8.1 et Windows Phone 8.1 sont simplement maintenues. Ce mode signifie que les applications et les scénarios existants, tels que l’inscription et la conformité, continuent d’être pris en charge pour ces plateformes. Ces applications peuvent toujours être téléchargées par le biais des canaux de distribution existants, tels que Microsoft Store. 

Mais une fois qu’elles sont simplement maintenues, ces applications reçoivent uniquement les mises à jour de sécurité critiques. Il n’y aura aucune mise à jour supplémentaire ou nouvelle fonctionnalité disponible pour ces applications. Pour bénéficier des nouvelles fonctionnalités, nous vous recommandons de mettre à jour vos appareils vers Windows 10 ou Windows 10 Mobile. 

### <a name="end-of-support-for-ios-80"></a>Fin du support d’iOS 8.0 
<!---1164477--->
Les applications gérées et l’application Portail d’entreprise pour iOS nécessitent iOS 9.0 ou une version ultérieure pour accéder aux ressources de l’entreprise. Les appareils qui ne sont pas mis à jour avant le mois de septembre ne peuvent plus accéder au Portail d’entreprise ou à ces applications. 

### <a name="platform-support-reminder-windows-phone-81-mainstream-support-ended-july-11-2017"></a>Rappel relatif au support de la plateforme : le support standard de Windows Phone 8.1 a pris fin le 11 juillet 2017
<!-- 1327781 -->
*11 juillet 2017*

La plateforme Windows Phone 8.1 a atteint la fin du support standard. Le support des PC Windows 8.1 n’est pas affecté.

Il n’y a aucun impact immédiat sur les appareils Windows Phone 8.1 gérés par le service Intune, y compris les appareils inscrits à la gestion des appareils mobiles (MDM) hybride. Les appareils inscrits continuent de fonctionner. Toutes les stratégies, configurations et applications continuent à fonctionner comme prévu. Remarque : aucune amélioration n’est prévue pour la plateforme Windows Phone 8.1 au sein du service Intune et pour l’application Portail d’entreprise Windows Phone 8.1.

Nous vous recommandons de mettre à niveau les appareils Windows Phone 8.1 éligibles vers Windows 10 Mobile dès que possible.  

### <a name="end-of-support-for-android-43-and-lower"></a>Fin du support pour Android 4.3 et versions antérieures
<!---1171127--->
*6 juillet 2017*

Les applications gérées et l’application Portail d’entreprise pour Android nécessitent Android 4.4 et versions ultérieures accéder aux ressources d’entreprise. Les appareils qui ne sont pas mis à jour avant le début du mois d’octobre ne peuvent plus accéder au Portail d’entreprise ou à ces applications. En décembre, tous les appareils inscrits sont mis hors service, provoquant ainsi la perte de l’accès aux ressources d’entreprise. Si vous utilisez des stratégies de protection d’application sans la Gestion des données de référence, les applications ne reçoivent pas de mises à jour et la qualité de l’expérience diminue avec le temps.



## <a name="see-also"></a>Voir aussi

- [Anciennes fonctionnalités de gestion des appareils mobiles hybride et remarques](whats-new-hybrid-archive.md)
- [Nouveautés de MDM dans System Center 2012 Configuration Manager](https://technet.microsoft.com/library/mt445560.aspx)
