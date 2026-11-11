# Organisation des Unités d'Organisation (OU)

## 1. Objectif

Structurer l'annuaire Active Directory de l'entreprise TechCorp en créant une hiérarchie d'Unités d'Organisation (OU). Cette structure permet de déléguer l'administration et d'appliquer des stratégies de groupe (GPO) de manière ciblée.

## 2. Contexte technique

Le domaine `lab.local` a été créé. Afin de refléter l'organisation de l'entreprise, une structure d'annuaire a été définie.

## 3. Configuration réalisée

L'arborescence suivante a été mise en place :

*   **OU Principale** : `Entreprise_Lab`
    *   **Sous-OU** : `IT` (Informatique)
    *   **Sous-OU** : `RH` (Ressources Humaines)
    *   **Sous-OU** : `Marketing`

## 4. Procédure

1. Ouverture de la console **Utilisateurs et ordinateurs Active Directory**.
2. Clic droit sur le domaine `lab.local` > **Nouveau** > **Unité d'organisation**.
3. Création de l'OU principale `Entreprise_Lab` (avec protection contre la suppression accidentelle).
4. Clic droit sur l'OU `Entreprise_Lab` > **Nouveau** > **Unité d'organisation**.
5. Création des sous-OU `IT`, `RH` et `Marketing`.

## 5. Vérifications

L'arborescence a été vérifiée visuellement dans la console d'administration. Les OU sont prêtes à recevoir les utilisateurs et les groupes.

## 6. Captures d'écran

**Figure 1 — Structure des OU dans Active Directory**
![Structure des OU](../../screenshots/03-identity-management/enterprise-lab-ou-structure.png)

## 7. Résultat obtenu

L'annuaire est maintenant structuré de manière logique, ce qui facilitera la gestion des futurs employés de TechCorp.

## 8. Difficultés rencontrées

Aucune difficulté particulière. Il est important de ne pas déplacer les conteneurs par défaut (comme `Users` ou `Computers`) mais de créer ses propres OU.

## 9. Conclusion

La création des OU est la première étape d'une bonne hygiène Active Directory. Elle permet de garder un annuaire propre et évolutif.