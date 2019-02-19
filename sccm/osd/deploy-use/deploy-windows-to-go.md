---
title: Déployer Windows To Go
titleSuffix: Configuration Manager
description: Découvrez comment mettre en service Windows To Go dans System Center Configuration Manager pour créer un espace de travail Windows To Go qui démarre à partir d’un lecteur externe.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 8eed50f5-80a4-422e-8aa6-a7ccb2171475
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 494824f80c03e05535ca73d38974a8fc68489ee5
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56122659"
---
# <a name="deploy-windows-to-go-with-system-center-configuration-manager"></a>Déployer Windows To Go avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique fournit les étapes permettant de mettre en service Windows To Go dans System Center Configuration Manager. Windows To Go est une fonctionnalité d'entreprise de Windows 8 qui permet de créer un espace de travail Windows To Go pouvant être démarré à partir d'un lecteur externe USB sur les ordinateurs qui satisfont les conditions de certification de Windows 7 ou Windows 8, quel que soit le système d'exploitation en cours d'exécution sur ces ordinateurs. Les espaces de travail Windows To Go peuvent utiliser la même image que celle que les entreprises utilisent pour leurs ordinateurs de bureau et ordinateurs portables ; ils peuvent être gérés de la même façon.  

 Pour plus d’informations sur Windows To Go, consultez [Windows To Go : vue d’ensemble des fonctionnalités](http://go.microsoft.com/fwlink/p/?LinkId=263433).  

## <a name="provision-windows-to-go"></a>Préparer Windows To Go  
 Windows To Go est un système d'exploitation stocké sur un lecteur externe USB. Vous pouvez préparer le lecteur Windows To Go de la même manière que vous préparez les déploiements d'autres systèmes d'exploitation. Toutefois, étant donné que Windows To Go a vocation à constituer une solution centrée sur l'utilisateur et hautement mobile, vous devez adopter une approche légèrement différente pour préparer ces lecteurs.  

 À niveau élevé, Windows To Go est un déploiement en deux phases qui vous permet de configurer le périphérique Windows To Go et le contenu préparé pour le déploiement du système d'exploitation. Vous pouvez y parvenir avec un impact minimal sur l’utilisateur tout en limitant le temps d’arrêt de son ordinateur. Une fois que vous avez préparé l'ordinateur, vous devez exécuter le processus de préparation pour vous assurer que l'ordinateur est prêt pour l'utilisateur. Le processus de préparation est similaire au processus de déploiement du système d'exploitation actif. Voici le flux de travail général pour préparer le contenu et préparer Windows To Go :  

1.  [Conditions préalables à la préparation de Windows To Go](#BKMK_Prereqs)  

2.  [Créer un média préparé](#BKMK_CreatePrestagedMedia)  

3.  [Créer un package Windows To Go Creator](#BKMK_CreatePackage)  

4.  [Mettre à jour la séquence de tâches pour activer BitLocker pour Windows To Go](#BKMK_UpdateTaskSequence)  

5.  [Déployer le package Windows To Go Creator et la séquence de tâches](#BKMK_Deployments)  

6.  [L’utilisateur exécute Windows To Go Creator](#BKMK_UserExperience)  

7.  [Configuration Manager configure et prépare le lecteur Windows To Go](#BKMK_ConfigureStageDrive)  

8.  [L’utilisateur ouvre une session Windows 8](#BKMK_UserLogsIn)  

###  <a name="BKMK_Prereqs"></a> Conditions préalables à la préparation de Windows To Go  
 Avant de mettre en service Windows To Go, vous devez effectuer les opérations suivantes dans Configuration Manager :  

-   **Distribuer une image de démarrage à un point de distribution**  

     avant de créer des médias préparés, vous devez distribuer l'image de démarrage à un point de distribution.  

    > [!NOTE]  
    >  Les images de démarrage sont utilisées pour installer le système d’exploitation sur les ordinateurs de destination dans votre environnement Configuration Manager. Elles contiennent une version de Windows PE qui installe le système d'exploitation, ainsi que les autres pilotes de périphérique nécessaires. Configuration Manager propose deux images de démarrage : Une pour prendre en charge les plates-formes x86 et l'autre pour prendre en charge les plates-formes x64. Vous pouvez également créer vos propres images de démarrage. Pour plus d’informations, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

-   **Distribuer l’image du système d’exploitation Windows 8 à un point de distribution**  

     avant de créer des médias préparés, vous devez distribuer l'image du système d'exploitation Windows 8 à un point de distribution.  

    > [!NOTE]  
    >  Les images de système d'exploitation sont des fichiers au format .WIM et représentent un regroupement compressé de fichiers et dossiers de référence nécessaires à l'installation et à la configuration d'un système d'exploitation sur un ordinateur. Pour plus d’informations, voir [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

-   **Créer une séquence de tâches pour déployer Windows 8**  

     vous devez créer une séquence de tâches pour un déploiement de Windows 8, auquel vous ferez référence lorsque vous créerez des médias préparés. Pour plus d’informations, consultez [Gérer les séquences de tâches pour automatiser des tâches](manage-task-sequences-to-automate-tasks.md).  

###  <a name="BKMK_CreatePrestagedMedia"></a> Créer un média préparé  
 Un média préparé contient l'image de démarrage utilisée pour démarrer l'ordinateur de destination et l'image du système d'exploitation qui est appliquée à l'ordinateur de destination. L'ordinateur que vous préparez avec des médias préparés peut être démarré à l'aide de l'image de démarrage. L'ordinateur peut alors exécuter une séquence de tâches de déploiement du système d'exploitation existant, pour installer un déploiement de système d'exploitation complet. La séquence de tâches qui déploie le système d'exploitation n'est pas incluse dans le média.  

 Vous pouvez ajouter du contenu, tel que des applications et des pilotes de périphériques, en plus de l’image du système d’exploitation et de l’image de démarrage, pendant la phase de préparation. Vous réduisez ainsi le temps nécessaire pour déployer un système d'exploitation et le trafic réseau car le contenu est déjà sur le lecteur.  

 Pour créer les médias préparés, appliquez la procédure suivante.  

#### <a name="to-create-prestaged-media"></a>Pour créer un média préparé  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4. Sur la page **Sélectionner le type de média** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

   -   Sélectionnez **Média préparé**.  

   -   Sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome** pour démarrer le déploiement de Windows To Go sans aucune interaction utilisateur.  

       > [!IMPORTANT]  
       >  Lorsque vous utilisez cette option avec la variable personnalisée SMSTSPreferredAdvertID (définie plus tard au cours de cette procédure), aucune interaction utilisateur n'est requise et l'ordinateur démarre automatiquement le déploiement de Windows To Go lorsqu'il détecte un lecteur Windows To Go. L'utilisateur est quand même invité à fournir un mot de passe si le média est configuré avec une protection par mot de passe. Si vous utilisez le paramètre **Autoriser le déploiement du système d'exploitation de manière autonome** sans configurer la variable SMSTSPreferredAdvertID, une erreur se produit lorsque vous déployez la séquence de tâches.  

5. Sur la page **Gestion du média** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

   -   Sélectionnez **Média dynamique** si vous souhaitez autoriser un point de gestion à rediriger le média vers un autre point de gestion, basé sur l'emplacement du client dans les limites du site.  

   -   Sélectionnez **Média basé sur le site** si vous souhaitez que le média contacte uniquement le point de gestion spécifié.  

6. Dans la page **Propriétés du média**  , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

   -   **Créé par** : spécifiez qui a créé le média.  

   -   **Version** : spécifiez le numéro de version du média.  

   -   **Commentaire** : spécifiez une description unique de ce pour quoi le média est utilisé.  

   -   **Fichier multimédia** : spécifiez le nom et le chemin d'accès des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Par exemple : **\\\nomserveur\dossier\outputfile.wim**  

7. Sur la page **Sécurité** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

   -   Sélectionnez **Activer la prise en charge d’ordinateur inconnu** pour autoriser le média à déployer un système d’exploitation sur un ordinateur qui n’est pas géré par Configuration Manager. Il n'existe aucun enregistrement de ces ordinateurs dans la base de données Configuration Manager. Les ordinateurs inconnus sont les suivants :  

       -   Un ordinateur sur lequel le client Configuration Manager n’est pas installé  

       -   Un ordinateur qui n’est pas importé dans Configuration Manager  

       -   Un ordinateur qui n’a pas été découvert par Configuration Manager.  

   -   Sélectionnez **Protéger le média à l'aide d'un mot de passe** et entrez un mot de passe fort pour mieux protéger le média contre les accès non autorisés. Lorsque vous spécifiez un mot de passe, l'utilisateur doit fournir ce mot de passe pour utiliser le média préparé.  

       > [!IMPORTANT]  
       >  Pour une sécurité optimale, il vous est conseillé de toujours attribuer un mot de passe pour protéger les médias préparés.  

       > [!NOTE]  
       >  Lorsque vous protégez le média préparé à l'aide d'un mot de passe, l'utilisateur est invité à entrer ce mot de passe même quand le média est configuré avec le paramètre **Autoriser le déploiement du système d'exploitation de manière autonome** .  

   -   Pour les communications HTTP, sélectionnez **Créer un certificat de média auto-signé**, puis spécifiez les dates de début et d'expiration du certificat.  

   -   Pour les communications HTTPS, sélectionnez **Importer un certificat PKI**, puis spécifiez le certificat à importer et son mot de passe.  

        Pour plus d’informations sur ce certificat client utilisé pour les images de démarrage, consultez [Configuration requise des certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Affinité entre utilisateur et appareil** : pour prendre en charge la gestion centrée sur l’utilisateur dans Configuration Manager, spécifiez la manière dont vous voulez que le média associe des utilisateurs à l’ordinateur de destination. Pour plus d’informations sur la prise en charge de l’affinité entre utilisateur et appareil par le déploiement de systèmes d’exploitation, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).  

       -   Spécifiez **Autoriser une affinité entre périphérique et utilisateur avec approbation automatique** si vous voulez que le média associe automatiquement des utilisateurs à l'ordinateur de destination. Cette fonctionnalité est basée sur les actions de la séquence de tâches qui déploie le système d'exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l'ordinateur de destination lorsqu'elle déploie le système d'exploitation sur l'ordinateur de destination.  

       -   Spécifiez **Autoriser une affinité entre périphérique et utilisateur en attente de l'approbation de l'administrateur** si vous souhaitez que le média associe des utilisateurs à l'ordinateur de destination une fois l'approbation accordée. Cette fonctionnalité est basée sur l'étendue de la séquence de tâches qui déploie le système d'exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l'ordinateur de destination, mais attend l'approbation d'un utilisateur administratif avant le déploiement du système d'exploitation.  

       -   Spécifiez **Ne pas autoriser d'affinité entre périphérique et utilisateur** si vous ne souhaitez pas que le média associe des utilisateurs à l'ordinateur de destination. Dans ce scénario, la séquence de tâches n'associe pas d'utilisateurs à l'ordinateur de destination lorsqu'elle déploie le système d'exploitation.  

8. Sur la page **Séquence de tâches** , spécifiez la séquence de tâches Windows 8 que vous avez créée dans la section précédente.  

9. Sur la page **Image de démarrage** , spécifiez les informations suivantes et cliquez sur **Suivant**.  

    > [!IMPORTANT]  
    >  L'architecture de l'image de démarrage qui est distribuée doit être adaptée à l'architecture de l'ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86. Pour les ordinateurs certifiés Windows 8 en mode EFI, vous devez utiliser une image de démarrage x64.  

    -   **Image de démarrage** : Spécifiez l'image de démarrage pour démarrer l'ordinateur de destination.  

    -   **Point de distribution** : spécifiez le point de distribution qui héberge l'image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

        > [!NOTE]  
        >  L'utilisateur administratif doit posséder des droits d'accès en **Lecture** au contenu de l'image de démarrage sur le point de distribution. Pour plus d’informations, consultez [Compte d’accès au package](/sccm/core/plan-design/hierarchy/accounts#package-access-account).  

    -   Si vous avez sélectionné **Média basé sur le site** sur la page **Gestion du média** de l'Assistant, dans la zone **Point de gestion** , spécifiez un point de gestion à partir d'un site principal.  

    -   Si vous avez sélectionné **Média dynamique** sur la page **Gestion du média** de l'Assistant, dans la zone **Points de gestion associés** , spécifiez les points de gestion de site principal à utiliser et un ordre de priorité pour les communications initiales.  

10. Sur la page **Images** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Package d’images** : spécifiez le package qui contient l’image du système d’exploitation Windows 8.  

    -   **Index d’images** : spécifiez l'image à déployer si le package contient plusieurs images de système d'exploitation.  

    -   **Point de distribution** : spécifiez le point de distribution qui héberge le package de l'image du système d'exploitation. L'Assistant extrait l'image du système d'exploitation à partir du point de distribution et l'écrit sur le média.  

        > [!NOTE]  
        >  L'utilisateur administratif doit posséder des droits d'accès en **Lecture** au contenu de l'image du système d'exploitation sur le point de distribution. Pour plus d’informations, consultez [Compte d’accès au package](/sccm/core/plan-design/hierarchy/accounts#package-access-account).  

11. Sur la page **Sélectionner une application** , sélectionnez le contenu d'application à inclure dans le fichier du média, puis cliquez sur **Suivant**.  

12. Sur la page **Sélectionner le package** , sélectionnez le contenu de package supplémentaire à inclure dans le fichier du média, puis cliquez sur **Suivant**.  

13. Sur la page **Sélectionner le package de pilotes** , sélectionnez le contenu du package de pilotes à inclure dans le fichier du média, puis cliquez sur **Suivant**.  

14. Sur la page **Points de distribution** , sélectionnez un ou plusieurs points de distribution comprenant le contenu requis par la séquence de tâches, puis cliquez sur **Suivant**.  

15. Sur la page **Personnalisation** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    - **Variables** : Spécifiez les variables que la séquence de tâches utilise pour déployer le système d'exploitation. Pour Windows To Go, utilisez la variable SMSTSPreferredAdvertID pour sélectionner automatiquement le déploiement de Windows To Go à l'aide du format suivant :  

       SMSTSPreferredAdvertID = {*DeploymentID*}, où DeploymentID correspond à l'ID de déploiement associé à la séquence de tâches que vous allez utiliser pour exécuter le processus de préparation du lecteur Windows To Go.  

      > [!TIP]  
      >  Lorsque vous utilisez cette variable avec une séquence de tâches définie pour s'exécuter sans assistance (définie plus tôt au cours de cette procédure), aucune interaction utilisateur n'est requise et l'ordinateur démarre automatiquement le déploiement de Windows To Go lorsqu'il détecte un lecteur Windows To Go. L'utilisateur est quand même invité à fournir un mot de passe si le média est configuré avec une protection par mot de passe.  

    - **Commandes de prédémarrage** : Spécifiez les commandes de prédémarrage que vous voulez exécuter avant l'exécution de la séquence de tâches. Les commandes de prédémarrage peuvent être un script ou un exécutable capable d'interagir avec l'utilisateur dans Windows PE avant que la séquence de tâches s'exécute pour installer le système d'exploitation. Configurez les éléments suivants pour le déploiement de Windows To Go :  

      - **OSDBitLockerPIN** : BitLocker pour Windows To Go nécessite une phrase secrète. Définissez la variable **OSDBitLockerPIN** dans le cadre d'une commande de prédémarrage pour définir la phrase secrète BitLocker pour le lecteur Windows To Go.  

        > [!WARNING]  
        >  Une fois que BitLocker est activé pour la phrase secrète, l'utilisateur doit entrer cette phrase secrète chaque fois que l'ordinateur démarre sur le lecteur Windows To Go.  

      - **SMSTSUDAUsers** : Spécifie l'utilisateur principal de l'ordinateur de destination. Utilisez cette variable pour collecter le nom d'utilisateur, lequel peut ensuite être utilisé pour associer l'utilisateur et le périphérique. Pour plus d’informations, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).  

        > [!TIP]  
        >  Pour extraire le nom d'utilisateur, vous pouvez créer une zone de saisie dans le cadre d'une commande de prédémarrage, inviter l'utilisateur à entrer son nom d'utilisateur, puis affecter la valeur à la variable. Par exemple, vous pouvez ajouter les lignes suivantes au fichier de script de la commande de prédémarrage :  
        >   
        >  `UserID = inputbox("Enter Username" ,"Enter your username:","",400,0)`  
        >   
        >  `env("SMSTSUDAUsers") = UserID`  

        Pour plus d’informations sur la manière de créer un fichier de script à utiliser en tant que commande de prédémarrage, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](../understand/prestart-commands-for-task-sequence-media.md).  

16. Effectuez toutes les étapes de l'Assistant.  

    > [!NOTE]  
    >  La création du fichier de média préparé par l'Assistant peut être un processus très long.  

###  <a name="BKMK_CreatePackage"></a> Créer un package Windows To Go Creator  
 Dans le cadre du déploiement de Windows To Go, vous devez créer un package pour déployer le fichier de média préparé. Le package doit inclure l'outil qui configure le lecteur Windows To Go et extrait le média préparé vers le lecteur. Appliquez la procédure suivante pour créer le package Windows To Go Creator.  

#### <a name="to-create-the-windows-to-go-creator-package"></a>Pour créer le package Windows To Go Creator  

1. Sur le serveur qui doit héberger les fichiers du package Windows To Go Creator, créez un dossier source pour les fichiers sources du package.  

   > [!NOTE]  
   >  Le compte d'ordinateur du serveur de site doit disposer de droits d'accès en **Lecture** sur le dossier source.  

2. Copiez le fichier du média préparé que vous avez créé dans la section [Create prestaged media](#BKMK_CreatePrestagedMedia) vers le dossier source du package.  

3. Copiez l'outil Windows To Go Creator (WTGCreator.exe) vers le dossier source du package. L’outil Creator est disponible sur n’importe quel serveur de site principal à l’emplacement suivant : <*dossier_installation_Configuration_Manager*>\OSD\Tools\WTG\Creator.  

4. Créez un package et un programme à l'aide de l'Assistant Création d'un package et d'un programme.  

5. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

6. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Gestion d'applications**, puis cliquez sur **Packages**.  

7. Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer le package**.  

8. Sur la page **Package** , spécifiez le nom et la description du package. Par exemple, entrez **Windows To Go** comme nom de package et spécifiez **Package to configure a Windows To Go drive using System Center Configuration Manager** comme description de package.  

9. Sélectionnez **Ce package contient des fichiers sources**, spécifiez le chemin d'accès au dossier source du package que vous avez créé à l'étape 1, puis cliquez sur **Suivant**.  

10. Sur la page **Type de programme** , sélectionnez **Programme standard**, puis cliquez sur **Suivant**.  

11. Sur la page **Programme standard** , spécifiez les informations suivantes :  

    -   **Nom** : spécifiez le nom du programme. Par exemple, tapez **Creator** comme nom de programme.  

    -   **Ligne de commande** : tapez **WTGCreator.exe /wim:PrestageName.wim**, où PrestageName correspond au nom du fichier préparé que vous avez créé et copié vers le dossier source du package pour le package Windows To Go Creator.  

         Éventuellement, vous pouvez ajouter les options suivantes :  

        -   **enableBootRedirect**: option de ligne de commande pour modifier les options de démarrage Windows To Go pour autoriser la redirection de démarrage. Lorsque vous utilisez cette option, l'ordinateur démarre à partir du lecteur USB sans avoir à modifier l'ordre de démarrage dans le microprogramme de l'ordinateur ni à inviter l'utilisateur à sélectionner une option de démarrage dans une liste au moment du démarrage. Si un lecteur Windows To Go est détecté, l'ordinateur démarre sur ce lecteur.  

    -   **Exécuter**: spécifiez **Normal** pour exécuter le programme en fonction des paramètres par défaut du système et du programme.  

    -   **Le programme peut s’exécuter** : spécifiez si le programme peut s'exécuter uniquement lorsqu'un utilisateur est connecté.  

    -   **Mode d’exécution** : spécifiez si le programme s'exécute avec les autorisations d'utilisateurs connectés ou les autorisations administratives. Windows To Go Creator requiert des autorisations avec élévation de privilèges pour s'exécuter.  

    -   Sélectionnez **Permettre aux utilisateurs d'afficher et d'interagir avec l'installation du programme**, puis cliquez sur **Suivant**.  

12. Sur la page Spécifications, spécifiez les informations suivantes :  

    - **Exigences de plateformes** : sélectionnez les plateformes Windows 8 applicables pour permettre la préparation.  

    - **Espace disque estimé** : spécifiez la taille du dossier source du package pour Windows To Go Creator.  

    - **Durée maximale d’exécution allouée (en minutes)** : spécifie la durée maximale d'exécution du programme sur l'ordinateur client. Par défaut, cette valeur est définie à 120 minutes.  

      > [!IMPORTANT]  
      >  Si vous utilisez des fenêtres de maintenance pour le regroupement sur lequel ce programme est exécuté, un conflit peut survenir si la **Durée maximale d'exécution allouée** est supérieure à la fenêtre de maintenance programmée. Si la durée d'exécution maximale est définie sur **Inconnu**, il démarre pendant la fenêtre de maintenance mais continue son exécution jusqu'à ce qu'il ait terminé ou échoué après la fermeture de la fenêtre de maintenance. Si vous définissez la durée d'exécution maximale sur une période donnée (pas sur Inconnu) qui dépasse la durée de toute fenêtre de maintenance disponible, ce programme n'est pas exécuté.  

      > [!NOTE]  
      >  Si la valeur définie est **Inconnu**, Configuration Manager fixe la durée d’exécution maximale autorisée à 12 heures (720 minutes).  

      > [!NOTE]  
      >  Si cette durée d’exécution maximale (qu’elle soit définie par l’utilisateur ou par défaut) est dépassée, Configuration Manager arrête le programme si **Exécuter avec les droits d’administration** est sélectionné et si **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme** n’est pas sélectionné sur la page **Programme standard**.  

      Cliquez sur **Suivant** pour terminer l'Assistant.  

###  <a name="BKMK_UpdateTaskSequence"></a> Mettre à jour la séquence de tâches pour activer BitLocker pour Windows To Go  
 Windows To Go active BitLocker sur un lecteur externe démarrable sans utiliser le Module de plateforme sécurisée (TPM). Par conséquent, vous devez utiliser un outil distinct pour configurer BitLocker sur le lecteur Windows To Go. Pour activer BitLocker, vous devez ajouter une action à la séquence de tâches après l'étape **Configurer Windows et ConfigMgr** .  

> [!NOTE]  
>  BitLocker pour Windows To Go nécessite une phrase secrète. À l'étape [Create prestaged media](#BKMK_CreatePrestagedMedia) , vous avez défini la phrase secrète dans le cadre d'une commande de prédémarrage à l'aide de la variable OSDBitLockerPIN.  

 Appliquez la procédure suivante pour mettre à jour la séquence de tâches Windows 8 pour activer BitLocker pour Windows To Go.  

#### <a name="to-update-the-windows-8-task-sequence-to-enable-bitlocker"></a>Pour mettre à jour la séquence de tâches Windows 8 pour activer BitLocker  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Gestion d'applications**, puis cliquez sur **Packages**.  

3.  Sous l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer le package**.  

4.  Sur la page **Package** , spécifiez le nom et la description du package. Par exemple, tapez **BitLocker for Windows To Go** comme nom de package et spécifiez **Package to update BitLocker for Windows To Go** comme description de package.  

5.  Sélectionnez **Ce package contient des fichiers sources**, spécifiez l'emplacement de l'outil BitLocker pour Windows To Go, puis cliquez sur **Suivant**. L’outil BitLocker est disponible sur n’importe quel serveur de site principal Configuration Manager à l’emplacement suivant : <*dossier_installation_Configuration_Manager*>\OSD\Tools\WTG\BitLocker\  

6.  Sur la page **Type de programme** , sélectionnez **Ne pas créer de programme**.  

7.  Cliquez sur **Suivant** pour terminer l'Assistant.  

8.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

9. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

10. Sélectionnez la séquence de tâches de Windows 8 que vous référencez dans les médias préparés.  

11. Sous l'onglet **Accueil** , dans le groupe **Séquence de tâches** , cliquez sur **Modifier**.  

12. Cliquez sur l'étape **Configurer Windows et ConfigMgr** , cliquez sur **Ajouter**, cliquez sur **Général**, puis sur **Exécuter la ligne de commande**. L'étape Exécuter la ligne de commande est ajoutée après l'étape Configurer Windows et ConfigMgr.  

13. Sous l'onglet **Propriétés** de l'étape **Exécuter la ligne de commande** , ajoutez les éléments suivants :  

    1.  **Nom** : spécifiez un nom pour la ligne de commande, par exemple, **activer BitLocker pour Windows To Go**.  

    2.  **Ligne de commande** : i386\osdbitlocker_wtg.exe /Enable /pwd:< *None&#124;AD*>  

         Paramètres :  

        -   /pwd:<None&#124;AD> : spécifiez le mode de récupération de mot de passe BitLocker. Ce paramètre est requis si vous utilisez le paramètre /Enable dans la ligne de commande.  

             Sélectionnez **AD** pour configurer le chiffrement de lecteur BitLocker pour la sauvegarde des informations de récupération des lecteurs protégés par BitLocker sur les services de domaine Active Directory (AD DS). La sauvegarde des mots de passe de récupération d'un lecteur protégé par BitLocker permet aux utilisateurs administratifs de récupérer le lecteur s'il est verrouillé. Ainsi, les utilisateurs autorisés peuvent toujours accéder aux données chiffrées appartenant à l'entreprise. Lorsque vous spécifiez **Aucun**, l'utilisateur est responsable de la conservation d'une copie du mot de passe de récupération ou de la clé de récupération. Si l'utilisateur perd ces informations ou omet de déchiffrer le lecteur avant de quitter l'organisation, les utilisateurs administratifs ne peuvent pas accéder facilement au lecteur.  

        -   /wait:<TRUE&#124;FALSE> : indiquez si la séquence de tâches attend la fin du chiffrement avant de se terminer.  

    3.  Sélectionnez **Package**, puis définissez le package que vous avez créé au début de cette procédure.  

    4.  Sous l'onglet **Options** , spécifiez les conditions suivantes :  

        -   Condition = Variable de séquence de tâches  

        -   Variable = _SMSTSWTG  

        -   Condition = Égal à  

        -   Valeur = True  

    > [!NOTE]  
    >  L'étape **Activer BitLocker** , susceptible d'intervenir après la nouvelle étape de ligne de commande, n'est pas utilisée pour activer BitLocker pour Windows To Go. Toutefois, vous pouvez conserver cette étape dans la séquence de tâches et l'utiliser pour les déploiements de Windows 8 qui n'utilisent pas un lecteur Windows To Go.  

###  <a name="BKMK_Deployments"></a> Déployer le package Windows To Go Creator et la séquence de tâches  
 Windows To Go est un processus de déploiement hybride. Par conséquent, vous devez déployer le package Windows To Go Creator et la séquence de tâches Windows 8. Utilisez les procédures suivantes pour terminer le processus de déploiement.  

#### <a name="to-deploy-the-windows-to-go-creator-package"></a>Pour déployer le package Windows To Go Creator  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Gestion d'applications**, puis cliquez sur **Packages**.  

3.  Sélectionnez le package Windows To Go que vous avez créé à l'étape [Créer un package Windows To Go Creator](#BKMK_CreatePackage) .  

4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

5.  Sur la page **Général** , spécifiez les paramètres suivants :  

    1.  **Logiciels** : vérifiez que le package Windows To Go est sélectionné.  

    2.  **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement vers lequel vous voulez déployer le package Windows To Go.  

    3.  **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** : sélectionnez cette option si vous voulez stocker le contenu du package sur le groupe de points de distribution par défaut du regroupement. Si vous n'avez pas associé le regroupement sélectionné à un groupe de points de distribution, cette option ne sera pas disponible.  

6.  Sur la page **Contenu** , cliquez sur **Ajouter** , puis sélectionnez les points de distribution ou les groupes de points de distribution vers lesquels le contenu associé à ce package et ce programme doit être déployé.  

7.  Sur la page **Paramètres de déploiement** , sélectionnez **Disponible** pour le type de déploiement, puis cliquez sur **Suivant**.  

8.  Sur la page **Planification**, configurez l'heure à laquelle ce package et ce programme seront déployés ou mis à disposition des périphériques clients.  

     Les options de cette page pourront différer selon si l'action de déploiement est définie sur **Disponible** ou sur **Obligatoire**.  

9. Sur la page **Planification**, configurez les paramètres suivants, puis cliquez sur **Suivant**.  

    1.  **Planifier la disponibilité de ce déploiement** : spécifiez la date et l'heure auxquelles le package et le programme sont disponibles pour s'exécuter sur l'ordinateur de destination. Lorsque vous sélectionnez **UTC**, ce paramètre s'assure que le package et le programme sont disponibles pour plusieurs ordinateurs de destination en même temps plutôt qu'à des heures différentes, en fonction de l'heure locale sur les ordinateurs de destination.  

    2.  **Planifier la date d’expiration de ce déploiement** : spécifiez la date et l'heure d'expiration du package et du programme sur l'ordinateur de destination. Lorsque vous sélectionnez **UTC**, ce paramètre s'assure que la séquence de tâches expire sur plusieurs ordinateurs de destination en même temps plutôt qu'à des heures différentes, en fonction de l'heure locale sur les ordinateurs de destination.  

10. Sur la page **Expérience utilisateur** de l'Assistant, spécifiez les informations suivantes :  

    -   **Installation du logiciel** : permet au logiciel d'être installé en dehors de toute fenêtre de maintenance configurée.  

    -   **Redémarrage du système (si nécessaire pour terminer l’installation)** : permet à un périphérique de redémarrer en dehors des fenêtres de maintenance configurées lorsque requis par l'installation du logiciel.  

    -   **Appareils Windows Embedded** : Lorsque vous déployez des packages et des programmes sur des périphériques Windows Embedded dont le filtre d'écriture est activé, vous pouvez choisir d'installer les packages et les programmes sur un segment de recouvrement temporaire puis de valider les modifications ultérieurement, ou de valider les modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

11. Sur la page **Points de distribution** , spécifiez les informations suivantes :  

    -   **Options de déploiement :** spécifiez **Télécharger le contenu à partir du point de distribution et l’exécuter localement**.  

    -   **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau** : sélectionnez cette option pour réduire la charge sur le réseau en permettant aux clients de télécharger du contenu à partir d'autres clients sur le réseau qui ont déjà téléchargé et mis en cache le contenu. Cette option utilise Windows BranchCache et peut être utilisée sur des ordinateurs exécutant Windows Vista SP2 et versions ultérieures.  

    -   **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** : spécifiez si les clients sont autorisés à revenir et à utiliser un point de distribution non préféré en tant qu'emplacement source de contenu lorsque le contenu n'est pas disponible sur un point de distribution préféré.  

12. Effectuez toutes les étapes de l'Assistant.  

#### <a name="to-deploy-the-windows-8-task-sequence"></a>Pour déployer la séquence de tâches de Windows 8  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Sélectionnez la séquence de tâche Windows 8 que vous avez créée à l'étape [Prerequisites to provision Windows To Go](#BKMK_Prereqs) .  

4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Déployer**.  

5.  Sur la page **Général** , spécifiez les paramètres suivants :  

    1.  **Séquence de tâches** : vérifiez que la séquence de tâches de Windows 8 est sélectionnée.  

    2.  **Regroupement** : cliquez sur **Parcourir** pour sélectionner le regroupement qui contient tous les appareils pour lesquels un utilisateur peut préparer Windows To Go.  

        > [!IMPORTANT]  
        >  Si le média préparé que vous avez créé dans dans la section [Créer un média préparé](#BKMK_CreatePrestagedMedia) utilise la variable SMSTSPreferredAdvertID, vous pouvez déployer la séquence de tâches sur le regroupement **Tous les systèmes** et définir le paramètre **Windows PE uniquement (masqué)** sur la page **Contenu** . La séquence de tâches étant masquée, elle ne sera disponible que pour le média.  

    3.  **Utiliser des groupes de points de distribution par défaut associés à ce regroupement** : sélectionnez cette option si vous voulez stocker le contenu du package sur le groupe de points de distribution par défaut du regroupement. Si vous n'avez pas associé le regroupement sélectionné à un groupe de points de distribution, cette option ne sera pas disponible.  

6.  Sur la page **Paramètres de déploiement** , configurez les paramètres suivants, puis cliquez sur **Suivant**.  

    -   **Fonction** : sélectionnez **Disponible**. Lorsque vous déployez la séquence de tâches sur un utilisateur, l'utilisateur peut voir la séquence de tâches publiée dans le catalogue des applications et il peut la demander au besoin. Si la séquence de tâches est déployée sur un périphérique, l'utilisateur pourra la voir dans le Centre logiciel et peut l'installer sur demande.  

    -   **Rendre disponible aux éléments suivants** : spécifiez si la séquence de tâches est disponible pour les clients Configuration Manager, les médias ou les environnements PXE.  

        > [!IMPORTANT]  
        >  Utilisez le paramètre **Média et environnement PXE uniquement (masqué)** pour les déploiements de séquence de tâches automatisés. Sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome** et définissez la variable SMSTSPreferredAdvertID à inclure dans le média préparé de sorte que l'ordinateur démarre automatiquement le déploiement de Windows To Go sans aucune interaction utilisateur lorsqu'il détecte un lecteur Windows To Go. Pour plus d'informations sur ces paramètres de média préparé, voir la section [Create prestaged media](#BKMK_CreatePrestagedMedia) .  

7.  Sur la page **Planification** , configurez les paramètres suivants, puis cliquez sur **Suivant**.  

    1.  **Planifier la disponibilité de ce déploiement** : spécifiez la date et l'heure auxquelles la séquence de tâches est disponible pour s'exécuter sur l'ordinateur de destination. Lorsque vous sélectionnez **UTC**, ce paramètre s'assure que la séquence de tâches est disponible pour plusieurs ordinateurs de destination en même temps plutôt qu'à des heures différentes, en fonction de l'heure locale sur les ordinateurs de destination.  

    2.  **Planifier la date d’expiration de ce déploiement** : spécifiez la date et l'heure d'expiration de la séquence de tâches sur l'ordinateur de destination. Lorsque vous sélectionnez **UTC**, ce paramètre s'assure que la séquence de tâches expire sur plusieurs ordinateurs de destination en même temps plutôt qu'à des heures différentes, en fonction de l'heure locale sur les ordinateurs de destination.  

8.  Sur la page **Expérience utilisateur** , spécifiez les informations suivantes :  

    -   **Afficher la progression de la séquence de tâches** : Spécifiez si le client Configuration Manager affiche la progression de la séquence de tâches.  

    -   **Installation du logiciel** : spécifiez si l'utilisateur est autorisé à installer le logiciel en dehors de fenêtres de maintenance configurées après l'heure prévue.  

    -   **Redémarrage du système (si nécessaire pour terminer l’installation)** : permet à un périphérique de redémarrer en dehors des fenêtres de maintenance configurées lorsque requis par l'installation du logiciel.  

    -   **Appareils Windows Embedded** : Lorsque vous déployez des packages et des programmes sur des périphériques Windows Embedded dont le filtre d'écriture est activé, vous pouvez choisir d'installer les packages et les programmes sur un segment de recouvrement temporaire puis de valider les modifications ultérieurement, ou de valider les modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance. Lorsque vous validez des modifications à l'échéance de l'installation ou au cours d'une fenêtre de maintenance, un redémarrage est requis et les modifications sont conservées sur l'appareil.  

    -   **Clients basés sur Internet** : spécifiez si la séquence de tâches est autorisée à s'exécuter sur un client basé sur Internet. Les opérations qui installent le logiciel, tel qu'un système d'exploitation, ne sont pas prises en charge avec ce paramètre. Utilisez cette option uniquement pour les séquences de tâches basées sur des scripts génériques qui effectuent des opérations dans le système d'exploitation standard.  

9. Sur la page **Alertes** , spécifiez les paramètres d'alerte que vous souhaitez pour ce déploiement de séquence de tâches, puis cliquez sur **Suivant**.  

10. Sur la page **Points de distribution** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Options de déploiement** : sélectionnez **Télécharger le contenu localement si nécessaire, en exécutant la séquence de tâches**.  

    -   **Lorsqu’aucun point de distribution local n’est disponible, utilisez un point de distribution distant** : spécifiez si les clients peuvent utiliser les points de distribution qui se trouvent sur des réseaux lents et peu fiables pour télécharger le contenu requis par la séquence de tâches.  

    -   **Autoriser les clients à utiliser un emplacement source de secours pour le contenu** :
        - *Avant la version 1610*, vous pouviez cocher la case Autoriser un emplacement source de secours pour le contenu pour permettre aux clients situés en dehors de ces groupes de limites d’avoir recours au point de distribution comme emplacement source pour le contenu quand aucun autre point de distribution n’est disponible.
        - *À partir de la version 1610*, vous ne pouvez plus configurer l’option **Autoriser un emplacement source de secours pour le contenu**.  Au lieu de cela, vous configurez des relations entre les groupes de limites qui déterminent quand un client peut commencer à rechercher un emplacement source de contenu valide dans d’autres groupes de limites. 

11. Effectuez toutes les étapes de l'Assistant.  

###  <a name="BKMK_UserExperience"></a> L’utilisateur exécute Windows To Go Creator  
 Suite au déploiement du package Windows To Go et de la séquence de tâches de Windows 8, Windows To Go Creator est disponible pour l'utilisateur. L'utilisateur peut accéder au catalogue de logiciels ou au centre logiciel si Windows To Go Creator a été déployé sur les périphériques et exécute le programme Windows To Go Creator. Une fois le package Creator téléchargé, une icône clignotante s'affiche dans la barre des tâches. Lorsque l'utilisateur clique sur cette icône, une boîte de dialogue s'affiche et permet à l'utilisateur de sélectionner le lecteur Windows To Go à préparer (sauf si l'option de ligne de commande /drive est utilisée). Si le lecteur n'est pas conforme à la configuration requise pour Windows To Go ou si l'espace disque disponible est insuffisant pour installer l'image, le programme Creator affiche un message d'erreur. L'utilisateur peut vérifier le lecteur et l'image qui sera appliquée à partir de la page de confirmation. Lorsque Creator configure et prépare un contenu pour le lecteur Windows To Go, une boîte de dialogue indique la progression. Une fois la préparation terminée, Creator vous invite à redémarrer l'ordinateur pour démarrer sur le lecteur Windows Go To.  

> [!NOTE]  
>  Si vous n'avez pas activé la redirection de démarrage dans le cadre de la ligne de commande du programme Creator dans la section [Create a Windows To Go Creator package](#BKMK_CreatePackage) , l'utilisateur devra peut-être effectuer manuellement le démarrage sur le lecteur Windows To Go à chaque redémarrage du système.  

###  <a name="BKMK_ConfigureStageDrive"></a> Configuration Manager configure et prépare le lecteur Windows To Go  
 Après le redémarrage de l'ordinateur sur le lecteur Windows To Go, le lecteur démarre dans Windows PE et se connecte au point de gestion pour obtenir la stratégie de finalisation du déploiement du système d'exploitation. Configuration Manager configure et prépare le lecteur. Après la préparation du lecteur par Configuration Manager, l’utilisateur peut redémarrer l’ordinateur pour finaliser le processus de mise en service (par exemple, joindre un domaine ou installer des applications). Ce processus est le même pour tous les médias préparés.  

###  <a name="BKMK_UserLogsIn"></a> L’utilisateur ouvre une session Windows 8  
 Lorsque Configuration Manager termine le processus de mise en service et que l’écran de verrouillage Windows 8 s’affiche, l’utilisateur peut ouvrir une session sur le système d’exploitation.  
