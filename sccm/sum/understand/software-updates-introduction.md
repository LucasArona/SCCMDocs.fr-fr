---
title: Présentation des mises à jour logicielles
titleSuffix: Configuration Manager
description: Découvrez les principes de base des mises à jour logicielles dans System Center Configuration Manager.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: d5528fc3e035cd5bed8bc92c8b65f3025d97a2d1
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351545"
---
# <a name="introduction-to-software-updates-in-system-center-configuration-manager"></a>Présentation des mises à jour logicielles dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les mises à jour logicielles dans System Center Configuration Manager offrent un ensemble d’outils et de ressources qui peuvent faciliter la gestion de la tâche complexe que représentent le suivi et l’application des mises à jour logicielles sur les ordinateurs clients de l’entreprise. Il est essentiel de disposer d'un processus de gestion des mises à jour logicielles efficace pour assurer le fonctionnement des opérations, résoudre les problèmes de sécurité et préserver la stabilité de l'infrastructure réseau. Toutefois, la gestion des mises à jour logicielles nécessite une attention constante et continue du fait que les technologies évoluent rapidement et que de nouvelles menaces de sécurité émergent constamment.  

Pour obtenir un exemple de scénario illustrant la façon dont vous pouvez déployer des mises à jour logicielles dans votre environnement, consultez [Exemple de scénario de déploiement de mises à jour logicielles de sécurité](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="BKMK_Synchronization"></a> Synchronisation des mises à jour logicielles  
 La synchronisation des mises à jour logicielles dans Configuration Manager se connecte à Microsoft Update pour récupérer les métadonnées des mises à jour logicielles. Le site de niveau supérieur (site d’administration centrale ou site principal autonome) se synchronise avec Microsoft Update selon une planification ou quand vous démarrez manuellement la synchronisation à partir de la console Configuration Manager. Dès lors que Configuration Manager a terminé la synchronisation des mises à jour logicielles sur le site de niveau supérieur, il la démarre sur les sites enfants, le cas échéant. Quand la synchronisation est terminée sur chaque site principal ou secondaire, une stratégie à l'échelle du site est créée, laquelle fournit aux ordinateurs clients l'emplacement des points de mise à jour logicielle.  

> [!NOTE]  
>  Les mises à jour logicielles sont activées par défaut dans les paramètres client. Toutefois, si vous définissez le paramètre client **Activer les mises à jour logicielles sur les clients** sur **Non** pour désactiver les mises à jour logicielles sur un regroupement ou dans les paramètres par défaut, l'emplacement des points de mise à jour logicielle ne sont pas envoyés aux clients associés. Pour plus d’informations, consultez [paramètres client des mises à jour logicielles](../../core/clients/deploy/about-client-settings.md#software-updates).  

 Une fois que le client a reçu la stratégie, il lance une analyse de la conformité des mises à jour logicielles et écrit les informations dans Windows Management Instrumentation (WMI). Les informations de conformité sont ensuite envoyées au point de gestion qui les transmet alors au serveur de site. Pour plus d'informations sur l'évaluation de la conformité, voir la section [Software updates compliance assessment](#BKMK_SUMCompliance) de cette rubrique.  

 Vous pouvez installer plusieurs points de mise à jour logicielle sur un site principal. Le premier point de mise à jour logicielle que vous installez est configuré en tant que source de synchronisation. Celle-ci effectue la synchronisation à partir de Microsoft Update ou d’un serveur WSUS ne figurant pas dans votre hiérarchie Configuration Manager. Les autres points de mise à jour logicielle au niveau du site utilisent le premier point de mise à jour logicielle en tant que source de synchronisation.  

> [!NOTE]  
>  Lorsque le processus de synchronisation des mises à jour logicielles est terminé sur le site de niveau supérieur, les métadonnées des mises à jour logicielles sont répliquées sur les sites enfants par réplication de la base de données. Quand vous connectez une console Configuration Manager au site enfant, Configuration Manager affiche les métadonnées des mises à jour logicielles. Toutefois, tant que vous n’avez pas installé ni configuré un point de mise à jour logicielle sur le site, les clients n’analysent pas la conformité des mises à jour logicielles, ils ne transmettent pas les informations de conformité à Configuration Manager et vous ne pouvez pas déployer correctement les mises à jour logicielles.  

### <a name="synchronization-on-the-top-level-site"></a>Synchronisation sur le site de niveau supérieur  
 Le processus de synchronisation des mises à jour logicielles sur le site de niveau supérieur permet de récupérer auprès de Microsoft Update les métadonnées des mises à jour logicielles qui respectent les critères que vous spécifiez dans les propriétés du composant du point de mise à jour logicielle. Vous configurez les critères uniquement sur le site de niveau supérieur.  

> [!NOTE]  
>  En guise de source de synchronisation, plutôt que Microsoft Updates, vous pouvez spécifier un serveur WSUS existant qui ne figure pas dans la hiérarchie Configuration Manager.  

 La liste suivante décrit les étapes de base du processus de synchronisation sur le site de niveau supérieur :  

1.  La synchronisation des mises à jour logicielles démarre.  

2.  Le Gestionnaire de synchronisation WSUS envoie une demande à WSUS exécuté sur le point de mise à jour logicielle pour lancer la synchronisation avec Microsoft Update.  

3.  Les métadonnées des mises à jour logicielles sont synchronisées à partir de Microsoft Update et toutes les modifications sont insérées ou mises à jour dans la base de données WSUS.  

4.  Quand WSUS a terminé la synchronisation, le gestionnaire de synchronisation WSUS synchronise les métadonnées des mises à jour logicielles de la base de données WSUS vers la base de données Configuration Manager, et toutes les modifications effectuées après la dernière synchronisation sont insérées ou mises à jour dans la base de données du site. Les métadonnées des mises à jour logicielles sont stockées dans la base de données du site sous la forme d'un élément de configuration.  

5.  Les éléments de configuration des mises à jour logicielles sont envoyées aux sites enfants par réplication de la base de données.  

6.  Une fois la synchronisation terminée avec succès, le Gestionnaire de synchronisation WSUS crée le message d'état 6702.  

7.  Le Gestionnaire de synchronisation WSUS envoie une demande de synchronisation à tous les sites enfants.  

8.  Le gestionnaire de synchronisation WSUS envoie une demande à la fois au serveur WSUS qui s'exécute sur d'autres points de mise à jour logicielle sur le site. Les serveurs WSUS sur les autres points de mise à jour logicielle sont configurés pour être des réplicas du serveur WSUS qui s'exécute sur le point de mise à jour logicielle par défaut sur le site.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Synchronisation sur les sites secondaires et principaux enfants  
 Lors du processus de synchronisation des mises à jour logicielles sur le site de niveau supérieur, les éléments de configuration des mises à jour logicielles sont répliqués sur les sites enfants par réplication de la base de données. À la fin du processus, le site de niveau supérieur envoie une demande de synchronisation au site enfant, puis le site enfant démarre la synchronisation WSUS. La liste suivante fournit les étapes de base pour le processus de synchronisation sur un site secondaire ou un site principal enfant :  

1.  Le gestionnaire de synchronisation WSUS reçoit une demande de synchronisation de la part du site de niveau supérieur.  

2.  La synchronisation des mises à jour logicielles démarre.  

3.  Le Gestionnaire de synchronisation WSUS effectue une demande à WSUS qui est exécuté sur le point de mise à jour logicielle pour démarrer la synchronisation.  

4.  WSUS exécuté sur le point de mise à jour logicielle sur le site enfant synchronise les métadonnées des mises à jour logicielles à partir de WSUS exécuté sur le point de mise à jour logicielle sur le site parent.  

5.  Une fois la synchronisation terminée avec succès, le Gestionnaire de synchronisation WSUS crée le message d'état 6702.  

6.  À partir d'un site principal, le gestionnaire de synchronisation WSUS envoie une demande de synchronisation aux sites secondaires enfants. Le site secondaire démarre la synchronisation des mises à jour logicielles avec le site principal parent. Le site secondaire est configuré en tant que réplica du serveur WSUS qui s'exécute sur le site parent.  

7.  Le gestionnaire de synchronisation WSUS envoie une demande à la fois au serveur WSUS qui s'exécute sur d'autres points de mise à jour logicielle sur le site. Les serveurs WSUS sur les autres points de mise à jour logicielle sont configurés pour être des réplicas du serveur WSUS qui s'exécute sur le point de mise à jour logicielle par défaut sur le site.  

##  <a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Avant de déployer des mises à jour logicielles sur des ordinateurs clients dans Configuration Manager, lancez une analyse de conformité des mises à jour logicielles sur ces ordinateurs. Pour chaque mise à jour logicielle, un message indiquant l'état de conformité de la mise à jour est créé. Les messages d'état sont envoyés en bloc vers le point de gestion, puis vers le serveur du site où l'état de conformité est inséré dans la base de données du site. L’état de conformité des mises à jour logicielles s’affiche dans la console Configuration Manager. Vous pouvez déployer et installer des mises à jour logicielles sur des ordinateurs qui nécessitent les mises à jour. Vous trouverez dans les sections suivantes des informations sur les états de conformité, ainsi qu'une description du processus d'analyse de la conformité des mises à jour logicielles.  

### <a name="software-updates-compliance-states"></a>États de conformité des mises à jour logicielles  
 Vous trouverez ci-dessous une description de chaque état de conformité affiché dans la console Configuration Manager pour les mises à jour logicielles.  

-   **Obligatoire**  

     Spécifie que la mise à jour logicielle est applicable et qu'elle est requise par l'ordinateur client. Lorsque l'état de la mise à jour est **Requise**, n'importe laquelle des conditions suivante peut être vérifiée :  

    -   La mise à jour logicielle n'a pas été déployée sur l'ordinateur client.  

    -   La mise à jour logicielle a été installée sur l'ordinateur client. Toutefois, le message d'état le plus récent n'a pas encore été inséré dans la base de données sur le serveur de site. Une fois l'installation terminée, l'ordinateur client analyse de nouveau la mise à jour. Un délai maximal de deux minutes peut être observé avant que le client n'envoie l'état actualisé au point de gestion, lequel le transfère ensuite au serveur de site.  

    -   La mise à jour logicielle a été installée sur l'ordinateur client. Toutefois, l'installation de la mise à jour logicielle requiert un redémarrage de l'ordinateur pour se terminer.  

    -   La mise à jour logicielle a été déployée sur l'ordinateur client, mais elle n'a pas encore été installée.  

-   **Non requis**  

     Spécifie que la mise à jour logicielle n'est pas applicable à l'ordinateur client. Par conséquent, elle n'est pas obligatoire.  

-   **Installé**  

     Indique que la mise à jour logicielle est applicable à l'ordinateur client et qu'elle est déjà installée sur celui-ci.  

-   **Inconnu.**  

     Indique que le serveur de site n'a reçu aucun message d'état émanant de l'ordinateur client, généralement pour l'une des raisons suivantes :  

    -   L'ordinateur client n'a pas réussi à faire l'analyse de conformité des mises à jour logicielles.  

    -   L'analyse s'est correctement terminée sur l'ordinateur client. Toutefois, le message d'état n'a pas encore été traité sur le serveur de site, probablement en raison d'un backlog de messages d'état.  

    -   L'analyse sur l'ordinateur client a abouti, mais le site enfant n'a envoyé aucun message d'état.  

    -   L'analyse sur l'ordinateur client a abouti, mais le fichier de message d'état est endommagé et n'a pas pu être traité.  

### <a name="scan-for-software-updates-compliance-process"></a>Processus d'analyse de la conformité des mises à jour logicielles  
 Quand le point de mise à jour logicielle est installé et synchronisé, une stratégie d’ordinateur à l’échelle du site est créée pour informer les ordinateurs clients que les mises à jour logicielles de Configuration Manager ont été activées pour le site. Lorsqu'un client reçoit la stratégie de l'ordinateur, une analyse d'évaluation de la conformité est planifiée pour démarrer de façon aléatoire dans les deux heures suivantes. Lorsqu'une analyse est lancée, le processus Agent client des mises à jour logicielles efface l'historique des analyses, soumet une requête pour rechercher le serveur WSUS qui devrait être utilisé pour l'analyse, et met à jour la stratégie de groupe local avec l'emplacement du serveur WSUS.  

> [!NOTE]  
>  Les clients basés sur Internet doivent se connecter au serveur WSUS à l'aide de SSL.  

 Une requête d'analyse est transmise à l'Agent Windows Update (WUA). L'Agent Windows Update (WUA) se connecte à l'emplacement du serveur WSUS répertorié dans la stratégie locale, récupère les métadonnées des mises à jour logicielles synchronisées sur le serveur WSUS, puis recherche les mises à jour sur l'ordinateur client. Le processus Agent client des mises à jour logicielles détecte que l'analyse de la conformité est terminée. Il crée des messages d'état pour chacune des mises à jour logicielles dont l'état de conformité a changé après la dernière analyse. Les messages d'état sont envoyés en bloc au point de gestion, toutes les 15 minutes. Le point de gestion transfère ensuite les messages d'état au serveur de site où ils sont insérés dans la base de données du serveur de site.  

 Après la première analyse de conformité des mises à jour logicielles, l'analyse démarre selon le calendrier d'analyse configuré. Cependant, si le client a effectué l'analyse de conformité des mises à jour logicielles dans la plage de temps indiquée par la valeur de durée de vie, il utilise les métadonnées des mises à jour logicielles stockées localement. Si la dernière analyse a été effectuée en dehors de la durée de vie, le client doit se connecter au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle et mettre à jour les métadonnées des mises à jour logicielles stockées sur le client.  

 En incluant la planification de l'analyse, l'analyse de la conformité des mises à jour logicielles peut être lancée de différentes manières :  

-   **Calendrier d’analyse des mises à jour logicielles**: l’analyse de la conformité des mises à jour logicielles commence selon le calendrier d’analyse configuré dans les paramètres Agent client des mises à jour logicielles. Pour plus d’informations sur la configuration des paramètres client des mises à jour logicielles, consultez [paramètres client des mises à jour logicielles](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Action Propriétés de Configuration Manager**: l’utilisateur peut démarrer l’action **Cycle d’analyse des mises à jour de logiciels** ou **Cycle d’évaluation des déploiements de mises à jour de logiciels** sous l’onglet **Action** de la boîte de dialogue **Propriétés du Configuration Manager** sur l’ordinateur client.  

-   **Planification de la réévaluation du déploiement**: l’évaluation du déploiement et l’analyse de la conformité des mises à jour logicielles commencent selon le calendrier de réévaluation du déploiement configuré, comme indiqué dans les paramètres Agent client des mises à jour logicielles. Pour plus d’informations sur les paramètres client des mises à jour logicielles, consultez [paramètres client des mises à jour logicielles](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Avant de télécharger les fichiers de mises à jour**: quand un ordinateur client reçoit une stratégie d’attribution pour un nouveau déploiement obligatoire, l’Agent client des mises à jour logicielles télécharge les fichiers de mise à jour logicielle dans le cache du client local. Avant de télécharger les fichiers de mise à jour logicielle, l'agent du client démarre une analyse pour vérifier que la mise à jour logicielle est toujours nécessaire.  

-   **Avant l’installation des mises à jour logicielles**: juste avant d’installer des mises à jour logicielles, l’Agent client des mises à jour logicielles démarre une analyse pour vérifier que les mises à jour logicielles sont toujours nécessaires.  

-   **Après l’installation des mises à jour logicielles**: juste après la fin de l’installation des mises à jour logicielles, l’Agent client des mises à jour logicielles démarre une analyse pour vérifier que les mises à jour logicielles ne sont plus nécessaires et crée un message d’état indiquant que la mise à jour logicielle est installée. Lorsque l'installation est terminée mais qu'un redémarrage est nécessaire, le message d'état indique que l'ordinateur client doit être redémarré.  

-   **Après le redémarrage du système**: si un ordinateur client attend le redémarrage du système pour terminer l’installation de la mise à jour logicielle, l’Agent client des mises à jour logicielles démarre une analyse après le redémarrage pour vérifier que la mise à jour logicielle n’est plus nécessaire et crée un message d’état indiquant que la mise à jour logicielle est installée.  

#### <a name="time-to-live-value"></a>Valeur de la durée de vie  
 Les métadonnées des mises à jour logicielles requises pour l'analyse de la conformité des mises à jour logicielles sont stockées sur l'ordinateur client local et, par défaut, sont pertinentes pendant 24 heures. Cette durée est appelée durée de vie.  

#### <a name="scan-for-software-updates-compliance-types"></a>Types d'analyse de conformité des mises à jour logicielles  
 Le client analyse la conformité des mises à jour logicielles à l'aide d'un outil d'analyse en ligne ou hors ligne. L'analyse peut être forcée ou non, en fonction de la méthode d'exécution adoptée. Vous trouverez ci-dessous une description des méthodes en ligne ou hors ligne, forcée ou non forcée, permettant de lancer l’analyse.  

-   **Calendrier d’analyse des mises à jour logicielles** (analyse en ligne non forcée)  

     Conformément au calendrier d'analyse configuré, le client se connecte au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles uniquement si la dernière analyse a été effectuée en dehors de la durée de vie définie.  

-   **Cycle d’analyse des mises à jour logicielles** ou **Cycle d’évaluation des déploiements de mises à jour**  (analyse en ligne forcée)  

     L'ordinateur client se connecte toujours au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles avant d'analyser la conformité des mises à jour logicielles. Une fois l'analyse terminée, le compteur de durée de vie est réinitialisé. Prenons l'exemple d'une valeur de durée de vie de 24 heures : si l'utilisateur lance une analyse de conformité des mises à jour logicielles, cette valeur est réinitialisée sur 24 heures.  

-   **Calendrier de la réévaluation du déploiement** (analyse en ligne non forcée)  

     Conformément au calendrier de réévaluation du déploiement configuré, le client se connecte au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles uniquement si la dernière analyse a été effectuée en dehors de la durée de vie définie.  

-   **Avant de télécharger les fichiers de mise à jour** (analyse en ligne non forcée)  

     Avant de pouvoir télécharger les fichiers de mise à jour dans les déploiements requis, le client se connecte au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles uniquement si la dernière analyse a été effectuée en dehors de la durée de vie définie.  

-   **Avant l’installation des mises à jour logicielles** (analyse en ligne non forcée)  

     Avant d'installer les mises à jour logicielles dans les déploiements requis, le client se connecte au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles uniquement si la dernière analyse a été effectuée en dehors de la durée de vie définie.  

-   **Après l’installation des mises à jour logicielles** (analyse hors ligne non forcée)  

     Une fois qu'une mise à jour logicielle a été installée, l'Agent client des mises à jour logicielles démarre une analyse à l'aide des métadonnées locales. Le client ne se connecte jamais au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles.  

-   **Après le redémarrage du système** (analyse hors ligne forcée)  

     Une fois qu'une mise à jour logicielle a été installée et l'ordinateur redémarré, l'Agent client des mises à jour logicielles démarre une analyse en utilisant les métadonnées locales. Le client ne se connecte jamais au serveur WSUS en cours d'exécution sur le point de mise à jour logicielle pour récupérer les métadonnées des mises à jour logicielles.  

##  <a name="BKMK_DeploymentPackages"></a> Packages de déploiement des mises à jour logicielles  
 Un package de déploiement de mise à jour logicielle est le véhicule utilisé pour télécharger des mises à jour logicielles vers un dossier partagé du réseau et copier les fichiers sources des mises à jour logicielles vers la bibliothèque de contenu sur les serveurs de site et sur les points de distribution qui sont définis dans le déploiement. À l'aide de l'Assistant Téléchargement des mises à jour, vous pouvez télécharger des mises à jour logicielles et les ajouter à des packages de déploiement avant de les déployer. Cet Assistant vous permet de préparer les mises à jour logicielles sur des points de distribution et de vérifier que cette partie du processus de déploiement a réussi avant que vous déployiez les mises à jour logicielles vers les clients.  

 Une fois que vous avez déployé les mises à jour logicielles téléchargées à l'aide de l'Assistant Déploiement des mises à jour logicielles, le déploiement utilise automatiquement le package de déploiement qui contient les mises à jour logicielles. Lorsque les mises à jour logicielles qui n'ont pas été téléchargées sont déployées, vous devez spécifier un package de déploiement nouveau ou existant dans l'Assistant Déploiement des mises à jour logicielles et les mises à jour logicielles sont téléchargées à la fin de l'exécution de l'Assistant.  

> [!IMPORTANT]  
>  Vous devez créer manuellement le dossier réseau partagé pour les fichiers sources du package de déploiement avant de le spécifier dans l'Assistant. Chaque package de déploiement doit utiliser un dossier réseau partagé différent.  

> [!IMPORTANT]  
>  Le compte d'ordinateur du fournisseur SMS et l'utilisateur administratif qui télécharge les mises à jour logicielles requièrent des autorisations en **Écriture** vers la source du package. Limitez l'accès à la source du package pour éviter qu'une personne malveillante falsifie les fichiers sources de mises à jour logicielles dans la source du package.  

 Lors de la création d'un package de déploiement, la version du contenu est définie sur 1 avant que des mises à jour logicielles soient téléchargées. Quand les fichiers de mise à jour logicielle sont téléchargés à l'aide du package, la version de contenu est incrémentée à 2. Par conséquent, tous les nouveaux packages de déploiement démarrent avec une version de contenu égale à 2. Chaque fois que le contenu d'un package de déploiement change, la version de contenu est incrémentée de 1. Pour plus d’informations, consultez [Concepts fondamentaux de la gestion de contenu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 Les clients installent les mises à jour logicielles dans un déploiement en utilisant tout point de distribution qui met à disposition les mises à jour logicielles, quel que soit le package de déploiement. Même si un package de déploiement est supprimé pour un déploiement actif, les clients peuvent toujours installer les mises à jour logicielles dans le déploiement à condition que chacune d'elles ait été téléchargée dans au moins un autre package de déploiement et qu'elle soit disponible sur un point de distribution accessible depuis le client. Lorsque le dernier package de déploiement contenant une mise à jour logicielle est supprimé, les ordinateurs clients ne peuvent pas récupérer la mise à jour logicielle tant qu'elle n'est pas à nouveau téléchargée vers un package de déploiement. Les mises à jour logicielles s’affichent avec une flèche rouge dans la console Configuration Manager quand les fichiers de mise à jour ne se trouvent dans aucun package de déploiement. Les déploiements apparaissent avec une double flèche rouge lorsqu'ils contiennent des mises à jour dans cet état.  

##  <a name="BKMK_DeploymentWorkflows"></a> Flux de travail de déploiement de mise à jour logicielle  
 Il existe deux principaux scénarios de déploiement des mises à jour logicielles dans votre environnement : le déploiement manuel et le déploiement automatique. En règle générale, vous déployez manuellement les mises à jour logicielles pour créer une ligne de base pour vos ordinateurs clients, puis vous gérez les mises à jour logicielles sur les clients à l'aide d'un déploiement automatique. Les sections suivantes fournissent un résumé du flux de travail pour le déploiement manuel et automatique pour les mises à jour logicielles.  

###  <a name="BKMK_ManualDeployment"></a> Déploiement manuel de mises à jour logicielles  
 Le déploiement manuel de mises à jour logicielles consiste à sélectionner des mises à jour logicielles dans la console Configuration Manager et à démarrer manuellement le processus de déploiement. Généralement, vous utilisez cette méthode de déploiement pour mettre à jour les ordinateurs clients avec les mises à jour logicielles requises avant de créer des règles de déploiement automatique qui gèrent les déploiements de mises à jour logicielles mensuelles en continu ; vous pouvez également déployer des mises à jour logicielles requises hors bande. La liste suivante fournit le flux de travail général pour le déploiement manuel de mises à jour logicielles :  

1.  filtre pour les mises à jour logicielles qui utilisent des configurations spécifiques. Par exemple, vous pouvez fournir des critères qui récupèrent toutes les mises à jour logicielles critiques ou de sécurité qui sont requises sur plus de 50 ordinateurs clients.  

2.  Créez un groupe de mises à jour logicielles contenant les mises à jour logicielles.  

3.  Téléchargez le contenu pour les mises à jour logicielles dans le groupe de mises à jour logicielles.  

4.  Déployez manuellement le groupe de mises à jour logicielles.  

###  <a name="BKMK_AutomaticDeployment"></a> Déploiement automatique de mises à jour logicielles  
 La configuration du déploiement automatique de mises à jour logicielles s’effectue à l'aide d’une règle de déploiement automatique. Vous utilisez généralement cette méthode de déploiement pour vos mises à jour logicielles mensuelles (généralement appelées Patch Tuesday) et pour la gestion des mises à jour de définitions. Quand la règle s'exécute, les mises à jour logicielles sont supprimées du groupe de mises à jour logicielles (dans le cas d'un groupe existant), celles qui répondent aux critères spécifiés (par exemple, toutes les mises à jour logicielles publiées au cours de la dernière semaine) sont ajoutées à un groupe de mises à jour logicielles, les fichiers de contenu des mises à jour logicielles sont téléchargés et copiés dans les points de distribution, et les mises à jour logicielles sont déployées sur les ordinateurs clients du regroupement cible. La liste suivante fournit le flux de travail général pour le déploiement automatique de mises à jour logicielles :  

1.  Créez une règle de déploiement automatique qui spécifie des paramètres de déploiement tels que :  

    -   Regroupement cible  

    -   Décider d'activer ou non le déploiement ou le rapport sur la conformité des mises à jour logicielles pour les ordinateurs clients du regroupement cible  

    -   Critères de mises à jour logicielles  

    -   Calendriers d'évaluation et de déploiement  

    -   Expérience utilisateur  

    -   Propriétés de téléchargement  

2.  Les mises à jour logicielles sont ajoutées à un groupe de mises à jour logicielles.  

3.  Le groupe de mises à jour logicielles est déployé sur les ordinateurs clients du regroupement cible, s'il est spécifié.  

 Vous devez déterminer quelle stratégie de déploiement utiliser dans votre environnement. Par exemple, vous pouvez créer la règle de déploiement automatique et cibler un regroupement de clients test. Après avoir vérifié que les mises à jour logicielles sont installées sur le groupe test, vous pouvez ajouter un nouveau déploiement à la règle ou modifier le regroupement dans le déploiement existant et le remplacer par un regroupement cible qui comprend un ensemble plus important de clients. Les objets de mise à jour logicielle qui sont créés par les règles de déploiement automatique sont interactifs.  

-   Les mises à jour logicielles qui ont été déployées à l'aide d'une règle de déploiement automatique sont déployées automatiquement sur les nouveaux clients ajoutés au regroupement cible.  

-   Les nouvelles mises à jour logicielles ajoutées à un groupe de mises à jour logicielles sont déployées automatiquement sur les clients du regroupement cible.  

-   Vous pouvez activer ou désactiver les déploiements à tout moment pour la règle de déploiement automatique.  

 Après avoir créé une règle de déploiement automatique, vous pouvez y ajouter des déploiements supplémentaires. Cela peut vous aider à gérer la complexité liée au déploiement de différentes mises à jour vers différents regroupements. Chaque nouveau déploiement possède la gamme complète de fonctionnalités et d'expérience de surveillance de déploiement, et chaque nouveau déploiement que vous ajoutez :  

-   utilise les mêmes packages et groupes de mise à jour que ceux créés lors de la première exécution de la règle de déploiement automatique ;  

-   peut spécifier un regroupement différent ;  

-   prend en charge des propriétés de déploiement uniques, notamment :  

    -   Heure d'activation  

    -   Échéance  

    -   Afficher ou masquer l'expérience utilisateur  

    -   Séparer les alertes pour ce déploiement  

##  <a name="BKMK_DeploymentProcess"></a> Processus de déploiement des mises à jour logicielles  
 Après avoir déployé des mises à jour logicielles ou lorsqu'une règle de déploiement automatique exécute et déploie des mises à jour logicielles, une stratégie d'attribution du déploiement est ajoutée à la stratégie de l'ordinateur pour le site. Les mises à jour logicielles sont téléchargées à partir de l'emplacement de téléchargement, d'Internet, ou du dossier réseau, vers la source du package. Les mises à jour logicielles sont copiées depuis la source du package vers la bibliothèque de contenu sur le serveur de site, puis copiées dans la bibliothèque de contenu sur le point de distribution.  

 Lorsqu'un ordinateur client du regroupement cible pour le déploiement reçoit la stratégie d'ordinateur, l'Agent du client de mise à jour logicielle démarre une analyse d'évaluation. L’agent du client télécharge le contenu pour les mises à jour logicielles requises depuis un point de distribution vers le cache du client local selon le paramètre **Temps disponible du logiciel** pour le déploiement, puis les mises à jour logicielles sont disponibles pour l’installation. Les mises à jour logicielles dans les déploiements facultatifs (déploiements qui ne possèdent pas d'échéance d'installation) ne sont pas téléchargées avant qu'un utilisateur démarre manuellement l'installation.  

 Une fois l'échéance configurée dépassée, l'Agent client des mises à jour logicielles effectue une analyse pour vérifier que les mises à jour logicielles sont toujours nécessaires. Il vérifie ensuite le cache local sur l'ordinateur client pour s'assurer que les fichiers sources de mise à jour logicielle sont toujours disponibles. Enfin, le client installe les mises à jour logicielles. Si le contenu a été supprimé de la mémoire cache du client pour laisser de la place à un autre déploiement, le client télécharge à nouveau les mises à jour logicielles depuis le point de distribution vers la mémoire cache du client. Les mises à jour logicielles sont toujours téléchargées sur la mémoire cache du client indépendamment de la taille maximale de la mémoire cache configurée pour le client. Lorsque l'installation est terminée, l'agent du client vérifie que les mises à jour logicielles ne sont plus requises, puis il envoie un message d'état au point de gestion pour indiquer que les mises à jour logicielles sont désormais installées sur le client.  

### <a name="required-system-restart"></a>Redémarrage du système obligatoire  
 Par défaut, lorsque des mises à jour logicielles d'un déploiement requis sont installées sur un ordinateur client, et qu'un redémarrage du système est nécessaire pour terminer l'installation, le redémarrage du système est effectué. Pour les mises à jour logicielles qui ont été installées avant l'échéance, le redémarrage automatique du système est repoussé à la date et à l'heure de l'échéance, à moins que l'ordinateur ne soit redémarré entre temps pour une autre raison. Le redémarrage du système peut être ignoré pour les serveurs et les stations de travail. Ces paramètres sont configurés sur la page **Expérience utilisateur** de l'Assistant Déploiement des mises à jour logicielles ou créez Assistant Création d'une règle de mises à jour automatique.  

### <a name="deployment-reevaluation-cycle"></a>Cycle de réévaluation des déploiements  
 Par défaut, les ordinateurs clients démarrent un cycle de réévaluation du déploiement tous les 7 jours. Durant ce cycle d'évaluation, l'ordinateur client analyse les mises à jour logicielles qui ont été précédemment déployées et installées. Si des mises à jour logicielles viennent à manquer, elles sont réinstallées à partir du cache local. Si une mise à jour logicielle n'est plus disponible dans le cache local, elle est téléchargée à partir d'un point de distribution, puis installée. Vous pouvez configurer le calendrier de réévaluation sur la page **Mises à jour logicielles** dans les paramètres client du site.  

##  <a name="BKMK_EmbeddedDevices"></a> Prise en charge des appareils Windows Embedded qui utilisent des filtres d'écriture  
 Lorsque vous déployez des mise à jour logicielles sur des appareils Windows Embedded à filtre d'écriture, vous pouvez spécifier s'il faut désactiver le filtre d'écriture sur l'appareil pendant le déploiement, puis redémarrer l'appareil après le déploiement. Si le filtre d'écriture n'est pas désactivé, le logiciel est déployé sur un segment de recouvrement temporaire et il n'est plus installé lorsque l'appareil redémarre, sauf si un autre déploiement force la conservation des modifications.  

> [!NOTE]  
>  Lorsque vous déployez une mise à jour logicielle sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée. Cela vous permet de gérer le moment auquel le filtre d'écriture est désactivé et activé et le moment auquel l'appareil redémarre.  

 Le paramètre d'expérience utilisateur qui contrôle le comportement du filtre d'écriture est une case à cocher nommée **Valider les changements à l'échéance ou pendant une fenêtre de maintenance (redémarrage requis)**.  

 Pour plus d’informations sur la façon dont Configuration Manager gère les appareils intégrés qui utilisent des filtres d’écriture, consultez [Planification du déploiement du client sur des appareils Windows Embedded](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="BKMK_ExtendSoftwareUpdates"></a> Étendre les mises à jour logicielles dans Configuration Manager  
 Utilisez l’éditeur de mise à jour Systems Center pour gérer les mises à jour logicielles qui ne sont pas disponibles à partir de Microsoft Update. Une fois que vous avez publié les mises à jour logicielles sur le serveur de mise à jour et que vous les avez synchronisées dans Configuration Manager, vous pouvez les déployer sur des clients Configuration Manager. Pour plus d’informations sur l’éditeur de mise à jour, consultez [Updates Publisher 2011](http://go.microsoft.com/fwlink/p/?LinkId=252947).  

## <a name="next-steps"></a>Étapes suivantes
[Planifier les mises à jour logicielles](../plan-design/plan-for-software-updates.md)
