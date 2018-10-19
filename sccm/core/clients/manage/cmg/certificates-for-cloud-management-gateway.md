---
title: Certificats de passerelle de gestion cloud
description: Découvrez les différents certificats numériques à utiliser avec la passerelle de gestion cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 09/10/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: 052210b53ec330a75d73508ae41218231bd75153
ms.sourcegitcommit: 65423b94f0fee5dc5026804d88f13416872b93d4
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/25/2018
ms.locfileid: "47173476"
---
# <a name="certificates-for-the-cloud-management-gateway"></a>Certificats pour la passerelle de gestion cloud

*S’applique à : System Center Configuration Manager (Current Branch)*

Selon le scénario que vous utilisez pour gérer des clients sur Internet avec la passerelle de gestion cloud, vous avez besoin d’un ou de plusieurs certificats numériques. Pour plus d’informations sur les différents scénarios, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


### <a name="general-information"></a>Informations générales
<!--SCCMDocs issue #779--> Les certificats pour la passerelle de gestion cloud prennent en charge les configurations suivantes :  

- **Longueur de clé de 4 096 bits**  

- À compter de la version 1710, prise en charge des certificats **Version 3**. Pour plus d’informations, consultez [Vue d’ensemble des certificats CNG](/sccm/core/plan-design/network/cng-certificates-overview).  

- À compter de la version 1802, quand vous configurez Windows avec la stratégie suivante : **Chiffrement système : utilisez des algorithmes compatibles FIPS pour le chiffrement, le hachage et la signature**  

- À compter de la version 1802, prise en charge de **TLS 1.2**. Pour plus d’informations, consultez [Informations techniques de référence sur les contrôles de chiffrement](/sccm/core/plan-design/security/cryptographic-controls-technical-reference#about-ssl-vulnerabilities).  



## <a name="cmg-server-authentication-certificate"></a>Certificat d’authentification serveur de passerelle de gestion cloud

*Ce certificat est obligatoire dans tous les scénarios.*

Vous fournissez ce certificat lors de la création de la passerelle de gestion cloud dans la console Configuration Manager.

La passerelle de gestion cloud crée un service HTTPS auquel les clients Internet se connectent. Le serveur nécessite un certificat d’authentification serveur pour créer le canal sécurisé. Faites l’acquisition d’un certificat à cet effet auprès d’un fournisseur public ou émettez-le à partir de votre infrastructure à clé publique. Pour plus d’informations, consultez [Certificat racine approuvé de passerelle de gestion cloud pour les clients](#cmg-trusted-root-certificate-to-clients).

 > [!TIP]
 > Ce certificat nécessite un nom global unique pour identifier le service dans Azure. Avant de demander un certificat, vérifiez que le nom de domaine Azure souhaité est unique. Par exemple, *GraniteFalls.CloudApp.Net*. Connectez-vous au [portail Microsoft Azure](https://portal.azure.com). Sélectionnez **Créer une ressource**, choisissez la catégorie **Calcul**, puis sélectionnez **Service cloud**. Dans le champ **Nom DNS**, tapez le préfixe souhaité, par exemple *GraniteFalls*. L’interface indique si le nom de domaine est disponible ou déjà utilisé par un autre service. Ne créez pas le service dans le portail ; utilisez ce processus seulement pour vérifier la disponibilité du nom. 
  
 > [!NOTE]
 > À compter de la version 1802, le certificat d’authentification du serveur de passerelle de gestion cloud prend en charge les caractères génériques. Certaines autorités de certification émettent des certificats en utilisant un caractère générique pour le nom d’hôte. Par exemple, **\*.contoso.com**. Certaines organisations utilisent des certificats génériques pour simplifier leur infrastructure à clé publique et réduire les coûts de maintenance.<!--491233-->  
 > 
 > Pour plus d’informations sur l’utilisation d’un certificat générique avec une passerelle de gestion cloud, consultez [Configurer une passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway#set-up-a-cmg).<!--SCCMDocs issue #565-->  


### <a name="cmg-trusted-root-certificate-to-clients"></a>Certificat racine approuvé de passerelle de gestion cloud pour les clients

Les clients doivent approuver le certificat d’authentification serveur de la passerelle de gestion cloud. Deux méthodes existent pour effectuer cette approbation : 

- Utiliser un certificat provenant d’un fournisseur de certificats public et approuvés globalement. Par exemple, DigiCert, Thawte ou VeriSign (liste non limitative). Les clients Windows incluent des autorités de certification racine approuvées provenant de ces fournisseurs. Si vous utilisez un certificat d’authentification serveur émis par un de ces fournisseurs, vos clients l’approuvent automatiquement.  

- Utiliser un certificat émis par une autorité de certification d’entreprise depuis votre infrastructure à clé publique. La plupart des implémentations d’infrastructure à clé publique d’entreprise ajoutent les autorités de certification racine de confiance aux clients Windows. Par exemple, dans le cas d’une utilisation des services de certificats Active Directory avec la stratégie de groupe. Si vous émettez le certificat d’authentification serveur de passerelle de gestion cloud depuis une autorité de certification que vos clients n’approuvent pas automatiquement, ajoutez le certificat racine approuvé de l’autorité de certification aux clients Internet.  

    - Vous pouvez également utiliser des profils de certificat Configuration Manager pour provisionner des certificats sur les clients. Pour plus d’informations, consultez [Présentation des profils de certificat](/sccm/protect/deploy-use/introduction-to-certificate-profiles).  

> [!Note]  
> À compter de la version 1806, quand vous créez une passerelle de gestion cloud, vous n’êtes plus obligé de fournir un certificat racine approuvé dans la page Paramètres. Ce certificat n’est pas nécessaire lorsque vous utilisez Azure Active Directory (Azure AD) pour l’authentification client, mais il était auparavant nécessaire dans l’Assistant. Si vous utilisez des certificats d’authentification client PKI, vous devez néanmoins encore ajouter un certificat racine approuvé pour la passerelle de gestion cloud.<!--SCCMDocs-pr issue #2872-->  


### <a name="server-authentication-certificate-issued-by-public-provider"></a>Certificat d’authentification serveur émis par le fournisseur public

Un fournisseur de certificats tiers ne peut pas créer un certificat pour CloudApp.net, car ce domaine est détenu par Microsoft. Vous pouvez seulement obtenir un certificat émis pour un domaine qui vous appartient. La principale raison pour acquérir un certificat auprès d’un fournisseur tiers est que vos clients approuvent déjà le certificat de racine de ce fournisseur.

Pour créer un alias DNS, procédez comme suit :

1. Créez un enregistrement de nom canonique (CNAME) dans le DNS public de votre organisation. Cet enregistrement crée un alias pour la passerelle de gestion cloud avec un nom convivial que vous utilisez dans le certificat public.

    Par exemple, Contoso nomme sa passerelle de gestion cloud **GraniteFalls**, qui devient **GraniteFalls.CloudApp.Net** dans Azure. Dans l’espace de noms contoso.com du DNS public de Contoso, l’administrateur DNS crée un enregistrement CNAME pour **GraniteFalls.Contoso.com** pour le nom d’hôte réel, **GraniteFalls.CloudApp.net**.  

2. Demandez à un fournisseur public un certificat d’authentification serveur en utilisant le nom commun (CN) de l’alias CNAME.
Par exemple, Contoso utilise **GraniteFalls.Contoso.com** comme nom commun du certificat.  

3. Créez la passerelle de gestion cloud dans la console Configuration Manager avec ce certificat. Dans la page **Paramètres** de l’Assistant Création d’une passerelle de gestion cloud :   

    - Quand vous ajoutez le certificat de serveur pour ce service cloud (depuis le **fichier de certificat**), l’Assistant extrait le nom d’hôte du certificat CN comme nom du service.  

    - Il ajoute ensuite ce nom d’hôte à **cloudapp.net** ou à **usgovcloudapp.net** pour le cloud Azure US Government, comme nom de domaine complet du service pour créer le service dans Azure.  

    - Par exemple, quand Contoso crée la passerelle de gestion cloud, Configuration Manager extrait le nom d’hôte **GraniteFalls** du nom commun du certificat. Azure crée le service proprement dit sous le nom **GraniteFalls.CloudApp.net**.  

Quand vous créez l’instance de la passerelle de gestion cloud dans Configuration Manager, alors que le certificat comporte GraniteFalls.Contoso.com, Configuration Manager extrait seulement le nom d’hôte, par exemple GraniteFalls. Il ajoute ce nom d’hôte à CloudApp.net, ce qui est exigé par Azure lors de la création d’un service cloud. L’alias CNAME dans l’espace de noms DNS pour votre domaine, Contoso.com, mappe ces deux noms de domaine complets. Configuration Manager donne aux clients une stratégie pour accéder à cette passerelle de gestion cloud et le mappage DNS les lie ensemble pour qu’ils puissent accéder de façon sécurisée au service dans Azure.<!--SCCMDocs issue #565-->  


### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>Certificat d’authentification serveur émis par l’infrastructure à clé publique d’entreprise

Créez un certificat SSL personnalisé pour la passerelle de gestion cloud de la même façon que pour un point de distribution cloud. Suivez les instructions pour le [déploiement du certificat de service pour les points de distribution cloud](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012), mais procédez différemment pour ce qui suit :

- Lors de la demande du certificat de serveur web personnalisé, fournissez un nom de domaine complet pour le nom commun du certificat. Il peut s’agir d’un nom de domaine public qui vous appartient, ou bien vous pouvez utiliser le domaine cloudapp.net. Si vous utilisez votre propre domaine public, référez-vous au processus ci-dessus concernant la création d’un alias DNS dans le DNS public de votre organisation.  

- Quand vous utilisez le domaine public cloudapp.net pour le certificat de serveur web de passerelle de gestion cloud :  

    - Sur le cloud public Azure, utilisez un nom qui se termine par **cloudapp.net**  

    - Utilisez un nom qui se termine par **usgovcloudapp.net** pour le cloud Azure US Government  



## <a name="azure-management-certificate"></a>Certificat de gestion Azure

*Ce certificat est obligatoire pour les déploiements de services classiques. Il n’est pas nécessaire pour les déploiements Azure Resource Manager.*

Vous fournissez ce certificat dans le portail Azure, lors de la création de la passerelle de gestion cloud dans la console Configuration Manager.

Pour créer la passerelle de gestion cloud dans Azure, le point de connexion du service Configuration Manager doit d’abord s’authentifier auprès de votre abonnement Azure. Lors de l’utilisation d’un déploiement de service classique, il utilise le certificat de gestion Azure pour cette authentification. Un administrateur Azure charge ce certificat sur votre abonnement. Quand vous créez la passerelle de gestion cloud dans la console Configuration Manager, fournissez ce certificat.

Pour plus d’informations et des instructions sur la manière de charger un certificat de gestion, consultez les articles suivants dans la documentation Azure :

- [Services cloud et certificats de gestion](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)  

- [Charger un certificat de gestion de service Azure](https://docs.microsoft.com/azure/azure-api-management-certs)  

> [!IMPORTANT]
> Veillez à copier l’ID d’abonnement associé au certificat de gestion. Vous l’utilisez pour la création de la passerelle de gestion cloud dans la console Configuration Manager.



## <a name="client-authentication-certificate"></a>Certificat d'authentification client

*Ce certificat est obligatoire pour les clients Internet exécutant Windows 7 ou Windows 8.1, et pour les appareils Windows 10 non joints à Azure Active Directory (Azure AD). Il est également obligatoire sur le point de connexion de passerelle de gestion cloud. Il n’est pas nécessaire pour les clients Windows 10 joints à Azure AD.*

Les clients utilisent ce certificat pour s’authentifier auprès de la passerelle de gestion cloud. Les appareils Windows 10 qui sont hybrides ou joints à un domaine cloud ne nécessitent pas ce certificat, car ils utilisent Azure AD pour s’authentifier.

Provisionnez ce certificat en dehors du contexte de Configuration Manager. Par exemple, utilisez les services de certificats Active Directory et la stratégie de groupe pour émettre des certificats d’authentification clients. Pour plus d’informations, consultez [Déploiement du certificat client pour les ordinateurs Windows](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012).


### <a name="client-trusted-root-certificate-to-cmg"></a>Certificat racine approuvé de client pour la passerelle de gestion cloud

*Ce certificat est obligatoire lors de l’utilisation de certificats d’authentification clients. Quand tous les clients utilisent Azure AD pour l’authentification, ce certificat n’est pas nécessaire.* 

Vous fournissez ce certificat lors de la création de la passerelle de gestion cloud dans la console Configuration Manager.

La passerelle de gestion cloud doit approuver les certificats d’authentification clients. Pour effectuer cette approbation, fournissez la chaîne de certificats racines approuvés. Vous pouvez spécifier deux autorités de certification racines de confiance et quatre autorités de certification (subordonnées) intermédiaires. 


#### <a name="export-the-client-certificates-trusted-root"></a>Exporter la racine de confiance du certificat client

Après avoir émis un certificat d’authentification client pour un ordinateur, utilisez ce processus sur cet ordinateur pour exporter la racine de confiance.

1.  Ouvrez le menu Démarrer. Tapez « run » pour ouvrir la fenêtre Exécuter. Ouvrez `mmc`.  

2.  Dans le menu Fichier, choisissez **Ajouter/supprimer un composant logiciel enfichable**.  

3.  Dans la boîte de dialogue Ajouter ou supprimer des composants logiciels enfichables, sélectionnez **Certificats**, puis sélectionnez **Ajouter**.  

    a. Dans la boîte de dialogue Composant logiciel enfichable Certificats, sélectionnez **Compte d’ordinateur**, puis sélectionnez **Suivant**.  

    b. Dans la boîte de dialogue Sélectionner un ordinateur, sélectionnez **Ordinateur local**, puis sélectionnez **Terminer**.  

    c. Dans la boîte de dialogue Ajouter ou supprimer des composants logiciels enfichables, sélectionnez **OK**.  

4.  Développez **Certificats**, développez **Personnel**, puis sélectionnez **Certificats**.  

5.  Sélectionnez un certificat dont le rôle prévu est **Authentification client**.  

    a. Dans le menu Action, sélectionnez **Ouvrir**.  

    b. Accédez à l’onglet **Chemin d’accès de certification**.  

    c. Sélectionnez le certificat suivant plus haut dans la chaîne, puis sélectionnez **Afficher le certificat**.  

6.  Dans cette boîte de dialogue Nouveau certificat, accédez à l’onglet **Détails**. Sélectionnez **Copier dans un fichier...**.  

7.  Effectuez l’Assistant Exportation de certificat en utilisant le format de certificat par défaut, **X.509 binaire encodé DER (*.cer)**. Notez le nom et l’emplacement du certificat exporté.  

8. Exportez tous les certificats dans le chemin de certification du certificat d’authentification client d’origine. Notez quels certificats exportés sont des autorités de certification intermédiaires, et lesquels sont des autorités de certification racines de confiance.  



## <a name="enable-management-point-for-https"></a>Activer le point de gestion pour HTTPS

*Spécifications pour les certificats*

- Dans les versions 1706 ou 1710, lors de la gestion de clients traditionnels avec des identités locales en utilisant un certificat d’authentification client, ce certificat est recommandé mais pas obligatoire.  

- Dans la version 1710, lors de la gestion de clients Windows 10 joints à Azure AD, ce certificat est obligatoire pour les points de gestion.  

- À compter de la version 1802, ce certificat est obligatoire dans tous les scénarios. Seuls les points de gestion que vous activez pour la passerelle de gestion cloud doivent être HTTPS. Ce changement de comportement offre une meilleure prise en charge de l’authentification basée sur un jeton Azure AD.  

Provisionnez ce certificat en dehors du contexte de Configuration Manager. Par exemple, utilisez les services de certificats Active Directory et la stratégie de groupe pour émettre un certificat de serveur web. Pour plus d’informations, consultez [Spécifications pour les certificats d’infrastructure à clé publique](/sccm/core/plan-design/network/pki-certificate-requirements) et [Déployer le certificat de serveur web pour les systèmes de site qui exécutent IIS](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012).



## <a name="next-steps"></a>Étapes suivantes

- [Configurer la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Questions fréquentes (FAQ) sur la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Sécurité et confidentialité de la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
