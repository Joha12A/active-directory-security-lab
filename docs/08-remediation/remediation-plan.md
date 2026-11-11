# Plan de remédiation

## 1. Objectif et périmètre

Ce document décrit le processus de traitement des constats de sécurité de l'infrastructure Active Directory TechCorp (`lab.local`). Il couvre le contrôleur de domaine `SRV-DC01`, les services DNS, les mécanismes d'authentification et les contrôles d'accès, conformément au périmètre défini dans la [méthodologie d'audit](../07-security-audit/audit-methodology.md).

Le plan d'action reste préparatoire : la méthodologie et les résultats de l'audit indiquent que les tests sont en attente de la résolution des contraintes de connectivité du laboratoire. Aucun constat confirmé n'est donc déclaré dans ce document. Les actions conditionnelles ci-dessous ne signifient pas que les vulnérabilités correspondantes ont été observées.

## 2. Priorisation

La priorité définitive de chaque action devra être établie à partir des preuves recueillies, de l'impact sur le domaine et de la facilité d'exploitation dans le contexte du laboratoire.

| Priorité | Critère de classement |
| :--- | :--- |
| P1 — Critique | Risque immédiat de compromission du domaine, d'accès administrateur non autorisé ou d'interruption majeure. Contenir puis corriger en priorité. |
| P2 — Élevée | Faiblesse pouvant conduire à une compromission significative ou à une élévation de privilèges. Corriger rapidement après validation. |
| P3 — Modérée | Configuration insuffisamment restrictive ou défaut à impact limité, nécessitant une correction planifiée. |
| P4 — Faible | Amélioration de défense en profondeur ou de documentation, sans risque immédiat identifié. |

Une priorité ne doit être attribuée qu'à un constat documenté et confirmé. Les délais de correction seront fixés par le responsable après évaluation du risque et des contraintes de disponibilité.

## 3. Plan d'action

| ID | Action | Déclencheur / périmètre | Priorité | Responsable | Échéance | Statut |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| PR-01 | Rétablir et vérifier la connectivité isolée entre la machine d'audit et le réseau `labnet`, puis consigner la configuration retenue. | Prérequis signalé dans la méthodologie d'audit. | Prérequis | Administrateur du laboratoire | Avant la reprise des tests | Bloqué — connectivité à résoudre |
| PR-02 | Réaliser les contrôles autorisés du périmètre et joindre les commandes, résultats et horodatages aux résultats d'audit. | Après levée du blocage PR-01. | Prérequis | Auditeur | Après PR-01 | En attente |
| RM-01 | Enregistrer chaque faiblesse confirmée dans le registre des constats avec preuve, système concerné, impact, priorité et recommandation. | Tout écart vérifié lors de l'audit. | Selon constat | Auditeur | À la clôture de l'analyse du constat | En attente |
| RM-02 | Corriger les paramètres de comptes, de mots de passe ou de verrouillage uniquement si les tests démontrent un écart par rapport aux exigences retenues. | Résultats des tests d'authentification et examen des stratégies appliquées. | Selon constat | Administrateur Active Directory | À définir après confirmation | Conditionnel |
| RM-03 | Réviser les autorisations de partage et NTFS, retirer les accès non justifiés et vérifier les accès avec des comptes représentatifs. | Écart confirmé entre les droits effectifs et les besoins métier. | Selon constat | Administrateur des systèmes / propriétaire des données | À définir après confirmation | Conditionnel |
| RM-04 | Corriger la configuration DNS concernée et vérifier la signature, les enregistrements DNSSEC et le comportement de validation attendu. Documenter séparément les limites de chaîne de confiance de la zone interne `lab.local`. | Échec ou mauvaise configuration DNSSEC confirmés par des tests. | Selon constat | Administrateur DNS | À définir après confirmation | Conditionnel |
| RM-05 | Restreindre ou désactiver les services et protocoles réseau identifiés comme inutiles ou insuffisamment protégés, après vérification de leur dépendance aux services AD. | Service exposé ou protocole faible confirmé dans le périmètre autorisé. | Selon constat | Administrateur systèmes / réseau | À définir après confirmation | Conditionnel |
| RM-06 | Rejouer les tests concernés après correction, consigner les résultats et faire approuver la clôture par le responsable du système. | Toute action de remédiation achevée. | Même priorité que le constat | Administrateur et auditeur | Après chaque correction | En attente |

## 4. Validation post-remédiation

Pour chaque constat, la validation doit permettre de comparer la situation avant et après correction :

1. Référencer l'identifiant du constat et la configuration ou le système concerné.
2. Consigner la correction appliquée, sa date et son responsable, sans inclure de secret dans les preuves.
3. Rejouer uniquement les contrôles autorisés qui avaient permis de confirmer le constat.
4. Vérifier qu'aucune régression ne perturbe les ouvertures de session, la résolution DNS, la localisation des contrôleurs de domaine ou les accès légitimes aux ressources.
5. Conserver les résultats, captures ou journaux nécessaires dans le dossier de preuves du laboratoire.
6. Marquer le constat comme corrigé uniquement lorsque le résultat attendu est observé et vérifiable. Sinon, le laisser ouvert, préciser le risque résiduel et définir l'action suivante.

Une résolution DNS réussie, à elle seule, ne démontre pas la validation DNSSEC. De même, la présence d'une stratégie de sécurité ne prouve pas qu'elle est effectivement appliquée aux comptes et systèmes concernés.

## 5. Critères de clôture

Le plan pourra être déclaré terminé lorsque :

- l'audit prévu a été réalisé ou ses limites ont été explicitement consignées ;
- chaque constat confirmé possède une priorité, un responsable, une échéance et une preuve ;
- les corrections ont été retestées, ou les risques résiduels ont été formellement acceptés par le responsable ;
- les résultats et le statut final ont été mis à jour dans les [résultats d'audit](../07-security-audit/audit-results.md) et les [constats de sécurité](../07-security-audit/security-findings.md).

## 6. Statut actuel

**En préparation — audit non clôturé.** La connectivité du réseau d'audit doit être rétablie avant de pouvoir établir des constats vérifiés et fixer les priorités et échéances de remédiation. Aucune vulnérabilité n'est déclarée comme confirmée dans le présent plan.
