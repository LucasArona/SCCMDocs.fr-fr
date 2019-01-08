---
title: Endpoint Protection
titleSuffix: Configuration Manager
description: Apprenez à gérer les stratégies de logiciel anti-programme malveillant et la sécurité du Pare-feu Windows pour les clients.
ms.date: 10/26/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 76c90f64-d729-456b-8304-01852cd66fb6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 160713fe480b0a47c2ad57376c4a1dccdbfb00b1
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53418949"
---
# <a name="endpoint-protection"></a>Endpoint Protection

*S’applique à : System Center Configuration Manager (Current Branch)*

Endpoint Protection gère les stratégies anti-programme malveillant et la sécurité du Pare-feu Windows pour les ordinateurs clients de votre hiérarchie Configuration Manager.  

> [!IMPORTANT]  
>  Vous devez détenir une licence pour pouvoir utiliser Endpoint Protection pour gérer les clients dans votre hiérarchie Configuration Manager.  

 L’utilisation d’Endpoint Protection avec Configuration Manager présente les avantages suivants :  

-   Configuration des stratégies de logiciel anti-programme malveillant, des paramètres du Pare-feu Windows et gestion du service Windows Defender - Protection avancée contre les menaces sur certains groupes d’ordinateurs  
-   Utilisation des mises à jour logicielles Configuration Manager pour télécharger les derniers fichiers de définitions de logiciel anti-programme malveillant pour tenir à jour les ordinateurs clients  
-   Envoyez des notifications par e-mail, utilisez la surveillance dans la console et visualisez des rapports. Ces actions informent les utilisateurs administratifs quand un programme malveillant est détecté sur des ordinateurs clients.  

Windows Defender est déjà installé sur les ordinateurs Windows 10 et Windows Server 2016. Pour ces systèmes d’exploitation, un client de gestion pour Windows Defender est installé lorsque le client Configuration Manager est installé. Sur les ordinateurs Windows 8.1 et antérieurs, le client Endpoint Protection est installé avec le client Configuration Manager. Windows Defender et le client Endpoint Protection offrent les possibilités suivantes :  

-   Détection des logiciels malveillants et des logiciels espions et mesures correctives  
-   Détection des rootkits et mesures correctives  
-   Évaluation des vulnérabilités critiques et mises à jour automatiques des définitions et du moteur  
-   Détection des vulnérabilités réseau via le système NIS (Network Inspection System)  
-   Intégration à Cloud Protection Service pour signaler les logiciels malveillants à Microsoft. Quand vous rejoignez ces services, le client Endpoint Protection ou Windows Defender télécharge les dernières définitions à partir du Centre de protection contre les programmes malveillants quand un programme malveillant non identifié est détecté sur un ordinateur.  

> [!NOTE]  
>  Le client Endpoint Protection peut être installé sur un serveur qui exécute Hyper-V et sur les machines virtuelles invitées dotées d’un système d’exploitation pris en charge. Pour éviter une utilisation excessive du processeur, les actions Endpoint Protection ont un délai randomisé intégré qui empêche les services de protection de s’exécuter simultanément.  

 De plus, vous gérez les paramètres du Pare-feu Windows avec Endpoint Protection dans la console Configuration Manager.  

 [Exemple de scénario : utilisation de System Center Endpoint Protection pour protéger des ordinateurs contre les programmes malveillants dans System Center Configuration Manager](scenarios-endpoint-protection.md) Endpoint Protection et le Pare-feu Windows.  


## <a name="managing-malware-with-endpoint-protection"></a>Gestion des logiciels malveillants avec Endpoint Protection  
 Endpoint Protection dans Configuration Manager vous permet de créer des stratégies de logiciel anti-programme malveillant qui contiennent des paramètres pour les configurations de client Endpoint Protection. Déployez ces stratégies anti-programme malveillant sur les ordinateurs clients. Ensuite, surveillez la conformité dans le nœud **État Endpoint Protection** sous **Sécurité** dans l’espace de travail **Surveillance**. Utilisez également les rapports Endpoint Protection dans le nœud **Reporting**.  

 Informations complémentaires :  

-   [Comment créer et déployer des stratégies anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md) : créez, déployer et surveillez des stratégies de logiciel anti-programme malveillant à partir de la liste des paramètres que vous pouvez configurer.  

-   [Comment surveiller Endpoint Protection dans System Center Configuration Manager](monitor-endpoint-protection.md) : surveillance des rapports d’activité, des ordinateurs clients infectés et bien plus encore.  

-   [Comment gérer les stratégies de logiciel anti-programme malveillant et les paramètres de pare-feu pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-firewall.md) : prenez des mesures correctives contre les programmes malveillants détectés sur les ordinateurs clients.  


## <a name="managing-windows-firewall-with-endpoint-protection"></a>Gestion du pare-feu Windows avec Endpoint Protection  
 Endpoint Protection dans Configuration Manager assure une gestion de base du Pare-feu Windows sur les ordinateurs clients. Pour chaque profil de réseau, vous pouvez :  

-   Activer ou désactiver le pare-feu Windows.  

-   Bloquer les connexions entrantes, y compris celles figurant dans la liste des programmes autorisés.  

-   Avertir l'utilisateur lorsque le pare-feu Windows bloque un nouveau programme.  

> [!NOTE]  
>  Endpoint Protection prend en charge la gestion du pare-feu Windows uniquement.  


 Pour plus d’informations, consultez [Guide pratique pour créer et déployer des stratégies de Pare-feu Windows pour Endpoint Protection](create-windows-firewall-policies.md).  


## <a name="windows-defender-advanced-threat-protection"></a>Windows Defender - Protection avancée contre les menaces

Endpoint Protection gère et surveille le service Windows Defender - Protection avancée contre les menaces. Le service Windows Defender - Protection avancée contre les menaces permet aux entreprises de détecter, d’examiner et de répondre aux attaques avancées sur leur réseau. Pour plus d’informations, consultez [Windows Defender - Protection avancée contre les menaces](windows-defender-advanced-threat-protection.md).

## <a name="endpoint-protection-workflow"></a>Flux de travail Endpoint Protection  
 Utilisez le diagramme suivant pour comprendre le flux de travail qui permet d’implémenter Endpoint Protection dans votre hiérarchie Configuration Manager.  

 ![Flux de travail Endpoint Protection](../media/Endpoint-Protection-Workflow.gif)  



## <a name="endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Client Endpoint Protection pour les ordinateurs Mac et les serveurs Linux  

> [!Important]  
> Le support de System Center Endpoint Protection (SCEP) pour Mac et Linux (toutes les versions) prend fin le 31 décembre 2018. La disponibilité de nouvelles définitions de virus pour SCEP pour Mac et SCEP pour Linux sera peut-être supprimée une fois que le support aura pris fin. Pour plus d’informations, consultez le [billet de blog sur la fin du support](https://go.microsoft.com/fwlink/?linkid=870182).  

 System Center Endpoint Protection comprend un client Endpoint Protection pour Linux et pour les ordinateurs Mac. Ces clients ne sont pas fournis avec Configuration Manager. Téléchargez les produits suivants à partir du [Centre de gestion des licences en volume Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx) :  

-   System Center Endpoint Protection pour Mac  

-   System Center Endpoint Protection pour Linux  


> [!Note]  
>  Vous devez être client d’une licence en volume Microsoft pour télécharger les fichiers d’installation d’Endpoint Protection pour Linux et Mac.  

 Ces produits ne peuvent pas être gérés à partir de la console Configuration Manager. Un pack d’administration System Center Operations Manager, fourni avec les fichiers d’installation, vous permet de gérer le client pour Linux.  

### <a name="how-to-get-the-endpoint-protection-client-for-mac-computers-and-linux-servers"></a>Guide pratique pour obtenir le client Endpoint Protection pour les ordinateurs Mac et les serveurs Linux

Procédez comme suit pour télécharger le fichier image contenant le logiciel client Endpoint Protection et la documentation pour les ordinateurs Mac et les serveurs Linux.
1. Connectez-vous au [Centre de gestion des licences en volume Microsoft](https://www.microsoft.com/licensing/servicecenter/default.aspx).
2. Sélectionnez l’onglet **Téléchargements et clés** situé en haut du site web.
3. Filtrez sur le produit **System Center Endpoint Protection (Current Branch)**.
4. Cliquez sur le lien vers **Télécharger**
5. Cliquez sur **Continuer**. Vous devez voir plusieurs fichiers, dont un nommé : **System Center Endpoint Protection (current branch - de la version 1606) pour Linux OS and Macintosh OS Multilanguage 32/64 bit 1878 MB ISO**.
6. Pour télécharger le fichier, cliquez sur l’icône de flèche. Le nom de fichier est **SW_DVD5_Sys_Ctr_Endpnt_Prtctn_1606_MultiLang_-3_EptProt_Lin_Mac_MLF_X21-67050.ISO**.

La mise à jour de janvier 2018 (X21-67050) inclut les versions suivantes :

- System Center Endpoint Protection pour Mac 4.5.32.0 (prise en charge de macOS 10.13 High Sierra)
- System Center Endpoint Protection pour Linux 4.5.20.0 

  Pour plus d’informations sur la façon d’installer et de gérer les clients Endpoint Protection pour les ordinateurs Mac et Linux, utilisez la documentation qui accompagne ces produits. Cette documentation de produit se trouve dans le dossier **Documentation** du fichier .ISO.
