---
title: Activer la cogestion
titleSuffix: Configuration Manager
description: Activer rapidement la cogestion dans Configuration Manager pour obtenir une valeur immédiate.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 8fac7ac5-96a3-4ec1-85cb-623b26bf5b1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 37dce37551627394da2630fa591a3c803ae8343f
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754939"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Comment activer la cogestion dans Configuration Manager

Lorsque vous activez la cogestion, vous pouvez obtenir une valeur immédiate. Une fois que vous êtes prêt, vous pouvez ensuite démarrer transition des charges de travail en fonction des besoins de votre environnement.

Assurez-vous que les conditions préalables de cogestion sont configurés avant de commencer ce processus. Pour plus d’informations, consultez [Prérequis](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Processus

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**. Cliquez sur **Configurer la cogestion** dans le ruban pour ouvrir l’**Assistant Intégration de la cogestion**.  

2. Sur le **abonnement** page de l’Assistant, sélectionnez **Sign In**. Connectez-vous à votre locataire Intune, puis sélectionnez **Suivant**.  

3. Sur le **activation** page, choisissez votre **inscription automatique dans Intune** définition, soit **pilote** ou **tous les**.   

    Cette action permet l’inscription automatique des clients dans Intune pour les clients Configuration Manager existants. Lorsque vous choisissez **Pilote**, seuls les clients Configuration Manager membres du regroupement pilote sont automatiquement inscrits à Intune. Cette option vous permet d’activer la cogestion sur un sous-ensemble de clients pour tester initialement la cogestion et la déployer au moyen d’une approche progressive.  

    > [!Note]  
    > À compter de la version 1806, l’inscription automatique n’est pas immédiate pour tous les clients. Ce comportement permet une mise à l’échelle de l’inscription plus adaptée pour les environnements de grande taille. Configuration Manager rend aléatoire l’inscription en fonction du nombre de clients. Par exemple, si votre environnement comporte 100 000 clients, quand vous activez ce paramètre, l’inscription se produit sur plusieurs jours.<!--1358003-->  

    Si vous avez des périphériques basés sur internet qui sont déjà inscrits dans Intune, copiez la ligne de commande sur cette page. Vous pouvez utiliser cette ligne de commande pour installer le client Configuration Manager en tant qu’application dans Intune.

4. Dans la page **Charges de travail**, de chaque charge de travail, choisissez le groupe d’appareils concerné par la gestion avec Intune. Pour plus d’informations, consultez [charges de travail](/sccm/comanage/workloads).  

    Si vous souhaitez uniquement activer la cogestion, vous n’avez pas besoin de basculer les charges de travail maintenant. Vous pouvez basculer les charges de travail plus tard. Pour plus d’informations, consultez [comment basculer des charges de travail](/sccm/comanage/how-to-switch-workloads).  

    Le paramètre **Intune pilote** bascule la charge de travail associée uniquement pour les appareils inclus dans le regroupement pilote. Le paramètre **Intune** bascule la charge de travail associée pour tous les appareils Windows 10 cogérés.  

    > [!Important] 
    > Avant de basculer des charges de travail, assurez-vous que vous puissiez correctement configurez et déployez la charge de travail correspondant dans Intune. Assurez-vous que les charges de travail sont toujours gérées par l’un des outils de gestion de vos appareils.  

5. Sur le **intermédiaire** page, configurez les paramètres suivants :  

    - **Pilote** : Le groupe pilote contient un ou plusieurs regroupements que vous sélectionnez. Utilisez ce groupe dans le cadre de votre déploiement progressif de la cogestion. Commencez par un regroupement test peu volumineux, puis ajoutez d’autres regroupements à ce groupe pilote au fur et à mesure que vous déployez la cogestion pour d’autres utilisateurs et appareils. Vous pouvez modifier les regroupements dans le groupe pilote à tout moment.  

    - **Production** : Configurez le **Groupe d’exclusions** avec un ou plusieurs regroupements. Les appareils membres d’une des collections de ce groupe sont exclus de l’utilisation de la cogestion.  

6. Pour activer la cogestion, terminez l’Assistant.  



## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez activé la cogestion, consultez les articles suivants pour la valeur immédiate, que vous pouvez obtenir dans votre environnement :

- [Accès conditionnel](/sccm/comanage/quickstart-conditional-access)  

- [Actions à distance à partir d’Intune](/sccm/comanage/quickstart-remote-actions)  

- [Intégrité du client](/sccm/comanage/quickstart-client-health)  
