---
title: Messages d'erreur
titleSuffix: Configuration Manager
description: En savoir plus sur les messages d’erreur provenant de Package Conversion Manager.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 0d3cf6e1-b295-4b05-821d-e9f57c74ca14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: a10ebaad901181e80a449c5c64274a0d68b53100
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56126443"
---
# <a name="technical-reference-for-package-conversion-manager-error-messages"></a>Informations techniques de référence sur les messages d'erreur de Package Conversion Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

<!--1357861-->

Cet article décrit les messages d’erreur affichés par Package Conversion Manager. Il indique également les causes possibles de l’erreur et les méthodes pour la corriger. Package Conversion Manager consigne les messages d’erreur dans le fichier **PCMTrace.log**. Pour plus d’informations, y compris le contrôle du niveau de détail, consultez la rubrique [Fichiers journaux](/sccm/apps/pcm/troubleshoot-pcm#log-files).


#### <a name="application-creation-failed-with-the-following-exception"></a>Échec de la création de l'application avec l'exception suivante

L'exception spécifiée s'est produite pendant l'envoi de l'objet d'application au serveur Configuration Manager.

Vérifiez vos autorisations dans Configuration Manager et votre connexion, puis réessayez. Si ces actions ne règlent pas le problème, examinez les fichiers **PCMtrace.log** (niveau de détail 4) et **SMSProv.log**.


#### <a name="conversion-error--applies-to-a-package-transform-status"></a>Erreur de conversion – S'APPLIQUE À UN ÉTAT DE TRANSFORMATION DU PACKAGE

une exception générale s'est produite pendant la conversion du package. Examinez le fichier **PCMtrace.log** (niveau de détail 4).

Vérifiez les autorisations des utilisateurs pour le partage réseau (source de données du package) et votre connectivité, puis réessayez. Si ces actions ne règlent pas le problème, examinez les fichiers **PCMtrace.log** (niveau de détail 4).


#### <a name="did-not-find-a-converted-package-and-its-resultant-application-in-the-workflow-outputs"></a>Un package converti et son application résultante sont introuvables dans les sorties de flux de travail
l'application (package converti/programme) a été supprimée.

modifiez le package/programme dépendant pour vérifier qu'il existe.


#### <a name="objects-were-not-created-successfully"></a>Des objets n'ont pas été créés correctement
Plusieurs causes sont possibles.

Vérifiez vos autorisations dans Configuration Manager et votre connexion, puis réessayez. Si ces actions ne règlent pas le problème, examinez les fichiers **PCMtrace.log** (niveau de détail 4) et **SMSProv.log**.


#### <a name="please-close-the-wizard-and-resolve-any-issues-with-the-selected-package-see-pcmtracelog-for-more-details"></a>Fermez l'Assistant et corrigez les problèmes liés au package sélectionné. Pour plus d’informations, consultez le fichier PCMTrace.Log
Plusieurs causes sont possibles.

Vérifiez vos autorisations dans Configuration Manager et votre connexion, puis réessayez. Si ces actions ne règlent pas le problème, examinez les fichiers **PCMtrace.log** (niveau de détail 4) et **SMSProv.log**.


#### <a name="some-deployment-types-are-missing-detection-methods-all-deployment-types-must-have-detection-methods"></a>Des méthodes de détection sont manquantes dans certains types de déploiement. Tous les types de déploiement doivent comporter des méthodes de détection
des méthodes de détection sont manquantes dans le programme.

Ajoutez une ou plusieurs méthodes de détection pendant le processus **Corriger et convertir**.


#### <a name="there-was-an-error-preparing-the-package-for-conversion"></a>Une erreur s'est produite pendant la préparation du package pour la conversion
Plusieurs causes sont possibles.

Vérifiez vos autorisations dans Configuration Manager et votre connexion, puis réessayez. Si ces actions ne règlent pas le problème, examinez les fichiers **PCMtrace.log** (niveau de détail 4) et **SMSProv.log**.


