---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Découvrez les nouvelles fonctionnalités disponibles dans la branche Technical Preview de Configuration Manager version 1807.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9095bdf431525a66a570267c4fff07a382a16fe4
ms.sourcegitcommit: af4f8bd8dffe6fb05f51322ea9e94d335a2cc0c0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2018
ms.locfileid: "39360765"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Fonctionnalités Technical Preview de Configuration Manager version 1807 

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités disponibles dans la version Technical Preview de Configuration Manager, version 1807. Installez cette version pour mettre à jour le site de votre version Technical Preview et lui ajouter de nouvelles fonctionnalités. 

Consultez l’article sur la version [Technical Preview](/sccm/core/get-started/technical-preview) avant d’installer cette mise à jour. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version vers une autre et comment envoyer des commentaires.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Problèmes connus 

### <a name="ki_o365"></a> Problèmes liés aux mises à jour logicielles d’Office 365
<!--521365--> Si vous gérez les mises à jour d’Office 365 à l’aide des versions de branche Technical Preview 1806 et 1806.2, celles-ci risquent de ne pas s’installer correctement sur les clients. 

#### <a name="workaround"></a>Solution de contournement
- Supprimez les packages de déploiement existants et les groupes de mise à jour logicielle pour Office 365.  

- À compter du 31 juillet 2018, synchronisez les mises à jour logicielles d’Office 365 et déployez uniquement les dernières mises à jour.  



</br>

**Les sections suivantes décrivent les nouvelles fonctionnalités à tester dans cette version :**  


## <a name="bkmk_hub"></a> Hub Communauté
<!--1357766-->

Le hub Communauté est un emplacement centralisé qui permet de partager des objets Configuration Manager utiles avec d’autres personnes. Consultez le nouvel espace de travail **Communauté** dans la console Configuration Manager, puis sélectionnez le nœud **Hub**. Utilisez le hub Communauté pour télécharger les types d’objet Configuration Manager suivants : 
- Scripts
- Éléments de configuration

![Console Configuration Manager, espace de travail Communauté, nœud Hub](media/1357766-hub.png)

Pour plus d’informations sur un élément disponible, cliquez sur ce dernier dans le hub. Dans la page des détails, cliquez sur **Télécharger** pour obtenir l’élément. Quand vous téléchargez un élément à partir du hub, il est automatiquement ajouté à votre site. 

![Console Configuration Manager, espace de travail Communauté, nœud Hub, page des détails](media/1357766-hub-details.png)

L’espace de travail **Communauté** inclut également les nœuds suivants :

- **Documentation** : affiche la [bibliothèque de documentation](https://docs.microsoft.com/sccm/) de Configuration Manager  

- **Commentaires** : affiche le [site UserVoice](https://configurationmanager.uservoice.com/) de Configuration Manager  


### <a name="prerequisites"></a>Prérequis

- Utilisez la console Configuration Manager sur un système d’exploitation client.  

    - Sinon, mais cela n’est pas recommandé, sur un système d’exploitation serveur, désactivez la [Configuration de sécurité renforcée d’Internet Explorer](https://go.microsoft.com/fwlink/?LinkId=253461).  

- L’ordinateur où se trouve la console nécessite un accès Internet et une connectivité aux sites suivants :  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Problème connu

La contribution des éléments au hub n’est pas disponible dans cette version. 



## <a name="bkmk_osd"></a> Spécifier le lecteur pour la maintenance des images de système d’exploitation hors connexion  
<!--1358924-->

Vos [commentaires UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive) ayant été pris en compte, vous pouvez à présent spécifier le lecteur utilisé par Configuration Manager durant l’installation hors connexion des images de système d’exploitation. Ce processus peut consommer une grande quantité d’espace disque en raison des fichiers temporaires. Cette option vous permet donc de sélectionner le lecteur à utiliser. 


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) avec vos réflexions sur la fonctionnalité.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Dans le ruban, cliquez sur **Configurer les composants de site**, puis sélectionnez **Point de mise à jour logicielle**.  

2. Passez à l’onglet **Installation hors connexion**, puis spécifiez l’option correspondant à **Lecteur local à utiliser pour l’installation hors connexion des images**.  

Par défaut, ce paramètre a la valeur **Automatique**. Avec cette valeur, Configuration Manager sélectionne le lecteur sur lequel il est installé. 

Durant l’installation hors connexion, Configuration Manager stocke les fichiers temporaires dans le dossier `<drive>:\ConfigMgr_OfflineImageServicing`. Il monte également les images du système d’exploitation dans ce dossier. 

Consultez le fichier journal **OfflineServicingMgr.log**. 



## <a name="bkmk_comgmt"></a> Activité de synchronisation d’appareil cogéré depuis Intune
<!--1358565-->

Déterminez à l’aide de la console Configuration Manager si un appareil cogéré est actif auprès de Microsoft Intune. Cet état est basé sur les données provenant de l’[entrepôt de données Intune](https://docs.microsoft.com/intune/reports-nav-create-intune-reports). Le tableau de bord **État du client** dans la console Configuration Manager affiche les **Clients inactifs utilisant Intune**. Cette nouvelle catégorie concerne les appareils cogérés inactifs auprès de Configuration Manager, mais qui se sont synchronisés avec le service Intune la semaine précédente.


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) avec vos réflexions sur la fonctionnalité.

Si vous avez déjà configuré votre site pour la cogestion : 

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**. Cliquez dans le ruban sur **Propriétés**.  

2. Passez à l’onglet **Rapports**. Cliquez sur **Connexion**, puis authentifiez-vous. Cliquez ensuite sur **Mettre à jour** afin d’activer les autorisations d’accès en lecture pour l’entrepôt de données Intune.  

3. Une fois le site synchronisé avec Intune, accédez à l’espace de travail **Analyse**, puis sélectionnez le nœud **État du client**. Dans la section **État général du client**, consultez la ligne relative aux **Clients inactifs utilisant Intune**.  

Pour plus d’informations sur l’activation de la cogestion, consultez [Cogestion pour les appareils Windows 10](/sccm/core/clients/manage/co-management-overview).



## <a name="bkmk_app-repair"></a> Réparer les applications
<!--1357866-->

Vos [commentaires UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application) ayant été pris en compte, vous pouvez à présent spécifier une ligne de commande de réparation pour les types de déploiement basés sur Windows Installer et le Programme d’installation de script. 


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) avec vos réflexions sur la fonctionnalité.

1. Dans la console Configuration Manager, ouvrez les propriétés d’un type de déploiement basé sur Windows Installer ou le Programme d’installation de script.  

2. Passez à l’onglet **Programmes**. Spécifiez la commande pour **Réparer le programme**.  

3. Déployez l’application. Sous l’onglet **Paramètres de déploiement** du déploiement, activez l’option **Autoriser les utilisateurs finaux à tenter de réparer cette application**.  


### <a name="known-issue"></a>Problème connu

Le nouveau bouton du Centre logiciel, qui permet aux utilisateurs de **Réparer** l’application n’est pas visible dans cette version.  



## <a name="bkmk_email-approve"></a> Approuver les demandes d’application par e-mail
<!--1321550-->

Configurez les notifications par e-mail pour les demandes d’approbation de l’application. Quand un utilisateur demande une application, vous recevez un e-mail. Cliquez sur les liens de l’e-mail pour approuver ou refuser la demande, sans avoir besoin d’utiliser la console Configuration Manager.


### <a name="prerequisites"></a>Prérequis

#### <a name="to-send-email-notifications"></a>Pour envoyer des notifications par e-mail
- Activez la [fonctionnalité facultative](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approuver les demandes d’application pour les utilisateurs appareil par appareil**.  

- Configurez la [notification par e-mail pour les alertes](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>Pour approuver ou refuser des demandes par e-mail
Si vous ne configurez pas ces prérequis, le site envoie une notification par e-mail pour les demandes d’application sans liens pour approuver ou refuser la demande.  

- Dans les propriétés du site, **Activez le point de terminaison REST pour tous les rôles fournisseurs de ce site, et autorisez le trafic de la passerelle de gestion cloud de Configuration Manager**. Pour plus d’informations, consultez [Accès aux données de point de terminaison OData](/sccm/core/get-started/capabilities-in-technical-preview-1612#odata-endpoint-data-access).  

    - Redémarrer le service SMS_EXEC après avoir activé le point de terminaison REST

- [Passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Intégrer le site aux [services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**  

    - Activer la [découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Configurez manuellement les paramètres suivants pour cette application native dans Azure AD :  

        - **URI de redirection** : `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Utilisez le FQDN (nom de domaine complet) du service CMG (Passerelle de gestion cloud), par exemple GraniteFalls.Contoso.com.   

        - **Manifeste** : affectez à **oauth2AllowImplicitFlow** la valeur true : `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) avec vos réflexions sur la fonctionnalité.

1. Dans la console Configuration Manager, déployez une application disponible pour une collection d’utilisateurs. Dans la page **Paramètres de déploiement**, activez-la pour approbation. Entrez ensuite une adresse e-mail *unique* pour recevoir une notification.  

     > [!Note]  
     > Toute personne de votre organisation Azure AD qui reçoit l’e-mail peut approuver la demande. Ne transférez pas l’e-mail à d’autres utilisateurs à moins que vous ne souhaitiez qu’ils effectuent une action.  

2. En tant qu’utilisateur, demandez l’application dans le Centre logiciel.  

3. Vous recevez une notification par e-mail semblable à l’exemple suivant :  

![Exemple de notification par e-mail pour une approbation de l’application](media/1321550-email.png)

> [!Note]  
> Le lien d’approbation ou de refus ne peut être utilisé qu’une seule fois. Par exemple, vous configurez un alias de groupe pour recevoir des notifications. Isabelle approuve la demande. Dans ce cas, Laurent ne peut pas refuser la demande.  



## <a name="bkmk_script"></a> Amélioration de la sortie de script
<!--1236459-->

Vous pouvez désormais afficher la sortie de script détaillée au format JSON brut ou structuré. Cette mise en forme rend la sortie plus facile à lire et à analyser. Si le script retourne du texte dans un format JSON valide, affichez la sortie détaillée en tant que **sortie JSON** ou en tant que **sortie brute**. Sinon, la seule option est la **sortie de script**. 

#### <a name="example-script-output-is-valid-json"></a>Exemple : la sortie de script correspond à un format JSON valide
Commande : `$PSVersionTable.PSVersion`  

Sortie :  
```
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Exemple : la sortie de script ne correspond pas à un format JSON valide
Commande : `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

Sortie :  
```
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Essayez !

Essayez d’effectuer les tâches. Envoyez ensuite des [commentaires](capabilities-in-technical-preview-1804.md#bkmk_feedback) avec vos réflexions sur la fonctionnalité.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, puis sélectionnez le nœud **Regroupements d’appareils**. Cliquez avec le bouton droit sur une collection, puis sélectionnez **Exécuter le script**. Pour plus d’informations sur la création et l’exécution de scripts, consultez [Créer et exécuter des scripts PowerShell à partir de la console Configuration Manager](/sccm/apps/deploy-use/create-deploy-scripts).  

2. Exécutez un script sur la collection cible.  

3. Au bas de la page **Monitoring de l’état du script** de l’Assistant Exécution de scripts, sélectionnez l’onglet **Résumé**. Remplacez les deux listes déroulantes situées vers le haut par **Sortie de script** et **Table de données**. Double-cliquez ensuite sur la ligne des résultats pour ouvrir la boîte de dialogue **Sortie détaillée**.  

4. Au bas de la page **Monitoring de l’état du script** de l’Assistant Exécution de scripts, sélectionnez l’onglet **Détails de l’exécution**. Double-cliquez sur une ligne de résultats pour ouvrir la boîte de dialogue de sortie détaillée de l’appareil correspondant.  



## <a name="bkmk_3pupdate"></a> Amélioration des mises à jour des logiciels tiers
<!--1358714-->

Vous pouvez désormais modifier les propriétés des catalogues personnalisés.

Pour plus d’informations, consultez [Prise en charge de mises à jour de logiciels tiers pour les catalogues personnalisés](/sccm/core/get-started/capabilities-in-technical-preview-1806-2#bkmk_3pupdate).



## <a name="next-steps"></a>Étapes suivantes

Pour plus d’informations sur l’installation ou la mise à jour de la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).    

Pour plus d’informations sur les différentes branches de Configuration Manager, consultez [Quelle branche de Configuration Manager dois-je utiliser ?](/sccm/core/understand/which-branch-should-i-use)