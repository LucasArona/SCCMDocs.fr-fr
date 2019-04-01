---
title: Intégration avec Windows Update for Business dans Windows 10
titleSuffix: Configuration Manager
description: Utilisez Windows Update for Business pour tenir à jour les appareils Windows 10 de votre organisation connectés au service Windows Update.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 03/28/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2929782880971b53be3b6013188f65d50d691c05
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523756"
---
# <a name="integration-with-windows-update-for-business-in-windows-10"></a>Intégration avec Windows Update for Business dans Windows 10

*S’applique à : System Center Configuration Manager (Current Branch)*

Windows Update for Business (WUfB) vous permet de garantir la mise à jour des appareils Windows 10 de votre organisation avec les mécanismes de sécurité et les fonctionnalités Windows les plus récents quand ces appareils se connectent directement au service Windows Update (WU). Configuration Manager peut faire la distinction entre les ordinateurs Windows 10 qui utilisent WUfB et WSUS pour obtenir les mises à jour logicielles.  

>[!WARNING]
> Si vous utilisez cogestion pour vos appareils et que vous avez déplacé la [stratégies Windows Update](/sccm/comanage/workloads#windows-update-policies) à Intune, vos appareils obtiendra leurs [des stratégies de mise à jour de Windows pour les entreprises à partir d’Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Si le client Configuration Manager est toujours installé sur l’appareil cogéré paramètres pour les mises à jour cumulatives et mises à jour de fonctionnalité sont gérés par Intune. Toutefois, par des tiers mise à jour corrective, si activé dans [ **paramètres Client**](/sccm/core/clients/deploy/about-client-settings#enable-third-party-software-updates), est toujours géré par Configuration Manager.  

 Certaines fonctionnalités de Configuration Manager ne sont plus disponibles quand les clients Configuration Manager sont configurés pour recevoir des mises à jour de Windows Update, notamment WUfB ou Windows Insiders :  

-   Rapports de conformité Windows Update :  

    -   Configuration Manager ne sera pas au courant des mises à jour publiées sur Windows Update. Les clients Configuration Manager configurés pour les mises à jour reçues à partir de Windows Update indiquent **inconnu** pour ces mises à jour dans la console Configuration Manager.  

    -   La résolution des problèmes liés à l’état de conformité global est difficile, car l’état **inconnu** concernait uniquement les clients qui n’avaient pas signalé leur état d’analyse à WSUS. Maintenant, il inclut également les clients Configuration Manager qui reçoivent les mises à jour de Windows Update.  

    -   L’accès conditionnel (pour les ressources d’entreprise) basé sur l’état de conformité de mise à jour ne fonctionnera pas comme prévu pour les clients qui reçoivent des mises à jour de Windows Update, car ils ne respecteront jamais la conformité de Configuration Manager.  

    -   La conformité des mises à jour de définition fait partie des rapports de conformité de mise à jour globaux et ne fonctionnera pas non plus comme prévu.  La conformité des mises à jour de définition fait également partie de l’évaluation de l’accès conditionnel.  

-   Les rapports Endpoint Protection globaux pour Defender basés sur l’état de conformité de mise à jour retourneront des résultats incorrects en raison des données d’analyse manquantes.  

-   Configuration Manager ne pourra pas déployer les mises à jour Microsoft, telles qu’Office, Internet Explorer et Visual Studio, sur les clients qui sont connectés à WUfB pour recevoir des mises à jour.  

-   Configuration Manager peut néanmoins déployer les mises à jour tierces publiées dans WSUS et gérées par le biais de Configuration Manager vers les clients qui sont connectés à WUfB pour recevoir des mises à jour. Si vous ne souhaitez pas 3e partie mises à jour pour être installé sur les clients connectés à WUfB, désactivez le paramètre nommé client [activer les mises à jour logicielles sur les clients](/sccm/core/clients/deploy/about-client-settings#software-updates).

-   Le déploiement de client complet Configuration Manager qui utilise l’infrastructure de mises à jour logicielles ne fonctionnera pas pour les clients qui sont connectés à WUfB pour recevoir des mises à jour.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifier les clients qui utilisent WUfB pour les mises à jour de Windows 10  
 Utilisez la procédure suivante qui permet d’identifier les clients qui utilisent WUfB pour obtenir les mises à niveau et les mises à jour de Windows 10. Ensuite, configurez ces clients pour arrêter d’utiliser WSUS pour obtenir les mises à jour, et déployez un paramètre d’agent client pour désactiver le flux de travail des mises à jour logicielles pour ces clients.  

 **Conditions préalables**  

-   Clients qui exécutent Windows 10 Desktop Pro ou Windows 10 Édition Entreprise version 1511 ou ultérieure  

-   [Windows Update for Business](https://technet.microsoft.com/library/mt622730\(v=vs.85\).aspx) est déployé et les clients utilisent WUfB pour obtenir les mises à niveau et les mises à jour Windows 10.  

#### <a name="to-identify-clients-that-use-wufb"></a>Pour identifier les clients qui utilisent WUfB  

1.  Désactivez l’Agent Windows Update, s’il était activé, afin que celui-ci n’effectue pas l’analyse sur WSUS. La clé de Registre suivante peut être définie pour indiquer si l’ordinateur effectue l’analyse sur WSUS ou Windows Update.  Lorsque la valeur est 2, il n’effectue pas l’analyse sur WSUS.  
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**

2.  Il existe un nouvel attribut, **UseWUServer**, sous le nœud **Windows Update** dans l’Explorateur de ressources Configuration Manager.  

3.  Créez un regroupement basé sur l’attribut **UseWUServer** pour tous les ordinateurs connectés via WUFB pour les mises à jour et les mises à niveau.  

4.  Créez un paramètre d’agent client pour désactiver le flux de travail de mise à jour de logiciel. Déployez le paramètre sur le regroupement d’ordinateurs qui sont connectés directement à WUfB.  

5.  Les ordinateurs qui sont gérés via WUFB affichent **Inconnu** dans l’état de conformité et ne sont pas comptabilisés dans le pourcentage de conformité global.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Configuration de Windows Update pour les stratégies d’entreprise de report d’entreprise
<!-- 1290890 -->
À compter de Configuration Manager version 1706, vous pouvez configurer des stratégies de report pour les appareils Windows 10 avec Mises à jour de fonctionnalités ou Mises à jour qualité gérés directement par Windows Update for Business. Vous pouvez gérer les stratégies de report du nouveau nœud **Stratégies Windows Update for Business** sous **Bibliothèque de logiciels** > **Maintenance de Windows 10**.

>[!NOTE] 
>À compter de Configuration Manager version 1802, vous pouvez définir des stratégies de report pour Windows Insider. <!--507201-->Pour plus d’informations sur le programme Windows Insider, consultez [Programme Windows Insider pour les entreprises](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites"></a>Prérequis
-   Windows 10 version 1703 ou ultérieure
-   Les appareils Windows 10 gérés par Windows Update pour Entreprise doivent avoir une connectivité Internet.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Pour créer une stratégie de report Windows Update for Business
1. Dans **Bibliothèque de logiciels** > **Maintenance de Windows 10** > **Mises à jour de Windows pour les stratégies d’entreprise**
2. Sous l’onglet **Accueil**, dans le groupe **Créer**, sélectionnez **Créer une stratégie Windows Update for Business** pour ouvrir l’assistant de création de stratégie Windows Update for Business.
3. Dans la page **Général**, indiquez un nom et une description pour la stratégie.
4. Sur la page **Stratégies de report**, choisissez de différer ou suspendre les mises à jour de fonctionnalités. Les mises à jour de fonctionnalités sont généralement de nouvelles fonctionnalités pour Windows. Après avoir configuré le paramètre **Niveau de préparation de la branche**, vous pouvez définir si et pour quelle durée vous souhaitez différer la réception des fonctionnalités mises à jour après leur disponibilité auprès de Microsoft.
    - **Niveau de préparation de la branche** : définissez la branche pour laquelle l’appareil recevra les mises à jour de Windows (Current Branch ou Current Branch for Business).
    - **Période de report (jours)** : spécifiez le nombre de jours pendant lesquels les mises à jour de fonctionnalités sont différées. Vous pouvez différer la réception de ces mises à jour de fonctionnalités jusqu’à 365 jours après leur publication.
    - **Suspendre le démarrage des mises à jour de fonctionnalités** : choisissez de suspendre la réception des mises à jour de fonctionnalités sur vos appareils jusqu’à 60 jours après la date de suspension des mises à jour. Une fois que le nombre maximal de jours s’est écoulé, la fonctionnalité de pause expirera automatiquement et l’appareil analysera les mises à jour de Windows pour déterminer celles qui sont applicables. Suite à cette analyse, vous pouvez à nouveau suspendre les mises à jour. Vous pouvez reprendre les mises à jour de fonctionnalités en désactivant la case à cocher.   
5. Choisissez de différer ou suspendre les mises à jour de qualité. Les mises à jour de qualité sont généralement des améliorations et correctifs apportés aux fonctionnalités existantes de Windows, et sont généralement publiées le premier mardi de chaque mois, même si la publication peut être effectuée à tout moment par Microsoft. Vous pouvez définir si et pour combien de temps vous souhaitez différer la réception des mises à jour de qualité après leur disponibilité.
    - **Période de report (jours)** : spécifiez le nombre de jours pendant lesquels les mises à jour de qualité sont différées. Vous pouvez différer la réception de ces mises à jour de qualité jusqu’à 30 jours après leur publication.
    - **Suspendre le démarrage des mises à jour de qualité** : choisissez de suspendre la réception des mises à jour de qualité sur vos appareils jusqu’à 35 jours après la date de suspension des mises à jour. Une fois que le nombre maximal de jours s’est écoulé, la fonctionnalité de pause expirera automatiquement et l’appareil analysera les mises à jour de Windows pour déterminer celles qui sont applicables. Suite à cette analyse, vous pouvez à nouveau suspendre les mises à jour. Vous pouvez reprendre les mises à jour de qualité en désactivant la case à cocher.
6. Sélectionnez **Installer les mises à jour à partir d’autres produits Microsoft** pour activer le paramètre de stratégie de groupe qui rend les paramètres de report applicables à Microsoft Update, ainsi qu’aux mises à jour de Windows.
7. Sélectionnez **Inclure les pilotes avec Windows Update** pour mettre à jour automatiquement les pilotes proposés avec les mises à jour de Windows. Si vous désactivez ce paramètre, les mises à jour de pilotes ne sont pas téléchargées à partir des mises à jour de Windows.
8. Terminez l'Assistant pour créer la stratégie de report.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>Pour déployer une stratégie de report Windows Update for Business
1. Dans **Bibliothèque de logiciels** > **Maintenance de Windows 10** > **Mises à jour de Windows pour les stratégies d’entreprise**
2. Sous l’onglet **Accueil** du groupe **Déploiement**, sélectionnez **Déployer la stratégie Windows Update for Business**.
3. Configurez les paramètres suivants :
    - **Stratégie de configuration à déployer** : sélectionnez la stratégie Windows Update for Business que vous souhaitez déployer.
    - **Regroupement**: cliquez sur **Parcourir** pour sélectionner le regroupement dans lequel vous souhaitez déployer la stratégie.
    - **Résoudre les règles non compatibles lorsqu’elles sont prises en charge** : sélectionnez cette option pour résoudre automatiquement toutes les règles qui ne sont pas compatibles pour Windows Management Instrumentation (WMI), le Registre, les scripts et tous les paramètres des appareils mobiles inscrits par Configuration Manager.
    - **Autoriser les corrections en dehors de la fenêtre de maintenance** : si une fenêtre de maintenance a été configurée pour le regroupement vers lequel vous déployez la stratégie, activez cette option pour laisser les paramètres de compatibilité résoudre la valeur en dehors de la fenêtre de maintenance. Pour plus d’informations sur les fenêtres de maintenance, consultez [Guide pratique pour utiliser les fenêtres de maintenance](/sccm/core/clients/manage/collections/use-maintenance-windows).
    - **Générer une alerte** : configure une alerte qui est générée si la compatibilité de la base de référence de configuration est inférieure à un pourcentage spécifié par une date et une heure spécifiques. Vous pouvez également spécifier si vous souhaitez qu'une alerte soit envoyée à System Center Operations Manager.
    - **Délai aléatoire (heures)** : spécifie un délai pour éviter un traitement excessif sur le service d’inscription d’appareils réseau. La valeur par défaut est 64 heures.
    - **Calendrier** : Spécifier le calendrier d’évaluation de la compatibilité par rapport auquel le profil déployé est évalué sur les ordinateurs clients. Il peut s'agir d'un calendrier simple ou d'un calendrier personnalisé. Lorsque l'utilisateur ouvre une session, le profil est évalué par les ordinateurs clients.
4.  Terminez l’assistant pour déployer le profil.
