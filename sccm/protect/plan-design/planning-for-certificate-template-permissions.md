---
title: Planification d’autorisations de modèles de certificat
titleSuffix: Configuration Manager
description: Informez-vous sur la planification des autorisations à configurer pour les modèles de certificat que System Center Configuration Manager utilise.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 44be093d079a06ac2cbc7e8fa82392fa3afd4f72
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32349362"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-system-center-configuration-manager"></a>Planification d’autorisations de modèles de certificat pour les profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


Les informations suivantes peuvent vous aider à prévoir comment configurer des autorisations pour les modèles de certificat que System Center Configuration Manager utilise quand vous déployez des profils de certificat.  

## <a name="default-security-permissions-and-considerations"></a>Considérations et autorisations de sécurité par défaut  
 Les autorisations de sécurité par défaut requises pour les modèles de certificat que System Center Configuration Manager utilise pour demander des certificats pour les utilisateurs et les appareils sont les suivantes :  

-   Lecture et Inscription pour le compte utilisé par le pool d'applications du service d'inscription de périphériques réseau  

-   Lecture pour le compte qui exécute la console System Center Configuration Manager  

 Pour plus d’informations sur ces autorisations de sécurité, consultez [Configuration de l’infrastructure des certificats](../deploy-use/certificate-infrastructure.md).  

 Lorsque vous utilisez cette configuration par défaut, les utilisateurs et les périphériques ne peuvent pas demander directement des certificats depuis les modèles de certificat et toutes les demandes doivent être lancées par le service d'inscription de périphériques réseau. Il s'agit d'une restriction importante car ces modèles de certificat doivent être configurés avec **Fourni dans la demande** comme objet de certificat, ce qui signifie qu'il existe un risque d'emprunt d'identité si un utilisateur non autorisé ou un périphérique compromis a demandé un certificat. Dans la configuration par défaut, le service d'inscription de périphériques réseau doit lancer une telle demande. Toutefois, ce risque d'emprunt d'identité demeure si le service qui exécute le service d'inscription de périphériques réseau est compromis. Afin d'éviter ce risque, suivez toutes les meilleures pratiques de sécurité pour le service d'inscription de périphériques réseau et l'ordinateur qui exécute ce service de rôle.  

 Si les autorisations de sécurité par défaut ne répondent pas à vos besoins, vous avez une autre option pour configurer les autorisations de sécurité sur les modèles de certificat : vous pouvez ajouter des autorisations Lecture et Inscription pour les utilisateurs et les ordinateurs.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Ajout d'autorisations Lecture et Inscription pour les utilisateurs et les ordinateurs  
 L’ajout d’autorisations Lecture et Inscription pour les utilisateurs et les ordinateurs peut être adapté si une équipe distincte gère votre équipe d’infrastructure d’autorité de certification et qu’elle veut que System Center Configuration Manager vérifie que les utilisateurs disposent d’un compte des services de domaine Active Directory valide avant de leur envoyer un profil de certificat pour demander un certificat utilisateur. Pour cette configuration, vous devez spécifier un ou plusieurs groupes de sécurité contenant les utilisateurs et leur accorder des autorisations Lecture et Inscription sur les modèles de certificat. Dans ce scénario, l'administrateur de l'autorité de certification gère le contrôle de sécurité.  

 Vous pouvez également spécifier un ou plusieurs groupes de sécurité qui contiennent des comptes d'ordinateur et accorder à ces groupes des autorisations Lecture et Inscription sur les modèles de certificat. Si vous déployez un profil de certificat d'ordinateur sur un ordinateur membre du domaine, le compte d'ordinateur de cet ordinateur doit bénéficier des autorisations Lecture et Inscription. Ces autorisations ne sont pas requises si l’ordinateur n’est pas membre du domaine, par exemple, s’il s’agit d’un ordinateur de groupe de travail ou d’un appareil mobile personnel.  

 Bien que cette configuration utilise un contrôle de sécurité supplémentaire, nous ne la recommandons pas comme meilleure pratique. En effet, les utilisateurs ou les propriétaires spécifiés des appareils pourraient demander des certificats indépendamment de System Center Configuration Manager, et fournir des valeurs pour l’objet du certificat qui pourraient être utilisées pour emprunter l’identité d’un autre utilisateur ou d’un autre appareil.  

 En outre, si vous spécifiez des comptes qui ne peuvent pas être authentifiés au moment de la demande du certificat, par défaut, la demande de certificat échoue. Par exemple, la demande de certificat échoue si le serveur exécutant le service d'inscription de périphériques réseau se trouve dans une forêt Active Directory non approuvée par la forêt contenant le serveur de système de site du point d'enregistrement de certificat. Vous pouvez configurer le point d'enregistrement de certificat afin qu'il continue si un compte ne peut pas être authentifié car un contrôleur de domaine ne répond pas. Toutefois, il ne s'agit pas d'une meilleure pratique de sécurité.  

 Notez que si le point d'enregistrement de certificat est configuré pour rechercher des autorisations de compte et qu'un contrôleur de domaine est disponible et rejette la demande d'authentification (par exemple, le compte est verrouillé ou a été supprimé), la demande d'inscription de certificat échouera.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>Pour rechercher des autorisations Lecture et Inscription pour les utilisateurs et les ordinateurs membres du domaine  

1.  Sur le serveur de système de site qui héberge le point d’enregistrement de certificat, créez la clé de Registre DWORD suivante de valeur 0 : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Si un compte ne peut pas être authentifié car un contrôleur de domaine ne répond pas et que vous souhaitez ignorer la vérification des autorisations :  

    -   Sur le serveur de système de site qui héberge le point d’enregistrement de certificat, créez la clé de Registre DWORD suivante de valeur 1 : HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Sur l'autorité de certification émettrice, dans l'onglet **Sécurité** des propriétés du modèle de certificat, ajoutez un ou plusieurs groupes de sécurité afin d'accorder aux comptes d'utilisateur ou de périphérique des autorisations Lecture et Inscription.  
