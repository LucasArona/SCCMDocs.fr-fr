---
title: Sélectionner des méthodes de découverte
titleSuffix: Configuration Manager
description: Passez en revue les considérations relatives aux méthodes à utiliser et aux sites sur lesquels les exécuter.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: d3965f0df55e16fa87d259532fdc4f2f580d1253
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65501416"
---
# <a name="select-discovery-methods-to-use-for-system-center-configuration-manager"></a>Sélectionner des méthodes de découverte à utiliser pour System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Pour utiliser correctement et efficacement la découverte pour System Center Configuration Manager, vous devez prendre en compte les méthodes à utiliser et les sites sur lesquels les exécuter.  

 La découverte peut générer un volume de trafic réseau considérable, et les enregistrements de données de découverte obtenus peuvent utiliser beaucoup de ressources du processeur pendant le traitement. Vous devez donc limiter l’utilisation des méthodes de découverte à celles qui sont nécessaires pour répondre à vos objectifs. Vous pouvez commencer par n’utiliser qu’une ou deux méthodes de découverte, avant d’éventuellement en activer d’autres de manière contrôlée par la suite pour étendre le niveau de découverte dans votre environnement. Les informations fournies dans cette rubrique peuvent vous aider à prendre des décisions éclairées.  

 Pour plus d’informations sur les différentes méthodes de découverte, consultez [À propos des méthodes de découverte pour System Center Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Sélectionner des méthodes pour découvrir des choses différentes  
 Pour découvrir des ordinateurs clients Configuration Manager potentiels ou des ressources utilisateur, vous devez activer les méthodes de découverte appropriées. Vous pouvez utiliser différentes combinaisons de méthodes de découverte pour localiser différentes ressources et découvrir des informations supplémentaires sur ces ressources. Les méthodes employées déterminent le type de ressources découvertes, ainsi que les services et agents Configuration Manager utilisés dans le processus de découverte. Elles déterminent également le type d'informations concernant les ressources que vous pouvez découvrir.  

### <a name="discover-computers"></a>Détecter les ordinateurs   
Quand vous voulez découvrir des ordinateurs, vous pouvez utiliser la **Découverte de systèmes Active Directory** ou la **Découverte du réseau**.  

 Par exemple, si vous souhaitez découvrir des ressources qui peuvent installer le client Configuration Manager avant d’utiliser l’installation Push du client, vous pouvez exécuter la découverte de systèmes Active Directory. À l’aide de cette méthode, vous découvrez non seulement la ressource, mais aussi des informations de base, et même des informations étendues à partir des services de domaine Active Directory. Ces informations peuvent être utiles pour créer des requêtes et des regroupements complexes à utiliser dans l'attribution de paramètres de client ou le déploiement de contenu.

En guise d’alternative, vous pouvez exécuter la découverte du réseau et utiliser ses options pour découvrir le système d’exploitation des ressources (nécessaire pour utiliser l’installation Push du client ultérieurement). La découverte du réseau fournit des informations sur la topologie de votre réseau que vous ne pouvez pas obtenir avec d’autres méthodes de découverte. Toutefois, cette méthode ne fournit aucune information sur votre environnement Active Directory.

 Il existe également une méthode appelée **Découverte par pulsations d’inventaire**. Il est possible d’utiliser uniquement la découverte par pulsations d’inventaire pour forcer la découverte des clients que vous avez installés à l’aide de méthodes autres que l’installation Push du client. Cependant, contrairement aux autres méthodes de découverte, la découverte par pulsations d’inventaire ne peut pas découvrir des ordinateurs qui ne disposent pas d’un client Configuration Manager actif. Elle retourne un ensemble limité d’informations, destinées à tenir à jour un enregistrement de base de données existant plutôt que la base de cet enregistrement. Les informations soumises par la découverte par pulsations d'inventaire peuvent ne pas suffire à construire des requêtes ou des regroupements complexes.  

 Si vous utilisez la **découverte de groupes Active Directory** pour découvrir l’appartenance d’un groupe spécifique, vous pouvez découvrir des informations limitées sur le système ou l’ordinateur. Cela ne remplace pas une découverte complète des ordinateurs, mais peut fournir des informations de base. Ces informations sont insuffisantes pour l’installation Push du client.  

### <a name="discover-users"></a>Découvrir des utilisateurs   
Quand vous voulez découvrir des informations sur les utilisateurs, utilisez la **Découverte d’utilisateurs Active Directory**. Comme pour la découverte de systèmes Active Directory, cette méthode découvre des utilisateurs d’Active Directory. Cela comprend les informations de base, en plus des informations étendues Active Directory. Vous pouvez utiliser ces informations pour générer des requêtes et des regroupements complexes similaires à ceux des ordinateurs.  

### <a name="discover-group-information"></a>Découvrir des informations de groupe   
Quand vous voulez découvrir des informations sur les groupes et les appartenances aux groupes, utilisez la **Découverte de groupes Active Directory**. Cette méthode de découverte crée des enregistrements de ressources pour les groupes de sécurité.  

 Vous pouvez utiliser cette méthode pour rechercher un groupe spécifique d’Active Directory afin d’identifier les membres de ce groupe, ainsi que les groupes imbriqués dans ce groupe. Cette méthode permet également de rechercher des groupes dans un emplacement Active Directory et de rechercher, de manière récursive, chaque conteneur enfant de cet emplacement dans les services de domaine Active Directory.  

 Cette méthode de découverte peut également rechercher l'appartenance des groupes de distribution. Elle permet également d'identifier les relations de groupe des utilisateurs et des ordinateurs.  

 Lorsque vous découvrez un groupe, vous pouvez également découvrir des informations limitées sur ses membres. Toutefois, cela ne remplace pas les méthodes de découverte de systèmes ou d’utilisateurs Active Directory. Cela ne suffit généralement pas pour créer des requêtes et des regroupements complexes, ou pour servir de base d’une installation Push du client.  

### <a name="discover-infrastructure"></a>Découvrir l’infrastructure   
Vous pouvez appliquer deux méthodes pour découvrir l’infrastructure réseau : la **Découverte de forêts Active Directory** et la **Découverte du réseau**.  

 Utilisez la découverte de forêts Active Directory pour rechercher des informations sur les sous-réseaux et les configurations de site Active Directory dans une forêt Active Directory. Ces configurations peuvent ensuite être automatiquement entrées dans Configuration Manager en tant qu’emplacements limites.  

 Lorsque vous souhaitez découvrir la topologie de votre réseau, utilisez la découverte du réseau. Les autres méthodes de découverte retournent des informations liées aux services de domaine Active Directory et peuvent identifier l’emplacement réseau actuel d’un client, mais elles ne peuvent pas fournir d’informations d’infrastructure basées sur la topologie des sous-réseaux ou du routeur de votre réseau.  

##  <a name="bkmk_shared"></a> Les données de découverte sont partagées entre les sites  
 Une fois que Configuration Manager a ajouté des données de découverte à une base de données, elles sont rapidement partagées parmi tous les sites de la hiérarchie. Comme il n’y a généralement pas d’avantage à découvrir les mêmes informations sur plusieurs sites de votre hiérarchie, il peut être judicieux de configurer une seule instance de chaque méthode de découverte que vous utilisez, pour qu’elle s’exécute sur un seul site. Cela vaut mieux que d’exécuter plusieurs instances d’une seule méthode sur différents sites.  

 Il peut toutefois être utile, pour certains environnements, d’attribuer la même méthode de découverte à plusieurs sites, avec une configuration et une planification distinctes à chaque fois. Par exemple, quand vous utilisez la découverte du réseau, vous souhaiterez peut-être diriger chaque site pour découvrir son réseau local, au lieu d’essayer de découvrir tous les emplacements réseau sur un réseau WAN.

Si vous configurez plusieurs instances des mêmes méthodes de découverte pour qu’elles s’exécutent sur différents sites, planifiez soigneusement la configuration de chaque site. Il faut éviter que plusieurs sites découvrent les mêmes ressources de votre réseau ou d’Active Directory. Cela peut consommer de la bande passante réseau supplémentaire et créer des enregistrements DDR en double.

Le tableau suivant identifie sur quels sites vous pouvez configurer les différentes méthodes de découverte.  

|Méthode de découverte|Emplacements pris en charge|  
|----------------------|-------------------------|  
|Découverte de forêts Active Directory|Site d'administration centrale<br /><br /> Site principal|  
|Découverte de groupes Active Directory|Site principal|  
|Découverte de systèmes Active Directory|Site principal|  
|Découverte d’utilisateurs Active Directory|Site principal|  
|Découverte par pulsations d’inventaire<sup>1</sup>|Site principal|  
|Découverte du réseau|Site principal<br /><br /> Site secondaire|  

 <sup>1</sup> Les sites secondaires ne peuvent pas configurer la découverte par pulsations d’inventaire, mais peuvent recevoir l’enregistrement de données de découverte par pulsation de la part d’un client.  

 Lorsque des sites secondaires exécutent la découverte du réseau, ou reçoivent des DDR de découverte par pulsations d'inventaire, ils transfèrent le DDR par réplication basée sur les fichiers vers leur site principal parent. Ceci est dû au fait que seuls les sites principaux et les sites d’administration centrale peuvent traiter les enregistrements de données de découverte. Pour plus d’informations sur le traitement des enregistrements de données de découverte, consultez [À propos des enregistrements de données de découverte](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Éléments à prendre en compte pour différentes méthodes de découverte  
 Chaque environnement réseau et de serveur de site étant différent, il est préférable de limiter vos configurations initiales pour la découverte. Ensuite, surveillez attentivement la capacité de chaque serveur de site à traiter les données de découverte générées.  

Quand vous utilisez une méthode de découverte **Active Directory** pour les systèmes, les utilisateurs ou les groupes :  

-   Exécutez la découverte sur un site qui dispose d'une connexion réseau rapide pour vos contrôleurs de domaine.  

-   Pensez à la topologie de réplication Active Directory pour vous assurer que la découverte peut accéder aux informations les plus récentes.  

-   Pensez à l’étendue de la configuration de la découverte et limitez la découverte aux emplacements et groupes Active Directory que vous souhaitez découvrir.  

Si vous utilisez la **Découverte du réseau** :  

-   Utilisez une configuration initiale limitée pour identifier votre topographie réseau.  

-   Après avoir identifié votre topographie réseau, configurez la découverte du réseau pour qu’elle s’exécute sur des sites spécifiques, qui jouent un rôle central pour les zones du réseau que vous souhaitez découvrir plus en détail.  

Dans la mesure où la **Découverte par pulsations d’inventaire** ne s’exécute pas sur un site spécifique, vous n’avez pas besoin de prendre en compte le lieu de l’exécution dans la planification générale.  

##  <a name="bkmk_best"></a> Bonnes pratiques pour la découverte  
Pour obtenir de meilleurs résultats avec la découverte, nous vous recommandons d’effectuer les opérations suivantes :

- **Réalisez une découverte de systèmes Active Directory et une découverte d’utilisateurs Active Directory avant de procéder à une découverte de groupes Active Directory.**  

  Lorsqu'une découverte de groupes Active Directory identifie en tant que membre d'un groupe un ordinateur ou un utilisateur jusqu'alors inconnu, elle tente de découvrir les détails de base concernant cet utilisateur ou cet ordinateur. La découverte de groupes Active Directory n’étant pas optimisée pour ce type de découverte, ce processus peut provoquer un ralentissement de son exécution. Par ailleurs, la découverte de groupes Active Directory identifie uniquement les informations de base sur les utilisateurs et les ordinateurs, et ne crée pas d’enregistrement complet de découverte d’utilisateurs ou d’ordinateurs. Quand vous procédez à une découverte de systèmes Active Directory et à une découverte d’utilisateurs Active Directory, les attributs Active Directory supplémentaires de chaque type d’objet sont disponibles. Ainsi, la découverte de groupes Active Directory est plus performante.  

- **Quand vous configurez la découverte de groupes Active Directory, spécifiez uniquement les groupes que vous utilisez avec Configuration Manager.**  

  Pour mieux contrôler les ressources utilisées par le processus de découverte de groupes Active Directory, spécifiez uniquement les groupes que vous utilisez avec Configuration Manager. En effet, la découverte de groupes Active Directory recherche de manière récursive les utilisateurs, les ordinateurs et les groupes imbriqués dans chaque groupe qu'elle découvre. La recherche dans chaque groupe imbriqué peut élargir l’étendue de la découverte de groupes Active Directory et réduire les performances. En outre, quand vous configurez la découverte delta pour la découverte de groupes Active Directory, la méthode de découverte surveille les modifications apportées à chaque groupe. Les performances sont ainsi d'autant plus ralenties lorsque la méthode doit rechercher des groupes qui ne sont pas nécessaires.  

- **Configurez les méthodes de découverte de telle sorte que l’intervalle entre les découvertes complètes soit plus long et que les découvertes delta soient plus fréquentes.**  

  La découverte delta consomme moins de ressources qu’un cycle de découverte complète et peut identifier les ressources nouvelles ou modifiées dans Active Directory. Ainsi, vous pouvez réduire la fréquence des cycles de découverte complète à un par semaine (ou moins). La découverte delta de la découverte de systèmes Active Directory, de la découverte d’utilisateurs Active Directory et de la découverte de groupes Active Directory identifie presque toutes les modifications apportées aux objets Active Directory, et peut conserver des données de découverte exactes concernant les ressources.  

- **Exécutez les méthodes de découverte Active Directory sur le site principal dont l’emplacement réseau est le plus proche de votre contrôleur de domaine Active Directory.**  

  Pour améliorer les performances de la découverte Active Directory, nous vous recommandons de l’exécuter sur un site principal connecté aux contrôleurs de domaine via une connexion réseau rapide. Si vous exécutez la même méthode de découverte Active Directory sur plusieurs sites, configurez chaque méthode de découverte pour éviter les chevauchements. Contrairement aux versions antérieures de Configuration Manager, les données de découverte sont partagées parmi les sites. Ainsi, il n’est pas nécessaire de procéder à la découverte des mêmes informations sur plusieurs sites. Pour plus d’informations, consultez [Les données de découverte sont partagées entre les sites](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Procédez à une découverte de forêts Active Directory sur un seul site quand vous envisagez de créer automatiquement des limites à partir des données de découverte.**  

  Si vous effectuez une découverte de forêts Active Directory sur plusieurs sites d’une hiérarchie, nous vous recommandons d’activer les options permettant de créer automatiquement des limites uniquement sur un site. En effet, lorsqu’une découverte de forêts Active Directory est réalisée sur chaque site et crée des limites, Configuration Manager ne peut pas fusionner ces limites en un objet de limite unique. Si vous configurez la découverte de forêts Active Directory de façon à ce qu’elle crée automatiquement des limites sur plusieurs sites, vous risquez de créer des objets de limite en double dans la console Configuration Manager.  
