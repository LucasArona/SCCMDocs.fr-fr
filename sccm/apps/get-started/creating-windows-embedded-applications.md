---
title: Créer des applications Windows Embedded
titleSuffix: Configuration Manager
description: Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour appareils Windows Embedded.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6374fa186ab13f3288e218e6670da3ea4ff10f4e
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="create-windows-embedded-applications-with-system-center-configuration-manager"></a>Créer des applications Windows Embedded avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

En plus des autres exigences et procédures System Center Configuration Manager à observer pour créer une application, vous devez aussi prendre en compte les éléments suivants au moment de créer et déployer des applications pour des appareils Windows Embedded.  

## <a name="general-considerations"></a>Considérations générales  

-   Quand vous déployez des applications sur des appareils Windows Embedded activés pour le filtrage d’écriture, vous pouvez spécifier s’il faut désactiver le filtre d’écriture sur l’appareil pendant le déploiement de l’application. Vous pouvez ensuite choisir de redémarrer le filtre d’écriture une fois l’application déployée. Si le filtre d’écriture n’est pas désactivé, le logiciel est déployé sur un segment de recouvrement temporaire. Cela signifie que, sauf si un autre déploiement force la conservation des modifications, le logiciel n’est plus installé lors du redémarrage de l’appareil.  

-   Lorsque vous déployez une application sur un appareil Windows Embedded, assurez-vous que l'appareil fait partie des membres d'un regroupement pour lequel une fenêtre de maintenance a été configurée. Cela vous permet de gérer le moment auquel le filtre d'écriture est désactivé et activé et le moment auquel l'appareil redémarre.  

-   Le paramètre qui contrôle le comportement du filtre d’écriture est une case à cocher nommée **Valider les changements à l’échéance ou pendant une fenêtre de maintenance (redémarrage requis)**.  

## <a name="tips-for-deploying-applications"></a>Conseils sur le déploiement d’applications  

**Utilisez les applications obligatoires plutôt que les applications disponibles pour les appareils Windows Embedded dont les filtres d’écriture sont activés.** Comme les utilisateurs ne peuvent pas installer d’applications à partir du Centre logiciel sur un appareil Windows Embedded dont les filtres d’écriture sont activés, déployez toujours les applications ayant pour objet du déploiement la valeur **Obligatoire** et non **Disponible** sur ces appareils. En général, cela ne pose pas de problème, car les ordinateurs qui exécutent un système d’exploitation Windows Embedded n’exécutent souvent qu’une seule application de la même manière pour plusieurs utilisateurs. Ainsi, ces périphériques font l'objet d'une gestion de haut niveau et sont verrouillés par le service informatique de l'entreprise. Les applications requises sont bien adaptées à ce scénario.

 Toutefois, si des utilisateurs exécutent plusieurs applications sur des périphériques Windows Embedded alors que les filtres d'écriture sont activés, pensez à les informer des limitations suivantes :  

-   Les utilisateurs ne peuvent pas installer les logiciels requis à partir du Centre logiciel.  

-   Les utilisateurs ne peuvent pas modifier leurs heures de bureau sous l’onglet Options du Centre logiciel.  

-   Les utilisateurs ne peuvent pas reporter l'installation d'une application requise.  

Par ailleurs, les utilisateurs disposant de droits restreints ne peuvent pas ouvrir une session pendant une période de maintenance si Configuration Manager valide des modifications pour les installations et les mises à jour logicielles. Au cours de cette période, les utilisateurs voient un message indiquant que le périphérique n'est pas disponible pour des raisons de maintenance.  

**Si des applications obligent l’utilisateur à accepter les termes du contrat de licence, ne les déployez pas sur des appareils Windows Embedded dont les filtres d’écriture sont activés.** Quand les filtres d’écriture sont désactivés et que Configuration Manager peut donc installer des logiciels sur les appareils intégrés, les utilisateurs disposant de droits restreints ne peuvent pas ouvrir de session sur l’appareil. Si l'installation oblige l'utilisateur à accepter les termes du contrat de licence, l'installation échoue, car cette opération est impossible. Si l'installation nécessite l'intervention de l'utilisateur, veillez à ne pas déployer des logiciels sur des périphériques Windows Embedded. Pour filtrer ces systèmes d’exploitation, vous pouvez utiliser la liste Plateformes applicables.  
