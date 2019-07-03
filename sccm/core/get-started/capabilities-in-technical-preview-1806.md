---
title: Version Technical Preview 1806
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités disponibles dans Configuration Manager Technical Preview version 1806.
ms.date: 06/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 52d64ef0-8c0d-42c3-857e-07d7ec776f29
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b57720d800e224d68f92f339e0c3b4964010e05
ms.sourcegitcommit: 3936b869d226cea41fa0090e2cbc92bd530db03a
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/20/2019
ms.locfileid: "67285947"
---
# <a name="capabilities-in-technical-preview-1806-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1806 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans la version Technical Preview 1806 de Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités au site de votre préversion technique. 

Consultez l’article [Technical Preview](/sccm/core/get-started/technical-preview) avant d’installer cette mise à jour. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->
## <a name="known-issues-in-this-technical-preview"></a>Problèmes connus dans cette préversion technique

### <a name="ki_contentlib"></a> Impossible de mettre à niveau le site à l’aide de la bibliothèque de contenu distante
<!--514642-->
Vous ne parvenez pas à mettre à niveau le site, et les erreurs suivantes sont journalisées dans **cmupdate.log** :  
```  
Failed to find any valid drives  
GetContentLibraryParameters failed; 0x80070057  
ERROR: Failed to process configuration manager update.  
```  

Dans cette version, ce problème se produit lorsque la bibliothèque de contenu se trouve à un emplacement distant.

#### <a name="workaround"></a>Solution de contournement
Déplacez la bibliothèque de contenu vers un lecteur local du serveur de site. Pour plus d’informations, consultez [Configurer une bibliothèque de contenu à distance pour le serveur de site](/sccm/core/get-started/capabilities-in-technical-preview-1804#configure-a-remote-content-library-for-the-site-server). 



</br>

**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  



## <a name="bkmk-3pupdate"></a> Mises à jour des logiciels tiers
<!--1352101-->
Pour répondre à la demande que vous avez exprimée par le biais des [commentaires UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8803711-3rd-party-patching-scup-integration-with-sccm-co), cette nouvelle version comprend une meilleure prise en charge des mises à jour de logiciels tiers. Pour certains scénarios courants, vous n’avez plus besoin d’utiliser l’éditeur de mise à jour System Center (SCUP). Le nouveau nœud **Catalogues de mises à jour de logiciels tiers** de la console Configuration Manager vous permet de vous abonner à des catalogues tiers, de publier leurs mises à jour sur votre point de mise à jour logicielle, puis de les déployer sur les clients. 

Cette version comprend les catalogues de mise à jour de logiciels tiers suivants :

 | Éditeur | Nom du catalogue |
 |--------|---------------------|
 | HP | Catalogue de mises à jour des clients HP |

SCUP continue de prendre en charge les autres catalogues et scénarios. La liste des catalogues qui se trouve sous le nœud Catalogues de mises à jour de logiciels tiers de la console Configuration Manager est une liste dynamique. Elle est donc mise à jour dès que de nouveaux catalogues sont disponibles et pris en charge.


### <a name="prerequisites"></a>Prérequis
- Configurez la gestion des mises à jour de logiciels avec un point de mise à jour logicielle HTTPS. Pour plus d’informations, consultez [Préparer la gestion des mises à jour logicielles](/sccm/sum/get-started/prepare-for-software-updates-management).  
  - Dans cette version, le point de mise à jour logicielle doit se trouver sur le serveur de site pour cette fonctionnalité. <!--515810--> 

    > [!Tip]  
    > Le point de mise à jour logicielle nécessite HTTPS, car il est nécessaire pour les API WSUS utilisées pour gérer les certificats de signature. HTTPS ne doit pas nécessairement être activé pour les clients non plus. Pour plus d’informations sur l’activation de HTTPS sur WSUS, consultez les articles suivants pour obtenir une assistance :  
    > - [Sécuriser WSUS avec le protocole SSL](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#bkmk_2.5.ConfigSSL) 
    > - [Billet de blog de prise en charge de WSUS](https://blogs.technet.microsoft.com/sus/2011/05/09/how-to-create-an-internet-facing-wsus-server-that-uses-different-internal-and-external-names/)

- Suffisamment d’espace disque sur le point de mise à jour logicielle où se trouve le dossier WSUSContent pour stocker le contenu binaire source des mises à jour de logiciels tiers. La quantité de stockage nécessaire varie en fonction du fournisseur, du type de mise à jour, ainsi que des mises à jour que vous publiez en vue de leur déploiement. Si vous devez déplacer le dossier WSUSContent vers un lecteur qui contient davantage d’espace, consultez ce billet de blog de l’équipe du support WSUS : [How to change the location where WSUS stores updates locally](https://blogs.technet.microsoft.com/sus/2008/05/19/wsus-how-to-change-the-location-where-wsus-stores-updates-locally/).  

- Activez puis déployez le paramètre client [Activer les mises à jour de logiciels tiers](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates) dans le groupe **Mises à jour logicielles**.  

- Le serveur de site nécessite un accès Internet au site download.microsoft.com via le port HTTPS 443. Le service de synchronisation des mises à jour de logiciels tiers doit être en cours d’exécution sur le serveur de site. Ce service met à jour la liste des catalogues tiers disponibles, télécharge les catalogues lorsque vous vous y abonnez et télécharge les mises à jour lorsque celles-ci sont publiées. Si nécessaire, configurez les paramètres du proxy Internet sous l’onglet **Proxy** des propriétés du rôle de système de site, sur l’ordinateur du serveur de site.  


### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.


#### <a name="phase-1-enable-and-set-up-the-feature"></a>Phase 1 : Activer et configurer la fonctionnalité
Pour activer et configurer la fonctionnalité à utiliser, effectuez les opérations suivantes *une fois pour chaque hiérarchie* :  

1. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site**, puis sélectionnez le nœud **Sites**.  

2. Sélectionnez le site de niveau supérieur dans la hiérarchie. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sélectionnez **Point de mise à jour logicielle**.  

3. Passez l’onglet **Mises à jour tierces**. Sélectionnez l’option **Activer les mises à jour de logiciels tiers**. Pour plus d’informations sur les options de certificat, consultez [Améliorations concernant la prise en charge des mises à jour des logiciels tiers](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvements-for-enabling-third-party-software-update-support).  

   > [!Note]  
   > Si vous utilisez l’option par défaut, qui permet de gérer le certificat avec Configuration Manager, un nouveau certificat de type **Third-party WSUS Signing** (Signature WSUS tierce) est créé sous le nœud **Certificats**, sous  **Sécurité**, dans l’espace de travail **Administration**.  


#### <a name="phase-2-subscribe-to-a-third-party-catalog-and-sync-updates"></a>Phase 2 : S’abonner à un catalogue tiers et synchroniser les mises à jour
Procédez aux étapes suivantes pour *chaque catalogue tiers* auquel vous voulez vous abonner :  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Mises à jour logicielles**, puis sélectionnez le nœud **Catalogues de mises à jour de logiciels tiers**.  

2. Sélectionnez le catalogue auquel vous abonner, puis cliquez sur **S’abonner au catalogue** dans le ruban.   

3. Examinez et approuvez le certificat du catalogue.  

   > [!Note]  
   > Lorsque vous vous abonnez à un catalogue de mises à jour de logiciels tiers, le certificat que vous examinez et approuvez dans l’Assistant est ajouté au site. Ce certificat appartient au type **Catalogue des mises à jour de logiciels tiers**. Vous pouvez le gérer dans le nœud **Certificats**, situé sous **Sécurité**, dans l’espace de travail **Administration**.  

4. Effectuez toutes les étapes de l'Assistant.  

   > [!Tip]  
   > Après un premier abonnement, le catalogue doit commencer à télécharger les mises à jour immédiatement. Ensuite, dans cette version, il effectue une resynchronisation toutes les 24 heures. Si vous ne souhaitez pas attendre que le catalogue télécharge automatiquement les mises à jour, cliquez sur **Synchroniser maintenant** dans le ruban.  
   > 
   > Une fois le catalogue téléchargé, les métadonnées des produits doivent être synchronisées avec le point de mise à jour logicielle. Pour plus d’informations sur ce processus et sur le lancement manuel du téléchargement, consultez [Synchroniser les mises à jour logicielles](/sccm/sum/get-started/synchronize-software-updates). À ce stade, vous pouvez voir les mises à jour des logiciels tiers sous le nœud **Toutes les mises à jour**. 

5. Ensuite, configurez le point de mise à jour logicielle **Produits** pour le catalogue tiers auquel vous vous êtes abonné. Pour plus d’informations, consultez [Configurer les classifications et les produits à synchroniser](/sccm/sum/get-started/configure-classifications-and-products). Lorsque les critères des produits sont modifiés, vous devez effectuer une nouvelle synchronisation des mises à jour logicielles.

Pour que vous puissiez voir les résultats de la conformité des clients, ceux-ci doivent analyser et évaluer les mises à jour. Vous pouvez déclencher ce cycle manuellement sur un client, à partir du panneau de configuration Configuration Manager, en exécutant l’action **Cycle d’analyse des mises à jour de logiciels**. Pour plus d’informations sur ce processus, consultez [Présentation des mises à jour logicielles](/sccm/sum/understand/software-updates-introduction).


#### <a name="phase-3-deploy-third-party-software-updates"></a>Phase 3 : Déployer des mises à jour de logiciels tiers
Procédez aux étapes suivantes pour *chaque mise à jour de logiciel tiers* que vous souhaitez déployer sur les clients :  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Mises à jour logicielles**, puis sélectionnez le nœud **Toutes les mises à jour logicielles**.  

   > [!Tip]  
   > Pour filtrer la liste des mises à jour, cliquez sur **Ajouter des critères**. Par exemple, ajoutez **Fournisseur** pour **Adobe Systems, Inc.** afin d’afficher toutes les mises à jour Adobe.  

2. Sélectionnez les mises à jour dont ont besoin les clients. Cliquez sur **Publier le contenu des mises à jour de logiciels tiers** et surveillez la progression dans le journal SMS_ISVUPDATES_SYNCAGENT.log. Cette action télécharge les fichiers binaires de mise à jour du fournisseur, et les stocke dans le dossier WSUSContent situé sur le point de mise à jour logicielle. Elle fait également passer la mise à jour de l’état « métadonnées uniquement » à l’état « avec contenu et prête au déploiement ».  

   > [!Note]  
   > Lorsque vous publiez le contenu de mises à jour de logiciels tiers, tous les certificats utilisés pour signer le contenu sont ajoutés au site. Ces certificats appartiennent au type **Contenu des mises à jour de logiciels tiers**. Vous pouvez les gérer dans le nœud **Certificats**, situé sous **Sécurité**, dans l’espace de travail **Administration**.  

3. Déployez les mises à jour à l’aide du processus de gestion des mises à jour logicielles existant. Pour plus d’informations, consultez [Déployer des mises à jour logicielles](/sccm/sum/deploy-use/deploy-software-updates). Dans la page **Emplacement de téléchargement** de l’Assistant Déploiement des mises à jour logicielles, sélectionnez l’option par défaut **Télécharger les mises à jour logicielles à partir d’Internet**. Dans ce scénario, le contenu a déjà été publié sur le point de mise à jour logicielle, qui est utilisé pour télécharger le contenu du package de déploiement.


### <a name="monitoring-progress-of-third-party-software-updates"></a>Surveillance de la progression du téléchargement des mises à jour de logiciels tiers
La synchronisation des mises à jour de logiciels tiers est gérée par le composant SMS_ISVUPDATES_SYNCAGENT, sur le serveur de site. Vous pouvez afficher les messages d’état de ce composant, ou lire des informations d’état plus détaillées dans le journal SMS_ISVUPDATES_SYNCAGENT.log. Ce journal se trouve sur le serveur de site dans le sous-dossier **Journaux** du répertoire d’installation du site. Par défaut, le chemin est le suivant : `C:\Program Files\Microsoft Configuration Manager\Logs`. Pour plus d’informations sur la surveillance du processus global de gestion des mises à jour logicielles, consultez [Surveiller les mises à jour logicielles](/sccm/sum/deploy-use/monitor-software-updates).


### <a name="known-issues"></a>Problèmes connus
- Le service de synchronisation des mises à jour de logiciels tiers ne prend pas en charge le point de mise à jour logicielle configuré pour utiliser un **Compte de connexion du serveur WSUS**. Si ce compte est configuré sous l’onglet **Paramètres de compte et proxy** de la page Propriétés du point de mise à jour logicielle, vous verrez l’erreur suivante dans le journal SMS_ISVUPDATES_SYNCAGENT.log :  
`WSUS access account appears to be configured, it is not yet supported for third party updates sync.`  
Pour plus d’informations sur ce compte, consultez [Compte de connexion de point de mise à jour logicielle](/sccm/core/plan-design/hierarchy/accounts#software-update-point-connection-account).<!--515492-->  

- Ne confondez pas l’utilisation des autres outils tels que SCUP, avec cette nouvelle fonctionnalité intégrée de mise à jour des logiciels tiers. Le service de synchronisation des mises à jour de logiciels tiers ne peut pas publier le contenu des mises à jour de métadonnées uniquement qui ont été ajoutées à WSUS par une autre application, un autre outil ou un autre script, tel que SCUP. L’action **Publier le contenu des mises à jour de logiciels tiers** échoue avec ces mises à jour. Si vous avez besoin de déployer des mises à jour tierces qui ne sont pas encore prises en charge par cette fonctionnalité, suivez l’intégralité de votre processus existant pour déployer ces mises à jour.<!--515497-->  



## <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Configurer les paramètres Windows Defender SmartScreen pour Microsoft Edge
<!--1353701-->
Cette version ajoute les trois paramètres [Windows Defender SmartScreen](/windows/security/threat-protection/windows-defender-smartscreen/windows-defender-smartscreen-overview) à la [stratégie de paramètres de conformité du navigateur Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles). Dans la page **Paramètres de SmartScreen**, la stratégie inclut désormais les paramètres supplémentaires suivants :
- **Autoriser SmartScreen** : Spécifie si Windows Defender SmartScreen est autorisé. Pour plus d’informations, consultez la [stratégie de navigateur AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Les utilisateurs peuvent remplacer l’invite SmartScreen pour les sites** : Indique si les utilisateurs peuvent ignorer les avertissements du filtre Windows Defender SmartScreen concernant les sites web potentiellement malveillants. Pour plus d’informations, consultez la [stratégie de navigateur PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Les utilisateurs peuvent remplacer l’invite SmartScreen pour les fichiers** : Indique si les utilisateurs peuvent ignorer les avertissements du filtre Windows Defender SmartScreen concernant le téléchargement de fichiers non vérifiés. Pour plus d’informations, consultez la [stratégie de navigateur PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="sync-mdm-policy-from-microsoft-intune-for-a-co-managed-device"></a>Synchroniser la stratégie MDM de Microsoft Intune pour un appareil cogéré
<!--1357377-->
À compter de cette version, lorsque vous [passez à une charge de travail en cogestion](/sccm/core/clients/manage/co-management-switch-workloads), les appareils cogérés sont automatiquement synchronisés avec la stratégie MDM de Microsoft Intune. Cette synchronisation est effectuée lorsque vous lancez l’action **Télécharger la stratégie d’ordinateur** à partir de Notification du client, dans la console Configuration Manager. Pour plus d’informations, consultez [Lancer une récupération de stratégie client en utilisant une notification de client](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="transition-office-365-workload-to-intune-using-co-management"></a>Transférer la charge de travail Office 365 vers Intune avec la cogestion
<!--1357841-->
Vous pouvez désormais transférer la charge de travail Office 365 de Configuration Manager vers Microsoft Intune après avoir activé la cogestion. Pour transférer cette charge de travail, accédez à la page de propriétés de cogestion et déplacez le curseur actuellement sur Configuration Manager vers Pilote ou Tout. Pour plus d’informations, consultez [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview).

Il existe également une nouvelle condition globale : **Are Office 365 applications managed by Intune on the device ?** (Les applications Office 365 sont-elles gérées par Intune sur cet appareil ?). Cette condition est ajoutée par défaut dans le cadre d’une exigence pour les nouvelles applications Office 365. Si vous transférez cette charge de travail, les clients cogérés ne répondront pas à cette exigence de l’application. Par conséquent, n’installez pas Office 365 par le biais d’un déploiement Configuration Manager.

### <a name="known-issue"></a>Problème connu
- Ce transfert de charge de travail concerne uniquement les déploiements Office 365. Configuration Manager continue de gérer les mises à jour Office 365.<!--510876--> Pour obtenir plus d’informations, ainsi qu’une solution de contournement, consultez la section [Le changement du paramètre client Office 365 ne s’applique pas](/sccm/core/servers/deploy/install/release-notes#changing-office-365-client-setting-doesnt-apply) dans les notes de publication de Configuration Manager version 1802.



## <a name="package-conversion-manager"></a>Package Conversion Manager 
<!--1357861-->
Package Conversion Manager est un nouvel outil intégré qui vous permet de convertir des packages Configuration Manager 2007 hérités en applications Configuration Manager Current Branch. Ensuite, vous pouvez utiliser les fonctionnalités des applications telles que les dépendances, les règles de spécification et l’affinité entre utilisateur et appareil.

> [!Tip]  
> La documentation héritée concernant les fonctionnalités existantes de Package Conversion Manager est disponible sur [TechNet](https://technet.microsoft.com/library/hh531519.aspx). Les informations pertinentes sont en cours de migration vers la bibliothèque docs.microsoft.com.

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

> [!Important]  
> Si vous avez installé une ancienne version de Package Conversion Manager, désinstallez-la avant de mettre à niveau votre site. La nouvelle version intégrée ne nécessite pas d’installation, toutefois, elle peut créer un conflit avec les versions existantes.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**. Développez **Gestion des applications**, puis sélectionnez **Packages**.  
2. Sélectionnez un package. Les trois options suivantes sont disponibles dans le groupe **Conversion de packages** du ruban :  
     - **Analyser le package** : Démarre le processus de conversion en analysant le package.
     - **Convertir le package** : Cette action permet de convertir facilement certains packages en applications.
     - **Corriger et convertir** : Certains packages nécessitent que les problèmes soient résolus avant leur conversion en applications.  

   Pour plus d’informations sur ces actions, consultez [Comment analyser et convertir des packages](https://docs.microsoft.com/previous-versions/system-center/system-center-2012-R2/hh846244%28v%3dtechnet.10%29).  

3. Accédez à l’espace de travail **Monitoring** (Surveillance), puis sélectionnez **Package Conversion Status** (État de la conversion du package). Ce nouveau tableau de bord montre l’analyse globale, ainsi que l’état de conversion des packages du site. Une nouvelle tâche d’arrière-plan résume automatiquement les données d’analyse.  

   > [!Tip]  
   > Package Conversion Manager ne nécessite pas qu’une analyse de packages soit planifiée. Cette action est désormais gérée par la tâche de totalisation intégrée.  

![Capture d’écran du tableau de bord d’état des conversions de packages](media/1357861-pcm-dashboard.png)



## <a name="deploy-software-updates-without-content"></a>Déployer des mises à jour logicielles sans contenu
<!--1357933-->
Vous pouvez désormais déployer des mises à jour logicielles sur vos appareils sans avoir à télécharger et à distribuer préalablement le contenu des mises à jour logicielles sur les points de distribution. Cette fonctionnalité est utile lorsque le contenu des mises à jour est très volumineux, ou si vous souhaitez que les clients obtiennent toujours le contenu via le service cloud Microsoft Update. Dans ce cas, les clients peuvent également télécharger le contenu auprès d’homologues qui disposent déjà du contenu nécessaire. Le client Configuration Manager continue de gérer le téléchargement de contenu. Vous pouvez donc utiliser la fonctionnalité de cache d’homologue Configuration Manager ou d’autres technologies telles que l’optimisation de la distribution. Cette fonctionnalité prend en charge tous les types de mises à jour pris en charge par la gestion des mises à jour logicielles Configuration Manager, y compris les mises à jour Windows et Office. 

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Démarrez un déploiement de mises à jour logicielles comme vous le feriez habituellement. Pour plus d’informations, consultez [Déployer des mises à jour logicielles](/sccm/sum/deploy-use/deploy-software-updates).
2. Dans la page **Package de déploiement** de l’Assistant Déploiement des mises à jour logicielles, sélectionnez la nouvelle option **No deployment package** (Aucun package de déploiement).

### <a name="known-issues"></a>Problèmes connus
- Une icône correspondant à une mise à jour déployée avec ce paramètre s’affiche avec une croix rouge, comme si la mise à jour n’était pas valide. Pour plus d’informations, consultez [Icônes utilisées pour les mises à jour logicielles](/sccm/sum/understand/software-updates-icons). <!--515556-->  
- Ce paramètre est intégré uniquement à l’Assistant Déploiement des mises à jour logicielles. Il n’est pas disponible pour les règles de déploiement automatique. <!--515558-->  



## <a name="office-customization-tool-integration-with-the-office-365-installer"></a>Intégration de l’Outil de personnalisation Office au programme d’installation d’Office 365
<!--1358149-->
L’outil de personnalisation Office est désormais intégré au programme d’installation d’Office 365 dans la console Configuration Manager. Lorsque vous créez un déploiement pour Office 365, vous pouvez désormais configurer dynamiquement les derniers paramètres de gestion Office. L’outil de personnalisation Office est mis à jour en même temps que les nouvelles builds d’Office 365. Vous pouvez désormais profiter des nouveaux paramètres de gestion d’Office 365 dès leur publication. 

### <a name="prerequisites"></a>Prérequis
- L’ordinateur qui exécute la console Configuration Manager nécessite un accès Internet via le port HTTPS 443. L’Assistant Installation du client Office 365 utilise une API de navigateur web Windows standard pour ouvrir https://config.office.com. Si un serveur proxy Internet est utilisé, l’utilisateur doit pouvoir accéder à cette URL.

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, puis sélectionnez le nœud **Gestion des clients Office 365**.
2. Dans le tableau de bord, cliquez sur la vignette **Programme d’installation d’Office 365** pour lancer l’Assistant Installation du client Office 365. Pour plus d’informations, consultez [Déployer des applications Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).
3. Dans la page **Paramètres Office**, cliquez sur **Go To Office Web Page** (Accéder à la page web d’Office). Utilisez l’outil de personnalisation en ligne d’Office pour spécifier les paramètres de ce déploiement. 
4. Lorsque vous avez terminé, cliquez sur **Envoyer** dans le coin supérieur droit. Terminez l’Assistant Installation du client Office 365.



## <a name="improvements-to-cloud-management-gateway"></a>Améliorations apportées à la passerelle de gestion cloud
Dans cette version, les améliorations suivantes ont été apportées à la passerelle de gestion cloud :

### <a name="simplified-client-bootstrap-command-line"></a>Ligne de commande de démarrage du client simplifiée
<!--1358215-->
Lorsque vous installez le client Configuration Manager via une passerelle de gestion cloud, le nombre de propriétés de ligne de commande nécessaires est désormais réduit. Lorsque vous vous préparez à la cogestion, consultez [Ligne de commande pour installer un client Configuration Manager](/sccm/comanage/how-to-prepare-Win10#install-the-configuration-manager-client) pour obtenir des informations détaillées sur l’un des exemples de ce scénario. 

Les propriétés de ligne de commande suivantes sont nécessaires pour tous les scénarios :
  - CCMHOSTNAME  
  - SMSSITECODE  

Les propriétés suivantes sont nécessaires lorsque vous utilisez Azure AD pour l’authentification client, au lieu de certificats d’authentification client PKI :
  - AADCLIENTAPPID  
  - AADRESOURCEURI  

La propriété suivante est nécessaire si le client doit revenir à l’intranet :
  - SMSMP  

L’exemple suivant comprend toutes les propriétés mentionnées ci-dessus :   
`ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver SMSMP=https://mp1.contoso.com`

Pour plus d’informations, consultez [Propriétés de l’installation du client](/sccm/core/clients/deploy/about-client-installation-properties).

### <a name="download-content-from-a-cmg"></a>Télécharger du contenu à partir d’une passerelle de gestion cloud
<!--1358651-->
Auparavant, vous deviez déployer un point de distribution cloud et une passerelle de gestion cloud en leur attribuant un rôle distinct. Dans cette version, une passerelle de gestion cloud peut également distribuer du contenu Office aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure. Pour activer cette fonctionnalité, activez la nouvelle option **Allow CMG to function as a cloud distribution point and serve content from Azure storage** (Autoriser la passerelle de gestion cloud à fonctionner comme un point de distribution cloud et à distribuer du contenu à partir du stockage Azure) sous l’onglet **Paramètres** des propriétés de la passerelle de gestion cloud. 

### <a name="trusted-root-certificate-isnt-required-with-azure-ad"></a>Les certificat racines approuvés ne sont plus nécessaires avec Azure AD
<!--503899-->
Lorsque vous créez une passerelle de gestion cloud, il n’est plus nécessaire de fournir un [certificat racine approuvé](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_cmgroot) dans la page Paramètres. Ce certificat n’est pas nécessaire lorsque vous utilisez Azure Active Directory (Azure AD) pour l’authentification client, mais il était auparavant nécessaire dans l’Assistant.

> [!Important]  
> Si vous utilisez des certificats d’authentification client PKI, vous devez continuer d’ajouter un certificat racine approuvé pour la passerelle de gestion cloud.



## <a name="improvements-to-secure-client-communications"></a>Amélioration des communications clientes sécurisées
<!--1358278,1358279-->
Cette version améliore encore davantage les [communications clientes sécurisées](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications) en supprimant les dépendances supplémentaires du compte d’accès réseau. Lorsque vous activez la nouvelle option de site **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**, les scénarios suivants ne nécessitent pas de compte d’accès réseau pour télécharger le contenu à partir d’un point de distribution :  

- Séquences de tâches exécutées à partir d’un support de démarrage ou d’un environnement PXE
- Séquence de tâches exécutées à partir du Centre logiciel  

Ces séquences de tâches conviennent aux déploiements de système d’exploitation et aux déploiements personnalisés. Elles sont également prises en charge par les ordinateurs de groupe de travail.



## <a name="software-center-infrastructure-improvements"></a>Améliorations apportées à l’infrastructure du Centre logiciel
<!--1358309-->
Les rôles du catalogue d’applications ne sont plus nécessaires pour afficher les applications accessibles aux utilisateurs dans le Centre logiciel. Cette modification permet d’alléger l’infrastructure de serveur nécessaire pour fournir des applications aux utilisateurs. Le Centre logiciel s’appuie désormais sur le point de gestion pour obtenir ces informations, ce qui permet une meilleure mise à l’échelle des grands environnements par l’attribution de [groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#management-points).

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Supprimez tous les rôles de catalogue d’applications présents sur le site. Ces rôles incluent le point de service web du catalogue d’applications et le point de site web du catalogue d’applications.
2. Déployez une application en la rendant accessible à un regroupement d’utilisateurs.
3. Utilisez le Centre logiciel en tant qu’utilisateur ciblé pour parcourir, demander et installer l’application.

### <a name="known-issue"></a>Problème connu
- Si vous utilisez un client joint à Azure Active Directory avec cette fonctionnalité, ne configurez pas le site sur **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**. Il existe actuellement un conflit avec cette fonctionnalité.<!--515846--> Pour plus d’informations sur ce paramètre, consultez [Amélioration des communications clientes sécurisées](/sccm/core/get-started/capabilities-in-technical-preview-1805#improved-secure-client-communications).



## <a name="provision-windows-app-packages-for-all-users-on-a-device"></a>Provisionner les packages d’application Windows pour tous les utilisateurs sur un appareil
<!--1358310-->
Vous pouvez désormais provisionner une application avec un package d’application Windows pour tous les utilisateurs d’un appareil. Un exemple courant de ce scénario est l’approvisionnement d’une application telle que « Minecraft : Education Edition » à partir de Microsoft Store pour Entreprises et Éducation, pour tous les appareils utilisés par les étudiants d’une école. Auparavant, Configuration Manager ne prenait en charge l’installation de ces applications que pour un seul utilisateur. Quand il se connectait à un nouvel appareil, l’élève devait attendre pour accéder à une application. À présent que l’application est provisionnée pour tous les utilisateurs d’un appareil, ceux-ci peuvent l’utiliser plus rapidement.

> [!Important]  
> Sachez que l’installation, le provisionnement et la mise à jour de plusieurs versions d’un même package d’application Windows sur un appareil peut entraîner des résultats inattendus. De tels résultats peuvent être obtenus lorsque vous utilisez Configuration Manager pour provisionner l’application, et que vous permettez aux utilisateurs de mettre à jour l’application à partir de Microsoft Store. Pour plus d’informations, consultez les instructions de la section Étapes suivantes pour [gérer les applications à partir du Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#next-steps).  

Lorsque vous provisionnez une application sous licence hors connexion, Configuration Manager ne permet pas à Windows de la mettre automatiquement à jour à partir de Microsoft Store.  

### <a name="try-it-out"></a>Essayez !
 Essayez d’effectuer les tâches. Envoyez-nous ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) pour nous indiquer comment cela a fonctionné.

1. Créez une application. Cette application doit provenir d’un package d’application Windows ou être une application sous licence hors connexion que vous avez synchronisée à partir de Microsoft Store pour Entreprises et Éducation.  

2. Dans la page **Informations générales** de l’Assistant Création d’une application, activez l’option **Provision this application for all users on the device** (Provisionner cette application pour tous les utilisateurs de l’appareil).  

   > [!Tip]  
   > Si vous modifiez une application existante, ce paramètre se trouve sous l’onglet **Expérience utilisateur** des propriétés de l’application.  

3. Déployez l’application sur un regroupement d’appareils.  

4. Connectez-vous à un appareil ciblé avec différents comptes d’utilisateurs, puis lancez l’application.  

> [!Note]  
> Si vous devez désinstaller une application provisionnée sur des appareils auxquels les utilisateurs se sont déjà connectés, vous devez créer deux déploiements de désinstallation. Pour le premier déploiement de désinstallation, ciblez le regroupement d’appareils qui contient les appareils en question. Pour le deuxième déploiement, ciblez le regroupement d’utilisateurs qui contient les utilisateurs déjà connectés aux appareils sur lesquels l’application est provisionnée. Lorsque vous désinstallez une application provisionnée d’un appareil, Windows ne la désinstalle pas pour les utilisateurs. 



## <a name="improvements-to-the-surface-dashboard"></a>Améliorations apportées au tableau de bord Surface
<!--1358654-->
Dans cette version, les améliorations suivantes ont été apportées au [tableau de bord Surface](/sccm/core/clients/manage/surface-device-dashboard) :
- Le tableau de bord Surface affiche désormais la liste des appareils appropriés quand les sections de graphe sont sélectionnées.
   - En cliquant sur la vignette **Pourcentage d’appareils Surface**, vous affichez la liste des appareils Surface.
   - En cliquant sur une barre de la vignette **Top cinq des versions de microprogramme**, vous affichez la liste des appareils Surface avec la version de leur microprogramme.
- Lorsque vous affichez ces listes d’appareils dans le tableau de bord Surface, vous pouvez cliquer avec le bouton droit sur l’un des appareils et effectuer des actions courantes.



## <a name="hardware-inventory-default-unit-revision"></a>Révision de l’unité par défaut pour l’inventaire matériel
<!--514442-->
Dans [Configuration Manager version 1710](/sccm/core/plan-design/changes/whats-new-in-version-1710#site-infrastructure), l’unité par défaut utilisée dans de nombreuses vues de rapports était passée des mégaoctets (Mo) aux gigaoctets (Go). En raison des [améliorations apportées à l’inventaire matériel au niveau des valeurs d’entiers longs](/sccm/core/get-started/capabilities-in-technical-preview-1805#improvement-to-hardware-inventory-for-large-integer-values), et en vue de répondre à la demande des utilisateurs, nous sommes repassé aux mégaoctets pour l’unité par défaut.



## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
