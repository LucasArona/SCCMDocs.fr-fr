---
title: Introduction
titleSuffix: Configuration Manager
description: Obtenez des informations de base faisant office de présentation de System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 3343eccf-bf09-41cd-9e68-03e893c7f904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f0986d713b47d15dc0298e413216a1e33fe2e937
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="introduction-to-system-center-configuration-manager"></a>Présentation de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Produit de la suite Microsoft System Center de solutions de gestion, System Center Configuration Manager peut vous aider à gérer les appareils et les utilisateurs localement et dans le cloud.  

**Configuration Manager peut vous aider à :**   
-   améliorer la productivité et l’efficacité de vos services informatiques en réduisant les tâches manuelles et en vous permettant de vous concentrer sur des projets à forte valeur ;  
-   optimiser les investissements matériels et logiciels ;  
-   maîtriser la productivité des utilisateurs en leur fournissant les bons logiciels au bon moment.  

**Configuration Manager vous permet d’offrir des services informatiques plus efficaces en prenant en charge :**  

-   Le déploiement de logiciels sécurisés et scalables.  
-   La gestion des paramètres de conformité.  
-   La gestion complète des ressources des serveurs, ordinateurs de bureau, ordinateurs portables et appareils mobiles.  

**Configuration Manager s'étend et fonctionne avec vos solutions et technologies Microsoft existantes.**  

Par exemple, Configuration Manager s’intègre aux éléments suivants :  

-   Microsoft Intune, pour gérer un vaste éventail de plateformes d’appareils mobiles.  
-   Windows Server Update Services (WSUS), pour gérer les mises à jour logicielles.  
-   Services de certificats.  
-   Exchange Server et Exchange Online.  
-   Stratégie de groupe Windows (GPO)
-   DNS.   
-   Kit de déploiement et d’évaluation Windows (Windows ADK) et outil de migration utilisateur (USMT).  
-   Services de déploiement Windows (WDS).  
-   Assistance à distance et Bureau à distance.  

Configuration Manager utilise également :  

-   Les services de domaine Active Directory pour la sécurité, l’emplacement du service, la configuration et pour découvrir les utilisateurs et les appareils que vous souhaitez gérer.  
-   Microsoft SQL Server comme base de données de gestion des modifications distribuée, qui s’intègre à SQL Server Reporting Services (SSRS) pour créer des rapports de surveillance et de suivi des activités de gestion.  
-   Des rôles de système de site qui étendent les fonctionnalités de gestion et l’utilisation des services web d’IIS (Internet Information Services).
-   Le service de transfert intelligent en arrière-plan (BITS) et BranchCache pour gérer la bande passante réseau disponible.  

Pour réussir avec Configuration Manager, vous devez d'abord soigneusement planifier et tester les fonctionnalités de gestion avant d'utiliser Configuration Manager dans un environnement de production. En tant qu'application de gestion performante, Configuration Manager est susceptible d'affecter tous les ordinateurs de votre organisation. Lorsque Configuration Manager est déployé et géré avec une planification minutieuse prenant en compte les exigences de votre entreprise, Configuration Manager peut réduire les frais administratifs généraux ainsi que le coût total de possession.  

Utilisez les rubriques suivantes et les autres sections de cette rubrique pour en savoir plus sur Configuration Manager.  


**Rubriques connexes dans la bibliothèque de documents :**  

-   [Fonctions et fonctionnalités de System Center Configuration Manager](../../core/plan-design/changes/features-and-capabilities.md)  
-   [Choisir une solution de gestion d’appareils pour System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  
-   [Ce qui a changé dans System Center Configuration Manager par rapport à System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md)
-   [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md)  
-   [Évaluer System Center Configuration Manager en créant votre propre environnement lab](/sccm/core/get-started/set-up-your-lab)
-   [Trouver de l’aide pour l’utilisation de System Center Configuration Manager](../../core/understand/find-help.md)  
-   [Éléments supprimés et dépréciés dans System Center Configuration Manager](../../core/plan-design/changes/deprecated/removed-and-deprecated.md)  

##  <a name="BKMK_Console"></a> Console Configuration Manager  
 Après l'installation de Configuration Manager, utilisez la console Configuration Manager pour configurer les sites et les clients, ainsi que pour exécuter et surveiller les tâches de gestion. Cette console est le principal point d'administration et vous permet de gérer plusieurs sites.  

 Elle peut également exécuter des consoles secondaires pour prendre en charge des tâches spécifiques de gestion de client. Par exemple :  

-   l’**Explorateur de ressources**pour afficher des informations sur la parc matériel et logiciel ;  
-   le**Contrôle à distance** pour se connecter à distance à un ordinateur client afin d’effectuer des tâches de dépannage.  

Vous pouvez installer la console Configuration Manager sur des ordinateurs supplémentaires, ainsi que restreindre l’accès et limiter ce que les utilisateurs administratifs voient dans la console à l’aide de l'administration basée sur des rôles de Configuration Manager.  

Pour plus d’informations, consultez [Installer des consoles System Center Configuration Manager](../../core/servers/deploy/install/install-consoles.md).

##  <a name="BKMK_ApplicationCatalog"></a> Le catalogue d'applications, le centre logiciel et le portail d'entreprise  
 Le **catalogue d’applications** est un site web sur lequel les utilisateurs peuvent rechercher et demander des logiciels pour leurs PC Windows. Pour utiliser le catalogue d'applications, vous devez installer le point de service Web du catalogue d'applications et le point de site Web du catalogue d'applications pour le site.  

 Le**Centre logiciel** est une application installée quand le client Configuration Manager est installé sur des ordinateurs Windows. Les utilisateurs exécutent cette application pour demander des logiciels et gérer les logiciels que Configuration Manager déploie à leur intention. Le Centre logiciel permet aux utilisateurs d'effectuer les opérations suivantes :  

-   rechercher et installer des logiciels à partir du catalogue d'applications ;  
-   afficher leur historique de demande de logiciels ;  
-   configurer à quel moment Configuration Manager peut installer des logiciels sur leurs équipements ;  
-   configurer les paramètres d'accès pour le contrôle à distance, si un utilisateur administratif a activé le contrôle à distance.  

**Le portail d’entreprise** est une application ou un site web qui offre des fonctions similaires au catalogue d’applications, mais pour les appareils mobiles qui sont inscrits par Windows Intune.  

Pour plus d’informations, consultez [Présentation de la gestion d’applications dans System Center Configuration Manager](../../apps/understand/introduction-to-application-management.md).  

###  <a name="BKMK_Client"></a> Propriétés de Configuration Manager (sur les PC Windows)  
 Lorsque le client Configuration Manager est installé sur les ordinateurs Windows, Configuration Manager est installé dans le Panneau de configuration. En règle générale, vous n’avez pas à configurer cette application, car la configuration du client est effectuée dans la console Configuration Manager. Cette application aide les utilisateurs administratifs et le support technique à résoudre les problèmes avec des clients individuels.  

 Pour plus d’informations sur le déploiement de clients, consultez [Méthodes d’installation du client dans System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md).  

##  <a name="BKMK_ExampleScenarios"></a> Exemples de scénarios de Configuration Manager  
 Les exemples de scénarios suivants montrent comment une entreprise nommée Trey Research utilise Configuration Manager pour permettre aux utilisateurs :  

-   d’être plus productifs ;  
-   d’unifier la gestion de la conformité des appareils pour rationaliser les tâches d’administration ;
-   de simplifier la gestion des appareils pour réduire les coûts d’exploitation informatiques.  

Dans tous les scénarios, Adam est l'administrateur principal de Configuration Manager.  

###  <a name="BKMK_ScenarioEmpower"></a> Exemple de scénario : donner aux utilisateurs plus d’autonomie en permettant l’accès aux applications à partir de tous les appareils  
 Trey Research veut s’assurer que les employés peuvent accéder aux applications dont ils ont besoin, et aussi efficacement que possible. Adam applique ces spécifications de l'entreprise aux scénarios suivants :  

|Exigence|État actuel de la gestion du client|État futur de la gestion du client|  
|-----------------|-------------------------------------|------------------------------------|  
|Les nouveaux employés peuvent travailler efficacement dès le premier jour.|Quand les employés intègrent l’entreprise et qu’ils ouvrent une session pour la première fois sur leur ordinateur, ils doivent attendre que les applications soient installées.|Quand les employés intègrent l’entreprise, ils ouvrent une session et voient leurs applications installées et prêtes à l’emploi sur leur ordinateur.|  
|Les employés peuvent demander rapidement et facilement les logiciels supplémentaires dont ils ont besoin.|Quand les employés ont besoin d’autres applications, ils envoient une demande au support technique. Ils attendent en général deux jours avant que la demande soit traitée et que les applications soient installées.|Quand les employés ont besoin d’autres applications, ils peuvent les demander à partir d’un site web. Ils peuvent ensuite les installer immédiatement en l’absence de restrictions de licences. S'il existe des restrictions de licences, les utilisateurs doivent tout d'abord demander l'approbation avant d'installer l'application.<br /><br /> Le site web présente aux utilisateurs uniquement les applications qu’ils sont autorisés à installer.|  
|Les employés peuvent utiliser leurs appareils mobiles au travail si ces appareils sont conformes aux stratégies de sécurité qui sont surveillées et appliquées.<br /><br /> Ces stratégies incluent l’application d’un mot de passe fort, le verrouillage d’un appareil après une période d’inactivité et la réinitialisation à distance d’appareils perdus ou volés.|Les employés connectent leurs appareils mobiles au serveur Exchange Server pour accéder au service de messagerie. Toutefois, les rapports de confirmation de la conformité avec les stratégies de sécurité sont limités dans les stratégies de boîte aux lettres ActiveSync Exchange par défaut. L'utilisation personnelle des appareils mobiles risque d'être interdite si le service informatique ne peut pas confirmer le respect de la stratégie.|Le service informatique peut confirmer la compatibilité de la sécurité de l'appareil mobile avec les paramètres requis. Cette confirmation permet aux utilisateurs de continuer à utiliser leur appareil mobile au travail. Les utilisateurs peuvent réinitialiser leur appareil mobile à distance en cas de perte ou de vol, et le support technique peut réinitialiser tout appareil mobile d’utilisateur qui a été signalé comme perdu ou volé.<br /><br /> Il est recommandé de fournir l'inscription des appareils mobiles dans un environnement d'infrastructure à clés publiques pour plus de contrôle et de sécurité.|  
|Les employés peuvent être productifs même s’ils ne sont pas à leur bureau.|Quand les employés ne sont pas à leur bureau et n’ont pas d’ordinateurs portables, ils ne peuvent pas accéder à leurs applications via les ordinateurs publics disponibles dans l’entreprise.|Les employés peuvent utiliser des ordinateurs publics pour accéder à leurs applications et données.|  
|En général, la pérennité des activités est prioritaire sur l'installation des applications et des mises à jour logicielles requises.|Les applications et les mises à jour logicielles requises sont installées pendant la journée, ce qui perturbe fréquemment le travail des utilisateurs dans la mesure où leurs ordinateurs ralentissent ou redémarrent au cours de l'installation.|Les utilisateurs peuvent définir leurs heures de travail pour empêcher l’installation des logiciels obligatoires pendant qu’ils utilisent leur ordinateur.|  

 Pour répondre aux conditions requises, Adam utilise les fonctionnalités de gestion et les options de configuration de Configuration Manager suivantes :  

-   Gestion des applications  
-   Gestion des appareils mobiles  

Il implémente ces fonctionnalités en effectuant les étapes de configuration décrites dans le tableau suivant :  

|Étapes de configuration|Résultat|  
|-------------------------|-------------|  
|Adam vérifie que les nouveaux utilisateurs ont des comptes d’utilisateur dans Active Directory, puis il crée un regroupement basé sur des requêtes dans Configuration Manager pour ces utilisateurs. Il définit ensuite l'affinité entre appareil et utilisateur pour ces utilisateurs en créant un fichier de mappage des comptes d'utilisateur aux ordinateurs principaux qui seront utilisés, et il importe ce fichier dans Configuration Manager.<br /><br /> Les applications dont les nouveaux utilisateurs ont besoin sont déjà créées dans Configuration Manager. Adam déploie ensuite les applications ayant l’objectif Obligatoire dans le regroupement qui contient les nouveaux utilisateurs.|En raison des informations relatives à l’affinité entre appareil et utilisateur, les applications sont installées sur l’ordinateur principal ou les ordinateurs de chaque utilisateur avant l’ouverture d’une session utilisateur.<br /><br /> L’utilisateur peut utiliser les applications aussitôt après avoir ouvert une session.|  
|Adam installe et configure les rôles de système de site du catalogue des applications pour permettre aux utilisateurs de rechercher les applications à installer. Il crée des déploiements d'applications dont l'objet est Disponible, puis il déploie ces applications sur le regroupement qui contient les nouveaux utilisateurs.<br /><br /> Dans le cas d'applications dont le nombre de licences est limité, Adam les configure pour en demander l'approbation.|Les utilisateurs peuvent maintenant accéder au catalogue des applications pour rechercher les applications qu’ils sont autorisés à installer. Ils peuvent ensuite installer les applications immédiatement, ou envoyer une demande d’approbation et revenir au catalogue des applications pour les installer une fois que le support technique a approuvé leur demande.|  
|Adam crée un connecteur Exchange Server dans Configuration Manager pour gérer les appareils mobiles qui se connectent au serveur Exchange Server local de l'entreprise. Il configure ce connecteur avec les paramètres de sécurité qui exigent de définir un mot de passe fort et de verrouiller l’appareil mobile après une période d’inactivité.<br /><br /> Pour gérer en plus les appareils exécutant Windows Phone 8, Windows RT et iOS, Adam prend un abonnement à Microsoft Intune. Il installe ensuite le rôle de système de site de point de connexion de service. Cette solution de gestion d'appareil mobile fournit à l'entreprise une meilleure prise en charge de la gestion de ces appareils. Cela inclut la mise des applications à la disposition des utilisateurs pour l’installation sur ces appareils, ainsi que la gestion étendue des paramètres. De plus, les connexions d'appareils mobiles sont sécurisées à l'aide de certificats PKI qui sont automatiquement créés et déployés par Intune.<br /><br /> Après avoir configuré le point de connexion de service et l’abonnement à utiliser avec Configuration Manager, Adam envoie un e-mail aux utilisateurs de ces appareils mobiles, avec un lien leur permettant de démarrer le processus d’inscription.<br /><br /> Pour inscrire les appareils mobiles auprès de Microsoft Intune, Adam utilise des paramètres de compatibilité afin de configurer des paramètres de sécurité pour ces appareils mobiles. Ces paramètres exigent la définition d’un mot de passe fort et le verrouillage de l’appareil mobile après une période d’inactivité.|Ces deux solutions de gestion des appareils mobiles permettent maintenant au service informatique de fournir des informations de rapport relatives aux appareils mobiles qui sont utilisés sur le réseau de l'entreprise et à leur compatibilité avec les paramètres de sécurité configurés.<br /><br /> Les utilisateurs apprennent à réinitialiser leur appareil mobile à distance à partir du catalogue des applications ou du portail d’entreprise s’ils perdent ou se font voler leur appareil mobile. Les membres du support technique apprennent également à réinitialiser à distance les appareils mobiles des utilisateurs à l'aide de la console Configuration Manager.<br /><br /> De plus, pour les appareils mobiles inscrits auprès de Microsoft Intune, Adam peut maintenant déployer des applications mobiles que les utilisateurs peuvent installer, collecter plus de données d'inventaire à partir de ces appareils et mieux contrôler la gestion des appareils en accédant à d'autres paramètres.|  
|Trey Research dispose de plusieurs ordinateurs publics, utilisés par les employés visitant les bureaux. Les employés veulent pouvoir utiliser leurs applications de n’importe quel endroit. Toutefois, Adam ne souhaite pas installer localement toutes les applications sur chaque ordinateur.<br /><br /> Pour ce faire, Adam crée les applications requises avec deux types de déploiement :<br /><br /> **Le premier :** une installation complète et locale de l’application qui ne peut être installée que sur l’appareil principal d’un utilisateur.<br /><br /> **Le second :** une version virtuelle de l’application qui ne doit pas être installée sur l’appareil principal de l’utilisateur.|Quand des visiteurs ouvrent une session sur un ordinateur public, ils retrouvent leurs applications affichées sous forme d’icônes sur le bureau de l’ordinateur public. Les applications qu’ils exécutent sont diffusées en continu comme des applications virtuelles. Ainsi, les utilisateurs sont aussi productifs que s’ils étaient assis à leur bureau.|  
|Adam informe les utilisateurs qu’ils peuvent définir leurs heures de travail dans le Centre logiciel, et sélectionner des options pour empêcher les activités de déploiement de logiciel pendant cette période et quand l’ordinateur se trouve en mode présentation.|Les utilisateurs sont plus productifs pendant leur journée de travail car ils peuvent contrôler le moment du déploiement des logiciels par Configuration Manager sur leurs ordinateurs.|  

 Ces étapes et résultats de configuration permettent à Trey Research de donner plus d'autonomie à ses employés en assurant leur accès aux applications à partir de n'importe quel appareil.  

###  <a name="BKMK_ScenarioUnify"></a> Exemple de scénario : unifier la gestion de la conformité pour les appareils  
 Trey Research souhaite appliquer une solution de gestion client unifiée pour assurer que les ordinateurs exécutent un logiciel antivirus automatiquement mis à jour. Plus précisément :  

-   Le Pare-feu Windows est activé.  
-   Toutes les mises à jour critiques sont installées.  
-   Des clés de Registre spécifiques sont définies.  
-   Les appareils mobiles gérés ne peuvent pas installer ou exécuter des applications non sécurisées.  

L'entreprise souhaite également étendre cette protection à Internet pour les ordinateurs portables qui se déplacent de l'intranet à Internet.  

Adam applique ces spécifications de l'entreprise aux scénarios suivants :  

|Exigence|État actuel de la gestion du client|État futur de la gestion du client|  
|-----------------|-------------------------------------|------------------------------------|  
|Tous les ordinateurs exécutent un logiciel anti-programme malveillant avec des fichiers de définition qui sont à jour et qui activent le pare-feu Windows.|Les ordinateurs exécutent différentes solutions de logiciels anti-programme malveillant qui ne sont pas toujours à jour. Le Pare-feu Windows est activé par défaut, mais les utilisateurs le désactivent parfois.<br /><br /> Les utilisateurs sont invités à contacter le support technique s'ils détectent un logiciel anti-programme malveillant sur leur ordinateur.|Tous les ordinateurs exécutent la même solution de logiciel anti-programme malveillant qui télécharge automatiquement les derniers fichiers de mise à jour des définitions et qui réactivent automatiquement le pare-feu Windows s'il a été désactivé par l'utilisateur.<br /><br /> Le support technique est automatiquement averti par courrier électronique si un logiciel malveillant est détecté.|  
|Tous les ordinateurs installent les mises à jour logicielles critiques pendant le premier mois après leur sortie.|Bien que les mises à jour logicielles soient installées sur les ordinateurs, beaucoup d’ordinateurs n’installent pas automatiquement les mises à jour logicielles critiques avant les deux ou trois mois suivant la publication de ces mises à jour. De ce fait, ces ordinateurs sont vulnérables aux attaques pendant cette période.<br /><br /> Pour les ordinateurs qui n’installent pas les mises à jour logicielles critiques, le support technique envoie d’abord un e-mail demandant aux utilisateurs d’installer les mises à jour. Les ingénieurs se connectent à distance aux ordinateurs qui restent non conformes et installent manuellement les mises à jour manquantes.|Le taux de conformité actuel pour le mois spécifié est passé à plus de 95 %. Le support technique n’a pas eu à envoyer d’e-mail de rappel, ni à installer manuellement les mises à jour.|  
|Les paramètres de sécurité pour des applications spécifiques sont régulièrement vérifiés et corrigés, si nécessaire.|Les ordinateurs exécutent des scripts de démarrage complexes qui s'appuient sur l'appartenance au groupe d'ordinateurs pour réinitialiser les valeurs de Registre pour des applications spécifiques.<br /><br /> Comme ces scripts s’exécutent uniquement au démarrage et que certains ordinateurs sont laissés sous tension pendant plusieurs jours, le support technique ne peut pas vérifier les écarts de configuration en temps voulu.|Les valeurs de Registre sont vérifiées et résolues automatiquement sans compter sur l'appartenance au groupe d'ordinateurs ou sur le redémarrage de l'ordinateur.|  
|Les appareils mobiles ne peuvent pas installer ou exécuter des applications non sécurisées.|Les utilisateurs sont invités à ne pas télécharger ni exécuter d’applications potentiellement dangereuses à partir d’Internet. Aucune mesure de contrôle n’a été mise en place pour surveiller ou appliquer cette recommandation.|Les appareils mobiles qui sont gérés avec Microsoft Intune ou Configuration Manager empêchent automatiquement l’installation ou l’exécution des applications non signées.|  
|Les ordinateurs portables qui passent de l'intranet à Internet doivent être sécurisés.|Les utilisateurs en déplacement ne parviennent pas toujours à se connecter quotidiennement via le réseau VPN. Ces ordinateurs portables ne sont alors plus conformes avec les conditions de sécurité requises.|Une simple connexion Internet suffit pour que les ordinateurs portables restent compatibles avec les conditions de sécurité requises. Les utilisateurs ne sont pas obligés d’ouvrir une session ou d’utiliser le réseau VPN.|  

 Pour répondre aux conditions requises, Adam utilise les fonctionnalités de gestion et les options de configuration de Configuration Manager suivantes :  

-   Endpoint Protection  
-   Mises à jour logicielles  
-   Paramètres de conformité  
-   Gestion des appareils mobiles  
-   Gestion des clients basés sur Internet  

Il implémente ces fonctionnalités en effectuant les étapes de configuration décrites dans le tableau suivant :  

|Étapes de configuration|Résultat|  
|-------------------------|-------------|  
|Adam configure Endpoint Protection. Il active le paramètre client pour désinstaller les autres solutions anti-programme malveillant, puis il active le Pare-feu Windows. Il configure des règles de déploiement automatique pour permettre aux ordinateurs de rechercher et d'installer régulièrement les dernières mises à jour de définitions.|La solution anti-programme malveillant unique vous aide à protéger tous les ordinateurs avec une surcharge administrative minimale. Comme le support technique est automatiquement averti par e-mail quand un logiciel anti-programme malveillant est détecté, les problèmes peuvent être résolus rapidement. Cela permet d'empêcher des attaques sur d'autres ordinateurs.|  
|Pour améliorer le taux de conformité, Adam utilise des règles de déploiement automatique, définit des fenêtres de maintenance pour les serveurs, et examine les avantages et inconvénients de l’utilisation de la fonctionnalité Wake-on-LAN pour les ordinateurs mis en veille prolongée.|La compatibilité des mises à jour logicielles critiques augmente, et la nécessité pour les utilisateurs ou le support technique d'installer des mises à jour logicielles manuellement est réduite.|  
|Adam utilise des paramètres de compatibilité pour vérifier la présence des applications spécifiées. Quand les applications sont détectées, les éléments de configuration vérifient alors les valeurs de Registre et les corrigent automatiquement si elles ne sont pas conformes.|Grâce au déploiement d’éléments de configuration et de bases de référence de configuration sur tous les ordinateurs et à la vérification quotidienne de la conformité des ordinateurs, vous n’avez plus besoin de créer des scripts distincts basés sur l’appartenance de l’ordinateur, ni de redémarrer l’ordinateur.|  
|Adam utilise des paramètres de compatibilité pour les appareils mobiles inscrits et configure le connecteur Exchange Server de sorte que les applications non signées ne sont pas autorisées à s'installer et s'exécuter sur des appareils mobiles.|Du fait de l’interdiction d’utiliser des applications non signées, les appareils mobiles sont protégés automatiquement contre les applications potentiellement dangereuses.|  
|Adam s’assure que les ordinateurs et les serveurs de système de site ont les certificats PKI requis par Configuration Manager pour les connexions HTTPS. Il installe ensuite des rôles de système de site supplémentaires dans le réseau de périmètre qui acceptent les connexions client à partir d’Internet.|Configuration Manager continue à gérer automatiquement les ordinateurs qui passent de l'intranet à Internet lorsqu'ils disposent d'une connexion Internet. Ces ordinateurs ne comptent pas sur les utilisateurs ouvrant une session sur leur ordinateur ou se connectant au réseau VPN.<br /><br /> Ces ordinateurs continuent à être gérés pour les logiciels anti-programme malveillant et le Pare-feu Windows, les mises à jour logicielles et les éléments de configuration. Par conséquent, les niveaux de compatibilité augmentent automatiquement.|  

 Ces étapes et résultats de configuration permettent à Trey Research d'unifier la gestion de la compatibilité des appareils.  

###  <a name="BKMK_ScenarioSimplify"></a> Exemple de scénario : simplifier la gestion des clients pour les appareils  
 Trey Research souhaite que tous les nouveaux ordinateurs installent automatiquement l'image d'ordinateur de base de l'entreprise qui exécute Windows 7. Une fois l’image du système d’exploitation installée sur ces ordinateurs, ceux-ci doivent être gérés et surveillés pour détecter tout autre logiciel que les utilisateurs installent. Les ordinateurs qui stockent des informations hautement confidentielles nécessitent des stratégies de gestion plus limitées que les autres ordinateurs. Par exemple, les ingénieurs du support technique ne doivent pas établir une connexion à distance à ces ordinateurs, un code confidentiel BitLocker doit être utilisé pour les redémarrages et uniquement les administrateurs locaux sont autorisés à installer un logiciel.  

 Adam applique ces spécifications de l'entreprise aux scénarios suivants :  

|Exigence|État actuel de la gestion du client|État futur de la gestion du client|  
|-----------------|-------------------------------------|------------------------------------|  
|Windows 7 est installé sur les nouveaux ordinateurs.|L’équipe du support technique installe et configure Windows 7 pour les utilisateurs, puis envoie l’ordinateur à l’emplacement prévu.|Les nouveaux ordinateurs sont envoyés directement à leur destination finale. Ils sont connectés au réseau, puis installent et configurent automatiquement Windows 7.|  
|Les ordinateurs doivent être gérés et surveillés. Cela inclut la collecte des données d’inventaire matériel et logiciel qui vous aident à déterminer les conditions de licence.|Le client Configuration Manager est déployé en utilisant l’installation Push automatique du client. Le support technique examine les échecs d’installation et vérifie les clients qui n’envoient pas de données d’inventaire comme prévu.<br /><br /> Les échecs sont fréquents à cause des dépendances d’installation qui ne sont pas respectées et de la corruption de WMI sur le client.|Les données d'installation et d'inventaire client collectées depuis des ordinateurs sont plus fiables et requièrent moins d'intervention du support technique. Les rapports indiquent l'utilisation du logiciel pour les informations de licence.|  
|Certains ordinateurs doivent avoir des stratégies de gestion plus rigoureuses.|En raison des stratégies de gestion plus rigoureuses, Configuration Manager ne gère pas encore ces ordinateurs.|Ces ordinateurs sont gérés à l’aide de Configuration Manager pour prendre en compte les exceptions, sans aucune surcharge administrative.|  

 Pour répondre aux conditions requises, Adam utilise les fonctionnalités de gestion et les options de configuration de Configuration Manager suivantes :  

-   Déploiement du système d'exploitation  
-   Déploiement du client et état du client  
-   Paramètres de conformité  
-   Paramètres du client  
-   Méthodes d’inventaire et Asset Intelligence  
-   Administration basée sur des rôles  

Il implémente ces fonctionnalités en effectuant les étapes de configuration décrites dans le tableau suivant :  

|Étapes de configuration|Résultat|  
|-------------------------|-------------|  
|Adam capture une image du système d’exploitation à partir d’un ordinateur qui exécute Windows 7 et qui est configuré selon les spécifications de l’entreprise. Il déploie ensuite le système d'exploitation sur les nouveaux ordinateurs à l'aide de la prise en charge d'ordinateur inconnu et de l'environnement PXE. Il installe également le client Configuration Manager dans le cadre du déploiement de système d'exploitation.|Les nouveaux ordinateurs sont prêts et s'exécutent plus rapidement sans intervention du support technique.|  
|Adam configure l'installation Push automatique du client à l'échelle du site pour installer le client Configuration Manager sur les ordinateurs découverts. Cela garantit que tous les ordinateurs non imagés avec le client installent toujours le client afin que l'ordinateur soit géré par Configuration Manager.<br /><br /> Adam configure l'état client pour corriger automatiquement les éventuels problèmes de client qui sont découverts. Il configure également des paramètres client pour la collecte des données d’inventaire requises et configure Asset Intelligence.|L’installation du client en même temps que le système d’exploitation est plus rapide et plus fiable que d’attendre que Configuration Manager découvre l’ordinateur et tente d’y installer les fichiers sources du client. Toutefois, en activant l’option d’installation Push automatique du client, vous fournissez une méthode de sauvegarde qui permet à un ordinateur où le système d’exploitation est déjà installé d’installer le client quand il se connecte au réseau.<br /><br /> Les paramètres client assurent que les clients envoient régulièrement leurs informations d'inventaire au site. Grâce à cela et aux tests de l’état du client, le client reste opérationnel avec une intervention minimale du support technique. Par exemple, les altérations de WMI sont détectées et résolues automatiquement.<br /><br /> Les rapports Asset Intelligence permettent de surveiller l'utilisation des logiciels et des licences.|  
|Adam crée un regroupement pour les ordinateurs auxquels il souhaite appliquer des paramètres de stratégie plus stricts. Il crée ensuite un paramètre d’appareil client personnalisé pour ce regroupement. Ce paramètre désactive le contrôle à distance, active l’entrée du code PIN BitLocker et autorise uniquement les administrateurs locaux à installer des logiciels.<br /><br /> Adam configure l’administration basée sur des rôles pour empêcher les ingénieurs du support technique de voir ce regroupement d’ordinateurs. Cette mesure évite que ces ordinateurs soient gérés comme des ordinateurs standard par inadvertance.|Ils sont désormais gérés par Configuration Manager, mais avec des paramètres spécifiques qui ne nécessitent pas l’installation d’un nouveau site.<br /><br /> Le regroupement de ces ordinateurs n’est pas visible par les ingénieurs du support technique. Cela réduit le risque que ces ordinateurs reçoivent accidentellement des déploiements et des scripts destinés aux ordinateurs standard.|  

 Ces étapes et résultats de configuration permettent à Trey Research de simplifier la gestion des clients pour les appareils.  

##  <a name="BKMK_NextSteps"></a> Étapes suivantes  
 Avant d'installer Configuration Manager, familiarisez-vous avec certains concepts de base et les termes qui sont spécifiques à Configuration Manager.  

-   Si vous connaissez déjà System Center 2012 Configuration Manager, consultez [Changements dans System Center Configuration Manager par rapport à System Center 2012 Configuration Manager](../../core/plan-design/changes/what-has-changed-from-configuration-manager-2012.md) pour comprendre les nouvelles fonctionnalités.  
-   Pour obtenir une vue d’ensemble technique globale de System Center Configuration Manager, consultez [Principes de base de System Center Configuration Manager](../../core/understand/fundamentals.md).  

Quand vous êtes familiarisé avec les concepts de base, aidez-vous de la documentation de System Center Configuration Manager pour déployer et utiliser correctement Configuration Manager.  
