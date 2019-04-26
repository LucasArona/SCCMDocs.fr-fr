---
title: Préparer Intune à la migration des utilisateurs
titleSuffix: Configuration Manager
description: Apprenez à préparer Intune sur Azure à la migration des utilisateurs à partir de la gestion hybride des appareils mobiles.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/26/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.collection: M365-identity-device-management
ms.openlocfilehash: e217c7afc2910a23fe3f29fa215d58574f3d79d8
ms.sourcegitcommit: 4e47f63a449f5cc2d90f9d68500dfcacab1f4dac
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62237007"
---
# <a name="prepare-intune-for-user-migration"></a>Préparer Intune à la migration des utilisateurs 

*S’applique à : System Center Configuration Manager (Current Branch)*    
Avant de migrer les utilisateurs de MDM hybride vers Intune autonome, effectuez les étapes pour préparer Intune. Ces étapes permettent de s’assurer que vos utilisateurs migrés et leurs appareils continuent d’être gérés. Lorsque vous effectuez ces étapes et démarrez la migration vers Intune, il n’existe aucun impact considérable sur les utilisateurs.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Résoudre les problèmes détectés pendant la collecte et l’importation de données
Si vous avez utilisé l’outil Intune Data Importer pour [importer des données de Configuration Manager à Microsoft Intune](migrate-import-data.md), il résumées les objets qu’il n’a pas pu importer. Certains des problèmes typiques, les étapes permettant de les résoudre dans Intune, sont répertoriés dans le tableau suivant : 

|Problème  |Correctif  |
|---------|---------|
|Collections basées sur l’appartenance directe ou sur un type complexe ne sont pas migrées automatiquement.|Créer des groupes Azure Active Directory (Azure AD) dans Azure pour remplacer la collection n’a pas été importée. Ensuite, assignez l’objet au groupe.|
|Stratégies n’ont pas été importables |Recréez la stratégie dans Intune.|
|Déploiement d’un objet non importé|Attribuez l’objet au groupe. Le groupe doit inclure les mêmes utilisateurs à partir de la collection pour le déploiement.|

## <a name="create-intune-objects"></a>Créer des objets Intune 
Si vous [importé des données de Configuration Manager à Microsoft Intune](migrate-import-data.md) et résolution des problèmes au cours du processus, vérifiez les objets importés sont correctement configurés. Créez également les objets supplémentaires (stratégies, profils et applications) dans Intune dont vous avez besoin dans votre organisation. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Attribuer des licences Intune aux utilisateurs qui ont migré
Dans le Gestionnaire de Configuration, vous ajoutez une collection à l’abonnement Intune et les membres de la collection peuvent inscrire leurs appareils. Pendant une licence Intune est réservée pour les appareils inscrits, ces licences ne sont pas associées à l’utilisateur ou l’appareil. Par exemple, vous n’aurait pas rechercher une licence Intune dans Azure AD pour un utilisateur qui dispose d’un appareil inscrit. 

Dans la version autonome d’Intune, configurez une licence Intune pour chaque utilisateur. Configurez la licence *avant* vous faites migrer un utilisateur vers Intune autonome. Cette action permet de s’assurer que l’utilisateur et leurs appareils sont gérés par Intune après le changement d’autorité de gestion des appareils mobiles. Pour plus d’informations, consultez [Attribuer des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Vérifier les groupes d’utilisateurs Intune
Vos utilisateurs et groupes sont probablement déjà dans Azure AD, car vous avez configurée la synchronisation d’annuaires. Pour vous assurer que vos utilisateurs font partie du groupe approprié, nous vous recommandons de passer en revue vos groupes d’utilisateurs Intune. Vous ciblez les stratégies, profils et des applications à ces groupes. Assurez-vous que les utilisateurs que vous migrez vers la version autonome d’Intune font partie des groupes appropriés. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurer le contrôle de l’administration basée sur des rôles
Dans le cadre de la migration, configurez tous les rôles de contrôle de l’administration basée sur des rôles nécessaires dans Intune et affectez des utilisateurs à ces rôles. Il existe des différences entre RBAC dans Configuration Manager et Intune, comme l’étendue des ressources. Pour plus d’informations, consultez [contrôle d’administration en fonction du rôle (RBAC) avec Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Affecter des stratégies et applications aux groupes AAD
Si vous [importé des données de Configuration Manager à Microsoft Intune](migrate-import-data.md), de nombreux objets peuvent déjà être affectés aux groupes Azure AD. Vérifiez que tous les objets (applications, les stratégies et profils) sont affectées à la bonne groupes Azure AD. Si vous affectez correctement les objets, les appareils de l’utilisateur sont automatiquement configurés une fois que l’utilisateur est migré et la migration ne doit pas avoir n’importe quel impact considérable sur les utilisateurs. Pour plus d’informations sur l’affectation des objets à un groupe Azure AD, consultez les articles suivants : 
- [Affecter des stratégies](https://docs.microsoft.com/intune/get-started-policies)  
- [Affecter des profils](https://docs.microsoft.com/intune/device-profile-assign)  
    > [!NOTE]  
    > Quand Intune déploie le nouveau profil de messagerie, les utilisateurs reçoivent une invite à entrer à nouveau son mot de passe. Ce comportement entraîne des e-mails en cours à télécharger à nouveau sur les appareils des utilisateurs. Toutes les modifications personnalisées effectuées par l’utilisateur doit être effectuée à nouveau. 
- [Affecter des applications](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Stratégie de conditions générales
Tout comme les autres stratégies au niveau du locataire, les stratégies de conditions générales migrent automatiquement vers Intune une fois que l’autorité mixte est activée pour votre locataire.  Toutefois, vous devez affecter les termes du contrat et conditions à un groupe qui contient migré les utilisateurs pour créer des rapports sur l’acceptation des utilisateurs migrés avec précision et de vous assurer que les conditions sont correctement ciblées pour futures et les mises à jour des conditions ou périphérique inscriptions. Les utilisateurs n’ont pas à réaccepter les conditions générales sauf s’il existe des modifications apportées à la stratégie dans la console Configuration Manager. Pour plus d’informations, consultez [affecter des conditions générales](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurer le connecteur Exchange
Si vous utilisez Exchange et que vous disposez d’un connecteur Exchange local dans Configuration Manager, vous devez [configurer le connecteur Exchange local dans Intune](https://docs.microsoft.com/intune/exchange-connector-install). Tenez également compte des informations dans les sections suivantes pour vous aider à migrer vers le connecteur Exchange Intune et s’assurer que l’accès conditionnel fonctionne correctement après la migration.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts PowerShell pour vous aider à migrer vers le connecteur Intune Exchange 
Des scripts PowerShell sont disponibles pour vous aider à préparer la transition de vos appareils Exchange depuis le connecteur Configuration Manager Exchange vers le connecteur Intune Exchange. Bien que l’exécution de ces scripts soit facultative, nous vous recommandons de les exécuter pour supprimer les appareils inactifs d’Exchange, ce qui empêche Intune de découvrir des appareils inutiles. L’exécution des scripts permet de s’assurer que les appareils découverts via Exchange peuvent être fusionnés avec les appareils inscrits auprès d’Intune aussi simplement que possible. Exécutez ces scripts avant de configurer le connecteur Intune Exchange. Les scripts PowerShell font partie de l’installation d’Intune Data Importer que vous utilisez pour [importer les données Configuration Manager dans Microsoft Intune](migrate-import-data.md) dans l’article suivant. Pour plus d’informations et pour télécharger les scripts, accédez à la page GitHub [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-make-sure-conditional-access-works-properly-after-user-migration"></a>Étapes pour que l’accès conditionnel que fonctionne correctement après la migration de l’utilisateur
Pour l’accès conditionnel fonctionne correctement une fois que vous migrez des utilisateurs et pour vous assurer que vos utilisateurs continuent à accéder à leur serveur e-mail, vérifiez que les configurations suivantes sont définies :
- Si le paramètre de niveau d’accès par défaut Exchange ActiveSync (DefaultAccessLevel) a la valeur Bloquer ou Quarantaine, les appareils risquent de perdre l’accès à leurs e-mails. 
- Si le connecteur Exchange est installé dans le Gestionnaire de Configuration et le **niveau d’accès quand un appareil mobile n’est pas géré par une règle** paramètre a la valeur **autoriser l’accès**, installez le [ Connecteur Exchange sur site](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) dans Intune avant de migrer des utilisateurs. Configurer le paramètre de niveau de l’accès par défaut dans Intune sur le **Exchange sur site** page **paramètres d’accès Exchange ActiveSync avancés**. Pour plus d’informations, consultez [configurer Exchange en local accès](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilisez la même configuration pour les deux connecteurs. Le dernier connecteur que vous configurez remplace les paramètres de l’organisation ActiveSync précédemment écrits par l’autre connecteur. Si vous configurez les connecteurs différemment, vous risquez d’obtenir des modifications inattendues de l’accès conditionnel.
- Supprimez les utilisateurs du ciblage de l’accès conditionnel dans Configuration Manager une fois qu’ils ont migré vers la version autonome d’Intune.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurer Microsoft Intune Certificate Connector
Si vous utilisez NDES pour émettre des certificats à l’aide de SCEP, vous devez configurer Microsoft Intune Certificate Connector. L’ordinateur qui héberge le connecteur NDES dans Intune ne peut pas être le même ordinateur qui héberge le connecteur NDES dans Configuration Manager. Pour plus d’informations, consultez [configurer et gérer des certificats SCEP avec Intune](https://docs.microsoft.com/intune/certificates-scep-configure). 

> [!Important]    
> Après avoir configuré le connecteur, modifier des profils SCEP importés pour faire référence à la nouvelle URL du serveur.

## <a name="next-step"></a>Étape suivante
Après avoir préparé Intune pour la migration, vous êtes prêt à migrer un ensemble d’utilisateurs de test vers Intune autonome. Pour plus d’informations, consultez [changer l’autorité de gestion des appareils mobiles pour des utilisateurs spécifiques (autorité mixte)](migrate-mixed-authority.md).


