---
title: Mettre à niveau les clients Linux et UNIX
titleSuffix: Configuration Manager
description: Mettez à niveau un client sur un serveur Linux ou UNIX dans Configuration Manager.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 7d2bb377-1005-4a55-bd1f-b80a6d0b22e1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 987014084626e13b09a3c39fe6eff08ecc8fbe6b
ms.sourcegitcommit: d8d142044586a53709b4478ad945f714737c8d6e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58523994"
---
# <a name="how-to-upgrade-clients-for-linux-and-unix-servers-in-configuration-manager"></a>Guide pratique pour mettre à niveau les clients pour des serveurs Linux et UNIX dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

> [!Important]  
> Depuis la version 1902, Configuration Manager ne prend en charge les clients Linux ou UNIX. 
> 
> Utilisez plutôt Microsoft Azure Management pour la gestion des serveurs Linux. Les solutions Azure offrent une prise en charge étendue de Linux qui, dans la plupart des cas, dépasse les fonctionnalités de Configuration Manager, notamment la gestion des correctifs de bout en bout pour Linux.

Vous pouvez mettre à niveau la version du client pour Linux et UNIX vers une version plus récente du client sans désinstaller au préalable le client actuel. Pour cela, installez le nouveau package d’installation du client sur l’ordinateur en utilisant la propriété de ligne de commande **-keepdb**. Quand le client pour Linux et UNIX est installé, il remplace les données du client existantes par les nouveaux fichiers du client. Toutefois, la propriété de ligne de commande **-keepdb** demande au processus d’installation de conserver l’identificateur unique (GUID) du client, la base de données locale d’informations et le magasin de certificats. Ces informations sont ensuite utilisées par la nouvelle installation du client.  

 Par exemple, vous avez un ordinateur RHEL5 x64 qui exécute le client à partir de la version d’origine du client Configuration Manager pour Linux et UNIX. Pour mettre à niveau ce client avec la version du client disponible dans la mise à jour cumulative 1, exécutez manuellement le script **install** pour installer le package du client approprié à partir de la mise à jour cumulative 1, en ajoutant le commutateur de ligne de commande **-keepdb**. Consultez l’exemple de ligne de commande suivante :  

`./install -mp <hostname\> -sitecode <code\> -keepdb ccm-Universal-x64.<build\>.tar`  



## <a name="how-to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Comment utiliser un déploiement de logiciels pour mettre à niveau le client sur des serveurs Linux et UNIX  
 Vous pouvez utiliser un déploiement de logiciels pour mettre à niveau le client sur des serveurs Linux et UNIX vers une nouvelle version du client. Toutefois, le client Configuration Manager ne peut pas exécuter directement le script d’installation pour installer le nouveau client, car l’installation d’un nouveau client doit d’abord désinstaller le client actuel. Cette action entraînerait l’arrêt du processus client Configuration Manager qui exécute le script d’installation avant que l’installation du nouveau client ne commence. Pour pouvoir utiliser un déploiement de logiciels pour installer le nouveau client, vous devez planifier l’installation pour qu’elle commence plus tard et qu’elle soit exécutée par les fonctionnalités de planification intégrées du système d’exploitation.  

 Utilisez un déploiement de logiciels pour d’abord copier les fichiers du nouveau package d’installation de client sur l’ordinateur client. Déployez et exécutez ensuite un script destiné à planifier le processus d’installation du client. Le script utilise la commande **at** intégrée du système d’exploitation pour retarder son démarrage. Quand le script s’exécute, son fonctionnement est géré par le système d’exploitation du client, et non par le client Configuration Manager sur l’ordinateur. Ce comportement permet à la ligne de commande appelée par le script de d’abord désinstaller le client Configuration Manager, puis d’installer le nouveau client. Ces actions terminent le processus de mise à niveau du client sur l’ordinateur UNIX ou Linux. Une fois la mise à niveau terminée, le client mis à niveau continue à être géré par Configuration Manager.  

 Utilisez la procédure suivante pour configurer un déploiement de logiciels destiné à mettre à niveau le client pour Linux et UNIX. Les étapes et exemples suivants mettent à niveau un ordinateur RHEL5 x64 qui exécute la version initiale du client vers la version du client disponible dans la mise à jour cumulative 1.  

#### <a name="to-use-a-software-deployment-to-upgrade-the-client-on-linux-and-unix-servers"></a>Pour utiliser un déploiement de logiciels destiné à mettre à niveau le client sur des serveurs Linux et UNIX  

1. Copiez le nouveau package d’installation du client sur l’ordinateur qui exécute le client Configuration Manager à mettre à niveau.  

    Par exemple, placez le package d’installation du client et le script d’installation de la mise à jour cumulative 1 dans l’emplacement suivant sur l’ordinateur client : **/tmp/PATCH**  

2. Créez un script pour gérer la mise à niveau du client Configuration Manager. Placez ensuite une copie de ce script dans le même dossier sur l’ordinateur client que les fichiers d’installation du client de l’étape 1.  

    Le script ne doit pas obligatoirement porter un nom spécifique. Il doit contenir les lignes de commande nécessaires pour utiliser les fichiers d’installation du client à partir d’un dossier local sur l’ordinateur client et installer le package d’installation du client à l’aide de la propriété de ligne de commande **-keepdb**. Utilisez la propriété de ligne de commande **-keepdb** pour conserver l’identificateur unique du client actuel afin qu’il soit utilisé par le nouveau client que vous installez.  

    Par exemple, créez un script nommé **upgrade.sh** contenant les lignes suivantes :  

   ```  
   #!/bin/sh  
   #  
   /tmp/PATCH/install -sitecode <code> -mp <hostname> -keepdb /tmp/PATCH/ccm-Universal-x64.<build>.tar  

   ```  

    Copiez-le ensuite dans le dossier **/tmp/PATCH** sur l’ordinateur client.

3. Utilisez le déploiement de logiciels pour que chaque client utilise la commande **at** intégrée de l’ordinateur pour exécuter le script **upgrade.sh** avec un court délai avant l’exécution du script.  

    Par exemple, utilisez la ligne de commande suivante pour exécuter le script : **at -f /tmp/upgrade.sh -m now + 5 minutes**  

   Une fois que le client a correctement planifié l’exécution du script **upgrade.sh** , le client envoie un message d’état indiquant que le déploiement de logiciels s’est terminé avec succès. Toutefois, l’installation du client actuel est ensuite gérée par l’ordinateur, une fois le délai écoulé. Une fois la mise à niveau du client terminée, validez l’installation en consultant le fichier **/var/opt/microsoft/scxcm.log** sur l’ordinateur client. Vérifiez que le client est installé et qu’il communique avec le site en affichant les détails relatifs au client dans le nœud **Appareils** de l’espace de travail **Ressources et Conformité** dans la console Configuration Manager.  
