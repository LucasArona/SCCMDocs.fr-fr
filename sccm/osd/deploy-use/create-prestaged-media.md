---
title: Créer un média préparé
titleSuffix: Configuration Manager
description: Créer un média préparé dans System Center Configuration Manager pour simplifier le déploiement de Windows dans plusieurs scénarios.
ms.date: 04/11/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: ff6e7267-302a-4563-815e-cdc0d1a4b60f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 97c4bde7e589e5d3d3c3ee3683055ca8e7412a03
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419833"
---
# <a name="create-prestaged-media-with-system-center-configuration-manager"></a>Créer un média préparé avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Le média préparé dans System Center Configuration Manager est un fichier WIM (Windows Imaging Format) qui peut être installé sur un ordinateur nu par le fabricant ou dans un centre de reclassement d’entreprise qui n’est pas connecté à l’environnement Configuration Manager.  
Un média préparé contient l'image de démarrage utilisée pour démarrer l'ordinateur de destination et l'image du système d'exploitation qui est appliquée à l'ordinateur de destination. Vous pouvez aussi spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. La séquence de tâches qui déploie le système d'exploitation n'est pas incluse dans le média. Un média préparé est appliqué au disque dur d'un nouvel ordinateur avant que l'ordinateur soit envoyé à l'utilisateur final. Utilisez un média préparé pour les scénarios de déploiement de système d’exploitation suivants :  

- [Créer une image pour un fabricant OEM en usine ou dépôt local](../../osd/deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)  

- [Installation d’une nouvelle version de Windows sur un nouvel ordinateur (système nu)](install-new-windows-version-new-computer-bare-metal.md)  

- [Déployer Windows To Go](deploy-windows-to-go.md)  

  Quand l’ordinateur démarre pour la première fois après l’application du média préparé, il démarre Windows PE et se connecte à un point de gestion pour localiser la séquence de tâches qui finalise le processus de déploiement du système d’exploitation. Vous pouvez spécifier les applications, les packages et les packages de pilotes à inclure dans le média préparé. Lorsque vous déployez une séquence de tâches qui fait appel à un média préparé, l'Assistant vérifie tout d'abord que le contenu du cache local de la séquence de tâches est valide. Si ce contenu est introuvable ou a été modifié, l'Assistant télécharge le contenu auprès du point de distribution.  

##  <a name="BKMK_CreatePrestagedMedia"></a> Comment créer un média préparé  
 Avant de créer un média préparé à l’aide de l’Assistant Création d’un média de séquence de tâches, vérifiez que toutes les conditions suivantes sont remplies :  

|Tâche|Description|  
|----------|-----------------|  
|Image de démarrage|Prenez en considération les éléments suivants relatifs à l’image de démarrage que vous utiliserez dans la séquence de tâches pour déployer le système d’exploitation :<br /><br /> -   L’architecture de l’image de démarrage doit être adaptée à l’architecture de l’ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.<br />-   Assurez-vous que l’image de démarrage contient les pilotes de stockage de masse et de réseau qui sont requis pour provisionner l’ordinateur de destination.|  
|Créer une séquence de tâches pour déployer un système d’exploitation|Dans le cadre du média préparé, vous devez spécifier la séquence de tâches destinée à déployer le système d’exploitation.<br /><br /> -   Pour connaître les étapes permettant de créer une séquence de tâches, voir [Créer une séquence de tâches pour installer un système d’exploitation](../../osd/deploy-use/create-a-task-sequence-to-install-an-operating-system.md).<br />-   Pour plus d’informations sur les séquences de tâches, voir [Gérer les séquences de tâches pour automatiser des tâches](../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).|  
|Distribuer tout le contenu associé à la séquence de tâches|Vous devez distribuer tout le contenu exigé par la séquence de tâches à au moins un point de distribution. Cela inclut l’image de démarrage, l’image du système d’exploitation et les autres fichiers associés. L'Assistant collecte les informations à partir du point de distribution lorsqu'il crée le média autonome. Vous devez disposer de droits d’accès en **Lecture** à la bibliothèque de contenu sur ce point de distribution.  Pour plus d’informations, voir [À propos de la bibliothèque de contenu](../../core/plan-design/hierarchy/the-content-library.md).|  
|Disque dur de l’ordinateur de destination|Le disque dur de l’ordinateur de destination doit être formaté avant que le support préparé soit préparé sur le disque dur de l’ordinateur. Si le disque dur n'est pas formaté lorsque le média est appliqué, la séquence de tâches qui déploie le système d'exploitation échouera lorsqu'elle tentera de démarrer l'ordinateur de destination.|  

> [!NOTE]  
>  L’Assistant Création d’un média de séquence de tâches définit la condition de variable de séquence de tâches suivante sur le média : **_SMSTSMediaType = OEMMedia**. Vous pouvez utiliser cette condition dans votre séquence de tâches.  

 Pour créer des médias préparés, appliquez la procédure suivante.  

#### <a name="to-create-prestaged-media"></a>Pour créer un média préparé  

1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Séquences de tâches**.  

3.  Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer un média de séquence de tâches** pour démarrer l'Assistant Création d'un média de séquence de tâches.  

4.  Sur la page **Sélectionner le type de média** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Sélectionnez **Média préparé**.  

    -   Éventuellement, si vous souhaitez autoriser le déploiement du système d'exploitation sans intervention de l'utilisateur, sélectionnez **Autoriser le déploiement du système d'exploitation de manière autonome**. Lorsque vous sélectionnez cette option, l'utilisateur n'est pas invité à fournir des informations de configuration réseau ou des séquences de tâches facultatives. Toutefois, l'utilisateur est toujours invité à fournir un mot de passe si le média est configuré avec la protection par mot de passe.  

5.  Sur la page **Gestion du média** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Sélectionnez **Média dynamique** si vous souhaitez autoriser un point de gestion à rediriger le média vers un autre point de gestion, basé sur l'emplacement du client dans les limites du site.  

    -   Sélectionnez **Média basé sur le site** si vous souhaitez que le média contacte uniquement le point de gestion spécifié.  

6.  Dans la page **Propriétés du média**  , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   **Créé par** : spécifiez qui a créé le média.  

    -   **Version** : spécifiez le numéro de version du média.  

    -   **Commentaire** : spécifiez une description unique de ce pour quoi le média est utilisé.  

    -   **Fichier multimédia** : spécifiez le nom et le chemin d'accès des fichiers de sortie. L'Assistant écrit les fichiers de sortie à cet emplacement. Par exemple : **\\\nomserveur\dossier\outputfile.wim**  

7.  Sur la page **Sécurité** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Cochez la case **Activer la prise en charge d'ordinateur inconnu** pour autoriser le média à déployer un système d'exploitation sur un ordinateur qui n'est pas géré par Configuration Manager. Il n'existe aucun enregistrement de ces ordinateurs dans la base de données Configuration Manager.  Pour plus d’informations, voir [Préparer les déploiements d’ordinateurs inconnus](../get-started/prepare-for-unknown-computer-deployments.md).  

    -   Activez la case à cocher **Protéger le média à l'aide d'un mot de passe** et entrez un mot de passe fort pour protéger le média contre les accès non autorisés. Lorsque vous spécifiez un mot de passe, l'utilisateur doit fournir ce mot de passe pour utiliser le média préparé.  

        > [!IMPORTANT]  
        >  Pour une sécurité optimale, il vous est conseillé de toujours attribuer un mot de passe pour protéger les médias préparés.  

    -   Pour les communications HTTP, sélectionnez **Créer un certificat de média auto-signé**, puis spécifiez les dates de début et d'expiration du certificat.  

    -   Pour les communications HTTPS, sélectionnez **Importer un certificat PKI**, puis spécifiez le certificat à importer et son mot de passe.  

         Pour plus d’informations sur ce certificat client utilisé pour les images de démarrage, consultez [Configuration requise des certificats PKI](../../core/plan-design/network/pki-certificate-requirements.md).  

    -   **Affinité entre utilisateur et périphérique** : Pour prendre en charge la gestion centrée sur l’utilisateur dans Configuration Manager, spécifiez la manière dont vous voulez que le média associe des utilisateurs à l’ordinateur de destination. Pour plus d’informations sur la prise en charge de l’affinité entre utilisateur et appareil par le déploiement de systèmes d’exploitation, consultez [Associer des utilisateurs à un ordinateur de destination](../get-started/associate-users-with-a-destination-computer.md).  

        -   Spécifiez **Autoriser une affinité entre périphérique et utilisateur avec approbation automatique** si vous voulez que le média associe automatiquement des utilisateurs à l'ordinateur de destination. Cette fonctionnalité est basée sur les actions de la séquence de tâches qui déploie le système d'exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l'ordinateur de destination lorsqu'elle déploie le système d'exploitation sur l'ordinateur de destination.  

        -   Spécifiez **Autoriser une affinité entre périphérique et utilisateur en attente de l'approbation de l'administrateur** si vous souhaitez que le média associe des utilisateurs à l'ordinateur de destination une fois l'approbation accordée. Cette fonctionnalité est basée sur l'étendue de la séquence de tâches qui déploie le système d'exploitation. Dans ce scénario, la séquence de tâches crée une relation entre les utilisateurs spécifiés et l'ordinateur de destination, mais attend l'approbation d'un utilisateur administratif avant le déploiement du système d'exploitation.  

        -   Spécifiez **Ne pas autoriser d'affinité entre périphérique et utilisateur** si vous ne souhaitez pas que le média associe des utilisateurs à l'ordinateur de destination. Dans ce scénario, la séquence de tâches n'associe pas d'utilisateurs à l'ordinateur de destination lorsqu'elle déploie le système d'exploitation.  

8.  Dans la page **Séquence de tâches** , spécifiez la séquence de tâches qui s’exécutera sur l’ordinateur de destination. Le contenu référencé par la séquence de tâches est affiché dans **Cette séquence de tâches fait référence au contenu suivant**. Vérifiez le contenu, puis cliquez sur **Suivant**.  

9. Sur la page **Image de démarrage** , spécifiez les informations suivantes et cliquez sur **Suivant**.  

    > [!IMPORTANT]  
    >  L'architecture de l'image de démarrage qui est distribuée doit être adaptée à l'architecture de l'ordinateur de destination. Par exemple, un ordinateur de destination x64 peut démarrer et exécuter une image de démarrage x86 ou x64. Toutefois, un ordinateur de destination x86 peut démarrer et exécuter uniquement une image de démarrage x86.  

    -   Dans la zone **Image de démarrage** , spécifiez l'image de démarrage pour démarrer l'ordinateur de destination. Pour plus d’informations, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

    -   Dans la zone **Point de distribution** , spécifiez le point de distribution où réside l'image de démarrage. L'Assistant extrait l'image de démarrage à partir du point de distribution et l'écrit sur le média.  

        > [!NOTE]  
        >  Vous devez disposer de droits d’accès en **lecture** à la bibliothèque de contenu sur le point de distribution. Pour plus d'informations, voir [À propos de la bibliothèque de contenu](../../core/plan-design/hierarchy/the-content-library.md).  

    -   Si vous avez sélectionné **Média basé sur le site** dans la page **Gestion du média** de l’Assistant, dans la zone **Point de gestion** , spécifiez un point de gestion à partir d’un site principal.  

    -   Si vous avez sélectionné **Média dynamique** dans la page **Gestion du média** de l’Assistant, dans la zone **Points de gestion associés** , spécifiez les points de gestion de site principal à utiliser et un ordre de priorité pour les communications initiales.  

10. Sur la page **Images** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Dans la zone **Package d’images** , spécifiez l’image du système d’exploitation. Pour plus d’informations, voir [Gérer les images de système d’exploitation](../get-started/manage-operating-system-images.md).  

    -   Si le package contient plusieurs images du système d'exploitation, dans la zone **Index d'images** , spécifiez l'image à déployer.  

    -   Dans la zone **Point de distribution** , spécifiez le point de distribution où réside le package d'images du système d'exploitation. L'Assistant extrait l'image du système d'exploitation à partir du point de distribution et l'écrit sur le média.  

11. Sur la page **Personnalisation** , spécifiez les informations suivantes, puis cliquez sur **Suivant**.  

    -   Spécifiez les variables que la séquence de tâches utilise pour déployer le système d'exploitation.  

    -   Spécifiez les commandes de prédémarrage que vous voulez exécuter avant l'exécution de la séquence de tâches. Les commandes de prédémarrage sont un script ou un exécutable qui peut interagir avec l'utilisateur dans Windows PE avant que la séquence de tâches s'exécute pour installer le système d'exploitation. Pour plus d’informations sur les commandes de prédémarrage pour les médias, voir [Commandes de prédémarrage pour les médias de séquence de tâches](../understand/prestart-commands-for-task-sequence-media.md).  

        > [!TIP]  
        >  Lors de la création du média de séquence de tâches, la séquence de tâches écrit l’ID du package et la ligne de commande de prédémarrage, y compris la valeur des variables de la séquence de tâches, dans le fichier journal CreateTSMedia.log sur l’ordinateur qui exécute la console Configuration Manager. Vous pouvez consulter ce fichier journal pour vérifier la valeur des variables de séquence de tâches.  

12. Effectuez toutes les étapes de l'Assistant.  

## <a name="next-steps"></a>Étapes suivantes
[Scénarios de déploiement de systèmes d’exploitation d’entreprise](scenarios-to-deploy-enterprise-operating-systems.md)
