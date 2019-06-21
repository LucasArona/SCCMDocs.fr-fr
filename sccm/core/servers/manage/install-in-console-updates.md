---
title: Mises à jour dans la console
titleSuffix: Configuration Manager
description: Installer des mises à jour pour Configuration Manager à partir du cloud Microsoft
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: b6eea68e5d700bda23a306257c4764d8446b2958
ms.sourcegitcommit: 86968fc2f129e404ff8e08f91a05fa17b5c47527
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/19/2019
ms.locfileid: "67252038"
---
# <a name="install-in-console-updates-for-configuration-manager"></a>Installer des mises à jour dans la console pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager se synchronise avec le service cloud Microsoft pour obtenir les mises à jour. Installez ensuite ces mises à jour à partir de la console Configuration Manager.



## <a name="get-available-updates"></a>Obtenir les mises à jour disponibles

Le site télécharge uniquement les mises à jour qui s’appliquent à votre infrastructure et à votre version. Cette synchronisation peut être automatique ou manuelle, selon la manière dont vous configurez le point de connexion de service pour votre hiérarchie :

- En **mode en ligne**, le point de connexion de service se connecte automatiquement au service cloud Microsoft et télécharge les mises à jour applicables.  

    Par défaut, Configuration Manager vérifie la disponibilité de nouvelles mises à jour toutes les 24 heures. Recherchez manuellement les mises à jour dans la console Configuration Manager. Accédez à l’espace de travail **Administration**, sélectionnez le nœud **Mises à jour et maintenance** et sélectionnez **Rechercher les mises à jour** dans le ruban.  

- En **mode hors connexion**, le point de connexion de service ne se connecte pas au service cloud Microsoft. Pour télécharger et importer les mises à jour disponibles, [utilisez l’outil de connexion de service](/sccm/core/servers/manage/use-the-service-connection-tool).  

> [!NOTE]  
> Si nécessaire, importez des correctifs hors bande dans votre console. Pour cela, [utilisez l’outil d’inscription de la mise à jour](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes). Ces correctifs hors bande complètent les mises à jour que vous obtenez lors de la synchronisation avec le service cloud Microsoft.  


Une fois les mises à jour synchronisées, vous pouvez les afficher dans la console Configuration Manager. Accédez à l’espace de travail **Administration** et sélectionnez le nœud **Mises à jour et maintenance**.  

- Les mises à jour que vous n’avez pas installées apparaissent **Disponibles**.  

- Les mises à jour que vous avez installées apparaissent **Installées**. Seule la mise à jour installée le plus récemment s’affiche. Pour afficher les mises à jour installées précédemment, sélectionnez **Historique** dans le ruban.  


Avant de configurer le point de connexion de service, vous devez comprendre et planifier ses utilisations supplémentaires. Les utilisations suivantes peuvent affecter la façon dont vous configurez ce rôle de système de site :  

- Le site utilise le point de connexion de service pour charger les informations d’utilisation relatives à votre site. Ces informations permettent au service cloud de Microsoft d’identifier les mises à jour disponibles pour la version actuelle de votre infrastructure. Pour plus d’informations, consultez [Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data).  

- Le site utilise le point de connexion de service pour gérer des appareils avec Microsoft Intune et à l’aide de la fonctionnalité de gestion des appareils mobiles locale de Configuration Manager. Pour plus d’informations, consultez [Gestion hybride des appareils mobiles (MDM)](/sccm/mdm/understand/hybrid-mobile-device-management).  

Pour mieux comprendre ce qui se passe quand des mises à jour sont téléchargées, consultez les organigrammes suivants :  

- [Organigramme - Téléchargement des mises à jour](/sccm/core/servers/manage/download-updates-flowchart)  

- [Organigramme - Réplication de mise à jour](/sccm/core/servers/manage/update-replication-flowchart)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>Attribuer les autorisations d’afficher et de gérer les mises à jour et les fonctionnalités

Pour qu’un utilisateur puisse afficher les mises à jour dans la console, un rôle de sécurité d’administration incluant la classe de sécurité **Packages de mise à jour** doit lui être attribué. Cette classe accorde l’autorisation d’afficher et de gérer les mises à jour dans la console Configuration Manager.    


#### <a name="about-the-update-packages-class"></a>À propos de la classe Packages de mise à jour   
Par défaut, la classe **Packages de mise à jour** (SMS_CM_Updatepackages) fait partie des rôles de sécurité intégrés suivants avec les autorisations répertoriées :  

- **Administrateur complet** avec autorisations **Modifier** et **Lecture** :  

    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Tout** peut afficher et installer les mises à jour. L’utilisateur peut également activer des fonctionnalités pendant l’installation ainsi que des fonctionnalités individuelles après les mises à jour du site.  

    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue de sécurité **Par défaut** peut afficher et installer les mises à jour. L’utilisateur peut également activer des fonctionnalités pendant l’installation et afficher des fonctionnalités après les mises à jour du site. En revanche, cet utilisateur ne peut pas activer les fonctionnalités après les mises à jour du site.  

- **Analyste en lecture seule** avec autorisations **Lecture** :  

    - Un utilisateur disposant de ce rôle de sécurité et de l’accès à l’étendue **Par défaut** peut afficher les mises à jour mais pas les installer. Cet utilisateur peut également afficher des fonctionnalités après les mises à jour du site, mais ne peut pas les activer.  


#### <a name="permissions-required-for-updates-and-servicing"></a>Autorisations requises pour les mises à jour et la maintenance   
- Utilisez un compte auquel vous affectez un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture**.  

- Affectez le compte à l’étendue **Par défaut**.  

#### <a name="permissions-to-only-view-updates"></a>Autorisations requises pour seulement voir les mises à jour   
- Utilisez un compte auquel vous affectez un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec l’autorisation **Lecture** uniquement.  

- Affectez le compte à l’étendue **Par défaut**.  

#### <a name="permissions-required-to-enable-features-after-the-site-updates"></a>Autorisations requises pour activer des fonctionnalités après les mises à jour du site   
-  Utilisez un compte auquel vous affectez un rôle de sécurité qui comprend la classe **Packages de mise à jour** avec les autorisations **Modifier** et **Lecture**.  

-  Affectez le compte à l’étendue **Tout**.  



##  <a name="bkmk_beforeinstall"></a> Avant d’installer une mise à jour dans la console  

Passez en revue les étapes suivantes avant d’installer une mise à jour à partir de la console Configuration Manager.  


###  <a name="bkmk_step1"></a> Étape 1 : Consulter la liste de contrôle de mise à jour  

Passez en revue la liste de contrôle de mise à jour applicable pour connaître les actions à entreprendre avant de lancer la mise à jour :

- [Liste de contrôle pour l’installation de la mise à jour 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902)

- [Liste de contrôle pour l’installation de la mise à jour 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810)  

- [Liste de contrôle pour l’installation de la mise à jour 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806)  

- [Liste de contrôle pour l’installation de la mise à jour 1802](/sccm/core/servers/manage/checklist-for-installing-update-1802)


###  <a name="bkmk_step2"></a> Étape 2 : Exécuter l’outil de vérification des prérequis avant d’installer une mise à jour  

Avant d’installer une mise à jour, envisagez d’exécuter la vérification des prérequis pour cette mise à jour. Si vous effectuez cette vérification avant d’installer une mise à jour :  

- Le site réplique les fichiers de mise à jour vers d’autres sites avant l’installation de la mise à jour.  

- Quand vous choisissez d’installer la mise à jour, la vérification des prérequis est automatiquement réexécutée.  

> [!NOTE]   
> Si vous lancez une vérification des prérequis, puis que vous affichez l’état, la phase **Installation** semble active. Toutefois, le site n’installe pas réellement la mise à jour. Pour exécuter la vérification des prérequis, le processus de mise à jour extrait le package de la bibliothèque de contenu. Il place ensuite le package dans un dossier intermédiaire où il peut accéder aux vérifications de prérequis en cours. Le même processus s’exécute à l’installation d’une mise à jour. Ce comportement est la raison pour laquelle la phase Installation s’affiche comme étant **En cours**. Seule l’étape *Extraire la mise à jour* apparaît dans la catégorie Installation.  

Par la suite, lorsque vous installez la mise à jour, vous pouvez configurer la mise à jour de manière à ignorer les avertissements relatifs à la vérification des prérequis.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>Pour exécuter l’Outil de vérification des prérequis avant d’installer une mise à jour  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Mises à jour et maintenance**.   

2. Sélectionnez le package de mise à jour pour lequel vous souhaitez exécuter la vérification des prérequis.  

3. Sélectionnez **Exécuter la vérification des prérequis** dans le ruban.  

    Lorsque vous exécutez la vérification des prérequis, le contenu de la mise à jour est répliqué sur des sites enfants. Consultez le fichier **distmgr.log** sur le serveur de site pour vérifier que le contenu est répliqué correctement.  

4. Pour afficher les résultats de la vérification des prérequis :  

    1. Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**.  

    2. Sélectionnez le nœud **État des mises à jour et de la maintenance** et recherchez l’état des prérequis.  

    3. Pour plus d’informations, consultez le fichier **ConfigMgrPrereq.log** sur le serveur de site.  



##  <a name="bkmk_install"></a> Installation de mises à jour dans la console  

Quand vous êtes prêt à installer des mises à jour à partir de la console Configuration Manager, commencez par le site de niveau supérieur de votre hiérarchie. Ce site est soit le site d’administration centrale, soit un site principal autonome.  

Installez la mise à jour en dehors des heures de bureau normales pour chaque site afin de minimiser l’impact sur les opérations commerciales. L’installation de la mise à jour peut inclure des actions telles que la réinstallation des composants de site et des rôles de système de site.  

- Les sites principaux enfants démarrent automatiquement la mise à jour après que le site d’administration centrale a installé la mise à jour. C’est le processus par défaut et recommandé. Pour contrôler le moment auquel un site principal installe les mises à jour, utilisez [Fenêtres de maintenance pour les serveurs de site](/sccm/core/servers/manage/service-windows).  

- Après la mise à jour du site principal parent, mettez à jour manuellement les sites secondaires à partir de la console Configuration Manager. La mise à jour automatique des serveurs de sites secondaires n’est pas prise en charge.  

- Quand vous utilisez une console Configuration Manager, vous êtes invité à mettre à jour la console après la mise à jour du site.  

- Après avoir mené à bien l’installation d’une mise à jour, le serveur de site met automatiquement à jour tous les rôles de système de site applicables. Toutefois, tous les points de distribution ne sont pas réinstallés et mis hors connexion pour être mis à jour simultanément. Au lieu de cela, le serveur de site utilise les paramètres de distribution de contenu du site pour distribuer la mise à jour à un sous-ensemble de points de distribution à la fois. Le résultat est que seuls certains points de distribution sont mis en mode hors connexion pour installer la mise à jour. Les points de distribution dont la mise à jour n’a pas commencé ou est terminée restent en ligne et peuvent fournir du contenu aux clients.


###  <a name="bkmk_overview"></a> Vue d’ensemble de l’installation d’une mise à jour dans la console  

#### <a name="1-when-the-update-installation-starts"></a>1. Au démarrage de l’installation de la mise à jour  
L’Assistant Mises à jour affiche la liste des zones de produit auxquelles s’applique la mise à jour.  

- Dans la page **Général** de l’Assistant, configurez les **avertissements relatifs à la configuration requise** en fonction des besoins :  

    - Les erreurs de configuration requise bloquent toujours l’installation de la mise à jour. Corrigez les erreurs avant de réessayer d’installer correctement la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry).  

    - Des avertissements de configuration requise peuvent également bloquer l’installation de la mise à jour. Corrigez les avertissements avant de réessayer d’installer la mise à jour. Pour plus d’informations, consultez [Nouvelle tentative d’installation d’une mise à jour ayant échoué](#bkmk_retry).  

    - **Ignorer les avertissements relatifs aux conditions requises et installer cette mise à jour sans tenir compte des manquements à la configuration requise** : Définissez une condition afin que l’installation de la mise à jour ignore les avertissements relatifs à la configuration requise. Cette option permet de poursuivre l’installation de la mise à jour. Si vous ne sélectionnez pas cette option, l’installation de la mise à jour s’arrête en cas d’avertissement. Si vous n’avez pas exécuté la vérification des prérequis et corrigé les avertissements relatifs aux prérequis pour un site, n’utilisez pas cette option.  

        Dans les espaces de travail **Administration** et **Surveillance**, le nœud Mises à jour et maintenance affiche un bouton **Ignorer les avertissements de configuration requise** dans le ruban. Ce bouton devient disponible quand l’installation d’un package de mise à jour n’arrive pas à terme en raison d’avertissements de vérification des prérequis. Par exemple, vous installez une mise à jour sans utiliser l’option pour ignorer les avertissements de configuration requise (à partir de l’Assistant Mises à jour). L’installation de la mise à jour s’interrompt, avec un état d’avertissement de configuration requise, mais sans erreur. Vous choisissez plus tard **Ignorer les avertissements de configuration requise** dans le ruban. Cette action déclenche la poursuite automatique de l’installation de cette mise à jour en ignorant les avertissements de configuration requise. Quand vous utilisez cette option, l’installation de la mise à jour se poursuit automatiquement après quelques minutes.  

- Quand une mise à jour s’applique au client Configuration Manager, choisissez de tester la mise à jour du client avec un ensemble limité de clients. Pour plus d’informations, consultez [Guide pratique pour tester les mises à niveau du client dans un regroupement de préproduction](/sccm/core/clients/manage/upgrade/test-client-upgrades).  


#### <a name="2-during-the-update-installation"></a>2. Lors de l’installation de la mise à jour  
Au cours de l’installation de la mise à jour, Configuration Manager effectue les actions suivantes :  

- réinstalle tous les composants concernés, comme les rôles de système de site ou la console Configuration Manager ;  

- gère les mises à jour des clients en fonction des sélections que vous avez effectuées pour le test du client et pour les [mises à niveau automatiques du client](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade) ;  

- Les serveurs de système de site n’ont généralement pas besoin de redémarrer dans le cadre de la mise à jour. Si un rôle utilise .NET et que le package met à jour ce composant prérequis, le système de site peut redémarrer.  

> [!TIP]  
> Quand vous installez des mises à jour Configuration Manager, le site met aussi à jour le dossier CD.Latest. Pour plus d’informations, consultez [Dossier CD.Latest](/sccm/core/servers/manage/the-cd.latest-folder).  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. Analyse de la progression des mises à jour durant le processus d’installation  
Utilisez les étapes suivantes pour surveiller la progression :  

- Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Mises à jour et maintenance**. Ce nœud affiche l’état d’installation de tous les packages de mise à jour.  

- Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **État des mises à jour et de la maintenance**. Ce nœud affiche l’état d’installation du package de mise à jour actuellement installé par le site uniquement.  

    L’installation de la mise à jour est décomposée en plusieurs phases pour faciliter la surveillance. Pour chacune des phases suivantes, des détails supplémentaires dans l’état d’installation indiquent le fichier journal à consulter pour obtenir plus d’informations :  

    - **Téléchargement** : Cette phase s’applique uniquement au site de niveau supérieur avec le point de connexion de service.   

    - **Réplication**   

    - **Vérification des prérequis**   

    - **Installation**    

    - **Post-installation** : Pour plus d’informations, consultez la page [Tâches de post-installation](#post-installation-tasks).  

- Affichez le fichier **CMUpdate.log** dans `<ConfigMgr_Installation_Directory>\Logs` sur le serveur de site.  


#### <a name="4-when-the-update-installation-completes"></a>4. Après l’installation de la mise à jour  
Une fois l’installation de la mise à jour sur le premier site terminée :  

- Les sites principaux enfants installent automatiquement la mise à jour. Aucune action supplémentaire n’est requise.  

- Mettez à jour manuellement les sites secondaires à partir de la console Configuration Manager. Pour plus d’informations, consultez [Pour démarrer l’installation de la mise à jour sur un site secondaire](#bkmk_secondary).  

- Tant que tous les sites de votre hiérarchie n’ont pas été mis à jour vers la nouvelle version, la hiérarchie fonctionne en mode mixte de versions. Pour plus d’informations, consultez [Interopérabilité entre les différentes versions](/sccm/core/plan-design/hierarchy/interoperability-between-different-versions).  


#### <a name="5-update-configuration-manager-consoles"></a>5. Mettre à jour des consoles Configuration Manager  
Dès lors qu’un site d’administration centrale ou un site principal est mis à jour, chaque console Configuration Manager qui se connecte au site doit aussi être mise à jour. Vous êtes invité à mettre à jour une console dans les cas suivants :  

- lorsque vous ouvrez la console ;  

- Quand vous accédez à un nouveau nœud dans une console ouverte  

Mettez à jour la console immédiatement après les mises à jour du site.  

Une fois la mise à jour de la console terminée, vérifiez que les versions de la console et du site sont correctes. Accédez à **À propos de System Center Configuration Manager** en haut à gauche de la console.  

> [!Note]  
> À compter de la version 1802, la version de la console est légèrement différente de la version du site. La version mineure de la console correspond maintenant à la version publiée de Configuration Manager. Par exemple, dans Configuration Manager version 1802, la version initiale du site est 5.0.8634.1000, et la version initiale de la console est 5.**1802**.1082.1700. Les numéros de build (1082) et de révision (1700) peuvent changer avec les correctifs logiciels futurs sur la version 1802.



###  <a name="bkmk_toptier"></a> Pour démarrer l’installation de la mise à jour sur le site de niveau supérieur  

Sur le site de niveau supérieur de votre hiérarchie, dans la console Configuration Manager, accédez à l’espace de travail **Administration**, puis sélectionnez le nœud **Mises à jour et maintenance**. Sélectionnez une mise à jour avec l’état **Disponible**, puis choisissez **Installer le package de mise à jour** dans le ruban.  


###  <a name="bkmk_secondary"></a> Pour démarrer l’installation de la mise à jour sur un site secondaire  

Après la mise à jour du site principal parent d’un site secondaire, mettez à jour ce dernier à partir de la console Configuration Manager. Pour ce faire, vous utilisez l’ **Assistant Mise à niveau d’un site secondaire**.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site secondaire que vous voulez mettre à jour, puis choisissez **Mettre à niveau** dans le ruban.  

2. Sélectionnez **Oui** pour démarrer la mise à jour du site secondaire.  

Pour surveiller l’installation de la mise à jour sur un site secondaire, sélectionnez le site secondaire, puis choisissez **Afficher l’état d’installation** dans le ruban. Ajoutez également la colonne **Version** au nœud Sites pour voir la version de chaque site secondaire.  

Dans certains cas, l’état dans la console ne s’actualise pas ou laisse supposer que la mise à jour a échoué. À l’issue de la mise à jour réussie d’un site secondaire, utilisez l’option **Réessayer l’installation**. Cette option ne réinstalle pas la mise à jour sur un site secondaire qui a correctement installé la mise à jour ; elle force la console à mettre à jour l’état.


### <a name="post-installation-tasks"></a>Tâches post-installation

Quand un site installe une mise à jour, plusieurs tâches ne peuvent pas démarrer tant que la mise à jour n’est pas installée sur le serveur de site. Cette liste comprend des tâches de post-installation essentielles aux opérations de site et de hiérarchie. Ces tâches étant critiques, elles sont activement surveillées. D’autres tâches ne sont pas directement surveillées, par exemple la réinstallation de rôles de système de site. Pour afficher l’état des tâches de post-installation critiques, sélectionnez la tâche de **post-installation** quand vous surveillez l’installation de la mise à jour d’un site.

Toutes les tâches ne se terminent pas immédiatement. Certaines tâches ne démarrent pas tant que chaque site n’a pas terminé l’installation de la mise à jour. Les nouvelles fonctionnalités que vous souhaitez utiliser peuvent être retardées en attendant la fin de ces tâches. Ces nouvelles fonctionnalités peuvent ne pas être visibles temporairement, car leur activation démarre seulement quand tous les sites ont terminé l’installation de la mise à jour.

Les tâches post-installation incluent :

- **Installation du service SMS_EXECUTIVE**
    - Service critique qui s’exécute sur le serveur de site.
    - La réinstallation de ce service devrait s’exécuter rapidement.

- **Installation du composant SMS_DATABASE_NOTIFICATION_MONITOR**
    - Thread de composant de site critique du service SMS_EXECUTIVE.
    - La réinstallation de ce service devrait s’exécuter rapidement.

- **Installation du composant SMS_HIERARCHY_MANAGER**
    - Composant de site critique qui s’exécute sur le serveur de site.
    - Responsable de la réinstallation des rôles sur les serveurs de système de site. L’état de la réinstallation d’un rôle de système de site individuel n’apparaît pas.
    - La réinstallation de ce service devrait s’exécuter rapidement.

- **Installation du composant SMS_REPLICATION_CONFIGURATION_MONITOR**
    - Composant de site critique qui s’exécute sur le serveur de site.
    - La réinstallation de ce service devrait s’exécuter rapidement.

- **Installation du composant SMS_POLICY_PROVIDER**
    - Composant de site critique qui s’exécute uniquement sur les sites principaux.
    - La réinstallation de ce service devrait s’exécuter rapidement.

- **Surveillance de l’initialisation de la réplication**   
    - Cette tâche s’affiche uniquement sur le site d’administration centrale et sur les sites principaux enfants.
    - Dépend de SMS_REPLICATION_CONFIGURATION_MONITOR.
    - Devrait s’exécuter rapidement.

- **Mise à jour du package de préproduction du client Configuration Manager**    
    - Cette tâche s’affiche même si le client en préproduction (également appelé pilotage du client) n’est pas activé pour être utilisé.
    - Ne commence pas tant que tous les sites dans la hiérarchie n’ont pas terminé l’installation de la mise à jour.

- **Mise à jour du dossier du client sur le serveur de site**
    - Cette tâche ne s’affiche pas si vous utilisez le client en préproduction.  
    - Devrait s’exécuter rapidement.

- **Mise à jour du package du client Configuration Manager**
    - Cette tâche ne s’affiche pas si vous utilisez le client en préproduction.  
    - Se termine uniquement une fois que tous les sites ont installé la mise à jour.  

- **Activation des fonctionnalités**
    - Cette tâche s’affiche uniquement sur le site de niveau supérieur de la hiérarchie.
    - Ne commence pas tant que tous les sites dans la hiérarchie n’ont pas terminé l’installation de la mise à jour.
    - Les fonctionnalités individuelles ne sont pas affichées.



##  <a name="bkmk_retry"></a> Nouvelle tentative d’installation d’une mise à jour ayant échoué  

Quand l’installation d’une mise à jour échoue, passez en revue les commentaires dans la console pour identifier les résolutions des avertissements et erreurs. Pour plus d’informations, consultez le fichier **ConfigMgrPrereq.log** sur le serveur de site. Avant de réessayer l’installation d’une mise à jour, vous devez corriger les erreurs et il est recommandé de corriger aussi les avertissements.  

> [!TIP]  
> Si une mise à jour présente des problèmes de téléchargement ou de réplication, utilisez [l’outil de réinitialisation de mises à jour](/sccm/core/servers/manage/update-reset-tool).  

Quand vous êtes prêt à réessayer l’installation d’une mise à jour, sélectionnez la mise à jour ayant échoué, puis choisissez une option applicable. Le comportement de nouvelle tentative d’installation de mise à jour dépend du nœud où vous lancez la nouvelle tentative et de l’option de nouvelle tentative que vous utilisez.  

#### <a name="retry-installation-for-the-hierarchy"></a>Réessayer l’installation pour la hiérarchie
Réessayez l’installation d’une mise à jour pour l’ensemble de la hiérarchie quand cette mise à jour est dans l’un des états suivants :  

- Les vérifications des prérequis ont généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de la mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud **Mises à jour et maintenance** est **Non**.)   

- La vérification des prérequis a échoué.    

- L’installation a échoué.  

- La réplication du contenu sur le site a échoué.   

Accédez à l’espace de travail **Administration** et sélectionnez le nœud **Mises à jour et maintenance**. Sélectionnez la mise à jour, puis choisissez l’une des options suivantes :  

- **Nouvelle tentative** : Lorsque vous exécutez **Nouvelle tentative** à partir du nœud **Mises à jour et maintenance**, l’installation de la mise à jour redémarre et ignore automatiquement les avertissements relatifs aux prérequis. Si la réplication du contenu a échoué précédemment, le contenu de la mise à jour est à nouveau répliqué.  

- **Ignorer les avertissements de configuration requise** : Si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez cliquer sur **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer après quelques minutes et utilise l’option pour ignorer les avertissements de prérequis.   

#### <a name="retry-installation-for-the-site"></a>Réessayer l’installation pour le site  
Réessayez l’installation d’une mise à jour sur un site spécifique quand cette mise à jour est dans l’un des états suivants :  

- Les vérifications des prérequis ont généré un ou plusieurs avertissements, et l’option permettant d’ignorer les avertissements de vérification des prérequis n’a pas été activée dans l’Assistant Mise à jour. (La valeur de la mise à jour pour **Ignorer l’avertissement de condition préalable** dans le nœud Mises à jour et maintenance est **Non**.)  

- La vérification des prérequis a échoué.    

- L’installation a échoué.    

Accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **État de maintenance du site**. Sélectionnez la mise à jour, puis choisissez l’une des options suivantes :  

- **Nouvelle tentative** : Lorsque vous exécutez **Nouvelle tentative** à partir du nœud **État de maintenance du site**, vous redémarrez l’installation de la mise à jour uniquement sur ce site. Contrairement à l’exécution de **Nouvelle tentative** à partir du nœud **Mises à jour et maintenance**, cette nouvelle tentative n’ignore pas les avertissements relatifs aux prérequis.  

- **Ignorer les avertissements de configuration requise** : Si l’installation de la mise à jour s’arrête en raison d’un avertissement, vous pouvez sélectionner **Ignorer les avertissements de configuration requise**. Cette action permet à l’installation de la mise à jour de continuer après quelques minutes et utilise l’option pour ignorer les avertissements de prérequis.  



##  <a name="bkmk_after"></a> Après l’installation d’une mise à jour sur un site  

Après les mises à jour du site, vérifiez la liste de contrôle postérieure à la mise à jour de la version applicable :  

- [Liste de contrôle postérieure à la mise à jour pour la version 1902](/sccm/core/servers/manage/checklist-for-installing-update-1902#post-update-checklist)  

- [Liste de contrôle postérieure à la mise à jour pour la version 1810](/sccm/core/servers/manage/checklist-for-installing-update-1810#post-update-checklist)  

- [Liste de contrôle postérieure à la mise à jour pour la version 1806](/sccm/core/servers/manage/checklist-for-installing-update-1806#post-update-checklist)  

- [Liste de contrôle postérieure à la mise à jour pour la version 1802](/sccm/core/servers/manage/checklist-for-installing-update-1802#post-update-checklist)  



##  <a name="bkmk_options"></a> Activation de fonctionnalités facultatives de mises à jour  

Lorsqu’une mise à jour inclut une ou plusieurs fonctionnalités facultatives, vous avez la possibilité d’activer celles-ci dans votre hiérarchie. Activez les fonctionnalités au moment de l’installation de la mise à jour ou revenez à la console ultérieurement pour activer les fonctionnalités facultatives.

Pour afficher les fonctionnalités disponibles et leur état, dans la console, accédez à l’espace de travail **Administration**, développez **Mises à jour et maintenance** et sélectionnez le nœud **Fonctionnalités**.

Quand une fonctionnalité n’est pas facultative, elle est installée automatiquement. Elle n’apparaît pas dans le nœud **Fonctionnalités**.  

> [!Important]  
> Dans une hiérarchie multisite, activez les fonctionnalités facultatives ou en préversion uniquement à partir du site d’administration centrale. Ceci vise à éviter les conflits au sein de la hiérarchie. <!--507197-->  

Quand vous activez une nouvelle fonctionnalité ou une fonctionnalité en préversion, le Gestionnaire de hiérarchie de Configuration Manager (HMAN) doit traiter le changement avant que cette fonctionnalité ne soit disponible. Le traitement du changement est souvent immédiat, mais il peut prendre jusqu’à 30 minutes en fonction du cycle de traitement HMAN. Une fois le changement traité, redémarrez la console pour pouvoir utiliser la fonctionnalité.

#### <a name="list-of-optional-features"></a>Liste des fonctionnalités facultatives
Les fonctionnalités suivantes sont facultatives dans la dernière version de Configuration Manager :<!--505213-->  

<!--Note to include in target articles

> [!Note]  
> Configuration Manager doesn't enable this optional feature by default. You must enable this feature before using it. For more information, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  

-->

- [Package Conversion Manager](/sccm/apps/pcm/package-conversion-manager) <!--1357861-->
- [Mises à jour de logiciels tiers](/sccm/sum/deploy-use/third-party-software-updates)<!--1357605,1352101,1358714-->
- [Approuver les requêtes d’application pour les utilisateurs appareil par appareil](/sccm/apps/deploy-use/deploy-applications#bkmk_deploy-settings) <!--1357015-->  
- [Prise en charge de Cisco AnyConnect 4.0.07x et version supérieure pour iOS](/sccm/mdm/deploy-use/create-vpn-profiles)<!--1357393-->
- [Évaluation de l’attestation de l’intégrité des appareils pour les stratégies de conformité pour l’accès conditionnel](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [Créer et exécuter des scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [Exécuter l’étape de la séquence de tâches](/sccm/osd/understand/task-sequence-steps#child-task-sequence) <!--1261338-->
- [Mise en cache préalable du contenu de la séquence de tâches](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [Mises à jour du pilote Surface](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [Passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Point de service de l’entrepôt de données](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [Cache de pair client](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [Créer un certificat PFX](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [Connecteur Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics) <!--1258052-->
- [Stratégie Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [VPN pour Windows 10](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [Windows Hello Entreprise](/sccm/protect/deploy-use/windows-hello-for-business-settings) (précédemment *Passport for Work*) <!--1245704-->
- [Accès conditionnel pour les PC gérés](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->


> [!Tip]  
> Pour plus d’informations sur les fonctionnalités qui nécessitent un consentement pour être activées, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).  
> 
> Pour plus d’informations sur les fonctionnalités qui sont disponibles uniquement dans la branche Technical Preview, consultez [Technical Preview](/sccm/core/get-started/technical-preview).



##  <a name="bkmk_prerelease"></a> Utiliser des fonctionnalités de préversions de mises à jour

L’édition Current Branch comprend des fonctionnalités en préversion à des fins de test préalable dans un environnement de production. Pour plus d’informations, consultez [Fonctionnalités en préversion](/sccm/core/servers/manage/pre-release-features).



## <a name="bkmk_faq"></a> Foire aux questions

###  <a name="why-dont-i-see-certain-updates-in-my-console"></a>Pourquoi certaines mises à jour ne s’affichent pas dans ma console ?  

Si vous ne trouvez pas une mise à jour spécifique dans votre console après une synchronisation réussie avec le service cloud Microsoft, les causes de ce comportement peuvent être les suivantes :  

- La mise à jour requiert une configuration que votre infrastructure n’utilise pas, ou votre version actuelle du produit ne remplit pas un prérequis pour la réception de la mise à jour.  

    Si vous pensez que vous disposez des configurations requises et prérequis pour une mise à jour manquante, vérifiez que votre point de connexion de service est en mode en ligne. Ensuite, utilisez l’option **Rechercher les mises à jour** dans le nœud **Mises à jour et maintenance** pour forcer la vérification. Si votre point de connexion de service est en mode hors connexion, utilisez l’outil de connexion de service pour effectuer une synchronisation manuelle avec le service cloud.  

- Votre compte ne dispose pas des autorisations d’administration basée sur des rôles appropriées pour afficher les mises à jour dans la console Configuration Manager. Pour plus d’informations, consultez [Autorisations de gérer les mises à jour](#assign-permissions-to-view-and-manage-updates-and-features).  

