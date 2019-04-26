---
title: 'Gérer les appareils mobiles '
titleSuffix: Configuration Manager
description: Découvrez comment gérer des appareils mobiles à l’aide du connecteur Exchange Server dans System Center Configuration Manager.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a157e8696a9b4b24acb722be037185351f94ccdc
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62255363"
---
# <a name="manage-mobile-devices-with-system-center-configuration-manager-and-exchange"></a>Gérer des appareils mobiles à l’aide de System Center Configuration Manager et d’Exchange

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez le connecteur Exchange Server dans System Center Configuration Manager pour gérer les appareils mobiles qui se connectent à Exchange Server (en local ou en ligne) en utilisant le protocole Microsoft Exchange ActiveSync, mais que vous ne pouvez pas inscrire à l’aide de Configuration Manager. Vous pouvez configurer les fonctionnalités de gestion des appareils mobiles d’Exchange, telles que la réinitialisation à distance de l’appareil et le contrôle des paramètres de plusieurs serveurs Exchange, dans la console Configuration Manager.  

 ![configmgr&#45;avec&#45;exchange](../../mdm/deploy-use/media/configmgr-with-exchange.png "configmgr-avec-exchange")  

 Quand vous gérez des appareils mobiles à l’aide du connecteur Exchange Server, le client Configuration Manager n’est pas installé sur les appareils mobiles. Certaines fonctions de gestion sont donc limitées. Par exemple, vous ne pouvez pas installer un logiciel sur ces périphériques ou les configurer à l'aide d'éléments de configuration. Pour plus d’informations sur les différentes fonctionnalités de gestion d’appareils mobiles que vous pouvez utiliser avec Configuration Manager, consultez [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

> [!IMPORTANT]  
>  Avant d’installer le connecteur Exchange Server, vérifiez que Configuration Manager prend bien en charge la version de Microsoft Exchange que vous utilisez. Pour plus d’informations, consultez la section « Connecteur Exchange Server » dans [Systèmes d’exploitation pris en charge pour les sites et les clients pour System Center Configuration Manager](/sccm/core/plan-design/configs/supported-operating-systems-for-site-system-servers).  

 Quand vous utilisez le connecteur Exchange Server, vous pouvez gérer les appareils mobiles avec les paramètres que vous configurez dans Configuration Manager au lieu des stratégies de boîte aux lettres Exchange ActiveSync par défaut. Définir les paramètres que vous souhaitez utiliser dans les paramètres de groupe suivants : **Général**, **mot de passe**, **gestion de la messagerie**, **sécurité**, et **Application**. Par exemple, dans le paramètre du groupe **Mot de passe** , vous pouvez indiquer que les appareils mobiles requièrent un mot de passe, la longueur minimale du mot de passe, la complexité du mot de passe, et si la récupération de mot de passe est autorisée.  

 Si vous configurez au moins un paramètre dans le groupe, Configuration Manager gère tous les paramètres dans le groupe pour les appareils mobiles. Si vous ne configurez pas de paramètre dans un groupe, Exchange Server continue à gérer les appareils mobiles pour ces paramètres. Les stratégies de boîte aux lettres Exchange ActiveSync configurées sur Exchange Server et attribuées aux utilisateurs continueront à être appliquées.  

 Vous pouvez également configurer le connecteur Exchange Server pour gérer les règles d'accès Exchange et autoriser, bloquer ou mettre en quarantaine des appareils mobiles. Vous pouvez réinitialiser à distance des appareils mobiles à partir de la console Configuration Manager. Les utilisateurs peuvent le faire pour leurs appareils mobiles à partir du catalogue d’applications.  

 L’appareil mobile d’un utilisateur s’affiche automatiquement dans le catalogue d’applications s’il est géré par le connecteur Exchange Server et si Exchange Server est installé en local. Si vous configurez le connecteur Exchange Server pour Microsoft Exchange Online, vous devez configurer manuellement l’affinité entre utilisateur et appareil pour que l’appareil mobile de l’utilisateur s’affiche dans le catalogue d’applications. Pour plus d’informations sur la configuration manuelle de l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

> [!TIP]  
>  Si vous gérez un appareil mobile à l’aide du connecteur Exchange Server et que cet appareil est transféré à un autre utilisateur, supprimez l’appareil mobile de la console Configuration Manager pour permettre au nouveau propriétaire de l’appareil mobile de configurer son compte Exchange sur cet appareil mobile transféré.  

## <a name="required-security-permissions"></a>Autorisations de sécurité requises  
 Vous devez disposer des autorisations de sécurité suivantes pour configurer le connecteur Exchange Server :  

- Pour ajouter, modifier et supprimer le connecteur Exchange Server : Autorisation **Modifier** pour l’objet **Site**.  

- Pour configurer les paramètres de périphérique mobile : **ModifyConnectorPolicy** autorisation pour le **Site** objet.  

  Le rôle de sécurité **Administrateur complet** comprend les autorisations requises pour configurer le connecteur Exchange Server.  

  Vous devez disposer des autorisations de sécurité suivantes pour gérer des appareils mobiles :  

- Pour réinitialiser un appareil mobile : **Supprimer la ressource** pour l’objet **Regroupement**.  

- Pour annuler une commande de réinitialisation : **Modifier la ressource** pour l’objet **Regroupement**.  

- Pour autoriser et bloquer des appareils mobiles : **Modifier la ressource** pour l’objet **Regroupement**.  

  Le rôle de sécurité **Administrateur d'opérations** comprend les autorisations nécessaires pour la gestion des appareils mobiles à l'aide du connecteur Exchange Server.  

  Pour plus d’informations sur la configuration des autorisations de sécurité, consultez [Configurer l’administration basée sur des rôles pour System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="installing-and-configuring-an-exchange-server-connector"></a>Installation et configuration d'un connecteur Exchange Server  
 Utilisez la procédure suivante pour installer et configurer un connecteur du serveur Exchange Server afin de gérer des appareils mobiles. Configuration Manager prend en charge un seul connecteur dans une organisation Exchange. Après avoir effectué ces étapes, vous pouvez surveiller les appareils mobiles trouvés et gérés par le connecteur en consultant les regroupements contenant des appareils mobiles et les rapports les concernant.  

> [!NOTE]  
>  Configuration Manager génère des noms pour les appareils mobiles qu’il trouve, au format *Nom d’utilisateur*_*Type d’appareil*. Si un utilisateur a plusieurs appareils mobiles du même type, Configuration Manager les affiche tous sous le même nom dans la console et les rapports.  

#### <a name="to-install-and-configure-an-exchange-server-connector"></a>Pour installer et configurer un connecteur Exchange Server  

1.  Décidez quel compte se connectera au serveur d'accès au client Exchange pour gérer les appareils mobiles. Le compte peut être le compte d'ordinateur du serveur de site ou un compte d'utilisateur Windows. Configurez ensuite ce compte pour exécuter les applets de commande Exchange Server suivantes :  

    -   **Clear-ActiveSyncDevice**  

    -   **Get-ActiveSyncDevice**  

    -   **Get-ActiveSyncDeviceAccessRule**  

    -   **Get-ActiveSyncDeviceStatistics**  

    -   **Get-ActiveSyncMailboxPolicy**  

    -   **Get-ActiveSyncOrganizationSettings**  

    -   **Get-ExchangeServer**  
    
    -   **Get-Mailbox**
    
    -   **Get-Recipient**  

    -   **Set-ADServerSettings**  

    -   **Set-ActiveSyncDeviceAccessRule**  

    -   **Set-ActiveSyncMailboxPolicy**  

    -   **Set-CASMailbox**  

    -   **New-ActiveSyncDeviceAccessRule**  

    -   **New-ActiveSyncMailboxPolicy**  

    -   **Remove-ActiveSyncDevice**  
    
    -   **Get-CasMailbox**  
    
    -   **Get-User**  
    
    -   **Set-ActiveSyncOrganizationSettings**  

    > [!NOTE]  
    >  Rôles de gestion Exchange Server suivants comprennent ces applets de commande : Gestion des destinataires, gestion de l’organisation en affichage seul et gestion de serveur. Pour plus d'informations sur les groupes de rôles de gestion dans Microsoft Exchange Server 2010, consultez [Présentation des groupes de rôles de gestion](http://go.microsoft.com/fwlink/p/?LinkId=212914).  

    > [!TIP]  
    >  Si vous essayez d'installer ou d'utiliser le connecteur Exchange Server sans les applets de commande requises, une erreur est consignée dans le message `Invoking cmdlet <cmdlet> failed` dans le fichier journal EasDisc.log de l'ordinateur du serveur de site.  

2.  Dans la console Configuration Manager, cliquez sur **Administration**.  

3.  Dans l'espace de travail **Administration** , développez **Configuration de la hiérarchie**, puis cliquez sur **Connecteurs du serveur Exchange Server**.  

4.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter le serveur Exchange Server**.  

5.  Effectuez toutes les étapes de l'Assistant Ajout d'un serveur Exchange Server :  

    -   Si vous utilisez une instance locale d'Exchange Server et spécifiez un serveur d'accès au client, vous pouvez spécifier un serveur unique ou un groupe de serveurs d'accès au client pour chaque site Active Directory. Si le serveur ou groupe de serveurs est hors connexion, Configuration Manager tente de trouver un serveur d’accès au client à utiliser. S’il n’en trouve pas, Configuration Manager utilise à la place un serveur de boîtes aux lettres pour établir une connexion à un serveur d’accès au client. Les nouvelles tentatives sont enregistrées en tant qu'avertissements dans le fichier EasDisc.log sur l'ordinateur du serveur de site. Par exemple, recherchez `Failed to open runspace for site <site_name>`.  

    -   Pour le compte du connecteur Exchange Server, spécifiez le compte que vous avez configuré à l'étape 1.  

    -   Si vous inscrivez également des appareils mobiles à l’aide de Configuration Manager, activez l’option **Gestion des appareils mobiles externes** pour vous assurer que ces appareils mobiles recevront encore les e-mails d’Exchange après leur inscription par Configuration Manager.  

    -   Dans la page **Compte** de l’Assistant, vous pouvez configurer le compte utilisé pour envoyer des notifications par e-mail aux clients qui sont bloqués par l’accès conditionnel de Configuration Manager. Le compte que vous spécifiez doit avoir une boîte aux lettres valide sur le serveur Exchange.  

         Pour plus d’informations, consultez [Gérer l’accès aux services dans System Center Configuration Manager](../../protect/deploy-use/manage-access-to-services.md).  

6.  Vous pouvez vérifier l'installation du connecteur Exchange Server à l'aide de messages d'état et en passant en revue les fichiers journaux :  

    -   Pour vérifier que le Gestionnaire de composants de site a bien installé le connecteur Exchange Server, recherchez l'ID de l'état **1015** pour le composant **SMS_EXCHANGE_CONNECTOR** . Si Configuration Manager ne peut pas installer correctement le connecteur (parce que l’ordinateur du serveur d’accès au client spécifié est hors connexion, par exemple), Configuration Manager effectue une nouvelle tentative d’installation toutes les 60 minutes jusqu’à ce que l’opération réussisse ou que vous supprimiez le connecteur Exchange Server.  

    -   Sur l'ordinateur du serveur de site, recherchez le fichier SiteComp.log, puis dans le fichier journal, recherchez `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. Quand l'installation s'effectue correctement, elle est enregistrée avec le texte suivant : `STATMSG: ID=1015`.  
