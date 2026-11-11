# Tests de validation des permissions

## 1. Objectif

Valider le bon fonctionnement des permissions configurées sur le partage réseau `\\SRV-DC01\IT`. L'objectif est de prouver que le cloisonnement des données fonctionne (le service IT a accès, les autres services sont bloqués).

## 2. Contexte technique

Les tests sont réalisés depuis le poste client `CLIENT-W10` (joint au domaine `lab.local`). Deux utilisateurs avec des profils différents sont utilisés : Lucas Bernard (IT) et Sarah Martin (Marketing).

## 3. Procédure de test

1. Déconnexion de la session en cours sur `CLIENT-W10`.
2. Connexion avec le compte `lab\smartin` (Sarah).
3. Ouverture de l'explorateur de fichiers et saisie du chemin `\\SRV-DC01\IT`.
4. Observation du résultat.
5. Déconnexion, puis connexion avec le compte `lab\lbernard` (Lucas).
6. Nouvelle tentative d'accès au chemin `\\SRV-DC01\IT`.
7. Création d'un fichier texte de test pour valider les droits d'écriture.

## 4. Résultats des tests

*   **Sarah Martin (Marketing)** : Accès refusé. Le message d'erreur Windows indique que l'utilisateur n'a pas les autorisations nécessaires. ✅
*   **Lucas Bernard (IT)** : Accès autorisé. Le dossier s'ouvre et la création d'un fichier texte est un succès. ✅

## 5. Captures d'écran

**Figure 1 — Accès autorisé pour Lucas (IT)**
![Accès Lucas](../../screenshots/04-access-control/lucas-access-granted.png)

**Figure 2 — Accès refusé pour Sarah (Marketing)**
![Accès refusé Sarah](../../screenshots/04-access-control/sarah-access-denied.png)

## 6. Résultat obtenu

Le cloisonnement est parfaitement fonctionnel. Les données du service informatique sont protégées contre les accès non autorisés, conformément aux règles de sécurité définies dans le scénario.

## 7. Difficultés rencontrées

Lors des tests, un problème de cache d'authentification sur le poste client a été rencontré. Il a été résolu en redémarrant le client Windows 10 pour forcer la mise à jour des jetons Kerberos.

## 8. Conclusion

Ces tests valident la puissance de l'Active Directory : la gestion centralisée des identités permet de sécuriser l'accès aux ressources réseau de manière simple et fiable.