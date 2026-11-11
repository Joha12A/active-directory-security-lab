# Méthodologie d'audit de sécurité

[Accueil du laboratoire](../README.md) · [Accueil du dépôt](../../README.md)

## 1. Objectif

Définir une démarche autorisée, limitée et reproductible pour examiner l’infrastructure TechCorp depuis l’environnement Kali Linux du laboratoire. Aucun test actif n’est considéré comme effectué tant que ses résultats ne sont pas consignés.

## 2. Périmètre de l'audit

Le périmètre prévu, une fois la connectivité validée, comprend :

- **Contrôleur de domaine `SRV-DC01` :** inventaire autorisé des services et vérification de leur nécessité.
- **DNS :** état des zones, enregistrements et paramètres DNSSEC ; contrôle des erreurs de résolution observées.
- **Authentification :** revue des stratégies de compte et vérification non destructive de leur application.
- **Partages :** revue des permissions SMB et NTFS et tests d’accès avec des comptes de laboratoire dédiés.

Les contrôles susceptibles de verrouiller un compte, modifier la configuration, perturber un service ou collecter des identifiants sont exclus tant qu’ils ne disposent pas d’une autorisation explicite, d’un compte de test, d’une fenêtre et d’un plan de retour arrière.

## 3. Outils prévus

*   **Nmap** : inventaire de services uniquement sur les adresses du laboratoire explicitement autorisées, avec une intensité adaptée.
*   **Outils Windows intégrés** : contrôles de configuration, DNS, GPO et AD depuis le système concerné.
*   **Consultation LDAP** : uniquement des requêtes autorisées, ciblées et en lecture seule.

Aucun de ces outils n’est présenté comme ayant été exécuté dans le cadre de l’audit documenté ici.

## 4. Statut

**En attente — aucun audit actif complet n’est documenté.**

Les captures VirtualBox montrent un réseau interne `labnet` et une interface NAT, pas un réseau Host-Only. L’accès de l’hôte Kali au réseau interne n’est pas démontré ; ne pas modifier la topologie avant d’avoir établi le chemin d’administration autorisé et préservé l’isolation du laboratoire. Par ailleurs, une capture `dcdiag` sur le contrôleur montre un échec DNS/DC locator à investiguer avant les tests.

[Résultats d’audit](audit-results.md) · [Constats](security-findings.md) · [Retour à l’index](../README.md)