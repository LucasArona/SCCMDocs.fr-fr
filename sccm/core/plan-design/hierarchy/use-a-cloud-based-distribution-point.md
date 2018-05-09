---
title: Point de distribution cloud
titleSuffix: Configuration Manager
description: Découvrez les configurations et les limites de l’utilisation d’un point de distribution cloud avec System Center Configuration Manager.
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd3e8c58b358093ebf9d90478920c45e127e382e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="use-a-cloud-based-distribution-point-with-system-center-configuration-manager"></a>Utiliser un point de distribution cloud avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un point de distribution cloud est un point de distribution System Center Configuration Manager qui est hébergé dans Microsoft Azure. Les informations suivantes visent à vous faire découvrir les différentes configurations et limitations liées à l’utilisation d’un point de distribution cloud.

Quand vous avez installé un site principal et que vous êtes prêt à installer un point de distribution cloud, consultez [Installer des points de distribution cloud dans Microsoft Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## <a name="plan-to-use-a-cloud-based-distribution-point"></a>Planifier l’utilisation d’un point de distribution cloud
Lorsque vous utilisez une distribution cloud, vous devez :  

-   **Configurer les paramètres clients** pour permettre aux utilisateurs et aux appareils d’accéder au contenu.  

-   **Spécifier un site principal pour gérer le transfert de contenu** vers le point de distribution.  

-   **Définir des seuils** pour la quantité de contenu que vous voulez stocker sur le point de distribution et celle pouvant être transférée par les clients à partir du point de distribution.  


Selon les seuils configurés, Configuration Manager peut déclencher des alertes pour vous avertir quand le volume total de contenu que vous avez stocké sur le point de distribution approche de la quantité de stockage spécifiée, ou quand les transferts de données par les clients avoisinent les seuils définis.  

Les points de distribution cloud prennent en charge plusieurs fonctionnalités également proposées par les points de distribution locaux :  

-   Vous gérez les points de distribution cloud individuellement ou en tant que membres de groupes de points de distribution.  

-   Vous pouvez utiliser un point de distribution cloud comme emplacement de contenu de secours.  

-   Prise en charge des clients basés sur intranet et Internet.  


Les points de distribution cloud offrent les autres avantages suivants :  

-   Configuration Manager chiffre le contenu envoyé à un point de distribution cloud, avant de l’envoyer à Azure.  

-   Dans Azure, vous pouvez adapter manuellement le service cloud en fonction des demandes de contenu émanant des clients, sans avoir à installer et préparer des points de distribution supplémentaires.  

-   Le point de distribution cloud prend en charge le téléchargement de contenu par les clients configurés pour Windows BranchCache.  


Un point de distribution cloud présente les limitations suivantes :  

-  Avant d’utiliser la version 1610 avec le correctif KB4010155, vous ne pouvez pas utiliser un point de distribution cloud pour héberger des packages de mises à jour logicielles. Ce problème est résolu dans la version 1702 et les versions ultérieures.  

-   Vous ne pouvez pas utiliser un point de distribution cloud pour PXE ou les déploiements en multidiffusion.  

-   Aucun point de distribution cloud n'est proposé aux clients en guise d'emplacement de contenu pour une séquence de tâches déployée à l'aide de l'option **Télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches**. Toutefois, les séquences de tâches qui sont déployées à l'aide de l'option de déploiement **Télécharger tout le contenu localement avant de démarrer la séquence de tâches** peuvent utiliser un point de distribution cloud en guise d'emplacement de contenu valide.  

-   Un point de distribution cloud ne prend pas en charge les packages exécutés à partir du point de distribution. Tout le contenu doit être téléchargé par le client et exécuté localement.  

-   Un point de distribution cloud ne prend pas en charge la diffusion en continu d'applications à l'aide d'Application Virtualization ou de programmes similaires.  

-   Un point de distribution cloud ne gère pas le contenu préparé. Le Gestionnaire de distribution du site principal qui gère le point de distribution transfère l'ensemble du contenu vers le point de distribution.  

-   Un point de distribution cloud ne peut pas être configuré en tant que point de distribution d'extraction.  

##  <a name="BKMK_PrereqsCloudDP"></a> Conditions préalables pour les points de distribution cloud  
 Un point de distribution cloud requiert les conditions préalables suivantes pour son utilisation :  

-   Un abonnement à Azure (consultez [À propos des abonnements et des certificats](#BKMK_CloudDPCerts) dans cette rubrique.).

-   Un certificat de gestion auto-signé ou PKI pour la communication entre un serveur de site principal Configuration Manager et le service cloud dans Azure (consultez [À propos des abonnements et des certificats](#BKMK_CloudDPCerts) dans cette rubrique).

-   Certificat de service (PKI) que les clients Configuration Manager utilisent pour se connecter aux points de distribution cloud et y télécharger du contenu via HTTPS.  

-  Un appareil ou un utilisateur doit avoir le paramètre client **Autoriser l’accès au point de distribution cloud** réglé sur **Oui** dans **Services cloud** pour pouvoir accéder au contenu d’un point de distribution cloud. Par défaut, cette valeur est définie sur **Non**.  

-   Un client doit être en mesure de résoudre le nom du service cloud, ce qui nécessite la présence d’un alias DNS (Domain Name System) et d’un enregistrement CNAME dans votre espace de noms DNS.  

-   Un client doit pouvoir accéder à Internet pour utiliser le point de distribution cloud.  

##  <a name="BKMK_CloudDPCost"></a> Coût d’utilisation d’une distribution cloud  
 Lorsque vous utilisez un point de distribution cloud, planifiez le coût du stockage de données et des téléchargements que les clients Configuration Manager effectuent.  

 Configuration Manager inclut des options facilitant le contrôle des coûts et de l’accès aux données :  

-   Vous pouvez contrôler et surveiller la quantité de contenu que vous stockez dans un service cloud.  

-   Vous pouvez configurer Configuration Manager pour être averti lorsque les **seuils** mensuels des téléchargements du client sont atteints ou dépassés.  

-   De plus, vous pouvez utiliser la mise en cache d’homologue (Windows BranchCache) pour réduire le nombre de transferts de données que les clients effectuent à partir des points de distribution cloud. Les clients Configuration Manager configurés pour Windows BranchCache peuvent transférer du contenu à l’aide des points de distribution cloud.  


**Options :**  

-   **Paramètres client pour cloud**: vous pouvez contrôler l’accès à tous les points de distribution cloud d’une hiérarchie à l’aide des **Paramètres client**.  

     Dans **Paramètres client**, la catégorie des **paramètres cloud** prend en charge le paramètre **Autoriser l'accès au point de distribution cloud**. Par défaut, ce paramètre est défini sur **Non**. Vous pouvez l’activer pour les utilisateurs et les appareils.  

-   **Seuils pour les transferts de données**: vous pouvez configurer des seuils pour la quantité de données que vous voulez stocker sur le point de distribution et pour la quantité de données que les clients peuvent télécharger à partir du point de distribution.  

     Les seuils des points de distribution cloud sont les suivants :  

    -   **Seuil d'alerte de stockage**: un seuil d'alerte de stockage définit la limite supérieure de la quantité de données ou de contenu que vous souhaitez stocker sur le point de distribution cloud. Configuration Manager peut générer une alerte d’avertissement lorsque l’espace disponible atteint le niveau défini.  

    -   **Seuil d'alerte de transfert**: un seuil d'alerte de transfert permet de surveiller la quantité de contenu transféré à partir du point de distribution vers les clients pendant une période de 30 jours. Le seuil d’alerte de transfert surveille le transfert de données pendant les 30 derniers jours et peut émettre une alerte d’avertissement et une alerte critique lorsque les transferts atteignent la valeur définie.  

        > [!IMPORTANT]  
        >  Configuration Manager surveille le transfert de données, mais n'interrompt pas ce transfert au-delà du seuil d'alerte de transfert défini.  

 Vous pouvez définir des seuils pour chaque point de distribution cloud pendant l'installation du point de distribution ou modifier les propriétés de chaque point de distribution cloud après son installation.  

-   **Alertes** : vous pouvez configurer Configuration Manager de manière à déclencher des alertes pour les transferts de données à destination et en provenance de chaque point de distribution cloud, en fonction des seuils de transfert de données que vous spécifiez. Ces alertes vous aident à surveiller les transferts de données, à décider quand arrêter le service cloud, à ajuster le contenu que vous stockez sur le point de distribution ou à modifier les clients pouvant utiliser les points de distribution cloud.  

     Dans un cycle horaire, le site principal qui surveille le point de distribution cloud télécharge des données transactionnelles à partir d’Azure et les stocke dans le fichier CloudDP-&lt;nom_service\>.log sur le serveur de site. Configuration Manager évalue ensuite ces informations par rapport aux quotas de stockage et de transfert pour chaque point de distribution du cloud. Lorsque le transfert de données atteint ou dépasse le volume défini pour les avertissements ou alertes critiques, Configuration Manager génère l’alerte appropriée.  

    > [!WARNING]  
    >  Comme les informations sur les transferts de données sont téléchargées depuis Azure toutes les heures, cette utilisation des données peut dépasser un seuil d’avertissement ou critique avant même que Configuration Manager n’accède aux données et n’émette une alerte.  

    > [!NOTE]  
    >  Les alertes pour un point de distribution cloud dépendent des statistiques d’utilisation fournies par Azure, un délai qui peut aller jusqu’à 24 heures. Pour plus d’informations sur Storage Analytics pour Azure et la fréquence de mise à jour des statistiques d’utilisation, consultez [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111) dans la bibliothèque MSDN Library.  


-   **Arrêter ou démarrer le service cloud à la demande**: vous pouvez choisir d’arrêter un service cloud à tout moment pour empêcher les clients de l’utiliser en continu. Lorsque vous arrêtez le service cloud, vous empêchez immédiatement les clients de télécharger tout autre contenu à partir du service. Vous pouvez redémarrer le service cloud pour restaurer l'accès aux clients. Par exemple, vous pouvez choisir d'arrêter un service cloud lorsque les seuils de données sont atteints.  

     Lorsque vous arrêtez un service cloud, le service cloud ne supprime pas le contenu du point de distribution et n'empêche pas le serveur de site de transférer du contenu supplémentaire vers le point de distribution cloud.  

     Pour arrêter un service cloud, dans la console Configuration Manager, sélectionnez le point de distribution dans le nœud **Points de distribution cloud**, sous **Services cloud**dans l'espace de travail **Administration**. Ensuite, cliquez sur **Arrêter le service** pour arrêter le service cloud qui s’exécute dans Azure.  

##  <a name="BKMK_CloudDPCerts"></a> À propos des abonnements et certificats pour les points de distribution cloud  
 Les points de distribution cloud ont besoin de certificats pour permettre à Configuration Manager de gérer le service cloud qui héberge le point de distribution et aux clients d'accéder au contenu à partir du point de distribution. Vous trouverez ci-dessous des informations générales sur ces certificats. Pour plus d’informations, consultez [Configuration requise des certificats PKI pour Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificats**  

-   **Certificat de gestion pour la communication entre un serveur de site et un point de distribution** : le certificat de gestion établit la relation de confiance entre l’API de gestion Azure et Configuration Manager. Cette authentification permet à Configuration Manager d’appeler l’API Azure quand vous effectuez des tâches comme le déploiement de contenu ou le démarrage et l’arrêt du service cloud. Azure permet aux clients de créer leurs propres certificats de gestion, qu’il s’agisse de certificats auto-signés ou de certificats émis par une Autorité de certification (AC) :  

    -   Fournissez le fichier .cer du certificat de gestion à Azure quand vous configurez Azure pour Configuration Manager. Le fichier .cer contient la clé publique pour le certificat de gestion. Avant d’installer un point de distribution cloud, vous devez charger ce certificat dans Azure. Il permet à Configuration Manager d’accéder à l’API Azure.  

    -   Fournissez le fichier .pfx du certificat de gestion à Configuration Manager lorsque vous installez le point de distribution cloud. Le fichier .pfx contient la clé privée pour le certificat de gestion. Configuration Manager stocke ce certificat dans la base de données du site. Comme le fichier .pfx contient la clé privée, vous devez fournir le mot de passe pour importer ce fichier de certificat dans la base de données Configuration Manager.  

    Si vous créez un certificat auto-signé, vous devez d’abord l’exporter au format .cer puis au format .pfx.  

    Vous pouvez éventuellement spécifier un fichier **.publishsettings** version 1 du Kit de développement logiciel (SDK) Azure 1.7. Pour plus d’informations sur les fichiers .publishsettings, consultez la documentation d’Azure.  

    Pour plus d’informations, consultez [Vue d’ensemble des certificats pour Azure Cloud Services](http://go.microsoft.com/fwlink/p/?LinkId=220281) et [How to add a management certificate to an Azure subscription (Comment ajouter un certificat de gestion à un abonnement Azure)](http://go.microsoft.com/fwlink/p/?LinkId=241722) dans la section de la bibliothèque MSDN consacrée à la plateforme Azure.  

-   **Certificat de service pour la communication entre le client et le point de distribution** : le certificat de service du point de distribution cloud Configuration Manager établit une relation de confiance entre les clients Configuration Manager et le point de distribution cloud, puis sécurise les données que les clients téléchargent à partir de ce point de distribution grâce au protocole SSL (Secure Socket Layer) sur HTTPS.  

    > [!IMPORTANT]  
    >  Le nom commun dans la zone d'objet de certificat du certificat de service doit être unique dans votre domaine et ne correspondre à aucun appareil joint à un domaine.  

   Pour obtenir un exemple de déploiement de ce certificat, consultez la section **Déployer le certificat de service pour les points de distribution cloud** dans la rubrique [Exemple de déploiement pas à pas des certificats PKI pour System Center Configuration Manager : autorité de certification Windows Server 2008](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="bkmk_Tasks"></a> Tâches de gestion courantes pour les points de distribution cloud  

-   **Communication entre un serveur de site et un point de distribution cloud**: quand vous installez un point de distribution cloud, vous devez affecter un site principal pour gérer le transfert de contenu vers le service cloud. Le principe est le même que lorsque vous installez le rôle de système de site du point de distribution sur un site spécifique.  

-   **Communication entre un client et un point de distribution cloud**: quand le paramètre client permettant l’utilisation d’un point de distribution cloud est activé pour un appareil ou un utilisateur d’appareil, l’appareil en question peut recevoir le point de distribution cloud comme emplacement de contenu valide :  

    -   Lorsqu’un client évalue les emplacements de contenu disponibles, un point de distribution cloud est considéré comme un point de distribution distant.  

    -   Les clients connectés via l'intranet utilisent uniquement les points de distribution cloud comme solution de secours si les points de distribution sur site ne sont pas disponibles.  

    Même si vous installez les points de distribution cloud dans des zones spécifiques d’Azure, les clients qui utilisent les points de distribution cloud ne connaissent pas ces régions Azure et sélectionnent un point de distribution cloud de façon non déterministe.

Par conséquent, si vous installez des points de distribution cloud dans plusieurs régions et qu’un client reçoit plusieurs points de distribution cloud comme emplacements de contenu, le client peut ne pas utiliser un point de distribution cloud de la même zone Azure que le client.  

Pour effectuer des demandes d’emplacement de contenu, les clients qui utilisent des points de distribution cloud respectent la séquence suivante :  

1.  Un client qui est configuré pour utiliser des points de distribution cloud commence toujours par essayer d'obtenir le contenu auprès d'un point de distribution préféré.  

2.  Lorsque le point de distribution préféré n’est pas disponible, le client utilise un point de distribution distant si le déploiement le permet et si un tel point est disponible.  

3.  Lorsqu'un point de distribution préféré ou un point de distribution distant n'est pas disponible, le client cherche alors à obtenir le contenu auprès d'un point de distribution cloud.  



  Lorsqu'un client utilise un point de distribution cloud comme emplacement de contenu, il s'authentifie auprès du point de distribution cloud en utilisant un jeton d'accès Configuration Manager. Si le client approuve le certificat de point de distribution cloud Configuration Manager, il peut ensuite télécharger le contenu demandé.  

-   **Surveillance des points de distribution cloud**: vous pouvez surveiller le contenu que vous déployez sur chaque point de distribution cloud, ainsi que le service cloud qui héberge le point de distribution.  

    -   **Contenu** : vous surveillez le contenu que vous déployez sur un point de distribution cloud comme lorsque vous déployez du contenu sur des points de distribution locaux.  

    -   **Service cloud** : Configuration Manager vérifie périodiquement le service Azure et émet une alerte si ce dernier est inactif ou si un problème d’abonnement ou de certificat est détecté. Vous pouvez également afficher des informations sur le point de distribution dans le nœud **Points de distribution cloud** sous **Services cloud** dans l'espace de travail **Administration** de la console Configuration Manager. À partir de cet emplacement, vous pouvez consulter les informations générales sur le point de distribution. Vous pouvez également sélectionner un point de distribution et modifier ses propriétés.  

    Quand vous modifiez les propriétés d’un point de distribution cloud, vous pouvez :  

    -   ajuster les seuils de données pour le stockage et les alertes ;  

    -   gérer le contenu comme pour un point de distribution local.  

    Enfin, pour chaque point de distribution cloud, vous pouvez afficher, sans toutefois modifier, l'ID d'abonnement, le nom du service et d'autres informations associées qui sont définies lors de l'installation de la distribution cloud.  

-   **Sauvegarde et récupération de points de distribution cloud**: quand vous utilisez un point de distribution cloud de votre hiérarchie, aidez-vous des informations suivantes pour planifier la sauvegarde ou la récupération du point de distribution :  

    -   Lorsque vous utilisez la tâche de maintenance prédéfinie **Serveur de site de sauvegarde**, Configuration Manager inclut automatiquement les configurations du point de distribution cloud.  

    -   Il est recommandé de sauvegarder et d’enregistrer une copie du certificat de gestion et du certificat de service utilisés avec un point de distribution cloud. En cas de restauration du site principal Configuration Manager qui gère le point de distribution cloud sur un autre ordinateur, vous devez réimporter les certificats pour continuer de les utiliser.  

-   **Désinstaller un point de distribution cloud** : pour désinstaller un point de distribution cloud, sélectionnez-le dans la console Configuration Manager, puis sélectionnez **Supprimer**.  

    Lorsque vous supprimez un point de distribution cloud d’une hiérarchie, Configuration Manager supprime le contenu du service cloud dans Azure.  
