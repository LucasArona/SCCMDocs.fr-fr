---
title: Utiliser Intune comme autorité MDM
titleSuffix: Configuration Manager
description: Découvrez comment passer de l’autorité MDM Configuration Manager (hybride) à la version autonome d’Intune.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/05/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: be503ec9-5324-4f7c-bcf5-77204328e99c
ms.openlocfilehash: d5efcb78ad5e732691cc2f214f81db0b357e0e19
ms.sourcegitcommit: 316899b08f2ef372993909e08e069f7edfed1d33
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/07/2018
ms.locfileid: "44111108"
---
# <a name="change-your-mdm-authority-to-intune-standalone"></a>Utiliser la version autonome d’Intune comme autorité MDM

*S’applique à : System Center Configuration Manager (Current Branch)*    

Vous pouvez faire passer un client Microsoft Intune déjà configuré de la console Configuration Manager (MDM hybride) à la version autonome d’Intune. Le changement d’autorité MDM côté client avec passage à Intune est la dernière phase du processus de [migration des appareils et des utilisateurs MDM hybrides vers la version autonome d’Intune](migrate-hybridmdm-to-intunesa.md) dans la configuration cloud seul.    

> [!Important]    
> Pour changer d’autorité MDM sans avoir au préalable migré les utilisateurs MDM hybrides sur Intune, consultez la page [Changer d’autorité MDM](change-mdm-authority.md).

Cet article fournit des informations sur la procédure à suivre pour modifier un client Microsoft Intune configuré et le faire passer de la console Configuration Manager (hybride) à la version autonome d’Intune ; il suppose que vous avez déjà effectué les étapes suivantes :
- utiliser [l’outil d’importation de données d’Intune](migrate-import-data.md) pour importer des objets du Gestionnaire de configuration dans Intune ; 
- [préparer Intune à la migration des utilisateurs](migrate-prepare-intune.md) pour que les utilisateurs et leurs appareils restent gérés après la migration ;
- [changer l’autorité MDM de certains utilisateurs (autorité MDM mixte)](migrate-mixed-authority.md) afin de commencer à gérer les appareils des utilisateurs à partir du Portail Azure.


## <a name="users-and-devices-that-have-not-been-migrated"></a>Utilisateurs et appareils non encore migrés
Vous avez déjà migré de nombreux utilisateurs et testé les fonctionnalités Intune pour vérifier que tout fonctionne comme prévu. Par conséquent, vos stratégies, profils, applications, etc. ont été configurés dans Intune, et vous avez soigneusement testé les objets sur les appareils. En théorie, aucune autre configuration n’est requise pour les stratégies côté client après le changement d’autorité MDM. Toutefois, pour les utilisateurs et appareils qui n’ont pas été migrés au préalable, lisez les informations suivantes sur les conséquences du changement d’autorité MDM :    
- Une période de transition (jusqu’à huit heures) peut survenir avant que l’appareil s’enregistre et se synchronise avec le service.
- Les appareils doivent se connecter au service après le changement afin que les paramètres de la nouvelle autorité MDM (version autonome d’Intune) remplacent les paramètres existants sur l’appareil.
- Certains des paramètres de base (notamment les profils) de l’autorité MDM précédente (hybride) restent sur l’appareil pendant sept jours maximum. 
- Les appareils qui n’ont pas d’utilisateurs associés (en général, lorsque vous utilisez le Programme d’inscription des appareils iOS ou des scénarios d’inscription en bloc) ne sont pas migrés vers la nouvelle autorité MDM. Pour ces appareils, vous devez contacter le support afin d’obtenir de l’aide pour déplacer ces appareils vers la nouvelle autorité MDM.

## <a name="prerequisites"></a>Prérequis
Passez en revue les informations suivantes pour préparer le passage à l’autorité MDM :
- Vous devez disposer de Configuration Manager 1610 ou version ultérieure pour pouvoir changer d’autorité MDM.
- Assurez-vous que tous les utilisateurs actuellement gérés par la MDM hybride disposent d’une licence Intune/EMS, attribuée avant le changement d’autorité MDM. Cette licence garantit que l’utilisateur et ses appareils sont gérés par la version autonome d’Intune après le changement d’autorité MDM. Pour plus d’informations, consultez [Attribuer des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Assurez-vous que le compte d’utilisateur administrateur dispose d’une licence Intune/EMS.

## <a name="change-the-mdm-authority-to-intune"></a>Utiliser Intune comme autorité MDM
Utilisez la procédure suivante pour choisir Intune comme autorité MDM côté client.

1.  Dans la console Configuration Manager, accédez à **Administration** &gt; **Vue d’ensemble** &gt; **Services Cloud** &gt; **Abonnement Microsoft Intune**, puis supprimez votre abonnement Intune existant.
2.  Sélectionnez **Utiliser Microsoft Intune comme autorité MDM**, puis cliquez sur **Suivant**.

    ![Supprimer la boîte de dialogue de l’abonnement Microsoft Intune](media/mdm-change-delete-subscription.png)
3.  Ouvrez une session dans le locataire Intune que vous avez utilisé lorsque vous avez défini pour la première fois l’autorité MDM dans Configuration Manager.
4.  Cliquez sur **Suivant** pour terminer l'Assistant.
5.  L’autorité MDM est maintenant réinitialisée. L’abonnement Intune n’apparaît plus dans le nœud des abonnements Microsoft Intune de la console Configuration Manager.
6.  Connectez-vous au [portail Intune](https://aka.ms/IntunePortal).
7.  Dans le panneau Microsoft Intune, cliquez sur **Inscription de l’appareil**.
8.  Dans la vue d’ensemble de l’inscription d’appareil, regardez la propriété **Autorité MDM**.

  > [!Important]    
  > N’utilisez pas la console Intune classique. Vous devez vous connecter à Intune sur le Portail Azure.
7.  Vérifiez que l’autorité MDM a été remplacée par **Microsoft Intune**. 

## <a name="next-steps"></a>Étapes suivantes
Une fois le changement d’autorité MDM effectué, lisez les informations suivantes :
- Le changement d’autorité MDM ne devrait avoir aucun impact significatif sur les utilisateurs finaux. 
- Il est inutile de reconfigurer les stratégies côté client. 
- Vous pouvez modifier les stratégies côté client à partir d’Intune sur le Portail Azure après le changement d’autorité MDM.
-  Après avoir modifié l’autorité MDM, procédez comme suit pour confirmer que les nouveaux appareils sont inscrits correctement auprès de la nouvelle autorité :   
    - Inscrire un nouvel appareil
    - Assurez-vous que l’appareil qui vient d’être inscrit s’affiche sur Intune.
    - Effectuez une action, par exemple un verrouillage à distance, à partir de la console d’administration sur l’appareil. Si elle réussit, l’appareil est géré par la nouvelle autorité MDM.
- Si vous rencontrez des problèmes avec des appareils spécifiques, vous pouvez annuler l’inscription puis réinscrire ces appareils pour les connecter à la nouvelle autorité et les gérer dès que possible.
- Pour les utilisateurs et les appareils non encore migrés :
    - Vérifiez que les appareils s’affichent maintenant comme appareils gérés sur le panneau **Appareils**. Après le changement d’autorité MDM, ils doivent s’enregistrer et se synchroniser avec le service avant d’apparaître. 
    - Lorsque le service Intune détecte que l’autorité MDM d’un client a changé, il envoie un message de notification à tous les appareils inscrits pour s’enregistrer et se synchroniser avec le service (en dehors de l’enregistrement régulier planifié). Par conséquent, une fois que l’autorité MDM du client est passée de la version hybride à la version autonome d’Intune, tous les appareils sous tension et en ligne se connectent au service, reçoivent la nouvelle autorité MDM et sont dès lors gérés par la version autonome d’Intune. Il n’y a aucune interruption au niveau de la gestion et de la protection de ces appareils.
    - Les appareils hors tension ou hors ligne pendant (ou juste après) le changement d’autorité MDM se connectent et se synchronisent avec le service sous la nouvelle autorité MDM quand ils sont sous tension et en ligne.  
    - Les utilisateurs peuvent rapidement basculer vers la nouvelle autorité MDM en lançant manuellement un enregistrement de l’appareil vers le service. Les utilisateurs peuvent facilement effectuer l’enregistrement avec l’application du Portail d’entreprise, en lançant une vérification de conformité de l’appareil.
    - Il existe une période temporaire pendant laquelle un appareil est hors ligne lors du changement d’autorité MDM et lorsque cet appareil s’enregistre auprès du service. Pour que l’appareil reste protégé et opérationnel pendant cet intervalle, les profils suivants restent dessus pendant sept jours maximum (ou jusqu’à ce que l’appareil se connecte à la nouvelle autorité MDM et reçoive les nouveaux paramètres qui remplacent les paramètres existants) :
        - Profil de messagerie
        - Profil VPN
        - Profil de certificat
        - Profil Wi-Fi
        - Profils de configuration
    - Appelez le support pour changer l’autorité MDM des appareils qui ne sont pas associés à un utilisateur. 
