---
title: Confidentialité des postes de travail Analytique données
titleSuffix: Configuration Manager
description: Analytique de bureau s’engage à la confidentialité des données client
ms.date: 06/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: b5606f15-f589-485c-a599-cdabf1a9e7ac
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: fb109bc126902f4d68b876860e8d5ec3ff514bb8
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67146006"
---
# <a name="desktop-analytics-data-privacy"></a>Confidentialité des postes de travail Analytique données

Analytique de postes de travail a été entièrement validé à la confidentialité des données client, centrage sur ces principes :

- **Transparence :** Nous documenter entièrement les événements de diagnostic de Windows. Passez en revue les avec les équipes de sécurité et de conformité de votre entreprise. La visionneuse de données de Diagnostic Windows vous permet de voir les données de diagnostic envoyées à partir d’un appareil donné. Pour plus d’informations, consultez [présentation de l’afficheur données Diagnostic](https://docs.microsoft.com/windows/configuration/diagnostic-data-viewer-overview).  

- **Contrôle :** Vous contrôlez le niveau de données de diagnostic à partager avec Microsoft. Windows 10, version 1709, ajoute une nouvelle stratégie pour limiter les données de diagnostic améliorées au minimum requis par l’Analytique de bureau.  

- **Sécurité :** Microsoft protège vos données avec chiffrement et une sécurité renforcée.  

- **Approbation :** Microsoft prend en charge les postes de travail Analytique [déclaration de confidentialité](https://privacy.microsoft.com/privacystatement) et [des termes du contrat de Service en ligne](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=46).  



## <a name="diagnostic-data-flow"></a>Flux de données de diagnostic

L’illustration suivante montre les données de diagnostic comment flux à partir d’appareils individuels via le Service de données de Diagnostic, le stockage Azure Log Analytique et à votre espace de travail Analytique de journal :

![Diagramme illustrant le flux de données de diagnostic à partir d’appareils](media/da-data-flow.png)

1. Connectez-vous pour le portail Azure et intégrer à l’Analytique de bureau. Vous créez l’application Azure AD pour se connecter avec le Gestionnaire de Configuration. Lorsque vous configurez l’Analytique de bureau, vous créez un espace de travail Analytique de journal Azure dans l’emplacement de votre choix.  

2. Connecter Configuration Manager et d’inscrire des appareils  

    1. Vous configurez le service de cloud d’Analytique de bureau dans le Gestionnaire de Configuration avec les détails de l’application Azure AD.  

    2. Dans les 15 minutes, Configuration Manager synchronise les regroupements de périphériques et les plans de déploiements avec Analytique de bureau. Il répète ce processus de toutes les heures.  

    3. Configuration Manager définit l’ID commercial, de niveau de données de diagnostic et d’autres paramètres pour les appareils du regroupement cible. Cette configuration spécifie les unités pour apparaître dans votre espace de travail Analytique de bureau.  

    4. Vous déployez des mises à jour de compatibilité pour tous les appareils cibles.  

3. Pour le service de gestion de données de Diagnostic Microsoft pour Windows, les appareils envoient des données de diagnostic. Ce service est hébergé aux États-Unis.  

4. Chaque jour, Microsoft génère un instantané des insights axés sur l’informatique. Cet instantané combine les données de diagnostic à partir de Windows avec votre avis sur les appareils inscrits. Ce processus se déroule dans le stockage temporaire, qui est utilisé uniquement par l’Analytique de bureau. Le stockage temporaire est hébergé dans des centres de données de Microsoft aux États-Unis. Les captures instantanées sont séparées par un ID commercial.  

5. Les instantanés sont ensuite copiés vers l’espace de travail Analytique de journal Azure approprié.  

6. Postes de travail Analytique stocke votre entrée dans le stockage Azure Log Analytique. Ces configurations incluent des plans de déploiement et les décisions de ressource pour la mise à niveau et l’importance.  



## <a name="other-resources"></a>Autres ressources

Pour les questions fréquemment posées relatifs à la confidentialité pour l’Analytique de bureau, consultez [Forum aux questions de confidentialité](/sccm/desktop-analytics/faq#privacy).

Pour plus d’informations sur les aspects de la confidentialité connexes, consultez les articles suivants :

- [Windows 10 et le RGPD pour les décideurs informatiques](https://docs.microsoft.com/windows/privacy/gdpr-it-guidance)  

- [Configurer les données de diagnostic Windows de votre organisation](https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization)  

- [Champs et des événements de données de diagnostic appraiser Windows 7, Windows 8 et Windows 8.1](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-8.1-and-8/appraiser-diagnostic-data-events-and-fields)  

- [Windows 10, version 1809 base au niveau Windows des événements de diagnostic et champs](https://docs.microsoft.com/windows/privacy/basic-level-windows-diagnostic-events-and-fields-1809)  

- [Windows 10, version 1709 amélioré des événements de données de diagnostic et les champs utilisés par l’Analytique de bureau](https://docs.microsoft.com/windows/privacy/enhanced-diagnostic-data-windows-analytics-events-and-fields)  

- [Vue d’ensemble de visionneuse de données de diagnostic](https://docs.microsoft.com/windows/privacy/diagnostic-data-viewer-overview)  

- [Termes du contrat de licence et documentation](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31)  

- [Sécurité et confidentialité dans les centres de données Microsoft Azure](https://azure.microsoft.com/global-infrastructure/)  

- [Faites confiance au cloud approuvé](https://azure.microsoft.com/overview/trusted-cloud/)  

- [Centre de confidentialité](https://www.microsoft.com/trustcenter)  
