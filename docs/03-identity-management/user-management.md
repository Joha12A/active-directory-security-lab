# Gestion des Utilisateurs

## 1. Objectif

Créer les comptes utilisateurs des employés de TechCorp et les placer dans leurs Unités d'Organisation respectives.

## 2. Contexte technique

La structure des OU (`IT`, `RH`, `Marketing`) étant en place, les comptes utilisateurs ont été créés manuellement via l'interface graphique.

## 3. Configuration réalisée

Les comptes suivants ont été créés :

| Nom complet | Identifiant (SamAccountName) | OU de rattachement | Rôle / Service |
| :--- | :--- | :--- | :--- |
| Lucas Bernard | `lbernard` | `IT` | Administrateur Système |
| Sarah Martin | `smartin` | `Marketing` | Chargée de communication |
| Jean Dupont | `jdupont` | `RH` | Gestionnaire RH |

*Note de sécurité : Les mots de passe ont été configurés avec l'option "L'utilisateur ne peut pas changer le mot de passe" pour les besoins du lab, mais l'option "Le compte est désactivé" a été rencontrée et corrigée sur le compte de Lucas Bernard.*

## 4. Procédure

1. Clic droit sur l'OU cible (ex: `IT`) > **Nouveau** > **Utilisateur**.
2. Saisie du prénom, nom, et nom d'ouverture de session (ex: `lbernard`).
3. Définition d'un mot de passe initial.
4. Vérification de l'état du compte (déverrouillé et activé).

## 5. Vérifications

Les utilisateurs apparaissent bien dans leurs OU respectives. Le test de connexion sur le client Windows 10 a été validé pour les trois comptes.

## 6. Captures d'écran

**Figure 1 — Comptes utilisateurs dans l'OU IT**
![Utilisateurs](../../screenshots/03-identity-management/domain-user-accounts.png)

## 7. Résultat obtenu

Les employés de TechCorp disposent d'une identité numérique unique et centralisée.

## 8. Difficultés rencontrées

Lors de la création du compte `lbernard`, le compte était désactivé par défaut (indiqué par une flèche bleue sur l'icône). Le problème a été résolu en décochant l'option "Le compte est désactivé" dans l'onglet Compte de l'utilisateur.

## 9. Conclusion

La gestion des utilisateurs est le cœur de l'Active Directory. Une création rigoureuse évite les problèmes de connexion et de sécurité.