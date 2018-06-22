---
title: Résoudre les problèmes liés à l’intégration de Lookout
titleSuffix: Configuration Manager
description: Cette rubrique décrit comment résoudre les problèmes qui se produisent couramment avec l’intégration de Lookout.
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: e36b98c7-d0f4-4dd6-bac3-6a6c4b4bf841
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ee978543248e70182e12a3d6234cfd12be80dc98
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32348580"
---
# <a name="troubleshoot-lookout-integration-with-intune"></a>Résoudre les problèmes liés à l’intégration de Lookout à Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

## <a name="troubleshoot-login-errors"></a>Résoudre les erreurs de connexion
### <a name="403-errors"></a>Erreurs 403
Une erreur 403 peut s’afficher quand vous vous connectez à la [console Lookout MTP](https://aad.lookout.com) : **vous n’êtes pas autorisé à accéder au service**. Cela peut arriver si le nom d’utilisateur que vous avez spécifié n’est pas membre du groupe Azure Active Directory (Azure AD) configuré pour accéder à Lookout MTP.

Lookout MTP est configuré pour autoriser uniquement l’accès aux utilisateurs d’un groupe Azure AD configuré. Si vous ne savez pas quel groupe est configuré pour accéder à Lookout MTP, contactez le support de Lookout.

Pour contacter le support de Lookout, choisissez l’une des méthodes suivantes :

* Envoyez un e-mail à enterprisesupport@lookout.com.
* Connectez-vous à la [Console MTP](http://aad.lookout.com)et accédez au module **Support**.
* Accédez à https://enterprise.support.lookout.com/hc/requests et procédez à une demande de support.

### <a name="unable-to-sign-in"></a>Connexion impossible
L’erreur suivante peut se produire si l’utilisateur administrateur général Azure AD n’accepte pas l’installation initiale de Lookout.

![capture de l’écran de connexion Lookout indiquant une erreur de connexion](media/lookout-consent-not-accepted-error.png)

Pour résoudre ce problème, l’utilisateur administrateur général doit se connecter à https://aad.lookout.com/les?action=consent et accepter l’invite de lancement de l’installation. Vous trouverez des informations plus détaillées dans la rubrique [Configurer votre abonnement avec Lookout MTP](set-up-your-subscription-with-lookout.md).

## <a name="troubleshoot-device-status-issues"></a>Résoudre les problèmes liés à l’état de l’appareil

### <a name="device-not-showing-up-in-the-lookout-mtp-console-device-list"></a>L’appareil n’apparaît pas dans la liste des appareils de la console Lookout MTP

Cela peut arriver dans l’un des scénarios suivants :
* Quand le propriétaire de cet appareil ne figure pas dans le **Enrollment Group** (Groupe d’inscriptions) spécifié dans la **Console Lookout MTP**.  À partir du module **System** (Système), accédez à l’onglet **Intune Connector** (Connecteur Intune) et examinez les paramètres **Enrollment Management** (Gestion des inscriptions).  Un ou plusieurs groupes Azure AD configurés pour l’inscription doivent être répertoriés.  Vérifiez que le propriétaire de l’appareil manquant fait partie de l’un des groupes Azure AD spécifiés.  Quand un nouvel utilisateur est ajouté au groupe d’inscriptions, l’appareil apparaît dans le module **Devices** (Appareils) de la console Lookout MTP au terme de l’intervalle d’interrogation (5 minutes par défaut).

* Si l’appareil n’est pas pris en charge par Lookout MTP.  Les appareils qui ne sont pas pris en charge sont répertoriés dans la section **Managed Devices** (Appareils gérés) des paramètres du connecteur dans la console Lookout MTP.

### <a name="device-continues-to-be-reported-as-pending"></a>L’appareil est signalé comme étant **en attente**

Si un appareil est **en attente**, cela signifie que l’utilisateur final n’a pas ouvert l’application Lookout for Work et qu’il n’a pas appuyé sur le bouton **Activate** (Activer). Pour plus d’informations sur l’activation de l’appareil à l’aide de l’application Lookout for Work, consultez la rubrique suivante :

[Vous êtes invité à installer Lookout for Work sur votre appareil Android](http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

### <a name="in-the-lookout-mtp-console-a-device-is-showing-as-active-but-does-not-have-a-device-id"></a>Dans la console Lookout MTP, un appareil apparaît comme étant actif, mais il n’est associé à aucun ID d’appareil.
Cela signifie que le propriétaire de cet appareil ne figure pas dans le groupe d’inscriptions spécifié dans la console Lookout MTP.   Un appareil peut être dans cet état si son propriétaire a été supprimé du groupe d’inscriptions ou si le groupe d’inscriptions auquel appartient l’utilisateur a été supprimé.

À partir du module **System** (Système) dans la console Lookout MTP, accédez à l’onglet **Intune Connector** (Connecteur Intune) et passez en revue les paramètres **Enrollment** (Inscription).  Un ou plusieurs groupes Azure AD configurés pour l’inscription doivent être répertoriés.  Vérifiez que le propriétaire de l’appareil fait partie de l’un des groupes Azure AD spécifiés.

Quand un appareil est dans cet état, Lookout continue à informer l’utilisateur des menaces détectées, mais les informations sur les menaces ne sont pas envoyées à Intune.

### <a name="device-shows-disconnected-state"></a>L’appareil indique un état déconnecté

Un état déconnecté signifie que Lookout MTP n’a pas reçu d’informations de l’appareil pendant un intervalle de temps préconfiguré (la valeur par défaut est de 30 jours, la valeur minimale de 7 jours). Cela signifie que l’application Portail d’entreprise ou Lookout for Work n’est pas installée sur l’appareil ou a été désinstallée. Pour résoudre ce problème, réinstallez les applications. Quand l’utilisateur ouvre Lookout for Work et active l’application, l’appareil se resynchronise avec Lookout MTP et Intune.

### <a name="forcing-a-resync-on-the-device"></a>Forcer une resynchronisation sur l’appareil
À partir du module **Devices** (Appareils) de la console Lookout MTP, l’administrateur peut sélectionner l’appareil et le supprimer.   La prochaine fois que le propriétaire de l’appareil ouvre l’application Lookout for Work et appuie sur **Activate** (Activer), l’appareil effectue une resynchronisation complète.

### <a name="the-owner-of-the-device-is-no-longer-using-this-device"></a>Le propriétaire de l’appareil n’utilise plus cet appareil
Vous devez réinitialiser l’appareil et demander au nouvel utilisateur de s’inscrire, comme indiqué dans [cette rubrique](https://docs.microsoft.com/sccm/mdm/deploy-use/wipe-lock-reset-devices#full-wipe).


Vous pouvez également accéder au module **Devices** (Appareils) de la console MTP Console et choisir **Delete** (Supprimer).

Tant que le nouvel utilisateur figure dans l’un des groupes d’inscription spécifiés dans la console Lookout MTP, l’appareil s’affiche quand Azure AD associe l’appareil au nouvel utilisateur.

## <a name="compliance-remediation-workflows"></a>Flux de travail de mise à jour de la conformité
[Vous êtes invité à installer Lookout for Work sur votre appareil Android]( http://docs.microsoft.com/intune/enduser/you-are-prompted-to-install-lookout-for-work-android)

[Vous devez résoudre une menace détectée par Lookout for Work sur votre appareil Android](http://docs.microsoft.com/intune/enduser/you-need-to-resolve-a-threat-found-by-lookout-for-work-android)
