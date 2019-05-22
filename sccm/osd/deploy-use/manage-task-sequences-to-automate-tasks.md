---
title: Gérer les séquences de tâches
titleSuffix: Configuration Manager
description: Créez, modifiez, déployez, importez et exportez des séquences de tâches pour les gérer et automatiser les tâches dans votre environnement.
ms.date: 05/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a1f099f1-e9b5-4189-88b3-f53e3b4e4add
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: cbc76a4f2ada16edfbdc139aca77e6a43d3c4a8b
ms.sourcegitcommit: 2db6863c6740380478a4a8beb74f03b8178280ba
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65082934"
---
# <a name="manage-task-sequences-to-automate-tasks"></a>Gérer les séquences de tâches pour automatiser des tâches

*S’applique à : System Center Configuration Manager (Current Branch)*

Utilisez des séquences de tâches pour automatiser des étapes dans votre environnement Configuration Manager. Ces étapes peuvent déployer une image OS sur un ordinateur de destination, créer et capturer une image OS à partir d’un ensemble de fichiers d’installation du système d’exploitation, et capturer et restaurer des informations d’état utilisateur. Les séquences de tâches sont affichées dans la console Configuration Manager. Dans l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**. Le nœud **Séquences de tâches**, qui contient les sous-dossiers que vous créez, est répliqué dans toute la hiérarchie Configuration Manager. Pour plus d’informations sur la planification, consultez [Considérations relatives à la planification de l’automatisation des tâches](/sccm/osd/plan-design/planning-considerations-for-automating-tasks).  



## <a name="BKMK_CreateTaskSequence"></a> Créer des séquences de tâches  

Créez des séquences de tâches à l'aide de l'Assistant Création d'une séquence de tâches. Cet Assistant peut créer les types de séquences de tâches suivants :  

|Type de séquence de tâches|Informations complémentaires|  
|------------------------|----------------------|  
|[Séquence de tâches pour installer un système d’exploitation](create-a-task-sequence-to-install-an-operating-system.md)|Ce type de séquence de tâches crée les étapes d’installation d’un système d’exploitation. Il comporte également des options permettant de migrer des données utilisateur, d’inclure des mises à jour logicielles et d’installer des applications.|  
|[Séquence de tâches pour mettre à niveau un système d’exploitation](create-a-task-sequence-to-upgrade-an-operating-system.md)|Ce type de séquence de tâches crée les étapes de mise à niveau d’un système d’exploitation. Il comporte également des options permettant d’inclure des mises à jour logicielles et d’installer des applications.|  
|[Séquence de tâches pour capturer un système d’exploitation](create-a-task-sequence-to-capture-an-operating-system.md)|Ce type de séquence de tâches crée les étapes nécessaires pour générer et capturer un système d’exploitation à partir d’un ordinateur de référence. Vous pouvez inclure des mises à jour logicielles et installer des applications sur l’ordinateur de référence avant de capturer l’image.|  
|[Séquence de tâches pour capturer et restaurer l’état utilisateur](create-a-task-sequence-to-capture-and-restore-user-state.md)|Cette séquence de tâches fournit les étapes à ajouter à une séquence de tâches pour capturer et restaurer des données d’état utilisateur.|  
|[Séquence de tâches personnalisée](create-a-custom-task-sequence.md)|Ce type de séquence de tâches n’ajoute aucune étape à la séquence de tâches. Après l’avoir créée, modifiez-la et ajoutez des étapes.|  



## <a name="BKMK_ModifyTaskSequence"></a> Modifier  

Modifiez une séquence de tâches en ajoutant ou en supprimant des étapes et des groupes, ou en changeant l’ordre des étapes. Pour modifier une séquence de tâches existante, procédez comme suit :  

> [!IMPORTANT]  
> Quand vous modifiez une séquence de tâches qui a été créée à l’aide de l’Assistant Création d’une séquence de tâches, le nom de l’étape peut être l’action ou le type de l’étape. Par exemple, vous pouvez voir une étape appelée « Partitionner le disque 0 », qui désigne l’action d’une étape de type [Formater et partitionner le disque](/sccm/osd/understand/task-sequence-steps#BKMK_FormatandPartitionDisk). Toutes les étapes de la séquence de tâches sont documentées selon leur type, et pas nécessairement selon le nom de l’étape qui s’affiche dans l’éditeur.  

### <a name="process-to-edit-a-task-sequence"></a>Processus de modification d’une séquence de tâches  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous souhaitez modifier.  

3. Sous l’onglet **Accueil** du ruban, sélectionnez **Modifier** dans le groupe **Séquence de tâches**. Ensuite, effectuez l’une des opérations suivantes :  

    - Pour ajouter une étape de séquence de tâches, sélectionnez **Ajouter**, puis le type d’étape et l’étape à ajouter. Par exemple, pour ajouter l’étape [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine), sélectionnez **Ajouter**, **Général**, puis **Exécuter la ligne de commande**.  

    - Pour ajouter un groupe à la séquence de tâches, sélectionnez **Ajouter**, puis **Nouveau groupe**. Après avoir ajouté un groupe, vous pouvez ajouter des étapes au groupe.  

    - Pour changer l’ordre des étapes et des groupes dans la séquence de tâches, sélectionnez l’étape ou le groupe que vous souhaitez réorganiser, puis utilisez les icônes **Déplacer l’élément vers le haut** ou **Déplacer l’élément vers le bas**. Vous pouvez déplacer une seule étape ou un seul groupe à la fois.  

    - Pour supprimer une étape ou un groupe, sélectionnez l’étape ou le groupe, puis **Supprimer**.  

4. Sélectionnez **OK** pour enregistrer les modifications et fermer la fenêtre. Sélectionnez **Appliquer** pour enregistrer les modifications et laisser l’Éditeur de séquence de tâches ouvert.  

Pour obtenir une liste des étapes de séquence de tâches disponibles, consultez [Étapes de séquence de tâches](/sccm/osd/understand/task-sequence-steps).  



## <a name="bkmk_prop-general"></a>Configurer les propriétés du Centre logiciel

Appliquez la procédure suivante pour configurer les détails de la séquence de tâches affichés dans le Centre logiciel. Ces détails sont fournis uniquement à titre d’informations.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.  

2. Sélectionnez la séquence de tâches à modifier, puis **Propriétés**.  

3. Sous l’onglet **Général**, les paramètres suivants du Centre logiciel sont disponibles :  

    - **Redémarrage requis** : indique à l’utilisateur si un redémarrage est nécessaire lors de l’installation.  

    - **Taille du téléchargement (Mo)**  : spécifie le nombre de mégaoctets affichés dans le Centre logiciel pour la séquence de tâches.  

    - **Durée d’exécution estimée (minutes)**  : spécifie la durée d’exécution estimée, en minutes, affichée dans le Centre logiciel pour la séquence de tâches.  



## <a name="bkmk_prop-advanced"></a>Configurer des paramètres de séquence de tâches avancés

Utilisez la procédure suivante pour configurer le comportement de la séquence de tâches sur le client Configuration Manager.  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.  

2. Sélectionnez la séquence de tâches à modifier, puis **Propriétés**.  

3. L’onglet **Avancé** contient les paramètres suivants :  

    - **Exécuter d’abord un autre programme** : sélectionnez cette option pour exécuter un programme dans un autre package avant la séquence de tâches. Par défaut, cette case à cocher est désactivée. Il n’est pas nécessaire de déployer séparément le programme qui devra s’exécuter en premier.  

        > [!IMPORTANT]
        > Ce paramètre s’applique uniquement aux séquences de tâches qui s’exécutent dans le système d’exploitation complet. Si vous démarrez la séquence de tâches à l’aide d’un environnement PXE ou d’un média de démarrage, Configuration Manager ignore ce paramètre.  

        - **Package** : recherchez le package contenant le programme à exécuter avant cette séquence de tâches.  

        - **Programme** : sélectionnez le programme à exécuter avant cette séquence de tâches.  

        > [!NOTE]  
        > Si l’exécution du programme sélectionné échoue sur un client, la séquence de tâches n’est pas exécutée. Si le programme sélectionné s’exécute correctement, il n’est pas réexécuté, même si la séquence de tâches est réexécutée sur le même client.  

    - **Supprimer les notifications de séquence de tâches** : sélectionnez cette option pour masquer la notification toast **Un nouveau logiciel est disponible**. L’icône **Nouveau logiciel** reste visible dans la zone de notification du Centre logiciel. Par défaut, cette option est désactivée.  

    - **Désactiver cette séquence de tâches sur les ordinateurs sur lesquels elle est déployée** : si vous sélectionnez cette option, Configuration Manager désactive temporairement tous les déploiements contenant cette séquence de tâches. Il supprime également la séquence de tâches de la liste des déploiements exécutables disponibles. La séquence de tâches ne s’exécute pas tant qu’elle n’est pas activée. Par défaut, cette option est désactivée.  

    - **Temps d’exécution maximal autorisé** : indique la durée maximale en minutes d’exécution de la séquence de tâches sur l’ordinateur de destination. Utilisez un nombre entier égal ou supérieur à zéro. La valeur par défaut est de 120 minutes.  

        > [!IMPORTANT]  
        > Si des fenêtres de maintenance sont utilisées pour le regroupement sur lequel cette séquence de tâches est déployée et que le **Temps d’exécution maximal autorisé** est supérieur à la fenêtre de maintenance planifiée, un conflit risque de se produire. Si le temps d’exécution maximal est défini sur **0**, la séquence de tâches démarre pendant la fenêtre de maintenance. Elle continue de s’exécuter jusqu’à ce qu’elle ait terminé ou échoué après la fermeture de la fenêtre de maintenance. En conséquence, les séquences de tâches dont la durée d'exécution maximale est définie sur **0** peuvent s'exécuter après la fin de leurs fenêtres de maintenance. Si le temps d’exécution maximal est défini sur une période (autre que zéro) qui dépasse la durée d’une fenêtre de maintenance disponible, cette séquence de tâches n’est pas exécutée. Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).  

        Si la valeur définie est **0**, Configuration Manager fixe le temps d’exécution maximal autorisé à **12** heures (720 minutes) pour suivre la progression. Toutefois, la séquence de tâches démarre tant que la durée du compte à rebours ne dépasse pas la valeur de la fenêtre de maintenance.  

        > [!NOTE]  
        > Si l’option **Exécuter avec les droits d’administration** est définie, mais non l’option **Autoriser les utilisateurs à interagir avec ce programme**, Configuration Manager arrête la séquence de tâches lorsque le temps d’exécution maximal est atteint. Si la séquence de tâches proprement dite n’est pas arrêtée, Configuration Manager en cesse le monitoring dès que le temps d’exécution maximal autorisé est atteint.  

    - **Utiliser une image de démarrage** : utiliser l’image de démarrage sélectionnée lors de l’exécution de la séquence de tâches. Sélectionnez **Parcourir** pour sélectionner une autre image de démarrage. Désactivez cette option pour désactiver l’utilisation de l’image de démarrage sélectionnée lors de l’exécution de la séquence de tâches.  

    - **Cette séquence de tâches peut s’exécuter sur n’importe quelle plateforme** : si vous sélectionnez cette option, Configuration Manager ne vérifie pas le type de plateforme de l’ordinateur de destination lors de l’exécution de la séquence de tâches. Cette option est activée par défaut.  

    - **Cette séquence de tâches ne peut s’exécuter que sur les plateformes clientes spécifiées** : cette option spécifie sur quels processeurs, versions de système d’exploitation et Service Packs cette séquence de tâches peut s’exécuter. Lorsque vous sélectionnez cette option, sélectionnez au moins une plateforme dans la liste. Par défaut, aucune plate-forme n'est sélectionnée. Configuration Manager utilise ces informations pour identifier les ordinateurs de destination d'un regroupement qui reçoivent la séquence de tâches déployée.  

        > [!NOTE]  
        > Lorsque vous exécutez une séquence de tâches à partir d’un média de démarrage ou d’un environnement PXE, Configuration Manager ignore cette option. La séquence de tâches s’exécute comme si l’option **Ce programme peut s’exécuter sur n’importe quelle plateforme** était sélectionnée.  



## <a name="configure-high-impact-task-sequence-settings"></a>Configurer des paramètres de séquence de tâches à fort impact

Configurez une séquence de tâches à fort impact et personnalisez les messages envoyés aux utilisateurs qui exécutent la séquence de tâches.


### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Définir une séquence de tâches comme séquence de tâches à fort impact

Appliquez la procédure suivante pour définir une séquence de tâches à fort impact.

> [!NOTE]  
> Toute séquence de tâches qui remplit certaines conditions est définie automatiquement comme séquence à fort impact. Pour plus d’informations, consultez [Gérer les déploiements à haut risque](/sccm/protect/understand/settings-to-manage-high-risk-deployments).

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.  

2. Sélectionnez la séquence de tâches à modifier, puis **Propriétés**.  

3. Sous l’onglet **Notification utilisateur**, sélectionnez **Il s’agit d’une séquence de tâches avec un impact élevé**.  


### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Créer une notification personnalisée pour les déploiements à haut risque

Utilisez la procédure suivante pour créer une notification personnalisée pour les déploiements à fort impact.

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez **Séquences de tâches**.  

2. Sélectionnez la séquence de tâches à modifier, puis **Propriétés**.  

3. Sous l’onglet **Notification utilisateur**, sélectionnez **Utiliser du texte personnalisé**.  

    > [!NOTE]
    > Le texte de la notification à l’utilisateur ne peut être défini que si l’option **Il s’agit d’une séquence de tâches à fort impact** est sélectionnée.  

4. Configurez les paramètres suivants :  

    > [!Note]  
    > Chaque zone de texte est soumise à une limite maximale de 255 caractères.  

    - **Texte du titre de la notification utilisateur** : spécifie le texte en bleu qui s’affiche sur la notification utilisateur du Centre logiciel. Par exemple, dans la notification utilisateur par défaut, cette section contient le message « Confirmez que vous voulez mettre à niveau le système d’exploitation sur cet ordinateur. ».  

    - **Texte du message de la notification utilisateur** : trois zones de texte fournissent le corps de la notification personnalisée. Toutes les zones de texte nécessitent la saisie d’un texte.  

        - Première zone de texte : spécifie le corps principal du texte, contenant généralement des instructions destinées à l’utilisateur. Par exemple, dans la notification utilisateur par défaut, cette section contient le message « La mise à niveau du système d’exploitation peut prendre du temps et entraîner plusieurs redémarrages de votre ordinateur. ».  

        - Deuxième zone de texte : spécifie le texte en gras dans le corps principal du texte. Par exemple, dans la notification utilisateur par défaut, cette section contient le message « Cette mise à niveau sur place installe le nouveau système d’exploitation et migre automatiquement vos applications, vos données et vos paramètres. ».  

        - Troisième zone de texte : spécifie la dernière ligne de texte sous le texte en gras. Par exemple, dans la notification utilisateur par défaut, cette section contient le message « Cliquez sur Installer pour commencer. Sinon, cliquez sur Annuler. ».  

#### <a name="example"></a>Exemple

Supposons que vous configurez la notification personnalisée suivante dans les propriétés.

![Onglet de notification utilisateur personnalisé des propriétés de la séquence de tâches](../media/user-notification.png)

Le message de notification suivant s’affiche quand l’utilisateur final ouvre l’installation à partir du Centre logiciel.

![Notification utilisateur personnalisée de la séquence de tâches à partir du Centre logiciel](../media/user-notification-enduser.png)



## <a name="BKMK_DistributeTS"></a> Distribuer le contenu associé  

Avant que les clients n’exécutent une séquence de tâches qui référence du contenu, distribuez ce contenu aux points de distribution. À tout moment, vous pouvez sélectionner la séquence de tâches et distribuer son contenu pour créer une nouvelle liste de packages de référence pour la distribution. Si vous apportez des modifications à la séquence de tâches avec du contenu mis à jour, redistribuez le contenu avant de le mettre à la disposition des clients. Pour distribuer le contenu qui est référencé par une séquence de tâches, procédez comme suit.  

### <a name="process-to-distribute-referenced-content-to-distribution-points"></a>Processus de distribution du contenu associé sur des points de distribution  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Dans la liste **Séquence de tâches** , sélectionnez la séquence de tâches que vous souhaitez distribuer.  

3. Sous l’onglet **Accueil** du ruban, sélectionnez **Distribuer du contenu** dans le groupe **Déploiement** pour lancer l’Assistant Distribution de contenu.  

4. Dans la page **Général**, vérifiez que la séquence de tâches correcte est sélectionnée pour la distribution.  

5. Sur la page **Contenu**, vérifiez le contenu à distribuer, et notamment l’image de démarrage associée à la séquence de tâches.  

6. Dans la page **Destination du contenu**, spécifiez les regroupements, le point de distribution ou le groupe de points de distribution où vous souhaitez distribuer le contenu de la séquence de tâches.  

    > [!IMPORTANT]  
    > Si la séquence de tâches que vous avez sélectionnée référence du contenu déjà distribué sur un certain point de distribution, l’Assistant ne liste pas ce point de distribution.  

7. Effectuez toutes les étapes de l'Assistant.  

Vous pouvez également préparer le contenu référencé dans la séquence de tâches. Configuration Manager crée un fichier de contenu compressé et préparé qui contient les fichiers, les dépendances associées et les métadonnées associées pour le contenu que vous sélectionnez. Ensuite, importez manuellement le contenu au niveau d’un serveur de site, d’un site secondaire ou d’un point de distribution. Pour plus d’informations sur la façon de préparer des fichiers de contenu, consultez [Préparer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).  



## <a name="BKMK_DeployTS"></a> Déployer  

Pour plus d'informations, voir [Déployer une séquence de tâches](/sccm/osd/deploy-use/deploy-a-task-sequence).

## <a name="BKMK_ExportImport"></a> Importer et exporter  

Exportez et importez des séquences de tâches avec ou sans leurs objets liés. Ce contenu référencé comprend les objets suivants :  

- Images de système d’exploitation  
- Images de démarrage  
- Packages, comme le package d’installation du client  
- Packages de pilotes  
- Applications avec dépendances  

Lorsque vous exportez et importez des séquences de tâches, tenez compte des points suivants :  

- Configuration Manager n’exporte pas les mots de passe dans la séquence de tâches. Si vous exportez et importez une séquence de tâches contenant des mots de passe, modifiez la séquence de tâches importée en entrant de nouveau les mots de passe. Voici les étapes susceptibles d’inclure un mot de passe :  

    - [Joindre un domaine ou un groupe de travail](/sccm/osd/understand/task-sequence-steps#BKMK_JoinDomainorWorkgroup)  
    - [Se connecter à un dossier réseau](/sccm/osd/understand/task-sequence-steps#BKMK_ConnectToNetworkFolder)  
    - [Exécuter la ligne de commande](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine)  

- Quand vous exportez une séquence de tâches en suivant l’étape **Définir des variables dynamiques**, Configuration Manager n’exporte pas les valeurs des variables configurées avec le paramètre **Valeur secrète**. Retapez les valeurs pour ces variables après avoir importé la séquence de tâches.  

- Si vous avez plusieurs sites principaux, importez les séquences de tâches sur le site d’administration centrale.  


### <a name="process-to-export-task-sequences"></a>Processus d’exportation de séquences de tâches  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Dans la liste **Séquence de tâches** , sélectionnez les séquences de tâches que vous voulez exporter. S’il y a plusieurs séquences de tâches sélectionnées, elles sont toutes stockées dans un même fichier d’exportation.  

3. Sous l’onglet **Accueil** du ruban, sélectionnez **Exporter** dans le groupe **Séquence de tâches** pour lancer l’Assistant Exportation d’une séquence de tâches.  

4. Sur la page **Général** , spécifiez les paramètres suivants :  

    - **Fichier** : spécifiez l’emplacement et le nom du fichier d’exportation. Si vous entrez directement le nom de fichier, veillez à inclure l'extension .zip au nom du fichier. Si vous indiquez l'emplacement du fichier d'exportation, l'Assistant ajoute automatiquement cette extension de fichier.  

    - Si vous ne voulez pas exporter les dépendances de séquences de tâches, désélectionnez l’option **Exporter toutes les dépendances de séquences de tâches**. Par défaut, l'Assistant analyse tous les objets liés et les exporte avec la séquence de tâches. Ces dépendances s’appliquent pour les applications.  

    - Si vous ne voulez pas copier le contenu de la source du package vers l’emplacement d’exportation, désélectionnez l’option **Exporter tout le contenu des séquences de tâches et des dépendances sélectionnées**. Si cette option est sélectionnée, l’Assistant Importation de séquences de tâches utilise le chemin d’importation comme nouvel emplacement de la source du package.  

    - **Commentaires de l’administrateur** : ajoutez une description des séquences de tâches à exporter.  

5. Effectuez toutes les étapes de l'Assistant.  

L'Assistant crée les fichiers de sortie suivants :  

- Si vous n’exportez pas de contenu : un fichier .zip.  

- Si vous exportez du contenu : un fichier .zip et un dossier nommé *exportation*_files, où *exportation* est le nom du fichier .zip qui contient le contenu exporté.  

Si vous incluez du contenu quand vous exportez une séquence de tâches, veillez à copier le fichier .zip et le dossier *export*_files ; sinon, l’importation échoue.  


### <a name="process-to-import-task-sequences"></a>Processus d’importation de séquences de tâches  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Systèmes d’exploitation**, puis sélectionnez le nœud **Séquences de tâches**.  

2. Sous l’onglet **Accueil** du ruban, sélectionnez **Importer une séquence de tâches** dans le groupe **Créer** pour lancer l’Assistant Importation d’une séquence de tâches.  

3. Sur la page **Général** du ruban, spécifiez le fichier .zip exporté.  

4. Sur la page **Contenu du fichier** , sélectionnez l'action dont vous avez besoin pour chaque objet que vous importez. Cette page affiche tous les objets à importer que Configuration Manager a trouvés.  

    - Si l'objet n'a jamais été importé, sélectionnez **Créer nouveau**.  

    - Si l'objet a été importé précédemment, sélectionnez l'une des actions suivantes :  

        - **Ignorer le doublon** (par défaut) : cette action n’importe pas l’objet. Au lieu de cela, l'Assistant lie l'objet existant à la séquence de tâches.  

        - **Remplacer**: cette action remplace l’objet existant par l’objet importé. Pour les applications, vous pouvez ajouter une révision pour mettre à jour l'application existante ou créer une nouvelle application.  

5. Effectuez toutes les étapes de l'Assistant.  

Après avoir importé la séquence de tâches, modifiez-la pour spécifier les mots de passe qui se trouvaient dans la séquence de tâches d'origine. Pour des raisons de sécurité, les mots de passe ne sont pas exportés.  



## <a name="return-to-previous-page-when-a-task-sequence-fails"></a>Revenir à la page précédente en cas d’échec d’une séquence de tâches

Vous pouvez revenir à une page précédente en cas d’échec de l’exécution d’une séquence de tâches. Dans les versions antérieures de Configuration Manager, vous deviez redémarrer la séquence de tâches après un échec. Utilisez le bouton **Précédent** dans les scénarios suivants :

- Quand un ordinateur démarre dans Windows PE, la boîte de dialogue d’amorçage de la séquence de tâches peut s’afficher avant que la séquence de tâches ne soit disponible. Une fois que vous avez sélectionné Suivant dans ce scénario, la dernière page de la séquence de tâches s’affiche avec un message indiquant qu’aucune séquence de tâches n’est disponible. Vous pouvez alors sélectionner **Précédent** pour relancer la recherche des séquences de tâches disponibles. Vous pouvez répéter ce processus jusqu’à ce que la séquence de tâches soit disponible.  

- L’exécution d’une séquence de tâches échoue si les packages de contenu dépendants ne sont pas encore disponibles sur les points de distribution. Vous pouvez maintenant distribuer le contenu manquant qui n’a pas encore été distribué ou attendre qu’il soit disponible sur les points de distribution. Ensuite, sélectionnez **Précédent** pour que la séquence de tâches recherche à nouveau le contenu.



## <a name="BKMK_CreateTSVariables"></a> Créer des variables de séquence de tâches pour les ordinateurs et les regroupements  

Vous pouvez définir des variables de séquence de tâches personnalisées pour des ordinateurs et des regroupements. Les variables qui sont définies pour un ordinateur sont appelées variables de séquence de tâches par ordinateur. Les variables définies pour un regroupement sont appelées variables de séquence de tâches par regroupement. En cas de conflit, les variables par ordinateur sont prioritaires par rapport aux variables par regroupement. Ce comportement signifie que les variables de séquence de tâches attribuées à un ordinateur spécifique ont automatiquement une priorité plus élevée que celles attribuées au regroupement contenant l’ordinateur.  

Par exemple, l’ordinateur XYZ est membre du regroupement ABC. Vous affectez MyVariable au regroupement ABC avec la valeur 1. Vous affectez également MyVariable à l’ordinateur XYZ avec la valeur 2. La variable affectée à l’ordinateur XYZ est prioritaire sur la variable affectée au regroupement ABC. Quand une séquence de tâches comportant cette variable s’exécute sur l’ordinateur XYZ, MyVariable a la valeur 2.

Vous pouvez masquer les variables par ordinateur et par regroupement pour qu’elles ne soient pas visibles dans la console Configuration Manager. Si l’option **Ne pas afficher cette valeur dans la console Configuration Manager** est utilisée, la valeur de la variable n’est pas affichée dans la console. La variable peut toutefois encore être utilisée par la séquence de tâches lors de son exécution. Si vous ne voulez plus que ces variables soient masquées, commencez par les supprimer. Ensuite, redéfinissez les variables sans sélectionner l’option permettant de les masquer.  

> [!WARNING]  
> Le paramètre **Ne pas afficher cette valeur dans la console Configuration Manager** s’applique uniquement à la console Configuration Manager. Les valeurs des variables sont toujours affichées dans le fichier journal de la séquence de tâches (SMSTS.LOG).

Vous pouvez gérer les variables par ordinateur sur un site principal ou sur un site d'administration centrale. Configuration Manager ne prend pas en charge plus de 1 000 variables affectées pour un même ordinateur.  

> [!IMPORTANT]  
> Quand vous utilisez des variables par regroupement pour des séquences de tâches, tenez compte des comportements suivants :  
>
> - Les modifications apportées aux regroupements sont toujours répliquées dans toute la hiérarchie. Toutes les modifications que vous apportez à des variables d’un regroupement sont donc appliquées aux membres du site actuel, mais aussi à tous les membres du regroupement à travers la hiérarchie.  
>  
> - La suppression d’un regroupement a également pour effet de supprimer les variables de séquence de tâches configurées pour le regroupement.  


### <a name="process-to-create-task-sequence-variables-for-a-computer"></a>Processus de création de variables de séquence de tâches pour un ordinateur  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, puis sélectionnez le nœud **Appareils**.  

2. Sélectionnez l’ordinateur cible, puis **Propriétés**.  

3. Dans la boîte de dialogue **Propriétés**, basculez sous l’onglet **Variables**.  

4. Pour chaque variable à créer, sélectionnez l’icône **Nouveau**. Indiquez le **Nom** et la **Valeur** de la variable de séquence de tâches. Si vous voulez masquer la variable pour qu’elle ne soit pas visible dans la console Configuration Manager, sélectionnez l’option **Ne pas afficher cette valeur dans la console Configuration Manager**.  

5. Après avoir ajouté toutes les variables aux propriétés de l’ordinateur, sélectionnez **OK**.  


### <a name="process-to-create-task-sequence-variables-for-a-collection"></a>Processus de création de variables de séquence de tâches pour un regroupement  

1. Dans la console Configuration Manager, accédez à l’espace de travail **Ressources et Conformité**, puis sélectionnez le nœud **Regroupements d’appareils**. Sélectionnez le regroupement cible, puis **Propriétés**.  

2. Dans la boîte de dialogue **Propriétés**, basculez sous l’onglet **Variables de regroupement**.  

3. Pour chaque variable à créer, sélectionnez l’icône **Nouveau**. Indiquez le **Nom** et la **Valeur** de la variable de séquence de tâches. Si vous voulez masquer la variable pour qu’elle ne soit pas visible dans la console Configuration Manager, sélectionnez l’option **Ne pas afficher cette valeur dans la console Configuration Manager**.  

4. Si vous le souhaitez, spécifiez la priorité que Configuration Manager doit utiliser lors de l’évaluation des variables de séquence de tâches.  

5. Après avoir ajouté toutes les variables aux propriétés du regroupement, sélectionnez **OK**.  



## <a name="BKMK_AdditionalActionsTS"></a> Actions supplémentaires pour gérer des séquences de tâches  

Vous pouvez gérer des séquences de tâches en utilisant des actions supplémentaires lorsque vous sélectionnez une séquence de tâches.  

### <a name="available-options"></a>Options disponibles

#### <a name="edit"></a>Éditer

Pour plus d’informations, voir [Modifier une séquence de tâches](#BKMK_ModifyTaskSequence).

#### <a name="enable"></a>Activez

Active la séquence de tâches afin que les clients puissent l’exécuter. Il est inutile de redéployer une séquence de tâches une fois activée.  

#### <a name="disable"></a>Désactiver

Désactive la séquence de tâches afin qu’elle ne puisse pas s’exécuter sur des ordinateurs. Il est possible de déployer une séquence de tâches désactivée, mais les ordinateurs ne l’exécutent pas tant qu’elle n’est pas activée.  

#### <a name="export"></a>Exporter

Pour plus d’informations, voir [Exporter et importer des séquences de tâches](#BKMK_ExportImport).

#### <a name="copy"></a>Copier

Effectue une copie de la séquence de tâches sélectionnée. Cette action est utile pour, à partir d’une séquence de tâches existante, en créer une nouvelle.

Lorsque vous faites une copie d'une séquence de tâches dans un dossier, la copie est répertoriée dans ce dossier jusqu'à ce que vous actualisiez le nœud de séquence de tâches. Après l'actualisation, la copie s'affiche dans le dossier racine.  

#### <a name="refresh"></a>Actualisation

Actualise les détails de la séquence de tâches sélectionnée.

#### <a name="delete"></a>Supprimer

Supprime la séquence de tâches sélectionnée.

#### <a name="create-phased-deployment"></a>Créer un déploiement par phases

Pour plus d’informations, voir [Créer des déploiements par phases](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence).

#### <a name="deploy"></a>Déployer

Pour plus d'informations, voir [Déployer une séquence de tâches](/sccm/osd/deploy-use/deploy-a-task-sequence).

#### <a name="distribute-content"></a>Distribuer du contenu

Démarre l’Assistant Distribuer du contenu pour envoyer le contenu référencé aux points de distribution.

#### <a name="create-prestaged-content-file"></a>Créer un fichier de contenu préparé

Démarre l'Assistant Création du fichier de contenu préparé pour préparer le contenu de séquence de tâches. Pour plus d’informations sur la création d’un fichier de contenu préparé, consultez [Préparer du contenu](/sccm/core/servers/deploy/configure/deploy-and-manage-content#bkmk_prestage).

#### <a name="move"></a>Déplacer

Déplace la séquence de tâches sélectionnée vers un autre dossier dans le nœud **Séquences de tâches**.

#### <a name="set-security-scopes"></a>Définir des étendues de sécurité

Sélectionnez les étendues de sécurité de la séquence de tâches sélectionnée. Pour plus d’informations, consultez [Sécurité et audit](/sccm/core/understand/fundamentals-of-role-based-administration#bkmk_PlanScope).

#### <a name="properties"></a>Propriétés

Pour plus d’informations, voir [Configurer les propriétés du Centre logiciel](#bkmk_prop-general) et [Configurer les paramètres avancés des séquences de tâches](#bkmk_prop-advanced).

#### <a name="view"></a>Afficher

<!--3633146-->
À compter de la version 1902, **Afficher** est l’action par défaut sur les séquences de tâches. Elle permet de voir les étapes de la séquence de tâches sans la verrouiller pour modification.  


## <a name="see-also"></a>Voir aussi

[Scénarios de déploiement de systèmes d’exploitation d’entreprise](scenarios-to-deploy-enterprise-operating-systems.md)
