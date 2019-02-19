---
title: Capacités de la version Technical Preview 1512
titleSuffix: Configuration Manager
description: Découvrez les fonctionnalités disponibles dans la version d’évaluation technique de System Center Configuration Manager, version 1512.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: e4d9e414-1346-4ed4-85d0-64d602b68731
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.collection: M365-identity-device-management
ms.openlocfilehash: 33bba1b837e8336a72ff5f3588a58ca8598e5d2d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56132538"
---
# <a name="capabilities-in-technical-preview-1512-for-system-center-configuration-manager"></a>Fonctionnalités dans la version d’évaluation technique 1512 de System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Technical Preview)*

Cet article présente les fonctionnalités qui sont disponibles dans la version d’évaluation technique de System Center Configuration Manager, version 1512. Vous pouvez installer cette version pour mettre à jour et ajouter de nouvelles fonctionnalités à votre site Configuration Manager Technical Preview. Avant d’installer cette version de la version d’évaluation technique, passez en revue la rubrique de présentation, [Version d’évaluation technique pour System Center Configuration Manager](technical-preview.md), pour vous familiariser avec les conditions générales et limitations d’utilisation d’une version d’évaluation technique, la mise à jour entre les versions et l’envoi de commentaires sur les fonctionnalités dans une version d’évaluation technique.  

 Vous trouverez ci-dessous les nouvelles fonctionnalités propres à cette version.  

##  <a name="bkmk_devicehealth"></a> Attestation de l’intégrité des appareils  
 À partir de la version d’évaluation technique 1512, les administrateurs peuvent afficher l’état de l’attestation de l’intégrité des appareils Windows 10 dans la console Configuration Manager.  Cette fonctionnalité est disponible pour Configuration Manager et Configuration Manager avec Microsoft Intune. L’attestation de l’intégrité des appareils permet à l’administrateur de s’assurer que les ordinateurs clients ont des configurations de BIOS, de Module de plateforme sécurisée (TPM) et de logiciel de démarrage dignes de confiance. Pour prendre en charge l’attestation de l’intégrité des appareils, les appareils clients doivent exécuter Windows 10 avec le Module de plateforme sécurisée (TPM) 2 activé. L’attestation de l’intégrité des appareils affiche le nombre d’appareils activés pour chacun des éléments suivants :  

-   Logiciel anti-programme malveillant à lancement anticipé  

-   BitLocker  

-   Démarrage sécurisé  

-   Intégrité du code  

La console affiche également les principaux paramètres d’attestation de l’intégrité manquants avec le nombre d’appareils.  

Pour afficher l’attestation d’intégrité de l’appareil, dans la console Configuration Manager, accédez à l’espace de travail **Surveillance**, cliquez sur le nœud **Sécurité**, puis cliquez sur **Attestation d’intégrité**.  

##  <a name="bkmk_viewterms"></a> Surveillance des conditions générales dans la console  
À compter de la version d’évaluation technique 1512, quand vous intégrez Configuration Manager avec Microsoft Intune, vous pouvez utiliser la console Configuration Manager pour afficher la liste des utilisateurs qui ont accepté les conditions générales configurées par votre service informatique et la liste de ceux qui ne les ont pas acceptées.  

**Pour afficher des informations de synthèse :**  

-   Dans la console Configuration Manager, accédez à **Surveillance** > **Vue d’ensemble** > **Déploiements** et sélectionnez le déploiement de conditions générales que vous souhaitez afficher.  

**Pour afficher des informations détaillées :**  

1.  Dans la console Configuration Manager, accédez à **Ressources et Conformité** > **Vue d’ensemble** > **Paramètres de compatibilité** > **Conditions générales**, puis sélectionnez les conditions générales à afficher.  

2.  En bas de la console, sélectionnez l’onglet **Déploiements**, sélectionnez le déploiement, puis cliquez sur **Afficher l’état**.  

##  <a name="bkmk_EPpolicy"></a> Améliorations apportées aux paramètres de stratégie Endpoint Protection  
Dans Technical Preview 1512, nous avons ajouté les nouveaux paramètres de stratégie de logiciel anti-programme malveillant Endpoint Protection suivants :  

-   Protection en temps réel : **Bloquer les applications potentiellement indésirables au téléchargement et avant l’installation**  

    -   Les applications potentiellement indésirables (PUA, Potential Unwanted Applications) sont une classification de menaces basée sur la réputation et l’identification pilotée par les recherches. En règle générale, il s’agit de programmes d’installation de logiciels indésirables ou de leurs applications groupées.  

    -   Le paramètre de stratégie de protection est activé par défaut (il a la valeur « Oui »). Quand il est activé, ce paramètre bloque les applications potentiellement indésirables au moment du téléchargement et de l’installation. Toutefois, vous pouvez exclure certains fichiers ou dossiers pour répondre aux besoins spécifiques de votre environnement.  

-   Paramètres d’analyse : **Analyser les lecteurs réseau mappés lors d’une analyse complète**  

    -   Ce paramètre offre à l’administrateur une granularité plus élevée et lui permet d’effectuer des analyses à la demande de fichiers réseau sans risquer de toujours analyser des lecteurs réseau mappés lors d’une analyse complète planifiée.  

    -   Pour pouvoir configurer le paramètre **Analyser les fichiers réseau**, vous devez d’abord l’activer.  

    -   Par défaut, ce paramètre est désactivé, ce qui signifie que l’analyse complète n’accède pas aux lecteurs réseau mappés.  

-   Paramètres d’envoi automatique d’exemples de fichiers :  

     Le moteur du logiciel anti-programme malveillant peut demander à ce que des exemples de fichiers soient envoyés à Microsoft pour une analyse plus approfondie. Par défaut, il affiche toujours une invite avant d’envoyer ces exemples. Les administrateurs peuvent désormais gérer les paramètres suivants pour configurer ce comportement :  

    -   Avancé : **Activer l’envoi automatique de fichier d’exemple pour aider Microsoft à déterminer si certains éléments détectés sont malveillants** :  Changez ce paramètre en « Oui » pour activer l’envoi automatique de fichier d’exemple. Par défaut, ce paramètre a la valeur « Non », ce qui signifie que l’envoi automatique d’exemple de fichier est désactivé et que les utilisateurs sont invités à donner leur accord avant l’envoi des fichiers.   (Ce paramètre a été introduit pour la première fois dans System Center 2012 R2 Configuration Manager SP1.)  

    -   Avancé : **Autoriser les utilisateurs à modifier les paramètres d’envoi automatique du fichier d’exemple** : Ce paramètre détermine si un utilisateur disposant de droits d’administrateur local sur un périphérique peut modifier le paramètre d’envoi automatique des fichiers d’exemple dans l’interface du client. Par défaut, ce paramètre a la valeur « Non », ce qui signifie que les paramètres ne peuvent être modifiés que dans la console Configuration Manager, et les administrateurs locaux d’un appareil ne peuvent pas modifier cette configuration.  

         L’exemple suivant montre le paramètre Windows Defender dans Windows 10 défini par l’administrateur comme activé, l’utilisateur n’étant pas autorisé à le modifier :  

         ![TechRef&#95;WinDefender](../../core/get-started/media/TechRef_WinDefender.png "TechRef_WinDefender")  

    En outre, le paramètre **Exclure des fichiers et des dossiers** existant dans la section « Paramètres d’exclusions » de la stratégie de logiciel anti-programme malveillant d’Endpoint Protection a été amélioré pour autoriser les exclusions d’appareils. Par exemple, vous pouvez maintenant spécifier l’exclusion suivante : **\device\mvfs** (pour Multiversion File System). La stratégie ne valide pas le chemin de l’appareil. La stratégie Endpoint Protection est fournie au moteur anti-programme malveillant sur le client qui doit pouvoir interpréter la chaîne de l’appareil.  

**Configuration requise pour l’utilisation de stratégies Endpoint Protection :**  

Pour pouvoir utiliser des stratégies Endpoint Protection, vous devez d’abord installer et gérer le client Endpoint Protection à l’aide des paramètres client Endpoint Protection. Cette opération s’effectue à l’aide du client System Center Endpoint Protection pour Windows 7, Windows 8, Windows 8.1 ou de Windows Defender managé pour Windows 10. Consultez [Endpoint Protection dans System Center Configuration Manager](../../protect/deploy-use/endpoint-protection.md).  
