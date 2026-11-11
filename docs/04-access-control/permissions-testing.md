# Validation des permissions d'accès

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

## 1. Objectif

Le but de cette validation est de confirmer que les droits d'accès au partage réseau `\\SRV-DC01\IT` sont correctement appliqués et respectent le principe du moindre privilège. La vérification doit démontrer que :

- les utilisateurs du service informatique sont autorisés à accéder au dossier partagé ;
- les utilisateurs d'autres départements n'ont pas accès à cette ressource ;
- la logique de contrôle d'accès centralisée dans Active Directory est bien effective.

## 2. Contexte technique

L'environnement de test est composé du contrôleur de domaine `SRV-DC01` et du poste client `CLIENT-W10`, appartenant au domaine `lab.local`. Les tests sont exécutés à partir d'un compte utilisateur standard, ce qui permet de reproduire un scénario d'accès réel dans un environnement d'entreprise.

Les deux comptes utilisés pour la validation sont :

- `lab\smartin` — Sarah Martin, membre du service Marketing ;
- `lab\lbernard` — Lucas Bernard, membre du service IT.

## 3. Configuration visible et résultat attendu

Les captures de configuration montrent :

- `GRP_IT` dans la liste des autorisations du partage SMB ;
- `GRP_IT` avec `Contrôle total` dans l’ACL NTFS, ainsi que d’autres entrées, dont `Utilisateurs`.

Le résultat attendu des tests est un accès pour Lucas (IT) et un refus pour Sarah (Marketing). L’ACL NTFS affichée doit être examinée pour déterminer les droits effectifs ; la capture ne permet pas de dire que `GRP_IT` est le seul principal autorisé au niveau du système de fichiers.

## 4. Procédure de test

1. Déconnecter la session active sur `CLIENT-W10`.
2. Se connecter avec le compte `lab\smartin`.
3. Ouvrir l'explorateur Windows.
4. Tenter d'accéder au chemin UNC `\\SRV-DC01\IT`.
5. Observer et noter le comportement système.
6. Se déconnecter puis se reconnecter avec le compte `lab\lbernard`.
7. Répéter la tentative d'accès au même chemin UNC.
8. Vérifier si l'utilisateur peut ouvrir le dossier et créer un fichier de test.

## 5. Résultats observés

| Utilisateur | Service | Résultat attendu | Résultat observé | Conclusion |
| :--- | :--- | :--- | :--- | :--- |
| `lab\smartin` | Marketing | Refus d'accès | Accès refusé | Correct |
| `lab\lbernard` | IT | Accès autorisé | Accès autorisé | Correct |

### Analyse détaillée

- La capture de Sarah Martin montre un refus d’accès à `\\SRV-DC01\IT`.
- La capture de Lucas Bernard montre l’ouverture du partage et un fichier de test. Ces observations confirment les résultats visibles à la date des captures, mais ne permettent pas d’isoler à elles seules la couche qui a refusé l’accès ni de déduire tous les droits effectifs.
- La capture NTFS contient d’autres entrées que `GRP_IT`, dont `Utilisateurs`. Voir la [configuration du partage](shared-folders.md) et contrôler l’accès effectif avant de conclure que l’ACL NTFS est minimale.

## 6. Captures d'écran

**Figure 1 — Accès autorisé pour Lucas Bernard (service IT)**
![Accès autorisé pour Lucas](../../screenshots/04-access-control/lucas-access-granted.png)

**Figure 2 — Accès refusé pour Sarah Martin (service Marketing)**
![Accès refusé pour Sarah](../../screenshots/04-access-control/sarah-access-denied.png)

## 7. Interprétation de la mise en œuvre

Ces captures documentent un résultat positif pour Lucas et un refus pour Sarah lors des essais. Elles ne constituent pas une revue exhaustive des ACL, des groupes imbriqués ou des droits d’autres utilisateurs.

Ce type de validation est particulièrement important en environnement de production, car il permet de confirmer que les permissions ne dépendent pas seulement de la structure AD, mais qu'elles sont effectivement respectées lors des accès réseau.

## 8. Résultat obtenu

Les résultats visibles sont cohérents avec le cloisonnement attendu pour les deux comptes testés. La conformité générale du partage reste à confirmer après revue des ACL effectives et des groupes de chaque compte.

## 9. Difficultés rencontrées

Une difficulté de cache d'authentification est rapportée pendant les premiers essais, suivie d’un redémarrage du client. La cause n’est pas démontrée par les preuves conservées ; ne pas l’attribuer spécifiquement à Kerberos sans journaux ou sortie de diagnostic.

## 10. Conclusion

Cette validation confirme la pertinence de la mise en place d'Active Directory comme mécanisme centralisé de gestion des droits. Les groupes de sécurité, associés aux permissions NTFS et SMB, permettent d'adopter un modèle d'accès robuste, lisible et facilement auditable, conforme aux bonnes pratiques de sécurité informatique.

[Configuration du partage](shared-folders.md) · [Retour à l’index](../README.md)