---
title: Sécurité et confidentialité pour le contrôle à distance
titleSuffix: Configuration Manager
description: Obtenez des informations de sécurité et de confidentialité pour le contrôle à distance dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 272ee86b-d3d9-4fd9-b5c4-73e490e1a1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fc49a74fe4e257acceaea54d7c423709998a87bd
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334179"
---
# <a name="security-and-privacy-for-remote-control-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour le contrôle à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations de sécurité et de confidentialité pour le contrôle à distance dans System Center 2012 Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Meilleures pratiques de sécurité pour le contrôle à distance  
 Utilisez les meilleures pratiques de sécurité suivantes lorsque vous gérez des ordinateurs client à l'aide du contrôle à distance.  

|Bonnes pratiques de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Quand vous vous connectez à un ordinateur distant, ne continuez pas si l’authentification NTLM est utilisée au lieu de l’authentification Kerberos.|Quand Configuration Manager détecte que la session de contrôle à distance est authentifiée à l’aide de NTLM plutôt que Kerberos, une invite apparaît pour vous avertir que l’identité de l’ordinateur distant ne peut pas être vérifiée. Ne poursuivez pas la session de contrôle à distance. L'authentification NTLM est un protocole d'authentification plus faible que Kerberos et elle est vulnérable à la relecture et à l'emprunt d'identité.|  
|N’activez pas le partage du Presse-papiers dans l’observateur de contrôle à distance.|Le Presse-papiers prend en charge des objets tels que des fichiers exécutables ou du texte et il peut être utilisé par l’utilisateur sur l’ordinateur hôte pendant la session de contrôle à distance pour exécuter un programme sur l’ordinateur d’origine.|  
|N’entrez pas de mots de passe pour les comptes privilégiés en cas d’administration à distance d’un ordinateur.|Des logiciels qui observent les saisies clavier peuvent intercepter le mot de passe. Ou bien, si le programme en cours d’exécution sur l’ordinateur client n’est pas celui auquel l’utilisateur du contrôle à distance pense, ce programme peut être en train de capturer le mot de passe. Lorsque des comptes et des mots de passe sont demandés, ils doivent être saisis par l'utilisateur final.|  
|Verrouillez le clavier et la souris pendant une session de contrôle à distance.|Si Configuration Manager détecte que la connexion de contrôle à distance est terminée, Configuration Manager verrouille automatiquement le clavier et la souris afin qu’aucun utilisateur ne puisse prendre le contrôle de la session de contrôle à distance ouverte. Toutefois, cette détection peut ne pas se produire immédiatement et ne se produit pas si le service de contrôle à distance est terminé.<br /><br /> Sélectionnez l'action **Verrouiller le clavier distant et la souris** dans la fenêtre **Contrôle à distance ConfigMgr** .|  
|N’autorisez pas les utilisateurs à configurer les paramètres de contrôle à distance dans le Centre logiciel.|N'activez pas le paramètre client **Les utilisateurs peuvent modifier les paramètres de stratégie ou de notification dans le Centre logiciel** pour empêcher l'espionnage des utilisateurs.<br /><br /> Ce paramètre est destiné à l’ordinateur et non à l’utilisateur connecté.|  
|Activez le profil de pare-feu Windows **Domaine** .|Activez le paramètre client **Activer le contrôle à distance sur les profils d'exception de pare-feu clients** , puis sélectionnez le pare-feu Windows **Domaine** pour les ordinateurs de l'intranet.|  
|Si vous fermez une session pendant un contrôle à distance et vous connectez en tant qu’utilisateur différent, assurez-vous de fermer la session avant de déconnecter la session de contrôle à distance.|Si vous ne fermez pas la session selon ce scénario, la session reste ouverte.|  
|N’accordez pas aux utilisateurs des droits d’administrateur local.|Lorsque vous accordez aux utilisateurs des droits d'administrateur local, ils peuvent reprendre votre session de contrôle à distance ou compromettre vos informations d'identification.|  
|Utilisez une stratégie de groupe ou Configuration Manager pour configurer les paramètres d’assistance à distance, mais pas les deux.|Vous pouvez utiliser Configuration Manager et une stratégie de groupe pour modifier la configuration des paramètres d’assistance à distance. Quand la stratégie de groupe est actualisée sur le client, par défaut, le processus est optimisé en modifiant uniquement les stratégies qui ont été modifiées sur le serveur. Configuration Manager modifie les paramètres de la stratégie de sécurité locale, qui ne peuvent pas être remplacés, sauf si la mise à jour de la stratégie de groupe est imposée.<br /><br /> Définir la stratégie aux deux emplacements peut provoquer des incohérences. Choisissez l'une des méthodes ci-dessous pour configurer vos paramètres d'assistance à distance.|  
|Activez le paramètre client **Inviter l’utilisateur à autoriser le contrôle à distance**.|Bien qu'il soit possible de contourner ce paramètre client qui invite un utilisateur à confirmer une session de contrôle à distance, activez ce paramètre afin de réduire le risque d'espionnage des utilisateurs lorsqu'ils travaillent sur des tâches confidentielles.<br /><br /> En outre, apprenez aux utilisateurs à vérifier le nom du compte qui est affiché pendant la session de contrôle à distance et à fermer la session s'ils pensent que le compte n'est pas autorisé.|  
|Limitez la liste des observateurs autorisés.|Des droits d'administrateur local ne sont pas nécessaires à l'utilisation du contrôle à distance par un utilisateur.|  

### <a name="security-issues-for-remote-control"></a>Problèmes de sécurité pour le contrôle à distance  
 La gestion d'ordinateurs client à l'aide du contrôle à distance présente les problèmes de sécurité suivants :  

-   Ne considérez pas les messages d’audit de contrôle à distance comme fiables.  

     Si vous démarrez une session de contrôle à distance et vous vous connectez ensuite à l’aide d’autres informations d’identification, c’est le compte d’origine qui envoie les messages d’audit et non le compte qui a utilisé les autres informations d’identification.  

     Les messages d’audit ne sont pas envoyés si vous copiez les fichiers binaires pour le contrôle à distance au lieu d’installer la console Configuration Manager, puis exécutez le contrôle à distance à partir de l’invite de commandes.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informations de confidentialité pour le contrôle à distance  
 Le contrôle à distance vous permet d’afficher les sessions actives sur les ordinateurs clients Configuration Manager et de consulter éventuellement des informations stockées sur ces ordinateurs. Par défaut, le contrôle à distance n’est pas activé.  

 Bien que vous puissiez le configurer pour envoyer des avis importants et obtenir le consentement d'un utilisateur avant le début d'une session de contrôle à distance, il peut également surveiller les utilisateurs sans qu'ils le veuillent ou le sachent. Vous pouvez configurer le niveau d'accès Afficher uniquement, de sorte que rien ne puisse être modifié sur le contrôle à distance ou le contrôle intégral. Le compte de l'administrateur de connexion s'affiche dans la session de contrôle à distance pour aider les utilisateurs à savoir qui se connecte à leur ordinateur.  

 Par défaut, Configuration Manager accorde au groupe Administrateurs local des autorisations de contrôle à distance.  

 Avant de configurer le contrôle à distance, analysez vos besoins en matière de confidentialité.  
