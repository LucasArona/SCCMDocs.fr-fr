---
title: Sécurité et confidentialité de la passerelle de gestion cloud
description: Découvrez les conseils et les recommandations en matière de sécurité et de confidentialité concernant la passerelle de gestion cloud.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7304730b-b517-4c76-aadd-4cbd157dc971
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9ff03c20ccbb79a527f23b6c5cf0cd179751e980
ms.sourcegitcommit: f9654cd1a3af6d67de52fedaccceb2e22dafc159
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67677754"
---
# <a name="security-and-privacy-for-the-cloud-management-gateway"></a>Sécurité et confidentialité de la passerelle de gestion cloud

*S’applique à : System Center Configuration Manager (Current Branch)*

Cet article inclut des informations sur la sécurité et la confidentialité pour la passerelle de gestion cloud (CMG) Configuration Manager. Pour plus d’informations, consultez [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).

## <a name="cmg-security-details"></a>Informations sur la sécurité de la passerelle de gestion cloud (CMG)
- La passerelle de gestion cloud accepte et gère les connexions à partir de points de connexion CMG. Elle utilise l’authentification mutuelle SSL à l’aide de certificats et d’ID de connexion.
- La passerelle de gestion cloud accepte et transfère les requêtes client à l’aide des méthodes suivantes :
    - Authentifie au préalable les connexions à l’aide d’un protocole SSL mutuel avec le certificat d’authentification client basé sur une infrastructure à clé publique (PKI) ou Azure AD. 
      - IIS sur les instances de machine virtuelle de la passerelle de gestion cloud vérifie que le chemin du certificat basé sur les certificats racines approuvés est chargé sur la passerelle de gestion cloud.
      - IIS sur les instances de machine virtuelle vérifie également la révocation des certificats clients, si elle est activée. Pour plus d’informations, consultez [Publication de la liste de révocation de certificats](#bkmk_crl).
    - La liste de certificats de confiance vérifie la racine du certificat d’authentification client. Elle effectue également la même validation que le point de gestion pour le client. Pour plus d’informations, consultez [Examiner les entrées de la liste de certificats de confiance du site](#bkmk_ctl).
    - Valide et filtre les requêtes client (URL) pour vérifier si un point de connexion CMG peut traiter la requête.  
    - Vérifie la longueur du contenu pour chaque point de terminaison de publication.
    - Utilise le comportement de tourniquet (round robin) pour équilibrer la charge des points de connexion CMG sur le même site.
- Le point de connexion CMG utilise les méthodes suivantes :
    - Crée des connexions HTTPS/TCP cohérentes pour toutes les instances de machine virtuelle à la passerelle de gestion cloud. Il vérifie et gère ces connexions toutes les minutes.
    - Utilise l’authentification mutuelle SSL avec la passerelle de gestion cloud à l’aide de certificats.
    - Transfère les requêtes client basées sur des mappages d’URL.
    - Indique l’état de la connexion pour afficher l’état d’intégrité du service dans la console.
    - Indique le trafic par point de terminaison toutes les cinq minutes.

### <a name="configuration-manager-client-facing-roles"></a>Rôles Configuration Manager utilisés par le client
Le point de gestion et le point de mise à jour logicielle hébergent des points de terminaison dans IIS pour traiter les requêtes client. La passerelle de gestion cloud n’expose pas tous les points de terminaison internes. Chaque point de terminaison publié sur la passerelle CMG comporte un mappage d’URL.
  - L’URL externe est celle que le client utilise pour communiquer avec la passerelle CMG.
  - L’URL interne est le point de connexion CMG utilisé pour transférer les demandes vers le serveur interne.

#### <a name="url-mapping-example"></a>Exemple de mappage d’URL
Quand vous activez le trafic CMG sur un point de gestion, Configuration Manager crée un ensemble interne de mappages d’URL pour chaque serveur de point de gestion. Par exemple : ccm_system, ccm_incoming et sms_mp. L’URL externe du point de terminaison ccm_system du point de gestion peut se présenter ainsi :  
`https://<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>/CCM_System`  
L’URL est unique pour chaque point de gestion. Le client Configuration Manager place ensuite le nom du point de gestion activé pour la passerelle de gestion cloud dans sa liste de points de gestion Internet. Ce nom se présente comme suit :  
`<CMG service name>/CCM_Proxy_MutualAuth/<MP Role ID>`  
Le site charge automatiquement toutes les URL externes publiées sur la passerelle de gestion cloud. Ce comportement permet à la passerelle de gestion cloud d’effectuer un filtrage des URL. Tous les mappages d’URL sont répliqués sur le point de connexion CMG. Il transfère ensuite la communication vers les serveurs internes en fonction de l’URL externe à partir de la requête client.



## <a name="security-guidance-for-cmg"></a>Conseils en matière de sécurité pour la passerelle de gestion cloud


<a name="bkmk_crl"></a>

### <a name="publish-the-certificate-revocation-list"></a>Publication de la liste de révocation de certificats

Publiez la liste de révocation de certificats de votre infrastructure à clé publique (PKI) pour permettre l’accès des clients Internet. Quand vous déployez une passerelle de gestion cloud à l’aide de l’infrastructure à clé publique, configurez le service sur **Vérifier la révocation des certificats clients** sous l’onglet Paramètres. Ce paramètre configure le service pour qu’il utilise une liste de révocation de certificats publiée. Pour plus d’informations, consultez [Planifier la révocation de certificats PKI](/sccm/core/plan-design/security/plan-for-security#BKMK_PlanningForCRLs).



<a name="bkmk_ctl"></a>

### <a name="review-entries-in-the-sites-certificate-trust-list"></a>Examiner les entrées de la liste de certificats de confiance du site
<!--503739-->
Chaque site Configuration Manager inclut une liste d’autorités de certification racines de confiance, la liste de certificats de confiance (CTL, Certificate Trust List). Pour consulter et modifier cette liste, accédez à l’espace de travail Administration, développez Configuration du site, puis sélectionnez Sites. Sélectionnez un site, puis cliquez sur Propriétés dans le ruban. Basculez vers l’onglet Communication de l’ordinateur client, puis cliquez sur **Définir** sous Autorités de certification racines de confiance.
 
Utilisez une liste de certificats de confiance plus restrictive pour un site avec une passerelle de gestion cloud à l’aide de l’authentification client PKI. Sinon, les clients disposant de certificats d’authentification client émis par toute racine de confiance qui existe déjà sur le point de gestion sont automatiquement acceptés pour l’inscription du client.

Ce sous-ensemble confère aux administrateurs un contrôle accru de la sécurité. La liste de certificats de confiance limite le serveur à accepter uniquement les certificats clients émis par les autorités de certification figurant dans cette liste. Par exemple, Windows est fourni avec différents certificats d’autorités de certification tierces renommées, telles que VeriSign et Thawte. Par défaut, l’ordinateur qui exécute les services Internet (IIS) approuve les certificats liés à ces autorités de certification connues. Sans configuration d’IIS avec une liste de certificats de confiance, tout ordinateur avec un certificat client publié par ces autorités de certification est accepté comme client Configuration Manager valide. Si vous configurez IIS avec une liste de certificats de confiance qui ne comprend pas ces autorités de certification, les connexions clientes sont rejetées si le certificat était lié à ces autorités de certification. 


<!--486209-->


<!-- ## Privacy information for CMG -->


## <a name="next-steps"></a>Étapes suivantes

- [Planifier la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)
- [Configurer la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [Questions fréquentes (FAQ) sur la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [Certificats pour la passerelle de gestion cloud](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)
