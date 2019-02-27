---
title: Haute disponibilité du serveur de site
titleSuffix: Configuration Manager
description: Découvrez comment configurer la haute disponibilité pour le serveur de site Configuration Manager, en ajoutant un serveur de site en mode passif.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6dcef836-c0d1-40af-ad30-cd8d864b09a9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: be12cfe29ff470f2f577bab2c685695ae5770bae
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131419"
---
# <a name="site-server-high-availability-in-configuration-manager"></a>Haute disponibilité du serveur de site dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1128774-->

Depuis la version 1806 de Configuration Manager, la haute disponibilité pour le rôle de serveur de site est une solution basée sur Configuration Manager, qui permet d’installer un serveur de site supplémentaire en mode *Passif*. Le serveur de site en mode passif vient s’ajouter à votre serveur de site existant qui se trouve en mode *Actif*. Un serveur de site en mode passif est disponible pour une utilisation immédiate, si nécessaire. Vous pouvez inclure ce serveur de site supplémentaire dans votre conception globale pour rendre le service Configuration Manager [hautement disponible](/sccm/core/servers/deploy/configure/high-availability-options).  

Un serveur de site en mode passif :
- Utilise la même base de données de site que votre serveur de site en mode actif
- N’écrit pas de données dans la base de données du site tant qu’il est en mode passif
- Utilise la même base de données de contenu que votre serveur de site en mode actif

Pour que le serveur de site en mode passif devienne actif, vous devez le *promouvoir* manuellement. Cette action fait passer le serveur de site actif en mode passif, et le serveur de site passif en mode actif. Les rôles de système de site disponibles sur le serveur en mode actif d’origine restent disponibles tant l’ordinateur est accessible. Seul le rôle de serveur de site bascule entre mode passif et mode actif.

> [!Note]  
> Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).



## <a name="prerequisites"></a>Prérequis

- Le serveur de site en mode passif peut être local ou dans le cloud Azure.  
    > [!Note]  
    > Un serveur de site basé sur le cloud en mode passif utilise l’infrastructure Azure comme un service (IaaS). Pour plus d’informations, consultez les articles suivants :  
    > - [Machines virtuelles Azure (pour infrastructure cloud)](/sccm/core/understand/use-cloud-services#azure-virtual-machines-for-cloud-based-infrastructure)
    > - [Questions fréquentes (FAQ) sur Configuration Manager dans Azure](/sccm/core/understand/configuration-manager-on-azure)  

- Les deux serveurs de site doivent être joints au même domaine Active Directory.  

- Le site est un site principal autonome. 

- Les deux serveurs de site doivent utiliser la même base de données, qui doit être distante de chaque serveur de site.  

     - Les deux serveurs de site nécessitent des autorisations **administrateur système** pour l’instance SQL Server qui héberge la base de données du site.

     - Le serveur SQL Server qui héberge la base de données de site peut utiliser une instance par défaut, une instance nommée, un [cluster SQL Server](/sccm/core/servers/deploy/configure/use-a-sql-server-cluster-for-the-site-database) ou un [groupe de disponibilité AlwaysOn SQL Server](/sccm/core/servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database).  

     - Le serveur de site en mode passif est configuré pour utiliser la même base de données de site que le serveur de site en mode actif. Le serveur de site en mode passif ne fait que lire les données de la base de données. Il n’y écrit pas de données tant qu’il n’a pas été promu vers le mode actif.  

- La bibliothèque de contenu de site doit se trouver sur un partage réseau distant. Les deux serveurs de site nécessitent des autorisations Contrôle total sur le partage et son contenu. Pour plus d’informations, consultez [Gérer la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/the-content-library#manage-content-library).<!--1357525-->  

    - Le serveur de site ne peut avoir le rôle de point de distribution. Le point de distribution utilise également la bibliothèque de contenu, et ce rôle ne prend pas en charge les bibliothèques de contenu distantes. Si vous déplacez la bibliothèque de contenu, vous ne pourrez plus ajouter le rôle de point de distribution au serveur de site.  

- Le serveur de site en mode passif :  

     - Doit respecter les [conditions requises pour installer un site principal](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site).  

     - Doit avoir un compte d’ordinateur faisant partie d’un groupe Administrateurs local sur le serveur de site en mode actif<!--516036-->

     - Est installé à l’aide de fichiers sources correspondant à la version du serveur de site en mode actif  

     - Ne peut pas avoir un rôle de système de site tant que le serveur de site en mode passif n’est pas installé  

- Les deux serveurs de site peuvent exécuter des systèmes d’exploitation différents ou des versions de Service Pack différentes, du moment qu’ils sont tous les deux [pris en charge par Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  



## <a name="limitations"></a>Limitations
- Un serveur de site unique en mode passif est pris en charge sur chaque site principal.  

- Un serveur de site en mode passif ne peut pas se trouver dans une hiérarchie. Une hiérarchie comprend un site d’administration centrale et un site principal enfant. Un serveur de site en mode passif ne doit être créé que sur un site principal autonome.<!--1358224-->

- Un serveur de site en mode passif ne peut pas se trouver sur un site secondaire.<!--SCCMDocs issue 680-->  

- La promotion d’un serveur de site passif vers le mode actif se fait manuellement. Il n’existe pas de basculement automatique.  

- Vous ne pouvez pas installer de rôles de système de site sur le nouveau serveur avant d’avoir ajouté le serveur de site en mode passif.  

    > [!Note]  
    > Après avoir installé le serveur de site en mode passif, vous pouvez ajouter des rôles supplémentaires, selon vos besoins. Par exemple, le fournisseur SMS ou un point de gestion du site principal.  

- Pour les rôles, tels que le point de rapport, qui utilisent une base de données, celle-ci doit être hébergée sur un serveur distant des deux serveurs de site.  

- Le fournisseur SMS ne peut pas être installé sur le serveur de site en mode passif. Vous devez vous connecter à un fournisseur du site pour promouvoir manuellement le serveur de site passif vers le mode actif. Installez au moins une instance supplémentaire du fournisseur sur un autre serveur. Pour plus d’informations, consultez [Planifier le fournisseur SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider).  

- La console Configuration Manager n’est pas installée automatiquement sur le serveur de site en mode passif.  



## <a name="add-a-site-server-in-passive-mode"></a>Ajouter un serveur de site en mode passif

Pour plus d’informations sur le processus général d’ajout de rôles, consultez [Installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles).

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, sélectionnez le nœud **Sites**, puis cliquez sur **Créer un serveur de système de site** dans le ruban.   

2. Dans la page **Général** de l’Assistant Création d’un serveur de système de site, spécifiez le serveur qui doit héberger le serveur de site en mode passif. Le serveur que vous spécifiez ne peut pas héberger des rôles de système de site tant que le serveur de site en mode passif n’est pas installé.  

3. Dans la page **Sélection du rôle système**, sélectionnez uniquement **Serveur de site en mode passif**.  

    > [!Note]  
    > Dans cette page, l’Assistant effectue la vérification des prérequis suivants :  
    > - Le serveur sélectionné n’est pas un serveur de site secondaire
    > - Le serveur sélectionné ne se trouve pas déjà sur un serveur de site en mode passif
    > - La bibliothèque de contenu du site se trouve à un emplacement distant  
    >  
    > Si tous les prérequis ne sont pas satisfaits, vous ne pourrez pas continuer.  

4. Dans la page **Serveur de site en mode passif**, vous devez fournir les informations suivantes qui seront utilisées pour exécuter le programme d’installation et installer le rôle de serveur de site sur le serveur spécifié :

     - Choisissez l'une des options suivantes :  

         - **Copier les fichiers sources d’installation sur le réseau à partir du serveur de site en mode actif** : cette option permet de créer un package compressé et de l’envoyer vers le nouveau serveur de site.  

         - **Utiliser les fichiers sources de l’emplacement suivant sur le serveur de site en mode passif** : il peut s’agir par exemple d’un chemin d’accès local dans lequel vous avez déjà copié les fichiers sources. Vérifiez que la version de ce contenu est la même que celle du serveur de site en mode actif.  

         - (*Recommandé*) **Utiliser les fichiers sources dans l’emplacement réseau suivant** : spécifiez le chemin d’accès direct du contenu du dossier **CD.Latest** situé sur le serveur de site en mode actif. Par exemple, `\\Server\SMS_ABC\CD.Latest` où « *Server* » correspond au nom du serveur de site en mode actif, et «*ABC*» au code de site.  

     - Spécifiez le chemin de l’emplacement local auquel installer Configuration Manager sur le nouveau serveur de site. Exemple : `C:\Program Files\Configuration Manager`  

5. Effectuez toutes les étapes de l'Assistant. Configuration Manager installe ensuite le serveur de site en mode passif sur le serveur spécifié.

Pour connaître l’état détaillé de l’installation, dans la console, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **État du serveur de site**. L’état du serveur de site en mode passif est **Installation**. Pour plus d’informations, sélectionnez le serveur, puis cliquez sur **Afficher l’état**. Cette action ouvre la fenêtre État d’installation du serveur de site. Lorsque le processus est terminé, l’état est **OK** pour les deux serveurs.   

Pour plus d’informations sur le processus d’installation, consultez [Configurer un serveur de site en mode passif - Diagramme](/sccm/core/servers/deploy/configure/passive-site-server-flowchart).

Une fois que vous avez ajouté le serveur de site en mode passif, vous pouvez voir que les deux serveurs de site se trouvent sous l’onglet **Nœuds**, dans le nœud **Sites** de la console. 

Sur le serveur de site en mode passif, tous les composants de serveur de site Configuration Manager sont en attente. Les services Windows sont toujours en cours d’exécution.



## <a name="site-server-promotion"></a>Promotion des serveurs de site  

Comme pour la sauvegarde et la récupération, vous pouvez planifier et tester votre processus pour changer de serveur de site. Prenez en compte les éléments suivants dans votre plan de promotion :  

- Testez une promotion planifiée, où les deux serveurs de site sont en ligne. Testez également un basculement non planifié, en forçant la déconnexion ou l’arrêt du serveur de site en mode actif.  

- Déterminez les processus en cours pendant le basculement, et ce que vous devez communiquer aux autres administrateurs Configuration Manager.  

- Avant une promotion planifiée :  

    - Vérifiez l’état global du site et de ses composants. Vérifiez que tout est normal dans votre environnement.  

    - Vérifiez l’état du contenu de tous les packages qui sont répliqués activement d’un site à l’autre.  

    - Ne démarrez pas de nouvelles tâches de distribution de contenu. 

        > [!Note]  
        > Si une réplication de fichiers entre sites est en cours pendant le basculement, le nouveau serveur de site ne peut pas recevoir le fichier répliqué. Si cela se produit, redistribuez le contenu logiciel une fois que le nouveau serveur de site est actif.<!--515436-->  


### <a name="process-to-promote-the-site-server-in-passive-mode-to-active-mode"></a>Processus de promotion d’un serveur de site passif en serveur de site actif

Cette section explique comment faire passer le serveur de site du mode passif au mode actif. Pour accéder au site et effectuer ce changement, vous devez pouvoir accéder à une instance du fournisseur SMS. Pour plus d’informations, consultez [Utiliser plusieurs fournisseurs SMS](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#BKMK_MultiSMSProv).  

> [!Important]  
> Par défaut, seul le serveur de site d’origine a le rôle de fournisseur SMS. Si ce serveur est hors connexion, vous ne pouvez pas vous connecter au site, car aucun fournisseur n’est disponible. Lorsque vous ajoutez le serveur de site en mode passif, le fournisseur SMS n’est pas automatiquement ajouté. Pour un service hautement disponible, ajoutez au moins un autre rôle de fournisseur SMS à votre site.  

> [!Tip]  
> La console Configuration Manager demande la liste des fournisseurs SMS disponibles à WMI sur le serveur de site. Quand vous installez plusieurs fournisseurs SMS sur un site, le site attribue de façon aléatoire à chaque nouvelle demande de connexion l’utilisation d’un fournisseur SMS installé. Vous ne pouvez pas spécifier l’emplacement du fournisseur SMS à utiliser avec une session de connexion spécifique. Si votre console ne peut pas se connecter au site parce que le serveur de site actuel est hors connexion, spécifiez l’autre serveur de site dans la fenêtre Connexion au site.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site, puis basculez vers l’onglet **Nœuds**. Sélectionnez le serveur de site en mode passif, puis cliquez sur **Promouvoir en mode actif** dans le ruban. Cliquez sur **Oui** pour continuer.   
  
2. Actualisez le nœud de la console. La colonne **État** du serveur que vous promouvez s’affiche sous l’onglet **Nœuds**. Il s’agit de l’état **Promotion**.  

3. Une fois la promotion terminée, la colonne **État** affiche **OK** à la fois pour le nouveau serveur de site en mode actif et pour le nouveau serveur de site en mode passif. La colonne **Nom du serveur** du site affiche désormais le nom du nouveau serveur de site en mode actif.

Pour connaître l’état détaillé, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **État du serveur de site**. La colonne **Mode** identifie le serveur *Actif* et le serveur *Passif*. Lorsque vous promouvez un serveur du mode passif au mode actif, sélectionnez le serveur de site en question, puis choisissez **Afficher l’état** dans le ruban. Cette opération ouvre la fenêtre État de promotion du serveur de site qui affiche des détails supplémentaires sur le processus.

Lorsqu’un serveur de site en mode actif bascule sur le mode passif, seul le rôle de système de site est rendu passif. Tous les autres rôles de système de site installés sur cet ordinateur restent actifs et accessibles aux clients.

Pour plus d’informations sur le processus de promotion *planifiée*, consultez [Promouvoir le serveur de site (planifié) - Diagramme](/sccm/core/servers/deploy/configure/promote-site-server-flowchart).


### <a name="unplanned-failover"></a>Basculement non planifié

Si le serveur de site en mode actif actuel est hors connexion, le serveur de site à promouvoir tente de le contacter pendant 30 minutes. Si le serveur hors connexion se reconnecte avant ces 30 minutes, celui-ci est notifié, et la modification se poursuit normalement. Sinon, le serveur de site à promouvoir force la mise à jour de la configuration du site pour que celui-ci soit actif. Si le serveur hors connexion ne s’est toujours pas reconnecté après ce délai, il vérifie d’abord l’état actuel dans la base de données du site. Ensuite, il se rétrograde lui-même en devenant le serveur de site en mode passif.

Pendant ces 30 minutes, aucun serveur de site n’est actif. Les clients continuent de communiquer avec les rôles qui leur répondent, comme les points de gestion, les points de mise à jour logicielle et les points de distribution. Les utilisateurs peuvent installer les logiciels qui sont déjà déployés. Aucune administration de site n’est possible pendant cette période. Pour plus d’informations, consultez [Impacts des défaillances du site](/sccm/core/servers/manage/site-failure-impacts).  

Si le serveur hors connexion est endommagé et ne peut pas répondre, supprimez le serveur de site à partir de la console. Ensuite, créez un serveur de site en mode passif pour restaurer un service hautement disponible. 

Pour plus d’informations sur le processus de basculement *non planifié*, consultez [Promouvoir le serveur de site (non planifié) - Diagramme](/sccm/core/servers/deploy/configure/promote-site-server-unplanned-flowchart).


### <a name="additional-tasks-after-site-server-promotion"></a>Tâches supplémentaires après la promotion d’un serveur de site  

Après le changement de serveur de site, vous n’avez pas à exécuter la plupart des autres tâches qui sont nécessaires lors d’une [récupération de site](/sccm/core/servers/manage/recover-sites#post-recovery-tasks). Par exemple, vous n’avez pas besoin de réinitialiser les mots de passe ou de reconnecter votre abonnement Microsoft Intune.

Les étapes suivantes peuvent être nécessaires si votre environnement l’exige :  

- Si vous importez des certificats PKI pour les points de distribution, réimporter le certificat pour les serveurs concernés. Pour plus d’informations, consultez [Regénérer les certificats pour les points de distribution](/sccm/core/servers/manage/recover-sites#regenerate-the-certificates-for-distribution-points).  

- Si vous intégrez Confguration Manager à Microsoft Store pour Entreprises, reconfigurez cette connexion. Pour plus d’informations, consultez [Gérer les applications à partir du Microsoft Store pour Entreprises](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).  



## <a name="daily-monitoring"></a>Surveillance quotidienne

Lorsque vous avez un serveur de site en mode passif, vous devez le surveiller quotidiennement. Vérifiez que son état est OK et qu’il est prêt à être utilisé. Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **État du serveur de site**. Affichez les serveurs de site et leur état actuel. Vous pouvez également voir l’état dans l’espace de travail **Administration**. Développez **Configuration du site**, puis sélectionnez le nœud **Sites**. Sélectionnez le site, puis basculez vers l’onglet **Nœuds**. 
