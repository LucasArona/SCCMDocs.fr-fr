---
title: Créer des applications
titleSuffix: Configuration Manager
description: Créez des applications avec des types de déploiement, des méthodes de détection et des spécifications pour installer les logiciels.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 947dfac82db43e5cb21d8304d31be23219bb83aa
ms.sourcegitcommit: 6e42785c8c26e3c75bf59d3df7802194551f58e1
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52456649"
---
# <a name="create-applications-in-configuration-manager"></a>Créer des applications dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Une application Configuration Manager définit les métadonnées concernant une application. Une application a un ou plusieurs types de déploiement. Ces types de déploiement incluent les fichiers d’installation et les informations nécessaires à l’installation du logiciel sur des appareils. Un type de déploiement comprend également des règles, telles que les méthodes de détection et les spécifications. Ces règles spécifient quand et comment le client installe les logiciels.  

Créez des applications en employant les méthodes suivantes :  

-   Créer automatiquement une application et des types de déploiement en lisant les fichiers d’installation de l’application :  
    - [Créer une application](#bkmk_create) et [détecter automatiquement](#bkmk_auto-app) les informations de l’application
    - [Créer un type de déploiement](#bkmk_create-dt) et [identifier automatiquement](#bkmk_auto-dt) les informations du type de déploiement

-   Créer manuellement une application, puis ajouter des types de déploiement :  
    - [Créer une application](#bkmk_create) et [spécifier manuellement](#bkmk_manual-app) les informations de l’application
    - [Créer un type de déploiement](#bkmk_create-dt) et [spécifier manuellement](#bkmk_manual-dt) les informations du type de déploiement

-   [Importer une application](#bkmk_import) à partir d’un fichier  

Cet article inclut également les informations suivantes pour configurer un type de déploiement :  
- [Contenu](#bkmk_dt-content)
- [Méthode de détection](#bkmk_dt-detect)
- [Expérience utilisateur](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Codes de retour](#bkmk_dt-return)
- [Dépendances](#bkmk_dt-depend)



## <a name="bkmk_create"></a> Créer une application  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.  

2.  Sous l’onglet **Accueil** du ruban, dans le groupe **Créer**, cliquez sur **Créer une application**.  

Ensuite, détectez automatiquement ou définissez manuellement les informations de l’application :  

-   [Détectez automatiquement](#bkmk_auto-app) les informations d’application pour créer une application de base avec un seul type de déploiement, par exemple, un fichier Windows Installer qui n’a pas de dépendances ou de spécifications. Une fois que vous avez créé une application à l’aide de cette procédure, modifiez-la en fonction de vos besoins. Vous pouvez ajouter ou changer des types de déploiement et ajouter des méthodes de détection, des dépendances ou des spécifications.  

-   [Spécifiez manuellement](#bkmk_manual-app) les informations sur l’application pour créer des applications plus complexes. Définissez plusieurs types de déploiement, dépendances, méthodes de détection ou spécifications.  


### <a name="bkmk_auto-app"></a> Détecter automatiquement les informations sur l’application  

1.  Dans la page **Général,** de l’Assistant Création d’une application, sélectionnez **Détecter automatiquement les informations de cette application à partir des fichiers d’installation**.  

2.  Dans la liste déroulante **Type** , choisissez le type de fichier d'installation d'application que vous souhaitez utiliser pour détecter les informations sur l'application. Pour plus d’informations sur les types d’installation disponibles, consultez [Types de déploiement pris en charge par Configuration Manager](/sccm/apps/deploy-use/create-applications#bkmk_deploy-types).  

3.  Dans la zone **Emplacement**, spécifiez le fichier d’installation de l’application que vous souhaitez utiliser pour détecter les informations sur l’application. Cet emplacement est un chemin réseau (`\\server\share\filename`) ou un lien vers le Store. Vous devez avoir accès au chemin réseau et aux sous-dossiers où figure le contenu de l’application.  

    > [!IMPORTANT]  
    >  Quand vous sélectionnez **Windows Installer (fichier \*.msi)** comme type d’application, le site importe tous les fichiers situés dans le dossier spécifié. Il envoie ensuite ces fichiers aux points de distribution. Vérifiez que le dossier spécifié contient uniquement les fichiers nécessaires à l’installation de l’application. Microsoft teste Configuration Manager pour prendre en charge jusqu’à 20 000 fichiers dans le package d’application. Si votre application contient plus de fichiers, pensez à créer plusieurs applications avec moins de fichiers.    

4.  Dans la page **Importer des informations** de l’Assistant Création d’une application, consultez les informations, puis cliquez sur **Suivant**. Si nécessaire, cliquez sur **Précédent** pour revenir en arrière et corriger les erreurs éventuelles.  

5.  Dans la page **Informations générales** de l’Assistant Création d’une application, spécifiez les informations suivantes :  

    > [!NOTE]  
    >  Si Configuration Manager détecte automatiquement ces informations dans les fichiers d’installation de l’application, elles y figurent déjà. En outre, les options affichées peuvent être différentes en fonction du type d'application que vous créez.  

    -   Informations générales sur l’application, telles que le **Nom**, les **Commentaires de l’administrateur**, **l’Éditeur** et la **Version du logiciel**. Pour vous aider à trouver l’application dans la console Configuration Manager, spécifiez une **Référence facultative** ou sélectionnez des **Catégories administratives**.  

    -   **Programme d'installation**: spécifiez le programme d'installation et les éventuelles propriétés obligatoires, nécessaires pour installer le type de déploiement de l'application.  

        > [!TIP]  
        >  Si le programme d’installation n’est pas indiqué, choisissez **Parcourir** et accédez à l’emplacement du programme d’installation.  

    -   **Comportement à l’installation** : sélectionnez une des trois options pour définir la façon dont Configuration Manager doit installer ce type de déploiement. Pour plus d’informations sur ces options, consultez [Expérience utilisateur](#bkmk_dt-ux).  

    -   **Utiliser une connexion VPN automatique (si elle est configurée)** : si vous avez déployé un profil VPN sur l’appareil sur lequel l’utilisateur lance l’application, connectez le VPN au démarrage de l’application. Cette option ne concerne que Windows 8.1 et Windows Phone 8.1. Sur les appareils Windows Phone 8.1, si vous y déployez plusieurs profils VPN, les connexions VPN automatiques ne sont pas prises en charge. Pour plus d’informations, consultez [Profils VPN](/sccm/protect/deploy-use/vpn-profiles).  

    - **Provisionner cette application pour tous les utilisateurs de cet appareil**<!--1358310--> : depuis la version 1806, provisionnez une application avec un package d’application Windows pour tous les utilisateurs d’un appareil. Pour plus d’informations, consultez [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications#bkmk_provision).  

       > [!Tip]  
       > Si vous modifiez une application existante, ce paramètre se trouve sous l’onglet **Expérience utilisateur** des propriétés du type de déploiement du package de l’application Windows.  

6.  Choisissez **Suivant**, examinez les informations sur l’application figurant dans la page **Résumé**, puis suivez toutes les étapes de l’Assistant Création d’une application.  

La nouvelle application s’affiche désormais dans le nœud **Applications** de la console Configuration Manager. Vous avez terminé la création d’une application. 

Pour ajouter d’autres types de déploiement ou configurer d’autres paramètres, consultez [Créer des types de déploiement pour l’application](#bkmk_create-dt).  


### <a name="bkmk_manual-app"></a> Spécifier manuellement les informations de l’application  

1.  Dans la page **Général** de l’Assistant Création d’une application, sélectionnez **Spécifier manuellement les informations de l’application**, puis choisissez **Suivant**.  

2.  Spécifiez les **Informations générales** sur l’application :  

    - Le **Nom** de l’application est obligatoire et doit comprendre moins de 256 caractères.  

    - Les **Commentaires de l’administrateur**, **l’Éditeur**, et la **Version du logiciel** sont des métadonnées supplémentaires pour mieux décrire l’application.  

    - Pour vous aider à trouver l’application dans la console Configuration Manager, spécifiez une **Référence facultative** ou sélectionnez des **Catégories administratives**.  

    - **Date de publication**  

    - Sélectionnez les utilisateurs ou groupes qui sont responsables de cette application en tant que **Propriétaires** et **Contacts du support**. Par défaut, ces valeurs sont définies sur votre nom d’utilisateur.  

3.  Dans la page **Catalogue d’applications** de l’Assistant Création d’une application, spécifiez les informations suivantes :  

    -   **Langue sélectionnée** : dans la liste déroulante, sélectionnez la version linguistique de l’application que vous souhaitez installer. Choisissez **Ajouter/Supprimer** pour configurer d’autres langues pour cette application.  

    -   **Nom de l’application localisée** : spécifiez le nom de l’application dans la langue sélectionnée.  

        > [!IMPORTANT]  
        > Un nom d’application localisée est obligatoire pour chaque version de langue que vous configurez.  

    -   **Catégories d’utilisateurs** : choisissez **Modifier** pour spécifier les catégories de l’application dans la langue sélectionnée. Les utilisateurs du Centre logiciel utilisent ces catégories pour filtrer et trier les applications disponibles.  

    -   **Documentation utilisateur** : spécifier l’emplacement d’un fichier à partir duquel les utilisateurs du Centre logiciel peuvent obtenir des informations supplémentaires sur cette application. Cet emplacement est une adresse de site web ou un chemin réseau et un nom de fichier. Vérifiez que les utilisateurs ont accès à cet emplacement.  

    -   **Texte de lien** : spécifiez le texte qui s’affiche à la place de l’URL de l’application.  

    -   **URL de la déclaration de confidentialité** : spécifiez une adresse de site web vers la déclaration de confidentialité de l’application.  

    -   **Description localisée** : entrez une description pour cette application dans la langue sélectionnée.  

    -   **Mots clés** : entrez une liste de mots clés dans la langue sélectionnée. Ces mots clés aident les utilisateurs du Centre logiciel à rechercher l’application.  

    -   **Icône** : cliquez sur **Parcourir** pour sélectionner une icône pour cette application. Si vous ne spécifiez pas d’icône, Configuration Manager utilise une icône par défaut. Les dimensions maximales des icônes sont 512 x 512 pixels.  

    -   **Afficher en tant qu’application proposée et la mettre en exergue sur le portail de l’entreprise** : cette option met en avant l’application sur le portail de l’entreprise sur les appareils mobiles.  

4.  Dans la page **Types de déploiement** de l’Assistant Création d’une application, choisissez **Ajouter** pour créer un type de déploiement. Pour plus d’informations, consultez [Créer des types de déploiement pour l’application](#bkmk_create-dt).  

5.  Choisissez **Suivant**, examinez les informations sur l’application figurant dans la page **Résumé**, puis suivez toutes les étapes de l’Assistant Création d’une application.  

La nouvelle application s’affiche désormais dans le nœud **Applications** de la console Configuration Manager.  



## <a name="bkmk_create-dt"></a> Créer des types de déploiement pour l’application  

Si vous [détectez automatiquement les informations de l’application](#bkmk_auto-app), vous n’aurez peut-être pas besoin de finaliser certaines étapes de cette section.  

> [!Note]  
> Quand vous affichez les propriétés d’un type de déploiement existant, les sections suivantes correspondent aux onglets de la fenêtre des propriétés du type de déploiement :  
> - [Contenu](#bkmk_dt-content)
> - [Méthode de détection](#bkmk_dt-detect)
> - [Expérience utilisateur](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Codes de retour](#bkmk_dt-return)
> - [Dépendances](#bkmk_dt-depend)
>  
> Pour plus d’informations sur l’onglet **Comportement à l’installation** relatif aux propriétés d’un type de déploiement, consultez [Vérifier si des fichiers exécutables sont en cours d’exécution](/sccm/apps/deploy-use/deploy-applications#bkmk_exe-check).  


### <a name="start-the-create-deployment-type-wizard"></a>Démarrer l’Assistant Création d’un type de déploiement  

Vous pouvez démarrer l’Assistant Création d’un type de déploiement de trois façons :

- **Dans le nœud Applications** : dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**. Sélectionnez une application, puis cliquez sur **Créer un type de déploiement** dans le ruban.  

- **Pendant la création d’une application** : quand vous [spécifiez manuellement les informations de l’application](#bkmk_manual-app) dans l’Assistant Création d’une application, cliquez sur **Ajouter** dans la page Types de déploiement.  

- **À partir des propriétés de l’application** : sélectionnez une application existante dans le nœud **Applications**, puis cliquez sur **Propriétés**. Basculez vers l’onglet **Types de déploiement**, puis cliquez sur **Ajouter**.

Ensuite, utilisez l’une des procédures suivantes pour [identifier automatiquement](#bkmk_auto-dt) ou [spécifier manuellement](#bkmk_manual-dt) les informations relatives au type de déploiement.  


### <a name="bkmk_auto-dt"></a> Identifier automatiquement les informations relatives au type de déploiement  

1.  Dans la page **Général** de l’Assistant Création d’un type de déploiement :  

    1. Sélectionnez le **Type** du fichier d’installation d’application à utiliser pour détecter les informations sur le type de déploiement.  

    2. Sélectionnez **Identifier automatiquement les informations sur ce type de déploiement à partir des fichiers d’installation**.  

    3.  Dans la zone **Emplacement**, spécifiez le fichier d’installation d’application à utiliser pour détecter les informations sur le type de déploiement. Cet emplacement est un chemin réseau (`\\server\share\filename`) ou un lien vers le Store. Vous devez avoir accès au chemin réseau et aux sous-dossiers où figure le contenu de l’application.  

2.  Dans la page **Importer des informations** de l’Assistant Création d’un type de déploiement, consultez les informations, puis cliquez sur **Suivant**. Si nécessaire, cliquez sur **Précédent** pour revenir en arrière et corriger les erreurs éventuelles.  

3.  Dans la page **Informations générales** de l’Assistant Création d’un type de déploiement, spécifiez les informations suivantes :  

    > [!NOTE]  
    >  Certaines informations relatives au type de déploiement peuvent déjà être présentes si elles ont été lues à partir des fichiers d'installation de l'application. De plus, les options affichées peuvent différer selon le type de déploiement que vous créez.  

    -   **Informations générales** sur le type de déploiement :      
        - **Nom**, obligatoire  

        - **Commentaires de l’administrateur**, pour mieux le décrire  

        - **Langues** disponibles pour celui-ci   

    -   **Programme d'installation**: spécifiez le programme d'installation et les éventuelles propriétés nécessaires pour installer le type de déploiement.  

    -   **Comportement à l’installation** : sélectionnez une des trois options pour définir la façon dont Configuration Manager doit installer ce type de déploiement. Pour plus d’informations sur ces options, consultez [Expérience utilisateur](#bkmk_dt-ux).  

    -   **Utiliser une connexion VPN automatique (si elle est configurée)** : si vous avez déployé un profil VPN sur l’appareil sur lequel l’utilisateur lance l’application, connectez le VPN au démarrage de l’application. Cette option ne concerne que Windows 8.1 et Windows Phone 8.1. Sur les appareils Windows Phone 8.1, si vous y déployez plusieurs profils VPN, les connexions VPN automatiques ne sont pas prises en charge. Pour plus d’informations, consultez [Profils VPN](/sccm/protect/deploy-use/vpn-profiles).  

4.  Choisissez **Suivant**, puis passez aux [options de contenu pour le type de déploiement](#bkmk_dt-content).  


### <a name="bkmk_manual-dt"></a> Spécifier manuellement les informations sur le type de déploiement  

1.  Dans la page **Général** de l’Assistant Création d’un type de déploiement, dans la liste déroulante **Type**, choisissez le type de fichier d’installation de l’application pour ce type de déploiement. 

2.  Sélectionnez **Spécifier manuellement les informations sur le type de déploiement**, puis cliquez sur **Suivant**.

3.  Dans la page **Informations générales** de l’Assistant Création d’un type de déploiement, attribuez un **Nom** au type de déploiement. Si vous le souhaitez, spécifiez les **Commentaires de l’administrateur** et sélectionnez les **Langues** pour ce type de déploiement, puis cliquez sur **Suivant**.  

4.  Passez aux [options de contenu pour le type de déploiement](#bkmk_dt-content).  

### <a name="bkmk_dt-content"></a> Options de **contenu** pour le type de déploiement  

Dans la page **Contenu**, spécifiez les informations suivantes :  

> [!Note]  
> Quand vous affichez les propriétés d’un type de déploiement existant, certaines de ces options apparaissent sous l’onglet **Contenu**, d’autres sous l’onglet **Programmes**.  

- **Emplacement du contenu** : spécifiez l’emplacement du contenu pour ce type de déploiement ou sélectionnez **Parcourir** pour choisir le dossier de contenu du type de déploiement.  

    > [!IMPORTANT]  
    >  Le compte du système de l’ordinateur du serveur de site doit disposer d’autorisations vers l’emplacement de contenu spécifié.  

    - **Conserver le contenu dans la mémoire cache du client** : le client Configuration Manager conserve indéfiniment dans son cache le contenu du type de déploiement. Le client conserve le contenu même si l’application est déjà installée. Cette option est utile avec certains déploiements, comme les logiciels basés sur Windows Installer. Windows Installer a besoin d’une copie locale du contenu source pour appliquer les mises à jour. Cette option réduit l’espace disponible dans le cache. Le choix de cette option peut entraîner l’échec d’un déploiement important plus tard si l’espace disponible dans le cache est insuffisant.  

- **Programme d’installation** : spécifiez le nom du programme d’installation et des paramètres d’installation requis.  

    - **Début de l’installation dans** : spécifiez éventuellement le dossier contenant le programme d’installation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client, ou un chemin vers le dossier du point de distribution contenant les fichiers d’installation.  

- **Programme de désinstallation** : spécifiez éventuellement le nom du programme de désinstallation et les paramètres obligatoires, le cas échéant.  

    - **Début de la désinstallation dans** : spécifiez éventuellement le dossier contenant le programme de désinstallation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client. Il peut aussi s’agir d’un chemin relatif sur un point de distribution du dossier contenant le package.  

- **Réparer le programme** : depuis la version 1810, pour les types de déploiement Windows Installer et Programme d’installation de script, spécifiez éventuellement le nom du programme de réparation et les paramètres obligatoires, le cas échéant.<!--1357866-->  

    - **Début de la réparation dans** : spécifiez éventuellement le dossier contenant le programme de réparation pour le type de déploiement. Ce dossier peut être un chemin absolu sur le client. Il peut aussi s’agir d’un chemin relatif sur un point de distribution du dossier contenant le package.  

- **Exécutez l'installation et désinstallez le programme en tant que processus 32 bits sur des clients 64 bits**: utilisez les emplacements de fichier et de Registre 32 bits sur des ordinateurs fonctionnant sous Windows pour exécuter le programme d'installation pour le type de déploiement.  


#### <a name="deployment-type-properties-content-options"></a>Options de **contenu** pour les propriétés du type de déploiement
Quand vous affichez les propriétés d’un type de déploiement, les options suivantes apparaissent uniquement sous l’onglet **Contenu** :

- **Paramètres du contenu de désinstallation** :  

    - **Identique au contenu d’installation** : si le contenu d’installation et le contenu de désinstallation sont identiques, sélectionnez cette option. Il s’agit de l’option par défaut.  

    - **Pas de contenu de désinstallation** : si votre application ne nécessite pas de contenu pour la désinstallation, sélectionnez cette option.  

    - **Différent du contenu d’installation** : si le contenu de désinstallation est différent du contenu d’installation, sélectionnez cette option.  

        - **Emplacement du contenu de désinstallation** : spécifiez le chemin réseau du contenu qui est utilisé pour désinstaller l’application.  

- **Autoriser les clients à utiliser des points de distribution du groupe de limites de site par défaut** : indiquez si les clients doivent télécharger et installer le logiciel à partir d’un point de distribution dans le groupe de limites de site par défaut quand le contenu n’est pas disponible à partir d’un point de distribution dans les groupes de limites actuels ou voisins.  

- **Options de déploiement** : indiquez si les clients doivent télécharger l’application quand ils utilisent un point de distribution à partir des groupes de limites de site par défaut ou d’un groupe voisin.  

- **Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau**: indiquez si vous souhaitez activer l’utilisation de BranchCache pour les téléchargements du contenu. Pour plus d’informations, consultez [BranchCache](/sccm/core/plan-design/hierarchy/fundamental-concepts-for-content-management#branchcache). Depuis la version 1802, BranchCache est toujours activé sur les clients. Ce paramètre est supprimé, car les clients utilisent BranchCache si le point de distribution le prend en charge.  


### <a name="bkmk_dt-detect"></a> Options de la **méthode de détection** du type de déploiement   

Cette procédure configure une méthode de détection qui indique la présence du type de déploiement. En d’autres termes, elle indique si l’application est installée sur l’appareil Windows. Utilisez une des deux méthodes suivantes pour créer une méthode de détection :  
- [Configurer des règles pour détecter la présence de ce type de déploiement](#bkmk_detect-rule)
- [Utiliser un script personnalisé pour détecter la présence de ce type de déploiement](#bkmk_detect-script)


#### <a name="bkmk_detect-rule"></a> Configurer des règles pour détecter la présence de ce type de déploiement

1.  Dans la page **Méthode de détection**, l’option **Configurer des règles pour détecter la présence de ce type de déploiement** est sélectionnée par défaut. Cliquez sur **Ajouter une clause**.  

2.  Dans la boîte de dialogue **Règle de détection**, cliquez sur la liste déroulante **Type de paramètre**. Sélectionnez une des méthodes suivantes pour détecter la présence du type de déploiement :  

    - **Système de fichiers** : détecte s’il existe un fichier ou un dossier spécifié sur un appareil. Cette détection indique que l’application est installée. Spécifiez les détails supplémentaires suivants :  

        - **Type** : indiquez s’il s’agit d’un fichier ou dossier.  

        - **Chemin d’accès** (obligatoire) : entrez ou recherchez le chemin local sur l’appareil qui inclut le fichier ou dossier. Par exemple, `C:\Program Files`. Vous ne pouvez pas spécifier un chemin réseau partagé. Si vous cliquez sur **Parcourir**, parcourez le système de fichiers local ou connectez-vous à un client représentatif à parcourir.  

        - **Nom de fichier ou de dossier** (obligatoire) : spécifiez le nom de fichier ou dossier à détecter dans le chemin ci-dessus. Si le client détecte ce fichier ou dossier sur l’appareil, il considère que l’application est installée sur ce dernier.  

        - **Ce fichier ou dossier est associé à une application 32 bits sur des systèmes 64 bits** : cette option est sélectionnée par défaut. Le client vérifie d’abord les emplacements de fichiers 32 bits pour le fichier ou dossier spécifié. Si le fichier ou dossier est introuvable, le client recherche dans les emplacements 64 bits.  

    - **Registre** : détermine si une clé ou une valeur de Registre spécifiée existe sur un appareil client. Cette détection indique que l’application est installée. Spécifiez les détails supplémentaires suivants :  

        - **Ruche** (obligatoire) : choisissez une ruche de Registre dans la liste déroulante. Par exemple, `HKEY_LOCAL_MACHINE`.  

        - **Clé** (obligatoire) : spécifiez la clé de Registre à parcourir dans la ruche ci-dessus. Par exemple, `SOFTWARE\Microsoft\Office`.  

        - **Valeur** (facultatif) : entrez une valeur spécifique à détecter dans la clé ci-dessus. Si vous souhaitez que le client détecte la valeur (Par défaut), activez l’option **Utiliser la valeur de clé de Registre (Par défaut) pour la détection**. Quand vous entrez une valeur ou que vous activez cette option, vous êtes invité à sélectionner un **Type de données**.  

        - **Cette clé de Registre est associée à une application 32 bits sur des systèmes 64 bits** : sélectionnez cette option pour vérifier d’abord si la clé de Registre spécifiée se trouve dans les emplacements de Registre 32 bits. Si la clé de Registre est introuvable, le client la recherche dans les emplacements 64 bits.  

    - **Windows Installer** : détermine si un fichier Windows Installer spécifié existe sur un appareil client. Cette détection indique que l’application est installée. Spécifiez le **Code de produit** MSI à détecter sur le client. Si vous cliquez sur **Parcourir**, sélectionnez le fichier MSI à partir duquel lire le code de produit. 

3.  En bas de la fenêtre Règle de détection, indiquez si l’élément doit exister ou satisfaire à une règle. Par exemple, si vous détectez un fichier, l’option suivante est sélectionnée par défaut : **Le paramètre du système de fichiers doit exister sur le système cible pour indiquer la présence de cette application**. Sélectionnez l’autre option pour créer une règle de détection basée sur les propriétés d’un fichier ou dossier. Ces propriétés incluent la Date de modification, la Date de création, la Version ou la Taille. Ces critères de règle diffèrent d’un type de paramètre à l’autre.  

4.  Cliquez sur **OK** pour fermer la boîte de dialogue **Règle de détection**.  

Quand vous créez plusieurs méthodes de détection pour un type de déploiement, créez une logique plus complexe en regroupant les clauses. 

Passez à la section suivante sur l’utilisation d’un script personnalisé comme méthode de détection. Ou passez directement aux options [Expérience utilisateur](#bkmk_dt-ux) pour le type de déploiement.


#### <a name="bkmk_detect-script"></a> Utiliser un script personnalisé pour vérifier la présence d’un type de déploiement  

1.  Dans la page **Méthode de détection**, cochez la case **Utiliser un script personnalisé pour détecter la présence de ce type de déploiement**. Ensuite, cliquez sur **Modifier**.  

2.  Dans la boîte de dialogue **Éditeur de script**, cliquez sur la liste déroulante **Type de script**. Sélectionnez un des langages de script suivants pour détecter le type de déploiement : PowerShell, VBScript ou JScript.  

3.  Dans la zone **Contenu du script**, entrez le script que vous souhaitez utiliser ou collez le contenu d’un script existant. Choisissez **Ouvrir** pour accéder à un script enregistré existant. Cliquez sur **Effacer** pour supprimer le texte du champ Contenu du script. Si nécessaire, activez l’option **Exécuter le script comme processus 32 bits sur des clients 64 bits**.  

    > [!NOTE]  
    >  La taille maximale d’un script est 32 Ko.  

4.  Cliquez sur **OK** pour enregistrer le script et fermer la boîte de dialogue **Script Editor**. Dans l’Assistant Création d’un type de déploiement, les champs **Type de script** et **Longueur du script** sont mis à jour avec des détails sur votre script.   


#### <a name="about-custom-script-detection-methods"></a>À propos des méthodes de détection de script personnalisé  

Configuration Manager vérifie les résultats du script. Il lit les valeurs écrites par le script dans le flux de sortie standard (STDOUT), le flux d’erreurs standard (STDERR) et le code de sortie. Si le script quitte avec une valeur non nulle, il échoue et l’état de la détection d’application est *Inconnu*. Si le code de sortie est égal à zéro et que STDOUT contient des données, l’état de la détection d’application est *installé*.

Utilisez les tableaux suivants pour vérifier si une application est installée à partir de la sortie d’un script :  

**Code de sortie nul :**  
|STDOUT|STDERR|Résultat du script|État de détection de l'application|
|---------|---------|---------|---------|
|Vide|Vide|Opération réussie|Non installé|
|Vide|N'est pas vide|Échec|Inconnu.|
|N'est pas vide|Vide|Opération réussie|Installé|
|N'est pas vide|N'est pas vide|Opération réussie|Installé|


**Code de sortie non nul :**  
|STDOUT|STDERR|Résultat du script|État de détection de l'application|
|---------|---------|---------|---------|
|Vide|Vide|Échec|Inconnu.|
|Vide|N'est pas vide|Échec|Inconnu.|
|N'est pas vide|Vide|Échec|Inconnu.|
|N'est pas vide|N'est pas vide|Échec|Inconnu.|


**Exemples VBScript**

Utilisez les exemples VBScript suivants pour écrire vos propres scripts de détection d’application :  

Exemple 1 : Le script retourne un code de sortie qui n’est pas égal à zéro. Ce code indique que le script n’a pas pu s’exécuter correctement. Dans ce cas, l'état de la détection d'application est inconnu.  
``` VBScript
WScript.Quit(1)
```

Exemple 2 : Le script retourne un code de sortie égal à zéro, mais la valeur de STDERR n’est pas vide. Ce résultat indique que le script n’a pas pu s’exécuter correctement. Dans ce cas, l'état de la détection d'application est inconnu.  
``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

Exemple 3 : Le script retourne un code de sortie égal à zéro, ce qui indique la réussite d’exécution. Toutefois, la valeur de STDOUT est vide, ce qui indique que l’application n’est pas installée.  
``` VBScript
WScript.Quit(0)
```

Exemple 4 : Le script retourne un code de sortie égal à zéro, ce qui indique la réussite d’exécution. La valeur de STDOUT n’est pas vide, ce qui indique que l’application est installée.  
``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

Exemple 5 : Le script retourne un code de sortie égal à zéro, ce qui indique la réussite d’exécution. Les valeurs de STDOUT et STDERR ne sont pas vides, ce qui indique que l’application est installée.  
``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```


### <a name="bkmk_dt-ux"></a> Options de **l’expérience utilisateur** pour le type de déploiement   

Ces paramètres indiquent comment le client installe l’application sur les appareils et ce que l’utilisateur voit.  

Sur la page **Expérience utilisateur** , spécifiez les informations suivantes :  

- **Comportement à l'installation**: sélectionnez l'une des options suivantes dans la liste déroulante :  

    - **Installer pour l’utilisateur** : le client n’installe l’application que pour l’utilisateur pour lequel vous la déployez.  

    - **Installer pour le système** : le client installe l’application une seule fois. Il est accessible à tous les utilisateurs.  

    - **Installer pour le système si la ressource est un périphérique ; sinon installer pour l’utilisateur** : si vous déployez l’application sur un appareil, le client l’installe pour tous les utilisateurs. Si vous déployez l’application pour un utilisateur, le client l’installe uniquement pour cet utilisateur.  

- **Condition d’ouverture de session** : sélectionnez une des options suivantes :  

    - **Uniquement quand un utilisateur a ouvert une session**  

    - **Qu’un utilisateur ait ouvert une session ou non**  

    - **Uniquement lorsqu’aucun utilisateur n’a de session ouverte**  

    > [!NOTE]  
    >  Par défaut, cette option est définie sur **Uniquement lorsqu’un utilisateur a ouvert une session**. Si vous sélectionnez **Installer pour l’utilisateur** dans la liste déroulante **Comportement à l’installation**, vous ne pouvez pas modifier cette option.  

- **Visibilité du programme d’installation** : spécifiez le mode d’exécution du type de déploiement sur les appareils clients. Sélectionnez l'une des options suivantes :  

    - **Agrandi**: le type de déploiement est exécuté de manière agrandie sur les appareils clients. Les utilisateurs voient toute l’activité de l’installation.  

    - **Normal**: le type de déploiement est exécuté en mode normal, en fonction des valeurs par défaut du système et du programme. Ce mode est la valeur par défaut.  

    - **Réduit**: le type de déploiement est exécuté de manière réduite sur les appareils clients. Les utilisateurs peuvent voir l'activité de l'installation dans la zone de notification ou dans la barre des tâches.  

    - **Masqué** : le type de déploiement s’exécute sous forme masquée sur les appareils clients. Les utilisateurs ne voient aucune activité d’installation.  

- **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme** : indique si un utilisateur peut interagir avec l’installation du type de déploiement pour configurer les options d’installation.  

    > [!NOTE]  
    >  Si vous sélectionner l’option **Installer pour l’utilisateur** dans la liste déroulante **Comportement à l’installation**, cette option est activée par défaut.  

    > [!IMPORTANT]  
    > Depuis la version 1802, quand vous sélectionnez le comportement **Installer pour le système**, ce paramètre est facultatif. Cette modification vise essentiellement à autoriser un utilisateur final à interagir avec l’installation au cours d’une séquence de tâches. Par exemple, pour exécuter un processus d’installation qui invite l’utilisateur final à choisir diverses options. Certains programmes d’installation d’application ne peuvent pas se passer d’invites utilisateur ou le processus d’installation exige des valeurs de configuration spécifiques que seul l’utilisateur connaît. <!--1356976-->  
    >  
    > Une installation dans un contexte système avec des utilisateurs autorisés à interagir avec l’installation ne constitue pas une configuration sécurisée. Pour plus d’informations, consultez [Sécurité et confidentialité pour la gestion d’applications](/sccm/apps/plan-design/security-and-privacy-for-application-management#bkmk_interact).  

- **Durée maximale d’exécution allouée (minutes)** : spécifiez la durée maximale en minutes pendant laquelle vous pensez que le type de déploiement est susceptible de s’exécuter sur l’ordinateur client. Spécifiez ce paramètre comme un nombre entier supérieur à zéro. La valeur par défaut est 120 minutes (deux heures).  

    Utilisez cette valeur pour les actions suivantes :  

    - Pour surveiller les résultats du type de déploiement.  

    - Pour vérifier si un type de déploiement est installé quand vous définissez des fenêtres de maintenance sur des appareils clients. Quand une fenêtre de maintenance est en place, un type de déploiement ne démarre que s’il reste suffisamment de temps dans la fenêtre de maintenance pour respecter le paramètre **Durée maximale d’exécution allouée**.  

    > [!IMPORTANT]  
    >  Un conflit peut se produire si la **durée maximale d'exécution allouée** est plus longue que celle de la fenêtre de maintenance planifiée. Si la durée maximale d’exécution définie par l’utilisateur est supérieure à la longueur des fenêtres de maintenance disponibles, ce type de déploiement ne s’exécute pas.  

- **Temps d’installation estimé (minutes)**  : indique la durée d’installation estimée du type de déploiement. Les utilisateurs voient cette durée dans le Centre logiciel.  


#### <a name="deployment-type-properties-user-experience-options"></a>Options de **l’expérience utilisateur** pour les propriétés du type de déploiement
Quand vous affichez les propriétés d’un type de déploiement, les options suivantes apparaissent uniquement sous l’onglet **Expérience utilisateur** :

Appliquez un comportement spécifique après l’installation. Sélectionnez l'une des options suivantes :  

- **Déterminer le comportement en fonction des codes de retour** : gère les redémarrages en fonction des codes configurés sous l’onglet [Codes de retour](#bkmk_dt-return). Le Centre logiciel affiche **Peut nécessiter un redémarrage**. Si un utilisateur s’est connecté pendant l’installation, il reçoit une invite en fonction de la configuration de l’expérience utilisateur du *déploiement*.  

- **Aucune action spécifique** : aucun redémarrage n’est nécessaire après l’installation. Le Centre logiciel signale qu’aucun redémarrage n’est nécessaire.  

- **Le programme d’installation logicielle va forcer un redémarrage du périphérique** : Configuration Manager ne contrôle pas ou ne lance pas de redémarrage, mais l’installation elle-même peut le faire sans avertissement. Utilisez ce paramètre pour empêcher que Configuration Manager signale l’échec de l’installation quand le programme d’installation lance un redémarrage. Le Centre logiciel affiche **Peut nécessiter un redémarrage**.  

- **Le client Configuration Manager va forcer un redémarrage obligatoire du périphérique** : Configuration Manager force un redémarrage de l’appareil après une installation réussie. Le Centre logiciel signale qu’un redémarrage est nécessaire. Si un utilisateur s’est connecté pendant l’installation, il reçoit une invite en fonction de la configuration de l’expérience utilisateur du *déploiement*.  


### <a name="bkmk_dt-require"></a> **Spécifications** pour le type de déploiement

Configuration Manager vérifie ces spécifications sur les appareils avant d’installer le type de déploiement. Utilisez les spécifications pour affiner et contrôler les appareils ou utilisateurs qui reçoivent cette application. Par exemple, si vous déployez l’application pour un regroupement d’utilisateurs, spécifiez ici les spécifications matérielles de l’application. 

1.  Dans la page **Spécifications**, cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Créer une spécification**.  

2.  Dans la liste déroulante **Catégorie**, sélectionnez une option pour indiquer si cette spécification concerne un **Appareil** ou un **utilisateur**.  

    Sélectionnez **Personnalisée** pour utiliser une condition globale créée précédemment. Quand vous sélectionnez **Personnalisé**, vous pouvez également choisir **Créer** pour créer une condition globale. Pour plus d’informations sur les conditions globales, consultez [Comment créer des conditions globales](/sccm/apps/deploy-use/create-global-conditions).  

    > [!IMPORTANT]  
    >  Si vous déployez l’application sur un regroupement d’appareils, le client ignore la spécification de la catégorie **Utilisateur** et la condition **Périphérique principal**.  

3.  Dans la liste déroulante **Condition**, sélectionnez la condition à utiliser pour déterminer si l’utilisateur ou l’appareil répond aux spécifications de l’installation. Le contenu de cette liste varie en fonction de la catégorie sélectionnée.  

4.  Dans la liste déroulante **Opérateur**, sélectionnez l’opérateur à utiliser. Cet opérateur compare la condition sélectionnée à la valeur spécifiée. Il évalue si l’utilisateur ou l’appareil respecte la spécification de l’installation. Les opérateurs disponibles varient en fonction de la condition sélectionnée.  

    > [!Note]  
    >  Les spécifications disponibles varient selon le type d’appareil utilisé par le type de déploiement.  

5.  Dans la zone **Valeur**, spécifiez les valeurs à utiliser pour la comparaison. Ces valeurs, ainsi que la condition et l’opérateur sélectionnés, évaluent si l’utilisateur ou l’appareil respecte les spécifications de l’installation. Les valeurs disponibles varient en fonction de la condition et de l’opérateur sélectionnés.  

6.  Choisissez **OK** pour enregistrer la spécification et fermer la boîte de dialogue **Créer une spécification**.  


### <a name="bkmk_dt-depend"></a> **Dépendances** pour le type de déploiement  

Les dépendances définissent un ou plusieurs types de déploiement d’une autre application que le client doit installer avant d’installer ce type de déploiement.   

> [!IMPORTANT]  
>  Dans certains cas, un type de déploiement est dépendant d’un type de déploiement qui a également des dépendances. Le nombre maximal de dépendances prises en charge dans la chaîne est de 5.  

1.  Dans la page **Dépendances**, cliquez sur **Ajouter**.  

2.  Dans la fenêtre Ajouter une dépendance, entrez le **nom du groupe de dépendances**. Ce nom fait référence à ce groupe de dépendances d’application.  

3.  Dans la fenêtre Ajouter une dépendance, cliquez sur **Ajouter**.  

4.  Dans la fenêtre **Spécifier l’application requise**, sélectionnez une application disponible et au moins un de ses types de déploiement à utiliser en tant que dépendance.  

    > [!TIP]  
    >  Cliquez sur **Afficher** pour afficher les propriétés de l’application ou du type de déploiement sélectionné.  

5.  Cliquez sur **OK** pour fermer la fenêtre **Spécifier l’application requise**.  

6.  Si vous souhaitez que le client installe automatiquement l’application dépendante, sélectionnez **installation automatique** en regard de la dépendance.  

    > [!NOTE]  
    >  Vous n’avez pas besoin de déployer une application dépendante pour que le client l’installe automatiquement.  

7.  Si vous ajoutez plusieurs dépendances, utilisez les boutons **Augmenter la priorité** et **Diminuer la priorité**. Ces actions changent l’ordre dans lequel le client évalue chaque dépendance.  

8.  Cliquez sur **OK** pour fermer la fenêtre **Ajouter une dépendance**.  


### <a name="bkmk_dt-return"></a> **Codes de retour** pour le type de déploiement

> [!Note]  
> Cette page ne se trouve pas dans l’Assistant Création d’un type de déploiement. Il s’agit uniquement d’un onglet sur les propriétés d’un type de déploiement existant.  

Spécifiez les codes de retour pour contrôler les comportements une fois que le type de déploiement se termine. Par exemple, signalez qu’un redémarrage est nécessaire, que l’installation est terminée ou personnalisez le texte affiché aux utilisateurs. 

1. Sous l’onglet **Codes de retour** de la fenêtre des propriétés du type de déploiement, cliquez sur **Ajouter**.  

2. Dans la fenêtre Ajouter un code de retour, spécifiez la **Valeur du code de retour** que vous attendez de ce type de déploiement. Cette valeur est un entier positif ou négatif compris entre `-2147483648` et `2147483647`.  

3. Sélectionnez un **Type de code** dans la liste déroulante. Ce paramètre définit comment Configuration Manager interprète le code de retour spécifié à partir de ce type de déploiement. Les types disponibles varient en fonction de la technologie de type de déploiement.   

    - **Réussite (pas de redémarrage)** : le type de déploiement s’est installé correctement et aucun redémarrage n’est nécessaire.  

    - **Échec (pas de redémarrage)** : l’installation du type de déploiement a échoué.  

    - **Redémarrage matériel** : le type de déploiement s’est installé correctement, mais l’appareil doit être redémarré. Rien d’autre ne peut être installé tant que l’appareil n’est pas redémarré.  

    - **Redémarrage logiciel** : le type de déploiement s’est installé correctement, mais l’appareil doit être redémarré. D’autres installations peuvent se produire avant le redémarrage de l’appareil.    

    - **Nouvelle tentative rapide** : une autre installation est déjà en cours sur l’appareil. Le client effectue une nouvelle tentative toutes les deux heures, pour un total de 10 fois.  

4. Si vous le souhaitez, entrez un **Nom** et une **Description** pour ce code de retour. Ce texte est affiché à l’utilisateur.  

5. Cliquez sur **OK** pour fermer la fenêtre Ajouter un code de retour.  


#### <a name="example-non-zero-success"></a>Exemple : réussite avec valeur de retour non nulle
Vous déployez une application qui retourne le code de sortie `1` quand elle s’installe correctement. Par défaut, Configuration Manager détecte ce code de retour non nul comme étant un échec. Spécifiez la Valeur du code de retour `1`, puis sélectionnez le Type de code **Réussite (pas de redémarrage)**. Configuration Manager interprète désormais ce code de retour comme étant une réussite pour ce type de déploiement.


#### <a name="default-return-codes"></a>Codes de retour par défaut
Quand vous créez certains types de déploiement, Configuration Manager ajoute automatiquement les codes de retour suivants qui sont communs à cette technologie :  

**Windows Installer (\*fichier .msi)**  
|Valeur    |Type de code|
|---------|---------|
|0        |Réussite (pas de redémarrage)|
|1707     |Réussite (pas de redémarrage)|
|3010     |Redémarrage logiciel|
|1641     |Redémarrage matériel|
|1618     |Nouvelle tentative rapide|

**Programme d’installation de script**  
|Valeur    |Type de code|
|---------|---------|
|0        |Réussite (pas de redémarrage)|
|1641     |Redémarrage matériel|
|3010     |Redémarrage logiciel|
|1618     |Nouvelle tentative rapide|

**Package d’application Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)**  
|Valeur    |Type de code|
|---------|---------|
|15605    |Nouvelle tentative rapide|
|15618    |Nouvelle tentative rapide|



## <a name="bkmk_appv"></a> Options supplémentaires pour les types de déploiement App-V  

Configurez des options supplémentaires qui sont spécifiques aux types de déploiement pour les applications virtuelles (App-V).  

### <a name="bkmk_appv-content"></a> Options de **contenu** pour le type de déploiement App-V  

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.  

2.  Sélectionnez une application avec un type de déploiement App-V, puis cliquez sur **Propriétés**.  

3.  Dans les propriétés de l’application, basculez vers l’onglet **Types de déploiement**. Sélectionnez le type de déploiement App-V, puis cliquez sur **Modifier**.  

4.  Dans les propriétés du type de déploiement, basculez vers l’onglet **Contenu**. Configurez les options suivantes en fonction de vos besoins :  

    -   **Conserver le contenu dans la mémoire cache du client** : le client Configuration Manager ne supprime pas de son cache le contenu pour ce type de déploiement.  

    -   **Charger le contenu dans le cache App-V avant le lancement** : avant le démarrage de l’application, le client Configuration Manager charge dans le cache App-V tout le contenu de ce type de déploiement. Le client n’épingle pas le contenu dans le cache. Il supprime le contenu selon les besoins.  

5.  Cliquez sur **OK** pour fermer les propriétés du type de déploiement. Ensuite, cliquez sur **OK** pour fermer les propriétés de l’application.  


### <a name="bkmk_appv-pub"></a> Options de **publication** pour le type de déploiement App-V   

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.  

2.  Sélectionnez une application avec un type de déploiement App-V, puis cliquez sur **Propriétés**.  

3.  Dans les propriétés de l’application, basculez vers l’onglet **Types de déploiement**. Sélectionnez le type de déploiement App-V, puis cliquez sur **Modifier**.  

4.  Dans les propriétés du type de déploiement, basculez vers l’onglet **Publication**. Sélectionnez les éléments de l’application virtuelle que vous souhaitez publier.  

5.  Cliquez sur **OK** pour fermer les propriétés du type de déploiement. Ensuite, cliquez sur **OK** pour fermer les propriétés de l’application.  



## <a name="bkmk_import"></a> Importer une application  

Utilisez la procédure ci-dessous pour importer une application dans Configuration Manager : 

1.  Dans la console Configuration Manager, accédez à l’espace de travail **Bibliothèque de logiciels**, développez **Gestion des applications** et sélectionnez le nœud **Applications**.   

2.  Dans le ruban, sous l’onglet **Accueil**, dans le groupe **Créer**, cliquez sur **Importer l’application**.  

3.  Dans la page **Général** de l’Assistant Importation de l’application, spécifiez le chemin réseau du **Fichier** à importer. Par exemple, `\\server\share\file.zip`. Ce fichier est une archive compressée valide (format ZIP) d’une application Configuration Manager exportée.  

4.  Dans la page **Contenu du fichier**, sélectionnez l’action à effectuer si cette application est un doublon d’une application existante. Créez une application ou ignorez la copie et ajoutez une nouvelle révision à l’application existante.  

5.  Dans la page **Résumé**, passez en revue les actions, puis terminez l’Assistant.  

La nouvelle application s’affiche dans le nœud **Applications**.  

> [!TIP]  
>  L’applet de commande Windows PowerShell **Import-CMApplication** permet de réaliser la même opération que cette procédure. Pour plus d’informations, consultez [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Pour plus d’informations sur l’exportation d’une application, consultez [Tâches de gestion pour les applications](/sccm/apps/deploy-use/management-tasks-applications). 



## <a name="bkmk_deploy-types"></a> Types de déploiement pris en charge  

Configuration Manager prend en charge les types de déploiement suivants pour les applications :

| Nom du type de déploiement | Description |   
|--------------------------|----------------------|  
| **Windows Installer (\*fichier .msi)** | Fichier Windows Installer. |  
| **Package d’application Windows (\*.appx, \*.appxbundle)** | Pour Windows 8 ou version ultérieure. Sélectionnez le fichier de package d’une application Windows ou le package d’un ensemble d’applications Windows. |  
| **Package d’application Windows (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** | Depuis la version 1806, pour les nouveaux formats de package d’application (.msix) et d’ensemble d’applications (.msixbundle) Windows 10. Sélectionnez le fichier de package d’une application Windows ou le package d’un ensemble d’applications Windows.<!--1357427--> |  
| **Package d’application Windows (dans le Windows Store)** | Pour Windows 8 ou version ultérieure. Spécifiez un lien vers l’application dans le Windows Store ou parcourez ce dernier pour sélectionner l’application.<sup>[Remarque 1](#bkmk_note1)</sup> |  
| **Programme d’installation de script** | Spécifiez un script ou un programme qui s’exécute sur les clients Windows pour installer un contenu ou effectuer une action. Utilisez ce type de déploiement pour les programmes d’installation setup.exe ou les wrappers de script. |  
| **Microsoft Application Virtualization 4** | Manifeste Microsoft App-V v4. |  
| **Microsoft Application Virtualization 5** | Fichier de package Microsoft App-V v5. |  
| **Package d’application Windows Phone (\*fichier .xap)** | Fichier de package d’application Windows Phone. |  
| **Package d’application Windows Phone (dans le Windows Phone Store)** | Spécifiez un lien vers l’application dans le Windows Store. |  
| **Package d’application pour iOS (fichier \*.ipa)** | Fichier de package d’application Apple iOS. |  
| **Package d’application pour iOS depuis l’App Store** | Spécifiez un lien vers l’application iOS dans l’Apple Store. |  
| **Package d’application pour Android (fichier \*.apk)** | Fichier de package d’application Android. |  
| **Package d’application pour Android sur Google Play** | Spécifiez un lien vers l’application dans le Google Play Store. |  
| **Mac OS X** | Pour les ordinateurs macOS exécutant le client Configuration Manager. Créez un fichier .cmmac avec l’outil **CMAppUtil**. |  
| **Application web** | Spécifiez un lien vers une application web. Ce type de déploiement installe un raccourci vers l’application web sur l’appareil de l’utilisateur.<sup>[Remarque 2](#bkmk_note2)</sup> |  
| **Windows Installer via la gestion des appareils mobiles (\*.msi)** | Créez et déployez des applications basées sur Windows Installer sur des appareils Windows 10. Pour plus d’informations, consultez [Déployer des applications Windows Installer sur des appareils Windows 10 inscrits à MDM](/sccm/apps/get-started/creating-windows-applications#bkmk_mdm-msi). |  

#### <a name="bkmk_note1"></a> Remarque 1 : Package d’application Windows (dans le Windows Store)
Pour déployer l’application sous forme de lien vers le Windows Store, configurez la stratégie de groupe **Désactiver l’application du Windows Store**. Définissez cette stratégie sur **Désactivé** ou **Non configuré**. Si vous activez ce paramètre, les clients ne peuvent pas se connecter au Windows Store pour télécharger et installer des applications.

Les clients Windows évaluent toujours en premier les types de déploiement qui utilisent un lien vers un store. Ils évaluent ensuite les types de déploiement par priorité. 

#### <a name="bkmk_note2"></a> Remarque 2 : Application web  
Si vous avez installé Microsoft Intune Managed Browser sur des appareils iOS ou Android, vérifiez que les utilisateurs peuvent uniquement utiliser Managed Browser pour ouvrir l’application. Dans l’adresse du site web, remplacez **http** par **http-intunemam**, ou **https** par **https-intunemam**. Par exemple : 
- `http-intunemam://<path to web app>`
- `https-intunemam://<path to web app>`

Utilisez des [spécifications d’application](#bkmk_dt-require) Configuration Manager pour que les applications web qui se servent de Managed Browser ne soient installées que sur des appareils iOS et Android. 

Pour plus d’informations sur le navigateur Intune Managed Browser, consultez [Gérer l’accès à Internet à l’aide de stratégies Managed Browser](/sccm/apps/deploy-use/manage-internet-access-using-managed-browser-policies).



## <a name="next-steps"></a>Étapes suivantes

Après avoir créé une application dans Configuration Manager, l’étape suivante consiste à [déployer l’application](/sccm/apps/deploy-use/deploy-applications).

Pour plus d’informations sur la création d’applications sur différentes plateformes de système d’exploitation, consultez les articles suivants :  
- [Créer des applications Windows](/sccm/apps/get-started/creating-windows-applications)
- [Créer des applications pour les appareils mobiles](/sccm/mdm/deploy-use/create-applications) (iOS, Windows Mobile et Android)  
- [Créer des applications Mac](/sccm/apps/get-started/creating-mac-computer-applications)
- [Créer des applications serveur Linux et UNIX](/sccm/apps/get-started/creating-linux-and-unix-server-applications)
- [Créer des applications Windows Embedded](/sccm/apps/get-started/creating-windows-embedded-applications)

