---
title: Définitions de logiciels malveillants pour Endpoint Protection
titleSuffix: Configuration Manager
description: Apprenez à configurer les mises à jour logicielles Configuration Manager pour remettre des mises à jour de définitions aux ordinateurs clients.
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 86452d628d025aea2b797d0ade92a3c2e2fff933
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418575"
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>Utilisation des mises à jour logicielles Configuration Manager pour remettre des mises à jour de définitions

*S’applique à : System Center Configuration Manager (Current Branch)*


 Vous pouvez configurer des mises à jour logicielles Configuration Manager pour remettre des mises à jour de définitions aux ordinateurs clients. Pour cela, vous devez configurer des règles de déploiement automatique. Avant de commencer à créer des règles de déploiement automatique, vérifiez que vous avez configuré des mises à jour logicielles Configuration Manager. Pour plus d’informations, consultez [Présentation des mises à jour logicielles dans System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).

> [!NOTE]
>  Cette procédure s’applique uniquement aux éléments qui doivent être configurés spécifiquement pour Endpoint Protection. Pour plus d’informations sur l’Assistant Création d’une règle de déploiement automatique, consultez [Déployer automatiquement des mises à jour logicielles](/sccm/sum/deploy-use/automatically-deploy-software-updates).

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>Pour configurer une règle de déploiement automatique pour fournir des mises à jour de définition

1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.

2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Mises à jour logicielles**, puis cliquez sur **Règles de déploiement automatique**.

3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Créer une règle de déploiement automatique**.

4. Sur la page **Général** de l' **Assistant Création d'une règle de déploiement automatique**, spécifiez les informations suivantes :

   -   **Nom** : entrez un nom unique pour la règle de déploiement automatique.

   -   **Regroupement** : sélectionnez le regroupement d'ordinateurs clients sur lesquels vous voulez déployer les mises à jour de définitions.

       > [!NOTE]
       >  Vous ne pouvez pas déployer des mises à jour de définition dans un regroupement d'utilisateurs.

5. Cliquez sur **Ajouter à un groupe de mises à jour logicielles existant**.

6. Vérifiez que la case  **Activer le déploiement après l’exécution de cette règle** est cochée, puis cliquez sur **Suivant**.

7. Sur la page **Paramètres de déploiement** de l'Assistant, dans la liste **Niveau de détail** , sélectionnez **Minimal**, puis cliquez sur **Suivant**.

   > [!NOTE]
   >  Dans la liste **Niveau de détail**, sélectionnez **Minimale** (Configuration Manager sans Service Pack) ou **Seulement les messages d’erreur** (Configuration Manager). Cette opération réduit le nombre de messages d’état retournés par le déploiement de définitions. Cette configuration permet de réduire les traitements du processeur sur les serveurs Configuration Manager.

8. Dans la liste **Filtres de propriétés** , sélectionnez la case à cocher **Classification des mises à jour** .

9. Dans la liste **Critères de recherche**, cliquez sur **<éléments à rechercher\>**. Ensuite, dans la boîte de dialogue **Critères de recherche** , dans la liste **Spécifiez la valeur à rechercher** , sélectionnez **Mises à jour de définitions**.

10. Cliquez sur **OK** pour fermer la boîte de dialogue **Critères de recherche** .

11. Dans la liste **Filtres de propriétés** , cochez la case **Produit** .

12. Dans la liste **Critères de recherche**, cliquez sur **<éléments à rechercher\>**. Puis, dans la boîte de dialogue **Critères de recherche** , dans la liste **Spécifiez la valeur à rechercher** , sélectionnez **Forefront Endpoint Protection 2010** pour Windows 8.1 et les versions antérieures, ou **Windows Defender** pour Windows 10 et les versions ultérieures.

13. Cliquez sur **OK** pour fermer la boîte de dialogue **Critères de recherche** , puis cliquez sur **Suivant**.

14. Si vous le souhaitez, vous pouvez filtrer les mises à jour remplacées.   Pour cela :
    1.  Dans la liste **Filtres de propriétés** , cochez la case **Remplacé** .
    2.  Dans la liste **Critères de recherche**, cliquez sur **<éléments à rechercher\>**. Ensuite, dans la boîte de dialogue **Critères de recherche** , dans la liste **Spécifiez la valeur à rechercher** , sélectionnez **on**.  <br><br>

15. Cliquez sur **OK** pour fermer la boîte de dialogue **Critères de recherche** , puis cliquez sur **Suivant**.

16. Dans la page **Calendrier d’évaluation** de l’Assistant, sélectionnez **Exécuter la règle selon un calendrier**, puis configurez le calendrier de téléchargement des mises à jour de définition. Définissez au minimum la règle pour qu’elle s’exécute deux heures après chaque synchronisation de point de mise à jour logicielle. Cliquez sur **Suivant**.

17. Sur la page **Calendrier de déploiement** de l'Assistant, configurez les paramètres suivants :

    -   **Heure basée sur** : sélectionnez **UTC** si vous souhaitez que tous les clients de la hiérarchie installent les dernières définitions en même temps. L’heure d’installation réelle varie dans une plage de deux heures. Il est recommandé de définir ce paramètre.

    -   **Temps disponible du logiciel** : spécifiez le temps disponible pour le déploiement qui est créé par cette règle. L’heure spécifiée doit être au moins une heure après l’exécution de la règle de déploiement automatique. Cela permet de garantir que le contenu a suffisamment de temps pour être répliqué sur les points de distribution de votre hiérarchie. Certaines mises à jour de définition peuvent également inclure des mises à jour du moteur anti-programme malveillant et peuvent nécessiter plus de temps pour atteindre les points de distribution.

    -   **Échéance de l’installation** : Sélectionnez **dès que possible**.

        > [!NOTE]
        >  Les échéances des mises à jour logicielles varient sur une période de deux heures pour empêcher que tous les clients demandent une mise à jour en même temps.

18. Cliquez sur **Suivant**.

19. Dans la page **Expérience utilisateur** de l’Assistant, dans la liste **Notifications à l’utilisateur** , sélectionnez **Masquer dans le Centre logiciel et toutes les notifications**.   Cette opération garantit que les mises à jour de définition s’installent en mode silencieux. Cliquez sur **Suivant**.

20. Dans la page **Alertes** de l’Assistant, vous n’avez pas à configurer d’alertes. Dans Configuration Manager, Endpoint Protection génère les alertes qui peuvent être nécessaires. Cliquez sur **Suivant**.

21. Dans la page **Paramètres de téléchargement** de l’Assistant, sélectionnez le comportement de téléchargement des mises à jour approprié, puis cliquez sur **Suivant**.

22. Sur la page **Package de déploiement** de l'Assistant, sélectionnez un package de déploiement existant ou créez un package de déploiement contenant les fichiers de mise à jour logicielle associés à la règle.

    > [!NOTE]
    >  Envisagez de placer les mises à jour de définition dans un package qui ne contient pas d’autres mises à jour logicielles. Cette stratégie garantit une taille réduite du package de mise à jour de définition, ce qui permet de le répliquer plus rapidement sur les points de distribution.

23. Dans la page **Points de distribution** de l’Assistant, sélectionnez un ou plusieurs points de distribution vers lesquels le contenu de ce package sera copié, puis cliquez sur **Suivant**.

24. Dans la page **Emplacement de téléchargement** de l’Assistant, sélectionnez **Télécharger les mises à jour logicielles depuis Internet**, puis cliquez sur **Suivant**.

25. Dans la page **Sélection de la langue** de l’Assistant, sélectionnez chaque version linguistique des mises à jour à télécharger, puis cliquez sur **Suivant**.

26. Terminez l'Assistant Création d'une règle de déploiement automatique.

27. Vérifiez que la nouvelle règle figure dans le nœud **Règles de déploiement automatique** de la console Configuration Manager.


> [!div class="button"]
> [Étape suivante >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Retour >](endpoint-configure-alerts.md)
