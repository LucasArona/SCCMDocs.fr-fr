---
title: Sécurité et confidentialité pour la migration
titleSuffix: Configuration Manager
description: Bonnes pratiques et informations de confidentialité pour la migration vers votre environnement System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8cc6c1cee04e815c8a34f24236333fb927ed44fc
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-migration-to-system-center-configuration-manager"></a>Sécurité et confidentialité pour la migration vers System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient les bonnes pratiques en matière de sécurité et les informations de confidentialité pour la migration vers votre environnement System Center Configuration Manager.  

## <a name="security-best-practices-for-migration"></a>Meilleures pratiques de sécurité pour la migration  
 Utilisez les meilleures pratiques de sécurité suivantes pour la migration.  

|Bonnes pratiques de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Utilisez le compte d'ordinateur pour le compte du fournisseur SMS du site source et le compte SQL Server du site source plutôt qu'un compte d'utilisateur.|Si vous devez utiliser un compte d'utilisateur pour la migration, supprimez les détails du compte une fois la migration terminée.|  
|Lorsque vous migrez le contenu d'un point de distribution d'un site source vers un point de distribution d'un site de destination, utilisez IPsec.|Bien que le contenu migré soit haché pour détecter la falsification, si les données sont modifiées pendant leur transfert, la migration échoue.|  
|Veillez à restreindre et surveiller les utilisateurs administratifs qui peuvent créer des tâches de migration.|L'intégrité de la base de données de la hiérarchie de destination dépend de l'intégrité des données que l'utilisateur administratif décide d'importer à partir de la hiérarchie source. En outre, cet utilisateur administratif peut lire toutes les données de la hiérarchie source.|  

### <a name="security-issues-for-migration"></a>Problèmes de sécurité pour la migration  
La migration présente les problèmes de sécurité suivants :  

-   Les clients dont l'accès à un site source a été bloqué peuvent être attribués correctement à la hiérarchie de destination, avant que leur enregistrement de client n'ait été migré.  

     Bien que Configuration Manager conserve l'état de blocage des clients que vous migrez, ces derniers peuvent être correctement affectés à la hiérarchie de destination si cette affectation a lieu avant la fin de la migration de l'enregistrement de client.  

-   Les messages d'audit ne sont pas migrés.  

Lorsque vous migrez les données d'un site source vers un site de destination, vous perdez toutes les informations d'audit de la hiérarchie source.  

## <a name="privacy-information-for-migration"></a>Informations de confidentialité pour la migration  
 La migration découvre des informations à partir des bases de données de site que vous identifiez dans une infrastructure source et stocke ces données dans la base de données de la hiérarchie de destination. Les informations que System Center Configuration Manager peut découvrir à partir d'un site ou d'une hiérarchie source dépendent des fonctionnalités qui ont été activées dans l'environnement source, ainsi que des opérations de gestion réalisées dans cet environnement.  

 Pour plus d'informations sur la sécurité et la confidentialité, consultez l'une des rubriques suivantes :  

-   Pour plus d'informations sur les informations de confidentialité pour Configuration Manager 2007, voir [Sécurité et confidentialité pour Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) dans la bibliothèque de documentation de Configuration Manager 2007.  

-   Pour plus d'informations sur les informations de confidentialité pour System Center 2012 Configuration Manager, voir [Sécurité et confidentialité pour System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) dans la bibliothèque de documentation de System Center 2012 Configuration Manager.  

-   Pour plus d’informations sur les informations de confidentialité pour System Center Configuration Manager, voir [Sécurité et confidentialité pour System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

Vous pouvez migrer l'intégralité des données prises en charge d'un site source vers une hiérarchie de destination ou uniquement une partie de ces données.  

La migration n'est pas activée par défaut et nécessite plusieurs étapes de configuration. Les informations relatives à la migration ne sont pas envoyées à Microsoft.  

Avant de migrer les données d'une hiérarchie source, analysez vos besoins en matière de confidentialité.  
