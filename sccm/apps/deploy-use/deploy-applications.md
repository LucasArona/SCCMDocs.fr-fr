---
title: Déployer des applications
titleSuffix: Configuration Manager
description: Créer ou simuler le déploiement d’une application sur un regroupement d’appareils ou d’utilisateurs
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a89c9d5a0fa4ea57a7824fe16b24120347ddaac
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338031"
---
# <a name="deploy-applications-with-system-center-configuration-manager"></a>Déployer des applications avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Créez ou simulez le déploiement d’une application sur un regroupement d’appareils ou d’utilisateurs dans Configuration Manager. Ce déploiement fournit des instructions au client Configuration Manager sur la manière et le moment d’installer le logiciel. 

Avant de déployer une application, créez au moins un type de déploiement pour l’application. Pour plus d’informations, consultez [Créer des applications](/sccm/apps/deploy-use/create-applications).

 Vous pouvez aussi simuler un déploiement d’application. Cette simulation teste les conditions d’application d’un déploiement sans installer ou désinstaller l’application. Un déploiement simulé évalue la méthode de détection, les spécifications et les dépendances d’un type de déploiement, et génère un rapport contenant les résultats dans le nœud **Déploiements** de l’espace de travail **Surveillance**. Pour plus d’informations, consultez [Simuler des déploiements d’applications](/sccm/apps/deploy-use/simulate-application-deployments).

> [!IMPORTANT]
>  Vous pouvez simuler le déploiement des applications nécessaires, mais pas les packages ni les mises à jour logicielles.   
>  Les appareils inscrits dans MDM ne prennent pas en charge les déploiements simulés, l’expérience utilisateur ou les paramètres de planification.



## <a name="deploy-an-application"></a>Déployer une application

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.

2.  Dans la liste **Applications** , sélectionnez l'application à déployer. Ensuite, sous l’onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.

### <a name="specify-general-information-about-the-deployment"></a>Spécifier des informations générales sur le déploiement

Dans la page **Général** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :

- **Logiciel** : cette valeur indique l’application à déployer. Cliquez sur **Parcourir** pour sélectionner une autre application.
- **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement dans lequel déployer l’application.
- **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** : stocke le contenu de l’application dans le groupe de points de distribution par défaut du regroupement. Si vous n’avez associé aucun groupe de points de distribution au regroupement sélectionné, cette option est grisée.
- **Distribuer automatiquement le contenu pour les dépendances** : si l’un des types de déploiement de l’application contient des dépendances, le site envoie aussi le contenu de l’application dépendante aux points de distribution.

    >[!IMPORTANT]
    > Si vous mettez à jour l’application dépendante après avoir déployé l’application principale, le site ne distribue pas automatiquement le nouveau contenu pour la dépendance.

- **Commentaires (facultatif)**  : si vous le souhaitez, entrez une description de ce déploiement.

### <a name="specify-content-options-for-the-deployment"></a>Spécifier les options de contenu pour le déploiement

Dans la page **Contenu**, cliquez sur **Ajouter** pour ajouter le contenu associé à ce déploiement aux points de distribution ou aux groupes de points de distribution. Si vous sélectionnez **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** dans la page **Général**, cette option est automatiquement remplie. Seul un membre du rôle de sécurité Administrateur d’application peut le modifier.

### <a name="specify-deployment-settings"></a>Spécifier des paramètres de déploiement

Dans la page **Paramètres de déploiement** de l’Assistant Déploiement logiciel, spécifiez les informations suivantes :

- **Action** : à partir de la liste déroulante, indiquez si ce déploiement est destiné à **Installer** ou **Désinstaller** l’application.

    > [!NOTE]
    >  Si une application est déployée deux fois sur un appareil, une fois avec l’action **Installer** et une autre fois avec l’action **Désinstaller**, le déploiement de l’application avec l’action **Installer** a la priorité.

  Vous ne pouvez pas modifier l’action d’un déploiement une fois que vous l’avez créé.

- **Objet**: dans la liste déroulante, choisissez l’une des options suivantes :  
    - **Disponible** : si l’application est déployée pour un utilisateur, celui-ci peut voir l’application publiée dans le Centre logiciel et l’installer à la demande.
    - **Obligatoire** : l’application est déployée automatiquement, selon la planification. Si l’état du déploiement de l’application n’est pas masqué, toute personne utilisant l’application peut suivre l’état de son déploiement et installer l’application à partir du Centre logiciel avant l’échéance.

    > [!NOTE]   
    >  Quand l’action de déploiement est définie sur **Désinstaller**, l’objet du déploiement est automatiquement défini sur **Obligatoire**. Vous ne pouvez pas modifier ce comportement.  

- **Déployer automatiquement en fonction de la planification, qu’un utilisateur soit connecté ou non** : si le déploiement est destiné à un utilisateur, sélectionnez cette option pour déployer l’application sur les appareils principaux de l’utilisateur. Ce paramètre ne nécessite pas que l'utilisateur se connecter avant que déploiement ne s'exécute. Ne sélectionnez pas cette option si l’utilisateur doit interagir avec l’installation. Cette option est disponible uniquement lorsque l'objet du déploiement est **Obligatoire**.

- **Envoyer des paquets de mise en éveil** : si l’objet du déploiement est **Obligatoire**, un paquet de mise en éveil est envoyé aux ordinateurs avant que le client exécute le déploiement. Ce paquet réveille les ordinateurs à l’échéance de l’installation. Avant d’utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour Wake On LAN.
- **Autoriser les clients avec une connexion Internet facturée à l’usage à télécharger le contenu une fois l’échéance d’installation atteinte, ce qui peut entraîner des frais supplémentaires** : cette option est disponible uniquement pour les déploiements dont l’objet est **Obligatoire**.
- **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement** : pour plus d’informations, consultez [Procédure pour vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application](#how-to-check-for-running-executable-files-before-installing-an-application).

- **Exiger l’approbation de l’administrateur si des utilisateurs demandent cette application** : pour les versions 1710 et antérieures, l’utilisateur ne peut pas installer l’application demandée tant que l’administrateur ne lui a pas donné son approbation. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou que l’application est déployée sur un regroupement d’appareils.  

    > [!NOTE]
    >  Les demandes d'approbation d'application sont affichées dans le nœud **Demandes d'approbation** , sous **Gestion d'applications** dans l'espace de travail **Bibliothèque de logiciels** . Si une demande ne reçoit pas d’approbation dans les 45 jours, elle est supprimée. La réinstallation du client risque d’annuler des demandes d’approbation en attente.  
    >  Après avoir approuvé l’installation d’une application, vous pouvez **Refuser** la demande dans la console Configuration Manager. Par cette action, le client ne désinstalle pas l’application sur les appareils, mais elle empêche les utilisateurs d’installer de nouvelles copies de l’application à partir du Centre logiciel.

- **Un administrateur doit approuver une demande pour cette application sur le périphérique** : depuis la version 1802, l’utilisateur ne peut pas installer l’application demandée tant que l’administrateur ne lui a pas donné son approbation. Si l’administrateur approuve la demande, l’utilisateur ne pourra installer l’application que sur cet appareil. Il devra soumettre une autre demande pour installer l’application sur un autre appareil. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou que l’application est déployée sur un regroupement d’appareils. <!--1357015-->  

    Cette fonctionnalité est facultative. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). Si cette fonctionnalité n’est pas activée, c’est l’expérience antérieure qui prévaut.  

    > [!Important]  
    > Le client Configuration Manager doit aussi se trouver sur la version 1802. Par ailleurs, vous devez utiliser le nouveau Centre logiciel.  

    > [!Note]  
    > Affichez **Demandes d’approbation** sous **Gestion des applications** dans l’espace de travail **Bibliothèque de logiciels** de la console de Configuration Manager. Il y a maintenant une colonne **Appareil** dans la liste de chaque demande. À chaque action effectuée sur la demande, la boîte de dialogue Demande d’application comprend également le nom de l’appareil utilisé par l’utilisateur pour envoyer la demande.  
    >  Si une demande ne reçoit pas d’approbation dans les 45 jours, elle est supprimée. La réinstallation du client risque d’annuler des demandes d’approbation en attente.  
    >  Après avoir approuvé l’installation d’une application, vous pouvez **Refuser** la demande dans la console Configuration Manager. Par cette action, le client ne désinstalle pas l’application sur les appareils, mais elle empêche les utilisateurs d’installer de nouvelles copies de l’application à partir du Centre logiciel.

- **Mettre automatiquement à niveau toutes les versions remplacées de cette application** : le client met à niveau toute version remplacée de l’application avec l’application de remplacement.    

    > [!NOTE]  
    > Depuis la version 1802, vous pouvez activer ou désactiver cette option pour l’objet d’installation **Disponible** ou **Obligatoire**. <!--1351266--> 


### <a name="specify-scheduling-settings-for-the-deployment"></a>Spécifier les paramètres de planification pour le déploiement

Dans la page **Planification** de l’Assistant Déploiement logiciel, définissez le moment où cette application est déployée ou mise à la disposition des appareils clients.
Les options de cette page diffèrent selon que l’action de déploiement est définie sur **Disponible** ou sur **Obligatoire**.

Dans certains cas, vous pouvez accorder plus de temps aux utilisateurs pour installer les mises à jour logicielles ou les déploiements d’applications obligatoires au-delà des échéances que vous avez définies. Ce comportement est généralement obligatoire après qu’un ordinateur est resté longuement inactif et qu’il nécessite l’installation de nombreuses applications. Par exemple, si un utilisateur est rentré de congés, il peut être amené à patienter longtemps pendant l’installation des déploiements d’applications en retard. Pour résoudre ce problème, vous pouvez désormais définir une période de grâce de mise en œuvre en déployant des paramètres du client Configuration Manager sur un regroupement.

Pour configurer la période de grâce, procédez comme suit :

- Dans la page **Agent ordinateur** des paramètres du client, configurez la nouvelle propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** avec une valeur comprise entre **1** et **120** heures.
- Dans la page **Planification** d’un déploiement d’application obligatoire, choisissez **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres du client**. La période de grâce de mise en œuvre s’applique à tous les déploiements pour lesquels cette option est activée et vise les appareils sur lesquels vous avez aussi déployé le paramètre client.

Une fois que l’échéance d’installation de l’application est atteinte, le client installe cette dernière au cours de la première fenêtre non ouvrée que l’utilisateur a configurée dans la limite de cette période de grâce. Toutefois, l’utilisateur peut toujours ouvrir le Centre logiciel et installer l’application à tout moment, s’il le souhaite. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard.

Si l’application que vous déployez en remplace une autre, vous pouvez définir l’échéance d’installation quand les utilisateurs reçoivent la nouvelle application. Définissez l’**Échéance d’installation** pour mettre à niveau les utilisateurs avec l’application remplacée.

### <a name="specify-user-experience-settings-for-the-deployment"></a>Spécifier les paramètres d’expérience utilisateur pour le déploiement

Dans la page **Expérience utilisateur** de l’Assistant Déploiement logiciel, spécifiez la façon dont les utilisateurs peuvent interagir avec l’installation de l’application.

Quand vous déployez des applications sur des appareils Windows Embedded avec le filtre d’écriture activé, vous pouvez demander à ce que l’application soit installée sur un segment de recouvrement temporaire puis les modifications validées ultérieurement. Vous pouvez aussi demander à ce que les modifications soient validées à l’échéance de l’installation ou au cours d’une fenêtre de maintenance. Si les modifications sont validées au moment de l’échéance d’installation ou au cours d’une fenêtre de maintenance, l’appareil doit être redémarré. Les modifications sont conservées sur l’appareil.

>[!NOTE]
    >  Quand vous déployez une application sur un appareil Windows Embedded, vérifiez qu’il est membre d’un regroupement associé à une fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance et les appareils Windows Embedded, consultez [Créer des applications Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).
    > Les options **Installation du logiciel** et **Redémarrage du système (si nécessaire pour terminer l'installation)** ne sont pas utilisées si l'objet du déploiement est défini sur **Disponible**. Vous pouvez également configurer le niveau de notification qu'un utilisateur peut voir lorsque l'application est installée.

### <a name="specify-alert-options-for-the-deployment"></a>Spécifier les options d’alerte pour le déploiement

Dans la page **Alertes** de l’Assistant Déploiement logiciel, configurez comment Configuration Manager et System Center Operations Manager génèrent des alertes pour ce déploiement. Vous pouvez configurer des seuils pour les alertes de rapport et désactiver les rapports pendant la durée du déploiement.

### <a name="associate-the-deployment-with-an-ios-app-configuration-policy"></a>Associer le déploiement à une stratégie de configuration d’application iOS

Dans la page **Stratégies de configuration des applications**, cliquez sur **Nouveau** pour associer ce déploiement à une stratégie de configuration d’application iOS (si vous en avez créé une). Pour plus d’informations sur ce type de stratégie, consultez [Configurer des applications iOS avec des stratégies de configuration des applications](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).

### <a name="deployment-properties"></a>Propriétés de déploiement

Recherchez le nouveau déploiement dans le nœud **Déploiements** de l’espace de travail **Analyse**. Vous pouvez modifier les propriétés de ce déploiement ou le supprimer de l'onglet **Déploiements** du volet Détail de l'application.



## <a name="delete-an-application-deployment"></a>Supprimer le déploiement d’une application

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Gestion des applications** > **Applications**.
3.  Dans la liste **Applications**, sélectionnez l’application qui inclut le déploiement à supprimer.
4.  Sous l’onglet **Déploiements** de la liste *<nom_application\>*, sélectionnez le déploiement d’application à supprimer. Ensuite, sous l’onglet **Déploiement**, dans le groupe **Déploiement**, cliquez sur **Supprimer**.

Quand vous supprimez un déploiement d’application, les instances déjà installées de l'application ne sont pas supprimées. Pour supprimer ces applications, vous devez déployer l’application sur des ordinateurs avec **Désinstaller**. Si vous supprimez un déploiement d’application ou que vous retirez une ressource du regroupement sur lequel le déploiement a lieu, l’application n’est plus visible dans le Centre logiciel.



## <a name="user-notifications-for-required-deployments"></a>Notifications à l’utilisateur pour les déploiements obligatoires
Quand vous recevez des logiciels obligatoires, dans le paramètre **Répéter et me le rappeler**, vous pouvez choisir une valeur dans la liste déroulante suivante :
- **Ultérieurement** : indique que les notifications sont planifiées selon les paramètres de notification configurés dans les paramètres du client.
- **Heure fixe** : indique que la notification est programmée pour s’afficher de nouveau après l’heure sélectionnée. Par exemple, si vous sélectionnez 30 minutes, la notification s’affiche de nouveau au bout de 30 minutes.

![Groupe Agent ordinateur dans les paramètres par défaut du client](media/ComputerAgentSettings.png)

L’intervalle de répétition maximal est toujours basé sur les valeurs de notification configurées dans les paramètres du client à tout instant le long de la chronologie du déploiement. Par exemple :
- Vous configurez le paramètre **Échéance du déploiement supérieure à 24 heures, effectuer un rappel à l’utilisateur toutes les (heures)** dans la page **Agent ordinateur** pour 10 heures.
- Le client affiche la boîte de dialogue de notification pendant plus de 24 heures avant l’échéance du déploiement.
- La boîte de dialogue affiche des options de répétition allant jusqu’à 10 heures, mais jamais au-delà. 
- À l’approche de l’échéance du déploiement, la boîte de dialogue affiche moins d’options. Ces options sont en cohérence avec les paramètres correspondants du client pour chaque composant de la chronologie du déploiement.

Pour un déploiement à haut risque, à l’image d’une séquence de tâches qui déploie un système d’exploitation, l’expérience de notification à l’utilisateur est plus intrusive. Au lieu d’obtenir une notification temporaire sur la barre des tâches, la boîte de dialogue ci-dessous s’affiche chaque fois que vous êtes averti qu’une maintenance logicielle critique est nécessaire :

![Boîte de dialogue de notification pour une opération de maintenance critique sur un logiciel requis](media/client-toast-notification.png)



## <a name="how-to-check-for-running-executable-files-before-installing-an-application"></a>Procédure pour vérifier si des fichiers exécutables sont en cours d’exécution avant d’installer une application

Dans la boîte de dialogue **Propriétés** d’un type de déploiement, sous l’onglet **Comportement à l’installation**, spécifiez un ou plusieurs fichiers exécutables. Si l’un de ces fichiers exécutables est en cours d’exécution sur le client, l’installation du type de déploiement est bloquée. L’utilisateur doit fermer le fichier exécutable en cours d’exécution pour permettre au client d’installer le type de déploiement. Pour les déploiements dont l’objet est Obligatoire, le client peut fermer automatiquement le fichier exécutable en cours d’exécution.

1. Ouvrez la boîte de dialogue **Propriétés** d’un type de déploiement.
2. Dans l’onglet **Comportement à l’installation** de la boîte de dialogue **Propriétés** de *<deployment type name>*, cliquez sur **Ajouter**.
3. Dans la boîte de dialogue **Ajouter ou modifier un fichier exécutable**, entrez le nom du fichier exécutable qui, s’il est en cours d’exécution, bloque l’installation de l’application. Si vous le souhaitez, vous pouvez également entrer un nom convivial pour l’application pour vous aider à l’identifier dans la liste.
4. Cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés** de *<deployment type name>*.
5. Au moment de déployer l’application, dans la page **Paramètres du déploiement** de l’Assistant Déploiement logiciel, sélectionnez **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet Comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**.

Une fois que les clients ont reçu le déploiement, voici le comportement qui prévaut :

- Si vous avez déployé l’application comme étant **Disponible** et qu’un utilisateur final tente de l’installer, le client invite ce dernier à fermer les fichiers exécutables en cours d’exécution spécifiés avant de poursuivre l’installation.

- Si vous avez déployé l’application comme étant **Obligatoire** et que vous avez spécifié **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**, une boîte de dialogue signale à l’utilisateur que les fichiers exécutables spécifiés se ferment automatiquement une fois que l’échéance d’installation de l’application est atteinte. Vous pouvez planifier ces boîtes de dialogue dans **Paramètres client** > **Agent ordinateur**. Si vous ne souhaitez pas que l’utilisateur final voit ces messages, sélectionnez **Masquer dans le Centre logiciel et toutes les notifications** sous l’onglet **Expérience utilisateur** des propriétés du déploiement.

- Si vous avez déployé l’application comme étant **Obligatoire** et que vous n’avez pas spécifié **Fermer automatiquement les fichiers exécutables en cours d’exécution que vous avez spécifiés sous l’onglet de comportement à l’installation de la boîte de dialogue des propriétés du type de déploiement**, l’installation de l’application échoue si une ou plusieurs des applications spécifiées sont en cours d’exécution.



## <a name="deploy-user-available-applications-on-azure-ad-joined-devices"></a>Déployer des applications accessibles à l’utilisateur sur des appareils joints à Azure AD
<!-- 1322613 -->
Si vous avez déployé des applications comme étant accessibles aux utilisateurs, depuis la version 1802, ils peuvent les parcourir et les installer via le Centre logiciel sur des appareils Azure Active Directory (Azure AD).  

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

    - Activer le paramètre client : **Autoriser les demandes de stratégies utilisateurs provenant de clients Internet** dans le groupe [Stratégie client](/sccm/core/clients/deploy/about-client-settings#client-policy)  

- Pour prendre en charge les clients sur l’intranet :  

    - Ajouter le point de distribution cloud à un groupe de limites utilisé par les clients  

    - Les clients doivent être en mesure de résoudre le nom de domaine complet (FQDN) du point de gestion compatible HTTPS  



## <a name="next-steps"></a>Étapes suivantes

   -  [Paramètres de gestion des déploiements à haut risque](../../protect/understand/settings-to-manage-high-risk-deployments.md)  
   -  [Guide pratique pour configurer les paramètres client](../../core/clients/deploy/configure-client-settings.md)
   -  [Guide de l’utilisateur sur le Centre logiciel](/sccm/core/understand/software-center)

