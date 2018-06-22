---
title: Sécurité et confidentialité des profils de certificat
titleSuffix: Configuration Manager
description: Découvrez les bonnes pratiques en matière de sécurité pour la gestion des profils de certificat des utilisateurs et des appareils dans System Center Configuration Manager.
ms.date: 12/28/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3393db41-900a-44c5-b950-2d46a35a198c
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: d5e9d10844a344ea56eaebb315c92675a760c983
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32350474"
---
# <a name="security-and-privacy-for-certificate-profiles-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour les profils de certificat dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


##  <a name="security-best-practices-for-certificate-profiles"></a>Bonnes pratiques pour la sécurité des profils de certificat  
 Utilisez les bonnes pratiques de sécurité suivantes lorsque vous gérez des profils de certificat pour des appareils.  

|Bonnes pratiques de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Identifiez et suivez les bonnes pratiques de sécurité pour le service d'inscription de périphériques réseau, ce qui comprend la configuration du site web Service d'inscription de périphériques réseau dans IIS (Internet Information Services) pour exiger le protocole SSL et ignorer les certificats clients.|Pour plus d'informations, voir [Guide du service d'inscription de périphérique réseau](http://go.microsoft.com/fwlink/p/?LinkId=309016) dans la bibliothèque des services de certificats Microsoft Active Directory sur TechNet.|  
|Lorsque vous configurez des profils de certificat SCEP, choisissez les options les plus sécurisées prises en charge par vos périphériques et votre infrastructure.|Identifiez, implémentez et suivez les bonnes pratiques de sécurité recommandées pour vos appareils et votre infrastructure.|  
|Spécifiez manuellement l'affinité entre utilisateur et appareil au lieu de permettre aux utilisateurs d'identifier leur appareil principal. En outre, n'activez pas la configuration basée sur l'utilisation.|Si vous cliquez sur l'option **Autoriser l'inscription du certificat uniquement sur le périphérique principal des utilisateurs** dans un profil de certificat SCEP, ne considérez pas les informations collectées à partir d'utilisateurs ou du périphérique comme faisant autorité. Si vous déployez des profils de certificat SCEP avec cette configuration et que l'affinité entre utilisateur et appareils n'est pas spécifiée par un utilisateur administratif approuvé, une élévation de privilèges et des certificats pour l'authentification peuvent être accordés à des utilisateurs qui ne sont pas autorisés.<br /><br /> **Remarque :** Si vous autorisez la configuration basée sur l’utilisation, ces informations sont collectées à l’aide de messages d’état non sécurisés par System Center Configuration Manager. Pour réduire l'étendue de cette menace, utilisez la signature SMB ou IPsec entre les ordinateurs clients et le point de gestion.|  
|N'ajoutez pas d'autorisations de lecture et d'inscription pour les utilisateurs sur les modèles de certificats ou configurez le point d'enregistrement de certificat de manière à ignorer la vérification du modèle de certificat.|Même si Configuration Manager prend en charge la vérification supplémentaire si vous ajoutez les autorisations de sécurité Lecture et Inscription pour les utilisateurs, et que vous pouvez configurer le point d’enregistrement de certificat de manière à ignorer cette vérification si l’authentification n’est pas possible, ces configurations ne représentent pas les bonnes pratiques en matière de sécurité. Pour plus d’informations, consultez [Planification d’autorisations de modèles de certificat pour les profils de certificat dans System Center Configuration Manager](../../protect/plan-design/planning-for-certificate-template-permissions.md).|  

## <a name="privacy-information-for-certificate-profiles"></a>Informations de confidentialité pour les profils de certificat  
 Vous pouvez utiliser des profils de certificat pour déployer des certificats d'Autorité de certification racine et clients et évaluer si ces appareils deviennent conformes après l'application des profils. Le point de gestion transmet les informations de compatibilité au serveur de site et System Center Configuration Manager les stocke dans la base de données de site. Les informations de compatibilité incluent des propriétés de certificat telles que le nom d'objet et l'empreinte numérique. Les informations sont chiffrées lorsque les appareils les envoient au point de gestion mais ne sont pas stockées au format chiffré dans la base de données de site. La base de données conserve les informations jusqu'à ce que la tâche de maintenance **Supprimer les données de gestion de configuration anciennes** les supprime après le délai par défaut de 90 jours. Vous pouvez configurer l'intervalle de suppression. Les informations de compatibilité ne sont pas transmises à Microsoft.  

 Les profils de certificat utilisent les informations que Configuration Manager collecte à l’aide de la découverte. Pour plus d'informations sur les informations de confidentialité pour la découverte, voir la section **Informations de confidentialité pour la découverte** dans la rubrique [Sécurité et confidentialité pour System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

> [!NOTE]  
>  Les certificats délivrés aux utilisateurs ou appareils peuvent autoriser l'accès aux informations confidentielles.  

 Par défaut, les appareils n'évaluent pas les profils de certificat. Vous devez aussi configurer les profils de certificat, puis les déployer pour des utilisateurs ou des appareils.  

 Avant de configurer les profils de certificat, pensez à vos besoins en matière de confidentialité.  
