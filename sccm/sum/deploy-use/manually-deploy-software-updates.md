---
title: Déployer manuellement des mises à jour logicielles
titleSuffix: Configuration Manager
description: Pour déployer manuellement des mises à jour logicielles, sélectionnez les mises à jour dans la console Configuration Manager et déployez-les manuellement, ou ajoutez les mises à jour à un groupe de mises à jour et déployez ce groupe.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/07/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 57184274-5fea-4d79-a2b4-22e08ed26daf
ms.openlocfilehash: 3f79da78df10e97813b221ffca3df25396591fbc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
#  <a name="BKMK_ManualDeploy"></a> Déployer manuellement des mises à jour logicielles  

*S’applique à : System Center Configuration Manager (Current Branch)*

 Le déploiement manuel des mises à jour logicielles consiste à sélectionner des mises à jour logicielles dans la console Configuration Manager et à lancer manuellement le processus de déploiement. Ou bien, vous pouvez ajouter des mises à jour logicielles sélectionnées à un groupe de mises à jour, puis déployer manuellement ce groupe. Avant de créer des règles ADR chargées de gérer en continu les déploiements mensuels de mises à jour logicielles, il est probable que vous aurez recours à un déploiement manuel pour mettre à jour vos appareils clients avec les mises à jour logicielles requises. Vous pourrez également utiliser une méthode manuelle pour déployer des mises à jour logicielles hors bande. Si vous avez besoin d’aide pour déterminer la méthode de déploiement qui vous convient, consultez [Déployer des mises à jour logicielles](deploy-software-updates.md).

 Les sections suivantes décrivent les étapes à effectuer pour déployer manuellement des mises à jour logicielles.  

##  <a name="BKMK_1SearchCriteria"></a> Étape 1 : spécifier les critères de recherche des mises à jour logicielles  
 Des milliers de mises à jour logicielles peuvent potentiellement s’afficher dans la console Configuration Manager. La première étape du flux de travail relatif au déploiement manuel de mises à jour logicielles consiste à identifier les mises à jour logicielles que vous souhaitez déployer. Par exemple, vous pourriez indiquer des critères permettant d'extraire toutes les mises à jour logicielles requises sur plus de 50 appareils clients et dont la classification est **Sécurité** ou **Critique** .  

> [!IMPORTANT]  
>  Le nombre maximal de mises à jour logicielles pouvant être incluses dans un déploiement unique s'élève à 1 000.  

#### <a name="to-specify-search-criteria-for-software-updates"></a>Pour spécifier des critères de recherche pour les mises à jour logicielles  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail Bibliothèque de logiciels, développez **Mises à jour logicielles**et cliquez sur **Toutes les mises à jour logicielles**. Les mises à jour logicielles synchronisées sont affichées.  

    > [!NOTE]  
    >  Dans le nœud **Toutes les mises à jour logicielles**, Configuration Manager affiche uniquement les mises à jour logicielles classées selon les critères **Critique** et **Sécurité** qui ont été publiées au cours des 30 derniers jours.  

3.  Dans le volet de recherche, appliquez un filtre pour identifier les mises à jour logicielles dont vous avez besoin en suivant l'une des étapes suivantes ou les deux :  

    -   Dans la zone de texte Rechercher, tapez une chaîne de recherche qui permettra de filtrer les mises à jour logicielles. Par exemple, tapez l'ID de l'article ou du bulletin d'une mise à jour logicielle spécifique, ou entrez une chaîne susceptible d'apparaître dans le titre de plusieurs mises à jour logicielles.  

    -   Cliquez sur **Ajouter des critères**, sélectionnez les critères que vous souhaitez utiliser pour filtrer les mises à jour logicielles, cliquez sur **Ajouter**, puis indiquez les valeurs pour les critères.  

4.  Cliquez sur **Rechercher** pour filtrer les mises à jour logicielles.  

    > [!TIP]  
    >  Vous avez la possibilité d'enregistrer les critères de filtre sur l'onglet **Rechercher** et dans le groupe **Enregistrer** .  

##  <a name="BKMK_2UpdateGroup"></a> Étape 2 : créer un groupe de mises à jour logicielles contenant les mises à jour logicielles  
 Les groupes de mises à jour logicielles permettent d'organiser efficacement les mises à jour logicielles en préparation à des fins de déploiement. Vous pouvez ajouter manuellement des mises à jour logicielles à un groupe de mises à jour logicielles, ou définir une règle ADR pour que Configuration Manager ajoute automatiquement les mises à jour logicielles à un groupe de mises à jour logicielles nouveau ou existant. Pour ajouter manuellement des mises à jour logicielles à un nouveau groupe de mises à jour logicielles, procédez comme suit.  

#### <a name="to-manually-add-software-updates-to-a-new-software-update-group"></a>Pour ajouter manuellement des mises à jour logicielles à un nouveau groupe de mises à jour logicielles  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail Bibliothèque de logiciels, cliquez sur **Mises à jour logicielles**.  

3.  Sélectionnez les mises à jour logicielles à ajouter au nouveau groupe de mises à jour logicielles.  

4.  Dans l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Créer un groupe de mises à jour logicielles**.  

5.  Spécifiez le nom du groupe de mises à jour logicielles et indiquez éventuellement une description. Utilisez un nom et une description suffisamment détaillés pour vous permettre de déterminer quel type de mises à jour logicielles se trouve dans le groupe de mises à jour logicielles. Pour continuer, cliquez sur **Créer**.  

6.  Cliquez sur le nœud **Groupes de mises à jour logicielles** pour afficher le nouveau groupe de mises à jour logicielles.  

7.  Sélectionnez le groupe de mises à jour logicielles et, sous l'onglet **Accueil** , dans le groupe **Mise à jour** , cliquez sur **Afficher les membres** pour afficher la liste des mises à jour logicielles incluses dans le groupe.  

##  <a name="BKMK_3DownloadContent"></a> Étape 3 : télécharger le contenu pour le groupe de mises à jour logicielles  
 Éventuellement, avant de déployer les mises à jour logicielles, vous pouvez télécharger le contenu de celles qui sont incluses dans le groupe de mises à jour logicielles. Vous pouvez choisir de procéder ainsi afin de vérifier que le contenu est disponible sur les points de distribution avant de déployer les mises à jour logicielles. Cela vous permet d'éviter des problèmes inattendus de remise de contenu. Vous pouvez ignorer cette étape et le contenu sera téléchargé et copié sur les points de distribution dans le cadre du processus de déploiement. Pour télécharger le contenu pour les mises à jour logicielles dans le groupe de mises à jour logicielles, procédez comme suit.  



#### <a name="to-download-content-for-the-software-update-group"></a>Pour télécharger le contenu pour le groupe de mises à jour logicielles
[!INCLUDE[downloadupdates](..\includes\downloadupdates.md)]
<!--- 1.  In the Configuration Manager console, click **Software Library**.  

2.  In the Software Library workspace, expand **Software Updates**, and click **Software Update Groups**.  

3.  Select the software update group for which you want to download content.  

4.  On the **Home** tab, in the **Update Group** group, click **Download**. The **Download Software Updates Wizard** opens.  

5.  On the **Deployment Package** page, configure the following settings:  

    1.  **Select deployment package**: Select this setting to use an existing deployment package for the software updates in the deployment.  

        > [!NOTE]  
        >  Software updates that have already been downloaded to the selected deployment package are not downloaded again.  

    2.  **Create a new deployment package**: Select this setting to create a new deployment package for the software updates in the deployment. Configure the following settings:  

        -   **Name**: Specifies the name of the deployment package. This must be a unique name that describes the package content. It is limited to 50 characters.  

        -   **Description**: Specifies the description of the deployment package. The package description provides information about the package contents and is limited to 127 characters.  

        -   **Package source**: Specifies the location of the software update source files.  Type a network path for the source location, for example, **\\\server\sharename\path**, or click **Browse** to find the network location. You must create the shared folder for the deployment package source files before you proceed to the next page.  

            > [!NOTE]  
            >  The deployment package source location that you specify cannot be used by another software deployment package.  

            > [!IMPORTANT]  
            >  The SMS Provider computer account and the user that is running the wizard to download the software updates must both have **Write** NTFS permissions on the download location. You should carefully restrict access to the download location in order to reduce the risk of attackers tampering with the software update source files.  

            > [!IMPORTANT]  
            >  You can change the package source location in the deployment package properties after Configuration Manager creates the deployment package. But if you do so, you must first copy the content from the original package source to the new package source location.  

     Click **Next**.  

6.  On the Distribution Points page, select the distribution points or distribution point groups that are used to host the software update files defined in the new deployment package, and then click **Next**.  

7.  On the Distribution Settings page, specify the following settings:  

    -   **Distribution priority**: Use this setting to specify the distribution priority for the deployment package. The distribution priority applies when the deployment package is sent to distribution points at child sites. Distribution packages are sent in priority order: **High**, **Medium**, or **Low**. Packages with identical priorities are sent in the order in which they were created. If there is no backlog, the package will process immediately regardless of its priority. By default, packages are sent using **Medium** priority.  

    -   **Distribute the content for this package to preferred distribution points**: Use this setting to enable on-demand content distribution to preferred distribution points. When this setting is enabled, the management point creates a trigger for the distribution manager to distribute the content to all preferred distribution points when a client requests the content for the package and the content is not available on any preferred distribution points. For more information about preferred distribution points and on-demand content, see [Content source location scenarios](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#bkmk_CSLscenarios).  

    -   **Prestaged distribution point settings**: Use this setting to specify how you want to distribute content to prestaged distribution points. Choose one of the following options:  

        -   **Automatically download content when packages are assigned to distribution points**: Use this setting to ignore the prestage settings and distribute content to the distribution point.  

        -   **Download only content changes to the distribution point**: Use this setting to prestage the initial content to the distribution point, and then distribute content changes to the distribution point.  

        -   **Manually copy the content in this package to the distribution point**: Use this setting to always prestage content on the distribution point. This is the default setting.  

         For more information about prestaging content to distribution points, see [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage).  

     Click **Next**.  

8.  On the Download Location page, specify location that Configuration Manager will use to download the software update source files. As needed, use the following options:  

    -   **Download software updates from the Internet**: Select this setting to download the software updates from the location on the Internet. This is the default setting.  

    -   **Download software updates from a location on the local network**: Select this setting to download software updates from a local folder or shared network folder. Use this setting when the computer running the wizard does not have Internet access.  

        > [!NOTE]  
        >  When you use this setting, download the software updates from any computer with Internet access, and then copy the software updates to a location on the local network that is accessible from the computer running the wizard.  

     Click **Next**.  

9. On the Language Selection page, specify the languages for which the selected software updates are to be downloaded, and then click **Next**. Configuration Manager downloads the software updates only if they are available in the selected languages. Software updates that are not language-specific are always downloaded.  

10. On the Summary page, verify the settings that you selected in the wizard, and then click **Next** to download the software updates.  

11. On the Completion page, verify that the software updates were successfully downloaded, and then click **Close**. --->

#### <a name="to-monitor-content-status"></a>Pour surveiller l'état du contenu
1. Pour surveiller l’état du contenu des mises à jour logicielles, cliquez sur **Surveillance** dans la console Configuration Manager.  

2. Dans l'espace de travail Surveillance, développez **État de distribution**, puis cliquez sur **État du contenu**.  

3. Sélectionnez le package de mises à jour logicielles que vous avez précédemment identifié pour télécharger les mises à jour logicielles dans le groupe de mises à jour logicielles.  

4. Sous l'onglet **Accueil** , dans le groupe **Contenu** , cliquez sur **Afficher l'état**.  

##  <a name="BKMK_4DeployUpdateGroup"></a> Étape 4 : déployer le groupe de mises à jour logicielles  
 Après avoir déterminé quelles mises à jour logicielles vous voulez déployer et après avoir ajouté ces mises à jour logicielles à un groupe de mises à jour logicielles, vous pouvez déployer manuellement les mises à jour logicielles dans le groupe de mises à jour logicielles. Pour déployer manuellement les mises à jour logicielles dans un groupe de mises à jour logicielles, procédez comme suit.  

#### <a name="to-manually-deploy-the-software-updates-in-a-software-update-group"></a>Pour déployer manuellement les mises à jour logicielles dans un groupe de mises à jour logicielles  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail Bibliothèque de logiciels, développez **Mises à jour logicielles**et cliquez sur **Groupes de mises à jour logicielles**.  

3.  Sélectionnez le groupe de mises à jour logicielles que vous souhaitez déployer.  

4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**. L' **Assistant Déploiement des mises à jour logicielles** s'ouvre.  

5.  Sur la page Général, configurez les paramètres suivants :  

    -   **Nom**: indiquez le nom du déploiement. Le déploiement doit porter un nom unique qui décrit son objectif et le différencie des autres déploiements dans le site Configuration Manager. Par défaut, Configuration Manager fournit automatiquement un nom pour le déploiement au format suivant : **Mises à jour logicielles Microsoft -** <*date*><*heure*>  

    -   **Description :** spécifiez la description du déploiement. La description fournit une vue d’ensemble du déploiement et toute autre information pertinente permettant d’identifier et de différencier le déploiement des autres déploiements dans le site Configuration Manager. Le champ de description facultatif est limité à 256 caractères et est vierge par défaut.  

    -   **Mise à jour logicielle/Groupe de mises à jour logicielles**: vérifiez que le groupe de mises à jour logicielles ou la mise à jour logicielle qui s’affiche est correct.  

    -   **Sélectionner un modèle de déploiement**: indiquez si un modèle de déploiement enregistré précédemment doit être appliqué. Vous pouvez configurer un modèle de déploiement de sorte qu'il contienne plusieurs propriétés de déploiement de mises à jour logicielles communes, puis l'utiliser lorsque vous déployez les mises à jour logicielles ultérieures afin d'assurer une cohérence entre des déploiements semblables et de gagner du temps.  

    -   **Regroupement**: indique le regroupement du déploiement, le cas échéant. Les membres du regroupement reçoivent les mises à jour logicielles définies dans le déploiement.  

6.  Sur la page Paramètres de déploiement, configurez les paramètres suivants :  

    -   **Type de déploiement**: indique le type de déploiement pour le déploiement des mises à jour logicielles. Sélectionnez **Obligatoire** pour créer un déploiement de mises à jour logicielles obligatoire où les mises à jour logicielles sont installées automatiquement sur les clients selon une échéance d'installation configurée. Sélectionnez **Disponible** pour créer un déploiement de mises à jour logicielles facultatives que les utilisateurs peuvent installer à partir du Centre logiciel.  

        > [!IMPORTANT]  
        >  Après avoir créé le déploiement de mises à jour logicielles, vous ne pourrez pas modifier ultérieurement le type de déploiement.  

        > [!NOTE]  
        >  Un groupe de mises à jour logicielles déployé avec l’option **Obligatoire** est téléchargé en arrière-plan et respecte les paramètres BITS, s’ils sont configurés.  
        > Toutefois, les groupes de mises à jour logicielles déployés avec l’option **Disponible** sont téléchargés au premier plan et ignore les paramètres BITS.  

    -   **Utiliser Wake-on-LAN pour réveiller les clients pour les déploiements requis**: indiquez si l’éveil par appel réseau (Wake On LAN) doit être activé à l’échéance pour envoyer des paquets de mise en éveil aux ordinateurs qui nécessitent une ou plusieurs mises à jour logicielles du déploiement. Tous les ordinateurs en mode veille à l'échéance de l'installation sont mis en éveil afin que l'installation des mises à jour logicielles puisse démarrer. Les clients en mode veille qui ne nécessitent pas les mises à jour logicielles incluses dans le déploiement ne sont pas démarrés. Par défaut, ce paramètre n'est pas activé et il est disponible uniquement lorsque le **Type de déploiement** est défini sur **Obligatoire**.  

        > [!WARNING]  
        >  Pour que vous puissiez utiliser cette option, les ordinateurs et les réseaux doivent être configurés pour utiliser l'éveil par appel réseau.  

    -   **Niveau de détail**: indiquez le niveau de détail pour les messages d’état qui sont signalés par les ordinateurs clients.  

7.  Sur la page Planification, configurez les paramètres suivants :  

    -   **Calendrier d’évaluation** : indiquez si la durée disponible et la date d’échéance de l’installation sont évaluées à l’heure UTC ou à l’heure locale de l’ordinateur exécutant la console Configuration Manager.  

        > [!NOTE]  
        >  Si vous sélectionnez l’heure locale, puis **Dès que possible** pour le **Temps disponible du logiciel** ou **Échéance d’installation**, l’heure actuelle sur l’ordinateur exécutant la console Configuration Manager est utilisée pour évaluer quand les mises à jour sont disponibles ou quand elles sont installées sur un client. Si le client est dans un autre fuseau horaire, ces actions se produisent quand l’heure du client atteint l’heure de l’évaluation.  

    -   **Temps disponible du logiciel**: sélectionnez l’un des paramètres suivants pour spécifier le moment où les mises à jour logicielles seront disponibles pour les clients :  

        -   **Dès que possible**: sélectionnez ce paramètre pour permettre aux clients d’accéder dès que possible aux mises à jour logicielles incluses dans le déploiement. Lors de la création du déploiement, la stratégie client est mise à jour, les clients sont informés du déploiement au prochain cycle d'interrogation de leur stratégie client, puis les mises à jour logicielles sont mises à disposition en vue de leur installation.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour permettre aux clients d’accéder aux mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques. Lorsque le déploiement est créé, la stratégie client est mise à jour et les clients sont informés au prochain cycle d'interrogation de leur stratégie client. Toutefois, les mises à jour logicielles incluses dans le déploiement ne sont pas disponibles à l'installation avant la date et l'heure spécifiées.  

    -   **Échéance d’installation**: sélectionnez l’un des paramètres suivants pour spécifier l’échéance d’installation des mises à jour logicielles incluses dans le déploiement.  

        > [!NOTE]  
        >  Vous pouvez configurer le paramètre relatif à l'échéance d'installation uniquement lorsque **Type de déploiement** est défini sur **Obligatoire** sur la page Paramètres de déploiement.  

        -   **Dès que possible**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement dès que possible.  

        -   **Heure spécifique**: sélectionnez ce paramètre pour installer automatiquement les mises à jour logicielles incluses dans le déploiement à une date et une heure spécifiques.  

        > [!NOTE]  
        >  L'heure d'échéance de l'installation réelle est l'heure spécifique que vous configurez plus un laps de temps aléatoire pouvant atteindre 2 heures. Elle permet de réduire l'impact lié à l'installation simultanée, par tous les ordinateurs clients du regroupement de destination, des mises à jour logicielles incluses dans le déploiement.  
        >   
        >  Vous pouvez configurer le paramètre client **Agent ordinateur** , **Désactiver la randomisation des échéances** , pour désactiver le délai de randomisation de l’installation des mises à jour logicielles requises. Pour plus d’informations, voir [Computer Agent](../../core/clients/deploy/about-client-settings.md#computer-agent).  

8.  Sur la page Expérience utilisateur, configurez les paramètres suivants :  

    -   **Notifications à l’utilisateur**: indiquez si vous souhaitez afficher les notifications des mises à jour logicielles dans le Centre logiciel sur l’ordinateur client selon la valeur **Temps disponible du logiciel** configuré et si les notifications à l’utilisateur doivent s’afficher sur les ordinateurs clients. Lorsque **Type de déploiement** est défini sur **Disponible** sur la page Paramètres de déploiement, vous ne pouvez pas sélectionner **Masquer dans le Centre logiciel et toutes les notifications**.  

    -   **Comportement à l’échéance** : Disponible uniquement quand **Type de déploiement** est défini sur **Obligatoire** dans la page Paramètres de déploiement.   
    spécifier le comportement qui doit se produire lorsque l'échéance est atteinte pour le déploiement des mises à jour logicielles. Indiquez si vous souhaitez installer les mises à jour logicielles incluses dans le déploiement. Spécifiez également si un redémarrage du système doit être effectué après l'installation des mises à jour logicielles, quelle que soit la fenêtre de maintenance configurée. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Comportement de redémarrage de l’appareil** : Disponible uniquement quand **Type de déploiement** est défini sur **Obligatoire** dans la page Paramètres de déploiement.    
    indiquer si le redémarrage du système sur les serveurs et stations de travail doit être supprimé une fois les mises à jour logicielles installées et si un redémarrage du système est nécessaire pour terminer l'installation.  

        > [!IMPORTANT]  
        >  La suppression des redémarrages du système peut s'avérer utile dans les environnements de serveurs ou lorsque vous ne souhaitez pas que les ordinateurs qui installent les mises à jour logicielles redémarrent par défaut. Toutefois, elle peut laisser les ordinateurs dans un état non sécurisé, alors que l'autorisation d'un redémarrage forcé contribue à garantir l'exécution immédiate de l'installation des mises à jour logicielles.

    -   **Traitement des filtres d’écriture pour les appareils Windows Embedded**: quand vous déployez des mises à jour logicielles sur des appareils Windows Embedded pour lesquels le filtre d’écriture est activé, vous pouvez choisir d’installer la mise à jour logicielle sur le segment de recouvrement temporaire et valider les modifications ultérieurement ou à l’échéance de l’installation ou bien pendant une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

        > [!NOTE]  
        >  Lorsque vous déployez une mise à jour logicielle sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée.  

    - **Comportement de réévaluation du déploiement des mises à jour logicielles après le redémarrage** : à compter de Configuration Manager version 1606, sélectionnez ce paramètre pour configurer les déploiements de mises à jour logicielles de façon à ce que les clients exécutent une analyse de conformité des mises à jour logicielles immédiatement après avoir installé celles-ci et redémarré. Cela permet au client de vérifier la disponibilité de mises à jour logicielles supplémentaires devenues applicables après le redémarrage, puis de les installer (et devenir ainsi conforme) au cours d’une même fenêtre de maintenance.

9. Sur la page Alertes, configurez la manière dont Configuration Manager et System Center Operations Manager génèreront des alertes pour ce déploiement. Vous pouvez configurer des alertes uniquement lorsque **Type de déploiement** est défini sur **Obligatoire** sur la page Paramètres de déploiement.  

    > [!NOTE]  
    >  Vous pouvez consulter les récentes alertes de mises à jour logicielles à partir du nœud **Mises à jour logicielles** dans l'espace de travail **Bibliothèque de logiciels** .  

10. Sur la page Paramètres de téléchargement, configurez les paramètres suivants :  

    - Indiquez si le client va télécharger et installer les mises à jour logicielles quand il est connecté à un réseau lent ou utilise un emplacement de secours pour le contenu.  

    - Indiquez si le client doit télécharger et installer les mises à jour logicielles à partir d'un point de distribution de secours quand le contenu pour les mises à jour logicielles n'est pas disponible sur un point de distribution préféré.  

    - **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations sur BranchCache, consultez [Concepts fondamentaux de la gestion de contenu](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

    - **Si les mises à jour logicielles ne sont pas disponibles sur le point de distribution de groupes actuels, voisins ou de site, téléchargez le contenu à partir de Microsoft Updates** : sélectionnez ce paramètre afin que les clients connectés à l’intranet téléchargent les mises à jour logicielles depuis Microsoft Update si les mises à jour logicielles ne sont pas disponibles sur les points de distribution. Les clients Internet peuvent toujours accéder à Microsoft Update pour obtenir le contenu des mises à jour logicielles.

    - Indiquez si les clients peuvent procéder au téléchargement une fois l’échéance de l’installation dépassée dans le cas où ils utilisent des connexions Internet facturées à l’usage. Les fournisseurs Internet facturent parfois en fonction de la quantité de données que vous envoyez et recevez lorsque vous utilisez une connexion Internet facturée à l'usage.  

    > [!NOTE]  
    >  Les clients demandent l'emplacement du contenu à partir d'un point de gestion pour les mises à jour logicielles dans un déploiement. Le comportement de téléchargement dépend de la manière dont vous avez configuré le point de distribution, le package de déploiement et les paramètres sur cette page. Pour plus d'informations, voir [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md).  

11. Si vous avez effectué l' [Étape 3 : télécharger le contenu pour le groupe de mises à jour logicielles](#BKMK_3DownloadContent), les pages Package de déploiement, Points de distribution et Sélection de la langue ne sont pas affichées et vous pouvez passer à l'étape 15 de l'Assistant.  

    > [!IMPORTANT]  
    >  Les mises à jour logicielles qui ont été téléchargées précédemment dans la bibliothèque de contenu sur le serveur de site ne sont pas téléchargées à nouveau. Cela est vrai même lorsque vous créez un package de déploiement pour les mises à jour logicielles. Si toutes les mises à jour logicielles ont déjà été téléchargées auparavant, l'Assistant passe à la page **Sélection de la langue** (étape 15).  

12. Sur la page Package de déploiement, sélectionnez un package de déploiement existant ou configurez les paramètres suivants pour spécifier un nouveau package de déploiement :  

    1.  **Nom** : spécifiez le nom du package de déploiement. Celui-ci doit être un nom unique qui décrit le contenu du package. Il est limité à 50 caractères.  

    2.  **Description**: spécifiez une description qui fournit des informations sur le package de déploiement. La description est limitée à 127 caractères.  

    3.  **Source du package**: spécifiez l’emplacement des fichiers sources des mises à jour logicielles.  Tapez un chemin réseau pour l’emplacement source, par exemple **\\\serveur\nom_partage\chemin**ou cliquez sur **Parcourir** pour trouver l’emplacement réseau. Vous devez créer le dossier partagé pour les fichiers sources du package de déploiement avant de passer à la page suivante.  

        > [!NOTE]  
        >  L'emplacement source du package de déploiement que vous spécifiez ne peut pas être utilisé par un autre package de déploiement de logiciel.  

        > [!IMPORTANT]  
        >  Le compte d'ordinateur du fournisseur SMS et l'utilisateur qui exécute l'Assistant Téléchargement des mises à jour logicielles nécessitent des autorisations NTFS en **Écriture** sur l'emplacement de téléchargement. Vous devez soigneusement limiter l'accès à l'emplacement de téléchargement pour éviter que des personnes malintentionnées ne falsifient les fichiers sources des mises à jour logicielles.  

        > [!IMPORTANT]  
        >  Une fois que le package de déploiement a été créé par Configuration Manager, vous pouvez modifier l’emplacement source du package de déploiement dans les propriétés du package. Mais le cas échéant, vous devez d'abord copier le contenu à partir de la source du package d'origine vers le nouvel emplacement source du package.  

    4.  **Priorité d’expédition**: spécifiez la priorité d’envoi pour le package de déploiement. Configuration Manager utilise la priorité d’expédition du package de déploiement quand il envoie le package aux points de distribution. Les packages de déploiement sont envoyés par ordre de priorité : Haute, Moyenne ou Faible. Les packages disposant de priorités identiques sont transmis dans l'ordre dans lequel ils ont été créés. En l'absence de backlog, le package est immédiatement traité quelle que soit sa priorité.  

13. Sur la page Points de distribution, spécifiez les points de distribution ou les groupes de points de distribution qui vont héberger les fichiers de mise à jour logicielle. Pour plus d’informations sur les points de distribution, consultez [Configurations des points de distribution](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs).  

14. Sur la page Emplacement de téléchargement, indiquez si les fichiers de mise à jour logicielle doivent être téléchargés à partir d'Internet ou de votre réseau local. Configurez les paramètres suivants :  

    -   **Télécharger les mises à jour logicielles depuis Internet**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un emplacement spécifié sur Internet. Ce paramètre est activé par défaut.  

    -   **Télécharger les mises à jour logicielles à partir d’un emplacement sur le réseau local**: sélectionnez ce paramètre pour télécharger les mises à jour logicielles à partir d’un dossier local ou d’un dossier réseau partagé. Ce paramètre s'avère utile lorsque l'ordinateur exécutant l'Assistant ne dispose d'aucun accès à Internet. Les mises à jour logicielles peuvent être préalablement téléchargées à partir de n'importe quel ordinateur qui a accès à Internet, puis stockées à un emplacement sur le réseau local à des fins d'accès ultérieur pour l'installation.  

15. Sur la page Sélection de la langue, sélectionnez les langues pour lesquelles les mises à jour logicielles sélectionnées sont téléchargées. Les mises à jour logicielles sont téléchargées uniquement si elles sont disponibles dans les langues sélectionnées. Les mises à jour logicielles qui ne sont spécifiques à aucune langue sont toujours téléchargées. Par défaut, l'Assistant sélectionne les langues que vous avez configurées dans les propriétés du point de mise à jour logicielle. Au moins une langue doit être sélectionnée avant de passer à la page suivante. Quand vous sélectionnez uniquement des langues qui ne sont pas prises en charge par une mise à jour logicielle, le téléchargement échoue pour cette mise à jour logicielle.  

16. Sur la page Résumé, passez en revue les paramètres. Pour enregistrer les paramètres dans un modèle de déploiement, cliquez sur **Enregistrer comme modèle**, entrez un nom et sélectionnez les paramètres à inclure dans le modèle, puis cliquez sur **Enregistrer**. Pour modifier un paramètre configuré, cliquez sur la page de l'Assistant associée et modifiez le paramètre.  

    > [!WARNING]  
    >  Le nom du modèle peut comporter des caractères ASCII alphanumériques ainsi que les caractères **\\** (barre oblique inverse) ou **‘** (guillemet-apostrophe).  

17. Cliquez sur **Suivant** pour déployer la mise à jour logicielle.  

 Quand vous avez terminé l’Assistant, Configuration Manager télécharge les mises à jour logicielles dans la bibliothèque de contenu sur le serveur de site, distribue les mises à jour logicielles aux points de distribution configurés, puis déploie le groupe de mises à jour logicielles sur les clients du regroupement cible. Pour plus d’informations sur le processus de déploiement, consultez [Software update deployment process](../understand/software-updates-introduction.md#BKMK_DeploymentProcess).

## <a name="next-steps"></a>Étapes suivantes
[Surveiller les mises à jour logicielles](monitor-software-updates.md)
