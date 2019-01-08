---
title: Créer des applications serveur Linux et UNIX
titleSuffix: Configuration Manager
description: Examinez les éléments à prendre en compte quand vous créez et déployez des applications pour appareils Linux et Unix.
ms.date: 04/13/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 12a3bffb48cba2e3f258d06489b7511d05b7daad
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53422077"
---
# <a name="create-linux-and-unix-server-applications-with-system-center-configuration-manager"></a>Créer des applications serveur Linux et UNIX avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Prenez en compte les points suivants quand vous créez et déployez des applications pour des ordinateurs qui exécutent Linux et UNIX.  

## <a name="general-considerations"></a>Considérations générales  
 Le client Configuration Manager pour Linux et UNIX prend en charge les **déploiements logiciels qui utilisent des packages et des programmes**. Vous ne pouvez pas déployer d’applications Configuration Manager sur des ordinateurs exécutant Linux et UNIX.  

 Le déploiement de logiciels Linux et UNIX inclut les possibilités suivantes :  

-   l’installation de logiciels pour des serveurs Linux et UNIX, notamment :  

    -   un déploiement de nouveaux logiciels ;  

    -   des mises à jour logicielles pour les programmes qui sont déjà installés sur un ordinateur ;  

    -   des correctifs de système d'exploitation.  

-   des commandes Linux et UNIX natives, et des scripts situés sur des serveurs Linux et UNIX  

-   des déploiements qui sont limités aux systèmes d’exploitation que vous spécifiez en sélectionnant l’option de programme **Uniquement sur les plateformes clientes spécifiées**

-   les fenêtres de maintenance pour contrôler à quel moment le logiciel s’installe

-   les messages d’état de déploiement pour contrôler les déploiements  

-   l’option permettant au client d’accélérer l’utilisation du réseau quand il télécharge des logiciels à partir d’un point de distribution  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Différences entre le déploiement sur des ordinateurs Linux et UNIX et le déploiement sur des appareils Windows
Les principales différences entre le déploiement de packages et de programmes sur des ordinateurs Linux et UNIX et le déploiement de packages et de programmes sur des appareils Windows sont les suivantes :  

|Configuration|Détails|  
|-------------------|-------------|  
|Utilisez uniquement des configurations destinées aux ordinateurs et non aux utilisateurs.|Le client Configuration Manager pour Linux et UNIX ne prend pas en charge les configurations destinées aux utilisateurs.|  
|Configurez les programmes de sorte qu’ils téléchargent les logiciels à partir du point de distribution et exécutez les programmes à partir du cache du client local.|Le client Configuration Manager pour Linux et UNIX ne prend pas en charge l’exécution de logiciels à partir du point de distribution. Vous devez configurer les logiciels de sorte qu’ils soient téléchargés sur le client, puis installés.<br /><br /> Par défaut, une fois que le client pour Linux et UNIX a installé un logiciel, celui-ci est supprimé de la mémoire cache du client. Toutefois, les packages configurés avec l'option **Conserver le contenu dans la mémoire cache du client** ne sont pas supprimés du client et restent dans sa mémoire cache une fois le logiciel installé.<br /><br /> Le client pour Linux et UNIX ne prend pas en charge les configurations de la mémoire cache du client, et la taille maximale de celle-ci est seulement limitée par l'espace disque disponible sur l'ordinateur client.|  
|Configurez le compte d'accès réseau pour l'accès au point de distribution.|Les ordinateurs Linux et UNIX sont conçus pour être des ordinateurs de groupe de travail. Pour accéder aux packages à partir du point de distribution dans le domaine du serveur de site Configuration Manager, vous devez configurer le compte d’accès réseau pour le site. Vous devez spécifier ce compte en tant que propriété de composant de distribution de logiciels et configurer le compte avant de déployer des logiciels.<br /><br /> Vous pouvez configurer plusieurs comptes d'accès réseau sur chaque site. Le client pour Linux et UNIX peut utiliser chacun des comptes que vous configurez comme un compte d'accès réseau.<br /><br /> Pour plus d'informations, voir [Site components for System Center Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Vous pouvez déployer des packages et des programmes vers des regroupements qui contiennent uniquement des clients Linux ou UNIX ou vers des regroupements qui contiennent une combinaison de types de client, tels que le **regroupement Tous les systèmes**. Toutefois, les clients non-Linux et non-UNIX n’installent pas les logiciels ou ne font pas état de l’échec.  

 Quand le client Configuration Manager pour Linux et UNIX reçoit et exécute un déploiement, il génère des messages d’état. Vous pouvez afficher ces messages d’état dans la console Configuration Manager ou en utilisant des rapports destinés à surveiller l’état du déploiement.  

 Pour plus d’informations sur l’utilisation de packages et de programmes, consultez [Packages et programmes](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Configurer des packages, programmes et déploiements pour les serveurs UNIX et Linux  
 Vous pouvez créer et déployer des packages et des programmes en utilisant les options par défaut disponibles dans la console Configuration Manager. Le client n'impose pas de configurations uniques.  

 Pour configurer les packages, les programmes et les déploiements, aidez-vous des informations figurant dans les sections suivantes.  

### <a name="packages-and-programs"></a>Packages et programmes  
 Pour créer un package et un programme pour un serveur Linux ou UNIX, utilisez l’**Assistant Création d’un package et d’un programme** à partir de la console Configuration Manager. Le client pour Linux et UNIX prend en charge la plupart des paramètres de package et de programme. Toutefois, certains ne sont pas pris en charge. Lorsque vous créez ou configurez un package et un programme, tenez compte des points suivants :  

-   Incluez les types de fichiers pris en charge par les ordinateurs de destination.  

-   Définissez les lignes de commande qu’il est approprié d’utiliser sur l’ordinateur de destination.  

-   Gardez à l’esprit que les paramètres qui interagissent avec les utilisateurs ne sont pas pris en charge.  

Le tableau suivant répertorie les propriétés pour packages et programmes qui ne sont pas prises en charge :  

|Propriété de package et de programme|Comportement|Informations complémentaires|  
|----------------------------------|--------------|----------------------|  
|Paramètres de partage de package :<br /><br /> - Toutes les options|Une erreur est générée et l’installation du logiciel échoue.|Le client ne prend pas en charge cette configuration. Au lieu de cela, le client doit télécharger le logiciel à l'aide du protocole HTTP ou HTTPS, puis exécuter la ligne de commande à partir de sa mémoire cache locale.|  
|Paramètres de mise à jour de package :<br /><br /> - Déconnecter les utilisateurs des points de distribution|Les paramètres sont ignorés.|Le client ne prend pas en charge cette configuration.|  
|Paramètres de déploiement du système d'exploitation :<br /><br /> - Toutes les options|Les paramètres sont ignorés.|Le client ne prend pas en charge cette configuration.|  
|Rapports :<br /><br /> - Utiliser prop. package pr. corresp. fichiers MIF d’état<br /><br /> - Utiliser ces champs pour la correspondance des fichiers MIF d’état|Les paramètres sont ignorés.|Le client ne prend pas en charge l'utilisation de fichiers MIF d'état.|  
|**Exécuter**:<br /><br /> - Toutes les options|Les paramètres sont ignorés.|Le client exécute toujours les packages sans aucune interface utilisateur.<br /><br /> Le client ignore toutes les options de configuration de l'exécution.|  
|Après l'exécution :<br /><br />- Configuration Manager redémarre l’ordinateur<br /><br /> - Le programme contrôle le redémarrage<br /><br /> - Configuration Manager déconnecte l’utilisateur|Une erreur est générée et l’installation du logiciel échoue.|Le paramètre de redémarrage du système et les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Lorsque le paramètre utilisé n'est pas **Aucune action requise** , le client génère une erreur et poursuit l'installation du logiciel, sans qu'aucune action ne soit effectuée.|  
|Le programme peut s'exécuter :<br /><br /> - Uniquement quand un utilisateur est connecté|Une erreur est générée et l’installation du logiciel échoue.|Les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Lorsque cette option est configurée, le client génère une erreur et fait échouer l'installation du logiciel.<br /><br /> Les autres options sont ignorées et l'installation du logiciel se poursuit.|  
|Mode d'exécution :<br /><br /> - Exécuter avec les droits d’utilisateur|Les paramètres sont ignorés.|Les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Toutefois, le client prend en charge l’exécution de la configuration avec des droits d’administration.<br /><br /> Quand vous spécifiez **Exécuter avec les droits d’administration**, le client Configuration Manager utilise ses informations d’identification racines.<br /><br /> Ce paramètre ne génère pas d'erreur ni d'entrée de journal. En revanche, l’installation du logiciel échoue quand le client génère une erreur pour la configuration requise **Le programme peut s’exécuter** = **Uniquement lorsqu’un utilisateur est connecté**.|  
|Permettre aux utilisateurs d’afficher et d’interagir avec l’installation du programme|Les paramètres sont ignorés.|Les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Cette configuration est ignorée et l'installation du logiciel se poursuit.|  
|Mode lecteur :<br /><br /> - Toutes les options|Les paramètres sont ignorés.|Ce paramètre n'est pas pris en charge, car le contenu est toujours téléchargé sur le client et exécuté localement.|  
|Exécuter un autre programme en premier|Une erreur est générée et l’installation du logiciel échoue.|L'installation récursive de programmes n'est pas prise en charge.<br /><br /> Lorsqu'un programme est configuré pour exécuter préalablement un autre programme, l'installation du logiciel échoue et l'installation de l'autre programme ne démarre pas.|  
|Lorsque ce programme est attribué à un ordinateur :<br /><br /> - Exécuter une fois pour chaque utilisateur qui se connecte|Les paramètres sont ignorés.|Les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Toutefois, le client prend en charge l’exécution de la configuration une fois pour l’ordinateur.<br /><br /> Ce paramètre ne génère pas d'erreur ni d'entrée de journal, car il en a déjà été créée pour la configuration requise de **Le programme peut s'exécuter** = **Uniquement quand un utilisateur a ouvert une session**.|  
|Supprimer les notifications de programmes|Les paramètres sont ignorés.|Le client n'implémente pas d'interface utilisateur.<br /><br /> Lorsque cette configuration est sélectionnée, elle est ignorée et l'installation du logiciel se poursuit.|  
|Désactiver ce programme sur les ordinateurs sur lesquels il est déployé|Les paramètres sont ignorés.|Ce paramètre n'est pas pris en charge et n'a pas d'incidence sur l'installation du logiciel.|  
|Autoriser l'installation de ce programme depuis la séquence de tâches d'installation du package sans le déployer||Le client ne prend pas en charge les séquences de tâches.<br /><br /> Ce paramètre n'est pas pris en charge et n'a pas d'incidence sur l'installation du logiciel.|  
|Windows Installer :<br /><br /> - Toutes les options|Les paramètres sont ignorés.|Le client ne prend pas en charge les fichiers ni les paramètres Windows Installer.|  
|Mode de maintenance OpsMgr :<br /><br /> - Toutes les options|Les paramètres sont ignorés.|Le client ne prend pas en charge cette configuration.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Déployer un logiciel sur un serveur Linux ou UNIX
 Pour déployer un logiciel sur un serveur Linux ou UNIX à l’aide d’un package et d’un programme, vous pouvez utiliser l’**Assistant Déploiement logiciel** de la console Configuration Manager. Le client pour Linux et UNIX prend en charge la plupart des paramètres de déploiement. Cela n’est toutefois pas le cas pour certains paramètres. Lors du déploiement d’un logiciel, tenez compte des points suivants :  

- Vous devez préparer le package sur au moins un point de distribution associé à un groupe de limites configuré pour l'emplacement du contenu.  

- Le client pour Linux et UNIX qui reçoit ce déploiement doit être en mesure d’accéder à ce point de distribution à partir de son emplacement réseau.  

- Le client pour Linux et UNIX télécharge le package à partir du point de distribution et exécute le programme sur l'ordinateur local.  

- Le client pour Linux et UNIX ne peut pas télécharger de packages à partir de dossiers partagés. Il télécharge les packages à partir de points de distribution compatibles IIS qui prennent en charge le protocole HTTP ou HTTPS.  

  Le tableau suivant répertorie les propriétés destinées aux déploiements non prises en charge :  

|Propriété de déploiement|Comportement|Informations complémentaires|  
|-------------------------|--------------|----------------------|  
|Paramètres de déploiement – objet :<br /><br /> - Disponible<br /><br /> - Obligatoire|Les paramètres sont ignorés.|Les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Toutefois, le client prend en charge le paramètre **Obligatoire**, qui applique l'heure d'installation planifiée, mais toute installation manuelle avant cette heure planifiée n'est pas prise en charge.|  
|Envoyer des paquets de mise en éveil|Les paramètres sont ignorés.|Le client ne prend pas en charge cette configuration.|  
|Calendrier d'attribution :<br /><br /> - ouverture de session<br /><br /> - fermeture de session|Une erreur est générée et l’installation du logiciel échoue.|Les paramètres spécifiques à l’utilisateur ne sont pas pris en charge.<br /><br /> Toutefois, le client prend en charge le paramètre **Dès que possible**.|  
|Paramètres de notification :<br /><br /> - Autoriser les utilisateurs à exécuter le programme indépendamment des attributions|Les paramètres sont ignorés.|Le client n'implémente pas d'interface utilisateur.|  
|Lorsque l'heure d'attribution planifiée est atteinte, autorisez l'exécution des activités suivantes en dehors de la fenêtre de maintenance :<br /><br /> - Redémarrage du système (si nécessaire pour terminer l’installation)|Une erreur est générée.|Le client ne prend pas en charge un redémarrage du système.|  
|Option de déploiement pour les réseaux (LAN) rapides :<br /><br /> - Exécuter le programme à partir du point de distribution|Une erreur est générée et l’installation du logiciel échoue.|Le client ne peut pas exécuter le logiciel à partir du point de distribution et doit au lieu de cela télécharger le programme avant de pouvoir l'exécuter.|  
|Option de déploiement pour une limite réseau lente ou non fiable ou un emplacement source de secours pour le contenu :<br /><br /> - Autoriser les clients à partager du contenu avec d’autres clients sur le même sous-réseau|Les paramètres sont ignorés.|Le client ne prend pas en charge le partage de contenu entre homologues.|  

 Pour plus d’informations sur l’emplacement du contenu, consultez [Gérer le contenu et l’infrastructure de contenu pour System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Pour plus d’informations sur la création d’un déploiement, consultez [Déployer des applications](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>Gérer la bande passante réseau pour les téléchargements de logiciels à partir de points de distribution  
 Le client Linux et UNIX prend en charge les contrôles de bande passante réseau quand il télécharge des logiciels à partir d’un point de distribution.  

 Le client utilise les paramètres de service de transfert intelligent en arrière-plan (BITS) que vous configurez comme paramètres du client dans Configuration Manager, mais il n’implémente pas BITS. Au lieu de cela, pour accélérer l'utilisation de la bande passante réseau, le client contrôle la taille du bloc de la demande HTTP et le délai intra-bloc pour le téléchargement de logiciels.  

 Pour configurer l'utilisation des contrôles de bande passante réseau par un client, configurez les paramètres clients pour **Transfert intelligent en arrière-plan** , puis appliquez les paramètres à l'ordinateur client. Pour utiliser les contrôles de bande passante, le client doit recevoir des paramètres du client pour **Transfert intelligent en arrière-plan** avec les paramètres suivants configurés sur **Oui** :  

- **Limiter la bande passante réseau maximale pour les transferts BITS en arrière-plan**  

  Le client prend en charge les configurations suivantes pour le Transfert intelligent en arrière-plan :  

  -   **Heure de début de la fenêtre de limitation**  

  -   **Heure de fin de la fenêtre de limitation**  

  -   **Taux de transfert maximal dans la fenêtre de limitation (Kbit/s)**  

  -   **Taux de transfert maximal en dehors de la fenêtre de limitation (Kbit/s)**  

La configuration suivante pour le Transfert intelligent en arrière-plan n'est pas prise en charge et est ignorée par le client pour Linux et UNIX :  

- **Autoriser les téléchargements BITS en dehors de la fenêtre de limitation**  

  Si le téléchargement de logiciels vers le client à partir d’un point de distribution est interrompu, le client pour Linux et UNIX ne reprend pas le téléchargement. Au lieu de cela, il redémarre le téléchargement de l’ensemble du package logiciel.  

##  <a name="configure-operations-for-software-deployments"></a>Configurer des opérations pour les déploiements de logiciels  
 À l’instar du client Windows, le client Configuration Manager pour Linux et UNIX détecte les nouveaux déploiements de logiciels en sondant et recherchant une nouvelle stratégie. La fréquence à laquelle le client recherche une nouvelle stratégie dépend de ses paramètres. Vous pouvez configurer les fenêtres de maintenance de façon à contrôler à quels moments les déploiements de logiciels se produisent.  

 Vous pouvez configurer les déploiements de logiciels sur les serveurs Linux et UNIX à partir des propriétés de package, de programme et de déploiement.  

 Lorsque le client reçoit la stratégie d'un déploiement, il envoie un message d'état. De même, il envoie des messages d’état quand il démarre l’installation d’un logiciel et que l’installation se termine ou échoue.  

 Dans le cadre des déploiements logiciels, les programmes s’exécutent avec les informations d’identification racines avec lesquelles le client Configuration Manager pour Linux et UNIX s’exécute. Le code de sortie de la commande du programme permet de déterminer la réussite ou l'échec de l'opération. Le code de sortie 0 (zéro) est considéré comme un succès. Par ailleurs, le flux de sortie standard (**stdout**) et le flux d'erreurs standard (**stderr**) sont copiés dans le fichier journal lorsque le niveau de journal est défini sur INFO ou TRACE.  

> [!TIP]  
>  Si le logiciel que vous voulez déployer est situé sur un partage NFS (Network File System) accessible au serveur Linux ou UNIX, vous n'avez pas besoin d'utiliser de point de distribution pour télécharger le package. En revanche, au moment de créer le package, n'activez pas la case à cocher **Ce package contient des fichiers sources**. Ensuite, lors de la configuration du programme, spécifiez la ligne de commande appropriée pour accéder directement au package sur le point de montage NFS.  
