---
title: 'Personnaliser les images de démarrage '
titleSuffix: Configuration Manager
description: Découvrez plusieurs façons d’utiliser Configuration Manager ou l’outil en ligne de commande de gestion et de maintenance des images de déploiement (DISM) pour personnaliser une image de démarrage.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 9cbfc406-d009-446d-8fee-4938de48c919
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 08156819af349af0f052cf2b58e8b4a44ef7b74b
ms.sourcegitcommit: 4981a796e7886befb7bdeeb346dba32be82aefd6
ms.translationtype: MTE75
ms.contentlocale: fr-FR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67516200"
---
# <a name="customize-boot-images-with-system-center-configuration-manager"></a>Personnaliser les images de démarrage avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Chaque version de Configuration Manager prend en charge une version spécifique du Kit de déploiement et d’évaluation Windows (Windows ADK). Vous pouvez utiliser, ou personnaliser, les images de démarrage depuis la console Configuration Manager quand elles sont basées sur une version Windows PE depuis la version prise en charge de Windows ADK. Vous devez déployer les autres images de démarrage à l'aide d'une autre méthode, telle que l'outil de ligne de commande Gestion et maintenance des images de déploiement (DISM) qui fait partie de Windows AIK et Windows ADK.  

 Vous trouverez ci-dessous des informations sur la version prise en charge de Windows ADK, la version de Windows PE sur laquelle l’image de démarrage est basée et qui peut être personnalisée à partir de la console Configuration Manager, ainsi que les versions de Windows PE sur lesquelles l’image de démarrage est basée et que vous pouvez personnaliser à l’aide de l’outil DISM avant d’ajouter l’image à Configuration Manager.  

- **Version de Windows ADK**  

   Windows ADK pour Windows 10  

- **Versions de Windows PE pour les images de démarrage personnalisables à partir de la console Configuration Manager**  

   Windows PE 10  

- **Versions prises en charge de Windows PE pour les images de démarrage non personnalisables à partir de la console Configuration Manager**  

   Windows PE 3.1<sup>1</sup> et Windows PE 5  

   <sup>1</sup> Vous pouvez ajouter une image de démarrage à Configuration Manager uniquement si elle est basée sur Windows PE 3.1. Installez le supplément Windows AIK pour Windows 7 SP1 pour mettre à niveau Windows AIK pour Windows 7 (basé sur Windows PE 3) avec le supplément Windows AIK pour Windows 7 SP1 (basé sur Windows PE 3.1). Vous pouvez télécharger le supplément Windows AIK pour Windows 7 SP1 depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

   Par exemple, si vous utilisez Configuration Manager, vous pouvez personnaliser les images de démarrage de Windows ADK pour Windows 10 (basées sur Windows PE 10) depuis la console Configuration Manager. Toutefois, si les images de démarrage basées sur Windows PE 5 sont prises en charge, vous devez les personnaliser depuis un autre ordinateur et utiliser la version de DISM installée avec Windows ADK pour Windows 8. Ensuite, vous pouvez ajouter l’image de démarrage à la console Configuration Manager.  

  Les procédures de cette rubrique expliquent comment ajouter les composants facultatifs requis par Configuration Manager à l’image de démarrage en utilisant les packages Windows PE suivants :  

- **WinPE-WMI**: Ajoute la prise en charge de Windows Management Instrumentation (WMI).  

- **WinPE-Scripting**: ajoute la prise en charge de Windows Script Host (WSH).  

- **WinPE-WDS-Tools**: installe les outils Windows Deployment Services.  

  D'autres packages Windows PE peuvent être ajoutés. Les ressources suivantes fournissent plus d'informations sur les composants facultatifs que vous pouvez ajouter à l'image de démarrage.  

- Pour Windows PE 5, consultez [WinPE : Ajouter des packages (informations de référence sur les composants facultatifs)](https://msdn.microsoft.com/library/windows/hardware/dn938382\(v=vs.85\).aspx)  

- Pour Windows PE 3.1, consultez la rubrique [Ajouter un package à une image Windows PE](https://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) dans la bibliothèque de documentation TechNet Windows 7.  

> [!NOTE]
>Lors du démarrage de WinPE à partir d’une image de démarrage personnalisée qui inclut des outils que vous avez ajoutés, vous pouvez ouvrir une invite de commandes à partir de WinPE et taper le nom de fichier de l’outil pour l’exécuter. L’emplacement de ces outils est automatiquement ajouté à la variable de chemin d’accès. L’invite de commandes ne peut être ajoutée que si le paramètre **Activer la prise en charge des commandes (test uniquement)** est sélectionné sous l’onglet **Personnalisation** des propriétés d’image de démarrage.

## <a name="customize-a-boot-image-that-uses-windows-pe-5"></a>Personnaliser une image de démarrage qui utilise Windows PE 5  
 Pour personnaliser une image de démarrage qui utilise Windows PE 5, vous devez installer Windows ADK et utiliser l’outil en ligne de commande DISM pour monter l’image de démarrage, ajouter des composants et des pilotes facultatifs et appliquer les modifications à l’image de démarrage. Pour personnaliser l'image de démarrage, procédez comme suit.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-5"></a>Pour personnaliser une image de démarrage qui utilise Windows PE 5  

1. Installez le kit Windows ADK sur un ordinateur qui n’a pas d’autre version de Windows AIK ni de Windows ADK, et sur lequel aucun composant Configuration Manager n’est installé.  

2. Téléchargez Windows ADK pour Windows 8.1 depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=39982).  

3. Copiez l’image de démarrage (wimpe.wim) du dossier d’installation de Windows ADK (par exemple, <*chemin_installation*>\Windows Kits\\<*version*>\Assessment and Deployment Kit\Windows Preinstallation Environment\\<*x86 ou amd64*>\\<*paramètres régionaux*>) vers un dossier de destination sur l’ordinateur à partir duquel vous personnaliserez l’image de démarrage. Cette procédure utilise C:\WinPEWAIK comme nom de dossier de destination.  

4. Utilisez DISM pour monter l'image de démarrage dans un dossier Windows PE local. Par exemple, tapez la ligne de commande suivante :  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Où C:\WinPEWAIK est le dossier qui contient l'image de démarrage et C:\WinPEMount est le dossier monté.  

   > [!NOTE]
   >  Pour plus d'informations sur DISM, consultez la rubrique [Informations techniques de référence sur l’outil Gestion et maintenance des images de déploiement](https://technet.microsoft.com/library/hh824821.aspx) dans la bibliothèque de documentation TechNet Windows 8.1 et Windows 8.

5. Une fois que vous avez monté l'image de démarrage, utilisez DISM pour ajouter des composants facultatifs à l'image de démarrage. Dans Windows PE 5, les composants facultatifs 64 bits sont situés dans <*chemin_installation*>\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs.  

   > [!NOTE]
   >  Cette procédure utilise l'emplacement suivant pour les composants facultatifs : C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs. Le chemin d'accès que vous utilisez peut être différent selon les options de version et d'installation que vous choisissez pour le kit Windows ADK.  

    Tapez la commande suivante pour installer les composants facultatifs :  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\WinPE-SecureStartup.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<paramètres régionaux\>* **\WinPE-SecureStartup_** *<paramètres régionaux\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<paramètres régionaux\>* **\WinPE-WMI_** *<paramètres régionaux\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<paramètres régionaux\>* **\WinPE-Scripting** *<paramètres régionaux\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\\** *<paramètres régionaux\>* **\WinPE-WDS-Tools_** *<paramètres régionaux\>* **.cab"**  

    Où C:\WinPEMount est le dossier monté et paramètres régionaux désigne les paramètres régionaux des composants. Par exemple, pour les paramètres régionaux **fr-fr** , tapez :  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-SecureStartup_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WMI_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-Scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files (x86)\Windows Kits\8.1\Assessment and Deployment Kit\Windows Preinstallation Environment\amd64\WinPE_OCs\en-us\WinPE-WDS-Tools_en-us.cab"**  

   > [!TIP]
   >  Pour plus d'informations sur les composants facultatifs que vous pouvez ajouter à l'image de démarrage, consultez la rubrique [Informations de référence sur les composants facultatifs Windows PE](https://technet.microsoft.com/library/hh824926.aspx) dans la bibliothèque de documentation TechNet Windows 8.1 et Windows 8.  

6. Utilisez DISM pour ajouter des pilotes spécifiques à l'image de démarrage, si nécessaire. Tapez la commande suivante pour ajouter des pilotes à l'image de démarrage :  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *chemin d'accès au fichier .inf du pilote* **>**  

    Où C:\WinPEMount est le dossier monté.  

7. Tapez la commande suivante pour démonter le fichier image de démarrage et valider les modifications.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Où C:\WinPEMount est le dossier monté.  

8. Ajoutez l’image de démarrage mise à jour à Configuration Manager pour pouvoir l’utiliser dans vos séquences de tâches. Utilisez les étapes suivantes pour importer l'image de démarrage mise à jour :  

   1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

   2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

   3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter une image de démarrage** pour démarrer l'Assistant Ajout d'une image de démarrage.  

   4. Sur la page **Source de données** , spécifiez les options suivantes et cliquez sur **Suivant**.  

      - Dans la zone **Chemin d'accès** , indiquez le chemin d'accès au fichier de l'image de démarrage mis à jour. Le chemin d'accès spécifié doit être un chemin d'accès réseau valide au format UNC. Par exemple : **\\\\<** <em>nom_serveur</em> **>\\<** <em>partage WinPEWAIK</em> **>\winpe.wim**.  

      - Sélectionnez l'image de démarrage dans la liste déroulante **Image de démarrage** . Si le fichier WIM contient plusieurs images de démarrage, chaque image est répertoriée.  

   5. Sur la page **Général** , spécifiez les options suivantes et cliquez sur **Suivant**.  

      -   Dans la zone **Nom** , spécifiez un nom unique pour l'image de démarrage.  

      -   Dans la zone **Version** , spécifiez un numéro de version pour l'image de démarrage.  

      -   Dans la zone **Commentaire** , spécifiez une description sommaire de l'utilisation de l'image de démarrage.  

   6. Effectuez toutes les étapes de l'Assistant.  

9. Vous pouvez activer une invite de commandes dans l'image de démarrage pour le débogage et le dépannage dans Windows PE. Utilisez les étapes suivantes pour activer l'invite de commandes.  

   1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

   2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

   3. Recherchez la nouvelle image de démarrage dans la liste et identifiez l'ID de package pour l'image. Vous pouvez trouver l'ID de package dans la colonne **ID de l'image** pour l'image de démarrage.  

   4. À partir d'une invite de commande, tapez **wbemtest** pour ouvrir le testeur WMI.  

   5. Tapez **\\\\<** <em>ordinateur_fournisseur_SMS</em> **>\root\sms\site_<** <em>code_site</em> **>** dans **Espace de noms**, puis cliquez sur **Connexion**.  

   6. Cliquez sur **Ouvrir une instance**, tapez **sms_bootimagepackage.packageID="<packageID\>"** , puis cliquez sur **OK**. Pour packageID, entrez la valeur que vous avez identifiée à l'étape 3.  

   7. Cliquez sur **Actualiser l'objet**, puis cliquez sur **EnableLabShell** dans le volet **Propriétés** .  

   8. Cliquez sur **Modifier la propriété**, remplacez la valeur par **TRUE**, puis cliquez sur **Enregistrer la propriété**.  

   9. Cliquez sur **Enregistrer l'objet**, puis fermez le testeur WMI.  

10. Vous devez distribuer l'image de démarrage vers des points de distribution, des groupes de points de distribution ou des regroupements associés à des groupes de points de distribution avant de pouvoir utiliser l'image de démarrage dans une séquence de tâches. Pour distribuer l'image de démarrage, procédez comme suit.  

    1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

    2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

    3.  Cliquez sur l'image de démarrage identifiée à l'étape 3.  

    4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Mettre à jour les points de distribution**.  

## <a name="customize-a-boot-image-that-uses-windows-pe-31"></a>Personnaliser une image de démarrage qui utilise Windows PE 3.1  
 Pour personnaliser une image de démarrage qui utilise WinPE 3.1, vous devez installer Windows AIK, installer le supplément Windows AIK pour Windows 7 SP1 et utiliser l'outil de ligne de commande DISM pour monter l'image de démarrage, ajouter des composants et des pilotes facultatifs et appliquer les modifications à l'image de démarrage. Pour personnaliser l'image de démarrage, procédez comme suit.  

#### <a name="to-customize-a-boot-image-that-uses-windows-pe-31"></a>Pour personnaliser une image de démarrage qui utilise Windows PE 3.1  

1. Installez Windows AIK sur un ordinateur qui n’a pas d’autre version de Windows AIK ni de Windows ADK, et sur lequel aucun composant Configuration Manager n’est installé. Téléchargez le kit Windows AIK depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=5753).  

2. Installez le supplément Windows AIK pour Windows 7 avec SP1 sur l'ordinateur de l'étape 1. Téléchargez le supplément Windows AIK pour Windows 7 SP1 depuis le [Centre de téléchargement Microsoft](http://www.microsoft.com/download/details.aspx?id=5188).  

3. Copiez l’image de démarrage (wimpe.wim) qui se trouve dans le dossier d’installation Windows AIK (par exemple, <*chemin_installation*>\Windows AIK\Tools\PETools\amd64\\) vers un dossier de l’ordinateur à partir duquel vous personnaliserez l’image de démarrage. Cette procédure utilise C:\WinPEWAIK comme nom de dossier.  

4. Utilisez DISM pour monter l'image de démarrage dans un dossier Windows PE local. Par exemple, tapez la ligne de commande suivante :  

    **dism.exe /mount-wim /wimfile:C:\WinPEWAIK\winpe.wim /index:1 /mountdir:C:\WinPEMount**  

    Où C:\WinPEWAIK est le dossier qui contient l'image de démarrage et C:\WinPEMount est le dossier monté.  

   > [!NOTE]
   >  Pour plus d’informations sur DISM, consultez la rubrique [Informations techniques de référence sur l’outil Gestion et maintenance des images de déploiement](https://technet.microsoft.com/library/dd744256\(v=ws.10\).aspx) dans la bibliothèque de documentation TechNet Windows 7.  

5. Une fois que vous avez monté l'image de démarrage, utilisez DISM pour ajouter des composants facultatifs à l'image de démarrage. Dans Windows PE 3.1, par exemple, les composants facultatifs sont situés dans <*chemin_installation*>\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\.  

   > [!NOTE]
   >  Cette procédure utilise l’emplacement suivant pour les composants facultatifs : C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs. Le chemin d'accès que vous utilisez peut être différent selon les options de version et d'installation que vous choisissez pour le kit Windows AIK.  

    Tapez la commande suivante pour installer les composants facultatifs :  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wmi.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-scripting.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\winpe-wds-tools.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wmi_** *<paramètres régionaux\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-scripting_** *<paramètres régionaux\>* **.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\\** *<locale\>* **\winpe-wds-tools_** *<paramètres régionaux\>* **.cab"**  

    Où C:\WinPEMount est le dossier monté et paramètres régionaux désigne les paramètres régionaux des composants. Par exemple, pour les paramètres régionaux **fr-fr** , tapez :  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wmi_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-scripting_en-us.cab"**  

    **dism.exe /image:C:\WinPEMount /add-package /packagepath:"C:\Program Files\Windows AIK\Tools\PETools\amd64\WinPE_FPs\en-us\winpe-wds-tools_en-us.cab"**  

   > [!TIP]
   >  Pour plus d’informations sur les différents packages que vous pouvez ajouter à l’image de démarrage, consultez la rubrique [Ajouter un package à une image Windows PE](https://technet.microsoft.com/library/dd799312\(v=WS.10\).aspx) dans la bibliothèque de documentation TechNet Windows 7.  

6. Utilisez DISM pour ajouter des pilotes spécifiques à l'image de démarrage, si nécessaire. Tapez la commande suivante pour ajouter des pilotes à l'image de démarrage, si nécessaire :  

    **dism.exe /image:C:\WinPEMount /add-driver /driver:&lt;** *chemin d'accès au fichier .inf du pilote* **>**  

    Où C:\WinPEMount est le dossier monté.  

7. Tapez la commande suivante pour démonter le fichier image de démarrage et valider les modifications.  

    **dism.exe /unmount-wim /mountdir:C:\WinPEMount /commit**  

    Où C:\WinPEMount est le dossier monté.  

8. Ajoutez l’image de démarrage mise à jour à Configuration Manager pour pouvoir l’utiliser dans vos séquences de tâches. Utilisez les étapes suivantes pour importer l'image de démarrage mise à jour :  

   1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

   2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

   3. Dans l'onglet **Accueil** , dans le groupe **Créer** , cliquez sur **Ajouter une image de démarrage** pour démarrer l'Assistant Ajout d'une image de démarrage.  

   4. Sur la page **Source de données** , spécifiez les options suivantes et cliquez sur **Suivant**.  

      - Dans la zone **Chemin d'accès** , indiquez le chemin d'accès au fichier de l'image de démarrage mis à jour. Le chemin d'accès spécifié doit être un chemin d'accès réseau valide au format UNC. Par exemple : **\\\\<** <em>nom_serveur</em> **>\\<** <em>partage WinPEWAIK</em> **>\winpe.wim**.  

      - Sélectionnez l'image de démarrage dans la liste déroulante **Image de démarrage** . Si le fichier WIM contient plusieurs images de démarrage, chaque image est répertoriée.  

   5. Sur la page **Général** , spécifiez les options suivantes et cliquez sur **Suivant**.  

      -   Dans la zone **Nom** , spécifiez un nom unique pour l'image de démarrage.  

      -   Dans la zone **Version** , spécifiez un numéro de version pour l'image de démarrage.  

      -   Dans la zone **Commentaire** , spécifiez une description sommaire de l'utilisation de l'image de démarrage.  

   6. Effectuez toutes les étapes de l'Assistant.  

9. Vous pouvez activer une invite de commandes dans l'image de démarrage pour le débogage et le dépannage dans Windows PE. Utilisez les étapes suivantes pour activer l'invite de commandes.  

   1. Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

   2. Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

   3. Recherchez la nouvelle image de démarrage dans la liste et identifiez l'ID de package pour l'image. Vous pouvez trouver l'ID de package dans la colonne **ID de l'image** pour l'image de démarrage.  

   4. À partir d'une invite de commande, tapez **wbemtest** pour ouvrir le testeur WMI.  

   5. Tapez **\\\\<** <em>ordinateur_fournisseur_SMS</em> **>\root\sms\site_<** <em>code_site</em> **>** dans **Espace de noms**, puis cliquez sur **Connexion**.  

   6. Cliquez sur **Ouvrir une instance**, tapez **sms_bootimagepackage.packageID="<packageID\>"** , puis cliquez sur **OK**. Pour packageID, entrez la valeur que vous avez identifiée à l'étape 3.  

   7. Cliquez sur **Actualiser l'objet**, puis cliquez sur **EnableLabShell** dans le volet **Propriétés** .  

   8. Cliquez sur **Modifier la propriété**, remplacez la valeur par **TRUE**, puis cliquez sur **Enregistrer la propriété**.  

   9. Cliquez sur **Enregistrer l'objet**, puis fermez le testeur WMI.  

10. Vous devez distribuer l'image de démarrage vers des points de distribution, des groupes de points de distribution ou des regroupements associés à des groupes de points de distribution avant de pouvoir utiliser l'image de démarrage dans une séquence de tâches. Pour distribuer l'image de démarrage, procédez comme suit.  

    1.  Dans la console Configuration Manager, cliquez sur **Bibliothèque de logiciels**.  

    2.  Dans l'espace de travail **Bibliothèque de logiciels** , développez **Systèmes d'exploitation**, puis cliquez sur **Images de démarrage**.  

    3.  Cliquez sur l'image de démarrage identifiée à l'étape 3.  

    4.  Dans l'onglet **Accueil** , dans le groupe **Déploiement** , cliquez sur **Mettre à jour les points de distribution**.  
