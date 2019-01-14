---
title: MDM hybride avec Microsoft Intune
titleSuffix: Configuration Manager
description: Découvrez la gestion des appareils mobiles (MDM) hybride avec Configuration Manager et Microsoft Intune.
ms.date: 11/02/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84dfc33fe79f5eb4d5397505a12052b8e92aebf
ms.sourcegitcommit: a3cec96a771eed69e58a29917d1a3fe1a5fb2e73
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/14/2019
ms.locfileid: "54250610"
---
# <a name="hybrid-mdm-with-configuration-manager-and-microsoft-intune"></a>MDM hybride avec Configuration Manager et Microsoft Intune

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Important]  
> Depuis le 14 août 2018, la gestion hybride des appareils mobiles est une [fonctionnalité déconseillée](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).
> <!--Intune feature 2683117-->  
> Depuis son lancement sur Azure il y a plus d’un an, Intune a ajouté des centaines de nouvelles fonctionnalités demandées par les clients et de services de premier plan. Il propose à présent bien plus de fonctionnalités que celles de la gestion des appareils mobiles (MDM) hybride. Intune sur Azure offre une expérience d’administration simplifiée et mieux intégrée pour répondre à vos besoins de mobilité d’entreprise.
> 
> Par conséquent, la plupart des clients choisissent Intune sur Azure de préférence à la gestion MDM hybride. Le nombre de clients qui utilisent la gestion MDM hybride continue de diminuer au fur et à mesure des migrations vers le cloud. C’est pourquoi, le 1er septembre 2019, Microsoft retirera l’offre de service de gestion MDM hybride. Prévoyez une [migration vers Intune sur Azure](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa) pour vos besoins de gestion MDM. 
> 
> Cette modification n’affecte ni Configuration Manager sur site ni la [cogestion pour les appareils Windows 10](/sccm/comanage/overview). Si vous ne savez pas si vous utilisez la gestion MDM hybride, accédez à l’espace de travail **Administration** de la console Configuration Manager, développez **Services cloud**, puis cliquez sur **Abonnements Microsoft Intune**. Si un abonnement Microsoft Intune est configuré, c’est le signe que votre locataire est configuré pour la gestion MDM hybride.
> 
> **Comment cela m’affecte-t-il ?**
> 
> - Microsoft prendra en charge votre utilisation de la gestion MDM hybride pour l’année à venir. La fonctionnalité continuera de recevoir les principaux correctifs de bogues. Microsoft gèrera les fonctionnalités existantes sur les nouvelles versions des systèmes d’exploitation, comme l’inscription sur iOS 12. Il n’y aura pas de nouvelles fonctionnalités pour la gestion MDM hybride.  
> 
> - Si vous migrez vers Intune sur Azure avant la fin de l’offre de gestion MDM hybride, il ne devrait y avoir aucun impact sur l’utilisateur final.  
> 
> - La gestion des licences reste inchangée. Les licences Intune sur Azure sont incluses avec la gestion MDM hybride.  
> 
> - Les fonctionnalités liées à l’accès conditionnel et à la gestion MDM locale dans Configuration Manager ne sont pas dépréciées. Les changements qui seront prochainement apportés à Configuration Manager permettront à ces fonctionnalités de fonctionner sans gestion MDM hybride. 
> 
> - Le 1er septembre 2019, les appareils MDM hybride restants ne recevront plus ni mises à jour des stratégies et des applications ni mises à jour de sécurité.  
> 
> **Que faire pour se préparer à ce changement ?**
> 
> - Commencez à planifier votre migration de la gestion MDM sur la console ConfigMgr vers Azure. De nombreux clients, de même que l’équipe informatique de Microsoft, sont passés par ce processus. Pour plus d’informations, voir [Étude de cas Microsoft](https://aka.ms/Intune_MSFT).  
> 
> - Étudiez la documentation et les outils suivants pour simplifier le processus de passage de la gestion MDM hybride vers Intune sur Azure :  
>     - [Importer les données de Configuration Manager dans Microsoft Intune](/sccm/mdm/deploy-use/migrate-import-data)  
>     - [Faire migrer des utilisateurs et appareils MDM hybrides vers la version autonome d’Intune](/sccm/mdm/deploy-use/migrate-hybridmdm-to-intunesa)  
> 
> - Pour obtenir de l’aide, contactez votre partenaire d’enregistrement ou FastTrack. [FastTrack pour Microsoft 365](https://aka.ms/hybrid_fasttrack) peut vous accompagner dans votre migration de la gestion MDM hybride vers Intune sur Azure. 
> 
> Pour plus d’informations, voir le [billet de blog du support Intune](https://aka.ms/hybrid_notification).



Avec la fonctionnalité de gestion des appareils mobiles (MDM) hybride de Configuration Manager, gérez les appareils iOS, Windows et Android. Toutes les tâches de gestion sont administrées à partir de la console Configuration Manager, où vous effectuez toutes vos autres tâches de gestion de manière intégrée et transparente avec le service en ligne de Microsoft Intune via Internet. Utilisez Configuration Manager pour permettre aux utilisateurs d’accéder aux ressources de l’entreprise sur leurs appareils de manière sécurisée et gérée. Avec la gestion des appareils, vous protégez les données d’entreprise tout en permettant aux utilisateurs d’inscrire leurs appareils personnels ou d’entreprise pour accéder aux données d’entreprise. 

Cet article part du principe que vous utilisez Configuration Manager pour gérer les ordinateurs. Il suppose également que vous envisagez d’étendre la console Configuration Manager avec Intune pour gérer les appareils mobiles. 



## <a name="capabilities"></a>Fonctionnalités

La gestion MDM hybride gère les fonctionnalités de gestion suivantes sur les appareils :

-   Mise hors service et réinitialisation des appareils  

-   Configuration des paramètres de compatibilité tels que les mots de passe, la sécurité, l'itinérance, le chiffrement et la communication sans fil  

-   Déploiement d’applications métier sur les appareils  

-   Déploiement d'applications sur des appareils qui se connectent au Windows Store, au Windows Phone Store, à l'App Store ou à Google Play  

-   Collecte de l'inventaire matériel  

-   Collecte de l'inventaire logiciel à l'aide de rapports intégrés  

Pour en savoir plus sur les nouvelles fonctionnalités disponibles pour la gestion des appareils mobiles (MDM) hybride, consultez [Nouvelles fonctionnalités pour la gestion des appareils mobiles (MDM) hybride](/sccm/mdm/understand/whats-new-in-hybrid-mobile-device-management).



## <a name="hybrid-mdm-enrollment"></a>Inscription à la gestion MDM hybride

Les appareils peuvent être gérés à l’aide de la gestion hybride s’ils ont été préalablement inscrits auprès du service. Le processus d’inscription des appareils dépend du type et de la propriété de l’appareil, ainsi que du niveau de gestion souhaité.

- **« Apportez votre propre appareil » (BYOD)**: Les utilisateurs inscrivent leurs téléphones personnels, tablettes ou PC  

- **Appareil d’entreprise (COD)**: Scénarios de gestion telles que la réinitialisation à distance, les appareils partagés ou affinité utilisateur pour un appareil  

- Si vous utilisez [Exchange ActiveSync](/sccm/mdm/plan-design/device-enrollment-methods#mobile-device-management-with-exchange-activesync-and-configuration-manager) (localement ou hébergé dans le cloud), vous pouvez choisir la gestion Intune simple sans inscription. Vous pouvez également gérer des PC Windows à l’aide du [logiciel client Intune](/intune/deploy-use/manage-windows-pcs-with-microsoft-intune).
