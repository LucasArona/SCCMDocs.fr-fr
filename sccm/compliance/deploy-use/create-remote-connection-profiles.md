---
title: Créer des profils de connexion à distance
titleSuffix: Configuration Manager
description: Utilisez les profils de connexion à distance System Center Configuration Manager pour permettre aux utilisateurs de se connecter à distance aux ordinateurs de travail.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: c0e94fd8669556223044403fc72216fcaaaa5e54
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32337698"
---
# <a name="remote-connection-profiles-in-system-center-configuration-manager"></a>Profils de connexion à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez les profils de connexion à distance System Center Configuration Manager pour permettre aux utilisateurs de se connecter à distance aux ordinateurs de travail quand ils ne sont pas connectés au domaine ou si leurs ordinateurs personnels sont connectés à Internet.  

 Les utilisateurs peuvent se connecter à leur ordinateur professionnel à partir des types d'appareils suivants :  

-   Ordinateurs qui exécutent Microsoft Windows  

-   Appareils qui exécutent iOS  

-   Appareils qui exécutent Android  

Les profils de connexion à distance vous permettent de déployer des paramètres de connexion Bureau à distance sur les utilisateurs dans votre hiérarchie Configuration Manager. Les utilisateurs peuvent ensuite utiliser le portail d'entreprise pour accéder à leurs ordinateurs professionnels principaux via le Bureau à distance en utilisant les paramètres de connexion Bureau à distance fournis par le portail d'entreprise.  

Microsoft Intune est nécessaire si vous voulez que les utilisateurs se connectent à leurs PC de travail via le portail d’entreprise. Si vous n’utilisez pas Intune, les utilisateurs peuvent toujours utiliser les informations du profil de connexion à distance pour se connecter à leurs PC de travail à l’aide du Bureau à distance via une connexion VPN.  

> [!IMPORTANT]  
>  Quand vous indiquez des paramètres de profil de connexion à distance à l’aide de la console Configuration Manager, ils sont stockés dans la stratégie locale de l’ordinateur client. Ces paramètres risquent donc de remplacer les paramètres du Bureau à distance configurés par une autre application. En outre, si vous utilisez la stratégie de groupe Windows pour configurer les paramètres du Bureau à distance, les paramètres spécifiés dans la stratégie de groupe remplacent ceux configurés à l’aide de Configuration Manager.  

 Quand vous installez Configuration Manager, un groupe de sécurité, **Connexion de PC à distance**, est créé. Ce groupe est renseigné lorsque vous déployez un profil de connexion à distance qui inclut les principaux utilisateurs de l'ordinateur sur lequel vous déployez le profil. Bien qu'un administrateur local puisse ajouter des noms d'utilisateur à ce groupe, ces utilisateurs sont retirés du groupe lors de l'évaluation de la compatibilité des profils de connexion à distance déployés.  

 Si vous ajoutez manuellement un utilisateur à ce groupe, l'utilisateur peut initier des connexions à distance, mais les informations de connexion ne seront pas publiées dans le portail d'entreprise.  

 Si vous supprimez manuellement du groupe un utilisateur qui a été ajouté par Configuration Manager, Configuration Manager corrige automatiquement ce changement en rajoutant l’utilisateur lors de la prochaine évaluation de la compatibilité du profil de connexion à distance.  

> [!IMPORTANT]  
>  Si la relation d’affinité entre utilisateur et appareil change (par exemple, l’ordinateur auquel se connecte un utilisateur n’est plus un appareil principal de l’utilisateur), Configuration Manager désactive le profil de connexion à distance et les paramètres du Pare-feu Windows pour empêcher les connexions à l’ordinateur.  

## <a name="prerequisites"></a>Prérequis  

### <a name="external-dependencies"></a>Dépendances externes  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Serveur de passerelle Bureau à distance.|Si vous souhaitez autoriser les utilisateurs à se connecter en dehors du domaine de la société, sur Internet, vous devez installer et configurer un serveur de passerelle Bureau à distance.<br /><br /> Si les paramètres Bureau à distance ou services Terminal Server sont gérés par une autre application ou les paramètres de stratégie de groupe, les profils de connexion à distance risquent de ne pas fonctionner correctement. Quand vous déployez des profils de connexion à distance à partir de la console Configuration Manager, ses paramètres sont stockés dans la stratégie locale de l’ordinateur client. Ces paramètres risquent donc de remplacer les paramètres du Bureau à distance configurés par une autre application. En outre, si vous utilisez les paramètres de stratégie de groupe pour configurer les paramètres du Bureau à distance, les paramètres spécifiés dans la stratégie de groupe remplacent ceux configurés par Configuration Manager.<br /><br /> Pour plus d'informations sur la procédure d'installation et de configuration d'un serveur de passerelle Bureau à distance, consultez la documentation Windows Server.|  
|Si les ordinateurs clients exécutent un pare-feu basé sur l'hôte, il doit autoriser le programme Mstsc.exe.|Lorsque vous configurez un profil de connexion à distance, vous devez activer le paramètre **Autoriser l'exception de pare-feu Windows pour les connexions sur les domaines Windows et sur les réseaux privés** . Quand ce paramètre est activé, Configuration Manager configure automatiquement le Pare-feu Windows pour autoriser le programme Mstsc.exe. Toutefois, si les ordinateurs clients exécutent un autre pare-feu basé sur l'hôte, vous devez configurer manuellement cette dépendance de pare-feu.<br /><br /> Les paramètres de stratégie de groupe pour configurer le Pare-feu Windows peuvent remplacer la configuration définie dans Configuration Manager. Si vous utilisez stratégie de groupe pour configurer le pare-feu Windows, assurez-vous que les paramètres de stratégie de groupe ne bloquent pas le programme Mstsc.exe.|  

### <a name="configuration-manager-dependencies"></a>Dépendances de Configuration Manager  

|Dépendance|Plus d'informations|  
|----------------|----------------------|  
|Configuration Manager doit être connecté à Microsoft Intune (« configuration hybride »).|Pour plus d’informations sur la connexion de Configuration Manager à Microsoft Intune, consultez Gérer les appareils mobiles avec Configuration Manager et Microsoft Intune.|  
|Pour qu'un utilisateur se connecte à un ordinateur professionnel sur le réseau de l'entreprise, cet ordinateur doit être un appareil principal de l'utilisateur.|Pour plus d’informations sur l’affinité entre utilisateur et appareil, consultez [Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).|  
|Des autorisations de sécurité spécifiques doivent avoir été accordées pour gérer les profils de connexion à distance.|Le rôle de sécurité **Gestionnaire de paramètres de compatibilité** inclut les autorisations nécessaires pour gérer les profils de connexion à distance. Pour plus d'informations, voir <br />[Configurer l’administration basée sur des rôles](/sccm/core/servers/deploy/configure/configure-role-based-administration).|  

## <a name="security-and-privacy-considerations-for-remote-connection-profiles"></a>Considérations relatives à la sécurité et à la confidentialité pour les profils de connexion à distance  

### <a name="security-considerations"></a>Considérations relatives à la sécurité  

|Bonnes pratiques de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Spécifiez manuellement l'affinité entre utilisateur et appareil au lieu de permettre aux utilisateurs d'identifier leur appareil principal. En outre, n'activez pas la configuration basée sur l'utilisation.|Étant donné que vous devez activer **Autoriser tous les utilisateurs principaux de l'ordinateur professionnel à se connecter à distance** avant de pouvoir déployer un profil de connexion à distance, spécifiez toujours manuellement l'affinité entre utilisateur et appareil. Ne considérez pas les informations collectées à partir d'utilisateurs ou de l'appareil comme faisant autorité. Si vous déployez des profils de connexion à distance alors que l'affinité entre utilisateur et appareil n'est pas spécifiée par un utilisateur administratif approuvé, des utilisateurs non autorisés peuvent recevoir des privilèges élevés et être en mesure de se connecter à distance aux ordinateurs.<br /><br /> Si vous autorisez la configuration basée sur l’utilisation, ces informations sont collectées à l’aide de messages d’état non sécurisés par Configuration Manager. Pour réduire l'étendue de cette menace, utilisez la signature SMB (Server Message Block) ou IPsec (Internet Protocol security) entre les ordinateurs clients et le point de gestion.|  
|Limiter les droits d'administrateur local sur l'ordinateur du serveur de site.|Un utilisateur disposant de droits d’administrateur local sur le serveur de site peut ajouter manuellement des membres au groupe de sécurité Connexion de PC à distance, qui est créé et géré automatiquement par Configuration Manager. Cela peut provoquer une élévation des privilèges dans la mesure où les membres qui sont ajoutés à ce groupe bénéficient d'autorisations Bureau à distance.|  

### <a name="privacy-considerations"></a>Considérations relatives à la confidentialité  

-   Si un utilisateur établit une connexion vers un ordinateur professionnel à partir du portail d'entreprise, un fichier comportant l'extension .rdp ou .wsrdp est téléchargé. Il contient le nom de l'appareil et le nom du serveur de passerelle Bureau à distance qui est requis pour ouvrir la session Bureau à distance. L'extension de fichier varie selon le système d'exploitation de l'appareil. Par exemple, les systèmes d’exploitation Windows 7 et Windows 8 utilisent un fichier .rdp, et Windows 8.1 utilise un fichier .wsrdp.  

-   L'utilisateur peut choisir d'ouvrir ou d'enregistrer le fichier .rdp. Si l'utilisateur choisit d'ouvrir le fichier .rdp, celui-ci peut être stocké dans le cache du navigateur Web, selon les paramètres de rétention configurés pour le navigateur. Si l'utilisateur choisit d'enregistrer le fichier, le fichier n'est pas stocké dans le cache du navigateur. Le fichier est enregistré jusqu'à ce que l'utilisateur le supprime manuellement.  

-   Le fichier .wsrdp est téléchargé et automatiquement enregistré localement. La prochaine fois que l'utilisateur exécutera une session Bureau à distance, le fichier sera écrasé.  

-   Avant de configurer les profils de connexion à distance, analysez vos besoins en matière de confidentialité.  


## <a name="create-a-remote-connection-profile"></a>Créer un profil de connexion à distance

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Profils de connexion à distance**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un profil de connexion à distance**.  

4.  Dans la page **Général** de l’ **Assistant Créer un profil de connexion à distance**, spécifiez un nom et une description éventuelle pour le profil en utilisant un maximum de 256 caractères pour chaque élément.  

5.  Dans la page **Paramètres de profil**, spécifiez les paramètres suivants pour le profil de connexion à distance :  

    -   **Nom complet et port du serveur de passerelle Bureau à distance (facultatif)** : spécifiez le nom du serveur de passerelle Bureau à distance à utiliser pour les connexions.  

        > [!NOTE]  
        >  Configuration Manager ne gère pas l’utilisation d’un nom de domaine internationalisé pour spécifier un serveur dans cette zone.  
        >   
        >  Le nom du serveur ne peut pas dépasser 256 caractères et peut contenir des caractères majuscules, des caractères minuscules, des caractères numériques et les caractères **–** et **_** , séparés par des points.  

    -   **Autoriser des connexions uniquement sur les ordinateurs qui exécutent le Bureau à distance avec authentification au niveau du réseau**  

6.  Sélectionnez **Activé** ou **Désactivé** pour chacun des paramètres de connexion suivants :  

    -   **Autoriser les connexions à distance aux ordinateurs professionnels**  

    -   **Autoriser tous les utilisateurs principaux de l'ordinateur professionnel à se connecter à distance**  

    -   **Autoriser l'exception du Pare-feu Windows pour les connexions sur des domaines Windows et sur des réseaux privés**  

    > [!IMPORTANT]  
    >  Ces trois paramètres doivent être les mêmes pour pouvoir continuer l'Assistant.  

7.  Dans la page **Résumé**, passez en revue les actions à exécuter, puis terminez l’Assistant.  

 Le nouveau profil de connexion à distance figure dans le nœud **Profils de connexion distance** dans l'espace de travail **Ressources et Conformité** .  

Déployer un profil de connexion à distance  

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité** > **Paramètres de compatibilité** > **Profils de connexion à distance**.  

3.  Dans la liste **Profils de connexion à distance** , sélectionnez le profil de connexion à distance que vous souhaitez déployer, puis, dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

4.  Dans la boîte de dialogue **Déployer le profil de connexion à distance** , spécifiez les éléments suivants :  

    -   **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement de périphériques sur lequel vous souhaitez déployer le profil de connexion à distance.  

    -   **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** : activez cette option pour résoudre automatiquement le profil de connexion à distance quand il n’est pas compatible sur un appareil (par exemple, s’il n’est pas présent).  

    -   **Autoriser les corrections en dehors de la fenêtre de maintenance** : si une fenêtre de maintenance a été configurée pour le regroupement sur lequel vous déployez le profil de connexion à distance, activez cette option pour permettre à Configuration Manager de résoudre le profil de connexion à distance en dehors de la fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).  

    -   **Générer une alerte** : activez cette option pour configurer une alerte qui est générée si la compatibilité du profil de connexion à distance est inférieure à un pourcentage spécifié par une date et une heure spécifiques. Vous pouvez également spécifier si vous souhaitez qu'une alerte soit envoyée à System Center Operations Manager.  

    -   **Spécifier le calendrier d’évaluation de la compatibilité pour cette ligne de base de configuration** : spécifiez le calendrier selon lequel le profil de connexion à distance déployé est évalué sur les appareils. Il peut s'agir d'un calendrier simple ou d'un calendrier personnalisé.  

    > [!TIP]  
    >  Si un périphérique quitte un regroupement sur lequel un profil de connexion à distance a été déployé, les paramètres du profil de connexion à distance sont désactivés sur le périphérique. Toutefois, pour que cela s'effectue correctement, vous devez déjà avoir déployé au moins un élément de configuration ou une ligne de base de configuration contenant un élément de configuration de votre site.  
    >   
    >  Le profil est évalué par les appareils quand l’utilisateur se connecte.  
    >   
    >  Supposons deux profils de connexion à distance déployés sur le même regroupement d’appareils. Dans l’un des profils, l’option **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** est cochée et dans l’autre, cette même option n’est pas cochée. De plus, les deux profils de connexion à distance contiennent des paramètres de connexion différents. Dans ce cas, le profil dans lequel l’option n’est pas cochée peut remplacer les paramètres de l’autre profil. Ce type de déploiement de profil de connexion à distance n’est pas pris en charge par Configuration Manager.  

5.  Cliquez sur **OK** pour fermer la boîte de dialogue **Déployer le profil de connexion à distance** et pour créer le déploiement.  

## <a name="monitor-a-remote-connection-profile"></a>Surveiller un profil de connexion à distance  

### <a name="view-compliance-results-in-the-configuration-manager-console"></a>Afficher les résultats de compatibilité dans la console Configuration Manager  

1.  Dans la console Configuration Manager, cliquez sur **Surveillance** > **Déploiements**.  

3.  Dans la liste **Déploiements** , sélectionnez le déploiement du profil de connexion à distance dont vous souhaitez vérifier les informations de compatibilité.  

4.  Vous pouvez consulter un résumé des informations relatives à la compatibilité du déploiement du profil de connexion à distance sur la page principale. Pour afficher des informations plus détaillées, sélectionnez le déploiement du profil de connexion à distance puis, dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Afficher l'état** pour ouvrir la page **État du déploiement** .  

     La page **État du déploiement** contient les onglets suivants :  

    -   **Compatible :** affiche la compatibilité du profil de connexion à distance en fonction du nombre de biens affectés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les périphériques qui sont compatibles avec le profil de connexion à distance. Le volet **Détails du bien** affiche également les périphériques compatibles avec ce profil. Double-cliquez sur un périphérique de la liste pour afficher des informations supplémentaires.  

        > [!IMPORTANT]  
        >  Un profil de connexion à distance n'est pas évalué s'il n'est pas applicable sur un périphérique client. Toutefois, il est retourné comme conforme.  

    -   **Erreur :** affiche la liste de toutes les erreurs pour le déploiement du profil de connexion à distance sélectionné en fonction du nombre de biens affectés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les périphériques qui ont généré des erreurs avec ce profil. Lorsque vous sélectionnez un périphérique, le volet **Détails du bien** affiche les périphériques qui sont concernés par le problème sélectionné. Double-cliquez sur un périphérique de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Non compatible :** affiche la liste de toutes les règles non compatibles au sein du profil de connexion à distance en fonction du nombre de biens affectés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les périphériques qui ne sont pas compatibles avec ce profil. Lorsque vous sélectionnez un périphérique, le volet **Détails du bien** affiche les périphériques qui sont concernés par le problème sélectionné. Double-cliquez sur un périphérique de la liste pour afficher des informations supplémentaires sur le problème.  

    -   **Inconnu :** affiche la liste de tous les appareils qui n’ont pas signalé de compatibilité pour le déploiement du profil de connexion à distance sélectionné, avec l’état du client actuel des appareils.  

5.  Sur la page **État du déploiement** , vous pouvez consulter des informations détaillées sur la compatibilité du profil de connexion à distance déployé. Un nœud temporaire est créé sous le nœud **Déploiements** qui vous aide à retrouver rapidement ces informations.  

### <a name="view-compliance-results-with-reports"></a>Afficher les résultats de compatibilité avec les rapports  
 Configuration Manager inclut des rapports intégrés que vous pouvez utiliser pour surveiller les informations sur les profils de connexion à distance. La catégorie de ces rapports est **Gestion de la conformité et des paramètres**.  

> [!IMPORTANT]  
>  Vous devez utiliser un caractère générique (%) lorsque vous utilisez les paramètres **Filtre de périphérique** et **Filtre d'utilisateur** dans les rapports des paramètres de compatibilité.  

 Pour plus d’informations sur la configuration de la génération de rapports dans Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](/sccm/core/servers/manage/reporting).  
