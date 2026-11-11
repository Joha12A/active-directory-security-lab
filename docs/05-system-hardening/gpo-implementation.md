# Implémentation des Stratégies de Groupe (GPO)

## 1. Objectif

Centraliser et renforcer la sécurité du domaine `lab.local` en appliquant des stratégies de mot de passe et de verrouillage de compte via les Group Policy Objects (GPO).

## 2. Contexte technique

Par défaut, Windows Server applique des règles assez permissives. Dans un environnement d'entreprise, il est indispensable d'imposer des mots de passe complexes et de bloquer les comptes en cas de tentative d'attaque par force brute.

## 3. Configuration réalisée

La **Default Domain Policy** a été modifiée pour appliquer les règles suivantes à tous les ordinateurs et utilisateurs du domaine :

*   **Longueur minimale du mot de passe** : 8 caractères.
*   **Complexité du mot de passe** : Activée (majuscule, minuscule, chiffre, symbole).
*   **Seuil de verrouillage du compte** : 3 tentatives échouées.
*   **Durée du verrouillage** : 15 minutes.
*   **Réinitialisation du compteur** : 15 minutes.

## 4. Procédure

1. Ouverture de la console **Gestion des stratégies de groupe** (GPMC).
2. Édition de la **Default Domain Policy**.
3. Navigation vers : `Configuration ordinateur` > `Stratégies` > `Paramètres Windows` > `Paramètres de sécurité` > `Stratégies de compte`.
4. Configuration des stratégies de mot de passe et de verrouillage.
5. Application forcée avec la commande `gpupdate /force` sur le serveur.

## 5. Vérifications et Tests

Le test a été réalisé depuis le poste client `CLIENT-W10` :
1. Après un redémarrage (pour appliquer la GPO), une tentative de connexion avec un mauvais mot de passe a été effectuée 3 fois de suite sur le compte `lbernard`.
2. **Résultat** : Le compte a été verrouillé avec succès par le contrôleur de domaine, affichant le message "Votre compte a été désactivé. Contactez l'administrateur de votre système." (ou message équivalent de verrouillage).

## 6. Captures d'écran

**Figure 1 — Console de gestion des stratégies de groupe (GPMC)**
![Console GPMC](../../screenshots/05-system-hardening/group-policy-management-console.png)

**Figure 2 — Configuration de la politique de mot de passe**
![Politique de mot de passe](../../screenshots/05-system-hardening/password-policy-configuration.png)

**Figure 3 — Configuration de la politique de verrouillage**
![Politique de verrouillage](../../screenshots/05-system-hardening/account-lockout-policy.png)

**Figure 4 — Test de verrouillage réussi sur le client Windows 10**
![Test verrouillage](../../screenshots/05-system-hardening/account-lockout-test.png)

## 7. Résultat obtenu

Le domaine TechCorp dispose désormais d'une base de sécurité solide. Les utilisateurs sont obligés de choisir des mots de passe robustes, et les attaques par force brute sont bloquées après 3 tentatives.

## 8. Difficultés rencontrées

Lors du premier test, la GPO n'était pas immédiatement appliquée sur le client. Un redémarrage complet du poste `CLIENT-W10` a été nécessaire pour forcer la récupération des nouvelles stratégies depuis le contrôleur de domaine.

## 9. Conclusion

Les GPO sont un outil extrêmement puissant. Elles permettent d'appliquer une politique de sécurité cohérente sur des centaines de machines sans intervention manuelle. C'est un pilier de la gestion d'un Active Directory.