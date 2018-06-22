---
title: Configurer la passerelle de gestion cloud
titleSuffix: Configuraton Manager
description: Utilisez cette procédure pas à pas pour configurer une passerelle de gestion cloud (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 04c1b262704ec6458bd9773c28c43a50d8fc0840
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32338310"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurer la passerelle de gestion cloud pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*  

Ce processus comprend les étapes nécessaires pour configurer une passerelle de gestion cloud (CMG). 

> [!Tip]
> Cette fonctionnalité a été introduite dans la version 1610 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1802, cette fonctionnalité n’est plus en préversion.



## <a name="before-you-begin"></a>Avant de commencer

Commencez par lire l’article [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Utilisez cet article pour déterminer votre conception de la passerelle de gestion cloud. 

Utilisez la liste de vérification suivante pour vous assurer que vous disposez des informations nécessaires et des prérequis pour créer une passerelle de gestion cloud :  

- L’environnement Azure à utiliser. Par exemple, le cloud public Azure ou le cloud Azure US Government.  

- Vous avez besoin d’un ou de plusieurs certificats pour la passerelle de gestion cloud, en fonction de votre conception. Pour plus d’informations, consultez [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- À compter de la version 1802, choisissez si vous utilisez le **déploiement Azure Resource Manager** ou un **déploiement de service classique**. Pour plus d’informations, consultez [Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Vous devez respecter les exigences suivantes pour un déploiement Azure Resource Manager de la passerelle de gestion cloud :  

    - Intégration à [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**. Découverte d’utilisateurs Azure AD non requise.  

    - Un administrateur des abonnements doit se connecter.  

- Vous devez respecter les exigences suivantes pour un déploiement de service classique de la passerelle de gestion cloud :  

    - ID d’abonnement Azure  

    - Certificat de gestion Azure  

- Un nom global unique pour le service. Ce nom provient du [ certificat d’authentification serveur de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).  

- La région Azure pour le déploiement de cette passerelle de gestion cloud.  

- Nombre d’instances de machine virtuelle dont vous avez besoin pour la mise à l’échelle et la redondance.  



## <a name="set-up-a-cmg"></a>Configurer une passerelle de gestion cloud

Effectuez cette procédure sur le site de niveau supérieur. Ce site est soit un site principal autonome, soit le site d’administration centrale.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Passerelle de gestion cloud**.  

2. Cliquez sur **Créer une Passerelle de gestion cloud** dans le ruban.  

3. À compter de la version 1802, dans la page Général de l’Assistant, choisissez d’abord la méthode de déploiement CMG : **Déploiement d’Azure Resource Manager** ou **Déploiement de service Classic**.  

    1. Pour le **déploiement Azure Resource Manager** : cliquez sur **Se connecter** pour vous authentifier avec un compte d’administrateur d’abonnements Azure. L’Assistant remplit automatiquement les champs restants à partir des informations stockées dans les prérequis de l’intégration d’Azure AD. Si vous possédez plusieurs abonnements, sélectionnez l’**ID de l’abonnement** que vous voulez utiliser.  

    2. Pour le **déploiement de service classique** *et les versions 1706 et 1710 de Configuration Manager* : entrez votre **ID d’abonnement** Azure. Cliquez ensuite sur **Parcourir**, puis sélectionnez le fichier .PFX du certificat de gestion Azure. 

4. Spécifiez l’**environnement Azure** pour cette passerelle de gestion cloud. Les options disponibles dans la liste déroulante peuvent varier en fonction de la méthode de déploiement.  

5. Cliquez sur **Suivant**. Attendez que le site teste la connexion à Azure.  

4. Dans la page Paramètres de l’Assistant, cliquez d’abord sur **Parcourir**, puis sélectionnez le fichier .PFX correspondant au certificat d’authentification serveur de la passerelle de gestion cloud. Le nom de ce certificat remplit les champs **Nom de domaine complet du service** et **Nom du service**.  

   > [!NOTE]  
   > À compter de la version 1802, le certificat d’authentification serveur de la passerelle de gestion cloud prend en charge les caractères génériques. Si vous utilisez un certificat générique, remplacez l’astérisque (\*) dans le champ **Nom de domaine complet du service** par le nom d’hôte souhaité pour la passerelle de gestion cloud.  
   <!--491233-->  

5. Cliquez sur la liste déroulante **Région** pour choisir la région Azure pour cette passerelle de gestion cloud.  

6. Dans la version 1802 et si vous utilisez un déploiement Azure Resource Manager, sélectionnez une option**Groupe de ressources**. 
   1. Si vous choisissez **Utiliser le fichier existant**, sélectionnez un groupe de ressources existant dans la liste déroulante.
   2. Si vous choisissez **Créer**, entrez le nom du nouveau groupe de ressources.

6. Dans le champ **Instance de machine virtuelle**, entrez le nombre de machines virtuelles pour ce service. La valeur par défaut est 1, mais vous pouvez définir jusqu’à 16 machines virtuelles par passerelle de gestion cloud.  

7. Cliquez sur **Certificats** pour ajouter des certificats racines approuvés de client. Ajoutez jusqu’à deux autorités de certification racines de confiance et quatre autorités de certification (subordonnées) intermédiaires.  

8. Par défaut, l’Assistant active l’option permettant de **Vérifier la révocation des certificats clients**. Une liste de révocation de certificats doit être publiée publiquement pour que cette vérification fonctionne. Si vous ne publiez pas de liste de révocation de certificats, décochez cette option.  

9. Cliquez sur **Suivant**.  

10. Pour surveiller le trafic de la passerelle de gestion cloud avec un seuil de 14 jours, cochez la case pour activer l’alerte de seuil. Ensuite, spécifiez le seuil et le pourcentage auquel déclencher les différents niveaux d’alerte. Choisissez **Suivant** quand vous avez terminé.  

11. Vérifiez les paramètres, puis choisissez **Suivant**. Configuration Manager commence à configurer le service. Une fois l’Assistant fermé, 5 à 15 minutes sont nécessaires pour provisionner complètement le service dans Azure. Vérifiez la colonne **État** de la nouvelle passerelle de gestion cloud pour déterminer quand le service est prêt.  

 > [!Note]  
 > Pour résoudre les problèmes de déploiement de passerelle de gestion cloud, utilisez **CloudMgr.log** et **CMGSetup.log**. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurer le site principal pour l’authentification de certification client

Si vous utilisez des [certificats d’authentification client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) pour que les clients s’authentifient auprès de la passerelle de gestion cloud, suivez la procédure suivante pour configurer chaque site principal.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**.  

2. Sélectionnez le site principal auquel vos clients Internet sont affectés, puis choisissez **Propriétés**.  

3. Passer à l’onglet **Communications des ordinateurs clients** de la feuille de propriétés du site principal, puis cochez la case **Utiliser le certificat client PKI (fonctionnalité d’authentification du client) lorsqu’il est disponible**.  

4. Si vous ne publiez pas de liste de révocation de certificats, désactivez l’option **Les clients vérifient la liste de révocation des certificats (CRL) pour les systèmes de site**.  



## <a name="add-the-cmg-connection-point"></a>Ajouter le point de connexion CMG

Le point de connexion CMG est le rôle de système de site permettant de communiquer avec la passerelle de gestion cloud. Pour ajouter le point de connexion CMG, suivez les instructions générales fournies pour [installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Dans la page Sélection du rôle système de l’Assistant Ajout des rôles de système de site, sélectionnez **Point de connexion de la passerelle de gestion cloud**. Sélectionnez ensuite le **Nom de la passerelle de gestion cloud** à laquelle ce serveur se connecte. L’Assistant affiche la région pour la passerelle de gestion cloud sélectionnée. 

> [!Important]
> Dans certains cas, le point de connexion CMG doit avoir un [certificat d’authentification client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate). 

 > [!Note]  
 > Pour résoudre les problèmes liés à l’intégrité du service de passerelle de gestion cloud, utilisez **CMGService.log** et **SMS_Cloud_ProxyConnector.log**. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurer les utilisés par le client pour le trafic de la passerelle de gestion cloud

Configurez les systèmes de site de point de gestion et de point de mise à jour logicielle pour accepter le trafic de la passerelle de gestion cloud. Effectuez cette procédure sur le site principal, pour tous les points de gestion et tous les points de mise à jour logicielle qui gèrent des clients Internet.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, cliquez avec le bouton droit sur **Serveurs et rôles de système de site**, puis sélectionnez **Point de gestion** dans la liste.  

2. Sélectionnez le serveur de système de site que vous souhaitez configurer pour le trafic de la passerelle de gestion cloud. Sélectionnez le rôle **Point de gestion** dans le volet d’informations, puis cliquez sur **Propriétés** dans le ruban.  

3. Dans la feuille des propriétés Point de gestion, sous Connexions client, cochez la case située en regard de l’option **Autoriser le trafic de la passerelle de gestion cloud de Configuration Manager**. 
    - En fonction de votre conception de la passerelle de gestion cloud et de la version de Configuration Manager, vous devrez peut-être activer l’option **HTTPS**. Pour plus d’informations, consultez [Activer le point de gestion pour HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

4. Cliquez sur **OK**.   

Répétez ces étapes pour les points de gestion supplémentaires si nécessaire, et pour tous les points de mise à jour logicielle. 



## <a name="configure-clients-for-cmg"></a>Configurer des clients pour la passerelle de gestion cloud

Une fois que la passerelle de gestion cloud et les rôles de système de site sont en cours d’exécution, les clients obtiennent automatiquement l’emplacement du service de passerelle de gestion cloud à la prochaine demande d’emplacement. Les clients doivent se trouver sur l’intranet pour recevoir l’emplacement du service de passerelle de gestion cloud, sauf si vous [installez et attribuez des clients Windows 10 à l’aide d’Azure AD à des fins d’authentification](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Le cycle d’interrogation pour les demandes d’emplacement est de 24 heures. Si vous ne souhaitez pas attendre la demande d’emplacement normalement planifiée, vous pouvez forcer la demande en redémarrant le service hôte de l’agent SMS (ccmexec.exe) sur l’ordinateur.  

> [!Note]
> Par défaut, tous les clients reçoivent une stratégie de passerelle de gestion cloud. Contrôlez ce paramètre à l’aide du paramètre client [Autoriser les clients à utiliser une passerelle de gestion cloud](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway).

Le client Configuration Manager détermine automatiquement s’il est sur l’intranet ou sur Internet. Si le client peut contacter un contrôleur de domaine ou un point de gestion local, il définit son type de connexion sur **Intranet actuellement**. Sinon, il passe à **Internet actuellement** et utilise l’emplacement du service de passerelle de gestion cloud pour communiquer avec le site.

>[!NOTE]
> Vous pouvez forcer le client à toujours utiliser la passerelle de gestion cloud, qu’il se trouve sur l’intranet ou sur Internet. Cette configuration est utile à des fins de test, ou pour les clients se trouvant dans des bureaux distants et que vous voulez forcer à utiliser la passerelle de gestion cloud. Définissez la clé de Registre suivante sur le client :
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> Vous pouvez également spécifier ce paramètre pendant l’installation du client à l’aide de la propriété [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf).

Pour vérifier que les clients disposent de la stratégie spécifiant la passerelle de gestion cloud, ouvrez une invite de commandes Windows PowerShell en tant qu’administrateur sur l’ordinateur client, puis exécutez la commande suivante : `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}`

Cette commande affiche tous les points de gestion Internet que le client connaît. Quand la passerelle de gestion cloud n’est pas techniquement un point de gestion Internet, elle s’affiche comme telle aux clients.

 > [!Note]  
 > Pour résoudre les problèmes liés au trafic client de passerelle de gestion cloud, utilisez **CMGHttpHandler.log**, **CMGService.log** et **SMS_Cloud_ProxyConnector.log**. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="modify-a-cmg"></a>Modifier une passerelle de gestion cloud

Après avoir créé une passerelle de gestion cloud, vous pouvez modifier certains de ses paramètres. Sélectionnez la passerelle de gestion cloud dans la console Configuration Manager, puis cliquez sur **Propriétés**. Les paramètres suivants sont configurables :  

- **Général**  

    - **Certificat de gestion Azure** : changez le certificat de gestion Azure pour la passerelle de gestion cloud. Cette option est utile lors de la mise à jour du certificat avant son expiration.  

- **Paramètres**  

    - **Fichier de certificat** : changez le certificat d’authentification serveur pour la passerelle de gestion cloud. Cette option est utile lors de la mise à jour du certificat avant son expiration.  

    - **Instance de machine virtuelle** : changez le nombre de machines virtuelles que le service utilise dans Azure. Ce paramètre vous permet de faire monter ou descendre en puissance le service de façon dynamique en fonction de considérations relatives à l’utilisation ou au coût.  

    - **Certificats** : ajoutez ou supprimez des certificats d’autorité de certification intermédiaires ou racines de confiance. Cette option est utile lors de l’ajout de nouvelles autorités de certification ou du retrait de certificats expirés.  

    - **Vérifier la révocation des certificats clients** : si vous n’avez pas activé ce paramètre initialement lors de la création de la passerelle de gestion cloud, vous pouvez l’activer ultérieurement une fois que vous publiez la liste de révocation de certificats.  

- **Alertes** : vous pouvez reconfigurer les alertes à tout moment après avoir créé la passerelle de gestion cloud. 

Les changements plus importants, tels que les configurations suivantes, exigent de redéployer le service :
- Méthode de déploiement classique sur Azure Resource Manager
- Abonnement
- Nom du service
- De PKI privée à PKI publique
- Région

Conservez toujours au moins une passerelle de gestion cloud active pour que les clients Internet reçoivent la stratégie mise à jour. Les clients Internet ne peuvent pas communiquer avec une passerelle de gestion cloud supprimée. Les clients n’ont pas connaissance de l’existence d’une nouvelle passerelle tant qu’ils ne se reconnectent pas à l’intranet. Quand vous créez une deuxième instance de passerelle de gestion cloud afin de supprimer la première, créez également un autre point de connexion CMG.

Étant donné que les clients actualisent la stratégie par défaut toutes les 24 heures, attendez au moins un jour après avoir créé une passerelle de gestion cloud pour supprimer l’ancienne. Si les clients sont désactivés ou sans connexion Internet, vous devrez peut-être attendre plus longtemps. 

À compter de la version 1802, si vous avez une passerelle de gestion cloud existante sur la méthode de déploiement classique, vous devez déployer une nouvelle passerelle de gestion cloud pour utiliser la méthode de déploiement Azure Resource Manager.<!--509753--> Il existe deux options :
- Si vous voulez réutiliser le même nom de service :
    1. Supprimez d’abord la passerelle de gestion cloud classique, en respectant le conseil de toujours avoir au moins une passerelle de gestion cloud active pour les clients Internet.
    2. Créez une passerelle de gestion cloud à l’aide d’un déploiement Resource Manager. Réutilisez le même certificat d’authentification serveur.
    3. Reconfigurez le point de connexion CMG pour utiliser la nouvelle instance de passerelle de gestion cloud.
- Si vous voulez utiliser un nouveau nom de service :
    1. Créez une passerelle de gestion cloud à l’aide d’un déploiement Resource Manager. Utilisez un nouveau certificat d’authentification serveur.
    2. Créez un point de connexion CMG et un lien avec la nouvelle passerelle de gestion cloud.
    3. Attendez au moins un jour que les clients Internet reçoivent la stratégie sur la nouvelle passerelle de gestion cloud.
    4. Supprimez la passerelle de gestion cloud classique.

Modifiez la passerelle de gestion cloud uniquement à partir de la console Configuration Manager. Apporter des modifications au service ou à des machines virtuelles sous-jacentes directement dans Azure n’est pas pris en charge. Tous les changements apportés peuvent être perdus sans préavis. Comme avec n’importe quel service PaaS, le service peut regénérer les machines virtuelles à tout moment. Ces régénérations peuvent se produire pour la maintenance du matériel principal, ou pour appliquer des mises à jour au système d’exploitation des machines virtuelles.

Si vous devez supprimer la passerelle de gestion cloud, effectuez-le également à partir de la console Configuration Manager. La suppression manuelle de tout composant dans Azure entraîne l’incohérence du système. Cet état conserve des informations orphelines, et des comportements inattendus peuvent se produire. 



## <a name="next-steps"></a>Étapes suivantes

- [Surveiller les clients pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Questions fréquentes (FAQ) sur la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
