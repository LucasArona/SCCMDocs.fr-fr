---
title: Windows Autopilot avec la cogestion
titleSuffix: Configuration Manager
description: Utilisez Windows Autopilot avec la cogestion dans Configuration Manager pour simplifier la configuration de nouveaux appareils Windows 10.
ms.date: 02/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28710b925444d681a161eff184b845a1cdd430b1
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56838750"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot avec la cogestion

La réception d’un nouvel appareil Windows 10 est toujours un moment d’excitation. Toutefois, vous pouvez passer pas mal de temps sur la configuration de tous vos paramètres et applications avant de pouvoir être productif. La cogestion résout ce problème de mise en service d’appareil avec Windows Autopilot.

AutoPilot offre une expérience simplifiée pour vous et vos utilisateurs dans les situations suivantes :
- Configurer et préconfigurer de nouveaux appareils Windows 10  
- Réinitialiser, recycler et récupérer des appareils existants  

Autopilot réduit le temps, les ressources et la complexité associés au déploiement, à la gestion et à la mise hors service des appareils. De plus, l’expérience de vos utilisateurs est simple et facile dès le premier démarrage.

Windows Autopilot prend en charge plusieurs scénarios, qui sont tous optimisés avec la cogestion :

- Les utilisateurs peuvent effectuer leurs propres déploiements de nouveaux appareils dans Active Directory avec la jonction Azure AD hybride ou dans Azure Active Directory (Azure AD).  

- Vous pouvez configurer le déploiement automatique de nouveaux appareils dans Azure AD pour les appareils partagés et les kiosques.  

- Avec Windows Autopilot pour les appareils existants, utilisez Configuration Manager pour migrer un appareil existant depuis Windows 7 et Active Directory vers Windows 10 et Azure AD.  

Dans la vidéo suivante, le program manager senior, Danny Guillory, et le program manager principal, Andrew McMurray, parlent et font la démonstration de Windows Autopilot avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Avantages

Quand vous utilisez la cogestion et Autopilot ensemble, vous avez la garantie que les nouveaux appareils qui entrent dans votre réseau finissent avec le même état de gestion. Dans cette configuration, les appareils sont inscrits à Intune et ont un client Configuration Manager.  Cela vous permet d’utiliser le nouveau modèle de mise en service Windows 10 et vous évite de devoir créer, gérer et mettre à jour des images de système d’exploitation personnalisées. 

Dans tous ces scénarios, vous pouvez [activer la cogestion](/sccm/comanage/how-to-prepare-win10) automatiquement par Intune. Cette automatisation vous assiste dans le processus de mise en service et de gestion continue de l’appareil.

Avec Autopilot, vous n’avez pas besoin de vous soucier des images et des pilotes. Concentrez-vous sur la mise en service des appareils par ce processus automatisé en utilisant Intune et Configuration Manager via la cogestion.


Voici en quoi l’utilisation conjointe de la cogestion et d’Autopilot peut vous aider dès maintenant :

#### <a name="reduce-time-costs-and-complexity"></a>Minimiser le temps, les coûts et la complexité
Windows Autopilot utilise la version optimisée par l’OEM de Windows 10 qui est préinstallée sur l’appareil. Avec cette configuration, les organisations n’ont pas besoin de gérer les images personnalisées et les pilotes pour chaque modèle d’appareil utilisé. Au lieu de réimager l’appareil, remplacez l’installation existante de Windows 10 par un état « Business-ready ». Cela applique les paramètres et les stratégies, installe les applications et change l’édition de Windows 10. Par exemple, la mise à niveau de Windows 10 Professionnel vers Windows 10 Entreprise pour pouvoir prendre en charge les fonctionnalités avancées.

#### <a name="improve-the-user-experience"></a>Améliorer l’expérience utilisateur
La meilleure expérience utilisateur est celle qui cause le moins de perturbations et qui aide les utilisateurs à reprendre leur travail. Windows Autopilot offre une approche simple qui permet à vos utilisateurs d’avoir tout de configuré rapidement avec quelques clics et leurs informations d’identification Azure AD. Pour de nombreuses organisations avec une grande part d’employés distants, utilisez Windows Autopilot pour expédier de nouveaux appareils directement du fabricant.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Utiliser Autopilot et Configuration Manager pour migrer des appareils Windows 7 existants vers Windows 10
Avec Windows Autopilot pour les appareils existants, vous créez un fichier de configuration et vous le déployez avec une séquence de tâches Configuration Manager. Ce processus migre facilement les appareils existants de Windows 7 vers Windows 10. Vous utilisez une image Windows 10 de signature dans Configuration Manager et vous l’appliquez à l’appareil Windows 7 existant avec la configuration Autopilot. Quand l’utilisateur démarre l’appareil, il passe par le processus d’intégration basé sur les utilisateurs Autopilot.

Voici les étapes Autopilot pour les appareils existants :

![Passer par la présentation Windows Autopilot pour les appareils existants](media/autopilot-for-existing-devices.png)

1. Déployer une stratégie de groupe pour rediriger les dossiers connus vers OneDrive
2. Générer le fichier de configuration Autopilot
3. Déployer une séquence de tâches pour mettre à niveau vers Windows 10
4. L’ordinateur Windows 10 passe par Autopilot au premier démarrage

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernisation de la mise en service des appareils pour tous les types d’employés
Avec Autopilot, vous pouvez actuellement offrir un déploiement de système d’exploitation autonome sur les appareils sans surveillance ou les appareils partagés à l’aide du mode de déploiement automatique. Cette configuration répond aux besoins de l’ensemble de vos différents types d’employés. De plus, la fonction Réinitialisation Windows Autopilot permet de s’assurer que la remise en service d’un appareil avec un nouvel utilisateur est simple et facile. Ce processus simplifie ce qui avait l’habitude d’être une tâche difficile quand vous avez des travailleurs saisonniers ou sous contrat. 



## <a name="case-study"></a>Étude de cas

La société de transport ferroviaire et de logistique allemande DB Shenker utilise Autopilot pour améliorer la productivité de ses employés et libérer ses équipes informatiques des tâches quotidiennes de support. Shenker a abandonné la création d’images traditionnelle pour la remplacer par une mise en service via le cloud. Maintenant, ils utilisent la jonction Azure AD et Intune pour que les nouveaux appareils deviennent rapidement opérationnels. 

Plutôt que leurs employés distants perdent leur temps à se rendre dans un endroit où se trouve un service informatique, Shenker utilise maintenant Windows Autopilot. Ils envoient aux employés leur matériel directement du fabricant à leur bureau local. Les employés connectent leur nouvel appareil à Internet et se connectent avec leurs informations d’identification Azure AD. L’appareil se connecte ensuite aux applications et services que le service informatique de Schenker assigne au profil de chaque utilisateur.

Pour plus d’informations, consultez [Global logistics firm centralizes IT, unites employees with modern digital workplace](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Proposition de valeur

Insufflez un sentiment de satisfaction dans votre organisation en créant une meilleure expérience utilisateur pour vos utilisateurs. Utilisez Windows Autopilot pour réduire les coûts. Libérez du temps pour vous concentrer sur d’autres projets plus importants et plus percutants pour votre organisation.



## <a name="configure"></a>Configurer

Pour plus d’informations, consultez les articles suivants :

[Utiliser Intune pour créer des profils Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)

Séquence de tâches [Windows Autopilot pour les appareils existants](/sccm/osd/deploy-use/windows-autopilot-for-existing-devices)

