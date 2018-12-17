---
title: Approuver les applications
titleSuffix: Configuration Manager
description: Découvrez les paramètres et les comportements d’approbation d’applications dans Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 20493c86-6454-4b35-8f22-0d049b68b8bb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f19146da963055ffc20b274e1017802274844698
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52458055"
---
# <a name="approve-applications-in-configuration-manager"></a>Approuver des applications dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Au moment de [déployer une application](/sccm/apps/deploy-use/deploy-applications) dans Configuration Manager, vous pouvez exiger une approbation avant l’installation. Une fois que les utilisateurs ont demandé l’application dans le Centre logiciel, vous examinez la demande dans la console Configuration Manager. Vous pouvez l’approuver ou la refuser. 



## <a name="bkmk_approval"></a> Paramètres d’approbation

Le comportement d’approbation d’applications dépend de votre version de Configuration Manager. La page **Paramètres de déploiement** du déploiement d’application présente l’un des paramètres d’approbation suivants :  

#### <a name="require-administrator-approval-if-users-request-this-application"></a>Exiger l’approbation de l’administrateur si des utilisateurs demandent cette application
*S’applique aux versions 1710 et antérieures*

L’administrateur approuve les demandes des utilisateurs pour une application avant qu’ils puissent l’installer. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou que vous déployez l’application sur un regroupement d’appareils.  

Les demandes d'approbation d'application sont affichées dans le nœud **Demandes d'approbation** , sous **Gestion d'applications** dans l'espace de travail **Bibliothèque de logiciels** . Si une demande ne reçoit pas d’approbation dans les 30 jours, elle est supprimée. La réinstallation du client risque d’annuler des demandes d’approbation en attente.  

Après avoir approuvé l’installation d’une application, vous pouvez **Refuser** la demande dans la console Configuration Manager. Cette action n’entraîne pas la désinstallation de l’application de tous les appareils par le client. Elle empêche les utilisateurs d’installer de nouvelles copies de l’application à partir du Centre logiciel.  


#### <a name="an-administrator-must-approve-a-request-for-this-application-on-the-device"></a>Un administrateur doit approuver la demande de cette application sur l’appareil
*S’applique aux versions 1802 et ultérieures<sup>[Remarque 1](#bkmk_note1)</sup>*

<a name="bkmk_note1"></a>

> [!Note]  
> **Remarque 1** : Par défaut, Configuration Manager n’active pas cette fonctionnalité facultative. Vous devez activer cette fonctionnalité avant de l’utiliser. Pour plus d’informations, consultez [Activer les fonctionnalités facultatives des mises à jour](/sccm/core/servers/manage/install-in-console-updates#bkmk_options). 
> 
> Si vous n’activez pas cette fonctionnalité, c’est l’expérience antérieure qui prévaut.  

L’administrateur approuve les demandes des utilisateurs pour une application avant qu’ils puissent l’installer sur l’appareil demandé. Si l’administrateur approuve la demande, l’utilisateur ne pourra installer l’application que sur cet appareil. Il devra soumettre une autre demande pour installer l’application sur un autre appareil. Cette option est grisée quand l’objet du déploiement est **Obligatoire** ou que vous déployez l’application sur un regroupement d’appareils. <!--1357015-->  

> [!Note]  
> Pour tirer parti des nouvelles fonctionnalités de Configuration Manager, commencez par mettre à jour les clients vers la dernière version. Bien que les nouvelles fonctionnalités s’affichent dans la console Configuration Manager quand vous mettez à jour le site et la console, le scénario complet n’est pas fonctionnel tant que la version cliente n’est pas également la plus récente.<!--SCCMDocs issue 646-->  

Affichez **Demandes d’approbation** sous **Gestion des applications** dans l’espace de travail **Bibliothèque de logiciels** de la console de Configuration Manager. Il y a maintenant une colonne **Appareil** dans la liste de chaque demande. À chaque action effectuée sur la demande, la boîte de dialogue Demande d’application comprend également le nom de l’appareil utilisé par l’utilisateur pour envoyer la demande.  

Si une demande ne reçoit pas d’approbation dans les 30 jours, elle est supprimée. La réinstallation du client risque d’annuler des demandes d’approbation en attente.  

Après avoir approuvé l’installation d’une application, vous pouvez **Refuser** la demande dans la console Configuration Manager. Cette action n’entraîne pas la désinstallation de l’application de tous les appareils par le client. Elle empêche les utilisateurs d’installer de nouvelles copies de l’application à partir du Centre logiciel.  

> [!Important]  
> Depuis la version 1806, *le comportement est différent* quand vous révoquez une approbation pour une application qui a été approuvée et installée. Maintenant, quand vous **refusez** la demande visant l’application, le client désinstalle l’application sur l’appareil de l’utilisateur.<!--1357891-->  



## <a name="bkmk_email-approve"></a> Notifications par e-mail
<!--1321550-->

Depuis la version 1810, configurez les notifications par e-mail pour les demandes d’approbation d’applications. Quand un utilisateur demande une application, vous recevez un e-mail. Cliquez sur les liens de l’e-mail pour approuver ou refuser la demande, sans avoir besoin d’utiliser la console Configuration Manager.


### <a name="prerequisites"></a>Prérequis

#### <a name="to-send-email-notifications-and-take-action-on-internal-network"></a>Pour envoyer des notifications par e-mail et effectuer une action sur le réseau interne
Avec ces prérequis, les destinataires reçoivent un e-mail avec une notification de la demande. S’ils se trouvent sur le réseau interne, ils peuvent aussi approuver ou refuser la demande à partir de l’e-mail.

- Activez la [fonctionnalité facultative](/sccm/core/servers/manage/install-in-console-updates#bkmk_options) **Approuver les demandes d’application pour les utilisateurs appareil par appareil**.  

- Configurez la [notification par e-mail pour les alertes](/sccm/core/servers/manage/use-alerts-and-the-status-system#to-configure-email-notification-for-alerts).  



#### <a name="to-take-action-from-internet"></a>Pour effectuer une action depuis Internet
Avec ces autres prérequis facultatifs, les destinataires peuvent approuver ou refuser la demande de n’importe où pourvu qu’ils disposent d’un accès Internet.

- Activez le service d’administration Fournisseur SMS via la passerelle de gestion cloud. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Configuration du site**, puis sélectionnez le nœud **Serveurs et rôles de système de site**. Sélectionnez le serveur associé au rôle Fournisseur SMS. Dans le volet d’informations, sélectionnez le rôle **Fournisseur SMS** et **Propriétés** dans le ruban de l’onglet Rôle du site. Sélectionnez l’option **Autoriser le trafic de la passerelle de gestion cloud Configuration Manager pour le service d’administration**.  

    - Le fournisseur SMS exige **.NET 4.5.2** ou une version ultérieure.  

- [Passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)  

- Intégrer le site aux [services Azure](/sccm/core/servers/deploy/configure/azure-services-wizard) pour la **gestion cloud**  

    - Activer la [découverte d’utilisateurs Azure AD](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Configurez manuellement les paramètres dans Azure AD :  

        1. Accédez au [portail Azure](https://portal.azure.com), sélectionnez **Azure Active Directory** et **Inscriptions d’applications**.  

        2. Sélectionnez l’application de type **Natif** que vous avez créée pour l’intégration de la **Gestion cloud** de Configuration Manager.  

        3. Dans les propriétés de l’application, sélectionnez **Paramètres**, puis **URI de redirection**.  

            1. Dans le volet URI de redirection, collez le chemin suivant : `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`  

            2. Remplacez `<CMG FQDN>` par le nom de domaine complet (FQDN) de votre service CMG (Passerelle de gestion cloud). Par exemple, GraniteFalls.Contoso.com.  

            3. Sélectionnez ensuite **Enregistrer**. Fermez le volet **Paramètres**.  

        4. Dans les propriétés de l’application, sélectionnez **Manifeste**.  

            1. Dans le volet Modifier le manifeste, recherchez la propriété **oauth2AllowImplicitFlow**.  

            2. Modifiez sa valeur en indiquant **true**. Par exemple, la ligne entière doit se présenter comme ceci : `"oauth2AllowImplicitFlow": true,`   

            3. Sélectionnez **Enregistrer**.  


### <a name="configure-email-approval"></a>Configurer l’approbation par e-mail

1. Dans la console Configuration Manager, [déployez une application](/sccm/apps/deploy-use/deploy-applications) accessible à un regroupement d’utilisateurs. Dans la page **Paramètres de déploiement**, activez-la pour approbation. Entrez ensuite la ou les adresses e-mail qui doivent recevoir une notification. Séparez les adresses e-mail par un point-virgule (`;`).  

     > [!Note]  
     > Toute personne de votre organisation Azure AD qui reçoit l’e-mail peut approuver la demande. Ne transférez pas l’e-mail à d’autres utilisateurs à moins que vous ne souhaitiez qu’ils effectuent une action.  

2. En tant qu’utilisateur, demandez l’application dans le Centre logiciel.  

3. Vous recevez une notification par e-mail dans les cinq minutes. Le contenu de l’e-mail est similaire à l’exemple suivant :  

![Exemple de notification par e-mail pour une approbation de l’application](media/1321550-email.png)

> [!Note]  
> Le lien d’approbation ou de refus ne peut être utilisé qu’une seule fois. Par exemple, vous configurez un alias de groupe pour recevoir des notifications. Isabelle approuve la demande. Dans ce cas, Laurent ne peut pas refuser la demande.  

Examinez le fichier **NotiCtrl.log** sur le serveur de site pour des besoins de dépannage.


## <a name="maintenance"></a>Maintenance 

Configuration Manager stocke des informations sur la demande d’approbation d’application dans la base de données du site. Les demandes annulées ou refusées sont supprimées de l’historique du site après 30 jours. Vous pouvez configurer ce comportement de suppression à l’aide de la [tâche de maintenance de site](/sccm/core/servers/manage/maintenance-tasks) **Supprimer les anciennes données de demande d’application**. Le site ne supprime jamais les demandes d’application approuvées ou en attente.

