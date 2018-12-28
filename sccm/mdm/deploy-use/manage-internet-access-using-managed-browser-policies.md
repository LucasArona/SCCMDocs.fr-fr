---
title: Gérer l'accès à Internet à l'aide de stratégies Managed Browser
titleSuffix: Configuration Manager
description: Déployez Intune Managed Browser pour gérer et limiter l’accès à Internet.
ms.date: 07/06/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 8e25e00c-c9a8-473f-bcb7-ea989f6ca3c5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2483a15286a2784f2fb8a4256029004374a313dc
ms.sourcegitcommit: 48098f9fb2f447672bf36d50c9f58a3d26acb9ed
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53419782"
---
# <a name="manage-internet-access-using-managed-browser-policies-with-system-center-configuration-manager"></a>Gérer l’accès à Internet à l’aide de stratégies Managed Browser avec System Center Configuration Manager

*S’applique à : System Center Configuration Manager (Current Branch)*

Dans System Center Configuration Manager, vous pouvez déployer Intune Managed Browser, application de navigation web, puis l’associer à une stratégie Managed Browser. La stratégie Managed Browser configure une liste autorisée ou une liste bloquée qui restreint les sites web auxquels les utilisateurs de Managed Browser peuvent accéder.  

 Comme il s’agit d’une application gérée, vous pouvez également lui appliquer des stratégies de gestion des applications mobiles, comme le contrôle de l’utilisation des fonctions de type Copier, Couper et Coller. Cela empêche les captures d’écran et garantit également que les liens vers du contenu ne s’ouvrent que dans d’autres applications gérées. Pour plus d’informations, consultez [Protection d’applications à l’aide de stratégies de gestion des applications mobiles](protect-apps-using-mam-policies.md).  

> [!IMPORTANT]  
>  Si les utilisateurs installent eux-mêmes l'application Managed Browser, celle-ci ne sera pas gérée par les stratégies que vous spécifiez. Pour vérifier que le navigateur est géré par Configuration Manager, ils doivent désinstaller l’application avant de la déployer en tant qu’application gérée.  

 Vous pouvez créer des stratégies Managed Browser pour les types d'appareils suivants :  

-   appareils qui exécutent Android 4 et versions ultérieures ;  

-   appareils qui exécutent iOS 7 et versions ultérieures.  

> [!NOTE]  
>  Pour plus d’informations sur l’application Managed Browser Intune et pour la télécharger, consultez [iTunes](https://itunes.apple.com/us/app/microsoft-intune-managed-browser/id943264951?mt=8) pour iOS et [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.intune.mam.managedbrowser&hl=en) pour Android.  

## <a name="create-a-managed-browser-policy"></a>Créer une stratégie Managed Browser  

1.  Dans la console Configuration Manager, choisissez **Bibliothèque de logiciels** > **Gestion des applications** > **Stratégies de gestion d’application**.  

3.  Sous l’onglet **Accueil**, dans le groupe **Créer**, choisissez **Créer une stratégie de gestion d’application**.  

4.  Dans la page **Général**, entrez le nom et la description de la stratégie, puis choisissez **Suivant**.  

5.  Dans la page **Type de stratégie**, sélectionnez la plateforme, **Managed Browser** pour le type de stratégie, puis choisissez **Suivant**.  

     Dans la page **Managed Browser** , sélectionnez l'une des options suivantes :  

    -   **Autoriser Managed Browser à ouvrir uniquement les URL ci-dessous (liste autorisée)**  : spécifiez une liste d’URL pouvant être ouvertes par Managed Browser.  

    -   **Empêcher Managed Browser d’ouvrir les URL ci-dessous (liste bloquée)**  : spécifiez une liste d’URL ne pouvant pas être ouvertes par Managed Browser.  

    > [!NOTE]  
    >  Vous ne pouvez pas inclure des URL autorisées et bloquées dans la même stratégie Managed Browser.  

     Pour plus d’informations sur les formats d’URL que vous pouvez spécifier, consultez Format des URL autorisées et des URL bloquées dans cet article.  

    > [!NOTE]  
    >  Le type de stratégie Général vous permet de modifier les fonctionnalités des applications que vous déployez pour les adapter aux stratégies de sécurité et de conformité de votre entreprise. Par exemple, vous pouvez limiter les opérations Couper, Copier et Coller dans une application restreinte. Pour plus d’informations sur le type de stratégie Général, consultez [Protéger des applications à l’aide de stratégies de gestion des applications mobiles](protect-apps-using-mam-policies.md).  

6.  Fermez l'Assistant.  

La nouvelle stratégie s'affiche dans le nœud **Stratégies de gestion d'application** de l'espace de travail **Bibliothèque de logiciels** .  

## <a name="create-a-software-deployment-for-the-managed-browser-app"></a>Créer un déploiement de logiciel pour l'application Managed Browser  
 Après avoir créé la stratégie Managed Browser, vous pouvez créer un type de déploiement de logiciel pour l'application Managed Browser. Vous devez associer une stratégie Général et une stratégie Managed Browser à l’application Managed Browser.  

 Pour plus d’informations, consultez [Créer des applications](create-applications.md).  

## <a name="security-and-privacy-for-the-managed-browser"></a>Sécurité et confidentialité de Managed Browser  

-   Sur les appareils iOS, les utilisateurs ne peuvent pas ouvrir les sites web possédant un certificat qui a expiré ou qui n’est pas approuvé.  

-   Les paramètres du navigateur intégré définis par les utilisateurs sur leur appareil ne sont pas utilisés par Managed Browser. Managed Browser n’a pas accès à ces paramètres.  

-   Si vous configurez l’option **Demander un code confidentiel simple pour l’accès** ou **Exiger des informations d’identification d’entreprise pour l’accès** dans une stratégie de gestion des applications mobiles associée à Managed Browser, un utilisateur peut cliquer sur Aide dans la page d’authentification et accéder à n’importe quel site, même si celui-ci a été ajouté à une liste bloquée dans la stratégie Managed Browser.  

-   Managed Browser peut uniquement bloquer l'accès aux sites qui font l'objet d'un accès direct. Il ne peut pas bloquer l'accès quand des services intermédiaires (tels qu'un service de traduction) sont utilisés pour accéder au site.  

## <a name="reference-information"></a>Informations de référence  

###  <a name="url-format-for-allowed-and-blocked-urls"></a>Format des URL autorisées et des URL bloquées  

Utilisez les informations suivantes pour en savoir plus sur les formats et les caractères génériques que vous pouvez utiliser pour spécifier des URL dans les listes autorisées et les listes bloquées.  

- Utilisez le caractère générique `*` (astérisque) conformément aux règles de la liste de modèles autorisés ci-dessous.  

- Faites précéder toutes les URL du préfixe **http** ou **https** quand vous les entrez dans la liste.  

- Spécifiez des numéros de port dans l’adresse. Si vous ne spécifiez pas de numéro de port, les valeurs suivantes sont utilisées :  

  - Port 80 pour http  

  - Port 443 pour https  

    N’utilisez pas de caractères génériques pour le numéro de port, car ce n’est pas pris en charge. Par exemple, `http://www.contoso.com:*`   

- Utilisez le tableau suivant pour en savoir plus sur les modèles autorisés que vous pouvez utiliser pour spécifier des URL :  


  |                                           Adresse URL                                            |                                                    Correspond à                                                    |                                    Ne correspond pas à                                     |
  |------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------|
  |                `http://www.contoso.com`<br /><br /> Correspond à une page unique                |                                               `www.contoso.com`                                               |  `host.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `contoso.com/`   |
  |                  `http://contoso.com`<br /><br /> Correspond à une page unique                  |                                                 `contoso.com`                                                 | `host.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `www.contoso.com` |
  | `http://www.contoso.com/*`<br /><br /> Correspond à toutes les URL commençant par `www.contoso.com` |      `www.contoso.com`<br /><br /> `www.contoso.com/images`<br /><br /> `www.contoso.com/videos/tvshows`      |               `host.contoso.com`<br /><br /> `host.contoso.com/images`                |
  |      `http://*.contoso.com/*`<br /><br /> Correspond à tous les sous-domaines sous contoso.com      | `developer.contoso.com/resources`<br /><br /> `news.contoso.com/images`<br /><br /> `news.contoso.com/videos` |                                  `contoso.host.com`                                   |
  |           `http://www.contoso.com/images`<br /><br /> Correspond à un dossier unique            |                                           `www.contoso.com/images`                                            |                             `www.contoso.com/images/dogs`                             |
  |    `http://www.contoso.com:80`<br /><br /> Correspond à une page unique avec un numéro de port    |                                          `http://www.contoso.com:80`                                          |                                                                                       |
  |           `https://www.contoso.com`<br /><br /> Correspond à une page unique sécurisée            |                                           `https://www.contoso.com`                                           |                               `http://www.contoso.com`                                |
  | `http://www.contoso.com/images/*`<br /><br /> Correspond à un dossier unique et à tous ses sous-dossiers |                    `www.contoso.com/images/dogs`<br /><br /> `www.contoso.com/images/cats`                    |                               `www.contoso.com/videos`                                |


- Voici quelques exemples de certaines entrées que vous ne pouvez pas spécifier :  

  -   `*.com`  

  -   `*.contoso/*`  

  -   `www.contoso.com/*images`  

  -   `www.contoso.com/*images*pigs`  

  -   `www.contoso.com/page*`  

  -   Adresses IP  

  -   `https://*`  

  -   `http://*`  

  -   `http://www.contoso.com:*`  

  -   `http://www.contoso.com: /*`  

> [!NOTE]  
>  `*.microsoft.com` est toujours autorisé.  

### <a name="how-conflicts-between-the-allow-and-block-list-are-resolved"></a>Résolution des conflits entre la liste autorisée et la liste bloquée  
 Si plusieurs stratégies Managed Browser sont déployées sur un appareil et qu'un conflit se produit entre les paramètres, le mode (autorisé ou bloqué) et les listes d'URL sont évalués pour déterminer les conflits. En cas de conflit, le comportement suivant s'applique :  

-   Si les modes dans chaque stratégie sont les mêmes, mais que les listes d’URL sont différentes, les URL ne sont pas appliquées sur l’appareil.  

-   Si les modes dans chaque stratégie sont différents, mais que les listes d’URL sont les mêmes, les URL ne sont pas appliquées sur l’appareil.  

-   Si un appareil reçoit des stratégies Managed Browser pour la première fois et qu'un conflit se produit entre deux stratégies, les URL ne sont pas appliquées sur l'appareil. Utilisez le nœud **Conflits de stratégies** de l'espace de travail **Stratégie** pour afficher les conflits.  

-   Si un appareil a déjà reçu une stratégie Managed Browser et qu'une deuxième stratégie est déployée avec des paramètres en conflit, les paramètres d'origine restent sur l'appareil. Utilisez le nœud **Conflits de stratégies** de l'espace de travail **Stratégie** pour afficher les conflits.  
