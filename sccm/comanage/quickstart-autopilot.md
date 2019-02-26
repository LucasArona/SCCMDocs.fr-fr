---
title: Autopilot Windows avec la cogestion
titleSuffix: Configuration Manager
description: Utiliser Windows Autopilot avec la cogestion dans Configuration Manager pour simplifier le jeu de configuration de nouveaux appareils Windows 10.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4c9867b7ea59b435bd1fd344dd0bf4aa67a2be21
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754919"
---
# <a name="windows-autopilot-with-co-management"></a>Autopilot Windows avec la cogestion

Réception d’un nouvel appareil Windows 10 est passionnant. Toutefois, il peut prendre moment pour configurer tous les paramètres et les applications afin que vous pouvez être productifs. Cogestion résout ce problème avec Windows Autopilot de provisionnement des appareils.

AutoPilot fournit une expérience simplifiée pour vous et vos utilisateurs dans les situations suivantes :
- Configurer et de préconfigurer de nouveaux appareils Windows 10  
- Réinitialiser, recycler et récupérer des appareils existants  

AutoPilot réduit le temps, ressources et la complexité associés à déployer, gérer et retrait d’appareils. En même temps, l’expérience de vos utilisateurs est rationalisé et facile à partir du premier démarrage.

Windows Autopilot prend en charge plusieurs scénarios, qui sont utilisés avec la cogestion :

- Les utilisateurs peuvent effectuer leurs propres déploiements de nouveaux appareils dans Active Directory avec une jointure hybrid Azure AD ou Azure Active Directory (Azure AD)  

- Vous pouvez configurer de déploiement automatique de nouveaux déploiements d’appareil dans Azure AD pour les appareils partagés et les bornes  

- Avec Autopilot Windows pour les périphériques existants, utilisez Configuration Manager pour migrer un périphérique existant à partir de Windows 7 et Active Directory pour Windows 10 et Azure AD  

Dans la vidéo suivante, responsable de programme senior Danny Guillory et responsable de programme principal Andrew McMurray discuteront et de démonstration Windows Autopilot avec la cogestion :

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Avantages

Lorsque vous utilisez la cogestion et Autopilot ensemble, vous vous assurer que les nouveaux appareils pénétrer dans votre réseau se retrouvent dans le même état de gestion. Dans cette configuration, les appareils sont inscrits dans Intune et qu’un client Configuration Manager.  Il vous permet d’utiliser le nouveau modèle d’approvisionnement Windows 10 et vous aide à éliminer la nécessité de créer, gérer et mettre à jour les images de système d’exploitation personnalisés. 

Dans tous ces scénarios, vous pouvez automatiquement [activer la cogestion](/sccm/comanage/how-to-prepare-win10) par Intune. Cette automatisation aide avec le processus d’approvisionnement et de gestion continue de l’appareil.

Avec Autopilot, vous n’avez pas besoin à vous soucier des images et des pilotes. Concentrez-vous sur l’approvisionnement des appareils par ce processus automatisé à l’aide d’Intune et Configuration Manager via la cogestion.


Voici comment l’utilisation conjointe de cogestion et Autopilot peut vous aider à dès maintenant :

#### <a name="reduce-time-costs-and-complexity"></a>Réduire le temps, les coûts et la complexité
Windows Autopilot utilise la version optimisée d’OEM de Windows 10 qui est préinstallé sur l’appareil. Cette configuration économise les organisations l’effort d’avoir à gérer des images personnalisées et les pilotes pour chaque modèle d’appareil en cours d’utilisation. Au lieu de la réinitialisation de l’appareil, transformer l’installation existante de Windows 10 dans un état « prêt à l’emploi ». Il applique les paramètres et les stratégies, installe les applications et modifie l’édition de Windows 10. Par exemple, la mise à niveau à partir de Windows 10 Professionnel vers Windows 10 entreprise afin que vous pouvez prendre en charge des fonctionnalités avancées.

#### <a name="improve-the-user-experience"></a>Améliorer l’expérience utilisateur
La meilleure expérience utilisateur entraîne le moins de perturbations et leur permet de revenir à se concentrer sur leur travail. Windows Autopilot offre une approche simple pour aider vos utilisateurs à configurer rapidement avec quelques clics et leurs informations d’identification Azure AD. Pour de nombreuses organisations avec un grand champ des employés distants, utilisez Windows Autopilot pour expédier des nouveaux appareils directement auprès du fabricant.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Permet de migrer des appareils existants de Windows 7 vers Windows 10 Autopilot et Configuration Manager
Avec Autopilot Windows pour les périphériques existants, vous créez un fichier de configuration et déployez avec une séquence de tâches de Configuration Manager. Ce processus migre aisément des appareils existants à partir de Windows 7 vers Windows 10. Vous utilisez une image de la signature Windows 10 dans Configuration Manager et puis l’appliquer à l’appareil Windows 7 existant avec la configuration Autopilot. Lorsque l’utilisateur commence l’appareil, ils utilisent le processus d’intégration pilotée par l’utilisateur Autopilot.

Voici les étapes pour Autopilot pour les périphériques existants :

![Vue d’ensemble du processus pour Windows Autopilot pour les périphériques existants](media/autopilot-for-existing-devices.png)

1. Déployer une stratégie de groupe pour rediriger des dossiers connus sur OneDrive
2. Générer un fichier de configuration Autopilot
3. Déployer la séquence de tâches pour mettre à niveau vers Windows 10
4. Machine Windows 10 traverse Autopilot au premier démarrage

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernisation de provisionnement des appareils pour tous les types de traitements
Avec Autopilot, vous pouvez désormais fournir un déploiement de système d’exploitation mains libres pour les appareils sans pilote ou d’appareils partagés à l’aide du mode de déploiement automatique. Ce programme d’installation répond aux besoins de vos différents types de traitements. En outre, la fonction Windows Autopilot Reset permet de s’assurer que la préparation d’un appareil à un nouvel utilisateur est simple et facile. Ce processus simplifie ce qui est traditionnellement une tâche difficile lorsque vous avez saisonnières ou le contrat de travailleurs. 



## <a name="case-study"></a>Étude de cas

La société de transport ferroviaire et la logistique allemand DB Shenker utilise Autopilot pour améliorer la productivité et de libérer ses équipes informatiques de travailler sur les tâches quotidiennes de prise en charge. Shenker a détachés d’imagerie traditionnel et remplacé par la mise en service via le cloud. Ils utilisent maintenant Azure AD join et Intune pour être opérationnel rapidement des nouveaux appareils. 

Au lieu que leur temps de déchets télétravailleurs en déplacement vers un emplacement avec les services informatiques, Shenker utilise désormais Windows Autopilot. Elles sont fournies dans leur matériel travailleurs directement auprès du fabricant à leur bureau local. Le processus de travail est le nouvel appareil connecté à internet, et ils se connectent avec leurs informations d’identification Azure AD. L’appareil, puis se connecte aux applications et services de ce Schenker assigne de service informatique pour le profil d’utilisateur individuels.

Pour plus d’informations, consultez [cabinet de logistique Global centralise informatique, regroupe des employés avec un espace de travail numérique moderne](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10).



## <a name="value-proposition"></a>Proposition de valeur

Créez la satisfaction de votre organisation en créant une meilleure expérience utilisateur pour vos utilisateurs. Utiliser Windows Autopilot pour réduire les coûts. Libérez votre temps pour vous concentrer sur d’autres projets d’optimiser l’impact de votre organisation et la valeur.



## <a name="configure"></a>Configurer

Pour plus d’informations, consultez [appareils Windows de s’inscrire dans Intune à l’aide de Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot).

