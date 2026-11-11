# Gestion des utilisateurs

## 1. Objectif

Cette étape consiste à créer les comptes utilisateur de l'entreprise TechCorp et à les rattacher aux bonnes unités d'organisation. Le but est de représenter un environnement de production réaliste au sein de l'annuaire Active Directory, tout en appliquant une logique de gestion cohérente pour les identités et les accès.

## 2. Contexte technique

Après la mise en place du domaine et la définition de la hiérarchie des OU, il est nécessaire d'ajouter les comptes correspondants aux services de l'organisation. Chaque compte doit être associé à une OU dédiée afin de faciliter la gestion administrative et la mise en oeuvre des politiques de sécurité.

## 3. Configuration réalisée

Les comptes suivants ont été créés dans le domaine :

| Nom complet | Identifiant (Login) | OU de rattachement | Service |
| :--- | :--- | :--- | :--- |
| Lucas Bernard | `lbernard` | `IT` | IT |
| Sarah Martin | `smartin` | `Marketing` | Marketing |
| Jean Dupont | `jdupont` | `RH` | RH |
| Thomas Moreau | `tmoreau` | `Comptabilité` | Comptabilité |

Chaque compte est associé à son service fonctionnel respectif. Cela permet d'organiser l'annuaire selon l'organisation réelle de l'entreprise et de préparer les tests d'autorisations par groupe.

## 4. Justification de la méthode

L'administration d'un domaine Active Directory repose sur l'identité. Il est essentiel de donner à chaque utilisateur :

- un compte unique,
- un identifiant explicite,
- un rattachement logique à un service,
- un mot de passe initial correctement géré,
- un statut actif adapté à la situation.

Cette logique permet d'éviter les comptes inutilisés, les erreurs d'organisation et les difficultés de gestion lors des audits de sécurité.

## 5. Procédure de création (exemple : Thomas Moreau)

1. Ouvrir la console **Utilisateurs et ordinateurs Active Directory**.
2. Sélectionner l'OU `Comptabilité`.
3. Cliquer avec le bouton droit > **Nouveau** > **Utilisateur**.
4. Saisir les informations du compte :
   - prénom : `Thomas`
   - nom : `Moreau`
   - nom d'ouverture de session : `tmoreau`
5. Définir un mot de passe initial conforme à la politique du laboratoire.
6. Valider la création du compte.
7. Vérifier le statut du compte dans les propriétés, car il peut être initialement désactivé.
8. Dans l'onglet **Compte**, décocher l'option **Le compte est désactivé** si nécessaire.

Cette étape doit être répétée pour chaque nouvel employé, en suivant les mêmes bonnes pratiques de gestion des identités.

## 6. Captures d'écran

**Figure 1 — Création du compte utilisateur Thomas Moreau**
![Création du compte utilisateur](../../screenshots/03-identity-management/user-creation-wizard.png)

**Figure 2 — Propriétés du compte Thomas Moreau**
![Compte Thomas Moreau](../../screenshots/03-identity-management/user-thomas-moreau.png)

## 7. Résultat obtenu

Les comptes utilisateurs de l'environnement sont désormais créés et correctement rattachés à leur service respectif. Les identités de l'entreprise sont centralisées dans Active Directory, ce qui permet de passer à la phase suivante de la mise en place des groupes, des autorisations et des contrôles d'accès.

## 8. Conclusion

La gestion des utilisateurs est une étape fondamentale dans la préparation d'un environnement AD sécurisé. Elle permet non seulement d'identifier les employés, mais aussi de structurer les services, d'optimiser les autorisations et d'aligner l'annuaire sur l'organisation réelle de l'entreprise.