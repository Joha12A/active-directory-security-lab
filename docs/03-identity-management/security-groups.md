# Groupes de Sécurité

## 1. Objectif

Créer des groupes de sécurité pour faciliter l'attribution des permissions (notamment sur les partages réseau) et respecter le principe du moindre privilège.

## 2. Contexte technique

Plutôt que de donner des droits directement aux utilisateurs, les droits sont attribués aux groupes. Les utilisateurs sont ensuite ajoutés à ces groupes.

## 3. Configuration réalisée

Trois groupes globaux de sécurité ont été créés :

| Nom du groupe | OU de rattachement | Membres |
| :--- | :--- | :--- |
| `GRP_IT` | `IT` | Lucas Bernard (`lbernard`) |
| `GRP_RH` | `RH` | Jean Dupont (`jdupont`) |
| `GRP_Marketing` | `Marketing` | Sarah Martin (`smartin`) |

## 4. Procédure

1. Clic droit sur l'OU cible > **Nouveau** > **Groupe**.
2. Nom du groupe (ex: `GRP_IT`), portée **Globale**, type **Sécurité**.
3. Double-clic sur le groupe créé > Onglet **Membres** > **Ajouter**.
4. Saisie du nom de l'utilisateur et validation.

## 5. Vérifications

Les membres sont bien listés dans les propriétés de chaque groupe.

## 6. Captures d'écran

**Figure 1 — Liste des groupes de sécurité**
![Groupes](../../screenshots/03-identity-management/security-groups-overview.png)

**Figure 2 — Membres du groupe GRP_IT**
![Membres GRP_IT](../../screenshots/03-identity-management/group-membership-it.png)

## 7. Résultat obtenu

L'administration des droits est maintenant simplifiée. Pour donner accès à un nouvel employé de l'IT à un dossier, il suffira de l'ajouter au groupe `GRP_IT`.

## 8. Difficultés rencontrées

Aucune.

## 9. Conclusion

L'utilisation de groupes de sécurité est une bonne pratique incontournable en entreprise. Elle rend l'infrastructure scalable et sécurisée.