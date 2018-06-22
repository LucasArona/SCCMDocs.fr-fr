---
title: Protéger les données avec la réinitialisation à distance, le verrouillage à distance ou la réinitialisation du code d'accès
titleSuffix: Configuration Manager
description: Protégez les données des appareils à l’aide de la réinitialisation complète, de la réinitialisation sélective, du verrouillage à distance ou de la réinitialisation du code d’accès en utilisant System Center Configuration Manager.
ms.date: 10/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 670667c21e85d7e5c174c051b6adbdca3eba55a8
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352999"
---
# <a name="protect-data-with-remote-wipe-lock-or-passcode-reset-by-using-system-center-configuration-manager"></a>Protéger les données à l’aide de la réinitialisation à distance, du verrouillage ou de la réinitialisation du code d’accès en utilisant System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

System Center Configuration Manager propose des fonctionnalités de réinitialisation sélective, de réinitialisation complète, de verrouillage à distance et de réinitialisation du code d’accès. Les appareils mobiles peuvent stocker leurs données sensibles et fournir un accès à de nombreuses ressources d'entreprise. Pour protéger les appareils, vous pouvez émettre :  

- Une réinitialisation complète pour rétablir les paramètres d'usine de l'appareil.  

- Une réinitialisation sélective pour supprimer uniquement les données de l'entreprise.  

- Un verrouillage à distance pour sécuriser un appareil censé être perdu.  

- Une réinitialisation du code d’accès de l’appareil.  

## <a name="full-wipe"></a>Réinitialisation complète  
Vous pouvez émettre une commande de réinitialisation vers un appareil lorsque vous devez sécuriser un appareil perdu ou lorsque vous mettez un appareil hors service.  

Émettez une **réinitialisation complète** sur un appareil pour restaurer l'appareil sur ses paramètres d'usine. Cette opération supprime toutes les données de l'entreprise et tous les paramètres utilisateur. Vous pouvez effectuer une réinitialisation complète sur les appareils Windows Phone, iOS, Android et Windows 10.  

> [!NOTE]
> Vous pouvez uniquement effectuer une réinitialisation complète sur les appareils d’entreprise.

> [!NOTE]
> Les appareils Windows 10 antérieurs à la version 1511 et qui sont dotés de moins de 4 Go de RAM peuvent rester sans réponse à l’occasion d’une réinitialisation. [En savoir plus](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Pour exécuter une réinitialisation à distance à partir de la console Configuration Manager  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** et **Appareils**. Vous pouvez également choisir **Regroupements d’appareils** , puis sélectionner un regroupement.  

2. Sélectionnez l'appareil que vous souhaitez mettre hors service/réinitialiser.  

3. Choisissez **Actions de l’appareil à distance** dans **Groupe d’appareils**, puis **Mettre hors service/Réinitialiser**.  

## <a name="selective-wipe"></a>Réinitialisation sélective  
Émettez une **réinitialisation sélective** sur un appareil pour supprimer uniquement les données de l'entreprise. Le tableau suivant décrit, en fonction de chaque plateforme, les données supprimées et l’effet de cette opération sur les données qui restent sur l’appareil après une réinitialisation sélective.  

**iOS**  

|Contenu supprimé lors de la mise hors service d’un appareil|iOS|  
|--------------------------------------------|---------|  
|Applications d’entreprise et données associées installées à l’aide de Configuration Manager et Intune|Les applications sont désinstallées. Les données des applications de l'entreprise sont supprimées.|  
|Profils VPN et Wi-Fi|Supprimé.|  
|Certificats|Supprimé et révoqué.|  
|Paramètres|Supprimé, à l’exception de : **Autoriser l’itinérance vocale**, **Autoriser l’itinérance des données**, et **Autoriser la synchronisation automatique lors de l’itinérance**.|  
|Agent de gestion|Le profil de gestion est supprimé.|  
|Profils de messagerie|Pour les profils de messagerie configurés par Intune, le compte de messagerie et l’adresse e-mail sont supprimés.|  

**Android et Android Samsung KNOX Standard**  

|Contenu supprimé lors de la mise hors service d’un appareil|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Applications d’entreprise et données associées installées à l’aide de Configuration Manager et Intune|Les applications et les données sont toujours installées.|Les applications sont désinstallées.|  
|Profils VPN et Wi-Fi|Supprimé.|Supprimé.|  
|Certificats|Révoqué.|Révoqué.|  
|Paramètres|La configuration requise est supprimée.|La configuration requise est supprimée.|  
|Agent de gestion|Le privilège d'administrateur d'appareil est révoqué.|Le privilège d'administrateur d'appareil est révoqué.|  
|Profils de messagerie|Non applicable.|Pour les profils de messagerie configurés par Intune, le compte de messagerie et l’adresse e-mail sont supprimés.|  

**Android for Work**

Sur un appareil Android for Work, la réinitialisation sélective supprime le profil professionnel ainsi que toutes les données, applications et paramètres du profil professionnel de l’appareil. Cette opération met l’appareil hors service vis-à-vis de la gestion avec Configuration Manager et Intune. La réinitialisation complète n’est pas prise en charge pour Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1 et Windows RT**  

|Contenu supprimé lors de la mise hors service d’un appareil|Windows 10, Windows 8.1 et Windows RT 8.1|  
|---------------------------------|-------------|
|Applications d’entreprise et données associées installées à l’aide de Configuration Manager et Intune|Les applications sont désinstallées et les clés de chargement de version test sont supprimées. Les applications utilisant la réinitialisation sélective de Windows voient la clé de chiffrement révoquée et les données ne sont plus accessibles.|  
|Profils VPN et Wi-Fi|Supprimé.|  
|Certificats|Supprimé et révoqué.|  
|Paramètres|La configuration requise est supprimée.|
|Agent de gestion|Non applicable. L’agent de gestion est intégré.|  
|Profils de messagerie|La messagerie électronique compatible avec EFS est supprimée, ce qui inclut l’application de messagerie pour le courrier et les pièces jointes Windows.|  

 **Windows 10 Mobile, Windows Phone 8.0 et Windows Phone 8.1**

|Contenu supprimé lors de la mise hors service d’un appareil|Windows 10 Mobile, Windows Phone 8 et Windows Phone 8.1|  
|-|-|
|Applications d’entreprise et données associées installées à l’aide de Configuration Manager et Intune|Les applications sont désinstallées. Les données des applications de l'entreprise sont supprimées.|  
|Profils VPN et Wi-Fi|Supprimé pour Windows 10 Mobile et Windows Phone 8.1.|  
|Certificats|Supprimé pour Windows Phone 8.1.|  
|Agent de gestion|Non applicable. L’agent de gestion est intégré.|  
|Profils de messagerie|Supprimé (à l’exception de Windows Phone 8.0).|  

Les paramètres suivants sont aussi supprimés des appareils Windows 10 Mobile et Windows Phone 8.1 :  

- **Exiger un mot de passe pour déverrouiller des appareils mobiles**  
- **Autoriser les mots de passe simples**  
- **Longueur minimale du mot de passe**  
- **Type de mot de passe requis**
- **Expiration du mot de passe (jours)**  
- **Mémoriser l’historique des mots de passe**  
- **Nombre d’échecs de connexion successifs autorisé avant réinitialisation de l’appareil**  
- **Minutes d’inactivité avant demande du mot de passe**  
- **Type de mot de passe requis - Nombre minimum de jeux de caractères**  
- **Autoriser l’appareil photo**
- **Exiger le chiffrement sur l’appareil mobile**  
- **Autoriser le stockage amovible**  
- **Autoriser le navigateur web**  
- **Autoriser la boutique d’applications**  
- **Autoriser la capture d’écran**  
- **Autoriser la géolocalisation**  
- **Autoriser un compte Microsoft**  
- **Autoriser la fonction copier-coller**  
- **Autoriser la connexion Wi-Fi**  
- **Autoriser la connexion automatique aux points d’accès Wi-Fi gratuits**  
- **Autoriser l’indication des points d’accès Wi-Fi**  
- **Autoriser la réinitialisation aux paramètres d’usine**
- **Autoriser Bluetooth**  
- **Autoriser NFC**
- **Autoriser le Wi-Fi**

#### <a name="to-initiate-a-remote-wipe-from-the-configuration-manager-console"></a>Pour exécuter une réinitialisation à distance à partir de la console Configuration Manager  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** et **Appareils**. Vous pouvez également choisir **Regroupements d’appareils** , puis sélectionner un regroupement.  

2. Sélectionnez l'appareil que vous souhaitez mettre hors service/réinitialiser.  

3. Choisissez **Actions de l’appareil à distance** dans **Groupe d’appareils**, puis **Mettre hors service/Réinitialiser**.  

## <a name="wiping-efs-enabled-content"></a>Réinitialisation du contenu EFS  
Windows 8.1 et Windows RT 8.1 prennent en charge la réinitialisation sélective du contenu EFS (Encrypting File System). Les éléments suivants s'appliquent à une réinitialisation sélective du contenu EFS :  

- Seules les applications et les données protégées par EFS utilisant le même domaine Internet que le compte Intune sont réinitialisées de manière sélective. Pour plus d'informations, consultez la page relative à la [réinitialisation sélective de Windows pour la gestion des données d'appareil](http://technet.microsoft.com/library/dn486874.aspx).  

- Si des modifications sont apportées au domaine associé à EFS, 48 heures peuvent être nécessaires avant que les applications et les données qui utilisent le nouveau domaine soient réinitialisées de manière sélective.  

- Chaque domaine inscrit auprès d’Intune est réinitialisé.  

Les données et les applications qui sont actuellement prises en charge par la réinitialisation sélective EFS sont :  

- Application de messagerie pour Windows.  

- Dossiers de travail.

- Fichiers et dossiers chiffrés par EFS. Pour plus d'informations, consultez [Meilleures pratiques pour le chiffrement des systèmes de fichiers](http://support.microsoft.com/kb/223316).  

### <a name="best-practices-for-selective-wipe"></a>Meilleures pratiques pour la réinitialisation sélective  

- Pour que la réinitialisation du courrier électronique réussisse, configurez les profils pour les appareils iOS et Windows Phone 8.1.  

- Pour que la réinitialisation des applications réussisse, vérifiez que les applications sont distribuées au moyen de la gestion d’applications d’appareil mobile.  

- Pour iOS, configurez le paramètre **Autoriser la sauvegarde sur iCloud** sur **Désactiver** pour que les utilisateurs ne puissent pas restaurer le contenu à l’aide d’iCloud.  

- Si un compte a été désactivé, au bout d’une année il est supprimé par Intune et une réinitialisation sélective est effectuée.  

##  <a name="passcode-reset"></a>Réinitialiser le code secret  
Si un utilisateur oublie son code d'accès, vous pouvez l'aider à résoudre ce problème en supprimant le code d'accès d'un appareil ou en forçant l'application d'un nouveau code accès temporaire sur un appareil. Le tableau ci-dessous indique la méthode de réinitialisation du code d’accès sur différentes plateformes mobiles.  

| Plate-forme                              | Réinitialiser le code secret                                                                               |
|---------------------------------------|----------------------------------------------------------------------------------------------|
| iOS                                   | Prise en charge de l'effacement du code d'accès d'un appareil. Ne crée pas un nouveau code d'accès temporaire. |
| macOS                                 | Non pris en charge.                                                                               |
| Android                               | Pris en charge sur les versions antérieures à Android 7.0. Crée un code d’accès temporaire.                |
| Android for Work                      | Non pris en charge.                                                                               |
| PC Windows 10                        | Non pris en charge.                                                                               |
| Windows 10 Mobile                     | Prise en charge, sauf les appareils joints à Azure AD.  |
| Windows Phone 8 et Windows Phone 8.1 | Pris en charge.                                                                                   |
| Windows RT 8.1                        | Non pris en charge.                                                                               |
| PC Windows 8.1                       | Non pris en charge.                                                                               |

> [!Note]    
> Vous devez procéder à la réinitialisation du code secret à partir du site de niveau supérieur dans votre environnement. Par exemple, si vous utilisez un site d’administration centrale, vous ne pouvez effectuer cette action que sur ce site. Si vous utilisez un site principal autonome, vous ne pouvez effectuer cette action que sur ce site.

#### <a name="to-reset-the-passcode-on-a-mobile-device-remotely-in-configuration-manager"></a>Pour réinitialiser le mot de passe sur un appareil mobile à distance dans Configuration Manager  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** et **Appareils**. Vous pouvez également choisir **Regroupements d’appareils** , puis sélectionner un regroupement.  

2. Sélectionnez les appareils sur lesquels vous voulez réinitialiser le code d'accès.  

3. Choisissez **Actions de l’appareil à distance** dans **Groupe d’appareils**, puis choisissez **Réinitialisation du code d’accès**.  

#### <a name="to-show-the-state-of-the-passcode-reset"></a>Pour afficher l'état de la réinitialisation du code d'accès  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** et **Appareils**. Vous pouvez également choisir **Regroupements d’appareils** , puis sélectionner un regroupement.  

2. Sélectionnez les appareils sur lesquels vous voulez réinitialiser le code d'accès.  

3. Choisissez **Actions de l’appareil à distance** dans **Groupe d’appareils**, puis choisissez **Afficher l’état du code secret**.  

## <a name="remote-lock"></a>Verrouillage à distance  
Si un utilisateur perd son appareil, vous pouvez verrouiller ce dernier à distance. Le tableau ci-dessous illustre le fonctionnement du verrouillage à distance sur différentes plateformes mobiles.  

|Plate-forme|Verrouillage à distance|  
|--------------|-----------------|  
|iOS|Pris en charge.|  
|Android|Pris en charge.|  
|Windows 10|Non pris en charge pour l’instant.|  
|Windows Phone 8 et Windows Phone 8.1|Pris en charge.|  
|Windows RT 8.1 |Prise en charge si l'utilisateur actuel de l'appareil est le même utilisateur qui a inscrit l'appareil.|  
|Windows 8.1|Prise en charge si l'utilisateur actuel de l'appareil est le même utilisateur qui a inscrit l'appareil.|  

> [!Note]    
> Vous devez effectuer l’action de verrouillage à distance à partir du site de niveau supérieur dans votre environnement. Par exemple, si vous utilisez un site d’administration centrale, vous ne pouvez effectuer cette action que sur ce site. Si vous utilisez un site principal autonome, vous ne pouvez effectuer cette action que sur ce site.

#### <a name="to-lock-a-mobile-device-remotely-through-the-configuration-manager-console"></a>Pour verrouiller un appareil mobile à distance via la console Microsoft Intune  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** et **Appareils**. Vous pouvez également choisir **Regroupements d’appareils** , puis sélectionner un regroupement.  

2. Sélectionnez les appareils à verrouiller.  

3. Choisissez **Actions de l’appareil à distance** dans **Groupe d’appareils**, puis choisissez **Verrouillage à distance**.  

#### <a name="to-show-the-state-of-the-remote-lock"></a>Pour afficher l'état du verrouillage à distance  

1. Dans la console Configuration Manager, choisissez **Ressources et Conformité** et **Appareils**. Vous pouvez également choisir **Regroupements d’appareils** , puis sélectionner un regroupement.  

2. Sélectionnez les appareils sur lesquels vous voulez afficher l'état du verrouillage à distance.  

3. Choisissez **Actions de l’appareil à distance** dans **Groupe d’appareils**, puis choisissez **Afficher l’état du verrouillage à distance**.  

### <a name="see-also"></a>Voir aussi  
[Réinitialisation sélective de Windows pour la gestion des données d’appareil](http://technet.microsoft.com/library/dn486874.aspx)   
