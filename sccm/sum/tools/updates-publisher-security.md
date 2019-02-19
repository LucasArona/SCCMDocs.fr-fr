---
title: Certificats et sécurité
titleSuffix: Configuration Manager
description: Gérer les certificats et la sécurité pour l’éditeur de mise à jour System Center
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2a0dbe80e2333df85893365a366d5862842ffa3d
ms.sourcegitcommit: 874d78f08714a509f61c52b154387268f5b73242
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/12/2019
ms.locfileid: "56125406"
---
# <a name="manage-certificates-and-security-for-updates-publisher"></a>Gérer les certificats et la sécurité pour l’éditeur de mise à jour

*S’applique à : System Center Configuration Manager (Current Branch)*

Les procédures suivantes peuvent vous aider à configurer le magasin de certificats sur le serveur de mise à jour, à configurer un certificat d’auto-signature sur l’ordinateur client, et à configurer la stratégie de groupe pour permettre à l’Agent Windows Update sur les ordinateurs de rechercher les mises à jour publiées.

## <a name="configure-the-certificate-store-on-the-update-server"></a>Configurer le magasin de certificats sur le serveur de mise à jour
 L’éditeur de mise à jour utilise un certificat numérique pour signer les mises à jour dans les catalogues qu'il publie. Pour pouvoir publier un catalogue sur le serveur de mise à jour, ce certificat doit figurer dans le magasin de certificats sur le serveur de mise à jour et dans le magasin de certificats de l’ordinateur de l’éditeur de mise à jour si cet ordinateur est éloigné du serveur de mise à jour.

La procédure suivante est une des méthodes possibles pour ajouter le certificat au magasin de certificats sur le serveur de mise à jour.

### <a name="to-configure-the-certificate-store"></a>Pour configurer le magasin de certificats
1.  Sur un ordinateur disposant à la fois d’un accès à l’ordinateur de l’éditeur de mise à jour et au serveur de mise à jour, cliquez sur **Démarrer**, cliquez sur **Exécuter**, tapez **MMC** dans la zone de texte, puis cliquez sur **OK** pour ouvrir la console MMC (Microsoft Management Console).

2.  Cliquez sur **Fichier**, sur **Ajouter/supprimer un composant logiciel enfichable**, **Ajouter**, **Certificats**, **Ajouter**, sélectionnez **Compte de l’ordinateur**, puis cliquez sur **Suivant**.

3.  Sélectionnez **Un autre ordinateur**, saisissez le nom du serveur de mise à jour ou cliquez sur **Parcourir** pour rechercher l’ordinateur du serveur de mise à jour, cliquez sur **Terminer**, sur **Fermer** puis sur **OK**.

4.  Développez ***Certificats (* nom du serveur de mise à jour**), **WSUS**, puis cliquez sur **Certificats**.

5.  Dans le volet des résultats, cliquez avec le bouton droit sur le certificat souhaité, sélectionnez **Toutes les tâches**, puis cliquez sur **Exporter**.

6.  Dans l’Assistant Exportation de certificat, utilisez les paramètres par défaut pour créer un fichier d’exportation avec le nom et l’emplacement spécifiés dans l’Assistant. Ce fichier doit être disponible pour le serveur de mise à jour avant de passer à l’étape suivante.

7.  Cliquez avec le bouton droit sur **Éditeurs approuvés**, sélectionnez **Toutes les tâches**, puis cliquez sur **Importer**. Terminez l’Assistant Importation de certificat en utilisant le fichier exporté à l’étape 6.

8.  Si vous utilisez un certificat auto-signé, par exemple des **éditeurs WSUS auto-signés**, cliquez avec le bouton droit sur **Autorités de certification racines de confiance**, sélectionnez **Toutes les tâches**, puis cliquez sur **Importer**. Terminez l’Assistant Importation de certificat en utilisant le fichier exporté à l’étape 6.

9.  Cliquez avec le bouton droit sur ***Certificats (* nom du serveur de mise à jour**), sélectionnez **Se connecter à un autre ordinateur**, entrez le nom d’ordinateur de l’éditeur de mise à jour, puis cliquez sur **OK**.

10. Si l’éditeur de mise à jour est éloigné du serveur de mise à jour, répétez les étapes 7 à 9 pour importer le certificat dans le magasin de certificats sur l’ordinateur de l’éditeur de mise à jour.



## <a name="configure-a-self-signing-certificate-on-client-computers"></a>Configurer un certificat d’auto-signature sur les ordinateurs clients
Sur les ordinateurs clients, l’Agent Windows Update (WUA) recherchera les mises à jour à partir du catalogue. Ce processus ne pourra pas installer les mises à jour si l’agent est incapable de localiser ce certificat numérique dans le magasin des éditeurs approuvés sur l’ordinateur local. Si un certificat auto-signé a été utilisé pour la publication du catalogue de mises à jour, comme des **éditeurs WSUS auto-signés**, le certificat doit également se trouver dans le magasin de certificats des autorités de certification racine approuvées, sur l'ordinateur local, afin que l’agent puisse vérifier la validité du certificat.

Vous pouvez utiliser une des méthodes disponibles pour configurer des certificats sur les ordinateurs clients, notamment la stratégie de groupe et l **’Assistant Importation de certificat**, ou à l’aide de l’outil Certutil et de la distribution de logiciels.

Voici un exemple montrant comment configurer le certificat de signature sur les ordinateurs clients.

### <a name="to-configure-a-self-signing-certificate-on-client-computers"></a>Pour configurer un certificat d’auto-signature sur les ordinateurs clients
1. Sur un ordinateur disposant d’un accès au serveur de mise à jour, cliquez sur **Démarrer**, cliquez sur **Exécuter**, tapez **MMC** dans la zone de texte, puis cliquez sur **OK** pour ouvrir la console MMC (Microsoft Management Console).

2. Cliquez sur **Fichier**, sur **Ajouter/supprimer un composant logiciel enfichable**, **Ajouter**, **Certificats**, **Ajouter**, sélectionnez **Compte de l’ordinateur**, puis cliquez sur **Suivant**.

3. Sélectionnez **Un autre ordinateur**, saisissez le nom du serveur de mise à jour ou cliquez sur **Parcourir** pour rechercher l’ordinateur du serveur de mise à jour, cliquez sur **Terminer**, sur **Fermer** puis sur **OK**.

4. Développez ***Certificats (* nom du serveur de mise à jour**), **WSUS**, puis cliquez sur **Certificats**.

5. Cliquez avec le bouton droit sur le certificat dans le volet des résultats, sélectionnez **Toutes les tâches**, puis cliquez sur **Exporter**. Terminez l **’Assistant Exportation de certificat**, utilisez les paramètres par défaut pour créer un fichier de certificat d’exportation avec le nom et l’emplacement spécifiés dans l’Assistant.

6. À l’aide de l’une des méthodes suivantes, ajoutez le certificat utilisé pour signer le catalogue de mises à jour sur chaque ordinateur client qui utilisera WUA pour rechercher les mises à jour dans le catalogue. Ajoutez le certificat sur l’ordinateur client comme suit :

   -   Pour les certificats auto-signés : Ajoutez le certificat aux magasins de certificats **Autorités de certification racines de confiance** et **Éditeurs approuvés**.

   -   Pour les certificats délivrés une autorité de certification : Ajoutez le certificat au magasin de certificats **Éditeurs approuvés**.

   > [!NOTE]
   > WUA vérifie également si le paramètre **Autoriser le contenu signé de la stratégie de groupe d'emplacement des services de mise à jour Microsoft sur l'intranet** est activé sur l'ordinateur local. Ce paramètre de stratégie doit être activé pour que WUA analyse les mises à jour qui ont été créées et publiées à l'aide de l'éditeur de mises à jour. Pour plus d’informations sur l’activation du paramètre Stratégie de groupe, consultez le [Guide pratique pour configurer la stratégie de groupe sur les ordinateurs clients](<https://technet.microsoft.com/library/bb530967.aspx(d=robot>).



## <a name="configuring-group-policy-to-allow-wuaon-computers-to-scan-for-published-updates"></a>Configuration de la stratégie de groupe pour autoriser WUA à rechercher sur les ordinateurs les mises à jour publiées
Avant que l’Agent Windows Update (WUA) recherche sur les ordinateurs les mises à jour logicielles qui ont été créées et publiées à l’aide de l’éditeur de mise à jour, un paramètre de stratégie doit être activé pour autoriser le contenu signé de l’emplacement intranet du service de mise à jour Microsoft. Lorsque vous activez le paramètre de stratégie, l’Agent Windows Update (WUA) accepte les mises à jour reçues via un emplacement intranet si les mises à jour apparaissent signées dans le magasin de certificats **Éditeurs approuvés** sur l’ordinateur local. Il existe plusieurs méthodes pour configurer la stratégie de groupe sur les ordinateurs dans l’environnement.

Pour les ordinateurs qui ne figurent pas sur le domaine, un paramètre de clé de registre peut être configuré afin d’autoriser le contenu signé de l'emplacement intranet du service de mise à jour Microsoft.

Les procédures suivantes fournissent les étapes de base permettant de configurer la stratégie de groupe pour les ordinateurs du domaine, ainsi qu’une valeur de clé de registre sur les ordinateurs qui ne figurent pas sur le domaine.

### <a name="to-configure-group-policy-to-allow-wua-to-scan-for-published-updates"></a>Pour configurer la stratégie de groupe afin d’autoriser l’Agent Windows Update (WUA) à rechercher les mises à jour publiées
1.  Ouvrez le composant logiciel enfichable de la console MMC pour l’éditeur d’objet de la stratégie de groupe avec un utilisateur disposant des droits de sécurité appropriés pour configurer la stratégie de groupe.

2.  Cliquez sur **Parcourir** et sélectionnez le domaine, l’unité d’organisation ou les objets stratégie de groupe liés au site où la stratégie de groupe configurée sera déployée sur les ordinateurs clients souhaités. Cliquez sur **OK**, **Terminer**, **Fermer**, puis sur **OK**.

3.  Développez le paramètre de sécurité sélectionnée dans l’arborescence de la console, développez **Configuration ordinateur**, **Modèles d'administration**, **Composants Windows**, puis cliquez sur **Windows Update**.

4.  Dans le volet des résultats, cliquez avec le bouton droit sur **Autoriser le contenu signé de l'emplacement intranet du service de mise à jour Microsoft**, sélectionnez **Propriétés**, **Activé**, puis cliquez sur **OK**.
