---
title: Sécurité et confidentialité pour la gestion des applications
titleSuffix: Configuration Manager
description: En savoir plus sur les conseils et les recommandations en matière de sécurité et de confidentialité pour la gestion des applications
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4d26deed-3b16-4116-b640-f618f2c20f5a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 80ae609bccd60e68cfee76878bd7a461b5f61716
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-application-management-in-system-center-configuration-manager"></a>Sécurité et confidentialité pour la gestion des applications dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*


##  <a name="security-guidance-for-application-management"></a>Conseils en matière de sécurité pour la gestion des applications  

|Conseils en matière de sécurité|Plus d'informations|  
|----------------------------|----------------------|  
|Configurer les points du catalogue d'applications pour utiliser des connexions HTTPS et informer les utilisateurs sur les dangers des sites Web malveillants.|Configurez le point du site web du catalogue des applications et le point de service web du catalogue des applications pour qu’ils acceptent les connexions HTTPS. Avec cette configuration, le serveur est authentifié auprès des utilisateurs et les données transmises sont protégées contre la falsification et la consultation. Limitez les chances de subir des attaques d’ingénierie sociale en invitant les utilisateurs à se connecter uniquement à des sites web approuvés.<br /><br /> Quand vous n’utilisez pas HTTPS, évitez d’utiliser les options de configuration de la personnalisation, qui affichent le nom de votre organisation dans le catalogue des applications comme preuve d’identité.|  
|Utiliser la séparation des rôles et installer le point de site Web du catalogue des applications et le point de service du catalogue des applications sur des serveurs distincts.|Si le point de site web du catalogue des applications est compromis, installez-le sur un serveur distinct du point de service web du catalogue des applications. Cette conception contribue à protéger les clients et l’infrastructure Configuration Manager. Cette configuration est particulièrement importante si le point du site web du catalogue des applications accepte les connexions des clients en partir d’Internet. Le serveur se trouve moins exposé aux attaques.|  
|Formez les utilisateurs à la fermeture de la fenêtre du navigateur lorsqu'ils ont terminé d'utiliser le catalogue des applications.|Si les utilisateurs naviguent jusqu'à un site Web externe dans la même fenêtre du navigateur que celle qu'ils ont utilisée pour le catalogue d'applications, le navigateur continue à utiliser les paramètres de sécurité adaptés aux sites approuvés dans l'intranet.|  
|Spécifiez manuellement l’affinité entre utilisateur et appareil au lieu de laisser les utilisateurs identifier leur appareil principal. N’activez pas la configuration basée sur l’utilisation.|Ne considérez pas comme faisant autorité les informations collectées auprès des utilisateurs ou de l’appareil. Si vous déployez un logiciel en utilisant une affinité entre utilisateur et périphérique qu’un administrateur ne spécifie pas, le logiciel risque de s’installer sur des ordinateurs et pour des utilisateurs qui ne sont pas autorisés à recevoir ce logiciel.|  
|Configurez toujours les déploiements pour télécharger du contenu à partir de points de distribution plutôt que de les exécuter à partir de points de distribution.|Quand vous configurez des déploiements pour télécharger du contenu à partir d’un point de distribution et que vous les exécutez localement, le client Configuration Manager vérifie le hachage du package après avoir téléchargé le contenu. Le client rejette le package si le hachage ne correspond pas à celui défini dans la stratégie. En comparaison, si vous configurez un déploiement pour qu’il s’exécute directement à partir d’un point de distribution, le client Configuration Manager ne vérifie pas le hachage du package. Ce comportement signifie que le client Configuration Manager peut installer un logiciel qui a été falsifié.<br /><br /> Si vous devez effectuer des déploiements directement à partir de points de distribution, utilisez les autorisations NTFS minimales sur les packages au niveau des points de distribution. De même, utilisez la sécurité du protocole Internet (IPsec) pour sécuriser le canal entre le client et les points de distribution et entre les points de distribution et le serveur de site.|  
|<a name="bkmk_interact"></a>Ne laissez pas les utilisateurs interagir avec les applications si vous activez les options **Exécuter avec les droits d’administration** ou **Installer pour le système**.|Quand vous configurez une application, vous pouvez définir l’option **Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme**. Ce paramètre permet aux utilisateurs de répondre à toutes les invites obligatoires dans l’interface utilisateur. Si vous configurez aussi l’application avec l’option **Exécuter avec les droits d’administration**, ou à partir de la version 1802, **Installer pour le système**, une personne malveillante sur l’ordinateur qui exécute le programme peut utiliser l’interface utilisateur pour élever les privilèges sur l’ordinateur client.<br /><br /> Utilisez des programmes utilisant Windows Installer pour l’installation et des privilèges élevés par utilisateur pour les déploiements de logiciels qui nécessitent des informations d’identification d’administration. Le programme d’installation doit être exécuté dans le contexte d’un utilisateur qui ne dispose pas d’informations d’identification d’administration. Les privilèges élevés par utilisateur de Windows Installer représentent la méthode la plus sûre pour déployer les applications avec cette spécification.|  
|Déterminez si les utilisateurs peuvent installer les logiciels de manière interactive à l'aide du paramètre du client **Autorisations d'installation** .|Configurez le paramètre d’appareil client **Agent ordinateur** **Autorisations d’installation** pour restreindre les types d’utilisateurs qui peuvent installer le logiciel à l’aide du catalogue des applications ou du Centre logiciel. Par exemple, créez un paramètre de client personnalisé après avoir défini **Installer les autorisations** sur **Administrateurs uniquement**. Appliquez ensuite ce paramètre du client à un regroupement de serveurs pour empêcher les utilisateurs sans autorisation d’administration d’installer des logiciels sur ces ordinateurs.|  
|Pour les appareils mobiles, déployez seulement les applications qui sont signées.|Déployez des applications d’appareil mobile seulement si leur code est signé par une autorité de certification approuvée par l’appareil mobile. Par exemple :<br /><ul><li>Une application d’un fournisseur, signée par une autorité de certification connue, comme VeriSign.</li><li>Une application interne que vous signez indépendamment de Configuration Manager, en utilisant votre autorité de certification interne.</li><li>Une application interne que vous signez à l’aide de Configuration Manager quand vous créez le type d’application et que vous utilisez un certificat de signature.</li></ul>|  
|Si vous signez des applications d’appareil mobile à l’aide de l’ **Assistant Création d’une application** dans Configuration Manager, sécurisez l’emplacement du fichier de certificat de signature, ainsi que le canal de communication.|Pour vous prémunir contre l’élévation de privilèges et les attaques de l’intercepteur, stockez le fichier de certificat de signature dans un dossier sécurisé. Utilisez IPsec entre les ordinateurs suivants :<br /><ul><li>Ordinateur qui exécute la console Configuration Manager</li><li>L’ordinateur qui stocke le fichier de signature de certificat.</li><li>L’ordinateur qui stocke les fichiers sources de l’application.</li></ul> Vous pouvez aussi signer l’application indépendamment de Configuration Manager et avant d’exécuter l’**Assistant Création d’une application**.|  
|Pour protéger les ordinateurs de référence, implémentez des contrôles d’accès.|Assurez-vous que lorsqu'un utilisateur administratif configure une méthode de détection dans un type de déploiement en naviguant vers un ordinateur de référence, cet ordinateur n'a pas été compromis.|  
|Limitez et surveillez les utilisateurs administratifs auxquels vous accordez les rôles de sécurité basée sur les rôles de gestion des applications suivants :<br /><ul><li>**Administrateur d’application**</li><li>**Auteur d’application**</li><li> **Gestionnaire de déploiement d’applications**</li></ul>|Même lorsque vous configurez l'administration basée sur les rôles, les utilisateurs administratifs qui créent et déploient des applications peuvent disposer d'un nombre d'autorisations plus important que ce que vous pensez. Par exemple, des utilisateurs administratifs qui créent ou modifient une application peuvent sélectionner des applications dépendantes qui ne sont pas dans leur étendue de sécurité.|  
|Quand vous configurez des environnements virtuels Microsoft Application Virtualization (App-V), sélectionnez des applications qui ont le même niveau de confiance dans l’environnement virtuel.|Dans la mesure où des applications dans un environnement virtuel App-V peuvent partager des ressources, comme le Presse-papiers, configurez l’environnement virtuel afin que les applications sélectionnées aient le même niveau de confiance.<br /><br /> Pour plus d’informations, consultez [Créer des environnements virtuels App-V](../../apps/deploy-use/create-app-v-virtual-environments.md).|  
|Si vous déployez des applications pour les ordinateurs Mac, assurez-vous que les fichiers source proviennent d'une source fiable.|L'outil CMAppUtil ne valide pas la signature du package source, assurez-vous qu'il provient d'une source de confiance. L’outil CMAppUtil ne peut pas détecter si les fichiers ont été falsifiés.|  
|Si vous déployez des applications pour des ordinateurs Mac, sécurisez l’emplacement du fichier **.cmmac**, ainsi que le canal de communication quand vous importez ce fichier dans Configuration Manager.|Le fichier **.cmmac** qui est généré par l’outil CMAppUtil et que vous importez dans Configuration Manager n’est pas signé ou validé. Pour éviter la falsification avec ce fichier, stockez-le dans un dossier sécurisé et utilisez IPSec ou SMB entre les ordinateurs suivants :<br /><br /><ul><li>Ordinateur qui exécute la console Configuration Manager</li><li>L’ordinateur qui stocke le fichier **.cmmac**.</li></ul>|  
|Si vous configurez un type de déploiement d'application Web, utilisez le protocole HTTPS plutôt que HTTP pour sécuriser la connexion.|Si vous déployez une application web en utilisant un lien HTTP plutôt qu’un lien HTTPS, l’appareil peut être redirigé vers un serveur non autorisé. Les données transférées entre l’appareil et le serveur ont pu être falsifiées.|  



##  <a name="security-issues-for-application-management"></a>Problèmes de sécurité pour la gestion des applications  

-   Les utilisateurs à faibles privilèges peuvent copier des fichiers à partir du cache du client sur l'ordinateur client.  

     Les utilisateurs peuvent lire le cache du client, mais pas y écrire. Avec les autorisations de lecture, un utilisateur peut copier des fichiers d'installation d'application d'un ordinateur à un autre.  

-   Les utilisateurs avec des privilèges faibles peuvent modifier les fichiers qui enregistrent l’historique de déploiement de logiciels sur l’ordinateur client.  

     Sachant que les informations de l’historique des applications ne sont pas protégées, un utilisateur peut modifier les fichiers qui indiquent si une application est installée.  

-   Les packages App-V ne sont pas signés.  

     Les packages App-V dans Configuration Manager ne prennent pas en charge la signature. Les signatures numériques vérifient que le contenu provient d’une source approuvée et qu’il n’a pas été altéré au cours du transit. Il n’existe aucune mesure d’atténuation du risque pour ce problème de sécurité. Suivez les bonnes pratiques de sécurité de façon à télécharger le contenu à partir d’une source approuvée et d’un emplacement sécurisé.  

-   Les applications App-V publiées peuvent être installées par tous les utilisateurs sur l'ordinateur.  

     Quand une application App-V est publiée sur un ordinateur, tous les utilisateurs qui se connectent à cet ordinateur peuvent installer l’application. Vous ne pouvez pas limiter les utilisateurs qui peuvent installer l’application après sa publication.  

-   Vous ne pouvez pas limiter les autorisations d'installation du portail d'entreprise.  

     Bien que vous puissiez configurer un paramètre client pour limiter les autorisations d’installation, par exemple aux utilisateurs principaux d’un appareil ou aux administrateurs locaux uniquement, ce paramètre ne fonctionne pas pour le portail d’entreprise. Ce problème peut entraîner une élévation de privilèges. Les utilisateurs peuvent ainsi installer une application alors qu’ils ne devraient pas être autorisés à le faire.  



##  Certificats <a name="BKMK_CertificatesSilverlight5"></a> pour Microsoft Silverlight 5 et mode de confiance élevée obligatoires pour le catalogue des applications  
 Les clients Configuration Manager requièrent Microsoft Silverlight 5, qui doit s’exécuter en mode de confiance élevée pour permettre aux utilisateurs d’installer des logiciels à partir du catalogue d’applications. Par défaut, les applications Silverlight s'exécutent en mode de confiance partielle pour empêcher les applications d'accéder aux données utilisateur. Si ce n’est pas déjà fait, Configuration Manager installe automatiquement Microsoft Silverlight 5 sur les clients. Par défaut, Configuration Manager définit le paramètre du client **Autoriser les applications Silverlight à s’exécuter en mode de confiance élevée** de l’Agent ordinateur sur **Oui**. Ce paramètre permet aux applications Silverlight signées et approuvées de demander le mode de confiance élevée.  

 Lors de l’installation du rôle de système de site du point de site web du catalogue d’applications, le client installe également un certificat de signature Microsoft dans le magasin de certificats Éditeurs approuvés de l’ordinateur sur chaque ordinateur client Configuration Manager. Les applications Silverlight signées par ce certificat s’exécutent en mode de confiance élevée, ce dont les ordinateurs ont besoin pour pouvoir installer des logiciels du catalogue des applications. Configuration Manager gère automatiquement ce certificat de signature. Pour assurer la continuité de service, ne supprimez pas ou ne déplacez pas manuellement ce certificat de signature Microsoft.  

> [!WARNING]  
>  Quand il est activé, le paramètre client **Autoriser les applications Silverlight à s’exécuter en mode de confiance élevée** permet à toutes les applications Silverlight signées par des certificats du magasin de certificats Éditeurs approuvés, que ce soit dans le magasin de l’ordinateur ou dans le magasin de l’utilisateur, de s’exécuter en mode de confiance élevée. Le paramètre client ne peut pas activer le mode de confiance élevée spécifiquement pour le catalogue des applications Configuration Manager ou pour le magasin de certificats Éditeurs approuvés du magasin de l’ordinateur. Si un logiciel malveillant ajoute un certificat non autorisé dans le magasin de certificats Éditeurs approuvés, un logiciel malveillant qui utilise sa propre application Silverlight peut dès lors s’exécuter aussi en mode de confiance élevée.  

 Si vous définissez le paramètre **Autoriser les applications Silverlight à s’exécuter en mode de confiance élevée** sur **Non**, les clients ne suppriment pas le certificat de signature Microsoft.  

 Pour plus d’informations sur les applications approuvées dans Silverlight, consultez [Applications approuvées](https://go.microsoft.com/fwlink/p/?LinkId=252842).  

 > [!NOTE]
 > Depuis Configuration Manager 1802, Silverlight n’est plus installé automatiquement. La fonctionnalité principale du catalogue des applications est désormais incluse dans le Centre logiciel. La prise en charge du site web du catalogue des applications prend fin avec la première mise à jour publiée après le 1er juin 2018.



##  <a name="privacy-information-for-application-management"></a>Informations de confidentialité pour la gestion d'applications  
 La gestion des applications vous permet d’exécuter n’importe quel programme, script ou application sur n’importe quel client de la hiérarchie. Configuration Manager n’a aucun contrôle sur les types d’applications, de programmes ou de scripts que vous exécutez, ni sur le type d’informations qu’ils transmettent. Lors du déploiement des applications, Configuration Manager peut transmettre des informations entre les clients et les serveurs qui identifient les comptes d’appareil et de connexion.  

 Configuration Manager gère les informations d’état relatives au processus de déploiement de logiciels. Les informations d’état relatives au déploiement logiciel ne sont pas chiffrées pendant la transmission, à moins que le client communique avec HTTPS. Les informations d’état ne sont pas stockées dans la base de données sous une forme chiffrée.  

 L’utilisation de l’installation d’applications de Configuration Manager pour installer à distance, en mode interactif ou silencieux des logiciels sur des clients peut être soumise à des termes de contrat de licence propres à ce logiciel. Cette utilisation est distincte des termes du contrat de licence logiciel pour System Center Configuration Manager. Consultez et acceptez toujours les termes du contrat de licence logiciel avant de déployer le logiciel à l’aide de Configuration Manager.  

 Le déploiement d’application ne se produit pas par défaut et nécessite plusieurs étapes de configuration.  

 Deux fonctionnalités facultatives qui contribuent au déploiement efficace de logiciels sont l'affinité entre périphérique et utilisateur et le catalogue d'applications :  

-   L’affinité entre utilisateur et périphérique mappe un utilisateur à des appareils. Un administrateur Configuration Manager déploie les logiciels pour un utilisateur. Le client installe automatiquement le logiciel sur le ou les ordinateurs que l’utilisateur utilise le plus souvent.  

-   Le catalogue des applications est un site web qui permet aux utilisateurs de demander l’installation de logiciels.  

 Consultez les sections suivantes pour obtenir des informations de confidentialité sur l'affinité entre périphérique et utilisateur et le catalogue d'applications.  

 Avant de configurer la gestion des applications, pensez à vos besoins en matière de confidentialité.  



##  <a name="user-device-affinity"></a>Affinité entre périphérique et utilisateur  
-  Configuration Manager peut transmettre des informations entre les clients et les systèmes de site du point de gestion. Les informations peuvent identifier le compte d’ordinateur et de connexion, ainsi que le résumé de l’utilisation pour les comptes de connexion.  
-  Les informations transmises entre le client et le serveur ne sont pas chiffrées, sauf si le point de gestion est configuré pour imposer aux clients de communiquer via HTTPS.  
-  Les informations relatives à l’ordinateur et à l’utilisation du compte de connexion, qui servent à mapper un utilisateur à un appareil, sont stockées sur les ordinateurs clients, envoyées aux points de gestion, puis stockées dans la base de données Configuration Manager. Les informations anciennes sont supprimées de la base de données par défaut après 90 jours. Le comportement de suppression peut être configuré en définissant la tâche de maintenance de site **Supprimer les anciennes données relatives à l'affinité entre périphérique et utilisateur** .
-  Configuration Manager conserve les informations d’état relatives à l’affinité entre utilisateur et appareil. Les informations d'état ne sont pas chiffrées lors de leur transmission, sauf si les clients sont configurés pour communiquer avec des points de gestion à l'aide de HTTPS. Les informations d'état sont stockées dans la base de données sous une forme non chiffrée.  
-  Les informations sur l’ordinateur et sur l’utilisation du compte de connexion ainsi que les informations d’état ne sont pas envoyées à Microsoft.  
-  Les informations sur l’ordinateur et sur la connexion qui sont utilisées pour déterminer l’affinité entre utilisateur et appareil sont toujours activées. En outre, les utilisateurs et utilisateurs administratifs peuvent fournir des informations relatives à l'affinité entre périphérique et utilisateur.  



##  <a name="application-catalog"></a>Catalogue d'applications  
-  Le catalogue des applications permet à l’administrateur Configuration Manager de publier n’importe quel programme, script ou application exécutable par les utilisateurs. Configuration Manager n’a aucun contrôle sur les types de programmes ou de scripts publiés dans le catalogue, ni sur le type des informations qu’ils transmettent.    
-  Configuration Manager peut transmettre des informations entre les clients et les rôles de systèmes de site du catalogue des applications. Les informations peuvent identifier les comptes d’ordinateur et de connexion. Les informations transmises entre le client et les serveurs ne sont pas chiffrées, sauf si ces rôles de système de site sont configurés pour imposer aux clients de se connecter via HTTPS.  
-  Les informations sur la demande d’approbation d’application sont enregistrées dans la base de données Configuration Manager. Les demandes qui sont annulées ou refusées, ainsi que les entrées d’historique de demande correspondantes, sont supprimées par défaut après 30 jours. Le comportement de suppression peut être configuré en définissant la tâche de maintenance de site **Supprimer les anciennes données de demande d'application** . Les demandes d’approbation d’application qui sont à l’état Approuvé et En attente ne sont jamais supprimées.  
-  Les informations envoyées vers et depuis le catalogue d'applications et ne sont pas transmises à Microsoft.  
-  Le catalogue des applications n'est pas installé par défaut. Cette installation nécessite plusieurs étapes de configuration.  
