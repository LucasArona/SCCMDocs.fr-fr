---
title: Comment créer des éléments de configuration pour les appareils Android for Work gérés via Microsoft Intune
titleSuffix: Configuration Manager
ms.date: 2017-07-31
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: ab6784fd-8c57-4be9-858f-50fe39f2ff5f
author: aczechowski
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 15e0c2ad91e512551e55d507d6a84bde3e46396f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56127403"
---
# <a name="how-to-create-configuration-items-for-android-for-work-devices-managed-with-intune"></a>Comment créer des éléments de configuration pour les appareils Android for Work gérés via Microsoft Intune

 Utilisez l’élément de configuration **Android for Work** de System Center Configuration Manager pour gérer les paramètres des appareils Android for Work qui sont inscrits dans Microsoft Intune ou gérés localement par Configuration Manager.  

### <a name="to-create-an-android-for-work-configuration-item"></a>Pour créer un élément de configuration Android for Work  

1. Dans la console Configuration Manager, cliquez sur **Ressources et conformité**.  

2. Dans l'espace de travail **Biens et conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Éléments de configuration**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  

4. Dans la page **Général** de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et une description éventuelle pour l’élément de configuration.  

5. Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Android for Work**.  

6. Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  

   Cliquez sur **Suivant**.

7. Dans la page **Paramètres de périphérique** de l’Assistant, sélectionnez les groupes de paramètres à configurer. Consultez [Informations de référence sur les paramètres d’élément de configuration Android for Work](#android-for-work-configuration-item-settings-reference) pour plus d’informations, puis cliquez sur **suivant**.  

   > [!TIP]  
   >  Si le paramètre souhaité n’est pas répertorié, cochez la case **Configurer d’autres paramètres qui ne se trouvent pas dans les groupes de paramètres par défaut**.  

8. Dans chaque page de paramètres, configurez les paramètres dont vous avez besoin et indiquez si vous voulez les corriger quand ils ne sont pas conformes sur des périphériques (quand cela est pris en charge).  

9. Pour chaque groupe de paramètres, vous pouvez également configurer la gravité signalée quand un élément de configuration n’est pas conforme :  

   -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  

   -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  

   -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  

   -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  

   -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme événement Windows dans le journal des événements des applications.  

10. Dans la page **Condition d’application de la plateforme** de l’Assistant, passez en revue tous les paramètres qui ne sont pas compatibles avec les plateformes prises en charge que vous avez sélectionnées précédemment. Vous pouvez revenir sur ces paramètres et les supprimer, ou vous pouvez continuer.  

    > [!TIP]  
    >  La conformité des paramètres non pris en charge n’est pas évaluée.  

11. Effectuez toutes les étapes de l'Assistant.  

    Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité**.  

##  <a name="android-for-work-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration Android for Work  

### <a name="password"></a>Mot de passe  

|Paramètre|Détails|  
|-------------|-------------|  
|**Exiger des paramètres de mot de passe sur les appareils**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant qu'un mot de passe ne doive être modifié.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe utilisés récemment.|  
|**Nombre d'échecs de tentative de connexion avant que l'appareil soit réinitialisé**|Réinitialise l'appareil si le nombre d'échecs de tentative de est atteint.|  
|**Durée d’inactivité avant le verrouillage de l’appareil**|Sélectionnez la durée d’inutilisation de l’appareil au terme de laquelle il est verrouillé.|
|**Qualité du mot de passe**|Sélectionnez le niveau de complexité du mot de passe requis et spécifiez si les appareils biométriques peuvent être utilisés.|  
|**Autoriser Smart Lock et d’autres agents de confiance**|Vous permet de contrôler la fonctionnalité Smart Lock sur les appareils Android compatibles. Cette fonctionnalité du téléphone, parfois appelée agents de confiance, vous permet de désactiver ou de contourner le mot de passe de l’écran de verrouillage de l’appareil si celui-ci se trouve dans un emplacement approuvé, comme quand il est connecté à un appareil Bluetooth spécifique, ou quand il se trouve à proximité d’une balise NFC. Vous pouvez utiliser ce paramètre pour empêcher les utilisateurs finaux de configurer Smart Lock.|
|**Empreinte digitale pour le déverrouillage**|&nbsp;|

###  <a name="work-profile"></a>Profil professionnel  
 Ces paramètres s’appliquent uniquement aux périphériques Samsung KNOX.  

|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Autoriser le partage de données entre les profils personnels et professionnels**|Choisissez parmi :<br>- **Non configuré**<br>- **Restrictions du partage par défaut**<br>- **Les applications dans le profil professionnel peuvent traiter la demande du profil personnel**<br>- **Les applications dans le profil personnel peuvent traiter la demande du profil professionnel**<br><br>(Voir aussi la définition des [paramètres copier-coller](#copy-paste-configuration-item-settings) au moyen d’un URI personnalisé)|  
|**Masquer les notifications de profil professionnel lorsque l’appareil est verrouillé (Android 6.0+)**||
|**Configurer la stratégie d’autorisation d’application par défaut (Android 6.0+)**|Choisissez parmi :<br>- **Non configuré**<br>- **Toujours demander**<br>- **Accorder automatiquement**<br>- **Refuser automatiquement**|

### <a name="copy-paste-configuration-item-settings"></a>Paramètres des éléments de configuration des opérations copier-coller
Aucune des options **Autoriser le partage de données entre les profils professionnel et personnel** n’empêche le comportement copier-coller. Utilisez un paramètre personnalisé qui peut être configuré pour empêcher le copier-coller. Vous pouvez le définir via une URI personnalisée.

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Type de valeur : Booléen

Le paramètre DisallowCrossProfileCopyPaste réglé sur true empêche le comportement de copier-coller entre le profil personnel et le profil de travail Android for Work.

## <a name="see-also"></a>Voir aussi  
 [Éléments de configuration pour les appareils gérés sans le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-without-the-client.md)
