---
title: Configurer la passerelle de gestion cloud
titleSuffix: Configuration Manager
description: Utilisez cette procédure pas à pas pour configurer une passerelle de gestion cloud (CMG).
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 11/27/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.collection: M365-identity-device-management
ms.openlocfilehash: e937bf4adf3b695bf33d41318e5d48bc560ad06b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56128100"
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configurer la passerelle de gestion cloud pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*  

Ce processus comprend les étapes nécessaires pour configurer une passerelle de gestion cloud (CMG). 

> [!Tip]
> Cette fonctionnalité a été introduite dans la version 1610 en tant que [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). À compter de la version 1802, cette fonctionnalité n’est plus en préversion.



## <a name="before-you-begin"></a>Avant de commencer

Commencez par lire l’article [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway). Utilisez cet article pour déterminer votre conception de la passerelle de gestion cloud. 

Utilisez la liste de vérification suivante pour vous assurer que vous disposez des informations nécessaires et des prérequis pour créer une passerelle de gestion cloud :  

- L’environnement Azure à utiliser. Par exemple, le cloud public Azure ou le cloud Azure US Government.  

- Vous avez besoin d’un ou de plusieurs certificats pour la passerelle de gestion cloud, en fonction de votre conception. Pour plus d’informations, consultez [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway).  

- À compter de la version 1802, sélectionnez le **déploiement Azure Resource Manager**. Pour plus d’informations, consultez [Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager). Vous devez respecter les exigences suivantes pour un déploiement Azure Resource Manager de la passerelle de gestion cloud :  

    - Intégration à [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**. La découverte des utilisateurs Azure AD n’est pas nécessaire.  
    
    - Le fournisseur de ressources **Microsoft.ClassicCompute** doit être enregistré dans l’abonnement Azure. Pour plus d’informations, consultez [Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-supported-services).

    - Un administrateur de l’abonnement doit se connecter.  

- Vous devez respecter les exigences suivantes pour un déploiement de service classique de la passerelle de gestion cloud :  

    > [!Important]  
    > Depuis la version 1810, les déploiements de services Classic dans Azure sont dépréciés dans Configuration Manager. Commencez par utiliser des déploiements Azure Resource Manager pour la passerelle de gestion cloud. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).  

    - ID d’abonnement Azure  

    - Certificat de gestion Azure  

- Un nom global unique pour le service. Ce nom provient du [ certificat d’authentification serveur de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).  

- En cas d’activation de la passerelle de gestion cloud en tant que Point de distribution cloud, le nom de service général unique de la passerelle de gestion cloud choisi doit également être disponible en tant que nom de compte de stockage général unique. Ce nom provient du [ certificat d’authentification serveur de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate).

- La région Azure pour le déploiement de cette passerelle de gestion cloud.  

- Nombre d’instances de machine virtuelle dont vous avez besoin pour la mise à l’échelle et la redondance.  



## <a name="set-up-a-cmg"></a>Configurer une passerelle de gestion cloud

Effectuez cette procédure sur le site de plus haut niveau. Ce site est soit un site principal autonome, soit le site d’administration centrale.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez **Passerelle de gestion cloud**.  

2. Sélectionnez **Créer une Passerelle de gestion cloud** dans le ruban.  

3. À compter de la version 1802, dans la page Général de l’Assistant, sélectionnez **Déploiement d’Azure Resource Manager** comme méthode de déploiement de la passerelle de gestion cloud.  

    Sélectionnez **Se connecter** pour vous authentifier avec un compte Administrateur d’abonnement Azure. L’Assistant remplit automatiquement les champs restants à partir des informations stockées dans les prérequis de l’intégration d’Azure AD. Si vous possédez plusieurs abonnements, sélectionnez l’**ID de l’abonnement** que vous voulez utiliser.

    > [!Note]  
    > Depuis la version 1810, les déploiements de services Classic dans Azure sont dépréciés dans Configuration Manager. 
    > 
    > Si vous devez utiliser un déploiement de service Classic, sélectionnez cette option dans cette page. Entrer d’abord votre **ID d’abonnement** Azure. Sélectionnez ensuite **Parcourir**, puis choisissez le fichier .PFX du certificat de gestion Azure. 

4. Spécifiez l’**environnement Azure** pour cette passerelle de gestion cloud. Les options disponibles dans la liste déroulante peuvent varier en fonction de la méthode de déploiement.  

5. Sélectionnez **Suivant**. Attendez que le site teste la connexion à Azure.  

6. Dans la page Paramètres de l’Assistant, sélectionnez d’abord **Parcourir**, puis choisissez le fichier .PFX correspondant au certificat d’authentification serveur de la passerelle de gestion cloud. Le nom de ce certificat remplit les champs **Nom de domaine complet du service** et **Nom du service**.  

   > [!NOTE]  
   > À compter de la version 1802, le certificat d’authentification serveur de la passerelle de gestion cloud prend en charge les caractères génériques. Si vous utilisez un certificat générique, remplacez l’astérisque (\*) dans le champ **Nom de domaine complet du service** par le nom d’hôte souhaité pour la passerelle de gestion cloud.  
   <!--491233-->  

7. Sélectionnez la liste déroulante **Région** pour choisir la région Azure pour cette passerelle de gestion cloud.  

8. Dans la version 1802 et si vous utilisez un déploiement Azure Resource Manager, sélectionnez une option**Groupe de ressources**. 
   1. Si vous choisissez **Utiliser le fichier existant**, sélectionnez un groupe de ressources existant dans la liste déroulante. Le groupe de ressources sélectionné doit déjà exister dans la région que vous avez sélectionnée à l’étape 7. Si vous sélectionnez un groupe de ressources existant et qu’il se trouve dans une région différente de celle de la région sélectionnée précédemment, le provisionnement de la passerelle de gestion cloud échoue.
   2. Si vous choisissez **Créer**, entrez le nom du nouveau groupe de ressources.

9. Dans le champ **Instance de machine virtuelle**, entrez le nombre de machines virtuelles pour ce service. La valeur par défaut est 1, mais vous pouvez définir jusqu’à 16 machines virtuelles par passerelle de gestion cloud.  

10. Sélectionnez **Certificats** pour ajouter des certificats racines approuvés de client. Ajoutez jusqu’à deux autorités de certification racines de confiance et quatre autorités de certification (subordonnées) intermédiaires.  

     > [!Note]  
     > À compter de la version 1806, quand vous créez une passerelle de gestion cloud, vous n’êtes plus obligé de fournir un certificat racine approuvé dans la page Paramètres. Ce certificat n’est pas nécessaire lorsque vous utilisez Azure Active Directory (Azure AD) pour l’authentification client, mais il était auparavant nécessaire dans l’Assistant. Si vous utilisez des certificats d’authentification client PKI, vous devez néanmoins encore ajouter un certificat racine approuvé pour la passerelle de gestion cloud.<!--SCCMDocs-pr issue #2872-->  

11. Par défaut, l’Assistant active l’option permettant de **Vérifier la révocation des certificats clients**. Une liste de révocation de certificats doit être publiée publiquement pour que cette vérification fonctionne. Si vous ne publiez pas de liste de révocation de certificats, désélectionnez cette option.  

12. À compter de la version 1806, l’assistant active l’option suivante par défaut : **Autoriser la passerelle de gestion cloud à fonctionner comme point de distribution cloud et à servir du contenu à partir du stockage Azure**. À présent, une passerelle de gestion cloud peut également délivrer du contenu aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure.  

13. Sélectionnez **Suivant**.  

14. Pour surveiller le trafic de la passerelle de gestion cloud avec un seuil de 14 jours, cochez la case pour activer l’alerte de seuil. Ensuite, spécifiez le seuil et le pourcentage auquel déclencher les différents niveaux d’alerte. Choisissez **Suivant** quand vous avez terminé.  

15. Vérifiez les paramètres, puis choisissez **Suivant**. Configuration Manager commence à configurer le service. Une fois l’Assistant fermé, 5 à 15 minutes sont nécessaires pour provisionner complètement le service dans Azure. Vérifiez la colonne **État** de la nouvelle passerelle de gestion cloud pour déterminer quand le service est prêt.  

    > [!Note]  
    > Pour résoudre les problèmes de déploiement de passerelle de gestion cloud, utilisez **CloudMgr.log** et **CMGSetup.log**. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-primary-site-for-client-certificate-authentication"></a>Configurer le site principal pour l’authentification de certification client

Si vous utilisez des [certificats d’authentification client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate) pour que les clients s’authentifient auprès de la passerelle de gestion cloud, suivez cette procédure pour configurer chaque site principal.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez **Sites**.  

2. Sélectionnez le site principal auquel vos clients Internet sont affectés, puis choisissez **Propriétés**.  

3. Passer à l’onglet **Communications des ordinateurs clients** de la feuille de propriétés du site principal, puis cochez la case **Utiliser le certificat client PKI (fonctionnalité d’authentification du client) lorsqu’il est disponible**.  

4. Si vous ne publiez pas de liste de révocation de certificats, désélectionnez l’option **Les clients vérifient la liste de révocation des certificats (CRL) pour les systèmes de site**.  



## <a name="add-the-cmg-connection-point"></a>Ajouter le point de connexion CMG

Le point de connexion CMG est le rôle de système de site permettant de communiquer avec la passerelle de gestion cloud. Pour ajouter le point de connexion CMG, suivez les instructions générales fournies pour [installer des rôles de système de site](/sccm/core/servers/deploy/configure/install-site-system-roles). Dans la page Sélection du rôle système de l’Assistant Ajout des rôles de système de site, sélectionnez **Point de connexion de la passerelle de gestion cloud**. Sélectionnez ensuite le **Nom de la passerelle de gestion cloud** à laquelle ce serveur se connecte. L’Assistant affiche la région pour la passerelle de gestion cloud sélectionnée. 

> [!Important]
> Dans certains cas, le point de connexion CMG doit avoir un [certificat d’authentification client](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate). 

 > [!Note]  
 > Pour résoudre les problèmes liés à l’intégrité du service de passerelle de gestion cloud, utilisez **CMGService.log** et **SMS_Cloud_ProxyConnector.log**. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>Configurer les utilisés par le client pour le trafic de la passerelle de gestion cloud

Configurez les systèmes de site de point de gestion et de point de mise à jour logicielle pour accepter le trafic de la passerelle de gestion cloud. Effectuez cette procédure sur le site principal, pour tous les points de gestion et tous les points de mise à jour logicielle qui gèrent des clients Internet.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Serveurs et rôles de système de site**. Sous l’onglet Accueil du ruban, dans le groupe Affichage, sélectionnez **Serveurs avec rôle**. Sélectionnez ensuite **Point de gestion** dans la liste.  

2. Sélectionnez le serveur de système de site que vous souhaitez configurer pour le trafic de la passerelle de gestion cloud. Sélectionnez le rôle **Point de gestion** dans le volet d’informations, puis sélectionnez **Propriétés** dans le ruban.  

3. Dans la feuille des propriétés Point de gestion, sous Connexions client, cochez la case située en regard de l’option **Autoriser le trafic de la passerelle de gestion cloud de Configuration Manager**. 
    - En fonction de votre conception de la passerelle de gestion cloud et de la version de Configuration Manager, vous devrez peut-être activer l’option **HTTPS**. Pour plus d’informations, consultez [Activer le point de gestion pour HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https).  

4. Sélectionnez **OK** pour fermer la fenêtre des propriétés du point de gestion.   

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

Cette commande affiche tous les points de gestion Internet que le client connaît. Alors que la passerelle de gestion cloud n’est techniquement pas un point de gestion Internet, les clients la voient cependant comme telle.

 > [!Note]  
 > Pour résoudre les problèmes liés au trafic client de passerelle de gestion cloud, utilisez **CMGHttpHandler.log**, **CMGService.log** et **SMS_Cloud_ProxyConnector.log**. Pour plus d’informations, consultez [Fichiers journaux](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway).



## <a name="modify-a-cmg"></a>Modifier une passerelle de gestion cloud

Après avoir créé une passerelle de gestion cloud, vous pouvez modifier certains de ses paramètres. Sélectionnez la passerelle de gestion cloud dans la console Configuration Manager, puis sélectionnez **Propriétés**. Configurez les paramètres sous les onglets suivants :  

#### <a name="general"></a>Général

- **Certificat de gestion Azure** : changez le certificat de gestion Azure pour la passerelle de gestion cloud. Cette option est utile lors de la mise à jour du certificat avant son expiration.  

#### <a name="settings"></a>Paramètres

- **Fichier de certificat** : changez le certificat d’authentification serveur pour la passerelle de gestion cloud. Cette option est utile lors de la mise à jour du certificat avant son expiration.  

- **Instance de machine virtuelle** : changez le nombre de machines virtuelles que le service utilise dans Azure. Ce paramètre vous permet de faire monter ou descendre en puissance le service de façon dynamique en fonction de considérations relatives à l’utilisation ou au coût.  

- **Certificats** : ajoutez ou supprimez des certificats d’autorité de certification intermédiaires ou racines de confiance. Cette option est utile lors de l’ajout de nouvelles autorités de certification ou du retrait de certificats expirés.  

- **Vérifier la révocation des certificats clients** : si vous n’avez pas initialement activé ce paramètre lors de la création de la passerelle de gestion cloud, vous pouvez l’activer ultérieurement une fois que vous publiez la liste de révocation de certificats.  

- **Autoriser la passerelle de gestion cloud à fonctionner comme point de distribution cloud et à servir du contenu à partir du stockage Azure** : À compter de la version 1806, cette nouvelle option est activée par défaut. À présent, une passerelle de gestion cloud peut également délivrer du contenu aux clients. Cette fonctionnalité réduit le nombre de certificats nécessaires, ainsi que les coûts associés aux machines virtuelles Azure.<!--1358651-->  

#### <a name="alerts"></a>Alertes
Reconfigurez les alertes à tout moment après avoir créé la passerelle de gestion cloud. 


### <a name="redeploy-the-service"></a>Redéployer le service

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

> [!Tip]  
> Pour déterminer le modèle de déploiement actuel d’une passerelle de gestion cloud :<!--SCCMDocs issue #611-->  
> 1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Passerelle de gestion cloud**.  
> 2. Sélectionnez l’instance de la passerelle de gestion cloud.  
> 3. Dans le volet Détails en bas de la fenêtre, recherchez l’attribut **Modèle de déploiement**. Pour un déploiement Resource Manager, cet attribut est **Azure Resource Manager**. 
> 
> Vous pouvez aussi ajouter l’attribut **Modèle de déploiement** comme colonne de la vue de liste.  


### <a name="modifications-in-the-azure-portal"></a>Modifications dans le portail Azure

Modifiez la passerelle de gestion cloud uniquement à partir de la console Configuration Manager. La possibilité d’apporter des modifications au service ou à des machines virtuelles sous-jacentes directement dans Azure n’est pas prise en charge. Tous les changements apportés peuvent être perdus sans préavis. Comme avec n’importe quel service PaaS, le service peut regénérer les machines virtuelles à tout moment. Ces régénérations peuvent se produire pour la maintenance du matériel principal, ou pour appliquer des mises à jour au système d’exploitation des machines virtuelles.


### <a name="delete-the-service"></a>Supprimer le service

Si vous devez supprimer la passerelle de gestion cloud, effectuez-le également à partir de la console Configuration Manager. La suppression manuelle de tout composant dans Azure entraîne l’incohérence du système. Cet état conserve des informations orphelines, et des comportements inattendus peuvent se produire. 



## <a name="next-steps"></a>Étapes suivantes

- [Surveiller les clients pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [Questions fréquentes (FAQ) sur la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
