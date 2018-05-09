---
title: Mises à jour dans la console
titleSuffix: Configuration Manager
description: Installer des mises à jour pour Configuration Manager à partir du cloud Microsoft
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9edf02333ec4ce272e69a896ed22e97fa6de0955
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>Installation de mises à jour dans la console pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager se synchronise avec le service cloud Microsoft pour obtenir les mises à jour. Vous pouvez installer ces mises à jour à partir de la console Configuration Manager.

## <a name="get-available-updates"></a>Obtenir les mises à jour disponibles
Seules les mises à jour qui s’appliquent à votre infrastructure et à votre version sont téléchargées et mises à disposition dans votre hiérarchie. Cette synchronisation peut être automatique ou manuelle, selon la manière dont vous configurez le point de connexion de service pour votre hiérarchie :

-   En **mode en ligne**, le point de connexion de service se connecte automatiquement au service cloud Microsoft et télécharge les mises à jour applicables.  

     Par défaut, Configuration Manager vérifie la disponibilité de nouvelles mises à jour toutes les 24 heures. Vous pouvez également rechercher des mises à jour immédiatement en choisissant **Rechercher les mises à jour** dans le nœud **Administration** > **Mises à jour et maintenance** de la console Configuration Manager. 

-   En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft. Pour télécharger et importer les mises à jour disponibles, [utilisez l’outil de connexion de service](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   Vous pouvez importer des correctifs hors bande dans votre console. Pour cela, [utilisez l’outil d’inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Ces correctifs hors bande complètent les mises à jour que vous obtenez lors de la synchronisation avec le service cloud Microsoft.


Une fois les mises à jour synchronisées, vous pouvez les afficher dans la console Configuration Manager en accédant au nœud **Administration** > **Mises à jour et maintenance** :  

-   Les mises à jour que vous n’avez pas installées apparaissent **Disponibles**.

-   Les mises à jour que vous avez installées apparaissent **Installées**. Seule la mise à jour installée le plus récemment s’affiche. Vous pouvez choisir le bouton **Historique** sur le ruban pour afficher les mises à jour installées précédemment.



Avant de configurer le point de connexion de service, vous devez comprendre et planifier ses utilisations supplémentaires. Les utilisations suivantes peuvent affecter la façon dont vous configurez ce rôle de système de site :  

-   Le point de connexion de service est utilisé pour charger les informations d’utilisation relatives à votre site. Ces informations permettent au service cloud de Microsoft d’identifier les mises à jour disponibles pour la version actuelle de votre infrastructure. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md).  

-   Le point de connexion de service permet de gérer des appareils avec Microsoft Intune et à l’aide de la fonctionnalité de gestion des appareils mobiles locale de Configuration Manager. Pour plus d’informations, consultez [Gestion des appareils mobiles (MDM) hybride avec System Center Configuration Manager et Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

Pour mieux comprendre ce qui se passe quand des mises à jour sont téléchargées, consultez :  

-   [Organigramme - Téléchargement des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/download-updates-flowchart.md)

-   [Organigramme - Réplication des mises à jour pour System Center Configuration Manager](../../../core/servers/manage/update-replication-flowchart.md)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Attribuer les autorisations d’afficher et de gérer les mises à jour et les fonctionnalités
Pour qu’un utilisateur puisse afficher les mises à jour dans la console, un rôle de sécurité d’administration incluant la classe de sécurité **Packages de mise à jour** doit lui être attribué. Cette classe accorde l’autorisation d’afficher et de gérer les mises à jour dans la console Configuration Manager.    

#### <a name="about-the-update-packages-class"></a>À propos de la classe Packages de mise à jour   
Par défaut, la classe **Packages de mise à jour** (SMS_CM_Updatepackages) fait partie des rôles de sécurité intégrés suivants avec les autorisations répertoriées :
 -  **Administrateur complet** avec autorisations **Modifier** et **Lecture** :
    -   Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Tout** peut afficher et installer les mises à jour. L’utilisateur peut également activer des fonctionnalités pendant l’installation et activer des fonctionnalités individuelles une fois la mise à jour installée.
    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Par défaut** peut afficher et installer les mises à jour. L’utilisateur peut également activer des fonctionnalités pendant l’installation et afficher des fonctionnalités une fois la mise à jour installée. En revanche, cet utilisateur ne peut pas activer les fonctionnalités après l’installation de la mise à jour.

- **Analyste en lecture seule** avec autorisations **Lecture** :
  -  Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue **Par défaut** peut afficher les mises à jour mais pas les installer. Il peut également afficher les fonctionnalités après l’installation d’une mise à jour mais pas les activer.

#### <a name="permissions-required-for-updates-and-servicing"></a>Autorisations requises pour les mises à jour et la maintenance   
  - Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture** .
  - L’étendue **Par défaut** doit être affectée au compte.

#### <a name="permissions-to-only-view-updates"></a>Autorisations requises pour seulement voir les mises à jour   
  - Utilisez un compte assigné à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec uniquement l’autorisation **Lecture**.
  - L’étendue **Par défaut** doit être affectée au compte.

#### <a name="permissions-required-to-enable-features-after-updates-are-installed"></a>Autorisations requises pour activer des fonctionnalités après l’installation de mises à jour   
  -  Utilisez un compte affecté à un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture** .
  -  L’étendue **Tout** doit être affectée au compte.



##  <a name="bkmk_beforeinstall"></a> Avant d’installer une mise à jour dans la console  
 Passez en revue les étapes suivantes avant d’installer une mise à jour à partir de la console Configuration Manager.  

###  <a name="bkmk_step1"></a> Étape 1 : consulter la liste de contrôle de mise à jour  
Passez en revue la liste de contrôle de mise à jour applicable pour connaître les actions à entreprendre avant de lancer la mise à jour :

- [Liste de contrôle pour l’installation de la mise à jour 1706](../../../core/servers/manage/checklist-for-installing-update-1706.md)  

- [Liste de contrôle pour l’installation de la mise à jour 1710](../../../core/servers/manage/checklist-for-installing-update-1710.md)  

- [Liste de contrôle pour l’installation de la mise à jour 1802](../../../core/servers/manage/checklist-for-installing-update-1802.md)


###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>Étape 2 : exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour  
Avant d’installer une mise à jour, envisagez d’exécuter la vérification des prérequis pour cette mise à jour. Si vous effectuez cette vérification avant d’installer une mise à jour :  

-   Les fichiers de mise à jour sont répliqués vers d’autres sites avant l’installation de la mise à jour.  

-   La vérification des prérequis est automatiquement réexécutée lorsque vous choisissez d’installer la mise à jour.  

> [!NOTE]   
> Si vous lancez une vérification des prérequis, puis que vous affichez l’état, la phase **Installation** semble active, mais la mise à jour n’est pas réellement en cours d’installation. Pour effectuer la vérification des prérequis, le processus de mise à jour extrait le package dans la bibliothèque de contenu et le place dans un dossier intermédiaire où sont accessibles les vérifications de prérequis en cours. Le même processus s’exécute à l’installation d’une mise à jour. C’est pourquoi l’installation s’affiche comme étant « En cours ». Seule l’étape *Extraire la mise à jour* apparaît dans la catégorie Installation.  

Par la suite, lorsque vous installez la mise à jour, vous pouvez configurer la mise à jour de manière à ignorer les avertissements relatifs à la vérification des prérequis.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Pour exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Mises à jour et maintenance**.   

2.  Cliquez avec le bouton droit sur le package de mise à jour pour lequel vous souhaitez exécuter la vérification des prérequis.  

3.  Choisissez **Exécuter la vérification de la condition préalable**.  

     Lorsque vous exécutez la vérification des prérequis, le contenu de la mise à jour est répliqué sur des sites enfants. Vous pouvez consulter le fichier distmgr.log sur le serveur du site pour vérifier que le contenu est répliqué correctement.  

4.  Pour afficher les résultats de la vérification, dans la console Configuration Manager, accédez à **Surveillance** > **État des mises à jour et de la maintenance**, puis recherchez l’état du prérequis. Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails.  



##  <a name="bkmk_install"></a> Installation de mises à jour dans la console  
 Quand vous êtes prêt à installer des mises à jour à partir de la console Configuration Manager, commencez par le site de niveau supérieur de votre hiérarchie. Ce site est soit le site d’administration centrale, soit un site principal autonome.  

 Nous vous recommandons d’installer la mise à jour en dehors des heures de bureau normales pour chaque site afin de minimiser l’impact sur les opérations commerciales. Cette recommandation s’explique par le fait que l’installation de la mise à jour peut inclure des actions telles que la réinstallation des composants de site et des rôles de système de site.  

-   Les sites principaux enfants démarrent la mise à jour automatiquement après que le site d’administration centrale a installé la mise à jour. C’est le processus par défaut et recommandé. Vous pouvez cependant utiliser des [fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows) pour contrôler à quel moment le site principal installe les mises à jour.  

-   Après la mise à jour du site principal parent, mettez à jour manuellement les sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.  

-   Quand vous utilisez une console Configuration Manager, vous êtes invité à mettre à jour la console après la mise à jour du site.  

-  Après avoir mené à bien l’installation d’une mise à jour, le serveur de site met automatiquement à jour tous les rôles de système de site applicables. Le seul inconvénient concerne les points de distribution. Lors de l’installation d’une mise à jour, tous les points de distribution ne sont pas réinstallés et mis hors connexion pour être mis à jour simultanément. Au lieu de cela, le serveur de site utilise les paramètres de distribution de contenu du site pour distribuer la mise à jour à un sous-ensemble de points de distribution à la fois. Résultat : seuls certains points de distribution passent en mode hors connexion pour l’installation de la mise à jour. Les points de distribution dont la mise à jour n’a pas commencé ou est terminée restent en ligne et peuvent fournir du contenu aux clients.


###  <a name="bkmk_overview"></a> Vue d’ensemble de l’installation d’une mise à jour dans la console  
#### <a name="1-when-the-update-installation-starts"></a>1. Au démarrage de l’installation de la mise à jour  
L’Assistant Mises à jour affiche la liste des zones de produit auxquelles s’applique la mise à jour.  

-   Dans la page **Général** de l’Assistant, vous pouvez configurer les **Avertissements relatifs à la configuration requise**.  
    -   Les erreurs de configuration requise bloquent toujours l’installation de la mise à jour. Corrigez les erreurs avant de réessayer d’installer correctement la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry).  

    -   Des avertissements de configuration requise peuvent également bloquer l’installation de la mise à jour. Corrigez les avertissements avant de réessayer d’installer la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry).  
    -   **Ignorer les avertissements relatifs aux conditions requises et installer cette mise à jour sans tenir compte des manquements à la configuration requise** : définit une condition pour que l’installation de la mise à jour ignore les avertissements relatifs aux prérequis. Cette option permet de poursuivre l’installation de la mise à jour. Si vous ne sélectionnez pas cette option, l’installation de la mise à jour s’arrête en cas d’avertissement. Si vous n’avez pas exécuté la vérification des prérequis et corrigé les avertissements relatifs aux prérequis pour un site, nous vous déconseillons d’utiliser cette option.  

      Dans les espaces de travail **Administration** et **Surveillance**, le nœud Mises à jour et maintenance affiche un bouton **Ignorer les avertissements de configuration requise** sur le ruban. Ce bouton devient disponible quand l’installation d’un package de mise à jour n’arrive pas à terme en raison d’avertissements de vérification des prérequis. Par exemple, vous installez une mise à jour sans utiliser l’option pour ignorer les avertissements de configuration requise (à partir de l’Assistant Mises à jour). L’installation de la mise à jour s’interrompt, avec un état d’avertissement de configuration requise, mais sans erreur. Vous pouvez plus tard choisir d’**ignorer les avertissements de configuration requise** dans le ruban pour poursuivre automatiquement l’installation de cette mise à jour en ignorant les avertissements de configuration requise. Quand vous utilisez cette option, l’installation de la mise à jour se poursuit automatiquement après quelques minutes.



-   Quand une mise à jour s’applique au client Configuration Manager, une option vous est proposée pour tester la mise à jour du client avec un ensemble limité de clients. Pour plus d’informations, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction](../../../core/clients/manage/upgrade/test-client-upgrades.md).  


#### <a name="2-during-the-update-installation"></a>2. Lors de l’installation de la mise à jour  
Au cours de l’installation de la mise à jour, Configuration Manager :  

-   réinstalle tous les composants concernés, comme les rôles de système de site ou la console Configuration Manager ;  

-   gère les mises à jour des clients en fonction des sélections que vous avez effectuées pour le test du client et pour les [mises à niveau automatiques du client](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) ;  

-   ne redémarre pas les serveurs de système de site dans le cadre de la mise à jour, sauf si .NET est installé en raison d’un prérequis lié aux rôles de système de site.  

> [!TIP]  
>  Lors de l’installation des mises à jour, Configuration Manager met aussi à jour le dossier CD.Latest. Ce dossier est utilisé pendant la récupération d’un site.  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Analyse de la progression des mises à jour durant le processus d’installation  
Pour surveiller l’état d’avancement, procédez comme suit :  

-   Dans la console Configuration Manager : nœud **Administration** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation de tous les packages de mise à jour.


-   Dans la console Configuration Manager, accédez au nœud **Administration** > **Vue d’ensemble** > **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation uniquement du package de mise à jour en cours d’installation.  

    L’installation du pack de mise à jour est décomposée selon les phases suivantes pour faciliter la surveillance. Pour chaque phase, des détails supplémentaires indiquent le fichier journal à consulter pour obtenir plus d’informations :  
    -   **Téléchargement** (cette phase s’applique uniquement au site de niveau supérieur où est installé le site du point de connexion de service.)   

    -   **Réplication**   

    -   **Vérification des prérequis**   

    -   **Installation**    

    -   **Post-installation** : pour plus d’informations, consultez [Tâches post-installation](#post-installation-tasks).  

-   Vous pouvez consulter le fichier **CMUpdate.log** dans **&lt;<Répertoire_Installation_ConfiMgr>\Logs**  


#### <a name="4-when-the-update-installation-completes"></a>4. Après l’installation de la mise à jour  
Une fois l’installation de la mise à jour sur le premier site terminée :  

-   Les sites principaux enfants installent automatiquement la mise à jour. Aucune action supplémentaire n’est requise.  

-   Les sites secondaires doivent être mis à jour manuellement dans la console Configuration Manager.
> [!TIP]
> Bien que la version d’un site secondaire n’apparaisse pas dans la console, vous pouvez utiliser le Kit de développement logiciel (SDK) Configuration Manager pour vérifier la version d’un site. Voir [SMS_Site Server WMI Class](/sccm/develop/reference/core/servers/configure/sms_site-server-wmi-class) (Classe WMI serveur SMS_Site).


-   Tant que tous les sites de votre hiérarchie n’ont pas été mis à jour vers la nouvelle version, la hiérarchie fonctionne en mode mixte de versions. Pour plus d’informations, consultez [Interopérabilité entre les différentes versions de Configuration Manager](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Mettre à jour des consoles Configuration Manager  
Dès lors qu’un site d’administration centrale ou un site principal est mis à jour, chaque console Configuration Manager qui se connecte à ce site doit aussi être mise à jour. Vous êtes invité à mettre à jour une console dans les cas suivants :  

-   lorsque vous ouvrez la console ;

-   Quand vous accédez à un nouveau nœud dans une console ouverte

Nous vous recommandons d’installer la mise à jour immédiatement.  

Une fois la mise à niveau de la console terminée, vous pouvez vérifier que les versions de la console et du site sont correctes. Accédez à **À propos de System Center Configuration Manager** en haut à gauche de la console.  

 > [!Note]  
 > À compter de la version 1802, la version de la console est légèrement différente de la version du site. La version mineure de la console correspond maintenant à la version publiée de Configuration Manager. Par exemple, dans Configuration Manager version 1802, la version initiale du site est 5.0.8634.1000, et la version initiale de la console est 5.**1802**.1082.1700. Les numéros de build (1082) et de révision (1700) peuvent changer avec les correctifs logiciels futurs sur la version 1802.



###  <a name="bkmk_toptier"></a> Pour démarrer l’installation de la mise à jour sur le site de niveau supérieur  
Sur le site de niveau supérieur de votre hiérarchie, dans la console Configuration Manager, accédez à **Administration** > **Mises à jour et maintenance**, sélectionnez une mise à jour **Disponible**, puis cliquez sur **Installer le package de mise à jour**.  


###  <a name="bkmk_secondary"></a> Pour démarrer l’installation de la mise à jour sur un site secondaire  
Après la mise à jour du site principal parent d’un site secondaire, vous pouvez mettre à jour ce dernier à partir de la console Configuration Manager. Pour ce faire, vous utilisez l’ **Assistant Mise à niveau d’un site secondaire**.  

1.  Dans la console Configuration Manager, accédez à **Administration** > **Configuration du site** > **Sites**, sélectionnez le site à mettre à jour, puis, sous l’onglet Accueil, dans le groupe **Site**, choisissez **Mettre à niveau**.  

2.  Cliquez sur **Oui** pour démarrer la mise à jour du site secondaire.  

Pour surveiller l’installation de la mise à jour sur un site secondaire, sélectionnez le serveur de site secondaire. Ensuite, sous l’onglet **Accueil**, dans le groupe **Site**, choisissez **Afficher l’état d’installation**. Vous pouvez également ajouter la colonne **Version** à l’affichage de la console pour voir la version de chaque site secondaire.  

À l’issue de la mise à jour d’un site secondaire, si l’état dans la console ne s’actualise pas ou laisse supposer que la mise à jour a échoué, utilisez l’option **Réessayer l’installation**. Cette option ne réinstalle pas la mise à jour sur un site secondaire qui a correctement installé la mise à jour ; elle force la console à mettre à jour l’état.


### <a name="post-installation-tasks"></a>Tâches post-installation
Lorsqu’un site installe une mise à jour, plusieurs tâches ne peuvent pas démarrer tant que la mise à jour n’est pas installée sur le serveur de site. Voici une liste des tâches post-installation essentielles aux opérations de site et de hiérarchie. Ces tâches étant critiques, elles sont activement surveillées. D’autres tâches ne sont pas directement surveillées, par exemple la réinstallation de rôles de système de site. Pour afficher l’état des tâches post-installation critiques, sélectionnez une tâche **post-installation** lorsque vous surveillez l’installation de la mise à jour d’un site.

Toutes les tâches ne se terminent pas immédiatement. Certaines tâches ne démarrent pas tant que chaque site n’a pas terminé l’installation de la mise à jour. Les nouvelles fonctionnalités que vous souhaitez utiliser peuvent être retardées en attendant la fin de ces tâches. Ces nouvelles fonctionnalités peuvent ne pas être visibles temporairement, car leur activation démarre seulement quand tous les sites ont terminé l’installation de la mise à jour.

Les tâches post-installation incluent :

-   **Installation du service SMS_EXECUTIVE**
  -   Service critique qui s’exécute sur le serveur de site.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_DATABASE_NOTIFICATION_MONITOR**
  -   Thread de composant de site critique du service SMS_EXECUTIVE.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_HIERARCHY_MANAGER**
  -   Composant de site critique qui s’exécute sur le serveur de site.
  -   Responsable de la réinstallation des rôles de système de site sur les serveurs de système de site. L’état de la réinstallation d’un rôle de système de site individuel n’apparaît pas.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_REPLICATION_CONFIGURATION_MONITOR**
  -   Composant de site critique qui s’exécute sur le serveur de site.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Installation du composant SMS_POLICY_PROVIDER**
  -   Composant de site critique qui s’exécute uniquement sur les sites principaux.
  -   La réinstallation de ce service devrait s’exécuter rapidement.


-   **Surveillance de l’initialisation de la réplication**   
  -   Cette tâche s’affiche uniquement sur le site d’administration centrale et sur les sites principaux enfants.
  -   Dépend de SMS_REPLICATION_CONFIGURATION_MONITOR.
  -   Devrait s’exécuter rapidement.


-   **Mise à jour du package de préproduction du client Configuration Manager**    
  -   Cette tâche s’affiche même si le client en préproduction (également appelé pilotage du client) n’est pas activé pour être utilisé.
  -   Ne commence pas tant que tous les sites dans la hiérarchie n’ont pas terminé l’installation de la mise à jour.


-   **Mise à jour du dossier du client sur le serveur de site**
  -   Cette tâche ne s’affiche pas si vous utilisez le client en préproduction.  
  -   Devrait s’exécuter rapidement.


-   **Mise à jour du package du client Configuration Manager**
  -   Cette tâche ne s’affiche pas si vous utilisez le client en préproduction.  
  -   Se termine uniquement une fois que tous les sites ont installé la mise à jour.  


-   **Activation des fonctionnalités**
  -   Cette tâche s’affiche uniquement sur le site de niveau supérieur de la hiérarchie.
  -   Ne commence pas tant que tous les sites dans la hiérarchie n’ont pas terminé l’installation de la mise à jour.
  -   Les fonctionnalités individuelles ne sont pas affichées.



##  <a name="bkmk_retry"></a> Nouvelle tentative d’installation d’une mise à jour ayant échoué  
Quand l’installation d’une mise à jour échoue, passez en revue les commentaires dans la console pour identifier les résolutions des avertissements et erreurs. Vous pouvez également consulter le fichier ConfigMgrPrereq.log sur le serveur du site pour plus de détails. Avant de réessayer l’installation d’une mise à jour, vous devez corriger les erreurs et il est recommandé de corriger aussi les avertissements.  

> [!TIP]  
> Si une mise à jour a des problèmes lors du téléchargement ou de réplication, vous pouvez utiliser la [outil de réinitialisation de mise à jour](/sccm/core/servers/manage/update-reset-tool). 

Quand vous êtes prêt à réessayer l’installation d’une mise à jour, sélectionnez la mise à jour ayant échoué, puis choisissez une option applicable. Le comportement de nouvelle tentative d’installation de mise à jour dépend du nœud où vous lancez la nouvelle tentative et de l’option de nouvelle tentative que vous utilisez.  

#### <a name="retry-installation-for-the-hierarchy"></a>Réessayer l’installation pour la hiérarchie
Vous pouvez réessayer l’installation d’une mise à jour pour l’ensemble de la hiérarchie lorsque cette mise à jour est dans l’un des états suivants :  

  -   Les vérifications des prérequis ont généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud **Mises à jour et maintenance** est **Non**.)   
  -   La vérification des prérequis a échoué.    
  -   L’installation a échoué.
  -   La réplication du contenu sur le site a échoué.   

Accédez à **Administration** > **Mises à jour et maintenance**, sélectionnez la mise à jour, puis choisissez l’une des options suivantes :  

  -   **Nouvelle tentative** : quand vous exécutez **Nouvelle tentative** à partir de ce nœud, l’installation de la mise à jour redémarre et ignore automatiquement les avertissements relatifs aux prérequis. Le contenu pour la mise à jour est uniquement répliqué si la réplication a échoué précédemment.
  - **Ignorer les avertissements de configuration requise** : si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de prérequis.   

#### <a name="retry-installation-for-the-site"></a>Réessayer l’installation pour le site  
 Vous pouvez réessayer l’installation d’une mise à jour sur un site spécifique lorsque cette mise à jour est dans l’un des états suivants :  

  -   Les vérifications des prérequis ont généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud Mises à jour et maintenance est **Non**.)  
  -   La vérification des prérequis a échoué.    
  -   L’installation a échoué.    

Accédez à **Surveillance** > **Vue d’ensemble** > **État de la maintenance de site**, sélectionnez la mise à jour, puis cliquez sur l’une des options suivantes :

  - **Nouvelle tentative** : quand vous exécutez **Nouvelle tentative** à partir de ce nœud, vous redémarrez l’installation de la mise à jour uniquement sur ce site. Contrairement à l’exécution de **Nouvelle tentative** à partir du nœud **Mises à jour et maintenance**, cette nouvelle tentative n’ignore pas les avertissements relatifs aux prérequis.
  - **Ignorer les avertissements de configuration requise** : si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer (après quelques minutes) et utilise l’option pour ignorer les avertissements de prérequis.



##  <a name="bkmk_after"></a> Après l’installation d’une mise à jour sur un site  
Utilisez la liste de vérification suivante pour effectuer les tâches courantes et les configurations nécessaires après la mise à jour d’un site.   

**Vérifier que la réplication de site à site est active :** dans la console Configuration Manager, accédez aux emplacements suivants pour consulter l’état et vérifier que la réplication est active :  

-   **Surveillance** > **Vue d’ensemble** > **Hiérarchie de site**  

-   **Surveillance** > **Vue d’ensemble** > **Réplication de base de données**  

Pour plus d’informations, consultez [Surveiller l’infrastructure de la hiérarchie et de la réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) et [À propos de l’analyseur de lien de réplication](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA).  

 **Vérifier que les serveurs de site et les serveurs de système de site distants ont redémarré (si nécessaire) :** examinez l’infrastructure de votre site et vérifiez que les serveurs de site et serveurs de système de site appropriés ont redémarré correctement. En règle générale, les serveurs de site redémarrent uniquement quand Configuration Manager installe .NET en tant que prérequis pour un rôle de système de site.  

 **Mettre à jour les consoles Configuration Manager autonomes :** vérifiez que toutes les consoles Configuration Manager distantes ont été mises à jour vers la même version. Vous êtes invité à mettre à jour la console dans les cas suivants :  

-   lorsque vous accédez à un nouveau nœud dans la console ;  

-   lorsque vous ouvrez la console.

**Reconfigurer les réplicas de base de données pour les points de gestion sur les sites principaux :** si vous utilisez des réplicas de base de données pour les points de gestion sur les sites principaux, vous devez désinstaller les réplicas de base de données avant de mettre à jour le site. Après avoir mis à niveau un site principal, reconfigurez le réplica de base de données pour les points de gestion. Pour plus d’informations, consultez [Réplicas de base de données pour les points de gestion](../../../core/servers/deploy/configure/database-replicas-for-management-points.md).  

**Reconfigurer les tâches de maintenance de base de données désactivées avant la mise à jour :** si vous avez désactivé les [tâches de maintenance](../../../core/servers/manage/maintenance-tasks.md) sur un site avant d’installer la mise à jour, reconfigurez ces tâches sur le site. Utilisez les mêmes paramètres qui étaient en vigueur avant la mise à jour.  

**Mettre à niveau les clients** : pour plus d’informations, consultez [Guide pratique pour mettre à niveau les clients pour les ordinateurs Windows](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

**Configurations supplémentaires :** examinez les modifications que vous avez apportées avant de commencer la mise à jour, puis restaurez ces configurations sur vos sites et votre hiérarchie.  



##  <a name="bkmk_options"></a> Activation de fonctionnalités facultatives de mises à jour  
Lorsqu’une mise à jour inclut une ou plusieurs fonctionnalités facultatives, vous avez la possibilité d’activer celles-ci dans votre hiérarchie. Vous pouvez activer les fonctionnalités au moment de l’installation de la mise à jour ou revenir à la console ultérieurement pour activer les fonctionnalités facultatives.

Pour afficher les fonctionnalités disponibles et leur état, dans la console, accédez à **Administration** > **Mises à jour et maintenance** > **Fonctionnalités**.

Quand une fonctionnalité n’est pas facultative, elle est installée automatiquement. Elle n’apparaît pas dans le nœud **Fonctionnalités**.  

> [!Important]  
> Dans une hiérarchie multisite, vous pouvez uniquement activer les fonctionnalités facultatives ou en préversion sur le site d’administration centrale. Ceci vise à éviter les conflits au sein de la hiérarchie. <!--507197-->
 

Quand vous activez une nouvelle fonctionnalité ou une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, vous devez redémarrer la console pour voir les nouveaux nœuds associés à cette fonctionnalité.

#### <a name="list-of-optional-features"></a>Liste des fonctionnalités facultatives
Les fonctionnalités suivantes sont facultatives dans la dernière version de Configuration Manager :<!--505213-->  
- [Accès conditionnel pour les PC gérés](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->
- [Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings) (également appelé *Windows Hello Entreprise*) <!--1245704-->
- [VPN pour Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [Stratégie Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [Connecteur OMS (Microsoft Operations Management Suite)](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) <!--1258052-->
- [Créer un certificat PFX](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Cache d’homologue client](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Point de service de l’entrepôt de données](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Mises à jour du pilote Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Mise en cache préalable du contenu de la séquence de tâches](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Exécuter l’étape de la séquence de tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [Créer et exécuter des scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Approuver les demandes d’application pour les utilisateurs par appareil](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  


> [!Tip]  
> Pour plus d’informations sur les fonctionnalités qui nécessitent un consentement pour être activées, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).  
> Pour plus d’informations sur les fonctionnalités qui sont disponibles uniquement dans la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Utiliser des fonctionnalités de préversions de mises à jour
Les fonctionnalités en préversion sont incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Vous pouvez utiliser ces fonctionnalités dans un environnement de production, mais elles ne doivent pas être considérées comme prêtes pour la production. Pour en savoir plus sur les fonctionnalités de préversion, y compris sur la façon de les activer dans votre environnement, consultez [Fonctionnalités de préversion](/sccm/core/servers/manage/pre-release-features).             



## <a name="frequently-asked-questions"></a>Forum aux questions

###  <a name="bkmk_faq"></a> Pourquoi certaines mises à jour ne s’affichent pas dans ma console ?  
 Si vous ne trouvez pas une mise à jour spécifique dans votre console après une synchronisation réussie avec le service cloud Microsoft, les causes possibles de ce comportement sont les suivantes :  

-   La mise à jour requiert une configuration que votre infrastructure n’utilise pas, ou votre version actuelle du produit ne remplit pas une condition préalable pour la réception de la mise à jour.  

     Si vous pensez que vous disposez des configurations requises et prérequis pour une mise à jour manquante, vérifiez que votre point de connexion de service est en mode en ligne. Ensuite, utilisez l’option **Rechercher les mises à jour** dans le nœud **Mises à jour et maintenance** pour forcer la vérification. Si vous êtes en mode hors connexion, vous devez recourir à l’outil de connexion au service pour synchroniser manuellement le service cloud.  

-   Votre compte ne dispose pas des autorisations d’administration basée sur des rôles appropriées pour afficher les mises à jour dans la console Configuration Manager.

    Pour plus d’informations sur les autorisations requises pour afficher les mises à jour et activer les fonctionnalités à partir de la console, consultez [Autorisations de gérer les mises à jour](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features) dans cette rubrique.

