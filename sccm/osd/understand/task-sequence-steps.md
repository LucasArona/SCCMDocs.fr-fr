---
title: Étapes de séquence de tâches
titleSuffix: Configuration Manager
description: Découvrez les différentes étapes que vous pouvez ajouter à une séquence de tâches Configuration Manager.
ms.date: 03/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 7c888a6f-8e37-4be5-8edb-832b218f266d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a678cbbd8500070e2d4056d6e424818e7000ef83
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32352649"
---
# <a name="task-sequence-steps-in-system-center-configuration-manager"></a>Étapes de séquence de tâches dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Vous trouverez ci-dessous les différentes étapes de séquence de tâches qui peuvent être ajoutées à une séquence de tâches Configuration Manager. Pour plus d’informations sur la modification d’une séquence de tâches, consultez [Modifier une séquence de tâches](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

Les paramètres suivants sont communs à toutes les étapes de la séquence de tâches :

Sous l’onglet **Propriétés**:
 - **Nom** : l’Éditeur de séquence de tâches vous demande de spécifier un nom court pour décrire cette étape. Quand vous ajoutez une nouvelle étape, l’Éditeur de séquence de tâches définit le nom en utilisant le type par défaut. La longueur du **Nom** ne peut pas dépasser 50 caractères.
 - **Description** : si vous le souhaitez, spécifiez des informations plus détaillées sur cette étape. La longueur de la **Description** ne peut pas dépasser 256 caractères.
Le reste de cet article décrit les autres paramètres présents sous l’onglet **Propriétés** de chaque étape de la séquence de tâches.

Sous l’onglet **Options** :  
-   **Désactiver cette étape** : la séquence de tâches ignore cette étape quand elle s’exécute sur un ordinateur. L’icône de cette étape est grisée dans l’Éditeur de séquence de tâches. 
-   **Continuer en cas d’erreur** : la séquence de tâches continue si une erreur se produit lors de l’exécution de l’étape.  
-   **Ajouter une condition** : la séquence de tâches évalue ces instructions conditionnelles pour déterminer si elle exécute l’étape.   
Les sections ci-dessous pour des étapes de séquence de tâches spécifiques décrivent d’autres paramètres possibles sous l’onglet **Options**.



##  <a name="BKMK_ApplyDataImage"></a> Appliquer l’image de données   
 Utilisez cette étape pour copier l’image de données sur la partition de destination spécifiée.  

 Cette étape est exécutée uniquement sous Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches, consultez [Variables d’action de séquence de tâches](task-sequence-action-variables.md).  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis **Appliquer l’image de données** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Package d’images**  
 Cliquez sur **Parcourir** pour spécifier le **Package d’images** utilisé par cette séquence de tâches. Sélectionnez le package à installer dans la boîte de dialogue **Sélectionner un package** . Les informations des propriétés associées à chaque package d'images s'affichent en bas de la boîte de dialogue **Sélectionner un package** . Utilisez la liste déroulante pour choisir l' **image** que vous souhaitez installer à partir du **package d'images**sélectionné.  

> [!NOTE]  
>  Cette action de séquence de tâches traite l’image comme un fichier de données. Cette action n’effectue aucune configuration pour démarrer l’image en tant que système d’exploitation.  

 **Destination**  
 Configurez une des options suivantes :

-   **Prochaine partition disponible** : utilisez la partition séquentielle suivante qui n’a pas déjà été ciblée par une action **Appliquer le système d’exploitation** ou **Appliquer l’image de données** dans cette séquence de tâches.  

-   **Disque et partition spécifiques** : sélectionnez le numéro de **disque** (à partir de 0) et le numéro de **partition** (à partir de 1).  

-   **Lettre de lecteur logique spécifique** : spécifiez la **lettre de lecteur** affectée à la partition par Windows PE. Cette lettre de lecteur peut être différente de la lettre de lecteur affectée par le système d’exploitation nouvellement déployé.  

-   **Lettre de lecteur logique stockée dans une variable** : spécifiez la variable de séquence de tâches contenant la lettre de lecteur affectée à la partition par Windows PE. Cette variable est généralement définie dans la section Avancé de la boîte de dialogue **Propriétés de la partition** pour l’action de séquence de tâches **Formater et partitionner le disque**.  

**Supprimer l’intégralité du contenu de la partition avant d’appliquer l’image**  
 Spécifie que la séquence de tâches supprime tous les fichiers sur la partition cible avant d’installer l’image. Si vous ne supprimez pas le contenu de la partition, cette étape peut être utilisée pour appliquer le contenu supplémentaire à une partition précédemment ciblée.  



##  <a name="BKMK_ApplyDriverPackage"></a> Appliquer le package de pilotes  
 Utilisez cette étape pour télécharger tous les pilotes du package de pilotes et les installer sur le système d’exploitation Windows.

 L'étape de séquence de tâches **Appliquer le package de pilotes** rend disponibles tous les pilotes d'appareils d'un package de pilotes pour l'utilisation avec Windows. Ajoutez cette étape entre les étapes **Appliquer le système d’exploitation** et **Configurer Windows et ConfigMgr** pour que les pilotes du package soient disponibles sous Windows. Généralement, l'étape **Appliquer le package de pilotes** est placée après l'étape de séquence de tâches **Appliquer automatiquement les pilotes** . L'étape de séquence de tâches **Appliquer le package de pilotes** est également utile avec des scénarios de déploiement de médias autonomes.  

 Assurez-vous que les pilotes de périphérique identiques sont placés dans un package de pilotes et distribuez-les aux points de distribution appropriés. Une fois qu’ils sont distribués, les ordinateurs clients Configuration Manager peuvent les installer. Par exemple, placez tous les pilotes d’un même fabricant dans un package de pilotes. Distribuez ensuite le package aux points de distribution auquel les ordinateurs associés peuvent accéder.

 L’étape **Appliquer le package de pilotes** est pratique pour un média autonome. Cette étape est également utile si vous voulez installer un ensemble spécifique de pilotes. Ces types de pilotes incluent les appareils qui ne sont pas détectés dans une analyse Plug-and-play, comme les imprimantes réseau.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer le package de pilotes](task-sequence-action-variables.md#BKMK_ApplyDriverPackage).  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Pilotes**, puis sélectionnez **Appliquer le package de pilotes** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Package de pilotes**  
 Spécifiez le package de pilotes qui contient les pilotes d'appareils nécessaires en cliquant sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package** . Spécifiez un package existant à rendre disponible. Les propriétés du package associé s'affichent dans la partie inférieure de la boîte de dialogue.  

 **Sélectionner le pilote de stockage de masse au sein du package devant être installé avant la configuration sur les systèmes d’exploitation antérieurs à Windows Vista**  
 Spécifiez les pilotes de stockage de masse nécessaires pour installer un système d’exploitation classique.  

 **Pilote**  
 Sélectionnez le fichier de pilote de stockage de masse à installer avant l’installation d’un système d’exploitation classique. La liste déroulante est complétée à partir du package spécifié.  

 **Modèle**  
 Spécifiez l'appareil critique au démarrage nécessaire aux déploiements des systèmes d'exploitation antérieurs à Windows Vista.  

 **Effectuer une installation autonome des pilotes non signés sur les versions de Windows le permettant**  
 Cette option permet à Windows Installer des pilotes sans signature numérique.  



##  <a name="BKMK_ApplyNetworkSettings"></a> Appliquer les paramètres réseau   
 Utilisez cette étape pour spécifier les informations de configuration du réseau ou du groupe de travail pour l’ordinateur de destination. La séquence de tâches stocke ces valeurs dans le fichier de réponses approprié. Le programme d’installation de Windows utilise ce fichier de réponses pendant l’action **Configurer Windows et ConfigMgr**.  

 Cette étape de séquence de tâches s'exécute dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer les paramètres réseau](task-sequence-action-variables.md#BKMK_ApplyNetworkSettings).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Paramètres**, puis sélectionnez **Appliquer les paramètres réseau** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Joindre un groupe de travail**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du groupe de travail spécifié. Entrez le nom du groupe de travail sur la ligne **Groupe de travail** . Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres réseau** .  

 **Joindre un domaine**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du domaine spécifié. Spécifiez ou accédez au domaine, tel que *fabricam.com*. Spécifiez ou accédez à un chemin LDAP (Lightweight Directory Access Protocol) pour une unité d’organisation. Par exemple : *LDAP//OU=ordinateurs, DC=Fabricam.com, C=com*  

 **Compte**  
 Cliquez sur **Définir** pour spécifier un compte bénéficiant des autorisations nécessaires pour associer l'ordinateur au domaine. Dans la boîte de dialogue **Compte d’utilisateur Windows**, vous pouvez entrer le nom d’utilisateur au format suivant : **Domaine\Utilisateur**.  

 **Paramètres de carte**  
 Spécifiez les configurations réseau pour chaque carte réseau dans l'ordinateur. Cliquez sur **Nouveau** pour ouvrir la boîte de dialogue **Paramètres réseau** , puis spécifiez les paramètres réseau. Si vous utilisez également l’étape **Capturer les paramètres réseau**, la séquence de tâches applique les paramètres précédemment capturés à la carte réseau. La séquence de tâches n’applique pas les paramètres que vous spécifiez dans cette étape. Si la séquence de tâches n’a pas déjà capturé de paramètres réseau, elle applique les paramètres spécifiés dans l’étape **Appliquer les paramètres réseau**. La séquence de tâches applique ces paramètres aux cartes réseau dans l’ordre d’énumération des appareils Windows.  



##  <a name="BKMK_ApplyOperatingSystemImage"></a> Appliquer l’image du système d’exploitation  

> [!TIP]  
> À compter de Windows 10 version 1709, le média inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour l’utilisation d’un package de mise à niveau du système d’exploitation ou d’une image de système d’exploitation, veillez à sélectionner une [édition prise en charge](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Utilisez cette étape pour installer un système d’exploitation sur l’ordinateur de destination. Cette étape effectue des actions selon qu’elle utilise une image de système d’exploitation ou un package de mise à niveau du système d’exploitation.  

 L’étape **Appliquer l’image du système d’exploitation** effectue les actions suivantes si une image de système d’exploitation est utilisée :  

1.  Supprime tout le contenu sur le volume cible, sauf les fichiers spécifiés par la variable &#95;SMSTSUserStatePath.

2.  Extrait le contenu du fichier .wim spécifié sur la partition de destination spécifiée.  

3.  Prépare le fichier de réponses :  

    1.  Crée un fichier de réponses d’installation de Windows par défaut (sysprep.inf ou unattend.xml) pour le système d’exploitation à déployer.  

    2.  Fusionne les valeurs du fichier de réponses fourni par l’utilisateur.  

4.  Copie les chargeurs de démarrage Windows dans la partition active.  

5.  Configure boot.ini ou BCD (Boot Configuration Database) pour qu’ils référencent le système d’exploitation nouvellement installé.  

 L’étape **Appliquer l’image du système d’exploitation** effectue les actions suivantes si un package de mise à niveau du système d’exploitation est utilisé :  

1.  Supprime tout le contenu sur le volume cible, sauf les fichiers spécifiés par la variable &#95;SMSTSUserStatePath.  

2.  Prépare le fichier de réponses :  

    1.  Crée un fichier de réponses entièrement nouveau, contenant les valeurs standard produites par Configuration Manager.  

    2.  Fusionne les valeurs du fichier de réponses fourni par l’utilisateur.  

> [!NOTE]  
>  L’étape **Configurer Windows et ConfigMgr** démarre l’installation de Windows. 

 À l’issue de l’exécution de l’action **Appliquer le système d’exploitation**, la variable OSDTargetSystemDrive est définie sur la lettre de lecteur de la partition contenant les fichiers du système d’exploitation.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer l’image du système d’exploitation](task-sequence-action-variables.md#BKMK_ApplyOperatingSystem).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis sélectionnez **Appliquer l’image du système d’exploitation** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Appliquer le système d’exploitation à partir d’une image capturée**  
 Installer une image du système d'exploitation qui a été précédemment capturée. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionner un package** , puis sélectionnez le package d'image existant à installer. Si plusieurs images sont associées au **Package d’images** spécifié, utilisez la liste déroulante pour spécifier l’image associée à utiliser pour ce déploiement. Vous pouvez afficher des informations de base sur chaque image existante en cliquant sur l'image en question.  

 **Appliquer l’image du système d’exploitation à partir d’une source d’installation d’origine**  
 Installe un système d'exploitation à l'aide d'une source d'installation d'origine. Cliquez sur **Parcourir** pour ouvrir la boîte de dialogue **Sélectionnez un package d’installation de système d’exploitation**. Sélectionnez ensuite le package de mise à niveau du système d’exploitation existant à utiliser. Vous pouvez afficher des informations de base sur chaque source d'image existante en cliquant sur l'image source en question. Les propriétés de la source d'image associée s'affichent dans le volet des résultats dans la partie inférieure de la boîte de dialogue. Si plusieurs éditions sont associées au package spécifié, utilisez la liste déroulante pour spécifier l' **Édition** associée qui est utilisée.  

 **Utiliser un fichier de réponse Sysprep ou autonome pour une installation personnalisée**  
 Utilisez cette option pour fournir un fichier de réponses d'installation Windows (**unattend.xml**, **unattend.txt**ou **sysprep.inf**) selon la version du système d'exploitation et la méthode d'installation. Le fichier que vous spécifiez peut inclure toutes les options de configuration standard prises en charge par les fichiers de réponse. Par exemple, vous pouvez l'utiliser pour spécifier la page d'accueil par défaut d'Internet Explorer. Spécifiez le package qui contient le fichier de réponses et le chemin associé au fichier dans le package.  

> [!NOTE]  
>  Le fichier de réponses d’installation de Windows que vous fournissez peut contenir des variables de séquence de tâches incorporées au format %*nom_variable*%, où *nom_variable* est le nom de la variable. L’étape **Configurer Windows et ConfigMgr** remplace la chaîne %*nom_variable*% par les valeurs réelles de la variable. Vous ne pouvez pas utiliser ces variables de séquence de tâches incorporées dans les champs exclusivement numériques d’un fichier de réponses unattend.xml.  

 Si vous ne fournissez pas de fichier de réponses d’installation de Windows, cette action de séquence de tâches génère automatiquement un fichier de réponses.  

 **Destination**  
 Configurez une des options suivantes :  

-   **Prochaine partition disponible** : utilisez la partition séquentielle suivante qui n’a pas déjà été ciblée par une action **Appliquer le système d’exploitation** ou **Appliquer l’image de données** dans cette séquence de tâches. 

-   **Disque et partition spécifiques** : sélectionnez le numéro de **disque** (à partir de 0) et le numéro de **partition** (à partir de 1).  

-   **Lettre de lecteur logique spécifique** : spécifiez la **lettre de lecteur** affectée à la partition par Windows PE. Cette lettre de lecteur peut être différente de la lettre de lecteur affectée par le système d’exploitation nouvellement déployé.  

-   **Lettre de lecteur logique stockée dans une variable** : spécifiez la variable de séquence de tâches contenant la lettre de lecteur affectée à la partition par Windows PE. Cette variable est généralement définie dans la section Avancé de la boîte de dialogue **Propriétés de la partition** pour l’action de séquence de tâches **Formater et partitionner le disque**.  

### <a name="options"></a>Options  
 Outre les options par défaut, configurez les paramètres supplémentaires suivants sous l’onglet **Options** de cette étape de séquence de tâches :  

-   **Accéder au contenu directement depuis le point de distribution**  
     Configurez la séquence de tâches pour accéder à l’image du système d’exploitation directement depuis le point de distribution. Par exemple, utilisez cette option quand vous déployez des systèmes d’exploitation sur des appareils intégrés ayant une capacité de stockage limitée. Quand cette option est sélectionnée, configurez aussi les paramètres de partage du package sous l’onglet **Accès aux données** des propriétés du package.  

    > [!NOTE]  
    >  Ce paramètre remplace l’option de déploiement que vous configurez dans la page **Points de distribution** de **l’Assistant Déploiement logiciel**. Ce remplacement est effectué seulement pour l’image du système d’exploitation spécifié par cette étape, et non pas pour le tout contenu de la séquence de tâches.  



##  <a name="BKMK_ApplyWindowsSettings"></a> Appliquer les paramètres Windows  
 Utilisez cette étape pour configurer les paramètres Windows de l’ordinateur de destination. La séquence de tâches stocke ces valeurs dans le fichier de réponses approprié. Le programme d’installation de Windows utilise ce fichier de réponses pendant l’action **Configurer Windows et ConfigMgr**.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer les paramètres Windows](task-sequence-action-variables.md#BKMK_ApplyWindowsSettings).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Paramètres**, puis sélectionnez **Appliquer les paramètres Windows** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Nom d’utilisateur**  
 Spécifiez le nom d'utilisateur inscrit qui est associé à l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'action de séquence de tâches **Capturer les paramètres Windows** .  

 **Nom de l’organisation**  
 Spécifiez le nom de l'organisation inscrite qui est associé à l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'action de séquence de tâches **Capturer les paramètres Windows** .  

 **Clé du produit**  
 Spécifiez la clé du produit qui est utilisée pour l'installation de Windows sur l'ordinateur de destination.  

 **Licence serveur**  
 Spécifiez le mode de licence serveur. Vous pouvez sélectionner le mode **Par serveur** ou **Par utilisateur** . Si vous sélectionnez **Par serveur**, spécifiez également le nombre maximal de connexions autorisées selon les termes de votre contrat de licence. Sélectionnez **Ne pas spécifier** si l'ordinateur de destination n'est pas un serveur ou si vous ne souhaitez pas spécifier le mode de licence.  

 **Nombre maximal de connexions**  
 Spécifiez le nombre maximal de connexions disponibles pour cet ordinateur comme spécifié dans votre accord de licence.  

 **Générer de façon aléatoire le mot de passe de l’administrateur local et désactiver le compte sur toutes les plates-formes prises en charge (recommandé)**  
 Sélectionnez cette option pour que le mot de passe de l’administrateur local soit une chaîne générée de façon aléatoire. Cette option désactive également le compte d’administrateur local sur les plateformes qui prennent en charge cette fonctionnalité.  

 **Activer le compte et spécifier le mot de passe de l’administrateur local**  
 Sélectionnez cette option pour activer le compte d’administrateur local avec le mot de passe spécifié. Entrez le mot de passe dans la ligne **Mot de passe** et confirmez-le dans la ligne **Confirmer le mot de passe** .  

 **Fuseau horaire**  
 Spécifiez le fuseau horaire à configurer sur l'ordinateur de destination. Cette valeur peut être remplacée par la valeur capturée par l'étape de séquence de tâches **Capturer les paramètres Windows** .  



##  <a name="BKMK_AutoApplyDrivers"></a> Appliquer automatiquement les pilotes  
 Utilisez cette étape pour trouver et installer des pilotes dans le cadre du déploiement du système d’exploitation.  

 L'étape de séquence de tâches **Appliquer automatiquement les pilotes** effectue les actions suivantes :  

1.  Analyse le matériel et trouve les ID Plug-and-Play de tous les périphériques présents sur le système.  

2.  Envoie la liste des périphériques et leurs ID Plug-and-Play au point de gestion. Celui-ci retourne depuis le catalogue de pilotes une liste de pilotes compatibles pour chaque périphérique matériel. La liste inclut tous les pilotes quel que soit le package de pilotes où ils se trouvent, les pilotes étiquetés avec la catégorie de pilotes spécifiée et les pilotes non désactivés.  

3.  Pour chaque périphérique matériel, la séquence de tâches choisit le meilleur pilote. Ce pilote est approprié pour le système d’exploitation déployé et se trouve sur un point de distribution accessible.  

4.  La séquence de tâches télécharge les pilotes sélectionnés à partir d’un point de distribution et prépare les pilotes sur le système d’exploitation cible.  

    1.  Pour les installations à base d’image, la séquence de tâches place les pilotes dans le magasin de pilotes du système d’exploitation.  

    2.  Pour les installations basées sur le programme d’installation, la séquence de tâches configure l’installation de Windows avec l’emplacement des pilotes.  

5.  Lors de l’étape **Configurer Windows et ConfigMgr** de la séquence de tâches, l’installation de Windows recherche les pilotes préparés par cette action.  

> [!IMPORTANT]
>  Un média autonome ne peut pas utiliser l’étape **Appliquer automatiquement les pilotes**. Dans ce scénario, l’installation de Windows n’a pas de connexion au site Configuration Manager.

Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Appliquer automatiquement les pilotes](task-sequence-action-variables.md#BKMK_AutoApplyDrivers).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Pilotes**, puis sélectionnez **Appliquer automatiquement les pilotes** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Installer uniquement les pilotes compatibles les plus appropriés**  
 Indique que l'étape de séquence de tâches installe uniquement le pilote le plus approprié pour chaque périphérique matériel détecté.  

 **Installer tous les pilotes compatibles**  
 La séquence de tâches installe tous les pilotes compatibles pour chaque périphérique matériel détecté. L’installation de Windows choisit ensuite le meilleur pilote. Cette option utilise davantage d’espace disque et de bande passante réseau. La séquence de tâches télécharge plus de pilotes, mais Windows peut sélectionner un meilleur pilote.  

 **Considérer les pilotes de toutes les catégories**  
 La séquence de tâches recherche les pilotes de périphériques appropriés dans toutes les catégories de pilotes disponibles.  

 **Limiter la correspondance des pilotes aux pilotes des catégories sélectionnées uniquement**  
 La séquence de tâches recherche les pilotes de périphériques appropriés dans les catégories de pilotes spécifiées.  

 **Effectuer une installation autonome des pilotes non signés sur les versions de Windows le permettant**  
 Cette option permet à Windows Installer des pilotes sans signature numérique.   

  > [!IMPORTANT]  
  >  Cette option ne s’applique pas aux systèmes d’exploitation où vous ne pouvez pas configurer la stratégie de signature des pilotes.  



##  <a name="BKMK_CaptureNetworkSettings"></a> Capturer les paramètres réseau  
 Utilisez cette étape pour capturer les paramètres réseau Microsoft de l’ordinateur exécutant la séquence de tâches. La séquence de tâches enregistre ces paramètres dans des variables de séquence de tâches. Ces paramètres remplacent les paramètres par défaut que vous configurez pour l’étape **Appliquer les paramètres réseau**.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer les paramètres réseau](task-sequence-action-variables.md#BKMK_CaptureNetworkSettings).  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Paramètres**, puis sélectionnez **Capturer les paramètres réseau** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Migrer l’appartenance au groupe de travail ou au domaine**  
 Capture les informations d'appartenance du domaine et du groupe de travail de l'ordinateur de destination.  

 **Migrer la configuration de la carte réseau**  
 Capture la configuration de la carte réseau de l'ordinateur de destination. Les informations capturées sont constituées des paramètres réseau globaux, du nombre de cartes et des paramètres réseau associés à chaque carte. Les paramètres sont constitués de paramètres associés à DNS, WINS, IP et aux filtres de port.  



##  <a name="BKMK_CaptureOperatingSystemImage"></a> Capturer l’image du système d’exploitation  
 Cette étape capture une ou plusieurs images à partir d’un ordinateur de référence. La séquence de tâches crée un fichier Image Windows (.wim) sur le partage réseau spécifié. Utilisez ensuite **l’Assistant Ajout d’un package d’image de système d’exploitation** pour importer cette image dans Configuration Manager pour les déploiements de systèmes d’exploitation à base d’image.  

 Configuration Manager capture chaque volume (lecteur) sur l’ordinateur de référence dans une image distincte au sein du fichier .wim. Si l’ordinateur de référence a plusieurs volumes, le fichier .wim obtenu contient une image distincte pour chaque volume. Seuls les volumes formatés au format NTFS ou FAT32 sont capturés. Les volumes d'un autre format et les volumes USB sont ignorés.  

 Le système d’exploitation installé sur l’ordinateur de référence doit être une version de Windows prise en charge par Configuration Manager. Utilisez l’outil Sysprep pour préparer le système d’exploitation de l’ordinateur de référence. Le volume du système d'exploitation installé et le volume de démarrage doivent correspondre.  

 Spécifiez un compte disposant d’autorisations d’écriture sur le partage réseau sélectionné.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer l’image du système d’exploitation](task-sequence-action-variables.md#BKMK_CaptureOperatingSystemImage).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis sélectionnez **Capturer l’image du système d’exploitation** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Cible**  
 Nom de chemin du système de fichiers menant à l’emplacement qu’utilise Configuration Manager pour stocker l’image de système d’exploitation capturée.  

 **Description**  
 Description facultative définie par l'utilisateur de l'image du système d'exploitation capturée qui est stockée dans le fichier WIM.  

 **Version**  
 Numéro de version facultatif défini par l'utilisateur à attribuer à l'image du système d'exploitation capturée. Cette valeur peut représenter n'importe quelle combinaison de lettres et de chiffres et est stockée dans le fichier WIM.  

 **Créé par**  
 (facultatif) Nom de l'utilisateur qui a créé l'image du système d'exploitation et qui est stocké dans le fichier WIM.  

 **Compte Capturer l’image du système d’exploitation**  
 Vous devez entrer le compte Windows qui dispose des droits d'accès au partage réseau que vous avez spécifié. Cliquez sur **Définir** pour indiquer le nom de ce compte Windows.  



##  <a name="BKMK_CaptureUserState"></a> Capturer l’état utilisateur  
 Utilisez cette étape pour faire usage de l’outil de migration utilisateur (USMT) pour capturer l’état et les paramètres utilisateur de l’ordinateur exécutant la séquence de tâches. Cette étape de séquence de tâches est utilisée avec l'étape de séquence de tâches **Restaurer l'état utilisateur** . Dans USMT 3.0.1 et ultérieur, cette option chiffre toujours le magasin d’état USMT au moyen d’une clé de chiffrement générée et gérée par Configuration Manager.  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Si vous voulez enregistrer et restaurer les paramètres d’état utilisateur à partir d’un point de migration d’état, utilisez l’étape **Capturer l’état utilisateur** avec les étapes **Demander le magasin d’état** et **Libérer le magasin d’état**.  

 L'étape de séquence de tâches **Capturer l'état utilisateur** permet de contrôler un sous-ensemble des options USMT les plus couramment utilisées. D'autres options de ligne de commande peuvent être spécifiées au moyen de la variable de séquence de tâches OSDMigrateAdditionalCaptureOptions.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer l’état utilisateur](task-sequence-action-variables.md#BKMK_CaptureUserState).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **État utilisateur**, puis sélectionnez **Capturer l’état utilisateur** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Package de l’outil de migration de l’état utilisateur**  
 Spécifiez le package qui contient l’outil USMT. La séquence de tâches utilise cette version de l’outil USMT pour capturer l’état et les paramètres utilisateur. Ce package ne requiert pas de programme. Spécifiez un package qui contient la version 32 bits ou 64 bits de l’outil USMT. L’architecture de l’outil USMT varie selon l’architecture du système d’exploitation à partir duquel la séquence de tâches capture l’état.  

 **Capturer tous les profils utilisateur présentant les options standard**  
 Migrez toutes les informations des profils utilisateur. Il s'agit de l'option par défaut.  

 Si vous sélectionnez cette option, mais que vous ne sélectionnez pas **Restaurer les profils utilisateur de l’ordinateur local** dans l’étape **Restaurer l’état utilisateur**, la séquence de tâches échoue. Configuration Manager ne peut pas migrer les nouveaux comptes sans leur attribuer des mots de passe. 

 Quand vous utilisez l’option **Installer un package d’image existant** de **l’Assistant Nouvelle séquence de tâches**, la séquence de tâches qui en résulte est par défaut **Capturer tous les profils utilisateur présentant les options standard**. Cette séquence de tâches par défaut ne sélectionne pas l’option permettant de **Restaurer les profils utilisateur de l’ordinateur local**, c’est-à-dire des comptes d’utilisateur n’appartenant pas au domaine.  

 Sélectionnez **Restaurer les profils utilisateur de l'ordinateur local** et spécifiez un mot de passe pour le compte à migrer. Dans une séquence de tâches qui a été manuellement créée, ce paramètre est disponible sous l'étape Restaurer l'état utilisateur. Dans une séquence de tâches créée à l'aide de l'Assistant **Nouvelle séquence de tâches** , ce paramètre est disponible sur la page de l'assistant d'étape **Restaurer les fichiers et paramètres utilisateur** .  

 Si vous ne disposez d’aucun compte d’utilisateur local, ce paramètre ne s’applique pas.  

 **Personnaliser la façon dont les profils utilisateur sont capturés**  
 Sélectionnez cette option pour indiquer une migration de fichiers de profils personnalisée. Cliquez sur **Fichiers** pour sélectionner les fichiers de configuration pour l'outil de migration de l'état utilisateur à utiliser avec cette étape. Spécifiez un fichier .xml personnalisé contenant les règles qui définissent les fichiers d’état utilisateur à migrer.  

 **Cliquez ici pour sélectionner les fichiers de configuration :**  
 Sélectionnez cette option pour sélectionner les fichiers de configuration dans le package USMT que vous souhaitez utiliser pour capturer les profils utilisateur. Cliquez sur le bouton **Fichiers** pour lancer la boîte de dialogue **Fichiers de configuration** . Pour indiquer un fichier de configuration, entrez son nom sur la ligne **Nom de fichier** , puis cliquez sur le bouton **Ajouter** .  

 **Activer la journalisation documentée**  
 Activez cette option pour générer des informations de fichiers journaux plus détaillées. Lors de la capture de l’état, la séquence de tâches par défaut génère Scanstate.log dans le dossier de journalisation de la séquence de tâches \windows\system32\ccm\logs.   

 **Ignorer les fichiers utilisant le système de fichiers chiffrés (EFS)**  
 Activez cette option pour ignorer la capture des fichiers chiffrés avec EFS (Encrypted File System). Ces fichiers incluent les fichiers de profil utilisateur. Selon le système d'exploitation et la version d'USMT, les fichiers chiffrés peuvent ne pas être accessibles après la restauration. Pour plus d'informations, consultez la documentation d'USMT.  

 **Copier en utilisant l’accès au système de fichiers**  
 Activez cette option pour spécifier les paramètres suivants :  

-   **Continuer si certains fichiers ne peuvent pas être capturés**: activez ce paramètre pour continuer le processus de migration même si certains fichiers ne peuvent pas être capturés. Si vous désactivez cette option et qu’un fichier ne peut pas être capturé, cette étape échoue. Cette option est activée par défaut.  

-   **Capturer localement en utilisant les liens au lieu de copier les fichiers**: activez ce paramètre pour utiliser des liens physiques NTFS pour capturer les fichiers.  

     Pour plus d'informations sur la migration de données à l'aide de liens directs, consultez [Magasin de migration de lien direct](http://go.microsoft.com/fwlink/p/?LinkId=240222)  

-   **Capturer en mode hors-ligne (Windows PE uniquement)**: activez ce paramètre pour capturer l’état utilisateur dans Windows PE au lieu du système d’exploitation complet.  
    
**Capturer en utilisant Volume Copy Shadow Service (VSS)**  
 Cette option vous permet de capturer des fichiers même s’ils sont verrouillés pour modification par une autre application.  



##  <a name="BKMK_CaptureWindowsSettings"></a> Capturer les paramètres Windows  
 Utilisez cette étape pour capturer les paramètres Windows de l’ordinateur exécutant la séquence de tâches. La séquence de tâches enregistre ces paramètres dans des variables de séquence de tâches. Ces paramètres capturés remplacent les paramètres par défaut que vous configurez pour l’étape **Appliquer les paramètres Windows**.  

 Cette étape de séquence de tâches s'exécute dans Windows PE ou un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Capturer les paramètres Windows](task-sequence-action-variables.md#BKMK_CaptureWindowsSettings).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Paramètres**, puis sélectionnez **Capturer les paramètres Windows** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Migrer le nom de l’ordinateur**  
 Capture le nom NetBIOS de l’ordinateur.  

 **Migrer les noms d’organisations et d’utilisateurs inscrits**  
 Capture les noms des utilisateurs et des organisations inscrits à partir de l’ordinateur.  

 **Migrer le fuseau horaire**  
 Capture le paramètre de fuseau horaire sur l’ordinateur.  



##  <a name="BKMK_CheckReadiness"></a> Vérifier la préparation  
 Utilisez cette étape pour vérifier que l’ordinateur cible satisfait aux conditions des prérequis du déploiement spécifiées.  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Vérifier la préparation** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Garantir une mémoire minimum (Mo)**  
 Vérifiez que la quantité de mémoire (en Mo), atteint ou dépasse la quantité spécifiée. L’étape active ce paramètre par défaut.  

 **Garantir une vitesse de processeur minimum (MHz)**  
 Vérifiez que la quantité de mémoire (en Mo) atteint ou dépasse la quantité spécifiée. L’étape active ce paramètre par défaut.  

 **Garantir un espace disque libre minimum (Mo)**  
 Vérifiez que la quantité d’espace disque libre (en Mo) atteint ou dépasse la quantité spécifiée.  

 **S’assurer que le SE à actualiser est**  
 Vérifiez que le système d’exploitation installé sur l’ordinateur cible remplit la condition spécifiée. Par défaut, l’étape définit cette valeur sur **CLIENT**.  

### <a name="options"></a>Options
 > [!NOTE]  
 > Si vous activez le paramètre **Continuer en cas d’erreur** sous l’onglet **Options** de cette étape, elle consigne seulement les résultats de la vérification de la préparation. Si une vérification échoue, la séquence de tâches ne s’arrête pas.



##  <a name="BKMK_ConnectToNetworkFolder"></a> Se connecter à un dossier réseau  
 Utilisez cette étape pour créer une connexion avec un dossier réseau partagé.  

 Cette étape de séquence de tâches s'exécute dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Se connecter à un dossier réseau](task-sequence-action-variables.md#BKMK_ConnecttoNetworkFolder).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Connexion à un dossier réseau** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Chemin**  
 Cliquez sur **Parcourir** pour spécifier le chemin du dossier réseau. Utilisez le format  *\\\serveur\partage*.

 **Lecteur**  
 Sélectionnez la lettre de lecteur local à affecter pour cette connexion. 

 **Compte**  
 Cliquez sur **Définir** pour spécifier le compte d’utilisateur disposant des autorisations nécessaires pour se connecter à ce dossier réseau.



##  <a name="BKMK_DisableBitLocker"></a> Désactiver BitLocker  
 Utilisez cette étape pour désactive le chiffrement BitLocker sur le lecteur du système d’exploitation actuel ou sur un lecteur spécifique. Cette action laisse les protecteurs de clé visibles en texte clair sur le disque dur, mais elle ne déchiffre pas le contenu du lecteur. En conséquence, cette action est terminée presque instantanément.  

> [!NOTE]  
>  Le chiffrement de lecteur BitLocker propose un cryptage de bas niveau du contenu d'un volume de disque.  

 Si vous avez plusieurs lecteurs chiffrés, vous devez désactiver BitLocker sur chaque lecteur de données avant de désactiver BitLocker sur le lecteur du système d'exploitation.  

 Cette étape s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Disques**, puis sélectionnez **Désactiver BitLocker** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Lecteur du système d’exploitation actuel**  
 Désactive BitLocker sur le disque du système d'exploitation courant.  

 **Lecteur spécifique**  
 Désactive BitLocker sur un disque spécifique. Dans la liste déroulante, sélectionnez le disque sur lequel BitLocker est désactivé.  



##  <a name="BKMK_DownloadPackageContent"></a> Télécharger le contenu du package  
 Utilisez cette étape pour télécharger un des types de package suivants :  

-   Images du système d'exploitation  

-   Packages de mise à niveau du système d’exploitation  

-   Packages de pilotes  

-   Packages  

-   Images de démarrage
    
Cette étape fonctionne bien dans une séquence de tâches pour mettre à niveau un système d’exploitation dans les scénarios suivants :  

-   Pour utiliser une seule séquence de tâches de mise à niveau qui peut fonctionner avec les plateformes x86 et x64. Incluez deux étapes **Télécharger le contenu du package** dans le groupe **Préparer pour la mise à niveau**. Spécifier des conditions sous l’onglet **Options** pour détecter l’architecture du client et télécharger seulement le package de mise à niveau du système d’exploitation approprié. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable. Utilisez cette variable pour le chemin du média pour l’étape **Mettre à niveau le système d’exploitation**.  

-   Pour télécharger dynamiquement un package de pilotes applicable, utilisez deux étapes **Télécharger le contenu du package** avec des conditions pour détecter le type de matériel approprié pour chaque package de pilotes. Configurez chaque étape **Télécharger le contenu du package** pour utiliser la même variable. Utilisez la variable pour la valeur de **Contenu intermédiaire** dans la section Pilotes de l’étape **Mettre à niveau le système d’exploitation**.  

> [!NOTE]    
> Quand vous déployez une séquence de tâches contenant l’étape Télécharger le contenu du package, ne sélectionnez pas **Télécharger tout le contenu localement avant de démarrer la séquence de tâches** ou **Accéder au contenu directement depuis le point de distribution** pour les **Options de déploiement** dans la page **Points de distribution** de l’Assistant Déploiement logiciel.  

Cette étape s'exécute dans un système d'exploitation standard ou Windows PE. Toutefois, la possibilité d’enregistrer le package dans le cache du client Configuration Manager n’est pas prise en charge dans WinPE.

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Logiciel**, puis sélectionnez **Télécharger le contenu du package** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 Icône**Sélectionner un package**  
 Cliquez sur l’icône pour sélectionner le package à télécharger. Après avoir sélectionné un package, vous pouvez cliquer une nouvelle fois sur l’icône pour choisir un autre package.  

 **Placez à l’emplacement suivant**  
 Choisissez d’enregistrer le package à l’un des emplacements suivants :  

 -   **Répertoire de travail de séquence de tâches**  

 -   **Cache du client Configuration Manager** : utilisez cette option pour stocker le contenu dans le cache du client. Le client agit en tant que source de cache d’homologue pour d’autres clients du cache d’homologue. Pour plus d’informations, consultez [Préparer la mise en cache d’homologue Windows PE pour réduire le trafic WAN](../get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md).  

 -    **Chemin personnalisé** : avec cette option, le moteur de séquence de tâches télécharge d’abord le package dans le répertoire de travail de séquence de tâches, puis le déplace vers le chemin que vous spécifiez. Le moteur de séquence de tâches ajoute le chemin avec l’ID de package. 
   
**Enregistrez le chemin d’accès en tant que variable**  
 Vous pouvez enregistrer le chemin en tant que variable que vous pouvez utiliser dans une autre étape de séquence de tâches. Configuration Manager ajoute un suffixe numérique au nom de la variable. Par exemple, si vous spécifiez une variable %*mon_contenu*% comme variable personnalisée, elle est la racine de l’emplacement où la séquence de tâches stocke tout le contenu référencé. Ce contenu peut contenir plusieurs packages. Ensuite, quand vous faites référence à la variable, ajoutez un suffixe numérique. Par exemple, pour le premier package, faites référence à %*mon_contenu01*%. Quand vous faites référence à la variable dans des étapes ultérieures, par exemple **Mettre à niveau le système d’exploitation**, utilisez %*mon_contenu02*% ou %*mon_contenu03*%, où le numéro correspond à l’ordre dans lequel l’étape **Télécharger le contenu du package** répertorie les packages.  

**En cas d’échec de téléchargement d’un package, continuer le téléchargement des autres packages de la liste**  
 Si la séquence de tâches échoue à télécharger un package, elle commence à télécharger le package suivant dans la liste.  



##  <a name="BKMK_EnableBitLocker"></a> Activer BitLocker  
Utilisez cette étape pour activer le chiffrement BitLocker sur au moins deux partitions du disque dur. La première partition active contient le code d'amorçage Windows. Une autre partition contient le système d'exploitation. La partition d'amorçage ne doit pas être chiffrée.  

Utilisez l'étape de séquence de tâches **Préconfigurer BitLocker** pour activer BitLocker sur un lecteur dans Windows PE. Pour plus d’informations, consultez la section [Préapprovisionner BitLocker](#BKMK_PreProvisionBitLocker).  

> [!NOTE]  
>  Le chiffrement de lecteur BitLocker propose un cryptage de bas niveau du contenu d'un volume de disque.  

L'étape **Activer BitLocker** s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Activer BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Quand vous spécifiez **TPM uniquement**, **TPM et clé de démarrage sur USB** ou **TPM et code confidentiel**, le module de plateforme sécurisée (TPM) doit être dans l’état suivant pour que vous puissiez effectuer l’étape **Activer BitLocker** :  

-   Permis  
-   Activé  
-   Propriété autorisée  
   
Cette étape effectue l’initialisation des éventuels modules de plateforme sécurisée restants. Les étapes restantes ne nécessitent pas de présence physique ni de redémarrages. Si nécessaire, l’étape **Activer BitLocker** effectue de façon transparente les étapes d’initialisation des modules de plateforme sécurisée restants :  

-   Créer une paire de clés de validité  
-   Créer une valeur d'autorisation du propriétaire et la déposer dans Active Directory, qui doit avoir été développé afin de prendre en charge cette valeur.  
-   Se définir comme propriétaire  
-   Créer la clé racine de stockage ou la réinitialiser si elle existe déjà mais qu'elle est incompatible.  
   
Si vous voulez que la séquence de tâches attende que l’étape **Activer BitLocker** termine le processus de chiffrement du lecteur, sélectionnez l’option **Attendre**. Si vous ne sélectionnez pas l’option **Attendre**, le processus de chiffrement du lecteur est effectué en arrière-plan. La séquence de tâches passe immédiatement à l’étape suivante.  

BitLocker peut être utilisé pour chiffrer plusieurs lecteurs sur un système d'ordinateurs (système d'exploitation et lecteurs de données). Pour chiffrer un lecteur de données, chiffrez d’abord le lecteur du système d’exploitation et terminez le processus de chiffrement. Cette opération est nécessaire, car le lecteur du système d’exploitation stocke les protecteurs de clé des lecteurs de données. Si vous chiffrez le lecteur du système d’exploitation et les lecteurs de données dans la même séquence de tâches, sélectionnez l’option **Attendre** pour l’étape **Activer BitLocker** pour le lecteur du système d’exploitation.  

Si le disque dur est déjà chiffré mais que BitLocker est désactivé, l’étape **Activer BitLocker** réactive les protecteurs de clé et se termine rapidement. Dans ce cas, il n'est pas nécessaire de chiffrer de nouveau le disque.  

Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Activer BitLocker](task-sequence-action-variables.md#BKMK_EnableBitLocker).  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Disques**, puis sélectionnez **Activer BitLocker** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Lecteur à chiffrer**  
 Indique le lecteur à chiffrer. Pour chiffrer le lecteur du système d'exploitation actuel, sélectionnez **Lecteur du système d'exploitation actuel** , puis configurez l'une des options suivantes de gestion des clés :  

-   **TPM uniquement**: sélectionnez cette option pour utiliser uniquement le module de plateforme sécurisée (TPM).  

-   **Clé de démarrage sur USB uniquement**: sélectionnez cette option pour utiliser une clé de démarrage stockée sur une clé USB. Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce qu'un périphérique USB contenant une clé de démarrage BitLocker soit connecté à l'ordinateur.  

-   **TPM et clé de démarrage sur USB**: sélectionnez cette option pour utiliser le module TPM et une clé de démarrage stockée sur une clé USB. Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce qu'un périphérique USB contenant une clé de démarrage BitLocker soit connecté à l'ordinateur.  

-   **TPM et code confidentiel**: sélectionnez cette option pour utiliser le module TPM et un numéro d’identification personnel (code confidentiel). Lorsque vous sélectionnez cette option, BitLocker verrouille le processus de démarrage normal jusqu'à ce que l'utilisateur fournisse le code confidentiel.  
   
Pour chiffrer un lecteur de données spécifique autre qu'un lecteur de système d'exploitation, sélectionnez **Lecteur spécifique**, puis sélectionnez le lecteur dans la liste.  

**Emplacement de création de la clé de récupération**  
 Pour spécifier où BitLocker crée le mot de passe de récupération et dépose la clé dans Active Directory, sélectionnez **Dans Active Directory**. Si vous sélectionnez cette option, vous devez étendre Active Directory pour le site. BitLocker peut ensuite enregistrer les informations de récupération associées dans Active Directory. Sélectionnez **Ne pas créer de clé de récupération** pour ne pas créer un mot de passe. La création d’un mot de passe est une bonne pratique.  

**Attendez que BitLocker termine le processus de chiffrement des lecteurs avant de poursuivre l’exécution de la séquence de tâches**  
 Sélectionnez cette option pour autoriser le chiffrement de lecteur BitLocker à se terminer avant l’exécution de la séquence de tâches suivante. Si vous sélectionnez cette option, BitLocker chiffre le volume de disque entier avant que l’utilisateur puisse se connecter à l’ordinateur.  

Le processus de chiffrement peut prendre des heures dans le cas du chiffrement d’un disque dur de grande taille. Si vous ne sélectionnez pas cette option, la séquence de tâches débute immédiatement.  



##  <a name="BKMK_FormatandPartitionDisk"></a> Formater et partitionner le disque  
 Utilisez cette étape pour formater et partitionner un disque spécifié sur un ordinateur de destination.  

> [!IMPORTANT]  
>  Chaque paramètre défini pour cette étape de la séquence de tâches s'applique à un seul disque spécifié. Pour formater et partitionner un autre disque sur l’ordinateur de destination, ajoutez une étape supplémentaire **Formater et partitionner le disque** à la séquence de tâches.  

 Cette étape de séquence de tâches s'exécute uniquement dans Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches pour cette action, consultez [Variables d’action de séquence de tâches Formater et partitionner le disque](task-sequence-action-variables.md#BKMK_FormatPartitionDisk).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Disques**, puis sélectionnez **Formater et partitionner le disque** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Numéro du disque**  
 Numéro de disque physique du disque à formater. Le numéro se base sur le classement d'énumération du disque Windows.  

 **Type du disque**  
 Le type du disque formaté. Deux options sont disponibles dans la liste déroulante : 

-   Standard (MBR) – Secteur de démarrage principal
-   GPT – Table de partition GUID  

> [!NOTE]  
>  Si vous passez le type de disque de **Standard (MBR)** à **GPT** et si la structure des partitions contient une partition étendue, la séquence de tâches supprime toutes les partitions étendues et logiques de la structure. L’Éditeur de séquence de tâches vous invite à confirmer cette action avant de changer le type de disque.  
   
**Volume**  
 Informations spécifiques sur la partition ou le volume créé par la séquence de tâches, incluant les attributs suivants :  

-   Nom  
-   Espace disque restant  
   
Pour créer une partition, cliquez sur **Nouveau** pour ouvrir la boîte de dialogue **Propriétés de la partition** . Spécifiez le type et la taille de la partition, et s’il s’agit d’une partition de démarrage. Pour modifier une partition existante, cliquez sur la partition à modifier puis sur le bouton Propriétés. Pour plus d’informations sur la façon de configurer des partitions de disque dur, consultez un des articles suivants :  

-   [Configurer des partitions de disque dur UEFI/GPT](http://go.microsoft.com/fwlink/?LinkID=272104)  
-   [Configurer des partitions de disque dur BIOS/MBR](http://go.microsoft.com/fwlink/?LinkId=272105)  

Pour supprimer une partition, sélectionnez-la, puis cliquez sur **Supprimer**.  



##  <a name="BKMK_InstallApplication"></a> Installer l’application  
Cette étape installe les applications spécifiées, ou un ensemble d’applications défini par une liste dynamique de variables de séquence de tâches. Lorsque cette étape est exécutée, l'installation de l'application commence immédiatement sans attendre un intervalle d'interrogation de stratégie.  

Les applications installées doivent répondre aux critères suivants :  

-   L’application doit avoir un type de déploiement Windows Installer ou Programme d’installation de script. Les types de déploiement Package d’application Windows (fichier .appx) ne sont pas pris en charge.  

-   Il doit être exécuté sous le compte système local et non le compte d'utilisateur.  

-   Il ne doit pas interagir avec le Bureau. Le programme doit s'exécuter en mode silencieux ou en mode sans assistance.  

-   Il ne doit pas lancer un redémarrage seul. L'application doit demander un redémarrage à l'aide du code de redémarrage standard 3010, qui est un code de sortie. Ce comportement garantit que l’étape de la séquence de tâches gère correctement le redémarrage. Si l'application renvoie un code de sortie 3010, le moteur de séquences de tâches sous-jacent effectue le redémarrage. Après le redémarrage, la séquence de tâches se poursuit automatiquement.  

Quand l’étape **Installer l’application** s’exécute, l’application vérifie l’applicabilité des règles de spécification et la méthode de détection sur ses types de déploiement. Selon les résultats de cette vérification, l'application installe le type de déploiement applicable. Si un type de déploiement contient des dépendances, le type de déploiement dépendant est évalué et installé dans le cadre de l'étape Installer l'application. Les dépendances d'application ne sont pas prises en charge pour les médias autonomes.  

> [!NOTE]  
>  Pour installer une application qui en remplace une autre, les fichiers de contenu de l’application remplacée doivent être disponibles. Si ce n’est pas le cas, cette étape de la séquence de tâches échoue. Par exemple, Microsoft Visio 2010 est installé sur un client ou dans une image capturée. Quand l’étape **Installer l’application** installe Microsoft Visio 2013, les fichiers de contenu de Microsoft Visio 2010 (l’application remplacée) doivent être disponibles sur un point de distribution. Si Microsoft Visio n’est pas installé du tout sur un client ou sur l’image capturée, la séquence de tâches installe Microsoft Visio 2013 sans rechercher les fichiers de contenu Microsoft Visio 2010.  

> [!NOTE]
> Si le client échoue à récupérer la liste des points de gestion auprès des services de localisation, utilisez les variables intégrées SMSTSMPListRequestTimeoutEnabled et SMSTSMPListRequestTimeout pour spécifier le délai d’attente (en millisecondes) d’une séquence de tâche avant qu’elle retente d’installer une application ou une mise à jour logicielle. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Logiciel**, puis sélectionnez **Installer l’application** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** pour cette étape, configurez les paramètres décrits dans cette section.  

 **Installer les applications suivantes**  
 La séquence de tâches installe ces applications dans l’ordre spécifié.  

 Configuration Manager exclut toutes les applications désactivées ou les applications avec les paramètres suivants :  

-   Uniquement quand un utilisateur a ouvert une session  
-   Exécuter avec les droits utilisateur  

Ces applications n’apparaissent pas dans la boîte de dialogue **Sélectionner l’application à installer**.
  
**Installer les applications en fonction de la liste de variables dynamiques**  
La séquence de tâches installe les applications en utilisant ce nom de variable de base. Le nom de variable de base vaut pour un ensemble de variables de séquence de tâches définies pour un regroupement ou un ordinateur. Ces variables spécifient les applications que la séquence de tâches installe pour ce regroupement ou cet ordinateur. Chaque nom de variable comprend son nom de base courant plus un suffixe numérique commençant par 01. La valeur de chaque variable doit contenir le nom de l'application et rien d'autre.  

Pour que la séquence de tâches installe les applications en utilisant une liste de variables dynamiques, activez le paramètre suivant sous l’onglet **Général** de la boîte de dialogue **Propriétés** de l’application : **Autoriser cette application à être installée à partir de l’action de la séquence de tâches Installer l’application plutôt que de la déployer manuellement**.  

> [!NOTE]  
>  Vous ne pouvez pas installer d'applications à l'aide d'une liste de variables dynamiques pour les déploiements de média autonome.  

Par exemple, pour installer une application unique à l'aide d'une variable de séquence de tâches nommée AA01, vous indiquez la variable suivante :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA01|Microsoft Office|  

Pour installer deux applications, vous indiqueriez les variables suivantes :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA01|Microsoft Lync|  
|AA02|Microsoft Office|  

Les conditions suivantes affectent les applications installées par la séquence de tâches :  

-   Si la valeur d'une variable contient d'autres informations que le nom de l'application. La séquence de tâches n’installe pas l’application et elle continue.  

-   Si la séquence de tâches ne trouve pas de variable avec le nom de base spécifié et le suffixe « 01 », la séquence de tâches n’installe aucune application. 
    
> [!Important]  
> Ces valeurs de texte respectent la casse. Par exemple, « installer » ne correspond pas à « Installer ». Si vous devez modifier la valeur, l’éditeur de séquence de tâches ne détecte pas un changement de casse. Vous devez effectuer une autre modifier en même temps, par exemple, modifier la description de l’étape.<!--509714-->   

   
**Si l’installation d’une application échoue, continuer d’installer les autres applications de la liste**  
 Ce paramètre spécifie que l’étape continue quand l’installation d’une application individuelle échoue. Si vous spécifiez ce paramètre, la séquence de tâches continue indépendamment des erreurs d’installation. Si vous ne spécifiez pas ce paramètre et que l’installation échoue, l’étape se termine immédiatement.  

### <a name="options"></a>Options
 > [!NOTE] 
 > Quand vous sélectionnez **Continuer en cas d’erreur** sous l’onglet **Options** de cette étape, la séquence de tâches continue quand l’installation d’une application échoue. Quand vous n’activez pas cette option, la séquence de tâches échoue et n’installe pas les applications restantes.  
 
Outre les options par défaut, configurez les paramètres supplémentaires suivants sous l’onglet **Options** de cette étape de séquence de tâches :  

-   **Recommencer cette étape si l’ordinateur redémarre inopinément**  
    Si une des installations d’application redémarre l’ordinateur de façon inattendue, recommence cette étape. L’étape active ce paramètre par défaut avec deux nouvelles tentatives. Vous pouvez spécifier de une à cinq nouvelles tentatives.  



##  <a name="BKMK_InstallPackage"></a> Installer le package
Utilisez cette étape pour installer un package logiciel dans le cadre de la séquence de tâches. Quand cette étape est exécutée, l’installation commence immédiatement sans attendre un intervalle d’interrogation de stratégie.  

Le package doit respecter les critères suivants :  

-   Il doit être exécuté sous le compte système local et non pas sous un compte d’utilisateur.  

-   Il ne doit pas interagir avec le Bureau. Le programme doit s'exécuter en mode silencieux ou en mode sans assistance.  

-   Il ne doit pas lancer un redémarrage seul. Le logiciel doit demander un redémarrage à l'aide du code de redémarrage standard 3010, qui est un code de sortie. Ce comportement garantit que l’étape de la séquence de tâches gère correctement le redémarrage. Si le logiciel retourne un code de sortie 3010, le moteur de séquences de tâches sous-jacent redémarre l’ordinateur. Après le redémarrage, la séquence de tâches se poursuit automatiquement.  

Les programmes qui utilisent l'option **Exécuter un autre programme en premier** pour installer un programme dépendant ne sont pas pris en charge lors du déploiement d'un système d'exploitation. Si vous activez l’option **Exécuter un autre programme en premier** et que le programme dépendant a déjà été exécuté sur l’ordinateur de destination, le programme dépendant s’exécute et la séquence de tâches continue. En revanche, si le programme dépendant n’a pas déjà été exécuté sur l’ordinateur de destination, l’étape de la séquence de tâches échoue.  

> [!NOTE]  
>  Le site d’administration centrale n’a pas les stratégies de configuration de client nécessaires pour activer l’agent de distribution logicielle lors de l’exécution de la séquence de tâches. Lorsque vous créez un média autonome pour une séquence de tâches sur le site d'administration centrale et que la séquence de tâches contient une étape **Installer le package** , l'erreur suivante peut apparaître dans le fichier CreateTsMedia.log :  
>   
>  `"WMI method SMS_TaskSequencePackage.GetClientConfigPolicies failed (0x80041001)"`  
>   
>  Pour un média autonome qui inclut une étape **Installer le package**, créez le média autonome sur un site principal où l’agent de distribution logicielle est activé. Vous pouvez aussi ajouter une étape **Exécuter la ligne de commande** après l’étape **Configurer Windows et ConfigMgr** et avant la première étape **Installer le package**. L’étape **Exécuter la ligne de commande** exécute une commande WMIC pour activer l’agent de distribution logicielle avant la première étape **Installer le package**. Utilisez la commande suivante dans l’étape **Exécuter la ligne de commande** :  
>   
>  **Ligne de commande** : `WMIC /namespace:\\\root\ccm\policy\machine\requestedconfig path ccm_SoftwareDistributionClientConfig CREATE ComponentName="Enable SWDist", Enabled="true", LockSettings="TRUE", PolicySource="local", PolicyVersion="1.0", SiteSettingsKey="1" /NOINTERACTIVE`  
>   
>  Pour plus d’informations sur la création d’un média autonome, consultez [Créer un média autonome](../deploy-use/create-stand-alone-media.md).  

Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Logiciel**, puis sélectionnez **Installer le package** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Installer un seul package logiciel**  
 Ce paramètre permet de spécifier un package logiciel Configuration Manager. L’étape attend que l’installation soit terminée.  

 **Installer les packages logiciels en fonction de la liste de variables dynamiques**  
 La séquence de tâches installe les packages en utilisant ce nom de variable de base. Le nom de variable de base vaut pour un ensemble de variables de séquence de tâches définies pour un regroupement ou un ordinateur. Ces variables spécifient les packages que la séquence de tâches installe pour ce regroupement ou cet ordinateur. Chaque nom de variable comprend son nom de base courant plus un suffixe numérique commençant par 001. La valeur de chaque variable doit contenir un ID de package et le nom du logiciel séparés par deux-points.  

 Pour que la séquence de tâches installe les logiciels en utilisant une liste de variables dynamiques, activez le paramètre suivant sous l’onglet **Avancé** de la boîte de dialogue **Propriétés** du package : **Autoriser l’installation de ce programme depuis la séquence de tâches d’installation du package sans le déployer**.  

> [!NOTE]  
>  Vous ne pouvez pas installer de packages logiciels à l'aide d'une liste de variables dynamiques pour les déploiements de média autonome.  

 Par exemple, pour installer un package logiciel unique à l'aide d'une variable de séquence de tâches nommée AA001, vous indiquez la variable suivante :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  

 Pour installer trois packages logiciels, vous indiqueriez les variables suivantes :  

|Nom de la variable :|Valeur de la variable|  
|-------------------|--------------------|  
|AA001|CEN00054:Install|  
|AA002|CEN00107:Install Silent|  
|AA003|CEN00031:Install|  

 Les conditions suivantes affectent les packages installés par la séquence de tâches :  

-   Si vous ne créez pas la valeur d’une variable au format correct, ou si elle ne spécifie pas un ID et un nom de package valides, l’installation du logiciel échoue.  

-   Si l’ID de package contient des caractères en minuscules, l’installation du logiciel échoue.  

-   Si la séquence de tâches ne trouve pas de variable avec le nom de base spécifié et le suffixe « 001 », la séquence de tâches n’installe aucun package. La séquence de tâches continue.  
    
> [!Important]  
> Ces valeurs de texte respectent la casse. Par exemple, « installer » ne correspond pas à « Installer ». Si vous devez modifier la valeur, l’éditeur de séquence de tâches ne détecte pas un changement de casse. Vous devez effectuer une autre modifier en même temps, par exemple, modifier la description de l’étape.<!--509714-->   

   
**Si l’installation d’un package logiciel échoue, continuer d’installer les autres packages de la liste**  
 Ce paramètre spécifie que l'étape se poursuit si l'installation d'un package logiciel individuel échoue. Si vous spécifiez ce paramètre, la séquence de tâches continue indépendamment des erreurs d’installation. Si vous ne spécifiez pas ce paramètre et que l’installation échoue, l’étape se termine immédiatement.  



##  <a name="BKMK_InstallSoftwareUpdates"></a> Installer les mises à jour logicielles  
Utilisez cette étape pour installer des mises à jour logicielles sur l’ordinateur de destination. L'ordinateur de destination n'est pas évalué pour déterminer les mises à jour logicielles applicables avant l'exécution de cette séquence de tâches. À ce moment, l’ordinateur de destination est évalué pour déterminer les mises à jour logicielles comme n’importe quel autre client Configuration Manager. Pour que cette étape installe des mises à jour logicielles, vous devez d’abord déployer les mises à jour sur un regroupement dont l’ordinateur cible est membre.  
>  [!IMPORTANT]
> Une bonne pratique pour optimiser les performances est d’installer la dernière version de l’Agent Windows Update. 
>* Pour Windows 7, consultez [l’article de la Base de connaissances 3161647](https://support.microsoft.com/kb/3161647).
>* Pour Windows 8, consultez [l’article de la Base de connaissances 3163023](https://support.microsoft.com/kb/3163023).

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Installer les mises à jour logicielles](task-sequence-action-variables.md#BKMK_InstallSoftwareUpdates).

 > [!NOTE]
 > Si le client échoue à récupérer la liste des points de gestion auprès des services de localisation, utilisez les variables intégrées SMSTSMPListRequestTimeoutEnabled et SMSTSMPListRequestTimeout pour spécifier le délai d’attente (en millisecondes) d’une séquence de tâche avant qu’elle retente d’installer une application ou une mise à jour logicielle. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Logiciel**, puis sélectionnez **Installer les mises à jour logicielles** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Nécessaires pour l’installation – Mises à jour logicielles obligatoires seulement**  
 Sélectionnez cette option pour installer toutes les mises à jour logicielles obligatoires avec des dates d’échéance d’installation définies par l’administrateur.  

 **Disponibles pour l’installation – Toutes les mises à jour logicielles**  
 Sélectionnez cette option pour installer toutes les mises à jour logicielles disponibles. Vous devez d’abord déployer ces mises à jour sur un regroupement dont l’ordinateur est membre. La séquence de tâches installe toutes les mises à jour logicielles disponibles sur les ordinateurs de destination.  

 **Évaluer les mises à jour logicielles à partir des résultats d’analyse en mémoire cache**  
 Par défaut, la séquence de tâches utilise les résultats de l’analyse en mémoire cache provenant de l’Agent Windows Update. Désactivez la case à cocher pour indiquer à l’Agent Windows Update de télécharger le dernier catalogue à partir du point de mise à jour logicielle. Choisissez cette option lors de l’utilisation d’une séquence de tâches pour [capturer et créer une image de système d’exploitation](../deploy-use/create-a-task-sequence-to-capture-an-operating-system.md). Dans ce scénario, le nombre de mises à jour logicielles est probablement élevé. La plupart de ces mises à jour auront des dépendances, par exemple installer X avant que Y apparaisse comme étant applicable. Quand vous désactivez ce paramètre et que vous déployez la séquence de tâches sur un grand nombre de clients, ils se connectent tous en même temps au point de mise à jour logicielle. Ce comportement peut entraîner des problèmes de performances pendant le traitement et le téléchargement du catalogue. La bonne pratique correspond au paramétrage par défaut, qui est d’utiliser les résultats de l’analyse en mémoire cache. 

La variable de séquence SMSTSSoftwareUpdateScanTimeout contrôle le délai d’expiration de l’analyse des mises à jour logicielles pendant cette étape. La valeur par défaut est de 30 minutes. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).

### <a name="options"></a>Options   
 Outre les options par défaut, configurez les paramètres supplémentaires suivants sous l’onglet **Options** de cette étape de séquence de tâches :  

-   **Recommencer cette étape si l’ordinateur redémarre inopinément**  
    Si une des mises à jour redémarre l’ordinateur de façon inattendue, recommence cette étape. L’étape active ce paramètre par défaut avec deux nouvelles tentatives. Vous pouvez spécifier de une à cinq nouvelles tentatives.  

    > [!NOTE]
    > Configurez la variable SMSTSWaitForSecondReboot pour spécifier le nombre de secondes de mise en suspens de la séquence de tâches après le redémarrage de l’ordinateur dans ce scénario. Pour plus d’informations, consultez [Variables intégrées de séquence de tâches](task-sequence-built-in-variables.md).



##  <a name="BKMK_JoinDomainorWorkgroup"></a> Joindre le domaine ou le groupe de travail  
 Utilisez cette étape pour ajouter l’ordinateur de destination à un domaine ou un groupe de travail.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables de l’action de séquence de tâches Joindre le domaine ou le groupe de travail](task-sequence-action-variables.md#BKMK_JoinDomainWorkgroup).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Joindre le domaine ou le groupe de travail** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Joindre un groupe de travail**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du groupe de travail spécifié. Si l’ordinateur est actuellement membre d’un domaine, la sélection de cette option provoque son redémarrage.  

 **Joindre un domaine**  
 Sélectionnez cette option pour que l'ordinateur de destination fasse partie du domaine spécifié.  

 Facultatif : entrez ou accédez à une unité d'organisation du domaine spécifié pour que l'ordinateur s'y joigne. Si l’ordinateur est actuellement membre d’un autre domaine ou groupe de travail, cette option provoque son redémarrage. Si l’ordinateur est déjà membre d’une autre unité d’organisation, dans la mesure où Active Directory Domain Services n’autorise pas le changement de l’unité d’organisation via cette méthode, l’installation de Windows ignore ce paramètre.  

 **Entrez le compte autorisé à joindre le domaine**  
 Cliquez sur **Définir** pour entrer le nom d’utilisateur et le mot de passe d’un compte ayant les autorisations de joindre le domaine. Entrez le compte au format : *domaine\compte*  



## <a name="BKMK_PrepareConfigMgrClientforCapture"></a> Préparer le client ConfigMgr pour capture  
Utilisez cette étape pour supprimer ou configurer le client Configuration Manager sur l’ordinateur de référence. Cette action prépare l’ordinateur pour la capture dans le cadre du processus de création d’image.

À compter de Configuration Manager version 1610, l’étape **Préparer le client ConfigMgr** supprime complètement le client Configuration Manager, au lieu de supprimer seulement les informations de clé. Quand la séquence de tâches déploie l’image capturée du système d’exploitation, elle installe chaque fois un nouveau client Configuration Manager.  

> [!Note]  
>  Le moteur de séquence de tâches supprime seulement le client pendant la séquence de tâches **Créer et capturer une image de système d’exploitation de référence**. Le moteur de séquence de tâches ne supprime pas le client lors de l’application des autres méthodes de capture, comme un média de capture ou une séquence de tâches personnalisée.

Avant Configuration Manager version 1610, cette étape effectuait les tâches suivantes :  

-   Supprime du fichier smscfg.ini présent dans le répertoire Windows la section des propriétés de configuration du client. Celles-ci comprennent des informations spécifiques au client, par exemple le GUID Configuration Manager, ainsi que d’autres identificateurs clients.  

-   Supprime tous les certificats d’ordinateur SMS ou Configuration Manager.  

-   Supprime le cache du client Configuration Manager.  

-   Efface la variable de site attribuée au client Configuration Manager.  

-   Supprime toutes les stratégies Configuration Manager locales.  

-   Supprime la clé racine approuvée du client Configuration Manager.  

Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis sélectionnez **Préparer le client ConfigMgr pour capture** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Cette étape ne nécessite aucun paramètre sous l’onglet **propriétés**.



##  <a name="BKMK_PrepareWindowsforCapture"></a> Préparer Windows pour capture  
 Utilisez cette étape pour spécifier les options Sysprep à utiliser lors de la capture d’une image de système d’exploitation sur l’ordinateur de référence. Cette action de séquence de tâches exécute Sysprep, puis redémarre l’ordinateur dans l’image de démarrage Windows PE spécifiée pour la séquence de tâches. Cette action échoue si l’ordinateur de référence est joint à un domaine.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Préparer Windows pour capture](task-sequence-action-variables.md#BKMK_PrepareWindowsCapture).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis sélectionnez **Préparer Windows pour capture** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Créer automatiquement la liste des pilotes de stockage de masse**  
 Sélectionnez cette option pour demander à Sysprep de générer automatiquement une liste de pilotes de stockage de masse à partir de l'ordinateur de référence. Cette option active l'option des pilotes de stockage de masse dans le fichier sysprep.inf sur l'ordinateur de référence. Pour plus d’informations sur ce paramètre, consultez la documentation de Sysprep.  

 **Ne pas réinitialiser l’indicateur d’activation**  
 Choisissez cette option pour empêcher Sysprep de réinitialiser l'indicateur d'activation du produit.  



##  <a name="BKMK_PreProvisionBitLocker"></a> Préconfigurer BitLocker  
 Utilisez cette étape pour activer BitLocker sur un lecteur dans Windows PE. Seul l'espace disque utilisé étant chiffré, l'opération de chiffrement est beaucoup plus rapide. Vous appliquez les options de gestion de clés à l'aide de l'étape de séquence de tâches [Activer BitLocker](#BKMK_EnableBitLocker) une fois le système d'exploitation installé. Cette étape est exécutée uniquement sous Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard.  

> [!IMPORTANT]  
>  Le préapprovisionnement de BitLocker nécessite au moins Windows 7. L’ordinateur doit également contenir un module de plateforme sécurisée (TPM) pris en charge et activé.  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Disques**, puis sélectionnez **Préconfigurer BitLocker** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Appliquer BitLocker au lecteur spécifié**  
 Spécifiez le lecteur pour lequel vous souhaitez activer BitLocker. Seul l'espace utilisé sur le lecteur est chiffré.  

 **Ignorer cette étape pour les ordinateurs n’ayant pas un module de plateforme sécurisée ou lorsque celui-ci n’est pas activé**  
 Sélectionnez cette option pour ignorer le chiffrement de lecteur sur un ordinateur qui ne contient-elle pas un module de plateforme sécurisée pris en charge ou activé. Par exemple, utilisez cette option quand vous déployez un système d’exploitation sur une machine virtuelle.  



##  <a name="BKMK_ReleaseStateStore"></a> Libérer le magasin d’état  
 Utilisez cette étape pour notifier au point de migration d’état que l’action de capture ou de restauration est terminée. Utilisez cette étape en combinaison avec les étapes **Demander le magasin d’état**, **Capturer l’état utilisateur** et **Restaurer l’état utilisateur**. Vous utilisez ces étapes pour migrer des données d’état utilisateur en utilisant un point de migration d’état et l’outil USMT.  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Si vous utilisez l’étape **Demander le magasin d’état** pour demander l’accès à un point de migration de l’état pour *capturer* l’état utilisateur, cette étape informe le point de migration d’état que le processus de capture est terminé. Le point de migration d’état marque ensuite les données d’état utilisateur comme étant disponibles pour la restauration. Le point de migration d’état définit les autorisations de contrôle d’accès pour les données d’état utilisateur de façon que seul l’ordinateur de restauration y ait accès en lecture seule.  

 Si vous utilisez l’étape **Demander le magasin d’état** pour demander l’accès à un point de migration d’état pour *restaurer* l’état utilisateur, cette étape informe le point de migration d’état que le processus de restauration est terminé. Le point de migration d’état active ensuite ses paramètres de rétention des données tels qu’ils ont été configurés.  

> [!IMPORTANT]  
>  Une bonne pratique est de définir l’option **Continuer en cas d’erreur** pour toutes les étapes entre les étapes **Demander le magasin d’état** et **Libérer le magasin d’état**. Chaque étape **Demander le magasin d’état** doit avoir une étape **Libérer le magasin d’état** correspondante.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Libérer le magasin d’état](task-sequence-action-variables.md#BKMK_ReleaseStateStore).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **État utilisateur**, puis sélectionnez **Libérer le magasin d’état** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Cette étape ne nécessite aucun paramètre sous l’onglet **propriétés**.



##  <a name="BKMK_RequestStateStore"></a> Demander le magasin d’état  
 Utilisez cette étape pour demander l’accès à un point de migration d’état pendant la capture ou la restauration de l’état.  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Utilisez cette étape en combinaison avec les étapes **Libérer le magasin d’état**, **Capturer l’état utilisateur** et **Restaurer l’état utilisateur**. Vous utilisez ces étapes pour migrer l’état de l’ordinateur en utilisant un point de migration d’état et l’outil USMT.  

> [!NOTE]  
>  Lors de la création d’un point de migration d’état, le stockage de l’état de l’utilisateur n’est pas disponible pendant jusqu’à une heure. Pour accélérer ce processus, ajustez les paramètres de propriété sur le point de migration d’état afin de déclencher une mise à jour du fichier de contrôle du site.  

 Cette étape de séquence de tâches s'exécute dans un système d'exploitation standard et dans Windows PE pour USMT en mode hors connexion. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches Demander le magasin d’état](task-sequence-action-variables.md#BKMK_RequestState).  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **État utilisateur**, puis sélectionnez **Demander le magasin d’état** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Capturer l’état à partir de l’ordinateur**  
 Recherche un point de migration d’état qui répond à la configuration minimale requise, telle qu’elle est configurée dans les paramètres du point de migration état. Par exemple, **Nombre maximum de clients** et **Quantité minimale d’espace disque libre**. Cette option ne garantit pas qu’un espace suffisant est disponible au moment de la migration d’état. Cette option demande l’accès à un point de migration d’état afin de capturer l’état et les paramètres utilisateur sur un ordinateur.  

 Si le site Configuration Manager a plusieurs points de migration d’état actifs, cette étape recherche un point de migration d’état avec l’espace disque disponible. La séquence de tâches interroge le point de gestion pour obtenir une liste de points de migration d’état, puis elle évalue chacun d’eux jusqu’à en trouver un qui répond aux exigences minimales.  

 **Restaurer l’état à partir d’un autre ordinateur**  
 Demande l’accès à un point de migration d’état pour restaurer un état et des paramètres utilisateur précédemment capturés sur un ordinateur de destination.  

 S’il existe plusieurs points de migration d’état, cette étape recherche le point de migration d’état qui a l’état pour l’ordinateur de destination.  

 **Nombre de tentatives**  
 Nombre de fois que cette étape tente de trouver un point de migration d’état approprié avant d’échouer.  

 **Délai de nouvelle tentative (en secondes)**  
 Durée en secondes pendant laquelle l'étape de séquence de tâches attend entre chaque tentative.  

 **Si le compte d’ordinateur ne parvient pas à se connecter au magasin d’état, utiliser le compte d’accès réseau.**  
 Si la séquence de tâches ne peut pas accéder au point de migration d’état en utilisant le compte d’ordinateur, elle utilise les informations d’identification du compte d’accès réseau pour se connecter. Cette option est moins sécurisée, car d’autres ordinateurs peuvent utiliser le compte d’accès réseau pour accéder à l’état stocké. Cette option peut être nécessaire si l’ordinateur de destination n’est pas joint à un domaine.  



##  <a name="BKMK_RestartComputer"></a> Redémarrer l’ordinateur  
 Utilisez cette étape pour redémarrer l’ordinateur qui exécute la séquence de tâches. Après avoir redémarré, l’ordinateur passe automatiquement à l’étape suivante de la séquence de tâches.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches Redémarrer l’ordinateur](task-sequence-action-variables.md#BKMK_RestartComputer).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Redémarrer l’ordinateur** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **L’image de démarrage attribuée à cette séquence de tâches**  
 Sélectionnez cette option pour que l’ordinateur de destination utilise l’image de démarrage qui est affectée à la séquence de tâches. La séquence de tâches utilise l’image de démarrage pour exécuter les étapes suivantes dans Windows PE.  

 **Le système d’exploitation par défaut installé actuellement**  
 Sélectionnez cette option pour que l'ordinateur de destination redémarre sous le système d'exploitation installé.  

 **Notifier l’utilisateur avant de redémarrer**  
 Sélectionnez cette option pour afficher une notification à l’utilisateur avant que l’ordinateur de destination redémarre. L’étape sélectionne cette option par défaut.  

 **Message de notification**  
 Entrez un message de notification à afficher à l’utilisateur avant le redémarrage de l’ordinateur de destination.  

 **Délai d’affichage du message**  
 Spécifiez le délai en secondes avant que l’ordinateur de destination redémarre. La valeur par défaut est de 60 secondes.  



##  <a name="BKMK_RestoreUserState"></a> Restaurer l’état utilisateur  
 Utilisez cette étape pour lancer l’outil USMT pour restaurer l’état et les paramètres utilisateur sur l’ordinateur de destination. Vous utilisez cette étape en combinaison avec l’étape **Capturer l’état utilisateur**.  

 Pour plus d’informations sur la gestion de l’état utilisateur pendant le déploiement de systèmes d’exploitation, consultez [Gérer l’état utilisateur](../get-started/manage-user-state.md).  

 Utilisez cette étape avec les étapes **Demander le magasin d’état** et **Libérer le magasin d’état** pour enregistrer ou restaurer les paramètres d’état avec un point de migration d’état. Dans USMT 3.0 et versions supérieures, cette option déchiffre toujours le magasin d’état USMT au moyen d’une clé de chiffrement générée et gérée par Configuration Manager.  

 L’étape **Restaurer l’état utilisateur** permet de contrôler un sous-ensemble limité des options USMT les plus couramment utilisées. Spécifiez d’autres options de ligne de commande avec la variable de séquence de tâches OSDMigrateAdditionalRestoreOptions.  

> [!IMPORTANT]  
>  Si vous utilisez cette étape dans un but non lié à un scénario de déploiement de système d’exploitation, ajoutez l’étape [Restaurer l’état utilisateur](#BKMK_RestartComputer) immédiatement après l’étape **Restaurer l’état utilisateur**.  

 Cette étape s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE. Pour plus d’informations sur les variables de séquence de tâches de cette action, consultez [Variables d’action de séquence de tâches Restaurer l’état utilisateur](task-sequence-action-variables.md#BKMK_RestoreUserState).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **État utilisateur**, puis sélectionnez **Restaurer l’état utilisateur** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Package de l’outil de migration de l’état utilisateur**  
 Spécifiez le package qui contient la version de l’outil USMT que cette étape doit utiliser. Ce package ne requiert pas de programme. Quand l’étape s’exécute, la séquence de tâches utilise la version de l’outil USMT présente dans le package spécifié. Spécifiez un package qui contient la version 32 bits ou 64 bits de l’outil USMT. L’architecture de l’outil USMT varie selon l’architecture du système d’exploitation dont la séquence de tâches restaure l’état. 

 **Restaurer tous les profils utilisateur capturés présentant des options standard**  
 Restaure les profils utilisateur capturés qui présentent des options standard. Pour personnaliser les options restaurées par l’outil USMT, sélectionnez **Personnaliser la façon dont les profils utilisateur sont capturés**.  

 **Personnaliser la restauration des profils utilisateur**  
 Permet de personnaliser les fichiers à restaurer sur l'ordinateur de destination. Cliquez sur **Fichiers** pour spécifier les fichiers de configuration du package USMT à utiliser pour restaurer les profils utilisateur. Pour ajouter un fichier de configuration, entrez le nom du fichier dans le champ **Nom de fichier** , puis cliquez sur **Ajouter**. Le volet Fichiers répertorie les fichiers de configuration utilisés par l’outil USMT. Le fichier .xml que vous spécifiez définit le fichier utilisateur restauré par l’outil USMT.  

 **Restaurer les profils utilisateur de l’ordinateur local**  
 Restaure les profils utilisateur de l'ordinateur local. Ces profils ne sont pas pour les utilisateurs de domaine. Vous devez attribuer de nouveaux mots de passe aux comptes d’utilisateur locaux. L’outil USMT ne peut pas migrer les mots de passe d’origine. Entrez le nouveau mot de passe dans le champ **Mot de passe** , puis confirmez le mot de passe dans le champ **Confirmer le mot de passe** .  

 **Continuer si certains fichiers ne peuvent pas être restaurés**  
 Continue la restauration de l’état et des paramètres utilisateur même si l’outil USMT ne peut pas restaurer certains fichiers. L’étape active cette option par défaut. Si vous désactivez cette option et que l’outil USMT rencontre des erreurs lors de la restauration de fichiers, cette étape échoue immédiatement. L’outil USMT ne restaure pas tous les fichiers.   

 **Activer la journalisation documentée**  
 Activez cette option pour générer des informations de fichiers journaux plus détaillées. Lors de la restauration de l’état, la séquence de tâches génère par défaut Loadstate.log dans le dossier de journalisation de la séquence de tâches, \windows\system32\ccm\logs.  



##  <a name="BKMK_RunCommandLine"></a> Exécuter la ligne de commande  
 Utilisez cette étape pour exécuter la ligne de commande spécifiée.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour plus d'informations sur les variables de séquences de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Exécuter la ligne de commande](task-sequence-action-variables.md#BKMK_RunCommand).  

 Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Exécuter la ligne de commande** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Ligne de commande**  
 Indique la ligne de commande exécutée. Ce champ doit obligatoirement être renseigné. Le fait d’inclure des extensions de noms de fichiers est une bonne pratique, par exemple, .vbs et .exe. Intégrez tous les fichiers de paramètres requis, les options des lignes de commande ou les commutateurs.  

 Si le nom de fichier est spécifié sans extension, Configuration Manager essaie les extensions .com, .exe et .bat. Si le nom de fichier a une extension, mais qu’il ne s’agit pas d’un fichier exécutable, Configuration Manager essaie d’appliquer une association locale. Par exemple, si la ligne de commande est readme.gif, Configuration Manager démarre l’application spécifiée sur l’ordinateur de destination pour ouvrir les fichiers .gif.  

 Exemples :  

 `setup.exe /a`  

 `cmd.exe /c copy Jan98.dat c:\sales\Jan98.dat`  

> [!NOTE]  
>  Pour que l’exécution se fasse correctement, faites précéder les actions de la ligne de commande de la commande **cmd.exe /c**. Des commandes de redirection de sortie, d’utilisation de canaux et de copie sont des exemples de ces actions.  

 **Désactiver la redirection du système de fichiers 64 bits**  
 Les systèmes d’exploitation 64 bits utilisent par défaut le redirecteur du système de fichiers WOW64 pour exécuter des lignes de commande. Ce comportement est destiné à trouver les versions 32 bits appropriées des exécutables et des bibliothèques du système d’exploitation. Sélectionnez cette option pour désactiver l’utilisation du redirecteur du système de fichiers WOW64. Windows exécute la commande en utilisant les versions 64 bits natives des exécutables et des bibliothèques du système d’exploitation. Cette option est sans effet lors de l’exécution sur un système d’exploitation 32 bits.  

 **Démarrer dans**  
 Spécifie le dossier exécutable pour le programme, comprenant jusqu'à 127 caractères. Ce dossier peut être un chemin d'accès absolu sur l'ordinateur de destination ou un chemin d'accès relatif au dossier du point de distribution qui contient le package. Ce champ est facultatif.  

 Exemples :  

 **c:\officexp**  

 **i386**  

> [!NOTE]  
>  Le bouton **Parcourir** permet de parcourir les fichiers et les dossiers de l’ordinateur local. Tout ce que vous sélectionnez doit également exister sur l’ordinateur de destination au même emplacement, et avec les mêmes noms de dossier et de fichier.  

 **Package**  
 Quand, sur la ligne de commande, vous spécifiez des fichiers ou des programmes qui ne sont pas déjà présents sur l’ordinateur de destination, sélectionnez cette option pour spécifier le package Configuration Manager qui contient les fichiers appropriés. Le package n'exige pas de programme. Cette option n'est pas nécessaire si le fichier spécifié existe sur l'ordinateur de destination.  

 **Délai**  
 Spécifie une valeur qui représente la durée pendant laquelle Configuration Manager autorise la ligne de commande à s’exécuter. Cette valeur est comprise entre 1 et 999 minutes. La valeur par défaut est 15 minutes.  

 Cette option est désactivée par défaut.  

> [!IMPORTANT]  
>  Si vous entrez une valeur qui ne donne pas suffisamment de temps à la commande spécifiée pour se terminer correctement, cette étape échoue. La séquence de tâches toute entière peut échouer en fonction d’autres paramètres de contrôle. Si le délai d’expiration est atteint, Configuration Manager met fin au processus de la ligne de commande.  

 **Exécuter cette étape en tant que compte suivant**  
 Spécifie que la ligne de commande est exécutée en tant que compte d'utilisateur Windows et non en tant que compte système local.  

> [!NOTE]  
>  Pour exécuter des scripts simples ou des commandes avec un autre compte après avoir installé le système d’exploitation, vous devez d’abord ajouter le compte à l’ordinateur. En outre, vous devez restaurer le profil de compte d’utilisateur Windows pour exécuter des programmes plus complexes, comme un programme d’installation de Windows.  

 **Compte**  
 Spécifie le compte d’utilisateur Windows que cette étape utilise pour exécuter la ligne de commande. La ligne de commande s’exécute avec les autorisations du compte spécifié. Cliquez sur **Définir** pour spécifier le compte de domaine ou le compte d'utilisateur local.  

> [!IMPORTANT]  
>  Si cette étape spécifie un compte d’utilisateur et s’exécute dans Windows PE, l’action échoue. Vous ne pouvez pas joindre Windows PE à un domaine. Le fichier smsts.log enregistre cet échec.  



##  <a name="BKMK_RunPowerShellScript"></a> Exécuter le script PowerShell  
 Utilisez cette étape pour exécuter le script PowerShell spécifié.  

 Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour exécuter cette étape dans Windows PE, PowerShell doit être activé dans l'image de démarrage. Vous pouvez activer Windows PowerShell (WinPE-PowerShell) à partir de l'onglet **Composants facultatifs** dans les propriétés de l'image de démarrage. Pour plus d’informations sur la modification d’une image de démarrage, consultez [Gérer les images de démarrage](../get-started/manage-boot-images.md).  

> [!NOTE]  
>  PowerShell n'est pas activé par défaut sur les systèmes d'exploitation Windows Embedded.  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Exécuter le script PowerShell** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Package**  
 Indique le package Configuration Manager qui contient le script PowerShell. Un package peut contenir plusieurs scripts PowerShell.  

 **Nom du script**  
 Spécifie le nom du script PowerShell à exécuter. Ce champ doit obligatoirement être renseigné.  

 **Paramètres**  
 Spécifie les paramètres passés au script Windows PowerShell. Ces paramètres sont les mêmes que les paramètres du script Windows PowerShell sur la ligne de commande.  

> [!IMPORTANT]  
>  Spécifiez les paramètres consommés par le script, et non pour la ligne de commande Windows PowerShell.  
>   
>  L'exemple suivant contient des paramètres valides :  
>   
>  `-MyParameter1 MyValue1 -MyParameter2 MyValue2`  
>   
>  L'exemple suivant contient des paramètres non valides. Les deux premiers éléments sont des paramètres de ligne de commande Windows PowerShell (**-NoLogo** et **-ExecutionPolicy Unrestricted**). Le script n’utilise pas ces paramètres.  
>   
>  `-NoLogo -ExecutionPolicy Unrestricted -File MyScript.ps1 -MyParameter1 MyValue1 -MyParameter2 MyValue2`  

 **Stratégie d'exécution de PowerShell**  
 Détermine les scripts Windows PowerShell (le cas échéant) que vous autorisez à s’exécuter sur l’ordinateur. Choisissez l'une des stratégies d'exécution suivantes :  

-   **AllSigned** : exécuter seulement les scripts signés par un éditeur approuvé  

-   **Non défini** : ne pas définir de stratégie d’exécution  

-   **Bypass** : charger tous les fichiers de configuration et exécuter tous les scripts Si vous téléchargez un script non signé à partir d’Internet, Windows PowerShell ne demande pas d’autorisation avant d’exécuter le script.  

> [!IMPORTANT]  
>  PowerShell 1.0 ne prend pas en charge les stratégies d'exécution Non défini et Ignorer.  



##  <a name="child-task-sequence"></a> Exécuter une séquence de tâches

À compter de Configuration Manager version 1710, vous pouvez ajouter une nouvelle étape qui exécute une autre séquence de tâches. Cette étape crée une relation parent-enfant entre les séquences de tâches. Avec les séquences de tâches enfants, vous pouvez créer des séquences de tâches plus modulaires et réutilisables.

Quand vous ajoutez une séquence de tâches enfant à une séquence de tâches, considérez les éléments suivants :
 - Les séquences de tâches parent et enfant sont en fait combinées en une stratégie unique exécutée par le client.
 - L’environnement est global. Si la séquence de tâches parent définit une variable et que la séquence de tâches enfant change cette variable, elle conserve la dernière valeur. Si la séquence de tâches enfant crée une variable, celle-ci est disponible pour le reste de la séquence de tâches parent.
 - Les messages d’état sont envoyés normalement pour une opération de séquence de tâches unique.
 - Les séquences de tâches inscrivent des entrées dans le fichier smsts.log et le nouveau journal écritures indique clairement lorsqu’une séquence de tâches enfant démarre.

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Exécuter une séquence de tâches** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

**Sélectionnez la séquence de tâches à exécuter**  
 Cliquez sur **Parcourir** pour sélectionner la séquence de tâches enfant. La boîte de dialogue **Sélectionner une séquence de tâches** n’affiche pas la séquence de tâches parent.



##  <a name="BKMK_SetDynamicVariables"></a> Définir des variables dynamiques  
 Utilisez cette étape pour effectuer les actions suivantes :  

1.  Recueillir des informations à partir de l'ordinateur et de l'environnement où il réside, puis définir des variables de séquence de tâches spécifiées avec les informations.  

2.  Évaluer les règles définies et définir des variables de séquence de tâches en fonction des variables et des valeurs configurées pour les règles avec la valeur true.  

La séquence de tâches définit automatiquement les variables de séquence de tâches en lecture seule suivantes :  
 -   &#95;SMSTSMake  
 -   &#95;SMSTSModel  
 -   &#95;SMSTSMacAddresses  
 -   &#95;SMSTSIPAddresses  
 -   &#95;SMSTSSerialNumber  
 -   &#95;SMSTSAssetTag  
 -   &#95;SMSTSUUID  

Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Pour plus d’informations sur les variables de séquence de tâches, consultez [Variables d’action de séquence de tâches](task-sequence-action-variables.md).  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Définir des variables dynamiques** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

**Règles dynamiques et variables**  
 Pour définir une variable dynamique à utiliser dans la séquence de tâches, ajoutez une règle. Ensuite, définissez une valeur pour chaque variable spécifiée dans la règle. Ajoutez aussi une ou plusieurs variables sans ajouter une règle. Quand vous ajoutez une règle, choisissez parmi les catégories suivantes :  

 -   **Ordinateur** : évalue des valeurs d’étiquette d’inventaire matériel, d’UUID, de numéro de série ou d’adresse MAC. Définissez plusieurs valeurs selon vos besoins. Si une des valeurs est true, la règle est évaluée comme étant vraie. Par exemple, la règle suivante est évaluée comme étant vraie si le numéro de série du périphérique est 5892087 et si l’adresse MAC est 22-A4-5A-13-78-26.  

     `IF Serial Number = 5892087 OR MAC address = 26-78-13-5A-A4-22 THEN`  

-   **Emplacement** : évalue les valeurs de la passerelle réseau par défaut  

-   **Marque et modèle** : évalue les valeurs de la marque et du modèle d’un ordinateur La marque et le modèle doivent tous deux être évalués comme vrais pour que la règle soit évaluée comme vraie.   

    <!-- for future edits: an escape code must be used for the bolded asterisk character, but may be removed somewhere along the way. Instead of five asterisk, should be bold tags with &#42; in-between -->

    À compter de Configuration Manager version 1610, vous pouvez spécifier un astérisque (**&#42;**) et un point d’interrogation (**?**) comme caractères génériques, où **&#42;** correspond à plusieurs caractères et où **?** correspond à un caractère unique. Par exemple, la chaîne « DELL*900? » correspond à DELL-ABC-9001 et DELL9009. 

    Spécifiez un astérisque (**&#42;**) et un point d’interrogation (**?**) comme caractères génériques, où **&#42;** correspond à plusieurs caractères et où **?** correspond à un caractère unique. Par exemple, la chaîne « DELL*900? » correspond à DELL-ABC-9001 et DELL9009.

-   **Variable de séquence de tâches** : ajoute une variable de séquence de tâches, une condition et une valeur à évaluer. La règle est évaluée comme vraie quand la valeur définie pour la variable remplit la condition spécifiée.  

    Spécifiez une ou plusieurs variables à définir pour une règle évaluée comme étant vraie, ou définissez des variables sans utiliser de règle. Sélectionnez une variable existante ou créez une variable personnalisée.  

     -   **Variables de séquence de tâches existantes** : sélectionnez une ou plusieurs variables dans une liste des variables de séquence de tâches existantes. Les variables tableau ne peuvent pas être sélectionnées.  

     -   **Variables de séquence de tâches personnalisées** : définissez une variable de séquence de tâches personnalisée. Vous pouvez également spécifier une variable de séquence de tâches existante. Ce paramètre utile pour spécifier un tableau de variables existantes, comme OSDAdapter, car les tableaux de variables ne figurent pas dans la liste des variables de séquence de tâches existantes.  

Après avoir sélectionné les variables pour une règle, vous devez fournir une valeur pour chaque variable. Lorsque la règle est évaluée comme vraie, la variable est définie à la valeur spécifiée. Pour chaque variable, vous pouvez sélectionner **Valeur secrète** pour masquer la valeur de la variable. Par défaut, certaines variables existantes (telles que la variable de séquence de tâches OSDCaptureAccountPassword) masquent les valeurs.  

> [!IMPORTANT]  
>  Configuration Manager supprime les valeurs des variables marquées comme **Valeur secrète** quand vous importez une séquence de tâches avec l’étape **Définir des variables dynamiques**. Entrez à nouveau la valeur de la variable dynamique après avoir importé la séquence de tâches.  



##  <a name="BKMK_SetTaskSequenceVariable"></a> Définir la variable de séquence de tâches  
Utilisez cette étape pour définir la valeur d’une variable qui est utilisée avec la séquence de tâches.  

Cette étape peut être exécutée dans un système d'exploitation standard ou Windows PE. Les variables de séquence de tâches sont lues par les actions et en déterminent le comportement. Pour plus d’informations sur des variables d’action de séquence de tâches spécifiques, consultez [Variables d’action de séquence de tâches](task-sequence-action-variables.md). Pour plus d’informations sur des variables intégrées de séquence de tâches spécifiques, consultez [Variables intégrées de séquence de tâches](/sccm/osd/understand/task-sequence-built-in-variables).

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Général**, puis sélectionnez **Définir la variable de séquence de tâches** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Variable de séquence de tâches**  
 Spécifiez le nom d’une variable intégrée ou d’action de séquence de tâches, ou spécifiez le nom de votre propre variable définie par l’utilisateur.  

 **Valeur**  
 La séquence de tâches définit la variable sur cette valeur. Définissez cette variable de séquence de tâches sur la valeur d’une autre variable de séquence de tâches avec la syntaxe %nom_variable%.  



##  <a name="BKMK_SetupWindowsandConfigMgr"></a> Configurer Windows et ConfigMgr  
 Utilisez cette étape pour effectuer la transition de Windows PE vers le nouveau système d’exploitation. Cette étape de séquence de tâches est obligatoire dans tout déploiement de système d'exploitation, elle installe le client Configuration Manager dans le nouveau système d’exploitation et prépare la poursuite de l’exécution de la séquence de tâches dans le nouveau système d’exploitation.  

 Cette étape est exécutée uniquement sous Windows PE. Elle ne s'exécute pas dans un système d'exploitation standard. Pour plus d’informations sur les variables de séquence de tâches de cette action de séquence de tâches, consultez [Variables d’action de séquence de tâches Configurer Windows et ConfigMgr](task-sequence-action-variables.md#BKMK_SetupWindows).  

 Cette étape remplace les variables de répertoire de sysprep.inf ou unattend.xml, comme %WINDIR% et %ProgramFiles%, par le répertoire d’installation de Windows°PE, X:\Windows. La séquence de tâches ignore les variables spécifiées avec ces variables d’environnement.  

 Utilisez cette étape de séquence de tâches pour effectuer les actions suivantes :  

1.  Préliminaires : Windows PE  

    1.  Remplacez les variables de séquence de tâches dans le fichier unattend.xml.  

    2.  Téléchargez le package qui contient le client Configuration Manager. Ajoutez le package à l’image déployée.  

2.  Configuration de Windows  

    1.  Installation à base d’image  

        1.  Désactivez le client Configuration Manager dans l’image, s’il existe. En d’autres termes, désactivez le démarrage automatique pour le service client Configuration Manager.  

        2.  Mettez à jour le Registre dans l’image déployée pour démarrer le système d’exploitation déployé avec la même lettre de lecteur que celle de l’ordinateur de référence.  

        3.  Redémarrez sur le système d’exploitation déployé.  

        4.  La mini-installation de Windows s’exécute en utilisant le fichier de réponses sysprep.inf ou unattend.xml spécifié précédemment et dont toutes les interactions avec l’utilisateur final sont supprimées. Si vous utilisez l’étape **Appliquer les paramètres réseau** pour la jonction à un domaine, ces informations se trouvent dans le fichier de réponses. La mini-installation de Windows joint l’ordinateur au domaine.  

    2.  Installation avec Setup.exe.  Exécute le fichier Setup.exe qui suit le processus d’installation de Windows classique :  

        1.  Copiez le package de mise à niveau du système d’exploitation spécifié dans l’étape **Appliquer le système d’exploitation** sur le disque dur.  

        2.  Redémarrez sur le système d’exploitation nouvellement déployé.  

        3.  La mini-installation de Windows s’exécute en utilisant le fichier de réponses sysprep.inf ou unattend.xml spécifié précédemment et dont tous les paramètres d’interface utilisateur sont supprimés. Si vous utilisez l’étape **Appliquer les paramètres réseau** pour la jonction à un domaine, ces informations se trouvent dans le fichier de réponses. La mini-installation de Windows joint l’ordinateur au domaine.  

3.  Configurer le client Configuration Manager  

    1.  Une fois la mini-installation de Windows terminée, la séquence de tâches reprend à l’aide de setupcomplete.cmd.  

    2.  Activez ou désactivez le compte d’administrateur local en fonction de l’option sélectionnée dans l’étape **Appliquer les paramètres Windows** .  

    3.  Installez le client Configuration Manager en utilisant le package précédemment téléchargé et les propriétés d’installation spécifiées dans cette étape. Le client est installé en « mode d’approvisionnement » afin de l’empêcher de traiter les demandes de nouvelles stratégies avant la fin de la séquence de tâches.  

    4.  Attendez que le client soit entièrement opérationnel.  

4.  La séquence de tâches continue en exécutant l’étape suivante.  

<!-- Engineering confirmed that the task sequence does nothing with respect to group policy processing.
> [!NOTE]  
>  The **Setup Windows and ConfigMgr** task sequence action is responsible for running Group Policy on the newly installed computer. The Group Policy is applied after the task sequence is finished.  
-->

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis sélectionnez **Configurer Windows et ConfigMgr** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
 Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

 **Package client**  
 Cliquez sur **Parcourir** et sélectionnez le package d’installation du client Configuration Manager que vous voulez utiliser avec cette étape.  

 **Utiliser le package client de préproduction quand il est disponible**  
 Si un package client de préproduction est disponible et que l’ordinateur est membre du regroupement pilote, la séquence de tâches utilise ce package à la place du package client de production. Le client de préproduction est une version plus récente à tester dans l’environnement de production. Cliquez sur **Parcourir** et sélectionnez le package d’installation du client de préproduction que vous voulez utiliser avec cette étape.  

 **Propriétés d’installation**  
 L'attribution de site et la configuration par défaut sont automatiquement spécifiées par l'action de la séquence de tâches. Ce champ permet de spécifier les propriétés d'installation supplémentaires à utiliser lorsque vous installez le client. Pour entrer plusieurs propriétés d'installation, séparez-les par un espace.  

 Vous pouvez spécifier des options de ligne de commande à utiliser lors de l'installation du client. Par exemple, vous pouvez entrer **/skipprereq: silverlight.exe** pour informer CCMSetup.exe de ne pas installer le composant requis Microsoft Silverlight. Pour plus d’informations sur les options de ligne de commande disponibles pour CCMSetup.exe, consultez [À propos des propriétés d’installation du client](../../core/clients/deploy/about-client-installation-properties.md).  

### <a name="options"></a>Options
> [!NOTE]
> N’activez pas **Continuer en cas d’erreur** sous l’onglet **Options**. Si une erreur se produit au cours de cette étape, la séquence de tâches échoue selon que vous activez ou non ce paramètre.



##  <a name="BKMK_UpgradeOS"></a> Mettre à niveau le système d’exploitation  
 > [!TIP]  
 > À compter de Windows 10 version 1709, le média inclut plusieurs éditions. Quand vous configurez une séquence de tâches pour l’utilisation d’un package de mise à niveau du système d’exploitation ou d’une image de système d’exploitation, veillez à sélectionner une [édition prise en charge](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).

 Utilisez cette étape pour mettre à niveau une version antérieure de Windows vers une version plus récente de Windows 10.  

 Cette étape de séquence de tâches s'exécute uniquement dans un système d'exploitation standard. Elle ne s'exécute pas dans Windows PE.  

Dans l’Éditeur de séquence de tâches, cliquez sur **Ajouter**, sélectionnez **Images**, puis sélectionnez **Mettre à niveau le système d’exploitation** pour ajouter cette étape. 

### <a name="properties"></a>Propriétés  
Sous l’onglet **Propriétés** de cette étape, configurez les paramètres décrits dans cette section.  

**Package de mise à niveau**  
 Sélectionnez cette option pour spécifier le package de mise à niveau de système d’exploitation Windows 10 à utiliser pour la mise à niveau.  

**Chemin source**  
 Spécifie un chemin local ou réseau au média de Windows 10 utilisé par l’installation de Windows. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows **/InstallFrom**. Vous pouvez également spécifier une variable, comme %mycontentpath% ou %DPC01%. Quand vous utilisez une variable pour le chemin source, elle doit être spécifiée plus tôt dans la séquence de tâches. Par exemple, si vous utilisez l’étape [Télécharger le contenu du package](#BKMK_DownloadPackageContent) dans la séquence de tâches, vous pouvez spécifier une variable pour l’emplacement du package de mise à niveau du système d’exploitation. Ensuite, vous pouvez utiliser cette variable pour le chemin source de cette étape.  

**Édition**  
 Spécifiez l’édition au sein du support du système d’exploitation à utiliser pour la mise à niveau.  

**Clé du produit**  
 Spécifier la clé de produit à appliquer au processus de mise à niveau  

**Fournir le contenu du pilote suivant à l’installation de Windows pendant la mise à niveau**  
 Ajouter des pilotes à l’ordinateur de destination lors du processus de mise à niveau. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows **/InstallDriver**. Les pilotes doivent être compatibles avec Windows 10. Spécifiez l'une des options suivantes :  

-   **Package de pilotes** : cliquez sur **Parcourir** et sélectionnez un package de pilotes existant dans la liste.  

-   **Contenu intermédiaire** : sélectionnez cette option pour spécifier l’emplacement du package de pilotes. Vous pouvez spécifier un dossier local, un chemin réseau ou une variable de séquence de tâches. Quand vous utilisez une variable pour le chemin source, elle doit être spécifiée plus tôt dans la séquence de tâches. Par exemple, en utilisant l’étape [Télécharger le contenu du package](task-sequence-steps.md#BKMK_DownloadPackageContent).  

**Délai d’expiration (minutes)**  
 Spécifie le nombre de minutes avant que Configuration Manager considère que cette étape a échoué. Cette option est utile si l’installation de Windows arrête le traitement mais ne se termine pas.  

**Effectuer une analyse de compatibilité d’installation de Windows sans démarrer la mise à niveau**  
 Effectuer l’analyse de compatibilité de l’installation de Windows sans démarrer le processus de mise à niveau. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows **/Compat ScanOnly**. Vous devez déployer toute la source de d’installation quand vous utilisez cette option. Le programme d’installation renvoie un code de sortie suite à l’analyse. Le tableau suivant indique certains des codes de sortie les plus courants.  

|Code de sortie|Détails|  
|-|-|  
|MOSETUP_E_COMPAT_SCANONLY (0xC1900210)|Aucun problème de compatibilité (« réussite »).|  
|MOSETUP_E_COMPAT_INSTALLREQ_BLOCK (0XC1900208)|Problèmes de compatibilité pouvant donner lieu à une action.|  
|MOSETUP_E_COMPAT_MIGCHOICE_BLOCK (0xC1900204)|Le choix de migration sélectionné n’est pas disponible. Par exemple, une mise à niveau depuis Entreprise vers Professionnel.|  
|MOSETUP_E_COMPAT_SYSREQ_BLOCK (0xC1900200)|Non éligible pour Windows 10.|  
|MOSETUP_E_COMPAT_INSTALLDISKSPACE_BLOCK (0XC190020E)|Espace disque disponible insuffisant.|  

Pour plus d’informations sur ce paramètre, consultez [Options de ligne de commande du programme d’installation de Windows](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).  

**Ignorer les messages de compatibilité révocables**  
 Spécifie que le programme d’installation a terminé l’installation, en ignorant tous les messages de compatibilité révocables. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows **/Compat IgnoreWarning**.  

**Mettre à jour dynamiquement l’installation de Windows avec Windows Update**  
 Permet au programme d’installation d’effectuer des opérations de mise à jour dynamiques, comme rechercher, télécharger et installer des mises à jour. Ce paramètre correspond à l’option de ligne de commande de l’installation de Windows **/DynamicUpdate**. Ce paramètre n’est pas compatible avec les mises à jour logicielles de Configuration Manager. Activez cette option quand vous gérez des mises à jour avec WSUS (Windows Server Update Services) autonome ou avec Windows Update pour Entreprise.  

**Remplacer la stratégie et utiliser Microsoft Update par défaut** : remplace temporairement la stratégie locale en temps réel, pour exécuter des opérations de mise à jour dynamique et permettre à l’ordinateur d’obtenir des mises à jour par le biais de Windows Update.
