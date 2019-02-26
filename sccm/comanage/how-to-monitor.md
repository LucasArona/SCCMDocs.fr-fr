---
title: Surveiller la cogestion
titleSuffix: Configuration Manager
description: Utilisez le tableau de bord de cogestion pour consulter les informations sur les appareils cogérés.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e83a7b0d-b381-4b4a-8eca-850385abbebb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7c731692bc2277cc5ce97e079387b392ca09ff3e
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56754928"
---
# <a name="how-to-monitor-co-management-in-configuration-manager"></a>Guide pratique pour surveiller la cogestion dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Après avoir activé la cogestion, surveillez les appareils de cogestion à l’aide des méthodes suivantes :

- [Tableau de bord de cogestion](#co-management-dashboard)  

- [Stratégies de déploiement](#deployment-policies)

- [Données de l’appareil WMI](#wmi-device-data)



## <a name="co-management-dashboard"></a>Tableau de bord de cogestion

Depuis la version 1802, consultez un tableau de bord comportant des informations sur la cogestion. Le tableau de bord vous permet d’examiner les machines qui sont cogérées dans votre environnement. Les graphiques peuvent vous aider à identifier les appareils qui demandent une attention particulière.<!--1356648-->

Dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, puis sélectionnez le nœud **Cogestion**.

Depuis la version 1810, le tableau de bord de cogestion a été amélioré avec des informations plus détaillées. <!--1358980-->

![Capture d’écran du tableau de bord de cogestion](media/co-management-dashboard.png)


### <a name="co-managed-devices"></a>Appareils cogérés

*S’applique aux versions 1802 et 1806*

Indique le pourcentage d’appareils cogérés dans tout votre environnement.

![Vignette appareils cogérés](media/co-management-dashboard/Percent-Co-managed-graph.PNG)


### <a name="client-os-distribution"></a>Distribution des systèmes d’exploitation clients

*S’applique à toutes les versions* 

Indique le nombre d’appareils clients par système d’exploitation et par version. Elle utilise les regroupements suivants :  
- Windows 7 et 8.x  
- Windows 10 antérieur à 1709  
- Windows 10 1709 et ultérieur  

    > [!Tip]  
    > Windows 10, version 1709 et ultérieures, est un prérequis pour la cogestion.  

Pointez sur une section du graphique pour connaître le pourcentage d’appareils appartenant à ce groupe de système d’exploitation.

![Vignette de distribution de système d’exploitation client](media/co-management-dashboard/Co-management-OS-distribution-graph.PNG)


### <a name="co-management-status-donut"></a>État de la cogestion (anneau)

*S’applique aux versions 1802 et 1806*

Indique la répartition des réussites et des échecs des appareils dans les catégories suivantes :
- Réussite, Joint à une version hybride d’Azure AD  
- Réussite, Joint à Azure AD  
- Échec : L’inscription automatique a échoué  

Pointez sur une section du graphe pour connaître le pourcentage d’appareils appartenant à cette catégorie. 

![Vignette d’état (anneau) de cogestion](media/co-management-dashboard/Co-management-status-graph.PNG)

Sélectionnez une section du graphe pour voir la liste des appareils appartenant à cette catégorie.

![Liste des appareils en échec d’inscription](media/co-management-dashboard/Enrollment-Failure_Device-List.PNG)


### <a name="co-management-status-funnel"></a>État de la cogestion (entonnoir)

*S’applique à la version 1810 et ultérieures*

Graphique en entonnoir qui indique le nombre d’appareils associés aux états suivants du processus d’inscription :  
- Appareils éligibles  
- Planifié  
- Inscription lancée  
- Inscrit  

![Vignette d’état de la cogestion (entonnoir)](media/co-management-dashboard/1358980-status-funnel.png)


### <a name="co-management-enrollment-status"></a>État d'inscription à la cogestion

*S’applique à la version 1810 et ultérieures*

Montre la répartition de l’état des appareils dans les catégories suivantes :
- Réussite, joint à une version hybride d’Azure AD  
- Réussite, joint à Azure AD  
- Inscription en cours, joint à une version hybride d’Azure AD  
- Échec, joint à une version hybride d’Azure AD  
- Échec, joint à Azure AD  
- En attente de la connexion de l’utilisateur  

Sélectionnez un état dans la vignette pour accéder à la liste des appareils qui se trouvent dans cet état.  

![Vignette d’état d’inscription à la cogestion](media/co-management-dashboard/1358980-enrollment-status.png)


### <a name="workload-transition"></a>Transition des charges de travail

*S’applique à toutes les versions*

Affiche un graphique à barres indiquant le nombre d’appareils dont vous avez opéré la transition vers Microsoft Intune pour les charges de travail disponibles. 

La liste des charges de travail varie selon la version de Configuration Manager. Pour plus d’informations, consultez [Charges de travail pouvant être transférées à Intune](/sccm/comanage/workloads).

Pointez sur une section du graphique pour connaître le nombre d’appareils ayant fait l’objet d’une transition pour la charge de travail. 

![Graphique à barres de transition de la charge de travail](media/co-management-dashboard/Workload-Transition.PNG)


### <a name="enrollment-errors"></a>Erreurs d’inscription

*S’applique à la version 1810 et aux versions ultérieures*

Cette table est une liste d’erreurs d’inscription à partir d’appareils. Ces erreurs peuvent provenir du composant de gestion des appareils mobiles dans Windows, le cœur du système d’exploitation Windows ou le client Configuration Manager. 

Il existe des centaines d’erreurs possibles. Le tableau suivant répertorie les erreurs les plus courantes.
<!-- SCCMDocs issue 1064, BUG 3158555 -->

| Erreur | Description |
|---------|---------|
| 2147549183 (0x8000FFFF) | L’inscription MDM n’a pas été configurée encore sur Azure AD, ou l’inscription d’URL n’est pas attendue.<br><br>[Activer l’inscription automatique Windows 10](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment) |
| 2149056536 (0x80180018)<br>MENROLL_E_USERLICENSE | Licence de l’utilisateur est dans l’inscription de blocage état incorrect<br><br>[Attribuer des licences aux utilisateurs](https://docs.microsoft.com/intune/licenses-assign) |
| 2149056555 (0x8018002B)<br>MENROLL_E_MDM_NOT_CONFIGURED | Lorsque vous tentez automatiquement inscrire à Intune, mais la configuration Azure AD n’est pas entièrement appliquée. Ce problème doit être temporaire, comme les nouvelles tentatives de périphérique après une courte période. |
| 2149056554 (0x‭8018002A‬)<br>&nbsp; | L’utilisateur a annulé l’opération<br><br>Si l’inscription MDM nécessite l’authentification multifacteur et l’utilisateur n’a pas encore connecté avec un second facteur pris en charge, Windows affiche une notification toast à l’utilisateur à inscrire. Si l’utilisateur ne répond pas pour la notification toast, cette erreur se produit. Ce problème doit être temporaire, Configuration Manager de nouvelle tentative et inviter l’utilisateur. Les utilisateurs doivent utiliser l’authentification multifacteur lors de leur connexion à Windows. En outre Apprenez-leur à ce comportement est attendu et si vous y êtes invité, prendre des mesures. | 
| 2149056533 (0x80180015)<br>MENROLL_E_NOTSUPPORTED | Gestion des appareils mobiles en général ne pas pris en charge | 
| 2149056514 (0x80180002)<br>MENROLL_E_DEVICE_AUTHENTICATION_ERROR | Échec du serveur authentifier l’utilisateur<br><br> Il n’existe aucun jeton Azure AD pour l’utilisateur. Assurez-vous que l’utilisateur puisse s’authentifier sur Azure AD. |
| 2147942450 (0x‭80070032‬)<br>&nbsp; | Inscription automatique GPM uniquement est pris en charge que sur Windows RS3 et versions ultérieures.<br><br>Assurez-vous que l’appareil respecte les [configuration minimale requise](/sccm/comanage/overview#windows-10) pour la cogestion. |
| 3400073293 | Réponse de compte de domaine utilisateur ADAL inconnu<br><br>Vérifiez votre configuration Azure AD et assurez-vous que les utilisateurs peuvent s’authentifier avec succès. | 
| 3399548929 | Besoin de connexion de l’utilisateur<br><br>Ce problème devrait être temporaire. Il se produit lorsque l’utilisateur rapidement se déconnecte avant la tâche d’inscription se produit. | 
| 3400073236 | Échec de la demande de jeton de sécurité de la bibliothèque ADAL.<br><br>Vérifiez votre configuration Azure AD et assurez-vous que les utilisateurs peuvent s’authentifier avec succès. |
| 2149122477 | Problème HTTP générique |
| 3400073247 | L’authentification Windows intégrée à la bibliothèque ADAL est uniquement pris en charge dans les flux fédéré<br><br>[Planifier votre implémentation de jonction hybride Azure Active Directory](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan) | 
| 3399942148 | Le serveur ou le proxy est introuvable.<br><br>Ce problème doit être temporaire, lorsque le client ne peut pas communiquer avec le cloud. Si elle persiste, assurez-vous que le client dispose d’une connectivité cohérente sur Azure. | 
| 2149056532 | Plateforme spécifique ou version n’est pas pris en charge<br><br>Assurez-vous que l’appareil respecte les [configuration minimale requise](/sccm/comanage/overview#windows-10) pour la cogestion. |
| 2147943568 | Élément introuvable<br><br>Ce problème devrait être temporaire. Si elle persiste, contactez le Support Microsoft. |
| 2192179208 | Pas suffisamment de ressources mémoire est disponibles pour traiter cette commande.<br><br>Ce problème devrait être temporaire, il doit résoudre de lui-même lorsque le client effectue une nouvelle tentative. |
| 3399614467 | Échec de la bibliothèque ADAL octroi d’autorisation pour cette assertion<br><br>Vérifiez votre configuration Azure AD et assurez-vous que les utilisateurs peuvent s’authentifier avec succès. |
| 2149056517 | Échec générique à partir du serveur d’administration, tels qu’erreur d’accès de base de données<br><br>Ce problème devrait être temporaire. Si elle persiste, contactez le Support Microsoft. |
| 2149134055 | Nom de WinHTTP non résolu<br><br>Le client ne peut pas résoudre le nom du service. Vérifiez la configuration DNS. | 
| 2149134050 | délai d’expiration Internet<br><br>Ce problème doit être temporaire, lorsque le client ne peut pas communiquer avec le cloud. Si elle persiste, assurez-vous que le client dispose d’une connectivité cohérente sur Azure. | 


Pour plus d’informations, consultez [les valeurs d’erreur d’inscription MDM](https://docs.microsoft.com/windows/desktop/mdmreg/mdm-registration-constants).



## <a name="deployment-policies"></a>Stratégies de déploiement

Deux stratégies sont créées dans le nœud **Déploiements** de l’espace de travail **Analyse**. Une stratégie est destinée au groupe pilote et l’autre à la production. Ces stratégies signalent uniquement le nombre d’appareils auxquels Configuration Manager a appliqué la stratégie. Elles ne prennent pas en considération le nombre d’appareils inscrits dans Intune, ce qui est obligatoire pour pouvoir cogérer des appareils.  



## <a name="wmi-device-data"></a>Données de l’appareil WMI

Requête la **SMS_Client_ComanagementState** classe WMI. Vous pouvez créer des regroupements personnalisés dans le Gestionnaire de Configuration, ce qui vous aider à déterminer l’état de votre déploiement de la cogestion. Pour plus d’informations sur la création de regroupements personnalisés, consultez [comment créer des regroupements](/sccm/core/clients/manage/collections/create-collections). 

Les champs suivants sont disponibles dans la classe WMI :  

- **MachineID** : Un ID d’appareil unique pour le client Configuration Manager  

- **MDMEnrolled** : Spécifie si l’appareil est inscrit à la gestion des appareils mobiles  

- **Autorité** : L’autorité pour laquelle l’appareil est inscrit  

- **ComgmtPolicyPresent** : Spécifie si la stratégie de cogestion Configuration Manager existe sur le client. Si la valeur **MDMEnrolled** est **0**, l’appareil n’est pas cogéré, que la stratégie de cogestion existe sur le client ou non.  

Un appareil est cogéré quand les champs **MDMEnrolled** et **ComgmtPolicyPresent** ont tous les deux la valeur **1**.  
