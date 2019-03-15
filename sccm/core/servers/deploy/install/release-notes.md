---
title: Notes de publication
titleSuffix: Configuration Manager
description: Découvrez plus en détail les problèmes urgents qui ne sont pas encore résolus dans le produit ni traités dans un article de la base de connaissances Support Microsoft.
ms.date: 03/05/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33ef7020e1b9312717919a9dda8ce189c8db533c
ms.sourcegitcommit: f3dd8405018fe1043434386be15c16752c1a4a3c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57558182"
---
# <a name="release-notes-for-configuration-manager"></a>Notes de publication de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec Configuration Manager, les notes de publication de produit se limitent aux problèmes urgents. Ces problèmes ne sont pas encore résolus dans le produit ni traités dans un article de la base de connaissances Support Microsoft.  

La documentation spécifique aux fonctionnalités inclut des informations sur les problèmes connus qui affectent les scénarios de base.  

Cette rubrique contient les notes de publication pour l’édition actuelle de Configuration Manager. Pour plus d’informations sur la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).  

Pour plus d’informations sur les nouvelles fonctionnalités introduites dans les différentes versions, consultez les articles suivants :
- [Nouveautés de la version 1810](/sccm/core/plan-design/changes/whats-new-in-version-1810)
- [Nouveautés de la version 1806](/sccm/core/plan-design/changes/whats-new-in-version-1806)  
- [Nouveautés de la version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)

> [!Tip]  
> Pour recevoir une notification en cas de mise à jour de cette page, copiez et collez l’URL suivante dans votre lecteur de flux RSS : `https://docs.microsoft.com/api/search/rss?search=%22release+notes+-+Configuration+Manager%22&locale=en-us`



## <a name="set-up-and-upgrade"></a>Installer et mettre à niveau  


### <a name="when-using-redistributable-files-from-the-cdlatest-folder-setup-fails-with-a-manifest-verification-error"></a>Lors de l’utilisation de fichiers redistribuables à partir du dossier CD.Latest, le programme d’installation échoue avec une erreur de vérification du manifeste
<!-- 510080, 490569  -->

Quand vous exécutez le programme d’installation à partir du dossier CD.Latest créé pour la version 1606 et que vous utilisez les fichiers redistribuables fournis avec ce dossier CD.Latest, le programme d’installation échoue avec les erreurs suivantes dans le journal d’installation de Configuration Manager :

  `ERROR: File hash check failed for defaultcategories.dll`  
  `ERROR: Manifest verification failed. Wrong version of manifest?`

#### <a name="workaround"></a>Solution de contournement
Utilisez l’une des options suivantes :
 - Pendant l’installation, choisissez de télécharger les fichiers redistribuables de Microsoft les plus récents. Utilisez les fichiers redistribuables les plus récents à la place des fichiers inclus dans le dossier CD.Latest.
 - Supprimez manuellement le dossier *cd.latest\redist\languagepack\zhh*, puis réexécutez le programme d’installation.


### <a name="setup-command-line-option-joinceip-must-be-specified"></a>L’option de la ligne de commande du programme d’installation JoinCEIP doit être spécifiée
<!--510806-->
*S’applique à : Configuration Manager version 1802*

Depuis Configuration Manager version 1802, la fonctionnalité du programme d’amélioration de l’expérience utilisateur (CEIP) ne figure plus dans le produit. Lors de [l’automatisation de l’installation](/sccm/core/servers/deploy/install/command-line-options-for-setup) d’un nouveau site à partir d’un script de ligne de commande ou sans assistance, le programme d’installation retourne une erreur indiquant qu’un paramètre requis est manquant. 

#### <a name="workaround"></a>Solution de contournement
Alors qu’il n’a aucun effet sur le résultat du processus d’installation, incluez le paramètre **JoinCEIP** dans la ligne de commande de l’installation.

 > [!Note]  
 > Le paramètre EnableSQM pour [l’installation de la console](/sccm/core/servers/deploy/install/install-consoles) n’est pas obligatoire.


### <a name="cloud-service-manager-component-stopped-on-site-server-in-passive-mode"></a>Composant de gestionnaire de service cloud arrêté sur le serveur de site en mode passif
<!--VSO 2858826, SCCMDocs issue 772-->
*S’applique à : Configuration Manager version 1806*

Si le [point de connexion de service](/sccm/core/servers/deploy/configure/about-the-service-connection-point) coexiste avec un [serveur de site en mode passif](/sccm/core/servers/deploy/configure/site-server-high-availability), le déploiement et la surveillance d’une [passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) ne démarrent pas. Le composant de gestionnaire de service cloud (SMS_CLOUD_SERVICES_MANAGER) est dans un état arrêté.

#### <a name="workaround"></a>Solution de contournement
Déplacez le rôle de point de connexion de service vers un autre serveur.



<!-- ## Backup and recovery  -->


<!--## Client deployment and upgrade-->



## <a name="os-deployment"></a>Déploiement de système d’exploitation

### <a name="after-passive-site-server-is-promoted-the-default-boot-image-packages-still-have-package-source-on-the-previous-active-server"></a>Une fois que le serveur de site en mode passif est promu, les packages d’images de démarrage par défaut conservent la source du package sur le serveur actif précédent
<!--3453224, SCCMDocs-pr issue 3097-->
*S’applique à : Configuration Manager version 1810*

Si vous avez un serveur de site en mode passif (serveur B) et que vous le promouvez à l’état actif, l’emplacement du contenu des images de démarrage par défaut continue à référencer le serveur précédemment actif (serveur A). Si le serveur A subit une défaillance matérielle, vous ne pouvez pas mettre à jour ni changer les images de démarrage par défaut.

#### <a name="workaround"></a>Solution de contournement
Aucun



## <a name="software-updates"></a>Mises à jour logicielles

### <a name="security-roles-are-missing-for-phased-deployments"></a>Les rôles de sécurité sont manquants pour les déploiements par phases
<!--3479337, SCCMDocs-pr issue 3095-->
*S’applique à : Configuration Manager version 1810*

Le rôle de sécurité intégré **Gestionnaire de déploiement de système d’exploitation** dispose des autorisations pour les [déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). Ces autorisations sont manquantes dans les rôles suivants :  

- **Administrateur d’application**  
- **Gestionnaire de déploiement d’applications**  
- **Gestionnaire des mises à jour logicielles**  

Le rôle **Auteur d’application** peut sembler disposer de quelques autorisations pour les déploiements par phases, mais ne devrait pas être en mesure de créer des déploiements. 

Un utilisateur disposant de l’un de ces rôles peut démarrer l’assistant « Create Phased Deployment » (Créer un déploiement par phases), et peut afficher les déploiements par phases d’une mise à jour d’application ou de logiciel. Toutefois, il ne peut pas terminer l’assistant ni faire de modifications à un déploiement existant.

#### <a name="workaround"></a>Solution de contournement
Créez un rôle de sécurité personnalisé. Copiez un rôle de sécurité existant, et ajoutez les autorisations suivantes sur la classe d’objet **Déploiement par phases** :
- Créer  
- Supprimer  
- Modifier  
- Lecture  

Pour plus d’informations, consultez [Créer des rôles de sécurité personnalisés](/sccm/core/servers/deploy/configure/configure-role-based-administration#BKMK_CreateSecRole)


### <a name="changing-office-365-client-setting-doesnt-apply"></a>La modification du paramètre client Office 365 ne s’applique pas 
<!--511551-->
*S’applique à : Configuration Manager version 1802*  

Déployez un [paramètre client](/sccm/core/clients/deploy/about-client-settings#enable-management-of-the-office-365-client-agent) avec **Activer la gestion de l’agent Office 365 Client** configuré sur `Yes`. Changez ensuite ce paramètre en `No` ou `Not Configured`. Après la mise à jour de la stratégie sur les clients ciblés, les mises à jour Office 365 continuent d’être gérées par Configuration Manager. 

#### <a name="workaround"></a>Solution de contournement
Changez la valeur de Registre suivante en `0` et redémarrez le **service Microsoft Office « Démarrer en un clic »** (ClickToRunSvc) :

```
[HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\office\16.0\Common\officeupdate]
"OfficeMgmtCOM"=dword:00000000
```



## <a name="mobile-device-management"></a>Gestion des appareils mobiles  

### <a name="validation-for-ios-app-link-sometimes-fails-on-valid-link"></a>La validation de liens d’application iOS valides échoue parfois
<!-- LSI 106004348 --> Lors de la création d’une application de type **Package d’application pour iOS provenant de l’App Store**, il y a des URL valides pour **l’Emplacement** que le validateur n’accepte pas. Plus précisément, l’App Store iOS ne réclame pas de valeur dans la section du nom d’application de l’URL. Par exemple, les deux liens suivants sont valides et pointent vers la même application, mais **l’Assistant Créer une application** n’accepte que le premier :
- `https://itunes.apple.com/us/app/app-name/id123456789?mt=8`
- `https://itunes.apple.com/us/app//id123456789?mt=8`

#### <a name="workaround"></a>Solution de contournement
Lorsque vous créez une application iOS dont l’URL ne comporte pas le nom, ajoutez à l’URL une valeur quelconque comme s’il s’agissait du nom de l’application. Par exemple :
- `https://itunes.apple.com/us/app/any-string/id123456789?mt=8`

Cette action permet d’aller au bout de l’Assistant. Le déploiement de l’application sur des appareils iOS réussit quand même. La chaîne ajoutée à l’URL apparaît comme **Nom** dans l’onglet **Informations générales** de l’Assistant. Elle constitue également l’étiquette de l’application sur le Portail d’entreprise.


### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Vous ne pouvez plus déployer de profils VPN Windows Phone 8.1 sur Windows 10
<!-- 503274  -->
*S’applique à : Configuration Manager version 1710*

Vous ne pouvez pas créer de profil VPN à l’aide du workflow Windows Phone 8.1, ce qui s’applique aussi aux appareils Windows 10. Pour ces profils, l’Assistant de création n’affiche plus la page Plateformes prises en charge. Windows Phone 8.1 est sélectionné automatiquement sur le serveur principal. La page Plateformes prises en charge est disponible dans les propriétés du profil, mais n’affiche pas les options de Windows 10.

#### <a name="workaround"></a>Solution de contournement
 Utilisez le workflow du profil VPN Windows 10 pour les appareils Windows 10. Si ce n’est pas possible pour votre environnement, contactez le support technique. Le support technique peut vous aider à ajouter le ciblage Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
