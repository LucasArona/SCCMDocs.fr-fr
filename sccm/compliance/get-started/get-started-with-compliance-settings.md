---
title: Prendre en main les paramètres de compatibilité
titleSuffix: Configuration Manager
description: En savoir plus sur les concepts de base et sur le fonctionnement des paramètres de conformité
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4e85b6886947fe0ac720f5840dcefd91a441d3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56130943"
---
# <a name="get-started-with-compliance-settings-in-system-center-configuration-manager"></a>Prise en main des paramètres de compatibilité dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de créer des paramètres de conformité Configuration Manager, commencez par vous familiariser avec les concepts de base et avec leur fonctionnement.  



## <a name="how-compliance-settings-work"></a>Fonctionnement des paramètres de conformité  
 Les paramètres de conformité vous permettent de gérer la configuration et la conformité des clients de votre organisation.  

 Les éléments de configuration se répartissent en deux catégories principales :  

-   **Paramètres pour les appareils gérés par le client Configuration Manager** : il s’agit généralement d’appareils sur lesquels vous avez installé le logiciel client Configuration Manager, grâce auquel vous pouvez gérer ces appareils.  

-   **Paramètres pour les appareils gérés sans le client Configuration Manager** : il s’agit généralement d’appareils qui sont gérés avec Microsoft Intune ou par le biais de la gestion des appareils locale de Configuration Manager.  



## <a name="what-devices-are-supported"></a>Quels sont les appareils pris en charge ?  

| Type d'appareil | Informations complémentaires |  
|------------|----------------------|  
| Ordinateurs Windows (avec le client Configuration Manager) | Créez des éléments de configuration personnalisés pour évaluer certains objets, notamment les clés et les fichiers de Registre ou encore les attributs Active Directory.<br /><br /> Quand vous utilisez le type d’élément de configuration Windows 10, sélectionnez les paramètres dans une liste prédéfinie. |  
| Ordinateurs Windows (inscrits auprès de Microsoft Intune) | Sélectionnez les paramètres dans une liste prédéfinie. |  
| Appareils iOS (inscrits auprès de Microsoft Intune) | Sélectionnez les paramètres dans une liste prédéfinie. |  
| Appareils Android (inscrits auprès de Microsoft Intune) | Sélectionnez les paramètres dans une liste prédéfinie. |  
| Appareils Windows Phone (inscrits auprès de Microsoft Intune) | Sélectionnez les paramètres dans une liste prédéfinie. |  
| Ordinateurs Mac (avec le client Configuration Manager) | Créez des éléments de configuration personnalisés pour évaluer certains objets, tels que des préférences macOS et des résultats retournés par un script. |  
| Ordinateurs Mac (inscrits auprès de Microsoft Intune) | Sélectionnez les paramètres dans une liste prédéfinie. |  



## <a name="what-is-a-configuration-item"></a>Qu’est-ce qu’un élément de configuration ?  
 Un élément de configuration est un conteneur qui stocke des informations spécifiques. Les informations que vous configurez dépendent du type d’élément de configuration. Les éléments de configuration peuvent inclure les informations suivantes :

-   **Informations sur la méthode de détection** : concernent uniquement les éléments de configuration Windows qui contiennent des paramètres d’application. Elles permettent de déterminer si une application est installée. Cette détection utilise le fichier Windows Installer de l’application ou un script personnalisé.  

-   **Paramètres** : représentent les conditions opérationnelles ou techniques d’évaluation de la conformité des appareils clients. Configurez un nouveau paramètre ou accéder à un paramètre existant sur un ordinateur de référence.  

-   **Règles de conformité** : spécifient les conditions qui définissent la conformité d’un paramètre d’élément de configuration. Avant d’évaluer la conformité d’un paramètre, le client doit avoir au moins une règle de conformité. Certains paramètres corrigent les paramètres non conformes. Créez des règles ou accédez à un paramètre existant dans n’importe quel élément de configuration et sélectionnez-y des règles.  

-   **Plateformes prises en charge** : plateformes d’appareils définies par vos soins, dans lesquelles le client évalue la conformité des éléments de configuration. Si vous déployez un élément de configuration sur un appareil qui ne figure pas dans la liste des plateformes prises en charge, sa conformité n’est pas évaluée.  



## <a name="what-is-a-configuration-baseline"></a>Qu’est-ce qu’une base de référence de configuration ?  
 Définissez une base de référence de configuration qui inclut les éléments de configuration à évaluer. De même, incluez les paramètres et les règles qui décrivent le niveau de conformité exigé. Importez ces données de configuration à partir des packs de configuration Configuration Manager. Ces packs de configuration sont définis par Microsoft et d’autres fournisseurs. Vous pouvez aussi créer des éléments de configuration et des bases de référence de configuration.  

 Après avoir défini une base de référence de configuration, déployez-la dans des regroupements d’utilisateurs et d’appareils. Le client évalue ensuite la conformité des paramètres de référence selon une planification. Vous pouvez déployer plusieurs bases de référence de configuration sur les appareils. Cette granularité offre un meilleur contrôle de la conformité. 

 Les périphériques client évaluent leur conformité par rapport à chaque ligne de base de configuration déployée et signalent immédiatement les résultats au site à l'aide de messages d'état. Si la base de référence de configuration a été téléchargée sur un appareil qui est actuellement déconnecté du réseau, il continue d’évaluer la conformité des éléments de configuration. Il envoie les informations de conformité une fois reconnecté.  

### <a name="monitoring-configuration-baselines"></a>Analyse des bases de référence de configuration
- Analysez les résultats de l’évaluation de conformité dans la console Configuration Manager, dans l’espace de travail **Analyse**, dans le nœud **Déploiements**. Par exemple :
    - Causes courantes de non-conformité
    - Errors
    - Nombre d’utilisateurs et d’appareils concernés
- Exécutez des rapports sur les paramètres de conformité avec des détails supplémentaires. Par exemple :
    - Identification des appareils conformes ou non conformes
    - Identification de l’élément de la base de référence de configuration à l’origine de la non-conformité d’un ordinateur
- Consultez les résultats de l’évaluation de la conformité sur un ordinateur Windows exécutant le client Configuration Manager. Ouvrez **Configuration Manager** dans le Panneau de configuration, puis accédez à l’onglet **Configurations**.  



## <a name="user-data-and-profiles-configuration-items"></a>Éléments de configuration des données et profils utilisateur  
 Les éléments de configuration pour les données et les profils utilisateur sont constitués de paramètres qui contrôlent la façon dont les utilisateurs des ordinateurs exécutant Windows 8 et ultérieur gèrent les éléments suivants :  
   - Redirection de dossiers
   - Fichiers hors connexion
   - Profils d’itinérance  

Déployez ces éléments de configuration dans les regroupements d’utilisateurs. Analysez leur conformité à partir du nœud **Surveillance** de la console Configuration Manager. Contrairement aux autres éléments de configuration, ne les ajoutez pas aux bases de référence de configuration avant de les déployer. Déployez-les directement en cliquant sur **Déployer** dans le ruban.  

 Pour plus d’informations, consultez [Créer des éléments de configuration des données et profils utilisateur](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  



## <a name="remote-connection-profiles"></a>Profils de connexion à distance  
 Les profils de connexion à distance proposent un ensemble d’outils et de ressources qui vous aident à créer, déployer et analyser les paramètres de connexion à distance. En déployant ces paramètres sur les appareils, vous permettez aux utilisateurs finaux de se connecter plus facilement à leurs ordinateurs sur le réseau d’entreprise.  

Pour en savoir plus, voir [Créer des profils de connexion à distance](/sccm/compliance/deploy-use/create-remote-connection-profiles).  



## <a name="windows-edition-upgrade"></a>Mise à niveau des éditions de Windows
La stratégie de mise à niveau d’édition met automatiquement à niveau les appareils qui exécutent certaines versions de Windows 10 vers une édition plus récente. L’appareil reçoit une nouvelle clé de produit ou un nouveau fichier de licence dont il se sert pour procéder à la mise à niveau.

Pour plus d’informations, consultez [Mettre à niveau des appareils Windows avec la stratégie de mise à niveau d’édition](/sccm/compliance/deploy-use/upgrade-windows-version).



## <a name="microsoft-edge-browser-profiles"></a>Profils du navigateur Microsoft Edge
<!-- 1357310 --> Depuis la version 1802, pour les clients qui utilisent le navigateur web [Microsoft Edge](https://technet.microsoft.com/microsoft-edge/bb265256) sur des clients Windows 10, créez une stratégie de paramètres de conformité pour configurer plusieurs paramètres Microsoft Edge. 

Pour plus d’informations, consultez [Profils du navigateur Microsoft Edge](/sccm/compliance/deploy-use/browser-profiles).

