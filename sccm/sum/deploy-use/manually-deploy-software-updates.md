---
title: Déployer manuellement des mises à jour logicielles
titleSuffix: Configuration Manager
description: Créez manuellement des déploiements logiciels pour permettre à vos clients de rester à jour avec les mises à jour logicielles nécessaires, ou bien pour déployer des mises à jour hors bande.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.collection: M365-identity-device-management
ms.openlocfilehash: 098091c0ed9fa5948e7bc36cf601342bc847be75
ms.sourcegitcommit: 659976b943226c5124057429ac7444989f98433f
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "67159472"
---
# <a name="manually-deploy-software-updates"></a>Déployer manuellement des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

Le déploiement manuel de mises à jour logicielles consiste à sélectionner des mises à jour logicielles dans la console Configuration Manager et à lancer manuellement le processus de déploiement. Vous pouvez aussi ajouter certaines mises à jour logicielles à un groupe de mises à jour, puis déployer manuellement ce groupe. Les déploiements manuels visent généralement à permettre à vos clients de rester à jour avec les mises à jour logicielles nécessaires. Des règles de déploiement automatique sont ensuite utilisées pour gérer les déploiements continus de mises à jour logicielles mensuelles. Cette méthode manuelle permet aussi de déployer des mises à jour logicielles hors bande. Pour identifier la méthode de déploiement la plus adaptée à votre cas, consultez [Déployer des mises à jour logicielles](deploy-software-updates.md).



##  <a name="BKMK_1SearchCriteria"></a> Étape 1 : spécifier les critères de recherche des mises à jour logicielles  

Selon les combinaisons de produits et les classifications que votre site synchronise, la console Configuration Manager peut potentiellement afficher des milliers de mises à jour logicielles. La première étape du flux de travail relatif au déploiement manuel de mises à jour logicielles consiste à identifier les mises à jour logicielles que vous souhaitez déployer. Par exemple, affichez toutes les mises à jour logicielles nécessaires sur plus de 50 appareils clients à l’aide d’une classification **Sécurité** ou **Critique**.  

> [!IMPORTANT]  
>  Un même déploiement de mises à jour logicielles est limité à 1 000 mises à jour logicielles.  

### <a name="process-to-specify-search-criteria-for-software-updates"></a>Processus pour spécifier des critères de recherche de mises à jour logicielles  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles**, puis cliquez sur **Toutes les mises à jour logicielles**. Ce nœud affiche toutes les mises à jour logicielles synchronisées.  

    > [!NOTE]  
    >  Le nœud **Toutes les mises à jour logicielles** affiche uniquement les mises à jour logicielles classées selon les critères **Critique** et **Sécurité** qui ont été publiées au cours des 30 derniers jours.  

2.  Dans le volet de recherche, filtrez pour identifier les mises à jour logicielles dont vous avez besoin. Utilisez l’une des options suivantes (ou les deux) :  

    -   Dans la zone de texte de recherche, tapez une chaîne de recherche pour filtrer les mises à jour logicielles. Par exemple, tapez l’ID de l’article ou du bulletin correspondant à une mise à jour logicielle spécifique. Ou bien, entrez une chaîne qui figure dans le titre de plusieurs mises à jour logicielles.  

    -   Cliquez sur **Ajouter des critères**, puis sélectionnez les critères en vue de filtrer les mises à jour logicielles. Cliquez sur **Ajouter**, puis indiquez les valeurs des critères.  

3.  Cliquez sur **Rechercher** pour filtrer les mises à jour logicielles.  

    > [!TIP]  
    >  Enregistrez les critères de filtre fréquemment utilisés. Sur le ruban, cliquez sur l’option **Enregistrer la recherche actuelle**. Récupérez les recherches précédentes en cliquant sur **Recherches enregistrées**.   



##  <a name="BKMK_2UpdateGroup"></a> Étape 2 : créer un groupe de mises à jour logicielles contenant les mises à jour logicielles   

Les groupes de mises à jour logicielles vous permettent d’organiser les mises à jour logicielles en vue du déploiement. Utilisez la procédure suivante pour ajouter manuellement des mises à jour logicielles à un nouveau groupe de mises à jour logicielles.  

### <a name="process-to-manually-add-software-updates-to-a-new-software-update-group"></a>Processus pour ajouter manuellement des mises à jour logicielles à un nouveau groupe de mises à jour logicielles  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, puis sélectionnez **Mises à jour logicielles**. Sélectionnez les mises à jour logicielles souhaitées.  

2.  Cliquez sur **Créer un groupe de mises à jour logicielles** dans le ruban.  

3.  Spécifiez le nom du groupe de mises à jour logicielles et indiquez éventuellement une description. Utilisez un nom et une description suffisamment révélateurs du type des mises à jour contenues dans le groupe de mises à jour logicielles. Cliquez sur **Créer**.  

4.  Sélectionnez le nœud **Groupes de mises à jour logicielles**, puis sélectionnez le nouveau groupe de mises à jour logicielles. Pour afficher la liste des mises à jour dans le groupe, cliquez sur **Afficher les membres** dans le ruban.  



##  <a name="BKMK_3DownloadContent"></a> Étape 3 : télécharger le contenu pour le groupe de mises à jour logicielles  

Avant de déployer les mises à jour logicielles, téléchargez le contenu des mises à jour logicielles dans le groupe de mises à jour logicielles. Cette étape vous permet de vérifier que le contenu est disponible sur les points de distribution avant de déployer les mises à jour logicielles. Par ailleurs, elle vous évite des problèmes inattendus liés à la distribution du contenu. Si vous ignorez cette étape, pendant le déploiement, le site télécharge le contenu et le distribue aux points de distribution. Pour télécharger le contenu pour les mises à jour logicielles dans le groupe de mises à jour logicielles, procédez comme suit.  


### <a name="process-to-download-content-for-the-software-update-group"></a>Processus pour télécharger le contenu pour le groupe de mises à jour logicielles
[!INCLUDE [downloadupdates](../includes/downloadupdates.md)]

### <a name="process-to-monitor-content-status"></a>Processus pour surveiller l’état du contenu
1. Pour surveiller l’état du contenu des mises à jour logicielles, accédez à l’espace de travail **Surveillance** dans la console Configuration Manager. Développez **État de distribution**, puis sélectionnez le nœud **État du contenu**.  

2. Sélectionnez le package de mises à jour logicielles que vous avez précédemment identifié pour télécharger les mises à jour logicielles dans le groupe de mises à jour logicielles.  

3. Cliquez sur **Afficher l’état** dans le ruban.  



##  <a name="BKMK_4DeployUpdateGroup"></a> Étape 4 : déployer le groupe de mises à jour logicielles  

Après avoir identifié les mises à jour logicielles que vous souhaitez déployer et après les avoir ajoutées à un groupe de mises à jour logicielles, déployez manuellement le groupe de mises à jour logicielles.  

### <a name="process-to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Processus pour déployer manuellement les mises à jour logicielles dans un groupe de mises à jour logicielles  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles**, puis sélectionnez le nœud **Groupes de mises à jour logicielles**.  

2. Sélectionnez le groupe de mises à jour de logiciels que vous souhaitez déployer. Cliquez sur **Déployer** dans le ruban.   

3. Dans la page **Général** de l’Assistant Déploiement des mises à jour logicielles, configurez les paramètres suivants :  

   -   **Nom**: indiquez le nom du déploiement. Le déploiement doit posséder un nom unique qui décrit son objectif et le distingue des autres déploiements dans le site. Ce champ de nom est limité à 256 caractères. Par défaut, Configuration Manager attribue automatiquement un nom au déploiement au format suivant : `Microsoft Software Updates - YYYY-MM-DD <time>`  

   -   **Description :** spécifiez la description du déploiement. La description est facultative, mais elle fournit une vue d’ensemble du déploiement. Ajoutez toute autre information pertinente permettant de l’identifier et de le distinguer des autres dans le site. Le champ de description est limité à 256 caractères et est vide par défaut.  

   -   **Mise à jour logicielle/Groupe de mises à jour logicielles** : vérifiez que le groupe de mises à jour logicielles ou la mise à jour logicielle qui s’affiche est correct.  

   -   **Sélectionner un modèle de déploiement**: indiquez si un modèle de déploiement enregistré précédemment doit être appliqué. Configurez un modèle de déploiement pour enregistrer des propriétés de déploiement de mises à jour logicielles courantes. Vous appliquerez ensuite ce modèle au moment de déployer ultérieurement des mises à jour logicielles. Ces modèles font gagner du temps et assurent une cohérence entre les déploiements similaires.  

   -   **Regroupement** : spécifiez le regroupement pour le déploiement. Les appareils contenus dans le regroupement reçoivent les mises à jour logicielles de ce déploiement.  

4. Dans la page **Paramètres de déploiement**, configurez les paramètres suivants :  

   -   **Type de déploiement**: indique le type de déploiement pour le déploiement des mises à jour logicielles.  

       > [!IMPORTANT]  
       >  Une fois que le déploiement de mises à jour logicielles est créé, vous ne pouvez plus modifier le type de déploiement.  

        - Sélectionnez **Requis** pour créer un déploiement de mises à jour logicielles obligatoire. Les mises à jour logicielles sont automatiquement installées sur les clients avant l’échéance d’installation que vous configurez.  

        - Sélectionnez **Disponible** pour créer un déploiement de mises à jour logicielles facultatif. Les utilisateurs peuvent installer ce déploiement à partir du Centre logiciel.  

       > [!NOTE]  
       >  Quand vous déployez un groupe de mises à jour logicielles avec l’option **Requis**, les clients téléchargent le contenu en arrière-plan et respectent les paramètres BITS éventuellement configurés.  
       > 
       > Pour les groupes de mises à jour logicielles déployés avec l’option **Disponible**, les clients téléchargent le contenu au premier plan et ignorent les paramètres BITS.  

   -   **Utiliser Wake On LAN pour réveiller les clients pour les déploiements requis** : indique si Wake On LAN est activé à l’échéance. Wake On LAN envoie des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles incluses dans le déploiement. Le site réveille tous les ordinateurs qui sont en mode veille à l’heure d’échéance de l’installation pour que l’installation puisse démarrer. Les clients en mode veille qui n’ont besoin d’aucune des mises à jour logicielle incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n’est pas activé. Il est disponible uniquement pour les déploiements **Requis**. Avant d’utiliser cette option, configurez les ordinateurs et les réseaux pour Wake On LAN. Pour plus d’informations, consultez [Guide pratique pour configurer Wake On LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

   -   **Niveau de détail** : indiquez le niveau de détail des messages d’état que les clients communiquent au site.  

5. Dans la page **Planification**, configurez les paramètres suivants :  

   -   **Calendrier d’évaluation** : spécifiez le moment où Configuration Manager évalue le temps de mise à disposition et les heures d’échéance de l’installation. Choisissez d’utiliser le temps universel coordonné (UTC) ou l’heure locale de l’ordinateur qui exécute la console Configuration Manager.  

       - Quand vous sélectionnez ici **Heure locale du client**, puis **Dès que possible** pour le **Temps disponible du logiciel**, l’heure actuelle de l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer à quel moment les mises à jour sont disponibles. Ce comportement est le même avec l’**Échéance de l’installation** et l’heure à laquelle les mises à jour sont installées sur un client. Si le client se trouve dans un autre fuseau horaire, ces actions se produisent quand l’heure du client correspond à l’heure de l’évaluation.  

   -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

       -   **Dès que possible** : permet aux clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d’interrogation de la stratégie client, les clients prennent connaissance du déploiement et les mises à jour sont disponibles pour l’installation.  

       -   **Heure spécifique** : permet aux clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Au prochain cycle d’interrogation de la stratégie client, les clients prennent connaissance du déploiement. Cependant, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles pour l’installation avant la date et l’heure configurées.  

   -   **Échéance de l’installation** : ces options son disponibles uniquement pour les déploiements **Requis**. Sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement.  

       -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

       -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques.  

           - L’heure d’échéance de l’installation réelle est l’heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre deux heures. La randomisation réduit l’impact potentiel lié à l’installation simultanée, par les clients du regroupement, des mises à jour incluses dans le déploiement.   

           - Pour désactiver le délai de randomisation de l’installation pour les mises à jour logicielles requises, configurez le paramètre client sur **Désactiver la randomisation des échéances** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [Paramètres client de l’Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

   -  **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres client** : activez ce paramètre pour accorder aux utilisateurs plus de temps pour installer les mises à jour logicielles requises au-delà de l’échéance.  

       - Ce comportement est généralement obligatoire quand un ordinateur reste longuement inactif et qu’il nécessite l’installation de nombreuses applications ou mises à jour logicielles. Par exemple, quand un utilisateur rentre de congés, il peut être amené à patienter longuement, le temps que le client installe les déploiements en retard.  

       - Configurez cette période de grâce avec la propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** dans les paramètres client. Pour plus d’informations, consultez la section [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent). La période de grâce de mise en œuvre s’applique à tous les déploiements pour lesquels cette option est activée et vise les appareils sur lesquels vous avez aussi déployé le paramètre client.  

       - Après l’échéance, le client installe les mises à jour logicielles au cours de la première fenêtre non ouvrée que l’utilisateur a configurée, dans la limite de cette période de grâce. Cependant, l’utilisateur peut toujours ouvrir le Centre logiciel et installer les mises à jour logicielles à tout moment. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard.  

6. Dans la page **Expérience utilisateur**, configurez les paramètres suivants :  

   -   **Notifications à l’utilisateur** : indiquez si vous souhaitez afficher les notifications dans le Centre logiciel au **Temps disponible du logiciel** configuré. Ce paramètre permet aussi de contrôler si des notifications doivent être envoyées aux utilisateurs sur les ordinateurs clients. Pour les déploiements **disponibles**, vous ne pouvez pas sélectionner l’option **Masquer dans le Centre logiciel et toutes les notifications**.  

   -   **Comportement à l’échéance** : ce paramètre peut être configuré uniquement pour les déploiements **requis**. Spécifiez ce qui se passe quand le déploiement de mises à jour logicielles arrive à échéance en dehors des fenêtres de maintenance définies. Vous pouvez entre autres choisir d’installer les mises à jour logicielles et d’exécuter un redémarrage du système après l’installation. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows). 
  
       > [!Note]
       > Cela ne s’applique que si la fenêtre de maintenance est configurée pour l’appareil client. Si aucune fenêtre de maintenance n’est définie sur l’appareil, la mise à jour de l’installation et le redémarrage se produisent toujours après l’échéance.

   -   **Comportement de redémarrage du périphérique** : ce paramètre peut être configuré uniquement pour les déploiements **requis**. Indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé si un redémarrage est nécessaire pour terminer l’installation des mises à jour.  

       > [!WARNING]  
       >  La suppression du redémarrage du système peut être utile dans les environnements de serveur ou quand vous ne souhaitez pas que les ordinateurs cibles redémarrent par défaut. Cependant, cela peut laisser les ordinateurs dans un état non sécurisé. Autoriser un redémarrage forcé aide à garantir l’exécution immédiate de l’installation des mises à jour logicielles.  

   -   **Traitement des filtres d’écriture pour les appareils Windows Embedded** : ce paramètre contrôle le comportement d’installation sur les appareils Windows Embedded qui sont activés avec un filtre d’écriture. Choisissez l’option permettant de valider les modifications à l’échéance de l’installation ou au cours d’une fenêtre de maintenance. Quand vous sélectionnez cette option, un redémarrage est nécessaire et les modifications sont conservées sur l’appareil. Sinon, la mise à jour est installée, appliquée sur l’overlay temporaire et validée ultérieurement.  

       -  Quand vous déployez une mise à jour logicielle sur un appareil Windows Embedded, vérifiez que l’appareil est membre d’un regroupement pour lequel une fenêtre de maintenance a été configurée.  

   - **Comportement de réévaluation du déploiement des mises à jour logicielles après le redémarrage** : sélectionnez ce paramètre pour configurer les déploiements de mises à jour logicielles de façon à ce que les clients exécutent une analyse de conformité des mises à jour logicielles immédiatement après avoir installé celles-ci et redémarré. Ce paramètre permet au client de rechercher d’autres mises à jour devenues applicables après son redémarrage, puis de les installer au cours d’une même fenêtre de maintenance.  

7. Dans la page **Alertes**, configurez la manière dont Configuration Manager génère des alertes pour ce déploiement. Examinez les alertes de mises à jour logicielles récentes de Configuration Manager dans le nœud **Mises à jour logicielles** de l’espace de travail **Bibliothèque de logiciels**. Si vous utilisez également System Center Operations Manager, configurez aussi ses alertes. Configurez uniquement les alertes pour les déploiements **requis**.  

8. Dans la page **Paramètres de téléchargement**, configurez les paramètres suivants :  

    > [!NOTE]  
    >  Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres de cette page.  

    - Indiquez si les clients doivent télécharger et installer les mises à jour quand ils utilisent un point de distribution d’un groupe voisin ou des groupes de limites de site par défaut.  

    - Indiquez si les clients doivent télécharger et installer les mises à jour logicielles à partir d’un point de distribution dans le groupe de limites de site par défaut quand le contenu des mises à jour logicielles n’est pas disponible à partir d’un point de distribution dans les groupes de limites actuels ou voisins.  

    - **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations, consultez [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). Depuis la version 1802, BranchCache est toujours activé sur les clients. Ce paramètre est supprimé, car les clients utilisent BranchCache si le point de distribution le prend en charge.  

    - **Si les mises à jour logicielles ne sont pas disponibles sur le point de distribution des groupes de limites actifs, voisins ou de site, télécharger le contenu à partir de Microsoft Updates** : sélectionnez ce paramètre pour que les clients connectés à l’intranet téléchargent les mises à jour logicielles à partir de Microsoft Update si les mises à jour ne sont pas disponibles sur les points de distribution. Les clients Internet accèdent toujours à Microsoft Update pour obtenir le contenu des mises à jour logicielles.

    - Indiquez si les clients peuvent procéder au téléchargement une fois l’échéance de l’installation dépassée dans le cas où ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez quand vous utilisez une connexion facturée à l’usage.  

9. Dans la page **Package de déploiement**, sélectionnez l’une des options suivantes :  

    > [!Note]  
    > Si vous avez déjà effectué l’[Étape 3 : Télécharger le contenu pour le groupe de mises à jour logicielles](#BKMK_3DownloadContent), l’Assistant n’affiche pas les pages **Package de déploiement**, **Points de distribution** et **Sélection de la langue**. Passez à la page [Résumé](#bkmk_summary) de l’Assistant.  
    > 
    >  Les mises à jour logicielles qui ont été téléchargées précédemment dans la bibliothèque de contenu sur le serveur de site ne sont pas téléchargées à nouveau. Ce comportement prévaut même quand vous créez un package de déploiement pour les mises à jour logicielles. Si toutes les mises à jour logicielles ont déjà été téléchargées, l’Assistant passe à la page [Résumé](#bkmk_summary).  

    - **Sélectionner un package de déploiement** : ajoute ces mises à jour à un package de déploiement existant.  

    - **Créer un package de déploiement** : ajoute ces mises à jour à un nouveau package de déploiement. Configurez les paramètres supplémentaires suivants :  

        -  **Nom**: spécifiez le nom du package de déploiement. Utilisez un nom unique qui décrit le contenu du package. Il est limité à 50 caractères.  

        -  **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description facultative est limitée à 127 caractères.  

        -  **Source du package**: spécifiez l’emplacement des fichiers sources des mises à jour logicielles. Tapez un chemin réseau pour l’emplacement source, par exemple `\\server\sharename\path`, ou cliquez sur **Parcourir** pour rechercher l’emplacement réseau. Créez le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

            - Vous ne pouvez pas utiliser l’emplacement spécifié comme source d’un autre package de déploiement logiciel.  

            - Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Dans ce cas, copiez d’abord le contenu de la source du package d’origine dans le nouvel emplacement source du package.  

            -  Le compte d’ordinateur du fournisseur SMS et l’utilisateur qui exécute l’Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations d’**Écriture** sur l’emplacement de téléchargement. Limitez l’accès à l’emplacement de téléchargement. Cette restriction réduit le risque que des personnes malveillantes falsifient les fichiers sources des mises à jour logicielles.  

        -  **Priorité d’expédition**: spécifiez la priorité d’envoi pour le package de déploiement. Configuration Manager utilise cette priorité quand il envoie le package aux points de distribution. Les packages de déploiement sont envoyés par ordre de priorité : haute, moyenne ou faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. S’il n’y a pas de backlog, le package est traité immédiatement, quelle que soit sa priorité.  

        - **Activer la réplication différentielle binaire** : activez ce paramètre pour limiter le trafic réseau entre les sites. La réplication différentielle binaire met à jour uniquement le contenu qui a changé dans le package, au lieu de mettre à jour l’ensemble du contenu du package. Pour plus d’informations, consultez [Réplication différentielle binaire](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

    - **Aucun package de déploiement** : depuis la version 1806, les mises à jour logicielles sont déployées sur les appareils sans que le contenu soit préalablement téléchargé et distribué aux points de distribution. Ce paramètre est particulièrement utile quand le contenu des mises à jour à traiter est extrêmement volumineux. Vous pouvez aussi l’utiliser quand vous voulez que les clients reçoivent systématiquement le contenu à partir du service cloud Microsoft Update. Dans ce cas, les clients peuvent également télécharger le contenu auprès d’homologues qui disposent déjà du contenu nécessaire. Le client Configuration Manager continue de gérer le téléchargement de contenu. Vous pouvez donc utiliser la fonctionnalité de cache d’homologue Configuration Manager ou d’autres technologies telles que l’optimisation de la distribution. Cette fonctionnalité prend en charge tous les types de mises à jour pris en charge par la gestion des mises à jour logicielles Configuration Manager, y compris les mises à jour Windows et Office.<!--1357933-->  

10. Dans la page **Points de distribution**, spécifiez les points de distribution ou les groupes de points de distribution où héberger les fichiers de mise à jour logicielle. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs).  

    > [!Note]  
    > Si vous avez déjà effectué l’[Étape 3 : Télécharger le contenu pour le groupe de mises à jour logicielles](#BKMK_3DownloadContent), l’Assistant n’affiche pas les pages **Package de déploiement**, **Points de distribution** et **Sélection de la langue**. Passez à la page [Résumé](#bkmk_summary) de l’Assistant.  

11. Dans la page **Emplacement de téléchargement**, indiquez si les fichiers de mise à jour logicielle doivent être téléchargés à partir d’Internet ou de votre réseau local. Configurez les paramètres suivants :  

    -   **Télécharger les mises à jour logicielles depuis Internet** : sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un emplacement spécifié sur Internet. Ce paramètre est activé par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un répertoire local ou d’un dossier partagé. Ce paramètre est utile quand l’ordinateur exécutant l’Assistant ne dispose d’aucun accès Internet. Tout ordinateur connecté à Internet peut télécharger préalablement les mises à jour logicielles, puis les stocker à un emplacement sur le réseau local auquel l’ordinateur exécutant l’Assistant peut accéder.  

12. Dans la page **Sélection de la langue**, sélectionnez les langues pour lesquelles le site télécharge les mises à jour logicielles sélectionnées. Le site télécharge uniquement ces mises à jour si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont pas propres à une langue sont toujours téléchargées. Par défaut, l’Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qu’une mise à jour logicielle ne prend pas en charge, le téléchargement de cette mise à jour échoue.  

    > [!Note]  
    > Si vous avez déjà effectué l’[Étape 3 : Télécharger le contenu pour le groupe de mises à jour logicielles](#BKMK_3DownloadContent), l’Assistant n’affiche pas les pages **Package de déploiement**, **Points de distribution** et **Sélection de la langue**. Passez à la page [Résumé](#bkmk_summary) de l’Assistant.  

13. <a name="bkmk_summary"></a> Dans la page **Résumé**, passez en revue les paramètres. Pour enregistrer les paramètres dans un modèle de déploiement, cliquez sur **Enregistrer en tant que modèle**. Entrez un nom et sélectionnez les paramètres que vous souhaitez inclure dans le modèle, puis cliquez sur **Enregistrer**. Pour modifier un paramètre configuré, cliquez sur la page de l'Assistant associée et modifiez le paramètre.  

    -  Le nom du modèle peut comporter des caractères ASCII alphanumériques, ainsi que les caractères `\` (barre oblique inverse) ou `'` (guillemet-apostrophe).  

14. Cliquez sur **Suivant** pour déployer la mise à jour logicielle.  

    Une fois l’Assistant terminé, Configuration Manager télécharge les mises à jour logicielles dans la bibliothèque de contenu sur le serveur de site. Il distribue ensuite le contenu aux points de distribution configurés et déploie le groupe de mises à jour logicielles sur les clients du regroupement cible. Pour plus d’informations sur le processus de déploiement, consultez [Software update deployment process](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentProcess).  



## <a name="next-steps"></a>Étapes suivantes
[Surveiller les mises à jour logicielles](monitor-software-updates.md)
