---
title: Notes de publication
titleSuffix: Configuration Manager
description: Découvrez plus en détail les problèmes urgents qui ne sont pas encore résolus dans le produit ni traités dans un article de la Base de connaissances Microsoft.
ms.date: 04/18/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 030947fd-f5e0-4185-8513-2397fb2ec96f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4aeacdbc73e21c3bae18111e22c8407eba865a87
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338157"
---
# <a name="release-notes-for-system-center-configuration-manager"></a>Notes de publication de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avec Configuration Manager, les notes de publication de produit se limitent aux problèmes urgents. Ces problèmes ne sont pas encore résolus dans le produit ni traités dans un article de la Base de connaissances Microsoft.  

La documentation spécifique aux fonctionnalités inclut des informations sur les problèmes connus qui affectent les scénarios de base.  

> [!TIP]  
>  Cette rubrique contient les notes de publication pour l’édition actuelle de Configuration Manager. Pour obtenir des informations sur l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](../../../../core/get-started/technical-preview.md)  

Pour plus d’informations sur les nouvelles fonctionnalités introduites dans les différentes versions, consultez les articles suivants :
- [Nouveautés de la version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802)
- [Nouveautés dans la version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710)
- [Nouveautés dans la version 1706](/sccm/core/plan-design/changes/whats-new-in-version-1706)  



## <a name="setup-and-upgrade"></a>Installation et mise à niveau  


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



<!-- ## Backup and recovery  -->


## <a name="client-deployment-and-upgrade"></a>Mise à niveau et déploiement du client

### <a name="azure-ad-enabled-clients-cant-communicate-with-management-point"></a>Les clients compatibles Azure AD ne peuvent pas communiquer avec le point de gestion
<!--501089-->
*S’applique à : Configuration Manager version 1706*
<!--also fixed in 1710 HFRU-->
Dans le scénario pour [installer et attribuer des clients Configuration Manager exécutant Windows 10 avec Azure AD pour l’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure), les communications du client échouent quand le point de gestion HTTPS utilise d’autres informations d’identification de base de données. 

#### <a name="workaround"></a>Solution de contournement
Pour atténuer ce problème, effectuez l’une des actions suivantes :
- Mettez à jour le site vers la dernière version et appliquez le dernier correctif
- Modifiez les informations d’identification utilisées par le point de gestion.


<!-- ## Operating system deployment  -->



## <a name="software-updates"></a>Mises à jour logicielles

### <a name="servicing-plans-create-many-duplicate-software-update-groups-and-deployments-by-default"></a>Les plans de maintenance créent un grand nombre de groupes et de déploiements de mises à jour logicielles en double  
<!-- 474326 -->
Par défaut, l’Assistant Créer un plan de maintenance s’exécute actuellement après chaque synchronisation des mises à jour logicielles. Chaque fois que l’Assistant s’exécute, il crée un groupe et un déploiement de mises à jour logicielles. Si vous avez une planification de la synchronisation des mises à jour logicielles qui s’exécute plusieurs fois par jour, l’Assistant Créer un plan de maintenance génère quotidiennement plusieurs groupes et déploiements de mises à jour logicielles.  

#### <a name="workaround"></a>Solution de contournement
 après avoir créé un plan de maintenance, ouvrez les propriétés de celui-ci, accédez à l’onglet **Calendrier d’évaluation**, sélectionnez **Exécuter la règle dans un calendrier**, cliquez sur **Personnaliser**, puis créez un calendrier personnalisé. Par exemple, vous pouvez faire en sorte que le plan de maintenance s’exécute tous les 60 jours.  


### <a name="changing-office-365-client-setting-doesnt-apply"></a>Le changement du paramètre client Office 365 ne s’applique pas 
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

### <a name="you-can-no-longer-deploy-windows-phone-81-vpn-profiles-to-windows-10"></a>Vous ne pouvez plus déployer de profils VPN Windows Phone 8.1 sur Windows 10
<!-- 503274  -->
*S’applique à : Configuration Manager version 1710*

Vous ne pouvez pas créer de profil VPN à l’aide du workflow Windows Phone 8.1, ce qui s’applique aussi aux appareils Windows 10. Pour ces profils, l’Assistant de création n’affiche plus la page Plateformes prises en charge. Windows Phone 8.1 est sélectionné automatiquement sur le serveur principal. La page Plateformes prises en charge est disponible dans les propriétés du profil, mais n’affiche pas les options de Windows 10.

#### <a name="workaround"></a>Solution de contournement
 Utilisez le workflow du profil VPN Windows 10 pour les appareils Windows 10. Si ce n’est pas possible pour votre environnement, contactez le support technique. Le support technique peut vous aider à ajouter le ciblage Windows 10.



<!-- ## Reports and monitoring    -->
<!-- ## Conditional access   -->
<!-- ## Endpoint Protection -->
