---
title: Déployer une séquence de tâches
titleSuffix: Configuration Manager
description: Suivez ces informations pour déployer une séquence de tâches sur les ordinateurs d’un regroupement.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b2abcdb0-72e0-4c70-a4b8-7827480ba5b2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18179301fc6edcc9148e8bff353a5e14c1b0f210
ms.sourcegitcommit: ab9f2a7fb7ea3a0c65808fce2975ab25a670281f
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/14/2019
ms.locfileid: "65613034"
---
# <a name="deploy-a-task-sequence"></a>Déployer une séquence de tâches

Une fois que vous avez créé une séquence de tâches et distribué le contenu associé, déployez-la sur un regroupement d’appareils pour qu’elle puisse s’exécuter sur un appareil. Une séquence de tâches déployée peut s’exécuter automatiquement, ou lors de l’installation par l’utilisateur de l’appareil.

> [!WARNING]  
> Vous pouvez gérer le comportement des déploiements de séquences de tâches à haut risque. Un déploiement à haut risque est un déploiement qui est installé automatiquement et qui est susceptible d'entraîner des résultats indésirables. Par exemple, une séquence de tâches ayant comme objectif **Obligatoire** qui déploie un système d’exploitation est considérée comme un déploiement à haut risque. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  


## <a name="process"></a>Processus

Pour déployer une séquence de tâches sur les ordinateurs d'un regroupement, procédez comme suit.  

> [!NOTE]  
> Les messages d’état du déploiement d’une séquence de tâches apparaissent dans la fenêtre de message sur un site principal, mais non sur un site d’administration centrale.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous voulez déployer.  

3. Sous l’onglet **Accueil** du ruban, sélectionnez **Déployer** dans le groupe **Déploiement**.  

    > [!NOTE]  
    > Si **Déployer** n’est pas disponible, c’est le signe que la séquence de tâches comporte une référence non valide. Corrigez la référence, puis tentez de déployer à nouveau la séquence de tâches.  

4. Dans la page **Général**, spécifiez les informations suivantes.  

    - **Séquence de tâches** : indiquez la séquence de tâches à déployer. Par défaut, cette zone affiche la séquence de tâches sélectionnée.  

    - **Regroupement** : sélectionnez le regroupement contenant les ordinateurs qui exécuteront la séquence de tâches.  

        Ne déployez pas une séquence de tâches qui installe un système d’exploitation sur des regroupements inappropriés, par exemple, le regroupement de tous les serveurs de votre centre de données. Le regroupement sélectionné ne doit contenir que les ordinateurs qui exécuteront la séquence de tâches.  

        Pour plus d’informations sur les déploiements à haut risque, Voir [Déploiements à haut risque](#bkmk_high-risk).

    - **Utiliser les groupes de points de distribution par défaut associés à ce regroupement** : stockez le contenu de la séquence de tâches dans le groupe de points de distribution par défaut du regroupement. Si vous n’avez associé aucun groupe de points de distribution au regroupement sélectionné, cette option est grisée.  

    - **Distribuer automatiquement le contenu des dépendances** : si le contenu référencé comporte des dépendances, le site envoie aussi le contenu dépendant aux points de distribution.  

    - **Prétélécharger le contenu de cette séquence de tâches** : pour plus d’informations, voir [Configurer la mise en cache préalable du contenu](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  

    - **Sélectionner le modèle de déploiement** : à compter de Configuration Manager version 1802,<!--1357391--> vous pouvez enregistrer et spécifier un modèle de déploiement pour une séquence de tâches.  

        > [!IMPORTANT]  
        > Dans la version 1802 de Configuration Manager, certains éléments ne sont pas enregistrés dans le modèle.  <!--510610--> Veillez à appliquer les éléments suivants quand vous exécutez l’Assistant Déploiement :  
        >
        > - Installation des logiciels
        > - Planification
        > - Prétélécharger le contenu

    - **Commentaires (facultatif) :** spécifiez des informations supplémentaires qui décrivent ce déploiement de la séquence de tâches.  

5. Dans la page **Paramètres de déploiement**, spécifiez les informations suivantes :  

    - **Objet**: dans la liste déroulante, choisissez l’une des options suivantes :  

        - **Disponible** : l’utilisateur voit la séquence de tâches dans le Centre logiciel et peut l’installer à la demande.  

        - **Obligatoire** : Configuration Manager exécute automatiquement la séquence de tâches suivant le planning configuré. Si la séquence de tâches n’est pas masquée, l’utilisateur peut toujours suivre son état de déploiement. Il peut également utiliser le Centre logiciel pour installer la séquence de tâches avant l’échéance.  

        > [!NOTE]
        > Si plusieurs utilisateurs sont connectés à l’appareil, les déploiements de package et de séquences de tâches peuvent ne pas s’afficher dans le centre logiciel.  

    - **Rendre disponible aux éléments suivants** : indiquez si la séquence de tâches est accessible aux types suivants :  

        - Clients Configuration Manager uniquement  
        - Clients, média et environnement PXE Configuration Manager  
        - Média et environnement PXE uniquement  
        - Média et environnement PXE uniquement (masqué)  

        > [!IMPORTANT]  
        > Utilisez le paramètre **Média et environnement PXE uniquement (masqué)** pour les déploiements de séquence de tâches automatisés. Pour que l’ordinateur démarre automatiquement sur le déploiement sans l’intervention de l’utilisateur, sélectionnez **Autoriser le déploiement automatisé du système d’exploitation** et définissez la variable **SMSTSPreferredAdvertID** dans le média. Pour plus d’informations sur les variables de séquence de tâches, voir [Variables de séquences de tâches](/sccm/osd/understand/task-sequence-variables#SMSTSPreferredAdvertID).  

    - **Envoyer des paquets de mise en éveil** : si le déploiement est **Obligatoire** et que cette option est sélectionnée, Configuration Manager envoie un paquet de mise en éveil aux ordinateurs avant que le client n’exécute le déploiement. Ce paquet réveille les ordinateurs à l’échéance de l’installation. Avant d’utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour Wake On LAN. Pour plus d’informations, consultez [Planifier la sortie de veille des clients](/sccm/core/clients/deploy/plan/plan-wake-up-clients).  

    - **Autoriser les clients utilisant une connexion Internet facturée à l’usage à télécharger le contenu après l’échéance d’installation, ce qui peut entraîner des frais supplémentaires** : cette option n’est disponible que pour les déploiements **Obligatoires**. Lorsque votre séquence de tâches personnalisée installe une application, mais qu’elle ne déploie pas de système d’exploitation, vous pouvez choisir d’autoriser ou non les clients à télécharger du contenu après l’échéance d’installation lorsqu’ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données utilisée sur une connexion Internet facturée à l’usage.  

        > [!NOTE]  
        > L’utilisation d’une connexion Internet facturée à l’usage pourrait fonctionner avec les séquences de tâches qui ne déploient pas de système d’exploitation, mais cette possibilité n’est pas prise en charge.  

6. Sur la page **Planification**, spécifiez les informations suivantes :  

    > [!IMPORTANT]  
    > Quand un client Windows PE démarre à partir d’un média de démarrage ou d’un environnement PXE, il n’évalue pas les plannings de déploiement (heures de démarrage, d’expiration et d’échéance). Configurez des planifications de déploiements uniquement sur des clients qui démarrent à partir du système d’exploitation Windows complet. Appliquez d'autres méthodes, telles que des fenêtres de maintenance, pour contrôler les séquences de tâches actives déployées sur les clients qui démarrent à partir de Windows PE.  

    - **Planifier la disponibilité de ce déploiement**: spécifiez la date et l’heure auxquelles la séquence de tâches est disponible pour s’exécuter sur l’ordinateur de destination. Lorsque l’option **UTC** est sélectionnée, la séquence de tâches est accessible à plusieurs ordinateurs en même temps. Sinon, le déploiement est disponible à des moments différents, selon l’heure locale de chaque ordinateur.  

        Si l’heure de début est antérieure à l’heure requise, le client télécharge le contenu de la séquence de tâches à l’heure de début.  

    - **Planifier la disponibilité de ce déploiement**: spécifiez la date et l’heure d’expiration de la séquence de tâches sur l’ordinateur de destination. Lorsque l’option **UTC** est sélectionnée, la séquence de tâches arrive à expiration sur plusieurs ordinateurs de destination en même temps. Sinon, le déploiement expire à des moments différents, selon l’heure locale de chaque ordinateur.  

    - **Calendrier des affectations** : pour un déploiement **Obligatoire**, spécifiez à quel moment le client exécute la séquence de tâches. Vous pouvez ajouter plusieurs calendriers. Le calendrier des affectations peut avoir les configurations suivantes :  

        - Date et heure spécifiques  
        - Périodicité mensuelle, hebdomadaire ou personnalisée  
        - Dès que possible  
        - Événements d’ouverture et de fermeture de session  

        > [!NOTE]  
        > Si, pour un déploiement obligatoire, vous planifiez une heure de début antérieure à la date et à l’heure de disponibilité de la séquence de tâches, le client Configuration Manager télécharge le contenu à l’heure de début affectée, et ce, même si la séquence de tâches est programmée pour être disponible plus tard.<!--SCCMDocs issue 777-->  

    - **Comportement de réexécution** : spécifiez quand la séquence de tâches s’exécute à nouveau. Sélectionnez l'une des options suivantes :  

        - **Ne jamais exécuter à nouveau un programme déployé** : si le client a déjà exécuté la séquence de tâches, il ne la réexécute pas. La séquence de tâches ne se réexécute pas même si elle a échoué initialement ou si ses fichiers associés ont changé.  

        - **Toujours exécuter à nouveau le programme** : la séquence de tâches s’exécute toujours une nouvelle fois sur le client lorsque le déploiement est planifié, même si elle s’est déjà exécutée avec succès. Ce paramètre est utile pour les déploiements périodiques dans lesquels la séquence de tâches est régulièrement mise à jour.  

            > [!IMPORTANT]  
            > Cette option est activée par défaut. Toutefois, elle n’a aucun effet tant qu’aucun déploiement obligatoire n’a été affecté. L’utilisateur peut toujours exécuter à nouveau des déploiements disponibles.  

        - **Exécuter à nouveau en cas d’échec de la tentative précédente** : la séquence de tâches s’exécute à nouveau quand le déploiement est planifié, mais seulement en cas d’échec de la précédente exécution. Ce paramètre est utile pour un déploiement obligatoire. Si la dernière tentative d’exécution a échoué, il tente automatiquement de s’exécuter à nouveau suivant le calendrier des affectations.  

        - **Exécuter à nouveau en cas de réussite de la tentative précédente** : la séquence de tâches ne s’exécute à nouveau que si elle s’est déjà exécutée avec succès sur le client. Ce paramètre est utile lorsque vous utilisez des déploiements périodiques dans lesquels la séquence de tâches est mise régulièrement à jour, et chaque mise à jour requiert que la précédente mise à jour soit installée avec succès.  

        > [!NOTE]  
        > Un utilisateur peut exécuter à nouveau le déploiement d’une séquence de tâches disponible. Avant de déployer une séquence de tâches disponibles dans un environnement de production, examinez ce qui se passe si l’utilisateur réexécute la séquence de tâches plusieurs fois.  

7. Sur la page **Expérience utilisateur** , spécifiez les informations suivantes :  

    - **Autoriser l’utilisateur à exécuter le programme indépendamment des affectations** : indiquez si l’utilisateur peut exécuter un déploiement obligatoire en dehors du planning des affectations. Cette option est toujours activée pour les déploiements disponibles.  

    - **Afficher la progression de la séquence de tâches** : spécifiez si le client Configuration Manager affiche la progression de la séquence de tâches.  

    - **Installation du logiciel** : spécifiez si l’utilisateur est autorisé à installer le logiciel en dehors d’une fenêtre de maintenance configurée après l’heure planifiée.  

    - **Redémarrage du système (si nécessaire pour terminer l’installation)**: spécifiez si l’utilisateur est autorisé à redémarrer l’ordinateur après une installation de logiciel en dehors d’une fenêtre de maintenance configurée après l’heure d’attribution.  

    - **Traitement des filtres d’écriture pour les appareils Windows Embedded** : ce paramètre contrôle le comportement d’installation sur les appareils Windows Embedded qui sont activés avec un filtre d’écriture. Choisissez l’option permettant de valider les modifications à l’échéance de l’installation ou au cours d’une fenêtre de maintenance. Quand vous sélectionnez cette option, un redémarrage est nécessaire, qui conserve les modifications sur l’appareil. Sinon, l’application est installée sur l’overlay temporaire et validée ultérieurement. Lorsque vous déployez une séquence de tâches sur un appareil Windows Embedded, vérifiez que celui-ci appartient à un regroupement pour lequel une fenêtre de maintenance a été configurée.  

    - **Autoriser la séquence de tâches à s’exécuter pour le client sur Internet** : spécifiez si la séquence de tâches est autorisée à s’exécuter sur un client basé sur Internet. Les opérations qui installent des logiciels, comme un système d’exploitation, ne sont pas prises en charge avec ce paramètre. Utilisez cette option uniquement pour les séquences de tâches basées sur des scripts génériques qui effectuent des opérations dans le système d’exploitation standard.  

        - À partir de la version 1802, ce paramètre est pris en charge pour les déploiements d’une séquence de tâches de mise à niveau sur place de Windows 10 qui sont effectués sur des clients basés sur Internet par le biais de la passerelle de gestion cloud. Pour plus d’informations, consultez [Déployer la mise à niveau sur place de Windows 10 à l’aide de la passerelle de gestion cloud](#deploy-windows-10-in-place-upgrade-via-cmg).  

8. Sur la page **Alertes**, spécifiez les paramètres d’alerte souhaités pour le déploiement de cette séquence de tâches.  

9. Sur la page **Points de distribution** , spécifiez les informations suivantes :  

    - **Options de déploiement**: spécifiez l’une des options suivantes :  

        > [!NOTE]  
        > Quand vous utilisez la multidiffusion pour déployer un système d’exploitation, téléchargez le contenu sur les ordinateurs de destination soit au fil des besoins, soit avant l’exécution de la séquence de tâches.  

        - **Télécharger le contenu localement lorsque la séquence de tâches en cours d’exécution l’exige** : spécifiez que les clients téléchargent le contenu du point de distribution en fonction des besoins de la séquence de tâches. Le client démarre la séquence de tâches. Lorsque l’une de ses étapes réclame du contenu, celui-ci est téléchargé avant l’exécution de l’étape.  

        - **Télécharger tout le contenu localement avant de démarrer la séquence de tâches** : spécifiez que les clients téléchargent tout le contenu du point de distribution avant l’exécution de la séquence de tâches. Si la séquence de tâches est mise à la disposition des déploiements sur média de démarrage et environnement PXE sur la page **Paramètres de déploiement**, cette option n’apparaît pas.  

        - **Accéder au contenu directement à partir d’un point de distribution lorsque la séquence de tâches en cours d’exécution l’exige** : spécifiez que les clients exécutent le contenu à partir du point de distribution. Cette option n’est disponible que lorsque tous les packages associés à la séquence de tâches sont autorisés à utiliser un partage de package sur le point de distribution. Pour que le contenu utilise un partage de package, consultez l'onglet **Accès aux données** dans les **Propriétés** de chaque package.  

            > [!IMPORTANT]  
            > Pour plus de sécurité, sélectionnez les options **Télécharger le contenu localement si nécessaire pour la séquence de tâches en cours d’exécution** ou **Télécharger tout le contenu localement avant de lancer la séquence de tâches**. Lorsqu’une de ces options est sélectionnée, Configuration Manager hache le package pour en garantir l’intégrité. Si l’option **Accéder directement au contenu à partir d’un point de distribution si nécessaire pour la séquence de tâches en cours d’exécution** est sélectionnée, Configuration Manager ne vérifie pas le hachage du package avant d’exécuter le programme spécifié. Dans la mesure où le site ne peut garantir l’intégrité du package, les utilisateurs disposant de droits d’administration ont la possibilité de modifier ou de falsifier son contenu.  

    - **Quand aucun point de distribution local n’est disponible, utiliser un point de distribution distant** : indiquez si les clients peuvent utiliser les points de distribution d’un groupe de limites voisin pour télécharger le contenu exigé par la séquence de tâches.  

    - **Autoriser les clients à utiliser des points de distribution du groupe de limites de site par défaut** : indiquez si les clients doivent télécharger le contenu à partir d’un point de distribution du groupe de limites de site par défaut quand il n’est pas disponible sur le point de distribution des groupes de limites actifs ou voisins.  

        > [!Note]  
        > À compter de la version 1810, quand un appareil exécute une séquence de tâches et a besoin d’acquérir du contenu, il utilise des comportements de groupe de limites comparables à ceux du client Configuration Manager. Pour plus d’informations, consultez [Prise en charge des séquences de tâches pour les groupes de limites](/sccm/core/servers/deploy/configure/boundary-groups#bkmk_bgr-osd).<!--1359025-->  

10. À compter de Configuration Manager 1802, enregistrez les paramètres dans l’objectif de les réutiliser. Pour cela, sélectionnez **Enregistrer comme modèle** sous l’onglet **Résumé**. Entrez un nom pour le modèle et sélectionnez les paramètres à enregistrer.  

11. Effectuez toutes les étapes de l'Assistant.  


## <a name="deploy-windows-10-in-place-upgrade-via-cmg"></a>Déployer la mise à niveau sur place de Windows 10 à l’aide de la passerelle de gestion cloud

<!-- 1357149 -->
À partir de la version 1802, la séquence de tâches de mise à niveau sur place de Windows 10 prend en charge le déploiement sur des clients basés sur Internet par le biais de la [passerelle de gestion cloud](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG). Cette capacité permet aux utilisateurs distants de passer plus facilement à Windows 10, sans avoir à se connecter à l’intranet.

Veillez à ce que tout le contenu référencé par la séquence de tâches de mise à niveau sur place soit distribué sur un [point de distribution cloud](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Sinon, les appareils ne pourront pas exécuter la séquence de tâches.

Lorsque vous déployez une séquence de tâches de mise à niveau, utilisez les paramètres suivants :

- **Autoriser la séquence de tâches à s’exécuter pour le client sur Internet**, sous l’onglet Expérience utilisateur du déploiement.  

- **Télécharger tout le contenu localement avant de démarrer la séquence de tâches**, sur la page Points de distribution du déploiement. Les autres options, comme **Télécharger le contenu localement lorsque la séquence de tâches en cours d’exécution l’exige**, ne fonctionnent pas dans ce scénario. Le moteur de séquence de tâches est actuellement incapable de récupérer du contenu à partir d’un point de distribution cloud. Le client Configuration Manager doit télécharger le contenu à partir du point de distribution cloud avant de démarrer la séquence de tâches.  

- (*Facultatif*) **Prétélécharger le contenu pour cette séquence de tâches**, sous l’onglet Général du déploiement. Pour plus d’informations, consultez la section [Configurer le contenu précache](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).  


## <a name="bkmk_high-risk"></a> Déploiements à haut risque

Quand vous effectuez un déploiement à haut risque, par exemple un système d’exploitation, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements personnalisés satisfaisant aux paramètres de vérification de déploiement configurés dans les propriétés du site. Les déploiements à haut risque sont toujours limités aux regroupements personnalisés, aux regroupements que vous créez et au regroupement **Ordinateurs inconnus** intégré. Quand vous créez un déploiement à haut risque, vous ne pouvez pas sélectionner un regroupement intégré, par exemple **Tous les systèmes**. Pour afficher tous les regroupements personnalisés qui contiennent moins de clients que la taille maximale configurée, désactivez l’option **Masquer les regroupements dont le nombre de membres est supérieur à la configuration de la taille minimale du site**. Pour plus d’informations, consultez [Paramètres de gestion des déploiements à haut risque](/sccm/core/servers/manage/settings-to-manage-high-risk-deployments).  

Les paramètres de vérification de déploiement sont basés sur l'appartenance actuelle du regroupement. Après le déploiement de la séquence de tâches, Configuration Manager ne réévalue pas l’adhésion au regroupement pour les paramètres de déploiement à haut risque.  

Supposons que vous affectez la valeur 100 à **Taille par défaut** et la valeur 1000 à **Taille maximale**. Quand vous créez un déploiement à haut risque, la fenêtre **Sélectionner un regroupement** affiche uniquement les regroupements qui contiennent moins de 100 clients. Si vous désactivez le paramètre **Masquer les regroupements avec un nombre de membres supérieur à la configuration de la taille minimale du site**, la fenêtre affiche les regroupements qui contiennent moins de 1 000 clients.  

Quand vous sélectionnez un regroupement qui contient un rôle de site, le comportement suivant s’applique :  

- Si le regroupement contient un serveur de système de site, et que vous avez configuré les paramètres de vérification du déploiement pour bloquer les regroupements contenant des serveurs de système de site, une erreur se produit. Vous ne pouvez alors pas continuer la création du déploiement.  

- Si l’un des critères suivants s’applique, l’Assistant Déploiement logiciel affiche un avertissement de risque élevé. Pour continuer, vous devez accepter de créer un déploiement à haut risque. Le site génère un message d’état d’audit.  

    - Si le regroupement contient un serveur de système de site, et que vous avez configuré les paramètres de vérification du déploiement pour afficher un avertissement pour les regroupements contenant des serveurs de système de site  

    - Si le regroupement dépasse la valeur de taille par défaut

    - Si le regroupement contient un serveur  


## <a name="see-also"></a>Voir aussi

[Gérer les séquences de tâches pour automatiser des tâches](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks)
