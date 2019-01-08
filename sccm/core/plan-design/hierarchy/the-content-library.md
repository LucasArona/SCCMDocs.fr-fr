---
title: Bibliothèque de contenu
titleSuffix: Configuration Manager
description: Découvrez la bibliothèque de contenu utilisée par Configuration Manager pour réduire la taille globale du contenu distribué.
ms.date: 09/19/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 65c88e54-3574-48b0-a127-9cc914a89dca
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4587549ef2f43be3dcc5e18021f60c42770f5800
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53415515"
---
# <a name="the-content-library-in-configuration-manager"></a>Bibliothèque de contenu dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

La bibliothèque de contenu est un stockage SIS (Single Instance Store) de contenu dans Configuration Manager. Le site l’utilise pour réduire la taille globale du corps combiné du contenu que vous distribuez. La bibliothèque de contenu stocke tous les fichiers de contenu pour les déploiements logiciels, par exemple des déploiements de mises à jour logicielles, d’applications et de systèmes d’exploitation.  

- Le site crée et gère automatiquement une copie de la bibliothèque de contenu sur chaque serveur de site et sur chaque point de distribution.  

- Avant d’ajouter des fichiers de contenu vers le serveur de site ou de copier les fichiers sur les points de distribution, Configuration Manager vérifie si chaque fichier de contenu se trouve déjà dans la bibliothèque de contenu.  

- Si le fichier de contenu est disponible, Configuration Manager ne copie pas le fichier. Au lieu de cela, il associe le fichier de contenu existant à l’application ou au package.  

Sur les serveurs de point de distribution, configurez les options suivantes :

- un ou plusieurs lecteurs de disque sur lesquels vous voulez créer la bibliothèque de contenu ;  

- une priorité pour chaque lecteur que vous utilisez.  

Configuration Manager copie les fichiers de contenu sur le lecteur avec la priorité la plus élevée, jusqu’à ce que ce lecteur ne dispose plus que d’une quantité d’espace libre inférieure à la quantité minimale spécifiée.  

- Vous configurez les paramètres de lecteur lors de l'installation du point de distribution.  

- Une fois l’installation terminée, vous ne pouvez plus configurer les paramètres de lecteur dans les propriétés du point de distribution.  


Pour plus d’informations sur la configuration des paramètres de lecteur pour le point de distribution, consultez [Gérer le contenu et l’infrastructure de contenu](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).  


> [!IMPORTANT]
>  Pour déplacer la bibliothèque de contenu à un autre emplacement sur un point de distribution après l’installation, utilisez **l’outil Content Library Transfer** des outils de Configuration Manager. Pour plus d’informations, consultez [Outil Transfert de bibliothèque de contenu](/sccm/core/support/content-library-transfer).  



## <a name="about-the-content-library-on-the-central-administration-site"></a>À propos de la bibliothèque de contenu sur le site d’administration centrale  
Par défaut, Configuration Manager crée une bibliothèque de contenu sur le site d’administration centrale, lors de l’installation du site. La bibliothèque de contenu est placée sur le lecteur du serveur de site possédant l'espace disponible le plus important. Comme vous ne pouvez pas installer un point de distribution sur le site d’administration centrale, vous ne pouvez pas attribuer une priorité aux lecteurs à utiliser pour la bibliothèque de contenu. Comme la bibliothèque de contenu sur d'autres serveurs de site ou sur des points de distribution, lorsque le lecteur contenant la bibliothèque de contenu n'a plus d'espace disponible, la bibliothèque de contenu s'étend sur le lecteur disponible suivant.  

Configuration Manager utilise la bibliothèque de contenu sur le site d’administration centrale dans les scénarios suivants :  

- Vous créez du contenu sur le site d’administration centrale  

- Vous migrez le contenu depuis un autre site Configuration Manager et vous désignez le site d’administration centrale comme site gérant ce contenu.  

> [!NOTE]  
>  Quand vous créez du contenu sur un site principal, puis que vous le distribuez à un autre site principal ou à un site secondaire sous un autre site principal, le site d’administration centrale stocke temporairement ce contenu dans la boîte de réception du planificateur sur le site d’administration centrale, sans toutefois ajouter ce contenu à sa bibliothèque de contenu.  

Utilisez les options suivantes pour gérer la bibliothèque de contenu sur le site d'administration centrale :  

- Pour empêcher l’installation de la bibliothèque de contenu sur un lecteur spécifique, créez un fichier vide nommé **no_sms_on_drive.sms**. Copiez-le à la racine du lecteur avant la création de la bibliothèque de contenu.  

- Une fois la bibliothèque de contenu créée, utilisez **l’outil Transfert de bibliothèque de contenu** des outils Configuration Manager pour gérer l’emplacement de la bibliothèque de contenu. Pour plus d’informations, consultez [Outil Transfert de bibliothèque de contenu](/sccm/core/support/content-library-transfer).  

> [!Note]  
> Les points de distribution cloud n’utilisent pas le stockage SIS (Single Instance Storage). Le site chiffre les packages avant de les envoyer à Azure, et chaque package a une clé chiffrée unique. Même si deux fichiers étaient identiques, leurs versions chiffrées ne seraient pas les mêmes.  



## <a name="bkmk_remote"></a> Configurer une bibliothèque de contenu distante pour le serveur de site  
<!--1357525--> À compter de la version 1806, pour configurer la [haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability) ou pour libérer de l’espace disque sur vos serveurs d’administration centrale ou de site principal, déplacez la bibliothèque de contenu à un autre emplacement de stockage. Déplacez la bibliothèque de contenu sur un autre disque du serveur de site, sur un serveur distinct ou sur des disques à tolérance de panne dans un réseau de zone de stockage (SAN). Un SAN est recommandé, car il est à haute disponibilité et fournit un stockage élastique capable de croître ou de se réduire au fil du temps pour répondre à vos besoins en termes de contenu. Pour plus d’informations, consultez [Options de haute disponibilité](/sccm/protect/understand/high-availability-options).

Cette bibliothèque de contenu distante est un prérequis pour la [haute disponibilité du serveur de site](/sccm/core/servers/deploy/configure/site-server-high-availability). 

> [!Note]  
> Cette action déplace uniquement la bibliothèque de contenu sur le serveur de site. Elle n’affecte pas l’emplacement de la bibliothèque de contenu sur les points de distribution. 

> [!Tip]  
> Planifiez aussi la gestion du contenu des packages, qui est extérieure à la bibliothèque de contenu. Chaque objet de logiciel dans Configuration Manager a une source de package sur un partage réseau. Envisagez la centralisation de toutes les sources sur un seul partage, mais vérifiez que cet emplacement est redondant et à haute disponibilité. 
> 
> Si vous déplacez la bibliothèque de contenu vers le même volume de stockage que vos sources de package, vous ne pouvez pas marquer ce volume pour la déduplication des données. Contrairement à la bibliothèque de contenu, le volume de sources de package ne prend pas en charge la déduplication des données. Pour plus d’informations, consultez [Déduplication des données](/sccm/core/plan-design/configs/support-for-windows-features-and-networks#bkmmk_datadedup).<!--SCCMDOcs issue #831-->  


### <a name="prerequisites"></a>Prérequis  

- Le compte de l’ordinateur du serveur de site doit disposer d’autorisations en **lecture** et en **écriture** pour le chemin réseau où vous déplacez la bibliothèque de contenu. Aucun composant n’est installé sur le système à distance.  

- Le serveur de site ne peut pas avoir le rôle de point de distribution. Le point de distribution utilise également la bibliothèque de contenu, et ce rôle ne prend pas en charge les bibliothèques de contenu distantes. Après avoir déplacé la bibliothèque de contenu, vous ne pouvez plus ajouter le rôle de point de distribution au serveur de site.  

> [!Important]  
> Ne réutilisez pas un emplacement de réseau partagé entre plusieurs sites. Par exemple, n’utilisez pas le même chemin à la fois pour un site d’administration centrale et pour un site principal enfant. Cette configuration est susceptible d’endommager la bibliothèque de contenu, ce qui nécessiterait sa recréation.<!--SCCMDocs-pr issue 2764-->  


### <a name="process-to-manage-the-content-library"></a>Processus de gestion de la bibliothèque de contenu

1. Créez un dossier dans un partage réseau comme cible de la bibliothèque de contenu. Par exemple, `\\server\share\folder`.  

    > [!Warning]  
    > Ne réutilisez pas un dossier comprenant déjà du contenu. Par exemple, n’utilisez pas le dossier où se trouvent vos sources de package. Avant de copier la bibliothèque de contenu, Configuration Manager supprime tout le contenu existant de l’emplacement spécifié.  

2. Dans la console de Configuration Manager, accédez à l’espace de travail **Administration**. Développez **Configuration du site**, sélectionnez le nœud **Sites**, puis sélectionnez le site. Dans l’onglet **Résumé** en bas du volet d’informations, vous noterez l’apparition d’une nouvelle colonne pour la **Bibliothèque de contenu**.  

3. Sur le ruban, cliquez sur **Gérer la bibliothèque de contenu**.   

4. Dans la fenêtre Gérer la bibliothèque de contenu, le champ **Emplacement actuel** indique le lecteur et le chemin local. Entrez un chemin réseau valide pour le **Nouvel emplacement**. Ce chemin d’accès est l’emplacement vers lequel le site déplace la bibliothèque de contenu. Il doit inclure un nom de dossier qui existe déjà sur le partage, par exemple `\\server\share\folder`. Cliquez sur **OK**.  

5. Notez la valeur de **État** dans la colonne Bibliothèque de contenu sur le volet Résumé du volet des informations. Elle se met à jour pour afficher la progression du site en termes de déplacement de la bibliothèque de contenu.  

   - Quand **En cours** est indiqué, la valeur de **Progression du déplacement (%)** affiche le pourcentage d’achèvement.  

   - En cas d’état d’erreur, l’état affiche l’erreur. **Accès refusé** et **Disque plein** sont des erreurs courantes.  

   - Quand l’opération est terminée, l’état passe à **Terminé**.  
    
     Consultez **distmgr.log** pour plus d’informations. Pour plus d’informations, consultez [Journaux serveur du serveur de site et du système de site](/sccm/core/plan-design/hierarchy/log-files#BKMK_SiteSiteServerLog).  

Pour plus d’informations sur ce processus, consultez [Diagramme de flux – Gérer la bibliothèque de contenu](/sccm/core/plan-design/hierarchy/manage-content-library-flowchart).

Le site *copie* les fichiers de la bibliothèque de contenu à l’emplacement distant. Ce processus ne supprime pas les fichiers de la bibliothèque de contenu à l’emplacement d’origine sur le serveur de site. Pour libérer l’espace, un administrateur doit supprimer manuellement ces fichiers d’origine.

Si vous avez besoin de redéplacer la bibliothèque de contenu vers le serveur de site, répétez ce processus, mais entrez un lecteur et un chemin local pour **Nouvel emplacement**. Il doit inclure un nom de dossier qui existe déjà sur le lecteur, par exemple `D:\SCCMContentLib`. Quand le contenu d’origine existe encore, le processus déplace rapidement la configuration à l’emplacement local sur le serveur de site. 

> [!Tip]  
> Pour déplacer le contenu vers un autre disque du serveur de site, utilisez l’outil **Transfert de bibliothèque de contenu**. Pour plus d’informations, consultez [Outil Transfert de bibliothèque de contenu](/sccm/core/support/content-library-transfer).  



## <a name="inside-the-content-library"></a>À l’intérieur de la bibliothèque de contenu

> [!Warning]  
> La section suivante est fournie uniquement à titre d’information. Ne modifiez pas, n’ajoutez pas et ne supprimez pas de fichiers ou de dossiers dans la bibliothèque de contenu. Si vous le faites, vous risquez d’endommager des packages, des contenus ou toute la bibliothèque de contenu. Si vous pensez que des données sont manquantes, endommagées ou non valides, utilisez la fonctionnalité de validation dans la console Configuration Manager pour détecter ces problèmes. Redistribuez ensuite le contenu affecté pour corriger les problèmes. 

Par défaut, la bibliothèque de contenu est stockée à la racine d’un lecteur dans un dossier nommé **SCCMContentLib**. Ce dossier est partagé par défaut en tant que **SCCMContentLib$**. Le dossier et le partage ont des autorisations limitées, de façon à empêcher les dommages accidentels. Toutes les modifications doivent être effectuées à partir de la console Configuration Manager. Ce dossier contient les objets suivants :  

- La bibliothèque de packages (dossier **PkgLib**) : Informations sur les packages qui sont présents sur le point de distribution.  

- La bibliothèque de données (dossier **DataLib**) : Informations sur la structure d’origine des packages.  

- La bibliothèque de fichiers (dossier **FileLib**) : Fichiers d’origine dans le package. Ce dossier est généralement ce qui utilise la majeure partie du stockage.  

![Diagramme donnant une vue d’ensemble de la bibliothèque de contenu de Configuration Manager](media/content-library-overview.png)

> [!Tip]  
> Utilisez l’outil **Explorateur de bibliothèque de contenu** des outils Configuration Manager pour parcourir le contenu de la bibliothèque de contenu. Vous ne pouvez pas utiliser cet outil pour modifier un contenu. Il fournit un insight de ce qui est présent, et permet la validation et la redistribution. Pour plus d’informations, consultez [Explorateur de bibliothèque de contenu](/sccm/core/support/content-library-explorer).  


### <a name="package-library"></a>Bibliothèque de packages
Le dossier de la bibliothèque de packages, **PkgLib**, inclut un fichier pour chaque package distribué au point de distribution. Le nom de fichier est l’ID de package, par exemple `ABC00001.INI`. Dans ce fichier, sous la section `[Packages]`, se trouve une liste d’ID des contenus qui font partie du package, ainsi que d’autres informations, comme la version. Par exemple, **ABC00001** est un package hérité en version **1**. L’ID de contenu dans ce fichier est `ABC00001.1`.


### <a name="data-library"></a>Bibliothèque de données
Le dossier de bibliothèque de données, **DataLib**, comprend un fichier et un dossier pour chacun des contenus de chaque package. Par exemple, ce fichier et ce dossier sont respectivement nommés `ABC00001.1.INI` et `ABC00001.1`. Le fichier contient des informations pour la validation. Le dossier recrée la structure de dossiers à partir du package d’origine. 

Les fichiers de la bibliothèque de données sont remplacés par des fichiers INI avec le nom du fichier d’origine dans le package. Par exemple, `MyFile.exe.INI`. Ces fichiers incluent des informations sur le fichier d’origine, comme la taille, l’heure de modification et le hachage. Utilisez les quatre premiers caractères du hachage pour localiser le fichier d’origine dans la bibliothèque de fichiers. Par exemple, le hachage dans MyFile.exe.INI est **DEF98765**, et les quatre premiers caractères sont **DEF9**.


### <a name="file-library"></a>Bibliothèque de fichiers
Si la bibliothèque de contenu s’étend sur plusieurs lecteurs, les fichiers de package peuvent se trouver dans le dossier de la bibliothèque de fichiers, **FileLib**, sur un de ces lecteurs.

Vous trouvez un fichier spécifique en utilisant les quatre premiers caractères du hachage figurant dans la bibliothèque de données. Le dossier de la bibliothèque de fichiers contient de nombreux dossiers, chacun avec un nom de quatre caractères. Recherchez le dossier qui correspond aux quatre premiers caractères du hachage. Une fois que vous trouvez ce dossier, vous voyez qu’il inclut un ou plusieurs ensembles de trois fichiers. Ces fichiers partagent le même nom, mais un des fichiers a l’extension INI, un autre l’extension SIG et un dernier fichier n’a pas d’extension de fichier. Le fichier d’origine est celui qui est sans extension et dont le nom est le hachage provenant de la bibliothèque de données.

Par exemple, le dossier **DEF9** inclut `DEF98765.INI`, `DEF98765.SIG` et `DEF98765`. `DEF98765` est le fichier `MyFile.exe` d’origine. Le fichier INI inclut une liste d’utilisateurs ou d’ID de contenu qui partagent le même fichier. Le site ne supprime pas de fichier, sauf si tous ces contenus sont également supprimés.


### <a name="drive-spanning"></a>Répartition sur plusieurs lecteurs

La bibliothèque de contenu peut être répartie sur plusieurs lecteurs. Vous choisissez ces lecteurs lors de la création du point de distribution. Par défaut, Configuration Manager choisit automatiquement les lecteurs lors de la répartition de la bibliothèque de contenu.

Quand vous choisissez les lecteurs, sélectionnez un lecteur principal et un lecteur secondaire. Le site stocke toutes les métadonnées sur le lecteur principal. Il répartit la bibliothèque de fichiers seulement sur le lecteur secondaire. Le nom de partage du dossier pour les lecteurs secondaire inclut la lettre de lecteur. Par exemple, si D: et E: sont des lecteurs secondaire pour la bibliothèque de contenu, les noms de partage sont **SCCMContentLibD$** et **SCCMContentLibE$**.

Si vous avez choisi l’option **Automatique**, Configuration Manager sélectionne le lecteur avec le plus d’espace libre disponible comme lecteur principal. Il stocke toutes les métadonnées sur ce lecteur. Le site répartit la bibliothèque de fichiers seulement sur des lecteurs secondaires. 

Vous spécifiez une quantité d’espace de réserve lors de la configuration. Configuration Manager tente d’utiliser un disque secondaire une fois que le disque avec le plus d’espace disponible ne dispose plus que de cette quantité d’espace de réserve. Chaque fois qu’un nouveau lecteur est sélectionné pour être utilisé, le lecteur avec le plus d’espace libre disponible est sélectionné.

Vous ne pouvez pas spécifier qu’un point de distribution doit utiliser tous les lecteurs à l’exception d’un ensemble spécifique. Empêchez ce comportement en créant un fichier vide à la racine du lecteur, nommé `NO_SMS_ON_DRIVE.SMS`. Placez ce fichier avant que Configuration Manager sélectionne le lecteur à utiliser. Si Configuration Manager détecte ce fichier à la racine du lecteur, il ne l’utilise pas pour la bibliothèque de contenu. 



## <a name="troubleshooting"></a>Résolution des problèmes

Les conseils suivants peuvent vous aider à résoudre les problèmes rencontrés avec la bibliothèque de contenu :  

- Examinez les journaux sur le serveur de site (**distmgr.log** et **PkgXferMgr.log**) et sur le point de distribution (**smsdpprov.log**) pour trouver d’éventuels pointeurs vers les échecs.  

- Utilisez l’outil [Explorateur de bibliothèque de contenu](/sccm/core/support/content-library-explorer).  

- Recherchez les verrouillages de fichier par d’autres processus, comme les logiciels antivirus. Excluez la bibliothèque de contenu des analyses antivirus automatiques sur tous les lecteurs, ainsi que le répertoire intermédiaire temporaire, **SMS_DP$**, sur chaque lecteur.  

- Pour voir s’il existe des incompatibilités de hachage, validez le package à partir de la console Configuration Manager.  

- En dernier recours, redistribuez le contenu. Cette action doit normalement résoudre la plupart des problèmes.  

