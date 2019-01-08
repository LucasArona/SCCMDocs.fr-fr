---
title: Déployer des applications
titleSuffix: Configuration Manager
description: Créer ou simuler le déploiement d’une application sur un regroupement d’appareils ou d’utilisateurs
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32c1aea44fb69ba667752807e9d3f73487db7c34
ms.sourcegitcommit: c60e057075a83f07d1ca2577c3de1c7d7c8e9cec
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/19/2018
ms.locfileid: "53626444"
---
# <a name="deploy-applications-with-configuration-manager"></a>Déployer les applications avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Créez ou simulez le déploiement d’une application sur un regroupement d’appareils ou d’utilisateurs dans Configuration Manager. Ce déploiement fournit des instructions au client Configuration Manager sur la manière et le moment d’installer le logiciel. 

Avant de déployer une application, créez au moins un type de déploiement pour l’application. Pour plus d’informations, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications).

Vous pouvez aussi simuler un déploiement d’application. Cette simulation teste les conditions d’application d’un déploiement sans installer ou désinstaller l’application. Un déploiement simulé évalue la méthode de détection, les spécifications et les dépendances d’un type de déploiement, et génère un rapport contenant les résultats dans le nœud **Déploiements** de l’espace de travail **Surveillance**. Pour plus d’informations, consultez [Simuler des déploiements d’applications](/sccm/apps/deploy-use/simulate-application-deployments).

> [!Note]
>  Vous pouvez uniquement simuler le déploiement des applications nécessaires, mais pas les packages ni les mises à jour logicielles.   
> 
>  Les appareils inscrits dans MDM ne prennent pas en charge les déploiements simulés, l’expérience utilisateur ou les paramètres de planification.



## <a name="bkmk_deploy"></a> Déployer une application

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.  

2.  Dans la liste **Applications**, sélectionnez une application à déployer. Dans le ruban, cliquez sur **Déployer**.  

> [!Note]  
> Quand vous affichez les propriétés d’un déploiement existant, les sections suivantes correspondent aux onglets de la fenêtre des propriétés du déploiement :  
> - [Général](#bkmk_deploy-general)
> - [Contenu](#bkmk_deploy-content)
> - [Paramètres de déploiement](#bkmk_deploy-settings)
> - [Planification](#bkmk_deploy-sched)
> - [Expérience utilisateur](#bkmk_deploy-ux)
> - [Alertes](#bkmk_deploy-alerts)
> - [iOS : Stratégies de configuration d’applications](#bkmk_deploy-ios)


### <a name="bkmk_deploy-general"></a> Informations **générales** sur le déploiement 

Dans la page **Général** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :  

- **Logiciels** : Cette valeur indique l’application à déployer. Cliquez sur **Parcourir** pour sélectionner une autre application.  

- **Regroupement** : Cliquez sur **Parcourir** pour sélectionner le regroupement sur lequel vous voulez déployer l’application.  

- **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** : Stockez le contenu de l’application sur le groupe de points de distribution par défaut du regroupement. Si vous n’avez associé aucun groupe de points de distribution au regroupement sélectionné, cette option est grisée.  

- **Distribuer automatiquement le contenu pour les dépendances** : Si l’un des types de déploiement de l’application a des dépendances, le site envoie aussi le contenu de l’application dépendante aux points de distribution.  

    >[!Note]  
    > Si vous mettez à jour l’application dépendante après avoir déployé l’application principale, le site ne distribue pas automatiquement le nouveau contenu pour la dépendance.  

- **Commentaires (facultatif)** : Si vous le souhaitez, entrez une description de ce déploiement.  


### <a name="bkmk_deploy-content"></a> Options relatives au **contenu** du déploiement

Dans la page **Contenu**, cliquez sur **Ajouter** pour distribuer le contenu de cette application à un point de distribution ou à un groupe de points de distribution. 

Si vous avez sélectionné l’option **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** dans la page Général, cette option est automatiquement remplie. Seul un membre du rôle de sécurité **Administrateur d’application** peut le modifier.

Si le contenu de l’application est déjà distribué, il apparaît ici. 


### <a name="bkmk_deploy-settings"></a> **Paramètres de déploiement**

Dans la page **Paramètres de déploiement**, spécifiez les informations suivantes :  

- **Action** : À partir de la liste déroulante, indiquez si ce déploiement est destiné à **Installer** ou **Désinstaller** l’application.  

    > [!NOTE]  
    >  Si vous créez un déploiement pour **installer** une application et un autre pour **désinstaller** la même application sur le même appareil, le déploiement **d’installation** est prioritaire.  

    Vous ne pouvez pas changer l’action d’un déploiement une fois que vous l’avez créé.  

- **Fonction** : Dans la liste déroulante, choisissez l'une des options suivantes :  

  - **Disponible** : L’utilisateur voit l’application dans le Centre logiciel. Il peut l’installer sur demande.  

  - **Obligatoire** : Le client installe automatiquement l’application conformément à la planification que vous définissez. Si l’application n’est pas masquée, un utilisateur peut suivre l’état de son déploiement. Il peut également utiliser le Centre logiciel pour installer l’application avant l’échéance.  

    > [!NOTE]   
    >  Quand vous définissez l’action de déploiement sur **Désinstaller**, l’objet du déploiement est automatiquement défini sur **Obligatoire**. Vous ne pouvez pas modifier ce comportement.  

- **Autoriser les utilisateurs finaux à tenter de réparer cette application** : À compter de la version 1810, si vous avez créé l’application avec une ligne de commande de réparation, activez cette option. Les utilisateurs voient une option dans le Centre logiciel pour **Réparer** l’application.<!--1357866-->  

- **Prédéployer des logiciels sur le périphérique principal de l’utilisateur** : Si le déploiement concerne un utilisateur, sélectionnez cette option pour déployer l’application sur l’appareil principal de l’utilisateur. Ce paramètre ne nécessite pas que l’utilisateur se connecte avant que le déploiement ne s’exécute. Si l’utilisateur doit interagir avec l’installation, ne sélectionnez pas cette option. Cette option est disponible uniquement quand le déploiement est **Obligatoire**.  

- **Envoyer des paquets de mise en éveil** : Si le déploiement est **Obligatoire**, Configuration Manager envoie un paquet de mise en éveil aux ordinateurs avant que le client n’exécute le déploiement. Ce paquet réveille les ordinateurs à l’échéance de l’installation. Avant d’utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour Wake On LAN. Pour plus d’informations, consultez [Planifier la sortie de veille des clients](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

- **Autoriser les clients avec une connexion Internet facturée à l’usage à télécharger le contenu une fois l’échéance d’installation atteinte, ce qui peut entraîner des frais supplémentaires** : Cette option est disponible uniquement pour les déploiements dont l’objectif est **Obligatoire**.  

- **Mettre automatiquement à niveau toutes les versions remplacées de cette application** : Le client met à jour toutes les versions remplacées de l’application avec l’application de remplacement. 

    > [!Note]  
    > Cette option fonctionne, quelle que soit l’approbation de l’administrateur. Si un administrateur a déjà approuvé la version obsolète, il n’a pas besoin d’approuver également la version de remplacement. L’approbation concerne les nouvelles demandes uniquement, pas les mises à niveau de remplacement.<!--515824-->  

    > [!NOTE]  
    > Depuis la version 1802, vous pouvez activer ou désactiver cette option pour l’objet d’installation **Disponible**. <!--1351266--> 


#### <a name="bkmk_approval"></a> Paramètres d’approbation
Un des paramètres d’approbation suivants s’affiche, en fonction de votre version de Configuration Manager :

- **Exiger l’approbation de l’administrateur si des utilisateurs demandent cette application** : Pour les versions 1710 et antérieures, l’administrateur approuve les demandes des utilisateurs pour une application avant qu’ils puissent l’installer. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou que vous déployez l’application sur un regroupement d’appareils.  

- **Un administrateur doit approuver la demande de cette application sur l’appareil** : À compter de la version 1802, l’administrateur approuve les demandes des utilisateurs pour une application avant qu’ils puissent l’installer sur l’appareil demandé. Si l’administrateur approuve la demande, l’utilisateur ne pourra installer l’application que sur cet appareil. Il devra soumettre une autre demande pour installer l’application sur un autre appareil. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou que vous déployez l’application sur un regroupement d’appareils.

 À compter de la version 1810, vous pouvez également définir une liste d’adresses e-mail qui reçoivent la demande d’approbation. 
<!--1357015-->  

Pour plus d’informations, consultez [Approuver des applications](/sccm/apps/deploy-use/app-approval).


#### <a name="deployment-properties-deployment-settings"></a>**Paramètres de déploiement** dans les propriétés de déploiement
Quand vous affichez les propriétés d’un déploiement, l’option suivante s’affiche dans l’onglet **Paramètres de déploiement** si elle est prise en charge par la technologie de type de déploiement :

**Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**. Pour plus d’informations, consultez [Vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application](#bkmk_exe-check).



### <a name="bkmk_deploy-sched"></a> Paramètres de **planification** d’un déploiement

Dans la page **Planification**, définissez le moment où cette application est déployée ou mise à la disposition des appareils clients.

Par défaut, Configuration Manager met immédiatement la stratégie de déploiement à la disposition des clients. Si vous souhaitez créer le déploiement, mais pas le mettre à la disposition des clients avant une date ultérieure, configurez l’option **Planifier la mise à disposition de l’application**. Ensuite, sélectionnez les date et heure, et indiquez si elles sont basées sur l’heure UTC ou l’heure locale du client. 

Si le déploiement est **Obligatoire**, spécifiez également **l’échéance de l’installation**. Par défaut, cette échéance est dès que possible. 

Par exemple, vous devez déployer une nouvelle application métier. Tous les utilisateurs disposent d’un certain délai pour l’installer, mais vous souhaitez leur donner la possibilité de l’adopter entre-temps. Vous devez également vous assurer que le site a distribué le contenu à tous les points de distribution. Vous planifiez l’application afin qu’elle soit disponible dans cinq jours à partir d’aujourd’hui. Cette planification vous laisse le temps de distribuer le contenu et de vérifier son état. Ensuite, vous définissez l’échéance de l’installation à un mois à compter d’aujourd’hui. Les utilisateurs voient l’application dans le Centre logiciel quand elle est disponible au bout de cinq jours. S’ils ne font rien, le client installe automatiquement l’application à l’échéance de l’installation. 

Si l’application que vous déployez en remplace une autre, définissez l’échéance d’installation quand les utilisateurs reçoivent la nouvelle application. Définissez l’**Échéance d’installation** pour mettre à niveau les utilisateurs avec l’application remplacée.


#### <a name="delay-enforcement-with-a-grace-period"></a>Mise en œuvre du délai avec une période de grâce
Vous pouvez accorder plus de temps aux utilisateurs pour installer les applications obligatoires *au-delà* des échéances que vous avez définies. Ce comportement est généralement obligatoire quand un ordinateur reste longuement inactif et qu’il nécessite l’installation de nombreuses applications. Par exemple, quand un utilisateur rentre de congés, il peut être amené à patienter longtemps pendant que le client installe les déploiements en retard. Pour résoudre ce problème, définissez une période de grâce pour la mise en œuvre.

- Tout d’abord, configurez cette période de grâce avec la propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** dans les paramètres clients. Pour plus d’informations, consultez le groupe [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent). Spécifiez une valeur comprise entre **1** et **120** heures.  

- Dans la page **Planification** d’un déploiement d’application obligatoire, activez l’option **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres du client**. La période de grâce de mise en œuvre s’applique à tous les déploiements pour lesquels cette option est activée et vise les appareils sur lesquels vous avez aussi déployé le paramètre client.

Après l’échéance, le client installe l’application au cours de la première fenêtre non ouvrée, que l’utilisateur a configurée, dans la limite de cette période de grâce. Toutefois, l’utilisateur peut toujours ouvrir le Centre logiciel et installer l’application à tout moment. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard.


### <a name="bkmk_deploy-ux"></a> Paramètres de **l’expérience utilisateur** du déploiement

Dans la page **Expérience utilisateur**, spécifiez la façon dont les utilisateurs peuvent interagir avec l’installation de l’application.

- **Notifications à l’utilisateur** : Indiquez si vous souhaitez afficher les notifications dans le Centre logiciel au temps disponible configuré. Ce paramètre permet aussi de contrôler si des notifications doivent être envoyées aux utilisateurs sur les ordinateurs clients. Pour les déploiements disponibles, vous ne pouvez pas sélectionner l’option **Masquer dans le Centre logiciel et toutes les notifications**.  

- **Installation du logiciel** et **Redémarrage du système** : Configurez ces paramètres uniquement pour les déploiements requis. Ils spécifient ce qui se passe quand le déploiement atteint l’échéance en dehors des fenêtres de maintenance définies. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).  

- **Traitement des filtres d’écriture pour les appareils Windows Embedded** : Ce paramètre contrôle le comportement d’installation sur les appareils Windows Embedded qui sont activés avec un filtre d’écriture. Choisissez l’option permettant de valider les modifications à l’échéance de l’installation ou au cours d’une fenêtre de maintenance. Quand vous sélectionnez cette option, un redémarrage est nécessaire, qui conserve les modifications sur l’appareil. Sinon, l’application est installée sur l’overlay temporaire et validée ultérieurement.  

    - Quand vous déployez une mise à jour logicielle sur un appareil Windows Embedded, vérifiez que l’appareil est membre d’un regroupement pour lequel une fenêtre de maintenance a été configurée. Pour plus d’informations sur les fenêtres de maintenance et les appareils Windows Embedded, consultez [Créer des applications Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications).  


### <a name="bkmk_deploy-alerts"></a> **Alertes** de déploiement

Dans la page **Alertes**, configurez la manière dont Configuration Manager génère des alertes pour ce déploiement. Si vous utilisez également Operations Manager, configurez aussi ses alertes. Vous ne pouvez configurer que certaines alertes pour les déploiements obligatoires. 


### <a name="bkmk_deploy-ios"></a> iOS : **Stratégies de configuration d’applications**

Quand vous déployez un type de déploiement iOS, vous voyez également la page **Stratégies de configuration des applications**. Si vous avez déjà créé une stratégie de configuration des applications iOS, cliquez sur **Nouveau** pour associer ce déploiement à la stratégie. Pour plus d’informations sur ce type de stratégie, consultez [Configurer des applications iOS avec des stratégies de configuration des applications](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies).



## <a name="bkmk_phased"></a> Créer un déploiement par phases
<!--1358147--> À compter de la version 1806, créez un déploiement par phases pour une application. Ils permettent d’orchestrer un lancement coordonné et séquencé de logiciels en fonction de groupes et de critères personnalisables. Par exemple, déployez l’application sur un regroupement pilote, puis poursuivez automatiquement le lancement en fonction des critères de réussite. 

Pour plus d’informations, consultez les articles suivants :  

- [Créer un déploiement par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  

- [Gérer et effectuer le monitoring des déploiements par phases](/sccm/osd/deploy-use/manage-monitor-phased-deployments?toc=/sccm/apps/toc.json&bc=/sccm/apps/breadcrumb/toc.json)  



## <a name="bkmk_delete"></a> Supprimer un déploiement

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.  

2.  Dans la liste **Applications**, sélectionnez l’application qui inclut le déploiement à supprimer.  

3.  Basculez vers l’onglet **Déploiements** du volet d’informations, puis sélectionnez le déploiement d’application.  

4. Dans le ruban, sous l’onglet **Déploiement**, dans le groupe **Déploiement**, cliquez sur **Supprimer**.  

Quand vous supprimez un déploiement d’application, les instances de l’application que les clients ont déjà installées ne sont pas supprimées. Pour supprimer ces applications, déployez l’application sur les ordinateurs avec la valeur **Désinstaller**. Si vous supprimez un déploiement d’application ou que vous retirez une ressource du regroupement sur lequel le déploiement a lieu, l’application n’est plus visible dans le Centre logiciel.



## <a name="bkmk_notify"></a> Notifications à l’utilisateur pour les déploiements obligatoires

Quand les utilisateurs reçoivent des logiciels obligatoires et qu’ils sélectionnent le paramètre **Répéter et me rappeler**, ils peuvent choisir parmi les options suivantes :  

- **Ultérieurement** : Indique que les notifications sont planifiées selon les paramètres de notification configurés dans les paramètres du client.  

- **Heure fixe** : Indique que la notification est programmée pour s’afficher de nouveau après l’heure sélectionnée. Par exemple, si vous sélectionnez 30 minutes, la notification s’affiche de nouveau au bout de 30 minutes.  

![Groupe Agent ordinateur dans les paramètres par défaut du client](media/ComputerAgentSettings.png)

L’intervalle de répétition maximal est toujours basé sur les valeurs de notification configurées dans les paramètres du client à tout instant le long de la chronologie du déploiement. Par exemple :  

- Vous configurez le paramètre **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)** dans la page **Agent ordinateur** pour 10 heures.  

- Le client affiche la boîte de dialogue de notification pendant plus de 24 heures avant l’échéance du déploiement.  

- La boîte de dialogue affiche des options de répétition allant jusqu’à 10 heures, mais jamais au-delà.   

- À l’approche de l’échéance du déploiement, la boîte de dialogue affiche moins d’options. Ces options sont en cohérence avec les paramètres correspondants du client pour chaque composant de la chronologie du déploiement.  

Pour un déploiement à haut risque, à l’image d’une séquence de tâches qui déploie un système d’exploitation, l’expérience de notification à l’utilisateur est plus intrusive. Au lieu d’obtenir une notification temporaire sur la barre des tâches, la boîte de dialogue ci-dessous s’affiche chaque fois que vous êtes averti qu’une maintenance logicielle critique est nécessaire :

![Boîte de dialogue de notification pour une opération de maintenance critique sur un logiciel requis](media/client-toast-notification.png)



## <a name="bkmk_exe-check"></a> Vérifier si des fichiers exécutables sont en cours d’exécution

Configurez un déploiement pour vérifier si certains fichiers exécutables sont en cours d’exécution sur le client. Utilisez cette option pour rechercher les processus susceptibles d’interrompre l’installation de l’application. Si l’un de ces fichiers exécutables est en cours d’exécution, le client bloque l’installation du type de déploiement. L’utilisateur doit fermer le fichier exécutable en cours d’exécution pour permettre au client d’installer le type de déploiement. Pour les déploiements dont l’objet est Obligatoire, le client peut fermer automatiquement le fichier exécutable en cours d’exécution.

1. Ouvrez la boîte de dialogue **Propriétés** du type de déploiement.  

2. Basculez vers l’onglet **Comportement à l’installation**, puis cliquez sur **Ajouter**.  

3. Dans la boîte de dialogue **Ajouter le fichier exécutable**, entrez le nom du fichier exécutable cible. Si vous le souhaitez, entrez un nom convivial pour l’application pour vous aider à l’identifier dans la liste.  

4. Cliquez sur **OK**, puis cliquez sur **OK** pour fermer la fenêtre des propriétés de type de déploiement.  

5. Quand vous déployez l’application, sélectionnez l’option **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**. Cette option se trouve sous l’onglet **Paramètres de déploiement** des propriétés de déploiement.  


### <a name="client-behaviors-and-user-notifications"></a>Comportements clients et notifications à l’utilisateur

Une fois que les clients ont reçu le déploiement, voici le comportement qui prévaut :  

- Si vous avez déployé l’application comme étant **Disponible** et qu’un utilisateur tente de l’installer, le client invite ce dernier à fermer les fichiers exécutables en cours d’exécution spécifiés avant de poursuivre l’installation.  

- Si vous avez déployé l’application comme étant **Obligatoire** et que vous avez spécifié **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**, le client affiche une notification. Il informe l’utilisateur que les fichiers exécutables spécifiés sont automatiquement fermés quand l’échéance d’installation de l’application est atteinte.  

    - Planifiez ces boîtes de dialogue dans le groupe **Agent ordinateur** des paramètres clients. Pour plus d’informations, consultez [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    - Si vous ne souhaitez pas que l’utilisateur voit ces messages, sélectionnez l’option **Masquer dans le Centre logiciel et toutes les notifications** sous l’onglet **Expérience utilisateur** des propriétés du déploiement. Pour plus d’informations, consultez [Paramètres de l’expérience utilisateur du déploiement](#bkmk_deploy-ux).  

- Si vous avez déployé l’application comme étant **Obligatoire** et que vous n’avez pas spécifié **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**, l’installation de l’application échoue si une ou plusieurs des applications spécifiées sont en cours d’exécution.  



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Déployer des applications accessibles à l’utilisateur sur des appareils joints à Azure AD
<!-- 1322613 --> Si vous avez déployé des applications comme étant accessibles aux utilisateurs, depuis la version 1802, ils peuvent les parcourir et les installer via le Centre logiciel sur des appareils Azure Active Directory (Azure AD).  

#### <a name="prerequisites"></a>Prérequis

- Activer HTTPS sur le point de gestion  

- Intégrer le site à [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**  

    - Configurer la [découverte des utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

- Déployer une application comme étant accessible à un regroupement d’utilisateurs à partir d’Azure AD  

- Distribuer le contenu de l’application sur un [point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point)  

- Activer le paramètre client **Utiliser le nouveau Centre logiciel** dans le groupe [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent)  

- Le système d’exploitation du client doit être Windows 10 et joint à Azure AD. Joint à un domaine purement cloud ou joint à Azure AD hybride.  

- Pour prendre en charge les clients basés sur Internet :  

    - [Passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway)  

    - Activez le paramètre client : **Autoriser les demandes de stratégies utilisateurs provenant de clients Internet** dans le groupe [Stratégie client](/sccm/core/clients/deploy/about-client-settings#client-policy)  

- Pour prendre en charge les clients sur l’intranet :  

    - Ajouter le point de distribution cloud à un groupe de limites utilisé par les clients  

    - Les clients doivent résoudre le nom de domaine complet (FQDN) du point de gestion compatible HTTPS  



## <a name="next-steps"></a>Étapes suivantes
 - [Surveiller les applications](/sccm/apps/deploy-use/monitor-applications-from-the-console)
 - [Tâches de gestion pour les applications](/sccm/apps/deploy-use/management-tasks-applications)
 - [Guide de l’utilisateur sur le Centre logiciel](/sccm/core/understand/software-center)

