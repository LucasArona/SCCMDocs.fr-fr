---
title: Sécurité et confidentialité du déploiement de systèmes d’exploitation
titleSuffix: Configuration Manager
description: Découvrez les bonnes pratiques en matière de sécurité et de confidentialité pour le déploiement de systèmes d’exploitation dans System Center Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4ec1457fafabe2e40106ec76310d9ff64b2aa267
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32351732"
---
# <a name="security-and-privacy-for-operating-system-deployment-in-system-center-configuration-manager"></a>Sécurité et confidentialité du déploiement de systèmes d’exploitation dans System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cette rubrique contient des informations de sécurité et de confidentialité pour le déploiement de systèmes d’exploitation dans System Center Configuration Manager.  

##  <a name="BKMK_Security_HardwareInventory"></a> Bonnes pratiques de sécurité pour le déploiement de systèmes d’exploitation  
 Utilisez les bonnes pratiques de sécurité suivantes lorsque vous déployez des systèmes d’exploitation avec Configuration Manager :  

-   **Instaurez des contrôles d’accès pour protéger les médias de démarrage**  

     Lorsque vous créez un média de démarrage, attribuez toujours un mot de passe pour sécuriser le média. Toutefois, même avec un mot de passe, seuls les fichiers qui contiennent des informations sensibles sont cryptés et tous les fichiers peuvent être remplacés.  

     Contrôlez l'accès physique au média pour qu'une personne malveillante ne puisse pas recourir à des attaques par chiffrement pour obtenir le certificat d'authentification du client.  

     Pour empêcher un client d’installer une stratégie client ou un contenu falsifié, le contenu est haché et doit être utilisé avec la stratégie d’origine.  Si le hachage de contenu échoue ou si la vérification détecte que le contenu correspond à la stratégie, le client n'utilise pas le média de démarrage. Seul le contenu est haché : la stratégie ne l'est pas. En revanche, elle est chiffrée et sécurisée lorsque vous spécifiez un mot de passe, ce qui rend la modification de la stratégie plus complexe pour les éventuels intrus.  

-   **Utilisez un emplacement sécurisé lorsque vous créez des médias pour des images de système d’exploitation**  

     Si des utilisateurs non autorisés ont accès à l'emplacement, ils peuvent falsifier les fichiers que vous créez et utiliser tout l'espace disque disponible pour faire échouer la création des médias.  

-   **Protégez les fichiers de certificat (.pfx) avec un mot de passe fort et, si vous les stockez sur le réseau, sécurisez le canal de réseau lorsque vous les importez dans Configuration Manager**  

     Lorsque vous avez besoin d'un mot de passe pour importer le certificat d'authentification client que vous utilisez pour des médias de démarrage, cela permet de protéger le certificat contre une personne malveillante.  

     Utilisez la signature SMB ou IPsec entre l'emplacement réseau et le serveur de site pour empêcher un intrus de falsifier le fichier de certificat.  

-   **Si le certificat client est compromis, bloquez ce certificat à partir de Configuration Manager et révoquez-le s’il s’agit d’un certificat PKI**  

     Pour déployer un système d'exploitation à l'aide d'un média de démarrage et un démarrage PXE, vous devez disposer d'un certificat d'authentification client avec une clé privée. Si ce certificat est compromis, bloquez le certificat dans le nœud **Certificats** de l'espace de travail **Administration** , nœud **Sécurité** .  

-   **Lorsque le fournisseur SMS se trouve sur un ou plusieurs ordinateurs autres que le serveur de site, sécurisez le canal de communication pour protéger les images de démarrage**  

     Lorsque des images de démarrage sont modifiées et que le fournisseur SMS est en cours d'exécution sur un serveur qui n'est pas le serveur de site, les images de démarrage sont vulnérables aux attaques. Protégez le canal de réseau entre ces ordinateurs en utilisant la signature SMB ou IPsec.  

-   **Activez les points de distribution pour la communication du client PXE uniquement sur des segments de réseau sécurisés**  

     Lorsqu'un client envoie une demande de démarrage PXE, vous n'avez aucun moyen de vous assurer que la demande est traitée par un point de distribution PXE valide. Ce scénario présente les risques de sécurité suivants :  

    -   Un point de distribution non autorisé qui répond aux demandes PXE peut fournir une image falsifiée aux clients.  

    -   Une personne malveillante peut lancer une attaque par le biais d'un intermédiaire (« man-in-the-middle ») contre le protocole TFTP utilisé par PXE, et envoyer du code nuisible avec les fichiers du système d'exploitation, ou créer un client non autorisé pour effectuer des demandes TFTP directement au point de distribution.  

    -   Une personne malveillante peut utiliser un client malveillant pour lancer une attaque par déni de service contre le point de distribution.  

     Adoptez un excellent système de défense pour protéger les segments réseau sur lesquels les clients accèderont aux points de distribution pour des demandes PXE.  

    > [!WARNING]  
    >  En raison de ces risques de sécurité, n'activez pas un point de distribution pour les communications PXE lorsqu'il se trouve sur un réseau non approuvé, tel qu'un réseau de périmètre.  

-   **Configurez le points de distribution PXE de sorte qu’il réponde aux demandes PXE uniquement sur des interfaces réseau spécifiées**  

     Si vous autorisez le point de distribution à répondre aux demandes PXE sur toutes les interfaces réseau, cette configuration peut exposer le service PXE à des réseaux non approuvés  

-   **Exigez un mot de passe pour le démarrage PXE**  

     Lorsque vous avez besoin d’un mot de passe pour le démarrage PXE, cette configuration ajoute un niveau supplémentaire de sécurité au processus de démarrage PXE afin d’éviter que des clients non autorisés rejoignent la hiérarchie Configuration Manager.  

-   **N’incluez pas d’applications métier ni de logiciels contenant des données sensibles dans une image qui sera utilisée pour un démarrage PXE ou une multidiffusion**  

     En raison des risques de sécurité liés à la multidiffusion et au démarrage PXE, réduisez les risques si l'ordinateur non autorisé télécharge l'image du système d'exploitation.  

-   **N’incluez pas d’applications métier ni de logiciels contenant des données sensibles dans des packages logiciels qui sont installés à l’aide de variables de séquences de tâches**  

     Lorsque vous déployez des packages logiciels à l'aide de variables de séquences de tâches, le logiciel peut être installé sur des ordinateurs et pour des utilisateurs qui ne sont pas autorisés à recevoir ce logiciel.  

-   **Lorsque vous migrez un état utilisateur, sécurisez le canal de réseau entre le client et le point de migration d’état à l’aide de la signature SMB ou d’IPsec**  

     Après la connexion initiale sur HTTP, les données de migration d'état utilisateur sont transférées à l'aide de SMB.  Si vous ne sécurisez pas le canal de réseau, une personne malveillante peut lire et modifier ces données.  

-   **Utilisez la dernière version de l’outil de migration de l’état utilisateur (USMT) pris en charge par Configuration Manager**  

     La dernière version d'USMT offre des améliorations de sécurité et un meilleur contrôle de la migration des données d'état utilisateur.  

-   **Supprimez manuellement des dossiers sur le point de migration d’état lorsqu’ils sont mis hors service**  

     Lorsque vous supprimez un dossier de point de migration d’état dans la console Configuration Manager sur les propriétés du point de migration d’état, le dossier physique n’est pas supprimé. Pour protéger les données de migration d'état utilisateur contre la divulgation d'informations, vous devez supprimer manuellement le partage réseau et supprimer le dossier.  

-   **Ne configurez pas la stratégie de suppression pour supprimer l’état utilisateur immédiatement**  

     Si vous configurez la stratégie de suppression sur le point de migration d'état afin de supprimer les données marquées pour suppression immédiatement, et si une personne malveillante parvient à récupérer les données d'état utilisateur avant l'ordinateur valide, les données d'état utilisateur seront immédiatement supprimées. Définissez l'intervalle **Supprimer après** de sorte qu'il soit suffisamment long pour permettre la vérification de la restauration correcte des données de l'état utilisateur.  

-   **Supprimez manuellement les associations d’ordinateurs lorsque la restauration des données de migration d’état utilisateur est terminée et vérifiée**  

     Configuration Manager ne supprime pas automatiquement les associations d’ordinateurs. Protégez l'identité des données d'état utilisateur en supprimant manuellement les associations d'ordinateurs qui ne sont plus nécessaires.  

-   **Sauvegardez manuellement les données de migration d’état utilisateur sur le point de migration d’état**  

     La sauvegarde Configuration Manager n’inclut pas les données de migration d’état utilisateur.  

-   **N’oubliez pas d’activer BitLocker après avoir installé le système d’exploitation**  

     Si un ordinateur prend en charge BitLocker, vous devez le désactiver à l'aide d'une étape de séquence de tâches si vous souhaitez installer le système d'exploitation en mode sans assistance. Configuration Manager n’active pas BitLocker une fois le système d’exploitation installé, vous devez donc réactiver BitLocker manuellement.  

-   **Instaurez des contrôles d’accès pour protéger les médias préparés**  

     Contrôlez l'accès physique au média pour qu'une personne malveillante ne puisse pas recourir à des attaques par chiffrement afin d'obtenir le certificat d'authentification du client et les données sensibles.  

-   **Instaurez des contrôles d’accès pour protéger le processus d’acquisition d’image de l’ordinateur de référence**  

     Vérifiez que l'ordinateur de référence utilisé pour capturer des images du système d'exploitation est situé dans un environnement sécurisé intégrant les contrôles d'accès appropriés afin que des logiciels malveillants ne puissent pas être installés et inclus par inadvertance dans l'image capturée. Lorsque vous capturez l'image, assurez-vous que l'emplacement du partage de fichiers réseau de destination est sécurisé afin que l'image ne puisse pas être falsifiée une fois capturée.  

-   **Installez systématiquement les mises à jour de sécurité les plus récentes sur l’ordinateur de référence**  

     Lorsque l'ordinateur de référence contient des mises à jour de sécurité, il permet de réduire la fenêtre de vulnérabilité des nouveaux ordinateurs lors de leur premier démarrage.  

-   **Si vous devez déployer des systèmes d’exploitation vers un ordinateur inconnu, implémentez des contrôles d’accès afin de bloquer la connexion des ordinateurs non autorisés au réseau**  

     Bien que le provisionnement des ordinateurs inconnus fournisse une méthode pratique pour déployer de nouveaux ordinateurs à la demande, il peut également permettre à une personne malveillante de devenir un client approuvé sur votre réseau. Limitez l'accès physique au réseau et contrôlez les clients afin de détecter les ordinateurs non autorisés. De même, toutes les données relatives aux ordinateurs répondant au déploiement du système d'exploitation établi par PXE risquent d'être détruites lors du déploiement du système d'exploitation. Cela peut engendrer une perte de disponibilité au niveau des systèmes qui sont reformatés par inadvertance.  

-   **Activez le chiffrement de packages de multidiffusion**  

     Pour chaque package de déploiement du système d’exploitation, vous pouvez activer le chiffrement lorsque Configuration Manager transfère le package par multidiffusion. Cette configuration permet d'empêcher les ordinateurs non autorisés de se joindre à la session multidiffusion et les personnes malveillantes d'altérer la transmission.  

-   **Contrôlez les points de distribution de multidiffusion activée**  

     Si des personnes malveillantes peuvent accéder à votre réseau, elles peuvent configurer des serveurs de multidiffusion non autorisés afin qu'ils usurpent un déploiement de systèmes d'exploitation.  

-   **Lorsque vous exportez des séquences de tâches vers un emplacement réseau, sécurisez l’emplacement et le canal de réseau**  

     Veillez à restreindre l'accès au dossier réseau.  

     Utilisez la signature SMB ou IPsec entre l'emplacement réseau et le serveur de site pour empêcher une personne malveillante de falsifier la séquence de tâches exportée.  

-   **Sécurisez le canal de communication lorsque vous chargez un disque dur virtuel vers Virtual Machine Manager**  

     Pour empêcher la falsification des données lorsqu’elles sont transférées via le réseau, utilisez la sécurité du protocole Internet (IPsec) ou le bloc de message serveur (SMB) entre l’ordinateur qui exécute la console Configuration Manager et l’ordinateur qui exécute Virtual Machine Manager.  

-   **Si vous devez utiliser le compte d’identification de séquence de tâches, prenez des précautions de sécurité supplémentaires**  

     Si vous utilisez le compte d'identification de séquence de tâches, prenez les précautions suivantes :  

    -   Utilisez un compte doté du moindre nombre d'autorisations possible.  

    -   N'utilisez pas le compte d'accès réseau pour ce compte.  

    -   Ne configurez en aucun cas le compte en tant qu'administrateur de domaine.  

     En outre :  

    -   Ne configurez jamais de profils itinérants pour ce compte. Lorsque la séquence de tâches s'exécute, elle télécharge le profil itinérant pour le compte, ce qui le rend vulnérable aux accès sur l'ordinateur local.  

    -   Limitez la portée du compte. Par exemple, créez différents comptes d'identification de séquence de tâches pour chaque séquence de tâches, de sorte que, si un compte est compromis, seuls les ordinateurs clients auxquels ce compte a accès sont compromis. Si la ligne de commande requiert un accès administrateur sur l'ordinateur, vous pouvez créer un compte administrateur local réservé au compte d'identification de séquence de tâches sur tous les ordinateurs qui exécuteront la séquence, puis supprimer le compte devenu inutile.  

-   **Limitez et surveillez les utilisateurs administratifs disposant du rôle de sécurité Gestionnaire de déploiement de système d’exploitation**  

     Les utilisateurs administratifs disposant du rôle de sécurité Gestionnaire de déploiement de système d’exploitation peuvent créer des certificats auto-signés pouvant ensuite être utilisés pour emprunter l’identité d’un client et obtenir une stratégie client de Configuration Manager.  

### <a name="security-issues-for-operating-system-deployment"></a>Problèmes de sécurité pour le déploiement de systèmes d’exploitation  
 Bien que le déploiement de systèmes d'exploitation puisse être un moyen efficace de déployer les systèmes d'exploitation et les configurations les plus sûrs pour les ordinateurs sur votre réseau, il comporte les risques de sécurité suivants :  

-   Divulgation d'informations et déni de service  

     Si une personne malveillante peut prendre le contrôle de votre infrastructure Configuration Manager, elle peut exécuter n’importe quelle séquence de tâches, ce qui peut inclure le formatage des disques durs de tous les ordinateurs clients. Des séquences de tâches peuvent être configurées pour contenir des informations sensibles, telles que les comptes autorisés à rejoindre le domaine et les clés de licence en volume.  

-   Emprunt d'identité et élévation de privilèges  

     Des séquences de tâches peuvent joindre un ordinateur au domaine, qui peut fournir l'accès réseau authentifié à un ordinateur non autorisé. Un autre principe important de la sécurité du déploiement du système d'exploitation consiste à protéger le certificat d'authentification du client utilisé pour le média de démarrage des séquences de tâches et pour le déploiement du démarrage PXE. Lorsque vous capturez un certificat d'authentification client, cela permet à la personne malveillante d'obtenir la clé privée dans le certificat puis d'emprunter l'identité d'un client valide sur le réseau.  

     Si une personne malveillante obtient le certificat client utilisé pour le média de démarrage des séquences de tâches et pour le déploiement du démarrage PXE, ce certificat peut être utilisé pour emprunter l’identité d’un client valide sur Configuration Manager. Dans ce scénario, l'ordinateur non autorisé peut télécharger une stratégie, qui peut contenir des données sensibles.  

     Si des clients utilisent le compte d'accès réseau pour accéder aux données stockées sur le point de migration d'état, ces clients partagent effectivement la même identité et peuvent accéder aux données de migration d'état d'un autre client utilisant le compte d'accès réseau. Les données sont chiffrées et seul le client d'origine peut donc les lire, mais elles peuvent être falsifiées ou supprimées.  

-   L’authentification des clients auprès du point de migration d’état s’effectue à l’aide d’un jeton Configuration Manager émis par le point de gestion.  

     Par ailleurs, Configuration Manager ne limite pas et ne gère pas la quantité de données stockées sur le point de migration d’état. Or, un intrus peut saturer l’espace disque disponible et provoquer un déni de service.  

-   Si vous utilisez des variables de regroupement, les administrateurs locaux peuvent lire des informations potentiellement sensibles.  

     Même si les variables de regroupement offrent une méthode flexible pour le déploiement des systèmes d'exploitation, elles peuvent entraîner une divulgation d'informations.  

##  <a name="BKMK_Privacy_HardwareInventory"></a> Informations de confidentialité pour le déploiement de systèmes d’exploitation  
 Configuration Manager peut non seulement permettre de déployer des systèmes d’exploitation sur des ordinateurs sans système d’exploitation, mais également permettre de migrer les fichiers et les paramètres des utilisateurs d’un ordinateur à un autre. L'administrateur configure les informations à transférer, notamment les fichiers de données personnelles, les paramètres de configuration et les cookies du navigateur.  

 Les informations sont stockées sur un point de migration de l'état et sont chiffrées durant la transmission et le stockage. Les informations peuvent être récupérées par le nouvel ordinateur associé aux informations d'état. Si le nouvel ordinateur perd la clé permettant d'extraire les informations, un administrateur Configuration Manager bénéficiant de l'autorisation Afficher les informations de récupération sur les objets d'instance d'association d'ordinateurs peut accéder aux informations et les associer au nouvel ordinateur. Une fois que le nouvel ordinateur a restauré les informations d'état, il supprime les données après un jour par défaut. Vous pouvez configurer le moment auquel le point de migration de l'état supprime les données marquées pour suppression. Les informations de migration de l'état ne sont pas stockées dans la base de données de site et ne sont pas envoyées à Microsoft.  

 Si vous utilisez un média de démarrage pour déployer des images du système d'exploitation, utilisez systématiquement l'option par défaut permettant de protéger par mot de passe le média de démarrage. Le mot de passe chiffre les variables stockées dans la séquence de tâches, mais les informations non stockées dans une variable peuvent être facilement divulguées.  

 Le déploiement du système d'exploitation peut utiliser des séquences de tâches pour effectuer un grand nombre de tâches durant le processus de déploiement, notamment l'installation d'applications et de mises à jour logicielles. Lorsque vous configurez des séquences de tâches, vous devez également être conscient des conséquences de l'installation de logiciels en termes de confidentialité.  

 Si vous téléchargez un disque dur virtuel vers Virtual Machine Manager sans utiliser Sysprep auparavant pour nettoyer l'image, le disque dur virtuel téléchargé peut contenir des données personnelles de l'image d'origine.  

 Configuration Manager ne met pas en œuvre le déploiement du système d’exploitation par défaut et requiert plusieurs étapes de configuration avant que vous puissiez recueillir des informations d’état utilisateur ou créer des séquences de tâches ou des images de démarrage.  

 Avant de configurer le déploiement du système d'exploitation, prenez en compte vos impératifs en matière de confidentialité.  
