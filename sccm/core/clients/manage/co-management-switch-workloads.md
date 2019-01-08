---
title: Basculer les charges de travail de Configuration Manager sur Intune
titleSuffix: Configuration Manager
description: Découvrez comment basculer les charges de travail actuellement gérées par Configuration Manager vers Microsoft Intune.
ms.prod: configuration-manager
ms.technology: configmgr-client
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 12/10/2018
ms.topic: conceptual
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: e3bd3bfda92fb877bac3ca68dbecf8b4a4078d4d
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53416943"
---
# <a name="switch-configuration-manager-workloads-to-intune"></a>Basculer les charges de travail de Configuration Manager sur Intune

Après avoir [préparé les appareils Windows 10 pour la cogestion](/sccm/core/clients/manage/co-management-prepare), l’étape suivante consiste à activer l’inscription automatique des clients à Intune. Lorsque vous êtes prêt, commencez ensuite à basculer des charges de travail Configuration Manager spécifiques vers Intune. 


## <a name="setup-co-management"></a>Configurer la cogestion

1. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**.  

2. Dans l’onglet **Accueil** du ruban, dans le groupe **Gérer**, choisissez  **Configurer la cogestion**. Cette action ouvre l’Assistant Configuration de la cogestion.  

3. Dans la page Abonnement, sélectionnez **Se connecter**. Connectez-vous à votre locataire Intune, puis sélectionnez **Suivant**.  

4. Dans la page Activation, choisissez **Pilote** ou **Tous**.  

    Cette action active l’inscription automatique des clients dans Intune. Lorsque vous choisissez **Pilote**, seuls les clients Configuration Manager membres du regroupement pilote sont automatiquement inscrits à Intune. Cette option vous permet d’activer la cogestion sur un sous-ensemble de clients pour tester initialement la cogestion et la déployer au moyen d’une approche progressive.  

    Utilisez la ligne de commande affichée pour déployer le client Configuration Manager en tant qu’application dans Intune pour les appareils déjà inscrits à Intune. Pour plus d’informations, consultez [Appareils Windows 10 inscrits à Intune](/sccm/core/clients/manage/co-management-prepare#windows-10-devices-enrolled-in-intune).  

5. Dans la page Charges de travail, choisissez de basculer ou non les charges de travail de Configuration Manager devant être gérées par Intune. Vous pouvez activer l’inscription sur la page précédente sans basculer des charges de travail pour l’instant. 

    Le paramètre **Intune pilote** bascule la charge de travail associée uniquement pour les appareils inclus dans le regroupement pilote. Le paramètre **Intune** bascule la charge de travail associée pour tous les appareils Windows 10 cogérés.  

    > [!Important] 
    > Avant de basculer toutes les charges de travail, vérifiez que vous avez correctement configuré et déployé la charge de travail correspondante dans Intune. Assurez-vous que les charges de travail sont toujours gérées par l’un des outils de gestion de vos appareils.  

6. Sur la page Mise en lots, configurez les paramètres suivants :  

    - **Pilote** : Le groupe pilote contient un ou plusieurs regroupements que vous sélectionnez. Utilisez ce groupe dans le cadre de votre déploiement progressif de la cogestion. Commencez par un regroupement test peu volumineux, puis ajoutez d’autres regroupements à ce groupe pilote au fur et à mesure que vous déployez la cogestion pour d’autres utilisateurs et appareils. Vous pouvez modifier les regroupements dans le groupe pilote à tout moment.  

    - **Production** : Configurez le **Groupe d’exclusions** avec un ou plusieurs regroupements. Les appareils membres d’une des collections de ce groupe sont exclus de l’utilisation de la cogestion.  

7. Pour activer la cogestion, terminez l’Assistant.  

<!--1357377--> À compter de Configuration Manager version 1806, quand vous passez à une charge de travail en cogestion, les appareils cogérés sont automatiquement synchronisés avec la stratégie MDM de Microsoft Intune. Cette synchronisation est effectuée lorsque vous lancez l’action **Télécharger la stratégie d’ordinateur** à partir de notifications du client dans la console Configuration Manager. Pour plus d’informations, consultez [Lancer une récupération de stratégie client en utilisant une notification de client](/sccm/core/clients/manage/manage-clients#initiate-client-policy-retrieval-using-client-notification).



## <a name="modify-your-co-management-settings"></a>Modifier les paramètres de cogestion

Après avoir activé la cogestion à l’aide de l’Assistant, modifiez les paramètres dans les propriétés de cogestion. Dans la console Configuration Manager, accédez à l’espace de travail **Administration**, développez **Services cloud**, puis sélectionnez le nœud **Cogestion**. Sélectionnez l’objet de cogestion, puis sélectionnez **Propriétés** dans le ruban. 



## <a name="supported-workloads"></a>Charges de travail prises en charge

Les charges de travail suivantes sont actuellement disponibles pour être basculées de Configuration Manager dans Intune :

- **Stratégies de conformité des appareils**  

- **Stratégies d’accès aux ressources** : Pour plus d’informations sur ces stratégies Intune, consultez [Déployer des profils d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles).
    - Profil de messagerie  
    - Profil Wi-Fi  
    - Profil VPN  
    - Profil de certificat  

- **Stratégies Windows Update**  

- **Endpoint Protection** : À compter de Configuration Manager version 1802, cette charge de travail inclut les fonctionnalités suivantes :  
    - Windows Defender Application Guard  
    - Pare-feu Windows Defender  
    - Windows Defender SmartScreen  
    - Chiffrement Windows  
    - Windows Defender Exploit Guard  
    - Windows Defender Application Control  
    - Centre de sécurité Windows Defender  
    - Windows Defender - Protection avancée contre les menaces  
    - Protection des informations Windows  

- **Configuration de l’appareil** : À compter de Configuration Manager version 1806<!--1357903--> :  

    - Le fait de déplacer la charge de travail de configuration des appareils déplace également les charges de travail **Accès aux ressources** et **Endpoint Protection**  

    - Vous pouvez toujours déployer des paramètres Configuration Manager sur des appareils cogérés, même si Intune représente l’autorité de configuration des appareils. Cette exception peut être utilisée pour configurer les paramètres qui sont exigés par votre entreprise, mais qui ne sont pas encore disponibles dans Intune. Spécifiez cette exception sur une [base de référence de configuration Configuration Manager](/sccm/compliance/deploy-use/create-configuration-baselines). Activez l’option **Toujours appliquer cette base de référence, même aux clients cogérés** lors de la création de la base de référence, ou sous l’onglet **Général** des propriétés de la base de référence existante.  

- **Applications « Démarrer en un clic » Office 365** : À compter de Configuration Manager version 1806<!--1357841--> :  

    - Après avoir déplacé la charge de travail, l’application s’affiche dans le **Portail d’entreprise** sur l’appareil  

    - Les mises à jour Office peuvent mettre environ 24 heures à s’afficher sur le client, sauf si les appareils sont redémarrés  

    - Il existe une nouvelle condition globale : **Are Office 365 applications managed by Intune on the device** (Les applications Office 365 sont-elles gérées par Intune sur cet appareil ?). Cette condition est ajoutée par défaut dans le cadre d’une exigence pour les nouvelles applications Office 365. Si vous transférez cette charge de travail, les clients cogérés ne répondront pas à cette exigence de l’application. Ils n’installeront donc pas Office 365 déployé via Configuration Manager.  

- **Applications clientes** : À compter de Configuration Manager version 1806 comme [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features))<!--1357892--> :  

    - Une fois cette charge de travail transférée, toutes les applications disponibles déployées à partir d’Intune seront accessibles sur le Portail d’entreprise  

    - Les applications déployées à partir de Configuration Manager sont disponibles dans le Centre logiciel  



## <a name="monitor-co-management"></a>Surveiller la cogestion

Après avoir activé la cogestion, surveillez les appareils de cogestion à l’aide des méthodes suivantes :

- [Tableau de bord de cogestion](/sccm/core/clients/manage/co-management-dashboard)  

- **Vue SQL et classe WMI** : Interrogez la vue SQL **v_ClientCoManagementState** dans la base de données du site Configuration Manager ou la classe WMI **SMS_Client_ComanagementState**. Avec les informations contenues dans la classe WMI, vous pouvez créer des regroupements personnalisés dans Configuration Manager pour vous aider à déterminer l’état du déploiement de la cogestion. Pour plus d’informations, consultez [Guide pratique pour créer des regroupements](/sccm/core/clients/manage/collections/create-collections). Les champs suivants sont disponibles dans la vue SQL et la classe WMI :  
  - **MachineID** : Spécifie un ID d’appareil unique pour le client Configuration Manager  
  - **MDMEnrolled** : Spécifie si l’appareil est inscrit à la gestion des appareils mobiles  
  - **Autorité** : Spécifie l’autorité pour laquelle l’appareil est inscrit  
  - **ComgmtPolicyPresent** : Spécifie si la stratégie de cogestion Configuration Manager existe sur le client. Si la valeur **MDMEnrolled** est **0**, l’appareil n’est pas cogéré, que la stratégie de cogestion existe sur le client ou non.  

    > [!Note]  
    > Un appareil est cogéré quand les champs **MDMEnrolled** et **ComgmtPolicyPresent** ont tous les deux la valeur **1**.  

- **Stratégies de déploiement** : Deux stratégies sont créées dans le nœud **Déploiements** de l’espace de travail **Analyse**. Une stratégie est destinée au groupe pilote et l’autre à la production. Ces stratégies signalent uniquement le nombre d’appareils auxquels Configuration Manager a appliqué la stratégie. Elles ne prennent pas en considération le nombre d’appareils inscrits dans Intune, ce qui est obligatoire pour pouvoir cogérer des appareils.  



## <a name="check-compliance-for-co-managed-devices"></a>Vérifier la conformité des appareils cogérés

Les utilisateurs peuvent utiliser le Centre logiciel pour vérifier la conformité de leurs appareils Windows 10 cogérés, que l’accès conditionnel soit géré par Configuration Manager ou par Intune. Ils peuvent également vérifier la conformité à l’aide de l’application Portail d’entreprise quand l’accès conditionnel est géré par Intune.



## <a name="next-steps"></a>Étapes suivantes

Utilisez les ressources suivantes pour vous aider à gérer les charges de travail que vous basculez vers Intune :
- [Stratégies de conformité des appareils](https://docs.microsoft.com/intune/device-compliance-get-started)
- [Stratégies d’accès aux ressources](https://docs.microsoft.com/intune/device-profiles)
- [Stratégies Windows Update pour Entreprise](https://docs.microsoft.com/intune/windows-update-for-business-configure)
- [Endpoint Protection pour Microsoft Intune](https://docs.microsoft.com/intune-classic/deploy-use/help-secure-windows-pcs-with-endpoint-protection-for-microsoft-intune)
