---
title: Gérer les mises à jour Office 365 ProPlus
titleSuffix: Configuration Manager
description: Configuration Manager synchronise les mises à jour du client Office 365 du catalogue WSUS vers le serveur de site de façon à rendre les mises à jour disponibles pour un déploiement sur les clients.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: eac542eb-9aa1-4c63-b493-f80128e4e99b
ms.openlocfilehash: 1fa5646b17646258e4863b3a53960c9c15497389
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418184"
---
# <a name="manage-office-365-proplus-with-configuration-manager"></a>Gérer Office 365 ProPlus avec Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Configuration Manager vous permet de gérer les applications Office 365 ProPlus comme suit :

- [Tableau de bord Gestion des clients Office 365](#office-365-client-management-dashboard) : vous pouvez consulter les informations sur un client Office 365 dans le tableau de bord Gestion des clients Office 365. À compter de Configuration Manager version 1802, le tableau de bord Gestion des clients Office 365 affiche une liste des appareils concernés quand des sections de graphe sont sélectionnées. <!--1357281 -->

- [Déployer des applications Office 365](#deploy-office-365-apps) : vous pouvez démarrer le programme d’installation d’Office 365 à partir du tableau de bord Gestion des clients Office 365 pour faciliter l’installation initiale des applications Office 365. L’Assistant vous permet de configurer les paramètres d’installation Office 365, de télécharger des fichiers à partir de réseaux de distribution de contenu Office et de créer et déployer une application de script avec le contenu.    

- [Déployer les mises à jour Office 365](#deploy-office-365-updates) : vous pouvez gérer les mises à jour du client Office 365 en utilisant le flux de travail de gestion des mises à jour logicielles. Lorsque Microsoft publie une nouvelle mise à jour du client Office 365 sur le réseau de distribution contenu (CDN) d’Office, Microsoft publie également un package de mise à jour sur Windows Server Update Services (WSUS). Après que Configuration Manager a synchronisé la mise à jour du client Office 365 du catalogue WSUS vers le serveur de site, la mise à jour est disponible pour un déploiement sur les clients.    

- [Ajouter des langues pour les téléchargements des mises à jour Office 365](#add-languages-for-office-365-update-downloads) : vous pouvez ajouter la prise en charge de Configuration Manager pour le téléchargement des mises à jour dans toutes les langues prises en charge par Office 365. Ainsi, Configuration Manager n’a pas à prendre en charge la langue dès lors qu’Office 365 le fait. Avant la version 1610 de Configuration Manager, il est nécessaire de télécharger et de déployer les mises à jour dans les langues configurées sur les clients Office 365. 

- [Modifier le canal de mise à jour](#change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager) : vous pouvez utiliser une stratégie de groupe pour distribuer un changement de valeur de clé de registre aux clients Office 365 afin de modifier le canal de mise à jour.


## <a name="office-365-client-management-dashboard"></a>Tableau de bord Gestion des clients Office 365  
Le tableau de bord Gestion des clients Office 365 fournit des graphiques pour les informations suivantes :

- Nombre de clients Office 365
- Versions du client Office 365
- Langues du client Office 365
- Canaux du client Office 365     
  Pour plus d’informations, consultez [Présentation des canaux de mise à jour pour Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).

Pour afficher le tableau de bord Gestion des clients Office 365 dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**. En haut du tableau de bord, utilisez le paramètre de liste déroulante **Regroupement** pour filtrer les données de tableau de bord selon les membres d’un regroupement spécifique. À compter de Configuration Manager version 1802, le tableau de bord Gestion des clients Office 365 affiche une liste des appareils concernés quand des sections de graphe sont sélectionnées.

### <a name="display-data-in-the-office-365-client-management-dashboard"></a>Afficher des données dans le tableau de bord Gestion des clients Office 365
Les données affichées dans le tableau de bord Gestion des clients Office 365 sont issues de l’inventaire matériel. Pour permettre l’affichage des données dans ce tableau de bord, activez l’inventaire matériel et sélectionnez la classe d’inventaire matériel **Configurations Office 365 ProPlus**. 
#### <a name="to-display-data-in-the-office-365-client-management-dashboard"></a>Pour afficher des données dans le tableau de bord Gestion des clients Office 365
1. Activez l’inventaire matériel si vous ne l’avez pas encore fait. Pour plus d’informations, consultez [Configurer l’inventaire matériel](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. Dans la console Configuration Manager, accédez à **Administration** > **Paramètres client** > **Paramètres client par défaut**.  
3. Dans l'onglet **Accueil** , dans le groupe **Propriétés** , cliquez sur **Propriétés**.  
4. Dans la boîte de dialogue **Paramètres client par défaut** , cliquez sur **Inventaire matériel**.  
5. Dans la liste **Paramètres du périphérique** , cliquez sur **Définir des classes**.  
6. Dans la boîte de dialogue **Classes d’inventaire matériel**, sélectionnez **Configurations Office 365 ProPlus**.  
7.  Cliquez sur **OK** pour enregistrer vos modifications et fermer la boîte de dialogue **Classes d'inventaire matériel** . <br/>Le tableau de bord Gestion des clients Office 365 commence à afficher des données dès qu’un inventaire matériel est signalé.

## <a name="deploy-office-365-apps"></a>Déployer des applications Office 365  
Démarrez le programme d’installation d’Office 365 à partir du tableau de bord Gestion des clients Office 365 pour l’installation initiale des applications Office 365. L’Assistant vous permet de configurer les paramètres d’installation Office 365, de télécharger des fichiers à partir de réseaux de distribution de contenu Office et de créer et déployer une application de script pour les fichiers. Tant qu’Office 365 n’est pas installé sur les clients et que la tâche [Mises à jour automatiques d’Office](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) ne s’exécute pas, les mises à jour Office 365 ne sont pas applicables. À titre d’essai, vous pouvez exécuter la tâche de mise à jour manuellement.

Dans les versions antérieures de Configuration Manager, vous devez exécuter les étapes suivantes pour installer des applications Office 365 pour la première fois sur les clients :
- Télécharger l’outil de déploiement Office 365 (ODT)
- Téléchargez les fichiers source d’installation Office 365, notamment tous les modules linguistiques dont vous avez besoin.
- Générez le fichier Configuration.xml qui spécifie la version et le canal Office corrects.
- Créez et déployez un package hérité ou une application de script pour les clients afin d’installer les applications Office 365.

### <a name="requirements"></a>spécifications
- L’ordinateur qui exécute le programme d’installation de Office 365 doit avoir accès à Internet.  
- L’utilisateur qui exécute le programme d’installation d’Office 365 doit avoir accès **en lecture** et en **écriture** au partage d’emplacement du contenu fourni dans l’Assistant.
- Si vous recevez une erreur de téléchargement 404, copiez les fichiers suivants dans le dossier utilisateur %temp% :
  - [releasehistory.xml](http://officecdn.microsoft.com/pr/wsus/releasehistory.cab)
  - [o365client_32bit.xml](http://officecdn.microsoft.com/pr/wsus/ofl.cab)  

### <a name="deploy-office-365-apps-using-configuration-manager-version-1806-or-higher"></a>Déployer des applications Office 365 à l’aide de Configuration Manager version 1806 ou supérieure : 
Depuis Configuration Manager 1806, l’Outil de personnalisation Office est intégré au programme d’installation d’Office 365 dans la console Configuration Manager. Au moment de créer un déploiement pour Office 365, vous pouvez configurer dynamiquement les derniers paramètres de gestion Office. <!--1358149-->

1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.
2. Cliquez sur **Office 365 Installer** (Programme d’installation d’Office 365) dans le volet supérieur droit. L’Assistant Installation d’Office 365 Client s’ouvre.
3. Dans la page **Application Settings** (Paramètres de l’application), indiquez le nom et une description de l’application, entrez l’emplacement de téléchargement pour les fichiers, puis cliquez sur **Suivant**. L’emplacement doit être spécifié sous la forme &#92;&#92;*server*&#92;*share*.
4. Dans la page **Paramètres Office**, cliquez sur **Accéder à l’Outil de personnalisation Office**. L’[Outil de personnalisation Office pour Démarrer en un clic](https://config.office.com) s’ouvre.
5. Configurez les paramètres souhaités pour votre installation Office 365. Cliquez sur **Envoyer** en haut à droite de la page une fois la configuration terminée. 
6. Dans la page **Déploiement**, déterminez si vous souhaitez procéder à un déploiement immédiat ou ultérieur. Si vous choisissez de déployer plus tard, vous pouvez trouver l’application dans **Bibliothèque de logiciels** < **Gestion des applications** < **Applications**.  
7. Confirmez les paramètres dans la page **Résumé**. 
8. Cliquez sur **Suivant**, puis sur **Fermer** à la fin de l’Assistant Installation du client Office 365. 

### <a name="deploy-office-365-apps-using-configuration-manager-version-1802-and-prior"></a>Déployer des applications Office 365 à l’aide de Configuration Manager version 1802 et antérieures :

1. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365**.
2. Cliquez sur **Office 365 Installer** (Programme d’installation d’Office 365) dans le volet supérieur droit. L’Assistant Installation d’Office 365 Client s’ouvre.
3. Dans la page **Application Settings** (Paramètres de l’application), indiquez le nom et une description de l’application, entrez l’emplacement de téléchargement pour les fichiers, puis cliquez sur **Suivant**. L’emplacement doit être spécifié sous la forme &#92;&#92;*server*&#92;*share*.
4. Dans la page **Importer les paramètres du client**, choisissez si vous voulez importer les paramètres du client Office 365 à partir d’un fichier de configuration XML existant ou spécifier manuellement les paramètres. Cliquez sur **Suivant** lorsque vous avez terminé.  

    Quand vous avez un fichier de configuration, entrez l’emplacement du fichier et passez à l’étape 7. Vous devez spécifier l’emplacement sous la forme &#92;&#92;*serveur*&#92;*partage*&#92;*nom_fichier*.XML.
    > [!IMPORTANT]    
    > Le fichier de configuration XML doit contenir uniquement des [langues prises en charge par le client Office 365 ProPlus](https://docs.microsoft.com/deployoffice/office2016/language-identifiers-and-optionstate-id-values-in-office-2016).

5. Dans la page **Produits du client**, sélectionnez la suite Office 365 que vous utilisez. Sélectionnez les applications que vous souhaitez inclure. Sélectionnez tous les autres produits Office qui doivent être inclus, puis cliquez sur **Suivant**.
6. Dans la page **Paramètres client**, choisissez les paramètres à inclure, puis cliquez sur **Suivant**.
7. Dans la page **Déploiement**, choisissez de déployer ou non l’application, puis cliquez sur **Suivant**. <br/>Si vous choisissez de ne pas déployer le package dans l’Assistant, passez à l’étape 9.
8. Configurez le reste des pages de l’Assistant comme vous le feriez pour un déploiement d’application standard. Pour plus d’informations, consultez [Créer et déployer une application](/sccm/apps/get-started/create-and-deploy-an-application).
9. Effectuez toutes les étapes de l'Assistant.
10. Vous pouvez déployer ou modifier l’application dans **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des applications** > **Applications**.    

Une fois que vous avez créé et déployé des applications Office 365 à l’aide du programme d’installation d’Office 365, Configuration Manager ne gère plus les mises à jour Office par défaut. Pour permettre aux clients Office 365 de recevoir les mises à jour de Configuration Manager, consultez [Déployer les mises à jour d’Office 365 avec Configuration Manager](#deploy-office-365-updates-with-configuration-manager).

Après avoir déployé des applications Office 365, vous pouvez créer des règles de déploiement automatique pour mettre à jour les applications. Pour créer une règle de déploiement automatique pour les applications Office 365, cliquez sur **Créer un ADR** dans le tableau de bord Gestion des clients Office 365. Sélectionnez **Client Office 365** quand vous choisissez le produit. Pour plus d’informations, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).


## <a name="deploy-office-365-updates"></a>Déploiement des mises à jour Office 365
Une tâche planifiée [Mises à jour automatiques dans Office 365](https://docs.microsoft.com/deployoffice/overview-of-the-update-process-for-office-365-proplus) s’exécute plusieurs fois par semaine. Si votre installation d’Office 365 est récente, il se peut que le canal de mise à jour n’a pas encore été défini et que la recherche de mises à jour ne trouve pas de mises à jour applicables. À titre d’essai, vous pouvez démarrer la tâche de mise à jour manuellement. 

Procédez comme suit pour déployer les mises à jour d’Office 365 avec le Gestionnaire de Configuration :

1.  [Vérifiez la configuration requise](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#requirements-for-using-configuration-manager-to-manage-office-365-client-updates) pour utiliser Configuration Manager en vue de gérer les mises à jour du client Office 365 dans la section **Configuration requise pour utiliser Configuration Manager afin de gérer les mises à jour du client Office 365** de l’article.  

2.  [Configurez les points de mise à jour logicielle](../get-started/configure-classifications-and-products.md) pour synchroniser les mises à jour du client Office 365. Définissez **Mises à jour** en guise de classification et sélectionnez **Office 365 Client** en guise de produit. Synchronisez les mises à jour logicielles après avoir configuré les points de mise à jour logicielle pour utiliser la classification **Mises à jour**.
3.  Habilitez les clients Office 365 à recevoir des mises à jour de Configuration Manager. Utilisez les paramètres du client Configuration Manager ou la stratégie de groupe pour activer le client.   

    **Méthode 1** : à compter de Configuration Manager version 1606, vous pouvez utiliser le paramètre du client Gestionnaire de configuration pour gérer l’agent client Office 365. Après avoir configuré ce paramètre et déployé les mises à jour Office 365, l’agent client Configuration Manager communique avec l’agent client Office 365 pour télécharger les mises à jour à partir d’un point de distribution et les installer. Configuration Manager dresse l’inventaire des paramètres du client Office 365 ProPlus.    

      1.  Dans la console Configuration Manager, cliquez sur **Administration** > **Vue d’ensemble** > **Paramètres client**.  

      2.  Ouvrez les paramètres d’appareil appropriés pour activer l’agent client. Pour plus d’informations sur les paramètres par défaut et personnalisés du client, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).  

      3.  Cliquez sur **Mises à jour logicielles** et sélectionnez **Oui** pour le paramètre **Activer la gestion de l’agent Office 365 Client**.  

    **Méthode 2** : [Habilitez les clients Office 365 à recevoir les mises à jour](/DeployOffice/manage-updates-to-office-365-proplus-with-system-center-configuration-manager#BKMK_EnableClient) de Configuration Manager via l’outil de déploiement Office ou la stratégie de groupe.  

4. [Déployez les mises à jour d’Office 365](deploy-software-updates.md) sur les clients.   

> [!Important]
> - Depuis la version 1706 de Configuration Manager, les mises à jour clients Office 365 ont été déplacées vers le nœud **Gestion des clients Office 365** >**Mises à jour Office 365**. Ce déplacement est sans effet sur la configuration actuelle des règles de déploiement automatique. 
> - Avant la version 1610 de Configuration Manager, il est nécessaire de télécharger et de déployer les mises à jour dans les langues configurées sur les clients Office 365. Par exemple, supposons que vous disposiez d’un client Office 365 configuré avec les langues en-us et fr-fr. Sur le serveur de site, vous téléchargez et déployez uniquement le contenu en-us pour une mise à jour Office 365 applicable. Lorsque l’utilisateur commence l’installation de cette mise à jour à partir du Centre logiciel, celle-ci se bloque pendant le téléchargement du contenu de-de.   


## <a name="restart-behavior-and-client-notifications-for-office-365-updates"></a>Comportement de redémarrage et notifications des clients pour les mises à jour d’Office 365
Quand vous déployez une mise à jour sur un client Office 365, le comportement de redémarrage et les notifications des clients diffèrent en fonction de la version de Configuration Manager. Le tableau suivant fournit des informations sur l’expérience utilisateur quand le client reçoit une mise à jour d’Office 365 :

|Version de Configuration Manager |Expérience de l’utilisateur final|  
|----------------|---------------------|
|1706, 1710|Le client reçoit des notifications contextuelles et dans l’application, ainsi qu’une boîte de dialogue de compte à rebours avant l’installation de la mise à jour.|
|1802| Le client reçoit des notifications contextuelles et dans l’application, ainsi qu’une boîte de dialogue de compte à rebours avant l’installation de la mise à jour. </br>Si des applications Office 365 sont en cours d’exécution au moment de l’application d’une mise à jour du client Office 365, rien ne les force à se fermer. Au lieu de cela, l’installation de la mise à jour affiche un message demandant le redémarrage du système <!--510006-->|


> [!Important]
>
>Dans Configuration Manager version 1706, notez les points suivants :
>
>- Une icône de notification s’affiche dans la zone de notification de la barre des tâches pour les applications requises dont l’échéance se situe dans un délai de 48 heures et dont le contenu de la mise à jour a été téléchargé. 
>- Un compte à rebours s’affiche pour les applications requises dont l’échéance se situe dans un délai de 7,5 heures et dont la mise à jour a été téléchargée. L’utilisateur peut reporter le compte à rebours jusqu’à trois fois avant l’échéance. Quand il est reporté, le compte à rebours s’affiche à nouveau au bout de deux heures. S’il n’est pas reporté, un compte à rebours de 30 minutes se déclenche et la mise à jour s’installe quand il est terminé.
>- Aucune notification contextuelle ne s’affiche tant que l’utilisateur ne clique pas sur l’icône située dans la zone de notification. De plus, si la zone de notification occupe un espace minimal, l’icône de notification peut ne pas être visible si l’utilisateur n’ouvre pas ou ne développe pas la zone de notification. 
>- La boîte de dialogue de notification et de compte à rebours peut s’afficher alors que l’utilisateur n’est pas actif sur l’appareil. Par exemple, quand l’appareil est verrouillé durant la nuit, il est possible que des applications Office en cours d’exécution sur l’appareil soient forcées à se fermer pour permettre l’installation de la mise à jour. Avant de fermer l’application, Office enregistre les données d’application pour empêcher une perte de données. 
>- Si l’échéance est passée ou configurée pour s’exécuter dès que possible, les applications Office en cours d’exécution peuvent être forcées à se fermer sans notification. 
>- Si l’utilisateur installe une mise à jour Office avant l’échéance, Configuration Manager vérifie que la mise à jour est installée quand l’échéance est atteinte. Si la mise à jour n’est pas détectée sur l’appareil, elle est installée. 
>- La barre de notification dans l’application ne s’affiche pas sur une application Office qui est en cours d’exécution avant le téléchargement de la mise à jour. Une fois la mise à jour téléchargée, la notification dans l’application s’affiche uniquement pour les applications nouvellement ouvertes.
>- Pour les mises à jour Office déclenchées par une fenêtre de service ou planifiées pour s’exécuter en dehors des heures d’ouverture, il est possible que les applications Office en cours d’exécution soient forcées à se fermer pour installer la mise à jour sans notification. 
>- Pour plus d’informations, consultez [Notifications de mise à jour pour les utilisateurs finaux avec Office 365](https://docs.microsoft.com/deployoffice/end-user-update-notifications-for-office-365-proplus)



## <a name="add-languages-for-office-365-update-downloads"></a>Ajouter des langues pour les téléchargements des mises à jour Office 365
Vous pouvez configurer Configuration Manager pour qu’il télécharge des mises à jour dans toutes les langues prises en charge par Office 365, que celles-ci soient ou non prises en charge par Configuration Manager.    

> [!IMPORTANT]  
> La configuration de langues supplémentaires pour les mises à jour Office 365 est un paramètre qui s’étend au niveau du site. Une fois les langues ajoutées à l’aide de la procédure suivante, toutes les mises à jour Office 365 sont téléchargées dans ces langues, ainsi que dans celles sélectionnées dans la page **Sélection de la langue** de l’Assistant Téléchargement des mises à jour logicielles ou de l’Assistant Déploiement des mises à jour logicielles.

### <a name="to-add-support-to-download-updates-for-additional-languages"></a>Pour télécharger des mises à jour dans des langues supplémentaires
Utilisez la procédure suivante sur le site d’administration centrale ou sur le site principal autonome du point de mise à jour logicielle.
1. À partir d’une invite de commande, tapez *wbemtest* avec des droits d’administration pour ouvrir le testeur WMI.
2. Cliquez sur **Connexion**, puis tapez *root\sms\site_&lt;siteCode&gt;*.
3. Cliquez sur **Requête**, puis exécutez la requête suivante : *select &#42; from SMS_SCI_Component where componentname ="SMS_WSUS_CONFIGURATION_MANAGER"*  
   ![Requête WMI](../media/1-wmiquery.png)
4. Dans le volet des résultats, double-cliquez sur l’objet avec le code de site pour le site d’administration centrale ou le site principal autonome.
5. Sélectionnez la propriété **Props**, cliquez sur **Modifier la propriété**, puis cliquez sur **Vue incorporée**.
   ![Éditeur de propriétés](../media/2-propeditor.png)
6. En commençant par le premier résultat de la requête, ouvrez chaque objet jusqu’à ce que vous trouviez celui dont la propriété **PropertyName** a la valeur **AdditionalUpdateLanguagesForO365**.
7. Sélectionnez **Value2**, puis cliquez sur **Modifier la propriété**.  
   ![Modifier la propriété Value2](../media/3-queryresult.png)
8. Ajoutez des langues supplémentaires à la propriété **Value2**, puis cliquez sur **Enregistrer la propriété**. <br/> Par exemple : pt-pt (Portugais - Portugal), af-za (Afrikaans - Afrique du Sud), nn-no (Norvégien [Nynorsk] - Norvège), etc. Vous devez taper `pt-pt,af-za,nn-no` pour les langues de l’exemple. N’utilisez pas d’espaces entre les langues.
 
   ![Ajouter des langues dans l’Éditeur de propriétés](../media/4-props.png)  
9. Cliquez sur **Fermer**, cliquez sur **Fermer**, cliquez sur **Enregistrer la propriété**, puis cliquez sur **Enregistrer l’objet** (si vous cliquez sur **Fermer** ici, les valeurs sont ignorées). Cliquez sur **Fermer**, cliquez sur **Quitter**, puis fermez le testeur WMI.
10. Dans la console Configuration Manager, accédez à **Bibliothèque de logiciels** > **Vue d’ensemble** > **Gestion des clients Office 365** > **Mises à jour Office 365**.
11. Désormais, quand vous téléchargez des mises à jour Office 365, celles-ci sont téléchargées dans les langues sélectionnées dans l’Assistant et dans celles configurées durant cette procédure. Pour vérifier que les mises à jour sont téléchargées dans les langues correctes, accédez à la source du package de la mise à jour et recherchez les fichiers dont le nom comprend le code de langue.  
    ![Noms de fichiers avec des langues supplémentaires](../media/5-verification.png)

## <a name="updating-office-365-during-task-sequences-when-office-365-is-installed-in-the-base-image"></a>Mise à jour d’Office 365 pendant des séquences de tâches quand Office 365 est installé dans l’image de base
Quand Office 365 est déjà installé dans l’image du système d’exploitation que vous installez, il se peut que la valeur de la clé de Registre du canal de mise à jour corresponde à l’emplacement d’installation d’origine. Dans ce cas, la recherche de mises à jour n’affiche aucune mise à jour du client Office 365 comme étant applicable. Une tâche planifiée de mises à jour automatiques d’Office s’exécute plusieurs fois par semaine. Après l’exécution de cette tâche, le canal de mise à jour pointe vers l’URL du CDN Office configurée et l’analyse affiche ces mises à jour comme étant applicables. <!--510452-->

Afin de vérifier que le canal de mise à jour est défini pour trouver les mises à jour applicables, effectuez les étapes suivantes :
1. Sur une machine avec la même version d’Office 365 que celle de l’image de base de système d’exploitation, ouvrez le Planificateur de tâches (taskschd.msc) et identifiez la tâche de mise à jour automatique d’Office 365. En règle générale, elle se trouve sous **Bibliothèque du Planificateur de tâches** >**Microsoft**>**Office**.
2. Cliquez avec le bouton droit sur la tâche des mises à jour automatiques et sélectionnez **Propriétés**.
3. Accédez à l’onglet **Actions** et cliquez sur **Modifier**. Copiez la commande et les arguments. 
4. Dans la console Configuration Manager, modifiez votre séquence de tâches.
5. Ajoutez une nouvelle étape **Exécuter la ligne de commande** avant l’étape **Installer les mises à jour** dans la séquence de tâches. 
6. Copiez la commande et les arguments que vous avez regroupés à partir de la tâche planifiée de mises à jour automatiques d’Office. 
7. Cliquez sur **OK**. 

## <a name="change-the-update-channel-after-you-enable-office-365-clients-to-receive-updates-from-configuration-manager"></a>Modifier le canal de mise à jour une fois les clients Office 365 habilités à recevoir des mises à jour de Configuration Manager
Pour modifier le canal de mise à jour une fois que les clients Office 365 sont habilités à recevoir des mises à jour de Configuration Manager, utilisez une stratégie de groupe pour distribuer un changement de valeur de clé de registre aux clients Office 365. Modifiez la clé de Registre **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Office\ClickToRun\Configuration\CDNBaseUrl** pour qu’elle utilise l’une des valeurs suivantes :

- Canal mensuel <br/>
<i>(anciennement Canal actuel)</i> :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/492350f6-3a01-4f97-b9c0-c7c6ddf67d60

- Canal semi-annuel <br/>
<i>(anciennement Canal différé)</i> :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/7ffbc6bf-bc32-4f92-8982-f9dd17fd3114

- Canal mensuel (ciblé)<Br/>
 <i>(anciennement Groupe First Release pour Canal actuel)</i> :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/64256afe-f5d9-4f86-8936-8840a6a4f5be

- Canal semi-annuel (ciblé) <br/>
<i>(anciennement Groupe First Release pour Canal différé)</i> :  
  **CDNBaseUrl** = http&#58;//officecdn.microsoft.com/pr/b8f9b850-328d-4355-9145-c59439a0c4cf <!--the channel names changed in Sept 2017- https://docs.microsoft.com/en-us/DeployOffice/overview-of-update-channels-for-office-365-proplus?ui=en-US&rs=en-US&ad=US-->


<!--- You can create an Office 365 app without using the Office 365 Installation Wizard. To do this, you use the Office 2016 Deployment Tool (ODT) to download Office installation source files to a network share, generate Configure.xml that specifies the correct Office version and channel, and so on. Then, create an app for the files using the normal app management process.
> [!Note]
> The Office 365 Installation Wizard was introduced in Configuration Manager version 1702 and provides an easy way to create Office 365 apps.

- [Download the Office 2016 Deployment Tool](http://aka.ms/ODT2016) from the Microsoft Download Center.  
- Review the [configuration options for the Office Deployment Tool](https://technet.microsoft.com/library/jj219426.aspx).

You can create an application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**. For details, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
--->

<!--- ## Next steps
Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps. For details, see [Manage Office 365 apps](manage-office-365-apps.md). --->
