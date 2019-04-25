---
title: Nouveautés de la version 1902
titleSuffix: Configuration Manager
description: Obtenez des informations détaillées sur les changements et les nouvelles fonctionnalités introduits dans la version 1902 de l’édition Current Branch de Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4812324b-e6aa-4431-bf1d-9fcd763a8caa
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: fbc38cdb72a2c8f595eed88e0b4b5b5e29374597
ms.sourcegitcommit: 6f4c2987debfba5d02ee67f6b461c1a988a3e201
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59673647"
---
# <a name="whats-new-in-version-1902-of-configuration-manager-current-branch"></a>Nouveautés de la version 1902 de l’édition Current Branch de Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1902 pour l’édition Current Branch de Configuration Manager est disponible sous forme de mise à jour dans la console. Appliquez cette mise à jour sur les sites qui exécutent la version 1802, 1806 ou 1810. <!-- baseline only statement:-->Lors de l’installation d’un nouveau site, elle est également disponible sous la forme d’une version de base de référence. Cet article récapitule les changements et les nouvelles fonctionnalités de Configuration Manager version 1902.  

Référez-vous toujours à la dernière liste de contrôle pour installer cette mise à jour. Pour plus d’informations, consultez [Liste de contrôle pour installer la mise à jour 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902). Après avoir mis à jour un site, consultez également la [Liste de contrôle post-mise à jour](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist).

Pour tirer pleinement parti des nouvelles fonctionnalités de Configuration Manager, mettez également à jour les clients vers la dernière version après la mise à jour du site. Bien que les nouvelles fonctionnalités apparaissent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version des clients n’est pas également la plus récente.

> [!Note]  
> Cet article liste toutes les fonctionnalités importantes de cette version. Toutefois, toutes les sections ne sont pas encore liées au contenu mis à jour en fonction des informations supplémentaires sur les nouvelles fonctionnalités. Continuez à consulter régulièrement cette page sur les mises à jour. Les changements apportés sont indiqués à l’aide de l’étiquette ***[Mis à jour]***. Cette indication sera supprimée quand le contenu sera finalisé.  

> [!Tip]  
> Pour recevoir une notification en cas de mise à jour de cette page, copiez et collez l’URL suivante dans votre lecteur de flux RSS : `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+version+1902+-+Configuration+Manager%22&locale=en-us`.



## <a name="bkmk_deprecated"></a> Fonctionnalités et systèmes d’exploitation dépréciés

Découvrez-en plus sur les changements de prise en charge avant leur implémentation dans [Éléments supprimés et dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

- L’implémentation du partage de contenu à partir d’Azure a évolué. Utilisez une passerelle de gestion cloud compatible avec le contenu en activant l’option **Autoriser la passerelle de gestion cloud à fonctionner comme un point de distribution cloud et à distribuer du contenu à partir du stockage Azure**. Vous ne pourrez pas créer de point de distribution cloud traditionnel à l’avenir.

La version 1902 n’offre plus de prise en charge pour les produits suivants :  

- Linux et UNIX en tant que client. La fin de la prise en charge a été annoncée comme déconseillée avec la [version 1802](/sccm/core/plan-design/changes/whats-new-in-version-1802#deprecation-announcement-for-linux-and-unix-client-support). Utilisez plutôt Microsoft Azure Management pour la gestion des serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.



## Infrastructure de site <a name="bkmk_infra"></a>

### <a name="client-health-dashboard"></a>Tableau de bord d’intégrité du client
<!--3599209-->
Vous déployez des mises à jour logicielles et d’autres applications pour aider à sécuriser votre environnement, mais ces déploiements atteignent seulement les clients sains. Les clients Configuration Manager non sains ont un effet négatif sur la conformité globale. Déterminer l’intégrité des clients peut s’avérer difficile en fonction du dénominateur retenu : combien d’appareils au total doivent se trouver dans votre étendue de gestion ? Par exemple, si vous découvrez tous les systèmes à partir d’Active Directory, même si certains de ces enregistrements concernent des machines mises hors service, ce processus augmente votre dénominateur. 

Vous pouvez désormais afficher un tableau de bord avec des informations sur l’intégrité des clients Configuration Manager de votre environnement. Consultez l’intégrité de vos clients, l’intégrité des scénarios et les erreurs courantes. Filtrez la vue selon plusieurs attributs, pour voir les problèmes potentiels par version du système d’exploitation et du client. 

Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**. Développez **État du client**, puis sélectionnez le nœud **Tableau de bord d’intégrité du client**. 

![Capture d’écran du tableau de bord d’intégrité du client](media/3599209-client-health-dashboard.png)

<!-- For more information, see [How to monitor clients](/sccm/core/clients/manage/monitor-clients). -->


### <a name="new-management-insight-rules"></a>Nouvelles règles des insights de gestion
La fonctionnalité des insights de gestion comportent les nouvelles règles suivantes :

- Plusieurs règles avec des recommandations sur la gestion des regroupements. Utilisez ces insights pour simplifier la gestion et améliorer les performances. Passez en revue ces nouvelles règles dans le groupe **Regroupements**.<!--3555752-->  

- **Mettez à jour des clients avec une règle prise en charge par Windows 10** dans le groupe **Gestion simplifiée**. Cette règle s’applique aux clients exécutant une version de Windows 10 qui n’est plus prise en charge. Elle inclut également les clients avec une version de Windows 10 en fin de vie (trois mois).<!--3897268-->  

<!-- For more information, see [Management insights](/sccm/core/servers/manage/management-insights). -->


### <a name="improvement-to-enhanced-http"></a>Amélioration apportée à HTTP avancé
<!--3798957-->
Vous pouvez maintenant activer HTTP avancé par site principal ou pour le site d’administration centrale. 

Dans les propriétés du site d'administration centrale, sélectionnez l’option **Utiliser les certificats générés par Configuration Manager pour les systèmes de site HTTP**. Ce paramètre s’applique uniquement aux rôles de système de site dans le site d’administration centrale. Il ne s’agit pas d’un paramètre global pour la hiérarchie. 

<!-- For more information, see [enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http). -->


### <a name="improvement-to-setup-prerequisites"></a>Amélioration apportée aux prérequis de l’installation
Désormais, quand vous installez la version 1902 ou effectuez une mise à jour vers celle-ci, le programme d’installation de Configuration Manager contient la vérification des prérequis suivante :

- **Redémarrage du système en attente sur le serveur SQL distant** : Cette vérification des prérequis est similaire à la règle **Redémarrage du système en attente**, mais elle vérifie un serveur SQL distant. Pour plus d’informations, voir [Liste des vérifications des prérequis](/sccm/core/servers/deploy/install/list-of-prerequisite-checks#pending-system-restart-on-the-remote-sql-server). <!--SCCMDocs-pr issue 3377-->  



## <a name="bkmk_cloud"></a> Gestion associée au cloud

### <a name="stop-cloud-service-when-it-exceeds-threshold"></a>Arrêter le service cloud quand il dépasse le seuil
<!--3735092-->
Configuration Manager peut désormais arrêter un service de passerelle de gestion cloud quand le transfert de données total dépasse votre limite. La passerelle de gestion cloud a toujours eu des alertes pour déclencher des notifications quand l’utilisation atteint des niveaux d’avertissement ou critiques. Pour aider à réduire les coûts Azure imprévus en raison d’un pic d’utilisation, cette nouvelle option désactive le service cloud. 

[Configurez des alertes de trafic sortant](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts) sur CMG, puis activez l’option **Arrêter ce service quand il dépasse le seuil critique**.  

<!-- For more information, see [Set up outbound traffic alerts](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway#set-up-outbound-traffic-alerts). -->


### <a name="use-azure-resource-manager-for-cloud-services"></a>Utiliser Azure Resource Manager pour les services cloud
<!--3605704-->
Depuis la version 1810, le déploiement de services Classic dans Azure était déprécié pour une utilisation dans Configuration Manager. Cette version est la dernière à prendre en charge la création de ces déploiements Azure. 

Les déploiements existants continuent de fonctionner. À compter de cette version de la branche actuelle, Azure Resource Manager est le seul mécanisme de déploiement pour les nouvelles instances de la passerelle de gestion cloud et du point de distribution cloud.

<!-- For more information, see [Azure Resource Manager for the cloud management gateway](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).   -->


### <a name="add-cloud-management-gateway-to-boundary-groups"></a>Ajouter une passerelle de gestion cloud à des groupes de limites
<!--3640932-->
Vous pouvez maintenant associer une passerelle de gestion cloud à un groupe de limites. Cette configuration permet aux clients d’utiliser la passerelle de gestion cloud par défaut ou comme passerelle de secours pour la communication cliente en fonction des relations de groupes de limites. Ce comportement est particulièrement utile dans les scénarios de filiale ou de VPN. Vous pouvez diriger le trafic client de façon à éviter les liaisons WAN coûteuses et lentes afin d’utiliser à la place des liens Internet plus rapides vers Microsoft Azure.

<!-- For more information, see [Plan for the CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). -->



## <a name="bkmk_real"></a> Gestion en temps réel

### <a name="run-cmpivot-from-the-central-administration-site"></a>Exécuter CMPivot à partir du site d’administration centrale
<!--3610960-->
***[Mis à jour]*** Configuration Manager prend désormais en charge l’exécution de CMPivot à partir du site d’administration centrale dans une hiérarchie. Le site principal gère néanmoins toujours la communication avec le client. Lors de l’exécution de CMPivot à partir du site d’administration centrale, il communique avec le site principal via le canal d’abonnement aux messages à haut débit. Cette communication ne repose pas sur la réplication SQL standard entre les sites.

Pour plus d’informations, consultez [CMPivot pour les données en temps réel](/sccm/core/servers/manage/cmpivot#bkmk_cmpivot1902).


### <a name="edit-or-copy-powershell-scripts"></a>Modifier ou copier des scripts PowerShell
<!--3705507-->
Vous pouvez maintenant **Modifier** ou **Copier** un script PowerShell existant utilisé avec la fonctionnalité Exécuter les scripts. Désormais, au lieu de recréer un script que vous devez changer, modifiez-le directement. Les deux actions utilisent la même expérience d’Assistant que lors de la création d’un script. Quand vous modifiez ou copiez un script, Configuration Manager ne conserve pas l’état d’approbation. 

<!-- For more information, see [Run Scripts](/sccm/apps/deploy-use/create-deploy-scripts). -->



## <a name="bkmk_content"></a> Gestion de contenu

### <a name="distribution-point-maintenance-mode"></a>Mode maintenance des points de distribution 
<!--3555754-->
Vous pouvez désormais définir un point de distribution en mode maintenance. Activez le mode maintenance lors de l’installation de mises à jour logicielles ou de modifications matérielles apportées au serveur.

Pendant que le point de distribution est en mode maintenance, il a les comportements suivants : 

- Le site ne lui distribue aucun contenu.  

- Les points de gestion ne retournent pas l’emplacement de ce point de distribution aux clients. 

- Quand vous mettez à jour le site, un point de distribution en mode maintenance se met néanmoins à jour. 

- Les propriétés du point de distribution sont en lecture seule. Par exemple, vous ne pouvez pas changer le certificat ou ajouter des groupes de limites.  

- Les tâches planifiées, comme la validation de contenu, s’exécutent néanmoins toujours selon la même planification. 

<!-- For more information, see [Maintenance mode](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_maint) -->



## <a name="bkmk_client"></a> Gestion des clients

### <a name="client-provisioning-mode-timeout"></a>Délai d’expiration du mode de provisionnement de client
<!--3197824-->
La séquence de tâches définit un horodatage quand elle place le client en mode de provisionnement. Un client en mode de provisionnement vérifie toutes les 60 minutes la durée de temps écoulée depuis l’horodatage. S’il a été en mode de provisionnement pendant plus de 48 heures, le client quitte automatiquement le mode de provisionnement et redémarre son processus. 

<!-- For more information, see ... -->

### <a name="view-first-screen-only-during-remote-control"></a>Afficher le premier écran uniquement pendant le contrôle à distance
<!--3231732-->
***[Mis à jour]*** Lors de la connexion à un client avec deux moniteurs ou plus, il peut être difficile de les voir tous dans la visionneuse de contrôle à distance Configuration Manager. Un opérateur d’outils à distance peut désormais choisir entre l’affichage de **Tous les écrans** ou uniquement le **Premier écran**.

Pour plus d’informations, consultez [Guide pratique pour administrer à distance un ordinateur client Windows](/sccm/core/clients/manage/remote-control/remotely-administer-a-windows-client-computer). 


### <a name="specify-a-custom-port-for-peer-wakeup"></a>Spécifier un port personnalisé pour mettre en éveil le pair
<!--3605925-->
Vous pouvez désormais spécifier un numéro de port personnalisé pour le proxy de sortie de veille. Dans le groupe **Gestion de l’alimentation** des paramètres du client, configurez le paramètre **Numéro de port Wake On LAN (UDP)**.  

<!-- For more information, see [How to configure Wake on LAN](/sccm/core/clients/deploy/configure-wake-on-lan). -->



<!-- ## <a name="bkmk_comgmt"></a> Co-management -->




<!-- ## <a name="bkmk_compliance"></a> Compliance settings -->



## <a name="bkmk_app"></a> Gestion des applications

### <a name="improvements-to-application-approvals-via-email"></a>Améliorations des approbations d’applications par e-mail
<!--3594063-->
Dans cette version, la fonctionnalité a été améliorée afin de recevoir des notifications par e-mail pour les requêtes d’application. Les utilisateurs peuvent toujours ajouter un commentaire à la requête depuis le Centre logiciel. Ce commentaire s’affiche sur la requête d’application dans la console Configuration Manager. Désormais, ce commentaire s’affiche aussi dans l’e-mail. Le fait d’inclure ce commentaire dans l’e-mail permet aux approbateurs de prendre une décision plus éclairée sur l’approbation ou le refus de la requête.

<!-- For more information, see [Email notifications](/sccm/apps/deploy-use/app-approval#bkmk_email-approve). -->


### <a name="improvements-to-package-conversion-manager"></a>Améliorations apportées à Package Conversion Manager
<!-- SCCMDocs-pr issue #3357 -->
Cette version inclut les améliorations suivantes apportées à [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager) :
- L’analyse planifiée des packages s’exécute tous les 7 jours par défaut
- Applets de commande PowerShell pour l’analyse et la conversion des packages
- Corrections de bogues et améliorations d’ordre général



## <a name="bkmk_osd"></a> Déploiement de système d’exploitation


### <a name="progress-status-during-in-place-upgrade-task-sequence"></a>État de progression pendant une séquence de tâches de mise à niveau sur place
<!--3747129-->
Vous voyez maintenant une barre de progression plus détaillée pendant une séquence de tâches de mise à niveau sur place de Windows 10. Cette barre affiche la progression de l’installation de Windows qui, par ailleurs, s’effectue sans assistance pendant la séquence de tâches. Les utilisateurs ont désormais une certaine visibilité de la progression sous-jacente. Cela est utile en cas de problèmes de suspension du processus de mise à niveau en raison de l’absence d’indication de progression.  

![Exemple de progression d’une séquence de tâches avec la progression de la mise à jour de Windows](media/3747129-installation-progress.png)

Cette fonctionnalité fonctionne avec n’importe quelle version prise en charge de Windows 10 et uniquement avec la séquence de tâches de mise à niveau sur place. 


### <a name="improvements-to-task-sequence-media-creation"></a>Améliorations apportées à la création d’un média de séquence de tâches 
<!--3556027, fka 1359388-->
Cette version inclut plusieurs améliorations pour vous aider à mieux créer et gérer le média de séquence de tâches. <!-- For more information, see [Create task sequence media](/sccm/osd/deploy-use/create-task-sequence-media). -->

#### <a name="specify-temporary-storage"></a>Spécifier le stockage temporaire
Quand vous créez un média de séquence de tâches, personnalisez l’emplacement utilisé par le site pour le stockage temporaire des données. Ce processus peut nécessiter une quantité importante d’espace disque temporaire. Ce changement vous permet de choisir où stocker ces fichiers temporaires de manière plus flexible. 

Dans l’**Assistant Création d’un média de séquence de tâches**, spécifiez un emplacement pour le **Dossier intermédiaire**. Par défaut, cet emplacement est semblable au suivant : `%UserProfile%\AppData\Local\Temp`.

#### <a name="add-a-label-to-the-media"></a>Ajouter une étiquette au média
Vous pouvez maintenant ajouter une étiquette au média de séquence de tâches. Cette étiquette vous permet de mieux identifier le média une fois celui-ci créé. Dans l’**Assistant Création d’un média de séquence de tâches**, spécifiez l’**Étiquette du média**.


### <a name="import-a-single-index-of-an-os-image"></a>Importer un index unique d’une image de système d’exploitation
<!--3719699-->
Lors de l’importation d’un fichier image (WIM) de Windows dans Configuration Manager, vous pouvez désormais spécifier d’importer automatiquement un seul index au lieu de tous les index de l’image dans le fichier. Cette option offre les avantages suivants :

- Fichier d’image plus petit  
- Maintenance hors connexion plus rapide  
- Optimiser la maintenance des images, pour obtenir un fichier d’image plus petit après la maintenance hors connexion 

Lorsque vous importez une image de système d’exploitation, sélectionnez l’option **Extraire un index d’images spécifique à partir du fichier WIM spécifié**. Ensuite, sélectionnez l’index d’image dans la liste.  

<!-- For more information, see [Add an OS image](/sccm/osd/get-started/manage-operating-system-images#BKMK_AddOSImages). -->


### <a name="optimized-image-servicing"></a>Maintenance optimisée des images
<!--3555951-->
Quand vous appliquez des mises à jour logicielles à une image de système d’exploitation, une nouvelle option permet d’optimiser la sortie en supprimant les mises à jour remplacées. L’optimisation de la maintenance hors connexion s’applique seulement à des images avec un seul index. 

Lorsque vous créez une planification pour mettre à jour une image de système d’exploitation, sélectionnez l’option **Supprimer les mises à jour remplacées après la mise à jour de l’image**. 

<!-- For more information, see [Apply software updates to an image](/sccm/osd/get-started/manage-operating-system-images#BKMK_OSImagesApplyUpdates).  -->


### <a name="improvements-to-run-powershell-script-task-sequence-step"></a>Améliorations apportées à l’étape de séquence de tâches Exécuter le script PowerShell
<!--3556028, fka 1359389-->
L’étape de séquence de tâches **Exécuter le script PowerShell** inclut désormais les améliorations suivantes :  

- Vous pouvez maintenant entrer directement le code Windows PowerShell à cette étape. Ce changement vous permet d’exécuter des commandes PowerShell durant une séquence de tâches sans devoir au préalable créer et distribuer un package avec le script.

- Lorsque vous choisissez l’option **Entrer un script PowerShell**, sélectionnez **Modifier le script**. La nouvelle fenêtre de script PowerShell propose les actions suivantes :  

    - Modifier le script directement  

    - Ouvrir un script existant depuis un fichier  

    - Accéder à un script approuvé existant dans Configuration Manager

- Enregistrer la sortie du script dans une variable de séquence de tâches personnalisée  

- Pour inclure les paramètres de script dans le journal de séquence de tâches, définissez la variable de séquence de tâches **OSDLogPowerShellParameters** sur **TRUE**. Par défaut, les paramètres ne sont pas dans le journal.  

- Autres améliorations offrant des fonctionnalités similaires à l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine). Par exemple, spécifiez d’autres informations d’identification d’un utilisateur ou un délai d’expiration. 

> [!Important]  
> Pour tirer pleinement parti de cette nouvelle fonctionnalité Configuration Manager, commencez par mettre à jour les clients avec la dernière version. Bien que les nouvelles fonctionnalités apparaissent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version des clients n’est pas également la plus récente.

<!-- For more information, see [Run PowerShell Script](/sccm/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript). -->


### <a name="other-improvements-to-os-deployment"></a>Autres améliorations apportées au déploiement du système d’exploitation
<!--3633146,3641475,3654172,3734270-->
Cette version comprend les améliorations suivantes du déploiement de système d’exploitation :

- Il existe une nouvelle action **Affichage** par défaut sur les séquences de tâches. <!--3633146-->  

- La boîte de dialogue Erreur d’exécution de la séquence de tâches affiche désormais plus d’informations. Elle montre le nom de l’étape de la séquence de tâches qui a échoué. <!--3641475-->  

- Quand vous définissez la variable de séquence de tâches **OSDDoNotLogCommand** sur true, la ligne de commande de l’étape Exécuter la ligne de commande est également masquée dans le fichier journal. Avant, seul le nom du programme de l’étape Installer le package était masqué dans le fichier smsts.log.<!--3654172-->  

- Quand vous activez un répondeur PXE sur un point de distribution sans service de déploiement Windows, il peut désormais se trouver sur le même serveur que le service DHCP. <!--3734270-->  <!-- For more information, see ... -->



## <a name="bkmk_userxp"></a> Centre logiciel

### <a name="replace-toast-notifications-with-dialog-window"></a>Remplacer les notifications toast par une fenêtre de dialogue
<!--3555947-->
Parfois, les utilisateurs ne voient pas la notification toast Windows relative à un redémarrage ou à un déploiement obligatoire. Ils ne voient pas non plus l’expérience qui permet de répéter le rappel. Ce comportement peut entraîner une mauvaise expérience utilisateur quand le client atteint une échéance.

Maintenant, quand des déploiements nécessitent un redémarrage ou quand des changements logiciels sont nécessaires, vous pouvez utiliser une fenêtre de dialogue plus intrusive. 

#### <a name="software-changes-are-required"></a>Des changements logiciels sont nécessaires
Dans la page **Expérience utilisateur** de l’Assistant Déploiement logiciel, sélectionnez l’option de notification utilisateur **Afficher dans le Centre logiciel et afficher toutes les notifications**. Sélectionnez ensuite l’option suivante : **Quand des changements logiciels sont nécessaires, présenter une fenêtre de dialogue à l’utilisateur au lieu d’une notification toast**.  

<!-- For more information, see [Configure Software Center](/sccm/apps/plan-design/plan-for-and-configure-application-management#bkmk_userex) -->

#### <a name="restart-required"></a>Redémarrage nécessaire
Dans le groupe **Redémarrage de l’ordinateur** des paramètres du client, activez l’option suivante : **Quand un déploiement nécessite un redémarrage, présenter une fenêtre de dialogue à l’utilisateur au lieu d’une notification toast**.  

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#computer-restart). -->


### <a name="configure-user-device-affinity-in-software-center"></a>Configurer l’affinité entre utilisateur et appareil dans le Centre logiciel
<!--3485366-->
Grâce aux [améliorations de l’infrastructure du Centre logiciel](/sccm/core/plan-design/changes/whats-new-in-version-1806#software-center-infrastructure-improvements) depuis la version 1806, les rôles de serveur de site du catalogue d’applications ne sont plus nécessaires pour la plupart des scénarios. Certains clients se servaient toujours du catalogue d’applications pour permettre aux utilisateurs de définir leur appareil principal pour l’affinité utilisateur/appareil. 

Désormais, les utilisateurs peuvent définir leur appareil principal dans le Centre logiciel. Cette action définit l’utilisateur comme utilisateur principal de l’appareil dans Configuration Manager.

<!-- For more information, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity). -->


### <a name="configure-default-views-in-software-center"></a>Configurer des vues par défaut dans le Centre logiciel
<!--3612112-->
Cette version de Configuration Manager améliore la façon dont vous pouvez personnaliser le Centre logiciel :
 
- Définir la disposition par défaut des applications, sous forme de vignettes ou de liste  

    - Si un utilisateur change cette configuration, le Centre logiciel conserve les préférences de l’utilisateur  

- Configurer le filtre d’application par défaut : toutes les applications ou uniquement les applications obligatoires  

    - Le Centre logiciel utilise toujours votre paramètre par défaut. Les utilisateurs peuvent changer ce filtre, mais le Centre logiciel ne conserve pas leurs préférences.    

Spécifiez ces paramètres dans le groupe **Centre logiciel** des paramètres du client.

<!-- For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-center). -->



## <a name="bkmk_sum"></a> Mises à jour logicielles

### <a name="specify-priority-for-feature-updates-in-windows-10-servicing"></a>Spécifier la priorité des mises à jour de fonctionnalités lors de la maintenance de Windows 10
<!--3734525-->
***[Mis à jour]*** Ajustez la priorité avec laquelle les clients installent une mise à jour de fonctionnalité via [Maintenance de Windows 10](/sccm/osd/deploy-use/manage-windows-as-a-service). Par défaut, les clients installent désormais les mises à jour de fonctionnalité avec une priorité de traitement plus élevée. 

Utilisez les paramètres du client pour configurer cette option. Dans le groupe **Mises à jour logicielles**, configurez le paramètre suivant : **Spécifier la priorité du thread pour les mises à jour des fonctionnalités**. 

Pour plus d’informations, consultez [À propos des paramètres client](/sccm/core/clients/deploy/about-client-settings#software-updates). 



## <a name="bkmk_o365"></a> Gestion d’Office

### <a name="redirect-windows-known-folders-to-onedrive"></a>Rediriger les dossiers Windows connus vers OneDrive
<!--3556021-->
***[Mis à jour]*** Utilisez Configuration Manager pour déplacer les dossiers Windows connus vers OneDrive Entreprise. Ces dossiers sont les suivants : Bureau, Documents et Images. Pour simplifier vos mises à niveau Windows 10, déployez ces paramètres sur les clients Windows 7 avant de déployer une séquence de tâches. 

Pour plus d’informations sur cette fonctionnalité de OneDrive Entreprise, consultez [Rediriger et déplacer les dossiers Windows connus vers OneDrive](https://docs.microsoft.com/onedrive/redirect-known-folders).

Tout d’abord, [rechercher votre ID de locataire Office 365](https://docs.microsoft.com/onedrive/find-your-office-365-tenant-id). Déployez ensuite la version de client de synchronisation OneDrive 18.111.0603.0004 ou ultérieur. Pour plus d’informations, consultez [Déployer des applications OneDrive à l’aide de System Center Configuration Manager](https://docs.microsoft.com/onedrive/deploy-on-windows).  

Pour créer et déployer un profil OneDrive Entreprise, dans la console Configuration Manager, accédez à l’espace de travail **Actifs et conformité**. Développez **Paramètres de conformité**, puis sélectionnez le nœud **Profils OneDrive Entreprise**.  

Pour plus d’informations, consultez la section Rediriger les dossiers Windows connus vers OneDrive dans l’article [Profils OneDrive Entreprise](/sccm/compliance/deploy-use/onedrive-profile).


### <a name="integration-for-office-365-proplus-readiness"></a>Intégration pour la préparation de Office 365 ProPlus
<!--3735402-->
***[Mis à jour]*** Utilisez Configuration Manager pour identifier les appareils avec une confiance élevée qui sont prêts à être mis à niveau vers Office 365 ProPlus. L’intégrant fournit des insights sur les éventuels problèmes de compatibilité avec les compléments et macros Office utilisés dans votre environnement. Ensuite, utilisez Configuration Manager pour déployer Office sur les appareils prêts. 

Le tableau de bord de gestion du client Office 365 présente maintenant une nouvelle vignette, **Office 365 ProPlus Upgrade Readiness**.

Pour plus d’informations, consultez le [Tableau de bord de gestion du client Office 365](/sccm/sum/deploy-use/office-365-dashboard#bkmk_o365_readiness)


### <a name="additional-languages-for-office-365-updates"></a>Langues supplémentaires pour les mises à jour Office 365
<!--3555955-->
Configuration Manager prend désormais en charge toutes les langues prises en charge pour les mises à jour du client Office 365. Le workflow mis à jour sépare désormais les 38 langues de **Windows Update** des nombreuses langues de la **Mise à jour du client Office 365**. 

Pour plus d’informations, consultez [Gérer les mises à jour d’Office 365](/sccm/sum/deploy-use/manage-office-365-proplus-updates#bkmk_o365_lang)


### <a name="office-products-on-lifecycle-dashboard"></a>Produits Office sur le tableau de bord Cycle de vie
<!--3556026-->
Le tableau de bord Cycle de vie du produit inclut maintenant des informations pour les versions installées d’Office 2003 à Office 2016. Les données s’affichent quand le site a exécuté la tâche de synthèse du cycle de vie, ce qui se produit toutes les 24 heures.

<!-- For more information, see [Use the Product Lifecycle dashboard](/sccm/core/clients/manage/asset-intelligence/product-lifecycle-dashboard). -->



<!-- ## <a name="bkmk_inv"></a> Inventory -->



## <a name="bkmk_pod"></a> Déploiements par phases

### <a name="dedicated-monitoring-for-phased-deployments"></a>Supervision dédiée pour les déploiements par phases
<!--3555949-->
Les déploiements par phases ont désormais leur propre nœud de supervision dédiée. Ce nœud facilite l’identification des déploiements par phases que vous avez créés, puis l’accès à la vue de supervision des déploiements par phases. Dans la console Configuration Manager, accédez à l’espace de travail **Supervision**, puis sélectionnez le nœud **Déploiements par phases**. Il montre la liste des déploiements par phases.

<!-- For more information, see [Phased deployment monitoring view](/sccm/osd/deploy-use/manage-monitor-phased-deployments#bkmk_monitor). -->


### <a name="improvement-to-phased-deployment-success-criteria"></a>Amélioration des critères de réussite du déploiement par phases
<!--3555946-->
Spécifiez des critères supplémentaires pour la réussite d’une phase d’un déploiement par phases. Au lieu d’être juste un pourcentage, ce critère peut maintenant être aussi le nombre d’appareils déployés. Cette option est utile si la taille de la collection est variable et que vous avez un nombre spécifique d’appareils dont afficher la réussite avant de passer à la phase suivante. 

Créez un déploiement par phases pour une séquence de tâches, une mise à jour logicielle ou une application. Puis, dans la page Paramètres de l’Assistant, sélectionnez l’option suivante comme critères de réussite de la première phase : **Nombre d’appareils déployés**. 

<!-- For more information, see [Create phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence). -->



## <a name="bkmk_admin"></a> Console Configuration Manager

### <a name="bkmk_console"></a> Améliorations apportées à la console Configuration Manager
<!--3594151-->
Suite aux commentaires des clients lors de l’édition 2018 de la conférence Desert Midwest Management Summit (MMS), cette version inclut les améliorations suivantes à la console Configuration Manager :
- Agrandir la fenêtre Parcourir le registre pour les méthodes de détection d’application
- Accéder au regroupement à partir d’un déploiement d’application
- Supprimer le contenu de la surveillance de l’état
- Tri des vues par des valeurs entières dans le nœud **Déploiements** de l’espace de travail **Analyse**
- Déplacer l’avertissement pour un grand nombre de résultats

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="configuration-manager-console-notifications"></a>Notifications de la console Configuration Manager
<!--3556016, fka 1318035-->
Pour mieux vous tenir informer et vous permettre de prendre les mesures appropriées, la console Configuration Manager vous notifie désormais de l’existence des événements suivants :
- Mise à jour disponible pour Configuration Manager
- Événements de cycle de vie et de maintenance dans l’environnement

Cette notification se présente sous la forme d’une barre située dans la partie supérieure de la fenêtre de console, sous le ruban. Elle remplace l’expérience précédente associée à la disponibilité de mises à jour Configuration Manager. Ces notifications dans la console affichent toujours des informations critiques, mais n’interfèrent pas avec votre travail dans la console. Vous ne pouvez pas faire disparaître les notifications critiques. La console affiche toutes les notifications dans une nouvelle zone de notification de la barre de titre. 

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="confirmation-of-console-feedback"></a>Confirmation de commentaires de la console
<!--3556010-->
***[Mis à jour]*** Quand vous envoyez des [commentaires](/sccm/core/understand/find-help#product-feedback) dans la console Configuration Manager, elle affiche désormais un message de confirmation. Ce message inclut un **ID de commentaire** que vous pouvez donner à Microsoft comme identificateur de suivi.

Pour plus d’informations, consultez [Commentaires produit](/sccm/core/understand/find-help#bkmk_feedbackid).


### <a name="view-recently-connected-consoles"></a>Afficher les consoles récemment connectées 
<!--3699367-->
***[Mis à jour]*** Vous pouvez désormais voir les connexions les plus récentes pour la console Configuration Manager. La vue comprend les connexions actives et les consoles récemment connectées. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Sécurité**, puis choisissez le nœud **Connexions à la console**.

Pour plus d’informations, consultez [Utilisation de la console Configuration Manager](/sccm/core/servers/manage/admin-console#bkmk_viewconnected).


### <a name="in-console-documentation-dashboard"></a>Tableau de bord Documentation dans la console
<!--3556019, fka 1357546-->
Un nouveau nœud **Documentation** figure dans le nouvel espace de travail **Communauté**. Ce nœud contient des informations à jour sur la documentation et les articles de support Configuration Manager.

<!-- For more information, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console). -->


### <a name="search-device-views-using-mac-address"></a>Vues de recherche d’appareils avec une adresse MAC
<!--3600878-->
Vous pouvez désormais rechercher une adresse MAC dans une vue des appareils de la console Configuration Manager. Cette propriété est utile pour les administrateurs de déploiement de système d’exploitation lors de la résolution des problèmes de déploiements PXE. Quand vous voyez une liste d’appareils, ajoutez la colonne **Adresse MAC** à la vue. Utilisez le champ de recherche pour ajouter le critère de recherche **Adresse MAC**. 


### <a name="use-net-47-for-improved-console-accessibility"></a>Utilisez .NET 4.7 pour une meilleure accessibilité de la console
<!-- SCCMDocs-pr issue #3228 -->
Pour améliorer les fonctionnalités d’accessibilité de la console Configuration Manager, mettez à jour .NET avec la version 4.7 ou versions ultérieures sur l’ordinateur qui exécute la console. 

Pour plus d’informations, consultez [Fonctionnalités d’accessibilité dans Configuration Manager](/sccm/core/understand/accessibility-features).


### <a name="changes-to-console-setup-process"></a>Modifications apportées au processus de configuration de la console

<!-- 3612513 -->
***[Mis à jour]*** De nouveaux composants sont requis lors de la configuration de la console Configuration Manager. Si vous créez un package pour configurer la console sur d’autres ordinateurs, assurez-vous que le package inclut les fichiers suivants :

- ConsoleSetup.exe
- AdminConsole.msi
- ConfigMgr.AC_Extension.i386.cab
- ConfigMgr.AC_Extension.amd64.cab

Quand vous configurez ou mettez à jour un serveur de site, il copie ces fichiers d’installation ainsi que les modules linguistiques pris en charge pour le site dans le sous-dossier **Tools\ConsoleSetup**. Pour plus d’informations, consultez [Installer la console Configuration Manager](/sccm/core/servers/deploy/install/install-consoles).



<!-- ## <a name="bkmk_opmdm"></a> On-premises MDM -->




## <a name="other-updates"></a>Autres mises à jour

En plus des nouvelles fonctionnalités, cette version inclut également des modifications supplémentaires comme des corrections de bogues. Pour plus d’informations, consultez [Récapitulatif des changements dans Configuration Manager Current Branch, version 1902](https://support.microsoft.com/help/4498910).

Pour plus d’informations sur les modifications apportées aux applets de commande Windows PowerShell pour Configuration Manager, consultez [Notes de publication pour PowerShell version 1902](https://docs.microsoft.com/powershell/sccm/1902-release-notes?view=sccm-ps).

<!-- 
The following update rollup (4486457) is available in the console starting on 25 January 2019: [Update rollup for Configuration Manager current branch, version 1902](https://support.microsoft.com/help/4486457).


### Hotfixes

The following additional hotfixes are available to address specific issues:

| ID | Title | Date | In-console |
|---------|---------|---------|---------|
| [4487960](https://support.microsoft.com/help/4487960) | Microsoft Intune connector certificate does not renew in Configuration Manager | 18 January 2019 | Yes |
 
-->



## <a name="next-steps"></a>Étapes suivantes

Quand vous êtes prêt à installer cette version, consultez [Installer des mises à jour pour Configuration Manager](/sccm/core/servers/manage/updates) et [Liste de contrôle pour installer la mise à jour 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902).

> [!TIP]  
> Pour installer un nouveau site, utilisez une version de base de référence de Configuration Manager.  
>
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](/sccm/core/servers/deploy/install/installing-sites)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Pour plus d’informations sur les problèmes importants et connus, consultez les [Notes de publication](/sccm/core/servers/deploy/install/release-notes).

Après avoir mis à jour un site, consultez également la [Liste de contrôle post-mise à jour](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist).
