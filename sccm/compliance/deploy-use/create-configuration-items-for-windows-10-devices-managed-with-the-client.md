---
title: 'Créer des éléments de configuration pour Windows 10 géré par le client '
titleSuffix: Configuration Manager
description: Utilisez l’élément de configuration System Center Configuration Manager Windows 10 pour gérer les paramètres des ordinateurs Windows 10 gérés par le client Configuration Manager.
ms.date: 03/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bdb48689efba4c6f884d4c36c1a4dee0bbcc6b65
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-create-configuration-items-for-windows-10-devices-managed-with-the-system-center-configuration-manager-client"></a>Comment créer des éléments de configuration pour des périphériques Windows 10 gérés avec le client System Center Configuration Manager
Utilisez l’élément de configuration System Center Configuration Manager **Windows 10** pour gérer les paramètres des ordinateurs Windows 10 gérés par le client Configuration Manager.  
  
> [!IMPORTANT]  
>  Dans cette version, si vous avez créé un paramètre **Mot de passe** pour un élément de configuration de type **Windows 10** (pour un appareil géré avec le client Configuration Manager), il est évalué à tort comme étant compatible si le paramètre n’existe pas déjà ou s’il n’a pas été configuré sur l’appareil Windows 10.  
>   
>  Pour résoudre ce problème, quand vous créez un paramètre pour ces périphériques, assurez-vous de sélectionner **Résoudre les paramètres non compatibles** dans les pages de paramètres de l’Assistant Création d’élément de configuration. De plus, quand vous déployez une base de référence de configuration contenant un élément de configuration Windows 10 qui inclue des paramètres de mot de passe, sélectionnez **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** dans la boîte de dialogue Déployer des lignes de base de configuration. En utilisant cette solution de contournement, le paramètre est analysé et corrigé s’il n’est pas compatible. Après la correction, le paramètre est correctement signalé comme **Compatible** (sauf si un problème est rencontré, auquel cas une **Erreur**est signalée).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>Pour créer un élément de configuration Windows 10  
  
1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.  
  
2.  Dans l'espace de travail **Biens et conformité** , développez **Paramètres de compatibilité**, puis cliquez sur **Éléments de configuration**.  
  
3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un élément de configuration**.  
  
4.  Dans la page **Général** page de l’ **Assistant Création d’élément de configuration**, spécifiez un nom et éventuellement une description pour l’élément de configuration.  
  
5.  Sous **Spécifier le type d’élément de configuration que vous voulez créer**, sélectionnez **Windows 10**.  
  
6.  Cliquez sur **Catégories** si vous créez et attribuez des catégories pour faciliter la recherche et le filtrage des éléments de configuration dans la console Configuration Manager.  
  
7.  Dans la page **Plateformes prises en charge** de l’Assistant, sélectionnez les plateformes Windows 10 spécifiques qui évaluent l’élément de configuration.  
  
8.  Dans la page **Paramètres de périphérique** de l’Assistant, sélectionnez le groupe de paramètres à configurer. Consultez [Windows 10 configuration item settings reference](#BKMK_Ref) dans cette rubrique pour plus d’informations, puis cliquez sur **Suivant**.  
  
    > [!TIP]  
    >  Si le paramètre souhaité n’est pas répertorié, cochez la case **Configurer d’autres paramètres qui ne se trouvent pas dans les groupes de paramètres par défaut**.  
  
9. Dans chaque page de paramètres, configurez les paramètres dont vous avez besoin et indiquez si vous voulez les corriger quand ils ne sont pas conformes sur des périphériques (quand cela est pris en charge).  
  
10. Pour chaque groupe de paramètres, vous pouvez également configurer la gravité signalée quand un élément de configuration n’est pas conforme :  
  
    -   **Aucun** : les appareils qui ne respectent pas cette règle de conformité ne signalent pas la gravité d’un échec pour les rapports Configuration Manager.  
  
    -   **Informations** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Informations** pour les rapports Configuration Manager.  
  
    -   **Avertissement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Avertissement** pour les rapports Configuration Manager.  
  
    -   **Critique** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager.  
  
    -   **Critique avec événement** : les appareils qui ne respectent pas cette règle de conformité signalent la gravité d’un échec de niveau **Critique** pour les rapports Configuration Manager. Ce niveau de gravité est également enregistré comme événement Windows dans le journal des événements des applications.  
  
11. Dans la page **Condition d’application de la plateforme** de l’Assistant, passez en revue tous les paramètres qui ne sont pas compatibles avec les plateformes prises en charge que vous avez sélectionnées précédemment. Vous pouvez revenir sur ces paramètres et les supprimer, ou vous pouvez continuer.  
  
    > [!TIP]  
    >  La conformité des paramètres non pris en charge n’est pas évaluée.  
  
12. Effectuez toutes les étapes de l'Assistant.  
  
 Vous pouvez afficher le nouvel élément de configuration dans le nœud **Éléments de configuration** de l’espace de travail **Ressources et Conformité**.  
  
##  <a name="windows-10-configuration-item-settings-reference"></a>Informations de référence sur les paramètres d’élément de configuration Windows 10  
  
### <a name="password"></a>Mot de passe  
  
|Paramètre|Détails|  
|-------------|-------------|  
|**Exiger des paramètres de mot de passe sur les appareils**|Exigez un mot de passe sur les appareils pris en charge.|  
|**Longueur minimale du mot de passe (caractères)**|Longueur minimale du mot de passe en caractères.|  
|**Expiration du mot de passe en jours**|Nombre de jours avant de devoir modifier le mot de passe.|  
|**Nombre de mots de passe mémorisés**|Empêche la réutilisation des mots de passe précédents.|  
|**Nombre d’échecs de tentative de connexion avant la réinitialisation du périphérique**|Réinitialise le périphérique si la connexion échoue ce nombre de fois.|  
|**Durée d’inactivité avant le verrouillage de l’appareil**|Indique le nombre de minutes pendant lequel le périphérique doit être inactif avant d’être automatiquement bloqué.|  
|**Complexité du mot de passe**|Choisissez si vous pouvez spécifier un code confidentiel tel que « 1234 » ou si vous devez fournir un mot de passe fort.|
|**Nombre de jeux de caractères complexes requis dans le mot de passe**|Si vous avez sélectionné un mot de passe **Fort**, utilisez ce paramètre pour configurer le nombre de jeux de caractères complexes requis. Pour un mot de passe fort, ce paramètre doit avoir au moins la valeur **3**, ce qui signifie qu’il doit comporter à la fois des chiffres et des lettres. Sélectionnez **4** si vous souhaitez exiger un mot de passe qui contienne des caractères spéciaux comme **(% $**.<br>(Windows 10 uniquement)  |
  
###  <a name="device"></a>Appareil  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**BlueTooth**|Permet l’utilisation de la fonctionnalité Bluetooth sur le périphérique.|  
  
### <a name="cloud"></a>Cloud  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Synchronisation des paramètres**|Permet la synchronisation des paramètres entre les appareils.|  
|**Synchronisation des informations d'identification**|Permet la synchronisation des informations d'identification entre les appareils.|  
|**Synchronisation des paramètres via des connexions limitées**|Autorisez la synchronisation des paramètres quand la connexion Internet est mesurée.|  
  
### <a name="roaming"></a>Itinérant  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Itinérance des données**|Autorisez l'itinérance entre réseaux lors de l'accès aux données.|  
  
### <a name="encryption"></a>Chiffrement  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Chiffrement de fichiers sur le périphérique**|Exige que les fichiers soient chiffrés sur le périphérique.|  
  
### <a name="system-security"></a>Sécurité système  
  
|Nom du paramètre|Détails|  
|------------------|-------------|  
|**Contrôle de compte d'utilisateur**|Configure le fonctionnement du contrôle de compte d’utilisateur Windows sur le périphérique.<br />Par exemple, vous pouvez le désactiver ou définir le niveau auquel vous êtes notifié.|  
|**Pare-feu réseau**|Active ou désactive le pare-feu Windows.|  
|**SmartScreen**|Activez ou désactivez Windows SmartScreen.|  
|**Protection antivirus**|Exige l’installation et la configuration du logiciel antivirus.|  
|**Les signatures de la protection antivirus sont à jour**|Exige que les fichiers de signature du logiciel antivirus de l’appareil soient à jour.|  
  
### <a name="windows-information-protection-wip"></a>Protection des informations Windows (WIP)

Avec l’augmentation du nombre d’appareils appartenant aux employés au sein de l’entreprise, il existe un risque accru de fuites accidentelles de données via les applications et les services, tels que le courrier électronique, les réseaux sociaux et le cloud public, qui sont en dehors du contrôle de l’entreprise. C’est par exemple le cas quand un employé envoie les dernières photos de conception à partir de son compte de messagerie personnel, quand il copie et colle des informations sur des produits dans un tweet ou quand il enregistre un rapport des ventes en cours dans son stockage cloud public.

La Protection des informations Windows (anciennement, Enterprise Data Protection) vous protège contre ces fuites de données potentielles sans interférer avec l’expérience de l’employé. WIP contribue aussi à protéger les données et les applications d’entreprise contre les fuites accidentelles de données sur les appareils d’entreprise et les appareils personnels que les employés apportent sur leur lieu de travail, sans exiger de modifications au niveau de votre environnement ou d’autres applications.

 Les éléments de configuration WIP de Configuration Manager permettent de gérer la liste des applications protégées par WIP, les emplacements réseau de l’entreprise, le niveau de protection et les paramètres de chiffrement.
  

Pour plus d’informations sur la Protection des informations Windows avec Configuration Manager, consultez [Protéger vos données d’entreprise à l’aide de la Protection des informations Windows (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
  
## <a name="see-also"></a>Voir aussi  
 [Éléments de configuration pour les appareils gérés avec le client System Center Configuration Manager](../../compliance/deploy-use/configuration-items-for-devices-managed-with-the-client.md)
