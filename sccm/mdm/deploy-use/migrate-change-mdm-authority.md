---
title: Utiliser Intune comme autorité MDM
titleSuffix: Configuration Manager
description: Découvrez comment passer de l’autorité MDM Configuration Manager (hybride) à la version autonome d’Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 02/27/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9d6a909be4b1817b9a251046d666839e2e351443
ms.sourcegitcommit: 0bf253085adeca0d9ea62d76497eb5ebf5ce89da
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/28/2019
ms.locfileid: "57012426"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Utiliser la version autonome d’Intune comme autorité MDM

*S’applique à : System Center Configuration Manager (Current Branch)*    

Vous pouvez faire passer un client Microsoft Intune déjà configuré de la console Configuration Manager (MDM hybride) à la version autonome d’Intune. Le changement d’autorité MDM côté client avec passage à Intune est la dernière phase du processus de [migration des appareils et des utilisateurs MDM hybrides vers la version autonome d’Intune](migrate-hybridmdm-to-intunesa.md) dans la configuration cloud seul.    

> [!Important]    
> Pour changer d’autorité MDM sans avoir au préalable migré les utilisateurs MDM hybrides sur Intune, consultez la page [Changer d’autorité MDM](change-mdm-authority.md).

Cet article fournit des informations sur la modification d’un locataire Microsoft Intune existant configuré à partir de la console Configuration Manager (hybride) à la version autonome d’Intune. Il part du principe que vous avez déjà effectué les étapes suivantes :
- utiliser [l’outil d’importation de données d’Intune](migrate-import-data.md) pour importer des objets du Gestionnaire de configuration dans Intune ; 
- [Préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md) pour garantir que les utilisateurs et leurs appareils restent gérés après la migration.
- [changer l’autorité MDM de certains utilisateurs (autorité MDM mixte)](migrate-mixed-authority.md) afin de commencer à gérer les appareils des utilisateurs à partir du Portail Azure.


## <a name="users-and-devices-that-havent-been-migrated"></a>Utilisateurs et appareils qui n’ont pas été migrés.
Vous avez déjà migré de nombreux utilisateurs et testé les fonctionnalités Intune pour vérifier que tout fonctionne comme prévu. Vous avez configuré des stratégies, des profils et des applications dans Intune, et vous avez soigneusement testé les objets sur les appareils. En théorie, aucune autre configuration n’est requise pour les stratégies côté client après le changement d’autorité MDM. Toutefois, pour les utilisateurs et appareils que vous n’avez pas précédemment migrés, passez en revue les informations suivantes sur ce qui se passe après le changement d’autorité de gestion des appareils mobiles :    

- Il est probablement un temps de transition de huit heures avant de l’appareil s’enregistre et se synchronise avec le service.  

- Les appareils doivent se connecter au service après le changement afin que les paramètres de la nouvelle autorité MDM (version autonome d’Intune) remplacent les paramètres existants sur l’appareil.  

- Certains des paramètres de base (notamment les profils) de l’autorité MDM précédente (hybride) restent sur l’appareil pendant sept jours maximum.  

- Les appareils qui ne sont associés à aucun utilisateur ne sont pas migrés vers la nouvelle autorité MDM. Ces périphériques sont généralement avec des scénarios pour le programme d’inscription d’appareil iOS ou de l’inscription en bloc. Pour ces appareils, vous devez contacter le support afin d’obtenir de l’aide pour déplacer ces appareils vers la nouvelle autorité MDM.



## <a name="prerequisites"></a>Prérequis
Passez en revue les informations suivantes pour préparer le passage à l’autorité MDM :
- Vous devez disposer de Configuration Manager 1610 ou version ultérieure pour pouvoir changer d’autorité MDM.
- Veillez à affecter une licence Intune/EMS à tous les utilisateurs actuellement gérés par des appareils mobiles hybride La licence permet de s’assurer que l’utilisateur et leurs appareils sont gérés par Intune autonome après le changement d’autorité de gestion des appareils mobiles. Pour plus d’informations, consultez [Attribuer des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Assurez-vous que le compte d’utilisateur administrateur dispose d’une licence Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Utiliser Intune comme autorité MDM
Utilisez la procédure suivante pour choisir Intune comme autorité MDM côté client.

1. Dans la console Configuration Manager, accédez à la **Administration** espace de travail, développez **Services Cloud**, puis sélectionnez le **abonnement Microsoft Intune** nœud. Supprimez votre abonnement Intune existant.  

2. Sélectionnez **comme autorité MDM Microsoft Intune**, puis sélectionnez **suivant**.

    ![Supprimer la boîte de dialogue de l’abonnement Microsoft Intune](media/mdm-change-delete-subscription.png)  

3. Ouvrez une session dans le locataire Intune que vous avez utilisé lorsque vous avez défini pour la première fois l’autorité MDM dans Configuration Manager. Sélectionnez **suivant** et terminez l’Assistant.

    L’autorité MDM est maintenant réinitialisée. L’abonnement Intune n’apparaît plus dans le nœud des abonnements Microsoft Intune de la console Configuration Manager.  

4. Se connecter à la [portail Intune](https://aka.ms/IntunePortal).

5. Sélectionnez **l’inscription d’appareils**.  

6. Dans la vue d’ensemble du inscription d’appareil, consultez le **autorité MDM** propriété.

   > [!Important]    
   > N’utilisez pas la console classique Intune. Connectez-vous à Intune dans le portail Azure.  

7. Vérifiez que l’autorité MDM a été remplacée par **Microsoft Intune**. 



## <a name="after-migration"></a>Après la migration

Une fois le changement d’autorité MDM effectué, lisez les informations suivantes :

- Le changement d’autorité MDM ne devrait avoir aucun impact significatif sur les utilisateurs finaux.  

- Vous n’êtes pas obligé de reconfigurer les stratégies au niveau du locataire.  

- Si vous avez besoin modifier les stratégies au niveau du locataire, effectuez cette action à partir d’Intune dans le portail Azure.  

- Si vous rencontrez des problèmes avec un appareil, vous pouvez le désinscrire, puis le réinscrire. Cette action Obtient les connecté à la nouvelle autorité et géré aussi rapidement que possible.


#### <a name="validate-new-device-enrollment"></a>Valider la nouvelle inscription d’appareil
Après avoir modifié l’autorité de gestion des appareils mobiles, procédez comme suit pour valider que les nouveaux appareils sont inscrits correctement auprès de la nouvelle autorité :   
1. Inscrire un nouvel appareil
2. Assurez-vous que l’appareil qui vient d’être inscrit s’affiche dans Intune
3. Démarrez une action d’appareil à partir du portail Intune, tel que [verrouillage à distance](https://docs.microsoft.com/intune/device-remote-lock). Si elle réussit, l’appareil est correctement géré par la nouvelle autorité MDM.


#### <a name="for-users-and-devices-that-you-havent-previously-migrated"></a>Pour les utilisateurs et appareils que vous n’avez pas précédemment migrés.

- Vérifiez que les appareils sont désormais affichés dans le **appareils** page en tant qu’appareils gérés. Avant qu’ils sont affichés, ces appareils doivent archiver et se synchroniser avec le service après le changement d’autorité MDM. 

- Lorsque le service Intune détecte que l’autorité de gestion des appareils mobiles d’un locataire a changé, il envoie un message de notification à tous les appareils inscrits. Il demande à des appareils à archiver et se synchroniser avec le service. Cette notification se produit en dehors de l’archivage régulièrement planifiée. Après avoir modifié l’autorité MDM du locataire de hybride vers Intune autonome, tous les appareils en ligne se connectent au service. Ils reçoivent la nouvelle autorité MDM et puis sont gérés par Intune autonome par la suite. Il n’existe aucune interruption de la gestion et la protection de ces appareils.

- Pour les appareils qui sont hors connexion pendant ou juste après le changement d’autorité de gestion des appareils mobiles, elles se connectent à et se synchroniser avec le service sous la nouvelle autorité MDM quand ils sont sous tension et en ligne.  

- Vous pouvez rapidement modifier pour la nouvelle autorité MDM en lançant manuellement un archivage à partir de l’appareil vers le service. Utilisez l’application portail d’entreprise pour démarrer une vérification de conformité.

- Il existe une période temporaire pendant laquelle un appareil est hors connexion pendant la modification dans l’autorité MDM et lorsque cet appareil s’enregistre auprès du service. Pour vous assurer que l’appareil reste protégé et opérationnel pendant cet intervalle, les profils suivants restent sur l’appareil pendant sept jours. Ils peuvent également rester jusqu'à ce que l’appareil se connecte à la nouvelle autorité MDM et reçoive les nouveaux paramètres qui remplaceront les existant :
    - Profil de messagerie
    - Profil VPN
    - Profil de certificat
    - Profil Wi-Fi
    - Profils de configuration

- Pour les appareils qui ne sont pas associés à un utilisateur, appelez le support pour vous aider à changer l’autorité de gestion des appareils mobiles. 

#### <a name="bkmk-ki-dep"></a> Enregistrements d’appareils Apple DEP
<!--ICM 105091970--> Après avoir effectué la migration de MDM hybride, vous pouvez remarquer appareil PED Apple sont conservés dans la console Configuration Manager. Une fois que vous modifiez l’autorité de gestion des appareils mobiles à Intune, vous ne pouvez pas supprimer ces appareils à partir du Gestionnaire de Configuration. 

Il existe deux solutions de contournement :

- Si vous voyez ce comportement avant de changer l’autorité de gestion des appareils mobiles, puis supprimer les enregistrements de la fonctionnalité de Configuration Manager.  

- Si vous avez déjà effectué la migration et sont toujours à l’aide de Configuration Manager, utilisez la commande SQL suivante sur la base de données de site pour supprimer les enregistrements :  

    ```SQL
    Delete from MDMCorpOwnedDevices where DeviceType=8 and DiscoverySources=4
    ```



## <a name="next-steps"></a>Étapes suivantes

Maintenant que votre migration est terminée, gérer vos appareils mobiles avec Intune. Pour plus d’informations, consultez [quelles sont les nouveautés dans Microsoft Intune](https://docs.microsoft.com/intune/whats-new).

