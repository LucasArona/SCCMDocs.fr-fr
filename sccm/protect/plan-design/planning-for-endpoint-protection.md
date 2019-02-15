---
title: Planifier Endpoint Protection
titleSuffix: Configuration Manager
ms.date: 03/07/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7610bbd3-a67f-4a09-8115-e35d40d43b42
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 94b1da6564c4b23c3db45b7b8851d795b97b061e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56133634"
---
# <a name="planning-for-endpoint-protection-in-system-center-configuration-manager"></a>Planification de Endpoint Protection dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Endpoint Protection dans System Center Configuration Manager vous permet de gérer les stratégies de logiciel anti-programme malveillant et la sécurité du Pare-feu Windows pour les ordinateurs clients de votre hiérarchie Configuration Manager.  

> [!IMPORTANT]  
>  Vous devez détenir une licence pour pouvoir utiliser Endpoint Protection pour gérer les clients dans votre hiérarchie Configuration Manager.  

L’utilisation d’Endpoint Protection avec Configuration Manager présente les avantages suivants :  

-   Configuration des stratégies de logiciel anti-programme malveillant, des paramètres du Pare-feu Windows et gestion du service Windows Defender - Protection avancée contre les menaces sur certains groupes d’ordinateurs  

-   Utilisation des mises à jour logicielles Configuration Manager pour télécharger les derniers fichiers de définitions de logiciel anti-programme malveillant pour tenir à jour les ordinateurs clients  

-   Envoi de notifications par courrier électronique, utilisation de la surveillance dans la console et affichage de rapports pour informer les utilisateurs administratifs qu’un logiciel malveillant a été détecté sur des ordinateurs clients  

Les ordinateurs Windows 10 n’ont besoin d’aucun autre client pour la gestion d’Endpoint Protection. Sur les ordinateurs Windows 8.1 et antérieurs, Endpoint Protection installe son propre client en plus du client Configuration Manager. Le client Endpoint Protection offre les possibilités suivantes :  

-   Détection des logiciels malveillants et des logiciels espions et mesures correctives  

-   Détection des rootkits et mesures correctives  

-   Évaluation des vulnérabilités critiques et mises à jour automatiques des définitions et du moteur  

-   Détection des vulnérabilités réseau via le système NIS (Network Inspection System)  

-   Intégration avec Cloud Protection Service pour signaler les logiciels malveillants à Microsoft. Quand vous rejoignez ces services, le client Windows Defender ou Endpoint Protection peut télécharger les dernières définitions à partir du Centre de protection contre les programmes malveillants quand un logiciel malveillant non identifié est détecté sur un ordinateur.  

> [!NOTE]  
>  Le client Endpoint Protection peut être installé sur un serveur qui exécute Hyper-V et sur les machines virtuelles invitées dotées d’un système d’exploitation pris en charge. Pour éviter une utilisation excessive de l’UC, les actions Endpoint Protection ont un délai intégré aléatoire, ce qui empêche les services de s’exécuter simultanément.  

  De plus, Endpoint Protection dans Configuration Manager vous permet de gérer les paramètres du Pare-feu Windows dans la console Configuration Manager.  

 [Exemple de scénario : l’utilisation de System Center Endpoint Protection pour protéger les ordinateurs contre les programmes malveillants dans System Center Configuration Manager](../deploy-use/scenarios-endpoint-protection.md) illustre la façon dont vous pouvez configurer et gérer Endpoint Protection et le Pare-feu Windows.  

## <a name="managing-malware-with-endpoint-protection"></a>Gestion des logiciels malveillants avec Endpoint Protection  

Endpoint Protection dans Configuration Manager vous permet de créer des stratégies de logiciel anti-programme malveillant qui contiennent des paramètres pour les configurations de client Endpoint Protection. Vous pouvez ensuite déployer ces stratégies sur les ordinateurs clients et les surveiller dans le nœud **État Endpoint Protection** dans l’espace de travail **Surveillance** ou à l’aide des rapports Configuration Manager.  

 Informations complémentaires :  

-   [Créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](../deploy-use/endpoint-antimalware-policies.md) : créez, déployez et surveillez des stratégies de logiciel anti-programme malveillant à l’aide d’une liste de paramètres que vous pouvez configurer  

-   [Surveiller Endpoint Protection dans System Center Configuration Manager](../deploy-use/monitor-endpoint-protection.md) : surveillez les rapports d’activité, les ordinateurs clients infectés, et bien d’autres choses encore.   

-   [Gérer les stratégies de logiciel anti-programme malveillant et les paramètres de pare-feu pour Endpoint Protection dans System Center Configuration Manager](../deploy-use/endpoint-antimalware-firewall.md) : vous pouvez changer la priorité des stratégies de [logiciel anti-programme malveillant](../deploy-use/endpoint-antimalware-firewall.md#manage-antimalware-policies) ou du [pare-feu](../deploy-use/endpoint-antimalware-firewall.md#manage-windows-firewall-policies), [prendre des mesures correctives contre les programmes malveillants détectés sur les ordinateurs clients](../deploy-use/endpoint-antimalware-firewall.md#remediate-detected-malware), et effectuer bien d’autres tâches

## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gestion du pare-feu Windows avec Endpoint Protection  
 Endpoint Protection dans Configuration Manager assure une gestion de base du Pare-feu Windows sur les ordinateurs clients. Pour chaque profil de réseau, vous pouvez :  

-   Activer ou désactiver le pare-feu Windows.  

-   Bloquer les connexions entrantes, y compris celles figurant dans la liste des programmes autorisés.  

-   Avertir l'utilisateur lorsque le pare-feu Windows bloque un nouveau programme.  

> [!NOTE]  
>  Endpoint Protection prend en charge la gestion du pare-feu Windows uniquement.  

  Pour plus d’informations sur la création et le déploiement de stratégies de Pare-feu Windows pour Endpoint Protection, consultez [Guide pratique pour créer et déployer des stratégies de Pare-feu Windows pour Endpoint Protection dans System Center Configuration Manager](../deploy-use/create-windows-firewall-policies.md).  

## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender - Protection avancée contre les menaces

À compter de la version 1606 de Configuration Manager (Current Branch), Endpoint Protection facilite la gestion et la surveillance du service Windows Defender - Protection avancée contre les menaces. Ce nouveau service aide les entreprises à détecter, analyser et contrer les attaques avancées ciblant leurs réseaux. Consultez [Windows Defender - Protection avancée contre les menaces](../deploy-use/windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flux de travail Endpoint Protection  
 Utilisez le diagramme suivant pour comprendre le flux de travail qui permet d’implémenter Endpoint Protection dans votre hiérarchie Configuration Manager.  

 ![Flux de travail Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)

## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Client Endpoint Protection pour les ordinateurs Mac et les serveurs Linux  
 System Center inclut un client Endpoint Protection pour Linux et pour les ordinateurs Mac. Ces clients ne sont pas fournis avec Configuration Manager. Vous devez télécharger les produits suivants à partir du [Centre de gestion des licences en volume Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).  

> [!IMPORTANT]  
>  Vous devez être client d’une licence en volume Microsoft pour télécharger les fichiers d’installation d’Endpoint Protection pour Linux et Mac.  

 Ces produits ne peuvent pas être gérés à partir de la console Configuration Manager. Toutefois, un pack d’administration System Center Operations Manager, fourni avec les fichiers d’installation, vous permet de gérer le client pour Linux à l’aide d’Operations Manager.  

 Pour plus d’informations sur l’installation et la gestion des clients Endpoint Protection sur les ordinateurs Mac et Linux, utilisez la documentation qui accompagne ces produits, disponible dans le dossier **Documentation** .

## <a name="best-practices-for-endpoint-protection-in-configuration-manager"></a>Méthodes conseillées pour Endpoint Protection dans Configuration Manager  
 Utilisez les bonnes pratiques suivantes pour Endpoint Protection dans System Center 2012 Configuration Manager.  

### <a name="configure-custom-client-settings-for-endpoint-protection"></a>Configurer les paramètres client personnalisés pour Endpoint Protection  
 Quand vous configurez les paramètres client pour Endpoint Protection, n’utilisez pas les paramètres client par défaut, car ils s’appliquent à tous les ordinateurs de votre hiérarchie. Configurez plutôt les paramètres client personnalisés et affectez ces paramètres aux regroupements d'ordinateurs dans votre hiérarchie.  

 Lorsque vous configurez les paramètres client personnalisés, vous pouvez effectuer les opérations suivantes :  

-   Personnalisez les paramètres de sécurité et de logiciels anti-programmes malveillants pour les différentes parties de votre organisation.  
-   Testez les conséquences liées à l’exécution d’Endpoint Protection sur un petit groupe d’ordinateurs avant de le déployer sur l’ensemble de la hiérarchie.  
-   Ajoutez des clients supplémentaires au regroupement au fil du temps pour échelonner votre déploiement du client Endpoint Protection.  

### <a name="distributing-definition-updates-by-using-software-updates"></a>Distribution mises à jour de définitions à l'aide de mises à jour logicielles  
 Si vous utilisez les mises à jour logicielles de Configuration Manager pour distribuer des mises à jour de définitions, placez les mises à jour de définitions dans un package qui ne contient pas d’autres mises à jour logicielles. Cela permet de conserver la taille du package de mise à jour de définition inférieure qui lui permet de répliquer vers plus rapidement les points de distribution.
