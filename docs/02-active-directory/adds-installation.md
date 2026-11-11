# Installation et configuration d'Active Directory (AD DS)

## 1. Objectif

Ce document décrit la procédure d'installation du rôle **Active Directory Domain Services (AD DS)** sur le serveur `SRV-DC01`, ainsi que la promotion de ce serveur en tant que contrôleur de domaine pour le domaine `lab.local`.

## 2. Contexte technique

L'installation a été réalisée sur la machine virtuelle `SRV-DC01` (Windows Server). Préalablement à l'installation, le serveur a été configuré avec une adresse IP statique (`192.168.56.10`) et son service DNS a été pointé vers lui-même (`127.0.0.1`), condition indispensable pour le bon fonctionnement du futur domaine.

## 3. Configuration réalisée

*   **Rôle installé** : Active Directory Domain Services (AD DS).
*   **Nom du domaine** : `lab.local`.
*   **Type de déploiement** : Création d'une nouvelle forêt.
*   **Niveau fonctionnel** : Windows Server (le plus élevé disponible).
*   **Serveur DNS** : Installé et configuré automatiquement lors de la promotion (intégré à l'AD).
*   **Base de données et journaux** : Emplacements par défaut.

## 4. Procédure

1. Ouverture du **Gestionnaire de serveur**.
2. Ajout du rôle **Services de domaine Active Directory**.
3. Lancement de l'assistant de promotion du serveur en contrôleur de domaine.
4. Sélection de l'option "Ajouter une nouvelle forêt" et saisie du nom de domaine racine : `lab.local`.
5. Définition du mot de passe du mode de restauration des services d'annuaire (DSRM).
6. Vérification des prérequis et lancement de l'installation.
7. Redémarrage automatique du serveur une fois l'installation terminée.

## 5. Vérifications

Après le redémarrage, les vérifications suivantes ont été effectuées :
*   Le serveur est bien authentifié sur le domaine `lab.local`.
*   L'outil **Utilisateurs et ordinateurs Active Directory** est fonctionnel.
*   La commande PowerShell `Get-ADDomain` retourne les informations correctes du domaine.
*   Le service DNS répond correctement.

## 6. Captures d'écran

**Figure 1 — Configuration IP du serveur `SRV-DC01`**
![Configuration IP](../../screenshots/02-active-directory/srv-dc01-ip-configuration.png)

**Figure 2 — État du déploiement AD DS dans le Gestionnaire de serveur**
![Rôle AD DS](../../screenshots/02-active-directory/adds-server-role.png)

**Figure 3 — Assistant de configuration du déploiement**
![Configuration du déploiement](../../screenshots/02-active-directory/adds-deployment-configuration.png)

**Figure 4 — Confirmation de la création du domaine `lab.local`**
![Domaine Active Directory](../../screenshots/02-active-directory/active-directory-domain.png)

**Figure 5 — État du contrôleur de domaine**
![Statut DC](../../screenshots/02-active-directory/domain-controller-status.png)

## 7. Résultat obtenu

Le serveur `SRV-DC01` est promu avec succès en tant que contrôleur de domaine. La forêt et le domaine `lab.local` sont opérationnels. L'annuaire est prêt à recevoir la structure organisationnelle et les comptes utilisateurs.

## 8. Difficultés rencontrées

Aucune difficulté majeure lors de l'installation du rôle. Cependant, il a été nécessaire de s'assurer que le DNS pointait bien vers le serveur lui-même avant la promotion pour éviter des erreurs de résolution.

## 9. Conclusion

Le déploiement d'AD DS est une étape fondamentale. Il permet de centraliser la gestion des identités et de fournir la base de l'infrastructure de sécurité du laboratoire TechCorp.