---
title: Configurer le contrôle à distance
titleSuffix: Configuration Manager
description: Configurez le contrôle à distance dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4e4d380319704eda608930ac938232513800b81a
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="configuring-remote-control-in-system-center-configuration-manager"></a>Configuration du contrôle à distance dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

 Cette procédure décrit la configuration des paramètres client par défaut pour le contrôle à distance. Ces paramètres s’appliquent à tous les ordinateurs de votre hiérarchie. Si vous voulez que ces paramètres s’appliquent seulement à certains ordinateurs, affectez un paramètre client personnalisé à un regroupement contenant ces ordinateurs. Pour plus d’informations, consultez [Guide pratique pour configurer les paramètres client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-settings.md). 

Pour utiliser l’Assistance à distance ou le Bureau à distance, vous devez les installer et les configurer sur l’ordinateur qui exécute la console Configuration Manager. Pour plus d’informations sur la procédure d’installation et de configuration de l’Assistance à distance ou du Bureau à distance, consultez votre documentation Windows.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>Pour activer le contrôle à distance et configurer les paramètres client  

1.  Dans la console Configuration Manager, choisissez **Administration** > **Paramètres client** > **Paramètres client par défaut**.  

4.  Sous l’onglet **Accueil**, dans le groupe **Propriétés**, choisissez **Propriétés**.  

5.  Dans la boîte de dialogue **Par défaut**, choisissez **Outils de contrôle à distance**.  

6.  Configurez les paramètres client du contrôle à distance, de l’Assistance à distance et du Bureau à distance. Pour obtenir la liste des paramètres client des outils de contrôle à distance que vous pouvez configurer, consultez [Outils de contrôle à distance](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

    Vous pouvez modifier le nom de l'entreprise qui apparaît dans la boîte de dialogue **Contrôle à distance ConfigMgr** en configurant une valeur pour **Nom d'organisation affiché dans le Centre logiciel** dans les paramètres client **Agent ordinateur** .  

 Les ordinateurs clients sont configurés avec ces paramètres la prochaine fois qu’ils téléchargent la stratégie du client. Pour lancer la récupération de stratégie pour un client unique, consultez [Comment gérer les clients dans System Center Configuration Manager](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Activer la traduction du clavier

Par défaut, Configuration Manager transmet la position des touches à partir de l’emplacement de la personne qui visualise vers l’emplacement de la personne effectuant le partage. Ceci peut poser un problème pour les configurations de clavier qui diffèrent entre la personne qui visualise et la personne effectuant le partage. Par exemple, un afficheur avec un clavier anglais tapait un « A », mais le clavier français de la personne effectuant le partage fournissait un « Q ». Nous pouvons maintenant configurer le contrôle à distance afin que le caractère lui-même soit transmis du clavier de la personne qui visualise vers la personne effectuant le partage, et que ce que la personne qui visualise veut taper parvienne à la personne effectuant le partage.

Pour activer la traduction du clavier, dans **Contrôle à distance de Configuration Manager**, choisissez **Action** et choisissez **Activer la traduction du clavier** pour transmettre la position des touches.

> [!NOTE]
>
> Les touches spéciales, notamment ~!#@$%, ne seront pas traduites correctement.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Raccourcis clavier relatifs à l’observateur de contrôle à distance

|Raccourci clavier|Description|  
|-----------------------|-----------------|  
|Alt+Pg préc|Bascule entre les programmes en cours d'exécution de gauche à droite.|  
|Alt+Pg suiv|Bascule entre les programmes en cours d'exécution de droite à gauche.|  
|Alt+Inser|Parcourt les programmes en cours d’exécution dans l’ordre dans lequel ils ont été ouverts.|  
|Alt+Origine|Affiche le menu **Démarrer** .|  
|Ctrl+Alt+Fin|Affiche la boîte de dialogue Sécurité de Windows (Ctrl+Alt+Suppr).|  
|Alt+Suppr|Affiche le menu Windows.|  
|Ctrl+Alt+Signe moins (sur le pavé numérique)|Copie la fenêtre active de l’ordinateur local vers le Presse-papiers de l’ordinateur distant.|  
|Ctrl+Alt+Signe plus (sur le pavé numérique)|Copie la zone entière de la fenêtre de l’ordinateur local dans le Presse-papiers de l’ordinateur distant.|  
