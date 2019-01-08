---
title: Surveiller les profils de certificat
titleSuffix: Configuration Manager
description: Découvrez comment surveiller l’état de compatibilité des profils de certificat System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 98feaa06-64b1-4e86-a122-93017c97cd4f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d061649744d7a2da37e67d55f3c8b655d18c0aa4
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416790"
---
# <a name="how-to-monitor-certificate-profiles-in-system-center-configuration-manager"></a>Comment surveiller des profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


##  <a name="view-compliance-results-in-the-configuration-manager-console"></a>Afficher les résultats de compatibilité dans la console Configuration Manager  

Pour surveiller la compatibilité des certificats SCEP, n’utilisez pas la console. Utilisez plutôt les [rapports](#view-compliance-results-by-using-reports). 

1. Dans la console Configuration Manager, choisissez **Surveillance**>  **Déploiements**.  

2. Sélectionnez le déploiement du profil de certificat qui vous intéresse.  

3. Examinez les informations de compatibilité de certificat résumées dans la page principale. Pour obtenir des informations plus détaillées, sélectionnez le profil de certificat et, sous l’onglet **Accueil**, dans le groupe **Déploiement**, choisissez **Afficher l’état** pour ouvrir la page **État du déploiement**.  

    La page **État du déploiement** contient les onglets suivants :  

   -   **Conforme** : affiche la compatibilité du profil de certificat en fonction du nombre de ressources concernées. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les utilisateurs qui sont compatibles avec le profil de certificat. Le volet **Détails du bien** affiche également les utilisateurs compatibles avec ce profil. Double-cliquez sur un utilisateur dans la liste pour afficher des informations supplémentaires.  

       > [!IMPORTANT]  
       >  Un profil de certificat n'est pas évalué s'il n'est pas applicable sur un périphérique client. Toutefois, il est retourné comme conforme.  

   -   **Erreur** : affiche une liste de toutes les erreurs pour le déploiement du profil de certificat sélectionné en fonction du nombre de biens concernés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les utilisateurs qui ont généré des erreurs avec ce profil. Lorsque vous sélectionnez un utilisateur, le volet **Détails du bien** affiche les utilisateurs qui sont concernés par le problème sélectionné. Double-cliquez sur un utilisateur dans la liste pour afficher des informations supplémentaires.  

   -   **Non conforme** : affiche une liste de toutes les règles non compatibles au sein du profil de certificat en fonction du nombre de biens concernés. Vous pouvez double-cliquer sur une règle pour créer un nœud temporaire sous le nœud **Utilisateurs** de l'espace de travail **Ressources et Conformité** . Ce nœud contient tous les utilisateurs qui ne sont pas compatibles avec ce profil. Lorsque vous sélectionnez un utilisateur, le volet **Détails du bien** affiche les utilisateurs qui sont concernés par le problème sélectionné. Double-cliquez sur un utilisateur de la liste pour afficher des informations supplémentaires sur le problème.  

   -   **Inconnu** : affiche une liste de tous les utilisateurs qui n'ont pas signalé de compatibilité pour le déploiement du profil de certificat sélectionné avec l'état du client actuel des périphériques.  

4. Dans la page **État du déploiement**, examinez les informations détaillées sur la compatibilité du profil de certificat déployé. Un nœud temporaire est créé sous le nœud **Déploiements** qui vous aide à retrouver rapidement ces informations.  

    L'état de l'inscription du certificat s'affiche sous la forme d'un numéro. Le tableau suivant permet de comprendre ce que chaque numéro signifie :  


   | État de l'inscription |                                                                                                                   Description                                                                                                                   |
   |-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
   |    0x00000001     |                                                                                         L'inscription a réussi et le certificat a été émis.                                                                                          |
   |    0x00000002     |                                                                    La demande a été soumise et l'inscription est en attente, ou la demande a été émise hors bande.                                                                    |
   |    0x00000004     |                                                                                                          L'inscription doit être différée.                                                                                                           |
   |    0x00000010     |                                                                                                               Une erreur s'est produite.                                                                                                                |
   |    0x00000020     |                                                                                                        L'état de l'inscription est inconnu.                                                                                                        |
   |    0x00000040     | Les informations d'état ont été ignorées. Cela peut se produire si une autorité de certification HYPERLINK "<http://msdn.microsoft.com/windows/ms721572>" \l "_security_certification_authority_gly" n’est pas valide ou n’a pas été sélectionnée pour la surveillance. |
   |    0x00000100     |                                                                                                           L'inscription a été refusée.                                                                                                           |

##  <a name="view-compliance-results-by-using-reports"></a>Afficher les résultats de compatibilité à l’aide de rapports

 Les paramètres de compatibilité de System Center Configuration Manager incluent des rapports intégrés que vous pouvez utiliser pour analyser des informations sur les profils de certificat. La catégorie de ces rapports est **Gestion de la conformité et des paramètres**.  

> [!IMPORTANT]  
>  Vous devez utiliser un caractère générique (%) lorsque vous utilisez les paramètres **Filtre de périphérique** et **Filtre d'utilisateur** dans les rapports des paramètres de compatibilité.  

Pour surveiller la compatibilité des certificats SCEP, utilisez les rapports de certificat sous le nœud des rapports **Accès aux ressources de l’entreprise** :  

 -   Historique d'émission des certificats  
 -   Liste de biens dont la date d'expiration des certificats approche  
 -   Liste de biens par état d'émission de certificat  



 Pour plus d’informations sur la configuration de la génération de rapports dans System Center Configuration Manager, consultez [Génération de rapports dans System Center Configuration Manager](../../core/servers/manage/reporting.md).  
