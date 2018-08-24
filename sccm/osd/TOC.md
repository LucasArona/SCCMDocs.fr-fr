# Comprendre et explorer
## [Présentation du déploiement de système d’exploitation](understand/introduction-to-operating-system-deployment.md)

# Planifier et concevoir
## [Configuration requise de l’infrastructure pour le déploiement de système d’exploitation](plan-design/infrastructure-requirements-for-operating-system-deployment.md)
## [Considérations relatives à la planification de l’automatisation des tâches](plan-design/planning-considerations-for-automating-tasks.md)
## [Sécurité et confidentialité pour le déploiement de système d’exploitation](plan-design/security-and-privacy-for-operating-system-deployment.md)
## [Planification de l’interopérabilité pour le déploiement de système d’exploitation](plan-design/planning-for-operating-system-deployment-interoperability.md)

# Bien démarrer
## [Préparer des rôles de système de site pour les déploiements de système d’exploitation](get-started/prepare-site-system-roles-for-operating-system-deployments.md)
## [Préparer le déploiement du système d’exploitation](get-started/prepare-for-operating-system-deployment.md)
### [Gérer les images de démarrage](get-started/manage-boot-images.md)
#### [Personnaliser les images de démarrage](get-started/customize-boot-images.md)

### [Gérer les images de système d’exploitation](get-started/manage-operating-system-images.md)
#### [Personnaliser les images de système d’exploitation](get-started/customize-operating-system-images.md)

### [Gérer les packages de mise à niveau de système d’exploitation](get-started/manage-operating-system-upgrade-packages.md)
### [Gérer les pilotes](get-started/manage-drivers.md)
### [Gérer l’état utilisateur](get-started/manage-user-state.md)
### [Préparer les déploiements d’ordinateurs inconnus](get-started/prepare-for-unknown-computer-deployments.md)
### [Associer des utilisateurs à un ordinateur de destination](get-started/associate-users-with-a-destination-computer.md)

## [Préparer la mise en cache d’homologue Windows PE pour réduire le trafic WAN](get-started/prepare-windows-pe-peer-cache-to-reduce-wan-traffic.md)

# Déployer et utiliser
## [Scénarios de déploiement de systèmes d’exploitation d’entreprise](deploy-use/scenarios-to-deploy-enterprise-operating-systems.md)
### [Effectuer une mise à niveau de Windows vers la dernière version](deploy-use/upgrade-windows-to-the-latest-version.md)
### [Actualiser un ordinateur existant avec une nouvelle version de Windows](deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md)
### [Installer une nouvelle version de Windows sur un nouvel ordinateur (système nu)](deploy-use/install-new-windows-version-new-computer-bare-metal.md)
### [Remplacement d’un ordinateur existant et transfert des paramètres](deploy-use/replace-an-existing-computer-and-transfer-settings.md)

## [Méthodes pour déployer des systèmes d’exploitation d’entreprise](deploy-use/methods-to-deploy-enterprise-operating-systems.md)
### [Utiliser PXE pour déployer Windows sur le réseau](deploy-use/use-pxe-to-deploy-windows-over-the-network.md)
### [Utiliser le Centre logiciel pour déployer Windows sur le réseau](deploy-use/use-software-center-to-deploy-windows-over-the-network.md)
### [Utiliser un média de démarrage pour déployer Windows sur le réseau](deploy-use/use-bootable-media-to-deploy-windows-over-the-network.md)
### [Utiliser un média autonome pour déployer Windows sans utiliser le réseau](deploy-use/use-stand-alone-media-to-deploy-windows-without-using-the-network.md)
### [Utiliser la multidiffusion pour déployer Windows sur le réseau](deploy-use/use-multicast-to-deploy-windows-over-the-network.md)
### [Créer une image pour un fabricant OEM en usine ou dépôt local](deploy-use/create-an-image-for-an-oem-in-factory-or-a-local-depot.md)
### [Déployer Windows To Go](deploy-use/deploy-windows-to-go.md)

## [Gérer Windows en tant que service](deploy-use/manage-windows-as-a-service.md)
## [Créer un déploiement par phases](deploy-use/create-phased-deployment-for-task-sequence.md)
## [Gérer et effectuer le monitoring des déploiements par phases](deploy-use/manage-monitor-phased-deployments.md)
## [Superviser les déploiements de système d’exploitation](deploy-use/monitor-operating-system-deployments.md)

## [Gérer les séquences de tâches pour automatiser des tâches](deploy-use/manage-task-sequences-to-automate-tasks.md)
### [Créer une séquence de tâches pour installer un système d’exploitation](deploy-use/create-a-task-sequence-to-install-an-operating-system.md)
### [Créer une séquence de tâches pour mettre à niveau un système d’exploitation](deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md)
### [Créer une séquence de tâches pour capturer un système d’exploitation](deploy-use/create-a-task-sequence-to-capture-an-operating-system.md)
### [Créer une séquence de tâches pour capturer et restaurer l’état utilisateur](deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md)
### [Utiliser une séquence de tâches pour gérer des disques durs virtuels](deploy-use/use-a-task-sequence-to-manage-virtual-hard-disks.md)

## Scénarios de séquence de tâches personnalisée
### [Créer une séquence de tâches personnalisée](deploy-use/create-a-custom-task-sequence.md)
### [Créer une séquence de tâches pour les déploiements autres que les déploiements de système d’exploitation](deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md)
### [Étapes de séquence de tâches pour gérer la conversion du BIOS en UEFI](deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md)
### [Préparer la mise en service de BitLocker dans Windows PE](deploy-use/preprovision-bitlocker-in-windows-pe.md)

## [Créer un média de séquence de tâches](deploy-use/create-task-sequence-media.md)
### [Créer un média autonome](deploy-use/create-stand-alone-media.md)
### [Créer un média préparé](deploy-use/create-prestaged-media.md)
### [Créer un média de démarrage](deploy-use/create-bootable-media.md)
### [Créer un média de capture](deploy-use/create-capture-media.md)

# Informations techniques de référence
## [Étapes de séquence de tâches](understand/task-sequence-steps.md)
## [Comment utiliser les variables de séquence de tâches](understand/using-task-sequence-variables.md)
## [Variables de séquence de tâches](understand/task-sequence-variables.md)
## [Commandes de prédémarrage pour les médias de séquence de tâches](understand/prestart-commands-for-task-sequence-media.md)

