---
title: Déployer automatiquement des mises à jour logicielles
titleSuffix: Configuration Manager
description: Déployez automatiquement des mises à jour logicielles en ajoutant de nouvelles mises à jour logicielles à un groupe de mises à jour qui est associé à un déploiement actif ou en utilisant des règles ADR.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: b27682de-adf8-4edd-9572-54886af8f7fb
ms.openlocfilehash: 3b267e122370cc12ecec2f42dcb1dfc62c45fe63
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32353584"
---
#  <a name="BKMK_AutoDeploy"></a> Déployer automatiquement des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

 Vous pouvez utiliser une règle de déploiement automatique (ADR) au lieu d’ajouter de nouvelles mises à jour à un groupe de mises à jour logicielles existant. D’une manière générale, vous utilisez des règles ADR pour déployer les mises à jour logicielles mensuelles (appelées mises à jour Patch Tuesday) et pour gérer les mises à jour de définitions. Si vous avez besoin d’aide pour déterminer la méthode de déploiement qui vous convient, consultez [Déployer des mises à jour logicielles](deploy-software-updates.md).

<!--##  <a name="BKMK_AddUpdatesToExistingGroup"></a> Add software updates to a deployed update group  
After you create and deploy a software update group, you can add software updates to the update group and they will be automatically deployed.  

> [!IMPORTANT]  
>  When you add software updates to an existing software update group that has already been deployed, it might take several minutes before the additional software updates are added to the deployment.  

Use the following procedure to add software updates to an existing update group.  

#### To add software updates to an existing software update group  

1.  In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Software Updates**.  

2.  Select the software updates that are to be added to the new software update group.  

3.  On the **Home** tab, in the **Update** group, click **Edit Membership**.  

4.  Select the software update group to which you want to add the software updates as members.  

5.  Click the **Software Update Groups** node to display the software update group.  

6.  Click the software update group, and in the **Home** tab, in the **Update** group, click **Show Members** to display a list of the software updates in the group.  --mstewart this is already doc'd on the SUG page. -->

##  <a name="BKMK_CreateAutomaticDeploymentRule"></a> Créer une règle de déploiement automatique (ADR)  
Vous pouvez approuver et déployer automatiquement des mises à jour logicielles en utilisant une règle ADR. Vous pouvez faire en sorte que la règle ajoute des mises à jour logicielles à un nouveau groupe de mises à jour logicielles chaque fois qu'elle s'exécute ou vous pouvez ajouter des mises à jour logicielles à un groupe existant. Quand une règle s’exécute et ajoute des mises à jour logicielles à un groupe existant, elle supprime toutes les mises à jour du groupe, puis ajoute au groupe les mises à jour qui répondent aux critères que vous définissez. 

> [!WARNING]  
>  Avant de créer une règle ADR pour la première fois, vérifiez que la synchronisation des mises à jour logicielles est terminée sur le site. C’est important quand vous exécutez Configuration Manager dans une langue autre que l’anglais, car les classifications des mises à jour logicielles s’affichent en anglais avant la première synchronisation, puis s’affichent dans la langue localisée une fois la synchronisation des mises à jour logicielles terminée. Les règles que vous créez avant de synchroniser les mises à jour logicielles risquent ne pas fonctionner correctement après la synchronisation car la chaîne de texte peut ne pas correspondre.  

 Utilisez la procédure suivante pour créer une règle ADR.  

#### <a name="to-create-an-adr"></a>Pour créer une règle ADR  

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels****Vue d’ensemble** > **Mises à jour logicielles** > **Règles de déploiement automatique**.  

2.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une règle de déploiement automatique**. L'Assistant Création d'une règle de déploiement automatique s'ouvre.  

3.  Sur la page **Général** , configurez les paramètres suivants :  

    -   **Nom :** spécifiez le nom de la règle ADR. Le nom doit être unique, permettre de décrire l'objectif de la règle et être identifiable parmi d'autres dans le site Configuration Manager.  

    -   **Description :** spécifiez une description pour la règle ADR. La description doit fournir une présentation de la règle de déploiement et autres informations pertinentes permettant de la différencier des autres. Le champ de description facultatif est limité à 256 caractères et est vierge par défaut.  

    -   **Sélectionner un modèle de déploiement**: indiquez si un modèle de déploiement enregistré précédemment doit être appliqué. Vous pouvez configurer un modèle de déploiement contenant plusieurs propriétés de déploiement de mise à jour communes, utilisables pour créer des règles ADR. Ces modèles permettent de garantir la cohérence entre des déploiements similaires et de gagner du temps.  

         - Vous pouvez opter pour l’un des modèles de déploiement de mises à jour logicielles prédéfinis à partir de l’Assistant Création d’une règle de déploiement automatique. Le modèle **Mises à jour de définitions** fournit des paramètres communs à utiliser lorsque vous déployez des mises à jour logicielles de définitions. Le modèle **Patch Tuesday** fournit des paramètres communs à utiliser lorsque vous déployez des mises à jour logicielles selon un cycle mensuel.  

    -   **Regroupement**: indique le regroupement cible à utiliser pour le déploiement. Les membres du regroupement reçoivent les mises à jour logicielles définies dans le déploiement.  

    -   déterminer si des mises à jour logicielles seront ajoutées à un groupe de mises à jour logicielles nouveau ou existant. Dans la plupart des cas, vous choisirez probablement de créer un nouveau groupe de mises à jour logicielles au moment d’exécuter la règle ADR. Toutefois, vous pouvez choisir d'utiliser un groupe existant, si la règle s'exécute selon une planification plus agressive. Par exemple, si vous exécutez la règle quotidiennement pour des mises à jour de définitions, vous pouvez ajouter les mises à jour logicielles à un groupe de mises à jour logicielles existant.  

    -   **Activer le déploiement après l’exécution de cette règle**: indiquez si le déploiement des mises à jour logicielles doit être activé après l’exécution de la règle ADR. En ce qui concerne cette spécification, tenez compte des éléments suivants :  

        -   Quand vous activez le déploiement, les mises à jour qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles. Le contenu des mises à jour logicielles est téléchargé en fonction. Le contenu est copié vers les points de distribution spécifiés et les mises à jour sont déployées sur les clients du regroupement cible.  

        -   Quand vous n’activez pas le déploiement, les mises à jour qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles. La stratégie de déploiement de mises à jour logicielles est configurée. Toutefois, les mises à jour ne sont pas téléchargées ou déployées sur les clients. Ce cas de figure vous laisse le temps de préparer le déploiement des mises à jour, de vérifier que les mises à jour répondant aux critères sont adéquates, puis d’activer le déploiement plus tard.  

4.  Sur la page Paramètres de déploiement, configurez les paramètres suivants :  

    -   **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis**: indique si l’éveil par appel réseau (Wake On LAN) doit être activé à l’échéance pour envoyer des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles du déploiement. Tous les ordinateurs en mode veille à l’échéance de l’installation sont mis en éveil pour que l’installation puisse démarrer. Les clients en mode veille qui ne nécessitent pas les mises à jour logicielles incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n'est pas activé. Avant de pouvoir utiliser cette option, vous devez configurer les ordinateurs et les réseaux pour l'éveil par appel réseau. 

    -   **Niveau de détail**: indiquez le niveau de détail pour les messages d’état qui sont signalés par les ordinateurs clients.  

        > [!IMPORTANT]  
        >  Quand vous déployez des mises à jour de définitions, définissez le niveau de détails sur **Erreur uniquement** pour que le client envoie un message d'état uniquement si une mise à jour de définition échoue. Sinon, le client envoie un grand nombre de messages d'état pouvant avoir un effet sur les performances du serveur de site.  

    -   **Paramètre du contrat de licence**: indiquez si les mises à jour logicielles doivent être déployées automatiquement avec un contrat de licence associé. Certaines mises à jour logicielles comprennent un contrat de licence, dans le cas d'un Service Pack par exemple. Lorsque vous déployez automatiquement des mises à jour logicielles, le contrat de licence ne s'affiche pas et il n'est pas possible d'accepter le contrat de licence. Vous pouvez choisir de déployer automatiquement toutes les mises à jour logicielles indépendamment d'un contrat de licence associé ou de déployer uniquement les mises à jour qui ne sont associées à aucun contrat de licence.  
        - Pour consulter le contrat de licence d’une mise à jour logicielle, vous pouvez sélectionner la mise à jour logicielle dans le nœud **Toutes les mises à jour logicielles** de l’espace de travail **Bibliothèque de logiciels**. Sous l’onglet **Accueil**, dans le groupe **Mise à jour** , cliquez sur **Consulter la licence**.    
        - Pour trouver des mises à jour logicielles avec un contrat de licence associé, vous pouvez ajouter la colonne **Termes du contrat de licence** dans le volet des résultats du nœud **Toutes les mises à jour logicielles**. Cliquez sur l’en-tête de la colonne pour trier les mises à jour logicielles associées à un contrat de licence.  

5.  Dans la page Mises à jour logicielles, configurez les critères des mises à jour logicielles que la règle ADR récupère et ajoute au groupe de mises à jour logicielles. Dans une règle ADR, le nombre limite de mises à jour logicielles est de 1 000. Si besoin, vous pouvez filtrer sur la taille du contenu des mises à jour logicielles dans les règles de déploiement automatique. Pour plus d’informations, consultez [Configuration Manager et maintenance Windows simplifiée sur des systèmes d’exploitation de bas niveau](https://blogs.technet.microsoft.com/enterprisemobility/2016/10/07/configuration-manager-and-simplified-windows-servicing-on-down-level-operating-systems/).


6.  Dans la page Calendrier d’évaluation, indiquez si l’exécution de la règle ADR doit obéir à un calendrier. Si elle est activée, cliquez sur **Personnaliser** pour définir le calendrier périodique. La configuration de l'heure de début du calendrier se base sur l'heure locale de l'ordinateur qui exécute la console Configuration Manager.
    - La configuration de l'heure de début du calendrier se base sur l'heure locale de l'ordinateur qui exécute la console Configuration Manager.
    - La règle ADR peut être évaluée jusqu’à trois fois par jour.
    - Ne définissez jamais le calendrier d’évaluation selon une fréquence supérieure au calendrier de synchronisation des mises à jour logicielles. Le calendrier de synchronisation du point de mise à jour logicielle s’affiche pour vous aider à déterminer la fréquence du calendrier d’évaluation. 
    - Pour exécuter manuellement la règle ADR, sélectionnez la règle, puis cliquez sur **Exécuter maintenant** sous l’onglet **Accueil** dans le groupe **Règle de déploiement automatique** .
    
       > [!NOTE]  
       >À compter de Configuration Manager version 1802, les règles ADR peuvent être planifiées pour évaluer le décalage à partir d’un jour de base. Cela signifie que si le correctif Mardi tombe en fait un mercredi pour vous, vous pouvez définir le calendrier d’évaluation pour le deuxième mardi du mois avec un décalage d’un jour. <!--1357133-->
       > - Quand la planification de l’évaluation se présente avec un décalage au cours de la dernière semaine du mois, l’évaluation est planifiée le dernier jour du mois si le décalage choisi dépasse sur le mois suivant. <!--506731-->

       > ![Décalage de la planification d’évaluation personnalisée ADR à partir du jour de base](./media/ADR-evaluation-schedule-offset.PNG)

   
7.  Sur la page Calendrier de déploiement, configurez les paramètres suivants :  

    -   **Calendrier d’évaluation** : indiquez si Configuration Manager évalue la durée disponible et la date d’échéance de l’installation à l’heure UTC ou à l’heure locale de l’ordinateur exécutant la console Configuration Manager.  
         - Si vous sélectionnez l’heure locale, puis **Dès que possible** pour le **Temps disponible du logiciel** ou **Échéance d’installation**, l’heure actuelle sur l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer quand les mises à jour sont disponibles ou quand elles sont installées sur un client. Si le client est dans un autre fuseau horaire, ces actions se produisent quand l’heure du client atteint l’heure de l’évaluation.  

    -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

        -   **Dès que possible** : permet aux ordinateurs clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d’interrogation de la stratégie cliente, les clients prennent connaissance du déploiement et peuvent obtenir les mises à jour disponibles à l’installation.  

        -   **Heure spécifique** : permet aux ordinateurs clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement. Toutefois, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles à l'installation avant la date et l'heure configurées.  

    -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement :  

        -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Configuration Manager détermine l’échéance d’installation des mises à jour logicielles en ajoutant l’intervalle **Heure spécifique** configuré au **Temps disponible du logiciel**.  

            - L’heure d’échéance de l’installation réelle est l’heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre deux heures. La randomisation réduit l’impact lié à l’installation simultanée, par les ordinateurs clients du regroupement, des mises à jour incluses dans le déploiement.  
          
             - Vous pouvez configurer le paramètre client **Agent ordinateur** , **Désactiver la randomisation des échéances** , pour désactiver le délai de randomisation de l’installation des mises à jour logicielles requises. Pour plus d’informations, voir [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8. Sur la page Expérience utilisateur, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur**: indiquez si vous souhaitez afficher les notifications des mises à jour logicielles dans le Centre logiciel sur l’ordinateur client selon la valeur **Temps disponible du logiciel** configuré et si les notifications à l’utilisateur doivent s’afficher sur les ordinateurs clients.  

    -   **Comportement à l’échéance**: spécifiez le comportement qui doit se produire lorsque l’échéance est atteinte pour le déploiement des mises à jour logicielles. Indiquez si vous souhaitez installer les mises à jour logicielles incluses dans le déploiement. Spécifiez également si un redémarrage du système doit être effectué après l'installation des mises à jour logicielles, quelle que soit la fenêtre de maintenance configurée. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportement de redémarrage du périphérique** : indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé si un redémarrage est nécessaire pour terminer l’installation des mises à jour.  

        > [!WARNING]  
        >  La suppression du redémarrage système peut s'avérer utile dans les environnements de serveurs ou lorsque vous ne souhaitez pas que les ordinateurs qui installent les mises à jour logicielles redémarrent par défaut. Toutefois, elle peut laisser les ordinateurs dans un état non sécurisé, alors que l'autorisation d'un redémarrage forcé contribue à garantir l'exécution immédiate de l'installation des mises à jour logicielles.  

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded**: quand vous déployez des mises à jour logicielles sur des appareils Windows Embedded pour lesquels le filtre d’écriture est activé, vous pouvez choisir d’installer la mise à jour logicielle sur le segment de recouvrement temporaire et valider les modifications ultérieurement ou à l’échéance de l’installation ou bien pendant une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

           -  Lorsque vous déployez une mise à jour logicielle sur un appareil Windows Embedded, assurez-vous que l’appareil fait partie des membres d’un regroupement pour lequel une fenêtre de maintenance a été configurée.  

    - **Comportement de réévaluation du déploiement des mises à jour logicielles après le redémarrage** : sélectionnez ce paramètre pour configurer les déploiements de mises à jour logicielles de façon à ce que les clients exécutent une analyse de conformité des mises à jour logicielles immédiatement après avoir installé celles-ci et redémarré. Ce paramètre permet au client de rechercher d’autres mises à jour devenues applicables après son redémarrage, puis de les installer au cours d’une même fenêtre de maintenance.

9. Sur la page Alertes, configurez la manière dont Configuration Manager et System Center Operations Manager génèreront des alertes pour ce déploiement. Vous pouvez consulter les récentes alertes de mises à jour logicielles à partir du nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

10. Sur la page Paramètres de téléchargement, configurez les paramètres suivants :  

    - Indiquez si les clients doivent télécharger et installer les mises à jour quand ils sont connectés à un réseau lent ou utilise un emplacement de secours pour le contenu.  

    - Indiquez si les clients doivent télécharger et installer les mises à jour logicielles à partir d’un point de distribution de secours quand le contenu pour les mises à jour logicielles n’est pas disponible sur un point de distribution préféré.  

    - **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations sur BrandCache, consultez [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Si les mises à jour logicielles ne sont pas disponibles sur le point de distribution de groupes actuels, voisins ou de site, téléchargez le contenu à partir de Microsoft Updates** : sélectionnez ce paramètre afin que les clients connectés à l’intranet téléchargent les mises à jour logicielles depuis Microsoft Update si les mises à jour ne sont pas disponibles sur les points de distribution. Les clients Internet peuvent toujours accéder à Microsoft Update pour obtenir le contenu des mises à jour logicielles.

    - Indiquez si les clients peuvent procéder au téléchargement une fois l’échéance de l’installation dépassée dans le cas où ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

    > [!NOTE]  
    >  Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres sur cette page. Pour plus d'informations, voir [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Sur la page Package de déploiement, sélectionnez un package de déploiement existant ou configurez les paramètres suivants pour créer un package de déploiement :  

    1.  **Nom**: spécifiez le nom du package de déploiement. Utilisez un nom unique qui décrit le contenu du package. Il est limité à 50 caractères.  

    2.  **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description est limitée à 127 caractères.  

    3.  **Source du package**: spécifie l’emplacement des fichiers sources des mises à jour logicielles.  Tapez un chemin réseau pour l’emplacement source, par exemple **\\\serveur\nom_partage\chemin**ou cliquez sur **Parcourir** pour rechercher l’emplacement réseau. Créez le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

        - L'emplacement source du package de déploiement spécifié ne peut pas être utilisé par un autre package de déploiement de logiciel.
        - Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Mais le cas échéant, vous devez d’abord copier le contenu à partir de la source du package d’origine vers le nouvel emplacement source du package.  
        -  Le compte d'ordinateur du fournisseur SMS et l'utilisateur qui exécute l'Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations NTFS en **Écriture** sur l'emplacement de téléchargement. Vous devez soigneusement limiter l'accès à l'emplacement de téléchargement pour éviter que des personnes malintentionnées ne falsifient les fichiers sources des mises à jour logicielles.  
       

    4.  **Priorité d’expédition**: spécifiez la priorité d’envoi pour le package de déploiement. Configuration Manager utilise la priorité d’expédition du package de déploiement quand il envoie le package aux points de distribution. Les packages de déploiement sont envoyés par ordre de priorité : Haute, Moyenne ou Faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. En l'absence de backlog, le package est immédiatement traité quelle que soit sa priorité.  

12. Sur la page Points de distribution, spécifiez les points de distribution ou les groupes de points de distribution qui vont héberger les fichiers de mise à jour logicielle. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Cette page est disponible uniquement lorsque vous créez un nouveau package de déploiement de mise à jour logicielle.
  

13. Sur la page Emplacement de téléchargement, indiquez si les fichiers de mise à jour logicielle doivent être téléchargés à partir d'Internet ou de votre réseau local. Configurez les paramètres suivants :  

    -   **Télécharger les mises à jour logicielles depuis Internet**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un emplacement spécifié sur Internet. Ce paramètre est activé par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un répertoire local ou d’un dossier partagé. Ce paramètre s'avère utile lorsque l'ordinateur exécutant l'Assistant ne dispose d'aucun accès à Internet. N'importe quel ordinateur connecté à Internet peut préalablement télécharger les mises à jour logicielles et les stocker à un emplacement sur le réseau local qui est accessible à partir de l'ordinateur qui exécute l'Assistant.  

14. Sur la page Sélection de la langue, sélectionnez les langues pour lesquelles les mises à jour logicielles sélectionnées sont téléchargées. Les mises à jour logicielles sont téléchargées uniquement si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont spécifiques à aucune langue sont toujours téléchargées. Par défaut, l'Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qui ne sont pas prises en charge par une mise à jour logicielle, le téléchargement échoue pour cette mise à jour.  

15. Sur la page Résumé, passez en revue les paramètres. Pour enregistrer les paramètres dans un modèle de déploiement, cliquez sur **Enregistrer en tant que modèle**. Entrez un nom et sélectionnez les paramètres que vous souhaitez inclure dans le modèle, puis cliquez sur **Enregistrer**. Pour modifier un paramètre configuré, cliquez sur la page de l'Assistant associée et modifiez le paramètre.  
    -  Le nom du modèle peut comporter des caractères ASCII alphanumériques ainsi que les caractères **\\** (barre oblique inverse) ou **‘** (guillemet-apostrophe).  

16. Cliquez sur **Suivant** pour créer la règle ADR.  

 La règle ADR s’exécute une fois que vous avez terminé l’Assistant. Cela ajoute les mises à jour logicielles qui remplissent les critères spécifiés dans un groupe de mises à jour logicielles. La règle ADR télécharge ensuite les mises à jour dans la bibliothèque de contenu sur le serveur de site, puis les distribue aux points de distribution configurés. Enfin, la règle ADR déploie le groupe de mises à jour logicielles sur les clients du regroupement cible.  

##  <a name="BKMK_AddDeploymentToADR"></a> Ajouter un nouveau déploiement à une règle ADR existante  
 Après avoir créé une règle de déploiement automatique, vous pouvez y ajouter des déploiements supplémentaires. Cela peut vous aider à gérer la complexité liée au déploiement de différentes mises à jour vers différents regroupements. Chaque nouveau déploiement possède la gamme complète de fonctionnalités et d'expérience de surveillance de déploiement.  

#### <a name="to-add-a-new-deployment-to-an-existing-adr"></a>Pour ajouter un nouveau déploiement à une règle ADR existante  

1.  Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Mises à jour logicielles** > **Règles de déploiement automatique**, puis sélectionnez la règle de votre choix.  

2.  Sous l’onglet **Accueil** , dans le groupe **Règle de déploiement automatique** , cliquez sur **Ajouter un déploiement**. L’Assistant Ajout de déploiement s’ouvre.  

3.  Dans la page **Regroupement** , configurez les paramètres suivants :  

    -   **Regroupement**: indique le regroupement cible à utiliser pour le déploiement. Les membres du regroupement reçoivent les mises à jour logicielles définies dans le déploiement.  

    -   **Activer le déploiement après l’exécution de cette règle**: indiquez si le déploiement des mises à jour logicielles doit être activé après l’exécution de la règle ADR. En ce qui concerne cette spécification, tenez compte des éléments suivants :  

        -   Quand vous activez le déploiement, les mises à jour qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles. Le contenu des mises à jour logicielles est téléchargé en fonction. Le contenu est copié vers les points de distribution spécifiés et les mises à jour sont déployées sur les clients du regroupement cible.  

        -  Quand vous n’activez pas le déploiement, les mises à jour qui répondent aux critères définis dans la règle sont ajoutées à un groupe de mises à jour logicielles. La stratégie de déploiement de mises à jour logicielles est configurée. Toutefois, les mises à jour ne sont pas téléchargées ou déployées sur les clients. Ce cas de figure vous laisse le temps de préparer le déploiement des mises à jour, de vérifier que les mises à jour répondant aux critères sont adéquates, puis d’activer le déploiement plus tard.  

4.  Sur la page Paramètres de déploiement, configurez les paramètres suivants :  

    -   **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis**: indique si l’éveil par appel réseau (Wake On LAN) doit être activé à l’échéance pour envoyer des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles du déploiement. Tous les ordinateurs en mode veille à l’échéance de l’installation sont mis en éveil pour que l’installation puisse démarrer. Les clients en mode veille qui ne nécessitent pas les mises à jour logicielles incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n'est pas activé. Avant de pouvoir utiliser cette option, vous devez configurer les ordinateurs et les réseaux pour l'éveil par appel réseau.  

    -   **Niveau de détail**: indiquez le niveau de détail pour les messages d’état qui sont signalés par les ordinateurs clients.  

        > [!IMPORTANT]  
        >  Lorsque vous déployez des mises à jour de définitions, affectez au niveau de détails la valeur **Erreur uniquement** pour que le client envoie un message d'état uniquement lorsqu'une mise à jour de définition ne lui est pas remise. Sinon, le client envoie un grand nombre de messages d'état pouvant avoir un effet sur les performances du serveur de site.  

5.  Sur la page Calendrier de déploiement, configurez les paramètres suivants :  

    -   **Calendrier d’évaluation** : indiquez si Configuration Manager évalue la durée disponible et la date d’échéance de l’installation à l’heure UTC ou à l’heure locale de l’ordinateur exécutant la console Configuration Manager.  

           -  Si vous sélectionnez l’heure locale, puis **Dès que possible** pour le **Temps disponible du logiciel** ou **Échéance d’installation**, l’heure actuelle sur l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer quand les mises à jour sont disponibles ou quand elles sont installées sur un client. Si le client est dans un autre fuseau horaire, ces actions se produisent quand l’heure du client atteint l’heure de l’évaluation.  

    -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles sont disponibles pour les clients :  

        -   **Dès que possible**: sélectionnez ce paramètre pour permettre aux ordinateurs clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Quand vous créez le déploiement avec ce paramètre sélectionné, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d’interrogation de la stratégie cliente, les clients prennent connaissance du déploiement et peuvent obtenir les mises à jour disponibles à l’installation.  

        -   **Heure spécifique** : permet aux ordinateurs clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Quand vous créez le déploiement avec ce paramètre activé, Configuration Manager met à jour la stratégie client. Ensuite, au prochain cycle d'interrogation de la stratégie client, les clients prennent connaissance du déploiement. Toutefois, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles à l'installation avant la date et l'heure configurées. 

    -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement :  

        -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Configuration Manager détermine l’échéance d’installation des mises à jour logicielles en ajoutant l’intervalle **Heure spécifique** configuré au **Temps disponible du logiciel**.  

               - L’heure d’échéance de l’installation réelle est l’heure d'échéance affichée plus un laps de temps aléatoire pouvant atteindre deux heures. Cela réduit l’impact lié à l’installation simultanée, par les ordinateurs clients du regroupement, des mises à jour incluses dans le déploiement.  
              - Vous pouvez configurer le paramètre client **Agent ordinateur** , **Désactiver la randomisation des échéances** , pour désactiver le délai de randomisation de l’installation des mises à jour logicielles requises. Pour plus d’informations, voir [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

6.  Sur la page Expérience utilisateur, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur**: indiquez si vous souhaitez afficher les notifications des mises à jour logicielles dans le Centre logiciel sur l’ordinateur client selon la valeur **Temps disponible du logiciel** configuré et si les notifications à l’utilisateur doivent s’afficher sur les ordinateurs clients.  

    -   **Comportement à l’échéance**: spécifiez le comportement qui doit se produire lorsque l’échéance est atteinte pour le déploiement des mises à jour logicielles. Indiquez si vous souhaitez installer les mises à jour logicielles incluses dans le déploiement. Spécifiez également si un redémarrage du système doit être effectué après l'installation des mises à jour logicielles, quelle que soit la fenêtre de maintenance configurée. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportement de redémarrage du périphérique** : indiquez si le redémarrage du système sur les serveurs et stations de travail doit être supprimé si un redémarrage est nécessaire pour terminer l’installation des mises à jour.  
 
           > [!WARNING]  
           >  La suppression du redémarrage système peut s'avérer utile dans les environnements de serveurs ou lorsque vous ne souhaitez pas que les ordinateurs qui installent les mises à jour logicielles redémarrent par défaut. Toutefois, elle peut laisser les ordinateurs dans un état non sécurisé, alors que l'autorisation d'un redémarrage forcé contribue à garantir l'exécution immédiate de l'installation des mises à jour logicielles.  

    - **Traitement des filtres d’écriture pour les appareils Windows Embedded**: quand vous déployez des mises à jour logicielles sur des appareils Windows Embedded pour lesquels le filtre d’écriture est activé, vous pouvez choisir d’installer la mise à jour logicielle sur le segment de recouvrement temporaire et valider les modifications ultérieurement ou à l’échéance de l’installation ou bien pendant une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

        - Lorsque vous déployez une mise à jour logicielle sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée.  

7.  Sur la page Alertes, configurez la manière dont Configuration Manager et System Center Operations Manager génèreront des alertes pour ce déploiement. Vous pouvez consulter les récentes alertes de mises à jour logicielles à partir du nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

8. Sur la page Paramètres de téléchargement, configurez les paramètres suivants :  

    - Indiquez si les clients doivent télécharger et installer les mises à jour logicielles quand ils sont connectés à un réseau lent ou utilise un emplacement de secours pour le contenu.  

    - Indiquez si le client doit télécharger et installer les mises à jour logicielles à partir d'un point de distribution de secours quand le contenu pour les mises à jour logicielles n'est pas disponible sur un point de distribution préféré.  

    - **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations sur BrandCache, consultez [Concepts for content management](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Si les mises à jour logicielles ne sont pas disponibles sur le point de distribution de groupes actuels, voisins ou de site, téléchargez le contenu à partir de Microsoft Updates** : sélectionnez ce paramètre afin que les clients connectés à l’intranet téléchargent les mises à jour logicielles depuis Microsoft Update si les mises à jour ne sont pas disponibles sur les points de distribution. Les clients Internet peuvent toujours accéder à Microsoft Update pour obtenir le contenu des mises à jour logicielles.

    - Indiquez si les clients peuvent procéder au téléchargement une fois l’échéance de l’installation dépassée dans le cas où ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

    > [!NOTE]  
    > Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres sur cette page. Pour plus d'informations, voir [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

Pour plus d’informations sur le processus de déploiement, consultez [Software update deployment process](../../sum/understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Étapes suivantes
[Surveiller les mises à jour logicielles](monitor-software-updates.md)
