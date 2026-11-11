# Architecture de l'infrastructure

## 1. Objectif

Ce document a pour but de décrire l'architecture technique du laboratoire Active Directory mis en place pour l'entreprise fictive **TechCorp**. Il détaille l'environnement de virtualisation, la topologie réseau et la répartition des rôles sur les différentes machines virtuelles.

## 2. Contexte technique

Le laboratoire est hébergé sur une machine physique sous **Kali Linux**, utilisant **Oracle VirtualBox** comme hyperviseur. L'infrastructure repose sur un réseau isolé, garantissant que les tests de sécurité et de configuration restent confinés à l'environnement de laboratoire.

## 3. Configuration réalisée

L'infrastructure se compose de trois machines virtuelles principales :

| Nom de la VM | Système d'exploitation | Rôle principal | Adresse IP |
| :--- | :--- | :--- | :--- |
| `SRV-DC01` | Windows Server | Contrôleur de domaine (AD DS) et DNS | `192.168.56.10` |
| `CLIENT-W10` | Windows 10 | Poste client joint au domaine | `192.168.56.20` |
| `Ubuntu-Server` | Ubuntu Server | Serveur Linux (intégration future) | `192.168.56.30` |

*(Note : La machine hôte Kali Linux est également utilisée pour l'administration et les futurs audits de sécurité).*

## 4. Procédure (Vue d'ensemble)

1. Création des machines virtuelles dans VirtualBox.
2. Configuration de deux adaptateurs réseau par VM (un pour le réseau interne `labnet`, un pour le NAT).
3. Attribution des adresses IP statiques sur le réseau `192.168.56.0/24`.
4. Configuration du service DNS sur `SRV-DC01` (pointant vers lui-même).

## 5. Vérifications

La connectivité réseau a été vérifiée via des requêtes `ping` entre les différentes machines. La machine cliente `CLIENT-W10` parvient à résoudre le nom de domaine `lab.local` et à contacter le contrôleur de domaine.

## 6. Captures d'écran

**Figure 1 — Vue d'ensemble des machines virtuelles dans VirtualBox**
![Vue d'ensemble VirtualBox](../../screenshots/01-architecture/virtualbox-vm-overview.png)

**Figure 2 — Configuration réseau d'une machine virtuelle**
![Configuration réseau VirtualBox](../../screenshots/01-architecture/virtualbox-network-settings.png)

**Figure 3 — Informations système du serveur `SRV-DC01`**
![Informations système SRV-DC01](../../screenshots/01-architecture/srv-dc01-system-information.png)

**Figure 4 — Informations système du client `CLIENT-W10`**
![Informations système CLIENT-W10](../../screenshots/01-architecture/client-w10-system-information.png)

## 7. Résultat obtenu

L'infrastructure virtuelle est opérationnelle. Les trois machines communiquent correctement sur le réseau interne `labnet`, et l'accès à Internet est maintenu via les cartes NAT, permettant les mises à jour système.

## 8. Difficultés rencontrées

Lors de la configuration initiale, un problème d'ordre d'amorçage a été rencontré sur la VM Windows 10 (l'ISO d'installation se relançait en boucle). Ce problème a été résolu en modifiant l'ordre de démarrage dans VirtualBox et en retirant le lecteur optique virtuel après l'installation.

## 9. Conclusion

Cette première phase a permis de poser les fondations d'un environnement Active Directory isolé et fonctionnel. La topologie réseau est prête à accueillir les services de domaine et les tests de sécurité.