---
title: Résoudre les problèmes liés à SCAP
titleSuffix: Configuraton Manager
description: Importer les paramètres de conformité SCAP sous la forme de bases de référence de configuration et exporter les résultats
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 27261853-1641-4826-98c6-afbb73a1209d
author: aczechowski
ms.author: aaroncz
manager: dougeby
robots: noindex,nofollow
ms.openlocfilehash: 05010d73916ac4c012c157a470ed98dce47fc747
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32334478"
---
# <a name="troubleshoot-the-scap-extensions-for-microsoft-system-center-configuration-manager"></a>Résoudre les problèmes liés aux Extensions SCAP pour Microsoft System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Tip]  
> Cette fonctionnalité a été introduite dans Technical Preview version 1803 sous la forme d’une [fonctionnalité en préversion](/sccm/core/servers/manage/pre-release-features). Cette préversion des Extensions SCAP peut être installée sur toutes les versions actuellement prises en charge de Configuration Manager Current Branch et LTSB 1606. À compter de Technical Preview 1803, le fichier d’installation se trouve dans cd.latest\SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi. 

Les Extensions SCAP pour Microsoft System Center Configuration Manager sont conçues pour fonctionner avec les flux de données SCAP destinés à l'outil SCAP validé, doté d'une fonctionnalité ACS pour prendre en charge USGCB. Normalement, vous ne rencontrerez aucun problème avec ces flux de données USGCB SCAP, téléchargés à partir du site web de l’institut NIST.

Toutefois, vous pouvez diagnostiquer et résoudre les problèmes éventuels à l’aide des méthodes suivantes :

- Vérifiez que les composants (scmdcm.msi) du client Extensions SCAP sont installés sur tous les ordinateurs cibles.
- Examinez la sortie du fichier journal de l’outil Microsoft.Sces.ScapToDcm.exe.
- Passez en revue les problèmes courants et solutions lors de l'utilisation des Extensions SCAP.
- Contactez Microsoft si vous avez des questions ou des commentaires sur les Extensions SCAP.



## <a name="review-microsoftscesscaptodcmexe-tool-log"></a>Examiner le journal de l’outil Microsoft.Sces.ScapToDcm.exe

L’outil Microsoft.Sces.ScapToDcm.exe crée un fichier journal nommé personnalisé, quand le paramètre –log est spécifié. Le fichier journal contient des informations sur les résultats de l’exécution de l’outil Microsoft.Sces.ScapToDcm.exe. Par exemple, le fichier journal contient le nombre d’éléments du fichier d’entrée XCCDF/DataStream qui ont été supprimés ou ignorés lors de l’exécution de l’outil Microsoft.Sces.ScapToDcm.exe.

Le tableau suivant répertorie certaines informations qui s'affichent dans le fichier journal ainsi qu'une description de chaque type d'informations.

### <a name="description-of-information-found-in-microsoftscesscaptodcmexe-log-files"></a>Description des informations se trouvant dans les fichiers journaux Microsoft.Sces.ScapToDcm.exe

| Informations | Description |
| --- | --- |
| Supprimer | Un élément peut être supprimé, car le type de test n'est pas pris en charge. |
| Skip |L'ID de définition OVAL correspond à une plateforme non valide. </br> </br> L'ID de définition OVAL n'est pas référencé par le fichier d'entrée XCCDF/DataStream.</br> </br> L'ID de test OVAL n'est pas référencé par le fichier d'entrée XCCDF/DataStream. </br> </br> L’ID du profil XCCDF ne contient pas d’instructions @select avec la valeur 1. </br> </br> L'ID du profil XCCDF inclut un attribut abstrait avec la valeur true. </br> </br> L'ID du profil XCCDF ne contient pas de règle de qualification.|

## <a name="common-problems-and-solutions"></a>Problèmes courants et solutions

Le tableau suivant répertorie certains problèmes courants et solutions pour vous aider à résoudre les problèmes.

Tableau 1.6 Problèmes courants et solutions

| Problème | Solution possible |
| --- | --- |
| En cas d’état **Erreur** ou **Inconnu** d’une base de référence et si Internet Explorer ne peut pas afficher correctement le rapport. IE indique &quot;Le rapport est vide ou non valide&quot; | Sélectionnez la ligne de base, puis cliquez sur **Évaluer** pour réexécuter la ligne de base. Ensuite, surveillez la mise à jour des paramètres **État conforme**/**Dernière évaluation**. Une fois la date de dernière évaluation mise à jour à la date et heure actuelles (c'est-à-dire que l'évaluation est terminée), sélectionnez la ligne de base et réexaminez le rapport. Si IE ne peut toujours pas afficher le rapport, la ligne de base est peut-être trop grande. Régénérez le contenu à l’aide d’une taille de lot inférieure pour créer des bases de référence enfants plus petites. Si ce problème se produit sur les bases de référence parents, essayez de déployer les bases de référence enfants à la place. |
| J’ai créé des objets de stratégie de groupe (GPO) qui incluent les paramètres USGCB prescrits et je les ai liés aux unités d’organisation (UO) qui contiennent des ordinateurs exécutant Windows 7. Toutefois, les rapports de conformité indiquent que certains des paramètres ne sont pas configurés correctement. | Il est possible que les autorisations de la stratégie de groupe soient incorrectes ou n'aient pas été liées à l'unité d'organisation correcte. Toutefois, il est plus probable que les nouveaux paramètres ne soient pas encore effectifs. Par défaut, la stratégie de groupe sur les ordinateurs clients qui appartiennent à un domaine Active Directory recherche les mises à jour de la stratégie de groupe toutes les 90 minutes. Cela peut être l'une des raisons pour laquelle les paramètres semblent ne pas être appliqués, même si vous avez correctement configuré les stratégies. Autre facteur à retenir : pour que plusieurs paramètres d'ordinateur prennent effet, un redémarrage est nécessaire. Par exemple, le paramètre appelé **Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature nécessite le redémarrage de l’ordinateur avant que Windows puisse utiliser les algorithmes de chiffrement spécifiés. Vous pouvez ignorer l’intervalle d’actualisation de la stratégie de groupe en entrant la commande suivante à une invite de commandes avec des privilèges d’administrateur : gpupdate /force Une fois l’actualisation de la stratégie de groupe terminée, redémarrez l’ordinateur pour vous assurer que tous les paramètres sont effectifs. Pour plus d’informations, consultez l’article 298444 de la Base de connaissances, [Description de l’utilitaire de mise à jour de Stratégie de groupe](http://support.microsoft.com/kb/298444). |
| Je ne parviens pas à établir une connexion avec la base de données à l'aide de mes informations d'organisation. | Pour savoir comment configurer vos informations de connexion à la base de données, consultez l’article [Installer et configurer les Extensions SCAP](/sccm/compliance/plan-design/scap/install-configure-scap). 

## <a name="next-step"></a>Étape suivante
> [!div class="nextstepaction"]
> [Installer et configurer les extensions SCAP](/sccm/compliance/plan-design/scap/install-configure-scap)