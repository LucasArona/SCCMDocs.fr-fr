---
title: Packages et programmes
titleSuffix: Configuration Manager
description: Prend en charge les déploiements qui utilisent des packages et des programmes ou des applications avec System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 818abdeb24d4c050bb8517bffda9ece0b012852c
ms.sourcegitcommit: abfc9e1b3945637fa93ca8d3a11519493a5d5391
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/28/2019
ms.locfileid: "66264411"
---
# <a name="packages-and-programs-in-system-center-configuration-manager"></a>Packages et programmes dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager continue de prendre en charge les packages et les programmes qui étaient utilisés dans Configuration Manager 2007. Un déploiement qui utilise des packages et des programmes peut être plus adapté qu’un déploiement qui utilise une application lors du déploiement de l’un des éléments suivants :  

- Applications pour les serveurs Linux et UNIX
- des scripts n’installant pas d’application sur un ordinateur, tel qu’un script pour défragmenter le lecteur de l’ordinateur ;
- des scripts exceptionnels qui ne doivent pas être surveillés en permanence ;  
- des scripts qui s’exécutent selon un planning défini et qui ne peuvent pas utiliser l’évaluation globale.

> [!TIP]  
> Envisagez d’utiliser la fonctionnalité [Scripts](/sccm/apps/deploy-use/create-deploy-scripts) dans la console Configuration Manager. Les scripts peuvent être une meilleure solution pour certains des scénarios précédents plutôt que d’utiliser des packages et des programmes.

Quand vous migrez des packages à partir d’une version antérieure de Configuration Manager, vous pouvez les déployer dans votre hiérarchie Configuration Manager. Une fois la migration terminée, les packages apparaissent dans le nœud **Packages** de l’espace de travail **Bibliothèque de logiciels** .

Vous pouvez modifier et déployer ces packages de la même façon que pour la distribution de logiciels. L’**Assistant Importation d’un package à partir d’une définition** reste dans Configuration Manager pour importer les packages hérités. Les publications sont converties en déploiements quand elles sont migrées de Configuration Manager 2007 vers une hiérarchie Configuration Manager.  

> [!NOTE]  
>  Vous pouvez utiliser Microsoft System Center Configuration Manager Package Conversion Manager pour convertir les packages et les programmes en applications Configuration Manager.  
>   
>  Pour plus d'informations, consultez [Gestionnaire de conversion des packages Configuration Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Les packages peuvent utiliser certaines nouvelles fonctionnalités de Configuration Manager, notamment les groupes de points de distribution et la surveillance. Les applications Microsoft Application Virtualization (App-V) ne peuvent pas être distribuées à l’aide de packages et de programmes dans Configuration Manager. Pour distribuer des applications virtuelles, vous devez les créer en tant qu’applications Configuration Manager.  

##  <a name="create-a-package-and-program"></a>Créer un package et un programme  
 Utilisez l’une de ces procédures pour créer ou importer aisément des packages et des programmes.  

### <a name="create-a-package-and-program-using-the-create-package-and-program-wizard"></a>Créer un package et un programme à l’aide de l’Assistant Création d’un package et d’un programme  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.  

2. Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer le package**.  

3. Sur la page **Package** de l' **Assistant Création d'un package et d'un programme**, spécifiez les informations suivantes :  

   -   **Nom** : spécifiez un nom pour le package, avec un maximum de 50 caractères.  

   -   **Description** : spécifiez une description pour ce package, avec un maximum de 128 caractères.  

   -   **Fabricant** (facultatif) : spécifiez un nom de fabricant pour mieux identifier le package dans la console Configuration Manager. Ce nom est limité à 32 caractères.

   -   **Langue** (facultatif) : spécifiez la version linguistique du package, avec un maximum de 32 caractères.  

   -   **Version** (facultatif) : spécifiez un numéro de version pour le package, avec un maximum de 32 caractères.

   -   **Ce package contient des fichiers sources** : ce paramètre indique si le package nécessite la présence de fichiers sources sur les appareils clients. Par défaut, cette case est décochée et Configuration Manager n’utilise pas de points de distribution pour le package. Lorsque cette case à cocher est activée, les points de distribution sont utilisés.  

   -   **Dossier source** : si le package contient des fichiers sources, choisissez **Parcourir** pour ouvrir la boîte de dialogue **Définir le dossier source** et spécifiez l’emplacement des fichiers sources du package.  

       > [!NOTE]  
       >  Le compte d’ordinateur du serveur de site doit disposer d’autorisations d’accès en lecture au dossier source que vous spécifiez.  

4. Dans la page **Type de programme** de l’**Assistant Création d’un package et d’un programme**, sélectionnez le type de programme que vous souhaitez créer, puis choisissez **Suivant**. Vous pouvez créer un programme pour un ordinateur ou un appareil, ou vous pouvez ignorer cette étape et créer un programme ultérieurement.  

   > [!TIP]  
   >  Pour créer un programme pour un package existant, sélectionnez d’abord le package. Sous l’onglet **Accueil**, dans le groupe **Package**, choisissez **Créer un programme** pour ouvrir l’**Assistant Création d’un programme**.  

5. Utilisez l'une des procédures suivantes pour créer un programme standard ou un programme de périphérique.  

   #### <a name="create-a-standard-program"></a>Créer un programme standard  

   1.  Dans la page **Type de programme** de l’**Assistant Création d’un package et d’un programme**, choisissez **Programme standard**, puis **Suivant**.     

   2.  Dans la page **Programme standard**, spécifiez les informations suivantes :  

       -   **Nom :** Spécifiez un nom pour le programme avec un maximum de 50 caractères.  

           > [!NOTE]  
           >  Le nom du programme doit être unique au sein d'un package. Après avoir créé un programme, vous ne pouvez pas modifier son nom.  

       -   **Ligne de commande** : entrez la ligne de commande à utiliser pour démarrer ce programme ou choisissez **Parcourir** pour naviguer jusqu’à l’emplacement du fichier.  

           Si un nom de fichier n’a pas d’extension définie, Configuration Manager tente d’utiliser .com, .exe et .bat comme extensions possibles.  

            Quand le programme est exécuté sur un client, Configuration Manager commence par rechercher le nom du fichier de ligne de commande au sein du package, dans le dossier Windows local, puis dans le dossier *%chemin%* local. Si le fichier demeure introuvable, le programme échoue.  

       -   **Dossier de démarrage**  (facultatif) : spécifiez le dossier à partir duquel le programme s’exécute, avec un maximum de 127 caractères. Ce dossier peut être un chemin absolu sur le client ou un chemin relatif au dossier du point de distribution qui contient le package.

       -   **Exécuter** : spécifiez le mode dans lequel le programme s’exécute sur les ordinateurs clients. Sélectionnez l’un des paramètres suivants :  

           -   **Normal** : le programme est exécuté en mode normal, en fonction des valeurs par défaut du système et du programme. Il s'agit du mode par défaut.  

           -   **Réduite** : le programme est exécuté sous forme réduite sur les appareils clients. Les utilisateurs peuvent voir l’activité de l’installation dans la zone de notification ou la barre des tâches.  

           -   **Agrandie** : le programme est exécuté sous forme agrandie sur les appareils clients. Les utilisateurs voient toute l’activité de l’installation.  

           -   **Masquée** : le programme est exécuté sous forme masquée sur les appareils clients. Les utilisateurs ne voient aucune activité d’installation.  

       -   **Le programme peut s’exécuter** : spécifiez si le programme s’exécute uniquement quand un utilisateur est connecté, uniquement quand aucun utilisateur n’est connecté, ou qu’un utilisateur soit connecté ou non sur l’ordinateur client.  

       -   **Mode d’exécution** : spécifiez si le programme s’exécute avec des autorisations administratives ou les autorisations de l’utilisateur actuellement connecté.  

       -   **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme** : utilisez ce paramètre pour spécifier s’il faut autoriser les utilisateurs à interagir avec l’installation du programme. Cette case à cocher n’est disponible que quand **Uniquement lorsqu’aucun utilisateur n’a de session ouverte** ou **Qu’un utilisateur ait ouvert une session ou non** est sélectionné pour **Le programme peut s’exécuter** et qu’**Exécuter avec les droits d’administration** est sélectionné pour **Mode d’exécution**.  

       -   **Mode lecteur** : spécifiez des informations sur la façon dont ce programme s’exécute sur le réseau. Choisissez l’une des options suivantes :  

           -   **S’exécute avec le nom UNC** : spécifiez que le programme s’exécute avec un nom Universal Naming Convention (UNC). Il s'agit du paramètre par défaut.  

           -   **Nécessite une lettre de lecteur** : spécifiez que le programme nécessite une lettre de lecteur pour qualifier entièrement son emplacement. Pour ce paramètre, Configuration Manager peut utiliser n’importe quelle lettre de lecteur disponible sur le client.  

           -   **Nécessite une lettre de lecteur spécifique** : spécifiez que le programme nécessite une lettre de lecteur spécifique que vous spécifiez pour qualifier entièrement son emplacement (par exemple, **Z:** ). Si la lettre de lecteur spécifiée est déjà utilisée sur un client, le programme ne s'exécute pas.  

       -   **Reconnecter au point de distribution à l’ouverture de session** : utilisez cette case à cocher pour indiquer si l’ordinateur client se reconnecte au point de distribution quand l’utilisateur ouvre une session. Par défaut, cette case à cocher est désactivée.  

   3.  Dans la page **Spécifications** de l’**Assistant Création d’un package et d’un programme**, spécifiez les informations suivantes :  

       -   **Exécuter un autre programme en premier** : utilisez ce paramètre pour identifier un package et un programme qui sont exécutés avant l’exécution de ce package et de ce programme.  

       -   **Exigences de plateformes** : sélectionnez **Ce programme peut être exécuté sur n’importe quelle plateforme** ou **Ce programme ne peut s’exécuter que sur des plateformes spécifiées**, puis choisissez les systèmes d’exploitation que les clients doivent exécuter pour pouvoir installer le package et le programme.  

       -   **Espace disque estimé** : spécifiez l’espace disque nécessaire à l’exécution du logiciel sur l’ordinateur. La valeur peut être **Inconnu** (paramètre par défaut) ou un chiffre supérieur ou égal à zéro. Si vous spécifiez une valeur, des unités doivent également être spécifiées pour cette valeur.  

       -   **Durée maximale d'exécution allouée (en minutes)** : spécifiez la durée maximale d'exécution attendue du programme sur l'ordinateur client. La valeur peut être **Inconnu** (paramètre par défaut) ou un chiffre supérieur à zéro.  

            Par défaut, cette valeur est définie à 120 minutes.  

           > [!IMPORTANT]  
           >  Si vous utilisez des fenêtres de maintenance pour le regroupement sur lequel ce programme est exécuté, un conflit peut survenir si la **Durée maximale d’exécution allouée** est supérieure à la fenêtre de maintenance programmée. Toutefois, si la durée maximale d’exécution a la valeur **Inconnu**, le programme démarre pendant la fenêtre de maintenance et continue de s’exécuter si nécessaire après la fermeture de la fenêtre de maintenance. Si la durée maximale d’exécution définie par l’utilisateur dépasse la longueur de toutes les fenêtres de maintenance disponibles, le programme n’est pas exécuté.  

            Si la valeur définie est **Inconnu**, Configuration Manager fixe la durée maximale d’exécution allouée à 12 heures (720 minutes).  

           > [!NOTE]  
           >  Si cette durée d’exécution maximale (qu’elle soit définie par l’utilisateur ou qu’il s’agisse de la valeur par défaut) est dépassée, Configuration Manager arrête le programme si **Exécuter avec les droits d’administration** est sélectionné et si **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme** n’est pas sélectionné.  

   4.  Choisissez **Suivant**.  

   #### <a name="create-a-device-program"></a>Créer un programme d’appareil  

   1.  Dans la page **Type de programme** de l’**Assistant Création d’un package et d’un programme**, sélectionnez **Programme pour le périphérique**, puis **Suivant**.  

   2.  Dans la page **Programme pour le périphérique**, spécifiez les informations suivantes :  

       -   **Nom** : spécifiez un nom pour le programme, avec un maximum de 50 caractères.  

           > [!NOTE]  
           >  Le nom du programme doit être unique au sein d'un package. Après avoir créé un programme, vous ne pouvez pas modifier son nom.  

       -   **Commentaire** (facultatif) : spécifiez un commentaire pour ce programme d’appareil, avec un maximum de 127 caractères.  

       -   **Dossier de téléchargement** : spécifiez le nom du dossier sur l’appareil Windows CE dans lequel les fichiers sources du package seront stockés. La valeur par défaut est **\Temp\\** .  

       -   **Ligne de commande** : entrez la ligne de commande à utiliser pour démarrer ce programme ou choisissez **Parcourir** pour naviguer jusqu’à l’emplacement du fichier.  

       -   **Exécuter la ligne de commande à partir du dossier de téléchargement** : sélectionnez cette option pour exécuter le programme à partir du dossier de téléchargement spécifié précédemment.  

       -   **Exécuter la ligne de commande à partir de ce dossier** : sélectionnez cette option pour spécifier un autre dossier à partir duquel exécuter le programme.  

   3.  Dans la page **Spécifications**, spécifiez les informations suivantes :  

       -   **Espace disque estimé** : spécifiez l’espace disque nécessaire pour le logiciel. Il est indiqué aux utilisateurs d’appareils mobiles avant l’installation du programme.  

       -   **Télécharger le programme** : spécifiez des informations indiquant quand ce programme peut être téléchargé vers des appareils mobiles. Vous pouvez spécifier **Dès que possible**, **Uniquement avec un réseau à haut débit**ou **Uniquement lorsque le périphérique est dans sa station d’accueil**.  

       -   **Configuration requise supplémentaire** : spécifiez toutes les exigences supplémentaires pour ce programme. Elles sont indiquées aux utilisateurs avant l’installation du logiciel. Par exemple, vous pouvez notifier aux utilisateurs dont ils ont besoin pour fermer toutes les autres applications avant d'exécuter le programme.  

   4.  Choisissez **Suivant**.  

   7.  Dans la page **Résumé**, passez en revue les actions qui seront exécutées, puis terminez l’Assistant.  

   Vérifiez que le nouveau package et le nouveau programme sont affichés dans le nœud **Packages** de l’espace de travail **Bibliothèque de logiciels**.  

## <a name="create-a-package-and-program-from-a-package-definition-file"></a>Créer un package et un programme à partir d’un fichier de définition de package  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.  

2. Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer un package à partir de la définition**.  

3. Dans la page **Définition du package** de l’**Assistant Création d’un package à partir d’une définition**, choisissez un fichier de définition de package existant ou cliquez sur **Parcourir** pour ouvrir un nouveau fichier de définition de package. Après avoir spécifié un nouveau fichier de définition de package, sélectionnez-le dans la liste **Définition du package**, puis choisissez **Suivant**.  

4. Dans la page **Fichiers sources**, spécifiez des informations sur tous les fichiers sources requis pour le package et le programme, puis choisissez **Suivant**.  

5. Si le package nécessite des fichiers sources, dans la page **Dossier source**, spécifiez l’emplacement à partir duquel les fichiers sources doivent être obtenus, puis choisissez **Suivant**.  

6. Dans la page **Résumé**, passez en revue les actions qui seront exécutées, puis terminez l’Assistant. Le nouveau package et le nouveau programme sont affichés dans le nœud **Packages** de l’espace de travail **Bibliothèque de logiciels**.  

   Pour plus d’informations sur les fichiers de définition de package, consultez [À propos du format des fichiers de définition de package](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) dans cette rubrique.  

##  <a name="deploy-packages-and-programs"></a>Déployer des packages et des programmes  

1. Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Packages**.  

2. Sélectionnez le package à déployer puis, sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Déployer**.  

3. Dans la page **Général** de l’**Assistant Déploiement logiciel**, spécifiez le nom du package et du programme à déployer, le regroupement vers lequel le package et le programme doivent être déployés et d’éventuels commentaires sur le déploiement.  

    Sélectionnez **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** si vous souhaitez enregistrer le contenu du package dans le groupe de points de distribution par défaut des regroupements. Si vous n’avez pas associé le regroupement sélectionné à un groupe de points de distribution, cette option n’est pas disponible.  

4. Dans la page **Contenu**, choisissez **Ajouter**, puis sélectionnez les points de distribution ou les groupes de points de distribution vers lesquels le contenu associé à ce package et ce programme doit être déployé.  

5. Dans la page **Paramètres de déploiement**, choisissez l’objet de ce déploiement, puis spécifiez des options pour les paquets de mise en éveil et les connexions limitées :  

   - **Objet** : choisissez parmi les options suivantes :  

     -   **Disponible** : si l’application est déployée sur un utilisateur, l’utilisateur peut voir le package et le programme publiés dans le catalogue d’applications et peut les demander au besoin. Si le package et le programme sont déployés sur un appareil, l’utilisateur peut les voir dans le Centre logiciel et les installer à la demande.  

     -   **Obligatoire** : le package et le programme sont déployés automatiquement, selon le calendrier configuré. Toutefois, un utilisateur peut suivre l'état de déploiement du package et du programme et peut les installer avant l'échéance depuis le Centre logiciel.  

     > [!NOTE]
     >  Si plusieurs utilisateurs sont connectés à l’appareil, les déploiements de package et de séquences de tâches peuvent ne pas s’afficher dans le centre logiciel.

   - **Envoyer des paquets de mise en éveil** : si l’objet du déploiement a la valeur **Obligatoire** et que cette option est sélectionnée, un paquet de mise en éveil est envoyé aux ordinateurs avant l’installation du déploiement, afin de sortir les ordinateurs de la veille à l’échéance de l’installation. Afin d'utiliser cette option, les ordinateurs doivent être configurés pour Wake On LAN.  

   - Si nécessaire, sélectionnez **Autoriser les clients avec une connexion Internet facturée à l’usage à télécharger le contenu une fois l’échéance d’installation atteinte, ce qui peut entraîner des frais supplémentaires**.  

   > [!NOTE]  
   >  L’option **Prédéployer des logiciels sur l’appareil principal de l’utilisateur** n’est pas disponible quand vous déployez un package et un programme.  

6. Dans la page **Planification**, indiquez à quel moment ce package et ce programme seront déployés ou mis à la disposition des appareils clients.  

    Les options de cette page peuvent différer selon que l’action de déploiement a la valeur **Disponible** ou **Obligatoire**.  

7. Si l’objet du déploiement a la valeur **Obligatoire**, configurez le comportement de réexécution du programme à partir du menu déroulant **Comportement de réexécution**. Choisissez parmi les options suivantes :  


   |             comportement de réexécution             |                                                                                                                        Informations complémentaires                                                                                                                        |
   |----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |      Ne jamais exécuter à nouveau un programme déployé      |                                                                      Le programme ne sera pas réexécuté sur le client, même si le programme a échoué initialement ou que les fichiers programmes sont modifiés.                                                                      |
   |          Toujours exécuter à nouveau le programme          |   Le programme est systématiquement réexécuté sur le client quand le déploiement est planifié, même si le programme a déjà été correctement exécuté. Cela peut être utile lorsque vous utilisez des déploiements périodiques dans lequel le programme est mis à jour, par exemple avec un logiciel antivirus.    |
   |    Exécuter à nouveau en cas d'échec de la tentative précédente    |                                                                              Le programme n’est réexécuté quand le déploiement est planifié qu’en cas d’échec de l’exécution précédente.                                                                              |
   | Exécuter à nouveau en cas de réussite de la tentative précédente | Le programme est réexécuté uniquement en cas de réussite de l’exécution précédente sur le client. Ceci s’avère particulièrement utile quand vous utilisez des publications récurrentes dans lesquelles le programme est régulièrement mis à jour et dans lesquelles chaque mise à jour exige la réussite de l’installation de la mise à jour précédente. |


8. Sur la page **Expérience utilisateur** , spécifiez les informations suivantes :  

    -   **Autoriser les utilisateurs à exécuter le programme indépendamment des attributions** : si cette option est activée, les utilisateurs peuvent installer ce logiciel à partir du Centre logiciel, indépendamment du moment auquel l’installation est planifiée.  

    -   **Installation du logiciel**: permet au logiciel d’être installé en dehors de toute fenêtre de maintenance configurée.  

    -   **Redémarrage du système (si nécessaire pour terminer l’installation)**  : si l’installation du logiciel nécessite un redémarrage de l’appareil pour se terminer, autorisez cette option en dehors des fenêtres de maintenance configurées.  

    -   **Appareils Windows Embedded** : quand vous déployez des packages et des programmes sur des appareils Windows Embedded dont le filtre d’écriture est activé, vous pouvez choisir d’installer les packages et les programmes sur un segment de recouvrement temporaire, puis de valider les modifications ultérieurement. Vous pouvez également valider les modifications à l’échéance de l’installation ou au cours d’une fenêtre de maintenance. Quand vous validez des modifications à l’échéance de l’installation ou au cours d’une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l’appareil.  

        > [!NOTE]  
        >  Lorsque vous déployez un package ou un programme sur un périphérique Windows Embedded, assurez-vous que le périphérique est un membre d'une collection qui dispose d'une fenêtre de maintenance configurée. Pour plus d’informations sur l’utilisation de fenêtres de maintenance pendant le déploiement de packages et de programmes sur des appareils Windows Embedded, consultez [Création d’applications Windows Embedded](../../apps/get-started/creating-windows-embedded-applications.md).  

9. Sur la page **Points de distribution** , spécifiez les informations suivantes :  

    -   **Options de déploiement** : spécifiez les actions qu’un client doit effectuer pour exécuter le contenu du programme. Vous pouvez spécifier le comportement lorsque le client est dans une limite réseau rapide ou une limite réseau lente ou instable.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau** : sélectionnez cette option pour réduire la charge sur le réseau en autorisant les clients à télécharger du contenu à partir d’autres clients sur le réseau qui a déjà téléchargé et mis en cache le contenu. Cette option utilise Windows BranchCache et peut être utilisée sur les ordinateurs qui exécutent Windows Vista SP2 et versions ultérieures.  

    -   **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** :  

        -  **Versions antérieures à 1610** : vous pouvez cocher la case **Autoriser un emplacement source de secours pour le contenu** afin de permettre aux clients situés en dehors de ces groupes de limites de revenir et d’utiliser le point de distribution comme emplacement source pour le contenu quand aucun autre point de distribution n’est disponible.

        - **Versions 1610 et ultérieures** : vous ne pouvez plus configurer **Autoriser un emplacement source de secours pour le contenu**.  Au lieu de cela, vous configurez des relations entre les groupes de limites qui déterminent quand un client peut commencer à rechercher un emplacement source de contenu valide dans d’autres groupes de limites.

10. Dans la page **Résumé**, passez en revue les actions qui seront exécutées, puis terminez l’Assistant.  

     Vous pouvez consulter le déploiement dans le nœud **Déploiement** de l'espace de travail **Surveillance** et dans le volet d'informations de l'onglet du déploiement de package, lorsque vous sélectionnez le déploiement. Pour plus d’informations, consultez [Surveiller les packages et les programmes](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) dans cette rubrique.  

> [!IMPORTANT]  
>  Si vous avez configuré l’option **Exécuter le programme à partir du point de distribution** dans la page **Points de distribution** de l’**Assistant Déploiement logiciel**, ne désactivez pas l’option **Copiez le contenu de ce package dans un partage de package sur les points de distribution**, car cela rend le package indisponible et empêche son exécution à partir des points de distribution.  

##  <a name="monitor-packages-and-programs"></a>Surveiller les packages et les programmes  
 Pour surveiller les déploiements de packages et de programmes, vous devez suivre les mêmes procédures que celles utilisées pour surveiller les applications, qui sont détaillées dans [Surveiller les applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Les packages et les programmes incluent également des rapports intégrés qui vous permettent de surveiller les informations relatives à l’état du déploiement des packages et des programmes. Ces rapports disposent des catégories **Distribution de logiciels – Packages et programmes** et **Distribution de logiciel - État du déploiement du package et du programme**.  

 Pour plus d’informations sur la configuration de la génération de rapports dans Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  <a name="manage-packages-and-programs"></a>Gérer les packages et les programmes  
 Dans l’espace de travail **Bibliothèque de logiciels**, développez **Gestion d’applications**, choisissez **Packages**, le package à gérer, puis une tâche de gestion dans le tableau suivant :  

|Tâche|Informations complémentaires|  
|----------|----------------------|  
|**Créer un fichier de contenu préparé**|Ouvre l’**Assistant Création du fichier de contenu préparé** qui vous permet de créer un fichier qui contient le contenu du package qui peut être importé manuellement vers un autre site. Ceci est utile dans les cas où vous disposez d'une faible bande passante du réseau entre le serveur de site et le point de distribution.|  
|**Créer un programme**|Ouvre l’**Assistant Création d’un programme** qui vous permet de créer un programme pour ce package.|  
|**Exporterer**|Ouvre l’**Assistant Exportation de package** qui vous permet d’exporter le package sélectionné et son contenu vers un fichier.<br /><br /> Pour plus d’informations sur l’importation des packages et des programmes, consultez [Créer des packages et des programmes](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) dans cette rubrique.|  
|**Déployer**|Ouvre l’**Assistant Déploiement logiciel** qui vous permet de déployer le package et le programme sélectionnés sur un regroupement. Pour plus d’informations, consultez [Déployer des packages et des programmes](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) dans cette rubrique.|  
|**Distribuer du contenu**|Ouvre l’**Assistant Distribuer du contenu** qui vous permet d’envoyer le contenu qui est associé au package et au programme vers les points de distribution ou groupes de points de distribution sélectionnés.|  
|**Mise à jour des points de distribution**|Met les points de distributions à jour avec le contenu le plus récent pour le package et le programme sélectionnés.|  

##  <a name="about-the-package-definition-file-format"></a>À propos du format des fichiers de définition de package  
 Les fichiers de définition de package sont des scripts qui vous permettent d’automatiser la création de packages et de programmes avec Configuration Manager. Ils procurent à Configuration Manager toutes les informations dont il a besoin pour créer un package et un programme, à l’exception de l’emplacement des fichiers sources du package. Chaque fichier de définition de package est un fichier texte ASCII ou UTF-8 qui utilise le format de fichier .ini et contient les sections suivantes :  

###  <a name="pdf"></a>[PDF]  
 Cette section identifie le fichier comme un fichier de définition de package. Il contient les informations suivantes :  

-   **Version** : spécifiez la version du format de fichier de définition de package utilisée par le fichier. Elle correspond à la version de System Management Server (SMS) ou de Configuration Manager pour laquelle il a été écrit. Cette entrée est obligatoire.  

###  <a name="package-definition"></a>[Package Definition]  
 Spécifiez les propriétés du package et du programme. Il fournit les informations suivantes :  

-   **Nom**: Le nom du package, comprenant jusqu'à 50 caractères.  

-   **Version** (facultatif) : version du package, comprenant jusqu’à 32 caractères.  

-   **Icon** (facultatif) : fichier contenant l’icône à utiliser pour ce package. Si elle est spécifiée, cette icône remplace l’icône de package par défaut dans la console Configuration Manager.

-   **Publisher**: éditeur du package, comprenant jusqu'à 32 caractères.

-   **Langue**: langue du package, comprenant jusqu'à 32 caractères.

-   **Comment** (facultatif) : commentaire concernant le package, comprenant jusqu’à 127 caractères.

-   **ContainsNoFiles**: cette entrée indique si une source est associée ou non au package.  

-   **Programs** : programmes qui sont définis pour ce package. Chaque nom de programme correspond à une section **[Program]** dans ce fichier de définition de package.  

     Exemple :  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: nom du fichier MIF (Management Information Format) qui contient l'état du package, limité à 50 caractères.  

-   **MIFName**: nom du package (pour la correspondance MIF), limité à 50 caractères.  

-   **MIFVersion**: numéro de version du package (pour la correspondance MIF), limité à 32 caractères.  

-   **MIFPublisher**: éditeur de logiciel du package (pour la correspondance MIF), qui peut comporter 32 caractères au maximum.  

###  <a name="program"></a>[Program]  
 Pour chaque programme spécifié dans l’entrée **Programs** de la section **[Package Definition]** , le fichier de définition de package doit inclure une section [Program] qui définit ce programme. Chaque section de programme fournit les informations suivantes :  

-   **Nom**: nom du programme, limité à 50 caractères. Cette entrée doit être unique dans un package. Ce nom est utilisé lors de la définition des publications. Sur les ordinateurs clients, le nom du programme est affiché dans **exécuter les programmes publiés** dans le panneau de configuration.  

-   **Icon** (facultatif) : spécifiez le fichier contenant l’icône à utiliser pour ce programme. Si elle est spécifiée, cette icône remplace l’icône de programme par défaut dans la console Configuration Manager et s’affiche sur les ordinateurs clients quand le programme est publié.

-   **Comment** (facultatif) : commentaire concernant le programme, comprenant jusqu’à 127 caractères.

-   **CommandLine** : spécifiez la ligne de commande du programme, comprenant jusqu’à 127 caractères. La commande est relatif au dossier source du package.

-   **StartIn** : spécifiez le dossier de travail pour le programme, comprenant jusqu’à 127 caractères. Cette entrée peut être un chemin absolu sur l’ordinateur client ou un chemin relatif au dossier source du package.

-   **Run** : spécifiez le mode d’exécution du programme. Vous pouvez spécifier **réduit**, **agrandie**, ou **masqué**. En l’absence de cette entrée, le programme s’exécute en mode normal.  

-   **AfterRunning** : spécifiez toute action spéciale qui se produit quand le programme est correctement terminé. Les options disponibles sont **SMSRestart**, **ProgramRestart**ou **SMSLogoff**. En l’absence de cette entrée, le programme n’exécute aucune action spéciale.  

-   **EstimatedDiskSpace** : spécifiez l’espace disque nécessaire à l’exécution du logiciel sur l’ordinateur. La valeur peut être **Inconnu** (paramètre par défaut) ou un chiffre supérieur ou égal à zéro. Si une valeur est spécifiée, les unités de la valeur doivent également être spécifiées.  

     Exemple :  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime** : spécifiez la durée estimée (en minutes) d’exécution du programme sur l’ordinateur client. La valeur peut être **Inconnu** (paramètre par défaut) ou un chiffre supérieur à zéro.  

     Exemple :  

     `EstimatedRunTime=25`  

-   **SupportedClients** : spécifiez les processeurs et les systèmes d’exploitation sur lesquels ce programme s’exécute. Les plateformes spécifiées doivent être séparés par des virgules. En l’absence de cette entrée, la vérification de la plateforme prise en charge est désactivée pour ce programme.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX** : spécifiez la plage du début à la fin pour les numéros de version des systèmes d’exploitation spécifiés dans l’entrée **SupportedClients**.  

     Exemple :  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements** (facultatif) : indiquez toute autre information ou exigence pour les ordinateurs clients, comprenant jusqu’à 127 caractères.

-   **CanRunWhen** : spécifiez l’état utilisateur nécessaire au programme pour qu’il s’exécute sur l’ordinateur client. Les valeurs disponibles sont **UserLoggedOn**, **NoUserLoggedOn**ou **AnyUserStatus**. La valeur par défaut est **UserLoggedOn**.  

-   **UserInputRequired** : spécifiez si le programme requiert une interaction avec l’utilisateur. Les valeurs disponibles sont **True** ou **False**. La valeur par défaut est **True**. Cette entrée est définie sur **False** si **CanRunWhen** n'a pas la valeur **UserLoggedOn**.  

-   **AdminRightsRequired** : spécifiez si le programme requiert des informations d’identification d’administration sur l’ordinateur pour pouvoir s’exécuter. Les valeurs disponibles sont **True** ou **False**. La valeur par défaut est **False**. Cette entrée est définie sur **True** si **CanRunWhen** n'a pas la valeur **UserLoggedOn**.  

-   **UseInstallAccount** : spécifiez si le programme utilise le compte d’installation du logiciel client quand il s’exécute sur les ordinateurs clients. Par défaut, cette valeur est **False**. Cette valeur est également **False** si **CanRunWhen** est défini à **UserLoggedOn**.  

-   **DriveLetterConnection** : spécifiez si le programme requiert une connexion de lettre de lecteur aux fichiers de package qui se trouvent sur le point de distribution. Vous pouvez spécifier **True** ou **False**. La valeur par défaut est **False**, ce qui permet au programme d’utiliser une connexion UNC (Universal Naming Convention). Quand la valeur est **True**, la lettre de lecteur suivante disponible est utilisée (en partant de Z: et en procédant par ordre décroissant).  

-   **SpecifyDrive** (facultatif) : spécifiez une lettre de lecteur dont le programme a besoin pour se connecter aux fichiers du package sur le point de distribution. Cette spécification force l'utilisation de la lettre de lecteur spécifiée pour les connexions clientes aux points de distribution.

-   **ReconnectDriveAtLogon** : spécifiez si l’ordinateur se reconnecte au point de distribution quand l’utilisateur se connecte. Les valeurs disponibles sont **True** ou **False**. La valeur par défaut est **False**.  

-   **DependentProgram** : spécifiez un programme dans ce package qui doit s’exécuter avant le programme actuel. Cette entrée utilise le format **DependentProgram**=<**nom_programme>** , où **<nom_programme\>** est l’entrée **Name** pour ce programme dans le fichier de définition de package. S'il n'existe pas de programme dépendant, laissez cette entrée vide.  

     Exemple :  

     DependentProgram = Admin  
    DependentProgram =  

-   **Assignment** : spécifiez la manière dont le programme est attribué aux utilisateurs. Cette valeur peut être **FirstUser** (seul le premier utilisateur qui se connecte au client exécute le programme) ou **EveryUser** (chaque utilisateur qui se connecte exécute le programme). Lorsque **CanRunWhen** n'a pas la valeur **UserLoggedOn**, cette entrée est définie sur **FirstUser**.  

-   **Désactivé** : spécifiez si ce programme peut être publié auprès de clients. Les valeurs disponibles sont **True** ou **False**. La valeur par défaut est **False**.  
