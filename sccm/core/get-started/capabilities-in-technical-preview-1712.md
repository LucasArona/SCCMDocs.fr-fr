---
title: Technical Preview 1712 | Microsoft Docs
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version Technical Preview 1712 de System Center Configuration Manager.
ms.date: 12/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3ce372d6-bd93-4d4d-b612-5303f89c36f0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: dc934948cf9431b8949f445a2ab2f46426638cbb
ms.sourcegitcommit: ef3fdf21180e43afd7af6c8264524711435e426e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/24/2019
ms.locfileid: "54896588"
---
# <a name="capabilities-in-technical-preview-1712-for-system-center-configuration-manager"></a>Fonctionnalités de la version Technical Preview 1712 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version 1712 de Technical Preview pour System Center Configuration Manager. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. 

Consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview) avant d’installer cette version Technical Preview. Cet article vous permet de vous familiariser avec les limitations et les conditions générales liées à l’utilisation d’une version Technical Preview, et explique comment effectuer une mise à jour d’une version avec une autre et comment envoyer des commentaires sur les fonctionnalités d’une version Technical Preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Problèmes connus dans cette version d’évaluation technique :**
- **La mise à jour vers une nouvelle préversion échoue s’il existe un serveur de site en mode passif**. Si vous avez un [serveur de site principal en mode passif](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), vous devez désinstaller le serveur de site en mode passif avant de procéder à la mise à jour vers cette nouvelle préversion. Vous pouvez réinstaller le serveur de site en mode passif une fois votre site mis à jour.

  Pour désinstaller le serveur de site en mode passif :
  1. Dans la console Configuration Manager, accédez à **Administration** > **Vue d’ensemble** > **Configuration du site** > **Serveurs et rôles de système de site**, puis sélectionnez le serveur de site en mode passif.
  2. Dans le volet **Rôles de système de site**, cliquez avec le bouton droit sur le rôle **Serveur de site**, puis choisissez **Supprimer le rôle**.
  3. Cliquez avec le bouton droit sur le serveur de site en mode passif, puis choisissez **Supprimer**.
  4. Après la désinstallation du serveur de site, redémarrez le service **CONFIGURATION_MANAGER_UPDATE** sur le serveur de site principal actif.
  <!--sms489412-->


**Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="do-not-automatically-upgrade-superseded-applications"></a>Ne pas mettre automatiquement à niveau les applications remplacées
<!-- 1351266 --> Suite à vos [commentaires User Voice](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/11532669-fix-supercedence-behavior), dans cette version vous pouvez configurer un déploiement d’application de sorte que celui-ci n’effectue pas de mise à niveau automatique des versions remplacées. Désormais, quand vous créez le déploiement, dans la page **Paramètres du déploiement** de **l’Assistant Déploiement logiciel**, pour un objectif d’installation **Disponible** ou **Requis**, vous pouvez activer ou désactiver l’option **Mettre automatiquement à niveau toutes les versions remplacées de cette application**.


## <a name="install-multiple-applications-in-software-center"></a>Installer plusieurs applications dans le Centre logiciel
<!-- 1357126 --> Si un utilisateur final ou un technicien a besoin d’installer plusieurs applications sur un appareil, le Centre logiciel prend désormais en charge l’installation de plusieurs applications sélectionnées. Cela permet à l’utilisateur de ne pas perdre de temps, car il n’est pas obligé d’attendre qu’une installation soit terminée pour commencer la suivante.

Quand vous utilisez le mode de sélection multiple sous l’onglet **Applications**, les critères suivants déterminent quelles applications le Centre logiciel active pour la sélection multiple :
 - L’application est visible par l’utilisateur
 - L’application n’est pas encore installée
 - L’approbation de l’administrateur n’est pas nécessaire ou est déjà accordée
 - L’état de l’application est disponible (par exemple, aucun téléchargement de contenu n’est en cours)

### <a name="try-it-out"></a>Essayez !
**Dans la console Configuration Manager :** déployez sur un utilisateur ou un appareil plusieurs applications pour l’installation, comme Disponible ou Requis (avec une date d’échéance à venir). N’exigez pas l’approbation de l’administrateur. Pour plus d’informations, consultez [Déployer des applications](/sccm/apps/deploy-use/deploy-applications).

**Dans le Centre logiciel :**
 1. L’onglet **Applications** doit s’ouvrir par défaut. 
 2. Pour activer le mode de sélection multiple dans la liste, cliquez sur la nouvelle icône ![Icône de sélection multiple dans le Centre logiciel](media/software-center-multi-select-apps.png) dans le coin supérieur droit.
 3. Sélectionnez plusieurs applications à installer en cochant la case à gauche des applications dans la liste.
 4. Cliquez sur le bouton **Installer les éléments sélectionnés**.

Les applications s’installent normalement, l’une après l’autre.


## <a name="client-based-pxe-responder-service"></a>Service de répondeur PXE basé sur le client
<!-- 1357148 --> L’un des défis courants pour les clients consiste à fournir des services PXE dans des bureaux distants/filiales avec peu ou aucune infrastructure de serveur. Le rôle de point de distribution prend en charge des systèmes d’exploitation clients, mais il ne peut pas être compatible PXE à cause de la dépendance envers les services de déploiement Windows.

De nouveaux paramètres client sont maintenant disponibles pour activer un service de répondeur PXE sur des clients Configuration Manager. Une image de démarrage compatible PXE doit résider dans le cache du client du répondeur PXE.

### <a name="try-it-out"></a>Essayez !
Vérifiez qu’il n’existe dans l’environnement de test aucun point de distribution compatible PXE ou d’autres serveurs PXE qui peuvent entrer en conflit avec ce répondeur PXE client.

Dans la console Configuration Manager :
1. Dans l’espace de travail **Bibliothèque de logiciels** sous **Systèmes d’exploitation**, **Séquences de tâches** : créez une séquence de tâches à l’aide du modèle personnalisé.
   1. Cliquez sur **Ajouter**, sélectionnez **Général**, puis l’étape **Définir la variable de séquence de tâches**. Entrez **SMSTSPersistContent** comme variable de séquence de tâches, puis entrez la valeur **TRUE**.
   1. Cliquez sur **Ajouter**, sélectionnez **Logiciel**, puis l’étape **Télécharger le contenu du package**. Cliquez sur l’astérisque doré, puis sélectionnez une image de démarrage compatible PXE. Incluez à la fois les images de démarrage x86 et x64. Configurez l’étape pour la placer dans le **cache du client Configuration Manager**.
   1. Cliquez sur **Ajouter**, sélectionnez **Général**, puis l’étape **Définir la variable de séquence de tâches**. Entrez **SMSTSPreserveContent** comme variable de séquence de tâches, puis entrez la valeur **TRUE**.
2. Dans l’espace de travail **Administration** sous **Paramètres client** : créez une stratégie de paramètres d’appareil client personnalisée.
   1. Sélectionnez le groupe **Paramètres du cache du client**.
   1. Affectez la valeur **Oui** au paramètre **Permettre au client Configuration Manager exécutant le système d’exploitation complet de partager du contenu**.
   1. Affectez la valeur **Oui** au paramètre **Activer le service de répondeur PXE**.
   1. Pour le paramètre **Créez un certificat auto-signé ou importez un certificat client PKI**, cliquez sur **Fournir un certificat**. Sélectionnez **Importer un certificat** si votre environnement de test a une infrastructure à clé publique. Sinon, cliquez sur **OK** pour créer un certificat auto-signé. 
   1. Configurez les paramètres restants selon les besoins de votre environnement de test. (Les paramètres par défaut doivent fonctionner, sauf s’il existe des exigences de sécurité ou de réseau spécifiques.)
3. Déployez la séquence de tâches et les paramètres client personnalisés sur un regroupement de clients cibles devant être des répondeurs PXE. Attendez que les stratégies soient appliquées et que la séquence de tâches soit exécutée.
4. Démarrez un autre client sur le même sous-réseau pour un démarrage PXE/réseau comme d’habitude.

### <a name="known-issues"></a>Problèmes connus
 - L’éditeur de séquence de tâches affiche une icône d’erreur rouge pour l’étape **Télécharger le contenu du package** quand vous ajoutez une image de démarrage, mais la séquence de tâches est enregistrée correctement. La réouverture de cette séquence de tâches dans l’éditeur affiche également un avertissement sans incidence signalant que des objets référencés sont introuvables. <!-- sms427542 -->
 - L’image de démarrage de l’étape Télécharger le contenu du package n’est pas affichée dans la liste des références de la séquence de tâches personnalisée. De plus, l’action **Distribuer du contenu** n’est pas disponible. <!-- sms504017 -->


## <a name="change-in-the-configuration-manager-client-install"></a>Changement dans l’installation du client Configuration Manager  
Suite à vos commentaires User Voice, [Silverlight n’est plus installé automatiquement sur les clients.](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/10886427-please-do-not-install-silverlight-by-default-in-v) <!--1356195-->
  

## <a name="change-to-the-surface-device-dashboard"></a>Changement dans le tableau de bord d’appareil Surface
Le tableau de bord Surface affiche maintenant les versions du microprogramme pour les appareils Surface, plutôt que la version du système d’exploitation. Dans la console, accédez à **Surveillance** > **Appareils Surface**. Vous pouvez voir les éléments suivants :
- Le pourcentage d’appareils Surface
- Le pourcentage de modèles Surface
- Les cinq principales versions de microprogramme <!--1355788-->


## <a name="improvements-to-office-365-client-management-dashboard"></a>Améliorations apportées au tableau de bord Gestion des clients Office 365 
Le tableau de bord Gestion des clients Office 365 affiche maintenant une liste des appareils concernés quand des sections de graphique sont sélectionnées. Dans la console, accédez à **Bibliothèque de logiciels** >**Vue d’ensemble** >**Gestion des clients Office 365**. Le tableau de bord est affiché à droite. La sélection de critères dans le graphique affiche une liste d’appareils.  
<!--1357281-->


## <a name="improvements-to-the-configuration-manager-console"></a>Améliorations apportées à la console Configuration Manager 
Nous avons apporté les améliorations suivantes à la console Configuration Manager suite à vos commentaires User Voice.

- [La liste des appareils affiche l’utilisateur principal](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8782225-enable-a-column-for-primary-user) : Les listes d’appareils sous Ressources et conformité, Appareils, affichent désormais l’utilisateur principal par défaut. Le dernier utilisateur connecté peut également être ajouté en tant que colonne facultative. <!-- 1357280 -->
- [Les regroupements renommés s’affichent dans les règles d’adhésion au regroupement existantes](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20125567-fix-the-renaming-of-collections) : Quand un regroupement est membre d’un autre regroupement et qu’il est renommé, le nouveau nom est mis à jour dans les règles d’adhésion.<!--1357282--> 


## <a name="improvements-to-operating-system-deployment"></a>Améliorations apportées au déploiement des systèmes d’exploitation
Les améliorations suivantes, inspirées notamment par vos commentaires User Voice, ont été apportées au déploiement des systèmes d’exploitation.
 - [Visionneuse du journal par défaut dans l’image de démarrage](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/19269823-stop-cmtrace-from-asking-us-if-we-want-to-use-it-a) : Dans Windows PE, lors du lancement de cmtrace.exe, vous n’êtes plus invité à choisir s’il faut utiliser ce programme comme visionneuse par défaut pour les fichiers journaux. <!-- SMS 500897 -->
 - Étape Télécharger le contenu du package : vous pouvez maintenant ajouter des images de démarrage à cette étape de séquence de tâches.


## <a name="windows-10-feedback-hub-app-integration"></a>Intégration de l’application Hub de commentaires Windows 10

Nous apprécions tellement vos commentaires que vous pouvez désormais nous les envoyer par le biais de [l’application Hub de commentaires](https://support.microsoft.com/en-us/help/4021566/windows-10-send-feedback-to-microsoft-with-feedback-hub-app) intégrée à Windows 10. Quand vous **ajoutez de nouveaux commentaires**, veillez à sélectionner la catégorie **Enterprise Management**, puis choisissez parmi les sous-catégories suivantes :
 - Client de Configuration Manager
 - Console Configuration Manager
 - Déploiement de système d’exploitation Configuration Manager
 - Serveur Configuration Manager

Continuez à utiliser notre [page User Voice](http://configurationmanager.uservoice.com/) afin de voter sur de nouvelles idées de fonctionnalités dans Configuration Manager.


<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Étapes suivantes
Pour obtenir des informations complémentaires sur l’installation ou la mise à jour de l’édition Technical Preview, consultez [Technical Preview pour System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
