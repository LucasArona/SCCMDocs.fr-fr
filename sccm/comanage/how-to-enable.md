---
title: Activer la cogestion
titleSuffix: Configuration Manager
description: Activez sans attendre la cogestion dans Configuration Manager pour en tirer des bénéfices immédiats.
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
ms.sourcegitcommit: 9aebc20b25cdef0af908918ccfd791f3264a5d94
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "56754939"
---
# <a name="how-to-enable-co-management-in-configuration-manager"></a>Comment activer la cogestion dans Configuration Manager

Lorsque vous activez la cogestion, vous pouvez en tirer des bénéfices immédiats. Dès que vous êtes prêt, vous pouvez commencer la transition des charges de travail de votre environnement.

Assurez-vous que les prérequis de cogestion sont configurés avant de commencer cette procédure. Pour plus d’informations, consultez [Prérequis](/sccm/comanage/overview#prerequisites).



## <a name="process"></a>Processus

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**. Cliquez sur **Configurer la cogestion** dans le ruban pour ouvrir l’**Assistant Intégration de la cogestion**.  

2. Dans la page **Abonnement** de l’Assistant, sélectionnez **Se connecter**. Connectez-vous à votre locataire Intune, puis sélectionnez **Suivant**.  

3. Dans la page **Activation**, choisissez votre paramètre **Inscription automatique dans Intune**, **Pilote** ou **Tout**.   

    Cette action permet d’inscrire automatiquement dans Intune les clients Configuration Manager existants. Lorsque vous choisissez **Pilote**, seuls les clients Configuration Manager membres du regroupement pilote sont automatiquement inscrits à Intune. Cette option vous permet d’activer la cogestion sur un sous-ensemble de clients pour tester initialement la cogestion et la déployer au moyen d’une approche progressive.  

    > [!Note]  
    > À compter de la version 1806, l’inscription automatique n’est pas immédiate pour tous les clients. Ce comportement permet une mise à l’échelle de l’inscription plus adaptée pour les environnements de grande taille. Configuration Manager rend aléatoire l’inscription en fonction du nombre de clients. Par exemple, si votre environnement comporte 100 000 clients et si vous activez ce paramètre, l’inscription prendra plusieurs jours.<!--1358003-->  

    Si vous avez des appareils basés sur Internet qui sont déjà inscrits dans Intune, copiez la ligne de commande sur cette page. Vous pouvez utiliser cette ligne de commande pour installer le client Configuration Manager en tant qu’application dans Intune.

4. Dans la page **Charges de travail**, de chaque charge de travail, choisissez le groupe d’appareils concerné par la gestion avec Intune. Pour plus d’informations, consultez [Charges de travail](/sccm/comanage/workloads).  

    Si vous souhaitez uniquement activer la cogestion, vous n’avez pas besoin de basculer les charges de travail maintenant. Vous pouvez les basculer plus tard. Pour plus d’informations, consultez [Guide pratique pour basculer les charges de travail](/sccm/comanage/how-to-switch-workloads).  

    Le paramètre **Intune pilote** bascule la charge de travail associée uniquement pour les appareils inclus dans le regroupement pilote. Le paramètre **Intune** bascule la charge de travail associée pour tous les appareils Windows 10 cogérés.  

    > [!Important] 
    > Avant de basculer des charges de travail, vérifiez que vous avez correctement configuré et déployé la charge de travail correspondante dans Intune. Assurez-vous que les charges de travail sont toujours gérées par l’un des outils de gestion de vos appareils.  

5. Dans la page **Préparation**, configurez les paramètres suivants :  

    - **Pilote** : Le groupe pilote contient un ou plusieurs regroupements que vous sélectionnez. Utilisez ce groupe dans le cadre de votre déploiement progressif de la cogestion. Commencez par un regroupement test peu volumineux, puis ajoutez d’autres regroupements à ce groupe pilote au fur et à mesure que vous déployez la cogestion pour d’autres utilisateurs et appareils. Vous pouvez modifier les regroupements dans le groupe pilote à tout moment.  

    - **Production** : Configurez le **Groupe d’exclusions** avec un ou plusieurs regroupements. Les appareils membres d’une des collections de ce groupe sont exclus de l’utilisation de la cogestion.  

6. Pour activer la cogestion, terminez l’Assistant.  



## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez activé la cogestion, consultez les articles suivants sur les bénéfices immédiats que vous pouvez obtenir dans votre environnement :

- [Accès conditionnel](/sccm/comanage/quickstart-conditional-access)  

- [Actions à distance à partir d’Intune](/sccm/comanage/quickstart-remote-actions)  

- [Intégrité du client](/sccm/comanage/quickstart-client-health)  
