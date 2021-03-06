---
title: "Gérer les regroupements | System Center Configuration Manager"
description: "Découvrez comment effectuer les principales tâches de gestion des regroupements dans System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
caps.latest.revision: 8
caps.handback.revision: 0
author: nbigman
ms.author: nbigman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: d7d0b9c40f22bf1a7c477d1b8626d5a531c959d7


---
# <a name="how-to-manage-collections-in-system-center-configuration-manager"></a>Guide pratique pour gérer des regroupements dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Aidez-vous des informations générales de cette rubrique pour effectuer les tâches de gestion des regroupements dans System Center Configuration Manager.  

> [!NOTE]  
>  Pour plus d’informations sur la création de regroupements dans Configuration Manager, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).  

## <a name="how-to-manage-device-collections"></a>Comment gérer des regroupements de périphériques  
 Dans l'espace de travail **Biens et conformité** , sélectionnez **Regroupements de périphériques**, puis le regroupement à gérer, et enfin sélectionnez une tâche de gestion.  

 Utilisez le tableau suivant pour obtenir plus d'informations sur les tâches de gestion qui pourraient nécessiter certaines informations avant de les sélectionner.  

|Tâche de gestion|Détails|Plus d'informations|  
|---------------------|-------------|----------------------|  
|**Afficher les membres**|Affiche toutes les ressources qui sont membres du regroupement sélectionné dans un nœud temporaire sous le nœud **Périphériques** .|Aucune information supplémentaire.|  
|**Ajouter les éléments sélectionnés**|Fournit les options suivantes pour exécuter l'une des actions suivantes :<br /><br /> - <br />                    **Ajouter des éléments sélectionnés à un regroupement d’appareils existant** : ouvre la boîte de dialogue **Sélectionner un regroupement**, où vous pouvez sélectionner le regroupement auquel vous souhaitez ajouter les membres du regroupement sélectionné. Le regroupement sélectionné est inclus dans ce regroupement grâce à la règle d'adhésion **Inclure des regroupements** .<br /><br /> - **Ajouter des éléments sélectionnés au nouveau regroupement d’appareils** : ouvre l’**Assistant Création d’un regroupement de périphériques** à partir duquel vous pouvez créer un nouveau regroupement. Le regroupement sélectionné est inclus dans ce regroupement grâce à la règle d'adhésion **Inclure des regroupements** .|[Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Installer le client**|Ouvre l’**Assistant Installation du client** qui utilise la méthode d’installation push du client pour installer un client Configuration Manager sur tous les ordinateurs du regroupement sélectionné.|[Tâches de déploiement du client pour System Center Configuration Manager](../../../../core/clients/deploy/client-deployment-tasks.md)|  
|**Gérer les demandes d'affinité**|Ouvre la boîte de dialogue **Gérer les demandes d'affinité entre périphérique et utilisateur** où vous pouvez approuver ou rejeter les demandes en attente pour établir des affinités des périphériques d'utilisateur pour les périphériques du regroupement sélectionné.|[Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Effacer les déploiements PXE requis**|Efface tous les déploiements de démarrage PXE requis à partir de tous les membres du regroupement sélectionné.|[Introduction au déploiement de systèmes d’exploitation](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**Mettre à jour l'adhésion**|Évalue l'adhésion pour le regroupement sélectionné. Pour les regroupements comportant de nombreux membres, l'exécution de cette mise à jour peut durer un certain temps. Utilisez l'action **Actualiser** pour mettre à jour l'affichage avec les nouveaux membres des regroupements une fois la mise à jour terminée.|Aucune information supplémentaire.|  
|**Ajouter des ressources**|Ouvre la boîte de dialogue **Ajouter des ressources au regroupement** dans laquelle vous pouvez rechercher de nouvelles ressources à ajouter au regroupement sélectionné.<br /><br /> L’icône du regroupement sélectionné affiche un symbole de sablier pendant l’exécution de la mise à jour.|Aucune information supplémentaire.|  
|**Notification du client**|Ordonne à tous les clients figurant dans le regroupement de périphériques sélectionné de télécharger la stratégie d’ordinateur ou utilisateur.|Aucune information supplémentaire.|  
|**Endpoint Protection**|Effectue une analyse rapide ou complète des logiciels anti-programme malveillant ou télécharge les dernières définitions de logiciels anti-programme malveillant sur les ordinateurs du regroupement sélectionné.|[Endpoint Protection dans System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md)|  
|**Exporter**|Ouvre l’**Assistant Exportation de regroupements** qui vous aide à exporter ce regroupement dans un fichier MOF (Managed Object Format) qui peut ensuite être archivé ou utilisé sur un autre site Configuration Manager.<br /><br /> Lorsque vous exportez un regroupement, les regroupements qui sont référencés par le regroupement sélectionné à l'aide d'une règle **Inclure** ou **Exclure** ne sont pas exportés.|Aucune information supplémentaire.|  
|**Copier**|Crée une copie du regroupement sélectionné. Le nouveau regroupement utilise le regroupement sélectionné comme limitation au regroupement.|Aucune information supplémentaire.|  
|**Supprimer**|Supprime le regroupement sélectionné. Vous pouvez également supprimer toutes les ressources du regroupement à partir de la base de données du site.<br /><br /> Vous ne pouvez pas supprimer les regroupements qui sont intégrés à Configuration Manager.|Pour obtenir la liste des regroupements intégrés, consultez [Présentation des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simuler un déploiement**|Ouvre l' **Assistant Simuler un déploiement d'application** , qui vous permet de tester les résultats du déploiement d'une application sans installer ou désinstaller l'application.|[Comment simuler des déploiements d’applications avec System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Déployer**|Affiche les options suivantes :<br /><br /> - <br />                    **Application** : ouvre l’**Assistant Déploiement logiciel**, où vous pouvez sélectionner et configurer le déploiement d’une application vers le regroupement sélectionné.<br /><br /> - <br />                    **Programme** : ouvre l' **Assistant Déploiement logiciel** , où vous pouvez sélectionner et configurer le déploiement d'un package et d'un programme vers le regroupement sélectionné.<br /><br /> - **Ligne de base de configuration** : ouvre la boîte de dialogue **Déployer des lignes de base de configuration**, dans laquelle vous pouvez configurer le déploiement d’une ou de plusieurs bases de référence de configuration vers le regroupement sélectionné.<br /><br /> - <br />                    **Séquence de tâches** : ouvre l' **Assistant Déploiement logiciel** , où vous pouvez sélectionner et configurer le déploiement d'une séquence de tâches vers le regroupement sélectionné.<br /><br /> - <br />                    **Mises à jour logicielles** : ouvre l’**Assistant Déploiement des mises à jour logicielles** où vous pouvez configurer le déploiement de mises à jour logicielles vers les ressources du regroupement sélectionné.|[Déployer des applications avec System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Packages et programmes dans System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Comment déployer des bases de référence de configuration dans System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [Gérer les séquences de tâches pour automatiser des tâches dans System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [Gérer les mises à jour logicielles dans System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## <a name="how-to-manage-user-collections"></a>Comment gérer des regroupements d’utilisateurs  
 Dans l'espace de travail **Biens et conformité** , sélectionnez **Regroupements d'utilisateurs**, puis le regroupement à gérer, et enfin sélectionnez une tâche de gestion.  

 Utilisez le tableau suivant pour obtenir plus d'informations sur les tâches de gestion qui pourraient nécessiter certaines informations avant de les sélectionner.  

|Tâche de gestion|Détails|Plus d'informations|  
|---------------------|-------------|----------------------|  
|**Afficher les membres**|Affiche toutes les ressources qui sont membres du regroupement sélectionné dans un nœud temporaire sous le nœud **Utilisateurs** .|Aucune information supplémentaire.|  
|**Ajouter les éléments sélectionnés**|Cette option vous permet d'exécuter l'une des actions suivantes :<br /><br /> - <br />                    **Ajouter des éléments sélectionnés à un regroupement d’utilisateurs existant** : ouvre la boîte de dialogue **Sélectionner un regroupement**, où vous pouvez sélectionner le regroupement auquel vous souhaitez ajouter les membres du regroupement sélectionné. Le regroupement sélectionné est inclus dans ce regroupement grâce à la règle d'adhésion **Inclure des regroupements** .<br /><br /> - **Ajouter des éléments sélectionnés au nouveau regroupement d’utilisateurs** : ouvre l’**Assistant Création d’un regroupement d’utilisateurs** à partir duquel vous pouvez créer un nouveau regroupement. Le regroupement sélectionné est inclus dans ce regroupement grâce à la règle d'adhésion **Inclure des regroupements** .|[Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Gérer les demandes d'affinité**|Ouvre la boîte de dialogue **Gérer les demandes d'affinité entre périphérique et utilisateur** où vous pouvez approuver ou rejeter les demandes en attente pour établir des affinités des périphériques d'utilisateur pour les utilisateurs du regroupement sélectionné.|[Lier des utilisateurs et des appareils avec l’affinité entre utilisateur et appareil dans System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Mettre à jour l'adhésion**|Évalue l'adhésion pour le regroupement sélectionné. Pour les regroupements comportant de nombreux membres, l'exécution de cette mise à jour peut durer un certain temps. Utilisez l'action **Actualiser** pour mettre à jour l'affichage avec les nouveaux membres des regroupements une fois la mise à jour terminée.<br /><br /> L’icône du regroupement sélectionné affiche un symbole de sablier pendant l’exécution de la mise à jour.|Aucune information supplémentaire.|  
|**Ajouter des ressources**|Ouvre la boîte de dialogue **Ajouter des ressources au regroupement** dans laquelle vous pouvez rechercher de nouvelles ressources à ajouter au regroupement sélectionné.|Aucune information supplémentaire.|  
|**Exporterer**|Ouvre l’**Assistant Exportation de regroupements** qui vous aide à exporter ce regroupement dans un fichier MOF (Managed Object Format) qui peut ensuite être archivé ou utilisé sur un autre site Configuration Manager.<br /><br /> Lorsque vous exportez un regroupement, les regroupements qui sont référencés par le regroupement sélectionné à l'aide d'une règle **Inclure** ou **Exclure** ne sont pas exportés.|Aucune information supplémentaire.|  
|**Copier**|Crée une copie du regroupement sélectionné. Le nouveau regroupement utilise le regroupement sélectionné comme limitation au regroupement.|Aucune information supplémentaire.|  
|**Supprimer**|Supprime le regroupement sélectionné. Vous pouvez également supprimer toutes les ressources du regroupement à partir de la base de données du site.<br /><br /> Vous ne pouvez pas supprimer les regroupements qui sont intégrés à Configuration Manager.|Pour obtenir la liste des regroupements intégrés, consultez [Présentation des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simuler un déploiement**|Ouvre l' **Assistant Simuler un déploiement d'application** , qui vous permet de tester les résultats du déploiement d'une application sans installer ou désinstaller l'application.|[Comment simuler des déploiements d’applications avec System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Déployer**|Affiche les options suivantes :<br /><br /> - **Application** : ouvre l’**Assistant Déploiement logiciel**, où vous pouvez sélectionner et configurer le déploiement d’une application vers le regroupement sélectionné.<br /><br /> - <br />                    **Programme** : ouvre l' **Assistant Déploiement logiciel** , où vous pouvez sélectionner et configurer le déploiement d'un package et d'un programme vers le regroupement sélectionné.<br /><br /> - **Ligne de base de configuration** : ouvre la boîte de dialogue **Déployer des lignes de base de configuration**, dans laquelle vous pouvez configurer le déploiement d’une ou de plusieurs bases de référence de configuration vers le regroupement sélectionné.|[Déployer des applications avec System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Packages et programmes dans System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [Comment déployer des bases de référence de configuration dans System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="a-namebkmkcollpropa-collection-properties"></a><a name="BKMK_CollProp"></a> Propriétés d’un regroupement  
 Lorsque vous ouvrez la boîte de dialogue **Propriétés** pour un regroupement, vous pouvez afficher et configurer les propriétés suivantes pour un regroupement  

|Nom de l'onglet|Plus d'informations|  
|--------------|----------------------|  
|**Général**|Permet d'afficher et de configurer des informations générales sur le regroupement sélectionné, y compris le nom du regroupement et la limitation au regroupement.|  
|**Règles d'adhésion**|Permet de configurer les règles d'adhésion qui définissent l'adhésion de ce regroupement. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements dans System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|**Gestion de l'alimentation**|Permet de configurer les modes de gestion de l'alimentation qui sont attribués aux ordinateurs du regroupement sélectionné. Pour plus d’informations, consultez [Présentation de la gestion de l’alimentation](../../../../core/clients/manage/power/introduction-to-power-management.md).|  
|**Déploiements**|Affiche tout logiciel qui a été déployé vers les membres du regroupement sélectionné.|  
|**Fenêtres de maintenance**|Permet d'afficher et de configurer les fenêtres de maintenance qui sont appliquées aux membres du regroupement sélectionné. Pour plus d’informations, consultez [Guide pratique pour utiliser les fenêtres de maintenance dans System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  
|**Variables du regroupement**|Permet de configurer les variables qui s'appliquent à ce regroupement et peuvent être utilisées par les séquences de tâches. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Groupes de points de distribution**|Permet d'associer un ou plusieurs groupes de points de distribution aux membres du regroupement sélectionné. Pour plus d’informations, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Sécurité**|Affiche les utilisateurs administratifs qui disposent d'autorisations pour le regroupement sélectionné à partir de rôles associés et d'étendues de sécurité.|  
|**Analyse**|Permet de configurer le moment où des alertes sont générées pour l'état du client et Endpoint Protection. Pour plus d’informations, consultez [Guide pratique pour configurer l’état du client dans System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md)et [Guide pratique pour surveiller Endpoint Protection dans System Center Configuration Manager](../../../../protect/deploy-use/monitor-endpoint-protection.md).|  



<!--HONumber=Nov16_HO1-->


