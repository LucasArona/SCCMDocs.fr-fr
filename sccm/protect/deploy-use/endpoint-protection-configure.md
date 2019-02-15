---
title: Configurer Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment configurer Configuration Manager pour mettre à jour et distribuer les définitions de programmes malveillants pour Windows Defender.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 89eee933d9845ae86bcc8d008045b669d104d03d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56156727"
---
# <a name="configure-endpoint-protection"></a>Configurer Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant d’utiliser Endpoint Protection pour gérer la sécurité et les programmes malveillants sur les ordinateurs client Configuration Manager, vous devez effectuer les étapes de configuration décrites dans cet article.  

## <a name="how-to-configure-endpoint-protection-in-configuration-manager"></a>Comment configurer Endpoint Protection dans Configuration Manager  
 Endpoint Protection comporte des dépendances externes et des dépendances internes à Configuration Manager.  

### <a name="steps-to-configure-endpoint-protection-in-configuration-manager"></a>Procédure pour configurer Endpoint Protection dans Configuration Manager  
 Utilisez le tableau suivant pour les étapes, les détails et les informations complémentaires relatifs à la configuration d’Endpoint Protection.  

> [!IMPORTANT]  
>  Si vous gérez Endpoint Protection sur des ordinateurs Windows 10, vous devez configurer Configuration Manager pour mettre à jour et distribuer les définitions de programmes malveillants pour Windows Defender. Windows Defender est inclus dans Windows 10, mais vous devez encore installer SCEPInstall et configurer les paramètres client personnalisés pour Endpoint Protection (comme décrit dans l’**étape 5** ci-dessous). </br> </br>
> À compter de Configuration Manager 1802, l’agent Endpoint Protection (SCEPInstall) n’a pas besoin d’être installé sur les appareils Windows 10. S’il est déjà installé sur les appareils Windows 10, Configuration Manager ne le supprime pas. Les administrateurs peuvent supprimer l’agent Endpoint Protection sur les appareils Windows 10 qui exécutent au moins la version client 1802. Il est possible que SCEPInstall.exe soit toujours dans C:\Windows\ccmsetup sur certaines machines, mais il ne doit pas être téléchargé sur de nouvelles installations de client. Les paramètres clients personnalisés pour Endpoint Protection (**Étape 5** ci-dessous) restent obligatoires. <!--503654-->

|Étapes|Détails|  
|-----------|-------------|  
|**Étape 1** : [Créer un rôle de système de site de point Endpoint Protection](endpoint-protection-site-role.md)|Pour que vous puissiez utiliser Endpoint Protection, le rôle de système de site de point Endpoint Protection doit avoir été installé. Il doit être installé sur un seul serveur de système de site et en haut de la hiérarchie sur un site d'administration centrale ou un site principal autonome. |  
|**Étape 2** : [Configurer des alertes pour Endpoint Protection](endpoint-configure-alerts.md)|Les alertes signalent à l'administrateur des événements spécifiques qui se produisent, tels qu'une infection par un logiciel malveillant. Les alertes s'affichent dans le nœud **Alertes** de l'espace de travail **Surveillance** ou éventuellement elles peuvent être envoyées par courrier électronique à des utilisateurs donnés. |  
|**Étape 3** : [Configurer les sources de mise à jour des définitions pour les clients Endpoint Protection](endpoint-definition-updates.md)|Endpoint Protection peut être configuré pour utiliser diverses sources de téléchargement des mises à jour des définitions. |  
|**Étape 4 :** [Configurer la stratégie de logiciel anti-programme malveillant par défaut et créer des stratégies de logiciel anti-programme malveillant personnalisées](endpoint-antimalware-policies.md)|La stratégie de logiciel anti-programme malveillant par défaut est appliquée au moment de l’installation du client Endpoint Protection. Les stratégies personnalisées que vous avez déployées sont appliquées par défaut dans les 60 minutes consécutives au déploiement du client. Vérifiez que vous avez configuré des stratégies anti-programme malveillant avant de déployer le client Endpoint Protection. |  
|**Étape 5** : [Configurer des paramètres client personnalisés pour Endpoint Protection](endpoint-protection-configure-client.md)|Utilisez des paramètres client personnalisés pour appliquer les paramètres configurés pour Endpoint Protection à certains regroupements d’ordinateurs dans la hiérarchie.<br /><br /> Remarque : configurez les paramètres client par défaut pour Endpoint Protection uniquement si vous voulez les appliquer à l’ensemble des ordinateurs de la hiérarchie. |  
