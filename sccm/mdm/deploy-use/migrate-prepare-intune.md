---
title: Préparer Intune à la migration des utilisateurs
titleSuffix: Configuration Manager
description: Apprenez à préparer Intune sur Azure à la migration des utilisateurs à partir de la gestion hybride des appareils mobiles.
author: aczechowski
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: db97ae9e-34f4-4e10-a282-cd211f612bb4
ms.openlocfilehash: a2636713f8c121eecd826eeba060f8e3f8e865f3
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353162"
---
# <a name="prepare-intune-for-user-migration"></a>Préparer Intune à la migration des utilisateurs 

*S’applique à : System Center Configuration Manager (Current Branch)*    

Avant de migrer des utilisateurs de la gestion hybride des appareils mobiles (MDM) (Intune intégré à Configuration Manager) vers la version autonome d’Intune, vous devez préparer Intune. Les étapes de préparation vous permettent de veiller à ce que vos utilisateurs migrés et leurs appareils continuent d’être gérés. Ces étapes et le démarrage de la migration vers Intune doivent être transparents pour vos utilisateurs.  

## <a name="fix-issues-found-during-data-collection-and-import"></a>Résoudre les problèmes détectés pendant la collecte et l’importation de données
Si vous avez terminé le processus d’[importation des données Configuration Manager dans Microsoft Intune](migrate-import-data.md), l’outil d’importation de données Intune vous a fourni un résumé de tous les objets qu’il n’a pas réussi à importer. Certains problèmes classiques que vous avez probablement rencontrés, ainsi que les étapes à suivre pour les résoudre dans Intune, sont répertoriés dans le tableau suivant : 

|Problème  |Correction  |
|---------|---------|
|Les regroupements basés sur les membres directs ou sur un type complexe ne migrent pas automatiquement.|Vous devez créer des groupes Azure Active Directory (AAD) dans Azure pour remplacer le regroupement qui n’a pas été importé. Ensuite, vous devez attribuer l’objet au groupe.|
|Stratégies non importables |Vous devez recréer la stratégie dans Intune.|
|Déploiement d’un objet non importé|Vous devez attribuer l’objet au groupe. Le groupe doit contenir les mêmes utilisateurs que ceux du regroupement pour le déploiement.|

## <a name="create-intune-objects"></a>Créer des objets Intune 
Si vous avez terminé le processus d’[importation des données Configuration Manager dans Microsoft Intune](migrate-import-data.md) et résolu les problèmes pendant le processus d’importation, vous devez vérifier que les objets importés sont correctement configurés. Créez également les objets supplémentaires (stratégies, profils, applications, etc.) dans Intune dont vous avez besoin dans votre organisation. 

## <a name="assign-intune-licenses-to-migrated-users"></a>Attribuer des licences Intune aux utilisateurs qui ont migré
Dans Configuration Manager, ajoutez un regroupement à l’abonnement Intune dont les membres ont la possibilité d’inscrire leurs appareils. Alors qu’une licence Intune est réservée aux appareils inscrits, cette licence n’est pas spécifiquement associée à l’utilisateur ou à l’appareil. Par exemple, vous ne trouverez pas une licence Intune dans AAD pour un utilisateur qui dispose d’un appareil inscrit. Toutefois, dans la version autonome d’Intune, vous devez configurer une licence Intune pour chaque utilisateur. Vous devez le faire AVANT de migrer un utilisateur vers la version autonome d’Intune pour veiller à ce que l’utilisateur et ses appareils soient gérés par Intune après le changement d’autorité MDM. Pour plus d’informations, consultez [Attribuer des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/licenses-assign). 

## <a name="verify-intune-user-groups"></a>Vérifier les groupes d’utilisateurs Intune
Vos utilisateurs et groupes sont probablement déjà dans AAD, car vous avez configuré la synchronisation d’annuaires. Pour vous assurer que vos utilisateurs font partie du groupe approprié, nous vous recommandons de passer en revue vos groupes d’utilisateurs Intune. Vous ciblez des stratégies, profils, applications, etc. sur ces groupes. Assurez-vous que les utilisateurs que vous migrez vers la version autonome d’Intune font partie des groupes appropriés. 

## <a name="configure-role-based-administration-control-rbac"></a>Configurer le contrôle de l’administration basée sur des rôles
Dans le cadre de la migration, configurez tous les rôles de contrôle de l’administration basée sur des rôles nécessaires dans Intune et affectez des utilisateurs à ces rôles. Notez qu’il existe des différences entre le contrôle de l’administration basée sur des rôles dans Configuration Manager et Intune, comme l’étendue des ressources. Pour plus d’informations, consultez [Contrôle de l’administration basée sur des rôles avec Intune](https://docs.microsoft.com/intune/role-based-access-control).

## <a name="assign-apps-and-policies-to-aad-groups"></a>Affecter des stratégies et applications aux groupes AAD
Si vous avez terminé la phase d’[importation des données Configuration Manager dans Microsoft Intune](migrate-import-data.md) du processus de migration pour migrer différents objets Configuration Manager vers Intune, un grand nombre de vos objets est peut-être déjà affecté aux groupes AAD. Toutefois, vous devez vérifier que tous les objets (applications, stratégies, profils, etc.) sont affectés aux bons groupes AAD. Si vous affectez correctement les objets, les appareils de l’utilisateur sont automatiquement configurés une fois que l’utilisateur a migré, laquelle migration doit être transparente pour lui. Pour plus d’informations sur l’affectation des objets à un groupe AAD, consultez : 
- [Affecter des stratégies](https://docs.microsoft.com/intune/get-started-policies) 
- [Affecter des profils](https://docs.microsoft.com/intune/device-profile-assign) 
- [Affecter des applications](https://docs.microsoft.com/intune/get-started-apps) 

## <a name="terms-and-conditions-policy"></a>Stratégie de conditions générales
Tout comme les autres stratégies au niveau du locataire, les stratégies de conditions générales migrent automatiquement vers Intune une fois que l’autorité mixte est activée pour votre locataire.  Toutefois, vous devez affecter les conditions générales à un groupe qui contient des utilisateurs qui ont migré pour qu’elles soient clairement signalées comme acceptées par ces utilisateurs et correctement ciblées en vue des futures mises à jour ou inscriptions d’appareils. Les utilisateurs n’ont pas à réaccepter les conditions générales sauf en cas de modifications apportées à la stratégie dans la console Configuration Manager. Pour plus d’informations, consultez [Affecter des conditions générales](https://docs.microsoft.com/intune/terms-and-conditions-create#assign-terms-and-conditions).

## <a name="configure-the-exchange-connector"></a>Configurer le connecteur Exchange
Si vous utilisez Exchange et que vous disposez d’un connecteur Exchange local dans Configuration Manager, vous devez [configurer le connecteur Exchange local dans Intune](https://docs.microsoft.com/intune/exchange-connector-install). Prenez également en compte les informations dans les sections suivantes qui ont pour but de vous aider à migrer vers le connecteur Intune Exchange et à s’assurer du bon fonctionnement de l’accès conditionnel après la migration.

### <a name="powershell-scripts-to-help-you-migrate-to-the-intune-exchange-connector"></a>Scripts PowerShell pour vous aider à migrer vers le connecteur Intune Exchange 
Des scripts PowerShell sont disponibles pour vous aider à préparer la transition de vos appareils Exchange depuis le connecteur Configuration Manager Exchange vers le connecteur Intune Exchange. Bien que l’exécution de ces scripts soit facultative, nous vous recommandons de les exécuter pour supprimer les appareils inactifs d’Exchange, ce qui empêche Intune de découvrir des appareils inutiles. L’exécution des scripts permet de s’assurer que les appareils découverts via Exchange peuvent être fusionnés avec les appareils inscrits auprès d’Intune aussi simplement que possible. Exécutez ces scripts avant de configurer le connecteur Intune Exchange. Les scripts PowerShell font partie de l’installation d’Intune Data Importer que vous utilisez pour [importer les données Configuration Manager dans Microsoft Intune](migrate-import-data.md) dans l’article suivant. Pour plus d’informations et pour télécharger les scripts, accédez à la page GitHub [Microsoft Intune Data Importer](https://github.com/ConfigMgrTools/Intune-Data-Importer).

### <a name="steps-to-ensure-conditional-access-works-properly-after-user-migration"></a>Procédure permettant de s’assurer que l’accès conditionnel fonctionne correctement après la migration des utilisateurs
Pour que l’accès conditionnel fonctionne correctement après la migration des utilisateurs et pour vous assurer que vos utilisateurs continuent d’avoir accès à leur serveur e-mail, vérifiez que les conditions suivantes sont vraies :
- Si le paramètre de niveau d’accès par défaut Exchange ActiveSync (DefaultAccessLevel) a la valeur Bloquer ou Quarantaine, les appareils risquent de perdre l’accès à leurs e-mails. 
- Si le connecteur Exchange est installé dans Configuration Manager et que le paramètre **Niveau d’accès lorsqu’un périphérique mobile n’est pas géré par une règle** a la valeur **Autoriser l’accès**, vous devez installer le [connecteur Exchange sur site](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access) dans Intune avant de migrer les utilisateurs. Configurer le paramètre de niveau d’accès par défaut dans Intune dans le panneau **Exchange sur site** des **paramètres d’accès Exchange ActiveSync avancés**. Pour plus d’informations, consultez [Configurer l’accès à Exchange sur site](https://docs.microsoft.com/intune/conditional-access-exchange-create#configure-exchange-on-premises-access).
- Utilisez la même configuration pour les deux connecteurs. Le dernier connecteur que vous configurez remplace les paramètres de l’organisation ActiveSync précédemment écrits par l’autre connecteur. Si vous configurez les connecteurs différemment, vous risquez d’obtenir des modifications inattendues de l’accès conditionnel.
- Supprimez les utilisateurs du ciblage de l’accès conditionnel dans Configuration Manager une fois qu’ils ont migré vers la version autonome d’Intune.

## <a name="configure-the-microsoft-intune-certificate-connector"></a>Configurer Microsoft Intune Certificate Connector
Si vous utilisez NDES pour émettre des certificats à l’aide de SCEP, vous devez configurer Microsoft Intune Certificate Connector. L’ordinateur qui héberge le connecteur NDES dans Intune ne peut pas être le même que celui qui héberge le connecteur NDES dans Configuration Manager. Pour plus d’informations, consultez [Configurer et gérer des certificats SCEP avec Intune](https://docs.microsoft.com/en-us/intune/certificates-scep-configure). 

> [!Important]    
> Après avoir configuré le connecteur, vous devez modifier les profils SCEP importés pour faire référence à la nouvelle URL du serveur.

## <a name="next-step"></a>Étape suivante
Après avoir préparé Intune à la migration, vous êtes prêt à faire migrer un ensemble d’utilisateurs de test vers la version autonome d’Intune. Pour plus d’informations, consultez [Changer l’autorité MDM pour des utilisateurs spécifiques (autorité mixte)](migrate-mixed-authority.md).


