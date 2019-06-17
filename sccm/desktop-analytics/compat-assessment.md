---
title: Évaluation de la compatibilité
titleSuffix: Configuration Manager
description: En savoir plus sur l’évaluation de compatibilité pour les applications Windows et les pilotes dans Analytique de bureau.
ms.date: 06/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.collection: M365-identity-device-management
ms.openlocfilehash: bef2c11732177dfb842f0961dc2d5d5a69edd55e
ms.sourcegitcommit: d47d2f03482e48d343e2139a341e61022331e6c2
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/14/2019
ms.locfileid: "67148096"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Évaluation de la compatibilité dans Desktop Analytique

> [!Note]  
> Ces informations est lié à un service en version préliminaire qui peut être substantiellement modifié avant sa commercialisation. Microsoft exclut toute garantie, expresse ou implicite, concernant les informations fournies ici.  

Évaluations de la mise à niveau dans Analytique de Windows ont été génériques, par exemple : Faites attention ou le correctif n’est disponible. Il ne fournit pas un indicateur visuel sur la façon de hiérarchiser les applications ou pilotes avec des problèmes ou de mettre à niveau des insights. Postes de travail Analytique remplace cette fonctionnalité avec **risque de compatibilité**. Analytique bureau affiche l’évaluation pour les applications que dans la vue de déploiement pour un scénario de pré-mise à niveau. Les applications basées sur les insights que Microsoft obtient à partir des ordinateurs inclus dans un plan de déploiement en cours sont classés.

Analytique de postes de travail utilise les catégories d’évaluation de compatibilité suivantes :

- **Faible** : Le service a trouvé aucun signaux pour cette application de mettre en danger pour un Windows mise à niveau. Il est sans doute sur le système d’exploitation cible en tant que-est.  

- **Support**: Analytique indique que l’application peut altérée fonctionnalité, bien que la mise à jour est probablement possible.  

- **Haute**: L’application est presque certaine Échec pendant ou après la mise à niveau. Elle peut avoir besoin d’une mise à jour.  

- **Inconnu** : L’application n’a pas été évaluée. Il n’existe aucune autre information comme *problèmes connus de MS* ou *prêt pour Windows*.  

Dans la liste des ressources d’application ou le pilote dans un plan de déploiement, vous verrez cette valeur pour chaque élément multimédia dans le **risque de compatibilité** colonne.


## <a name="app-risk-assessment"></a>Évaluation des risques application

Il existe plusieurs sources Desktop Analytique utilise pour générer la note d’évaluation pour les applications :

- [Problèmes connus de Microsoft](#microsoft-known-issues)
- [Prêt pour le catalogue Windows](#ready-for-windows)
- [Informations avancées](#advanced-insights)

Vous pouvez trouver l’évaluation pour chaque source de l’application de bureau Analytique. Dans la liste des ressources d’application dans un plan de déploiement, sélectionnez une application individuelle pour ouvrir son volet de menu volant de propriétés. Vous verrez un niveau global de la recommandation et d’évaluation. Le **les facteurs de risque de compatibilité** section affiche les détails pour ces évaluations.


## <a name="microsoft-known-issues"></a>Problèmes connus de Microsoft

Postes de travail Analytique examine la base de données de compatibilité application Microsoft pour les problèmes connus. Elle utilise cette base de données pour déterminer les blocs de compatibilité existants pour les applications accessibles à partir de Microsoft ou d’autres éditeurs. Cette vérification s’applique uniquement à la cible du système d’exploitation pour le plan de déploiement que vous sélectionnez.

Vous verrez les problèmes suivants dans le volet de propriétés d’application en tant que **problèmes connus de MS**:

### <a name="application-is-removed-during-upgrade"></a>Application a été supprimée pendant la mise à niveau

Windows a détecté des problèmes de compatibilité. L’application ne sont pas migrées vers la nouvelle version du système d’exploitation. Aucune action n’est requise pour la mise à niveau continuer.

### <a name="blocking-upgrade"></a>Mise à niveau de blocage

Windows a détecté des problèmes de blocage et ne peut pas supprimer l’application au cours de la mise à niveau. Il peut ne pas fonctionner sur la nouvelle version du système d’exploitation. Avant la mise à niveau, supprimez l’application. Réinstallez et testez-la sur la nouvelle version du système d’exploitation.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Bloque la mise à niveau, mais peut être réinstallés après la mise à niveau

L’application est compatible avec la nouvelle version du système d’exploitation, mais ne sont pas migrées. Supprimer l’application avant la mise à niveau de Windows. Réinstaller sur la nouvelle version du système d’exploitation.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Bloque la mise à niveau, de mettre à jour l’application à la version la plus récente

La version existante de l’application n’est pas compatible avec la nouvelle version du système d’exploitation et ne sont pas migrées. Une version compatible de l’application est disponible. Mettre à jour l’application avant la mise à niveau.

### <a name="disk-encryption-blocking-upgrade"></a>Blocage mise à niveau de chiffrement de disque

Les fonctionnalités de chiffrement de l’application bloquent la mise à niveau. Désactiver la fonctionnalité de chiffrement avant de mettre à niveau de Windows et l’activer après la mise à niveau.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Ne fonctionne pas avec le nouveau système d’exploitation, mais ne bloquent pas mise à niveau

L’application n’est pas compatible avec la nouvelle version du système d’exploitation, mais ne bloque pas la mise à niveau. Aucune action n’est requise pour la mise à niveau continuer. Installer une version compatible de l’application sur la nouvelle version du système d’exploitation.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Ne fonctionne pas avec le nouveau système d’exploitation et bloqueront la mise à niveau

L’application n’est pas compatible avec la nouvelle version du système d’exploitation et bloque la mise à niveau. Supprimer l’application avant la mise à niveau. Une version compatible de l’application peut-être être disponible.

### <a name="evaluate-application-on-new-os"></a>Évaluer l’application sur le nouveau système d’exploitation

Windows sera migrer l’application, mais il a détecté des problèmes qui peuvent affecter les performances de l’application sur la nouvelle version du système d’exploitation. Aucune action n’est requise pour la mise à niveau continuer. Tester l’application sur la nouvelle version du système d’exploitation.

### <a name="may-block-upgrade-test-application"></a>Peut bloquer la mise à niveau, tester des applications

Windows a détecté des problèmes qui peuvent interférer avec la mise à niveau, mais nécessitent une étude approfondie. Tester le comportement de l’application au cours de la mise à niveau. Si elle bloque la mise à niveau, supprimez-le avant la mise à niveau. Puis le réinstaller et tester sur la nouvelle version du système d’exploitation.

### <a name="multiple"></a>Plusieurs

Plusieurs problèmes affectent l’application. Sélectionnez **requête** pour afficher les détails sur les problèmes détectés par Windows.

### <a name="reinstall-application-after-upgrading"></a>Réinstallez l’application après la mise à niveau

L’application est compatible avec la nouvelle version du système d’exploitation, mais vous devez le réinstaller une fois que vous mettez à niveau Windows. Le processus de mise à niveau supprime l’application. Aucune action n’est requise pour la mise à niveau continuer. Réinstallez l’application sur la nouvelle version du système d’exploitation.


## <a name="ready-for-windows"></a>Prêt pour Windows

Le [prêt pour Windows](https://www.readyforwindows.com) catalogue d’applications met en corrélation les sources de données suivantes :

- Données de diagnostic à partir d’autres clients qui signalent les mêmes applications
- Des vérifications supplémentaires de Microsoft comme blocs de compatibilité sur un appareil

Les catégories possibles sont :

- **Hautement adoptées**: Au moins 100 000 appareils Windows 10 commerciales ont installé cette application.  

- **Adopté**: Au moins 10 000 appareils Windows 10 commerciales ont installé cette application.  

- **Données insuffisantes**: Trop peu d’appareils Windows 10 commerciale partagent des informations pour cette application pour Microsoft de catégoriser son adoption.

- **Contactez le développeur**: Il existe peut-être des problèmes de compatibilité avec cette version de l’application. Microsoft vous recommande de contacter le fournisseur de logiciels pour en savoir plus. Pour plus d’informations, consultez [prêt pour Windows](https://www.readyforwindows.com/).  

- **Inconnu** : Aucune information de prêt pour Windows n’est disponible pour cette version de cette application. Informations peuvent être disponibles pour d’autres versions de l’application au [prêt pour Windows](https://www.readyforwindows.com/).  

### <a name="support-statement"></a>Instruction de prise en charge

Si le fournisseur de logiciel prend en charge une ou plusieurs versions de cette application sur Windows 10, vous verrez cette instruction dans le volet de propriétés d’application. Dans la section de facteurs de risque de compatibilité, examinons le **prend en charge instruction**.



## <a name="advanced-insights"></a>Informations avancées

Analytique de bureau peut également détecter les problèmes à l’aide des informations supplémentaires suivantes :

### <a name="adopted-version-available"></a>Version adoptée disponible

Il existe une autre version de cette application est hautement adoptée par d’autres clients. Ce signal utilise des données à partir de prêt pour Windows. S’il existe des bloqueurs de mise à niveau avec votre version actuelle, envisagez de déployer la version de remplacement à la place.

### <a name="driver-dependency"></a>Dépendance de pilote

L’application dépend d’un pilote. Analytique bureau vous recommande de l’application de test pilote. Cela devrait fonctionner correctement pour le pilote, mais vous trouverez les régressions. Si vous rencontrez des problèmes, contactez l’éditeur pour demander une version compatible avec Windows 10.



## <a name="driver-risk-assessment"></a>Évaluation des risques de pilote

Postes de travail Analytique répertorie également et groupes par la disponibilité de tous les pilotes qui ne sont pas migrées vers la version du système d’exploitation.

Vous trouverez l’évaluation sur le pilote dans Analytique de bureau. Dans la liste des ressources de pilote dans un plan de déploiement, sélectionnez un pilote individuel pour ouvrir son volet de menu volant de propriétés. Vous verrez un niveau global de la recommandation et d’évaluation. Le **les facteurs de risque de compatibilité** section affiche les détails pour ces évaluations.

| Disponibilité du pilote | Action requise ? | Cela signifie que | Guidance |
|---------------------|------------------|---------------|----------|
| Disponible dans l’emploi | Non, pour la reconnaissance uniquement | La version actuellement installée d’une application ou le pilote ne sont pas migrées vers la nouvelle version du système d’exploitation. Une version compatible est installée avec la nouvelle version du système d’exploitation. | Aucune action n’est requise pour la mise à niveau continuer. |
| Importer à partir de la mise à jour de Windows | Oui | La version actuellement installée d’un pilote ne sont pas migrées vers la nouvelle version du système d’exploitation. Une version compatible est disponible à partir de Windows Update. | Si l’ordinateur reçoit automatiquement les mises à jour à partir de Windows Update, aucune action n’est requise. Sinon, importer un nouveau pilote à partir de Windows Update une fois que vous mettez à niveau Windows. |
| Disponible dans l’emploi et à partir de Windows Update | Oui | La version actuellement installée d’un pilote ne sont pas migrées vers la nouvelle version du système d’exploitation. Bien qu’un nouveau pilote est installé au cours de la mise à niveau, une version plus récente est disponible à partir de Windows Update. | Si l’ordinateur reçoit automatiquement les mises à jour à partir de Windows Update, aucune action n’est requise. Sinon, importer un nouveau pilote à partir de Windows Update une fois que vous mettez à niveau Windows. |
| Vérifiez auprès de fournisseur | Oui | Le pilote ne sont pas migrées vers la nouvelle version du système d’exploitation et d’Analytique de bureau ne peut pas trouver une version compatible. | Pour une solution, vérifiez auprès des fournisseurs indépendants (IHV) qui fabrique le pilote ou le fabricant (OEM) qui a fourni l’appareil. |


## <a name="see-also"></a>Voir aussi

FastTrack Center Benefit pour Windows 10 fournit l’accès aux **Desktop App assurer**. Cet avantage est un service conçu pour résoudre les problèmes avec Windows 10 et la compatibilité des applications Office 365 ProPlus. Pour plus d’informations, consultez [Desktop App assurer](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
