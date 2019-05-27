---
title: Nouvelle version 1702
titleSuffix: Configuration Manager
description: Obtenez des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1702 de System Center Configuration Manager.
ms.date: 05/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 409e26e1-7716-4f1d-a0ee-34feabf20792
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55e29269bab2ed1a75f00848a59f3345d0a8c071
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65495148"
---
# <a name="what39s-new-in-version-1702-of-system-center-configuration-manager"></a>Nouveautés de la version 1702 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La mise à jour 1702 de la version Current Branch de System Center Configuration Manager est une mise à jour dans la console des sites déjà installés qui exécutent la version 1602, 1606 ou 1610. Elle est également disponible sous la forme d’une version de ligne de base, que vous pouvez utiliser lors de l’installation d’un nouveau déploiement.

> [!TIP]  
> Pour installer un nouveau site, vous devez utiliser une version de base de Configuration Manager.  
>  Informations supplémentaires :    
>   - [Installation de nouveaux sites](https://technet.microsoft.com/library/mt590197.aspx)  
>   - [Installation de mises à jour sur les sites](https://technet.microsoft.com/library/mt607046.aspx)  
>   - [Versions de base et de mise à jour](/sccm/core/servers/manage/updates#a-namebkmkbaselinesa-baseline-and-update-versions)  

Les sections suivantes fournissent des détails sur les modifications et les nouvelles fonctionnalités introduites dans la version 1702 de Configuration Manager.  

## <a name="deprecated-features-and-operating-systems"></a>Fonctionnalités et systèmes d'exploitation déconseillés
Découvrez plus d’informations sur les changements de prise en charge avant leur implémentation dans [Éléments supprimés et dépréciés](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated).

La version 1702 n’offre plus de prise en charge pour les produits suivants :
- **SQL Server 2008 R2**, pour les serveurs de base de données de site. La fin de la prise en charge a été [annoncée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-support-for-sql-server-versions-as-a-site-database) le 10 juillet 2015. Cette version de SQL Server reste prise en charge si vous utilisez une version de Configuration Manager antérieure à la version 1702.
- **Windows Server 2008 R2**, pour les serveurs de système de site et la plupart des rôles de système de site. La fin de la prise en charge a été [annoncée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) le 10 juillet 2015. Cette version de Windows reste prise en charge si vous utilisez une version de Configuration Manager antérieure à la version 1702.  
- **Windows Server 2008**, pour les serveurs de système de site et la plupart des rôles de système de site. La fin de la prise en charge a été [annoncée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-server#deprecated-server-operating-systems) le 10 juillet 2015.
- **Windows XP Embedded**, en tant que système d’exploitation client. La fin de la prise en charge a été [annoncée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-client#deprecated-client-operating-systems) le 10 juillet 2015. Cette version de Windows reste prise en charge si vous utilisez une version de Configuration Manager antérieure à la version 1702.




## <a name="site-infrastructure"></a>Infrastructure de site

### <a name="improvements-for-in-console-search"></a>Améliorations apportées à la recherche dans la console
Voici des améliorations apportées à l’utilisation de la recherche dans la console Configuration Manager :
 - **Chemin d’accès de l’objet :**  
  De nombreux objets prennent désormais en charge une colonne nommée **Chemin d’accès de l’objet**.  Quand vous effectuez des recherches et incluez cette colonne dans les résultats d’affichage, vous pouvez afficher le chemin d’accès à chaque objet. Par exemple, si vous exécutez une recherche d’applications dans le nœud Applications et également dans les sous-nœuds, la colonne *Chemin d’accès de l’objet* dans le volet des résultats affiche le chemin d’accès à chaque objet retourné.   

- **Conservation du texte recherché :**  
  Quand vous entrez du texte dans la zone de recherche, puis que vous changez la zone dans laquelle effectuer la recherche (d’un sous-nœud au nœud actuel), le texte saisi est désormais conservé et vous n’avez pas à le retaper.

- **Maintien de votre décision d’effectuer des recherches dans les sous-nœuds :**  
 L’option que vous choisissez pour effectuer des recherches dans le *nœud actuel* ou *tous les sous-nœuds* est désormais conservée quand vous changez le nœud dans lequel vous travaillez. Ce nouveau comportement signifie que vous n’avez pas besoin de réinitialiser constamment la décision quand vous parcourez la console. Par défaut, quand vous ouvrez la console, l’option consiste à effectuer des recherches uniquement dans le nœud actuel.


### <a name="send-feedback-from-the-configuration-manager-console"></a>Envoyer des commentaires à partir de la console Configuration Manager

 Vous pouvez utiliser les options de commentaires dans la console pour envoyer vos commentaires directement à l’équipe de développement.

 L’option **Commentaires** est accessible :
- Dans le ruban, à l’extrême gauche de l’onglet Accueil de chaque nœud.  
  ![Ruban](./media/feedback-home.png)

- Quand vous cliquez avec le bouton droit sur n’importe quel objet dans la console.   
   ![Option de clic droit](./media/feedback-option.png)   

  Un clic sur **Commentaires** affiche le site de commentaires [Configuration Manager UserVoice dans votre navigateur](https://go.microsoft.com/fwlink/?linkid=617029).


###  <a name="changes-for-updates-and-servicing"></a>Modifications pour les mises à jour et la maintenance
Voici des modifications apportées aux mises à jour et à la maintenance :

- **Emplacement du nœud**   
  Après avoir installé la version 1702, le nœud **Mises à jour et maintenance** apparaît comme un nœud de niveau supérieur sous **Administration**. Il n’est plus un nœud enfant situé sous **Services de cloud**.

- **Nouveaux états de mise à jour**  
  Lorsque vous affichez les mises à jour disponibles dans la console, deux nouveaux états apparaissent :  
  - **Disponible pour l’installation** : il s’agit d’une mise à jour qui a été téléchargée et qui est prête à être installée.
  - **Prêt pour le téléchargement** : cette mise à jour est disponible mais n’a pas été téléchargée. Vous pouvez choisir de télécharger cette mise à jour, mais elle a été remplacée par une mise à jour plus récente.


- **Choix de mise à jour plus simples**  
  Si votre infrastructure est en droit de recevoir plusieurs mises à jour, seule la dernière mise à jour est téléchargée. Par exemple, si le numéro de version actuel de votre site est inférieur de deux ou plus à la version la plus récente disponible, seule cette dernière version de mise à jour est téléchargée automatiquement.  

  Vous pouvez choisir de télécharger et d’installer les autres mises à jour disponibles, même quand il ne s’agit pas de la version la plus récente. Si vous téléchargez une mise à jour plus ancienne, vous recevrez un message d’avertissement indiquant que la mise à jour a été remplacée par une version plus récente. Pour télécharger une mise à jour qui est *Disponible en téléchargement*, sélectionnez la mise à jour dans la console, puis cliquez sur **Télécharger**.

- **Nettoyage amélioré des anciennes mises à jour**   
  Nous avons ajouté une fonction de nettoyage automatique qui supprime les téléchargements inutiles du dossier « EasySetupPayload » sur votre serveur de site. Puisqu’elle a été introduite avec la version 1702, la fonction de nettoyage commence à fonctionner après l’installation d’une mise à jour comme un correctif cumulatif ou une version de mise à jour ultérieure.  


### <a name="data-warehouse-service-point"></a>Point de service de l’entrepôt de données
 Utilisez le point de service de l’entrepôt de données pour stocker des données d’historique à long terme et créer des rapports sur celles-ci pour votre déploiement de Configuration Manager.

 L’entrepôt de données prend en charge jusqu’à 2 To de données, avec des horodatages pour le suivi des modifications. Pour stocker des données, vous utilisez des synchronisations automatisées entre la base de données du site Configuration Manager et la base de données de l’entrepôt de données. Ces informations sont ensuite accessibles à partir de votre point de Reporting Services.

 Pour en savoir plus, consultez la section relative au [point de service de l’entrepôt de données](/sccm/core/servers/manage/data-warehouse).


### <a name="peer-cache-improvements"></a>Améliorations de Cache d’homologue
 À compter de la version 1702, un ordinateur source de cache d’homologue rejette une demande de contenu quand il remplit l’une des conditions suivantes :  
  -  Il est en mode de batterie faible.
  -  La charge de l’UC dépasse 80 % au moment où le contenu est demandé.
  -  Les E/S disque ont une valeur *AvgDiskQueueLength* supérieure à 10.
  -  Il n’y a plus de connexion disponible vers l’ordinateur.   
Pour plus d’informations, consultez **Accès limité à une source de cache d’homologue** dans [Cache d’homologue pour les clients Configuration Manager](/sccm/core/plan-design/hierarchy/client-peer-cache).   

En outre, trois nouveaux rapports sont ajoutés à votre point de rapport. Vous pouvez utiliser ces rapports pour obtenir plus de détails sur les requêtes de contenu rejetées, notamment le groupe de limites, l’ordinateur et le contenu impliqués. Consultez la section [Surveillance](/sccm/core/plan-design/hierarchy/client-peer-cache#monitoring) dans la rubrique de cache d’homologue.

### <a name="content-library-cleanup-tool"></a>Outil de nettoyage de la bibliothèque de contenu
 Utilisez l’[outil de nettoyage de la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/content-library-cleanup-tool) pour supprimer du contenu des points de distribution lorsque ce contenu n’est plus associé à une application.


### <a name="use-the-oms-connector-with-the-azure-government-cloud"></a>Utiliser le connecteur OMS avec Azure Government Cloud
Vous pouvez utiliser le connecteur OMS pour vous connecter à OMS Log Analytics dans Azure Government Cloud. Pour cela, vous devez modifiez un fichier de configuration avant d’installer le connecteur OMS afin que le connecteur puisse travailler avec Government Cloud. Pour plus d’informations, consultez [Utiliser le connecteur OMS avec Azure Government Cloud](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#fairfaxconfig).

### <a name="software-update-points-are-added-to-boundary-groups"></a>Des points de mise à jour logicielle sont ajoutés aux groupes de limites
Depuis la version 1702, les clients utilisent des groupes de limites pour rechercher un nouveau point de mise à jour logicielle et pour rétablir et trouver un nouveau point de mise à jour logicielle si leur point actuel n’est plus accessible. Vous pouvez ajouter des points de mise à jour logicielle individuels à différents groupes de limites pour contrôler les serveurs qu’un client peut trouver. Pour plus d’informations, consultez la section [Points de mise à jour logicielle](/sccm/core/servers/deploy/configure/boundary-groups#software-update-points) dans la rubrique [Configuration des groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups).


<!-- ## Migration  -->

<!-- ## Client management  -->

## <a name="compliance-settings"></a>Paramètres de conformité

### <a name="new-compliance-settings-for-ios"></a>Nouveaux paramètres de conformité pour iOS

Nous avons ajouté plusieurs nouveaux paramètres afin que les appareils iOS correspondent à ceux qui sont disponibles avec Microsoft Intune.
Pour obtenir une liste de tous les paramètres disponibles, consultez [Créer des éléments de configuration pour les appareils iOS et Mac OS X gérés via Microsoft Intune](/sccm/mdm/deploy-use/create-configuration-items-for-ios-and-mac-os-x-devices-managed-without-the-client).


## <a name="application-management"></a>Gestion des applications

### <a name="improved-support-for-windows-store-for-business-apps"></a>Meilleure prise en charge des applications du Windows Store pour Entreprises

Vous pouvez désormais déployer des applications sous licence à partir du Windows Store pour Entreprises vers des PC sous Windows 10 que vous gérez à l’aide du client Configuration Manager.
Pour plus d’informations, consultez [Gérer les applications à partir du Windows Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

### <a name="check-for-running-executable-files-before-installing-an-application"></a>Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application

Dans la boîte de dialogue **Propriétés** d’un type de déploiement, sous l’onglet **Comportement à l’installation**, vous pouvez désormais spécifier un ou plusieurs fichiers exécutables qui, s’ils sont en cours d’exécution, bloqueront l’installation du type de déploiement. L’utilisateur doit fermer le fichier exécutable en cours d’exécution (ou il peut être fermé automatiquement pour les déploiements dont l’objet est défini sur Obligatoire) pour que le type de déploiement puisse être installé.

Si l’application a été déployée en tant que **Disponible** et qu’un utilisateur final tente d’installer une application, il est invité à fermer les fichiers exécutables en cours d’exécution que vous avez spécifiés avant de poursuivre l’installation.

Si l’application a été déployée en tant que **Obligatoire** et que l’option **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement** est sélectionnée, une boîte de dialogue signale à l’utilisateur que les fichiers exécutables que vous avez spécifiés seront fermés automatiquement quand l’installation de l’application arrivera à échéance.

### <a name="app-management-improvements-for-hybrid-mdm"></a>Amélioration de la gestion des applications pour la gestion des appareils mobiles hybride

- [Déployer des applications iOS achetées en volume sur des regroupements d’appareils](#deploy-volume-purchased-ios-apps-to-device-collections)
- [Prise en charge du programme d’achat en volume iOS pour l’éducation](#support-for-ios-volume-purchase-program-for-education)
- [Prise en charge de plusieurs jetons de programme d’achat en volume](#support-for-multiple-volume-purchase-program-tokens)


## <a name="operating-system-deployment"></a>Déploiement du système d'exploitation

### <a name="expire-stand-alone-media"></a>Expiration des supports autonomes
Lorsque vous créez un support autonome, de nouvelles options vous permettent de définir des dates facultatives de début et d’expiration pour ce support. Ces paramètres sont désactivés par défaut. Les dates sont comparées à l’heure système de l’ordinateur avant l’exécution du support autonome. Lorsque l’heure du système est antérieure à l’heure de début ou ultérieure à l’heure d’expiration, le support autonome n’est pas démarré. Ces options sont également disponibles avec l’applet de commande New-CMStandaloneMedia PowerShell. Pour plus d’informations, consultez [Créer un média autonome](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="package-id-displayed-in-task-sequence-steps"></a>L’’ID de package s’affiche désormais dans les séquences de tâches
Toutes les étapes de séquence de tâches qui font référence à un package, un package de pilotes, une image de système d’exploitation, une image de démarrage ou un package de mise à niveau de système d’exploitation affichent désormais l’ID de package de l’objet référencé. Lorsqu’une séquence de tâches fait référence à une application, elle affiche l’ID de l’objet.

### <a name="support-for-additional-content-in-stand-alone-media"></a>Prise en charge du contenu supplémentaire dans un média autonome
Le contenu supplémentaire est maintenant pris en charge dans le média autonome. Vous pouvez sélectionner des packages supplémentaires, des packages de pilotes et des applications en vue d’effectuer une copie intermédiaire sur les supports, ainsi que d’autres types de contenu référencés dans la séquence de tâches. Auparavant, seul le contenu référencé dans la séquence de tâches était copié sur les supports autonomes. Pour plus d’informations, consultez [Créer un média autonome](/sccm/osd/deploy-use/create-stand-alone-media).

### <a name="hardware-inventory-collects-uefi-information"></a>L’inventaire matériel collecte des informations UEFI
Une nouvelle classe d’inventaire matériel (**SMS_Firmware**) et une nouvelle propriété (**UEFI**) sont disponibles pour vous aider à déterminer si un ordinateur démarre ou non en mode UEFI. Quand un ordinateur démarre en mode UEFI, la propriété **UEFI** est définie sur **TRUE**. Cette option est activée dans l’inventaire matériel par défaut. Pour plus d’informations sur l’inventaire matériel, consultez [Guide pratique pour configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).

### <a name="improvements-to-software-center-warning-messages-for-high-impact-task-sequences"></a>Améliorations apportées aux messages d’avertissement du Centre logiciel pour les séquences de tâches à fort impact
Cette version inclut les améliorations suivantes apportées messages d’avertissement du Centre logiciel pour les séquences de tâches de déploiement à fort impact :

- Dans les propriétés de la séquence de tâches, vous pouvez maintenant configurer n’importe quelle séquence de tâches, notamment celles non liées au système d’exploitation, comme déploiement à haut risque. Toute séquence de tâches qui remplit certaines conditions est définie automatiquement comme séquence à fort impact. Pour plus d’informations, consultez [Paramètres pour gérer les déploiements à haut risque pour System Center Configuration Manager](/sccm/protect/understand/settings-to-manage-high-risk-deployments).
- Dans les propriétés de la séquence de tâches, vous pouvez choisir d’utiliser le message de notification par défaut ou créer votre propre message de notification personnalisé pour les déploiements à fort impact.
- Dans les propriétés de la séquence de tâches, vous pouvez configurer les propriétés du Centre logiciel, notamment exiger un redémarrage ou définir la taille de téléchargement de la séquence de tâches et la durée d’exécution estimée.
- Le message de déploiement à fort impact par défaut pour les mises à niveau sur place signale désormais que vos applications, vos données et vos paramètres sont migrés automatiquement. Auparavant, le message par défaut pour toute installation de système d’exploitation indiquait que tous les paramètres, les données et les applications seraient perdues, ce qui était faux pour une mise à niveau sur place.

Pour plus d’informations, consultez [Configurer des paramètres de séquence de tâches à fort impact](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#set-a-task-sequence-as-a-high-impact-task-sequence)

### <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Revenir à la page précédente en cas d’échec d’une séquence de tâches
Vous pouvez désormais revenir à une page précédente quand vous exécutez une séquence de tâches qui échoue. Avant cette version, vous deviez redémarrer la séquence de tâches en cas d’échec. Par exemple, vous pouvez utiliser le bouton **Précédent** dans les scénarios suivants :

- Quand un ordinateur démarre dans Windows PE, la boîte de dialogue d’amorçage de la séquence de tâches peut s’afficher avant que la séquence de tâches ne soit disponible. Quand vous cliquez sur Suivant dans ce scénario, la dernière page de la séquence de tâches s’affiche avec un message indiquant qu’aucune séquence de tâches n’est disponible. À présent, vous pouvez cliquer sur **Précédent** pour relancer la recherche des séquences de tâches disponibles. Vous pouvez répéter ce processus jusqu’à ce que la séquence de tâches soit disponible.
- Quand vous exécutez une séquence de tâches, mais que les packages de contenu dépendants ne sont pas encore disponibles sur les points de distribution, la séquence de tâches échoue. Vous pouvez désormais distribuer le contenu manquant (s’il ne l’a pas encore été) ou attendre qu’il soit disponible sur les points de distribution, puis cliquer sur **Précédent** pour que la séquence de tâches recherche une nouvelle fois le contenu.

### <a name="pre-cache-content-for-available-deployments-and-task-sequences"></a>Mettre préalablement en cache le contenu pour les déploiements et les séquences de tâches disponibles
Depuis la version 1702, pour les déploiements disponibles des séquences de tâches, vous pouvez choisir d’utiliser la mise en cache préalable du contenu. La mise en cache préalable du contenu permet au client de télécharger uniquement le contenu applicable dès qu’il reçoit le déploiement. Ainsi, quand l’utilisateur clique sur **Installer** dans le Centre logiciel, le contenu est prêt et l’installation démarre rapidement, car le contenu se trouve sur le disque dur local. Pour plus d’informations, consultez [Configurer la mise en cache préalable du contenu](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).

### <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Convertir du BIOS en UEFI pendant une mise à niveau sur place
Windows 10 Creators Update inclut un outil de conversion simple qui automatise le processus de repartitionnement du disque dur pour le matériel compatible UEFI et intègre l’outil de conversion dans le processus de mise à niveau sur place de Windows 7 vers Windows 10. Lorsque vous combinez cet outil avec la séquence de tâches de mise à niveau du système d’exploitation et l’outil OEM qui convertit le microprogramme du BIOS en UEFI, vous pouvez convertir vos ordinateurs du BIOS en UEFI pendant une mise à niveau sur place vers Windows 10 Creators Update. Pour plus d’informations, consultez [Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

### <a name="improvements-to-the-install-applications-task-sequence-step"></a>Améliorations apportées à l’étape de séquence de tâches Installer les applications
Cette version intègre les améliorations suivantes :
- Augmentation à 99 du nombre maximal d’applications que vous pouvez installer dans l’étape de séquence de tâches **Installer les applications**. Auparavant, le maximum était de 9 applications.
- Lorsque vous ajoutez une application dans la séquence de tâches **Installer les applications** dans l’éditeur de séquences de tâches, il vous est désormais possible de sélectionner plusieurs applications dans le volet **Sélectionner l’application à installer**.

### <a name="improvements-to-the-auto-apply-driver-task-sequence"></a>Améliorations apportées à la séquence de tâches Appliquer automatiquement les pilotes
De nouvelles variables de séquence de tâches sont désormais disponibles pour configurer le délai d’expiration dans la séquence de tâches Appliquer automatiquement les pilotes lorsque vous effectuez des demandes de catalogue HTTP. Les variables et valeurs par défaut (en secondes) suivantes sont disponibles :
   - SMSTSDriverRequestResolveTimeOut  
     Valeur par défaut : 60
   - SMSTSDriverRequestConnectTimeOut  
     Valeur par défaut : 60
   - SMSTSDriverRequestSendTimeOut  
     Valeur par défaut : 60
   - SMSTSDriverRequestReceiveTimeOut  
     Valeur par défaut : 480

### <a name="windows-10-adk-tracked-by-build-version"></a>Le kit de déploiement et d’évaluation Windows 10 (ADK) est suivi par le numéro de version
Le kit de déploiement et d’évaluation Windows 10 est désormais suivi par le numéro de version pour garantir une meilleure prise en charge lors de la personnalisation d’images de démarrage Windows 10. Par exemple, si le site utilise la version 1607 du Windows ADK pour Windows 10, seules les images de démarrage dont la version est 10.0.14393 pourront être personnalisées dans la console. Pour plus d’informations sur la personnalisation des versions de WinPE, consultez [Personnaliser les images de démarrage](/sccm/osd/get-started/customize-boot-images).

### <a name="default-boot-image-source-path-can-no-longer-be-changed"></a>Le chemin source par défaut de l’image de démarrage ne peut plus être modifié
Les images de démarrage par défaut sont gérées par Configuration Manager et le chemin source par défaut de l’image de démarrage ne peut donc plus être modifié dans la console Configuration Manager ni à l’aide du SDK Configuration Manager. Vous pouvez toutefois continuer à configurer un chemin source personnalisé pour les images de démarrage personnalisées.

### <a name="default-boot-images-are-regenerated-after-upgrading-configuration-manager-to-a-new-version"></a>Les images de démarrage par défaut sont régénérées après la mise à niveau de Configuration Manager vers une nouvelle version.
À compter de cette version, quand vous mettez à niveau la version du Windows ADK et que vous utilisez les mises à jour et la maintenance pour installer la dernière version de Configuration Manager, Configuration Manager régénère les images de démarrage par défaut. Ceci inclut la nouvelle version de Windows PE du Windows ADK mis à jour, la nouvelle version du client Configuration Manager, les pilotes, les personnalisations, etc. Les images de démarrage personnalisées ne sont pas modifiées. Pour plus d’informations, consultez [Gérer les images de démarrage](/sccm/osd/get-started/manage-boot-images#BKMK_BootImageDefault).

## <a name="software-updates"></a>Mises à jour logicielles

### <a name="deploy-office-365-apps-to-clients"></a>Déployer des applications Office 365 sur des clients
Depuis la version 1702, à partir du tableau de bord Gestion des clients Office 365, vous pouvez démarrer le programme d’installation d’Office 365 qui vous permet de configurer les paramètres d’installation Office 365, de télécharger des fichiers à partir de réseaux de distribution de contenu Office et de déployer les fichiers en tant qu’application dans Configuration Manager. Pour plus d’informations, consultez [Gérer les mises à jour Office 365 ProPlus](/sccm/sum/deploy-use/manage-office-365-proplus-updates#deploy-office-365-apps).

> [!IMPORTANT]
> L’application Office 365 que vous créez et déployez à l’aide de l'Assistant Création d'une application Office 365 dans Configuration Manager n’est pas automatiquement gérée par Configuration Manager tant que vous n’avez pas activé le paramètre de l’agent client des mises à jour logicielles **Enable management of the Office 365 Client Again**. Pour plus d’informations, consultez [À propos des paramètres du client](/sccm/core/clients/deploy/about-client-settings).

### <a name="manage-express-installation-files-for-windows-10-updates"></a>Gérer les fichiers d’installation rapide pour les mises à jour de Windows 10
Depuis la version 1702, Configuration Manager prend en charge les fichiers d’installation rapide pour les mises à jour de Windows 10. Quand vous utilisez une version prise en charge de Windows 10, vous pouvez utiliser les paramètres Configuration Manager pour télécharger uniquement les modifications entre la mise à jour cumulative de Windows 10 du mois en cours et la mise à jour du mois précédent. Sans les fichiers d’installation rapide, Configuration Manager télécharge l’intégralité de la mise à jour cumulative de Windows 10 (notamment toutes les mises à jour des mois précédents) chaque mois. L’utilisation de fichiers d’installation rapide permet des téléchargements plus petits et des durées d’installation plus courtes sur les clients. Pour plus d’informations, consultez [Gérer les fichiers d’installation rapide pour les mises à jour de Windows 10](/sccm/sum/deploy-use/manage-express-installation-files-for-windows-10-updates).


<!-- ## Reporting  -->

<!-- ## Inventory  -->

## <a name="mobile-device-management"></a>Gestion des appareils mobiles

### <a name="android-and-ios-versions-are-no-longer-targetable-in-creation-wizards-for-hybrid-mdm"></a>Les versions Android et iOS ne peuvent plus être ciblées dans les Assistants de création pour la gestion MDM hybride

Depuis la version 1702, vous n’avez plus besoin de cibler des versions Android et iOS spécifiques quand vous créez des stratégies et des profils pour des appareils gérés par Intune dans le cadre d’une gestion des appareils mobiles (MDM) hybride. Au lieu de cela, vous choisissez l’un des types d’appareils suivants :

- Android
- Samsung KNOX Standard 4.0 et versions supérieures
- iPhone
- iPad

Cette modification affecte les Assistants de création des éléments suivants :

- Éléments de configuration
- Stratégies de conformité
- Profils de certificat
- Profils de messagerie
- Profils VPN
- Profils Wi-Fi

Grâce à cette modification, les déploiements hybrides peuvent prendre en charge plus rapidement les nouvelles versions Android et iOS sans avoir besoin d’une nouvelle version de Configuration Manager ou d’une extension. Quand une nouvelle version est prise en charge dans Intune autonome, les utilisateurs peuvent mettre à niveau leurs appareils mobiles avec cette version.

Pour éviter tout problème lors de la mise à niveau de versions antérieures de Configuration Manager, les versions des systèmes d’exploitation des appareils mobiles restent disponibles dans les pages de propriétés de ces éléments. Si vous avez encore besoin de cibler une version spécifique, créez l’élément, puis spécifiez la version ciblée dans la page de propriétés du nouvel élément. 

> [!NOTE]
> La dernière version du système d’exploitation mobile disponible sur les pages de propriétés s’applique à cette version et à toutes les versions ultérieures. Les pages de propriétés offrent les options suivantes pour cibler les systèmes d’exploitation ultérieurs à Android 7 et à iOS 10 : 
> - **Android 7 et versions ultérieures**
> - **Tous les iPhone et iPod touch sous iOS 10 et versions ultérieures**
> - **Tous les iPad sous iOS 10 et versions ultérieures**

### <a name="android-for-work-support"></a>Prise en charge d’Android for Work
À partir de la version 1702, la gestion des appareils mobiles hybride avec Microsoft Intune prend désormais en charge l’inscription et la gestion des appareils Android for Work. Guide pour la gestion des appareils Android for Work :

- [Inscrire des appareils Android for Work](/sccm/mdm/deploy-use/enroll-hybrid-android#enable-android-enrollment)
- [Approuver et déployer des applications Android for Work](/sccm/mdm/deploy-use/creating-android-applications#approve-and-deploy-android-for-work-apps)
- [Créer des éléments de configuration Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client#android-for-work-configuration-items)
- [Effectuer une réinitialisation sélective sur des appareils Android for Work](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe)
- [Profils de messagerie pour Android for Work](/sccm/mdm/deploy-use/create-exchange-activesync-profiles)
- [Stratégies de conformité pour Android for Work](/sccm/mdm/deploy-use/create-compliance-policy)


### <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Déployer des applications iOS achetées en volume sur des regroupements d’appareils

Vous pouvez désormais déployer des applications sous licence sur des appareils ainsi que des utilisateurs. En fonction de la capacité des applications à prendre en charge les licences d’appareils, une licence appropriée sera réclamée lors du déploiement, comme suit :

|||||
|-|-|-|-|
|Version de Configuration Manager|L’application prend-elle en charge les licences d’appareil ?|Type de regroupement de déploiement|Licence demandée|
|Antérieure à 1702|Oui|utilisateur|Licence utilisateur|
|Antérieure à 1702|Non|utilisateur|Licence utilisateur|
|Antérieure à 1702|Oui|Appareil|Licence utilisateur|
|Antérieure à 1702|Non|Appareil|Licence utilisateur|
|1702 et versions ultérieures|Oui|utilisateur|Licence utilisateur|
|1702 et versions ultérieures|Non|utilisateur|Licence utilisateur|
|1702 et versions ultérieures|Oui|Appareil|Licence d’appareil|
|1702 et versions ultérieures|Non|Appareil|Licence utilisateur|

Pour plus d’informations sur les applications achetées en volume, consultez [Gérer des applications iOS achetées en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-ios-volume-purchase-program-for-education"></a>Prise en charge du programme d’achat en volume iOS pour l’éducation

Désormais, vous pouvez également déployer et suivre les applications que vous avez achetées via le Programme d’achat en volume iOS pour l’éducation.
Pour plus d’informations sur les applications achetées en volume, consultez [Gérer des applications iOS achetées en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-multiple-volume-purchase-program-tokens"></a>Prise en charge de plusieurs jetons de programme d’achat en volume

Vous pouvez maintenant associer plusieurs jetons de programme d’achat en volume Apple à Configuration Manager.
Pour plus d’informations sur les applications achetées en volume, consultez [Gérer des applications iOS achetées en volume](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).

### <a name="support-for-line-of-business-apps-in-windows-store-for-business"></a>Prise en charge des applications métier dans le Windows Store pour Entreprises

Vous pouvez désormais synchroniser des applications métier personnalisées à partir du Windows Store pour Entreprises.

### <a name="conditional-access-device-compliance-policy-improvements"></a>Améliorations apportées aux stratégies de conformité des appareils pour l’accès conditionnel

Une nouvelle règle de stratégie de conformité de l’appareil est disponible pour vous aider à bloquer l’accès aux ressources d’entreprise qui prennent en charge l’accès conditionnel, quand des utilisateurs utilisent des applications qui figurent dans une liste d’applications non conformes. La liste des applications non conformes peut être définie par l’administrateur lors de l’ajout de la nouvelle règle de conformité **Applications qui ne peuvent pas être installées**. Cette règle exige que l’administrateur entre le **Nom de l’application**, l’**ID de l’application** et l’**Éditeur de l’application**  (facultatif) lors de l’ajout d’une application à la liste des applications non conformes. Ce paramètre s’applique uniquement aux appareils iOS et Android.

Cela permet également aux organisations de réduire les fuites de données via des applications non sécurisées, et d’empêcher la consommation excessive de données par certaines applications.

- Consultez cet article pour en savoir plus sur le [fonctionnement des stratégies de conformité des appareils](/sccm/mdm/deploy-use/device-compliance-policies).
- Consultez cet article pour en savoir plus sur [la façon de créer des stratégies de conformité des appareils](/sccm/mdm/deploy-use/create-compliance-policy).

### <a name="new-mobile-threat-defense-monitoring-tools"></a>Nouveaux outils de surveillance de protection contre les menaces mobiles

Depuis la version 1702, vous disposez de nouveaux moyens de surveiller l’état de conformité avec votre fournisseur de services de protection contre les menaces mobiles.

- Découvrez [comment surveiller la conformité de la protection contre les menaces mobiles](https://docs.microsoft.com/sccm/mdm/deploy-use/monitor-mobile-threat-defense-compliance).

## <a name="protect-devices"></a>Protéger les appareils

### <a name="detect-outdated-antimalware-client-versions"></a>Détecter les versions obsolètes des clients anti-programme malveillant
Depuis la version 1702, vous pouvez configurer une alerte pour vous assurer que les clients Endpoint Protection ne sont pas obsolètes. Pour plus d’informations, consultez [Alerte pour le client anti-programme malveillant](/sccm/protect/deploy-use/endpoint-configure-alerts#detect-outdated-antimalware-client-versions).

### <a name="device-health-attestation-updates"></a>Mises à jour de l’attestation d’intégrité des appareils
Le service d’attestation d’intégrité des appareils pour les clients locaux peut désormais être configuré et géré à partir du point de gestion. Pour plus d’informations, consultez [Attestation d’intégrité](/sccm/core/servers/manage/health-attestation).

### <a name="certificate-profiles-for-windows-hello-for-business"></a>Profils de certificat pour Windows Hello Entreprise

Si vous envisagez de stocker des profils de certificat dans le conteneur de clés Windows Hello Entreprise et que le profil de certificat utilise une clé étendue pour l’ouverture de session avec carte à puce, vous devez configurer des autorisations pour inscrire cette clé et garantir que le certificat est validé correctement.
Pour plus d’informations, consultez [Paramètres Windows Hello Entreprise](/sccm/protect/deploy-use/windows-hello-for-business-settings).

### <a name="new-windows-hello-for-business-notification-for-end-users"></a>Nouvelle notification Windows Hello Entreprise pour les utilisateurs finaux
Une nouvelle notification Windows 10 informe les utilisateurs finaux qu’ils doivent prendre des mesures supplémentaires pour terminer l’installation de Windows Hello Entreprise (par exemple, la configuration d’un code confidentiel).
