---
title: Bonnes pratiques pour le déploiement de clients
titleSuffix: Configuration Manager
description: Bonnes pratiques pour le déploiement de clients dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9c68a51202152e4b1418101412739b0d83f10203
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32333516"
---
# <a name="best-practices-for-client-deployment-in-system-center-configuration-manager"></a>Bonnes pratiques pour le déploiement de clients dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Utilisation de l'installation de client basée sur des mises à jour logicielles sur les ordinateurs Active Directory  
 Cette méthode de déploiement du client utilise les technologies Windows existantes, s’intègre avec votre infrastructure Active Directory et ne nécessite qu’une configuration minimale dans Configuration Manager. Elle est la plus facile pour configurer le pare-feu et elle est aussi la plus sûre. À l'aide de groupes de sécurité et du filtrage WMI pour la configuration de stratégie de groupe, vous disposez d'une grande flexibilité pour contrôler quels ordinateurs installent le client Configuration Manager.  

 Pour plus d’informations, voir [Comment installer des clients Configuration Manager à l'aide d'une installation basée sur les mises à jour logicielles](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Développement du schéma Active Directory et publication du site afin de pouvoir exécuter CCMSetup sans options de ligne de commande  
 Lorsque vous étendez le schéma Active Directory pour Configuration Manager et que le site est publié dans les services de domaine Active Directory, de nombreuses propriétés d'installation du client sont publiées dans les services de domaine Active Directory. Si un ordinateur peut localiser ces propriétés d'installation du client, il peut les utiliser au cours du déploiement du client Configuration Manager. Ces informations étant générées automatiquement, le risque d'erreur humaine propre à la saisie manuelle des propriétés d'installation est éliminé.  

 Pour plus d’informations, consultez [À propos de la publication des propriétés d’installation du client sur les services de domaine Active Directory dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Utiliser un déploiement échelonné pour gérer l’utilisation de l’UC  
 Minimisez les besoins de traitement par le processeur sur le serveur de site en utilisant un déploiement échelonné des clients. Déployez les clients en dehors des heures de travail pour que les autres services disposent de plus de bande passante pendant la journée et pour éviter de perturber le travail des utilisateurs si leur ordinateur ralentit ou nécessite un redémarrage.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Activation de la mise à niveau automatique après le déploiement client principal  
 [Les mises à niveau automatiques du client](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) sont utiles quand vous voulez mettre à niveau un petit nombre d’ordinateurs clients qui peuvent avoir été ignorés par votre méthode d’installation principale du client, par exemple car ils étaient hors connexion. 

> [!NOTE]  
>  Les améliorations des performances dans Configuration Manager vous permettent d’utiliser les mises à niveau automatiques comme méthode principale de mise à niveau des clients. Toutefois, les performances dépendent de l'infrastructure de votre hiérarchie, par exemple, le nombre de clients.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Utilisation de SMSMP et FSP pour l'installation du client avec les propriétés client.msi  
 La propriété SMSMP définit le point de gestion initial avec lequel le client communique et supprime la dépendance sur les solutions d'emplacement de service telles que les services de domaine Active Directory, DNS et WINS.  

 Utilisez la propriété FSP et installez un point d'état de secours afin de pouvoir surveiller l'installation et l'affectation du client, et identifier les problèmes de communication.  

 Pour plus d’informations sur ces options, consultez [À propos des propriétés d’installation du client dans System Center Configuration Manager](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Installer des modules linguistiques client avant d’installer les clients  
Nous vous recommandons d’installer les modules linguistiques client avant de déployer le client. Si vous installez [des modules linguistiques client](../../../../core/servers/deploy/install/language-packs.md) (pour activer des langues supplémentaires) sur un site après avoir installé des clients, vous devez réinstaller ces derniers avant qu’ils puissent utiliser ces langues. Pour les clients d’appareils mobiles, vous devez réinitialiser les appareils mobiles et les réinscrire.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Préparer les certificats PKI nécessaires à l’avance  
 Pour gérer des appareils sur Internet, des appareils mobiles inscrits et des ordinateurs Mac, vous devez disposer de certificats PKI sur les systèmes de site (points de gestion et points de distribution) et les appareils clients. Sur les réseaux de production, l'approbation de la gestion des modifications peut être requise pour utiliser de nouveaux certificats et redémarrer les serveurs de système de site. Sinon, les utilisateurs devront devront fermer la session et la rouvrir pour appliquer l'appartenance au nouveau groupe. En outre, vous devrez laisser suffisamment de temps pour la réplication des autorisations de sécurité et pour les nouveaux modèles de certificat.  

 Pour plus d’informations sur les certificats PKI nécessaires, consultez [Configuration requise des certificats PKI pour System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Configuration des paramètres client et des fenêtres de maintenance requis avant l'installation de clients  
 Même si vous pouvez [configurer les paramètres client](../../../../core/clients/deploy/configure-client-settings.md) et les fenêtres de maintenance avant ou après l’installation des clients, il est préférable de configurer les paramètres nécessaires avant d’installer les clients pour pouvoir utiliser ces paramètres dès que le client est installé. 

 Configurez des fenêtres de maintenance pour les serveurs et les appareils Windows Embedded, afin de garantir un fonctionnement ininterrompu des appareils critiques. Les fenêtres de maintenance garantissent que les mises à jour logicielles et les logiciels anti-programme malveillant nécessaires ne redémarrent pas l’ordinateur pendant les heures de bureau.  

> [!IMPORTANT]  
>  Pour les ordinateurs Windows 10 que vous souhaitez protéger avec le Filtre d’écriture unifié (UWF), vous devez configurer le périphérique pour UWF avant d’installer le client. Ceci permet à Configuration Manager d’installer le client avec un fournisseur d’informations d’identification personnalisées qui empêche des utilisateurs aux droits restreints de se connecter à l’appareil pendant qu’il est en mode maintenance.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planifier l’expérience d’inscription de vos utilisateurs pour les ordinateurs Mac et les appareils mobiles   
 Si des utilisateurs doivent inscrire leurs ordinateurs Mac et leurs appareils mobiles avec Configuration Manager, planifiez l’expérience utilisateur. Par exemple, vous pouvez créer un script pour le processus d’installation et d’inscription en utilisant une page web sur laquelle les utilisateurs indiquent seulement les informations strictement nécessaires, et leur envoyer les instructions avec un lien par e-mail.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Utiliser des filtres d’écriture basés sur des fichiers pour les appareils Windows Embedded 
 Les appareils embarqués qui utilisent des filtres d'écriture améliorés (EWF) peuvent rencontrer des resynchronisations de messages d'état. Si vous n'avez que quelques appareils embarqués qui utilisent des filtres d'écriture améliorés, il est possible que vous ne vous en rendiez pas compte. Par contre, si vous en avez beaucoup qui resynchronisent leurs informations, par exemple qui envoient un inventaire complet plutôt qu'un inventaire différentiel, cela risque de générer une augmentation détectable des paquets réseau et un traitement par le processeur plus élevé sur le serveur de site.  

 Si vous avez le choix du type de filtre d’écriture à activer, choisissez des filtres d’écriture basés sur des fichiers et configurez des exceptions pour conserver l’état du client et les données d’inventaire entre redémarrages d’appareil et préserver l’efficacité du réseau et du processeur sur le client Configuration Manager. Pour plus d’informations sur les filtres d’écriture, consultez   [Planification du déploiement de clients sur des appareils Windows Embedded dans System Center Configuration Manager](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Pour plus d’informations sur le nombre maximal de clients Windows Embedded pris en charge par un site principal, consultez [Systèmes d’exploitation pris en charge pour les clients et les appareils](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).  
