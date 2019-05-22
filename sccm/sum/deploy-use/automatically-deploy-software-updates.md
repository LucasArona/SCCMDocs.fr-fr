---
title: Déployer automatiquement des mises à jour logicielles
titleSuffix: Configuration Manager
description: Déployez automatiquement des mises à jour logicielles à l’aide de règles de déploiement automatique (ADR).
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/02/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.collection: M365-identity-device-management
ms.openlocfilehash: c1b77b4c35cfadd3e0e48ddec99344745f402d66
ms.sourcegitcommit: 80cbc122937e1add82310b956f7b24296b9c8081
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65500248"
---
#  <a name="automatically-deploy-software-updates"></a>Déployer automatiquement des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez une règle de déploiement automatique (ADR) au lieu d’ajouter de nouvelles mises à jour à un groupe de mises à jour logicielles existant. D’une manière générale, vous utilisez des règles ADR pour déployer les mises à jour logicielles mensuelles (également appelées mises à jour « Patch Tuesday ») et pour gérer les mises à jour de définitions Endpoint Protection. Si vous avez besoin d’aide pour déterminer la méthode de déploiement qui vous convient, consultez [Déployer des mises à jour logicielles](deploy-software-updates.md).


##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Créer une règle de déploiement automatique (ADR)  
Approuvez et déployez automatiquement des mises à jour logicielles en utilisant une règle ADR. La règle peut ajouter des mises à jour logicielles à un nouveau groupe de mises à jour logicielles chaque fois qu’elle s’exécute, ou vous pouvez ajouter des mises à jour logicielles à un groupe existant. Quand une règle s’exécute et ajoute des mises à jour logicielles à un groupe existant, la règle supprime toutes les mises à jour du groupe. Elle ajoute ensuite au groupe les mises à jour qui répondent aux critères que vous définissez. 

> [!WARNING]  
>  Avant de créer une règle ADR pour la première fois, vérifiez que le site a terminé la synchronisation des mises à jour logicielles. Cette étape est importante quand vous exécutez Configuration Manager dans une langue autre que l’anglais. Les classifications des mises à jour logicielles s’affichent en anglais avant la première synchronisation, puis elles s’affichent dans la langue localisée une fois la synchronisation des mises à jour logicielles terminée. Les règles que vous créez avant de synchroniser les mises à jour logicielles risquent ne pas fonctionner correctement après la synchronisation car la chaîne de texte peut ne pas correspondre.  


### <a name="bkmk_adr-process"></a> Processus de création d’une règle ADR  

1.  Dans la console de Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles**, puis sélectionnez le nœud **Règles de déploiement automatique**.  

2.  Dans le ruban, cliquez sur **Créer une règle de déploiement automatique**.  

3.  Dans la page **Général** de l’Assistant Création d’une règle de déploiement automatique, configurez les paramètres suivants :  

    -   **Nom :** spécifiez le nom de la règle ADR. Le nom doit être unique, permettre de décrire l’objectif de la règle et être identifiable parmi d’autres dans le site Configuration Manager.  

    -   **Description :** spécifiez une description pour la règle ADR. La description doit fournir une présentation de la règle de déploiement et autres informations pertinentes permettant de la différencier des autres. Le champ de description facultatif est limité à 256 caractères et est vierge par défaut.  

    -   **Modèle** : sélectionnez un modèle de déploiement pour spécifier s’il faut appliquer des configurations ADR enregistrées précédemment. Configurez un modèle de déploiement contenant plusieurs propriétés de déploiement de mise à jour communes, utilisables pour créer des règles ADR supplémentaires. Ces modèles permettent de gagner du temps et de garantir la cohérence entre des déploiements similaires. Sélectionnez l’un des modèles de déploiement de mises à jour logicielles prédéfinis suivants :  

         - Le modèle **Patch Tuesday** fournit des paramètres communs à utiliser lorsque vous déployez des mises à jour logicielles selon un cycle mensuel.  

         - Le modèle **Mises à jour d’Office 365 Client** fournit des paramètres communs à utiliser quand vous déployez des mises à jour pour les clients Office 365 Pro Plus.  

         - Le modèle **Mises à jour de SCEP et de l’antivirus Windows Defender** fournit des paramètres communs à utiliser quand vous déployez des mises à jour de définitions Endpoint Protection.  

    -   **Regroupement**: indique le regroupement cible à utiliser pour le déploiement. Les membres du regroupement reçoivent les mises à jour logicielles définies dans le déploiement.  

    -   déterminer si des mises à jour logicielles seront ajoutées à un groupe de mises à jour logicielles nouveau ou existant. Dans la plupart des cas, choisissez de créer un nouveau groupe de mises à jour logicielles au moment d’exécuter la règle ADR. Si la règle s’exécute selon une planification plus agressive, vous pouvez choisir d’utiliser un groupe existant. Par exemple, si vous exécutez la règle quotidiennement pour des mises à jour de définitions, vous pouvez ajouter les mises à jour logicielles à un groupe de mises à jour logicielles existant.  

    -   **Activer le déploiement après l’exécution de cette règle**: indiquez si le déploiement des mises à jour logicielles doit être activé après l’exécution de la règle ADR. Examinez les options suivantes pour ce paramètre :  

        -   Quand vous activez le déploiement, les mises à jour qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles. Le contenu des mises à jour logicielles est téléchargé en fonction. Le contenu est copié vers les points de distribution spécifiés, et les mises à jour sont déployées sur les clients du regroupement cible.  

        -   Quand vous n’activez pas le déploiement, les mises à jour qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles. Le contenu du déploiement de mises à jour logicielles est téléchargé, en fonction des besoins, et distribué aux points de distribution spécifiés. Le site crée un déploiement désactivé sur le groupe de mises à jour logicielles afin d’empêcher le déploiement des mises à jour sur les clients. Cette option vous laisse le temps de préparer le déploiement des mises à jour, de vérifier que les mises à jour répondant aux critères sont adéquates, puis d’activer le déploiement.  

4.  Dans la page **Paramètres de déploiement**, configurez les paramètres suivants :  

    -   **Utiliser Wake On LAN pour réveiller les clients pour les déploiements requis** : spécifie s’il faut activer Wake On LAN à l’échéance. Wake On LAN envoie des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles dans le déploiement. Le site réveille tous les ordinateurs qui sont en mode veille à l’heure d’échéance de l’installation pour que l’installation puisse démarrer. Les clients en mode veille qui n’ont besoin d’aucune des mises à jour logicielle incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n’est pas activé. Avant d’utiliser cette option, configurez les ordinateurs et les réseaux pour Wake On LAN. Pour plus d’informations, consultez [Guide pratique pour configurer Wake On LAN](/sccm/core/clients/deploy/configure-wake-on-lan).  

    -   **Niveau de détail** : indiquez le niveau de détail des messages d’état d’application des mises à jour qui sont signalés par les clients.  

        > [!IMPORTANT]  
        >  Quand vous déployez des mises à jour de définitions, définissez le niveau de détails sur **Erreur uniquement** pour que le client envoie un message d'état uniquement si une mise à jour de définition échoue. Sinon, le client envoie un grand nombre de messages d’état pouvant avoir un effet sur les performances du serveur de site.  
        
> [!NOTE]  
> Le niveau de détail **Erreur uniquement** n’envoie pas les messages d’état d’application nécessaires au suivi des redémarrages en attente.

    -   **Paramètre du contrat de licence**: indiquez si les mises à jour logicielles doivent être déployées automatiquement avec un contrat de licence associé. Certaines mises à jour logicielles comprennent un contrat de licence. Quand vous déployez automatiquement des mises à jour logicielles, le contrat de licence ne s’affiche pas et il n’est pas possible de l’accepter. Choisissez de déployer automatiquement toutes les mises à jour logicielles indépendamment d’un contrat de licence associé, ou déployez uniquement les mises à jour qui ne sont associées à aucun contrat de licence.  

         - Pour consulter le contrat de licence d’une mise à jour logicielle, sélectionnez la mise à jour logicielle dans le nœud **Toutes les mises à jour logicielles** de l’espace de travail **Bibliothèque de logiciels**. Dans le ruban, cliquez sur **Consulter la licence**.    

         - Pour trouver des mises à jour logicielles avec un contrat de licence associé, ajoutez la colonne **Termes du contrat de licence** dans le volet des résultats du nœud **Toutes les mises à jour logicielles**. Cliquez sur l’en-tête de la colonne pour trier les mises à jour logicielles associées à un contrat de licence.  

5.  Dans la page **Mises à jour logicielles**, configurez les critères des mises à jour logicielles que la règle ADR récupère et ajoute au groupe de mises à jour logicielles.  

     - Dans une règle ADR, le nombre limite de mises à jour logicielles est de 1 000.  

     - Si nécessaire, filtrez sur la taille du contenu des mises à jour logicielles dans les règles de déploiement automatique. Pour plus d’informations, consultez [Configuration Manager et maintenance Windows simplifiée sur des systèmes d’exploitation de bas niveau](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).  

     - À compter de la version 1806, un filtre de propriété pour **Architecture** est disponible. Utilisez ce filtre pour exclure des architectures comme Itanium et ARM64 qui sont moins fréquentes. N’oubliez pas qu’il existe des applications 32 bits (x86) et des composants exécutés sur des systèmes 64 bits (x64). Sauf si vous êtes certain de ne pas besoin de x86, activez-le aussi lorsque vous choisissez x64.<!--1322266-->  


6.  Dans la page **Calendrier d’évaluation**, indiquez si l’exécution de la règle ADR doit obéir à un calendrier. Si elle est activée, cliquez sur **Personnaliser** pour définir le calendrier périodique.  

    - La configuration de l'heure de début du calendrier se base sur l'heure locale de l'ordinateur qui exécute la console Configuration Manager.  

    - La règle ADR peut être évaluée jusqu’à trois fois par jour.  

    - Ne définissez jamais le calendrier d’évaluation selon une fréquence supérieure au calendrier de synchronisation des mises à jour logicielles. Cette page affiche le calendrier de synchronisation du point de mise à jour logicielle pour vous aider à déterminer la fréquence du calendrier d’évaluation.  
    
    - Pour exécuter manuellement la règle ADR, sélectionnez la règle dans le nœud **Règle de déploiement automatique** de la console, puis cliquez sur **Exécuter maintenant** dans le ruban.  
    
       > [!NOTE]  
       > À compter de la version 1802, les règles ADR peuvent être planifiées pour évaluer le décalage à partir d’un jour de base. Par exemple, si le correctif Patch Tuesday tombe en fait un mercredi pour vous, définissez le calendrier d’évaluation sur le deuxième mardi du mois avec un décalage d’un jour.<!--1357133-->  
       >  
       > Si vous choisissez un décalage qui se poursuit jusqu’au mois suivant, le site planifie l’évaluation pour le dernier jour du mois en cas de décalage durant la dernière semaine du mois.<!--506731-->  
       >  
       > ![Décalage de la planification d’évaluation personnalisée ADR à partir du jour de base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Dans la page **Calendrier de déploiement**, configurez les paramètres suivants :  

    -   **Calendrier d’évaluation** : spécifiez le moment où Configuration Manager évalue la durée disponible et l’échéance de l’installation. Choisissez d’utiliser le temps universel coordonné (UTC) ou l’heure locale de l’ordinateur qui exécute la console Configuration Manager.  

          - Quand vous sélectionnez ici **Heure locale du client**, puis **Dès que possible** pour le **Temps disponible du logiciel**, l’heure actuelle de l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer à quel moment les mises à jour sont disponibles. Ce comportement est le même avec l’**Échéance de l’installation** et l’heure à laquelle les mises à jour sont installées sur un client. Si le client se trouve dans un autre fuseau horaire, ces actions se produisent quand l’heure du client correspond à l’heure de l’évaluation.  

    -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

        -   **Dès que possible** : permet aux clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d’interrogation de la stratégie client, les clients prennent connaissance du déploiement et les mises à jour sont disponibles pour l’installation.  

        -   **Heure spécifique** : permet aux clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Au prochain cycle d’interrogation de la stratégie client, les clients prennent connaissance du déploiement. Cependant, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles pour l’installation avant la date et l’heure configurées.  

    -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement :  

        -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Configuration Manager détermine l’échéance d’installation des mises à jour logicielles en ajoutant l’intervalle **Heure spécifique** configuré au **Temps disponible du logiciel**.  

             - L’heure d’échéance de l’installation réelle est l’heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre deux heures. La randomisation réduit l’impact potentiel lié à l’installation simultanée, par les clients du regroupement, des mises à jour incluses dans le déploiement.  

             - Pour désactiver le délai de randomisation de l’installation pour les mises à jour logicielles requises, configurez le paramètre client sur **Désactiver la randomisation des échéances** dans le groupe **Agent ordinateur**. Pour plus d’informations, consultez [Paramètres client de l’Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent).  

    -  **Différer la mise en œuvre de ce déploiement selon les préférences de l’utilisateur, dans la limite de la période de grâce définie dans les paramètres client** : activez ce paramètre pour accorder aux utilisateurs plus de temps pour installer les mises à jour logicielles requises au-delà de l’échéance.  

        - Ce comportement est généralement obligatoire quand un ordinateur reste longuement inactif et qu’il nécessite l’installation de nombreuses applications ou mises à jour logicielles. Par exemple, quand un utilisateur rentre de congés, il peut être amené à patienter longuement, le temps que le client installe les déploiements en retard.  

        - Configurez cette période de grâce avec la propriété **Période de grâce pour la mise en œuvre après l’échéance du déploiement (en heures)** dans les paramètres client. Pour plus d’informations, consultez la section [Agent ordinateur](/sccm/core/clients/deploy/about-client-settings#computer-agent). La période de grâce de mise en œuvre s’applique à tous les déploiements pour lesquels cette option est activée et vise les appareils sur lesquels vous avez aussi déployé le paramètre client.  

        - Après l’échéance, le client installe les mises à jour logicielles au cours de la première fenêtre non ouvrée que l’utilisateur a configurée, dans la limite de cette période de grâce. Cependant, l’utilisateur peut toujours ouvrir le Centre logiciel et installer les mises à jour logicielles à tout moment. Une fois que la période de grâce a expiré, le comportement de mise en œuvre redevient normal pour les déploiements en retard.  

8. Dans la page **Expérience utilisateur**, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur** : indiquez si vous souhaitez afficher les notifications dans le Centre logiciel au **Temps disponible du logiciel** configuré. Ce paramètre contrôle également s’il faut avertir les utilisateurs sur les clients.  

    -   **Comportement à l’échéance** : spécifiez ce qui se passe quand le déploiement de mises à jour logicielles atteint l’échéance en dehors des fenêtres de maintenance définies. Vous pouvez entre autres choisir d’installer les mises à jour logicielles et d’exécuter un redémarrage du système après l’installation. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).  
        
        > [!Note]
        > Cela ne s’applique que si la fenêtre de maintenance est configurée pour l’appareil client. Si aucune fenêtre de maintenance n’est définie sur l’appareil, la mise à jour de l’installation et le redémarrage se produisent toujours après l’échéance.

    -   **Comportement de redémarrage du périphérique** : indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé si un redémarrage est nécessaire pour terminer l’installation des mises à jour.  

        > [!WARNING]  
        >  La suppression du redémarrage du système peut être utile dans les environnements de serveur ou quand vous ne souhaitez pas que les ordinateurs cibles redémarrent par défaut. Cependant, cela peut laisser les ordinateurs dans un état non sécurisé. Autoriser un redémarrage forcé aide à garantir l’exécution immédiate de l’installation des mises à jour logicielles.  

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded** : ce paramètre contrôle le comportement d’installation sur les appareils Windows Embedded qui sont activés avec un filtre d’écriture. Choisissez l’option permettant de valider les modifications à l’échéance de l’installation ou au cours d’une fenêtre de maintenance. Quand vous sélectionnez cette option, un redémarrage est nécessaire et les modifications sont conservées sur l’appareil. Sinon, la mise à jour est installée, appliquée sur l’overlay temporaire et validée ultérieurement.  

           -  Quand vous déployez une mise à jour logicielle sur un appareil Windows Embedded, vérifiez que l’appareil est membre d’un regroupement pour lequel une fenêtre de maintenance a été configurée.  

    - **Comportement de réévaluation du déploiement des mises à jour logicielles après le redémarrage** : sélectionnez ce paramètre pour configurer les déploiements de mises à jour logicielles de façon à ce que les clients exécutent une analyse de conformité des mises à jour logicielles immédiatement après avoir installé celles-ci et redémarré. Ce paramètre permet au client de rechercher d’autres mises à jour devenues applicables après son redémarrage, puis de les installer au cours d’une même fenêtre de maintenance.  

9. Dans la page **Alertes**, configurez la manière dont Configuration Manager génère des alertes pour ce déploiement. Examinez les alertes de mises à jour logicielles récentes de Configuration Manager dans le nœud **Mises à jour logicielles** de l’espace de travail **Bibliothèque de logiciels**. Si vous utilisez également System Center Operations Manager, configurez aussi ses alertes.  

10. Dans la page **Paramètres de téléchargement**, configurez les paramètres suivants :  

    - Indiquez si les clients doivent télécharger et installer les mises à jour quand ils utilisent un point de distribution d’un groupe voisin ou des groupes de limites de site par défaut.  

    - Indiquez si les clients doivent télécharger et installer les mises à jour logicielles à partir d’un point de distribution dans le groupe de limites de site par défaut quand le contenu des mises à jour logicielles n’est pas disponible à partir d’un point de distribution dans les groupes de limites actuels ou voisins.  

    - **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations, consultez [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). Depuis la version 1802, BranchCache est toujours activé sur les clients. Ce paramètre est supprimé, car les clients utilisent BranchCache si le point de distribution le prend en charge.  

    - **Si les mises à jour logicielles ne sont pas disponibles sur le point de distribution des groupes de limites actifs, voisins ou de site, télécharger le contenu à partir de Microsoft Updates** : sélectionnez ce paramètre pour que les clients connectés à l’intranet téléchargent les mises à jour logicielles à partir de Microsoft Update si les mises à jour ne sont pas disponibles sur les points de distribution. Les clients Internet accèdent toujours à Microsoft Update pour obtenir le contenu des mises à jour logicielles.  

    - Indiquez si les clients peuvent procéder au téléchargement une fois l’échéance de l’installation dépassée dans le cas où ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez quand vous utilisez une connexion facturée à l’usage.  

    > [!NOTE]  
    >  Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres dans cette page.   

11. Dans la page **Package de déploiement**, sélectionnez l’une des options suivantes :  

    - **Sélectionner un package de déploiement** : ajouter ces mises à jour à un package de déploiement existant.  

    - **Créer un package de déploiement** : ajoute ces mises à jour à un nouveau package de déploiement. Configurez les paramètres supplémentaires suivants :  

        -  **Nom**: spécifiez le nom du package de déploiement. Utilisez un nom unique qui décrit le contenu du package. Il est limité à 50 caractères.  

        -  **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description facultative est limitée à 127 caractères.  

        -  **Source du package**: spécifie l’emplacement des fichiers sources des mises à jour logicielles. Tapez un chemin réseau pour l’emplacement source, par exemple `\\server\sharename\path`, ou cliquez sur **Parcourir** pour rechercher l’emplacement réseau. Créez le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

            - Vous ne pouvez pas utiliser l’emplacement spécifié comme source d’un autre package de déploiement logiciel.  

            - Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Dans ce cas, copiez d’abord le contenu de la source du package d’origine dans le nouvel emplacement source du package.  

            -  Le compte d’ordinateur du fournisseur SMS et l’utilisateur qui exécute l’Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations d’**Écriture** sur l’emplacement de téléchargement. Limitez l’accès à l’emplacement de téléchargement. Cette restriction réduit le risque que des personnes malveillantes falsifient les fichiers sources des mises à jour logicielles.  

        -  **Priorité d’expédition**: spécifiez la priorité d’envoi pour le package de déploiement. Configuration Manager utilise cette priorité quand il envoie le package aux points de distribution. Les packages de déploiement sont envoyés par ordre de priorité : haute, moyenne ou faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. S’il n’y a pas de backlog, le package est traité immédiatement, quelle que soit sa priorité.  

        - **Activer la réplication différentielle binaire** : activez ce paramètre pour limiter le trafic réseau entre les sites. La réplication différentielle binaire met à jour uniquement le contenu qui a changé dans le package, au lieu de mettre à jour l’ensemble du contenu du package. Pour plus d’informations, consultez [Réplication différentielle binaire](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#binary-differential-replication).  

    - **Aucun package de déploiement** : depuis la version 1806, les mises à jour logicielles sont déployées sur les appareils sans que le contenu soit préalablement téléchargé et distribué aux points de distribution. Ce paramètre est particulièrement utile quand le contenu des mises à jour à traiter est extrêmement volumineux. Vous pouvez aussi l’utiliser quand vous voulez que les clients reçoivent systématiquement le contenu à partir du service cloud Microsoft Update. Dans ce cas, les clients peuvent également télécharger le contenu auprès d’homologues qui disposent déjà du contenu nécessaire. Le client Configuration Manager continue de gérer le téléchargement de contenu. Vous pouvez donc utiliser la fonctionnalité de cache d’homologue Configuration Manager ou d’autres technologies telles que l’optimisation de la distribution. Cette fonctionnalité prend en charge tous les types de mises à jour pris en charge par la gestion des mises à jour logicielles Configuration Manager, y compris les mises à jour Windows et Office.<!--1357933-->  

        > [!Note]  
        > Une fois cette option sélectionnée et les paramètres appliqués, elle n’est plus modifiable. Les autres options sont grisées.<!--SCCMDocs-pr issue 3003-->  

12. Dans la page **Points de distribution**, spécifiez les points de distribution ou les groupes de points de distribution où héberger les fichiers de mise à jour logicielle. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points#bkmk_configs). Cette page est disponible uniquement lorsque vous créez un nouveau package de déploiement de mise à jour logicielle.  
  

13. Dans la page **Emplacement de téléchargement**, indiquez si les fichiers de mise à jour logicielle doivent être téléchargés à partir d’Internet ou de votre réseau local. Configurez les paramètres suivants :  

    -   **Télécharger les mises à jour logicielles depuis Internet** : sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un emplacement spécifié sur Internet. Ce paramètre est activé par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un répertoire local ou d’un dossier partagé. Ce paramètre est utile quand l’ordinateur exécutant l’Assistant ne dispose d’aucun accès Internet. Tout ordinateur connecté à Internet peut télécharger préalablement les mises à jour logicielles, puis les stocker à un emplacement sur le réseau local auquel l’ordinateur exécutant l’Assistant peut accéder.  

14. Dans la page **Sélection de la langue**, sélectionnez les langues pour lesquelles le site télécharge les mises à jour logicielles sélectionnées. Le site télécharge uniquement ces mises à jour si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont pas propres à une langue sont toujours téléchargées. Par défaut, l’Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qu’une mise à jour logicielle ne prend pas en charge, le téléchargement de cette mise à jour échoue.  

15. Dans la page **Résumé** , vérifiez les paramètres. Pour enregistrer les paramètres dans un modèle de déploiement, cliquez sur **Enregistrer en tant que modèle**. Entrez un nom et sélectionnez les paramètres que vous souhaitez inclure dans le modèle, puis cliquez sur **Enregistrer**. Pour modifier un paramètre configuré, cliquez sur la page de l'Assistant associée et modifiez le paramètre.  

    -  Le nom du modèle peut comporter des caractères ASCII alphanumériques, ainsi que les caractères `\` (barre oblique inverse) ou `'` (guillemet-apostrophe).  

16. Cliquez sur **Suivant** pour créer la règle ADR.  

Une fois l’Assistant terminé, la règle ADR s’exécute. Elle ajoute les mises à jour logicielles qui remplissent les critères spécifiés dans un groupe de mises à jour logicielles. La règle ADR télécharge ensuite les mises à jour dans la bibliothèque de contenu sur le serveur de site, puis les distribue aux points de distribution configurés. Enfin, la règle ADR déploie le groupe de mises à jour logicielles sur les clients du regroupement cible.  



##  <a name="BKMK_AddDeploymentToADR"></a> Ajouter un nouveau déploiement à une règle ADR existante  

Après avoir créé une règle ADR, vous pouvez y ajouter des déploiements supplémentaires. Cela peut vous aider à gérer la complexité liée au déploiement de différentes mises à jour vers différents regroupements. Chaque nouveau déploiement possède la gamme complète de fonctionnalités et d'expérience de surveillance de déploiement.  


### <a name="process-to-add-a-new-deployment-to-an-existing-adr"></a>Pour ajouter un nouveau déploiement à une règle ADR existante  

1.  Dans la console de Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Mises à jour logicielles**, sélectionnez le nœud **Règles de déploiement automatique**, puis sélectionnez la règle souhaitée.  

2.  Dans le ruban, cliquez sur **Ajouter un déploiement**.   

3.  Dans la page **Regroupement** de l’Assistant Ajout de déploiement, configurez les paramètres disponibles de la même façon que dans la page **Général** de l’Assistant Création d’une règle de déploiement automatique. Pour plus d’informations, consultez la section précédente expliquant comment [créer une règle ADR](#bkmk_adr-process). Le reste de l’Assistant Ajout de déploiement comprend les pages suivantes, qui correspondent également aux descriptions détaillées ci-dessus :  

     - Paramètres de déploiement
     - Calendrier de déploiement
     - Expérience utilisateur
     - Alertes
     - Paramètres de téléchargement  

Les déploiements peuvent également être ajoutés par programmation à l’aide des cmdlets Windows PowerShell. Pour obtenir une description complète de l’utilisation de cette méthode, consultez [New-CMSoftwareUpdateDeployment](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmsoftwareupdatedeployment) .

Pour plus d’informations sur le processus de déploiement, consultez [Software update deployment process](/sccm/sum/understand/software-updates-introduction#BKMK_DeploymentProcess).


## <a name="next-steps"></a>Étapes suivantes
[Surveiller les mises à jour logicielles](monitor-software-updates.md)
