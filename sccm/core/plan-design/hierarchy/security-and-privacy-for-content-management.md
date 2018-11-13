---
title: Sécurité et confidentialité pour la gestion du contenu
titleSuffix: Configuration Manager
description: Optimisez la sécurité et la confidentialité pour la gestion de contenu dans Configuration Manager.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5f38b726-dc00-433a-ba05-5b7dbb0d8e99
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f24760e11dd3972c43600225eec405523988696c
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411058"
---
# <a name="security-and-privacy-for-content-management-in-configuration-manager"></a>Sécurité et confidentialité pour la gestion de contenu dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article contient des informations de sécurité et de confidentialité pour la gestion de contenu dans Configuration Manager. 



##  <a name="BKMK_Security_ContentManagement"></a> Meilleures pratiques de sécurité pour la gestion de contenu  


#### <a name="advantages-and-disadvantages-of-https-or-http-for-intranet-distribution-points"></a>Avantages et inconvénients de HTTPS ou HTTP pour les points de distribution intranet
Pour les points de distribution sur l’intranet, prenez en compte les avantages et les inconvénients de l’utilisation des protocoles HTTP et HTTPS. Dans la plupart des cas, utiliser le protocole HTTP et des comptes d'accès aux packages pour l'autorisation est plus sûr qu'utiliser le protocole HTTPS avec chiffrement mais sans autorisation. Toutefois, si des données sensibles se trouvent dans votre contenu que vous souhaitez chiffrer lors du transfert, utilisez le protocole HTTPS.  

-   **Quand vous utilisez HTTPS pour un point de distribution**, Configuration Manager n’utilise pas les comptes d’accès aux packages pour autoriser l’accès au contenu, mais le contenu est chiffré pendant son transfert sur le réseau.  

-   **Quand vous utilisez HTTP pour un point de distribution**, vous pouvez utiliser des comptes d’accès aux packages pour l’autorisation, mais le contenu n’est pas chiffré pendant son transfert sur le réseau.  

À compter de la version 1806, activez **HTTP amélioré** pour le site. Cette fonctionnalité permet aux clients d’utiliser l’authentification Azure Active Directory pour communiquer de manière sécurisée avec un point de distribution HTTP. Pour plus d’informations, consultez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http).

#### <a name="protect-the-client-authentication-certificate-file"></a>Protéger le fichier de certificat d’authentification client
Si vous utilisez un certificat d'authentification de client PKI plutôt qu'un certificat auto-signé pour le point de distribution, protégez le fichier de certificat (.pfx) avec un mot de passe fort. Si vous stockez le fichier sur le réseau, sécurisez le canal du réseau lorsque vous importez le fichier dans Configuration Manager.

Quand vous avez besoin d’un mot de passe pour importer le certificat d’authentification du client que le point de distribution utilise pour communiquer avec des points de gestion, cette configuration permet de protéger le certificat contre les utilisateurs malveillants. Utilisez la signature SMB (Server Message Block) ou IPsec entre l’emplacement réseau et le serveur de site pour empêcher une personne malveillante de falsifier le fichier de certificat.  

#### <a name="remove-the-distribution-point-role-from-the-site-server"></a>Supprimer le rôle de point de distribution du serveur de site
Par défaut, le programme d’installation de Configuration Manager installe un point de distribution sur le serveur de site. Les clients n’ont pas besoin de communiquer directement avec le serveur de site. Pour réduire la surface d’attaque, attribuez le rôle de point de distribution à d’autres systèmes de site et retirez-le du serveur de site.  

#### <a name="secure-content-at-the-package-access-level"></a>Sécuriser le contenu au niveau de l’accès aux packages
Le partage de point de distribution permet un accès en lecture à tous les utilisateurs. Pour restreindre les utilisateurs pouvant accéder au contenu, utilisez les comptes d'accès aux packages lorsque le point de distribution est configuré pour le protocole HTTP. Cette configuration ne s’applique pas aux points de distribution cloud, qui ne prennent pas en charge les comptes d’accès aux packages. Pour plus d’informations, consultez [Comptes d’accès aux packages](/sccm/core/plan-design/hierarchy/accounts#package-access-account).

#### <a name="configure-iis-on-the-distribution-point-role"></a>Configurer IIS sur le rôle de point de distribution
Si Configuration Manager installe IIS quand vous ajoutez un rôle de système de site du point de distribution, supprimez la redirection HTTP ou les scripts et outils de gestion IIS une fois l’installation du point de distribution terminée. Le point de distribution ne nécessite pas la redirection HTTP ou les scripts et outils de gestion IIS. Pour réduire la surface d’attaque, supprimez ces services de rôle pour le rôle de serveur Web.  Pour plus d’informations sur les services de rôle pour le rôle de serveur web pour les points de distribution, consultez [Prérequis des sites et systèmes de site](/sccm/core/plan-design/configs/site-and-site-system-prerequisites).  

#### <a name="set-package-access-permissions-when-you-create-the-package"></a>Définir des autorisations d'accès aux packages lors de la création du package
Comme les modifications apportées aux comptes d'accès sur les fichiers de package ne sont mises en place qu'une fois que le package a été redistribué, paramétrez les autorisations d'accès au package avec précaution lorsque vous créez le package pour la première fois. Cette configuration est importante quand le package est volumineux ou distribué à de nombreux points de distribution, et quand la capacité de la bande passante réseau pour la distribution de contenu est limitée.  

#### <a name="implement-access-controls-to-protect-media-that-contains-prestaged-content"></a>Implémenter des contrôles d'accès pour protéger les supports qui contiennent le contenu préparé
Le contenu préparé est compressé mais n'est pas chiffré. Une personne malveillante pourrait lire et modifier les fichiers qui sont téléchargés vers des appareils. Les clients Configuration Manager rejettent le contenu qui a été falsifié, mais ils le téléchargent malgré tout.  

#### <a name="import-prestaged-content-with-extractcontent"></a>Importer du contenu préparé avec ExtractContent
Importez du contenu préparé uniquement à l’aide de l’outil en ligne de commande ExtractContent.exe. Pour éviter toute falsification et une élévation de privilèges, n’utilisez que l’outil en ligne de commande fourni avec Configuration Manager.  

#### <a name="secure-the-communication-channel-between-the-site-server-and-the-package-source-location"></a>Sécuriser le canal de communication entre le serveur de site et l'emplacement source du package
Utilisez une signature SMB ou IPsec entre le serveur de site et l’emplacement source du package quand vous créez des applications et des packages. Cette configuration permet d’empêcher une personne malveillante de falsifier les fichiers sources.  

#### <a name="remove-default-virtual-directories-for-custom-website-with-the-distribution-point-role"></a>Supprimer les répertoires virtuels par défaut pour le site web personnalisé avec le rôle de point de distribution
Si vous changez l’option de configuration du site pour utiliser un site web personnalisé plutôt que le site web par défaut après l’installation d’un rôle de point de distribution, supprimez les répertoires virtuels par défaut. Quand vous passez du site web par défaut à un site web personnalisé, Configuration Manager ne supprime pas les anciens répertoires virtuels. Supprimez les répertoires virtuels suivants que Configuration Manager a créés initialement sous le site web par défaut :  

-   SMS_DP_SMSPKG$  

-   SMS_DP_SMSSIG$  

-   NOCERT_SMS_DP_SMSPKG$  

-   NOCERT_SMS_DP_SMSSIG$  


#### <a name="for-cloud-distribution-points-protect-your-azure-subscription-details-and-certificates"></a>Pour les points de distribution cloud, protéger vos informations d’abonnement Azure et vos certificats
Quand vous utilisez des points de distribution cloud, protégez les éléments particulièrement importants suivants :
- Le nom d’utilisateur et le mot de passe de votre abonnement Azure
- Le certificat de gestion Azure 
- Le certificat du service du point de distribution cloud

Stockez les certificats de manière sécurisée. Si vous y accédez via le réseau lors de la configuration du point de distribution cloud, utilisez la signature SMB ou IPsec entre le serveur de système de site et l’emplacement source.  

#### <a name="for-service-continuity-monitor-the-expiry-date-of-the-cloud-distribution-point-certificates"></a>Pour garantir la continuité du service, superviser la date d’expiration des certificats de point de distribution cloud
Configuration Manager ne vous avertit pas quand les certificats importés pour le point de distribution cloud sont sur le point d’expirer. Supervisez les dates d’expiration indépendamment de Configuration Manager. Pensez à renouveler puis à importer le nouveau certificat avant la date d’expiration. Cette action est importante si vous faites l’acquisition un certificat d’authentification serveur auprès d’un fournisseur public externe, car l’acquisition d’un certificat renouvelé peut prendre plus de temps.  

 En cas d’expiration d’un certificat, le Gestionnaire de services cloud génère l’ID de message d’état **9425**. Le fichier CloudMgr.log contient une entrée pour indiquer que le certificat **est dans l’état Expiré**, avec la date d’expiration également exprimée au format UTC.  



## <a name="security-considerations-for-content-management"></a>Considérations de sécurité pour la gestion de contenu  

Tenez compte des points suivants au moment de planifier la gestion de contenu :  

-   Les clients ne valident pas le contenu jusqu’au téléchargement de celui-ci.  

     Les clients Configuration Manager ne valident le hachage du contenu qu’après le téléchargement de celui-ci dans leur cache client. Si un individu mal intentionné falsifie la liste des fichiers à télécharger ou le contenu lui-même, le processus de téléchargement peut consommer une quantité importante de bande passante réseau pour que le client supprime ensuite le contenu quand il rencontre le hachage non valide.  

-   Quand vous utilisez des points de distribution cloud, l’accès au contenu est automatiquement limité à votre entreprise. Vous ne pouvez pas le limiter de façon plus précise en sélectionnant des utilisateurs ou des groupes.  

-   Quand vous utilisez des points de distribution cloud, les clients sont authentifiés par le point de gestion, puis ils utilisent un jeton Configuration Manager pour accéder aux points de distribution cloud. Le jeton reste valide pendant huit heures. Ce comportement signifie que si vous bloquez un client parce qu’il n’est plus approuvé, il peut continuer à télécharger du contenu à partir d’un point de distribution cloud jusqu’à la fin de la période de validité de ce jeton. À ce stade, le point de gestion n’émettra pas d’autre jeton pour le client, puisque celui-ci aura été bloqué.  

     Pour empêcher un client bloqué de télécharger du contenu pendant cette période de huit heures, arrêtez le service de cloud. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Points de distribution cloud**.  



##  <a name="BKMK_Privacy_ContentManagement"></a> Informations de confidentialité pour la gestion de contenu  

 Configuration Manager n’inclut pas de données utilisateur dans les fichiers de contenu, même si un utilisateur administratif peut choisir d’effectuer cette action.  



## <a name="see-also"></a>Voir aussi

- [Concepts fondamentaux de la gestion de contenu](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management)  

- [Sécurité et confidentialité pour la gestion des applications](/sccm/apps/plan-design/security-and-privacy-for-application-management)  

- [Sécurité et confidentialité pour les mises à jour logicielles](/sccm/sum/plan-design/security-and-privacy-for-software-updates)  

- [Sécurité et confidentialité pour le déploiement de système d’exploitation](/sccm/osd/plan-design/security-and-privacy-for-operating-system-deployment)  