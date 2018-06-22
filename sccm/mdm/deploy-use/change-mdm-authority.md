---
title: Changer d’autorité MDM
titleSuffix: Configuration Manager
description: Découvrez comment changer l’autorité MDM en passant de Configuration Manager (hybride) à la version autonome d’Intune
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 04/11/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.assetid: cc397ab5-125f-4f17-905b-fab980194f49
ms.openlocfilehash: e5b97ccea5bb6e52badb12f635b5bc97061ca1d1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349515"
---
# <a name="change-your-mdm-authority"></a>Changer d’autorité MDM
Vous pouvez modifier votre autorité MDM sans avoir à contacter le Support Microsoft, et sans devoir annuler l’inscription de vos appareils gérés existants et les réinscrire. Cet article décrit les étapes à suivre pour modifier un client Microsoft Intune déjà configuré et le faire passer de la console Configuration Manager (hybride) à la version autonome d’Intune. Lorsque vous effectuez les étapes décrites dans cet article, les appareils sont gérés par Microsoft Intune dans le [portail Azure](https://portal.azure.com). 

> [!Note]    
> Si vous souhaitez modifier un locataire Microsoft Intune existant, dont l’autorité MDM est définie sur Intune, pour le passer sur Configuration Manager (hybride), consultez [Changer l’autorité MDM](https://docs.microsoft.com/intune-classic/deploy-use/change-mdm-authority).

> [!Important]    
> Cet article concerne le changement d’autorité de gestion des appareils mobiles (MDM) dans le cas où aucun utilisateur n’a fait l’objet d’une migration. Pour la changer après avoir [migré un sous-ensemble d’utilisateurs](migrate-hybridmdm-to-intunesa.md), consultez la page [Changer d’autorité MDM](migrate-change-mdm-authority.md).

## <a name="key-considerations"></a>Principales considérations
Lorsque vous modifiez l’autorité MDM, la période de transition peut prendre jusqu’à 8 heures. C’est seulement après cette transition que l’appareil est synchronisé avec le service. Pour que les appareils inscrits continuent d’être gérés et protégés après la modification, configurez les paramètres directement dans Intune. Tenez compte des éléments suivants :
- Les appareils doivent se connecter au service après le changement afin que les paramètres de la nouvelle autorité MDM (version autonome d’Intune) remplacent les paramètres existants sur l’appareil.
- Après avoir changé d’autorité MDM, certains des paramètres de base (tels que les profils) de l’autorité MDM précédente (hybride) restent sur l’appareil pendant sept jours. Il est recommandé de configurer les applications et les paramètres (stratégies, profils, applications, etc.) dès que possible dans la nouvelle autorité MDM. Déployez également les paramètres sur les groupes d’utilisateurs contenant ceux qui possèdent des appareils déjà inscrits. Dès qu’un appareil se connecte au service après le changement d’autorité MDM, il reçoit les nouveaux paramètres de la nouvelle autorité MDM. Toutes les stratégies qui viennent d’être ciblées remplacent les stratégies existantes sur l’appareil.
- Après la sélection de la nouvelle autorité MDM, une semaine peut être nécessaire avant que les données de conformité s’affichent correctement dans le [portail Azure](https://portal.azure.com). Cependant, les états de conformité dans Azure Active Directory et sur l’appareil restent corrects. L’appareil est toujours protégé.
- Les appareils qui ne sont associés à aucun utilisateur ne sont pas migrés vers la nouvelle autorité MDM. Cela se produit généralement dans les scénarios impliquant des inscriptions en bloc ou le programme d’inscription des appareils iOS. Pour ces appareils, contactez le support afin d’obtenir de l’aide pour déplacer ces appareils vers la nouvelle autorité MDM.

## <a name="prepare-to-change-the-mdm-authority-to-intune-standalone"></a>Se préparer à utiliser la version autonome d’Intune comme autorité MDM
Passez en revue les informations suivantes pour préparer le passage à l’autorité MDM :
- Après le passage à la nouvelle autorité MDM, la connexion d’un appareil au service peut prendre jusqu’à huit heures.
- Assurez-vous que tous les utilisateurs actuellement gérés par un système hybride disposent d’une licence Intune/EMS qui leur a été attribuée avant le changement d’autorité MDM. Cette licence garantit que l’utilisateur et ses appareils sont gérés par la version autonome d’Intune après le changement d’autorité MDM. Pour plus d’informations, consultez [Attribuer des licences Intune à vos comptes d’utilisateur](https://docs.microsoft.com/intune/get-started/start-with-a-paid-subscription-to-microsoft-intune-step-4).
- Assurez-vous que le compte d’utilisateur administrateur dispose d’une licence Intune/EMS. Vérifiez que le compte d’utilisateur Administrateur peut se connecter à Intune avant de changer l’autorité MDM. L’autorité MDM devrait afficher **Définir sur Configuration Manager** (locataire hybride) dans Intune dans le [portail Azure](https://portal.azure.com) avant le changement d’autorité MDM.
- Le changement d’autorité MDM ne devrait avoir aucun impact significatif sur les utilisateurs finaux. 

## <a name="change-the-mdm-authority-to-intune-standalone"></a>Utiliser la version autonome d’Intune comme autorité MDM
Le processus pour utiliser la version autonome d’Intune comme autorité MDM comprend les étapes principales suivantes :  
- Dans la console Configuration Manager, utilisez l’option **Utiliser la version autonome d’Intune comme autorité MDM** pour supprimer l’abonnement Microsoft Intune existant.
- Dans Intune dans le [portail Azure](https://portal.azure.com), configurez et déployez les nouveaux réglages et les nouvelles applications à partir de la nouvelle autorité MDM (Intune).
- La prochaine fois qu’ils se connecteront au service, les appareils se synchroniseront et recevront les nouveaux paramètres à partir de la nouvelle autorité MDM.

#### <a name="to-change-the-mdm-authority-to-intune-standalone"></a>Pour utiliser la version autonome d’Intune comme autorité MDM
1. Dans la console Configuration Manager, accédez à **Administration** &gt; **Vue d’ensemble** &gt; **Services Cloud** &gt; **Abonnement Microsoft Intune**, puis supprimez votre abonnement Intune existant.
2. Sélectionnez **Utiliser Microsoft Intune comme autorité MDM**, puis cliquez sur **Suivant**.
   ![Assistant Suppression d’abonnement Microsoft Intune, page Introduction](./media/mdm-change-delete-subscription.png)
3. Ouvrez une session dans le locataire Intune que vous avez utilisé lorsque vous avez défini pour la première fois l’autorité MDM dans Configuration Manager.
4. Cliquez sur **Suivant** pour terminer l'Assistant.
5. L’autorité MDM a maintenant la valeur **Microsoft Intune**. L’abonnement Intune ne s’affiche pas dans le nœud des abonnements Microsoft Intune de la console Configuration Manager. 
6. Pour vérifier que l’autorité MDM est définie, effectuez les étapes suivantes : a. Connectez-vous au [portail Azure](https://portal.azure.com) avec le locataire Intune que vous avez utilisé précédemment. 
    b. Choisissez **Autres services** > **Surveillance + Gestion** > **Intune** > **Inscription de l’appareil**. L’autorité MDM s’affiche dans la section en haut à droite du panneau **Vue d’ensemble**. 

## <a name="next-steps"></a>Étapes suivantes
Une fois le changement d’autorité MDM effectué, passez en revue les étapes suivantes :
- Lorsque le service Intune détecte que l’autorité MDM d’un locataire a changé, il envoie un message de notification à tous les appareils inscrits pour qu’ils s’enregistrent et se synchronisent avec le service. Ce comportement est différent de l’enregistrement régulier planifié. Par conséquent, une fois que l’autorité MDM du client est passée de la version hybride à la version autonome d’Intune, tous les appareils sous tension et en ligne se connectent au service, reçoivent la nouvelle autorité MDM et sont gérés par la version autonome d’Intune. Il n’y a aucune interruption au niveau de la gestion et de la protection de ces appareils.
- Les appareils hors tension ou hors ligne pendant (ou juste après) le changement d’autorité MDM se connectent et se synchronisent avec le service sous la nouvelle autorité MDM quand ils sont sous tension et en ligne.  
- Les utilisateurs peuvent rapidement basculer vers la nouvelle autorité MDM en lançant manuellement un enregistrement de l’appareil vers le service. Les utilisateurs peuvent facilement effectuer cette opération à l’aide de l’application du portail d’entreprise, en lançant une vérification de conformité d’appareil.
- Pour confirmer que tout fonctionne correctement une fois les appareils enregistrés et synchronisés avec le service après le changement d’autorité MDM, recherchez les appareils dans le [portail Azure](https://portal.azure.com). Les appareils précédemment gérés par Configuration Manager (hybride) s’affichent désormais comme des appareils gérés dans Intune.    
- Il existe une période temporaire pendant laquelle un appareil est hors ligne lors du changement d’autorité MDM et lorsque cet appareil s’enregistre auprès du service. Pour que l’appareil reste protégé et opérationnel pendant cet intervalle, les profils suivants restent dessus pendant sept jours maximum (ou jusqu’à ce que l’appareil se connecte à la nouvelle autorité MDM et reçoive les nouveaux paramètres qui remplacent les paramètres existants) :
    - Profil de messagerie
    - Profil VPN
    - Profil de certificat
    - Profil Wi-Fi
    - Profils de configuration
- Pour remplacer les anciens paramètres, vérifiez que les nouveaux paramètres destinés à remplacer les paramètres existants portent le même nom que les anciens. Sinon, les appareils risquent de contenir des stratégies et des profils redondants.    

  > [!TIP]   
  > Il est recommandé de créer tous les paramètres de gestion et toutes les configurations, ainsi que les déploiements, peu de temps après le changement d’autorité MDM. Cela permet de s’assurer que les appareils sont protégés et activement gérés pendant la période temporaire.   
-  Après avoir modifié l’autorité MDM, procédez comme suit pour confirmer que les nouveaux appareils sont inscrits correctement auprès de la nouvelle autorité :   
    - Inscrire un nouvel appareil
    - Assurez-vous que l’appareil qui vient d’être inscrit s’affiche sur le [portail Azure](https://portal.azure.com).
    - Effectuez une action, par exemple un verrouillage à distance, à partir du [portail Azure](https://portal.azure.com) sur l’appareil. Si elle réussit, l’appareil est géré par la nouvelle autorité MDM.
- Si vous rencontrez des problèmes avec un appareil, vous pouvez le désinscrire, puis le réinscrire. Cette action établit une connexion avec la nouvelle autorité et est effectuée aussi rapidement que possible.
- Si vous avez activé [Android for Work](/sccm/mdm/deploy-use/create-configuration-items-for-android-for-work-devices-managed-without-the-client) en tant que locataire hybride, puis avez migré votre locataire vers une version autonome d’Intune, le paramètre Android for Work situé sous les restrictions d’inscription peut afficher Bloquer au lieu d’Autoriser. Définissez-le manuellement sur **Autoriser** pour réactiver l’inscription Android for Work.<!--512117-->