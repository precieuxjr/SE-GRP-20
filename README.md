# SE-GRP-20
projet _académique


Résumé du Projet
****************


Ce projet consiste en la conception et le déploiement d'une infrastructure de virtualisation complète basée sur les technologies de pointe du monde Open Source : KVM (Kernel-based Virtual Machine) et Libvirt.

L'objectif principal était de transformer un système hôte Ubuntu en un hyperviseur performant capable de gérer simultanément des environnements invités (guests) aux profils radicalement différents, illustrant ainsi la flexibilité de l'allocation des ressources matérielles.

 Détails Techniques de l'Infrastructure
 
•	Architecture de l'Hyperviseur :  Utilisation de KVM comme hyperviseur de type 1/2 hybride, directement intégré au noyau Linux pour des performances quasi-natives.
-	Implémentation de Libvirt comme couche d'abstraction pour standardiser la gestion des machines virtuelles, du stockage et des interfaces réseau.
•	Gestion des environnements virtuels :

1.	Profil Station de Travail (Lubuntu) : Déploiement d'un système graphique utilisant l'environnement de bureau LXQt. Ce choix stratégique a permis de fournir une interface utilisateur complète et ergonomique tout en maintenant une empreinte mémoire vive (RAM) extrêmement faible.

2.	Profil Serveur Minimaliste (Alpine Linux) : Déploiement d'un système ultra-léger (ISO de ~50 Mo) en mode console, optimisé pour une consommation de ressources CPU/RAM quasi nulle au repos, idéal pour l'hébergement de micro-services.
   
•	Stockage et Persistance :
-	Standardisation du stockage dans /var/lib/libvirt/images/ pour une gestion rigoureuse des permissions système (AppArmor/SELinux).
-	Utilisation du format de disque .qcow2, permettant l'allocation dynamique ("Thin Provisioning") et la sécurisation des données via des instantanés (Snapshots).
  
•	Connectivité Réseau :
-	Mise en place d'un pont réseau virtuel (virbr0) avec gestion du NAT.
-	Isolation des machines virtuelles dans un sous-réseau privé avec attribution dynamique d'adresses via un serveur DHCP intégré à Libvirt.
 Défis relevés & Solutions
Le projet a également couvert des aspects critiques de l'administration système, notamment :

•	Troubleshooting de Boot : Résolution des erreurs d'amorçage via la reconfiguration de la priorité des périphériques dans le BIOS virtuel.
•	Sécurité des privilèges : Configuration fine des groupes Linux (libvirt, kvm) pour permettre une administration sécurisée sans privilèges root permanents.
