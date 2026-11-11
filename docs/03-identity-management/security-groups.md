# Groupes de Sécurité

## 1. Objectif

Créer des groupes de sécurité pour faciliter l'attribution des permissions et respecter le principe du moindre privilège.

## 2. Configuration réalisée

| Nom du groupe | OU de rattachement | Membres |
| :--- | :--- | :--- |
| `GRP_IT` | `IT` | Lucas Bernard (`lbernard`) |
| `GRP_RH` | `RH` | Jean Dupont (`jdupont`) |
| `GRP_Marketing` | `Marketing` | Sarah Martin (`smartin`) |
| `GRP_Compta` | `Comptabilité` | Thomas Moreau (`tmoreau`) |

## 3. Procédure (Exemple avec le groupe GRP_Compta)

1. Clic droit sur l'OU `Comptabilité` > **Nouveau** > **Groupe**.
2. Nom du groupe : `GRP_Compta`, portée **Globale**, type **Sécurité**.
3. Double-clic sur le groupe > Onglet **Membres** > **Ajouter**.
4. Saisie du nom `tmoreau` et validation.

## 4. Captures d'écran

**Figure 1 — Liste des groupes de sécurité**
![Groupes](../../screenshots/03-identity-management/security-groups-overview.png)

**Figure 2 — Ajout d'un membre dans le groupe Comptabilité**
![Membres GRP_Compta](../../screenshots/03-identity-management/group-membership-compta.png)

## 5. Résultat obtenu

L'administration des droits est simplifiée. La création de l'utilisateur Thomas et son ajout au groupe Compta illustrent la procédure standard de "Onboarding" d'un nouvel employé.