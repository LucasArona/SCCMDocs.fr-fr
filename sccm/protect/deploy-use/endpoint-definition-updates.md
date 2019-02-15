---
title: Configurer Endpoint Protection
titleSuffix: Configuration Manager
description: Découvrez comment sélectionner et configurer des méthodes avec Endpoint Protection dans System Center Configuration Manager pour tenir à jour les définitions du logiciel anti-programme malveillant sur les ordinateurs clients.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 537dd2a7-4e44-4877-b8dd-5e1499407f8d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: f87f6c439a7f42144553406081e0b21bcef84c9b
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56123860"
---
#  <a name="configure-definition-updates-for-endpoint-protection"></a>Configurer les mises à jour des définitions pour Endpoint Protection  

*S’applique à : System Center Configuration Manager (Current Branch)*

 Avec Endpoint Protection dans System Center Configuration Manager, vous pouvez utiliser une des diverses méthodes disponibles pour tenir à jour les définitions du logiciel anti-programme malveillant sur les ordinateurs clients de votre hiérarchie. Les informations contenues dans cette rubrique peuvent vous aider à sélectionner et à configurer ces méthodes.

 Pour mettre à jour des définitions de logiciels anti-programmes malveillants, vous pouvez utiliser une ou plusieurs des méthodes suivantes :

- [Mises à jour distribuées depuis Configuration Manager](endpoint-definitions-configmgr.md) : cette méthode utilise des mises à jour logicielles de Configuration Manager pour remettre les mises à jour du moteur et des définitions aux ordinateurs de votre hiérarchie.

- [Mises à jour distribuées à partir de Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) : cette méthode utilise l’infrastructure WSUS pour remettre les mises à jour du moteur et des définitions aux ordinateurs.

- [Mises à jour distribuées à partir de Microsoft Update](endpoint-definitions-microsoft-updates.md) : cette méthode permet aux ordinateurs de se connecter directement à Microsoft Update pour télécharger les mises à jour du moteur et des définitions. Cette méthode peut être utile pour les ordinateurs qui ne sont pas souvent connectés au réseau d’entreprise.

- [Mises à jour distribuées à partir du Centre de protection Microsoft contre les programmes malveillants](endpoint-definitions-protection-center.md) : cette méthode télécharge les mises à jour des définitions à partir du Centre de protection Microsoft contre les programmes malveillants.

- [Mises à jour à partir de partages de fichiers UNC](endpoint-definitions-network.md) : avec cette méthode, vous pouvez enregistrer les dernières mises à jour du moteur et des définitions dans un partage sur le réseau. Les clients peuvent ensuite accéder au réseau pour installer les mises à jour.

  Vous pouvez configurer plusieurs sources de mise à jour de définition et contrôler l’ordre dans lequel elles sont évaluées et appliquées. Cette opération s’effectue dans la boîte de dialogue **Configurer les sources de mise à jour de définition** quand vous créez une stratégie de logiciel anti-programme malveillant.

> [!IMPORTANT]
>  Pour les PC Windows 10, vous devez configurer Endpoint Protection pour mettre à jour les définitions de programmes malveillants pour Windows Defender.

## <a name="how-to-configure-definition-update-sources"></a>Comment configurer des sources de mise à jour de définition
 Utilisez la procédure suivante pour configurer les sources de mise à jour de définition à utiliser pour chaque stratégie de logiciel anti-programme malveillant.

1.  Dans la console Configuration Manager, cliquez sur **Ressources et Conformité**.

2.  Dans l’espace de travail **Ressources et Conformité** , développez **Endpoint Protection**, puis cliquez sur **Stratégies anti-programme malveillant**.

3.  Ouvrez la page de propriétés de la **Stratégie de logiciel anti-programme malveillant par défaut** ou créez une stratégie de logiciel anti-programme malveillant. Pour plus d’informations sur la création de stratégies de logiciel anti-programme malveillant, consultez [Guide pratique pour créer et déployer des stratégies de logiciel anti-programme malveillant pour Endpoint Protection dans System Center Configuration Manager](endpoint-antimalware-policies.md).

4.  Dans la section **Mises à jour de définitions** de la boîte de dialogue des propriétés du logiciel anti-programme malveillant, cliquez sur **Définir la source**.

5.  Dans la boîte de dialogue **Configurer les sources de mise à jour de définition** , sélectionnez les sources à utiliser pour les mises à jour de définition. Vous pouvez cliquer sur **Haut** ou **Bas** pour modifier l’ordre dans lequel ces sources sont utilisées.

6.  Cliquez sur **OK** pour fermer la boîte de dialogue **Configurer les sources de mise à jour de définition** .

## <a name="configure-endpoint-protection-definitions"></a>Configurer les définitions Endpoint Protection

-   [Mises à jour distribuées depuis Configuration Manager](endpoint-definitions-configmgr.md) : cette méthode utilise des mises à jour logicielles de Configuration Manager pour remettre les mises à jour du moteur et des définitions aux ordinateurs de votre hiérarchie.

-   [Mises à jour distribuées à partir de Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) : cette méthode utilise l’infrastructure WSUS pour remettre les mises à jour du moteur et des définitions aux ordinateurs.

-   [Mises à jour distribuées à partir de Microsoft Update](endpoint-definitions-microsoft-updates.md) : cette méthode permet aux ordinateurs de se connecter directement à Microsoft Update pour télécharger les mises à jour du moteur et des définitions. Cette méthode peut être utile pour les ordinateurs qui ne sont pas souvent connectés au réseau d’entreprise.

-   Mises à jour distribuées à partir du Centre de protection Microsoft contre les programmes malveillants : cette méthode télécharge les mises à jour des définitions à partir du Centre de protection Microsoft contre les programmes malveillants.

-   [Mises à jour à partir de partages de fichiers UNC](endpoint-definitions-network.md) : avec cette méthode, vous pouvez enregistrer les dernières mises à jour du moteur et des définitions dans un partage sur le réseau. Les clients peuvent ensuite accéder au réseau pour installer les mises à jour.
