---
title: Maintenance de groupe de serveurs
titleSuffix: Configuration Manager
description: La console System Center Configuration Manager fournit des alertes et des états pour surveiller les mises à jour et la compatibilité.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/07/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 304a83ea-0f72-437d-9688-2e6e0c7526dd
ms.collection: M365-identity-device-management
ms.openlocfilehash: aac5c9d6c683447fe7dda50e6dcfd52b7024656d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56131640"
---
# <a name="service-a-server-group"></a>Maintenance de groupe de serveurs

*S’applique à : System Center Configuration Manager (Current Branch)*

>[!IMPORTANT]
>Les fonctionnalités de préversion sont des fonctions incluses dans la branche Current Branch à des fins de test préalable dans un environnement de production. Ces fonctionnalités sont entièrement prises en charge mais sont toujours en cours de développement. Elles peuvent donc être modifiées jusqu'à ce qu’elles passent en préversion. Vous devez activer cette fonctionnalité pour qu’elle soit disponible. Pour plus d’informations, consultez [Utiliser des fonctionnalités de préversions de mises à jour](https://docs.microsoft.com/sccm/core/servers/manage/install-in-console-updates#bkmk_prerelease).

À partir de System Center Configuration Manager version 1606, vous pouvez configurer les paramètres de groupe de serveurs pour un regroupement, afin de définir le nombre, le pourcentage ou l’ordre des ordinateurs du regroupement qui installeront les mises à jour logicielles. Vous pouvez également configurer des scripts PowerShell de prédéploiement et de post-déploiement pour exécuter des actions personnalisées.

Lorsque vous déployez des mises à jour logicielles dans un regroupement dont les paramètres de groupe de serveurs sont configurés, Configuration Manager détermine le nombre d’ordinateurs du regroupement qui peuvent installer les mises à jour logicielles à un moment donné quelconque et met à disposition le même nombre de verrous de déploiement. Seuls les ordinateurs qui obtiennent un verrou de déploiement commenceront l’installation des mises à jour logicielles. Lorsqu’un verrou de déploiement est disponible, un ordinateur obtient le verrou de déploiement, installe les mises à jour logicielles, puis libère le verrou de déploiement lorsque l’installation des mises à jour logicielles se termine correctement. Ensuite, le verrou de déploiement devient disponible pour d’autres ordinateurs. Si un ordinateur ne parvient pas à libérer un verrou de déploiement, vous pouvez libérer manuellement tous les verrous de déploiement de groupe de serveurs pour le regroupement.

>[!IMPORTANT]
>Tous les ordinateurs du regroupement doivent être affectés au même site.

#### <a name="to-create-a-collection-for-a-server-group"></a>Pour créer un regroupement pour un groupe de serveurs  
Les paramètres du groupe de serveurs sont configurés dans les propriétés d’un regroupement d’appareils. Pour effectuer la maintenance d’un groupe de serveurs, tous les membres du regroupement doivent être affectés au même site. Utilisez les étapes suivantes pour créer un regroupement et configurer les paramètres du groupe de serveurs :
1.  [Créez un regroupement d’appareils](../../core/clients/manage/collections/create-collections.md) contenant les ordinateurs du groupe de serveurs.  

2.  Dans l’espace de travail **Ressources et Conformité**, cliquez sur **Regroupements d’appareils**, cliquez avec le bouton droit sur le regroupement qui contient les ordinateurs du groupe de serveurs, puis cliquez sur **Propriétés**.  

3.  Sous l’onglet **Général**, sélectionnez **Tous les appareils font partie du même groupe de serveurs**, puis cliquez sur **Paramètres**.  

4.  Dans la page **Paramètres de groupe de serveurs**, spécifiez l’un des paramètres suivants :  

    -   **Autoriser un pourcentage de machines à être mises à jour en même temps** : Spécifie qu’un certain pourcentage de clients sont mis à jour simultanément. Si, par exemple, le regroupement compte 10 clients, et qu’il est configuré pour mettre à jour 30 % des clients en même temps, seuls 3 clients installeront les mises à jour logicielles à un moment donné quelconque.  

    -   **Autoriser un nombre de machines à être mises à jour en même temps** : Spécifie qu’un certain nombre de clients sont mis à jour simultanément.  

    -   **Spécifier la séquence de maintenance** : Spécifie que les clients du regroupement seront mis à jour l’un après l’autre, dans l’ordre que vous configurez. Un client installe les mises à jour logicielles après seulement que le client qui le précède dans la liste a terminé l’installation de ses mises à jour logicielles.  

5.  Indiquez s’il convient d’utiliser un script de prédéploiement (drainage de nœud) ou un script de post-déploiement (relance de nœud).  

    > [!WARNING]
    > Les scripts personnalisés ne sont pas signés par Microsoft. Il vous incombe de préserver l’intégrité de ces scripts.

    > [!TIP]  
    > Voici des exemples que vous pouvez utiliser dans des tests de scripts de prédéploiement et de post-déploiement qui enregistrent l’heure actuelle dans un fichier texte :  
    >   
    >  **Prédéploiement**  
    >   
    >  `#Start`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\start.txt`  
    >   
    >  **Post-déploiement**  
    >   
    >  `#End`  
    >   
    >  `$a = Get-Date`  
    >   
    >  `Write-Output "Universal Time: " + $a.ToUniversalTime()  |`  
    >   
    >  `Out-File C:\Windows\Temp\end.txt`  

## <a name="deploy-software-updates-to-the-server-group-and-monitor-status"></a>Déployer des mises à jour logicielles dans le groupe de serveurs et surveiller leur état  
Vous déployez des mises à jour logicielles dans le regroupement de groupe de serveurs à l’aide du processus de déploiement standard. Après avoir déployé les mises à jour logicielles, vous pouvez surveiller le déploiement des mises à jour logicielles dans la console Configuration Manager.
1.  [Déployez les mises à jour logicielles](manually-deploy-software-updates.md) sur le regroupement du groupe de serveurs.   

2.  [Surveillez le déploiement des mises à jour logicielles](monitor-software-updates.md). Outre les affichages d’analyse standard pour le déploiement de mises à jour logicielles, l’état **En attente d’un verrou** est affiché lorsqu’un client attend son tour pour installer les mises à jour logicielles. Vous pouvez passer en revue le fichier UpdatesDeployment.log pour obtenir plus d’informations.


## <a name="clear-the-deployment-locks-for-computers-in-a-server-group"></a>Désactivez les verrous de déploiement pour les ordinateurs d’un groupe de serveurs  
Quand un ordinateur ne parvient pas à libérer un verrou de déploiement, vous pouvez libérer manuellement tous les verrous de déploiement de groupe de serveurs du regroupement. Désactivez les verrous uniquement lorsqu’un déploiement est bloqué lors de la mise à jour des ordinateurs du regroupement et que des ordinateurs ne sont toujours pas compatibles.  
1.  Dans l’espace de travail **Ressources et Conformité**, cliquez sur **Regroupements d’appareils**, puis cliquez sur le regroupement pour désactiver les verrous de déploiement.  

2.  Sous l’onglet **Accueil**, dans le groupe **Déploiement**, cliquez sur **Supprimer les verrous de déploiement du groupe de serveurs**. Quand des clients ne parviennent pas à installer les mises à jour logicielles et empêchent les autres clients d’installer leurs mises à jour logicielles, les verrous de déploiement peuvent être désactivés manuellement.  
