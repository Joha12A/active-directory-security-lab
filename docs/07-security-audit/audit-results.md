# Résultats de l'audit de sécurité

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

## 1. Objectif

Consigner les preuves disponibles et les limites des vérifications relatives au domaine `lab.local`. Ce document ne remplace pas les exports bruts des outils ; aucun résultat de scan réseau n’est actuellement joint.

## 2. Éléments observés

| Contrôle / preuve | Observation | Interprétation et suite |
|---|---|---|
| `dcdiag`, capture [domain-controller-status.png](../../screenshots/02-active-directory/domain-controller-status.png) | Le test initial de connectivité échoue ; un nom GUID sous `_msdcs.lab.local` ne peut pas être résolu. | Échec opérationnel observé, pas une vulnérabilité confirmée. Rejouer le diagnostic et examiner les enregistrements DNS et l’état des interfaces. |
| Enregistrements DNS, capture [dnssec-signed-records.png](../../screenshots/06-dns-security/dnssec-signed-records.png) | `SRV-DC01` est visible avec `192.168.56.10` et `10.0.3.15`; des `RRSIG`/`NSEC3` apparaissent dans la zone. | Vérifier l’adresse retournée aux clients et corréler l’adresse supplémentaire avec les interfaces. La présence d’enregistrements signés ne prouve pas une validation complète par les clients. |
| Stratégies de compte et verrouillage | Les captures montrent les paramètres de mot de passe/verrouillage et un compte verrouillé. | Les paramètres résultants et leur portée doivent être vérifiés ; la capture indique un intervalle de 14 minutes pour la réinitialisation du compteur. Voir la [documentation GPO](../05-system-hardening/gpo-implementation.md). |
| Partage `IT` | Des captures montrent un accès refusé pour Sarah et un accès réussi pour Lucas. | Résultats limités aux deux comptes testés ; la revue des ACL effectives reste à terminer. Voir les [tests d’accès](../04-access-control/permissions-testing.md). |

## 3. Contrôles non documentés comme exécutés

- Inventaire réseau et de ports avec Nmap : aucun résultat brut dans le dépôt.
- Audit complet de l’authentification et des protocoles : aucun résultat brut dans le dépôt.
- Validation DNSSEC par un résolveur client et chaîne de confiance : non démontrées.
- Vérification complète des stratégies résultantes et des ACL effectives : à réaliser.

Les captures d’écran ne comportent pas toutes un fichier de sortie ou un horodatage associé. Les observations sont donc limitées à leur contenu visible et ne constituent pas une preuve de l’état actuel de l’infrastructure.

## 4. Conclusion provisoire

**Audit incomplet.** L’échec DNS/DC locator est observé et requiert une investigation. Aucune vulnérabilité n’est confirmée dans ce document ; aucune CVE n’est attribuée. Les résultats d’un éventuel audit actif devront être ajoutés avec la date, la cible autorisée, l’outil et sa version, la commande, la sortie pertinente et les limites.

[Méthodologie](audit-methodology.md) · [Constats](security-findings.md) · [Plan de remédiation](../08-remediation/remediation-plan.md) · [Retour à l’index](../README.md)