# Groupes de sécurité

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

## 1. Objectif

La gestion des autorisations dans Active Directory repose fortement sur les groupes de sécurité. L'objectif de cette étape est de regrouper les utilisateurs selon leur service ou leur rôle afin de simplifier l'attribution des droits et d'appliquer le principe du moindre privilège.

## 2. Contexte technique

Une fois les unités d'organisation créées, il est nécessaire d'associer les utilisateurs à des groupes de sécurité cohérents. Cela permet ensuite de gérer les autorisations sur les ressources, les dossiers partagés, les services ou les objets AD sans avoir à configurer chaque droit individuellement.

## 3. Configuration réalisée

Les groupes suivants sont mentionnés dans les notes du laboratoire :

| Nom du groupe | OU de rattachement | Membres |
| :--- | :--- | :--- |
| `GRP_IT` | `IT` | Lucas Bernard (`lbernard`) |
| `GRP_RH` | `RH` | Jean Dupont (`jdupont`) |
| `GRP_Marketing` | `Marketing` | Sarah Martin (`smartin`) |
| `GRP_COMPTA` | `Comptabilité` | Thomas Moreau (`tmoreau`) |

Cette liste reflète les rattachements annoncés dans les notes. Les captures disponibles confirment la création de `GRP_COMPTA` en groupe global de sécurité et l’ajout de `tmoreau`, mais montrent `lab.local/Users` comme emplacement du groupe et de Thomas Moreau. Elles ne confirment donc pas leur placement dans l’OU `Comptabilité`, ni la création des autres groupes de la liste.

## 4. Justification du choix

Les groupes de sécurité sont un mécanisme fondamental en AD. Ils permettent de :

- centraliser la gestion des accès ;
- réduire les erreurs humaines liées aux permissions individuelles ;
- faciliter les changements de responsabilités au sein de l'entreprise ;
- sécuriser les ressources en limitant les privilèges au strict nécessaire.

Un groupe regroupe des comptes et peut être utilisé comme principal de sécurité auquel des autorisations sont attribuées. Il ne remplace ni les OU ni les règles de délégation.

## 5. Procédure de création (exemple : `GRP_COMPTA`)

1. Ouvrir la console **Utilisateurs et ordinateurs Active Directory**.
2. Sélectionner l’OU `Comptabilité` avant la création. La capture actuelle montre le conteneur par défaut `Users` ; le placement de l’objet doit être contrôlé.
3. Cliquer avec le bouton droit > **Nouveau** > **Groupe**.
4. Saisir le nom du groupe : `GRP_COMPTA`.
5. Définir la portée sur **Globale** et le type sur **Sécurité**.
6. Valider la création.
7. Ouvrir les propriétés du groupe.
8. Aller dans l'onglet **Membres** puis cliquer sur **Ajouter**.
9. Ajouter le compte `tmoreau`.
10. Valider la modification.

Cette procédure est reproductible pour chaque équipe ou service de l'entreprise, ce qui permet de standardiser la sécurité dans l'annuaire.

## 6. Captures d'écran

**Figure 1 — Création du groupe global de sécurité ; le chemin affiché est `lab.local/Users`**
![Création du groupe GRP_COMPTA dans le conteneur Users](../../screenshots/03-identity-management/group-creation-wizard.png)

**Figure 2 — Membre affiché dans le groupe ; son emplacement indiqué est `lab.local/Users`**
![Membres du groupe GRP_COMPTA](../../screenshots/03-identity-management/group-membership-compta.png)

## 7. Résultat obtenu

Les captures prouvent que `GRP_COMPTA` et son membre `tmoreau` existent. Leur emplacement visible dans `Users` diffère de l’OU annoncée ; le placement doit être corrigé ou expliqué avant de conclure que l’organisation est conforme. L’appartenance à un groupe ne prouve pas, à elle seule, l’accès effectif à une ressource.

## 8. Conclusion

La mise en place de groupes de sécurité est une étape clé dans la gestion des autorisations AD. Leur portée, leurs membres, leur emplacement et leurs droits effectifs doivent être vérifiés ensemble.

[Utilisateurs](user-management.md) · [Tests d’accès](../04-access-control/permissions-testing.md) · [Retour à l’index](../README.md)