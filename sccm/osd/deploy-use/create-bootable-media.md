---
title: Créer un média de démarrage
titleSuffix: Configuration Manager
description: Un média de démarrage dans Configuration Manager facilite l’installation d’une nouvelle version de Windows ou le remplacement d’un ordinateur et le transfert de paramètres.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f26dd2928bac3c2dd60da35473a92e7dc36adb53
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53420479"
---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>Créer un média de démarrage avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Un média de démarrage dans Configuration Manager contient l’image de démarrage, des commandes de prédémarrage facultatives et leurs fichiers associés, ainsi que les fichiers de Configuration Manager. Utilisez un média préparé pour les scénarios de déploiement de système d’exploitation suivants :  

-   [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

-   [Remplacement d’un ordinateur existant et transfert des paramètres](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="BKMK_CreateBootableMedia"></a> Créer un média de démarrage  
 Quand vous démarrez sur le média de démarrage, l’ordinateur de destination démarre, se connecte au réseau, puis récupère la séquence de tâches, l’image du système d’exploitation et tout autre contenu nécessaire à partir du réseau. Étant donné que la séquence de tâches ne se trouve pas sur le média, vous pouvez modifier la séquence de tâches ou le contenu sans avoir à recréer le média. Les packages sur le média de démarrage ne sont pas chiffrés. Vous devez prendre les mesures de sécurité appropriées, telles que l’ajout d’un mot de passe au média, afin de garantir que le contenu du package est protégé contre les utilisateurs non autorisés.  

 Avant de créer un média de démarrage à l’aide de l’Assistant Création d’un média de séquence de tâches, vérifiez que toutes les conditions suivantes sont remplies :  

|Tâche|Description|  
|----------|-----------------|  
|Image de démarrage|Prenez en considération les éléments suivants relatifs à l’image de démarrage que vous utiliserez dans la séquence de tâches pour déployer le système d’exploitation :<br /><br /> -   L’architecture de l’image de démarrage doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.<br />-   Assurez-vous que l’image de démarrage contient les pilotes de stockage de masse et de réseau qui sont requis pour provisionner l’ordinateur de destination.|  
|Créer une séquence de tâches pour déployer un système d’exploitation|Dans le cadre du média de démarrage, vous devez spécifier la séquence de tâches destinée à déployer le système d’exploitation. Pour connaître les étapes permettant de créer une séquence de tâches, consultez [Créer une séquence de tâches pour installer un système d’exploitation](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md).|  
|Distribuer tout le contenu associé à la séquence de tâches|Vous devez distribuer tout le contenu exigé par la séquence de tâches à au moins un point de distribution. Sont inclus l’image de démarrage et les autres fichiers de prédémarrage associés. L’Assistant collecte les informations à partir du point de distribution quand il crée le média de démarrage. Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur ce point de distribution.  Pour plus d’informations, consultez [À propos de la bibliothèque de contenu](../../core/plan-design/hierarchy/the-content-library.md).|  
|Préparer le lecteur USB amovible|Pour un lecteur USB amovible :<br /><br /> Si vous envisagez d’utiliser un lecteur USB amovible, ce dernier doit être connecté à l’ordinateur sur lequel est exécuté l’Assistant et il doit être détectable par Windows en tant que périphérique amovible. L’Assistant écrit directement sur le lecteur USB quand il crée le média. Le média autonome utilise un système de fichiers FAT32. Vous ne pouvez pas créer de média autonome sur un disque mémoire flash USB dont le contenu inclut un fichier d'une taille supérieure à 4 Go.|  
|Créer un dossier de sortie|Pour un ensemble de CD/DVD :<br /><br /> Avant d'exécuter l'Assistant Création d'un média de séquence de tâches afin de créer un média pour un ensemble de CD ou DVD, vous devez créer un dossier pour les fichiers de sortie créés par l'Assistant. Le média créé pour un ensemble de CD ou DVD est écrit sous forme de fichiers .iso directement dans le dossier.|  

 Pour créer un média de démarrage, procédez comme suit.  

### <a name="to-create-bootable-media"></a>Pour créer un média de démarrage  

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4. Sur la page **Sélectionner le type de média** , spécifiez les options suivantes, puis cliquez sur **Suivant**.  

   -   Sélectionnez **Média de démarrage**.  

   -   Éventuellement, si vous souhaitez uniquement autoriser le déploiement du système d'exploitation sans intervention de l'utilisateur, sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome**.  

       > [!IMPORTANT]  
       >  Lorsque vous sélectionnez cette option, l'utilisateur n'est pas invité à fournir des informations de configuration réseau ou des séquences de tâches facultatives. Toutefois, l'utilisateur est toujours invité à fournir un mot de passe si le média est configuré avec la protection par mot de passe.  

5. Sur la page **Gestion du média** , spécifiez les options suivantes, puis cliquez sur **Suivant**.  

   -   Sélectionnez **Média dynamique** si vous souhaitez autoriser un point de gestion à rediriger le média vers un autre point de gestion, basé sur l'emplacement du client dans les limites du site.  

   -   Sélectionnez **Média basé sur le site** si vous souhaitez que le média contacte uniquement le point de gestion spécifié.  

6. Dans la page **Type de média** , spécifiez si le média est un disque mémoire flash ou un ensemble de CD/DVD, puis cliquez pour configurer les éléments suivants :  

   > [!IMPORTANT]  
   >  Le média autonome utilise un système de fichiers FAT32. Vous ne pouvez pas créer de média autonome sur un disque mémoire flash USB dont le contenu inclut un fichier d'une taille supérieure à 4 Go.  

   - Si vous sélectionnez **Périphérique flash USB**, spécifiez le lecteur sur lequel stocker le contenu.  

   - Si vous sélectionnez **Ensemble CD/DVD**, spécifiez la capacité du média et le nom et le chemin d'accès des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Par exemple : **\\\nom_serveur\dossier\fichier_sortie.iso**  

      Si la capacité du média est insuffisante pour stocker l’ensemble du contenu, plusieurs fichiers sont créés et vous devez stocker le contenu sur plusieurs CD ou DVD. Quand plusieurs médias sont nécessaires, Configuration Manager ajoute un numéro de séquence au nom de chaque fichier de sortie qu’il crée. De plus, si vous déployez une application en même temps que le système d’exploitation et que cette application ne peut pas tenir sur un seul média, Configuration Manager stocke l’application sur plusieurs médias. Quand le média autonome est exécuté, Configuration Manager invite l’utilisateur à insérer le média suivant sur lequel l’application est stockée.  

     > [!IMPORTANT]  
     >  Si vous sélectionnez une image .iso existante, l'Assistant Média de séquence de tâches supprime cette image du lecteur ou du partage dès lors que vous passez à la page suivante de l'Assistant. L'image existante est supprimée même si vous annulez ensuite l'Assistant.  

     Cliquez sur **Suivant**.  

7. Sur la page **Sécurité** , spécifiez les options suivantes, puis cliquez sur **Suivant**.  

   -   Cochez la case **Activer la prise en charge d’ordinateur inconnu** pour autoriser le média à déployer un système d’exploitation sur un ordinateur qui n’est pas géré par Configuration Manager. Il n’existe aucun enregistrement de ces ordinateurs dans la base de données Configuration Manager.  

        Les ordinateurs inconnus sont les suivants :  

       -   Un ordinateur sur lequel le client Configuration Manager n’est pas installé  

       -   Un ordinateur qui n’est pas importé dans Configuration Manager  

       -   Un ordinateur qui n’est pas détecté par Configuration Manager.  

   -   Activez la case à cocher **Protéger le média à l'aide d'un mot de passe** et entrez un mot de passe fort pour protéger le média contre les accès non autorisés. Lorsque vous spécifiez un mot de passe, l'utilisateur doit fournir ce mot de passe pour utiliser le média de démarrage.  

       > [!IMPORTANT]  
       >  Une bonne pratique de sécurité consiste à toujours attribuer un mot de passe pour contribuer à protéger les médias de démarrage.  

   -   Pour les communications HTTP, sélectionnez **Créer un certificat de média auto-signé**, puis spécifiez les dates de début et d'expiration du certificat.  

   -   Pour les communications HTTPS, sélectionnez **Importer un certificat PKI**, puis spécifiez le certificat à importer et son mot de passe.  

        Pour plus d’informations sur ce certificat client utilisé pour les images de démarrage, consultez [Configuration requise des certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

   -   **Affinité entre utilisateur et appareil** : Pour prendre en charge la gestion centrée sur l’utilisateur dans Configuration Manager, spécifiez la manière dont vous voulez que le média associe des utilisateurs à l’ordinateur de destination. Pour plus d’informations sur la prise en charge de l’affinité entre utilisateur et appareil par le déploiement de systèmes d’exploitation, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).  

       -   Spécifiez **Autoriser une affinité entre périphérique et utilisateur avec approbation automatique** si vous voulez que le média associe automatiquement des utilisateurs à l'ordinateur de destination. Cette fonctionnalité est basée sur les actions de la séquence de tâches qui déploie le système d'exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l'ordinateur de destination lorsqu'elle déploie le système d'exploitation sur l'ordinateur de destination.  

       -   Spécifiez **Autoriser une affinité entre périphérique et utilisateur en attente de l'approbation de l'administrateur** si vous souhaitez que le média associe des utilisateurs à l'ordinateur de destination une fois l'approbation accordée. Cette fonctionnalité est basée sur l'étendue de la séquence de tâches qui déploie le système d'exploitation.  Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l'ordinateur de destination, mais attend l'approbation d'un utilisateur administratif avant le déploiement du système d'exploitation.  

       -   Spécifiez **Ne pas autoriser d'affinité entre périphérique et utilisateur** si vous ne souhaitez pas que le média associe des utilisateurs à l'ordinateur de destination. Dans ce scénario, la séquence de tâches n'associe pas d'utilisateurs à l'ordinateur de destination lorsqu'elle déploie le système d'exploitation.  

8. Sur la page **Image de démarrage** , spécifiez les options suivantes et cliquez sur **Suivant**.  

   > [!IMPORTANT]  
   >  L'architecture de l'image de démarrage qui est distribuée doit être adaptée à l'architecture de l'ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.  

   -   Dans la zone **Image de démarrage** , spécifiez l'image de démarrage pour démarrer l'ordinateur de destination.  

   -   Dans la zone **Point de distribution** , spécifiez le point de distribution où réside l'image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

       > [!NOTE]  
       >  Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur le point de distribution.  

   -   Si vous créez un média de démarrage basé sur le site dans la page **Gestion du média** de l’Assistant, spécifiez un point de gestion à partir d’un site principal dans la zone **Point de gestion** .  

   -   Si vous créez un média de démarrage dynamique dans la page **Gestion du média** de l’Assistant, spécifiez les points de gestion de site principal à utiliser et un ordre de priorité pour les communications initiales dans **Points de gestion associés**.  

9. Sur la page **Personnalisation** , spécifiez les options suivantes et cliquez sur **Suivant**.  

    -   Spécifiez les variables que la séquence de tâches utilise pour déployer le système d'exploitation.  

    -   Spécifiez les commandes de prédémarrage que vous voulez exécuter avant l'exécution de la séquence de tâches. Les commandes de prédémarrage sont un script ou un exécutable qui peut interagir avec l'utilisateur dans Windows PE avant que la séquence de tâches s'exécute pour installer le système d'exploitation. Pour plus d’informations, consultez [Commandes de prédémarrage pour les médias de séquence de tâches](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Lors de la création du média de séquence de tâches, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des variables de la séquence de tâches, dans le fichier journal CreateTSMedia.log sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

         Si vous le souhaitez, activez la case à cocher **Fichiers pour la commande de prédémarrage** pour inclure tous les fichiers requis pour la commande de prédémarrage.  

10. Effectuez toutes les étapes de l'Assistant.  

## <a name="create-bootable-media-on-a-usb-drive-from-a-network-share"></a>Créer un média de démarrage sur un lecteur USB à partir d’un partage réseau
Les informations fournies dans cette section indiquent comment créer un média de démarrage sur un lecteur flash USB qui n’est pas connecté à l’ordinateur exécutant la console Configuration Manager. Pour créer le média de démarrage sur le lecteur USB, vous pouvez créer le média de démarrage de séquence de tâches, monter l’image ISO, puis transférer les fichiers de l’image ISO sur le lecteur USB.

1. [Créez le média de démarrage de séquence de tâches](#to-create-task-boobable-media). Dans la page **Type de média**, sélectionnez **Ensemble CD/DVD**. L’Assistant écrit les fichiers de sortie à l’emplacement que vous spécifiez. Par exemple : **\\\nom_serveur\dossier\fichier_sortie.iso**.  
2. Préparez le lecteur USB amovible. Le lecteur doit être formaté, vide et démarrable.
3. Montez l’image ISO à partir de l’emplacement du partage, puis transférez les fichiers de l’image ISO sur le lecteur USB.

## <a name="next-steps"></a>Étapes suivantes  
[Utiliser un média de démarrage pour déployer Windows sur le réseau](use-bootable-media-to-deploy-windows-over-the-network.md)  
