---
title: Sécurité et confidentialité pour le déploiement de système d’exploitation
titleSuffix: Configuration Manager
description: Découvrez les bonnes pratiques en matière de sécurité et de confidentialité pour le déploiement de système d’exploitation dans Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e2bb7992854f8743efa45f924e3d3d0718a3efe
ms.sourcegitcommit: 8791bb9be477fe6a029e8a7a76e2ca310acd92e0
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/31/2018
ms.locfileid: "50411389"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Sécurité et confidentialité pour le déploiement de système d’exploitation dans Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article contient des informations de sécurité et de confidentialité pour la fonctionnalité de déploiement de système d’exploitation dans Configuration Manager.  



##  <a name="bkmk_security"></a> Bonnes pratiques en matière de sécurité pour le déploiement de système d’exploitation  

 Utilisez les bonnes pratiques de sécurité suivantes lorsque vous déployez des systèmes d’exploitation avec Configuration Manager :  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Instaurez des contrôles d'accès pour protéger les supports de démarrage

 Lorsque vous créez un média de démarrage, attribuez toujours un mot de passe pour sécuriser le média. Même avec un mot de passe, seuls les fichiers qui contiennent des informations sensibles sont chiffrés et tous les fichiers peuvent être remplacés.  

 Contrôlez l'accès physique au média pour qu'une personne malveillante ne puisse pas recourir à des attaques par chiffrement pour obtenir le certificat d'authentification du client.  

 Pour empêcher un client d’installer une stratégie client ou un contenu falsifié, le contenu est haché et doit être utilisé avec la stratégie d’origine. Si le hachage du contenu échoue ou si la vérification détecte que le contenu correspond à la stratégie, le client n’utilise pas le média démarrable. Seul le contenu est haché. La stratégie n’est pas hachée, mais elle est chiffrée et sécurisée quand vous spécifiez un mot de passe. Il est donc plus difficile pour un attaquant de modifier la stratégie.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Utiliser un emplacement sécurisé quand vous créez des médias pour les images de système d’exploitation

 Si des utilisateurs non autorisés ont accès à l’emplacement, ils peuvent falsifier les fichiers que vous créez. Ils peuvent également utiliser tout l’espace disque disponible pour faire échouer la création des médias.  


### <a name="protect-certificate-files"></a>Protéger les fichiers de certificat 

 Protégez les fichiers de certificat (.pfx) avec un mot de passe fort. Si vous les stockez sur le réseau, sécurisez le canal de réseau quand vous les importez dans Configuration Manager.

 Quand vous avez besoin d’un mot de passe pour importer le certificat d’authentification client que vous utilisez pour les médias démarrables, cette configuration permet de protéger le certificat contre un attaquant.  

 Utilisez la signature SMB ou IPsec entre l'emplacement réseau et le serveur de site pour empêcher un intrus de falsifier le fichier de certificat.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Bloquer ou révoquer les certificats compromis 

 Si le certificat client est compromis, bloquez-le dans Configuration Manager. S’il s’agit d’un certificat PKI, révoquez-le.  

 Pour déployer un système d’exploitation à l’aide d’un média démarrable et d’un démarrage PXE, vous devez disposer d’un certificat d’authentification client avec une clé privée. Si ce certificat est compromis, bloquez le certificat dans le nœud **Certificats** de l'espace de travail **Administration** , nœud **Sécurité** .  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Sécuriser le canal de communication entre le serveur de site et le fournisseur SMS

 Quand le fournisseur SMS et le serveur de site sont distants l’un de l’autre, sécurisez le canal de communication pour protéger les images de démarrage.

 Quand vous modifiez des images de démarrage et que le fournisseur SMS est en cours d’exécution sur un serveur qui n’est pas le serveur de site, les images de démarrage sont vulnérables aux attaques. Protégez le canal de réseau entre ces ordinateurs en utilisant la signature SMB ou IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Activez les points de distribution pour la communication du client PXE uniquement sur des segments de réseau sécurisés

Quand un client envoie une demande de démarrage PXE, vous n’avez aucun moyen de vérifier que la demande est traitée par un point de distribution PXE valide. Ce scénario présente les risques de sécurité suivants :  

 - Un point de distribution non autorisé qui répond aux demandes PXE peut fournir une image falsifiée aux clients.  

 - Un attaquant peut lancer une attaque de l’intercepteur contre le protocole TFTP utilisé par PXE. Cette attaque peut envoyer du code malveillant avec les fichiers du système d’exploitation. L’attaquant peut également créer un client non autorisé pour effectuer des demandes TFTP directement au point de distribution.  

 - Une personne malveillante peut utiliser un client malveillant pour lancer une attaque par déni de service contre le point de distribution.  

Adoptez un système de défense en profondeur pour protéger les segments réseau sur lesquels les clients accèdent aux points de distribution compatibles PXE.  

> [!WARNING]  
>  En raison de ces risques de sécurité, n’activez pas un point de distribution pour les communications PXE s’il se trouve sur un réseau non approuvé (par exemple, un réseau de périmètre).  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Configurez le point de distribution PXE de sorte qu'il réponde aux demandes PXE uniquement sur des interfaces réseau spécifiées  

 Si vous autorisez le point de distribution à répondre aux demandes PXE sur toutes les interfaces réseau, cette configuration peut exposer le service PXE à des réseaux non approuvés  


### <a name="require-a-password-to-pxe-boot"></a>Exigez un mot de passe pour le démarrage PXE

 Quand vous avez besoin d’un mot de passe pour le démarrage PXE, cette configuration ajoute un niveau de sécurité supplémentaire au processus de démarrage PXE. Cette configuration permet d’éviter que des clients non autorisés ne rejoignent la hiérarchie Configuration Manager.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Restreindre le contenu dans les images de système d’exploitation utilisées pour le démarrage PXE ou la multidiffusion

 N’incluez pas d’applications métier ni de logiciels contenant des données sensibles dans une image que vous utilisez pour le démarrage PXE ou la multidiffusion.  

 En raison des risques de sécurité liés à la multidiffusion et au démarrage PXE, réduisez les risques si un ordinateur non autorisé télécharge l’image du système d’exploitation.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Restreindre le contenu installé par les variables de séquences de tâches

 N’incluez pas d’applications métier ni de logiciels contenant des données sensibles dans les packages d’applications que vous installez à l’aide de variables de séquences de tâches.  

 Quand vous déployez un logiciel à l’aide de variables de séquences de tâches, il peut être installé sur des ordinateurs et pour des utilisateurs qui ne sont pas autorisés à le recevoir.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Sécuriser le canal de réseau durant la migration d’un état utilisateur

 Quand vous migrez un état utilisateur, sécurisez le canal réseau entre le client et le point de migration d’état à l’aide d’une signature SMB ou d’IPsec.  

 Après la connexion initiale sur HTTP, les données de migration d'état utilisateur sont transférées à l'aide de SMB. Si vous ne sécurisez pas le canal de réseau, un attaquant peut lire et modifier ces données.  


### <a name="use-the-latest-version-of-usmt"></a>Utiliser la dernière version de l’outil USMT

 Utilisez la dernière version de l’outil de migration de l’état utilisateur (USMT) pris en charge par Configuration Manager.  

 La dernière version d'USMT offre des améliorations de sécurité et un meilleur contrôle de la migration des données d'état utilisateur.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Supprimer manuellement les dossiers des points de migration d’état après leur mise hors service  

 Quand vous supprimez un dossier de point de migration d’état dans la console Configuration Manager sur les propriétés du point de migration d’état, le site ne supprime pas le dossier physique. Pour protéger les données de migration d’état utilisateur contre la divulgation d’informations, supprimez manuellement le partage réseau et supprimez le dossier.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Ne pas configurer la stratégie de suppression pour supprimer immédiatement l’état utilisateur  

 Si vous configurez la stratégie de suppression sur le point de migration d’état afin de supprimer immédiatement les données marquées pour suppression, et qu’un attaquant parvient à récupérer les données d’état utilisateur avant l’ordinateur valide, le site supprime immédiatement les données d’état utilisateur. Définissez l'intervalle **Supprimer après** de sorte qu'il soit suffisamment long pour permettre la vérification de la restauration correcte des données de l'état utilisateur.  


### <a name="manually-delete-computer-associations"></a>Supprimer manuellement les associations d’ordinateurs 

 Supprimez manuellement les associations d’ordinateurs quand la restauration des données de migration d’état utilisateur est terminée et vérifiée.

 Configuration Manager ne supprime pas automatiquement les associations d’ordinateurs. Protégez l’identité des données d’état utilisateur en supprimant manuellement les associations d’ordinateurs qui ne sont plus nécessaires.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Sauvegardez manuellement les données de migration d'état utilisateur sur le point de migration d'état  

 La sauvegarde Configuration Manager n’inclut pas les données de migration d’état utilisateur dans la sauvegarde de site.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Instaurez des contrôles d'accès pour protéger les médias préparés  

 Contrôlez l'accès physique au média pour qu'une personne malveillante ne puisse pas recourir à des attaques par chiffrement afin d'obtenir le certificat d'authentification du client et les données sensibles.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Instaurez des contrôles d'accès pour protéger le processus d'acquisition d'image de l'ordinateur de référence  

 Vérifiez que l’ordinateur de référence que vous utilisez pour capturer les images de système d’exploitation se trouve dans un environnement sécurisé. Utilisez des contrôles d’accès appropriés pour empêcher l’installation de logiciels inattendus ou malveillants et éviter leur inclusion accidentelle dans l’image capturée. Quand vous capturez l’image, vérifiez que l’emplacement réseau de destination est sécurisé. Ce processus rend impossible toute falsification de l’image une fois celle-ci capturée.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Installez systématiquement les mises à jour de sécurité les plus récentes sur l'ordinateur de référence  

 Lorsque l'ordinateur de référence contient des mises à jour de sécurité, il permet de réduire la fenêtre de vulnérabilité des nouveaux ordinateurs lors de leur premier démarrage.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implémenter des contrôles d’accès durant le déploiement d’un système d’exploitation sur un ordinateur inconnu

 Si vous devez déployer un système d’exploitation sur un ordinateur inconnu, implémentez des contrôles d’accès pour empêcher les ordinateurs non autorisés de se connecter au réseau.  

 Le provisionnement d’ordinateurs inconnus constitue une méthode pratique pour déployer de nouveaux ordinateurs à la demande. Toutefois, elle peut également permettre à un attaquant de devenir un client approuvé sur votre réseau. Limitez l'accès physique au réseau et contrôlez les clients afin de détecter les ordinateurs non autorisés. 

 Sur les ordinateurs qui répondent à un déploiement de système d’exploitation lancé par PXE, toutes les données peuvent être détruites au cours du processus. Ce comportement peut entraîner une perte de la disponibilité des systèmes qui sont reformatés par inadvertance.  


### <a name="enable-encryption-for-multicast-packages"></a>Activez le chiffrement de packages de multidiffusion  

 Pour chaque package de déploiement de système d’exploitation, vous pouvez activer le chiffrement quand Configuration Manager transfère le package par multidiffusion. Cette configuration empêche les ordinateurs non autorisés de rejoindre la session de multidiffusion. Elle empêche également les attaquants de falsifier la transmission.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Contrôlez les points de distribution de multidiffusion activée  

 Si des attaquants peuvent accéder à votre réseau, ils peuvent configurer des serveurs de multidiffusion non autorisés de manière à usurper l’identité d’un déploiement de système d’exploitation.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Lorsque vous exportez des séquences de tâches vers un emplacement réseau, sécurisez l'emplacement et le canal de réseau

 Veillez à restreindre l'accès au dossier réseau.  

 Utilisez la signature SMB ou IPsec entre l'emplacement réseau et le serveur de site pour empêcher une personne malveillante de falsifier la séquence de tâches exportée.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Adopter des mesures de sécurité supplémentaire en cas d’utilisation du compte d’identification de séquence de tâches

 Si vous utilisez le [compte d’identification de séquence de tâches](/sccm/core/plan-design/hierarchy/accounts#task-sequence-run-as-account), prenez les précautions suivantes :  

 - Utilisez un compte doté du moindre nombre d'autorisations possible.  

 - N’utilisez pas le compte d’accès réseau pour ce compte.  

 - Ne configurez en aucun cas le compte en tant qu'administrateur de domaine.  

 - Ne configurez jamais de profils itinérants pour ce compte. Quand la séquence de tâches s’exécute, elle télécharge le profil itinérant pour le compte, ce qui le rend vulnérable aux accès sur l’ordinateur local.  

 - Limitez la portée du compte. Par exemple, créez un compte d’identification différent pour chaque séquence de tâches. Si un compte est compromis, seuls les ordinateurs clients auxquels ce compte a accès sont compromis. Si la ligne de commande nécessite un accès administratif sur l’ordinateur, songez à créer un compte administrateur local réservé au compte d’identification de séquence de tâches. Créez ce compte local sur tous les ordinateurs qui exécutent la séquence de tâches et supprimez-le dès qu’il n’est plus nécessaire.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Limiter et superviser les utilisateurs administratifs bénéficiant du rôle de sécurité Gestionnaire de déploiement de système d’exploitation

 Les utilisateurs administratifs qui se voient accorder le rôle de sécurité **Gestionnaire de déploiement de système d’exploitation** peuvent créer des certificats auto-signés. Ces certificats peuvent ensuite être utilisés pour emprunter l’identité d’un client et obtenir la stratégie client auprès de Configuration Manager.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Utiliser le protocole HTTP amélioré pour éviter de recourir à un compte d’accès réseau

À compter de la version 1806, quand vous activez [HTTP amélioré](/sccm/core/plan-design/hierarchy/enhanced-http), les scénarios suivants de déploiement de système d’exploitation ne nécessitent pas un compte d’accès réseau pour télécharger du contenu à partir d’un point de distribution. Pour plus d’informations, consultez [Séquences de tâches et compte d’accès réseau](/sccm/osd/plan-design/planning-considerations-for-automating-tasks#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Problèmes de sécurité pour le déploiement de système d’exploitation  

 Bien que le déploiement de système d’exploitation puisse être un moyen pratique de déployer les systèmes d’exploitation et les configurations les plus sécurisés sur les ordinateurs de votre réseau, il comporte les risques de sécurité suivants :  


### <a name="information-disclosure-and-denial-of-service"></a>Divulgation d'informations et déni de service  

 Si un attaquant parvient à prendre le contrôle de votre infrastructure Configuration Manager, il peut exécuter n’importe quelle séquence de tâches. Ce processus peut inclure le formatage des disques durs de tous les ordinateurs clients. Des séquences de tâches peuvent être configurées pour contenir des informations sensibles, telles que les comptes autorisés à rejoindre le domaine et les clés de licence en volume.  


### <a name="impersonation-and-elevation-of-privileges"></a>Emprunt d'identité et élévation de privilèges  

 Des séquences de tâches peuvent joindre un ordinateur au domaine, qui peut fournir l'accès réseau authentifié à un ordinateur non autorisé. 

 Protégez le certificat d’authentification client utilisé pour le média de la séquence de tâches démarrable et pour le déploiement du démarrage PXE. Quand vous capturez un certificat d’authentification client, un attaquant peut en profiter pour obtenir la clé privée dans le certificat. Ce certificat lui permet ensuite d’emprunter l’identité d’un client valide sur le réseau. Dans ce scénario, l'ordinateur non autorisé peut télécharger une stratégie, qui peut contenir des données sensibles.  

 Si les clients utilisent le compte d’accès réseau pour accéder aux données stockées sur le point de migration d’état, ces clients partagent effectivement la même identité. Ils peuvent accéder aux données de migration d’état à partir d’un autre client qui utilise le compte d’accès réseau. Les données sont chiffrées et seul le client d'origine peut donc les lire, mais elles peuvent être falsifiées ou supprimées.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>L’authentification des clients auprès du point de migration d’état s’effectue à l’aide d’un jeton Configuration Manager émis par le point de gestion.  

 Configuration Manager ne limite pas et ne gère pas la quantité de données stockées sur le point de migration d’état. Un attaquant peut remplir l’espace disque disponible et provoquer un déni de service.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Si vous utilisez des variables de regroupement, les administrateurs locaux peuvent lire des informations potentiellement sensibles.  

 Même si les variables de regroupement offrent une méthode flexible pour le déploiement de systèmes d’exploitation, elles peuvent entraîner une divulgation d’informations.  



##  <a name="bkmk_privacy"></a> Informations de confidentialité pour le déploiement de système d’exploitation  

 Configuration Manager permet non seulement de déployer un système d’exploitation sur un ordinateur dépourvu de système d’exploitation, mais aussi de migrer les fichiers et paramètres des utilisateurs d’un ordinateur à un autre. L'administrateur configure les informations à transférer, notamment les fichiers de données personnelles, les paramètres de configuration et les cookies du navigateur.  

 Configuration Manager stocke les informations sur un point de migration d’état qu’il chiffre durant la transmission et le stockage. Seul le nouvel ordinateur associé aux informations d’état peut récupérer les informations stockées. Si le nouvel ordinateur perd la clé permettant d’extraire les informations, un administrateur Configuration Manager bénéficiant de l’autorisation **Afficher les informations de récupération** sur les objets d’instance d’association d’ordinateurs peut accéder aux informations et les associer au nouvel ordinateur. Une fois que le nouvel ordinateur a restauré les informations d’état, il supprime par défaut les données après une journée. Vous pouvez configurer le moment auquel le point de migration de l'état supprime les données marquées pour suppression. Configuration Manager ne stocke pas les informations de migration d’état dans la base de données de site et ne les envoie pas à Microsoft.  

 Si vous utilisez un média de démarrage pour déployer des images de système d’exploitation, utilisez systématiquement l’option par défaut pour protéger par mot de passe le média de démarrage. Le mot de passe chiffre les variables stockées dans la séquence de tâches, mais les informations non stockées dans une variable peuvent être facilement divulguées.  

 Le déploiement du système d’exploitation peut utiliser des séquences de tâches pour effectuer un grand nombre de tâches durant le processus de déploiement, notamment l’installation d’applications et de mises à jour logicielles. Lorsque vous configurez des séquences de tâches, vous devez également être conscient des conséquences de l'installation de logiciels en termes de confidentialité.  

 Configuration Manager n’implémente pas le déploiement de système d’exploitation par défaut. Vous devez effectuer plusieurs étapes de configuration avant de pouvoir collecter des informations d’état utilisateur ou créer des séquences de tâches ou des images de démarrage.  

 Avant de configurer le déploiement de système d’exploitation, prenez en compte vos impératifs en matière de confidentialité.  



## <a name="see-also"></a>Voir aussi

[Données de diagnostic et d’utilisation](/sccm/core/plan-design/diagnostics/diagnostics-and-usage-data)

[Sécurité et confidentialité pour Configuration Manager](/sccm/core/plan-design/security/security-and-privacy)