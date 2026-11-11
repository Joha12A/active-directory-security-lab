# Constats de sécurité (Findings)

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

## 1. Objectif

Séparer les vulnérabilités confirmées des observations opérationnelles ou des écarts de preuve. Une observation ne reçoit pas de sévérité de vulnérabilité sans analyse d’impact et validation reproductible.

## 2. Vulnérabilités confirmées

**Aucune vulnérabilité confirmée à ce stade.** L’audit actif n’est pas documenté comme terminé ; l’absence de constat ne signifie pas que le domaine est exempt de vulnérabilités.

## 3. Observations à investiguer

| ID | Type | Observation vérifiable | Suite recommandée | Statut |
|---|---|---|---|---|
| OBS-01 | Échec de contrôle opérationnel | La capture `dcdiag` montre que le test initial de connectivité échoue en raison d’un nom GUID sous `_msdcs.lab.local` non résolu. | Rejouer `dcdiag /test:dns /v`, vérifier les enregistrements de localisation AD et comparer les adresses publiées avec les interfaces du contrôleur. | Ouvert — résultat à reproduire |
| OBS-02 | Écart de configuration DNS à vérifier | Une capture DNS montre `SRV-DC01` associé à `192.168.56.10` et `10.0.3.15`. | Déterminer si la seconde adresse correspond à l’interface NAT et si elle doit être publiée pour les clients du réseau interne. Ne pas modifier sans validation et plan de retour arrière. | Ouvert |
| OBS-03 | Écart entre notes et captures | Les captures d’objet utilisateur/groupe indiquent `lab.local/Users`, tandis que les notes annoncent des OU de service. | Vérifier les emplacements réels et déplacer les objets uniquement après validation de la structure et des GPO liées. | Ouvert |
| OBS-04 | Écart entre notes et ACL visible | La capture NTFS montre `Contrôle total` pour `GRP_IT` et une entrée `Utilisateurs`. | Examiner les ACL effectives et réduire les droits si l’accès observé dépasse le besoin métier. | Ouvert |

Ces observations ne sont pas classées comme vulnérabilités et ne reçoivent pas de sévérité tant que leur impact n’a pas été vérifié.

## 4. Statut

**En cours de constitution.** Compléter ce registre après l’audit autorisé, avec des preuves datées et des résultats reproductibles. Ne pas ajouter de CVE sans identifier précisément un produit/version concerné et confirmer l’applicabilité.

[Méthodologie](audit-methodology.md) · [Résultats](audit-results.md) · [Plan de remédiation](../08-remediation/remediation-plan.md) · [Retour à l’index](../README.md)