---
title: Déployer des clients UNIX/Linux
titleSuffix: Configuration Manager
description: Découvrez comment déployer un client sur un serveur UNIX ou Linux dans System Center Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7caffbbccfa53ef4e502685263cb0d81c6e83535
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-system-center-configuration-manager"></a>Comment déployer des clients sur des serveurs UNIX et Linux dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Avant de pouvoir gérer un serveur Linux ou UNIX avec System Center Configuration Manager, vous devez installer le client Configuration Manager pour Linux et UNIX sur chaque serveur Linux ou UNIX. Vous pouvez soit installer manuellement le client sur chaque ordinateur, soit utiliser un script Shell qui installe le client à distance. Configuration Manager ne prend pas en charge l’installation Push du client pour les serveurs Linux ou UNIX. Vous pouvez éventuellement configurer un Runbook pour System Center Orchestrator pour automatiser l’installation du client sur le serveur Linux ou UNIX.  

 Quelle que soit la méthode d’installation utilisée, le processus d’installation nécessite un script nommé **install** pour gérer le processus d’installation. Ce script est inclus lorsque vous téléchargez le Client pour Linux et UNIX.  

 Le script d’installation pour le client Configuration Manager pour Linux et UNIX prend en charge les propriétés de ligne de commande. Certaines propriétés de ligne de commande sont requises, tandis que d'autres sont facultatives. Par exemple, lorsque vous installez le client, vous devez spécifier un point de gestion à partir du site est utilisé par le serveur Linux ou UNIX pour son contact initial avec le site. Pour obtenir la liste complète des propriétés de ligne de commande, consultez [Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX](#BKMK_CmdLineInstallLnUClient).  

 Après avoir installé le client, spécifiez les paramètres du client dans la console Configuration Manager pour configurer l’agent du client. Suivez la même procédure que pour un client Windows. Pour plus d’informations, consultez [Paramètres client pour les serveurs Linux et UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="BKMK_AboutInstallPackages"></a> À propos des Packages d'Installation de Client et l'Agent universel  
 Pour installer le client pour Linux et UNIX sur une plateforme spécifique, vous devez utiliser le package d’installation du client applicable pour l’ordinateur sur lequel vous installez le client. Les packages d’installation de client applicables sont inclus dans chaque téléchargement du client effectué à partir du [Centre de téléchargement Microsoft](http://go.microsoft.com/fwlink/?LinkID=525184). En plus des packages d’installation de client, le téléchargement du client comprend le script **install** qui gère l’installation du client sur chaque ordinateur.  

 Lorsque vous installez un client, vous pouvez utiliser les mêmes propriétés de processus et de ligne de commande que vous utilisez le package d'installation client.  

 Pour plus d’informations sur les systèmes d’exploitation, les plateformes et les packages d’installation de client pris en charge par chaque version du client Configuration Manager pour Linux et UNIX, consultez [Serveurs Linux et UNIX](/sccm/core/plan-design/configs/supported-operating-systems-for-clients-and-devices#linux-and-unix-servers).  

##  <a name="BKMK_InstallLnUClient"></a> Installer le Client sur des serveurs Linux et UNIX  
 Pour installer le client pour Linux et UNIX, vous exécutez un script sur chaque ordinateur Linux ou UNIX. Le script est nommé **installer** et prend en charge les propriétés de ligne de commande qui modifient le comportement d'installation et de référencent le package d'installation du client. Le package d'installation installation script et le client doit se trouver sur le client. Le package d’installation client contient les fichiers du client Configuration Manager pour une plate-forme et un système d’exploitation Linux ou UNIX spécifiques.
Chaque package d'installation du client contient tous les fichiers nécessaires pour terminer l'installation du client et contrairement aux ordinateurs fonctionnant sous Windows, ne pas télécharge des fichiers supplémentaires à partir d'un point de gestion ou un autre emplacement source.  

 Après avoir installé le client Configuration Manager pour Linux et UNIX, vous n’avez pas besoin de redémarrer l’ordinateur. Dès que l'installation est terminé, le client est opérationnel. Si vous redémarrez l’ordinateur, le client Configuration Manager redémarre automatiquement.  

 Le client installé s'exécute avec les informations d'identification racine. Des informations d’identification racine sont nécessaires pour collecter l’inventaire matériel et effectuer les déploiements de logiciels.  

 Le format de la commande est le suivant :  

 **./install -mp &lt;ordinateur\> -sitecode &lt;code_site\> &lt;propriété 1> &lt;propriété 2> &lt;package d’installation du client\>**  

-   **installer** est le nom du fichier de script qui installe le client pour Linux et UNIX. Ce fichier est fourni avec le logiciel client.  

-   **-mp &lt;ordinateur** spécifie le point de gestion initial utilisé par le client.  

     Exemple : smsmp.contoso.com  

-   **-sitecode &lt;code_site\>** spécifie le code de site auquel le client est affecté.  

     Exemple : S01  

-   &lt;propriété 1> &lt;propriété 2> spécifie les propriétés de ligne de commande à utiliser avec le script d’installation.  

    > [!NOTE]  
    >  Pour plus d’informations, consultez [Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX](#BKMK_CmdLineInstallLnUClient)  

-   **package d’installation du client** est le nom du package .tar d’installation du client pour le système d’exploitation, la version et l’architecture d’UC de l’ordinateur. Le fichier .tar d'installation client doit être spécifié en dernier.  

     Exemple : ccm-Universal-x64.&lt;build\>.tar  

###  <a name="BKMK_ToInstallLnUClinent"></a> Pour installer le Client Configuration Manager sur des serveurs Linux et UNIX  

1.  Sur un ordinateur Windows, [téléchargez le fichier client approprié pour le serveur Linux ou UNIX](http://go.microsoft.com/fwlink/?LinkID=525184) que vous souhaitez gérer.  

2.  Exécutez le fichier .exe à extraction automatique sur l’ordinateur Windows pour extraire le script d’installation et le fichier .tar d’installation du client.  

3.  Copiez le script d’ **installation** et le fichier .tar dans un dossier sur le serveur que vous souhaitez gérer.  

4.  Sur le serveur UNIX ou Linux, exécutez la commande suivante pour autoriser le script à s’exécuter comme un programme : **chmod +x install**  

    > [!IMPORTANT]  
    >  Vous devez utiliser des informations d'identification racine pour installer le client.  

5.  Ensuite, exécutez la commande suivante pour installer le client Configuration Manager : **./install –mp &lt;nom_hôte\> -sitecode &lt;code\> ccm-Universal-x64.&lt;build\>.tar**  

     Lorsque vous entrez cette commande, utilisez les propriétés de ligne de commande supplémentaires que vous avez besoin.  Pour obtenir la liste des propriétés de ligne de commande, consultez [Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX](#BKMK_CmdLineInstallLnUClient).  

6.  Une fois le script exécuté, validez l’installation en examinant le fichier **/var/opt/microsoft/scxcm.log** . De plus, vous pouvez vérifier que le client est installé et qu’il communique avec le site en affichant les détails relatifs au client dans le nœud **Appareils** de l’espace de travail **Ressources et Conformité** dans la console Configuration Manager.  

###  <a name="BKMK_CmdLineInstallLnUClient"></a> Propriétés de ligne de commande pour installer le client sur des serveurs Linux et UNIX  
 Les propriétés suivantes sont disponibles pour modifier le comportement du script d’installation :  

> [!NOTE]  
>  Utilisez la propriété **-h** pour afficher la liste des propriétés prises en charge.  

-   **-mp &lt;nom_de_domaine_complet_du_serveur\>**  

     Obligatoire. Spécifie le nom de domaine complet, le serveur de point de gestion que le client utilisera comme un point de contact initial.  

    > [!IMPORTANT]  
    >  Cette propriété n’indique pas le point de gestion auquel le client sera attribué après l’installation.  

    > [!NOTE]  
    >  Quand vous utilisez la propriété **-mp** pour spécifier un point de gestion qui est configuré pour accepter uniquement les connexions client HTTPS, vous devez également employer la propriété **-UsePKICert** .  

-   **-sitecode &lt;code_site\>**  

     Obligatoire. Spécifie le site principal Configuration Manager auquel attribuer le client Configuration Manager.  

     Exemple : -sitecode S01  

-   **-fsp &lt;nom_de_domaine_complet_du_serveur>**  

     Facultatif. Spécifie le nom de domaine complet, le serveur de point d'état de secours que le client utilise pour envoyer des messages d'état.  

     Pour plus d’informations sur le point d’état de secours, consultez [Determine Whether You Require a Fallback Status Point](/sccm/core/clients/deploy/plan/determine-the-site-system-roles-for-clients#determine-if-you-need-a-fallback-status-point) .  


-   **-dir &lt;répertoire\>**  

     Facultatif. Spécifie un autre emplacement pour installer les fichiers du client Configuration Manager.  

     Par défaut, le client est installé à l'emplacement suivant : **/opt/microsoft**.  

-   **-nostart**  

     Facultatif. Empêche le démarrage automatique du service client Configuration Manager, **ccmexec.bin**, après l’installation du client.  

     Une fois le client installé, vous devez démarrer manuellement le service client.  

     Par défaut, le service client démarre après la fin de l'installation du client, et chaque fois que l'ordinateur redémarre.  

-   **-nettoyage**  

     Facultatif. Spécifie la suppression de tous les fichiers du client et les données à partir d'un client installé précédemment pour Linux et UNIX, avant le démarrage de la nouvelle installation. Cela supprime le magasin de certificats et la base de données du client.  

-   **-keepdb n' n'**  

     Facultatif. Spécifie que la base de données client local est conservée et réutilisée, lorsque vous réinstallez un client. Par défaut, lorsque vous réinstallez un client de cette base de données est supprimé.  

-   **-UsePKICert &lt;paramètre\>**  

     Facultatif. Spécifie le chemin d'accès et le nom complet à un certificat X.509 PKI au format Public Key Certificate Standard (PKCS #12). Ce certificat est utilisé pour l'authentification du client. Si aucun certificat n’est spécifié pendant l’installation et que vous devez en ajouter ou en modifier un, faites appel à l’utilitaire **certutil** . Pour plus d’informations sur certutil, consultez [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) .  

     Quand vous utilisez **-UsePKICert**, vous devez également fournir le mot de passe associé au fichier PKCS #12 à l’aide du paramètre de ligne de commande **-certpw** .  

     Si vous n'utilisez pas cette propriété pour spécifier un certificat PKI, le client utilise un certificat auto-signé et sont des systèmes de site de toutes les communications via HTTP.  

     Si vous spécifiez un certificat non valide sur le client installation de ligne de commande, aucune erreur n'est retournée. Il s'agit, car la validation de certificat se produit après l'installation du client. Lorsque le client démarre, les certificats sont validés avec le point de gestion et si un certificat de validation échoue le message suivant apparaît dans **scxcm.log**, le fichier journal du client Unix et Linux Configuration Manager : **Échec de valider le certificat de Point de gestion**. L’emplacement par défaut du fichier journal est :  **/var/opt/microsoft/scxcm.log**.  

    > [!NOTE]  
    >  Vous devez spécifier cette propriété quand vous installez un client et utiliser la propriété **-mp** pour indiquer un point de gestion qui est configuré pour accepter uniquement les connexions client HTTPS.  

     Exemple : -UsePKICert &lt;chemin_complet_et_nom_de_fichier\> -certpw &lt;mot_de_passe\>  

-   **-certpw &lt;paramètre\>**  

     Facultatif. Spécifie le mot de passe associé au fichier PKCS #12 que vous avez spécifié à l'aide de la **- /usepkicert** propriété.  

     Exemple : -UsePKICert &lt;chemin_complet_et_nom_de_fichier\> -certpw &lt;mot_de_passe\>  

-   **-/Nocrlcheck**  

     Facultatif. Spécifie qu'un client ne doit pas vérifier la liste de révocation de certificats (CRL) lorsqu'il communique via HTTPS à l'aide d'un certificat PKI. Lorsque cette option n'est pas spécifiée, le client vérifie la révocation de certificats avant d'établir une connexion HTTPS à l'aide de certificats PKI. Pour plus d'informations sur la vérification de révocation de certificats client, consultez Planification de la révocation de certificats PKI.  

     Exemple : -UsePKICert &lt;chemin_complet_et_nom_de_fichier\> -certpw &lt;mot_de_passe\> -NoCRLCheck  

-   **-rootkeypath &lt;emplacement_fichier\>**  

     Facultatif. Spécifie le chemin d’accès complet et le nom de fichier de la clé racine approuvée Configuration Manager. La clé racine approuvée Configuration Manager fournit un mécanisme que les clients Linux et UNIX utilisent pour vérifier qu’ils sont connectés à un système de site qui appartient à la hiérarchie appropriée.  

     Si vous ne spécifiez pas la clé racine approuvée sur la ligne de commande, le client approuve le premier point de gestion avec lequel il communique et récupère automatiquement la clé racine approuvée à partir de ce point de gestion.  

     Pour plus d’informations, consultez  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Exemple : -rootkeypath \>chemin_complet_et_nom_de_fichier&lt;  

-   **-httpport &lt;port\>**  

     Facultatif. Spécifie le port est configuré sur les points de gestion que le client utilise lors de la communication aux points de gestion via HTTP. Si le port n'est pas spécifié, la valeur par défaut 80 est utilisée.  

     Exemple : -httpport 80  

-   **-httpsport &lt;port\>**  

     Facultatif. Spécifie le port est configuré sur les points de gestion que le client utilise lors de la communication aux points de gestion via HTTPS. Si le port n'est pas spécifié, la valeur par défaut 443 est utilisée.  

     Exemple : -UsePKICert &lt;chemin_complet_et_nom_de_certificat\> -httpsport 443  

-   **-ignoreSHA256validation**  

     Facultatif. Spécifie que l'installation du client ignore la validation de l'algorithme SHA-256. Utilisez cette option quand vous installez le client sur des systèmes d’exploitation publiés avec une version d’OpenSSL qui ne prend pas en charge SHA-256. Pour plus d’informations, voir [About Linux and UNIX Operating Systems That do not Support SHA-256](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   **-signcertpath &lt;emplacement_fichier\>**  

     Facultatif. Spécifie le chemin d'accès complet et **.cer** nom de fichier du certificat auto-signé exporté sur le serveur de site. Si les certificats PKI ne sont pas disponibles, le serveur de site Configuration Manager génère automatiquement des certificats auto-signés.  

     Ces certificats sont utilisés pour valider que les stratégies client téléchargés à partir du point de gestion ont été envoyés à partir du site de destination. Si aucun certificat auto-signé n’est spécifié pendant l’installation ou que vous devez modifier le certificat, faites appel à l’utilitaire **certutil** . Pour plus d’informations sur certutil, consultez [How to manage certificates on the client for Linux and UNIX](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts) .  

     Ce certificat, qui peut être récupéré dans le magasin de certificats **SMS** , porte le nom d’objet **Serveur de site** et le nom convivial **Certificat de signature du serveur de site**.  

     Si cette option n'est pas spécifiée lors de l'installation, les clients Linux et UNIX approuvent le premier point de gestion qu'ils communiquent avec et récupère automatiquement le certificat de signature à partir de ce point de gestion.  

     Exemple : -signcertpath &lt;chemin_complet_et_nom_de_fichier\>  

-   **-rootcerts**  

     Facultatif. Spécifie les autres certificats PKI pour importer qui ne font pas partie d'une hiérarchie d'autorité de certification gestion des points. Si vous spécifiez plusieurs certificats dans la ligne de commande, ils doivent être séparés par des virgules.  

     Utilisez cette option si vous utilisez des certificats clients PKI qui ne se lient pas à un certificat d'autorité de certification racine approuvée par les points de gestion de vos sites. Les points de gestion rejettent le client si le certificat client n’est pas associé à un certificat racine approuvé dans la liste des émetteurs de certificat du site.  

     Si vous n'utilisez pas cette option, le client Linux et UNIX vérifiera la hiérarchie d'approbation en utilisant uniquement le certificat dans le **- /usepkicert** option.  

     Exemple : -rootcerts &lt;chemin_complet_et_nom_de_fichier\>,&lt;chemin_complet_et_nom_de_fichier\>  

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

 Pour plus d’informations sur la manière dont les clients localisent les points de gestion, consultez [Locating Management Points](/sccm/core/clients/deploy/assign-clients-to-a-site#locating-management-points).
