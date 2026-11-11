# Organisation des unités d'organisation (OU)

## 1. Objectif

L'objectif de cette étape est de structurer le domaine Active Directory de TechCorp de manière logique et exploitable. La création d'unités d'organisation (OU) permet de séparer les différents services de l'entreprise, de mieux administrer les comptes et de préparer l'application de politiques de sécurité et de gestion centralisées.

## 2. Contexte technique

Le domaine `lab.local` a été initialement créé dans le contrôleur de domaine `SRV-DC01`. Pour simuler un environnement d'entreprise réaliste, il a été nécessaire de définir une hiérarchie de gestion basée sur les entités fonctionnelles de l'organisation.

Cette approche permet notamment de :

- séparer les comptes par service,
- mieux contrôler les droits d'administration,
- appliquer des GPO selon les besoins de chaque département,
- éviter une administration centralisée trop lourde et peu lisible.

## 3. Configuration réalisée

L'arborescence suivante a été mise en place dans le domaine :

- `Entreprise_Lab`
  - `IT`
  - `RH`
  - `Marketing`
  - `Comptabilité`

Cette organisation reflète les départements fonctionnels de l'entreprise et permet d'associer naturellement les comptes utilisateur, les groupes de sécurité et les systèmes à leur service d'appartenance.

## 4. Justification de l'organisation

La création des OU n'est pas seulement esthétique. Elle répond à des objectifs de sécurité et d'administration :

- un service ne doit pas manipuler les objets d'un autre service sans raison valable ;
- les comptes et groupes peuvent être regroupés selon leur contexte métier ;
- les GPO peuvent être appliquées de manière ciblée sur une OU précise ;
- l'arborescence devient un support de gouvernance pour la gestion du cycle de vie des identités.

## 5. Procédure de création (exemple : l'OU Comptabilité)

1. Ouvrir la console **Utilisateurs et ordinateurs Active Directory**.
2. Sélectionner le domaine ou l'OU parent `Entreprise_Lab`.
3. Cliquer avec le bouton droit > **Nouveau** > **Unité d'organisation**.
4. Saisir le nom `Comptabilité`.
5. Valider la création.
6. Cocher l'option de protection contre la suppression accidentelle pour éviter une suppression involontaire de l'unité.

Cette méthode permet de conserver une arborescence stable et de réduire les risques liés aux erreurs d'administration.

## 6. Captures d'écran

**Figure 1 — Structure globale des OU du domaine**
![Structure des OU](../../screenshots/03-identity-management/enterprise-lab-ou-structure.png)

## 7. Résultat obtenu

L'annuaire Active Directory dispose désormais d'une structure logique et cohérente. Les comptes, groupes et ressources peuvent être rattachés à des services métiers précis, ce qui facilite la gestion administrative et prépare le terrain pour les tests de permissions, la mise en place des groupes de sécurité et l'application des GPO.

## 8. Conclusion

Cette étape constitue la base de l'organisation de l'annuaire. Elle permet d'aligner la structure AD sur l'organigramme de l'entreprise, ce qui est indispensable pour mettre en place un modèle de sécurité robuste et facilement auditable.