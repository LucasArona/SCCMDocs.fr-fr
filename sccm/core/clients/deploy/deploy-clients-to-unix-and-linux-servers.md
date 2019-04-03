---
title: Déployer des clients UNIX/Linux
titleSuffix: Configuration Manager
description: Découvrez comment déployer un client sur un serveur UNIX ou Linux dans Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 855869db6d127999218964d06e50179c70efed0a
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58524096"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Comment déployer des clients sur des serveurs UNIX et Linux dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Important]  
> Depuis la version 1902, Configuration Manager ne prend en charge les clients Linux ou UNIX. 
> 
> Utilisez plutôt Microsoft Azure Management pour la gestion des serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.


Avant de pouvoir gérer un serveur Linux ou UNIX avec Configuration Manager, vous devez installer le client Configuration Manager pour Linux et UNIX sur chaque serveur Linux ou UNIX. Vous pouvez soit installer manuellement le client sur chaque ordinateur, soit utiliser un script Shell qui installe le client à distance. Configuration Manager ne prend pas en charge l’installation Push du client pour les serveurs Linux ou UNIX. Vous pouvez éventuellement configurer un Runbook pour System Center Orchestrator pour automatiser l’installation du client sur le serveur Linux ou UNIX.  

 Quelle que soit la méthode d’installation utilisée, le processus d’installation nécessite un script nommé **install** pour gérer le processus d’installation. Ce script est inclus lorsque vous téléchargez le Client pour Linux et UNIX.  

 Le script d’installation pour le client Configuration Manager pour Linux et UNIX prend en charge les propriétés de ligne de commande. Certaines propriétés de ligne de commande sont requises, tandis que d'autres sont facultatives. Par exemple, lorsque vous installez le client, vous devez spécifier un point de gestion à partir du site est utilisé par le serveur Linux ou UNIX pour son contact initial avec le site. Pour obtenir la liste complète des propriétés de ligne de commande, consultez [Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX](#BKMK_CmdLineInstallLnUClient).  

 Après avoir installé le client, spécifiez les paramètres du client dans la console Configuration Manager pour configurer l’agent du client. Suivez la même procédure que pour un client Windows. Pour plus d’informations, consultez [Paramètres client pour les serveurs Linux et UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> À propos des Packages d'Installation de Client et l'Agent universel  
 Pour installer le client pour Linux et UNIX sur une plateforme spécifique, vous devez utiliser le package d’installation du client applicable pour l’ordinateur sur lequel vous installez le client. Les packages d’installation de client applicables sont inclus dans chaque téléchargement du client effectué à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). En plus des packages d’installation de client, le téléchargement du client comprend le script **install** qui gère l’installation du client sur chaque ordinateur.  

 Lorsque vous installez un client, vous pouvez utiliser les mêmes propriétés de processus et de ligne de commande que vous utilisez le package d'installation client.  

 Pour plus d’informations sur les systèmes d’exploitation, les plateformes et les packages d’installation de client pris en charge par chaque version du client Configuration Manager pour Linux et UNIX, consultez [Serveurs Linux et UNIX](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers).  

##  <a name="BKMK_InstallLnUClient"></a> Installer le client sur des serveurs Linux et UNIX  
 Pour installer le client pour Linux et UNIX, vous exécutez un script sur chaque ordinateur Linux ou UNIX. Le script est nommé **installer** et prend en charge les propriétés de ligne de commande qui modifient le comportement d'installation et de référencent le package d'installation du client. Le package d'installation installation script et le client doit se trouver sur le client. Le package d’installation client contient les fichiers du client Configuration Manager pour une plate-forme et un système d’exploitation Linux ou UNIX spécifiques.
Chaque package d'installation du client contient tous les fichiers nécessaires pour terminer l'installation du client et contrairement aux ordinateurs fonctionnant sous Windows, ne pas télécharge des fichiers supplémentaires à partir d'un point de gestion ou un autre emplacement source.  

 Après avoir installé le client Configuration Manager pour Linux et UNIX, vous n’avez pas besoin de redémarrer l’ordinateur. Dès que l'installation est terminé, le client est opérationnel. Si vous redémarrez l’ordinateur, le client Configuration Manager redémarre automatiquement.  

 Le client installé s'exécute avec les informations d'identification racine. Des informations d’identification racine sont nécessaires pour collecter l’inventaire matériel et effectuer les déploiements de logiciels.  

 Utilisez le format de commande suivant :  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` est le nom du fichier de script qui installe le client pour Linux et UNIX. Ce fichier est fourni avec le logiciel client.  

-   `-mp <computer>` spécifie le point de gestion initial utilisé par le client. Exemple : `smsmp.contoso.com`  

-   `-sitecode <site code>` spécifie le code de site auquel le client est affecté. Exemple : `S01`  

-   `<property #1> <property #2>` spécifie les propriétés de ligne de commande à utiliser avec le script d’installation.  

    > [!NOTE]  
    >  Pour plus d’informations, consultez [Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX](#BKMK_CmdLineInstallLnUClient).  

-   **package d’installation du client** est le nom du package .tar d’installation du client pour le système d’exploitation, la version et l’architecture d’UC de l’ordinateur. Le fichier .tar d'installation client doit être spécifié en dernier. Exemple : `ccm-Universal-x64.<build>.tar`  

###  <a name="BKMK_ToInstallLnUClinent"></a> Pour installer le client Configuration Manager sur des serveurs Linux et UNIX  

1.  Sur un ordinateur Windows, [téléchargez le fichier client approprié pour le serveur Linux ou UNIX](https://go.microsoft.com/fwlink/?LinkID=525184) que vous souhaitez gérer.  

2.  Exécutez le fichier .exe à extraction automatique sur l’ordinateur Windows pour extraire le script d’installation et le fichier .tar d’installation du client.  

3.  Copiez le script d’ **installation** et le fichier .tar dans un dossier sur le serveur que vous souhaitez gérer.  

4.  Sur le serveur UNIX ou Linux, exécutez la commande suivante pour autoriser le script à s’exécuter comme un programme : `chmod +x install`  

    > [!IMPORTANT]  
    >  Vous devez utiliser des informations d'identification racine pour installer le client.  

5.  Exécutez ensuite la commande suivante pour installer le client Configuration Manager : `./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Lorsque vous entrez cette commande, utilisez les propriétés de ligne de commande supplémentaires que vous avez besoin. Pour obtenir la liste des propriétés de ligne de commande, consultez [Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX](#BKMK_CmdLineInstallLnUClient)  

6.  Une fois le script exécuté, validez l’installation en examinant le fichier **/var/opt/microsoft/scxcm.log** . De plus, vous pouvez vérifier que le client est installé et qu’il communique avec le site en affichant les détails relatifs au client dans le nœud **Appareils** de l’espace de travail **Ressources et Conformité** dans la console Configuration Manager.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX  
 Les propriétés suivantes sont disponibles pour modifier le comportement du script d’installation :  

> [!NOTE]  
>  Utilisez la propriété `-h` pour afficher la liste des propriétés prises en charge.  

-   `-mp <server FQDN>`  

     Obligatoire. Spécifie le nom de domaine complet, le serveur de point de gestion que le client utilise comme un point de contact initial.  

    > [!IMPORTANT]  
    >  Cette propriété n’indique pas le point de gestion auquel le client est attribué après l’installation.  

    > [!NOTE]  
    >  Quand vous utilisez la propriété `-mp` pour spécifier un point de gestion qui est configuré pour accepter uniquement les connexions client HTTPS, vous devez également employer la propriété `-UsePKICert`.  

-   `-sitecode <sitecode>`  

     Obligatoire. Spécifie le site principal Configuration Manager auquel attribuer le client Configuration Manager. Exemple : `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     Facultatif. Spécifie le nom de domaine complet, le serveur de point d'état de secours que le client utilise pour envoyer des messages d'état. Pour plus d’informations, consultez [Déterminer si vous avez besoin d’un point d’état de secours](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point).  

-   `-dir <directory>`  

     Facultatif. Spécifie un autre emplacement pour installer les fichiers du client Configuration Manager. Par défaut, le client est installé à l'emplacement suivant : `/opt/microsoft`  

-   `-nostart`  

     Facultatif. Empêche le démarrage automatique du service client Configuration Manager, **ccmexec.bin**, après l’installation du client.  

     Une fois le client installé, vous devez démarrer manuellement le service client.  

     Par défaut, le service client démarre après la fin de l'installation du client, et chaque fois que l'ordinateur redémarre.  

-   `-clean`  

     Facultatif. Spécifie la suppression de tous les fichiers du client et les données à partir d'un client installé précédemment pour Linux et UNIX, avant le démarrage de la nouvelle installation. Cette action supprime le magasin de certificats et la base de données du client.  

-   `-keepdb`  

     Facultatif. Spécifie que la base de données client local est conservée et réutilisée, lorsque vous réinstallez un client. Par défaut, lorsque vous réinstallez un client de cette base de données est supprimé.  

-   `-UsePKICert <parameter>`  

     Facultatif. Spécifie le chemin d'accès et le nom complet à un certificat X.509 PKI au format Public Key Certificate Standard (PKCS #12). Ce certificat est utilisé pour l'authentification du client. Si aucun certificat n’est spécifié pendant l’installation et que vous devez en ajouter ou en modifier un, faites appel à l’utilitaire **certutil** . Pour plus d’informations, consultez [Comment gérer des certificats sur le Client pour Linux et UNIX](/sccm/core/clients/manage/manage-clients-for-linux-and-unix-servers#BKMK_ManageLinuxCerts).  

     Avec `-UsePKICert`, vous devez également vous servir du mot de passe associé au fichier PKCS#12 en utilisant le paramètre de ligne de commande `-certpw`.  

     Si vous n'utilisez pas cette propriété pour spécifier un certificat PKI, le client utilise un certificat auto-signé et sont des systèmes de site de toutes les communications via HTTP.  

     Si vous spécifiez un certificat non valide sur le client installation de ligne de commande, aucune erreur n'est retournée. La validation de certificat se produit après l'installation du client. Lorsque le client démarre, les certificats sont validés avec le point de gestion. Si la validation d’un certificat échoue, le message suivant apparaît dans **scxcm.log** : **Échec de la validation du certificat de point de gestion**. L’emplacement par défaut du fichier journal est :  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Vous devez spécifier cette propriété quand vous installez un client et utiliser la propriété `-mp` pour indiquer un point de gestion qui est configuré pour accepter uniquement les connexions client HTTPS.  

     Exemple : `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     Facultatif. Spécifie le mot de passe associé au fichier PKCS #12 que vous avez spécifié à l'aide de la propriété `-UsePKICert`.  

     Exemple : `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     Facultatif. Spécifie qu'un client ne doit pas vérifier la liste de révocation de certificats (CRL) lorsqu'il communique via HTTPS à l'aide d'un certificat PKI. Lorsque cette option n'est pas spécifiée, le client vérifie la révocation de certificats avant d'établir une connexion HTTPS à l'aide de certificats PKI. Pour plus d'informations sur la vérification de révocation de certificats client, consultez Planification de la révocation de certificats PKI.  

     Exemple : `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     Facultatif. Spécifie le chemin d’accès complet et le nom de fichier de la clé racine approuvée Configuration Manager. La clé racine approuvée Configuration Manager fournit un mécanisme que les clients Linux et UNIX utilisent pour vérifier qu’ils sont connectés à un système de site qui appartient à la hiérarchie appropriée.  

     Si vous ne spécifiez pas la clé racine approuvée sur la ligne de commande, le client approuve le premier point de gestion avec lequel il communique et récupère automatiquement la clé racine approuvée à partir de ce point de gestion.  

     Pour plus d’informations, consultez  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Exemple : `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     Facultatif. Spécifie le port est configuré sur les points de gestion que le client utilise lors de la communication aux points de gestion via HTTP. Si le port n'est pas spécifié, la valeur par défaut 80 est utilisée.  

     Exemple : `-httpport 80`  

-   `-httpsport <port>`  

     Facultatif. Spécifie le port est configuré sur les points de gestion que le client utilise lors de la communication aux points de gestion via HTTPS. Si le port n'est pas spécifié, la valeur par défaut 443 est utilisée.  

     Exemple : `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     Facultatif. Spécifie que l'installation du client ignore la validation de l'algorithme SHA-256. Utilisez cette option quand vous installez le client sur des systèmes d’exploitation publiés avec une version d’OpenSSL qui ne prend pas en charge SHA-256. Pour plus d’informations, voir[À propos des systèmes d’exploitation Linux et UNIX qui ne prennent pas en charge SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     Facultatif. Spécifie le chemin d'accès complet et **.cer** nom de fichier du certificat auto-signé exporté sur le serveur de site. Si les certificats PKI ne sont pas disponibles, le serveur de site Configuration Manager génère automatiquement des certificats auto-signés.  

     Ces certificats sont utilisés pour valider que les stratégies client téléchargés à partir du point de gestion ont été envoyés à partir du site de destination. Si aucun certificat auto-signé n’est spécifié pendant l’installation ou que vous devez modifier le certificat, faites appel à l’utilitaire **certutil** . Pour plus d’informations, consultez [Comment gérer des certificats sur le Client pour Linux et UNIX](/sccm/core/clients/manage/manage-clients-for-linux-and-unix-servers#BKMK_ManageLinuxCerts).  

     Ce certificat, qui peut être récupéré dans le magasin de certificats **SMS** , porte le nom d’objet **Serveur de site** et le nom convivial **Certificat de signature du serveur de site**.  

     Si cette option n’est pas spécifiée lors de l’installation, les clients Linux et UNIX approuvent le premier point de gestion avec lequel ils communiquent. Ils récupèrent automatiquement le certificat de signature auprès de ce point de gestion.  

     Exemple : `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     Facultatif. Spécifie les autres certificats PKI pour importer qui ne font pas partie d'une hiérarchie d'autorité de certification gestion des points. Si vous spécifiez plusieurs certificats dans la ligne de commande, ils doivent être séparés par des virgules.  

     Utilisez cette option si vous utilisez des certificats clients PKI qui ne se lient pas à un certificat d'autorité de certification racine approuvée par les points de gestion de vos sites. Les points de gestion rejettent le client si le certificat client n’est pas associé à un certificat racine approuvé dans la liste des émetteurs de certificat du site.  

     Si vous n’utilisez pas cette option, le client Linux et UNIX vérifie la hiérarchie d’approbation en utilisant uniquement le certificat figurant dans l’option `-UsePKICert`.  

     Exemple : `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="BKMK_UninstallLnUClient"></a> Désinstallation du client sur des serveurs Linux et UNIX  
 Pour désinstaller le client Configuration Manager pour Linux et UNIX, vous utilisez l’utilitaire de désinstallation, **uninstall**. Par défaut, ce fichier se trouve dans le **/opt/microsoft/configmgr/bin/** dossier sur l'ordinateur client. Cette commande de désinstallation ne prend pas en charge des paramètres de ligne de commande et supprimera tous les fichiers liés au logiciel client à partir du serveur.  

 Pour désinstaller le client, utilisez la ligne de commande suivante : **/opt/microsoft/configmgr/bin/uninstall**  

 Après avoir désinstallé le client Configuration Manager pour Linux et UNIX, vous n’avez pas besoin de redémarrer l’ordinateur.  

##  <a name="BKMK_ConfigLnUClientCommuincations"></a> Configurer les Ports de requêtes pour le Client pour Linux et UNIX  
 Comme les clients basés sur Windows, le client Configuration Manager pour Linux et UNIX utilise HTTP et HTTPS pour communiquer avec les systèmes de site Configuration Manager. Les ports que le client Configuration Manager utilise pour communiquer sont appelés ports de demande.  

 Lorsque vous installez le client Configuration Manager pour Linux et UNIX, vous pouvez modifier les ports de demande par défaut du client en spécifiant les propriétés d’installation **-httpport** et **-httpsport**. Lorsque vous ne spécifiez pas la propriété d'installation et une valeur personnalisée, le client utilise les valeurs par défaut. Les valeurs par défaut sont **80** pour le trafic HTTP et **443** pour le trafic HTTPS.  

 Après avoir installé le client, vous ne pouvez pas modifier sa configuration de port de demande. En revanche, pour modifier la configuration du port, vous devez réinstaller le client et spécifier la configuration du port. Lorsque vous réinstallez le client pour modifier les numéros de port de requête, exécutez le **installer** commande semblable à l'installation du client, mais utilisez la propriété de ligne de commande supplémentaires de **- keepdb ne**. Ce commutateur indique à l'installation pour conserver la base de données client et les fichiers, notamment le magasin GUID et des certificats clients.  

 Pour plus d’informations sur les numéros de port de communication client, consultez [Comment configurer les ports de communication des clients dans System Center Configuration Manager](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="BKMK_ConfigClientMP"></a> Configurer le Client pour Linux et UNIX de localiser des Points de gestion  
 Lorsque vous installez le client Configuration Manager pour Linux et UNIX, vous devez spécifier un point de gestion à utiliser comme point de contact initial.  

 Le client Configuration Manager pour Linux et UNIX contacte ce point de gestion au moment de l’installation du client. Si le client ne parvient pas à contacter le point de gestion, le logiciel client renouvelle les tentatives jusqu’à ce que le contact soit établi.  

 Pour plus d’informations sur la manière dont les clients localisent les points de gestion, consultez [Localisation de points de gestion](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).
