---
title: Résoudre les problèmes liés à SCAP
titleSuffix: Configuration Manager
description: Découvrez comment résoudre les problèmes liés aux extensions SCAP pour Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 58a3c69e6206aa651e55f96286f98f64f748de70
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56137134"
---
# <a name="troubleshoot-the-scap-extensions-for-configuration-manager"></a>Résoudre les problèmes liés aux extensions SCAP pour Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Les extensions SCAP pour Configuration Manager sont conçues pour fonctionner avec les flux de données SCAP destinés à l’outil SCAP validé, doté d’une fonctionnalité ACS pour prendre en charge USGCB. Normalement, vous ne rencontrerez aucun problème avec ces flux de données USGCB SCAP, téléchargés à partir du site web de l’institut NIST.

Diagnostiquez et résolvez les problèmes à l’aide des méthodes suivantes :  

- Vérifiez que les composants (scmdcm.msi) du client des extensions SCAP sont installés sur tous les ordinateurs cibles.  

- Examinez la sortie du fichier journal de l’outil Microsoft.Sces.ScapToDcm.exe.  

- Passez en revue les problèmes courants et solutions pendant l’utilisation des extensions SCAP.  

- Contactez Microsoft si vous avez des questions ou des commentaires sur les extensions SCAP.



## <a name="review-microsoftscesscaptodcmexe-log"></a>Examiner le journal de Microsoft.Sces.ScapToDcm.exe

L’outil Microsoft.Sces.ScapToDcm.exe crée un fichier journal nommé personnalisé, quand vous spécifiez le paramètre `–log`. Le fichier journal contient des informations sur les résultats de l’exécution de l’outil Microsoft.Sces.ScapToDcm.exe. Par exemple, il contient le nombre d’éléments du fichier d’entrée XCCDF/DataStream qui ont été supprimés ou ignorés au moment de l’exécution de l’outil Microsoft.Sces.ScapToDcm.exe.

Le tableau suivant répertorie certaines informations qui s'affichent dans le fichier journal ainsi qu'une description de chaque type d'informations.

### <a name="information-found-in-the-microsoftscesscaptodcmexe-log-file"></a>Informations se trouvant dans le fichier journal Microsoft.Sces.ScapToDcm.exe

| Informations | Description |
| --- | --- |
| **Drop** | Un élément peut être supprimé, car le type de test n’est pas pris en charge. |
| **Skip** | L'ID de définition OVAL correspond à une plateforme non valide. </br> </br> L’ID de définition OVAL n’est pas référencé par le fichier d’entrée XCCDF/DataStream.</br> </br> L’ID de test OVAL n’est pas référencé par le fichier d’entrée XCCDF/DataStream. </br> </br> L’ID du profil XCCDF ne contient pas d’instructions `@select` avec la valeur 1. </br> </br> L’ID du profil XCCDF inclut un attribut abstrait avec la valeur true. </br> </br> L’ID du profil XCCDF ne contient pas de règle de qualification.|



## <a name="common-problems-and-solutions"></a>Problèmes courants et solutions

Voici certains problèmes courants et les solutions qui vont vous aider à les résoudre.

- Vous voyez un état **Error** ou **Unknown** (Inconnu) pour une base de référence et Internet Explorer ne peut pas afficher le rapport correctement. L’erreur du navigateur indique que le rapport est vide ou non valide (« The report is either empty or invalid »).  

     - Réexécutez la base de référence. Sélectionnez la base de référence et cliquez sur **Evaluate**. Ensuite, patientez avant de vérifier **l’état de conformité**/**la dernière mise à jour de l’évaluation**. Une fois la date de dernière évaluation mise à jour à la date et heure actuelles, ce qui signifie que l’évaluation est terminée, sélectionnez la base de référence et réexaminez le rapport.  

     - Si Internet Explorer ne peut toujours pas afficher le rapport, la base de référence est peut-être trop grande. Régénérez le contenu à l’aide d’une taille de lot inférieure pour créer des bases de référence enfants plus petites.  

     - Si ce problème se produit sur les bases de référence parents, essayez de déployer les bases de référence enfants à la place.  

- J’ai créé des objets de stratégie de groupe (GPO) qui incluent les paramètres USGCB prescrits. Je les ai liés aux unités d’organisation (UO) qui contiennent des ordinateurs exécutant Windows 7. Les rapports de conformité indiquent que certains paramètres ne sont pas configurés correctement.  

     - Il est possible que les autorisations de la stratégie de groupe soient incorrectes ou n’aient pas été liées à l’unité d’organisation correcte.  

     - Il est plus probable que les nouveaux paramètres ne soient pas encore effectifs. Par défaut, les clients Active Directory recherchent les mises à jour de stratégie de groupe toutes les 90 minutes. Ce cycle peut être l’une des raisons pour laquelle les paramètres semblent ne pas être appliqués, même si vous avez correctement configuré les stratégies.  

     - Pour que plusieurs paramètres d’ordinateur prennent effet, un redémarrage est nécessaire. Par exemple, le paramètre de **Chiffrement système : Utilisez des algorithmes conformes aux normes FIPS (Federal Information Processing Standard) pour le chiffrement, le hachage et la signature** nécessite le redémarrage de l’ordinateur avant que Windows puisse utiliser les algorithmes de chiffrement spécifiés. Ignorez l’intervalle d’actualisation de la stratégie de groupe en entrant la commande suivante à une invite de commandes avec des privilèges d’administrateur : `gpupdate /force`. Une fois l'actualisation de la stratégie de groupe terminée, redémarrez l'ordinateur pour vous assurer que tous les paramètres sont effectifs. Pour plus d’informations, consultez [Description de l’utilitaire de mise à jour de Stratégie de groupe](https://support.microsoft.com/help/298444).

- Je ne parviens pas à établir une connexion avec la base de données à l’aide de mes informations d’organisation.  

     - Pour plus d’informations sur la façon de configurer la connexion à la base de données, consultez [Installer et configurer SCAP](/sccm/compliance/plan-design/scap/install-configure-scap).  
