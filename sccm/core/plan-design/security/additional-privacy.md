---
title: Déclaration de confidentialité - Informations supplémentaires
titleSuffix: Configuration Manager
description: Découvrez comment Microsoft collecte et utilise les données provenant de System Center Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 1fcc921f-085f-4b0b-9c53-1e0707211076
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e98afcbc4215d3157a361eb35b9df54223df97e0
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32339302"
---
# <a name="additional-information-about-privacy-for-system-center-configuration-manager"></a>Informations supplémentaires sur la confidentialité pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="updates-and-servicing"></a>Mises à jour et maintenance
System Center Configuration Manager introduit un nouveau modèle de mise à jour qui vous aide à maintenir à jour votre déploiement actuel de Configuration Manager avec les dernières mises à jour et fonctionnalités. Une fois installée, cette fonctionnalité ajoute un nouveau rôle de système de site qui est appelé point de connexion de service sur un serveur de site choisi par un administrateur. Pour en savoir plus sur les informations collectées et sur leur utilisation, consultez la section Données d’utilisation dans cet article.


## <a name="usage-data"></a>Données d’utilisation
System Center Configuration Manager collecte les données d’utilisation et de diagnostic sur lui-même. Microsoft utilise ensuite ces données pour améliorer le processus d’installation, la qualité et la sécurité des versions ultérieures.
Des données d’utilisation et de diagnostic sont collectées pour chaque hiérarchie System Center Configuration Manager. Elle consistent en requêtes SQL Server qui s’exécutent chaque semaine sur chaque site principal et sur le site d’administration centrale. Quand la hiérarchie utilise un site d’administration centrale, les données provenant des sites principaux sont répliquées sur ce site. Sur le site de niveau supérieur de votre hiérarchie, le point de connexion de service soumet ces informations quand il recherche des mises à jour. Si le point de connexion de service est en mode hors connexion, les informations sont transférées à l’aide de l’outil de connexion de service.

Configuration Manager collecte uniquement les données de la base de données SQL Server des sites. Il ne collecte pas de données directement à partir des clients ni des serveurs de site.

Les administrateurs peuvent modifier le niveau des données collectées en accédant à la section **Données d’utilisation** de la console Configuration Manager.

Pour plus d’informations, consultez les articles « En savoir plus » sur les niveaux et les paramètres des données d’utilisation mentionnés dans l’article [Données d’utilisation et de diagnostic pour System Center Configuration Manager](https://go.microsoft.com/fwlink/?LinkID=626566).


## <a name="customer-experience-improvement-program"></a>Programme d'amélioration de l'expérience utilisateur

> [!Note]  
> À compter de Configuration Manager version 1802, la fonctionnalité CEIP ne figure plus dans le produit.

Le programme d’amélioration de l’expérience utilisateur (CEIP) collecte des informations de base à partir de la console Configuration Manager sur votre configuration matérielle, et sur votre utilisation de nos logiciels et services afin d’identifier des tendances et des modèles d’utilisation. Le programme CEIP collecte également le type et le nombre d’erreurs rencontrées, les performances logicielles et matérielles, et la rapidité des services. Nous ne collectons pas votre nom, votre adresse ni d’autres informations de contact. Aucune donnée CEIP n'est collectée à partir des ordinateurs des clients.

Les informations recueillies sont utilisées pour améliorer la qualité, la fiabilité et les performances des produits et services Microsoft.

Pour plus d’informations sur les informations collectées, traitées et transmises par le programme d’amélioration de l’expérience utilisateur (CEIP), consultez la [Déclaration de confidentialité pour le programme d’amélioration de l’expérience utilisateur de Microsoft](https://go.microsoft.com/fwlink/?LinkID=525211).

## <a name="operations-management-suite-connector"></a>Connecteur Operations Management Suite
Le connecteur Microsoft Operations Management Suite synchronise les données, comme les regroupements, de System Center Configuration Manager vers Microsoft Operations Management Suite. L’ID et la clé secrète de l’abonnement Microsoft Azure sont stockés dans la base de données Configuration Manager quand un administrateur configure la fonctionnalité. La clé secrète du client Azure Active Directory et la clé partagée de l’espace de travail Microsoft Operations Management Suite sont stockées dans la base de données locale de System Center Configuration Manager. Toutes les communications entre System Center Configuration Manager et Microsoft Operations Management Suite utilisent HTTPS. Aucune information supplémentaire sur les regroupements n’est fournie à Microsoft en dehors de données de télémétrie aléatoires. Pour plus d’informations sur les informations collectées par Microsoft Operations Management Suite, consultez [Sécurité des données Log Analytics](https://go.microsoft.com/fwlink/?LinkId=823545).

## <a name="asset-intelligence"></a>Asset Intelligence
Asset Intelligence permet aux administrateurs informatiques de définir, de suivre et de gérer de façon proactive la conformité à des normes de configuration. La mesure et les rapports concernant le déploiement et l'utilisation des applications physiques et virtuelles permettent aux entreprises de prendre de meilleures décisions au sujet des licences de logiciel et de tenir à jour la conformité aux accords de licence. Une fois les données d’utilisation des clients Configuration Manager collectées, les administrateurs peuvent utiliser différentes fonctionnalités pour afficher les données, notamment les regroupements, les requêtes et les rapports.

Lors de chaque synchronisation, un catalogue des logiciels connus est téléchargé à partir de Microsoft. Les administrateurs informatiques peuvent choisir d’envoyer à Microsoft des informations sur les titres de logiciels sans catégorie découverts au sein de leur organisation pour y effectuer des recherches et les ajouter au catalogue. Avant le chargement de ces informations, une boîte de dialogue montre les données qui vont être chargées. Les données téléchargées ne peuvent pas être rappelées. Asset Intelligence n'envoie pas d'informations sur les utilisateurs, les ordinateurs ou l'utilisation des licences à Microsoft.

Une fois qu’un titre de logiciel est chargé, les chercheurs de Microsoft l’identifient, le classent, puis le mettent à la disposition de tous les autres clients qui utilisent cette fonctionnalité et d’autres utilisateurs du catalogue. Tout titre de logiciel chargé devient public. L’application et sa classification font alors partie du catalogue et peuvent ensuite être téléchargées par d’autres utilisateurs du catalogue. Avant de configurer le regroupement de données Asset Intelligence et de décider de soumettre des informations à Microsoft, pensez aux besoins de votre organisation en matière de confidentialité.

Asset Intelligence n’est pas activé dans System Center Configuration Manager par défaut. Le téléchargement de titres sans catégorie ne se produit jamais automatiquement et le système n'est pas conçu pour que cette tâche soit automatisée. Vous devez sélectionner et approuver manuellement le téléchargement de chaque nom de logiciel.

## <a name="endpoint-protection"></a>Endpoint Protection
Microsoft Cloud Protection Service s’appelait auparavant Microsoft Active Protection Service ou MAPS.
Les produits applicables sont Microsoft Cloud Protection Service et la fonctionnalité Endpoint Protection de System Center Configuration Manager (pour la gestion de System Center Endpoint Protection et de Windows Defender pour Windows 10). Cette fonctionnalité n’est pas implémentée pour System Center Endpoint Protection pour Linux ni System Center Endpoint Protection pour Mac.

La communauté anti-programme malveillant de Microsoft Cloud Protection Service est une communauté en ligne internationale bénévole qui rassemble les utilisateurs de System Center Endpoint Protection. Quand vous vous joignez à Microsoft Cloud Protection Service, System Center Endpoint Protection envoie automatiquement des informations à Microsoft. Microsoft utilise les informations pour déterminer les logiciels où rechercher d’éventuelles menaces et pour améliorer l’efficacité de System Center Endpoint Protection. Cette communauté contribue à limiter la portée des infections des nouveaux logiciels malveillants. Si un rapport Microsoft Cloud Protection Service inclut des détails sur des logiciels malveillants ou potentiellement non désirés que le client Endpoint Protection peut supprimer, Microsoft Cloud Protection Service télécharge la signature la plus récente pour y procéder. Microsoft Cloud Protection Service peut également rechercher de « faux positifs » (un élément initialement identifié comme logiciel malveillant mais qui ne l’est pas) et les corriger.

Les rapports Microsoft Cloud Protection Service contiennent des informations sur les fichiers des logiciels malveillants potentiels, comme les noms de fichiers, le hachage de chiffrement, le fournisseur, la taille et les horodatages. Par ailleurs, Microsoft Cloud Protection Service peut collecter des URL complètes pour indiquer l’origine du fichier. Ces URL contiennent parfois des informations personnelles, comme des termes de recherche ou des données entrées dans des formulaires. Les rapports peuvent également inclure les actions que vous avez effectuées quand Endpoint Protection vous a informé sur des logiciels indésirables. Les rapports Microsoft Cloud Protection Service incluent ces informations pour aider Microsoft à évaluer l’efficacité avec laquelle Endpoint Protection peut détecter et supprimer des programmes malveillants et potentiellement indésirables et pour tenter d’identifier les nouveaux logiciels malveillants.

Vous pouvez adhérer à Microsoft Cloud Protection Service si vous avez un abonnement de base ou avancé. Les rapports des abonnés de base contiennent les informations décrites ci-dessus. Les rapports des abonnés avancés sont plus complets et peuvent contenir des informations complémentaires sur les logiciels détectés par Endpoint Protection, notamment l’emplacement, le nom des fichiers, le mode de fonctionnement du logiciel et l’incidence sur votre ordinateur. Ces rapports, ainsi que ceux des autres utilisateurs d’Endpoint Protection qui participent à Microsoft Cloud Protection Service, aident les chercheurs de Microsoft à découvrir les nouvelles menaces plus rapidement. Les définitions des programmes malveillants sont ensuite créées pour les programmes qui répondent aux critères d'analyse et les définitions actualisées sont rendues disponibles à tous les utilisateurs via Microsoft Update.

Pour vous aider à détecter et résoudre certains types d’infections de logiciels malveillants, le produit envoie régulièrement à Microsoft Cloud Protection Service des informations sur l’état de sécurité de votre ordinateur. Ces informations comprennent des informations sur les paramètres de sécurité et les fichiers journaux de votre ordinateur qui décrivent les pilotes et autres logiciels qui se chargent pendant que votre ordinateur démarre.
Un numéro qui identifie de façon unique votre PC est également envoyé. De plus, Microsoft Cloud Protection Service peut collecter les adresses IP auxquelles les fichiers de programmes malveillants potentiels se connectent.

Les rapports Microsoft Cloud Protection Service sont utilisés pour améliorer les logiciels et services Microsoft. Ils peuvent également servir à des fins de statistique, de test ou d’analyse, et pour générer des définitions. Seuls les employés, les prestataires, les sous-traitants, les partenaires et les fournisseurs de Microsoft qui ont besoin d’utiliser les rapports dans le cadre de leurs activités professionnelles y ont accès.

Microsoft Cloud Protection Service ne collecte pas intentionnellement des informations personnelles. Dans la mesure où Microsoft Cloud Protection Service collecte des informations personnelles, Microsoft ne les utilise pas pour vous identifier ou vous contacter.

Vous pouvez trouver des informations supplémentaires sur les données collectées dans la documentation du produit, dans [Endpoint Protection dans System Center Configuration Manager](https://go.microsoft.com/fwlink/?LinkId=823547).

## <a name="site-hierarchy--geographical-view-with-bing-maps"></a>Hiérarchie de site : vue géographique avec cartes Bing
Hiérarchie de site : la vue géographique vous permet d’utiliser des cartes fournies par Microsoft Bing Maps pour afficher la topologie des serveurs physiques de Configuration Manager. Pour activer cette fonctionnalité, les informations d’emplacement que vous fournissez sont envoyées depuis votre serveur au service web Bing Maps.

Microsoft utilise les informations pour exploiter et améliorer les cartes Microsoft Bing et autres sites et services Microsoft. Pour plus d’informations, consultez la [Déclaration de confidentialité de Microsoft](https://go.microsoft.com/fwlink/?LinkId=823548).
Vous pouvez choisir de ne pas utiliser la vue géographique pour la hiérarchie du site. La vue Diagramme de la hiérarchie vous permet d’afficher la hiérarchie ; elle n’utilise pas le service Bing Maps.

## <a name="microsoft-intune-subscription"></a>Abonnement Microsoft Intune
Les clients qui ont souscrit un abonnement à Microsoft Intune peuvent utiliser Configuration Manager pour gérer leurs appareils mobiles connectés via Microsoft Intune. La [déclaration de confidentialité des Services en ligne de Microsoft](https://go.microsoft.com/fwlink/?LinkId=262214) s’applique à Microsoft Online Services, qui inclut Microsoft Intune. Si les clients possèdent également un abonnement à Microsoft Intune, la [déclaration de confidentialité Microsoft Online Services](https://go.microsoft.com/fwlink/?LinkId=262214) doit être lue conjointement avec la présente déclaration de confidentialité.

Toutes les communications avec Microsoft Intune utilisent le protocole HTTPS. Pour configurer l’abonnement à Microsoft Intune et télécharger la Demande de signature de certificat (DSC) qui est nécessaire à la configuration de la prise en charge d’iOS, un administrateur doit se connecter à Microsoft Intune en utilisant son compte et son mot de passe professionnels. Ces informations d'identification ne sont pas stockées dans Configuration Manager. Toutes les autres communications avec Microsoft Intune sont authentifiées à l’aide de certificats PKI qui sont générés automatiquement par Microsoft Intune.

Pour gérer les appareils connectés à Microsoft Intune, certaines informations sont envoyées à et reçues de Microsoft Intune. Ces informations incluent le nom principal de l’utilisateur (UPN) de tous les utilisateurs qui sont affectés au service et les informations d’inventaire d’appareils pour les appareils qui sont gérés par Microsoft Intune. Des métadonnées, comme le nom, l’éditeur et la version de l’application, pour le contenu qui est affecté aux points de distribution Manage.Microsoft.com sont envoyées à Microsoft Intune. Le contenu binaire réel affecté à un point de distribution Manage.Microsoft.com est chiffré avant son chargement vers Microsoft Intune.

Cette fonction n'est pas configurée par défaut. Les administrateurs contrôlent le contenu qui est transféré vers le point de distribution Manage.Microsoft.com et les utilisateurs qui sont affectés au service. La fonctionnalité peut être supprimée à tout moment.
